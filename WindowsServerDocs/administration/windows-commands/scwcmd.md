---
title: Scwcmd
description: Artigo de referência para * * * *-
ms.topic: reference
ms.assetid: 188ae881-c7d4-4a7a-b967-8fdc79f5f345
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4095d022a9bd84033eebf63b63420dc400f2c594
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636877"
---
# <a name="scwcmd"></a>Scwcmd

> Aplica-se a: Windows Server 2012 R2, Windows Server 2012

A ferramenta de linha de comando Scwcmd.exe incluída com o ACS (Assistente de configuração de segurança) pode ser usada para executar as seguintes tarefas:
-   Configure um ou vários servidores com uma política gerada pelo ACS.
-   Analise um ou vários servidores com uma política gerada pelo ACS.
-   Exibir resultados da análise no formato HTML.
-   Reverter políticas do ACS.
-   Transforme uma política gerada pelo ACS em arquivos nativos com suporte pelo Política de Grupo.
-   Registrar uma extensão de banco de dados de configuração de segurança com o ACS.

Quando você usa **scwcmd** para configurar, analisar ou reverter uma política em um servidor remoto, o ACS deve ser instalado no servidor remoto.

## <a name="syntax"></a>Sintaxe

```
scwcmd <command> [<subcommand>]
```

### <a name="parameters"></a>Parâmetros

|Subcomando|Descrição|
|----------|-----------|
|/analyze|Determina se um computador está em conformidade com uma política.</br>Consulte [scwcmd: Analyze](scwcmd-analyze.md) for Syntax e Options.|
|/Configure|Aplica uma política de segurança gerada pelo ACS a um computador.</br>Consulte [scwcmd: Configure](scwcmd-configure.md) para obter a sintaxe e as opções.|
|/Register|Estende ou personaliza o banco de dados de configuração de segurança do ACS registrando um arquivo de banco de dados de configuração de segurança que contém definições de função, tarefa, serviço ou porta.</br>Consulte [scwcmd: Register](scwcmd-register.md) para sintaxe e opções.|
|/rollback|Aplica a política de reversão mais recente disponível e, em seguida, exclui essa política de reversão.</br>Consulte [scwcmd: Rollback](scwcmd-rollback.md) para obter a sintaxe e as opções.|
|/transform|Transforma um arquivo de política de segurança gerado usando o ACS em um novo objeto de Política de Grupo (GPO) no Active Directory Domain Services.</br>Confira a sintaxe [scwcmd: Transform](scwcmd-transform.md) e as opções.|
|/view|Renderiza um arquivo. xml usando uma transformação. xsl especificada.</br>Consulte [scwcmd: View](scwcmd-view.md) para obter a sintaxe e as opções.|
|/?|Exibe a ajuda no prompt de comando.|

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
