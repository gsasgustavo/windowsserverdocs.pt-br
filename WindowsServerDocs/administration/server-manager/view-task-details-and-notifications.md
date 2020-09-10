---
title: Exibir detalhes e notificações de tarefas
description: Gerenciador do Servidor
ms.topic: article
ms.assetid: 95117407-2dd3-4f9a-841f-4331be3544c3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 096fdab1cb44f1d71b8db81270396aeea0727fb9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627721"
---
# <a name="view-task-details-and-notifications"></a>Exibir detalhes e notificações de tarefas

>Aplica-se a: Windows Server 2016

Em Gerenciador do Servidor no Windows Server 2012 R2 ou no Windows Server 2012, quando você executa tarefas de gerenciamento, como adicionar funções e recursos, iniciar serviços, atualizar dados que são exibidos no console do Gerenciador do Servidor ou criar um grupo personalizado de servidores, uma notificação é exibida na área **notificações** do cabeçalho do console do Gerenciador do servidor. Notificações e a caixa de diálogo **detalhes da tarefa** que você pode abrir no menu **notificações** clicando no ícone de sinalizador, exibe o status das tarefas ou solicitações do usuário, mostra se uma tarefa falhou e ajuda a solucionar problemas apontando para mensagens de erro detalhadas sobre falhas de tarefas.

## <a name="the-notifications-area"></a>A área de Notificações
A área de **notificações** na barra de menus Gerenciador do servidor, marcada por um ícone de sinalizador, exibe os resultados das tarefas que você inicia em Gerenciador do servidor. As notificações informam se as tarefas iniciadas no Gerenciador do Servidor foram bem-sucedidas ou falharam. Quando há notificações disponíveis para você exibir, o número de notificações disponíveis é exibido ao lado do ícone de sinalizador. Se uma tarefa falhou, pôde ser concluída apenas parcialmente (por exemplo, se não foi possível concluí-la em todos os servidores remotos nos quais você desejava executar a tarefa) ou foi concluída com avisos, o sinalizador **Notificações** fica vermelho. As tarefas para as quais são exibidas notificações incluem as seguintes.

-   Atualizar manualmente os dados exibidos no Gerenciador do Servidor (as notificações são exibidas para atualizações automáticas somente se as atualizações falharem)

-   iniciando e parando serviços

-   Instalando ou desinstalando funções, serviços de função e recursos

-   Iniciando uma verificação de Analisador de Práticas Recomendadas (BPA)

-   Adicionando servidores remotos para gerenciar (as notificações são exibidas para falhas para contatar ou atualizar os dados exibidos para servidores remotos)

Os itens no menu **Notificações** mostram uma barra de progresso, uma breve descrição da tarefa, o nome do servidor de destino da tarefa (ou um dos servidores de destino, se foram selecionados vários servidores de destino), um link para um controle ou uma caixa de diálogo relacionada, se aplicável, e um menu **Tarefas**. O menu **Tarefas** mostra os comandos que se aplicam à notificação ativa (a notificação sobre a qual o cursor do mouse está focalizado). Por exemplo, se você parar um serviço, poderá clicar em **Reiniciar** no menu **Tarefas** na notificação para reiniciar o serviço.

As notificações são particularmente úteis para instalar ou desinstalar funções, serviços de função e recursos. Por exemplo, se você iniciar uma instalação de recurso em um servidor remoto, poderá fechar o assistente para adicionar funções e recursos enquanto a instalação ainda estiver em andamento, mas a tarefa ativa permanecerá na lista de **notificações** . O item **notificações** mostra uma barra de progresso para a instalação e permite reabrir o assistente para adicionar funções e recursos, se necessário, clicando em **Adicionar Assistente de funções e recursos**. Os itens nessa lista informam se uma instalação falhou ou se são necessárias etapas de configuração adicionais para concluir a implantação do recurso.

As notificações também desempenham uma parte importante na solução de problemas com tarefas ou processos no Gerenciador do Servidor. Para obter mais informações sobre como usar mensagens na área de **notificações** e na caixa de diálogo **detalhes da tarefa** para solucionar problemas de tarefas ou processos sem êxito, consulte o [Fórum Gerenciador do servidor](/answers/topics/windows-server-manager.html).

Para excluir uma notificação que você não deseja mais ver na lista de **notificações** , passe o cursor do mouse sobre a notificação e clique em **remover tarefa** (**X**).

## <a name="viewing-and-troubleshooting-tasks-by-using-task-details"></a>Exibindo e Solucionando problemas de tarefas usando os detalhes da tarefa
O comando **detalhes da tarefa** na parte inferior do menu **notificações** abre a caixa de diálogo detalhes da **tarefa** , que fornece descrições completas dos eventos de tarefa (iniciando, parando, avisos, êxitos ou falhas). Como outros controles de lista em Gerenciador do Servidor, como **eventos**, **Serviços**e blocos de **analisador de práticas recomendadas** , você pode filtrar e criar consultas para serem executadas nas tarefas que são exibidas na caixa de diálogo **detalhes da tarefa** . (para obter mais informações sobre filtragem e criação de consultas em controles de lista, consulte [Filtrar, classificar e consultar dados em blocos de Gerenciador do servidor](filter-sort-and-query-data-in-server-manager-tiles.md).) No painel superior, você pode examinar as notificações conforme elas foram exibidas no menu **notificações** e ver quantas notificações foram geradas sobre a mesma tarefa. a seleção de uma notificação no painel superior exibe detalhes completos sobre a notificação no painel inferior.

O painel inferior é especialmente útil para solucionar problemas de tarefas com falha. Se Gerenciador do Servidor não puder se conectar ou obter dados para um servidor que seja membro do pool de servidores, as entradas nesse painel geralmente contêm mensagens detalhadas, incluindo o texto completo de problemas subjacentes de gerenciamento remoto do Windows (WinRM), rede ou segurança que impedem Gerenciador do Servidor de se comunicar com um servidor de destino.

## <a name="see-also"></a>Consulte Também
[Filtrar, classificar e consultar dados em blocos](filter-sort-and-query-data-in-server-manager-tiles.md) 
 de Gerenciador do servidor [Gerenciador do servidor Fórum](/answers/topics/windows-server-manager.html).