---
title: Adicionar pasta de destino
description: Este tópico descreve como adicionar destinos de pasta (caminhos UNC)
ms.author: jgerend
manager: brianlic
ms.topic: article
author: jasongerend
ms.date: 12/10/2020
ms.openlocfilehash: 354047e2882a14d33b43b1bef609120b06202e47
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946942"
---
# <a name="add-folder-targets"></a>Adicionar destinos de pasta

> Aplica-se a: Windows Server 2019, Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Um destino de pasta é o caminho UNC (Convenção de Nomenclatura Universal) de uma pasta compartilhada ou outro namespace associado a uma pasta em um namespace. A adição de vários destinos de pasta aumenta a disponibilidade da pasta no namespace.

## <a name="to-add-a-folder-target"></a>Para adicionar uma pasta alvo

Para adicionar uma pasta usando gerenciamento DFS, use o procedimento a seguir:

1.  Clique em **Iniciar**, aponte para **Ferramentas Administrativas** e clique em **Gerenciamento DFS**.

2.  Na árvore de console, no nó **Namespaces**, clique com o botão direito do mouse em uma pasta e, em seguida, clique em **Adicionar alvo de pasta**.

3.  Digite o caminho para o destino de pasta ou clique em **procurar** para localizar o destino de pasta.

4.  Se a pasta é replicada usando a replicação DFS, você pode especificar se você deseja adicionar o novo destino de pasta para o grupo de replicação.

> [!TIP]
> Para adicionar um alvo de pasta usando o Windows PowerShell, use o [New-DfsnFolderTarget](/powershell/module/dfsn/new-dfsnfoldertarget). O módulo do Windows PowerShell de DFSN foi apresentado no Windows Server 2012.

> [!NOTE]
> As pastas podem conter destinos de pasta ou outras pastas DFS, mas não ambos, no mesmo nível na hierarquia de pastas.

## <a name="additional-references"></a>Referências adicionais

-   [Implantar namespaces do DFS](deploying-dfs-namespaces.md)
-   [Delegar permissões de gerenciamento para namespaces do DFS](delegate-management-permissions-for-dfs-namespaces.md)
-   [Replicar destinos de pasta usando Replicação do DFS](replicate-folder-targets-using-dfs-replication.md)
