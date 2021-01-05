---
title: Os discos rígidos virtuais com arquivos de paginação devem ser excluídos da replicação
description: Saiba o que fazer quando os arquivos de paginação experimentam um alto volume de atividade de entrada/saída, o que exigirá necessariamente recursos muito maiores para participar da replicação.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: c0be8a5f-64a1-488a-944e-bb913bb90517
ms.date: 8/16/2016
ms.openlocfilehash: c710891396ffe8914819796c18abaf0ddc41fea4
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845754"
---
# <a name="virtual-hard-disks-with-paging-files-should-be-excluded-from-replication"></a>Os discos rígidos virtuais com arquivos de paginação devem ser excluídos da replicação

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Informações|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*Os arquivos de paginação devem ser excluídos da participação na replicação, mas nenhum disco foi excluído.*

## <a name="impact"></a>Impacto
*Os arquivos de paginação experimentam um alto volume de atividade de entrada/saída, o que exigirá, desnecessariamente, recursos muito maiores para participar da replicação. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Se você ainda não tiver feito isso, crie um disco rígido virtual separado para o arquivo de paginação do Windows. Se a replicação inicial já tiver sido concluída, use o Gerenciador do Hyper-V para remover a replicação. Em seguida, configure a replicação novamente e exclua o disco rígido virtual com o arquivo de paginação da replicação.*



