---
title: Monitor de pacotes (Pktmon)
description: Este tópico fornece uma visão geral da ferramenta de diagnóstico de rede do monitor de pacotes (Pktmon).
ms.topic: overview
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 3db2bcf2719c3cfb5430d8feb8fcac1684578452
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632387"
---
# <a name="packet-monitor-pktmon"></a>Pktmon do monitor de pacotes \(\)

>Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

O monitor de pacotes (Pktmon) é uma ferramenta de diagnóstico de rede entre componentes para Windows. Ele pode ser usado para captura de pacotes, detecção de pacotes drop, filtragem de pacotes e contagem. A ferramenta é especialmente útil em cenários de virtualização, como rede de contêineres e SDN, pois fornece visibilidade dentro da pilha de rede. Ele está disponível na caixa por meio do comando pktmon.exe e por meio de extensões do centro de administração do Windows. 

## <a name="overview"></a>Visão geral

Qualquer computador que se comunique pela rede tem pelo menos um adaptador de rede. Todos os componentes entre esse adaptador e um aplicativo formam uma pilha de rede: um conjunto de componentes de rede que processam e movem o tráfego de rede. Em cenários tradicionais, a pilha de rede é pequena e todos os roteamentos e comutadores de pacotes ocorrem em dispositivos externos.

<center>

:::image type="content" source="media/networking-stack.png" alt-text="Pilha de rede em cenários tradicionais" border="false":::

</center>

No entanto, com o advento da virtualização de rede, o tamanho da pilha de rede foi multiplicado. Essa pilha de rede estendida agora inclui componentes como o comutador virtual que lida com o processamento e a alternância de pacotes. Esse ambiente flexível permite uma maior utilização de recursos e isolamento de segurança, mas também deixa mais espaço para erros de configuração que podem ser difíceis de diagnosticar. O monitor de pacotes fornece a visibilidade aprimorada na pilha de rede que geralmente é necessária para identificar esses erros.

<center>

:::image type="content" source="media/packet-capture.png" alt-text="Captura de pacotes entre componentes do PacketMon" border="false":::

</center>

O monitor de pacotes intercepta os pacotes em vários locais em toda a pilha de rede, expondo a rota do pacote. Se um pacote foi descartado por um componente com suporte na pilha de rede, o monitor de pacotes relatará esse descarte de pacotes. Isso permite que os usuários diferenciem entre um componente que é o destino pretendido para um pacote e um componente que está interferindo com um pacote. Além disso, o monitor de pacotes relatará os motivos de remoção; por exemplo, MTU Mistmatch, ou VLAN filtrada, etc. Esses motivos de eliminação fornecem a causa raiz do problema sem a necessidade de esgotar todas as possibilidades. O monitor de pacotes também fornece contadores de pacotes para cada ponto de intercepção, permitindo um exame de fluxo de pacotes de alto nível sem a necessidade de análise de log demorada.

<center>

:::image type="content" source="media/drop-detection.png" alt-text="Detecção de remoção do PacketMon" border="false":::

</center>

## <a name="functionality"></a>Funcionalidade

A funcionalidade do monitor de pacotes evoluiu por meio de versões do Windows. A tabela a seguir mostra seus principais recursos e a versão correspondente do Windows.

| Funcionalidade                                                                  | RS5 (17763) | 19H1 (18362) | Vibranium (19041) |
|:---------------------------------------------------------------------------:|:-----------:|:------------:|:-----------------:|
| Monitoramento e contagem de pacotes em vários locais ao longo da pilha de rede | &#x2611;    | &#x2611;     | &#x2611;          |
| Detecção de pacotes Drop em vários locais de pilha                          | &#x2611;    | &#x2611;     | &#x2611;          |
| Filtragem de pacotes em tempo de execução flexível                                           | &#x2611;    | &#x2611;     | &#x2611;          |
| Suporte a encapsulamento                                                       | &#x2610;    | &#x2611;     | &#x2611;          |
| Análise de rede baseada na análise de pacotes TcpDump                            | &#x2610;    | &#x2611;     | &#x2611;          |
| Análise de metadados de pacote (OOB)                                              | &#x2610;    | &#x2610;     | &#x2611;          |
| Monitoramento de pacotes na tela em tempo real                                       | &#x2610;    | &#x2610;     | &#x2611;          |
| Registro em log na memória de alto volume                                               | &#x2610;    | &#x2610;     | &#x2611;          |
| Suporte para o Wireshark e o formato de Monitor de Rede                                | &#x2610;    | &#x2610;     | &#x2611;          |

>[!NOTE]
>Azure Stack o HCI e os clientes do hub de Azure Stack devem esperar a funcionalidade vibranium.

## <a name="limitations"></a>Limitações

Abaixo estão algumas das limitações mais significativas do monitor de pacotes.

- O suporte a mídia sem fio está disponível somente em builds de ferro
- Nenhuma integração de firewall
- Drop Reporting só está disponível para componentes integrados

## <a name="get-started-with-packet-monitor"></a>Introdução ao monitor de pacotes

Os recursos a seguir estão disponíveis para ajudá-lo a começar a usar o monitor de pacotes.

### <a name="pktmon-command-syntax-and-formatting"></a>[Sintaxe e formatação do comando Pktmon](pktmon-syntax.md)

O monitor de pacotes está disponível na caixa por meio do comando pktmon.exe no sistema operacional vibranium (Build 19041). Você pode [usar este tópico](pktmon-syntax.md) para aprender a entender a sintaxe, os comandos, a formatação e a saída do pktmon.

### <a name="packet-monitoring-extension-in-windows-admin-center"></a>[Extensão de monitoramento de pacotes no centro de administração do Windows](pktmon-wac-extension.md)

A extensão de monitoramento de pacotes permite que você opere e consuma o monitor de pacotes por meio do centro de administração do Windows. A extensão ajuda você a diagnosticar sua rede capturando e exibindo o tráfego de rede por meio da pilha de rede em um log que é fácil de seguir e manipular. Você pode [usar este tópico](pktmon-wac-extension.md) para aprender a operar a ferramenta e a entender sua saída.

### <a name="sdn-data-path-diagnostics-extension-in-windows-admin-center"></a>[Extensão de diagnóstico de caminho de dados SDN no centro de administração do Windows](pktmon-sdn-data-path-wac-extension.md)

O diagnóstico de caminho de dados SDN é uma ferramenta dentro da extensão de monitoramento de SDN do centro de administração do Windows. A ferramenta automatiza capturas de pacotes baseadas em monitor de pacotes de acordo com vários cenários de SDN e apresenta a saída em uma única exibição que é fácil de seguir e manipular. Você pode [usar este tópico](pktmon-sdn-data-path-wac-extension.md) para aprender a operar a ferramenta e a entender sua saída.

### <a name="microsoft-network-monitor-netmon-support"></a>[Suporte ao Monitor de Rede da Microsoft (Netmon)](pktmon-netmon-support.md)

O monitor de pacotes gera logs no formato ETL. Esses logs podem ser analisados usando o Monitor de Rede da Microsoft (Netmon) usando analisadores especiais. [Este tópico](pktmon-netmon-support.md) explica como analisar arquivos ETL gerados pelo monitor de pacotes no Netmon.

### <a name="wireshark-pcapng-format-support"></a>[Suporte do Wireshark (formato pcapng)](pktmon-pcapng-support.md)

O monitor de pacotes pode converter logs em formato pcapng. Esses logs podem ser analisados usando o Wireshark (ou qualquer analisador de pcapng). [Este tópico](pktmon-pcapng-support.md) explica a saída esperada e como aproveitá-la.

## <a name="provide-feedback-to-engineering-team"></a>Fornecer comentários à equipe de engenharia

Relate quaisquer bugs ou envie comentários por meio do hub de comentários usando as seguintes etapas:

1. Inicie o  **Hub de comentários**   por meio do menu **Iniciar** .

1. Selecione o botão **relatar um problema** ou o botão **sugerir um recurso** .

1. Forneça um título de feedback significativo na caixa **resumir seu problema**   .

1. Forneça detalhes e etapas para reproduzir o problema na caixa **nos fornecer mais detalhes**   .

1. Selecione  **rede e Internet**   como a categoria superior e, em seguida, **Monitor de pacotes (pktmon.exe)** como a subcategoria.

1. Para nos ajudar a identificar e corrigir o bug mais rapidamente, Capture capturas de tela, anexe o log de saída do pktmon e/ou recrie o problema.

1. Clique em **Enviar**.

Depois de enviar o feedback/bug, a equipe de engenharia poderá dar uma olhada nos comentários e solucioná-los.
