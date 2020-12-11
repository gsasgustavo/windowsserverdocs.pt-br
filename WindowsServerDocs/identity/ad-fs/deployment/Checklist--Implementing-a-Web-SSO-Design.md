---
description: 'Saiba mais sobre: lista de verificação: Implementando um design de SSO da Web'
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: Lista de verificação-implementando um design de SSO da Web
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: eb8627434fb29b167896a4704617231adb4b1794
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97050324"
---
# <a name="checklist-implementing-a-web-sso-design"></a>Lista de verificação: implementando um design de SSO da Web

Esta lista de verificação pai inclui \- links de referência cruzada para conceitos importantes sobre o design de SSO de logon único da Web \- \- \( \) para serviços de Federação do Active Directory (AD FS) \( AD FS \) . Ela também contém links para listas de verificação subordinadas que ajudarão a concluir as tarefas exigidas para implementar esse design.

> [!NOTE]
> Execute as tarefas desta lista de verificação na ordem indicada. Quando um link de referência o encaminhar para um tópico conceitual ou para uma lista de verificação subordinada, volte para este tópico após revisar o tópico conceitual ou conclua as tarefas na lista de verificação subordinada, de forma que você possa continuar com as tarefas restantes nesta lista de verificação.

![](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**lista de verificação de SSO da Web: Implementando um design de SSO da Web**

|Tarefa|Referência|
|--------|-------------|
|Examine conceitos importantes sobre o design de SSO da Web e determine quais AD FS objetivos de implantação você pode usar para personalizar esse design para atender às necessidades da sua organização. **Observação**:|![Design de](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[SSO Web](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807033(v=ws.11)) de SSO da Web<p>![SSO da Web](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[identificando suas metas de implantação de AD FS](../design/identifying-your-ad-fs-deployment-goals.md)|
|Examine os requisitos de hardware, software, certificado, DNS do sistema de nome de domínio \( \) , repositório de atributos e cliente para a implantação de AD FS em sua organização.|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Apêndice A de SSO da Web A: revisando requisitos de AD FS](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678034(v=ws.11))|
|De acordo com seu plano de design, instale um ou mais servidores de Federação na rede corporativa ou na rede de perímetro. **Observação:** O design de SSO da Web requer que apenas um servidor de Federação funcione com êxito. Um único servidor de Federação atua na função de provedor de declarações e na função de terceira parte confiável.|![](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[lista de verificação de SSO da Web: Configurando um servidor de Federação](Checklist--Setting-Up-a-Federation-Server.md)|
|\(Opcional \) determine se sua organização precisa ou não de um proxy de servidor de Federação na rede de perímetro.|![](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[lista de verificação de SSO da Web: Configurando um proxy de servidor de Federação](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|
|Dependendo de seu plano de design SSO da Web e como você pretende usá-lo, adicione o repositório de atributos apropriado, os objetos de confiança da terceira parte confiável, declarações e regras de declarações ao Serviço de Federação.|![](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[lista de verificação de SSO da Web: Configurando a organização do parceiro de conta](Checklist--Configuring-the-Account-Partner-Organization.md)|
|Se você for um administrador na organização do parceiro de recurso, \- as declarações habilitam seu aplicativo de navegador da Web, aplicativo de serviço Web ou aplicativo do Microsoft &reg; Office SharePoint &reg; Server usando o WIF e o SDK do WIF. **Observação**:|![SSO da Web](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<p>![Web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|
