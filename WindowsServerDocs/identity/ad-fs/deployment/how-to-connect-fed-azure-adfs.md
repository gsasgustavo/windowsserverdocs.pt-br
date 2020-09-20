---
title: Serviços de Federação do Active Directory no Azure | Microsoft Docs
description: Neste documento, você aprenderá a implantar o AD FS no Azure para obter alta disponibilidade.
author: billmath
manager: mtillman
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.topic: get-started-article
ms.date: 10/28/2018
ms.author: billmath
ms.openlocfilehash: a077a76814cc5ed99d4a1c0eb6c23584b22363e1
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766749"
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Implantando os Serviços de Federação do Active Directory no Azure
O AD FS fornece recursos simplificados e seguros de federação de identidade e de logon único (SSO) da Web. A federação com o Azure AD ou o O365 habilita os usuários a se autenticar usando credenciais locais e acessar todos os recursos na nuvem. Como resultado, é importante ter uma infraestrutura altamente disponível do AD FS para garantir o acesso a recursos locais e na nuvem. Implantar o AD FS no Azure pode ajudar a atingir a alta disponibilidade necessária com esforço mínimo.
Há várias vantagens na implantação do AD FS no Azure. Algumas delas são listadas abaixo:

* **Alta disponibilidade** -com a tecnologia de Conjuntos de Disponibilidade do Azure, você garante uma infraestrutura altamente disponível.
* **Fácil de dimensionar** – precisa de mais desempenho? Migre facilmente para computadores mais eficientes com apenas alguns cliques no Azure
* **Redundância geográfica cruzada** – com a Redundância Geográfica do Azure, você pode ter certeza de que sua infraestrutura é altamente disponível em todo o mundo
* **Fácil de gerenciar** – com opções de gerenciamento altamente simplificado no portal do Azure, o gerenciamento da infraestrutura é muito fácil e não tem complicações

## <a name="design-principles"></a>Princípios de design
![Design de implantação](./media/how-to-connect-fed-azure-adfs/deployment.png)

O diagrama acima mostra a topologia básica recomendada para começar a implantar a infraestrutura do AD FS no Azure. Os princípios por trás dos vários componentes da topologia são listados abaixo:

* **DC/Servidores ADFS**: se tem menos de 1.000 usuários, você pode simplesmente instalar a função do AD FS nos controladores de domínio. Se não quiser que haja impacto no desempenho nos controladores de domínio ou se tiver mais de 1.000 usuários, implante o AD FS em servidores separados.
* **Servidor WAP** – é necessário implantar servidores de Proxy de Aplicativo Web para que os usuários também possam acessar o AD FS quando não estiverem na rede da empresa.
* **Rede de Perímetro**: os servidores de Proxy de Aplicativo Web serão colocados na rede de perímetro, e o acesso TCP/443 só será permitido entre a rede de perímetro e a sub-rede interna.
* **Balanceadores de Carga**: para garantir a alta disponibilidade do AD FS e dos servidores de Proxy de Aplicativo Web, é recomendável usar um balanceador de carga interno para servidores do AD FS e o Azure Load Balancer para servidores Proxy de Aplicativo Web.
* **Conjuntos de disponibilidade**: para fornecer redundância para sua implantação do AD FS, é recomendável agrupar duas ou mais máquinas virtuais em um Conjunto de Disponibilidade para cargas de trabalho semelhantes. Essa configuração garante que durante um evento de manutenção planejada ou não planejada, pelo menos uma máquina virtual esteja disponível
* **Contas de armazenamento**: é recomendável ter duas contas de armazenamento. Ter uma única conta de armazenamento pode levar à criação de um ponto único de falha e pode fazer com que a implantação fique indisponível em um cenário improvável, em que a conta de armazenamento fica inativa. Duas contas de armazenamento ajudarão a associar uma conta de armazenamento a cada linha de falha.
* **Segregação de rede**: servidores de Proxy de Aplicativo Web devem ser implantados em uma rede de perímetro separada. Você pode dividir uma rede virtual em duas sub-redes e implantar servidores de Proxy de Aplicativo Web em uma sub-rede isolada. Você pode simplesmente definir as configurações de grupo de segurança de rede para cada sub-rede e permitir somente a comunicação necessária entre as duas sub-redes. Mais detalhes são fornecidos para cada cenário de implantação abaixo

## <a name="steps-to-deploy-ad-fs-in-azure"></a>Etapas para implantar o AD FS no Azure
As etapas mencionadas nesta seção descrevem o guia para implantar no Azure a infraestrutura do AD FS descrita abaixo.

### <a name="1-deploying-the-network"></a>1. implantando a rede
Conforme descrito acima, você pode criar duas sub-redes em uma única rede virtual ou criar duas redes virtuais completamente diferentes (VNet). Este artigo abordará a implantação de uma única rede virtual e sua divisão em duas sub-redes. Essa é uma abordagem mais fácil, pois duas redes virtuais separadas exigiriam um gateway de rede virtual para rede virtual para comunicações.

**1.1 Criar rede virtual**

![Criar rede virtual](./media/how-to-connect-fed-azure-adfs/deploynetwork1.png)

No portal do Azure, selecione a rede virtual, e você poderá implantar a rede virtual e uma sub-rede imediatamente com apenas um clique. A sub-rede INT também é definida e agora está pronta para que as VMs sejam adicionadas.
A próxima etapa é adicionar outra sub-rede à rede, ou seja, a sub-rede de perímetro. Para criar a sub-rede de perímetro, simplesmente

* Selecione a rede recém-criada
* Nas propriedades, selecione sub-rede
* No painel de sub-rede, clique no botão Adicionar
* Forneça o nome da sub-rede e as informações de espaço de endereço para criar a sub-rede

![Sub-rede](./media/how-to-connect-fed-azure-adfs/deploynetwork2.png)

![Sub-rede de perímetro](./media/how-to-connect-fed-azure-adfs/deploynetwork3.png)

**1.2. Criar grupos de segurança de rede**

Um NSG (Grupo de segurança de rede) contém uma lista de regras de ACL (Lista de Controle de Acesso) que permitem ou negam o tráfego de rede para suas instâncias de VM em uma Rede Virtual. Os NSGs podem ser associados a sub-redes ou instâncias de VM individuais dentro dessa sub-rede. Quando um grupo de segurança de rede é associado a uma sub-rede, as regras de ACL se aplicam a todas as instâncias de VM nessa sub-rede.
Para os fins deste guia, vamos criar dois NSGs: um para uma rede interna e uma rede de perímetro. Eles serão rotulados como NSG_INT e NSG_DMZ, respectivamente.

![Criar NSG](./media/how-to-connect-fed-azure-adfs/creatensg1.png)

Depois que o NSG for criado, haverá 0 regra de saída e 0 regra de entrada. Quando as funções nos respectivos servidores estiverem instaladas e funcionais, as regras de entrada e saída poderão ser criadas de acordo com o nível de segurança desejado.

![Inicializar NSG](./media/how-to-connect-fed-azure-adfs/nsgint1.png)

Depois que os NSGs forem criados, associe NSG_INT à sub-rede INT e NSG_DMZ à sub-rede de perímetro. Uma captura de tela de exemplo é fornecida abaixo:

![Configurar NSG](./media/how-to-connect-fed-azure-adfs/nsgconfigure1.png)

* Clique em sub-redes para abrir o painel para sub-redes
* Selecione a sub-rede a ser associada ao NSG

Após a configuração, o painel Sub-redes deverá ser semelhante ao exemplo abaixo:

![Sub-redes após NSG](./media/how-to-connect-fed-azure-adfs/nsgconfigure2.png)

**1.3. Criar conexão local**

Será necessária uma conexão local para implantar o DC (controlador de domínio) no Azure. O Azure oferece várias opções de conectividade para conectar a infraestrutura local à infraestrutura do Azure.

* Ponto a site
* Rede virtual Site a Site
* ExpressRoute

É recomendável usar o ExpressRoute. O ExpressRoute permite criar conexões privadas entre os data centers do Azure e a infraestrutura que está em seu local ou em um ambiente de colocalização. As conexões de ExpressRoute não passam pela Internet pública. Elas oferecem mais confiabilidade e velocidade, latências menores e maior segurança do que as conexões comuns pela Internet.
Embora seja recomendável usar o ExpressRoute, você pode escolher qualquer método de conexão mais adequado à sua organização. Para saber mais sobre o ExpressRoute e as diversas opções de conectividade que o utilizam, confira [Visão geral técnica do ExpressRoute](/azure/expressroute/expressroute-introduction).

### <a name="2-create-storage-accounts"></a>2. criar contas de armazenamento
Para manter a alta disponibilidade e evitar a dependência de uma única conta de armazenamento, você pode criar duas contas de armazenamento. Divida os computadores em cada conjunto de disponibilidade em dois grupos e atribua a cada grupo uma conta de armazenamento separada.

![Criar contas de armazenamento](./media/how-to-connect-fed-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. criar conjuntos de disponibilidade
Para cada função (DC/AD FS e WAP), crie conjuntos de disponibilidade com 2 computadores cada, no mínimo. Isso ajudará a obter maior disponibilidade para cada função.
Ao criar os conjuntos de disponibilidade, é essencial decidir o seguinte:

* **Domínios de falha**: máquinas virtuais no mesmo domínio de falha compartilham a mesma fonte de energia e o mesmo comutador de rede física. É recomendável ter no mínimo 2 domínios de falha. O valor padrão é 3, e você pode mantê-lo como está para os fins desta implantação
* **Atualizar domínios**: computadores que pertencem ao mesmo domínio de atualização são reiniciados juntos durante uma atualização. Convém ter no mínimo 2 domínios de atualização. O valor padrão é 5, e você pode mantê-lo como está para os fins desta implantação

![Conjuntos de disponibilidade](./media/how-to-connect-fed-azure-adfs/availabilityset1.png)

Crie os conjuntos de disponibilidade a seguir

| Conjunto de disponibilidade | Função | Domínios de falha | Atualizar domínios |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. implantar máquinas virtuais
A próxima etapa é implantar máquinas virtuais que hospedam as diferentes funções na infraestrutura. No mínimo duas máquinas são recomendadas em cada conjunto de disponibilidade. Crie quatro máquinas virtuais para a implantação básica.

| Computador | Função | Sub-rede | Conjunto de disponibilidade | Conta de armazenamento | Endereço IP |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |Estático |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |Estático |
| contosowap1 |WAP |Rede de Perímetro |contosowapset |contososac1 |Estático |
| contosowap2 |WAP |Rede de Perímetro |contosowapset |contososac2 |Estático |

Como você deve ter notado, nenhum NSG foi especificado. Isso ocorre porque o Azure permite que você use NSG no nível de sub-rede. Em seguida, você pode controlar o tráfego de rede de máquinas usando o NSG individual associado à sub-rede ou ao objeto NIC. Leia mais em [O que é um NSG (grupo de segurança de rede)?](/azure/virtual-network/tutorial-filter-network-traffic).
Um endereço IP estático é recomendável se você estiver gerenciando o DNS. Você pode usar o DNS do Azure e, em vez disso, nos registros DNS do domínio, referir-se às novas máquinas por seus FQDNs do Azure.
O painel da máquina virtual deve ser semelhante ao exemplo abaixo após a implantação ser concluída:

![Máquinas Virtuais implantadas](./media/how-to-connect-fed-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-the-domain-controller--ad-fs-servers"></a>5. Configurando os servidores do controlador de domínio/AD FS
 Para autenticar qualquer solicitação de entrada, o AD FS precisará contatar o controlador de domínio. Para evitar a viagem dispendiosa do Azure para o DC local para autenticação, é recomendável implantar uma réplica do controlador de domínio no Azure. Para alcançar a alta disponibilidade, é recomendável criar um conjunto de disponibilidade com pelo menos 2 controladores de domínio.

| Controlador de domínio | Função | Conta de armazenamento |
|:---:|:---:|:---:|
| contosodc1 |Réplica |contososac1 |
| contosodc2 |Réplica |contososac2 |

* Promova os dois servidores como controladores de domínio de réplica com DNS
* Configure os servidores do AD FS instalando a função AD FS usando o gerenciador de servidores.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. implantando Load Balancer internas (ILB)
**6.1. Criar ILB**

Para implantar um ILB, selecione Balanceadores de Carga no portal do Azure e clique em adicionar (+).

> [!NOTE]
> Se você não encontrar **Balanceadores de Carga** no menu, clique em **Procurar** na parte inferior esquerda do portal e role até ver **Balanceadores de Carga**.  Clique na estrela amarela para adicioná-lo ao menu. Agora, selecione o novo ícone de balanceador de carga para abrir o painel e iniciar a configuração do balanceador de carga.
>
>

![Procurar balanceador de carga](./media/how-to-connect-fed-azure-adfs/browseloadbalancer.png)

* **Nome**: atribua qualquer nome adequado ao balanceador de carga
* **Esquema**: como esse balanceador de carga será colocado na frente dos servidores de AD FS e destina-se somente a conexões de rede internas, selecione "interno"
* **Rede virtual**: escolha a rede virtual em que você está implantando o AD FS
* **Sub-rede**: selecione a sub-rede interna aqui
* **Atribuição de endereço IP**: estática

![Balanceador de carga interno](./media/how-to-connect-fed-azure-adfs/ilbdeployment1.png)

Depois que você clicar em Criar e o ILB for implantado, você deverá vê-lo na lista de balanceadores de carga:

![Balanceadores de carga após ILB](./media/how-to-connect-fed-azure-adfs/ilbdeployment2.png)

A próxima etapa é configurar o pool de back-end e a investigação de back-end.

**6.2. Configurar pool de back-end ILB**

Selecione o ILB recém-criado no painel Balanceadores de Carga. Isso abrirá o painel de configurações.

1. Selecione pools de back-end no painel de configurações
2. No painel Adicionar pool de back-end, clique em Adicionar máquina virtual
3. Você verá um painel em que pode escolher o conjunto de disponibilidade
4. Escolha o conjunto de disponibilidade do AD FS

![Configurar pool ILB](./media/how-to-connect-fed-azure-adfs/ilbdeployment3.png)

**6.3. Configurando investigação**

No painel de configurações doe ILB, selecione Investigações de Integridade.

1. Clique em adicionar
2. Fornecer detalhes para investigação a. **Nome**: nome de investigação b. **Protocolo**: http c. **Porta**: 80 (HTTP) d. **Caminho**: /adfs/probe e. **Intervalo**: 5 (valor padrão) – é o intervalo em que o ILB investigará as máquinas no pool de back-end f. **Limite não íntegro**: 2 (valor padrão) – esse é o limite de falhas de investigação consecutivas após o qual o ILB declarará que uma máquina no pool de back-end não está respondendo e interromperá o envio de tráfego para ela.


Estamos usando o ponto de extremidade /adfs/probe criado explicitamente para verificações de integridade em um ambiente do AD FS em que uma verificação completa do caminho HTTPS não pode ocorrer.  Isso é consideravelmente melhor que uma verificação básica da porta 443, que não reflete com precisão o status de uma implantação moderna do AD FS.  Encontre mais informações sobre esse tópico em https://blogs.technet.microsoft.com/applicationproxyblog/2014/10/17/hardware-load-balancer-health-checks-and-web-application-proxy-ad-fs-2012-r2/.

**6.4. Criar regras de balanceamento de carga**

Para equilibrar o tráfego de modo eficiente, o ILB deve ser configurado com regras de balanceamento de carga. Para criar uma regra de balanceamento de carga,

1. Selecione a regra de balanceamento de carga no painel de configurações do ILB
2. Clique em Adicionar no painel de regra de balanceamento de carga
3. No painel adicionar regra de balanceamento de carga a. **Nome**: forneça um nome para a regra b. **Protocolo**: selecione TCP c. **Porta**: 443 d. **Porta de back-end**: 443 e. **Pool de back-end**: selecione o pool criado para o cluster do AD FS anteriormente f. **Investigação**: selecione a investigação criada anteriormente para os servidores do AD FS

![Configurar regras de balanceamento ILB](./media/how-to-connect-fed-azure-adfs/ilbdeployment5.png)

**6.5. Atualizar DNS com ILB**

Usando seu servidor DNS interno, crie um registro A para o ILB. O registro a deve ser para o serviço de Federação com o endereço IP apontando para o endereço IP do ILB. Por exemplo, se o endereço IP ILB for 10.3.0.8 e o serviço de Federação instalado for fs.contoso.com, crie um registro A para fs.contoso.com apontando para 10.3.0.8.
Isso garantirá que todos os dados trasmitted para fs.contoso.com acabem no ILB e sejam adequadamente roteados.

> [!WARNING]
> Se você estiver usando o WID (banco de dados interno do Windows) para seu banco de dados AD FS, esse valor deverá ser definido temporariamente para apontar para o servidor de AD FS primário ou o proxy de aplicativo Web falhará registro. Depois de registrar com êxito todos os servidores proxy Application da Web, altere essa entrada DNS para apontar para o balanceador de carga.

> [!NOTE]
> Se sua implantação também estiver usando IPv6, certifique-se de criar um registro AAAA correspondente.
>

### <a name="7-configuring-the-web-application-proxy-server"></a>7. Configurando o servidor proxy de aplicativo Web
**7.1. Configurar os servidores de Proxy de Aplicativo Web para acessar os servidores do AD FS**

Para garantir que os servidores de Proxy de Aplicativo Web possam acessar os servidores do AD FS por trás do ILB, crie um registro em %systemroot%\system32\drivers\etc\hosts para o ILB. Observe que o DN (nome diferenciado) deve ser o nome de serviço de federação, por exemplo, fs.contoso.com. E a entrada IP deve ser a do endereço IP do ILB (10.3.0.8 como no exemplo).

> [!WARNING]
> Se você estiver usando o WID (banco de dados interno do Windows) para seu banco de dados AD FS, esse valor deverá ser definido temporariamente para apontar para o servidor de AD FS primário ou o proxy de aplicativo Web falhará registro. Depois de registrar com êxito todos os servidores proxy Application da Web, altere essa entrada DNS para apontar para o balanceador de carga.


**7.2. Instalar a função de Proxy de Aplicativo Web**

Depois de garantir que os servidores de Proxy de Aplicativo da Web possam acessar os servidores do AD FS por trás do ILB, você pode instalar os servidores de Proxy de Aplicativo Web.
Os servidores de Proxy de Aplicativo Web não precisam ser associados ao domínio. Instale as funções de Proxy de Aplicativo Web em dois servidores de Proxy de Aplicativo Web selecionando a função de Acesso Remoto. O gerenciador de servidores o guirá para concluir a instalação do WAP.
Para obter mais informações sobre como implantar o WAP, leia [Instalar e configurar o servidor de Proxy de Aplicativo Web](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383662(v=ws.11)).

### <a name="8--deploying-the-internet-facing-public-load-balancer"></a>8. implantando a Internet (pública) Load Balancer
**8,1. criar Load Balancer voltados para a Internet (público)**

No portal do Azure, selecione Balanceadores de Carga e clique em Adicionar. No painel Criar balanceador de carga, insira as informações a seguir

1. **Nome**: nome para o balanceador de carga
2. **Esquema**: público – essa opção informa ao Azure que este balanceador de carga precisará de um endereço público.
3. **Endereço IP**: crie um novo endereço IP (dinâmico)

![Balanceador de Carga para a Internet](./media/how-to-connect-fed-azure-adfs/elbdeployment1.png)

Após a implantação, o balanceador de carga será exibido na lista de balanceadores de carga.

![Lista de balanceadores de carga](./media/how-to-connect-fed-azure-adfs/elbdeployment2.png)

**8.2. Atribuir um rótulo DNS ao IP público**

Clique na entrada do balanceador de carga recém-criado no painel Balanceadores de carga para exibir o painel de configuração. Execute as seguintes etapas para configurar o rótulo DNS para o IP público:

1. Clique no endereço IP público. Isso abrirá o painel para o IP público e suas configurações
2. Clique em Configuração
3. Forneça um rótulo DNS. Esse se tornará o rótulo DNS público que você pode acessar de qualquer lugar, por exemplo, contosofs.westus.cloudapp.azure.com. Você pode adicionar uma entrada no DNS externo para o serviço de federação (como fs.contoso.com) que é resolvida como o rótulo DNS do balanceador de carga externo (contosofs.westus.cloudapp.azure.com).

![Configurar balanceador de carga para a Internet](./media/how-to-connect-fed-azure-adfs/elbdeployment3.png)

![Configurar balanceador de carga (DNS) para a Internet](./media/how-to-connect-fed-azure-adfs/elbdeployment4.png)

**8.3. Configurar o pool de back-end para o Balanceador de Carga para a Internet (Público)**

Siga as mesmas etapas usadas para criar o balanceador de carga interno a fim de configurar o pool de back-end para o Balanceador de Carga para a Internet (Público) como o conjunto de disponibilidade para os servidores WAP. Por exemplo, contosowapset.

![Configurar pool de back-end do Balanceador de Carga para Internet](./media/how-to-connect-fed-azure-adfs/elbdeployment5.png)

**8.4. Configurar investigação**

Siga as mesmas etapas usadas para configurar o balanceador de carga interno a fim de configurar a investigação do pool de back-end de servidores WAP.

![Configurar investigação do Balanceador de Carga para Internet](./media/how-to-connect-fed-azure-adfs/elbdeployment6.png)

**8.5. Criar regra(s) de balanceamento de carga**

Siga as mesmas etapas usadas no ILB para configurar a regra de balanceamento de carga para TCP 443.

![Configurar regras de balanceamento do Balanceador de Carga para Internet](./media/how-to-connect-fed-azure-adfs/elbdeployment7.png)

### <a name="9-securing-the-network"></a>9. protegendo a rede
**9.1. Proteger a sub-rede interna**

Em geral, você precisa das regras a seguir para proteger com eficiência sua sub-rede interna (na ordem listada abaixo)

| Regra | Descrição | Flow |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Permitir a comunicação HTTPS de rede de perímetro |Entrada |
| DenyInternetOutbound |Sem acesso à Internet |Saída |

![Regras de acesso INT (entrada)](./media/how-to-connect-fed-azure-adfs/nsg_int.png)

**9.2. Proteger a sub-rede de perímetro**

| Regra | Descrição | Flow |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |Permitir HTTPS da Internet para a rede de perímetro |Entrada |
| DenyInternetOutbound |Tudo para a Internet é bloqueado, exceto HTTPS |Saída |

![Regras de acesso EXT (entrada)](./media/how-to-connect-fed-azure-adfs/nsg_dmz.png)

> [!NOTE]
> Se a autenticação de certificado de usuário do cliente (autenticação clientTLS usando os certificados de usuário X. 509) for necessária, AD FS exigirá que a porta TCP 49443 seja habilitada para acesso de entrada.
>
>

### <a name="10-test-the-ad-fs-sign-in"></a>10. testar a entrada AD FS
A maneira mais fácil é testar o AD FS usando a página IdpInitiatedSignon.aspx. Para fazer isso, é necessário habilitar IdpInitiatedSignOn nas propriedades do AD FS. Siga as etapas abaixo para verificar a instalação do AD FS

1. Execute o cmdlet abaixo no servidor do AD FS, usando o PowerShell, para defini-lo como habilitado.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. Em qualquer computador externo, acesse https:\//adfs-server.contoso.com/adfs/ls/IdpInitiatedSignon.aspx.
3. Você deve ver a página do AD FS como indicado abaixo:

![Testar página de logon](./media/how-to-connect-fed-azure-adfs/test1.png)

Quando você entrar com êxito, ele lhe fornecerá uma mensagem de êxito, conforme mostrado abaixo:

![Êxito do teste](./media/how-to-connect-fed-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Modelo de implantação do AD FS no Azure
O modelo implanta uma configuração de seis máquinas, duas para controladores de domínio, AD FS e WAP.

[AD FS no modelo de implantação do Azure](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Você pode usar uma rede virtual existente ou criar uma nova VNETao implantar esse modelo. Os diversos parâmetros disponíveis para personalizar a implantação estão listados abaixo, com a descrição do uso do parâmetro no processo de implantação.

| Parâmetro | Descrição |
|:--- |:--- |
| Location |A região para implantar os recursos, por exemplo, Leste dos EUA. |
| StorageAccountType |O tipo de conta de armazenamento criada |
| VirtualNetworkUsage |Indica se uma nova rede virtual será criada ou se uma existente será usada |
| VirtualNetworkName |O nome da Rede Virtual para criar, obrigatória no uso da rede virtual nova ou existente |
| VirtualNetworkResourceGroupName |Especifica o nome do grupo de recursos onde reside a rede virtual existente. Ao usar uma rede virtual existente, isso se torna um parâmetro obrigatório para que a implantação possa encontrar a ID da rede virtual existente |
| VirtualNetworkAddressRange |O intervalo de endereços da nova VNET, obrigatória se você estiver criando uma nova rede virtual |
| InternalSubnetName |O nome da sub-rede interna, obrigatório em ambas as opções de uso de rede virtual (novas ou existentes) |
| InternalSubnetAddressRange |O intervalo de endereços da sub-rede interna, que contém os servidores de controladores de domínio e o ADFS, obrigatórios se você estiver criando uma nova rede virtual. |
| DMZSubnetAddressRange |O intervalo de endereços da sub-rede dmz, que contém os servidores proxy de aplicativo do Windows, obrigatórios se você estiver criando uma nova rede virtual. |
| DMZSubnetName |O nome da sub-rede interna, obrigatório em ambas as opções de uso de rede virtual (novas ou existentes). |
| ADDC01NICIPAddress |O endereço IP interno do primeiro controlador de domínio; esse endereço IP será atribuído estaticamente para o controlador de domínio e deve ser um endereço ip válido dentro da sub-rede interna |
| ADDC02NICIPAddress |O endereço IP interno do segundo controlador de domínio; esse endereço IP será atribuído estaticamente para o controlador de domínio e deve ser um endereço ip válido dentro da sub-rede interna |
| ADFS01NICIPAddress |O endereço IP interno do primeiro servidor ADFS; esse endereço IP será atribuído estaticamente para o servidor ADFS e deve ser um endereço ip válido dentro da sub-rede interna |
| ADFS02NICIPAddress |O endereço IP interno do segundo servidor ADFS; esse endereço IP será atribuído estaticamente para o servidor ADFS e deve ser um endereço ip válido dentro da sub-rede interna |
| WAP01NICIPAddress |O endereço IP interno do primeiro servidor WAP; esse endereço IP será atribuído estaticamente para o servidor WAP e deve ser um endereço ip válido dentro da sub-rede DMZ |
| WAP02NICIPAddress |O endereço IP interno do segundo servidor WAP; esse endereço IP será atribuído estaticamente para o servidor WAP e deve ser um endereço ip válido dentro da sub-rede DMZ |
| ADFSLoadBalancerPrivateIPAddress |O endereço IP interno do balanceador de carga do ADFS; esse endereço IP será atribuído estaticamente ao balanceador de carga e deve ser um endereço ip válido dentro da sub-rede interna |
| ADDCVMNamePrefix |Prefixo de nome de máquina virtual para controladores de domínio |
| ADFSVMNamePrefix |Prefixo do nome de máquina virtual para servidores ADFS |
| WAPVMNamePrefix |Prefixo do nome de máquina virtual para servidores WAP |
| ADDCVMSize |O tamanho da vm dos controladores de domínio |
| ADFSVMSize |O tamanho da vm dos servidores ADFS |
| WAPVMSize |O tamanho da vm dos servidores WAP |
| AdminUserName |O nome do administrador local das máquinas virtuais |
| AdminPassword |A senha para a conta de administrador local das máquinas virtuais |

## <a name="additional-resources"></a>Recursos adicionais
* [Conjuntos de disponibilidade](https://aka.ms/Azure/Availability)
* [Azure Load Balancer](/azure/load-balancer/load-balancer-overview)
* [Balanceador de Carga Interno](/azure/load-balancer/quickstart-load-balancer-standard-internal-powershell)
* [Balanceador de Carga para a Internet](/azure/load-balancer/quickstart-load-balancer-standard-public-powershell)
* [Contas de Armazenamento](https://aka.ms/Azure/Storage)
* [Redes virtuais do Azure](/azure/virtual-network/virtual-networks-overview)
* [AD FS e Links de Proxy de Aplicativo Web](/archive/blogs/tangent_thoughts/qrg-quick-reference-guide-active-directory-federation-services)

## <a name="next-steps"></a>Próximas etapas
* [Integração de suas identidades locais com o Active Directory do Azure](/azure/active-directory/hybrid/whatis-hybrid-identity)
* [Configurar e gerenciar o AD FS usando o Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-fed-whatis)
* [Implantação AD FS de alta disponibilidade entre regiões no Azure com o Gerenciador de tráfego do Azure](active-directory-adfs-in-azure-with-azure-traffic-manager.md)