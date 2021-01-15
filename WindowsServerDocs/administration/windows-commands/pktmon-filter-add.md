---
title: Adicionar filtro pktmon
description: Artigo de referência para o comando pktmon filtro Add.
ms.topic: reference
author: khdownie
ms.author: v-kedow
ms.date: 1/14/2021
ms.openlocfilehash: e1e69bbad5433eedd582b1d6218e462b4c70f71d
ms.sourcegitcommit: 5dd48d0da9400d7e8a6ae40b4c977d1703c4e669
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241030"
---
# <a name="pktmon-filter-add"></a>Adicionar filtro pktmon

> Aplica-se a: Windows Server (canal semestral), Windows Server 2019, Windows 10, Azure Stack HCI, Hub de Azure Stack, Azure

Pktmon filtro Add permite que você adicione um filtro para controlar quais pacotes são relatados. Para que um pacote seja relatado, ele deve corresponder a todas as condições especificadas em pelo menos um filtro. Até oito filtros podem estar ativos ao mesmo tempo.

## <a name="syntax"></a>Syntax

```
pktmon filter add <name> [-m mac [mac2]] [-v vlan] [-d { IPv4 | IPv6 | number }]
                         [-t { TCP [flags...] | UDP | ICMP | ICMPv6 | number }]
                         [-i ip [ip2]] [-p port [port2]] [-e [port]]
```

Você pode fornecer um nome opcional ou uma descrição do filtro.

  > [!NOTE]
  > Quando dois MACs (-m), IPs (-i) ou portas (-p) são especificados, o filtro corresponde aos pacotes que contêm ambos. Ele não fará distinção entre a origem ou o destino para essa finalidade.

### <a name="parameters"></a>Parâmetros

| **Parâmetro** | **Descrição** |
| ------------- | --------------- |
| **-m,--Mac [-address]** | Corresponder endereço MAC de origem ou de destino. Consulte a observação acima. |
| **-v,--VLAN** | Corresponder por ID de VLAN (VID) no cabeçalho 802.1 Q. |
| **-d,--data-link [-Protocol],--EtherType** | Corresponder pelo protocolo de vínculo de dados (camada 2). Pode ser IPv4, IPv6, ARP ou um número de protocolo. |
| **-t,--Transport [-Protocol],--IP-Protocol** | Corresponder pelo protocolo de transporte (camada 4). Pode ser TCP, UDP, ICMP, ICMPv6 ou um número de protocolo. Para filtrar ainda mais os pacotes TCP, é possível fornecer uma lista opcional de sinalizadores TCP para correspondência. Os sinalizadores com suporte são FIN, SYN, RST, PSH, ACK, URG, ECE e CWR. |
| **-i,--IP [-address]** | Corresponder endereço IP de origem ou de destino. Consulte a observação acima. Para fazer a correspondência por sub-rede, use a notação CIDR com o comprimento do prefixo. |
| **-p,--porta** | Corresponder ao número da porta de origem ou de destino. Consulte a observação acima. |
| **-e,--encap** | Esse filtro também se aplica a pacotes internos encapsulados, além do pacote externo. Os métodos de encapsulamento com suporte são VXLAN, GRE, NVGRE e IP-in-IP. A porta VXLAN personalizada é opcional e o padrão é 4789. |

## <a name="examples"></a>Exemplos

O conjunto de filtros a seguir capturará qualquer tráfego ICMP de ou para o endereço IP 10.0.0.10, juntamente com qualquer tráfego na porta 53.

```PowerShell
C:\Test> pktmon filter add -i 10.0.0.10 -t icmp
C:\Test> pktmon filter add -p 53
```

O filtro a seguir capturará todos os pacotes SYN enviados ou recebidos pelo endereço IP 10.0.0.10:

```PowerShell
C:\Test> pktmon filter add -i 10.0.0.10 -t tcp syn
```

O filtro a seguir chamou pings de **myping** 10.10.10.10 usando o protocolo ICMP:

```PowerShell
C:\Test> pktmon filter add MyPing -i 10.10.10.10 -t ICMP
```

O filtro a seguir chamado **MySmbSyb** captura o tráfego SMB sincronizado com TCP:

```PowerShell
C:\Test> pktmon filter add MySmbSyn -i 10.10.10.10 -t TCP SYN -p 445
```

O filtro a seguir, chamado **mysubnet** , captura o tráfego na máscara de sub-rede 255.255.255.0 ou/24 na notação CIDR:

```PowerShell
C:\Test> pktmon filter add MySubnet -i 10.10.10.0/24
```

## <a name="other-references"></a>Outras referências

- [Pktmon](pktmon.md)
- [Comp de Pktmon](pktmon-comp.md)
- [Contadores de Pktmon](pktmon-counters.md)
- [Filtro de Pktmon](pktmon-filter.md)
- [Formato Pktmon](pktmon-format.md)
- [Lista de Pktmon](pktmon-list.md)
- [Pktmon pcapng](pktmon-pcapng.md)
- [Redefinição de Pktmon](pktmon-reset.md)
- [Pktmon iniciar](pktmon-start.md)
- [Descarregamento de Pktmon](pktmon-unload.md)
- [Visão geral do monitor de pacotes](/windows-server/networking/technologies/pktmon/pktmon)
