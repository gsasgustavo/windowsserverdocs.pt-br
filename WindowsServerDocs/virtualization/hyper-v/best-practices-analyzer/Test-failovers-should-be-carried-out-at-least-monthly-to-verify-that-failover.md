---
title: Os failovers de teste devem ser executados pelo menos mensalmente para verificar se o failover será bem sucedido e se as cargas de trabalho da máquina virtual funcionarão conforme o esperado após o failover
description: Saiba o que fazer quando não houve nenhum failover de teste em pelo menos um mês.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 57a8aa50-e59e-4a4b-8571-1099d5a8eee4
ms.date: 8/16/2016
ms.openlocfilehash: bf2b1f8bae67c2303fe19a92ac15a2cfdb46511c
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845837"
---
# <a name="test-failovers-should-be-carried-out-at-least-monthly-to-verify-that-failover-will-succeed-and-that-virtual-machine-workloads-will-operate-as-expected-after-failover"></a>Os failovers de teste devem ser executados pelo menos mensalmente para verificar se o failover será bem sucedido e se as cargas de trabalho da máquina virtual funcionarão conforme o esperado após o failover

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Operações|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*Não houve nenhum failover de teste em pelo menos um mês.*

## <a name="impact"></a>Impacto
*Não há nenhuma confirmação de que um failover planejado ou não planejado terá sucesso ou as operações de carga de trabalho continuarão corretamente após um failover. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Use o Gerenciador do Hyper-V para conduzir um failover de teste.*



