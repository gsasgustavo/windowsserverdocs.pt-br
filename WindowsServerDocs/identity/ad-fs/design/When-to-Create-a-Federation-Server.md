---
description: 'Saiba mais sobre: quando criar um servidor de Federação'
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: Quando criar um Servidor de Federação
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: d3ced02154d3945b8022d565d8fa834164d2d229
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97048994"
---
# <a name="when-to-create-a-federation-server"></a>Quando criar um Servidor de Federação

Ao criar um servidor de Federação Serviços de Federação do Active Directory (AD FS) \( AD FS \) , você fornece um meio pelo qual sua organização pode:

-   Participe do logon único da Web com \- \- \( \) comunicação baseada em SSO com outra organização \( que também tenha pelo menos um servidor de Federação \) e, quando necessário, com os funcionários em sua própria organização \( que precisam de acesso pela Internet \) .

-   Habilitar serviços de front-end para representar usuários em serviços de infraestrutura usando a delegação de identidade. Para obter mais informações, consulte [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md).

As seções a seguir descrevem algumas das principais decisões para determinar quando e onde criar um ou mais servidores de Federação.

## <a name="determine-the-organizational-role-for-the-federation-server"></a>Determinar a função organizacional do servidor de federação
Para tomar uma decisão informada sobre quando criar um novo servidor de Federação, primeiro você deve determinar em qual organização o servidor residirá. A função que um servidor de federação desempenha em uma organização depende se você coloca o servidor de Federação na organização do parceiro de conta ou na organização do parceiro de recurso.

Quando um servidor de Federação é colocado na rede corporativa do parceiro de conta, sua função é autenticar as credenciais do usuário do navegador, serviço Web ou clientes do seletor de identidade e enviar tokens de segurança para os clientes. Para obter mais informações, consulte [Review the Role of the Federation Server in the Account Partner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).

Quando um servidor de Federação é colocado na rede corporativa do parceiro de recurso, sua função é autenticar usuários, com base em um token de segurança que é emitido por um servidor de Federação na organização do parceiro de recurso, ou sua função é redirecionar solicitações de token de aplicativos Web ou serviços Web configurados para a organização de parceiro de conta à qual o cliente pertence. Para obter mais informações, consulte [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).

## <a name="determine-which-ad-fs-design-to-deploy"></a>Determinar qual design do AD FS será implantado
Você cria servidores de Federação em sua organização sempre que desejar implantar qualquer um dos seguintes designs de AD FS:

-   [Design SSO da Web](Web-SSO-Design.md)

-   [Design SSO da Web federado](Federated-Web-SSO-Design.md)

Se necessário, uma organização que implanta um design de SSO da Web federado pode configurar um único servidor de Federação para que ele atue na função de parceiro de conta e na função de parceiro de recurso. Nesse caso, o servidor de Federação pode produzir Security Assertion Markup Language \( \) tokens SAML, com base em contas de usuário em sua própria organização, ou redirecionar solicitações de token para a organização, com base em onde as contas dos usuários residem.

> [!NOTE]
> Para o design de SSO da Web federado, deve haver pelo menos um servidor de Federação no parceiro de conta e pelo menos um servidor de Federação no parceiro de recurso.

## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>Diferenças entre um servidor de federação e um proxy do servidor de federação
Um servidor de Federação pode fornecer páginas da Web para entrada \- , política, autenticação e descoberta da mesma maneira que um proxy do servidor de Federação. As principais diferenças entre um servidor de Federação e um proxy de servidor de Federação têm a ver com quais operações um servidor de Federação pode executar que um proxy de servidor de Federação não pode executar.

A seguir estão as operações que apenas um servidor de Federação pode executar:

-   O servidor de Federação executa as operações de criptografia que produzem o token. Embora os proxies do servidor de Federação não possam produzir tokens, eles podem ser usados para rotear ou redirecionar os tokens para os clientes e, quando necessário, de volta para o servidor de Federação. Para obter mais informações sobre como usar servidores de Federação, consulte [quando criar um proxy de servidor de Federação](When-to-Create-a-Federation-Server-Proxy.md).

-   Os servidores de Federação dão suporte ao uso da autenticação integrada do Windows para clientes na rede corporativa; os proxies do servidor de Federação não fazem isso. Para obter mais informações sobre como usar a autenticação integrada do Windows com o servidor de Federação, consulte [quando criar um farm de servidores de Federação](When-to-Create-a-Federation-Server-Farm.md).

> [!CAUTION]
> A comunicação entre os servidores de federação e os bancos de dados de configuração do SQL Server, os repositórios de atributos do SQL Server, os controladores de domínio e as instâncias de AD LDS não tem sua integridade ou confidencialidade protegida de modo padrão. Para atenuar isso, considere a possibilidade de proteger o canal de comunicação entre esses servidores usando IPSEC ou uma conexão segura fisicamente entre todos esses servidores. Para a comunicação entre os servidores de federação e os SQL Servers, considere usar a proteção SSL na cadeia de conexão. Para conexões entre servidores de federação e controladores de domínio, considere habilitar a criptografia e autenticação Kerberos. Para LDAP, \/ não há suporte para LDAP S para AD LDS \/ AD DS.

## <a name="how-to-create-a-federation-server"></a>Como criar um servidor de federação
Você pode criar um servidor de Federação usando o assistente de configuração do servidor de Federação AD FS ou a ferramenta de linha de comando Fsconfig.exe \- . Ao usar uma dessas ferramentas, escolha uma das opções a seguir para criar um servidor de federação.

-   Criar um \- servidor de Federação autônomo

    Para obter mais informações sobre como configurar um servidor de \- Federação autônomo, consulte [criar um Stand-Alone servidor de Federação](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md).

-   Criar o primeiro servidor de federação em um farm de servidores de federação

    Para obter mais informações sobre como configurar o primeiro servidor de federação ou adicionar um servidor de federação a um farm, consulte [Create the First Federation Server in a Federation Server Farm](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md).

-   Adicionar um servidor de federação a um farm de servidores de federação

    Para obter mais informações sobre como adicionar um servidor de federação a um farm, consulte [Add a Federation Server to a Federation Server Farm](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md).

Para obter informações mais detalhadas sobre como cada uma dessas opções funcionam, consulte [The Role of the AD FS Configuration Database](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).

Para obter mais informações sobre como configurar todos os pré-requisitos necessários para implantar um servidor de federação, consulte [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md).

## <a name="see-also"></a>Consulte Também
[Guia de design do AD FS no Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

