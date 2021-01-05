---
title: Evite mapear um caminho de armazenamento para vários pools de recursos
description: Saiba o que fazer quando um caminho de arquivo de armazenamento é mapeado para vários pools de recursos.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
ms.date: 8/16/2016
ms.openlocfilehash: f39ea4da5a7b966a29b0ad943d40b02556c9460d
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834631"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>Evite mapear um caminho de armazenamento para vários pools de recursos

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
*Um caminho de arquivo de armazenamento é mapeado para vários pools de recursos.*

## <a name="impact"></a>**Impacto**
*Para o tipo de pool de armazenamento especificado, os seguintes pools pai e filho compartilham o mesmo caminho de armazenamento:*

\<list of pools>

## <a name="resolution"></a>**Resolução**
*Use o Windows PowerShell para reconfigurar os pools de recursos de armazenamento para que vários pools não usem o mesmo caminho de armazenamento.*



