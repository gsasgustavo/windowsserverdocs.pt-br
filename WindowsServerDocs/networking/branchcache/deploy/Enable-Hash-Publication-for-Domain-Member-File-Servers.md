---
title: Habilitar publicação de hash para servidores de arquivos associados ao domínio
description: Saiba como habilitar a publicação de hash do BranchCache para vários servidores de arquivos.
manager: brianlic
ms.topic: how-to
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: lizross
author: eross-msft
ms.date: 01/05/2021
ms.openlocfilehash: f09b26b76cfdf343773767067d33a39fbd458736
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948452"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>Habilitar publicação de hash para servidores de arquivos associados ao domínio

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Quando estiver usando Active Directory Domain Services (AD DS), você poderá usar o Política de Grupo de domínio para habilitar a publicação de hash do BranchCache para vários servidores de arquivos. Para fazer isso, você deve criar uma UO (unidade organizacional), adicionar servidores de arquivos à UO, criar uma publicação de hash do BranchCache Política de Grupo objeto (GPO) e, em seguida, configurar o GPO.

Consulte os tópicos a seguir para habilitar a publicação de hash para vários servidores de arquivos.

-   [Criar a unidade organizacional de servidores de arquivos BranchCache](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [Mover servidores de arquivos para a unidade organizacional de servidores de arquivos BranchCache](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)

-   [Criar o Objeto de Política de Grupo de publicação de hash BranchCache](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)

-   [Configurar o Objeto de Política de Grupo de publicação de hash BranchCache](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)



