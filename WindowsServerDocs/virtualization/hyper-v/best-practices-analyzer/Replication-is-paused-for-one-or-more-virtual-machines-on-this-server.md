---
title: A replicação está em pausa para uma ou mais máquinas virtuais neste servidor
description: Saiba o que fazer quando a replicação é pausada para uma ou mais máquinas virtuais. Enquanto a máquina virtual primária estiver pausada, as alterações que ocorrerem serão acumuladas e serão enviadas para a máquina virtual de réplica depois que a replicação for retomada.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: e1119a40-eda3-4058-8648-7df81cbc6c29
ms.date: 8/16/2016
ms.openlocfilehash: bc8a173773217ea00c47080ded74901f70384b2a
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846119"
---
# <a name="replication-is-paused-for-one-or-more-virtual-machines-on-this-server"></a>A replicação está em pausa para uma ou mais máquinas virtuais neste servidor

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Operações|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*A replicação está em pausa para uma ou mais máquinas virtuais. Enquanto a máquina virtual primária estiver pausada, as alterações que ocorrerem serão acumuladas e serão enviadas para a máquina virtual de réplica depois que a replicação for retomada.*

## <a name="impact"></a>Impacto
*Desde que a replicação seja pausada, as alterações acumuladas que ocorrerem na máquina virtual primária consumirão o espaço em disco disponível no servidor primário. Depois que a replicação é retomada, pode haver uma grande intermitência de tráfego de rede para o servidor de réplica. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Confirme se a pausa da replicação foi intencional. Se a replicação foi pausada para resolver o espaço em disco ou a conectividade de rede insuficiente, retome a replicação assim que esses problemas forem resolvidos.*



