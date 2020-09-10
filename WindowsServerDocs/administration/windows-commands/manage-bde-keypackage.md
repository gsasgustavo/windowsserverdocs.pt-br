---
title: Manage-bde pacote de pacotes
description: Artigo de referência para o comando Manage-bde KeyPackage, que gera um pacote de chaves para uma unidade.
ms.topic: reference
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: b183c06dfa73d20f7dc3236b88d5346a8694ec61
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639305"
---
# <a name="manage-bde-keypackage"></a>Manage-bde pacote de pacotes

Gera um pacote de chaves para uma unidade. O pacote de chaves pode ser usado em conjunto com a ferramenta de reparo para reparar unidades corrompidas.

## <a name="syntax"></a>Sintaxe

```
manage-bde -keypackage [<drive>] [-ID <keyprotectoryID>] [-path <pathtoexternalkeydirectory>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<drive>` | Representa uma letra de unidade seguida de dois-pontos. |
| -ID | Cria um pacote de chaves usando o protetor de chave com o identificador especificado por esse valor de ID. **Dica:** Use o comando **Manage-bde – protectors – get** , junto com a letra da unidade para a qual você deseja criar um pacote de chaves, para obter uma lista de GUIDs disponíveis para usar como o valor de ID. |
| -caminho | Especifica o local para salvar o pacote de chaves criado. |
| -ComputerName | Especifica que manage-bde.exe será usado para modificar a proteção do BitLocker em um computador diferente. Você também pode usar **-CN** como uma versão abreviada desse comando. |
| `<name>` | Representa o nome do computador no qual a proteção do BitLocker será modificada. Os valores aceitos incluem o nome NetBIOS do computador e o endereço IP do computador. |
| -? ou/? | Exibe a ajuda resumida no prompt de comando. |
| -Help ou-h | Exibe a ajuda completa no prompt de comando. |

### <a name="examples"></a>Exemplos

Para criar um pacote de chaves para a unidade C, com base no protetor de chave identificado pelo GUID, e para salvar o pacote de chaves em F:\Folder, digite:

```
manage-bde -keypackage C: -id {84E151C1...7A62067A512} -path f:\Folder
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Manage-bde](manage-bde.md)
