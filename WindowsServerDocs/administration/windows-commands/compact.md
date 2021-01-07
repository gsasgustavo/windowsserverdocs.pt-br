---
title: compact
description: Artigo de referência para o comando Compact, que exibe ou altera a compactação de arquivos ou diretórios em partições NTFS.
ms.topic: reference
ms.assetid: 429b3752-df0a-43a4-a210-df2f3ad03c3b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 12c835071c06255a638e65f0bdb78b0d8816cb4d
ms.sourcegitcommit: 528bdff90a7c797cdfc6839e5586f2cd5f0506b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97977241"
---
# <a name="compact"></a>compact

Exibe ou altera a compactação de arquivos ou diretórios em partições NTFS. Se usado sem parâmetros, **Compact** exibe o estado de compactação do diretório atual e os arquivos que ele contém.

## <a name="syntax"></a>Sintaxe

```
compact [/C | /U] [/S[:dir]] [/A] [/I] [/F] [/Q] [/EXE[:algorithm]] [/CompactOs[:option] [/windir:dir]] [filename [...]]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
| --------- | ----------- |
| /c | Compacta o diretório ou arquivo especificado. Os diretórios são marcados para que todos os arquivos adicionados posteriormente sejam compactados, a menos que o parâmetro/EXE seja especificado. |
| /u | Descompacta o diretório ou arquivo especificado. Os diretórios são marcados para que todos os arquivos adicionados posteriormente não sejam compactados. Se o parâmetro/EXE for especificado, somente os arquivos compactados como executáveis serão descompactados; Se você não especificar o parâmetro/EXE, somente os arquivos compactados NTFS serão descompactados. |
| /s`[:<dir>]` | Executa a operação escolhida nos arquivos no diretório especificado e em todos os subdiretórios. Por padrão, o diretório atual é usado como o `<dir>` valor. |
| /a | Exibe arquivos ocultos ou do sistema. Por padrão, esses arquivos não são incluídos. |
| /i | Continua executando a operação especificada, ignorando erros. Por padrão, esse comando para quando um erro é encontrado. |
| /f | Força a compactação ou descompactação do diretório ou arquivo especificado. Os arquivos já compactados são ignorados por padrão. O parâmetro **/f** é usado no caso de um arquivo que foi parcialmente compactado quando a operação foi interrompida por uma falha do sistema. Para forçar o arquivo a ser compactado em sua totalidade, use os parâmetros **/c** e **/f** e especifique o arquivo parcialmente compactado. |
| /q | Relata apenas as informações mais essenciais. |
| /EXE | Usa a compactação otimizada para arquivos executáveis que são lidas com frequência, mas não modificadas. Os algoritmos com suporte são:<ul><li>**XPRESS4K** (valor mais rápido e padrão)</li><li>**XPRESS8K**</li><li>**XPRESS16K**</li><li>**LZX** (mais compacta)</li></ul> |
| /CompactOs | Define ou consulta o estado de compactação do sistema. As opções com suporte são:<ul><li>**Query** – consulta o estado **compacto** do sistema.</li><li>**sempre** -compacta todos os binários do sistema operacional e define o estado do sistema como Compact, o que permanece, a menos que o administrador o altere.</li><li>**nunca** – descompacta todos os binários do sistema operacional e define o estado do sistema como não compacto, o que permanece, a menos que o administrador o altere.</li></ul> |
| /windir | Usado com o parâmetro de **consulta/CompactOs:** ao consultar o sistema operacional offline. Especifica o diretório em que o Windows está instalado. |
| `<filename>` | Especifica um padrão, arquivo ou diretório. Você pode usar vários nomes de arquivo e o **&#42;** e **?** caracteres curinga. |
| /? | Exibe a ajuda no prompt de comando. |

#### <a name="remarks"></a>Comentários

- Esse comando é a versão de linha de comando do recurso de compactação do sistema de arquivos NTFS. O estado de compactação de um diretório indica se os arquivos são compactados automaticamente quando são adicionados ao diretório. Definir o estado de compactação de um diretório não altera necessariamente o estado de compactação dos arquivos que já estão no diretório.

- Você não pode usar esse comando para ler, gravar ou montar volumes compactados usando o DriveSpace ou o DoubleSpace. Você também não pode usar esse comando para compactar partições FAT (tabela de alocação de arquivos) ou FAT32.

## <a name="examples"></a>Exemplos

Para definir o estado de compactação do diretório atual, seus subdiretórios e arquivos existentes, digite:

```
compact /c /s
```

Para definir o estado de compactação de arquivos e subdiretórios no diretório atual, sem alterar o estado de compactação do próprio diretório atual, digite:

```
compact /c /s *.*
```

Para compactar um volume, no diretório raiz do volume, digite:

```
compact /c /i /s:\
```

> [!NOTE]
> Este exemplo define o estado de compactação de todos os diretórios (incluindo o diretório raiz no volume) e compacta todos os arquivos no volume. O parâmetro **/i** impede que mensagens de erro interrompam o processo de compactação.

Para compactar todos os arquivos com a extensão de nome de arquivo. bmp no diretório \tmp e todos os subdiretórios de \tmp, sem modificar o atributo compactado dos diretórios, digite:

```
compact /c /s:\tmp *.bmp
```

Para forçar a compactação completa do arquivo *zebra.bmp*, que foi parcialmente compactado durante uma falha do sistema, digite:

```
compact /c /f zebra.bmp
```

Para remover o atributo compactado do diretório c:\tmp, sem alterar o estado de compactação de todos os arquivos nesse diretório, digite:

```
compact /u c:\tmp
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)