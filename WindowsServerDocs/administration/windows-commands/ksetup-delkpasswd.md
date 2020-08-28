---
title: ksetup delkpasswd
description: Artigo de referência para o comando ksetup delkpasswd, que remove um servidor de senha Kerberos (kpasswd) para um realm.
ms.topic: reference
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8918b429bc29cd2eec88f5c32d1e0c358fa2610
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025560"
---
# <a name="ksetup-delkpasswd"></a>ksetup delkpasswd

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Remove um servidor de senha Kerberos (kpasswd) para um realm.

## <a name="syntax"></a>Sintaxe

```
ksetup /delkpasswd <realmname> <kpasswdname>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<realmname>` |  Especifica o nome DNS em maiúsculas, como CORP. CONTOSO.COM e é listado como o realm ou **Realm padrão =** quando **ksetup** é executado. |
| `<kpasswdname>` | Especifica o servidor de senha Kerberos. Ele é declarado como um nome de domínio totalmente qualificado, que não diferencia maiúsculas de minúsculas, como mitkdc.contoso.com. Se o nome do KDC for omitido, o DNS poderá ser usado para localizar KDCs. |

### <a name="examples"></a>Exemplos

Para garantir o realm CORP. CONTOSO.COM usa o mitkdc.contoso.com do servidor KDC não Windows como o servidor de senha, digite:

```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```

Para garantir o realm CORP. CONTOSO.COM não está mapeado para um servidor de senha Kerberos (o nome do KDC), digite `ksetup` no computador com Windows e, em seguida, exiba a saída.

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando ksetup](ksetup.md)

- [comando ksetup delkpasswd](ksetup-delkpasswd.md)
