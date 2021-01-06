---
title: Etapa 1 configurar a infraestrutura básica do DirectAccess
description: Saiba como configurar a infraestrutura necessária para uma implantação básica do DirectAccess usando um único servidor DirectAccess em um ambiente misto de IPv4 e IPv6.
manager: brianlic
ms.topic: article
ms.assetid: ba4de2a4-f237-4b14-a8a7-0b06bfcd89ad
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 41009608862a21987097ad2a58f4fb524b535f06
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947252"
---
# <a name="step-1-configure-the-basic-directaccess-infrastructure"></a>Etapa 1 configurar a infraestrutura básica do DirectAccess

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Este tópico descreve como configurar a infraestrutura necessária a uma implantação básica do DirectAccess que utiliza um servidor individual do DirectAccess em um ambiente misto de IPv4 e IPv6. Antes de iniciar as etapas de implantação, verifique se você concluiu as etapas de planejamento descritas em [planejar uma implantação básica do DirectAccess](../../../remote-access/directaccess/single-server-wizard/Plan-a-Basic-DirectAccess-Deployment.md).

|Tarefa|Descrição|
|----|--------|
|Definir configurações de rede do servidor|Definir as configurações de rede do servidor do DirectAccess.|
|Configurar o roteamento da rede corporativa|Configurar o roteamento da rede corporativa para verificar se o tráfego está devidamente roteado.|
|Configurar firewalls|Configurar firewalls adicionais, se necessário.|
|Configurar o servidor DNS|Configurar as definições de DNS do servidor do DirectAccess|
|Configurar o Active Directory|Unir computadores cliente e o servidor do DirectAccess no domínio do Active Directory.|
|Configurar GPOs|Configurar os GPOs para implantação, se necessário.|
|Configurar os grupos de segurança|Configurar os grupos de segurança que conterão os computadores cliente do DirectAccess e quaisquer outros grupos de segurança requeridos na implantação.|

> [!NOTE]
> Este tópico inclui cmdlets do Windows PowerShell de exemplo que podem ser usados para automatizar alguns dos procedimentos descritos. Para obter mais informações, confira [Usando os Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).

## <a name="configure-server-network-settings"></a><a name="ConfigNetworkSettings"></a>Definir configurações de rede do servidor
As configurações de interface de rede a seguir são requeridas para uma implantação de servidor único em um ambiente com IPv4 e IPv6. Todos os endereços IP são configurados usando **Alterar configurações do adaptador** na **Central de Rede e Compartilhamento do Windows**.

-   Topologia de borda

    -   Um endereço público estático IPv4 ou IPv6 voltado para a Internet.

        > [!NOTE]
        > Dois endereços IPv4 públicos consecutivos são necessários para o Teredo. Se não estiver usando o Teredo, você poderá configurar um endereço IPv4 estático público individual.

    -   Um único endereço estático interno IPv4 ou IPv6.

-   Atrás do dispositivo NAT (dois adaptadores de rede)

    -   Um único endereço estático interno IPv4 ou IPv6 voltado para a rede.

    -   Um único endereço estático de perímetro IPv4 ou IPv6 voltado para a rede.

-   Atrás do dispositivo NAT (um adaptador de rede)

    -   Um único endereço estático IPv4 ou IPv6.

> [!NOTE]
> Se o servidor do DirectAccess tiver dois adaptadores de rede (um classificado no perfil do domínio e outro em um perfil público/privado), porém uma topologia de NIC único for usada, veja as recomendações a seguir:
>
> 1.  Assegure que o segundo NIC e todos os outros NICs adicionais estejam classificados no perfil de domínio.
> 2.  Se o segundo NIC não puder ser configurado para o perfil do domínio por alguma razão, a política de IPsec do DirectAccess deve ser manualmente estendida a todos os perfis usando os seguintes comandos do Windows PowerShell:
>
>     ```
>     $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>
>     Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any
>     Save-NetGPO -GPOSession $gposession
>     ```
>
>     Os nomes das políticas IPsec são DirectAccess-DaServerToInfra e DirectAccess-DaServerToCorp.

## <a name="configure-routing-in-the-corporate-network"></a><a name="ConfigRouting"></a>Configurar o roteamento da rede corporativa
Configure o roteamento na rede corporativa da seguinte forma:

-   Quando o IPv6 nativo for implantado na organização, adicione uma rota para que os roteadores no tráfego IPv6 da rota de rede interna retorne pelo servidor de Acesso Remoto.

-   Configure manualmente as rotas IPv4 e IPv6 da organização nos servidores de Acesso Remoto. Adicione uma rota publicada para que todo o tráfego com um prefixo IPv6 (/48) da organização seja encaminhado à rede interna. Além disso, para tráfego IPv4, adicione rotas explícitas para que o tráfego IPv4 seja encaminhado para a rede interna.

## <a name="configure-firewalls"></a><a name="ConfigFirewalls"></a>Configurar firewalls
Ao usar firewalls adicionais na sua implantação, aplique as seguintes exceções de firewall voltado para a Internet do tráfego de Acesso Remoto quando o servidor de Acesso Remoto está na Internet IPv4:

-   tráfego 6to4-protocolo IP 41 de entrada e saída.

-   IP-HTTPS-protocolo TCP porta de destino 443 e saída da porta de origem TCP 443. Quando o servidor de Acesso Remoto tem um único adaptador de rede e o servidor de local de rede está no servidor de acesso remoto, a porta TCP 62000 também é necessária.

    > [!NOTE]
    > Essa isenção deve ser configurada no servidor de acesso remoto. Todas as outras isenções devem ser configuradas no firewall de borda.

> [!NOTE]
> Para tráfego Teredo e 6to4, essas exceções devem ser aplicadas para os endereços IPv4 públicos consecutivos voltados para a Internet no servidor de Acesso Remoto. Para IP-HTTPS, as exceções precisam ser aplicadas apenas para o endereço no qual o nome externo do servidor é resolvido.

Ao usar firewalls adicionais, aplique as seguintes exceções de firewall voltado para a Internet do tráfego de Acesso Remoto quando o servidor de Acesso Remoto está na Internet IPv6:

-   Protocolo IP 50

-   Entrada da porta de destino UDP 500 e saída da porta de origem UDP 500.

Ao usar firewalls adicionais, aplique as seguintes exceções do firewall de rede interna no tráfego de Acesso Remoto:

-   ISATAP-protocolo 41 de entrada e saída

-   TCP/UDP para todo o tráfego IPv4/IPv6

## <a name="configure-the-dns-server"></a><a name="ConfigDNS"></a>Configurar o servidor DNS
Você deve configurar manualmente uma entrada DNS para o site do servidor de local da rede interna da sua implantação.

### <a name="to-create-the-network-location-server-and-ncsi-probe-dns-records"></a><a name="NLS_DNS"></a>Para criar os registros do servidor de local de rede e do DNS da sonda NCSI

1.  No servidor DNS da rede interna, execute **DNSMGMT. msc** e pressione Enter.

2.  No painel esquerdo do console **Gerenciador DNS**, expanda a zona de pesquisa direta para o seu domínio. Clique com o botão direito no domínio e clique em **Novo Host (A ou AAAA)**.

3.  Na caixa de diálogo **Novo Host**, na caixa **Nome (usa o nome de domínio pai se deixado em branco)**, digite o nome de DNS para o site do servidor de local de rede (este é o nome que os clientes do DirectAccess usam para conectar ao servidor de local de rede). Na caixa **Endereço IP**, digite o endereço IPv4 no servidor de local de rede e clique em **Adicionar Host**. Na caixa de diálogo **DNS**, clique em **OK**.

4.  Na caixa de diálogo **Novo Host**, na caixa **Nome (usa o nome de domínio pai se deixado em branco)**, digite o nome do DNS para a sonda da web (o nome para a sonda da web é directaccess-webprobehost). Na caixa **Endereço IP**, digite o endereço IPv4 da sonda da web e clique em **Adicionar Host**. Repita esse processo para o directaccess-corpconnectivityhost e quaisquer verificadores de conectividade criados manualmente. Na caixa de diálogo **DNS**, clique em **OK**.

5.  Clique em **Concluído**.

![](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif) * *_<em>Comandos equivalentes</em>_* do Windows PowerShell

O seguinte cmdlet ou cmdlets do Windows PowerShell executam a mesma função que o procedimento anterior. Insira cada cmdlet em uma única linha, mesmo que possa aparecer quebra em várias linhas aqui devido a restrições de formatação.

```
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>
```

Você também deve configurar entradas DNS para o seguinte:

-   _ *O servidor IP-HTTPS**-os clientes DirectAccess devem ser capazes de resolver o nome DNS do servidor de acesso remoto da Internet.

-   **Verificação de revogação de CRL** – o DirectAccess usa a verificação de revogação de certificado para a conexão IP-HTTPS entre clientes DirectAccess e o servidor de acesso remoto e para a conexão baseada em https entre o cliente DirectAccess e o servidor de local de rede. Em ambos os casos, os clientes do DirectAccess devem poder resolver e acessar o local do ponto de distribuição da CRL.

## <a name="configure-active-directory"></a><a name="ConfigAD"></a>Configurar o Active Directory
O servidor de Acesso Remoto e todos os computadores cliente do DirectAccess devem ser ingressados em um domínio do Active Directory. Os computadores cliente do DirectAccess devem ser membros de um dos seguintes tipos de domínio:

-   Domínios pertencentes à mesma floresta que o servidor de Acesso Remoto.

-   Domínios pertencentes a florestas com relações de confiança bidirecional com a floresta do servidor de Acesso Remoto.

-   Domínios com relação de confiança bidirecional com o domínio do servidor de Acesso Remoto.

#### <a name="to-join-the-remote-access-server-to-a-domain"></a>Para ingressar o servidor do DirectAccess em um domínio

1.  No Gerenciador do Servidor, clique em **Servidor Local**. No painel de detalhes, clique no link ao lado do **Nome do computador**.

2.  Na caixa de diálogo **Propriedades do sistema** , clique na guia **nome do computador** . Na guia **nome do computador** , clique em **alterar**.

3.  Em **Nome do Computador**, digite o nome do computador se você também estiver alterando o nome do computador ao ingressar o servidor no domínio. Em **Membro de**, clique em **Domínio** e digite o nome do domínio em que você deseja ingressar o servidor; por exemplo, corp.contoso.com, e clique em **OK**.

4.  Quando você for solicitado a informar um nome de usuário e uma senha, digite o nome de usuário e a senha de um usuário com direitos de ingressar computadores no domínio e clique em **OK**.

5.  Quando você vir uma caixa de diálogo de boas-vindas ao domínio, clique em **OK**.

6.  Quando você for solicitado a reiniciar o computador, clique em **OK**.

7.  Na caixa de diálogo **Propriedades do Sistema**, clique em **Fechar**.

8.  Quando for solicitado a reiniciar o computador, clique em **Reiniciar Agora**.

#### <a name="to-join-client-computers-to-the-domain"></a>Para ingressar computadores cliente no domínio

1.  Execute **explorer.exe**.

2.  Clique com o botão direito do mouse no ícone Computador e em **Propriedades**.

3.  Na página **Sistema**, clique em **Configurações avançadas do sistema**.

4.  Na caixa de diálogo **Propriedades do Sistema**, na guia **Nome do Computador**, clique em **Alterar**.

5.  Em **Nome do computador**, digite o nome do computador se você também estiver alterando o nome do computador ao ingressar o servidor no domínio. Em **Membro de**, clique em **Domínio** e digite o nome do domínio em que você deseja ingressar o servidor; por exemplo, corp.contoso.com, e clique em **OK**.

6.  Quando você for solicitado a informar um nome de usuário e uma senha, digite o nome de usuário e a senha de um usuário com direitos de ingressar computadores no domínio e clique em **OK**.

7.  Quando você vir uma caixa de diálogo de boas-vindas ao domínio, clique em **OK**.

8.  Quando você for solicitado a reiniciar o computador, clique em **OK**.

9. Na caixa de diálogo **Propriedades do Sistema**, clique em Fechar. Clique em **Reiniciar Agora** quando solicitado.

![](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif) * *_<em>Comandos equivalentes</em>_* do Windows PowerShell

O seguinte cmdlet ou cmdlets do Windows PowerShell executam a mesma função que o procedimento anterior. Insira cada cmdlet em uma única linha, mesmo que possa aparecer quebra em várias linhas aqui devido a restrições de formatação.

Observe que você deve fornecer as credenciais do domínio depois de inserir o comando Add-Computer abaixo.

```
Add-Computer -DomainName <domain_name>
Restart-Computer
```

## <a name="configure-gpos"></a><a name="ConfigGPOs"></a>Configurar GPOs
Para implantar o acesso remoto, você precisa de um mínimo de dois objetos de diretiva de Grupo: um objeto de política de grupo contém configurações para o servidor de acesso remoto e uma delas contém configurações para computadores cliente do DirectAccess. Quando você configura o acesso remoto, o assistente cria automaticamente o objeto de diretiva de grupo necessário. No entanto, se sua organização aplicar uma Convenção de nomenclatura ou se você não tiver as permissões necessárias para criar ou editar objetos de política de grupo, elas deverão ser criadas antes de configurar o acesso remoto.

Para criar um objeto de política de grupo, consulte [criar e editar um objeto de política de grupo](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754740(v=ws.11)).

> [!IMPORTANT]
> O administrador pode vincular manualmente o objeto de política de grupo do DirectAccess a uma unidade organizacional usando estas etapas:
>
> 1.  Antes de configurar o DirectAccess, vincule os GPOs criados às respectivas Unidades Organizacionais.
> 2.  Configure o DirectAccess, especificando um grupo de segurança para computadores cliente.
> 3.  O administrador pode ou não ter permissões para vincular os Objetos de Política de Grupo ao domínio. De qualquer maneira, os Objetos de Política de Grupo serão configurados automaticamente. Se os GPOs já estiverem vinculados a uma OU, os links não serão removidos. E os GPOs não serão vinculados ao domínio. Para um GPO de servidor, a OU deverá conter o objeto de computador do servidor, ou o GPO será vinculado à raiz do domínio.
> 4.  Se a vinculação à OU não foi feita antes de executar o Assistente do DirectAccess, depois de concluir a configuração, o administrador poderá vincular os Objetos de Política de Grupo do DirectAccess às Unidades Organizacionais requeridas. O link para o domínio pode ser removido. As etapas para vincular um objeto de política de grupo a uma unidade organizacional podem ser encontradas [aqui](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732979(v=ws.11))

> [!NOTE]
> Se um objeto de política de grupo tiver sido criado manualmente, será possível durante a configuração do DirectAccess que o objeto de política de grupo não estará disponível. O objeto de política de grupo pode não ter sido replicado para o controlador de domínio mais próximo para o computador de gerenciamento. Neste caso, o administrador pode aguardar a replicação ser concluída, ou forçá-la.

> [!Warning]
> O uso de qualquer meio que não seja o assistente de instalação do DirectAccess para configurar o DirectAccess, como a modificação direta de objetos do DirectAccess Política de Grupo ou a modificação manual das configurações de política padrão no servidor ou cliente, não tem suporte.

## <a name="configure-security-groups"></a><a name="ConfigSGs"></a>Configurar os grupos de segurança
As configurações do DirectAccess contidas nos objetos de política de grupo do computador cliente são aplicadas somente a computadores que são membros dos grupos de segurança que você especifica ao configurar o acesso remoto.

### <a name="to-create-a-security-group-for-directaccess-clients"></a><a name="Sec_Group"></a>Para criar um grupo de segurança para os clientes do DirectAccess

1.  Execute _ * DSA. msc * *. No console **Usuários e Computadores do Active Directory**, no painel esquerdo, expanda o domínio que conterá o grupo de segurança, clique com o botão direito do mouse em **Usuários**, aponte para **Novo** e clique em **Grupo**.

2.  Na caixa de diálogo **Novo Objeto - Grupo**, em **Nome do grupo**, digite o nome do grupo de segurança.

3.  Em **Escopo do grupo**, clique em **Global**, em **Tipo de grupo**, escolha **Segurança** e clique em **OK**.

4.  Clique no grupo de segurança dos computadores cliente do DirectAccess e, na caixa de diálogo de propriedades, clique na guia **Membros**.

5.  Na guia **Membros**, clique em **Adicionar**.

6.  Na caixa de diálogo **Selecionar Usuários, Contatos, Computadores ou Contas de Serviço**, selecione os computadores cliente que você deseja habilitar para o DirectAccess e clique em **OK**.

![](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)**Comandos equivalentes** do Windows PowerShell

O seguinte cmdlet ou cmdlets do Windows PowerShell executam a mesma função que o procedimento anterior. Insira cada cmdlet em uma única linha, mesmo que possa aparecer quebra em várias linhas aqui devido a restrições de formatação.

```
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>
```

## <a name="next-step"></a><a name="BKMK_Links"></a>Próxima etapa

-   [Etapa 2: Configurar o servidor do DirectAccess Básico](da-basic-configure-s2-server.md)

