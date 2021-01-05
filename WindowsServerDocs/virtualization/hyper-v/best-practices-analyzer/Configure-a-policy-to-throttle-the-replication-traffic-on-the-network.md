---
title: Configurar uma política para limitar o tráfego de replicação na rede
description: Saiba o que fazer quando pode não haver um limite na quantidade de largura de banda de rede que a replicação pode consumir.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
ms.date: 8/16/2016
ms.openlocfilehash: 69a03e85dd410f1f3b59daaf97ff97c2db5c7d48
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834841"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>Configurar uma política para limitar o tráfego de replicação na rede

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*Pode não haver um limite para a quantidade de largura de banda de rede que a replicação pode consumir.*

## <a name="impact"></a>Impacto
*A largura de banda da rede poderia se tornar totalmente dominada pelo tráfego de replicação, afetando outras atividades de rede críticas. Isso afeta as seguintes portas:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Se você usar outro método para limitar o tráfego de rede, poderá ignorá-lo. Caso contrário, use o editor de Política de Grupo para configurar uma política que limitará o tráfego de rede à porta relevante do servidor de réplica.*




