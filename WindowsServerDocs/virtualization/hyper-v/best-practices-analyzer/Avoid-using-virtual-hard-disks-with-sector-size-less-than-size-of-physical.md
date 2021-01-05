---
title: Evite usar discos rígidos virtuais com um tamanho de setor menor que o tamanho de setor do armazenamento físico que armazena o arquivo de disco rígido virtual
description: Saiba o que fazer quando um ou mais discos rígidos virtuais têm um tamanho de setor físico menor do que o tamanho de setor físico do armazenamento no qual o arquivo de disco rígido virtual está localizado.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: b7cf994e-bf4b-4b1b-bad6-ecf7d46d105e
ms.date: 8/16/2016
ms.openlocfilehash: e664b0947479935dd22c3409eeb0948e01fa9b89
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834481"
---
# <a name="avoid-using-virtual-hard-disks-with-a-sector-size-less-than-the-sector-size-of-the-physical-storage-that-stores-the-virtual-hard-disk-file"></a>Evite usar discos rígidos virtuais com um tamanho de setor menor que o tamanho de setor do armazenamento físico que armazena o arquivo de disco rígido virtual

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Operacional** <br />**System**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>**Problema**
*Um ou mais discos rígidos virtuais têm um tamanho de setor físico menor do que o tamanho do setor físico do armazenamento no qual o arquivo do disco rígido virtual está localizado.*

## <a name="impact"></a>**Impacto**
*Podem ocorrer problemas de desempenho na máquina virtual ou no aplicativo que usa o disco rígido virtual. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>**Resolução**
*Realize um dos seguintes procedimentos:*

-   *Executar uma migração de armazenamento para mover o disco rígido virtual para um novo sistema físico*

-   *Use o Windows PowerShell ou o WMI para habilitar um disco rígido virtual de formato VHDX para relatar um tamanho de setor específico*

-   *Use uma configuração do registro para habilitar um disco rígido virtual em formato VHD para relatar um tamanho de setor físico de 4K*



