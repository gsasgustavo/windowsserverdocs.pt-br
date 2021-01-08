---
title: ETAPA 7 testar a conectividade ao retornar ao corpnet
description: Saiba como testar a conectividade ao retornar para o corpnet em CLIENT1.
manager: brianlic
ms.topic: article
ms.assetid: 5a7252d0-6db8-4a9d-98ee-75082ecd2929
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: c4b9392c6234d1b99f65dd0a133dc2e6be4be893
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040536"
---
# <a name="step-7-test-connectivity-when-returning-to-the-corpnet"></a>ETAPA 7 testar a conectividade ao retornar ao corpnet

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Muitos de seus usuários se moverão entre locais remotos e o corpnet, portanto, é importante que, quando eles retornam ao corpnet, eles possam acessar recursos sem precisar fazer nenhuma alteração de configuração. O acesso remoto torna isso possível porque quando o cliente DirectAccess retorna para o corpnet, ele é capaz de estabelecer uma conexão com o servidor de local de rede. Depois que a conexão HTTPS for estabelecida com êxito ao servidor de local de rede, o cliente DirectAccess desabilitará a configuração do cliente DirectAccess e usará uma conexão direta com o corpnet.

### <a name="test-connectivity-on-client1"></a>Testar a conectividade em CLIENT1

1. Desligue o CLIENT1 e desconecte o CLIENT1 da sub-rede HomeNet ou do comutador virtual e conecte-o à sub-rede corpnet ou ao comutador virtual. Ative o CLIENT1 e faça logon como CORP\User1.

2. Abra uma janela do Windows PowerShell com privilégios elevados, digite **ipconfig/all** e pressione Enter. A saída indicará que CLIENT1 tem um endereço IP local e que não há nenhum túnel 6to4, Teredo ou IP-HTTPS ativo.

3. Teste a conectividade com o compartilhamento de rede em APP2. Na tela **Iniciar** , digite <strong> \\ \APP2\Files</strong>e pressione Enter. Você poderá abrir o arquivo nessa pasta.



