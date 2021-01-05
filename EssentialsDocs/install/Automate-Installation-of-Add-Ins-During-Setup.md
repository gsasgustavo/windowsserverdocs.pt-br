---
title: Automatizar a instalação de suplementos durante a configuração
description: Saiba como usar o método postal. cmd para instalar suplementos automaticamente durante a instalação do Windows Server Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 2e6ff6e4-8d68-4d49-9e38-8088bc8bf95e
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 0982cfc5064167044466a82ee44a575717596e2a
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711481"
---
# <a name="automate-installation-of-add-ins-during-setup"></a>Automatizar a instalação de suplementos durante a configuração

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="automate-installing-add-ins-during-setup"></a><a name="BKMK_AddIns"></a> Automatizar a instalação de suplementos durante a instalação
 Para instalar suplementos durante a instalação, use o método PostIC.cmd descrito na seção [Criar o arquivo PostIC.cmd para executar tarefas de configuração pós-início](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) deste documento.

 Adicione a seguinte entrada ao PostIC.cmd:

```
C:\Program Files\Windows Server\bin\Installaddin.exe <full path to wssx file> -q
```

 O suplemento agora tem suporte para pré-instalação e etapas de desinstalação personalizadas.

 A etapa de pré-instalação é executada antes de instalar todos os arquivos **.msi** especificados em addin.xml. Ao executar no modo interativo, o diálogo de progresso será mostrado, mas sem alterar o progresso. O botão de cancelamento é desativado durante a fase de pré-instalação. Para implantar uma etapa de pré-instalação, adicione os seguintes conteúdos em addin.xml (diretamente sob Pacote):

> [!NOTE]
>  O esquema xml precisa seguir exatamente o seguinte:

```
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <Id>...</Id>
  <Version>...</Version>
  <Name>...</Name>
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>
  <ServerBinary>...</ServerBinary>
  <ClientBinary32>...</ClientBinary32>
  <ClientBinary64>...</ClientBinary64>
  <SupportedSkus>...</SupportUrl>
  <SupportUrl>...</SupportUrl>
  <Location>...</Location>
  <PrivacyStatement>...</PrivacyStatement>
  <OtherBinaries>...</OtherBinaries>
  <Preinstall>
<Executable>exefile</Executable>
<NormalArgs>args-for-interactive-mode</NormalArgs>
<SilentArgs>args-for-silent-mode</SilentArgs>
<IgnoreExitCode>true</IgnoreExitCode>
  </Preinstall>
  <UninstallConfirm>...</UninstallConfirm>
</Package>
<¦>
<¦>
```

 Em que **exefile** é o arquivo executável no pacote de suplemento para realizar a etapa de pré-instalação e deve ser especificado. **NormalArgs** especifica argumentos a serem enviados ao exefile na linha de comando quando o modo interativo é usado. Nesse modo, o exefile pode abrir alguns diálogos em pop-up para interação com o usuário. **SilentArgs** especifica argumentos a serem enviados ao exefile na linha de comando quando o modo silencioso é usado (-q é especificado ao chamar installaddin.exe). O exefile não deve abrir nenhuma janela em pop-up nesse modo. Se **IgnoreExitCode** for especificado como verdadeiro, a etapa de pré-instalação é sempre considerada bem-sucedida, caso contrário, o código de saída 0 indica sucesso, 1 indica cancelamento e outros valores indicam falha. As marcas **NormalArgs**, **SilentArgs** e **IgnoreExitCode** são todas opcionais.

 Uma etapa de desinstalação personalizada pode ser usada para qualquer um dos seguintes:

- Substituir o diálogo de confirmação interno.

- Preencher os diálogos personalizados antes da desinstalação.

- Realizar certas tarefas antes da desinstalação.

  Para implantar uma etapa de desinstalação, adicione os seguintes conteúdos em addin.xml (diretamente sob Pacote):

```
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <Id>...</Id>
  <Version>...</Version>
  <Name>...</Name>
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>
  <ServerBinary>...</ServerBinary>
  <ClientBinary32>...</ClientBinary32>
  <ClientBinary64>...</ClientBinary64>
  <SupportedSkus>...</SupportUrl>
  <SupportUrl>...</SupportUrl>
  <Location>...</Location>
  <PrivacyStatement>...</PrivacyStatement>
  <OtherBinaries>...</OtherBinaries>
  <Preinstall>¦</Preinstall>
<UninstallConfirm>
<Executable>full-path-to-exefile</Executable>
<Arguments>command-line-arguments</Arguments>
</UninstallConfirm>
</Package>
```

 Em que **full-path-to-exefile** especifica o exefile já instalado no sistema. **Arguments** é opcional, ele especifica os argumentos da linha de comando para o exefile. O exefile é chamado antes de a caixa de diálogo interna de confirmação de desinstalação ser exibida.

 Nesta fase, o exefile pode executar as seguintes tarefas:

- Abrir em pop-up alguns diálogos para interação com o usuário.

- Realizar algumas tarefas em segundo plano.

  O código de saída deste arquivo exe determina como o processo de desinstalação avança:

- 0: o processo de desinstalação continua sem preencher o diálogo de confirmação interno, da mesma forma que se o usuário já tivesse confirmado. (essa abordagem pode ser usada para substituir o diálogo de confirmação interno);

- 1: o processo de desinstalação é cancelado e, por fim, uma mensagem de cancelamento será mostrada ao usuário. Tudo permanece inalterado;

- Outro: o processo de desinstalação continua com o diálogo de confirmação interno, como se a etapa de desinstalação personalizada não estivesse presente.

  Qualquer falha em chamar o exefile levará ao mesmo comportamento que se o exefile retornasse um código que não 0 ou 1.

## <a name="see-also"></a>Consulte Também
 [Criando e personalizando a imagem](Creating-and-Customizing-the-Image.md) [personalizações adicionais](Additional-Customizations.md) [preparando a imagem para](Preparing-the-Image-for-Deployment.md) [testar a implantação da experiência do cliente](Testing-the-Customer-Experience.md)