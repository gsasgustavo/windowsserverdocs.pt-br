---
title: Escolher unidades para Espaços de Armazenamento Diretos
description: Saiba mais sobre como escolher unidades para Espaços de Armazenamento Diretos.
ms.assetid: 1368bc83-9121-477a-af09-4ae73ac16789
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 07/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: b84b177a6f73da1a74caa2c715cafc3c776aae59
ms.sourcegitcommit: 528bdff90a7c797cdfc6839e5586f2cd5f0506b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97977481"
---
# <a name="choosing-drives-for-storage-spaces-direct"></a>Escolher unidades para Espaços de Armazenamento Diretos

> Aplica-se a: Windows Server 2019, Windows Server 2016

Este tópico fornece diretrizes sobre como escolher unidades para [Espaços de Armazenamento Diretos](storage-spaces-direct-overview.md) para atender às suas necessidades de desempenho e capacidade.

## <a name="drive-types"></a>Tipos de unidade

Espaços de Armazenamento Diretos atualmente funciona com quatro tipos de unidades:

| Tipo de unidade | Descrição |
| --- | --- |
| :::image type="content" source="media/understand-the-cache/pmem-100px.png" alt-text="Imagem do PMem (memória persistente)"::: | **Memória persistente.** Um novo tipo de armazenamento de baixa latência e alto desempenho. |
| :::image type="content" source="media/understand-the-cache/NVMe-100px.png" alt-text="Imagem de NVMe (memória não volátil Express)"::: | **NVMe (memória não volátil Express).** Unidades de estado sólido que ficam diretamente no barramento PCIe. Os fatores forma comuns são U.2 de 2,5", PCIe Add-In-Card (AIC) e M.2. O NVMe oferece IOPS e taxa de transferência de e/s maiores com latência menor do que qualquer outro tipo de unidade que damos suporte hoje, exceto a memória persistente. |
| :::image type="content" source="media/understand-the-cache/SSD-100px.png" alt-text="Imagem da unidade SSD)"::: | **SSD.** Unidades de estado sólido, que se conectam por meio de SATA ou SAS convencionais. |
| :::image type="content" source="media/understand-the-cache/HDD-100px.png" alt-text="Imagem do HDD)"::: | **HDD.** Unidades de disco rígido magnéticos, que oferecem grande capacidade de armazenamento. |

## <a name="built-in-cache"></a>Cache embutido

Os Espaços de Armazenamento Diretos têm um cache no servidor interno. Trata-se de um cache de leitura e gravação grande, persistente e em tempo real. Em implantações com vários tipos de unidades, ele é configurado automaticamente para usar todas as unidades do tipo "mais rápido". As unidades restantes são usadas para a capacidade.

Para obter mais informações, consulte [Noções básicas sobre o cache em Espaços de Armazenamento Diretos](understand-the-cache.md).

## <a name="option-1--maximizing-performance"></a>Opção 1 – maximizar o desempenho

Para obter latência previsível e uniforme de submilissegundos entre leituras aleatórias e gravações em qualquer dado, ou para obter IOPS alta (fizemos [mais de 6 milhões](https://www.youtube.com/watch?v=0LviCzsudGY&t=28m)!) ou taxa de transferência de e/s (fizemos [mais de 1 TB/s](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=16m50s)!), você deve ir para "todos-Flash".

Atualmente, há três maneiras de fazer isso:

![Todas as opções de implantação do flash para maximizar o desempenho](media/choosing-drives-and-resiliency-types/All-Flash-Deployment-Possibilities.png)

1. **Todos os NVMe.** Usar tudo NVMe oferece um desempenho incomparável, incluindo a baixa latência mais previsível. Se todas as unidades forem do mesmo modelo, não haverá cache. Você também pode combinar modelos NVMe de resistência superior e resistência inferior e configurar o primeiro para armazenar em cache as gravações do último ([requer configuração](understand-the-cache.md#manual-configuration)).

2. **NVMe + SSD.** Ao usar o NVMe com SSDs, o NVMe armazenará automaticamente as gravações em cache nos SSDs. Isso permite que as gravações sejam agrupadas em cache e desescalonadas somente conforme necessário, para reduzir o desgaste nos SSDs. Isso fornece características de gravação estilo NVMe, enquanto as leituras são fornecidas diretamente dos SSDs igualmente rápidos.

3. **Toda SSD.** Como na opção Tudo NVMe, não existe cache quando todas as unidades são do mesmo modelo. Combinando modelos de resistência superior e resistência inferior, você pode configurar o primeiro para armazenar em cache as gravações do último ([requer configuração](understand-the-cache.md#manual-configuration)).

    > [!NOTE]
    > Uma vantagem de usar tudo NVMe ou tudo SSD sem cache é que você obtém capacidade de armazenamento utilizável de cada unidade. Não há capacidade "gasta" no armazenamento em cache, o que pode ser atraente em menor escala.

## <a name="option-2--balancing-performance-and-capacity"></a>Opção 2 – balancear desempenho e capacidade

Para ambientes com vários aplicativos e cargas de trabalho, alguns com requisitos de desempenho rigorosos e outros que exigem uma capacidade considerável de armazenamento, você deve ir "híbrido" com o cache NVMe ou SSDs para HDDs maiores.

![Opções de implantação híbrida para balancear o desempenho e a capacidade](media/choosing-drives-and-resiliency-types/Hybrid-Deployment-Possibilities.png)

1. **NVMe + HDD**. As unidades NVMe aceleram as leituras e gravações armazenando ambas em cache. O armazenamento de leituras em cache permite que o HDDs foquem nas gravações. O armazenamento de gravações em cache absorve picos e permite que as gravações sejam agrupadas e desescalonadas somente conforme necessário, de maneira artificialmente serializada que maximiza a taxa de transferência de IOPS e E/S do HDD. Isso proporciona características de gravação estilo NVMe e, para dados lidos recentemente ou com frequência, características de leitura estilo NVMe também.

2. **SSD + HDD**. Semelhante ao especificado acima, o SSD acelera leituras e gravações armazenando ambas em cache. Isso proporciona características de gravação estilo SSD, bem como características de leitura estilo SSD para dados lidos recentemente ou com frequência.

    Há mais uma opção, em vez de exóticas: para usar unidades de *todos os três* tipos.

3. **NVMe + SSD + HDD.** Com unidades dos três tipos, as unidades NVMe armazenarão os dados em cache para os SSDs e HDDs. O apelo é que você pode criar volumes no SSDs e volumes nos HDDs, lado a lado no mesmo cluster, todos acelerados pelo NVMe. Os primeiros são exatamente como na implantação "tudo flash", e os últimos são exatamente como nas implantações "híbridas" descritas acima. Isso é conceitualmente como ter dois pools, com gerenciamento de capacidade amplamente independente, ciclos de falha e reparo e assim por diante.

    > [!IMPORTANT]
    > Recomendamos usar a camada SSD para colocar as cargas de trabalho mais dependentes de desempenho em all-flash.

## <a name="option-3--maximizing-capacity"></a>Opção 3 – maximizar a capacidade

Para cargas de trabalho que exigem grande capacidade e gravação com pouca frequência, como arquivamento, destinos de backup, data warehouses ou armazenamento "frio", você deve combinar alguns SSDs para cache com muitos HDDs maiores para a capacidade.

![Opções de implantação para maximizar a capacidade](media/choosing-drives-and-resiliency-types/maximizing-capacity.png)

1. **SSD + HDD**. Os SSDs armazenam leituras e gravações em cache para absorver picos e oferecer um desempenho de gravação estilo SSD, com desescalonamento otimizado posterior para os HDDs.

>[!IMPORTANT]
>Não há suporte para a configuração com HDDs somente. Não é recomendável o cache SSDs de endurance alto para SSDs Endurance baixo.

## <a name="sizing-considerations"></a>Considerações de dimensionamento

### <a name="cache"></a>Cache

Cada servidor deve ter pelo menos duas unidades de cache (o mínimo necessário para redundância). É recomendável que o número de unidades de capacidade seja um múltiplo do número de unidades de cache. Por exemplo, se você tiver quatro unidades de cache, ocorrerá um desempenho mais consistente com oito unidades de capacidade (taxa de 1:2) do que com 7 ou 9.

O cache deve ser dimensionado para acomodar o conjunto de trabalho de seus aplicativos e cargas de trabalho, por exemplo, todos os dados que eles estão lendo e gravando ativamente em um determinado momento. Não há qualquer requisito de dimensionamento de cache além desse. Para implantações com HDDs, um local de início justo é de 10% da capacidade, por exemplo, se cada servidor tiver 4 x 4 TB HDD = 16 TB de capacidade, então 2 x 800 GB SSD = 1,6 TB de cache por servidor. Para todas as implantações de flash, especialmente com alta Endurance] ( https://techcommunity.microsoft.com/t5/storage-at-microsoft/understanding-ssd-endurance-drive-writes-per-day-dwpd-terabytes/ba-p/426024) SSDs, pode ser justo começar mais perto de 5% da capacidade – por exemplo, se cada servidor tiver 24 x 1,2 TB SSD = 28,8 TB de capacidade, 2 x 750 GB NVMe = 1,5 TB de cache por servidor. Você pode adicionar ou remover unidades de cache posteriormente para ajustar.

### <a name="general"></a>Geral

É recomendável limitar a capacidade de armazenamento total por servidor a aproximadamente 400 terabytes (TB). Quanto maior a capacidade de armazenamento por servidor, mais tempo é necessário para ressincronizar os dados após a inatividade ou reinicialização, como na aplicação de atualizações de software. O tamanho máximo atual por pool de armazenamento é de 4 petabytes (PB) (4.000 TB) para o Windows Server 2019 ou 1 petabyte para Windows Server 2016.

## <a name="additional-references"></a>Referências adicionais

- [Visão geral dos Espaços de Armazenamento Diretos](storage-spaces-direct-overview.md)
- [Noções básicas sobre o cache nos Espaços de Armazenamento Diretos](understand-the-cache.md)
- [Requisitos de hardware Espaços de Armazenamento Diretos](storage-spaces-direct-hardware-requirements.md)
- [Planejamento de volumes nos Espaços de Armazenamento Diretos](plan-volumes.md)
- [Tolerância a falhas e eficiência de armazenamento](storage-spaces-fault-tolerance.md)
