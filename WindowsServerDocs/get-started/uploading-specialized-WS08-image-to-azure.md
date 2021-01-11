---
title: Carregar uma imagem especializada do Windows Server 2008/2008 R2 no Azure
description: O Windows Server 2008 e 2008 R2 estão se aproximando do fim de serviço. Saiba como migrar sua carga de trabalho para o Azure hospedando o Windows Server na nuvem.
ms.mktglfcycl: manage
ms.sitesec: library
author: eross-msft
ms.author: thierryp
ms.date: 07/11/2018
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: a34aad872bf52bbca965571e20d4dd3ebb975228
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948052"
---
# <a name="upload-a-windows-server-20082008-r2-specialized-image-to-azure"></a>Carregar uma imagem especializada do Windows Server 2008/2008 R2 no Azure

![Tópico de imagem da faixa que apresenta o WS08](media/WS08-image-banner-large.png)

Agora você pode executar uma VM do Windows Server 2008/2008 R2 na nuvem com o Azure.

## <a name="prep-the-windows-server-20082008-r2-specialized-image"></a>Preparar a imagem especializada do Windows Server 2008/2008 R2
Antes de poder carregar uma imagem, faça as seguintes alterações:

- Baixe e instale o Windows Server 2008 SP2 (Service Pack 2), caso ainda não o tenha instalado na sua imagem.

- Definir configurações da RDP (Área de Trabalho Remota).
  1. Vá para o **Painel de Controle** > **Configurações do sistema**.
  2. Selecione **Configurações remotas** no menu esquerdo.

     ![Captura de tela das configurações do sistema, realçando as "Configurações remotas".](media/1a_remote_settings.png)

  3. Selecione a guia **Remoto** nas Propriedades do Sistema.

     ![Captura de tela da guia remoto nas propriedades do sistema.](media/2c_sysprops.png)

  4. Selecione Permitir conexões de computadores executando qualquer versão da Área de Trabalho Remota (menos seguro).
  5. Clique em **Aplicar** e em **OK**.
- Defina as configurações do Firewall do Windows.
   1. No prompt de comando, no modo Admin, insira "**wf.msc**" para o Firewall do Windows e as configurações de segurança avançadas.
   2. Classifique as descobertas por **Portas**, selecione a **porta 3389**.
     ![Captura de tela das regras de entrada das configurações do Firewall do WIndows.](media/3b_inboundrules.png)
   3. Habilite a Área de Trabalho Remota (TCP-IN) para os perfis: **Domínio**, **Privado** e **Público** (mostrado acima).

- Salve todas as configurações e desligue a imagem.
- Se você estiver usando o Hyper-V, o AVHD secundário deverá ser mesclado ao VHD principal para que as alterações persistam.

Um bug conhecido atual faz com que a senha do administrador na imagem carregada expire em até 24 horas. Execute as seguintes etapas para evitar esse problema:

1. Vá para **Iniciar** > **Executar**
2. Digite **lusrmgr.msc**
3. Selecione **Usuários** em Usuários e Grupos Locais
4. Clique com o botão direito do mouse em **Administrador** e selecione **Propriedades**
5. Selecione **senha nunca expira** e depois selecione **OK**
![Captura de tela das propriedades do administrador.](media/6_adminprops.png)

## <a name="uploading-the-image-vhd"></a>Como carregar o VHD da imagem
Você pode usar o script a seguir para carregar o VHD. Antes de fazer isso, você precisará publicar o arquivo de configurações da sua conta do Azure. Obter as [configurações de arquivo do Azure](https://azure.microsoft.com/downloads/).

Eis o script:

```powershell
Get-AzurePublishSettingsFile

Login-AzureRmAccount

      # Import publishsettings
      Import-AzurePublishSettingsFile -PublishSettingsFile <LocationOfPublishingFile>
      $subscriptionId = 'xxxx-xxxx-xxxx-xxxx-xxxxx'

      # Set NodeFlight subscription as default subscription
      Select-AzureRmSubscription -SubscriptionId $subscriptionId
      Set-AzureRmContext -SubscriptionId $subscriptionId
      $rgName = "<resourcegroupname>"

      $urlOfUploadedImageVhd = "<BlobUrl>/<NameForVHD>.vhd"
      Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd -LocalFilePath "<FilePath>"
```
## <a name="deploy-the-image-in-azure"></a>Implantar a imagem no Azure
Nesta seção, você implantará o VHD da imagem no Azure.

> [!IMPORTANT]
> Não use imagens de usuário predefinidas no Azure.

1.    Crie um novo [grupo de recursos](/rest/api/resources/resourcegroups/createorupdate).
2.    Crie um novo [blob de armazenamento](/rest/api/storageservices/put-blob) dentro do grupo de recursos.
3.    Crie um [contêiner](/rest/api/storageservices/create-container) dentro do blob de armazenamento.
4.    Copie a URL do armazenamento de blobs das propriedades.
5.    Use o script fornecido acima para carregar sua imagem para o novo blob de armazenamento.
6.    Crie um [disco](/azure/virtual-machines/windows/prepare-for-upload-vhd-image) para o seu VHD.
     a.    Vá para Discos e clique em **Adicionar**.
     b.    Insira um nome para o disco. Selecione a assinatura que deseja usar, defina a região e escolha o tipo de conta.
     c. Para Tipo de Fonte, selecione armazenamento. Navegue até o local do VHD do blob criado usando o script.
     d. Selecione o tipo de sistema operacional Windows e o Tamanho (padrão: 1023).
     e. Clique em **Criar**.

7.    Vá para o Disco Criado e clique em **Criar VM**.
     a.    Dê um nome à VM.
     b.    Selecione o grupo criado na etapa 5, onde você carregou o disco.
     c.    Escolha um tamanho e um plano de SKU para sua VM.
     d.    Selecione um adaptador de rede na página de configurações. Verifique se o adaptador de rede tem a seguinte regra especificada:

        PORTA: 3389 Protocolo: TCP Ação: Permitir Prioridade: 1000 Nome: 'RDP-Rule'.
     e.    Clique em **Criar**.
