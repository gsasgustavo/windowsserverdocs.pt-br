---
title: Todos os adaptadores de rede virtual devem ser habilitados
description: Saiba o que fazer quando um ou mais adaptadores de rede virtual associados a um adaptador de rede física estiverem desabilitados no sistema operacional de gerenciamento.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: b17d647d-a34a-44de-ada6-01a2bf5eeb48
ms.date: 8/16/2016
ms.openlocfilehash: 6b3fcd786a1f7f294b7c35a4dc0a8b3cf0971c83
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834751"
---
# <a name="all-virtual-network-adapters-should-be-enabled"></a>Todos os adaptadores de rede virtual devem ser habilitados

>Aplica-se a: Windows Server 2016



|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema

*Um ou mais adaptadores de rede virtual associados a um adaptador de rede física estão desabilitados no sistema operacional de gerenciamento.*

## <a name="impact"></a>Impacto

*A configuração deste servidor não é a ideal.*

O sistema operacional de gerenciamento não pode se conectar a uma rede física (externa) usando um dos adaptadores de rede física neste computador porque ele está associado a um adaptador de rede virtual desabilitado.

## <a name="resolution"></a>Resolução

*Use as configurações de rede & Internet para habilitar o adaptador de rede virtual. Ou use o Gerenciador de comutador virtual para reconfigurar o comutador virtual externo para que ele não seja compartilhado com o sistema operacional de gerenciamento.*



