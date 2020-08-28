---
title: Get-Server
description: Artigo de referência para Get-Server, que recupera informações do servidor de serviços de implantação do Windows especificado.
ms.topic: reference
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13bceebfb619fc93cbab7b2b45d3dd34838760ed
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89029494"
---
# <a name="get-server"></a>Get-Server

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Recupera informações do servidor de serviços de implantação do Windows especificado.

## <a name="syntax"></a>Sintaxe
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
### <a name="parameters"></a>Parâmetros
|Parâmetro|Descrição|
|-------|--------|
|[/Server:<Server name>]|Especifica o nome do servidor. Esse pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome de servidor for especificado, o servidor local será usado.|
|/Show: {config &#124; imagens &#124; todos}|Especifica o tipo de informações a serem retornadas.<p>-   **Config** retorna informações de configuração.<br />-   As **imagens** retornam informações sobre grupos de imagens, imagens de inicialização e imagens de instalação.<br />-   **Todos** retorna informações de configuração e informações de imagem.|
|[/detailed]|Você pode usar essa opção com **/show: images** ou **/show: ALL** para indicar que todos os metadados de imagem de cada imagem devem ser retornados. Se a opção **/detailed** não for usada, o comportamento padrão será retornar o nome da imagem, a descrição e o nome do arquivo.|
## <a name="examples"></a>Exemplos
Para exibir informações sobre o servidor, digite:
```
wdsutil /Get-Server /Show:Config
```
Para exibir informações detalhadas sobre o servidor, digite:
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>Referências adicionais
- Chave de sintaxe [de linha de comando](command-line-syntax-key.md) 
 [Usando o comando](using-the-disable-server-command.md) 
 Disable-Server [Usando o comando](using-the-enable-server-command.md) 
 Enable-Server [Usando o comando](using-the-initialize-server-command.md) 
 Initialize-Server [Subcomando: Set-Server](subcommand-set-server.md) 
 [Subcomando: Start-Server](subcommand-start-server.md) 
 [Subcomando: Stop-Server](subcommand-stop-server.md) 
 [A opção Uninitialize-Server](the-uninitialize-server-option.md)
