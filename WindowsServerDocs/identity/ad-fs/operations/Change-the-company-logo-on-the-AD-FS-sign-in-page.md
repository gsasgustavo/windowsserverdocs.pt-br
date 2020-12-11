---
description: 'Saiba mais sobre: alterando o logotipo da empresa na página de entrada AD FS'
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: Alterando o logotipo da empresa na página de entrada AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.openlocfilehash: a04f7a81c26dea4234fbb92edc44125ae11e51f6
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97040274"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>Alterando o logotipo da empresa na página de entrada AD FS

## <a name="change-company-logo"></a>Altere o logotipo da empresa

Para alterar o logotipo da empresa que é exibido na página de entrada \- , use o cmdlet e a sintaxe do PowerShell do Windows PowerShell a seguir.

![alterar logotipo](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

> [!IMPORTANT]
> Recomendamos que as dimensões para o logotipo sejam de 260x35 a 96 DPI com um arquivo que não exceda o tamanho de 10 KB.

```powershell
Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}
```

> [!NOTE]
> O `TargetName` parâmetro é obrigatório. O tema padrão que é liberado com AD FS é denominado *padrão*.

## <a name="additional-references"></a>Referências adicionais

[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
