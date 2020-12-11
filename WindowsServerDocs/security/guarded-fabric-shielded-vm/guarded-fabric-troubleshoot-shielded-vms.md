---
description: 'Saiba mais sobre: solucionar problemas de VMs blindadas'
title: Solucionar problemas de VMs blindadas
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 10/3/2018
ms.openlocfilehash: 3f4c0eb81169f9b66170d3332d220233d476ba5f
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049204"
---
# <a name="troubleshoot-shielded-vms"></a>Solucionar problemas de VMs blindadas

>Aplica-se a: Windows Server 2019, Windows Server (canal semestral), Windows Server 2016

A partir do Windows Server versão 1803, o modo de sessão avançada de conexão de máquina virtual (VMConnect) e o PS Direct são habilitados novamente para VMs totalmente blindadas. O administrador de virtualização ainda requer credenciais de convidado de VM para obter acesso à VM, mas isso torna mais fácil para um hoster solucionar problemas de uma VM blindada quando sua configuração de rede é interrompida.

Para habilitar o VMConnect e o PS Direct para suas VMs blindadas, basta movê-las para um host Hyper-V que executa o Windows Server versão 1803 ou posterior. Os dispositivos virtuais que permitem esses recursos serão habilitados novamente automaticamente. Se uma VM blindada for movida para um host que executa o e a versão anterior do Windows Server, o VMConnect e o PS Direct serão desabilitados novamente.

Para clientes sensíveis à segurança que se preocupam se os hosters têm qualquer acesso à VM e desejam retornar ao comportamento original, os seguintes recursos devem ser desabilitados no sistema operacional convidado:

- Desabilite o serviço direto do PowerShell na VM:

  ```powershell
  Stop-Service vmicvmsession
  Set-Service vmicvmsession -StartupType Disabled
  ```

- O modo de sessão avançada do VMConnect só poderá ser desabilitado se o SO convidado for pelo menos o Windows Server 2019 ou Windows 10, versão 1809. Adicione a seguinte chave do registro em sua VM para desabilitar as conexões de console de sessão avançada do VMConnect:

  ```
  reg add "HKLM\Software\Microsoft\Virtual Machine\Guest" /v DisableEnhancedSessionConsoleConnection /t REG_DWORD /d 1
  ```
