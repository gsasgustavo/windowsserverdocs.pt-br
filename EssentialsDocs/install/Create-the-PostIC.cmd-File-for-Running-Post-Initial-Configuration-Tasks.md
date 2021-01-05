---
title: Criar o Arquivo PostIC.cmd para Execução de Tarefas após a Configuração Inicial
description: Saiba como criar o arquivo postal. cmd para executar tarefas de configuração iniciais posteriores para o Windows Server Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 99e258bc-0695-48c9-b694-a7f3cbe2a2d0
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 8092714d1a2071f8e14d1f1dcc696bdb027a52ba
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711241"
---
# <a name="create-the-posticcmd-file-for-running-post-initial-configuration-tasks"></a>Criar o Arquivo PostIC.cmd para Execução de Tarefas após a Configuração Inicial

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Você pode adicionar personalizações à configuração pós-inicial escrevendo seu próprio código e então chamando esse código de um arquivo de script chamado PostIC.cmd. Ao usar o arquivo PostIC.cmd, é preciso cumprir as seguintes diretrizes:

- O código de personalização deve ser executado silenciosamente (não é possível exibir uma Interface de Usuário).

- O código de personalização não pode iniciar uma reinicialização do servidor. A Configuração Inicial irá reiniciar o servidor como a última tarefa.

- O código de personalização deve ser executado em três minutos ou menos.

  Configure o arquivo PostIC.cmd para retornar um 0 se o código for executado com êxito. Se for retornado qualquer outro valor, o sistema operacional procurará um arquivo nomeado [SetupFailure.cmd](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md#BKMK_SetupFailure), que contém um código que deverá ser executado caso o código do arquivo PostIC.cmd não seja executado com êxito. O arquivo PostIC.cmd e o arquivo SetupFailure.cmd devem estar localizados em C:\Windows\Setup\Scripts.

#### <a name="to-define-post-initial-configuration-customizations"></a>Para definir as personalizações após a configuração inicial

1.  Escreva o código chamado a partir do script PostIC.cmd.

2.  Usando o Bloco de Notas, crie um arquivo chamado PostIC.cmd e adicione a chamada ao código criado na etapa 1. Verifique se seu código retorna um valor de êxito.

3.  Salve PostIC.cmd em C:\Windows\Setup\Scripts.

4.  (Opcional) Crie um arquivo SetupFailure.cmd que executará o código se PostIC.cmd retornar algo diferente de 0.

###  <a name="setupfailurecmd"></a><a name="BKMK_SetupFailure"></a> SetupFailure. cmd
 Você pode fornecer notificação de problemas na Configuração Inicial usando SetupFailure.cmd. O arquivo SetupFailure.cmd contém o código que você deseja executar se ocorrerem problemas. O arquivo SetupFailure.cmd está em C:\Windows\Setup\Scripts e será executado em caso de problemas com uma tarefa de configuração ou quando o arquivo PostIC.cmd retornar um valor diferente de 0.

##### <a name="to-define-notifications"></a>Para definir notificações

1.  Escreva o código chamado a partir do script SetupFailure.cmd.

2.  Usando o Bloco de Notas, crie um arquivo chamado SetupFailure.cmd e adicione a chamada ao código criado na etapa 1. Verifique se seu código retorna um valor de êxito.

3.  Salve o SetupFailure.cmd em C:\Windows\Setup\Scripts.

## <a name="see-also"></a>Consulte Também
 [Introdução com o Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) [criando e personalizando a imagem](Creating-and-Customizing-the-Image.md) [personalizações adicionais](Additional-Customizations.md) [preparando a imagem para](Preparing-the-Image-for-Deployment.md) [testar a implantação da experiência do cliente](Testing-the-Customer-Experience.md)