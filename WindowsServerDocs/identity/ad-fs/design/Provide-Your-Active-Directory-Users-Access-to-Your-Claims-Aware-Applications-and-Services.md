---
description: 'Saiba mais sobre: forneça aos seus Active Directory usuários acesso aos seus aplicativos e serviços com reconhecimento de declaração'
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: Fornecer a seus usuários do Active Directory acesso a aplicativos e serviços com reconhecimento de declarações
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: a37147b46dc0ed8a6aac7700ad3549052c90c4bb
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049414"
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Fornecer a seus usuários do Active Directory acesso a aplicativos e serviços com reconhecimento de declarações

Quando você é um administrador na organização do parceiro de conta em um Serviços de Federação do Active Directory (AD FS) \( AD FS \) implantação e tem uma meta de implantação para fornecer \- \- \( acesso SSO de logon único \) para funcionários na rede corporativa para seus recursos hospedados:

-   Funcionários que estiverem conectados a uma floresta do Active Directory na rede corporativa podem usar o SSO para acessar vários aplicativos ou serviços na rede de perímetro da sua organização. Esses aplicativos e serviços são protegidos por AD FS.

    Por exemplo, a Fabrikam pode querer que os funcionários da rede corporativa tenham acesso federado a \- aplicativos baseados na Web hospedados na rede de perímetro para a Fabrikam.

-   Os funcionários remotos que fizeram logon em um domínio de Active Directory podem obter AD FS tokens do servidor de Federação em sua organização para obter acesso federado a AD FS \- \- aplicativos ou serviços protegidos baseados na Web que também residem em sua organização.

-   Informações do armazenamento de atributo do Active Directory podem ser preenchidas em tokens do AD FS dos funcionários.

Os seguintes componentes são necessários para essa meta de implantação:

-   **Active Directory Domain Services \( AD DS \) :** AD DS contém as contas de usuário dos funcionários que são usadas para gerar tokens de AD FS. Informações, como associações de grupo e atributos, são preenchidas em tokens do AD FS como declarações de grupo e declarações personalizadas.

    > [!NOTE]
    > Você também pode usar LDAP de protocolo de acesso de diretório Lightweight \( \) ou linguagem SQL \( SQL \) para conter as identidades para AD FS geração de tokens.

-   **DNS corporativo:** Essa implementação do DNS do sistema de nomes de domínio \( \) contém um \( registro de recurso de host simples \) para que os clientes de intranet possam localizar o servidor de Federação de conta. Essa implementação do DNS também pode hospedar outros registros DNS necessários na rede corporativa. Para obter mais informações, consulte [Requisitos de resolução de nomes para servidores de federação](Name-Resolution-Requirements-for-Federation-Servers.md).

-   **Servidor de Federação do parceiro de conta:** Esse servidor de Federação é associado a um domínio na floresta do parceiro de conta. Ele autentica as contas de usuário do funcionário e gera tokens do AD FS. O computador cliente do funcionário executa a autenticação integrada do Windows nesse servidor de Federação para gerar um token de AD FS. Para obter mais informações, consulte [Review the Role of the Federation Server in the Account Partner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).

    O servidor de Federação do parceiro de conta pode autenticar os seguintes usuários:

    -   Funcionários com contas de usuário neste domínio

    -   Funcionários com contas de usuário em qualquer lugar deste domínio

    -   Funcionários com contas de usuário em qualquer lugar em florestas que são confiáveis para essa floresta \( por meio de uma relação de confiança de duas \- vias do Windows\)

-   **Funcionário:** Um funcionário acessa um \- serviço baseado na Web \( por meio de um aplicativo \) ou de um \- aplicativo baseado na Web \( por meio de um navegador da Web com suporte \) enquanto ele está conectado à rede corporativa. O computador cliente do funcionário na rede corporativa se comunica diretamente com o servidor de Federação para autenticação.

Depois de revisar as informações nos tópicos vinculados, você pode começar a implantar essa meta, seguindo as etapas em [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md).

A ilustração a seguir mostra cada um dos componentes necessários para essa AD FS meta de implantação.

![acesso às suas declarações](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)

## <a name="see-also"></a>Consulte Também
[Guia de design do AD FS no Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
