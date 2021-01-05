---
title: A autenticação baseada em certificado está configurada, mas o certificado especificado não está instalado no servidor de réplica ou nos nós de cluster de failover
description: Saiba o que fazer quando o certificado de segurança que a réplica do Hyper-V tiver sido configurado para fornecer replicação baseada em certificado não estiver instalado no servidor de réplica (ou em qualquer nó de cluster de failover).
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: 4cabbce3-9367-4ddc-a108-1e5e1ab2bcff
ms.date: 8/16/2016
ms.openlocfilehash: 2f45c8e5699d8f55ea0ba0c69418217fd046bc63
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97833621"
---
# <a name="certificate-based-authentication-is-configured-but-the-specified-certificate-is-not-installed-on-the-replica-server-or-failover-cluster-nodes"></a>A autenticação baseada em certificado está configurada, mas o certificado especificado não está instalado no servidor de réplica ou nos nós de cluster de failover

>Aplica-se a: Windows Server 2016



*Para obter mais informações sobre práticas recomendadas e verificações, consulte* [analisador de práticas recomendadas](https://go.microsoft.com/fwlink/?LinkId=122786).

|Propriedade|Detalhes|
|-|-|
|**Sistema operacional**|Windows Server 2016|
|**Produto/Recurso**|Hyper-V|
|**Gravidade**|Erro|
|**Categoria**|Configuração|

Nas seções a seguir, os itálicos indicam o texto da interface do usuário que aparece na ferramenta de Analisador de Práticas Recomendadas para esse problema.

## <a name="issue"></a>Problema

*O certificado de segurança que a réplica do Hyper-V foi configurado para fornecer replicação baseada em certificado não está instalado no servidor de réplica (ou em qualquer nó de cluster de failover).*

## <a name="impact"></a>Impacto

*No caso de um failover de cluster ou de mudança para outro nó, a replicação do Hyper-V será pausada se o novo nó também não tiver o certificado apropriado instalado. Isso afeta os seguintes nós:*

\<list of nodes>

## <a name="resolution"></a>Resolução

*Instale o certificado configurado no servidor de réplica (e todos os nós associados no cluster de failover, se houver).*



