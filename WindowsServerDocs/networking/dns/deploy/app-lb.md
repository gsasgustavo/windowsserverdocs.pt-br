---
title: Usar a Política de DNS para balanceamento de carga de aplicativo
description: Saiba como configurar a política DNS para executar o balanceamento de carga do aplicativo.
manager: brianlic
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 849baf9e95af51d5bd3c3bd4460f181fa8836691
ms.sourcegitcommit: 029b1e19ce11160d5f988046e04a83e8ab5a60dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97904911"
---
# <a name="use-dns-policy-for-application-load-balancing"></a>Usar a Política de DNS para balanceamento de carga de aplicativo

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para aprender a configurar a política DNS para executar o balanceamento de carga do aplicativo.

As versões anteriores do DNS do Windows Server forneceram apenas o balanceamento de carga usando round robin respostas; Mas com o DNS no Windows Server 2016, você pode configurar a política DNS para balanceamento de carga do aplicativo.

Quando você implantou várias instâncias de um aplicativo, pode usar a política DNS para balancear a carga de tráfego entre as diferentes instâncias do aplicativo, alocando, assim, dinamicamente a carga de tráfego para o aplicativo.

## <a name="example-of-application-load-balancing"></a>Exemplo de balanceamento de carga de aplicativo

Veja a seguir um exemplo de como você pode usar a política DNS para o balanceamento de carga do aplicativo.

Este exemplo usa uma empresa fictícia-serviços de presente da Contoso, que fornece serviços de oferta online e que tem um site chamado **contosogiftservices.com**.

O site contosogiftservices.com é hospedado em vários data centers que têm endereços IP diferentes.

Em América do Norte, que é o mercado principal para os serviços de presentes da Contoso, o site é hospedado em três datacenters: Chicago, IL, Dallas, TX e Seattle, WA.

O servidor Web de Seattle tem a melhor configuração de hardware e pode lidar com duas vezes mais carga que os outros dois sites. Os serviços de presentes da Contoso querem o tráfego de aplicativo direcionado da seguinte maneira.

- Como o servidor Web de Seattle inclui mais recursos, metade dos clientes do aplicativo é direcionado para esse servidor
- Um trimestre dos clientes do aplicativo é direcionado para o Dallas, o datacenter TX
- Um trimestre dos clientes do aplicativo é direcionado para Chicago, IL, Datacenter

A ilustração a seguir descreve esse cenário.

![Balanceamento de carga do aplicativo DNS com a política DNS](../../media/Dns-App-Lb/dns-app-lb.jpg)


### <a name="how-application-load-balancing-works"></a>Como o balanceamento de carga do aplicativo funciona

Depois de configurar o servidor DNS com a política DNS para balanceamento de carga de aplicativo usando este cenário de exemplo, o servidor DNS responde 50% do tempo com o endereço do servidor Web de Seattle, 25% do tempo com o endereço do servidor Web Dallas e 25% do tempo com o endereço do servidor Web Chicago.

Portanto, para cada quatro consultas que o servidor DNS recebe, ele responde com duas respostas para Seattle e outra para Dallas e Chicago.

Um possível problema com o balanceamento de carga com a política DNS é o cache de registros DNS pelo cliente DNS e o resolvedor/LDNS, que pode interferir no balanceamento de carga porque o cliente ou o resolvedor não envia uma consulta ao servidor DNS.

Você pode mitigar o efeito desse comportamento usando um valor TTL de tempo \- de \- vida \( baixo \) para os registros DNS que devem ter balanceamento de carga.

### <a name="how-to-configure-application-load-balancing"></a>Como configurar o balanceamento de carga do aplicativo

As seções a seguir mostram como configurar a política de DNS para o balanceamento de carga do aplicativo.

#### <a name="create-the-zone-scopes"></a>Criar os escopos de zona

Primeiro, você deve criar os escopos do contosogiftservices.com de zona para os data centers onde eles estão hospedados.

Um escopo de zona é uma instância exclusiva da zona. Uma zona DNS pode ter vários escopos de zona, com cada escopo de zona contendo seu próprio conjunto de registros DNS. O mesmo registro pode estar presente em vários escopos, com endereços IP diferentes ou os mesmos endereços IP.

>[!NOTE]
>Por padrão, um escopo de zona existe nas zonas DNS. Esse escopo de zona tem o mesmo nome que a zona e as operações de DNS herdadas funcionam nesse escopo.

Você pode usar os seguintes comandos do Windows PowerShell para criar escopos de zona.

```powershell
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DallasZoneScope"
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "ChicagoZoneScope"
```

Para obter mais informações, consulte [Add-DnsServerZoneScope](/powershell/module/dnsserver/add-dnsserverzonescope)

#### <a name="add-records-to-the-zone-scopes"></a><a name="bkmk_records"></a>Adicionar registros aos escopos de zona

Agora você deve adicionar os registros que representam o host do servidor Web nos escopos de zona.

No **SeattleZoneScope**, você pode adicionar o registro www.contosogiftservices.com com o endereço IP 192.0.0.1, localizado no datacenter de Seattle.

No **ChicagoZoneScope**, você pode adicionar o mesmo registro \( www.contosogiftservices.com \) com o endereço IP 182.0.0.1 no datacenter de Chicago.

Da mesma forma, no **DallasZoneScope**, você pode adicionar um registro \( www.contosogiftservices.com \) com o endereço IP 162.0.0.1 no datacenter de Chicago.

Você pode usar os seguintes comandos do Windows PowerShell para adicionar registros aos escopos de zona.

```powershell
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope"
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "182.0.0.1" -ZoneScope "ChicagoZoneScope"
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "162.0.0.1" -ZoneScope "DallasZoneScope"
```

Para obter mais informações, consulte [Add-DnsServerResourceRecord](/powershell/module/dnsserver/add-dnsserverresourcerecord).

#### <a name="create-the-dns-policies"></a><a name="bkmk_policies"></a>Criar as políticas de DNS

Depois de criar as partições (escopos de zona) e adicionar registros, você deve criar políticas de DNS que distribuem as consultas de entrada entre esses escopos de forma que 50% das consultas para contosogiftservices.com sejam respondidas com o endereço IP do servidor Web no datacenter de Seattle e o restante sejam igualmente distribuídos entre os data centers Chicago e Dallas.

Você pode usar os seguintes comandos do Windows PowerShell para criar uma política de DNS que equilibre o tráfego do aplicativo entre esses três data centers.

>[!NOTE]
>No exemplo de comando abaixo, a expressão – ZoneScope "SeattleZoneScope, 2; ChicagoZoneScope, 1; DallasZoneScope, 1 "configura o servidor DNS com uma matriz que inclui a combinação de parâmetros `<ZoneScope>` , `<weight>` .

```powershell
Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1;DallasZoneScope,1" -ZoneName "contosogiftservices.com"
```

Para obter mais informações, consulte [Add-DnsServerQueryResolutionPolicy](/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy).

Você criou com êxito uma política de DNS que fornece o balanceamento de carga de aplicativos entre servidores Web em três data centers diferentes.

Você pode criar milhares de políticas de DNS de acordo com seus requisitos de gerenciamento de tráfego e todas as novas políticas são aplicadas dinamicamente, sem reiniciar o servidor DNS-em consultas de entrada.
