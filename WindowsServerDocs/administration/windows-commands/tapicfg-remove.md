---
title: remover Tapicfg
description: Artigo de referência para o comando Tapicfg remove, que remove uma partição de diretório de aplicativo TAPI.
ms.topic: reference
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 09/29/2020
ms.openlocfilehash: 5d5b7e1cc5d362d66041a292e86e022187896dea
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91729804"
---
# <a name="tapicfg-remove"></a>remover Tapicfg

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Remove uma partição de diretório de aplicativos TAPI.

> [!IMPORTANT]
> Você deve ser membro do grupo Administradores de empresa no Active Directory para executar esse comando.

## <a name="syntax"></a>Sintaxe

```
tapicfg remove /directory:<partitionname>
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| remova `/directory:<partitionname>` | Obrigatórios. Especifica o nome DNS da partição de diretório do aplicativo TAPI a ser removida. Observe que esse nome deve ser um nome de domínio totalmente qualificado. |
| /? | Exibe a ajuda no prompt de comando. |

#### <a name="remarks"></a>Comentários

- Essa ferramenta de linha de comando pode ser executada em qualquer computador que seja membro do domínio.

- O texto fornecido pelo usuário (como os nomes das partições de diretório do aplicativo TAPI, servidores e domínios) com caracteres internacionais ou Unicode só será exibido corretamente se as fontes apropriadas e o suporte a idioma estiverem instalados.

- Você ainda pode usar servidores ILS (serviço de localização da Internet) em sua organização, se o ILS for necessário para dar suporte a determinados aplicativos, porque os clientes TAPI que executam o Windows XP ou um sistema operacional Windows Server 2003 podem consultar servidores ILS ou partições de diretório de aplicativos TAPI.

- Você pode usar **Tapicfg** para criar ou remover pontos de conexão de serviço. Se a partição de diretório do aplicativo TAPI for renomeada por qualquer motivo (por exemplo, se você renomear o domínio no qual ele reside), será necessário remover o ponto de conexão de serviço existente e criar um novo que contenha o novo nome DNS da partição de diretório do aplicativo TAPI a ser publicada. Caso contrário, os clientes TAPI não poderão localizar e acessar a partição de diretório de aplicativos TAPI. Você também pode remover um ponto de conexão de serviço para fins de manutenção ou segurança (por exemplo, se não quiser expor dados TAPI em uma partição de diretório de aplicativo TAPI específica).

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [instalação de Tapicfg](tapicfg-install.md)

- [Tapicfg publishscp](tapicfg-publishscp.md)

- [Tapicfg removescp](tapicfg-removescp.md)

- [Tapicfg mostrar](tapicfg-show.md)

- [Tapicfg MakeDefault](tapicfg-makedefault.md)