---
title: Exportar-imagem
description: Artigo de referência para Export-Image, que exporta uma imagem existente do repositório de imagens para outro arquivo de imagem do Windows (. wim).
ms.topic: reference
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: fb7cb7d955d507c6c4a3bd4ddb7434123f37b296
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89638346"
---
# <a name="export-image"></a>Exportar-imagem

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exporta uma imagem existente do repositório de imagens para outro arquivo de imagem do Windows (. wim).

## <a name="syntax"></a>Sintaxe
para imagens de inicialização:
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```
para imagens de instalação:
```
wdsutil [Options] /Export-Imagmedia:<Image name> [/Server:<Server name>]
   mediatype:InstallmediaGroup:<Image group name>]
     [/Filename:<File name>]
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No | append}]
```
### <a name="parameters"></a>Parâmetros
|Parâmetro|Descrição|
|-------|--------|
meio<Image name>|Especifica o nome da imagem a ser exportada.|
|[/Server:<Server name>]|Especifica o nome do servidor. Pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome de servidor for especificado, o servidor local será usado.|
MediaType: {boot &#124; install}|Especifica o tipo de imagem a ser exportada.|
|\mediaGroup: <Image group name> ]|Especifica o grupo de imagens que contém a imagem a ser exportada. Se nenhum nome de grupo de imagens for especificado e houver apenas um grupo de imagens no servidor, esse grupo de imagens será usado por padrão. Se houver mais de um grupo de imagens no servidor, o grupo de imagens deverá ser especificado.|
|/Architecture: {x86 &#124; IA64 &#124; x64}|Especifica a arquitetura da imagem a ser exportada. Como é possível ter o mesmo nome de imagem para imagens de inicialização em diferentes arquiteturas, especificar o valor da arquitetura garante que a imagem correta será retornada.|
|[/Filename:<Filename>]|se a imagem não puder ser identificada exclusivamente pelo nome, o nome do arquivo deverá ser especificado.|
|/DestinationImage|Especifica as configurações para a imagem de destino. Você pode especificar essas configurações usando as seguintes opções:<p>-/FilePath.: <File path and name> -especifica o caminho de arquivo completo para a nova imagem.<br />-[/Name: <Name> ] – define o nome de exibição da imagem. Se nenhum nome for especificado, o nome de exibição da imagem de origem será usado.<br />- [/Description: <Description>] – Define a descrição da imagem.|
|[/Overwrite: {Yes &#124; no &#124; Append}]|Determina se o arquivo especificado na opção **/DestinationImage** será substituído se já existir um arquivo existente com esse nome no/FilePath.<p>-   **Sim** faz com que o arquivo existente seja substituído.<br />-   **Não** (a opção padrão) faz com que ocorra um erro se já existir um arquivo com o mesmo nome.<br />-   **Append** faz com que a imagem gerada seja acrescentada como uma nova imagem dentro do arquivo. wim existente.|
## <a name="examples"></a>Exemplos
Para exportar uma imagem de inicialização, digite uma das seguintes opções:
```
wdsutil /Export-Imagmedia:WinPE boot imagemediatype:Boot /Architecture:x86 /DestinationImage /Filepath:C:\temp\boot.wim
wdsutil /verbose /Progress /Export-Imagmedia:WinPE boot image /Server:MyWDSServemediatype:Boot /Architecture:x64 /Filename:boot.wim
/DestinationImage /Filepath:\\Server\Share\ExportImage.wim /Name:Exported WinPE image /Description:WinPE Image from WDS server /Overwrite:Yes
```
Para exportar uma imagem de instalação, digite uma das seguintes opções:
```
wdsutil /Export-Imagmedia:Windows Vista with Officemediatype:Install /DestinationImage /Filepath:C:\Temp\Install.wim
wdsutil /verbose /Progress /Export-Imagmedia:Windows Vista with Office /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1
/Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:Exported Windows image /Description:Windows Vista image from WDS server /Overwrite:append
```
## <a name="additional-references"></a>Referências adicionais
- Chave de sintaxe [de linha de comando](command-line-syntax-key.md) 
 [Usando o comando](using-the-add-image-command.md) 
 Add-Image [Usando o comando](using-the-copy-image-command.md) 
 Copy-Image [Usando o comando](using-the-get-image-command.md) 
 Get-Image [Usando o comando](using-the-remove-image-command.md) 
 Remove-Image [Usando o comando](using-the-replace-image-command.md) 
 replace-Image [Subcomando: Set-Image](subcommand-set-image.md)
