---
description: 'Saiba mais sobre: alterar a ilustração na página de entrada do AD FS'
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: Alterar a ilustração na página de entrada AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 30f6b4cc31869b06f57939123b5feca9371715a3
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97040214"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>Alterar a ilustração na página de entrada AD FS

## <a name="change-the-illustration"></a>Alterar a ilustração

Para alterar a ilustração, o gráfico à esquerda, que é exibido na página de entrada \- , use o seguinte cmdlet e sintaxe do Windows PowerShell.

![alterar ilustração](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

> [!IMPORTANT]
> Recomendamos que as dimensões para a ilustração sejam de 1420x1080 pixels a 96 DPI com um arquivo que não exceda o tamanho de 200 KB.

```powershell
Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}
```

## <a name="additional-references"></a>Referências adicionais

[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
