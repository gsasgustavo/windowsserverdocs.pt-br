---
title: WDSUTIL Get-myImages
description: Artigo de referência para o comando WDSUTIL Get-myImages, que recupera informações sobre todas as imagens em um servidor.
ms.topic: reference
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2fe93036c5493baed122fede4b25b71349996536
ms.sourcegitcommit: 28b5ab74cb0b40539ccc1a83998d6391e87fe51f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96614928"
---
# <a name="wdsutil-get-allimages"></a>WDSUTIL Get-myImages

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Recupera informações sobre todas as imagens em um servidor.

## <a name="syntax"></a>Sintaxe

```
wdsutil /get-allimages [/server:<servername>] /show:{boot | install | legacyris | all} [/detailed]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| `[/server:<servername>]` | Especifica o nome do servidor. Pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome de servidor for especificado, o servidor local será usado. |
| `/show:{boot | install | legacyris | all}` | Quando a **inicialização** retorna apenas imagens de inicialização, **install** retorna imagens de instalação, bem como informações sobre os grupos de imagens que os contêm, **LEGACYRIS** retorna somente imagens de RIS (serviços de instalação remota) e **todas** as informações de imagem de inicialização, informações de instalação de imagem (incluindo informações sobre os grupos de imagens) e informações de imagem do RIS. |
| [/detailed] | Indica que todos os metadados de imagem de cada imagem devem ser retornados. Se essa opção não for usada, o comportamento padrão será retornar apenas o nome da imagem, a descrição e o nome do arquivo. |

## <a name="examples"></a>Exemplos

Para exibir informações sobre as imagens, digite:

```
wdsutil /get-allimages /show:install
```

```
wdsutil /verbose /get-allimages /server:MyWDSServer /show:all /detailed
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando de adição de imagem do WDSUTIL](wdsutil-add-image.md)

- [comando de cópia de imagem do WDSUTIL](wdsutil-copy-image.md)

- [comando WDSUTIL Export-Image](wdsutil-export-image.md)

- [comando de remoção de imagem do WDSUTIL](wdsutil-remove-image.md)

- [comando de substituição do WDSUTIL-imagem](wdsutil-replace-image.md)

- [WDSUTIL Set-Command Image](wdsutil-set-image.md)
