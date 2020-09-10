---
title: rpcinfo
description: Artigo de referência do comando rpcinfo, que lista os programas em um computador remoto.
ms.topic: reference
ms.assetid: 7c342232-a8f0-42ff-8f11-d18c4981f5ca
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 3e5865bb976f71b9fbb90e4dd77008f00056a455
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639828"
---
# <a name="rpcinfo"></a>rpcinfo

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Lista os programas em computadores remotos. O utilitário de linha de comando **rpcinfo** faz uma chamada de procedimento remoto (RPC) para um servidor RPC e relata o que ele encontra.

## <a name="syntax"></a>Sintaxe

```
rpcinfo [/p [<node>]] [/b <program version>] [/t <node program> [<version>]] [/u <node program> [<version>]]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| /p `[<node>]` | lista todos os programas registrados com o mapeador de porta no host especificado. Se você não especificar um nome de nó (computador), o programa consultará o mapeador de porta no host local. |
| /b. `<program version>` | Solicita uma resposta de todos os nós de rede que têm o programa e a versão especificados registrados com o mapeador de porta. Você deve especificar um nome de programa ou número e um número de versão. |
| /t `<node program> [\<version>]` | Usa o protocolo de transporte TCP para chamar o programa especificado. Você deve especificar um nome de nó (computador) e um nome de programa. Se você não especificar uma versão, o programa chamará todas as versões. |
| /u `<node program> [\<version>]` | Usa o protocolo de transporte UDP para chamar o programa especificado. Você deve especificar um nome de nó (computador) e um nome de programa. Se você não especificar uma versão, o programa chamará todas as versões. |
| /? | Exibe a ajuda no prompt de comando. |

## <a name="examples"></a>Exemplos

Para listar todos os programas registrados com o mapeador de porta, digite:

```
rpcinfo /p [<node>]
```

Para solicitar uma resposta de nós de rede que têm um programa especificado, digite:

```
rpcinfo /b <program version>
```

Para usar o protocolo TCP para chamar um programa, digite:

```
rpcinfo /t <node program> [<version>]
```

Use UDP (User Datagram Protocol) para chamar um programa:

```
rpcinfo /u <node program> [<version>]
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
