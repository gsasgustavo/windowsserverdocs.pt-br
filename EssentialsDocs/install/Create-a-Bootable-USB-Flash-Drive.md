---
title: Criar uma Unidade Flash USB Inicializável
description: Saiba como criar uma unidade flash USB inicializável para usar para implantar o Windows Server Essentials.
ms.date: 05/04/2018
ms.topic: article
ms.assetid: 2fe8e35c-69f9-40b3-a270-22e2402510d8
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: e4b1388913106273397a5ade45e3f8f1aa9b38d4
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711441"
---
# <a name="create-a-bootable-usb-flash-drive"></a>Criar uma Unidade Flash USB Inicializável

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Você pode criar uma unidade flash USB inicializável para usar para implantar o Windows Server Essentials. A primeira etapa é preparar a unidade flash USB usando DiskPart, um utilitário de linha de comando. Para obter informações sobre o DiskPart, consulte [Usando opções de linha de comando de DiskPart](https://go.microsoft.com/fwlink/?LinkId=207073).


> [!TIP]
> Para criar uma unidade flash USB inicializável para uso na recuperação ou reinstalação do Windows em um PC, em vez de em um servidor, consulte [criar uma unidade de recuperação](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive).

 Para outros cenários em que convenham criar ou usar uma unidade unidade flash USB inicializável, consulte os seguintes tópicos:

-   [Restaurar um sistema completo de um backup de computador cliente existente](../manage/restore-a-full-system-from-an-existing-client-computer-backup.md)

-   [Restaurar ou reparar o servidor que executa o Windows Server Essentials](../manage/restore-or-repair-your-server-running-windows-server-essentials.md)


### <a name="to-create-a-bootable-usb-flash-drive"></a>Para criar uma unidade flash USB inicializável

1.  Insira uma unidade flash USB em um computador em execução.

2.  Abra uma janela de Prompt de comando como administrador.

3.  Digite `diskpart`.

4.  Na nova linha de comando aberta, para determinar o número da unidade flash USB ou a letra da unidade, digite `list disk`, e clique em ENTER. O comando `list disk` exibe todos os discos no computador. Observe o número da unidade ou a letra da unidade flash USB.

5.  No prompt de comando, digite `select disk <X>`, em que X é o número da unidade ou a letra da unidade flash USB, e clique em ENTER.

6.  Digite `clean`e clique em ENTER. Esse comando exclui todos os dados da unidade flash USB.

7.  Para criar uma nova partição primária na unidade flash USB, digite `create partition primary`e clique em ENTER.

8.  Para selecionar a partição recém-criada, digite `select partition 1`e clique em ENTER.

9. Para formatar a partição, digite `format fs=ntfs quick`e clique em ENTER.

    > [!IMPORTANT]
    >  Se a sua plataforma de servidor tiver suporte para UEFI (Unified Extensible Firmware Interface), você deve formatar a unidade flash USB como FAT32 em vez de NTFS. Para formatar a partição como FAT32, digite `format fs=fat32 quick`e clique em ENTER.

10. Digite `active`e clique em ENTER.

11. Digite `exit`e clique em ENTER.

12. Quando terminar de preparar sua imagem personalizada, salve-a na raiz da unidade flash USB.

## <a name="see-also"></a>Consulte Também

 [Introdução com o Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) [criando e personalizando a imagem](Creating-and-Customizing-the-Image.md) [personalizações adicionais](Additional-Customizations.md) [preparando a imagem para](Preparing-the-Image-for-Deployment.md) [testar a implantação da experiência do cliente](Testing-the-Customer-Experience.md)

 [Como podemos ajudá-lo?](https://windows.microsoft.com/windows/support)
