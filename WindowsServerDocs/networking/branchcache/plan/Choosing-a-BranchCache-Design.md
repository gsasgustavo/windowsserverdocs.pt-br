---
title: Escolher um design para o BranchCache
description: Saiba como saber mais sobre os modos de BranchCache e para selecionar os melhores modos para sua implantação.
ms.topic: how-to
ms.assetid: 86c1ccad-2aa4-40fe-84c1-f77c49eb1216
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: 972f2941afa2544307933ec422eb40578e084672
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946702"
---
# <a name="choosing-a-branchcache-design"></a>Escolher um design para o BranchCache

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para saber mais sobre os modos de BranchCache e para selecionar os melhores modos para sua implantação.

Você pode usar este guia para implantar o BranchCache nos modos e combinações de modo a seguir.

-   Todas as filiais são configuradas para o modo de cache distribuído.

-   Todas as filiais são configuradas para o modo de cache hospedado e têm um servidor de cache hospedado no site.

-   Algumas filiais estão configuradas para o modo de cache distribuído e algumas filiais têm um servidor de cache hospedado no site e são configuradas para o modo de cache hospedado.

A ilustração a seguir descreve uma instalação de modo duplo, com uma filial configurada para o modo de cache distribuído e uma filial configurada para o modo de cache hospedado.

![Escolher um design do BranchCache](../../media/Choosing-a-BranchCache-Design/bc_new_modes.jpg)

Antes de implantar o BranchCache, selecione o modo que você prefere para cada filial em sua organização.



