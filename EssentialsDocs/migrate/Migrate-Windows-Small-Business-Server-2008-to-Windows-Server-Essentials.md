---
title: Migrar do Windows Small Business Server 2008 para o Windows Server Essentials
description: Saiba como migrar um domínio existente do Windows SBS 2008 para o Windows Server 2012 Essentials em novo hardware e, em seguida, migre as configurações e os dados.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 71e3243e-2da9-409a-ae1f-813d4c9062e1
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 1c8e6a52fbb9292e21d4eb17e086a4f78e1fadaa
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810863"
---
# <a name="migrate-windows-small-business-server-2008-to-windows-server-essentials"></a>Migrar do Windows Small Business Server 2008 para o Windows Server Essentials

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Este guia descreve como migrar um domínio existente do Windows SBS 2008 para o Windows Server &reg; 2012 Essentials em novo hardware e, em seguida, migrar as configurações e os dados. Este guia também descreve como remover o servidor existente da rede do Windows Server Essentials depois de concluir a migração.

> [!NOTE]
>  Para evitar problemas durante a migração, a equipe de desenvolvimento de produtos do Windows Server Essentials recomenda enfaticamente que você leia este documento antes de começar a migração.
>
> [!NOTE]
>
>  Para migrar os dados do servidor para a versão mais recente do Windows Server Essentials, consulte [migrar para o Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).


## <a name="additional-resources"></a>Recursos adicionais
 Para ter acesso a links com informações adicionais, ferramentas e recursos da comunidade com orientações sobre o processo de migração, visite o site [Migração do Windows Small Business Server](https://go.microsoft.com/fwlink/?LinkId=217520).

## <a name="terms-and-definitions"></a>Termos e definições
 **Servidor de origem:** O servidor existente do qual você está migrando suas configurações e dados.

 **Servidor de destino:** O novo servidor para o qual você está migrando suas configurações e dados.

## <a name="migration-process-summary"></a>Resumo do processo de migração
 Este guia de migração inclui as seguintes etapas:


1.  [Prepare o servidor de origem para a migração do Windows Server Essentials](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Você deve garantir que o servidor de origem e a rede estejam prontos para a migração. Esta seção o guia pelos processos de backup do servidor de origem, avaliação da integridade do sistema do servidor de origem, instalação dos service packs e das correções mais recentes e verificação da configuração da rede.

2.  [Instale o Windows Server Essentials no modo de migração](Install-Windows-Server-Essentials-in-migration-mode.md).  Esta seção descreve as etapas que devem ser seguidas para instalar o Windows Server Essentials no servidor de destino no modo de migração.

3.  [Junte computadores à nova rede do Windows Server Essentials](Join-computers-to-the-new-Windows-Server-Essentials-network.md).  Esta seção aborda a adição de computadores cliente à nova rede do Windows Server Essentials e a atualização de Política de Grupo configurações.

4.  [Mova os dados e as configurações do SBS 2008 para o servidor de destino](./move-windows-sbs-2008-to-the-destination-server-for-migration.md).  Esta seção fornece informações sobre a migração de dados e configurações do servidor de origem.

5.  [Habilite o redirecionamento de pasta no servidor de destino do Windows Server Essentials](Enable-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Caso o redirecionamento de pastas esteja habilitado no servidor de origem, você poderá habilitá-lo no servidor de destino e excluir a antiga configuração de Política de Grupo de Redirecionamento de Pastas.

6.  [Rebaixe e remova o servidor de origem da nova rede do Windows Server Essentials](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Antes da remoção do servidor de origem da rede, você deve forçar uma atualização da Política de Grupo e rebaixar o servidor de origem.

7.  [Executar tarefas de pós-implantação para a migração do Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Depois de concluir a migração de todas as configurações e dados para o Windows Server Essentials, talvez você queira mapear os computadores permitidos para as contas de usuário.

8.  [Execute o analisador de práticas recomendadas do Windows Server Essentials](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Depois de concluir a migração de configurações e dados para o Windows Server Essentials, você deve executar o BPA do Windows Server Essentials.


 Vários procedimentos de migração exigem a abertura de uma janela de prompt de comando como administrador.

###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a> Para abrir uma janela de prompt de comando no servidor de origem como administrador

1.  Clique em Iniciar.

2.  Na caixa de pesquisa, digite cmd.

3.  Na lista de resultados, clique com botão direito cmd e, em seguida, clique em Executar como administrador.

#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>Para abrir uma janela de prompt de comando no servidor de destino como administrador.

1.  Na tela **Início**, na caixa de pesquisa, digite **cmd**.

2.  Na lista de resultados, clique com o botão direito em **cmd** e clique em **Executar como administrador**.