---
description: 'Saiba mais sobre: lista de verificação: Implementando um design de SSO Web federado'
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: Lista de verificação-implementando um design de SSO da Web federado
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: b6bec4d2923e69c80e32585a14d8781a6f705ae5
ms.sourcegitcommit: 3247e193d9fe1b57543fff215460a6d9db52f58b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/30/2020
ms.locfileid: "97814945"
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>Lista de verificação: implementando um design de SSO da Web federado

Esta lista de verificação pai inclui \- links de referência cruzada para conceitos importantes sobre o design de SSO de logon único da Web federada \- \- \( \) para serviços de Federação do Active Directory (AD FS) \( AD FS \) . Ela também contém links para listas de verificação subordinadas que ajudarão a concluir as tarefas exigidas para implementar esse design.

> [!NOTE]
> Execute as tarefas desta lista de verificação na ordem indicada. Quando houver um link de referência para um tópico conceitual ou uma lista de verificação subordinada, retorne a este tópico depois de revisar aquele ou concluir as tarefas da lista de verificação subordinada para poder executar as tarefas restantes desta lista de verificação.

![Ícone para a lista de verificação da implementação de um design de SSO da Web federado. ](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Lista de verificação: Implementando um design de SSO da Web federado**

|Tarefa|Referência|
|--------|-------------|
|Examine conceitos importantes sobre o design de SSO da Web federado e determine quais AD FS objetivos de implantação você pode usar para personalizar esse design para atender às necessidades da sua organização.|![Ícone do link de design de SSO da Web federado que você pode usar em referência à implementação de um design de SSO da Web federado. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Design de SSO Web federado](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807050(v=ws.11))<p>![Ícone para o link identificando seus objetivos de implantação do AD FS você pode usar em referência à implementação de um design de SSO da Web federado. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Identificando suas metas de implantação de AD FS](../design/identifying-your-ad-fs-deployment-goals.md)<p>![Ícone para o link planejar sua implantação que você pode usar em referência à implementação de um design de SSO da Web federado. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planejando a implantação](../design/planning-your-deployment.md)|
|Examine os requisitos de hardware, software, certificado, DNS do sistema de nome de domínio \( \) , repositório de atributos e cliente para a implantação de AD FS em sua organização.|![Ícone do apêndice A: examinar AD FS link de requisitos você pode usar em referência à implementação de um design de SSO da Web federado. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Apêndice A: revisando requisitos de AD FS](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678034(v=ws.11))|
|Examine conceitos importantes sobre declarações, regras de declaração, repositórios de atributos e o banco de dados de configuração de AD FS antes de implantar AD FS em ambas as organizações parceiras.|![Ícone do link entendendo a chave AD FS conceitos que você pode usar em referência à implementação de um design de SSO da Web federado. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Entendendo os principais conceitos de AD FS](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|
|De acordo com seu plano de design, instale um ou mais servidores de Federação em cada organização parceira. **Observação:** Para o design de SSO da Web federado, você precisa de pelo menos um servidor de Federação na organização do parceiro de conta e pelo menos um servidor de Federação na organização do parceiro de recurso.|![Ícone da lista de verificação: configurar um link do servidor de Federação que você pode usar em referência à implementação de um design de SSO da Web federado. ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Lista de verificação: Configurando um servidor de Federação](Checklist--Setting-Up-a-Federation-Server.md)|
|\(Opcional \) determine se sua organização precisa ou não de um proxy de servidor de Federação. Se o plano de design chamar um proxy, você poderá instalar um ou mais proxies de servidor de Federação em cada organização parceira.|![Ícone da lista de verificação: configuração de um link de proxy do servidor de Federação que você pode usar em referência à implementação de um design de SSO da Web federado. ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Lista de verificação: Configurando um proxy de servidor de Federação](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|
|De acordo com seu plano de design, compartilhe certificados, configure clientes e configure as relações de confiança nas duas organizações parceiras para que elas possam se comunicar por meio de confiança de federação.|![Ícone da lista de verificação: Configurando o link da organização do parceiro de conta, você pode usar em referência à implementação de um design de SSO da Web federado. ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Lista de verificação: Configurando a organização do parceiro de conta](Checklist--Configuring-the-Account-Partner-Organization.md)<p>![Ícone da lista de verificação: Configurando o link de organização do parceiro de recurso, você pode usar em referência à implementação de um design de SSO da Web federado. ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Lista de verificação: Configurando a organização do parceiro de recurso](Checklist--Configuring-the-Resource-Partner-Organization.md)|
|Se você for um administrador na organização do parceiro de recurso, \- as declarações habilitam seu aplicativo de navegador da Web, aplicativo de serviço Web ou aplicativo do Microsoft &reg; Office SharePoint &reg; Server usando o WIF e o SDK do WIF.|![Ícone do link do Windows Identity Foundation que você pode usar em referência à implementação de um design de SSO da Web federado. ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<p>![SDK Web federado do](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)|
