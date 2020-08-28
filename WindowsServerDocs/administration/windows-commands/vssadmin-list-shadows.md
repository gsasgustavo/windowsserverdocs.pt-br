---
title: Vssadmin da lista de sombras
description: Uma descrição do comando VSSadmin list Shadows.
ms.topic: reference
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: ee35fd65a6fdab68b8f4e4155d52182980b2d0c9
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89022900"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin da lista de sombras

> Aplica-se a: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Lista todas as cópias de sombra existentes de um volume especificado. Se você usar esse comando sem parâmetros, ele exibirá todas as cópias de sombra de volume no computador na ordem determinada pelo **conjunto de cópias de sombra**.

## <a name="syntax"></a>Sintaxe

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

### <a name="parameters"></a>Parâmetros

|Parâmetro|Descrição|
|---|---|
|/for =\<ForVolumeSpec>|Especifica em qual volume as cópias de sombra serão listadas.|
|/Shadow =\<ShadowID>|Lista a cópia de sombra especificada por Shadowid. Para obter a ID da cópia de sombra, use o comando **VSSadmin list Shadows** . Ao digitar uma ID de cópia de sombra, use o seguinte formato, em que cada *X* representa um caractere hexadecimal:<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|

## <a name="additional-references"></a>Referências adicionais

* [Chave de sintaxe de linha de comando](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
