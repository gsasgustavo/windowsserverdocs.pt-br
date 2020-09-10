---
title: logman import e logman export
description: Artigo de referência para importação de Logman e exportação de logman, que importa um conjunto de coletores de dados de um arquivo XML ou exporta um conjunto de coletores de dados para um arquivo XML.
ms.topic: reference
ms.assetid: c258daba-fb93-47c0-a53b-2fe83ed2c743
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: eeb0c30011b70a6fa72bffca18b16ec11e27b958
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639988"
---
# <a name="logman-import-and-logman-export"></a>logman import e logman export

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Importa um conjunto de coletores de dados de um arquivo XML ou exporta um conjunto de coletores de dados para um arquivo XML.

## <a name="syntax"></a>Sintaxe

```
logman import <[-n] <name> <-xml <name> [options]
logman export <[-n] <name> <-xml <name> [options]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| -s `<computer name>` | Execute o comando no computador remoto especificado. |
| -configuração `<value>` | Especifica o arquivo de configurações que contém as opções de comando. |
| [-n] `<name>` | O nome do objeto de destino. |
| -XML `<name>` | Nome do arquivo XML a ser importado ou exportado. |
| -ETS | Envia comandos para sessões de rastreamento de eventos diretamente sem salvar ou agendar. |
| -[-] u `<user [password]>` | Especifica o usuário a ser executado como. Inserir um `*` para a senha produz um prompt para a senha. A senha não é exibida quando você a digita no prompt de senha. |
| -y | Responde sim a todas as perguntas sem avisar. |
| /? | Exibe a ajuda contextual. |

### <a name="examples"></a>Exemplos

Para importar o arquivo XML *c:\windows\perf_log.xml* do computador *server_1* como um conjunto de coletores de dados chamado *perf_log*, digite:

```
logman import perf_log -s server_1 -xml c:\windows\perf_log.xml
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando logman](logman.md)
