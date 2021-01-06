---
title: Criar o Objeto de Política de Grupo de publicação de hash BranchCache
description: Saiba como criar a publicação de hash do BranchCache Política de Grupo objeto (GPO).
manager: brianlic
ms.topic: how-to
ms.assetid: c3d33bed-83ef-4eb8-acf9-0719ecb4a931
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: 0598701ecf060390001bd18ce704df9dfde6ab3c
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948462"
---
# <a name="create-the-branchcache-hash-publication-group-policy-object"></a>Criar o Objeto de Política de Grupo de publicação de hash BranchCache

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para criar a publicação de hash do BranchCache Política de Grupo objeto (GPO).

A associação a **Adminis. do Domínio** ou equivalente é o requisito mínimo para a execução deste procedimento.

> [!NOTE]
> Antes de executar este procedimento, crie a unidade organizacional de servidores de arquivos BranchCache e mova os servidores de arquivos para a UO. Para obter mais informações, consulte [habilitar a publicação de hash para servidores de arquivos do membro do domínio](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md).

### <a name="to-create-the-branchcache-hash-publication-group-policy-object"></a>Para criar a publicação de hash do BranchCache Política de Grupo objeto

1.  Abra o Windows PowerShell, digite **mmc** e pressione ENTER. O Console de Gerenciamento Microsoft (MMC) é aberto.

2.  No MMC, no menu **Arquivo**, clique em **Adicionar/Remover Snap-in**. A caixa de diálogo **Adicionar ou Remover Snap-ins** é aberta.

3.  Em **Adicionar ou Remover Snap-ins**, em **Snap-ins disponíveis**, clique duas vezes em **Gerenciamento de Diretiva de Grupo** e clique em **OK**.

4.  No MMC do Gerenciamento de Diretiva de Grupo, expanda o caminho para a UO dos servidores de arquivos BranchCache criada anteriormente. Por exemplo, se sua floresta se chama example.com, seu domínio é denominado example1.com e sua UO é denominada servidores de arquivos do BranchCache, expanda o seguinte caminho: **política de grupo Management**, **Forest: example.com**, **domínios**, **example1.com**, **servidores de arquivos do BranchCache**.

5.  Clique com o botão direito do mouse em **servidores de arquivos do BranchCache** e clique em **criar um GPO nesse domínio e vincule-o aqui**. A caixa de diálogo **Novo GPO** é aberta. Em **nome**, digite um nome para o novo GPO. Por exemplo, se desejar denominar o objeto como Publicação de Hash do BranchCache, digite **Publicação de Hash do BranchCache**. Clique em **OK**.



