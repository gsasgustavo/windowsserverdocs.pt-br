---
title: Solucionar problemas no cliente DHCP
description: Este Artilce apresenta como solucionar problemas no cliente DHCP e coletar dados.
manager: dcscontentpm
ms.date: 5/26/2020
ms.topic: troubleshooting
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 62ac48a59dcbcc31316dc0a5fc4dbc99509ec140
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947192"
---
# <a name="troubleshoot-problems-on-the-dhcp-client"></a>Solucionar problemas no cliente DHCP

Este artigo discute como solucionar problemas que ocorrem em clientes DHCP.

## <a name="troubleshooting-checklist"></a>Lista de verificação de solução de problemas

Verifique os seguintes dispositivos e configurações:

  - Os cabos estão conectados e funcionando.

  - A filtragem de MAC está habilitada nos comutadores aos quais o cliente está conectado.

  - O adaptador de rede está habilitado.

  - O driver de adaptador de rede correto está instalado e atualizado.

  - O serviço cliente DHCP é iniciado e está em execução. Para verificar isso, execute o comando **net start** e procure o **cliente DHCP**.

  - Não há nenhuma porta de bloqueio de firewall 67 e 68 UDP no computador cliente.

## <a name="event-logs"></a>Logs de eventos

Examine os logs de eventos de administrador/eventos do cliente Microsoft-Windows-DHCP e Microsoft-Windows-DHCP. Todos os eventos relacionados ao serviço de cliente DHCP são enviados a esses logs de eventos.
Os eventos do cliente Microsoft-Windows-DHCP estão localizados na Visualizador de Eventos em **logs de aplicativos e serviços**.

O comando do PowerShell "Get-netadapter-IncludeHidden" fornece as informações necessárias para interpretar os eventos listados nos logs. Por exemplo, ID de interface, endereço MAC e assim por diante.

## <a name="data-collection"></a>Coleta de dados

Recomendamos que você colete dados simultaneamente no cliente DHCP e no lado do servidor quando o problema ocorrer. No entanto, dependendo do problema real, você também pode iniciar sua investigação usando um único conjunto de dados no cliente DHCP ou no servidor DHCP.

Para coletar dados do servidor e do cliente afetado, use o [Wireshark](https://www.wireshark.org/download.html). Comece a coletar ao mesmo tempo no cliente DHCP e nos computadores do servidor DHCP.

Execute os seguintes comandos no cliente que está enfrentando o problema:

```console
ipconfig /release
ipconfig /renew
```

Em seguida, interrompa o Wireshark no cliente e no servidor. Verifique os rastreamentos gerados. Eles devem, pelo menos, dizer em qual estágio a comunicação será interrompida.