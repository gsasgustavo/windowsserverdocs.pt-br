---
title: Verifique se o driver de função virtual opera corretamente quando uma máquina virtual está configurada para usar SR-IOV
description: Saiba o que fazer quando o driver de função virtual não está operando corretamente no sistema operacional convidado de uma ou mais máquinas virtuais.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
ms.date: 8/16/2016
ms.openlocfilehash: a009060dc67ba29c12e986167b2ed746865311d5
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845913"
---
# <a name="ensure-that-the-virtual-function-driver-operates-correctly-when-a-virtual-machine-is-configured-to-use-sr-iov"></a>Verifique se o driver de função virtual opera corretamente quando uma máquina virtual está configurada para usar SR-IOV

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
*O driver de função virtual não está operando corretamente no sistema operacional convidado de uma ou mais máquinas virtuais.*

## <a name="impact"></a>Impacto
*O desempenho de rede não é o ideal nas seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*No sistema operacional convidado, faça o seguinte: Verifique se os drivers apropriados estão instalados e se todos os dispositivos de rede estão habilitados e verifique se há erros ou avisos no log de eventos.*



