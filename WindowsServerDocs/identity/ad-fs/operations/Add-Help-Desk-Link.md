---
description: 'Saiba mais sobre: Adicionar link de suporte técnico'
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: Adicione link de suporte técnico
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: c806390687d5293feacd2575b10569504334914f
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044364"
---
# <a name="add-help-desk-link"></a>Adicione link de suporte técnico


## <a name="to-add-a-help-desk-link"></a>Para adicionar um link de suporte técnico
Para adicionar o link de suporte técnico que é exibido na página de entrada \- , use o cmdlet e a sintaxe do Windows PowerShell a seguir.

![Adicionar suporte técnico](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)


`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`


> [!IMPORTANT]
> O parâmetro `linkText` nesse cmdlet não é necessário, a menos que você use outro valor diferente do padrão, que é *Ajuda*. A vantagem de usar o padrão é que ele é localizado para todas as localidades de cliente. Depois de personalizar a página, a personalização terá prioridade; portanto, você deve personalizar todos os idiomas aos quais deseja dar suporte.


## <a name="additional-references"></a>Referências adicionais
[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
