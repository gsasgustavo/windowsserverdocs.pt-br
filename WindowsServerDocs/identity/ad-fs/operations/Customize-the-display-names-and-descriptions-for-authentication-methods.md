---
description: 'Saiba mais sobre: personalizar os nomes de exibição e descrições para métodos de autenticação'
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: Personalizar os nomes de exibição e as descrições de métodos de autenticação
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 0b4c094aec3bf36d00074a93753e675d0d642e9f
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97039894"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>Personalizar os nomes de exibição e as descrições de métodos de autenticação

Para personalizar as descrições e os nomes de exibição para os métodos de autenticação, você pode usar o cmdlet do PowerShell do `Set-AdfsAuthenticationProviderWebContent` .  Para usar este cmdlt, você deve primeiro obter o nome do método de autenticação que você deseja personalizar.  Isso pode ser feito por meio do `Get-AdfsGlobalAuthenticationPolicy`.  No exemplo abaixo, vemos que, em nossa página de entrada \- , o seguinte é exibido: "entrar usando um certificado X. 509".  Queremos simplificar isso para nossos usuários.

![Personalizar DisplayName](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)

Portanto, primeiro obtemos o nome do método de autenticação e, em seguida, editamos o texto exibido.

```powershell
Get-AdfsGlobalAuthenticationPolicy

AdditionalAuthenticationProvider  : {}
DeviceAuthenticationEnabled   : False
PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}
PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}
WindowsIntegratedFallbackEnabled  : True

Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"
 ```

![Personalizar DisplayName](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)

Agora vemos que nossa mensagem de exibição foi alterada.

![Personalizar DisplayName](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)

## <a name="additional-references"></a>Referências adicionais

[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
