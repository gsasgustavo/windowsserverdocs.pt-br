---
title: Um ou mais adaptadores de rede devem ser configurados como a origem do espelhamento de porta
description: Saiba o que fazer quando uma ou mais máquinas virtuais têm um adaptador de rede configurado como um destino para espelhamento de porta, mas não há nenhuma origem correspondente no comutador virtual.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 147fd00f-1440-44d1-94e3-3a8af63aa7ed
ms.date: 8/16/2016
ms.openlocfilehash: 19e5d7cb571b11095e83dcb30aa818cbbd72b394
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846031"
---
# <a name="one-or-more-network-adapters-should-be-configured-as-the-source-for-port-mirroring"></a>Um ou mais adaptadores de rede devem ser configurados como a origem do espelhamento de porta

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>**Problema**
*Uma ou mais máquinas virtuais têm um adaptador de rede configurado como destino para o espelhamento de porta, mas não há nenhuma origem correspondente no comutador virtual.*

## <a name="impact"></a>**Impacto**
*O espelhamento de porta não funcionará corretamente para os seguintes comutadores virtuais e máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>**Resolução**
*Use o Windows PowerShell ou o Gerenciador do Hyper-V para concluir ou corrigir a configuração de espelhamento de porta.*



