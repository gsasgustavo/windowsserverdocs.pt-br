---
title: Exibir registros de recurso de DNS para um endereço IP específico
description: Este tópico faz parte do guia de gerenciamento do IPAM (gerenciamento de endereços IP) no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: f590fb86-4195-4f90-98cb-e90459d4c1e3
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 2f1dd1f87ecaa390d5e5c43a7dc2ad9267fe8161
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948312"
---
# <a name="view-dns-resource-records-for-a-specific-ip-address"></a>Exibir registros de recurso de DNS para um endereço IP específico

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para exibir os registros de recursos de DNS que estão associados ao endereço IP que você escolher.

A associação em **Administradores**, ou equivalente, é o requisito mínimo para executar este procedimento.

### <a name="to-view-resource-records-for-an-ip-address"></a>Para exibir registros de recursos para um endereço IP

1.  Em Gerenciador do Servidor, clique em  **IPAM**. O console do cliente IPAM é exibido.

2.  No painel de navegação, em **espaço de endereço IP**, clique em **inventário de endereço IP**. No painel de navegação inferior, clique em **IPv4** ou **IPv6**. O inventário de endereço IP aparece na exibição de pesquisa do painel de exibição. Localize e selecione o endereço IP cujos registros de recursos DNS você deseja exibir.

    ![Exibir o inventário de endereços IP](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_01.jpg)

3.  No modo de exibição **detalhes** do painel de exibição, clique em **registros de recursos DNS**. Os registros de recursos associados ao endereço IP selecionado são exibidos.

    ![Exibir registros de recursos de DNS](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_02.jpg)

## <a name="see-also"></a>Consulte Também
Gerenciamento de registros de [recursos de DNS](DNS-Resource-Record-Management.md) 
 [Gerenciar IPAM](Manage-IPAM.md)



