---
title: Use pelo menos o protocolo SMB versão 3,0 para compartilhamentos de arquivos que armazenam arquivos para máquinas virtuais.
description: Saiba o que fazer quando arquivos de máquina virtual ou arquivos de disco rígido virtual são armazenados em um compartilhamento de arquivos que não suporta pelo menos o protocolo SMB versão 3,0.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 4bb832b8-f1aa-4c1f-a0f2-324dd53553ea
ms.date: 8/16/2016
ms.openlocfilehash: 783ba7b2e8b5dc83eb575ee395d85e58701c0b89
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846223"
---
# <a name="use-at-least-smb-protocol-version-30-for-file-shares-that-store-files-for-virtual-machines"></a>Use pelo menos o protocolo SMB versão 3,0 para compartilhamentos de arquivos que armazenam arquivos para máquinas virtuais.

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Erro|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>**Problema**
*Os arquivos de máquina virtual ou os arquivos de disco rígido virtual são armazenados em um compartilhamento de arquivos que não dá suporte ao protocolo SMB versão 3,0.*

## <a name="impact"></a>**Impacto**
*A Microsoft não oferece suporte a essa configuração. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>**Resolução**
*Mova os arquivos para um compartilhamento de arquivos que usa pelo menos o protocolo SMB versão 3,0.*



