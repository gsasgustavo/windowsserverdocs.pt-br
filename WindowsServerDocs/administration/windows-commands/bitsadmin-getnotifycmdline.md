---
title: bitsadmin getnotifycmdline
description: Artigo de referência para o comando Bitsadmin getnotifycmdline, que recupera o comando de linha de comando que é executado quando o trabalho termina de transferência de dados.
ms.topic: reference
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 26b2f50520f0b77f5792b279513caedaf560eea9
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631927"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

Recupera o comando de linha de comando a ser executado depois que o trabalho especificado terminar de transferir dados.

> [!NOTE]
> Esse comando não tem suporte no BITS 1,2 e versões anteriores.

## <a name="syntax"></a>Sintaxe

```
bitsadmin /getnotifycmdline <job>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| -------------- | -------------- |
| trabalho | O nome de exibição ou o GUID do trabalho. |

## <a name="examples"></a>Exemplos

Para recuperar o comando de linha de comando usado pelo serviço quando o trabalho chamado *myDownloadJob* for concluído.

```
bitsadmin /getnotifycmdline myDownloadJob
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando Bitsadmin](bitsadmin.md)
