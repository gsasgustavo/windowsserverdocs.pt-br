---
title: pktmon iniciar
description: Artigo de referência para o comando pktmon Start.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: 92e8048958dbba1e4d8b71addbc010f5ba8bc31c
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241031"
---
# <a name="pktmon-start"></a>pktmon iniciar

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

Inicia o monitoramento de pacotes.

## <a name="syntax"></a>Sintaxe

```
pktmon start [-c { all | nics | [ids...] }] [-d] [--etw [-p size] [-k keywords]]
             [-f] [-s] [--log-mode {circular | multi-file | real-time | memory}]
```

### <a name="parameters"></a>Parâmetros

| **Parâmetro** | **Descrição** |
| ------------- | --------------- |
| **-c,--componentes** | Selecione os componentes a serem monitorados. Pode ser todos os componentes, somente NICs ou uma lista de IDs de componentes. O padrão é todos. |
| **-d,--somente descartar** | Relate pacotes ignorados. Por padrão, a propagação de pacotes bem-sucedida também é relatada. |
| **--ETW** | Inicie uma sessão de registro em log para captura de pacote. |
| **-p,--tamanho do pacote** | Número de bytes para registrar em cada pacote. Para sempre registrar o pacote inteiro, defina-o como 0. O padrão é 128 bytes. |
| **-k,--palavras-chave** | Bitmask hexadecimal (ou seja, soma dos sinalizadores abaixo) que controla quais eventos são registrados. O padrão é 0x012. Consulte os sinalizadores de palavra-chave, abaixo. |
| **-f,--nome-do-arquivo** | arquivo de log. etl. O padrão é PktMon. etl |
| **-s,--tamanho do arquivo** | Tamanho máximo do arquivo de log em megabytes. O padrão é 512 MB. |
| **-l,--modo de log** | Selecione o modo de log. O padrão é circular. Consulte os modos de log, abaixo. |

### <a name="keyword-flags"></a>Sinalizadores de palavra-chave

Os sinalizadores a seguir se aplicam ao parâmetro **-k** ou **--Keywords** (veja acima).

| **Sinalizador** | **Descrição** |
| --------- | ----------- |
| **0x001** | Erros de monitor de pacotes internos.
| **0x002** | Informações sobre componentes, contadores e filtros. Essas informações são adicionadas ao final do arquivo de log.
| **0x004** | Informações de origem e destino para o primeiro pacote no grupo de NET_BUFFER_LIST.
| **0x008** | Selecione metadados de pacote da enumeração NDIS_NET_BUFFER_LIST_INFO.
| **0x010** | Pacote bruto, truncado para o tamanho especificado no parâmetro [--Packet-size].

### <a name="logging-modes"></a>Modos de log

O modo de log é definido usando o parâmetro **-l** ou **--log-Mode** (veja acima).

| **Modo** | **Descrição** |
| -------- | --------------- |
| **redondo** | Novos eventos substituem os mais antigos quando o tamanho máximo do arquivo é atingido. |
| **vários arquivos** | Um novo arquivo de log é criado quando o tamanho máximo do arquivo é atingido. Os arquivos de log são numerados sequencialmente: PktMon1. ETL, PktMon2. ETL, etc. |
| **tempo real** | Exibir eventos e pacotes na tela em tempo real. Nenhum arquivo de log é criado. Pressione **Ctrl + C** para interromper o monitoramento. |
| **memória** | Os eventos são gravados em um buffer de memória circular. O tamanho do buffer é especificado no parâmetro [--file-size]. O conteúdo do buffer é gravado em um arquivo de log durante a operação de parada. |

## <a name="examples"></a>Exemplos

O comando a seguir inicia a captura e habilita o log de pacotes:

```PowerShell
C:\Test> pktmon start --etw
```

O comando a seguir inicia a captura, habilita o registro em log de pacotes e seleciona o modo de log em tempo real:

```PowerShell
C:\Test> pktmon start --etw -l real-time
```

O comando a seguir capturará contadores de pacotes de todos os adaptadores de rede sem pacotes de log:

```PowerShell
C:\Test> pktmon start -c nics
```

O comando a seguir capturará somente os pacotes ignorados que passam pelos componentes 4 e 5 e os registrará:

```PowerShell
C:\Test> pktmon start --etw -c 4,5 -d
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
- [Descarregamento de Pktmon](pktmon-unload.md)
- [Visão geral do monitor de pacotes](/windows-server/networking/technologies/pktmon/pktmon)
