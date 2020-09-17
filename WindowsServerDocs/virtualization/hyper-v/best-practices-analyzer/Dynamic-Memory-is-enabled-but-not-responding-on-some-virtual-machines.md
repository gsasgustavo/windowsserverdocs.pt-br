---
title: Memória Dinâmica está habilitado, mas não respondendo em algumas máquinas virtuais
description: Versão online do texto para esta regra de Analisador de Práticas Recomendadas.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 91b7f50f-a071-4ab6-beb1-1b29f92f52b6
ms.date: 8/16/2016
ms.openlocfilehash: c826fc39637b3a7cf0f155065945d180bce5e4cb
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/17/2020
ms.locfileid: "90744131"
---
# <a name="dynamic-memory-is-enabled-but-not-responding-on-some-virtual-machines"></a>Memória Dinâmica está habilitado, mas não respondendo em algumas máquinas virtuais

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
*Uma ou mais máquinas virtuais estão enfrentando problemas com o driver necessário para Memória Dinâmica no sistema operacional convidado.*

## <a name="impact"></a>Impacto
*O sistema operacional convidado nas seguintes máquinas virtuais pode não ser executado ou pode ser executado de forma não confiável porque o Hyper-V não pode ajustar a memória dinamicamente para responder às alterações na demanda de memória. Isso afeta as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Esse comportamento será esperado se a máquina virtual estiver inicializando. Se a máquina virtual não estiver inicializando, verifique se os serviços de integração estão atualizados para a versão mais recente e se o sistema operacional convidado dá suporte a Memória Dinâmica.*

A partir do Windows Server 2016, o Integration Services é fornecido por meio de Windows Update. Verifique se as máquinas virtuais estão configuradas para receber atualizações para obter a versão mais recente do Integration Services.

Memória Dinâmica funciona com versões específicas de convidados com suporte. Consulte [visão geral de memória dinâmica do Hyper-V](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831766(v=ws.11)) para versões anteriores ao windows Server 2016 e Windows 10.