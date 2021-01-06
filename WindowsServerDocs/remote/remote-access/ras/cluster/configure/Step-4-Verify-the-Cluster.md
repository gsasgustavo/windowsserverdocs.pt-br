---
title: Etapa 4 verificar o cluster
description: Saiba como verificar se você configurou corretamente sua implantação de cluster do DirectAccess.
manager: brianlic
ms.topic: article
ms.assetid: f22dcf10-b453-4664-a9ef-e40e95c72f63
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 92f51a3b6fa00a06006223abe4f6d28bc40d744f
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947772"
---
# <a name="step-4-verify-the-cluster"></a>Etapa 4 verificar o cluster

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Este tópico descreve como verificar se você configurou corretamente sua implantação de cluster do DirectAccess.

### <a name="to-verify-access-to-internal-resources-through-the-cluster"></a>Para verificar o acesso a recursos internos por meio do cluster

1.  Conecte um computador cliente do DirectAccess à rede corporativa e obtenha a política de grupo.

2.  Conecte o computador cliente à rede externa e tentar acessar os recursos internos.

    Você deve conseguir acessar todos os recursos corporativos.

3.  Teste a conectividade por meio de cada servidor no cluster desativando ou desconectando da rede externa, tudo menos um dos servidores de cluster. No computador cliente, tente acessar os recursos corporativos. Repita o teste em um servidor de cluster diferente.

    Você deve ser capaz de acessar todos os recursos corporativos por meio de cada servidor de cluster.



