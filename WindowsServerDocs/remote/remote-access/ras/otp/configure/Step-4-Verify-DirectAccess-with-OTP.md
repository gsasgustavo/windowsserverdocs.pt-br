---
title: Etapa 4 verificar DirectAccess com OTP
description: Este tópico faz parte do guia implantar o acesso remoto com autenticação OTP no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: ed49a0a3-1c45-42e5-8f13-cad20c1c1d68
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: c122eb1113d7d4bb63c5e03c3b047b2d88d53be4
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946442"
---
# <a name="step-4-verify-directaccess-with-otp"></a>Etapa 4 verificar DirectAccess com OTP

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Este tópico descreve como verificar se você configurou corretamente o DirectAccess com a implantação de OTP.

### <a name="to-verify-otp-health-on-the-remote-access-server"></a>Para verificar a integridade da OTP no servidor de acesso remoto

1. No servidor de acesso remoto, abra o console de **Gerenciamento de acesso remoto** .

2. Em **servidores de acesso remoto** , clique no servidor de acesso remoto que foi configurado para o suporte à OTP.

3. Clique em **status de operações**.

4. Verifique se o status de OTP exibe o ícone verde e está funcionando.

    > [!NOTE]
    > O intervalo de atualização do status de integridade será um máximo da soma dos valores da chave do registro HKLM\SYSTEM\CCS\Services\Ramgmtsvc\parameters\HealthRefreshTimeout e do **intervalo de tempo para a atividade do servidor** que foi definida na configuração de acesso remoto.

### <a name="to-verify-access-to-internal-resources-using-otp-authentication"></a>Para verificar o acesso a recursos internos usando a autenticação OTP

1.  Conecte um computador cliente do DirectAccess à rede corporativa e execute **gpupdate/force** no prompt de comando para obter a política de grupo.

2.  Desconecte o computador cliente da rede corporativa, conecte-se à rede externa e tente acessar os recursos internos. Você não deve ter acesso aos recursos internos.

3.  No caso de um token de software, acesse o token do cliente de OTP usando as instruções do fornecedor e anote o código do token atual. Quando um token de hardware for usado, siga as instruções do fornecedor para autenticação.

4.  Clique no ícone **Conexões de rede** na área de notificação para acessar o Gerenciador de Mídia do DA.

5.  Clique na **conexão do DirectAccess** e clique em **continuar**.

6.  Insira o código do token observado anteriormente e clique em **OK**. Aguarde a conclusão da autenticação. O status da conexão do local de trabalho do DirectAccess agora será **conectado**.

7.  Tentativa de acessar recursos internos. Você deve conseguir acessar todos os recursos corporativos.



