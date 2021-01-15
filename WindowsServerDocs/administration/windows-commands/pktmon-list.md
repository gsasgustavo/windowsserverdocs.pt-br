---
title: lista de pktmon
description: Artigo de referência para o comando de lista de pktmon.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: 6f03eccb554c1a63f4a798b9896709e6ba69be8c
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241048"
---
# <a name="pktmon-list"></a>lista de pktmon

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

Lista todos os componentes ativos, permitindo que você examine o layout da pilha de rede. O comando mostra os componentes de rede (drivers) organizados por associações de adaptadores.

## <a name="syntax"></a>Sintaxe

```
pktmon [comp] list
```

### <a name="parameters"></a>Parâmetros

| **Parâmetro** | **Descrição** |
| ------------- | --------------- |
| **-i,--mostrar-oculto** | Mostre os componentes que estão ocultos por padrão. |
| **--JSON** | Saída da lista no formato JSON. |

## <a name="additional-references"></a>Referências adicionais

- [Pktmon](pktmon.md)
- [Comp de Pktmon](pktmon-comp.md)
- [Contadores de Pktmon](pktmon-counters.md)
- [Filtro de Pktmon](pktmon-filter.md)
- [Adicionar filtro Pktmon](pktmon-filter-add.md)
- [Formato Pktmon](pktmon-format.md)
- [Pktmon pcapng](pktmon-pcapng.md)
- [Redefinição de Pktmon](pktmon-reset.md)
- [Pktmon iniciar](pktmon-start.md)
- [Descarregamento de Pktmon](pktmon-unload.md)
- [Visão geral do monitor de pacotes](/windows-server/networking/technologies/pktmon/pktmon)
