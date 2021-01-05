---
title: A ressincronização da replicação deve ser agendada para o horário de pico
description: Saiba o que fazer quando a ressincronização de replicação para as máquinas virtuais primárias não estiver agendada para horários de pico.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
ms.date: 8/16/2016
ms.openlocfilehash: 3669abf4da79db82d0ba7ca985b886a02a180ea9
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845815"
---
# <a name="resynchronization-of-replication-should-be-scheduled-for-off-peak-hours"></a>A ressincronização da replicação deve ser agendada para o horário de pico

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
*A ressincronização da replicação para as máquinas virtuais primárias não está agendada para horários de pico.*

## <a name="impact"></a>Impacto
*Quanto mais longa uma máquina virtual estiver em um estado que exija ressincronização, mais tempo os arquivos de log de replicação aumentarão e mais alterações não replicadas ocorrerão nas máquinas virtuais primárias. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Use o Gerenciador do Hyper-V para modificar as configurações de replicação da máquina virtual para executar a ressincronização automaticamente fora do horário de pico.*



