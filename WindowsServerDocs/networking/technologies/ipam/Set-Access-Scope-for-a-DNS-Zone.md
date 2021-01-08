---
title: Definir escopo de acesso para uma zona DNS
description: Saiba como definir o escopo de acesso para uma zona DNS usando o console do cliente IPAM.
manager: brianlic
ms.topic: article
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 8d679dcc0e16e1dc3e38e11247637463a26ed0f5
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040136"
---
# <a name="set-access-scope-for-a-dns-zone"></a>Definir escopo de acesso para uma zona DNS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para definir o escopo de acesso para uma zona DNS usando o console do cliente IPAM.

A associação em **Administradores**, ou equivalente, é o requisito mínimo para executar este procedimento.

### <a name="to-set-the-access-scope-for-a-dns-zone"></a>Para definir o escopo de acesso para uma zona DNS

1.  Em Gerenciador do Servidor, clique em  **IPAM**. O console do cliente IPAM é exibido.

2.  No painel de navegação, clique em **zonas DNS**. No painel de exibição, clique com o botão direito do mouse na zona DNS para a qual você deseja alterar o escopo de acesso. e clique em **definir escopo de acesso**.

    ![Definir Escopo de Acesso](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)

3.  A caixa de diálogo **definir escopo de acesso** é aberta. Se necessário para sua implantação, clique para anular a seleção **de herdar o escopo de acesso do pai**. Em **selecionar o escopo de acesso**, selecione um item e clique em **OK**.

    ![Selecionar o escopo de acesso](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)

4.  No painel de exibição do console do cliente IPAM, verifique se o escopo de acesso da zona foi alterado.

    ![Verifique se o escopo de acesso da zona foi alterado](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)

## <a name="see-also"></a>Consulte Também
Controle de acesso [baseado em função](Role-based-Access-Control.md) 
 [Gerenciar IPAM](Manage-IPAM.md)



