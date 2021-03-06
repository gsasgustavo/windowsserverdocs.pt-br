---
title: Fazer logoff ou desconectar sessões do usuário
description: Saiba como fazer logoff de um usuário manualmente
ms.topic: article
ms.assetid: 3e9bbcdc-e33b-481e-8b46-787a4f6d58bc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 0436f33df87da55792ba01a581c8f5c05f3500ce
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969323"
---
# <a name="log-off-or-disconnect-user-sessions"></a>Fazer logoff ou desconectar sessões do usuário
Os usuários do MultiPoint Services podem fazer logon e fazer logoff das sessões da área de trabalho como eles fariam com qualquer sessão do Windows. Os usuários também podem desconectar ou suspender sua sessão para que a estação de serviços do MultiPoint não esteja sendo usada, mas sua sessão permanece ativa na memória do computador do sistema de serviços do MultiPoint.

Além disso, os usuários administrativos podem encerrar a sessão de um usuário se o usuário tiver passado de sua sessão de serviços do MultiPoint ou se tiver esquecido de fazer logoff do sistema.

## <a name="logging-off-or-disconnecting-a-session"></a>Logoff ou desconexão de uma sessão
A tabela a seguir descreve as diferentes opções que você ou qualquer usuário pode usar para fazer logoff, suspender ou encerrar uma sessão.

|||
|-|-|
|**Ação**|**Efeito**|
|Clique em **Iniciar**, clique em configurações, clique no nome de usuário (canto superior direito) e, em seguida, clique em **sair**.|A sessão é encerrada e a estação fica disponível para logon por qualquer usuário.|
|Clique em **Iniciar**, clique em **Configurações**, clique em Energia e, em seguida, clique em **Desconectar**.|A sessão é desconectada e fica preservada na memória do computador. A estação fica disponível para o logon pelo mesmo usuário ou por um usuário diferente.|
|Clique em **Iniciar**, clique em configurações, clique no nome de usuário (canto superior direito) e, em seguida, clique em **Bloquear**|A estação é bloqueada e fica preservada na memória do computador.|

## <a name="suspending-or-ending-a-users-session"></a>Suspendendo ou encerrando a sessão de um usuário
A tabela a seguir descreve as diferentes opções que você, como um usuário administrativo, podem usar para desconectar ou encerrar a sessão de um usuário.

|||
|-|-|
|**Ação**|**Efeito**|
|**Suspender:** No Gerenciador do MultiPoint, use a guia **estações** para suspender a sessão do usuário. Para obter mais informações, consulte o tópico [Suspender e manter a sessão do usuário ativa](Suspend-and-Leave-User-Session-Active.md).|A sessão do usuário termina e é preservada na memória do computador. A estação fica disponível para o logon pelo mesmo usuário ou por um usuário diferente. O usuário pode fazer logon na mesma estação ou em outra e continuar trabalhando.|
|**Fim:** No Gerenciador do MultiPoint, use a guia **estações** para encerrar a sessão do usuário. Você também pode encerrar todas as sessões de usuário na guia **estações** . Para obter mais informações, consulte o tópico [encerrar uma sessão de usuário](End-a-User-Session.md) .|A sessão do usuário termina e a estação fica disponível para logon por qualquer usuário. A sessão do usuário não é mais exibida na guia **estações** e não está na memória do computador.|

## <a name="see-also"></a>Consulte Também
[Suspender e deixar a sessão de usuário ativa](Suspend-and-Leave-User-Session-Active.md) 
 [Encerrar uma sessão](End-a-User-Session.md) 
 de usuário [Gerenciar áreas de trabalho](manage-user-desktops-using-multipoint-dashboard.md) 
 de usuários [Fazer](Log-Off-User-Sessions.md) logoff de sessões de usuário