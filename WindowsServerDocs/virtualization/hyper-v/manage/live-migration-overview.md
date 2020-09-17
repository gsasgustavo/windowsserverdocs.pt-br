---
title: Visão geral de migração ao vivo
description: Fornece visão geral da funcionalidade de migração dinâmica no Windows Server 2016.
ms.topic: article
ms.assetid: 5cc875ab-05c4-439e-b27d-6bfc77054660
ms.author: benarm
author: BenjaminArmstrong
ms.date: 06/27/2017
ms.openlocfilehash: 46768ced2b493ff68df945739fb0b3f920846c7d
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746611"
---
# <a name="live-migration-overview"></a>Visão geral de migração ao vivo

A migração ao vivo é um recurso do Hyper-V no Windows Server.  Ele permite mover de forma transparente as máquinas virtuais em execução de um host Hyper-V para outro sem tempo de inatividade percebido.  O principal benefício da migração ao vivo é a flexibilidade; as máquinas virtuais em execução não estão ligadas a um único computador host.  Isso permite ações como descarregar um host específico de máquinas virtuais antes de descomissionar ou atualizá-la.  Quando emparelhado com o clustering de failover do Windows, a migração ao vivo permite a criação de sistemas altamente disponíveis e tolerantes a falhas.

## <a name="related-technologies-and-documentation"></a>Tecnologias e documentação relacionadas

A migração dinâmica é geralmente usada em conjunto com algumas tecnologias relacionadas, como clustering de failover e System Center Virtual Machine Manager.  Se você estiver usando Migração ao Vivo por meio dessas tecnologias, aqui estão os ponteiros para a documentação mais recente:
* [Clustering de failover](../../../failover-clustering/failover-clustering-overview.md) (Windows Server 2016)
* [System Center Virtual Machine Manager](/system-center/vmm/) (System Center 2016)

Se você estiver usando versões mais antigas do Windows Server ou precisar de detalhes sobre os recursos introduzidos em versões anteriores do Windows Server, aqui estão os ponteiros para a documentação histórica:
* [Migração ao vivo](/previous-versions/windows/it-pro/microsoft-hyper-v-server-2008-R2/ee815293(v=ws.10)) (Windows Server 2008 R2)
* [Migração ao vivo](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831435(v=ws.11)) (Windows Server 2012 R2)
* [Clustering de failover](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831579(v=ws.11)) (Windows Server 2012 R2)
* [Clustering de failover](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff182338(v=ws.10)) (Windows Server 2008 R2)
* [System Center Virtual Machine Manager](/previous-versions/system-center/system-center-2012-R2/gg610610(v=sc.12)) (System Center 2012 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/cc917964.aspx) (System Center 2008 R2)

## <a name="live-migration-in-windows-server-2016"></a>Migração ao Vivo no Windows Server 2016

No Windows Server 2016, há menos restrições na implantação da migração dinâmica.  Agora ele funciona sem clustering de failover.  Outras funcionalidades permanecem inalteradas de versões anteriores do Migração ao Vivo.  Para obter mais detalhes sobre como configurar e usar a migração dinâmica sem clustering de failover:
* [Configurar hosts para migração ao vivo sem clustering de failover](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)
* [Usar a migração ao vivo sem clustering de failover para mover uma máquina virtual](use-live-migration-without-failover-clustering-to-move-a-virtual-machine.md)