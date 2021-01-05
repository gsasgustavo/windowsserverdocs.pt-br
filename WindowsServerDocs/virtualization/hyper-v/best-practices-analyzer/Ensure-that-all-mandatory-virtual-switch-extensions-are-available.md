---
title: Verifique se todas as extensões obrigatórias do comutador virtual estão disponíveis
description: Saiba o que fazer quando um ou mais adaptadores de rede virtual estiverem conectados a um comutador virtual com extensões obrigatórias que estão desabilitadas ou não instaladas.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
ms.date: 8/16/2016
ms.openlocfilehash: 0af9d5823740ebcfaaf740f8738ea91d4d827baa
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846135"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>Verifique se todas as extensões obrigatórias do comutador virtual estão disponíveis

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
*Um ou mais adaptadores de rede virtual estão conectados a um comutador virtual com extensões obrigatórias que estão desabilitadas ou não instaladas.*

## <a name="impact"></a>Impacto
*O tráfego de rede é bloqueado em um ou mais adaptadores de rede virtual nas seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Primeiro, verifique se a extensão obrigatória foi instalada no host e instale a extensão, se necessário. Em seguida, se a extensão obrigatória estiver desabilitada, use o Gerenciador de comutador virtual ou o cmdlet do Windows PowerShell Enable-VMSwitchExtension para habilitar a extensão.*



