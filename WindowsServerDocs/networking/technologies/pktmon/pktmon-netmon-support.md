---
title: Suporte Pktmon para Monitor de Rede da Microsoft (Netmon)
description: Use esta página para analisar arquivos ETL gerados pelo monitor de pacotes no Netmon.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 7c6e3a40558ea27a273464d157fa4fbdbacd7134
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632382"
---
# <a name="pktmon-support-for-microsoft-network-monitor-netmon"></a>Suporte Pktmon para Monitor de Rede da Microsoft (Netmon)

>Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

O monitor de pacotes (Pktmon) gera logs no formato ETL. Esses logs podem ser analisados usando o Monitor de Rede da Microsoft (Netmon) usando analisadores especiais. Este tópico explica como analisar arquivos ETL gerados pelo monitor de pacotes no Netmon.

## <a name="network-monitor-setup-and-configuration"></a>Instalação e configuração do Monitor de Rede

Siga estas etapas para instalar e configurar o netmon para analisar os arquivos ETL gerados pelo monitor de pacotes:

   1. [Instale o Monitor de Rede 3,4](/download/4865).
   1. Inicie Monitor de Rede elevado e defina o Windows como perfil do analisador ativo em (ferramentas/opções/perfis do analisador).
   1. Copie etl_Microsoft-Windows-PktMon-Events. NPL [aqui](https://github.com/microsoft/NetMon_Parsers_for_PacketMon/blob/main/etl_Microsoft-Windows-PktMon-Events.npl)   para "%ProgramData%\Microsoft\Network monitor 3 \ NPL\NetworkMonitor Parsers\Windows"
   1. Copie stub_etl_Microsoft-Windows-PktMon-Events. NPL [aqui](https://github.com/microsoft/NetMon_Parsers_for_PacketMon/blob/main/stub_etl_Microsoft-Windows-PktMon-Events.npl) para "%ProgramData%\Microsoft\Network monitor 3 \ NPL\NetworkMonitor Parsers\Windows\Stubs"
   1. Renomeie stub_etl_Microsoft-Windows-PktMon-Events. NPL para etl_Microsoft-Windows-PktMon-Events. NPL
   1. Incluir etl_Microsoft-Windows-PktMon-Events. NPL em NetworkMonitor_Parsers_sparser. NPL em "%PROGRAMDATA%\Microsoft\Network monitor 3 \ NPL\NetworkMonitor parsers"
   1. Reinicie Monitor de Rede elevado para recriar os analisadores.

