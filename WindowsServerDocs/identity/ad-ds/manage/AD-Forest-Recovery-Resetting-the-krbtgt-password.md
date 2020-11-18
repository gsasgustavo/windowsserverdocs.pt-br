---
title: Recuperação de floresta do AD-redefinindo a senha krbtgt
description: Como redefinir a senha krbtgt para o domínio.
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 3bd6c1d0-d316-4b03-b7b4-557d4537635c
ms.openlocfilehash: 0fc21aa9daf6ed528d5501f1703c847c03a8aff7
ms.sourcegitcommit: 7f859d8ec86664fdedd05901ac3714f84e7868b5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94703762"
---
# <a name="ad-forest-recovery---resetting-the-krbtgt-password"></a>Recuperação de floresta do AD-redefinindo a senha krbtgt

> Aplica-se a: Windows Server 2019, Windows Server 2016, Windows Server 2012 e 2012 R2, Windows Server 2008 e 2008 R2

Use o procedimento a seguir para redefinir a senha krbtgt para o domínio. O procedimento a seguir aplica os DCs graváveis, mas não os RODCs (controladores de domínio somente leitura).

> [!IMPORTANT]
> Se você planeja recuperar os RODCs online durante a recuperação da floresta, não exclua as contas krbtgt para os RODCs. A conta krbtgt para um RODC é listada no formato krbtgt_ *número*.
>
> Se você usar um filtro de senha personalizado (como passfilt.dll) em um controlador de domínio, poderá receber um erro ao tentar redefinir a senha krbtgt. Para obter mais informações, incluindo uma solução alternativa, consulte o [artigo 2549833](https://support.microsoft.com/kb/2549833) da base de dados de conhecimento Microsoft ( https://support.microsoft.com/kb/2549833) .

## <a name="to-reset-the-krbtgt-password"></a>Para redefinir a senha krbtgt

1. Clique em **Iniciar**, aponte para **painel de controle**, aponte para **ferramentas administrativas** e clique em **Active Directory usuários e computadores**.

2. Clique em **Exibir** e em **Recursos Avançados**.

3. Na árvore de console, clique duas vezes no contêiner de domínio e, em seguida, clique em **usuários**.

4. No painel de detalhes, clique com o botão direito do mouse na conta de usuário **krbtgt** e clique em **Redefinir senha**.

   ![Redefinir senha](media/AD-Forest-Recovery-Resetting-the-krbtgt-password/resetpass1.png)

5. Em **nova senha**, digite uma nova senha, digite a senha novamente em **Confirmar senha** e clique em **OK**. A senha que você especificar não é significativa porque o sistema irá gerar uma senha forte automaticamente independente da senha que você especificar.

> [!IMPORTANT]
> Você deve executar essa operação duas vezes. Ao redefinir a senha da conta de serviço do centro de distribuição de chaves duas vezes, um período de espera de 10 horas é necessário entre as redefinições. 10 horas são o **tempo de vida máximo padrão para o tíquete de usuário** e o **tempo de vida máximo para configurações de** política de tíquete de serviço, portanto, em um caso em que o período de tempo de vida máximo foi alterado, o período de espera mínimo entre redefinições deve ser maior que o valor configurado.  

> [!NOTE]
> O valor do histórico de senha para a conta krbtgt é 2, o que significa que ela inclui as 2 senhas mais recentes. Ao redefinir a senha duas vezes, você limpa efetivamente todas as senhas antigas do histórico, portanto, não há como o outro controlador de domínio será replicado com esse controlador de domínio usando uma senha antiga.

## <a name="next-steps"></a>Próximas etapas

- [Guia de recuperação de floresta do AD](AD-Forest-Recovery-Guide.md)

- [Recuperação de floresta do AD – Procedimentos](AD-Forest-Recovery-Procedures.md)
