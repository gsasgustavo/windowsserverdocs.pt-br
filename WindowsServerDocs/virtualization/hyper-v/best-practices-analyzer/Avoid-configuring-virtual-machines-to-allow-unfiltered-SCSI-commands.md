---
title: Evite configurar máquinas virtuais para permitir comandos SCSI não filtrados
description: Saiba o que fazer quando uma máquina virtual estiver configurada para permitir comandos SCSI não filtrados.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
ms.date: 8/16/2016
ms.openlocfilehash: 70282ef6367c711e04bf5d29ee10303841019b2c
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834691"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>Evite configurar máquinas virtuais para permitir comandos SCSI não filtrados

>Aplica-se a: Windows Server 2016



*Para obter mais informações sobre práticas recomendadas e verificações, consulte* [analisador de práticas recomendadas](https://go.microsoft.com/fwlink/?LinkId=122786).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Operações|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema

*Uma máquina virtual está configurada para permitir comandos SCSI não filtrados.*

## <a name="impact"></a>Impacto

*Ignorar a filtragem de comando SCSI representa um risco de segurança. Essa configuração deve ser habilitada somente se for necessária para compatibilidade com aplicativos de armazenamento em execução no sistema operacional convidado. As seguintes máquinas virtuais estão configuradas para permitir comandos SCSI não filtrados:*

\<list of virtual machine names>

## <a name="resolution"></a>Resolução

*Entre em contato com seu fornecedor de armazenamento para determinar se essa configuração é necessária. Além disso, se o sistema operacional de gerenciamento ou outros sistemas operacionais convidados estiverem comprometidos ou apresentarem comportamento incomum, reconfigure a máquina virtual para bloquear os comandos.*



