---
title: WDSUTIL Get-meus dispositivos
description: Artigo de referência para o comando WDSUTIL Get-mydevices, que exibe as propriedades dos serviços de implantação do Windows de todos os computadores pré-configurados.
ms.topic: reference
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: a960a30fd61056e2e2eb183e8a873223daa78be2
ms.sourcegitcommit: 28b5ab74cb0b40539ccc1a83998d6391e87fe51f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96614868"
---
# <a name="wdsutil-get-alldevices"></a>WDSUTIL Get-meus dispositivos

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exibe as propriedades dos serviços de implantação do Windows de todos os computadores pré-configurados. Um computador pré-configurado é um computador físico que foi vinculado a uma conta de computador nos serviços de domínio Active Directory.

## <a name="syntax"></a>Sintaxe

```
wdsutil [options] /get-alldevices [/forest:{Yes | No}] [/referralserver:<servername>]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| `[/forest:{Yes | No}]` | Especifica se os serviços de implantação do Windows devem retornar computadores em toda a floresta ou no domínio local. A configuração padrão é **não**, o que significa que somente os computadores no domínio local são retornados. |
| `[/referralserver:<servername>]` | Retorna somente os computadores que são pré-configurados para o servidor especificado. |

## <a name="examples"></a>Exemplos

Para exibir todos os computadores, digite:

```
wdsutil /get-alldevices
```

```
wdsutil /verbose /get-alldevices /forest:Yes /referralserver:MyWDSServer
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [WDSUTIL Set-comando de dispositivo](wdsutil-set-device.md)

- [comando de adição de dispositivo WDSUTIL](wdsutil-add-device.md)

- [comando de Get-Device do WDSUTIL](wdsutil-get-device.md)
