---
title: A interface de equipe associada a um comutador virtual deve estar no modo padrão
description: Saiba o que fazer quando alguns comutadores virtuais estão associados a uma interface de equipe, mas a interface de equipe não passa o tráfego em todas as VLANs para os comutadores virtuais.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 8c118e1e-865f-4cff-acdc-7c35e45d5da9
ms.date: 8/16/2016
ms.openlocfilehash: e12ed7286a3aba4d6bb4f4bd3c72481326f44e0f
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97845901"
---
# <a name="the-team-interface-bound-to-a-virtual-switch-should-be-in-default-mode"></a>A interface de equipe associada a um comutador virtual deve estar no modo padrão

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
*Alguns comutadores virtuais estão associados a uma interface de equipe, mas a interface de equipe não passa o tráfego em todas as VLANs para os comutadores virtuais.*

## <a name="impact"></a>**Impacto**
*Os seguintes comutadores virtuais não podem ter acesso a todas as VLANs: \n{0}*

## <a name="resolution"></a>**Resolução**
*Use Gerenciador do Servidor ou o cmdlet do Windows PowerShell Set-NetLbfoTeamNic para redefinir a interface de equipe para o modo padrão.*



