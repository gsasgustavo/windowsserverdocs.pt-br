---
title: Definir as configurações de TCP/IP de failover que você deseja que a máquina virtual de réplica use no caso de um failover
description: Saiba o que fazer quando as máquinas virtuais de réplica configuradas com um endereço IP estático devem ser configuradas para usar um endereço IP diferente do seu equivalente de máquina virtual primária no caso de failover.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.date: 8/16/2016
ms.openlocfilehash: 2a52cdd937589476abe254ea923b376d0d3472ed
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846435"
---
# <a name="configure-the-failover-tcpip-settings-that-you-want-the-replica-virtual-machine-to-use-in-the-event-of-a-failover"></a>Definir as configurações de TCP/IP de failover que você deseja que a máquina virtual de réplica use no caso de um failover

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*As máquinas virtuais de réplica configuradas com um endereço IP estático devem ser configuradas para usar um endereço IP diferente de seu equivalente de máquina virtual primária no caso de failover.*

## <a name="impact"></a>Impacto
*Os clientes que usam a carga de trabalho com suporte da máquina virtual primária podem não conseguir se conectar à máquina virtual de réplica após um failover. Além disso, o endereço IP original da máquina virtual primária não será válido na topologia de rede da máquina virtual de réplica. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Use o Gerenciador do Hyper-V para configurar o endereço IP que a máquina virtual de réplica deve usar no caso de failover.*



