---
title: Prompt de AD FS = logon
description: Saiba mais sobre o suporte nativo para o parâmetro prompt = login que está disponível no AD FS.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.openlocfilehash: 4ef4c832dab13f156b5a0bf5b7dc8ea2a07d36c5
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97811433"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Suporte ao parâmetro prompt=login dos Serviços de Federação do Active Directory (AD FS)

O documento a seguir descreve o suporte nativo para o parâmetro prompt = login que está disponível no AD FS.

## <a name="what-is-promptlogin"></a>O que é prompt = logon?

Quando os aplicativos precisam solicitar uma nova autenticação do Azure AD, o que significa que eles precisam do Azure AD para autenticar novamente o usuário, mesmo que o usuário já tenha sido autenticado, ele pode enviar o `prompt=login` parâmetro para o Azure ad como parte da solicitação de autenticação.

Quando essa solicitação é para um usuário federado, o Azure AD precisa informar ao IdP, como AD FS, que a solicitação é para a nova autenticação.

Por padrão, o Azure AD é convertido `prompt=login` em `wfresh=0` e `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` ao enviar esse tipo de solicitações de autenticação para o IDP federado.

Estes parâmetros significam:

- `wfresh=0`: fazer nova autenticação
- `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`: usar nome de usuário/senha para a nova solicitação de autenticação

Isso pode causar problemas com cenários de intranet corporativa e autenticação multifator nos quais um tipo de autenticação diferente de nome de usuário e senha, conforme solicitado pelo `wauth` parâmetro, é desejado.

AD FS no Windows Server 2012 R2 com o pacote cumulativo de atualizações de julho de 2016 introduziu o suporte nativo para o `prompt=login` parâmetro. Isso significa que agora o Azure AD pode enviar esse parâmetro como está para AD FS serviço como parte das solicitações de autenticação do Azure AD e do Office 365.

## <a name="ad-fs-versions-that-support-promptlogin"></a>AD FS versões que dão suporte a prompt = logon

A seguir está uma lista de versões AD FS que dão suporte ao `prompt=login` parâmetro.

- AD FS no Windows Server 2012 R2 com o pacote cumulativo de atualizações de julho de 2016
- AD FS no Windows Server 2016

## <a name="how-to-configure-a-federated-domain-to-send-promptlogin-to-ad-fs"></a>Como configurar um domínio federado para enviar prompt = logon para AD FS

Use o módulo do PowerShell do Azure AD para definir a configuração.

> [!NOTE]
> O `prompt=login` recurso (habilitado pela `PromptLoginBehavior` Propriedade) está disponível no momento apenas na [versão 1,0 do módulo do PowerShell do Azure ad](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185), no qual os cmdlets têm nomes que incluem "MSol", como Set-MsolDomainFederationSettings.  Ele não está disponível atualmente por meio da ' versão 2,0 ' do módulo do PowerShell do Azure AD, cujos cmdlets têm nomes como "Set-AzureAD \* ".

1. Primeiro, obtenha os valores atuais de `PreferredAuthenticationProtocol` , `SupportsMfa` e `PromptLoginBehavior` para o domínio federado executando o seguinte comando do PowerShell:

```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | Format-List *
```

> [!NOTE]
> A saída de `Get-MsolDomainFederationSettings` por padrão não exibe determinadas propriedades no console. Para exibir todas as propriedades, você deve canalizar ( `|` ) sua saída para `Format-List *` para forçar a saída de todas as propriedades do objeto.

![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)

> [!NOTE]
> Se o valor da propriedade `PromptLoginBehavior` estiver vazio ( `$null` ), o comportamento de `TranslateToFreshPasswordAuth` será usado.

2. Configure o valor desejado de `PromptLoginBehavior` executando o seguinte comando:

```powershell
    Set-MsolDomainFederationSettings –DomainName <your_domain_name> -PreferredAuthenticationProtocol <current_value_from_step1> -SupportsMfa <current_value_from_step1> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

A seguir estão os possíveis valores de `PromptLoginBehavior` parâmetro e seu significado:

- **TranslateToFreshPasswordAuth**: significa o comportamento padrão do Azure AD de conversão `prompt=login` para `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` e `wfresh=0` .
- **NativeSupport**: significa que o `prompt=login` parâmetro será enviado como é para AD FS. Esse é o valor recomendado se AD FS estiver no Windows Server 2012 R2 com o pacote cumulativo de atualizações de julho de 2016 ou superior.
- **Disabled**: significa que somente `wfresh=0` é enviado para AD FS.
