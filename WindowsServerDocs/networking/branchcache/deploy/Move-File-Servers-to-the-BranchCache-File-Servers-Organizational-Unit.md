---
title: Mover servidores de arquivos para a unidade organizacional de servidores de arquivos BranchCache
description: Saiba como adicionar servidores de arquivos do BranchCache a uma UO (unidade organizacional) no Active Directory Domain Services (AD DS).
manager: brianlic
ms.topic: how-to
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: b96f417078d46ccdcc75621b24d4853a6695c69f
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949692"
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>Mover servidores de arquivos para a unidade organizacional de servidores de arquivos BranchCache

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para adicionar servidores de arquivos BranchCache a uma UO (unidade organizacional) no AD DS (Serviços de Domínio Active Directory).

A associação a **Adminis. do Domínio** ou equivalente é o requisito mínimo para a execução deste procedimento.

> [!NOTE]
> Você deve criar uma UO de servidores de arquivos BranchCache no console de Usuários e Computadores do Active Directory antes de adicionar contas de computador à UO com este procedimento. Para obter mais informações, consulte [criar a unidade organizacional de servidores de arquivos do BranchCache](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md).

### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>Para mover servidores de arquivos para a unidade organizacional de servidores de arquivos BranchCache

1.  Em um computador em que o AD DS está instalado, em Gerenciador do Servidor, clique em **ferramentas** e, em seguida, clique em **Active Directory usuários e computadores**. O console de Usuários e Computadores do Active Directory é aberto.

2.  No console de Usuários e Computadores do Active Directory, localize a conta de computador de um servidor de arquivos BranchCache, clique para selecionar a conta e arraste e solte a conta de computador na UO de servidores de arquivos BranchCache que você criou. Por exemplo, se você criou anteriormente uma UO denominada **servidores de arquivos do BranchCache**, arraste e solte a conta de computador na UO servidores de arquivos do **BranchCache** .

3.  Repita a etapa anterior para cada servidor de arquivos BranchCache no domínio que você deseja mover para a UO.



