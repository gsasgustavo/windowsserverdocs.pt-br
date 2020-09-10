---
title: ksetup delkdc
description: Artigo de referência para o comando ksetup delkdc, que exclui instâncias de nomes de centro de distribuição de chaves (KDC) para o realm Kerberos.
ms.topic: reference
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6bdc53a77f822130553af9d88e18658227c899fa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639681"
---
# <a name="ksetup-delkdc"></a>ksetup delkdc

Exclui instâncias de nomes de centro de distribuição de chaves (KDC) para o realm Kerberos.

O mapeamento é armazenado no registro, em `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains` . Depois de executar esse comando, é recomendável verificar se o KDC foi removido e não aparece mais na lista.

> [!NOTE]
> Para remover dados de configuração de realm de vários computadores, use o snap-in **modelo de configuração de segurança** com distribuição de política, em vez de usar o comando **ksetup** explicitamente em computadores individuais.

## <a name="syntax"></a>Sintaxe

```
ksetup /delkdc <realmname> <KDCname>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<realmname>` | Especifica o nome DNS em maiúsculas, como CORP. CONTOSO.COM. Esse é o realm padrão que aparece quando você executa o comando **ksetup** e é o realm do qual você deseja excluir o KDC. |
| `<KDCname>` | Especifica o nome de domínio totalmente qualificado, diferenciando maiúsculas de minúsculas, como mitkdc.contoso.com. |

### <a name="examples"></a>Exemplos

Para exibir todas as associações entre o realm do Windows e o realm não Windows, e para determinar quais deles remover, digite:

```
ksetup
```

Para remover a associação, digite:

```
ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando ksetup](ksetup.md)

- [comando ksetup addkdc](ksetup-addkdc.md)