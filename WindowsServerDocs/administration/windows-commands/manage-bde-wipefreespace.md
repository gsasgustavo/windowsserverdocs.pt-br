---
title: Manage-bde wipefreespace
description: Artigo de referência para o comando Manage-bde wipefreespace, que apaga o espaço livre no volume, removendo quaisquer fragmentos de dados que possam ter existido no espaço.
ms.topic: reference
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d263a38545cd5cc59298c7e8bfdf7bc9a35b1b84
ms.sourcegitcommit: 6fbe337587050300e90340f9aa3e899ff5ce1028
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97599659"
---
# <a name="manage-bde-wipefreespace"></a>Manage-bde wipefreespace

Apaga o espaço livre no volume, removendo quaisquer fragmentos de dados que possam ter existido no espaço. Executar esse comando em um volume criptografado usando o método de criptografia **somente espaço usado** fornece o mesmo nível de proteção que o método de criptografia de **criptografia de volume completo** .

## <a name="syntax"></a>Sintaxe

```
manage-bde -wipefreespace|-w [<drive>] [-cancel] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<drive>` | Representa uma letra de unidade seguida de dois-pontos. |
| -cancelar | Cancela um apagamento de espaço livre em andamento. |
| -ComputerName | Especifica que manage-bde.exe será usado para modificar a proteção do BitLocker em um computador diferente. Você também pode usar **-CN** como uma versão abreviada desse comando. |
| `<name>` | Representa o nome do computador no qual a proteção do BitLocker será modificada. Os valores aceitos incluem o nome NetBIOS do computador e o endereço IP do computador. |
| -? ou/? | Exibe a ajuda resumida no prompt de comando. |
| -Help ou-h | Exibe a ajuda completa no prompt de comando. |

### <a name="examples"></a>Exemplos

Para apagar o espaço livre na unidade C, digite:

```
manage-bde -w C:
```

```
manage-bde -wipefreespace C:
```

Para cancelar o apagamento do espaço livre na unidade C, digite:

```
manage-bde -w -cancel C:
```

```
manage-bde -wipefreespace -cancel C:
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Manage-bde](manage-bde.md)
