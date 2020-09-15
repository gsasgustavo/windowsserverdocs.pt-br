---
title: Serviços do MultiPoint – tarefas de pós-implantação
description: Saiba como validar e fechar sua migração para os serviços do MultiPoint
ms.date: 07/29/2016
ms.topic: article
ms.assetid: 1497cae0-071e-467d-89b8-a7050815d7de
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 4cfd658c8d5ed6109bd18c7ebb06ce6fcf355661
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90077573"
---
# <a name="multipoint-services---post-migration-tasks"></a>Serviços do MultiPoint – tarefas de pós-implantação

>Aplica-se a: Windows Server 2016

Depois de migrar para os serviços do MultiPoint no Windows Server 2016, use as informações a seguir para validar a migração e executar etapas de limpeza.

## <a name="validate-the-migration-by-running-a-pilot-program"></a>Validar a migração executando um programa piloto

Você pode validar sua migração de serviços do MultiPoint criando um projeto piloto no ambiente de produção. Execute o projeto piloto nos servidores antes de colocar os serviços de função migrados em produção para verificar se a implantação funciona conforme o esperado. Considere limitar o número de conexões primeiro, aumentando lentamente o número de usuários que acessam os serviços do MultiPoint.

> [!NOTE]
> Sempre use contas de teste para testar a migração. Use uma conta com privilégios administrativos e uma conta para um usuário válido.

## <a name="retire-the-source-server"></a>Desativar o servidor de origem
Depois de validar a migração, você pode desligar ou desconectar o servidor de origem da rede. Se o servidor tiver ingressado no domínio, remova-o do domínio antes de desconectá-lo.

