---
title: Aumentar autenticações simultâneas processadas pelo NPS
description: Saiba como melhorar o desempenho do NPS aumentando o número de autenticações simultâneas permitidas entre o NPS e o controlador de domínio.
manager: brianlic
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: fd48dc876cd2b8a24199ffc4fc95b8fa5a6d0d72
ms.sourcegitcommit: d42b80f947dbfa8660d982be67d77745a28081e5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2021
ms.locfileid: "98113372"
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>Aumentar autenticações simultâneas processadas pelo NPS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para obter instruções sobre como configurar as autenticações simultâneas do servidor de políticas de rede.

Se você instalou o NPS do servidor de políticas de rede \( \) em um computador que não seja um controlador de domínio e o NPS estiver recebendo um grande número de solicitações de autenticação por segundo, você poderá melhorar o desempenho do NPS aumentando o número de autenticações simultâneas permitidas entre o NPS e o controlador de domínio.

Para fazer isso, você deve editar a seguinte chave do registro:

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

Adicione um novo valor chamado **MaxConcurrentApi** e atribua a ele um valor de 2 a 5.

>[!CAUTION]
>Se você atribuir um valor a **MaxConcurrentApi** que seja muito alto, o NPS poderá fazer uma carga excessiva em seu controlador de domínio.

Para obter mais informações sobre como gerenciar o NPS, consulte [gerenciar o servidor de políticas de rede](nps-manage-top.md).

Para obter mais informações sobre o NPS, consulte [servidor de diretivas de rede (NPS)](nps-top.md).