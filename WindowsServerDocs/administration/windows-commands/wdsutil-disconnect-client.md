---
title: WDSUTIL desconectar-cliente
description: Artigo de referência para o comando de desconexão-cliente WDSUTIL, que desconecta um cliente de uma transmissão ou namespace multicast.
ms.topic: reference
ms.assetid: 876bbe6c-76ab-4de5-879b-d2066e700326
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: dd837fd9a677f78b5890cd1f2092529d44a2bc68
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070328"
---
# <a name="wdsutil-disconnect-client"></a>WDSUTIL desconectar-cliente

Desconecta um cliente de uma transmissão multicast ou de um namespace. A menos que você especifique **/Force** , o cliente voltará para outro método de transferência (se ele tiver suporte do cliente).

## <a name="syntax"></a>Sintaxe

```
wdsutil /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/Force]
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|--|--|
| ClientID`<ClientID>` | Especifica a ID do cliente a ser desconectado. Para exibir a ID de um cliente, execute o `wdsutil /get-multicasttransmission /show:clients` comando. |
| [/Server:`<Servername>`] | Especifica o nome do servidor. Esse pode ser o nome NetBIOS ou o FQDN (nome de domínio totalmente qualificado). Se nenhum nome de servidor for especificado, o servidor local será usado. |
| /Force | Interrompe completamente a instalação e não usa um método de fallback. Como Wdsmcast.exe não dá suporte a nenhum mecanismo de fallback, o comportamento padrão é o seguinte:<ul><li>**Se você estiver usando o cliente dos serviços de implantação do Windows:** O cliente continua a instalação usando unicasting.</li><li>**Se você não estiver usando o cliente dos serviços de implantação do Windows:** A instalação falha.</li></ul>**Importante:** É altamente recomendável usar esse parâmetro com cuidado porque, se a instalação falhar, o computador poderá ser deixado em um estado inutilizável. |

## <a name="examples"></a>Exemplos

Para desconectar um cliente, digite:

```
wdsutil /Disconnect-Client /ClientId:1
```

Para desconectar um cliente e forçar a falha da instalação, digite:

```
wdsutil /Disconnect-Client /Server:MyWDSServer /ClientId:1 /Force
```

## <a name="additional-references"></a>Referências adicionais

- [Chave da sintaxe de linha de comando](command-line-syntax-key.md)

- [comando WDSUTIL Get-MulticastTransmission](wdsutil-get-multicasttransmission.md)

- [Cmdlets dos serviços de implantação do Windows](/powershell/module/wds)
