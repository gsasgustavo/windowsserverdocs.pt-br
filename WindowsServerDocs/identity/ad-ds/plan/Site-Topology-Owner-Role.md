---
description: 'Saiba mais sobre: função do proprietário da topologia de site'
ms.assetid: af76ddbe-83a2-4a62-9989-873e3bb1c772
title: Função de proprietário da topologia do site
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 4cac0905993b1e1b750cdbc9e0a64d17c2637cd6
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049254"
---
# <a name="site-topology-owner-role"></a>Função de proprietário da topologia do site

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

O administrador que gerencia a topologia do site é conhecido como o proprietário da topologia do site. O proprietário da topologia de site compreende as condições da rede entre os sites e tem autoridade para alterar as configurações em Active Directory Domain Services (AD DS) para implementar alterações na topologia do site. As alterações na topologia do site afetam as alterações na topologia de replicação. As responsabilidades do proprietário da topologia de site incluem:

-   Controle de alterações na topologia do site se a conectividade de rede mudar.

-   Obtenção e manutenção de informações sobre conexões de rede e roteadores do grupo de rede. O proprietário da topologia do site deve manter uma lista de endereços de sub-rede, máscaras de sub-rede e o local ao qual cada um pertence. O proprietário da topologia do site também deve entender quaisquer problemas sobre a velocidade da rede e a capacidade que afetam a topologia do site para definir efetivamente os custos para links de site.

-   Mover Active Directory objetos de servidor que representam controladores de domínio entre sites se o endereço IP de um controlador de domínio for alterado para uma sub-rede diferente em um site diferente, ou se a própria sub-rede for atribuída a um site diferente. Em ambos os casos, o proprietário da topologia do site deve mover manualmente o objeto do Active Directory Server do controlador de domínio para o novo site.



