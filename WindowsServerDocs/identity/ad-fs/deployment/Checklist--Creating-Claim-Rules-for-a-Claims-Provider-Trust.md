---
description: 'Saiba mais sobre: lista de verificação: Criando regras de declaração para uma confiança do provedor de declarações'
ms.assetid: 503733f8-be0c-429c-81f0-cd4205e8b118
title: Lista de verificação – criando regras de declaração para uma confiança do provedor de declarações
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 40e79c394ad413b60dadb0ba19385ceabd881b3f
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97050364"
---
# <a name="checklist-creating-claim-rules-for-a-claims-provider-trust"></a>Lista de verificação: criando regras de declaração para uma confiança do provedor de declarações


Esta lista de verificação inclui tarefas para planejamento, criação e implantação de regras de declaração associadas a uma confiança do provedor de declarações no Serviços de Federação do Active Directory (AD FS) \( AD FS \) .

> [!NOTE]
> Execute as tarefas desta lista de verificação na ordem indicada. Quando um link de referência levar você a um procedimento, volte para este tópico depois de executar as etapas nesse procedimento para que você possa prosseguir com as tarefas restantes na lista de verificação.

![Criando lista de](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**verificação de regras de declaração: Criando um conjunto de regras de declaração para uma confiança do provedor de declarações**

|Tarefa|Referência|
|--------|-------------|
|Examine os conceitos sobre declarações, regras de declaração, conjuntos de regras de declaração e modelos de regra de declaração e como eles estão associados a relações de confiança federadas.|![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[a função de declarações](../../ad-fs/technical-reference/The-Role-of-Claims.md)<p>![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[a função de regras de declaração](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|
|Examine os conceitos sobre como uma declaração flui em todos os estágios no pipeline de emissão de declarações e como as regras são processadas pelo mecanismo de emissão de declarações.|![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[a função do pipeline de declarações](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<p>![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[a função do mecanismo de declarações](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|
|Para planejar e implementar efetivamente as declarações de saída que serão emitidas por essa confiança do provedor de declarações, determine se uma ou mais regras de declaração são necessárias e quais regras de declaração você deve usar com essa confiança do provedor de declarações.|![a criação de regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[determina o tipo de modelo de regra de declaração a ser usado](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)|
|Examine os conceitos sobre quando criar uma regra de declaração sobre outra e como você pode usar o idioma da regra de declaração para fornecer uma lógica mais complexa do que as regras padrão, a fim de fornecer um resultado desejado no conjunto de declarações de saída ideal.|![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[quando usar uma regra de passagem ou de declaração de filtro](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)<p>![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[quando usar uma regra de declaração de transformação](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)<p>![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[quando usar uma regra enviar atributos LDAP como declarações](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)<p>![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[quando usar uma associação de grupo de envio como uma regra de declaração](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)<p>![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[quando usar uma regra de declaração personalizada](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)<p>![Criando regras de Declaração](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[a função do idioma da regra de declaração](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|
|Uma descrição de declaração deve ser criada se ainda não existir uma que atenda às necessidades da sua organização. O AD FS é fornecido com um conjunto padrão de descrições de declaração que são expostas no snap-in Gerenciamento de AD FS \- .|![Criando regras](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[de declaração adicionar uma descrição de declaração](../../ad-fs/operations/Add-a-Claim-Description.md)|
|Dependendo das necessidades da sua organização, crie uma ou mais regras de declaração para o conjunto de regras de transformação de aceitação associado a essa confiança do provedor de declarações para que as declarações sejam emitidas adequadamente.|![criar regras de Declaração](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[criar uma regra para passar ou filtrar uma declaração de entrada](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)<p>![criar regras de Declaração](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[criar uma regra para enviar atributos LDAP como declarações](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<p>![Criando regras de Declaração](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[criar uma regra para enviar a associação de grupo como uma declaração](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<p>![Criando regras de Declaração](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[criar uma regra para transformar uma declaração de entrada](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)<p>![Criando regras de Declaração](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[criar uma regra para enviar uma declaração de método de autenticação](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)<p>![Criando regras de Declaração](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[criar uma regra para enviar uma declaração compatível com AD FS 1. x](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<p>![Criando regras de Declaração](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[criar uma regra para enviar declarações usando uma regra personalizada](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|


