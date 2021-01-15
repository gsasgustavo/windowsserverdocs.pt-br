---
title: pktmon
description: Artigo de referência para a ferramenta de diagnóstico de rede pktmon para Windows que pode ser usada para captura de pacote, detecção de pacotes de eliminação, filtragem de pacotes e contagem.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: 55b8ad90ca49349482e5e4b9ccb2ad11132a044d
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241027"
---
# <a name="pktmon"></a>pktmon

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

O monitor de pacotes (Pktmon) é uma ferramenta de diagnóstico de rede entre componentes para Windows. Ele pode ser usado para captura de pacote, detecção de eliminação, filtragem e contagem. O Pktmon é especialmente útil em cenários de virtualização, como rede de contêineres e SDN, pois fornece visibilidade dentro da pilha de rede.

## <a name="syntax"></a>Syntax

```
pktmon { filter | comp | reset | counters | format | list | start | stop | pcapng | unload | help } [options]
```

### <a name="commands"></a>Comandos

| **Comando** | **Descrição** |
| --------- | ----------- |
| [filtro de pktmon](pktmon-filter.md) | Gerenciar filtros de pacote. |
| [comp de pktmon](pktmon-comp.md) | Gerenciar componentes registrados. |
| [redefinição de pktmon](pktmon-reset.md) | Redefina os contadores como zero. |
| [contadores de pktmon](pktmon-counters.md) | Contadores de pacotes de consulta. |
| [formato pktmon](pktmon-format.md) | Converter arquivo de log em texto. |
| [lista de pktmon](pktmon-list.md) | Listar todos os componentes ativos. |
| [pktmon iniciar](pktmon-start.md) | Inicie o monitoramento de pacotes. |
| pktmon parar | Parar monitoramento de pacotes. |
| [pktmon pcapng](pktmon-pcapng.md) | Converta o arquivo de log no formato pcapng. |
| [descarregamento de pktmon](pktmon-unload.md) | Descarregar o driver pktmon. |
| ajuda do pktmon | Exibe um breve resumo dos subcomandos. |

## <a name="additional-references"></a>Referências adicionais

- [Visão geral do monitor de pacotes](/windows-server/networking/technologies/pktmon/pktmon)
- [Suporte Pktmon para Monitor de Rede da Microsoft (Netmon)](/windows-server/networking/technologies/pktmon/pktmon-netmon-support)
