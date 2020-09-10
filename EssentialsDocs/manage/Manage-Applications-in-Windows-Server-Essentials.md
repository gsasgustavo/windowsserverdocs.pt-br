---
title: Gerenciar aplicativos no Windows Server Essentials
description: Descreve como usar o Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: ae89c46a-0afd-4858-9150-ec97650f45a4
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 30b8dfa2087e76cc80011eb359715c95564ec1b6
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623270"
---
# <a name="manage-applications-in-windows-server-essentials"></a>Gerenciar aplicativos no Windows Server Essentials

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 O painel do servidor no Windows Server Essentials e no Windows Server 2012 R2 com a função de experiência do Windows Server Essentials instalada torna possível executar tarefas administrativas comuns. Para realizar essas tarefas, veja o seguinte:

-   [Tarefas de gerenciamento de aplicativos no Painel](Manage-Applications-in-Windows-Server-Essentials.md#BKMK_1)

-   [Instalar ou remover suplementos usando o Painel](Manage-Applications-in-Windows-Server-Essentials.md#BKMK_2)

##  <a name="application-management-tasks-in-the-dashboard"></a><a name="BKMK_1"></a> Tarefas de gerenciamento de aplicativos no painel
 A página de Gerenciamento de **Aplicativos** do Painel fornece:

- Uma lista de suplementos instalados, que exibe:

  -   O nome do serviço online ou suplemento

  -   O status de atualização do suplemento

  -   O status da assinatura de complemento

  -   O nome da empresa ou distribuidor que está disponibilizando o suplemento

- Um painel de tarefas que inclui um conjunto de tarefas para gerenciamento de um suplemento selecionado

- Uma lista de suplementos que estão disponíveis para download e instalação a partir do Microsoft Pinpoint

  A tabela a seguir descreve as várias tarefas de gerenciamento de suplemento que estão disponíveis no Painel do servidor. Algumas tarefas são específicas do suplemento, então, elas são visíveis apenas quando você seleciona um suplemento na lista.

|Nome da tarefa|Descrição|
|---------------|-----------------|
|Remover o suplemento|Remove o suplemento selecionado do servidor e de todos os outros computadores da rede.|
|Instalar o suplemento nos computadores da rede|Ajuda a programar a instalação do suplemento selecionado em todos os outros computadores da rede.|
|Obter ajuda com o suplemento|Abre o navegador da Internet em um site do qual você pode procurar soluções para problemas e saber mais sobre um suplemento selecionado.|
|Atualizar o suplemento|Ajuda a baixar e instalar atualizações para os suplementos instalados no seu servidor e nos computadores da rede.|
|Renovar a assinatura do suplemento|Abre seu navegador da Internet em um site do qual você pode renovar sua assinatura do suplemento.|
|Ler a política de privacidade do suplemento|Abre seu navegador da Internet em um site que possa exibir a política de privacidade.|
|Como fazer para instalar ou remover suplementos?|Abre seu navegador da Internet em uma página da Web que exibe o tópico de Ajuda do assunto.|

##  <a name="install-or-remove-add-ins-using-the-dashboard"></a><a name="BKMK_2"></a> Instalar ou remover suplementos usando o painel
 Um suplemento é um aplicativo de software que fornece recursos e funcionalidades adicionais para seu servidor. Um número crescente de suplementos está disponível da Microsoft e de outros ISVs (fornecedores de software independentes).

 Antes de você poder aproveitar a funcionalidade estendida que um suplemento fornece, você deve primeiro instalar o suplemento no servidor.

#### <a name="to-install-an-add-in-from-microsoft-pinpoint"></a>Para instalar um suplemento do Microsoft Pinpoint

1.  No painel do servidor, clique em **aplicativos**e, em seguida, clique na guia **Microsoft Pinpoint** .  Uma lista de suplementos disponíveis é exibida.

2.  Clique no suplemento que você deseja instalar. A página de informações do suplemento será exibida.

3.  Na página de informações do suplemento, clique em Download e siga as instruções na tela para baixar e instalar o suplemento.

4.  Siga as instruções no Assistente para instalar o suplemento.

5.  Quando a instalação for concluída, reinicie o Painel, abra a página **Aplicativos** do Painel do servidor e verifique se o suplemento aparece na exibição de lista.

#### <a name="to-install-an-add-in-from-another-provider"></a>Para instalar um suplemento de outro provedor

1.  Abra o Windows Explorer e navegue até o local do arquivo de instalação do suplemento.

2.  Clique duas vezes no arquivo para executar o Assistente de instalação.

3.  Siga as instruções no Assistente para instalar o suplemento.

4.  Quando a instalação for concluída, reinicie o Painel, abra a página **Aplicativos** e verifique se o suplemento aparece na exibição de lista.

#### <a name="to-remove-an-add-in"></a>Para remover um suplemento

1.  Abra o Painel do servidor.

2.  Clique na guia **Aplicativos**.

3.  Na guia **Suplementos**, selecione o suplemento que você deseja remover e em seguida, clique em **Remover o suplemento**.

4.  Na janela **Remover o suplemento**, clique em **Remover**.

    > [!NOTE]
    >  Talvez seja necessário reiniciar o Painel para remover completamente o suplemento.

## <a name="additional-references"></a>Referências adicionais

-   [Visão geral do painel](Overview-of-the-Dashboard-in-Windows-Server-Essentials.md)

-   [Gerenciar o Windows Server Essentials](Manage-Windows-Server-Essentials.md)
