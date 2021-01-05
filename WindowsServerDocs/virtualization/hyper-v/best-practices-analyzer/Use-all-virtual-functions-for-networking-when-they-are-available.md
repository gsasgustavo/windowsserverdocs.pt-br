---
title: Usar todas as funções virtuais para rede quando elas estiverem disponíveis
description: Saiba o que fazer quando alguns recursos de aceleração de hardware não estão sendo utilizados.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: bf895484-6a0d-4aa4-9a42-9fac739e875d
ms.date: 8/16/2016
ms.openlocfilehash: 4252fd790c34bb9f4eca116eff84eb900033658b
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846313"
---
# <a name="use-all-virtual-functions-for-networking-when-they-are-available"></a>Usar todas as funções virtuais para rede quando elas estiverem disponíveis

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
*Alguns recursos de aceleração de hardware não estão sendo utilizados*

## <a name="impact"></a>Impacto
*Essa configuração pode fazer com que a utilização geral da CPU seja maior do que o necessário. O desempenho de rede pode não ser o ideal nas seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Considere configurar o adaptador de rede virtual para SR-IOV se o hardware físico oferecer suporte a SR-IOV e se essa configuração não entrar em conflito com os recursos de rede exigidos pela máquina virtual.*



