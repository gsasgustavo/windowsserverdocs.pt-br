---
title: O backup das máquinas virtuais deve ser feito pelo menos uma vez a cada semana
description: Saiba o que fazer quando uma ou mais máquinas virtuais não tiverem sido submetidas a backup na última semana.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
ms.date: 8/16/2016
ms.openlocfilehash: 9c2cc7836eca57b5d7ae7e180a8af5c6e3104996
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846291"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>O backup das máquinas virtuais deve ser feito pelo menos uma vez a cada semana

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Erro|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*Uma ou mais máquinas virtuais não foram submetidas a backup na última semana.*

## <a name="impact"></a>Impacto
*Uma perda significativa de dados poderá ocorrer se a máquina virtual encontrar um problema e um backup recente não existir. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Agende um backup das máquinas virtuais para ser executado pelo menos uma vez por semana. Você poderá ignorar essa regra se essa máquina virtual for uma réplica e sua máquina virtual primária estiver sendo submetida a backup, ou se esta for a máquina virtual primária e sua réplica estiver sendo submetida a backup.*



