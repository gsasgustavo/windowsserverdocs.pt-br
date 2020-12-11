---
description: 'Saiba mais sobre: alterar o nome da empresa na página de entrada do AD FS'
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: Alterar o nome da empresa na página de entrada AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 907043517d56790cd4f6de49d67de5ed3905f0ad
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97040244"
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>Alterar o nome da empresa na página de entrada AD FS

Para alterar o nome da empresa que é exibida na página de entrada \- , use o seguinte cmdlet e sintaxe do Windows PowerShell. Esse valor é definido por padrão usando o valor do nome de exibição de Serviço de Federação que você digitou durante a configuração.

![alterar nome](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)

```powershell
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"
```

> [!NOTE]
> Você também pode usar o Ambiente de Script Integrado do Windows PowerShell \( ISE \) para alterar o nome da empresa. Usando o ISE do Windows PowerShell, você pode exibir o conteúdo em um \- ambiente em conformidade com Unicode. Para obter informações adicionais, consulte [Apresentando o Windows PowerShell ISE](/previous-versions/mt707506(v=msdn.10)).

## <a name="additional-references"></a>Referências adicionais

- [AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
