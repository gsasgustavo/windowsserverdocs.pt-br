---
title: Personalizar Inscrição para a tarefa do Microsoft Azure Online Backup
description: Saiba como personalizar a tarefa inscrever-se no serviço de backup online da Microsoft.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: a7eafbb3-7728-487e-b287-90bbd6fee7f0
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 3c34e948da79d5b6a21b24da575d8b5b23022d96
ms.sourcegitcommit: e00e789dff216dbade861e61365f078b758a5720
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97755102"
---
# <a name="customize-sign-up-for-microsoft-online-backup-service-task"></a>Personalizar Inscrição para a tarefa do Microsoft Azure Online Backup

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Por padrão, a tarefa **Inscrever-se para o Serviço de Backup Online da Microsoft** na guia **DISPOSITIVOS** do Dashboard abra no site Microsoft Online Backup Service. O site fornece informações sobre o serviço e ajuda-o a inscrever-se para o serviço e baixar o software necessário.

 Você pode personalizar a tarefa **Inscrever-se para o Serviço de Backup Online da Microsoft** de duas maneiras:

-   Você pode substituir o URL padrão do site padrão por um URL que represente a experiência do usuário personalizada. Para substituir a URL padrão, abra o Editor de Registro, crie a chave de registro: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\LinkUrl**, e então atribua o URL personalizado como o valor para a chave.

-   Você pode ocultar a tarefa: Para ocultar a tarefa, abra o Editor do Registro e crie a chave de registro: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OnlineBackup\OnlineBackupInstalled**.

## <a name="see-also"></a>Consulte Também
 [Criando e personalizando a imagem](Creating-and-Customizing-the-Image.md) [personalizações adicionais](Additional-Customizations.md) [preparando a imagem para](Preparing-the-Image-for-Deployment.md) [testar a implantação da experiência do cliente](Testing-the-Customer-Experience.md)