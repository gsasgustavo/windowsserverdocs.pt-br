---
title: Questões conhecidas do DirectAccess
description: Este tópico fornece um link para documentos de suporte técnico da Microsoft para o DirectAccess no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 3511a91f-1d5d-45a0-97f2-3fc0d6f079b4
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 117e598542ff0140c1cacc533e26d85174f0fcc6
ms.sourcegitcommit: eb995fa887ffe1408b9f67caf743c66107173666
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/21/2021
ms.locfileid: "98666565"
---
# <a name="directaccess-known-issues"></a>Questões conhecidas do DirectAccess

>Aplica-se a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2019

## <a name="dns-registration-of-directaccess-client-ipv6-addresses"></a>Registro DNS de endereços IPv6 do cliente DirectAccess

A partir do Windows 10 pode ser 2020 atualização, um cliente não registra mais seus endereços IP em servidores DNS configurados em um Tabela de Políticas de Resolução de Nomes (NRPT).
Se o registro de DNS for necessário, por exemplo, **gerencie**-o, ele poderá ser explicitamente habilitado com essa chave do registro no cliente:

Caminho: `HKLM\System\CurrentControlSet\Services\Dnscache\Parameters`<br/>
Digite: `DWORD`<br/>
Nome do valor: `DisableNRPTForAdapterRegistration`<br/>
Valores:<br/>
`1` -Registro de DNS desabilitado (padrão, pois a atualização do Windows 10 pode ser 2020)<br/>
`0` -Registro de DNS habilitado

## <a name="recommended-hotfixes-and-updates-for-windows-server-2012-directaccess"></a>Hotfixes e atualizações recomendados para o Windows Server 2012 DirectAccess
O link a seguir lista os documentos de suporte técnico da Microsoft para o DirectAccess que você deve examinar e aplicar antes de iniciar a implantação para evitar uma configuração inutilizável.

-   [Hotfixes e atualizações recomendados para o Windows Server 2012 DirectAccess](https://support.microsoft.com/kb/2883952)


