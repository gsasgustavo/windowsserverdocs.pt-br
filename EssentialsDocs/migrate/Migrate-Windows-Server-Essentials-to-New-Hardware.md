---
title: Migrar do Windows Server Essentials para um novo hardware
description: Descreve como usar o Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: f695ae90-3160-407b-bebf-9e460f22c86d
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 704fc7fa97c949080104846011cf07e8e28da73a
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625866"
---
# <a name="migrate-windows-server-essentials-to-new-hardware"></a>Migrar do Windows Server Essentials para um novo hardware

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Este guia descreve como migrar um domínio existente do Windows Server &reg; 2012 Essentials para o Windows Server Essentials em um novo hardware e, em seguida, migrar as configurações e os dados. Este guia também descreve como remover o servidor existente da rede do Windows Server Essentials depois de concluir a migração.

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


1. [Prepare o servidor de origem para a migração do Windows Server Essentials](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Você deve garantir que o servidor de origem e a rede estejam prontos para a migração. Esta seção o guia pelos processos de backup do servidor de origem, avaliação da integridade do sistema do servidor de origem, instalação dos service packs e das correções mais recentes e verificação da configuração da rede.

2. [Instale o Windows Server Essentials no modo de migração](Install-Windows-Server-Essentials-in-migration-mode.md).  Esta seção descreve as etapas que devem ser seguidas para instalar o Windows Server Essentials no servidor de destino no modo de migração.

3. [Junte computadores ao novo servidor do Windows Server Essentials](Join-computers-to-the-new-Windows-Server-Essentials-server.md).  Esta seção aborda a adição de computadores cliente ao novo servidor do Windows Server Essentials e a atualização de Política de Grupo configurações.

4. [Mova as configurações e os dados para o servidor de destino para a migração do Windows Server Essentials](Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Esta seção fornece informações sobre a migração de dados e configurações do servidor de origem.

5. [Configure o redirecionamento de pasta no servidor de destino do Windows Server Essentials](Configure-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Caso o redirecionamento de pastas esteja habilitado no servidor de origem, você poderá habilitá-lo no servidor de destino e excluir a antiga configuração de Política de Grupo de Redirecionamento de Pastas.

6. [Rebaixe e remova o servidor de origem da nova rede do Windows Server Essentials](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Antes da remoção do servidor de origem da rede, você deve forçar uma atualização da Política de Grupo e rebaixar o servidor de origem.

7. [Executar tarefas de pós-implantação para a migração do Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Depois de concluir a migração de todas as configurações e dados para o Windows Server Essentials, talvez você queira mapear os computadores permitidos para as contas de usuário.

8. [Execute o analisador de práticas recomendadas do Windows Server Essentials](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Depois de concluir a migração de configurações e dados para o Windows Server Essentials, você deve baixar e executar o BPA do Windows Server Essentials.

   Vários procedimentos de migração exigem a abertura de uma janela de prompt de comando como administrador.

#### <a name="to-open-a-command-prompt-window-as-an-administrator"></a>Abra uma janela de Prompt de Comando como administrador.

1.  Na tela **Início**, na caixa de pesquisa, digite **cmd**.

2.  Na lista de resultados, clique com o botão direito em **cmd** e clique em **Executar como administrador**.
