---
title: Criar a unidade organizacional de servidores de arquivos BranchCache
description: Saiba como criar uma UO (unidade organizacional) no Active Directory Domain Services (AD DS) para servidores de arquivos do BranchCache.
manager: brianlic
ms.topic: how-to
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: ff436166eedb4a3214361267f1d508ebe3acc6e4
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97950292"
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>Criar a unidade organizacional de servidores de arquivos BranchCache

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para criar uma UO (unidade organizacional) no AD DS (Serviços de Domínio Active Directory) para servidores de arquivos BranchCache.

A associação a **Adminis. do Domínio** ou equivalente é o requisito mínimo para a execução deste procedimento.

### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>Para criar a unidade organizacional de servidores de arquivos BranchCache

1.  Em um computador em que o AD DS está instalado, em Gerenciador do Servidor, clique em **ferramentas** e, em seguida, clique em **Active Directory usuários e computadores**. O console de Usuários e Computadores do Active Directory é aberto.

2.  No console de Usuários e Computadores do Active Directory, clique com o botão direito do mouse no domínio ao qual você deseja adicionar uma UO. Por exemplo, se o domínio for denominado exemplo.com, clique com o botão direito do mouse em **exemplo.com**. Aponte para **Novo** e clique em **Unidade Organizacional**. A caixa de diálogo **novo objeto – unidade organizacional** é aberta.

3.  Na caixa de diálogo **novo objeto – unidade organizacional** , em **nome**, digite um nome para a nova UO. Por exemplo, se desejar denominar a UO de Servidores de arquivos BranchCache, digite **Servidores de arquivos BranchCache** e clique em **OK**.



