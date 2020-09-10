---
title: online disk
description: Artigo de referência do comando de disco online, que coloca o disco offline no estado online.
ms.topic: reference
ms.assetid: bc44a783-eaa4-40ca-be01-5703b5bf4eb3
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a2c33a85a8217963a220495e75efebf0c6999309
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627326"
---
# <a name="online-disk"></a>online disk

Coloca o disco offline no estado online. Para discos básicos, esse comando tenta colocar online o disco selecionado e todos os volumes nesse disco. Para discos dinâmicos, esse comando tenta colocar online todos os discos que não estão marcados como externos no computador local. Ele também tenta colocar todos os volumes online no conjunto de discos dinâmicos.

Se um disco dinâmico em um grupo de discos for colocado online e for o único disco do grupo, o grupo original será recriado e o disco será movido para esse grupo. Se houver outros discos no grupo e eles estiverem online, o disco será simplesmente adicionado de volta ao grupo. Se o grupo de um disco selecionado contiver volumes espelhados ou RAID-5, esse comando também ressincronizará esses volumes.

> [!NOTE]
> Um disco deve ser selecionado para que o comando de **disco online** tenha sucesso. Use o comando [selecionar disco](select-disk.md) para selecionar um disco e deslocar o foco para ele.

> [!IMPORTANT]
> Esse comando falhará se for usado em um disco somente leitura.

## <a name="syntax"></a>Sintaxe

```
online disk [noerr]
```

### <a name="parameters"></a>Parâmetros

Para obter instruções sobre como usar esse comando, consulte [reativar um disco dinâmico ausente ou offline](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc732026(v=ws.11)).

| Parâmetro | Descrição |
|--|--|
| NOERR | Somente para scripts. Quando um erro é encontrado, o DiskPart continua processando comandos como se o erro não tivesse ocorrido. Sem esse parâmetro, um erro faz com que o DiskPart saia com um código de erro. |

### <a name="examples"></a>Exemplos

Para colocar o disco com foco online, digite:

```
online disk
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
