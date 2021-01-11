---
title: Limite de credenciais por aplicativo
description: Solução de um problema em que apenas vinte credenciais podem ser usadas por aplicativo.
ms.topic: troubleshooting
author: HeidiLohr
manager: lizross
ms.author: helohr
ms.date: 12/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5ce9b606e9205758b819dfe89cadbd0187357243
ms.sourcegitcommit: 4f7308430a69fe7965e16aa5b31f87c5d68e4a09
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97578260"
---
# <a name="credential-limit-per-app"></a>Limite de credenciais por aplicativo

O Windows só permite até 20 credenciais por aplicativo. Caso você precise ter mais de 20 credenciais por aplicativo, siga as instruções descritas neste artigo.

## <a name="bypass-the-20-credential-limit"></a>Ignorar o limite de 20 credenciais

Para ignorar o limite de 20 credenciais:

1. Abra o PowerShell como administrador.
2. Defina o valor da entrada do Registro DWORD **HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Vault\MaxPerAppCredentialNumber** com um número maior que 20.
3. Reinicie o computador.
4. Teste as configurações criando um conjunto de credenciais no cliente da Área de Trabalho Remota.

## <a name="potential-risks"></a>Riscos potenciais

Ao alterar essa configuração do Registro, é importante se lembrar do seguinte:

- Essa é uma operação de administrador. Qualquer erro introduzido no Registro pode fazer com que o computador se torne instável. Os usuários devem alterar as entradas do Registro por sua conta e risco.
- Essa alteração do Registro afetará todos os aplicativos do computador.
