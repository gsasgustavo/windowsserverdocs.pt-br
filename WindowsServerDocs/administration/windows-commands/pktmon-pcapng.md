---
title: pktmon pcapng
description: Artigo de referência para o comando pktmon pcapng.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: 7b906efd5548b6aa22168294668a1bde6da3c3c8
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241026"
---
# <a name="pktmon-pcapng"></a>pktmon pcapng

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

Pktmon pcapng converte os arquivos de log no formato pcapng. Os pacotes ignorados não são incluídos por padrão.

## <a name="syntax"></a>Sintaxe

```
pktmon pcapng log.etl [-o log.pcapng]
```

### <a name="parameters"></a>Parâmetros

| **Parâmetro** | **Descrição** |
| ------------- | --------------- |
| **-o,--out** | Nome do arquivo pcapng formatado. |
| **-d,--somente descartar** | Converta somente pacotes ignorados. |
| **-c,--ID do componente** | Filtre os pacotes por uma ID de componente específica. |

## <a name="example"></a>Exemplo

O exemplo a seguir converte apenas os pacotes descartados das placas de interface de rede no arquivo de log *PktMon. etl* para o formato pcapng:

```powershell
C:\Test> pktmon pcapng C:\tmp\PktMon.etl -d -c nics
```

## <a name="additional-references"></a>Referências adicionais

- [Pktmon](pktmon.md)
- [Comp de Pktmon](pktmon-comp.md)
- [Contadores de Pktmon](pktmon-counters.md)
- [Filtro de Pktmon](pktmon-filter.md)
- [Adicionar filtro Pktmon](pktmon-filter-add.md)
- [Formato Pktmon](pktmon-format.md)
- [Lista de Pktmon](pktmon-list.md)
- [Descarregamento de Pktmon](pktmon-unload.md)
- [Redefinição de Pktmon](pktmon-reset.md)
- [Pktmon iniciar](pktmon-start.md)
- [Visão geral do monitor de pacotes](/windows-server/networking/technologies/pktmon/pktmon)
