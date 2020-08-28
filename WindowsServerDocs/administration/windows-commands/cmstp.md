---
title: cmstp
description: Artigo de referência para cmstp, que instala ou remove um perfil de serviço do Gerenciador de conexões.
ms.topic: reference
ms.assetid: 34aad544-11c3-4e85-8bbf-5bc5a971da93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 99e5e3d81855069b8a4465d554e7d9699c4bc08e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030954"
---
# <a name="cmstp"></a>cmstp

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Instala ou remove um perfil de serviço do Gerenciador de conexões. Usado sem parâmetros opcionais, o **cmstp** instala um perfil de serviço com as configurações padrão apropriadas para o sistema operacional e para as permissões do usuário.

## <a name="syntax"></a>Sintaxe

Sintaxe 1-essa é a sintaxe típica usada em um aplicativo de instalação personalizada. Para usar essa sintaxe, você deve executar o **cmstp** a partir do diretório que contém o `<serviceprofilefilename>.exe` arquivo.

```
<serviceprofilefilename>.exe /q:a /c:cmstp.exe <serviceprofilefilename>.inf [/nf] [/s] [/u]
```

Sintaxe 2
```
cmstp.exe [/nf] [/s] [/u] [drive:][path]serviceprofilefilename.inf
```

#### <a name="parameters"></a>Parâmetros
| Parâmetro | Descrição |
| --------- | ----------- |
| `<serviceprofilefilename>.exe` | Especifica, por nome, o pacote de instalação que contém o perfil que você deseja instalar.<p>Necessário para a sintaxe 1, mas não é válido para a sintaxe 2. |
| /q: a | Especifica que o perfil deve ser instalado sem avisar o usuário. A mensagem de verificação de que a instalação foi bem-sucedida ainda será exibida.<p>Necessário para a sintaxe 1, mas não é válido para a sintaxe 2. |
| [unidade:] Multi-Path `<serviceprofilefilename>.inf` | Obrigatórios. Especifica, por nome, o arquivo de configuração que determina como o perfil deve ser instalado.<p>O parâmetro [unidade:] [caminho] não é válido para a sintaxe 1. |
| /nf | Especifica que os arquivos de suporte não devem ser instalados. |
| /s | Especifica que o perfil de serviço deve ser instalado ou desinstalado silenciosamente (sem solicitar a resposta do usuário ou exibir a mensagem de verificação). Esse é o único parâmetro que você pode usar em combinação com **/u**.|
| /u | Especifica que o perfil de serviço deve ser desinstalado. |
| /? | Exibe a ajuda no prompt de comando. |

## <a name="examples"></a>Exemplos

Para instalar o perfil de serviço *ficção* sem nenhum arquivo de suporte, digite:

```
fiction.exe /c:cmstp.exe fiction.inf /nf
```

Para instalar silenciosamente o perfil de serviço de *ficção* para um único usuário, digite:

```
fiction.exe /c:cmstp.exe fiction.inf /s /su
```

Para desinstalar silenciosamente o perfil de serviço *ficção* , digite:

```
fiction.exe /c:cmstp.exe fiction.inf /s /u
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)
