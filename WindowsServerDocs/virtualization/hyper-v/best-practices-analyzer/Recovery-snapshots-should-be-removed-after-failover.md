---
title: Os instantâneos de recuperação devem ser removidos após o failover
description: Saiba o que fazer quando uma máquina virtual com failover tiver um ou mais instantâneos de recuperação.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 922115fa-e8dd-4055-aaf1-4a4437c5cf28
ms.date: 8/16/2016
ms.openlocfilehash: e37e59b8796913c2d46914834f4467e927f7e32b
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846274"
---
# <a name="recovery-snapshots-should-be-removed-after-failover"></a>Os instantâneos de recuperação devem ser removidos após o failover

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Operações|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>**Problema**
*Uma máquina virtual com failover tem um ou mais instantâneos de recuperação.*

## <a name="impact"></a>**Impacto**
*O espaço disponível pode ficar no disco físico que armazena os arquivos de instantâneo. Se isso ocorrer, nenhuma operação de disco adicional poderá ser executada no armazenamento físico. Qualquer máquina virtual que dependa do armazenamento físico poderá ser afetada. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>**Resolução**
*Para cada máquina virtual com failover, use o cmdlet Complete-VMFailover no Windows PowerShell para remover os instantâneos de recuperação e indicar a conclusão do failover.*



