---
title: Evite usar pontos de verificação em uma máquina virtual que executa uma carga de trabalho de servidor em um ambiente de produção
description: Saiba o que fazer quando uma máquina virtual com um ou mais pontos de verificação for encontrada.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 1be75890-d316-495a-b9b7-be75fc1aac10
ms.date: 8/16/2016
ms.openlocfilehash: 0fef612d9da5ad74561429c3852d407623d9d334
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834561"
---
# <a name="avoid-using-checkpoints-on-a-virtual-machine-that-runs-a-server-workload-in-a-production-environment"></a>Evite usar pontos de verificação em uma máquina virtual que executa uma carga de trabalho de servidor em um ambiente de produção

>Aplica-se a: Windows Server 2016



*Para obter mais informações sobre práticas recomendadas e verificações, consulte* [analisador de práticas recomendadas](https://go.microsoft.com/fwlink/?LinkId=122786).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Operações|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

> [!NOTE]
> No Windows Server 2012 R2, os instantâneos de máquina virtual foram renomeados para pontos de verificação de máquina virtual no Gerenciador do Hyper-V para corresponder à terminologia usada no gerenciamento de máquinas virtuais do System Center. Para obter detalhes, consulte [visão geral de pontos de verificação e instantâneos](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn818483(v=ws.11)).

## <a name="issue"></a>Problema

*Uma máquina virtual com um ou mais pontos de verificação foi encontrada.*

## <a name="impact"></a>Impacto

*O espaço disponível pode ficar no disco físico que armazena os arquivos de pontos de verificação. Se isso ocorrer, nenhuma operação de disco adicional poderá ser executada no armazenamento físico. Qualquer máquina virtual que dependa do armazenamento físico poderá ser afetada.*

Se o espaço em disco físico for esgotado, qualquer máquina virtual em execução que tenha pontos de verificação ou discos rígidos virtuais armazenados nesse disco poderá ser pausada automaticamente. O Gerenciador do Hyper-V mostra o status dessas máquinas virtuais como em pausa-crítico.

## <a name="resolution"></a>Resolução

*Se a máquina virtual executar uma carga de trabalho de servidor em um ambiente de produção, coloque a máquina virtual offline e, em seguida, use o Gerenciador do Hyper-V para aplicar ou excluir os pontos de verificação. Para excluir pontos de verificação, você deve desligar a máquina virtual para concluir o processo.*

> [!NOTE]
> Os pontos de verificação de produção agora estão disponíveis como uma alternativa aos pontos de verificação padrão. Para obter detalhes, consulte [escolher entre pontos de verificação padrão ou de produção](../manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md).