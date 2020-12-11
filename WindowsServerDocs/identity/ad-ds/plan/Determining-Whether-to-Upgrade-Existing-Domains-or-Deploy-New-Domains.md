---
description: 'Saiba mais sobre: determinando se deseja atualizar os domínios existentes ou implantar novos domínios'
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: Determinando se é necessário atualizar domínios existentes ou implantar novos domínios
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: b89ea1c898fc1c7a6859b88d2b7ba21d47516d06
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97044064"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>Determinando se é necessário atualizar domínios existentes ou implantar novos domínios

> Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Cada domínio em seu design será um novo domínio ou um domínio atualizado existente. Os usuários de domínios existentes que você não atualizar devem ser movidos para novos domínios.

A movimentação de contas entre domínios pode afetar os usuários finais. Antes de decidir se deseja mover os usuários para um novo domínio ou para atualizar os domínios existentes, avalie os benefícios administrativos de longo prazo de um novo domínio de AD DS em relação ao custo de mover os usuários para o domínio.

Para obter mais informações sobre como atualizar domínios de Active Directory para o Windows Server 2008, consulte [atualizando domínios de Active Directory para domínios do Windows server 2008 e do Windows server 2008 R2 AD DS](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731188(v=ws.10)).

Para obter mais informações sobre como reestruturar AD DS domínios dentro e entre florestas, consulte o [Guia do ADMT: migrando e Reestruturando Active Directory domínios](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc974332(v=ws.10)).

Para uma planilha para ajudá-lo a documentar seus planos para domínios novos e atualizados, baixe Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip de [ajudas de trabalho para o kit de implantação do Windows Server 2003](https://microsoft.com/download/details.aspx?id=9608) e abra o "planejamento de domínio" (DSSLOGI_5.doc).
