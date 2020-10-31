---
title: WDSUTIL exportar-imagem
description: Artigo de referência do comando WDSUTIL Export-Image, que exporta uma imagem existente do repositório de imagens para outro arquivo de imagem do Windows (. wim).
ms.topic: reference
ms.assetid: a9b8b467-0f2d-4754-8998-55503a262778
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8c3c390e43cc8707d8d94ade757130276b5f2753
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93071038"
---
# <a name="wdsutil-export-image"></a>WDSUTIL exportar-imagem

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exporta uma imagem existente do repositório de imagens para outro arquivo de imagem do Windows (. wim).

## <a name="syntax"></a>Syntax

Para imagens de inicialização:

```
wdsutil [options] /Export-Image image:<Image name> [/Server:<Servername>]
    imagetype:Boot /Architecture:{x86 | ia64 | x64} [/Filename:<Filename>]
     /DestinationImage
         /Filepath:<Filepath and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No}]
```

Para imagens de instalação:

```
wdsutil [options] /Export-Image image:<Image name> [/Server:<Servername>]
    imagetype:Install imageGroup:<Image group name>]
     [/Filename:<Filename>]
     /DestinationImage
         /Filepath:<Filepath and name>
         [/Name:<Name>]
         [/Description:<Description>]
     [/Overwrite:{Yes | No | append}]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| imagem`<Imagename>` | Especifica o nome da imagem a ser exportada. |
| [/Server:`<Servername>`] | Especifica o nome do servidor. Pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome de servidor for especificado, o servidor local será usado. |
| ImageType`{Boot|Install}` | Especifica o tipo de imagem a ser exportada. |
| \imageGroup: `<Image group name>` ] | Especifica o grupo de imagens que contém a imagem a ser exportada. Se nenhum nome de grupo de imagens for especificado e houver apenas um grupo de imagens no servidor, esse grupo de imagens será usado por padrão. Se houver mais de um grupo de imagens no servidor, o grupo de imagens deverá ser especificado. |
| Arquitectura`{x86|ia64|x64}` | Especifica a arquitetura da imagem a ser exportada. Como é possível ter o mesmo nome de imagem para imagens de inicialização em diferentes arquiteturas, especificar o valor da arquitetura garante que a imagem correta será retornada. |
| [/Filename:`<Filename>`] | se a imagem não puder ser identificada exclusivamente pelo nome, o nome do arquivo deverá ser especificado. |
| /DestinationImage | Especifica as configurações para a imagem de destino. Você pode especificar essas configurações usando as seguintes opções:<ul><li>`/Filepath:<Filepath and name>` -Especifica o caminho de arquivo completo para a nova imagem.</li><li>`[/Name:<Name>]` – Define o nome de exibição da imagem. Se nenhum nome for especificado, o nome de exibição da imagem de origem será usado.</li><li>`[/Description: <Description>]` – Define a descrição da imagem.</li></ul> |
| [/Overwrite: `{Yes|No|append}` ] | Determina se o arquivo especificado na opção **/DestinationImage** será substituído se já existir um arquivo existente com esse nome no/FilePath. A opção **Sim** faz com que o arquivo existente seja substituído, a opção **não** (padrão) faz com que um erro ocorra se um arquivo com o mesmo nome já existir e a opção **acrescentar** fizer com que a imagem gerada seja anexada como uma nova imagem no arquivo. wim existente. |

## <a name="examples"></a>Exemplos

Para exportar uma imagem de inicialização, digite:

```
wdsutil /Export-Image image:WinPE boot image imagetype:Boot /Architecture:x86 /DestinationImage /Filepath:C:\temp\boot.wim
```

```
wdsutil /verbose /Progress /Export-Image image:WinPE boot image /Server:MyWDSServer imagetype:Boot /Architecture:x64 /Filename:boot.wim /DestinationImage /Filepath:\\Server\Share\ExportImage.wim /Name:Exported WinPE image /Description:WinPE Image from WDS server /Overwrite:Yes
```

Para exportar uma imagem de instalação, digite:

```
wdsutil /Export-Image image:Windows Vista with Office imagetype:Install /DestinationImage /Filepath:C:\Temp\Install.wim
```

```
wdsutil /verbose /Progress /Export-Image image:Windows Vista with Office /Server:MyWDSServer imagetype:Instal imageGroup:ImageGroup1 /Filename:install.wim /DestinationImage /Filepath:\\server\share\export.wim /Name:Exported Windows image /Description:Windows Vista image from WDS server /Overwrite:append
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando de adição de imagem do WDSUTIL](wdsutil-add-image.md)

- [comando de cópia de imagem do WDSUTIL](wdsutil-copy-image.md)

- [comando de Get-Image do WDSUTIL](wdsutil-get-image.md)

- [comando de remoção de imagem do WDSUTIL](wdsutil-remove-image.md)

- [comando de substituição do WDSUTIL-imagem](wdsutil-replace-image.md)

- [WDSUTIL Set-Command Image](wdsutil-set-image.md)

- [Cmdlets dos serviços de implantação do Windows](/powershell/module/wds)