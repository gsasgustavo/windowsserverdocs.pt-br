---
description: 'Saiba mais sobre: personalizar os nomes de exibição e descrições para métodos de autenticação'
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: Personalizar os nomes de exibição e as descrições de métodos de autenticação
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 33a264bc2230087d89a88c70e29edb76e3a09ed6
ms.sourcegitcommit: 6a62d736e4d9989515c6df85e2577662deb042b6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98103798"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>Personalizar os nomes de exibição e as descrições de métodos de autenticação

Para personalizar os nomes de exibição e as descrições de métodos de autenticação, você pode usar o `Set-AdfsAuthenticationProviderWebContent` cmdlet do PowerShell.  Para usar esse cmdlet, primeiro você deve obter o nome do método de autenticação que deseja personalizar.  Isso pode ser feito por meio do `Get-AdfsGlobalAuthenticationPolicy`.  No exemplo abaixo, vemos que, em nossa página de entrada \- , o seguinte é exibido: "entrar usando um certificado X. 509".  Queremos simplificar isso para nossos usuários.

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

![Captura de tela que mostra como obter o nome do método de autenticação e editar o texto exibido.](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)

Agora vemos que nossa mensagem de exibição foi alterada.

![Captura de tela que mostra que a mensagem de exibição foi alterada.](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)

## <a name="additional-references"></a>Referências adicionais

[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
