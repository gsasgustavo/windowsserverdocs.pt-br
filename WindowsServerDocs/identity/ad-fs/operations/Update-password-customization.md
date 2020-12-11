---
description: 'Saiba mais sobre: atualizar a personalização de senha'
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: Atualizar personalização de senha
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 58699ca51b1a56296f5ad1618dd2eefca4301ac2
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97039674"
---
# <a name="update-password-customization"></a>Atualizar personalização de senha

Em algumas instâncias, os usuários, às vezes, não podem se conectar à rede corporativa para alterarem a senha de sua conta. Esse fator pode ser especialmente problemático para funcionários remotos que moram longe do escritório corporativo mais próximo. Para esses casos específicos, a página de atualização de senha pode ser usada somente para se conectar à Internet.

Você pode personalizar a página de atualização de senha fornecendo sua própria descrição para a página.

Para habilitar a página de atualização de senha, acesse o Gerenciamento de AD FS sob Pontos de Extremidade. O ponto de extremidade para atualização de senha está localizado na parte inferior, sob Outros - /adfs/portal/updatepassword/. Depois de ter habilitado o ponto de extremidade, você deve reiniciar o serviço AD FS. Isso deve ser feito manualmente. Se você espera usar a página da Web de senha de atualização externamente e, ao usar o proxy de aplicativo, na mesma opção, precisa habilitá-la no proxy (habilitar no proxy). Em seguida, você pode navegar até `https://<fqdn>/adfs/portal/updatepassword/` em um dispositivo ingressado no local de trabalho e verá a página atualizar senha.

![atualizar](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)

## <a name="customize-the-update-password-page-description"></a>Personalize a descrição da página de Atualização de senha

Para personalizar a descrição da página de senha de atualização, use o seguinte cmdlet e sintaxe do Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."
```

## <a name="additional-references"></a>Referências adicionais

[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
