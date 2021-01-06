---
title: Limpar dados de utilização
description: Este tópico faz parte do guia de gerenciamento do IPAM (gerenciamento de endereços IP) no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 125d91951f5deac4bf7a32591d9f98efbfabae66
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948002"
---
# <a name="purge-utilization-data"></a>Limpar dados de utilização

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para saber como excluir dados de utilização do banco de dado do IPAM.

Você deve ser membro de **Administradores do IPAM**, do grupo **Administradores** do computador local ou equivalente, para executar esse procedimento.

## <a name="to-purge-the-ipam-database"></a>Para limpar o banco de dados IPAM
1. Abra Gerenciador do Servidor e, em seguida, navegue até a interface do cliente IPAM.
2. Navegue até um dos seguintes locais: **blocos de endereço IP**, **inventário de endereço IP** ou **grupos de intervalos de endereços IP**.
3. Clique em **tarefas** e, em seguida, clique em **limpar dados de utilização**. A caixa de diálogo **limpar dados de utilização** é aberta.
4. Em **limpar todos os dados de utilização em ou antes**, clique em **selecionar uma data**.
5. Escolha a data para a qual você deseja excluir todos os registros de banco de dados e antes dessa data.
6. Clique em **OK**. IPAM exclui todos os registros que você especificou.
