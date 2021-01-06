---
title: Eventos de log de DHCP para registros de registro DNS
description: Este tópico fornece informações sobre eventos de log de servidor DHCP no Windows Server 2016.
manager: brianlic
ms.topic: how-to
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 51ca6af9b060b754f75de63089464d8310263734
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948802"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>Eventos de log de DHCP para registros de DNS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Os logs de eventos do servidor DHCP agora fornecem informações detalhadas sobre falhas de registro de DNS.

>[!NOTE]
>Em muitos casos, o motivo para falhas de registro de registro de DNS por servidores DHCP é que uma zona de pesquisa inversa de DNS \- está configurada incorretamente ou não está configurada.

Os novos eventos de DHCP a seguir ajudam você a identificar facilmente quando os registros de DNS estão falhando devido a uma zona de pesquisa inversa de DNS ausente ou configurada incorretamente \- .

|ID|Evento|Valor|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4. ForwardRecordDNSFailure|O registro de registro de encaminhamento para o endereço IPv4% 1 e FQDN %2 falhou com o erro %3. Isso provavelmente ocorre porque a zona de pesquisa direta deste registro não existe no servidor DNS.|
|20318|DHCPv4. ForwardRecordDNSTimeout|O registro de registro de encaminhamento para o endereço IPv4% 1 e FQDN %2 falhou com o erro %3.|
|20319|DHCPv4. PTRRecordDNSFailure|Falha no registro de registro PTR para o endereço IPv4% 1 e FQDN %2 com o erro %3. Isso provavelmente ocorre porque a zona de pesquisa inversa para esse registro não existe no servidor DNS.|
|20320|DHCPv4. PTRRecordDNSTimeout|Falha no registro de registro PTR para o endereço IPv4% 1 e FQDN %2 com o erro %3.|
|20321|DHCPv6. ForwardRecordDNSFailure|O registro de registro de encaminhamento para o endereço IPv6% 1 e FQDN %2 falhou com o erro %3. Isso provavelmente ocorre porque a zona de pesquisa direta deste registro não existe no servidor DNS.|
|20322|DHCPv6. ForwardRecordDNSTimeout|O registro de registro de encaminhamento para o endereço IPv6% 1 e FQDN %2 falhou com o erro %3.|
|20323|DHCPv6. PTRRecordDNSFailure|Falha no registro de registro PTR para o endereço IPv6% 1 e FQDN %2 com o erro %3. Isso provavelmente ocorre porque a zona de pesquisa inversa para esse registro não existe no servidor DNS.|
|20324|DHCPv6. PTRRecordDNSTimeout|Falha no registro de registro PTR para o endereço IPv6% 1 e FQDN %2 com o erro %3.|
|20325|DHCPv4. ForwardRecordDNSError|Falha no registro de registro PTR para o endereço IPv4% 1 e FQDN %2 com o erro %3 \( %4 \) .|
|20326|DHCPv6. ForwardRecordDNSError|O registro de registro de encaminhamento para o endereço IPv6% 1 e FQDN %2 falhou com o erro %3 \( %4\)|
|20327|DHCPv6. PTRRecordDNSError|Falha no registro de registro PTR para o endereço IPv6% 1 e FQDN %2 com o erro %3 \( %4 \) .|

