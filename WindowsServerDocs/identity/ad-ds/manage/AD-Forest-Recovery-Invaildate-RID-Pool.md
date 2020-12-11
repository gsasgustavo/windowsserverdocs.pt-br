---
description: 'Saiba mais sobre: recuperação de floresta do AD-invalidando o pool RID atual'
title: Recuperação de floresta do AD-invalidando o pool RID
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.openlocfilehash: 7d517600a00fe5806b4b1539f08602beb1699269
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97042914"
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>Recuperação de floresta do AD-invalidando o pool RID atual

>Aplica-se a: Windows Server 2016, Windows Server 2012 e 2012 R2, Windows Server 2008 e 2008 R2

Use o procedimento a seguir para o Windows PowerShell para invalidar o pool RID atual em um controlador de domínio. O Windows PowerShell é habilitado por padrão no Windows Server 2012 e no Windows Server 2008 R2, mas não no Windows Server 2008, onde ele deve ser instalado usando **Adicionar recursos**. Ele pode ser [baixado](https://www.microsoft.com/download/details.aspx?id=20020) para ser executado no Windows Server 2003.

Para verificar se o comando foi concluído com êxito, verifique a ID do evento 16654 (a origem é Directory-Services-SAM) no log do sistema em Visualizador de Eventos no Windows Server 2012. As versões anteriores do Windows não registram esse evento.

> [!NOTE]
> Depois de invalidar o pool RID, você receberá um erro quando tentar criar a entidade de segurança (usuário, computador ou grupo). A tentativa de criar um objeto dispara uma solicitação para um novo pool de RIDs. A repetição da operação é realizada com sucesso porque o novo pool de RIDs será alocado.

## <a name="to-invalidate-the-current-rid-pool"></a>Para invalidar o pool RID atual

- Abra uma sessão do Windows PowerShell com privilégios elevados, execute o seguinte comando e pressione ENTER:

   ```powershell
   $Domain = New-Object System.DirectoryServices.DirectoryEntry
   $DomainSid = $Domain.objectSid
   $RootDSE = New-Object System.DirectoryServices.DirectoryEntry("LDAP://RootDSE")
   $RootDSE.UsePropertyCache = $false
   $RootDSE.Put("invalidateRidPool", $DomainSid.Value)
   $RootDSE.SetInfo()
   ```

## <a name="next-steps"></a>Próximas etapas

- [Guia de recuperação de floresta do AD](AD-Forest-Recovery-Guide.md)
- [Recuperação de floresta do AD – Procedimentos](AD-Forest-Recovery-Procedures.md)
