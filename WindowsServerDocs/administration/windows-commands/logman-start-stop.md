---
title: logman start e logman stop
description: Artigo de referência para os comandos logman start e logman stop, que inicia um coletor de dados e define a hora de início como manual ou para um conjunto de coletores de dados e define a hora de término como manual.
ms.topic: reference
ms.assetid: a40006a1-876e-474b-aaf1-f365c730deea
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 9a684eb010d52e5aba01fee609f878cc5485a7d5
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639967"
---
# <a name="logman-start-and-logman-stop"></a>logman start e logman stop

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

O comando **Iniciar do logman** inicia um coletor de dados e define a hora de início como manual. O comando **logman Stop** interrompe um conjunto de coletores de dados e define a hora de término como manual.

## <a name="syntax"></a>Sintaxe

```
logman start <[-n] <name>> [options]
logman stop <[-n] <name>> [options]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| -s `<computer name>` | Execute o comando no computador remoto especificado. |
| -configuração `<value>` | Especifica o arquivo de configurações que contém as opções de comando. |
| [-n] `<name>` | Especifica o nome do objeto de destino. |
| -ETS | Envia comandos para sessões de rastreamento de eventos diretamente, sem salvar ou agendar. |
| -como | Executa a operação solicitada de forma assíncrona. |
| -? | Exibe a ajuda contextual. |

### <a name="examples"></a>Exemplos

Para iniciar o coletor de dados *perf_log*, no computador remoto *server_1*, digite:

```
logman start perf_log -s server_1
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando logman](logman.md)
