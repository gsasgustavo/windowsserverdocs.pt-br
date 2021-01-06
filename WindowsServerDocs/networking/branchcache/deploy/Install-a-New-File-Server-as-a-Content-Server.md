---
title: Instalar um novo servidor de arquivos como um servidor de conteúdo
description: Saiba como instalar a função de servidor de serviços de arquivo e o BranchCache para o serviço de função de arquivos de rede em um computador que executa o Windows Server 2016.
manager: brianlic
ms.topic: how-to
ms.assetid: 1f49fc3c-28a6-4d3d-b787-1be9e61e792f
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: 29687cd09795b2b2a3b65b6d659fc9d047c80cf0
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949702"
---
# <a name="install-a-new-file-server-as-a-content-server"></a>Instalar um novo servidor de arquivos como um servidor de conteúdo

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para instalar a função de servidor de serviços de arquivo e o **BranchCache para** o serviço de função de arquivos de rede em um computador que executa o Windows Server 2016.

A associação a **Administradores** ou equivalente é o requisito mínimo para a execução deste procedimento.

> [!NOTE]
> Para executar esse procedimento usando o Windows PowerShell, execute o Windows PowerShell como administrador, digite os seguintes comandos no prompt do Windows PowerShell e pressione ENTER.
>
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`
>
> `Restart-Computer`
>
> Para instalar o serviço de função eliminação de duplicação de dados, digite o comando a seguir e pressione ENTER.
>
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`

### <a name="to-install-file-services-and-the-branchcache-for-network-files-role-service"></a>Para instalar os Serviços de Arquivo e o BranchCache para o serviço de função de arquivos de rede

1.  No Gerenciador do Servidor, clique em **Gerenciar** e depois em **Adicionar Funções e Recursos**. O Assistente para Adicionar Funções e Recursos é aberto. Em **Antes de Começar**, clique em **Avançar**.

2.  Em **Selecionar tipo de instalação**, verifique se a instalação baseada em **função ou em recurso** está selecionada e clique em **Avançar**.

3.  Em **selecionar servidor de destino**, verifique se o servidor correto está selecionado e clique em **Avançar**.

4.  Em **selecionar funções de servidor**, em **funções**, observe que a função **serviços de arquivo e armazenamento** já está instalada; Clique na seta à esquerda do nome da função para expandir a seleção de serviços de função e, em seguida, clique na seta à esquerda de **serviços de arquivo e iSCSI**.

5.  Marque as caixas de seleção do **servidor de arquivos** e **do BranchCache para arquivos de rede**.

    > [!TIP]
    > É recomendável que você também marque a caixa de seleção para **eliminação de duplicação de dados**.

    Clique em **Avançar**.

6.  Em **selecionar recursos**, clique em **Avançar**.

7.  Em **confirmar seleções de instalação**, examine suas seleções e clique em **instalar**. O painel **progresso da instalação** é exibido durante a instalação. Quando a instalação for concluída, clique em **fechar**.
