---
title: O número de máquinas virtuais em execução configuradas para SR-IOV não deve exceder o número de funções virtuais disponíveis para as máquinas virtuais
description: Saiba o que fazer quando não houver funções virtuais suficientes disponíveis para o número de máquinas virtuais em execução configuradas para SR-IOV (virtualização de e/s de raiz única).
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
ms.date: 8/16/2016
ms.openlocfilehash: 783b5dbf170756e922b448d73881543b5a811ce9
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845890"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>O número de máquinas virtuais em execução configuradas para SR-IOV não deve exceder o número de funções virtuais disponíveis para as máquinas virtuais

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
*Não há funções virtuais suficientes disponíveis para o número de máquinas virtuais em execução configuradas para SR-IOV (virtualização de e/s de raiz única).*

## <a name="impact"></a>Impacto
*O desempenho de rede pode não ser o ideal nas seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Considere desabilitar a SR-IOV em uma ou mais máquinas virtuais que não exigem uma função virtual de SR-IOV.*



