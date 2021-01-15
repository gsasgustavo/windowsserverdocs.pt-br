---
title: descarregamento de pktmon
description: Artigo de referência para o comando pktmon Unload.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: cc7313054445bdc72bd98cb60a7f4f6d11095553
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241036"
---
# <a name="pktmon-unload"></a>descarregamento de pktmon

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

Pare o serviço de driver PktMon e descarregue PktMon.sys. Efetivamente equivalente a ' sc.exe Stop PktMon '. A medida (se ativa) será interrompida imediatamente e qualquer Estado será excluído (contadores, filtros, etc.).

## <a name="syntax"></a>Syntax

```
pktmon unload
```

## <a name="additional-references"></a>Referências adicionais

- [Pktmon](pktmon.md)
- [Comp de Pktmon](pktmon-comp.md)
- [Contadores de Pktmon](pktmon-counters.md)
- [Filtro de Pktmon](pktmon-filter.md)
- [Adicionar filtro Pktmon](pktmon-filter-add.md)
- [Formato Pktmon](pktmon-format.md)
- [Lista de Pktmon](pktmon-list.md)
- [Pktmon pcapng](pktmon-pcapng.md)
- [Redefinição de Pktmon](pktmon-reset.md)
- [Pktmon iniciar](pktmon-start.md)
- [Visão geral do monitor de pacotes](/windows-server/networking/technologies/pktmon/pktmon)
