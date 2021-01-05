---
description: 'Saiba mais sobre: avaliando AD DS exemplos de estratégia de implantação'
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: Avaliar exemplos de estratégia de implantação do AD DS
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 5612bc24e3f0662103aae1d831578c7417cc578e
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711791"
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>Avaliar exemplos de estratégia de implantação do AD DS

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Considere o exemplo a seguir de uma empresa fictícia, Contoso Pharmaceuticals, que está implantando Active Directory Domain Services (AD DS) em seu ambiente. O ambiente da Contoso consiste em quatro domínios. O nível funcional da floresta é o Windows Server 2003. A ilustração a seguir mostra a estrutura de domínio atual para a organização Contoso.

![Ilustração que mostra a estrutura de domínio atual para a organização Contoso.](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)

Depois de examinar seu ambiente existente e identificar suas metas de implantação, a Contoso estabeleceu a seguinte estratégia de implantação de AD DS:

-   Atualize domínios do Windows Server 2003 para domínios do Windows Server 2008.

-   Habilite recursos de AD DS avançados elevando os níveis funcionais de domínio e floresta para o Windows Server 2008.

-   Reestruture o domínio africa.concorp.contoso.com dentro da floresta para consolidar esse domínio com o domínio EMEA. concorp. contoso. con.

Aumentar o nível funcional da floresta para o Windows Server 2008 permitirá que a contoso Aproveite ao máximo os novos recursos de AD DS. Reestruturar os domínios dentro da floresta, conforme mostrado na ilustração a seguir, reduzirá a quantidade de administração necessária para gerenciar os domínios.

![Estratégia de implantação de AD DS](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)



