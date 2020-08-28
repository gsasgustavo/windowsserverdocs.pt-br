---
title: fsutil transaction
description: Artigo de referência para o comando fsutil Transaction, que gerencia transações NTFS.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
ms.topic: reference
ms.date: 10/16/2017
ms.openlocfilehash: 4eeefc4e98e621cf44baa881c69ccbe36d20a689
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89032934"
---
# <a name="fsutil-transaction"></a>fsutil transaction

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Gerencia transações de NTFS.

## <a name="syntax"></a>Sintaxe

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <filename>
fsutil transaction [list]
fsutil transaction [query] [{files | all}] <GUID>
fsutil transaction [rollback] <GUID>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| confirmar | Marca o fim de uma transação especificada implícita ou explícita bem-sucedida. |
| `<GUID>` | Especifica o valor GUID que representa uma transação. |
| FileInfo  | Exibe informações de transação para o arquivo especificado. |
| `<filename>` | Especifica o caminho completo e nome de arquivo. |
| list | Exibe uma lista de transações em execução. |
| Consulta | Exibe informações para a transação especificada.<ul><li>Se `fsutil transaction query files` for especificado, as informações do arquivo serão exibidas somente para a transação especificada.</li><li>Se `fsutil transaction query all` for especificado, todas as informações da transação serão exibidas.</li></ul> |
| reversão | Reverte uma transação especificada para o início. |

### <a name="examples"></a>Exemplos

Para exibir as informações da transação para o arquivo *c:\test.txt*, digite:

```
fsutil transaction fileinfo c:\test.txt
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [NTFS transacional](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v=ws.10))
