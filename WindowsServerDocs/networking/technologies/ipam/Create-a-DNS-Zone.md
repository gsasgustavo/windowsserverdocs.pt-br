---
title: Criar uma zona DNS
description: Este tópico faz parte do guia de gerenciamento do IPAM (gerenciamento de endereços IP) no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: a030ff51-a815-4fc4-b26d-aae41c3e4ce5
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 7131e1334330206dba31830d5966f878ee846bce
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949042"
---
# <a name="create-a-dns-zone"></a>Criar uma zona DNS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este tópico para criar uma zona DNS usando o console do cliente IPAM.

A associação em **Administradores**, ou equivalente, é o requisito mínimo para executar este procedimento.

### <a name="to-create-a-dns-zone"></a>Para criar uma zona DNS

1.  Em Gerenciador do Servidor, clique em  **IPAM**. O console do cliente IPAM é exibido.

2.  No painel de navegação, em **monitorar e gerenciar**, clique em **servidores DNS e DHCP**. No painel de exibição, clique em **tipo de servidor** e, em seguida, clique em **DNS**. Todos os servidores DNS gerenciados pelo IPAM são listados nos resultados da pesquisa.

3.  Localize o servidor no qual você deseja adicionar uma zona e clique com o botão direito do mouse no servidor.  Clique em **criar zona DNS**.

    ![Criar zona DNS](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)

4.  A caixa de diálogo **criar zona DNS** é aberta. Em **Propriedades gerais**, selecione uma categoria de zona, um tipo de zona e insira um nome em **nome da zona**. Selecione também os valores apropriados para sua implantação em **Propriedades avançadas** e clique em **OK**.

    ![Propriedades avançadas](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)

## <a name="see-also"></a>Consulte Também
Gerenciamento de zona [DNS](DNS-Zone-Management.md) 
 [Gerenciar IPAM](Manage-IPAM.md)



