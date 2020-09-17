---
title: Pelo menos uma rede para o tráfego de migração ao vivo deve ter uma velocidade de link de pelo menos 1 Gbps
description: Versão online do texto para esta regra de Analisador de Práticas Recomendadas.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 5714df3f-f810-4618-8c93-e24881651100
ms.date: 8/16/2016
ms.openlocfilehash: cf1f09a635d6f6a46ee2a0bab2de53c898af9084
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746291"
---
# <a name="at-least-one-network-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>Pelo menos uma rede para o tráfego de migração ao vivo deve ter uma velocidade de link de pelo menos 1 Gbps

>Aplica-se a: Windows Server 2016



|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Erro|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*Nenhuma das redes para o tráfego de migração ao vivo tem uma velocidade de link de pelo menos 1 Gbps.*

## <a name="impact"></a>Impacto
*As migrações ao vivo podem ocorrer lentamente, o que pode interromper a conexão de rede devido a um tempo limite de conexão TCP.*

## <a name="resolution"></a>Resolução
*Configure pelo menos uma rede de migração dinâmica com velocidade de 1 Gbps ou mais rápida.*

Consulte a documentação do fornecedor de hardware de rede para saber se algum adaptador de rede existente pode dar suporte a uma velocidade de link de pelo menos 1 Gbps.



