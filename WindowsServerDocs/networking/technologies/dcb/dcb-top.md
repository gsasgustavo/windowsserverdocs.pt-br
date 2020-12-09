---
title: DCB (Data Center Bridging)
description: Você pode usar este tópico para obter informações introdutórias sobre a ponte do Data Center no Windows Server 2016.
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: eab47e24ad8c2bd5436b3516babee9237c3c80f3
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96865565"
---
# <a name="data-center-bridging-dcb"></a>DCB \(Data Center Bridging\)

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para obter informações introdutórias sobre a ponte do Data Center \( DCB \) .

O DCB é um conjunto de padrões IEEE de Instituto de engenheiros elétricos e eletrônicos \( \) que habilitam malhas convergentes no Data Center, onde o armazenamento, a rede de dados, o IPC de comunicação entre processos de cluster \- \( \) e o tráfego de gerenciamento compartilham a mesma infraestrutura de rede Ethernet.

>[!NOTE]
>Além deste tópico, a seguinte documentação do DCB está disponível
>
>- [Instalar o DCB no Windows Server 2016 ou no Windows 10](dcb-install.md)
>- [Gerenciar a ponte do Data Center (DCB)](dcb-manage.md)

O DCB fornece \- alocação de largura de banda baseada em hardware para um tipo específico de tráfego de rede e aprimora a confiabilidade do transporte Ethernet com o uso do \- controle de fluxo baseado em prioridade.

\-A alocação de largura de banda baseada em hardware será essencial se o tráfego ignorar o sistema operacional e for descarregado para um adaptador de rede convergido, que pode dar suporte a iSCSI da Internet Small Computer System \( \) , acesso remoto direto à memória \( RDMA \) sobre Ethernet ou Fiber Channel sobre Ethernet \( FCoE \) .

\-O controle de fluxo baseado em prioridade será essencial se o protocolo de camada superior, como Fiber Channel, assumir um transporte subjacente sem perdas.

## <a name="dcb-protocols-and-management-options"></a>Protocolos DCB e opções de gerenciamento

DCB consiste no conjunto de protocolos a seguir.

- Serviço de transmissão aprimorado \( ETS \) – IEEE 802.1 Qaz, que se baseia nos padrões 802.1 p e 802.1 q
- Controle de fluxo \( de prioridade PFC \) , IEEE 802.1 QBB
- DCB Exchange Protocol \( DCBX \) , IEEE 802.1 AB, como estendido no padrão 802.1 Qaz.

O protocolo DCBX permite que você configure o DCB em um comutador, que pode então configurar automaticamente um dispositivo final, como um computador executando o Windows Server 2016.

Se você preferir gerenciar o DCB de um comutador, não precisará instalar o DCB como um recurso no Windows Server 2016, no entanto, essa abordagem inclui algumas limitações.

Como DCBX só pode informar o adaptador de rede do host dos tamanhos de classe do ETS e a habilitação de PFC, no entanto, os hosts do Windows Server geralmente exigem que o DCB esteja instalado para que o tráfego seja mapeado para as classes do ETS.

Normalmente, os aplicativos do Windows não são projetados para participar de trocas de DCBX. Por isso, o host deve ser configurado separadamente dos comutadores de rede, mas com configurações idênticas.

Se você optar por gerenciar o DCB de um comutador, ainda poderá exibir as configurações no Windows Server 2016 usando comandos do Windows PowerShell.

##  <a name="important-dcb-functionality"></a>Funcionalidade de DCB importante

A lista a seguir resume a funcionalidade fornecida pelo DCB.

1. Fornece interoperabilidade entre \- adaptadores de rede compatíveis com DCB e \- comutadores compatíveis com DCB.

2. Fornece um transporte de Ethernet sem perdas entre um computador executando o Windows Server 2016 e seu comutador vizinho ativando \- o controle de fluxo baseado em prioridade no adaptador de rede.

3. Fornece a capacidade de alocar largura de banda a um controle de tráfego \( TC \) por porcentagem, em que o TC pode consistir em uma ou mais classes de tráfego que são diferenciadas pelos indicadores de prioridade de classe de tráfego 802.1 p \( \) .

4. Permite que os administradores do servidor ou administradores de rede atribuam um aplicativo a uma determinada classe de tráfego ou prioridade com base em protocolos bem conhecidos, porta TCP/UDP bem conhecida ou porta NetworkDirect usada por esse aplicativo.

5. Fornece gerenciamento de DCB por meio do Windows Server 2016 Instrumentação de Gerenciamento do Windows \( WMI \) e Windows PowerShell. Para obter mais informações, consulte a seção [comandos do Windows PowerShell para DCB](#bkmk_wps) mais adiante neste tópico, além dos tópicos a seguir.
    - [Componentes DCB fornecidos pelo sistema](/windows-hardware/drivers/network/system-provided-dcb-components)
    - [Requisitos de QoS de NDIS para ponte de data center](/windows-hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. Fornece gerenciamento de DCB por meio do Windows Server 2016 Política de Grupo.

7. Dá suporte à coexistência de soluções de QoS de qualidade de serviço do Windows Server 2016 \( \) .

>[!NOTE]
>Antes de usar qualquer RDMA sobre a \( versão de RoCE Ethernet convergida \) de RDMA, você deve habilitar o DCB. Embora não seja necessário para redes iWARP de protocolo RDMA de Internet de longa distância \( \) , os testes determinaram que todas as \- tecnologias RDMA baseadas em Ethernet funcionam melhor com o DCB. Por isso, você deve considerar o uso de DCB para implantações do iWARP RDMA. Para obter mais informações, consulte [acesso remoto direto à memória (RDMA) e Comutador incorporado (Set)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).

##  <a name="practical-applications-of-dcb"></a>Aplicativos práticos do DCB

Muitas organizações têm grandes \( \) \( instalações de San de rede de área de armazenamento de Fibre Channel FC \) para o serviço de armazenamento. A SAN em FC exige adaptadores de rede especiais em servidores e comutadores FC na rede. Essas organizações normalmente também usam adaptadores de rede Ethernet e comutadores.

Na maioria dos casos, o hardware de FC é significativamente mais caro de ser implantado do que o hardware Ethernet, o que resulta em grandes despesas de capital. Além disso, o requisito para adaptador de rede Ethernet e FC separado e hardware de switch requer espaço adicional, energia e capacidade de resfriamento em um datacenter, o que resulta em despesas operacionais adicionais e contínuas.

De uma perspectiva de custo, é vantajoso que muitas organizações mesclem sua tecnologia FC com sua \- solução de hardware baseada em Ethernet para fornecer serviços de rede de armazenamento e dados.

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>Usando o DCB para uma \- malha convergida baseada em Ethernet para armazenamento e rede de dados

Para organizações que já têm uma grande SAN FC, mas desejam migrar para fora do investimento adicional na tecnologia FC, o DCB permite que você crie uma malha convergida baseada em Ethernet para armazenamento e rede de dados. Uma malha convergida DCB pode reduzir o TCO do custo total de propriedade \( futuro \) e simplificar o gerenciamento.

Para hosters que já adotaram ou que planejam adotar, iSCSI como sua solução de armazenamento, o DCB pode fornecer \- reserva de largura de banda assistida por hardware para tráfego iSCSI para garantir o isolamento de desempenho. E ao contrário de outras soluções proprietárias, o DCB é baseado em padrões \- e, portanto, relativamente fácil de implantar e gerenciar em um ambiente de rede heterogêneo.

Uma \- implementação baseada no Windows Server 2016 do DCB alivia muitos dos problemas que podem ocorrer quando as soluções de malha convergidas são fornecidas por vários OEMs de fabricantes de equipamentos originais \( \) .

As implementações de soluções proprietárias fornecidas por vários OEMs não podem interoperar umas com as outras, podem ser difíceis de gerenciar e normalmente terão agendas de manutenção de software diferentes.

Por outro lado, o Windows Server 2016 DCB é \- baseado em padrões e você pode implantar e gerenciar o DCB em uma rede heterogênea.

## <a name="windows-powershell-commands-for-dcb"></a><a name="bkmk_wps"></a>Comandos do Windows PowerShell para DCB

Há comandos DCB do Windows PowerShell para o Windows Server 2016 e o Windows Server 2012 R2. Você pode usar todos os comandos para o Windows Server 2012 R2 no Windows Server 2016.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Comandos do Windows PowerShell 2016 do Windows Server para DCB

O tópico a seguir para o Windows Server 2016 fornece descrições e sintaxe de cmdlets do Windows PowerShell para toda a ponte de data center \( DCB a \) qualidade dos \( \) \- cmdlets específicos de QoS de serviço. Ela lista os cmdlets em ordem alfabética com base no verbo no início do cmdlet.

- [Módulo DcbQoS](/powershell/module/dcbqos/)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Comandos do Windows PowerShell para DCB do Windows Server 2012 R2

O tópico a seguir para o Windows Server 2012 R2 fornece descrições e sintaxe de cmdlets do Windows PowerShell para toda a ponte de data center \( DCB a \) qualidade dos \( \) \- cmdlets específicos de QoS de serviço. Ela lista os cmdlets em ordem alfabética com base no verbo no início do cmdlet.

- [Cmdlets de Qualidade de Serviço (QoS) de Ponte de Datacenter no Windows PowerShell](/powershell/module/dcbqos/)
