---
title: Use pelo menos a versão 3,0 do protocolo SMB configurada para disponibilidade contínua em compartilhamentos de arquivos que armazenam arquivos para máquinas virtuais
description: Saiba o que fazer quando arquivos de máquina virtual ou arquivos de disco rígido virtual são armazenados em um compartilhamento de arquivos de rede que não está configurado com o recurso de disponibilidade contínua do protocolo SMB versão 3,0.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: a1fa5cf9-8a48-4f63-bb57-d81e63e77b30
ms.date: 8/16/2016
ms.openlocfilehash: a71976a3ebe8eb152993be6e4760679664a6eeed
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846300"
---
# <a name="use-at-least-smb-protocol-version-30-configured-for-continuous-availability-on-file-shares-that-store-files-for-virtual-machines"></a>Use pelo menos a versão 3,0 do protocolo SMB configurada para disponibilidade contínua em compartilhamentos de arquivos que armazenam arquivos para máquinas virtuais

>Aplica-se a: Windows Server 2016

Para obter mais informações sobre práticas recomendadas e varreduras, confira [Executar varreduras do Analisador de Práticas Recomendadas e gerenciar os resultados](https://go.microsoft.com/fwlink/p/?LinkID=223177).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Aviso|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>**Problema**
*Os arquivos de máquina virtual ou os arquivos de disco rígido virtual são armazenados em um compartilhamento de arquivos de rede que não está configurado com o recurso de disponibilidade contínua do protocolo SMB versão 3,0.*

## <a name="impact"></a>**Impacto**
*A Microsoft não recomenda essa configuração porque ela pode afetar a disponibilidade das máquinas virtuais usando o servidor. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>**Resolução**
Realize um dos seguintes procedimentos:

-   Mova os arquivos para um compartilhamento de arquivos SMB 3,0 configurado para disponibilidade contínua.

-   Reconfigure o compartilhamento de arquivos atual para fornecer disponibilidade contínua.



