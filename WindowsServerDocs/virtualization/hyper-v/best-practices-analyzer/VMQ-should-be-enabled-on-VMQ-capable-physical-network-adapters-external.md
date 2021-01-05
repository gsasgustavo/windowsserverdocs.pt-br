---
title: A VMQ deve ser habilitada em adaptadores de rede física compatíveis com VMQ vinculados a um comutador virtual externo
description: Saiba o que fazer quando os adaptadores de rede a seguir são capazes de realizar a fila de máquina virtual (VMQ), mas o recurso está desabilitado.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 93d1b155-bf44-46b0-bb69-d34d5b30e574
ms.date: 8/16/2016
ms.openlocfilehash: 1ab79c106fd17d459a1b6b6adcedba620ae5a89c
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846210"
---
# <a name="vmq-should-be-enabled-on-vmq-capable-physical-network-adapters-bound-to-an-external-virtual-switch"></a>A VMQ deve ser habilitada em adaptadores de rede física compatíveis com VMQ vinculados a um comutador virtual externo

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
*Os adaptadores de rede a seguir são capazes de uma VMQ (fila de máquina virtual), mas o recurso está desabilitado.*

## <a name="impact"></a>**Impacto**
*O Windows não pode aproveitar ao máximo os descarregamentos de hardware disponíveis nos seguintes adaptadores de rede:*

\<list of network adapters>

## <a name="resolution"></a>**Resolução**
*Habilite a VMQ usando o cmdlet Enable-NetAdapterVmq Windows PowerShell ou usando a interface do usuário de propriedades avançadas para o adaptador de rede.*



