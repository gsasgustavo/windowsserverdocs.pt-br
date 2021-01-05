---
title: Extensão de monitoramento de pacotes no Windows Admin Center
description: Use esta página para operar e consumir o monitor de pacotes (Pktmon) por meio do centro de administração do Windows.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: eabcda1c535086472fda55136b14073ce6181d36
ms.sourcegitcommit: b0c10eaffaa5de3eeff44c433580b41270c27d32
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/30/2020
ms.locfileid: "97826189"
---
# <a name="packet-monitoring-extension-in-windows-admin-center"></a>Extensão de monitoramento de pacotes no Windows Admin Center

>Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

A extensão de monitoramento de pacotes permite que você opere e consuma o monitor de pacotes por meio do centro de administração do Windows. A extensão ajuda você a diagnosticar sua rede capturando e exibindo o tráfego de rede por meio da pilha de rede em um log que é fácil de seguir e manipular.

## <a name="what-is-packet-monitor-pktmon"></a>O que é o monitor de pacotes (Pktmon)?
O monitor de pacotes (Pktmon) é uma ferramenta de diagnóstico de rede entre componentes para Windows. Ele pode ser usado para captura de pacotes, detecção de pacotes drop, filtragem de pacotes e contagem. A ferramenta é especialmente útil em cenários de virtualização, como rede de contêineres e SDN, pois fornece visibilidade dentro da pilha de rede.

## <a name="what-is-windows-admin-center"></a>O que é o Windows Admin Center?
O centro de administração do Windows é uma ferramenta de gerenciamento baseada em navegador, implantada localmente, que permite que você gerencie seus servidores Windows sem dependências do Azure ou da nuvem. O Windows Admin Center oferece controle total sobre todos os aspectos da infraestrutura de servidor e é particularmente útil para gerenciar servidores em redes privadas que não estejam conectadas à Internet. O Windows Admin Center é a evolução moderna das ferramentas de gerenciamento "nativas", como o Gerenciador de Servidores e o MMC.

## <a name="before-you-start"></a>Antes de começar
- Para usar a ferramenta, o servidor de destino precisa estar executando o Windows Server 2019 versão 1903 (19H1) e superior.
- [Instale o centro de administração do Windows](/windows-server/manage/windows-admin-center/deploy/install).
- Adicionar um servidor ao centro de administração do Windows:
  1. Clique em **+ Adicionar** em **todas as conexões**.
  2. Escolha Adicionar uma conexão de servidor.
  3. Digite o nome do servidor e, se solicitado, as credenciais a serem usadas.
  4. Clique em **Enviar** para concluir.

O servidor será adicionado à sua lista de conexões na página **visão geral** .

## <a name="getting-started"></a>Introdução

Para obter a ferramenta, navegue até o servidor que você criou na etapa anterior e, em seguida, vá para a extensão "monitoramento de pacotes".

## <a name="applying-filters"></a>Aplicando filtros

É altamente recomendável aplicar filtros antes de iniciar qualquer captura de pacote, pois a solução de problemas de conectividade para um destino específico é mais fácil ao se concentrar em um único fluxo de pacotes. Por outro lado, capturar todo o tráfego de rede pode tornar a saída muito ruidosa para ser analisada. De acordo, a extensão o guiará primeiro ao painel filtros antes de iniciar a captura. Você pode ignorar essa etapa clicando em **Avançar** para iniciar a captura sem filtros. O painel filtros orienta você a adicionar filtros em 3 etapas.

1. Filtrando por componentes da pilha de rede

   Se você quiser capturar o tráfego que passa por apenas componentes específicos, a primeira etapa do painel filtros mostra o layout da pilha de rede para que você possa selecionar os componentes pelos quais filtrar. Esse também é um ótimo lugar para analisar e entender o layout da pilha de rede de seu computador.

   :::image type="content" source="media/filtering-by-networking-stack-components.png" alt-text="Exemplo de filtragem por componentes de pilha de rede" border="true" lightbox="media/filtering-by-networking-stack-components.png":::

2. Filtrando por parâmetros de pacote

   Para a segunda etapa, o painel permite que você filtre os pacotes por seus parâmetros. Para que um pacote seja relatado, ele deve corresponder a todas as condições especificadas em pelo menos um filtro; Há suporte para até 8 filtros ao mesmo tempo. Para cada filtro, você pode especificar parâmetros de pacote como endereços MAC, endereços IP, portas, EtherType, protocolo de transporte, ID de VLAN.

   - Quando dois MACs, IPs ou portas forem especificados, a ferramenta não fará distinção entre a origem ou o destino; Ele capturará os pacotes que têm os dois valores, seja como destino ou origem. No entanto, os filtros de exibição podem fazer essa distinção; consulte a seção [filtros de exibição](#display-filters) abaixo.
   - Para filtrar ainda mais os pacotes TCP, é possível fornecer uma lista opcional de sinalizadores TCP para correspondência. Os sinalizadores com suporte são FIN, SYN, RST, PSH, ACK, URG, ECE e CWR.
   - Se a caixa de **encapsulamento** estiver marcada, a ferramenta aplicará o filtro aos pacotes internos encapsulados, além do pacote externo. Os métodos de encapsulamento com suporte são VXLAN, GRE, NVGRE e IP-in-IP. A porta VXLAN personalizada é opcional e o padrão é 4789.

   :::image type="content" source="media/filtering-by-packet-parameters.png" alt-text="Exemplo de filtragem por parâmetros de pacote" border="true" lightbox="media/filtering-by-packet-parameters.png":::

3. Filtrando por status de fluxo de pacote

   O monitor de pacotes capturará o fluxo e os pacotes descartados por padrão. Para capturar somente em pacotes descartados, selecione **pacotes descartados**.

   :::image type="content" source="media/filtering-by-packet-flow-status.png" alt-text="Exemplo de filtragem por status de fluxo de pacotes" border="true" lightbox="media/filtering-by-packet-flow-status.png":::

   Posteriormente, um resumo de todas as condições de filtro selecionadas será exibido para revisão. Você poderá recuperar essa exibição depois de iniciar a captura por meio do botão **capturar condições** .

   :::image type="content" source="media/filters-review.png" alt-text="Como capturar somente pacotes descartados" border="true" lightbox="media/filters-review.png":::

## <a name="capture-log"></a>Log de captura

Os resultados são exibidos em uma tabela que mostra os parâmetros principais dos pacotes capturados: timestamp, endereço IP de origens, porta de origem, endereço IP de destino, porta de destino, EtherType, protocolo, sinalizadores TCP, se o pacote foi descartado e o motivo da remoção.

   - O carimbo de data/hora de cada um desses pacotes também é um hiperlink que o redirecionará para uma página diferente, na qual você pode encontrar mais informações sobre o pacote selecionado. Consulte a seção de detalhes da página abaixo.
   - Todos os pacotes eliminados têm um valor "verdadeiro" na guia **descartada** , um motivo de eliminação e são exibidos em texto vermelho para facilitar o Pinpoint.
   - Todas as guias podem ser classificadas em ordem crescente e decrescente.
   - Você pode pesquisar um valor em qualquer coluna no log usando a barra de pesquisa.
   - Você pode reiniciar a captura com os mesmos filtros escolhidos usando o botão **reiniciar** .

   :::image type="content" source="media/capture-log-result.png" alt-text="Exemplo de tabela de resultados do log de captura" border="true" lightbox="media/capture-log-result.png":::

## <a name="details-page"></a>Página de detalhes

Esta página apresenta um instantâneo do pacote conforme ele flui por cada componente da pilha de rede local. Essa exibição mostra o caminho do fluxo de pacotes e permite que você investigue como os pacotes são alterados conforme eles são processados por cada componente que eles passam.

   - Os instantâneos de pacote são agrupados por cada adaptador/pilha de comutador; ou seja, instantâneos de pacote capturados por um adaptador/comutador, seus drivers de filtro e seus drivers de protocolo serão agrupados sob o nome do adaptador/comutador. Isso fará com que seja mais fácil seguir o fluxo do pacote de um adaptador para o outro.
   - Quando um instantâneo é selecionado, mais detalhes sobre esse instantâneo específico são mostrados, incluindo os cabeçalhos de pacotes brutos.
   - Todos os pacotes eliminados têm um valor "verdadeiro" na guia **descartada** , um motivo de eliminação e são exibidos em texto vermelho para facilitar o Pinpoint.

   :::image type="content" source="media/details-page.png" alt-text="Exemplo de página de detalhes mostrando instantâneos de pacote" border="true" lightbox="media/details-page.png":::

## <a name="display-filters"></a>Filtros de exibição

Os filtros de exibição permitem filtrar o log depois de capturar os pacotes. Para cada filtro, você pode especificar parâmetros de pacote como endereços MAC, endereços IP, portas, EtherType e protocolo de transporte. Ao contrário dos filtros de captura:

   - Filtros de exibição podem distinguir entre a origem e o destino de endereços IP, endereços MAC e portas.
   - Os filtros de exibição podem ser excluídos e editados depois de serem aplicados para alterar a exibição do log.
   - Os filtros de exibição são revertidos nos logs salvos.

   :::image type="content" source="media/display-filters.png" alt-text="Tela de filtros de exibição" border="true" lightbox="media/display-filters.png":::

## <a name="save-feature"></a>Salvar recurso

O botão salvar permite que você salve o log no computador local, no computador remoto ou em ambos. Os filtros de exibição serão revertidos no log salvo.

   - Se o log for salvo em seu computador local, você poderá salvá-lo em vários formatos:
      - Formato ETL que pode ser analisado usando Monitor de Rede da Microsoft. Observação: consulte esta página para obter mais informações.
      - Formato de texto que pode ser analisado usando qualquer editor de texto como TextAnalysisTool.NET.
      - Pcapng fomat, que pode ser analisado usando ferramentas como o Wireshark.
         - A maioria dos metadados do monitor de pacotes será perdida durante essa conversão. [Confira esta página](pktmon-pcapng-support.md) para obter mais informações.

   :::image type="content" source="media/packet-monitoring-save-feature.png" alt-text="Salvando uma cópia local da captura" border="true" lightbox="media/packet-monitoring-save-feature.png":::

## <a name="open-feature"></a>Abrir recurso

O recurso abrir permitirá que você reabra qualquer um dos cinco últimos logs salvos para analisar por meio da ferramenta.

   :::image type="content" source="media/open.png" alt-text="Abrindo um log recente" border="true" lightbox="media/open.png":::