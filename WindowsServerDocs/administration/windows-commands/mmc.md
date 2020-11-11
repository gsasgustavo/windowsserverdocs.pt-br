---
title: mmc
description: Artigo de referência do comando MMC, que permite abrir um console específico do MMC, abrir o MMC no modo de autor ou especificar para abrir a versão de 32 bits ou 64 bits do MMC.
ms.topic: reference
ms.assetid: 7bfa4030-ce42-40fb-922f-2f5145a80872
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ac3ad08c59f384c23f916b824d8f80fff1378e8d
ms.sourcegitcommit: 429b7f14666642d0a3f7a48e5c5a0b0b145c8c23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94482064"
---
# <a name="mmc"></a>mmc

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Usando opções de linha de comando do MMC, você pode abrir um console do **MMC** específico, abrir o **MMC** no modo de autor ou especificar que a versão de 32 bits ou 64 bits do **MMC** esteja aberta.

## <a name="syntax"></a>Sintaxe

```
mmc <path>\<filename>.msc [/a] [/64] [/32]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| `<path>\<filename>.msc` | inicia o **MMC** e abre um console salvo. Você precisa especificar o caminho completo e o nome do arquivo do console salvo. Se você não especificar um arquivo de console, o **MMC** abrirá um novo console. |
| /a | Abre um console salvo no modo de autor.  Usado para fazer alterações em consoles salvos. |
| /64 | Abre a versão de 64 bits do **MMC** (MMC64). Use esta opção somente se você estiver executando um sistema operacional Microsoft de 64 bits e quiser usar um snap-in de 64 bits. |
| /32 | Abre a versão de 32 bits do **MMC** (MMC32). Ao executar um sistema operacional Microsoft de 64 bits, você pode executar snap-ins de 32 bits abrindo o MMC com essa opção de linha de comando quando tiver snap-ins somente de 32 bits. |

## <a name="remarks"></a>Comentários

- Você pode usar variáveis de ambiente para criar linhas de comando ou atalhos que não dependem do local explícito dos arquivos de console. Por exemplo, se o caminho para um arquivo de console estiver na pasta do sistema (por exemplo, **MMC c:\winnt\system32\ console_name. msc** ), você poderá usar a cadeia de caracteres de dados expansível **% systemroot%** para especificar o local ( **mmc% systemroot% \ system32 \ console_name. msc** ). Isso pode ser útil se você estiver delegando tarefas a pessoas em sua organização que estão trabalhando em computadores diferentes.

- Quando os consoles são abertos usando a opção **/a** , eles são abertos no modo de autor, independentemente do seu modo padrão. Isso não altera permanentemente a configuração de modo padrão para arquivos; Quando você omite essa opção, o MMC abre arquivos de console de acordo com suas configurações de modo padrão.

- Depois de abrir o **MMC** ou um arquivo de console no modo de autor, você pode abrir qualquer console existente clicando em **abrir** no menu do **console** .

- Você pode usar a linha de comando para criar atalhos para abrir o **MMC** e os consoles salvos. Um comando de linha de comando funciona com o comando **executar** no menu **Iniciar** , em qualquer janela de prompt de comando, em atalhos ou em qualquer arquivo ou programa em lotes que chame o comando.

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
