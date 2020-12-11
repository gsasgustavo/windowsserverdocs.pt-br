---
description: 'Saiba mais sobre: Adicionar link inicial'
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: Adicione o link da página inicial
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 5f684ae3e68459721678a50c91cc04d58c89d81c
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97039344"
---
# <a name="add-home-link"></a>Adicione o link da página inicial

Para adicionar o link inicial que é exibido na página de entrada \- , use o seguinte cmdlet e sintaxe do Windows PowerShell.


![Adicionar link inicial](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)


`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home `


> [!IMPORTANT]
> O parâmetro `linkText` nesse cmdlet não é necessário, a menos que você use outro valor diferente do padrão, que é *Página Inicial*. A vantagem de usar o padrão é que ele é localizado para todas as localidades de cliente. Depois que a \- página de entrada é personalizada, a personalização tem precedência; portanto, você deve personalizar para todos os idiomas aos quais você deseja dar suporte.

## <a name="additional-references"></a>Referências adicionais
[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
