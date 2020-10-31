---
title: Recuperação de floresta do AD-redefinindo uma senha de confiança
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.openlocfilehash: a4e1c02710b215ff5a527fa8ad39c6f78cdedceb
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070818"
---
# <a name="resetting-a-trust-password-on-one-side-of-the-trust"></a>Redefinindo uma senha de confiança em um lado da relação de confiança

>Aplica-se a: Windows Server 2016, Windows Server 2012 e 2012 R2, Windows Server 2008 e 2008 R2

 Se a recuperação de floresta estiver relacionada a uma violação de segurança, use o procedimento a seguir para redefinir uma senha de confiança em um lado da relação de confiança. Isso inclui confianças implícitas entre domínios filho e pai, bem como relações de confiança explícitas entre esse domínio (o domínio confiante) e outro domínio (o domínio confiável).

 Redefina a senha somente no lado do domínio confiante da relação de confiança, também conhecida como a relação de confiança de entrada (o lado onde pertence esse domínio). Em seguida, use a mesma senha no lado do domínio confiável da relação de confiança, também conhecida como a relação de confiança de saída. Redefina a senha da relação de confiança de saída ao restaurar o primeiro controlador de domínio em cada um dos outros domínios (confiáveis).

 Redefinir a senha de confiança garante que o DC não seja replicado com controladores de domínio potencialmente inválidos fora do seu Ao definir a mesma senha de confiança ao restaurar o primeiro controlador de domínio em cada um dos domínios, você garante que esse DC seja replicado com cada um dos DCs recuperados. Os DCs subsequentes no domínio que são recuperados com a instalação do AD DS irão replicar automaticamente essas novas senhas durante o processo de instalação.

## <a name="to-reset-a-trust-password-on-one-side-of-the-trust"></a>Para redefinir uma senha de confiança em um lado da relação de confiança

1. Em um prompt de comando, digite o seguinte comando e pressione ENTER:

   ```
   netdom experthelp trust
   ```

2. Use a sintaxe que esse comando fornece para usar a ferramenta NetDom para redefinir a senha de confiança.
   Por exemplo, se houver dois domínios na floresta — pai e filho — e você estiver executando esse comando no controlador de domínio restaurado no domínios pai, use a seguinte sintaxe de comando:

   ```
   netdom trust parent domain name /domain:child domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*
   ```

   Ao executar esse comando no domínio filho, use a seguinte sintaxe de comando:

   ```
   netdom trust child domain name /domain:parent domain name /resetOneSide /passwordT:password /userO:administrator /passwordO:*
   ```

   > [!NOTE]
   > a **senha** deve ter o mesmo valor em ambos os lados da relação de confiança. Execute este comando apenas uma vez (ao contrário do comando **netdom resetpwd** ) porque ele redefine automaticamente a senha duas vezes.

## <a name="next-steps"></a>Próximas etapas

- [Guia de recuperação de floresta do AD](AD-Forest-Recovery-Guide.md)
- [Recuperação de floresta do AD – Procedimentos](AD-Forest-Recovery-Procedures.md)
