---
title: Comandos do Windows PowerShell para RSS e vRSS
description: Neste tópico, você aprenderá a localizar rapidamente informações de referência técnica sobre os comandos do Windows PowerShell para RSS (recepção lateral) e o vRSS (RSS virtual).
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/05/2018
ms.openlocfilehash: a5cc6d3b95b842e806c9f2c9a5762e5f29ce4c7b
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96863965"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>Comandos do Windows PowerShell para RSS e vRSS

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Neste tópico, você aprenderá a localizar rapidamente informações de referência técnica sobre os comandos do Windows PowerShell para receber o RSS de escala lateral e o RSS \( \) virtual \( vRSS \) .

Use os comandos RSS a seguir para configurar o RSS em um computador físico com vários processadores ou vários núcleos. Você pode usar os mesmos comandos para configurar o vRSS em uma VM de máquina virtual \( \) que esteja executando um sistema operacional com suporte. Para obter mais informações, consulte [cmdlets do adaptador de rede no Windows PowerShell](/powershell/module/netadapter/).

## <a name="configure-vmq"></a>Configurar a VMQ

o vRSS requer que a VMQ esteja habilitada e configurada. Você pode usar os seguintes comandos do Windows PowerShell para gerenciar as configurações de VMQ.

- [Desabilitar-NetAdapterVmq](/powershell/module/netadapter/disable-netadaptervmq)
- [Habilitar-NetAdapterVmq](/powershell/module/netadapter/enable-netadaptervmq)
- [Get-NetAdapterVmq](/powershell/module/netadapter/get-netadaptervmq)
- [Set-NetAdapterVmq](/powershell/module/netadapter/set-netadaptervmq)

## <a name="enable-and-configure-rss-on-a-native-host"></a>Habilitar e configurar o RSS em um host nativo

Use os comandos do PowerShell a seguir para configurar o RSS em um host nativo, bem como gerenciar o RSS em uma VM ou em uma NIC virtual do host (vNIC). Alguns dos parâmetros desses comandos também podem afetar Fila de Máquina Virtual \( VMQ \) no host Hyper-V.

>[!IMPORTANT]
>Habilitar o RSS em uma VM ou em um host vNIC é um pré-requisito para habilitar e usar o vRSS.

- [Desabilitar-NetAdapterRss](/powershell/module/netadapter/disable-netadapterrss)
- [Habilitar-NetAdapterRss](/powershell/module/netadapter/enable-netadapterrss)
- [Get-NetAdapterRss](/powershell/module/netadapter/get-netadapterrss)
- [Set-NetAdapterRss](/powershell/module/netadapter/Set-NetAdapterRss)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>Habilitar o vRSS na \- porta do comutador virtual Hyper-V

Além de habilitar o RSS na VM, o vRSS exige que você habilite o vRSS na \- porta do comutador virtual Hyper-V.

Determine as configurações atuais para vRSS e habilite ou desabilite o recurso para uma VM.

   **Exibir as configurações atuais:**

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **Habilitado o recurso:**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## <a name="enable-or-disable-vrss-on-a-host-vnic"></a>Habilitar ou desabilitar o vRSS em um host vNIC

Determine as configurações atuais para vRSS e habilite ou desabilite o recurso para um host vNIC.

   **Exibir as configurações atuais:**

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **Habilitar ou desabilitar o recurso:**

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## <a name="configure-the-scheduling-mode-on-the-hyper-v-virtual-switch-port"></a>Configurar o modo de agendamento na porta do comutador virtual do Hyper-V
>Aplica-se a: Windows Server 2019

No Windows Server 2019, o vRSS pode atualizar os processadores lógicos usados para processar o tráfego de rede dinamicamente.  Os dispositivos com drivers com suporte têm esse modo de agendamento habilitado por padrão.

Determine o modo de agendamento atual em um sistema ou modifique o modo de agendamento de uma VM.

   **Exibir as configurações atuais:**

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **Definir ou modificar o modo de agendamento:**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## <a name="configure-the-scheduling-mode-on-a-host-vnic"></a>Configurar o modo de agendamento em um host vNIC
>Aplica-se a: Windows Server 2019

Para determinar o modo de agendamento atual ou para modificar o modo de agendamento de um host vNIC, use os seguintes comandos do Windows PowerShell:

   **Exibir as configurações atuais:**

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **Definir ou modificar o modo de agendamento:**

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>Tópicos relacionados
Para obter mais informações, consulte os tópicos de referência a seguir.

- [Get-VMNetworkAdapter](/powershell/module/hyper-v/get-vmnetworkadapter)
- [Set-VMNetworkAdapter](/powershell/module/hyper-v/set-vmnetworkadapter)

Para obter mais informações, consulte [vRSS (recepção virtual)](vrss-top.md).
