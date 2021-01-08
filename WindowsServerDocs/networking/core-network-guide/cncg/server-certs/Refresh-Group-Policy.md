---
title: Atualizar Diretiva de Grupo
description: Saiba como atualizar manualmente Política de Grupo no computador local.
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: db578b1c36548106fa2995469a7e302d4d029901
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98038536"
---
# <a name="refresh-group-policy"></a>Atualizar Diretiva de Grupo

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para atualizar manualmente a Diretiva de Grupo no computador local. Quando a Diretiva de Grupo é atualizada, se o registro automático de certificados estiver configurado e funcionando corretamente, o computador local terá o registro automático de um certificado pela autoridade de certificação (CA).

> [!NOTE]
> A Diretiva de Grupo é atualizada automaticamente quando você reinicia ou um usuário faz logon em um computador membro do domínio. Além disso, a Diretiva de Grupo é atualizada periodicamente. Por padrão, essa atualização periódica é realizada a cada 90 minutos com uma diferença de horário aleatória de até 30 minutos.

A associação em **Administradores**, ou equivalente, é o requisito mínimo necessário para concluir este procedimento.

### <a name="to-refresh-group-policy-on-the-local-computer"></a>Para atualizar a Diretiva de Grupo no computador local

1.  No computador em que o NPS está instalado, abra o Windows PowerShell &reg; usando o ícone na barra de tarefas.

2.  No prompt do Windows PowerShell, digite **gpupdate** e pressione Enter.



