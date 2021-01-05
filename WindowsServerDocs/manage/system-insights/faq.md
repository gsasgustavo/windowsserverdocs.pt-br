---
title: Perguntas frequentes do System insights
description: Perguntas frequentes do System insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: f522623fa88c5ea979d405be013fa26937c658f1
ms.sourcegitcommit: 5f234fb15c1d0365b60e83a50bf953e317d6239c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97879825"
---
# <a name="system-insights-faq"></a>Perguntas frequentes do System insights

>Aplica-se a: Windows Server 2019

## <a name="how-can-you-use-system-insights-with-azure-monitor-or-system-center-operations-manager"></a>Como você pode usar as informações do sistema com Azure Monitor ou System Center Operations Manager?

[Azure monitor](https://azure.microsoft.com/services/monitor/) e [System Center Operations Manager](/system-center/scom/welcome?view=sc-om-1807&preserve-view=true) fornecem informações operacionais em suas implantações para ajudá-lo a gerenciar sua infraestrutura. O System insights, por outro lado, é um recurso do Windows Server que apresenta recursos de análise preditiva local. Juntos, o System insights e o Azure Monitor ou o SCOM podem ajudar a trazer as previsões em uma população de dispositivos:

 Azure Monitor ou SCOM podem deschavear os eventos criados pelo System insights, uma vez que o System insights gera o resultado de cada Previsão para o log de eventos. Eles podem trazer essas previsões específicas de computador por uma frota de servidores Windows, permitindo que você tenha uma exibição unificada dessas previsões em um grupo de instâncias de servidor.

 Consulte as IDs de canal e de evento para cada previsão [aqui](./managing-capabilities.md#retrieving-capability-results).

## <a name="how-does-system-insights-relate-to-windows-ml"></a>Como o System insights está relacionado ao Windows ML?

O [Windows ml](/windows/uwp/machine-learning/) é uma plataforma que permite aos desenvolvedores importar e pontuar modelos de aprendizado de máquina pré-treinados em dispositivos Windows. Esses modelos se beneficiam da aceleração de hardware e podem ser pontuados localmente.

O System insights é um recurso do Windows Server 2019 que oferece recursos de previsão locais juntamente com uma experiência de gerenciamento completa, incluindo a integração do PowerShell e do centro de administração do Windows.

## <a name="can-i-use-system-insights-for-my-cluster"></a>Posso usar o System insights para o meu cluster?

Sim. O System insights pode ser executado de forma independente em cada nó de cluster de failover individual, e o comportamento padrão de insights do sistema prevê o uso entre o armazenamento local, o volume, a CPU e a rede. **Você também pode habilitar a previsão de armazenamento em cluster** para que os recursos de previsão de armazenamento prevejam o uso de volumes e armazenamento clusterizados.

Você pode gerenciar essas configurações no centro de administração do Windows ou no PowerShell, e informações mais detalhadas sobre essa funcionalidade estão disponíveis [aqui](https://blogs.technet.microsoft.com/filecab/2018/10/03/using-system-insights-to-forecast-clustered-storage-usage/).


## <a name="how-expensive-is-it-to-run-the-default-capabilities"></a>Quão caro é a execução dos recursos padrão?

Cada funcionalidade padrão é barata para ser executada. Cada recurso levará mais tempo para ser executado à medida que você coletar mais dados, mas eles normalmente devem ser concluídos em apenas alguns segundos.

## <a name="additional-references"></a>Referências adicionais
Para saber mais sobre o System insights, use os seguintes recursos:

- [Visão geral dos insights do sistema](overview.md)
- [Noções básicas dos recursos](understanding-capabilities.md)
- [Gerenciar recursos](managing-capabilities.md)
- [Adicionar e desenvolver recursos](adding-and-developing-capabilities.md)
