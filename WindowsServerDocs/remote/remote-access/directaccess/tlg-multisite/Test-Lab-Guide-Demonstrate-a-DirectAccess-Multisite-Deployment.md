---
title: Guia de laboratório de teste – demonstrar uma implantação multissite do DirectAccess
description: Saiba mais sobre como estender o guia de laboratório de teste – demonstre a configuração do servidor único do DirectAccess com IPv4 e IPv6 mistos para demonstrar o acesso remoto em um cenário multissite.
manager: brianlic
ms.topic: article
ms.assetid: 3c98106c-67cc-406a-810e-f2e09f7e2c5e
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 01357e5271932f3b8ad3140f34b3247c426f40e9
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040196"
---
# <a name="test-lab-guide-demonstrate-a-directaccess-multisite-deployment"></a>Guia de Teste de Laboratório: demonstrar implantação multissite do DirectAccess

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

O acesso remoto é uma função de servidor nos sistemas operacionais Windows Server 2016, Windows Server 2012 R2 e Windows Server 2012 que permite que os usuários remotos acessem com segurança recursos de rede internos usando o DirectAccess ou VPN RRAS. Este guia contém instruções passo a passo para estender o guia de [laboratório de teste: demonstre a configuração do servidor único do DirectAccess com IPv4 e IPv6 mistos](https://go.microsoft.com/fwlink/p/?LinkId=237004) para demonstrar o acesso remoto em um cenário multissite.

A implantação de acesso remoto em um cenário multissite permite configurar servidores de acesso remoto em locais geograficamente diversificados. Anteriormente, os usuários remotos eram obrigados a sempre se conectar à rede corporativa por meio de um servidor DirectAccess específico. Com o Windows Server 2016, o Windows Server 2012 R2 ou o Windows Server 2012 e o Windows 10 ou o Windows 8, você pode configurar pontos de entrada para cada local geográfico em sua implantação. Cada ponto de entrada pode ser um único servidor de acesso remoto ou um cluster de servidores de acesso remoto. Os usuários remotos têm a opção de se conectar a qualquer um dos pontos de entrada de acesso remoto da organização. Por exemplo, se um usuário remoto geralmente se conecta ao ponto de entrada de acesso remoto localizado na Ásia, mas, em seguida, entra em uma viagem de negócios à Europa, o computador cliente se conecta automaticamente ao ponto de entrada de acesso remoto mais próximo.

## <a name="about-this-guide"></a>Sobre este guia
Este guia contém instruções para configurar e demonstrar o acesso remoto usando nove servidores e três computadores cliente. O laboratório de teste multissite de acesso remoto concluído simula uma intranet, a Internet e uma rede doméstica e demonstra a funcionalidade de acesso remoto em diferentes cenários de conexão com a Internet.

> [!IMPORTANT]
> Este laboratório é uma verificação de conceito usando o número mínimo de computadores. A configuração detalhada neste guia é apenas para fins de teste de laboratório, e não deve ser usada em um ambiente de produção.



