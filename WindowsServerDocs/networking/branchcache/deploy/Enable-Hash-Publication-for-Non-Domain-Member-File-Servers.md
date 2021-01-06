---
title: Habilitar publicação de hash para servidores de arquivos do membro que não sejam de domínio
description: Saiba como configurar a publicação de hash para o BranchCache usando o computador local Política de Grupo em um servidor de arquivos com o serviço de função BranchCache para arquivos de rede da função de servidor serviços de arquivos instalada.
manager: brianlic
ms.topic: how-to
ms.assetid: 11584b73-f9e2-4530-afa5-b8df970e6b24
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: 9da8c5677f3dd137fb682a17adc55da29f973f82
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948432"
---
# <a name="enable-hash-publication-for-non-domain-member-file-servers"></a>Habilitar publicação de hash para servidores de arquivos do membro que não sejam de domínio

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para configurar a publicação de hash para o BranchCache usando o computador local Política de Grupo em um servidor de arquivos que esteja executando o Windows Server 2016 com o serviço de função **BranchCache para arquivos de rede** da função de servidor serviços de arquivo instalada.

Este procedimento se destina ao uso em um servidor de arquivos que não é membro do domínio. Se você executar este procedimento em um servidor de arquivos membro do domínio e também configurar o BranchCache usando a Diretiva de Grupo do domínio, as configurações da Diretiva de Grupo do domínio substituirão as configurações da Diretiva de Grupo local.

A associação a **Administradores** ou equivalente é o requisito mínimo para a execução deste procedimento.

> [!NOTE]
> Se você tiver um ou mais servidores de arquivos membro do domínio, poderá adicioná-los a uma UO (unidade organizacional) nos Serviços de Domínio Active Directory e então usar a Diretiva de Grupo para configurar publicação de hash para todos os servidores de arquivos de uma vez, em vez de configurar cada servidor de arquivos individualmente. Para obter mais informações, consulte [habilitar a publicação de hash para servidores de arquivos do membro do domínio](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).

### <a name="to-enable-hash-publication-for-one-file-server"></a>Para habilitar publicação de hash para um servidor de arquivos

1.  Abra o Windows PowerShell, digite **mmc** e pressione ENTER. O Console de Gerenciamento Microsoft (MMC) é aberto.

2.  No MMC, no menu **Arquivo**, clique em **Adicionar/Remover Snap-in**. A caixa de diálogo **Adicionar ou Remover Snap-ins** é aberta.

3.  Em **Adicionar ou Remover Snap-ins**, em **Snap-ins disponíveis**, clique duas vezes em **Editor de Objeto de Diretiva de Grupo**. O Assistente de Diretiva de Grupo é aberto com o objeto Computador Local selecionado. Clique em **Concluir** e em **OK**.

4.  No Editor de Política de Grupo Local MMC, expanda o seguinte caminho: **política de computador local**, **configuração do computador**, **modelos administrativos**, **rede**, **servidor do LanMan**. Clique em **Servidor Lanman**.

5.  No painel de detalhes, clique duas vezes em **Publicação de Hash para BranchCache**. A caixa de diálogo **Publicação de Hash para BranchCache** é aberta.

6.  Na caixa de diálogo **Publicação de Hash para BranchCache**, clique em **Habilitado**.

7.  Em **Opções**, clique em **Permitir publicação de hash para todas as pastas compartilhadas** e clique em uma das opções a seguir:

    1.  Para habilitar a publicação de hash para todas as pastas compartilhadas neste computador, clique em **Permitir publicação de hash para todas as pastas compartilhadas**.

    2.  Para habilitar a publicação de hash somente para as pastas compartilhadas nas quais o BranchCache está habilitado, clique em **Permitir a publicação de hash somente em pastas compartilhadas nas quais o BranchCache está habilitado**.

    3.  Para não permitir a publicação de hash para todas as pastas compartilhadas no computador, mesmo que o BranchCache esteja habilitado nos compartilhamentos de arquivos, clique em **Impedir a publicação de hash em todas as pastas compartilhadas**.

8.  Clique em **OK**.



