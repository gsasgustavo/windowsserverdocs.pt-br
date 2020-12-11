---
description: 'Saiba mais sobre: mensagens de erro personalizadas para AD FS página de entrada'
ms.assetid: 1df78c2a-5054-4b54-8310-c48ea62e6e0b
title: Mensagens de erro personalizadas para AD FS página de entrada
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: acfe34a7d151a7e14348e44350e9304a816428b9
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97039904"
---
# <a name="custom-error-messages-for-ad-fs-sign-in-page"></a>Mensagens de erro personalizadas para AD FS página de entrada

Você pode configurar mensagens de erro personalizadas que podem ser ajustadas à sua organização. A ilustração a seguir mostra uma descrição de página de erro personalizada e uma mensagem de erro genérica. Use os seguintes cmdlets do Windows PowerShell para personalizar suas mensagens de erro.

![erro personalizado](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom3.png)

## <a name="customize-the-error-page-description"></a>Personalize a descrição da página de erro

Para personalizar a descrição da página de erro, use o seguinte cmdlet e sintaxe do Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description"
```

## <a name="customize-a-generic-error-message"></a>Personalize uma mensagem de erro genérica
Para personalizar a mensagem de erro genérica, use o seguinte cmdlet e sintaxe do Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageGenericErrorMessage "This is a generic error message.  Contact Contoso IT for assistance."
```

## <a name="customize-an-authorization-error-message"></a>Personalize uma mensagem de erro de autorização
Para personalizar a mensagem de erro de autorização, use o seguinte cmdlet e sintaxe do Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageAuthorizationErrorMessage "You have received an Authorization error.  Contact Contoso IT for assistance."
```

## <a name="customize-a-device-authentication-error-message"></a>Personalize uma mensagem de erro de autenticação de dispositivo
Para personalizar a mensagem de erro de autenticação do dispositivo, use o seguinte cmdlet e sintaxe do Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageDeviceAuthenticationErrorMessage "Your device is not authorized.  Contact Contoso IT for assistance."
```

## <a name="customize-a-support-email-error-message"></a>Personalize uma mensagem de erro de email do suporte
Você pode configurar um endereço de email de suporte no AD FS. Se configurado, AD FS mostra automaticamente um link para os usuários finais enviarem os detalhes do erro por email.

Para personalizar a mensagem de erro de email de suporte, use o seguinte cmdlet e sintaxe do Windows PowerShell.

```powershell
Set-AdfsGlobalWebContent -ErrorPageSupportEmail  "admin@contoso.com"
```

## <a name="customize-a-relying-party-authorization-message"></a>Personalize uma mensagem de autorização da terceira parte confiável
Você pode configurar uma mensagem de erro de autorização de terceira parte confiável no AD FS.

Para personalizar a mensagem de erro de terceira parte confiável, use o seguinte cmdlet e sintaxe do Windows PowerShell.

```powershell
Set-AdfsRelyingPartyWebContent -Name fedpassive -ErrorPageAuthorizationErrorMessage "<p> You need to be a member of Security Auditors to access this site. Click <A href='http://accessrequest/'>here</A> for more information.</p>"
```

## <a name="additional-references"></a>Referências adicionais

[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
