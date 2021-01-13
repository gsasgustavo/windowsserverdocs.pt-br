---
title: Visão geral sobre o controle de conta de usuário
description: Saiba mais sobre o controle de conta de usuário, como ele é um componente fundamental da visão geral da segurança da Microsoft e como ele ajuda a reduzir o impacto de um programa mal-intencionado.
ms.topic: article
ms.assetid: 1b7a39cd-fc10-4408-befd-4b2c45806732
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: 7cb2e6bb17ab92dc2ff23ace2de2654f6a2b2197
ms.sourcegitcommit: decb6c8caf4851b13af271d926c650d010a6b9e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98177275"
---
# <a name="user-account-control-overview"></a>Visão geral sobre o controle de conta de usuário
\(O UAC do controle \) de conta de usuário é um componente fundamental da visão geral da segurança da Microsoft.  O UAC ajuda a minimizar o impacto de um programa mal-intencionado.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>Descrição do recurso
O UAC permite que todos os usuários façam logon em seus computadores usando uma conta de usuário padrão. Processos iniciados com um token de usuário padrão podem realizar tarefas com direitos de acesso concedidos a um usuário padrão. Por exemplo, o Windows Explorer herda automaticamente as permissões de nível de usuário padrão. Além disso, todos os programas que são executados usando \( o Windows Explorer, por exemplo, clicando duas vezes \- em um atalho de aplicativo \) também são executados com o conjunto padrão de permissões de usuário. Muitos aplicativos, incluindo aqueles incluídos no próprio sistema operacional, são projetados para funcionar corretamente dessa maneira.

Outros aplicativos, especialmente aqueles que não foram projetados especificamente com as configurações de segurança em mente, geralmente exigem permissões adicionais para serem executados com êxito. Esses tipos de programas são chamados de aplicativos herdados. Além disso, ações como instalar novo software e fazer alterações de configuração em programas como o Firewall do Windows exigem mais permissões do que as disponíveis para uma conta de usuário padrão.

Quando um aplicativo precisa ser executado com mais de direitos de usuário padrão, o UAC pode restaurar grupos de usuários adicionais para o token. Isso permite que o usuário tenha controle explícito de programas que estão fazendo alterações no nível do sistema em seu computador ou dispositivo.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Aplicações práticas
O modo de aprovação de administrador no UAC ajuda a impedir que programas mal-intencionados sejam instalados silenciosamente sem o conhecimento de um administrador. Ele também ajuda a proteger contra alterações inadvertidas do sistema \- . Por fim, ele pode ser usado para impor um nível mais alto de conformidade, no qual os administradores devem consentir ativamente ou fornecer as credenciais de cada processo administrativo.



