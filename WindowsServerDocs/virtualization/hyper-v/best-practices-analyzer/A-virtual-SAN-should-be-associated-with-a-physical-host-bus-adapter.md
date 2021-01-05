---
title: Uma SAN virtual deve ser associada a um adaptador de barramento de host físico
description: Saiba o que fazer quando uma rede de área de armazenamento virtual (SAN) tiver sido configurada sem uma associação a um adaptador de barramento de host (HBA).
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 14bca69b-e779-4e90-b5c1-1b015625572f
ms.date: 8/16/2016
ms.openlocfilehash: 73ce82a03e4831ab5056cb6e75c2bf08cc52b494
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834201"
---
# <a name="a-virtual-san-should-be-associated-with-a-physical-host-bus-adapter"></a>Uma SAN virtual deve ser associada a um adaptador de barramento de host físico

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Configuração|


Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>**Problema**
*Uma SAN (rede de área de armazenamento) virtual foi configurada sem uma associação a um adaptador de barramento de host (HBA).*

## <a name="impact"></a>**Impacto**
*Uma máquina virtual não será iniciada quando estiver configurada com um adaptador de Fibre Channel virtual conectado a uma SAN virtual configurada incorretamente. Isso afeta as seguintes SANs virtuais:*


\<list of virtual SANs>


## <a name="resolution"></a>**Resolução**
*Reconfigure a rede SAN virtual conectando-a a um adaptador de barramento de host.*





