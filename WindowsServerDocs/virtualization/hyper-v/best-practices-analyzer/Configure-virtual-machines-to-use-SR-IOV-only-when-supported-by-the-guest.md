---
title: Configurar máquinas virtuais para usar o SR-IOV somente quando houver suporte do sistema operacional convidado
description: Saiba o que fazer quando uma ou mais máquinas virtuais são configuradas para usar O SR-IOV (virtualização de e/s de raiz única), mas o sistema operacional convidado não oferece suporte a SR-IOV.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 33cf5b68-e43e-47ef-adbc-6b266c1d4dce
ms.date: 8/16/2016
ms.openlocfilehash: 2f919f3ed2708b9d388a5215d73e629dc93f9922
ms.sourcegitcommit: 42581433c0bb62e291d412ee9e13869b42e69a4b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846388"
---
# <a name="configure-virtual-machines-to-use-sr-iov-only-when-supported-by-the-guest-operating-system"></a>Configurar máquinas virtuais para usar o SR-IOV somente quando houver suporte do sistema operacional convidado

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
*Uma ou mais máquinas virtuais estão configuradas para usar O SR-IOV (virtualização de e/s de raiz única), mas o sistema operacional convidado não oferece suporte a SR-IOV*

## <a name="impact"></a>Impacto
*As funções virtuais SR-IOV não serão alocadas para as seguintes máquinas virtuais:*

\<list of virtual machines>

## <a name="resolution"></a>Resolução
*Desabilite o SR-IOV em todas as máquinas virtuais que executam sistemas operacionais convidados que não dão suporte a SR-IOV.*

O SR-IOV tem suporte apenas em alguns convidados do Windows de 64 bits. Para obter detalhes, consulte [compatibilidade de recursos do Hyper-V por geração e convidado](../Hyper-V-feature-compatibility-by-generation-and-guest.md).



