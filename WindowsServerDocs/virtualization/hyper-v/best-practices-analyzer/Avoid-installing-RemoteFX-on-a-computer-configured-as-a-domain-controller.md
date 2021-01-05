---
title: Evite instalar o RemoteFX em um computador configurado como um controlador de domínio Active Directory
description: Saiba o que fazer quando o RemoteFX é instalado em um controlador de domínio.
ms.author: benarm
author: BenjaminArmstrong
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
ms.date: 8/16/2016
ms.openlocfilehash: d22f21af2fcc54c44d142ef790b9da4ae66483c9
ms.sourcegitcommit: 48d45b2adf44afb0207214be9c57fe589360d177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97834661"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Evite instalar o RemoteFX em um computador configurado como um controlador de domínio Active Directory

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
*O RemoteFX é instalado em um controlador de domínio.*

## <a name="impact"></a>**Impacto**
*Os computadores virtuais configurados para RemoteFX não podem ser usados nesses computadores.*

## <a name="resolution"></a>**Resolução**
*Decida se deseja que esse servidor seja configurado com o RemoteFX para Hyper-V ou como um controlador de Domínio do Active Directory e reconfigure o servidor conforme necessário.*



