---
title: Suporte Pktmon para Wireshark (pcapng)
description: Use este tópico para analisar logs de pcapng gerados pelo monitor de pacotes com o Wireshark.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: c65604f6e3f4e87b806513063800ee62d52d1feb
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632381"
---
# <a name="pktmon-support-for-wireshark-pcapng"></a>Suporte Pktmon para Wireshark (pcapng)

>Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

O monitor de pacotes (Pktmon) pode converter logs em formato pcapng. Esses logs podem ser analisados usando o Wireshark (ou qualquer analisador de pcapng); no entanto, algumas das informações críticas podem estar ausentes nos arquivos pcapng. Este tópico explica a saída esperada e como aproveitá-la.

## <a name="pktmon-pcapng-syntax"></a>Sintaxe Pktmon pcapng

Use os comandos a seguir para converter a captura pktmon para o formato pcapng.

```powershell
C:\Test> pktmon pcapng help
pktmon pcapng log.etl [-o log.pcapng]
    Convert log file to pcapng format.
    Dropped packets are not included by default.

-o, --out
    Name of the formatted pcapng file.

-d, --drop-only
    Convert dropped packets only.

-c, --component-id
    Filter packets by a specific component ID.

Example: pktmon pcapng C:\tmp\PktMon.etl -d -c nics
```

## <a name="output-filtering"></a>Filtragem de saída

Todas as informações sobre os relatórios de descarte de pacotes e o fluxo de pacotes por meio da pilha de rede serão perdidos na saída do pcapng. Portanto, o conteúdo do log deve ser cuidadosamente filtrado previamente para tal conversão. Por exemplo:

- O formato Pcapng não faz distinção entre um pacote de fluxo e um pacote Descartado. Para separar todos os pacotes na captura de pacotes descartados, gere dois arquivos pcapng; um que contém todos os pacotes (" **pktmon pcapng log. etl-out log-Capture. etl** ") e outro que contém apenas pacotes descartados (" **pktmon pcapng log. etl--drop-out-out log-drop. etl** "). Dessa forma, você poderá analisar os pacotes descartados em um log separado.
- O formato Pcapng não faz distinção entre diferentes componentes de rede em que um pacote foi capturado. Para cenários com várias camadas, especifique a ID de componente desejada na saída pcapng " **pktmon pcapng log. etl--Component-ID 5** ". Repita esse comando para cada conjunto de IDs de componentes nos quais você está interessado.
