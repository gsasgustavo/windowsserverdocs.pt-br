---
title: Evite armazenar arquivos de paginação inteligente em um disco do sistema
description: Saiba o que fazer quando a configuração de memória para uma ou mais máquinas virtuais puder exigir o uso de paginação inteligente se a máquina virtual for reinicializada e o local especificado para o arquivo de paginação inteligente é o disco do sistema do servidor que executa o Hyper-V.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 9b57c9b8-76c5-43c7-bfa6-2c95b3cb6510
ms.date: 8/16/2016
ms.openlocfilehash: 990067509f0fbfe9ba19781da23ea3ea0b6e4091
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834591"
---
# <a name="avoid-storing-smart-paging-files-on-a-system-disk"></a>Evite armazenar arquivos de paginação inteligente em um disco do sistema

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Operações|

Nas seções a seguir, os itálicos indicam o texto que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema
*A configuração de memória para uma ou mais máquinas virtuais pode exigir o uso de paginação inteligente se a máquina virtual for reinicializada e o local especificado para o arquivo de paginação inteligente é o disco do sistema do servidor que executa o Hyper-V.*

## <a name="impact"></a>Impacto
*O uso do disco do sistema para paginação inteligente pode fazer com que o servidor que executa o Hyper-V tenha problemas. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Reconfigure as máquinas virtuais para armazenar os arquivos de paginação inteligente em um disco que não seja do sistema.*



