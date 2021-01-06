---
title: Etapa 4 verificar a implantação multissite
description: Saiba como verificar se você configurou corretamente sua implantação multissite de acesso remoto.
manager: brianlic
ms.topic: article
ms.assetid: 345b676a-a397-4d51-9973-8b25bc05fa55
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 29c4c65673399b017716b2bfc299742f1d0c1307
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949192"
---
# <a name="step-4-verify-the-multisite-deployment"></a>Etapa 4 verificar a implantação multissite

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Este tópico descreve como verificar se você configurou corretamente sua implantação multissite de acesso remoto.

### <a name="to-verify-access-to-internal-resources-through-the-multisite-deployment"></a>Para verificar o acesso a recursos internos por meio da implantação multissite

1.  Conecte um computador cliente do DirectAccess à rede corporativa e obtenha a política de grupo.

2.  Conecte o computador cliente à rede externa e tentar acessar os recursos internos.

    Você deve conseguir acessar todos os recursos corporativos.

3.  Teste a conectividade por meio de cada servidor na implantação multissite desativando ou desconectando da rede externa, tudo, exceto um dos servidores de acesso remoto. No computador cliente, tente acessar os recursos corporativos. Repita o teste em um servidor multisite diferente. Pode levar até 10 minutos para que o computador cliente se conecte ao novo ponto de entrada. Isso ocorre porque a investigação é desativada por 10 minutos para um ponto de entrada depois que é considerada inacessível, para otimizar a largura de banda e a vida útil da bateria. Como alternativa, você pode alternar entre os vários pontos de entrada manualmente escolhendo o ponto de entrada desejado na caixa de combinação mostrada ao executar **daprop.exe**.

    Você deve ser capaz de acessar todos os recursos corporativos por meio de cada servidor multissite.

4.  Conecte um &reg;  computador cliente do Windows 7 à rede corporativa e obtenha a política de grupo.

5.  Conecte o computador cliente do Windows 7 à rede externa e tente acessar os recursos internos.

    Você deve conseguir acessar todos os recursos corporativos.

6.  Teste a conectividade para clientes do Windows 7 por meio de cada servidor na implantação multissite acessando o console Active Directory usuários e computadores e movendo o computador cliente para o grupo de segurança que corresponde a cada servidor. Depois que as alterações forem replicadas em todo o domínio, reinicie o computador cliente enquanto estiver conectado à rede corporativa para obter a nova política de grupo. Tentativa de acessar recursos corporativos. Repita o teste em um servidor multisite diferente.

    Você deve ser capaz de acessar todos os recursos corporativos por meio de cada servidor multissite.

    Em um ambiente de produção, esse método pode não ser viável devido à quantidade de tempo necessária para que as alterações sejam replicadas em todo o domínio. Talvez você queira forçar a replicação sempre que possível. O teste também pode ser feito de vários computadores cliente diferentes do Windows 7 que já são membros dos diferentes grupos de segurança do Windows 7 na implantação multissite.



