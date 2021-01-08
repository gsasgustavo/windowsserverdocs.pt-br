---
title: Filtrar a exibição de registros de recursos de DNS
description: Saiba como filtrar a exibição de registros de recursos de DNS no console do cliente IPAM.
manager: brianlic
ms.topic: article
ms.assetid: 5b80294a-7325-476b-84eb-69f0d051e8b2
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: b17c071d78079933a04663e4fd1cd3528a9b86cb
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98039556"
---
# <a name="filter-the-view-of-dns-resource-records"></a>Filtrar a exibição de registros de recursos de DNS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para filtrar a exibição de registros de recursos de DNS no console do cliente IPAM.

A associação em **Administradores**, ou equivalente, é o requisito mínimo para executar este procedimento.

### <a name="to-filter-the-view-of-dns-resource-records"></a>Para filtrar a exibição de registros de recursos de DNS

1.  Em Gerenciador do Servidor, clique em  **IPAM**. O console do cliente IPAM é exibido.

2.  No painel de navegação, em **monitorar e gerenciar**, clique em **zonas DNS**.  O painel de navegação divide-se em um painel de navegação superior e em um painel de navegação inferior.

3.  No painel de navegação inferior, clique em **pesquisa direta**. Todas as zonas de pesquisa direta do DNS gerenciadas pelo IPAM são exibidas nos resultados da pesquisa do painel de exibição.

4.  Clique na zona cujos registros você deseja exibir e filtrar.

5.  No painel de exibição, clique em **exibição atual** e em **registros de recursos**. Os registros de recursos para a zona são mostrados no painel de exibição.

6.  No painel de exibição, clique em **Adicionar critérios**.

    ![Adicionar critérios](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_01.jpg)

7.  Selecione um critério na lista suspensa. Por exemplo, se você quiser exibir um tipo de registro específico, clique em **tipo de registro**.

    ![Selecionar um critério](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_02.jpg)

8.  Clique em **Adicionar**.

    ![Adicionar os critérios](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_03.jpg)

9. O **tipo de registro** é adicionado como um parâmetro de pesquisa. Insira o texto para o tipo de registro que você deseja localizar. Por exemplo, se você quiser exibir somente os registros SRV, digite **SRV**.

    ![Especifique o tipo de registro que você deseja localizar](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_04.jpg)

10. Pressione ENTER. Os registros de recurso DNS são filtrados de acordo com os critérios e a frase de pesquisa que você especificou.

    ![Executar o filtro](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_05.jpg)

## <a name="see-also"></a>Consulte Também
Gerenciamento de registros de [recursos de DNS](DNS-Resource-Record-Management.md) 
 [Gerenciar IPAM](Manage-IPAM.md)



