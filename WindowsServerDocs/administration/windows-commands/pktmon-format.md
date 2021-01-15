---
title: formato pktmon
description: Artigo de referência para o comando de formato pktmon.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: f40ea62f4a15bc52a18a8e9bbccdc45745aaa93b
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241028"
---
# <a name="pktmon-format"></a>formato pktmon

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

O formato Pktmon converte arquivos de log em formato de texto.

## <a name="syntax"></a>Sintaxe

```
pktmon format log.etl [-o log.txt] [-b] [-v [level]] [-x] [-e] [-l [port]
```

### <a name="parameters"></a>Parâmetros

| **Parâmetro** | **Descrição** |
| ------------- | --------------- |
| **-o,--out** | Nome do arquivo de texto formatado. |
| **-s,--somente estatísticas** | Exibir informações estatísticas do arquivo de log. |
| **-b,--Brief** | Formato de pacote abreviado. |
| **-v, --verbose** | Nível de detalhes [1.. 3]. |
| **-x,--Hex** | Formato hexadecimal. |
| **-e,--não-Ethernet** | Não Imprimir cabeçalho de Ethernet. |
| **-l,--vxlan** | Porta VXLAN personalizada. |

## <a name="additional-references"></a>Referências adicionais

- [Pktmon](pktmon.md)
- [Comp de Pktmon](pktmon-comp.md)
- [Contadores de Pktmon](pktmon-counters.md)
- [Filtro de Pktmon](pktmon-filter.md)
- [Adicionar filtro Pktmon](pktmon-filter-add.md)
- [Lista de Pktmon](pktmon-list.md)
- [Pktmon pcapng](pktmon-pcapng.md)
- [Redefinição de Pktmon](pktmon-reset.md)
- [Pktmon iniciar](pktmon-start.md)
- [Descarregamento de Pktmon](pktmon-unload.md)
- [Visão geral do monitor de pacotes](/windows-server/networking/technologies/pktmon/pktmon)
