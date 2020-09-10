---
title: Migrar do Windows Server 2008 Foundation para o Windows Server Essentials
description: Descreve como usar o Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: f22fc0a4-cb82-4e60-afe6-2d03145745e7
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 7ccb0e79094c5d3393b9548fc733224fd8fa9cbf
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625870"
---
# <a name="migrate-windows-server-2008-foundation-to-windows-server-essentials"></a>Migrar do Windows Server 2008 Foundation para o Windows Server Essentials

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Este guia descreve como migrar um domínio existente do Windows Server 2008 Foundation para o Windows Server &reg; 2012 Essentials em novo hardware e, em seguida, migrar as configurações e os dados. Este guia também descreve como remover o servidor existente da rede do Windows Server Essentials depois de concluir a migração.

> [!NOTE]
>  Para evitar problemas durante a migração, a equipe de desenvolvimento de produtos do Windows Server Essentials recomenda enfaticamente que você leia este documento antes de começar a migração.

## <a name="additional-resources"></a>Recursos adicionais
 Para ter acesso a links com informações adicionais, ferramentas e recursos da comunidade com orientações sobre o processo de migração, visite o site de [Migração do Windows Small Business Server](https://go.microsoft.com/fwlink/?LinkId=217520).

## <a name="terms-and-definitions"></a>Termos e definições
 **Servidor de origem:** O servidor existente do qual você está migrando suas configurações e dados.

 **Servidor de destino:** O novo servidor para o qual você está migrando suas configurações e dados.

## <a name="migration-process-summary"></a>Resumo do processo de migração
 Este guia de migração inclui as seguintes etapas:


1.  [Prepare o servidor de origem para a migração do Windows Server Essentials](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Você deve garantir que o servidor de origem e a rede estejam prontos para a migração. Esta seção o guia pelos processos de backup do servidor de origem, avaliação da integridade do sistema do servidor de origem, instalação dos service packs e das correções mais recentes e verificação da configuração da rede.

2.  [Instale o Windows Server Essentials no modo de migração](Install-Windows-Server-Essentials-in-migration-mode.md).  Esta seção descreve as etapas que devem ser seguidas para instalar o Windows Server Essentials no servidor de destino no modo de migração.

3.  [Junte computadores à nova rede do Windows Server Essentials](Join-computers-to-the-new-Windows-Server-Essentials-network.md).  Esta seção aborda a adição de computadores cliente à nova rede do Windows Server Essentials e a atualização de Política de Grupo configurações.

4.  [Mova os dados e as configurações do Windows Server 2008 Foundation para o servidor de destino](./move-windows-server-2008-foundation-to-the-destination-server-for-migration.md).  Esta seção fornece informações sobre a migração de dados e configurações do servidor de origem.

5.  [Rebaixe e remova o servidor de origem da nova rede do Windows Server Essentials](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Antes da remoção do servidor de origem da rede, você deve forçar uma atualização da Política de Grupo e rebaixar o servidor de origem.

6.  [Executar tarefas de pós-implantação para a migração do Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Depois de concluir a migração de todas as configurações e dados para o Windows Server Essentials, talvez você queira mapear os computadores permitidos para as contas de usuário.

7.  [Execute o analisador de práticas recomendadas do Windows Server Essentials](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Depois de concluir a migração de configurações e dados para o Windows Server Essentials, você deve executar o BPA do Windows Server Essentials.


 Vários procedimentos de migração exigem a abertura de uma janela de prompt de comando como administrador.

###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a> Para abrir uma janela de prompt de comando no servidor de origem como administrador

1.  Clique em **Iniciar**.

2.  Na caixa de pesquisa, digite **cmd**.

3.  Na lista de resultados, clique com o botão direito em **cmd** e clique em **Executar como administrador**.

#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>Para abrir uma janela de prompt de comando no servidor de destino como administrador.

1.  Na tela **Início**, na caixa de pesquisa, digite **cmd**.

2.  Na lista de resultados, clique com o botão direito em **cmd** e clique em **Executar como administrador**.