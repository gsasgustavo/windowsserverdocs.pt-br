---
title: Extensão de diagnóstico de caminho de dados SDN no centro de administração do Windows
description: Use este tópico para automatizar capturas de pacotes baseadas no monitor de pacotes com a extensão de diagnóstico de caminho de dados SDN no centro de administração do Windows
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 9b1a247e0d07a4e44ba7640aa2e95180956ccee8
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632385"
---
# <a name="sdn-data-path-diagnostics-extension-in-windows-admin-center"></a>Extensão de diagnóstico de caminho de dados SDN no centro de administração do Windows

>Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

O diagnóstico de caminho de dados SDN é uma ferramenta dentro da extensão de monitoramento de SDN do centro de administração do Windows que automatiza capturas de pacotes baseadas em monitor de pacote de acordo com vários cenários de SDN e apresenta a saída em uma única exibição que é fácil de seguir e manipular.

## <a name="what-is-packet-monitor-pktmon"></a>O que é o monitor de pacotes (Pktmon)?
O monitor de pacotes (Pktmon) é uma ferramenta de diagnóstico de rede entre componentes para Windows. Ele pode ser usado para captura de pacotes, detecção de pacotes de eliminação, filtragem de pacotes e contagem. A ferramenta é especialmente útil em cenários de virtualização, como rede de contêineres e SDN, pois fornece visibilidade dentro da pilha de rede.

## <a name="what-is-windows-admin-center"></a>O que é o Windows Admin Center?
O centro de administração do Windows é uma ferramenta de gerenciamento baseada em navegador, implantada localmente, que permite que você gerencie seus servidores Windows sem dependências do Azure ou da nuvem. O Windows Admin Center oferece controle total sobre todos os aspectos da infraestrutura de servidor e é particularmente útil para gerenciar servidores em redes privadas que não estejam conectadas à Internet. O Windows Admin Center é a evolução moderna das ferramentas de gerenciamento "nativas", como o Gerenciador de Servidores e o MMC.

## <a name="before-you-start"></a>Antes de começar
- Para usar a ferramenta, o servidor de destino precisa estar executando o Windows Server 2019 versão 1903 (19H1) e superior.
- [Instale o centro de administração do Windows](/windows-server/manage/windows-admin-center/deploy/install).
- Adicionar um cluster ao centro de administração do Windows:
  1. Clique em **+ Adicionar** em **todas as conexões**.
  2. Escolha Adicionar uma Hyper-Converged conexão de cluster.
  3. Digite o nome do cluster e, se solicitado, as credenciais a serem usadas.
  4. Marque **Configurar o controlador de rede** para continuar.
  5. Insira o URI do controlador de rede e clique em **validar**.
  6. Clique em **Adicionar** para concluir.

O cluster será adicionado à lista de conexões. Clique nele para iniciar o painel.

<center>

:::image type="content" source="media/add-sdn-enabled-hci-connection.png" alt-text="Adicionando uma conexão de HCI habilitada para SDN com o centro de administração do Windows" border="true":::

</center>

## <a name="getting-started"></a>Introdução

Para obter a ferramenta, navegue até o cluster que você criou na etapa anterior, depois para a extensão "SDN Monitoring" e, em seguida, para a guia "diagnóstico de caminho de dados".

## <a name="selecting-scenarios"></a>Selecionando cenários

A primeira página lista todos os cenários de SDN classificados como cenários de carga de trabalho e cenários de infraestrutura, conforme mostrado na imagem abaixo. Para iniciar, selecione o cenário de SDN que precisa ser diagnosticado.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-main-page.png" alt-text="Monitoramento de SDN-página cenários de diagnóstico" border="true":::

</center>

## <a name="scenario-parameters"></a>Parâmetros de cenário

Depois de escolher o cenário, preencha uma lista de parâmetros obrigatórios e opcionais para iniciar a captura. Esses parâmetros básicos indicarão a ferramenta para a conexão que precisa ser diagnosticada. Em seguida, a ferramenta usará esses parâmetros para consultas para executar uma captura bem-sucedida, sem nenhuma intervenção do usuário para descobrir o fluxo de pacotes esperado, os computadores envolvidos no cenário, sua localização no cluster ou os filtros de captura a serem aplicados em cada computador. Os parâmetros obrigatórios permitem que a captura seja executada e os parâmetros opcionais ajudam a filtrar alguns ruídos.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-scenario-parameters.png" alt-text="Monitoramento de SDN – página condições de captura" border="true":::

</center>

## <a name="capture-log"></a>Log de captura

Depois de iniciar a captura, a extensão mostrará uma lista de computadores em que a captura está sendo iniciada. Você poderá receber uma solicitação para entrar nessas máquinas se suas credenciais não tiverem sido salvas. Você pode começar a reproduzir o ping ou o problema que você está tentando diagnosticar capturando os pacotes relativos. Depois que os pacotes são capturados, a extensão mostrará as marcas ao lado dos computadores em que os pacotes foram capturados.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-loading-wheel2.png" alt-text="Iniciando a captura de pacotes" border="true":::

</center>

Depois de parar a captura, os logs de todos os computadores serão mostrados em uma única página, dividida pelo título da máquina. Cada título incluirá o nome do computador, sua função no cenário e seu host no caso de VMs (máquinas virtuais).

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-log.png" alt-text="Log de diagnóstico de caminho de dados após parar a captura" border="true":::

</center>

Os resultados são exibidos em uma tabela que mostra os parâmetros principais dos pacotes capturados: timestamp, endereço IP de origens, porta de origem, endereço IP de destino, porta de destino, EtherType, protocolo, sinalizadores TCP, se o pacote foi descartado e o motivo da remoção.

   - O carimbo de data/hora de cada um desses pacotes também é um hiperlink que o redirecionará para uma página diferente, na qual você pode encontrar mais informações sobre o pacote selecionado. Consulte a seção de detalhes da página abaixo.
   - Todos os pacotes descartados têm um valor "verdadeiro" na guia **descartada** , um motivo de eliminação e são exibidos em texto vermelho para facilitar o Pinpoint.
   - Todas as guias podem ser classificadas em ordem crescente e decrescente.
   - Você pode procurar um valor em qualquer coluna no log usando a barra de pesquisa.
   - Você pode reiniciar a captura com os mesmos filtros escolhidos usando o botão **reiniciar** .

## <a name="details-page"></a>Página de detalhes

As informações nesta página são particularmente valiosas se você tiver problemas de propagação de pacotes incorretos ou problemas de configuração incorretas, pois você pode investigar o fluxo do pacote por meio de cada componente da pilha de rede. Para cada salto de pacote, há detalhes que incluem os parâmetros de pacote, bem como os detalhes do pacote bruto.

- Os saltos são agrupados com base nos componentes envolvidos. Cada adaptador e os drivers sobre ele são agrupados pelo nome do adaptador. Isso torna mais fácil acompanhar o pacote em um alto nível por meio desses títulos de grupo.
- Todos os pacotes removidos também serão exibidos em texto vermelho para facilitar o Pinpoint.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-details-page.png" alt-text="Página de detalhes de diagnóstico de caminho de dados" border="true":::

</center>

Selecione um salto para exibir mais detalhes. Em cenários de encapsulamento e NAT (conversão de endereços de rede), esse recurso permite que você veja a alteração do pacote à medida que ele passa pela pilha de rede e verifique se há problemas de configuração incorreta.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-details-page-with-pane1.png" alt-text="exibindo detalhes sobre um salto específico" border="true":::

</center>

Role para baixo para exibir detalhes de pacotes brutos:

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-details-page-with-pane-raw-packet1.png" alt-text="exibindo detalhes de pacotes brutos sobre um salto específico" border="true":::

</center>

## <a name="display-filters"></a>Filtros de exibição

Os filtros de exibição permitem filtrar o log depois de capturar os pacotes. Para cada filtro, você pode especificar parâmetros de pacote como endereços MAC, endereços IP, portas, EtherType e protocolo de transporte.

   - Filtros de exibição podem distinguir entre a origem e o destino de endereços IP, endereços MAC e portas.
   - Os filtros de exibição podem ser excluídos e editados depois de serem aplicados para alterar a exibição do log.
   - Os filtros de exibição são revertidos nos logs salvos.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-display-filters.png" alt-text="filtrando logs com filtros de exibição" border="true":::

</center>

## <a name="save"></a>Salvar

O botão salvar permite que você salve o log em seu computador local para análise adicional por meio de outras ferramentas. Os filtros de exibição serão revertidos no log salvo. Os logs podem ser salvos em vários formatos:

   - Formato ETL que pode ser analisado usando Monitor de Rede da Microsoft. Observação: [consulte esta página](pktmon-netmon-support.md) para obter mais informações.
   - Formato de texto que pode ser analisado usando qualquer editor de texto como TextAnalysisTool.NET.
   - Pcapng fomat, que pode ser analisado usando ferramentas como o Wireshark.
      - A maioria dos metadados do monitor de pacotes será perdida durante essa conversão. Observação: [consulte esta página](pktmon-pcapng-support.md) para obter mais informações.

<center>

:::image type="content" source="media/sdn-data-path-diagnostics-save.png" alt-text="Salvando logs localmente" border="true":::

</center>
