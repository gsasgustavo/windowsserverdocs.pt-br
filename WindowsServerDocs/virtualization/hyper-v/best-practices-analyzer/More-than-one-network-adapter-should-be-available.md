---
title: Mais de um adaptador de rede deve estar disponível
description: Saiba o que fazer quando o servidor é configurado com um adaptador de rede, que deve ser compartilhado pelo sistema operacional de gerenciamento e por todas as máquinas virtuais que exigem acesso a uma rede física.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
ms.date: 8/16/2016
ms.openlocfilehash: 4cf106b15d69079e860b5a76febbc0ab549b0f34
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846285"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>Mais de um adaptador de rede deve estar disponível

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, consulte [Analisador de Práticas Recomendadas](https://go.microsoft.com/fwlink/?LinkId=122786).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Erro|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema

*Esse servidor é configurado com um adaptador de rede, que deve ser compartilhado pelo sistema operacional de gerenciamento e por todas as máquinas virtuais que exigem acesso a uma rede física.*

## <a name="impact"></a>Impacto

*O desempenho da rede pode ser degradado no sistema operacional de gerenciamento.*

## <a name="resolution"></a>Resolução

*Adicione mais adaptadores de rede a este computador. Para reservar um adaptador de rede para uso exclusivo pelo sistema operacional de gerenciamento, não o configure para uso com uma rede virtual externa.*

Para obter informações sobre como adicionar um adaptador de rede ao computador, consulte a documentação do computador ou adaptador de rede. Em seguida, para reservar exclusivamente para o sistema operacional de gerenciamento, não conecte-o a um comutador virtual.



