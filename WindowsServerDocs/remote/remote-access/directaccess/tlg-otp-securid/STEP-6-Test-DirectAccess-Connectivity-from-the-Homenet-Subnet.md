---
title: ETAPA 6 teste a conectividade do DirectAccess da sub-rede HomeNet
description: Saiba como começar a testar a conectividade da sub-rede HomeNet.
manager: brianlic
ms.topic: article
ms.assetid: b9b77cfd-8dd4-476b-a118-f3d6bf59e7b1
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 1d0cd5c85ca97ffd7d5275d2402db17a560255fa
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98040336"
---
# <a name="step-6-test-directaccess-connectivity-from-the-homenet-subnet"></a>ETAPA 6 teste a conectividade do DirectAccess da sub-rede HomeNet

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

A implantação de OTP (senha de uso único) do DirectAccess agora está concluída e você pode começar a testar a conectividade da sub-rede HomeNet.

### <a name="to-test-otp-functionality-from-the-homenet-subnet-on-client1"></a>Para testar a funcionalidade de OTP da sub-rede HomeNet em CLIENT1

1. Em CLIENT1, certifique-se de que você está conectado como **Usuário1**.

2. Na tela **Iniciar** , digite **powershell.exe**, clique com o botão direito do mouse em **PowerShell**, clique em **avançado** e, em seguida, clique em **Executar como administrador**. Se a caixa de diálogo **Controle de Conta de Usuário** aparecer, confirme se a ação exibida é a que você deseja e, em seguida, clique em **Sim**.

3. Na janela do Windows PowerShell, digite **gpupdate/force** e pressione Enter.

4. Desconecte o CLIENT1 da sub-rede corpnet e conecte-o à sub-rede HomeNet.

5. Em CLIENT1, abra o Internet Explorer e, na barra de endereços, digite **https://app1.corp.contoso.com/** e pressione Enter. Pressione F5.

   O site não deve abrir.

6. Na tela **Iniciar** , digite **RSA** e clique em **token RSA SecurID**.

7. Aguarde até que o token RSA SecurID altere a senha de uso único e, em seguida, clique em **copiar**.

8. Clique no ícone **Conexões de rede** na área de notificação para acessar o Gerenciador de Mídia do DA.

9. Clique em **conexão do contoso DirectAccess** e clique em **continuar**.

10. Pressione Ctrl + Alt + Delete e clique no bloco **OTP (senha de uso único)** .

11. Cole o tokencode de oito dígitos copiado anteriormente e clique em **OK**. Aguarde a conclusão da autenticação. O status da conexão do local de trabalho do DirectAccess agora será **conectado**.

12. No Internet Explorer, na barra de endereços, digite **https://app1.corp.contoso.com/** e pressione Enter. Pressione F5. Você verá o site de IIS padrão no APP1.

13. Na barra de endereços do Internet Explorer, digite **https://app2.corp.contoso.com/** e pressione Enter. Pressione F5. Você verá o site do IIS padrão em APP2.

14. Na tela **Iniciar** , digite <strong> \\ \app1\files</strong>e pressione Enter.

15. Na janela pasta compartilhada **arquivos** , clique duas vezes no arquivo **Example.txt** . Você verá o conteúdo do arquivo de Example.txt.

16. Na tela **Iniciar** , digite <strong> \\ \app2\files</strong>e pressione Enter.

17. Na janela pasta compartilhada **arquivos** , clique duas vezes no novo arquivo de **Document.txtde texto** . Você verá o conteúdo do novo arquivo de Document.txt de texto.



