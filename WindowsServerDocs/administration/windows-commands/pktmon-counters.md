---
title: contadores de pktmon
description: Artigo de referência para o comando pktmon Counters.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: df61499d96ec8b9eee6ee2939860e95431478b52
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241051"
---
# <a name="pktmon-counters"></a>contadores de pktmon

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

Os contadores do Pktmon permitem consultar e exibir os contadores por componente atuais para confirmar a presença do tráfego esperado e obter uma exibição de alto nível de como o tráfego flui no computador.

## <a name="syntax"></a>Sintaxe

```
pktmon [comp] counters [-t { all | drop | flow }] [-z] [--json]
```

### <a name="parameters"></a>Parâmetros

| **Parâmetro** | **Descrição** |
| ------------- | --------------- |
| **-t,--tipo de contador** | Selecione os tipos de contadores a serem mostrados. Os valores com suporte são todos os contadores (padrão), somente quedas ou somente fluxos. |
| **-z,--mostrar-zeros** | Mostrar contadores que são zero em ambas as direções. |
| **-i,--mostrar-oculto** | Mostre os componentes que estão ocultos por padrão. |
| **--JSON** | Gere os contadores no formato JSON. |

## <a name="additional-references"></a>Referências adicionais

- [Pktmon](pktmon.md)
- [Comp de Pktmon](pktmon-comp.md)
- [Filtro de Pktmon](pktmon-filter.md)
- [Adicionar filtro Pktmon](pktmon-filter-add.md)
- [Formato Pktmon](pktmon-format.md)
- [Lista de Pktmon](pktmon-list.md)
- [Pktmon pcapng](pktmon-pcapng.md)
- [Redefinição de Pktmon](pktmon-reset.md)
- [Pktmon iniciar](pktmon-start.md)
- [Descarregamento de Pktmon](pktmon-unload.md)
- [Visão geral do monitor de pacotes](/windows-server/networking/technologies/pktmon/pktmon)
