---
title: Máquinas virtuais configuradas com um adaptador de Fibre Channel virtual devem ser configuradas para alta disponibilidade para o armazenamento baseado em Fibre Channel
description: Saiba o que fazer quando uma ou mais máquinas virtuais não têm uma conexão altamente disponível com o armazenamento baseado em Fibre Channel porque essas máquinas virtuais são configuradas com um adaptador de Fibre Channel virtual que está conectado a apenas um HBA (adaptador de barramento de host).
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
ms.date: 8/16/2016
ms.openlocfilehash: 407db3e9e9f289deb438f67ad7e79c98cb2b914b
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845829"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>Máquinas virtuais configuradas com um adaptador de Fibre Channel virtual devem ser configuradas para alta disponibilidade para o armazenamento baseado em Fibre Channel

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Informações|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>**Problema**
*Uma ou mais máquinas virtuais não têm uma conexão altamente disponível com o armazenamento baseado em Fibre Channel porque essas máquinas virtuais são configuradas com um adaptador de Fibre Channel virtual que está conectado a apenas um HBA (adaptador de barramento de host).*

## <a name="impact"></a>**Impacto**
*Uma falha do adaptador de barramento de host pode bloquear a conexão de Fibre Channel entre o armazenamento e as máquinas virtuais. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>**Resolução**
*Adicione outra conexão da máquina virtual ao adaptador de barramento de host e configure o MPIO (Multipath I/O) no sistema operacional convidado para estabelecer conexões de Fibre Channel redundantes.*



