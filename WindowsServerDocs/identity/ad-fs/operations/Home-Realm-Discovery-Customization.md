---
description: 'Saiba mais sobre: personalização da descoberta de realm inicial'
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: Personalização da descoberta de realm inicial
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 3a3bc01b4ec28d28d4815fc46c797b3f6ff62cfe
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97039854"
---
# <a name="home-realm-discovery-customization"></a>Personalização da descoberta de realm inicial


Quando o cliente de AD FS solicita primeiro um recurso, o servidor de Federação de recurso não tem informações sobre o realm do cliente. O servidor de Federação de recursos responde ao cliente do AD FS com uma página de **descoberta de realm do cliente** , onde o usuário seleciona o realm inicial de uma lista. Os valores da lista são preenchidos a partir da propriedade de nome de exibição nas Relações de Confiança do Provedor de Declarações. Use os seguintes cmdlets do Windows PowerShell para modificar e personalizar a experiência de descoberta do AD FS Home realm.

![Realm inicial](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)

> [!WARNING]
> Fique atento ao nome do Provedor de Declarações que aparece para o Active Directory local, se ele é o nome de exibição do serviço de federação.




## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>Configure o Provedor de identidade para usar determinados sufixos de email
Uma organização pode federar com vários provedores de declarações. O AD FS agora fornece a \- funcionalidade do box para que os administradores listem os sufixos, por exemplo,, @us.contoso.com @eu.contoso.com que têm suporte de um provedor de declarações e habilitá-lo para a \- descoberta baseada em sufixo. Com essa configuração, os usuários finais podem digitar sua conta institucional e o AD FS selecionará automaticamente o provedor de declarações correspondente.

Para configurar um IDP de provedor de identidade \( \) , como `fabrikam` , para usar determinados sufixos de email, use o seguinte cmdlet e sintaxe do Windows PowerShell.


`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") `

>[!NOTE]
> Ao federar entre dois servidores AD FS, defina a propriedade PromptLoginFederation na relação de confiança do provedor de declarações como ForwardPromptAndHintsOverWsFederation.  Isso é para que AD FS encaminhará o login_hint e solicitará controlar para o IDP.  Isso pode ser feito executando o seguinte cmdlet do PowerShell:
>
>`Set-AdfsclaimsProviderTrust -PromptLoginFederation ForwardPromptAndHintsOverWsFederation`

## <a name="configure-an-identity-provider-list-per-relying-party"></a>Configurar uma lista de provedores de identidade por terceira parte confiável.
Para alguns cenários, uma organização pode desejar que os usuários finais vejam somente os provedores de declarações específicos para um aplicativo, de forma que somente um subconjunto de provedores de declarações é exibido na página de descoberta de realm inicial.

Para configurar uma lista IDP por RP de terceira parte confiável \( \) , use o seguinte cmdlet e sintaxe do Windows PowerShell.


`Set-AdfsRelyingPartyTrust -TargetName claimapp -ClaimsProviderName @("Fabrikam","Active Directory") `


## <a name="bypass-home-realm-discovery-for-the-intranet"></a>Ignore a descoberta de realm inicial para Intranet.
A maior parte das organizações dá suporte somente ao seu Active Directory local para qualquer usuário que acessa de dentro de seu firewall. Nesses casos, os administradores podem configurar AD FS para ignorar a descoberta de realm inicial para a intranet.

Para ignorar o HRD para a intranet, use o seguinte cmdlet e sintaxe do Windows PowerShell.


`Set-AdfsProperties -IntranetUseLocalClaimsProvider $true `


> [!IMPORTANT]
> Observe que se uma lista de provedores de identidade para uma terceira parte confiável tiver sido configurada, mesmo que a configuração anterior tenha sido habilitada e o usuário acesse a partir da intranet, AD FS ainda mostrará a página HRD de descoberta de realm inicial \( \) . Para ignorar a HRD nesse caso, você precisa assegurar que o "Active Directory" também tenha sido adicionado à lista de IDP para essa terceira parte confiável.

## <a name="additional-references"></a>Referências adicionais
[AD FS a personalização de entrada do usuário](AD-FS-user-sign-in-customization.md)
