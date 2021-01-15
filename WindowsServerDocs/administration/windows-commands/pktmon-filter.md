---
title: filtro de pktmon
description: Artigo de referência para o comando de filtro pktmon.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: 80f3978105b0c73602c8ab04d78c48d80c88c444
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241049"
---
# <a name="pktmon-filter"></a>filtro de pktmon

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

O filtro Pktmon permite listar, adicionar ou remover filtros de pacote.

## <a name="syntax"></a>Sintaxe

```
pktmon filter { list | add | remove } [OPTIONS | help]
```

### <a name="parameters"></a>Parâmetros

| **Parâmetro** | **Descrição** |
| ------------- | --------------- |
| **lista de filtros pktmon** | Exibir filtros de pacotes ativos. |
| **Adicionar filtro pktmon** |  Adicione um filtro para controlar quais pacotes são relatados. |
| **Remover filtro de pktmon** | Remova todos os filtros de pacote. |

## <a name="additional-references"></a>Referências adicionais

- [Pktmon](pktmon.md)
- [Comp de Pktmon](pktmon-comp.md)
- [Contadores de Pktmon](pktmon-counters.md)
- [Adicionar filtro Pktmon](pktmon-filter-add.md)
- [Formato Pktmon](pktmon-format.md)
- [Lista de Pktmon](pktmon-list.md)
- [Pktmon pcapng](pktmon-pcapng.md)
- [Redefinição de Pktmon](pktmon-reset.md)
- [Pktmon iniciar](pktmon-start.md)
- [Descarregamento de Pktmon](pktmon-unload.md)
- [Visão geral do monitor de pacotes](/windows-server/networking/technologies/pktmon/pktmon)
