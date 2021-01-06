---
title: Cmdlets para configurar dispositivos de memória persistente para VMs do Hyper-V
description: Como configurar dispositivos de memória persistente para VMs do Hyper-V
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc08039ba1d
ms.author: benarm
author: BenjaminArmstrong
ms.date: 12/08/2020
ms.openlocfilehash: 087ba6e04efa3055d7f430fbcc49402df9de11fc
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97941352"
---
# <a name="cmdlets-for-configuring-persistent-memory-devices-for-hyper-v-vms"></a>Cmdlets para configurar dispositivos de memória persistente para VMs do Hyper-V

>Aplica-se a: Windows Server 2019

Este artigo fornece aos administradores de sistema e profissionais de ti informações sobre a configuração de VMs do Hyper-V com memória persistente (também conhecido como memória de classe de armazenamento ou NVDIMM). NVDIMM em conformidade com JDEC-N dispositivos de memória persistente têm suporte no Windows Server 2016 e no Windows 10 e fornecem acesso em nível de byte a dispositivos não voláteis de latência muito baixa. Os dispositivos de memória persistente da VM têm suporte no Windows Server 2019.

## <a name="create-a-persistent-memory-device-for-a-vm"></a>Criar um dispositivo de memória persistente para uma VM

Use o cmdlet **[New-VHD](/powershell/module/hyper-v/new-vhd)** para criar um dispositivo de memória persistente para uma VM. O dispositivo deve ser criado em um volume DAX NTFS existente.  A nova extensão de nome de arquivo (. vhdpmem) é usada para especificar que o dispositivo é um dispositivo de memória persistente. Somente o formato de arquivo VHD fixo tem suporte.

**Exemplo:** `New-VHD d:\VMPMEMDevice1.vhdpmem -Fixed -SizeBytes 4GB`

## <a name="create-a-vm-with-a-persistent-memory-controller"></a>Criar uma VM com um controlador de memória persistente

Use o **cmdlet New-VM** para criar uma VM de geração 2 com o tamanho e o caminho de memória especificados para uma imagem VHDX. Em seguida, use **Add-VMPmemController** para adicionar um controlador de memória persistente a uma VM.

**Exemplo:**

```powershell
New-VM -Name "ProductionVM1" -MemoryStartupBytes 1GB -VHDPath c:\vhd\BaseImage.vhdx

Add-VMPmemController ProductionVM1x
```

## <a name="attach-a-persistent-memory-device-to-a-vm"></a>Anexar um dispositivo de memória persistente a uma VM

Use **[Add-VMHardDiskDrive](/powershell/module/hyper-v/add-vmharddiskdrive)** para anexar um dispositivo de memória persistente a uma VM

**Exemplo:** `Add-VMHardDiskDrive ProductionVM1 PMEM -ControllerLocation 1 -Path D:\VPMEMDevice1.vhdpmem`

Dispositivos de memória persistentes em uma VM Hyper-V aparecem como um dispositivo de memória persistente a ser consumido e gerenciado pelo sistema operacional convidado. Os sistemas operacionais convidados podem usar o dispositivo como um volume do bloco ou DAX. Quando dispositivos de memória persistentes em uma VM são usados como um volume DAX, eles se beneficiam da capacidade de endereço de nível de byte de baixa latência do dispositivo de host (sem virtualização de e/s no caminho de código).

>[!NOTE]
>Há suporte para a memória persistente apenas para VMs Gen2 do Hyper-V. A migração de Migração ao Vivo e armazenamento não tem suporte para VMs com memória persistente. Os pontos de verificação de produção das VMs não incluem o estado de memória persistente.
