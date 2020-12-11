---
description: 'Saiba mais sobre: autorizar hosts Hyper-V usando o atestado de administrador confiável'
title: Adicionar informações do host para o atestado confiável do administrador
ms.topic: article
ms.assetid: 87089ebc-b953-4aa3-96b5-966cf91acb02
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 0a4a9f7ebf3f88f6e19c4a78cb8dabd66c2004b9
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97047534"
---
# <a name="authorize-hyper-v-hosts-using-admin-trusted-attestation"></a>Autorizar hosts Hyper-V usando o atestado de administrador confiável

> Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

> [!IMPORTANT]
> O atestado confiável de administrador (modo de anúncio) é preterido a partir do Windows Server 2019. Para ambientes em que o atestado do TPM não é possível, configure o [atestado de chave do host](guarded-fabric-initialize-hgs-key-mode.md). O atestado de chave de host fornece garantia semelhante ao modo AD e é mais simples de configurar.


Para autorizar um host protegido no modo AD:

1. No domínio de malha, adicione os hosts Hyper-V a um grupo de segurança.
2. No domínio HGS, registre o SID do grupo de segurança com HGS.

## <a name="add-the-hyper-v-host-to-a-security-group-and-reboot-the-host"></a>Adicionar o host Hyper-V a um grupo de segurança e reinicializar o host

1. Crie um grupo de segurança **global** no domínio de malha e adicione hosts Hyper-V que executarão VMs blindadas.
   Reinicie os hosts para atualizar sua associação de grupo.

2. Use Get-ADGroup para obter o SID (identificador de segurança) do grupo de segurança e fornecê-lo ao administrador do HGS.

   ```powershell
   Get-ADGroup "Guarded Hosts"
   ```

   ![Get-AdGroup comando com a saída](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

## <a name="register-the-sid-of-the-security-group-with-hgs"></a>Registrar o SID do grupo de segurança com HGS

1. Obtenha o SID do grupo de segurança para hosts protegidos do administrador da malha e execute o comando a seguir para registrar o grupo de segurança com o HGS.
   Execute novamente o comando, se necessário, para grupos adicionais.
   Forneça um nome amigável para o grupo.
   Ele não precisa corresponder ao nome do grupo de segurança Active Directory.

   ```powershell
   Add-HgsAttestationHostGroup -Name "<GuardedHostGroup>" -Identifier "<SID>"
   ```

2. Para verificar se o grupo foi adicionado, execute [Get-HgsAttestationHostGroup](https://technet.microsoft.com/library/mt652172.aspx).


