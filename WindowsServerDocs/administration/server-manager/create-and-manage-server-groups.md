---
title: Create and Manage Server Groups
description: Gerenciador do Servidor
ms.topic: article
ms.assetid: 9d5b1be8-49fd-4ff7-9580-e4ff21fe4b17
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b9afff5a5080487ee14759d27537b2ce1278f5e1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628336"
---
# <a name="create-and-manage-server-groups"></a>criar e gerenciar grupos de servidores

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Este tópico descreve como criar grupos de servidores personalizados e definidos pelo usuário no Gerenciador do Servidor no Windows Server.

## <a name="server-groups"></a><a name=BKMK_groups></a>Grupos de servidores
Os servidores que você adiciona ao pool de servidores são exibidos na página **todos os servidores** no Gerenciador do servidor. Você pode criar grupos personalizados de servidores adicionados. Os grupos de servidores permitem exibir e gerenciar um subconjunto menor de seu pool de servidores como uma unidade lógica; por exemplo, você pode criar um grupo chamado **servidores de contabilidade** para todos os servidores no departamento de contabilidade de sua organização ou um grupo chamado **Chicago** para todos os servidores que estão geograficamente localizados em Chicago. Depois de criar um grupo de servidores, o home page do grupo em Gerenciador do Servidor exibe informações sobre eventos, serviços, contadores de desempenho, resultados de Analisador de Práticas Recomendadas e funções e recursos instalados para o grupo como um todo.

Os servidores podem ser membros de mais de um grupo.

#### <a name="to-create-a-new-server-group"></a>Para criar um novo grupo de servidores

1.  No menu **gerenciar** , clique em **Criar grupo de servidores**.

2.  Na caixa de texto **Nome do grupo de servidores**, digite um nome fácil para seu grupo de servidores, como **Servidores Contábeis**.

3.  Adicione servidores à lista **selecionada** do pool de servidores ou adicione outros servidores ao grupo usando as guias **Active Directory**, **DNS**ou **Import** . Para obter mais informações sobre como usar essas guias, consulte [adicionar servidores a Gerenciador do servidor](add-servers-to-server-manager.md) neste guia.

4.  Após concluir a adição de servidores ao grupo, clique em **OK**. O novo grupo é exibido no painel de navegação Gerenciador do Servidor no grupo **todos os servidores** .

#### <a name="to-edit-an-existing-server-group"></a>Para editar um grupo de servidores existente

1.  Execute uma delas.

    -   No painel de navegação Gerenciador do Servidor, clique com o botão direito do mouse em um grupo de servidores e clique em **Editar grupo de servidores**.

    -   Na home page do grupo de servidores, abra o menu **tarefas** no bloco **servidores** e clique em **Editar grupo de servidores**.

2.  Altere o nome do grupo ou adicione ou remova servidores do grupo.

    > [!NOTE]
    > a remoção de servidores de um grupo de servidores não remove servidores do Gerenciador do Servidor. Os servidores removidos de um grupo permanecem no grupo **Todos os Servidores**, no pool de servidores.

3.  Após concluir as alterações no grupo, clique em **OK**.

#### <a name="to-delete-an-existing-server-group"></a>Para excluir um grupo de servidores existente

1.  Execute uma delas.

    -   No painel de navegação Gerenciador do Servidor, clique com o botão direito do mouse em um grupo de servidores e clique em **excluir grupo de servidores**.

    -   Na home page do grupo de servidores, abra o menu **tarefas** no bloco **servidores** e clique em **excluir grupo**de servidores.

2.  Quando for exibida uma mensagem perguntando se você deseja excluir o grupo de servidores, clique em **Sim**.

    > [!NOTE]
    > a exclusão de um grupo de servidores não remove servidores de Gerenciador do Servidor. Os servidores que estavam em um grupo excluído permanecem no grupo **Todos os Servidores**, no pool de servidores.

3.  Após concluir as alterações no grupo, clique em **OK**.

## <a name="see-also"></a>Consulte Também
[adicionar servidores a Gerenciador do servidor](add-servers-to-server-manager.md) 
 [Gerenciador do servidor](server-manager.md)



