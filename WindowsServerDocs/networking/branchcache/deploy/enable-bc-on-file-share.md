---
title: Habilitar BranchCache em um compartilhamento de arquivos (opcional)
description: Saiba como habilitar o BranchCache em um compartilhamento de arquivos.
manager: brianlic
ms.topic: how-to
ms.assetid: 9c465a9e-c504-44ec-9ebc-4e06ba54db30
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: d66192168cffcdab54d61c659fd53084d5b12a5a
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946712"
---
# <a name="enable-branchcache-on-a-file-share-optional"></a>Habilitar BranchCache em um compartilhamento de arquivos (opcional)

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para habilitar o BranchCache em um compartilhamento de arquivos.

> [!IMPORTANT]
> Você não precisará executar esse procedimento se definir a configuração de publicação de hash com o valor **Permitir publicação de hash para todas as pastas compartilhadas**.

A associação a **Administradores** ou equivalente é o requisito mínimo para a execução deste procedimento.

### <a name="to-enable-branchcache-on-a-file-share"></a>Para habilitar o BranchCache em um compartilhamento de arquivos

1.  Abra o Windows PowerShell, digite **mmc** e pressione ENTER. O Console de Gerenciamento Microsoft (MMC) é aberto.

2.  No MMC, no menu **Arquivo**, clique em **Adicionar/Remover Snap-in**. A caixa de diálogo **Adicionar ou Remover Snap-ins** é aberta.

3.  Em **Adicionar ou remover snap-ins**, em **snap-ins disponíveis**, clique duas vezes em **pastas compartilhadas**. O assistente de pastas compartilhadas é aberto com o objeto computador local selecionado. Configure o modo de exibição que você preferir, clique em **concluir** e em **OK**.

4.  Clique duas vezes em **pastas compartilhadas (local)** e em **compartilhamentos**.

5.  No painel de detalhes, clique com o botão direito do mouse em um compartilhamento e clique em **Propriedades**. A caixa de diálogo **Propriedades** do compartilhamento é aberta.

6.  Na caixa de diálogo **Propriedades** , na guia **geral** , clique em **configurações offline**. A caixa de diálogo **configurações offline** é aberta.

7.  Verifique se **somente os arquivos e programas que os usuários especificam estão disponíveis offline** está selecionado e clique em **Habilitar BranchCache**.

8.  Clique em **OK** duas vezes.


