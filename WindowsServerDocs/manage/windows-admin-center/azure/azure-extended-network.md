---
title: Estenda suas sub-redes locais para o Azure usando a rede estendida do Azure
description: Estenda suas sub-redes locais para o Azure usando a rede estendida do Azure
ms.technology: manage
ms.topic: article
author: grcusanz
ms.author: grcusanz
ms.date: 12/17/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 0704c23e7e84b4e2e1611c50ab5b8980e41176c7
ms.sourcegitcommit: 14c9526b1c74821341d4b66de92adce9bee92f10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94559068"
---
# <a name="extend-your-on-premises-subnets-into-azure-using-azure-extended-network"></a>Estenda suas sub-redes locais para o Azure usando a rede estendida do Azure

> Aplica-se a: Windows Admin Center, Versão prévia do Windows Admin Center

## <a name="overview"></a>Visão geral

A rede estendida do Azure permite que você alongue uma sub-rede local no Azure para permitir que as máquinas virtuais locais mantenham seus endereços IP privados locais originais ao migrar para o Azure.
A rede é estendida usando um túnel VXLAN bidirecional entre duas VMs do Windows Server 2019 atuando como dispositivos virtuais, uma em execução localmente e a outra em execução no Azure, cada uma também conectada à sub-rede a ser estendida.
Cada sub-rede que você vai estender requer um par de dispositivos. Várias sub-redes podem ser estendidas usando vários pares.

> [!NOTE]
> A rede estendida do Azure só deve ser usada para computadores que não podem ter seu endereço IP alterado durante a migração para o Azure. É sempre melhor alterar o endereço IP e conectá-lo a uma sub-rede que existe integralmente no Azure, se essa for uma opção.

## <a name="planning"></a>Planejamento

Para se preparar para usar a rede estendida do Azure, você deve identificar qual sub-rede deseja ampliar e, em seguida, executar as seguintes etapas:

### <a name="capacity-planning"></a>planejamento de capacidade

Você pode estender até 250 endereços IP usando a rede estendida do Azure. Você pode esperar uma taxa de transferência agregada de cerca de 700 Mbps, com certa variabilidade, dependendo da velocidade da CPU das soluções de virtualização de rede estendida do Azure.

### <a name="configuration-in-azure"></a>Configuração no Azure

Antes de usar o centro de administração do Windows, você deve executar as seguintes etapas por meio do portal do Azure:

1. Crie uma rede virtual no Azure que contenha pelo menos duas sub-redes, além de sub-redes necessárias para sua conexão de gateway. Uma das sub-redes que você cria deve usar o mesmo CIDR de sub-rede que a sub-rede local que você deseja estender. A sub-rede deve ser exclusiva em seu domínio de roteamento para que ela não se sobreponha às sub-redes locais.
2. Configure um gateway de rede virtual para usar uma conexão site a site ou ExpressRoute para conectar a rede virtual à sua rede local.
3. Crie uma VM do Windows Server 2019 no Azure que seja capaz de executar a virtualização aninhada. Esse é um dos seus dois dispositivos virtuais. Conecte a interface de rede primária à sub-rede roteável e a segunda interface de rede à sub-rede estendida.
4. Inicie a VM, habilite a função Hyper-V e reinicialize. Por exemplo:

```powershell
Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart
```

5. Crie dois comutadores virtuais externos na VM e conecte um a cada uma das interfaces de rede. Por exemplo:

```powershell
New-VMSwitch -Name "External" -AllowManagementOS $true -NetAdapterName "Ethernet"
New-VMSwitch -Name "Extended" -AllowManagementOS $true -NetAdapterName "Ethernet 2"
```

### <a name="on-premises-configuration"></a>Configuração local

Você também deve executar algumas configurações manuais em sua infraestrutura local, incluindo a criação de uma VM para servir como a solução de virtualização local:

1. Verifique se as sub-redes estão disponíveis no computador físico em que você implantará a VM local (dispositivo virtual). Isso inclui a sub-rede que você deseja estender e uma segunda sub-rede que é exclusiva e não se sobrepõe às sub-redes na rede virtual do Azure.
2. Crie uma VM do Windows Server 2019 em qualquer hipervisor que ofereça suporte à virtualização aninhada. Este é o dispositivo virtual local. Recomendamos que você crie isso como uma VM altamente disponível em um cluster. Conecte um adaptador de rede virtual à sub-rede roteável e um segundo adaptador de rede virtual à sub-rede estendida.
3. Inicie a VM e, em seguida, execute este comando de uma sessão do PowerShell na VM para habilitar a função Hyper-V e reinicie a VM:

```powershell
Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart
```

4. Execute os seguintes comandos em uma sessão do PowerShell na VM para criar dois comutadores virtuais externos na VM e conecte um a cada uma das interfaces de rede:

```powershell
New-VMSwitch -Name "External" -AllowManagementOS $true -NetAdapterName "Ethernet"
New-VMSwitch -Name "Extended" -AllowManagementOS $true -NetAdapterName "Ethernet 2"
```

### <a name="additional-prerequisites"></a>Pré-requisitos adicionais

Se você tiver um firewall entre sua rede local e o Azure, você deve configurá-lo para permitir o roteamento assimétrico. Isso pode incluir etapas para desabilitar a randomização de número de sequência e habilitar o bypass de estado TCP. Consulte a documentação do seu fornecedor de firewall para essas etapas.

## <a name="deploy"></a>Implantar

A implantação é orientada pelo centro de administração do Windows.

### <a name="install-and-configure-windows-admin-center"></a>Instalar e configurar o centro de administração do Windows

1. [Baixe e instale o centro de administração do Windows](../understand/windows-admin-center.md) em qualquer computador capaz de executar o centro de administração do Windows, além dos dois dispositivos virtuais criados anteriormente.
2. No centro de administração do Windows, selecione **configurações** (no canto superior direito da página) > **extensões**. Em seguida, selecione **extensões** : ![ captura de tela mostrando a guia extensões disponíveis de configurações](../media/azure-extended-network/installed-extensions.png)
2. Na guia **extensões disponíveis** , selecione **rede estendida do Azure** e, em seguida, selecione **instalar**.
Após alguns segundos, você deverá ver uma mensagem indicando uma instalação bem-sucedida.
3. [Conecte o centro de administração do Windows ao Azure](azure-integration.md), caso ainda não tenha feito isso. Se você ignorar esta etapa agora, solicitaremos que você faça isso mais tarde no processo.
4. No centro de administração do Windows, vá para **todas as conexões**  >  **Adicionar** e, em seguida, selecione **Adicionar** no bloco do **Windows Server** . Insira o nome do servidor (e as credenciais, se necessário) para o dispositivo virtual local.
![Captura de tela do centro de administração do Windows mostrando a ferramenta de rede estendida do Azure em Gerenciador do Servidor no dispositivo virtual local ](../media/azure-extended-network/azure-extended-network.png) clique em **rede estendida do Azure** para começar. Na primeira vez que você receberá uma visão geral e um botão de instalação: ![ imagem](../media/azure-extended-network/azure-extended-network-intro.png)

### <a name="deploy-azure-extended-network"></a>Implantar a rede estendida do Azure

1. Clique em **Configurar** para iniciar a configuração.
2. Clique em **Avançar** para continuar após a visão geral.
3. No painel carregar pacote, você precisará baixar o pacote do agente de rede estendido do Azure e carregá-lo no dispositivo virtual. Siga as instruções no painel.

> [!IMPORTANT] Role para baixo, se necessário, e clique em **carregar** antes de clicar em **Avançar: Extended-Network configuração**.

4. Selecione o CIDR de sub-rede da rede local que você deseja estender. A lista de sub-redes é lida no dispositivo virtual. Se você não conectou a solução de virtualização ao conjunto correto de sub-redes, você não verá o CIDR de sub-rede desejado nesta lista.
Clique em Avançar depois de selecionar o CIDR da sub-rede.
5. Selecione a assinatura, o grupo de recursos e a rede virtual que você está estendendo: ![ rede do Azure ](../media/azure-extended-network/azure-network.png) a região (local do Azure) e a sub-rede são selecionadas automaticamente. Selecione Avançar: configuração do gateway de Extended-Network para continuar.
6. Agora, você configurará os dispositivos virtuais. O gateway local deve ter suas informações preenchidas automaticamente: ![ Gateway de rede local ](../media/azure-extended-network/on-premises-network-gateway.png) se parecer correto, você pode clicar em Avançar.
7. Para o dispositivo virtual do Azure, você precisará selecionar o grupo de recursos e a VM a ser usada: ![ Gateway de rede do Azure ](../media/azure-extended-network/azure-network-gateway.png) depois de selecionar a VM, você também precisará selecionar o CIDR de sub-rede do gateway de Extended-Network do Azure. Em seguida, clique em Avançar: implantar.
8. Examine as informações de resumo e clique em implantar para iniciar o processo de implantação. A implantação levará aproximadamente 5-10 minutos. Quando a implantação for concluída, você verá o painel a seguir para gerenciar os endereços IP estendidos e o status deverá dizer **OK** : ![ instalação concluída](../media/azure-extended-network/installation-complete.png)

## <a name="manage"></a>Gerenciar

Cada endereço IP que você deseja que possa ser acessado pela rede estendida precisará ser configurado. Você pode configurar até 250 endereços para estender.
Para estender um endereço

1. Clique em **adicionar endereços IPv4** : ![ imagem](../media/azure-extended-network/add-ipv4-addresses.png)

2. Você verá o submenu **Adicionar novos endereços IPv4** à direita: ![ imagem](../media/azure-extended-network/add-ipv4-addresses-panel.png)

3. Use o botão **Adicionar** para adicionar um endereço manualmente. Os endereços que você adicionar que estão no local poderão ser acessados pelos endereços do Azure que você adicionar à lista de endereços do Azure e vice-versa.

4. A rede estendida do Azure verifica a rede para descobrir endereços IP e popula as listas de sugestões com base nessa verificação. Para estender esses endereços, você deve usar a lista suspensa e marcar a caixa de seleção ao lado do endereço descoberto. Nem todos os endereços serão descobertos. Opcionalmente, use o botão **Adicionar** para adicionar manualmente os endereços que não são descobertos automaticamente.
![Imagem](../media/azure-extended-network/add-ipv4-addresses-panel-filled.png)

5. Clique em **Enviar** ao concluir. Você verá o status alterar para **atualizando** , depois **progredindo** e, finalmente, de volta para **OK** quando a configuração for concluída.

Seus endereços agora são estendidos. Use o botão adicionar endereços IPv4 para adicionar endereços adicionais a qualquer momento. Se um endereço IP não estiver mais em uso em qualquer extremidade da rede estendida, marque a caixa de seleção ao lado dele e selecione remover endereços IPv4.

Se você não quiser mais usar a rede estendida do Azure, clique no botão **remover rede estendida do Azure** . Isso desinstalará o agente dos dois dispositivos virtuais e removerá os endereços IP estendidos. A rede deixará de ser estendida. Você precisará executar novamente a instalação depois de removê-la, se quiser começar a usar a rede estendida novamente.

## <a name="troubleshooting"></a>Solução de problemas

Se você receber um erro durante a implantação da rede estendida do Azure, use as seguintes etapas:

1. Verifique se ambos os dispositivos virtuais estão usando o Windows Server 2019.
2. Verifique se você não está executando o centro de administração do Windows em um dos dispositivos virtuais. Recomendamos que você execute o centro de administração do Windows de uma rede local.
3. Verifique se você pode realizar remotamente a VM local do gateway do centro de administração do Windows usando `enter-pssession` .
4. Se houver um firewall entre o Azure e o local, confirme se ele está configurado para permitir o tráfego UDP na porta selecionada (padrão 4789). Use uma ferramenta como ctsTraffic para configurar um ouvinte e um remetente. Verifique se o tráfego pode ser enviado em ambas as direções na porta especificada.
5. Use pktmon para verificar se os pacotes estão sendo enviados e recebidos conforme o esperado. Execute pktmon em cada dispositivo virtual:

```powershell
Pktmon start –etw
```

6. Execute a configuração de rede estendida do Azure e, em seguida, interrompa o rastreamento:

```powershell
Pktmon stop
Netsh trace convert input=<path to pktmon etl file>
```

7. Abra o arquivo de texto que é produzido de cada dispositivo virtual e pesquise o tráfego UDP na porta especificada (padrão 4789). Se você vir o tráfego enviado da solução de virtualização local, mas não recebido pelo dispositivo virtual do Azure, você precisará verificar o roteamento e o firewall entre os dispositivos. Se você vir o tráfego enviado do local para o Azure, você deverá ver o dispositivo virtual do Azure enviar um pacote em resposta. Se esse pacote nunca for recebido pelo dispositivo virtual local, você precisará verificar se o roteamento está correto e não há um firewall bloqueando o tráfego entre eles.

### <a name="diagnosing-the-data-path-after-initial-configuration"></a>Diagnosticando o caminho de dados após a configuração inicial

Quando a rede estendida do Azure é configurada, problemas adicionais que você pode encontrar normalmente são devido a firewalls bloqueando o tráfego ou a MTU excedida se a falha for intermitente.

1. Verifique se ambos os dispositivos virtuais estão em execução.
2. Verifique se o agente de rede estendida do Azure está em execução em cada um dos dispositivos virtuais:

```powershell
get-service extnwagent
```

3. Se o status não estiver em execução, você poderá iniciá-lo com:

```powershell
start-service extnwagent
```

4. Use packetmon conforme descrito na etapa 5 acima, enquanto o tráfego é enviado entre duas VMs na rede estendida para verificar se o tráfego é recebido pelos dispositivos virtuais, enviado pela porta UDP configurada e, em seguida, recebido e encaminhado por outro dispositivo virtual.
