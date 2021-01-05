---
description: 'Saiba mais sobre: lista de verificação: Implementando um design de SSO da Web'
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: Lista de verificação-implementando um design de SSO da Web
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: de48195031fd1d413a2751c554fd1020ff59093b
ms.sourcegitcommit: 3247e193d9fe1b57543fff215460a6d9db52f58b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/30/2020
ms.locfileid: "97814985"
---
# <a name="checklist-implementing-a-web-sso-design"></a>Lista de verificação: implementando um design de SSO da Web

Esta lista de verificação pai inclui \- links de referência cruzada para conceitos importantes sobre o design de SSO de logon único da Web \- \- \( \) para serviços de Federação do Active Directory (AD FS) \( AD FS \) . Ela também contém links para listas de verificação subordinadas que ajudarão a concluir as tarefas exigidas para implementar esse design.

> [!NOTE]
> Execute as tarefas desta lista de verificação na ordem indicada. Quando um link de referência o encaminhar para um tópico conceitual ou para uma lista de verificação subordinada, volte para este tópico após revisar o tópico conceitual ou conclua as tarefas na lista de verificação subordinada, de forma que você possa continuar com as tarefas restantes nesta lista de verificação.

![Ícone para a lista de verificação da implementação de design de SSO da Web. ](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Lista de verificação: Implementando um design de SSO da Web**

|Tarefa|Referência|
|--------|-------------|
|Examine conceitos importantes sobre o design de SSO da Web e determine quais AD FS objetivos de implantação você pode usar para personalizar esse design para atender às necessidades da sua organização. **Observação**:|![Ícone para o link identificando seus objetivos de implantação do AD FS você pode usar em referência à implementação de um design de SSO da Web. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Design de SSO da Web](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807033(v=ws.11))<p>![Ícone do link de design de SSO da Web que você pode usar em referência à implementação de um design de SSO da Web. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Identificando suas metas de implantação de AD FS](../design/identifying-your-ad-fs-deployment-goals.md)|
|Examine os requisitos de hardware, software, certificado, DNS do sistema de nome de domínio \( \) , repositório de atributos e cliente para a implantação de AD FS em sua organização.|![Ícone do apêndice A: revisando AD FS link de requisitos você pode usar em referência à implementação de um design de SSO da Web. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Apêndice A: revisando requisitos de AD FS](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678034(v=ws.11))|
|De acordo com seu plano de design, instale um ou mais servidores de Federação na rede corporativa ou na rede de perímetro. **Observação:** O design de SSO da Web requer que apenas um servidor de Federação funcione com êxito. Um único servidor de Federação atua na função de provedor de declarações e na função de terceira parte confiável.|![Ícone da lista de verificação: configurar um link do servidor de Federação que você pode usar em referência à implementação de um design de SSO da Web. ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Lista de verificação: Configurando um servidor de Federação](Checklist--Setting-Up-a-Federation-Server.md)|
|\(Opcional \) determine se sua organização precisa ou não de um proxy de servidor de Federação na rede de perímetro.|![Ícone da lista de verificação: configuração de um link de proxy do servidor de Federação que você pode usar em referência à implementação de um design de SSO da Web. ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Lista de verificação: Configurando um proxy de servidor de Federação](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|
|Dependendo de seu plano de design SSO da Web e como você pretende usá-lo, adicione o repositório de atributos apropriado, os objetos de confiança da terceira parte confiável, declarações e regras de declarações ao Serviço de Federação.|![Ícone da lista de verificação: Configurando o link da organização do parceiro de conta, você pode usar em referência à implementação de um design de SSO da Web. ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Lista de verificação: Configurando a organização do parceiro de conta](Checklist--Configuring-the-Account-Partner-Organization.md)|
|Se você for um administrador na organização do parceiro de recurso, \- as declarações habilitam seu aplicativo de navegador da Web, aplicativo de serviço Web ou aplicativo do Microsoft &reg; Office SharePoint &reg; Server usando o WIF e o SDK do WIF. **Observação**:|![Ícone do link do Windows Identity Foundation que você pode usar em referência à implementação de um design de SSO da Web. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<p>![Web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|
