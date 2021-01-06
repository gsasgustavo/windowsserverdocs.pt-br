---
title: Cancelar o registro de um NPS de um domínio do Active Directory
description: Você pode usar este tópico para registrar um servidor que executa o servidor de diretivas de rede no Windows Server 2016 no domínio padrão do NPS ou em outro domínio.
manager: brianlic
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: aff5090a5f9fcd2791835f21e2caf1c0dccaa510
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949332"
---
# <a name="unregister-an-nps-from-an-active-directory-domain"></a>Cancelar o registro de um NPS de um domínio do Active Directory

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

No processo de gerenciamento da implantação do NPS, talvez seja útil mover um NPS para outro domínio, substituir um NPS ou desativar um NPS.

Ao mover ou desativar um NPS, você pode cancelar o registro do NPS nos domínios de Active Directory em que o NPS tem permissão para ler as propriedades de contas de usuário em Active Directory.

A associação a **Administradores** ou equivalente é o requisito mínimo para a execução destes procedimentos.

## <a name="to-unregister-an-nps"></a>Para cancelar o registro de um NPS

1. No controlador de domínio, em Gerenciador do Servidor, clique em **ferramentas** e, em seguida, clique em **Active Directory usuários e computadores**. O console de Usuários e Computadores do Active Directory é aberto.

2. Clique em **usuários** e, em seguida, clique duas vezes em **Servidores RAS e ias**.

3. Clique na guia **Membros** e selecione o NPS que você deseja cancelar o registro.

4. Clique em **remover**, em **Sim** e em **OK**.

