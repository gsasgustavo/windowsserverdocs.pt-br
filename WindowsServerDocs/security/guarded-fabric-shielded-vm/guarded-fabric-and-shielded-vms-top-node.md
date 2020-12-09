---
title: Malha protegida e VMs blindadas
ms.topic: article
ms.assetid: 5c7ada81-2d97-41d4-87cf-1a7ccf06cd20
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 001e0fe38c27e6331a5b2b38d76cd193bfb184f1
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96864841"
---
# <a name="guarded-fabric-and-shielded-vms"></a>Malha protegida e VMs blindadas

>Aplica-se a: Windows Server 2019, Windows Server (canal semestral), Windows Server 2016

Uma das metas mais importantes de fornecer um ambiente hospedado é garantir a segurança das máquinas virtuais em execução no ambiente. Como um provedor de serviços de nuvem ou um administrador de nuvem privada corporativa, você pode usar uma malha protegida para fornecer um ambiente mais seguro para as VMs. Uma malha protegida consiste em um HGS (Serviço de Guardião de Host), em geral, um cluster de três nós, além de um ou mais hosts protegidos e um conjunto de VMs (máquinas virtuais) protegidas.

> [!IMPORTANT]
> Verifique se você instalou a atualização cumulativa mais recente antes de implantar máquinas virtuais blindadas em produção.

## <a name="videos-blog-and-overview-topic-about-guarded-fabrics-and-shielded-vms"></a>Tópicos de vídeos, blog e visão geral sobre malhas protegidas e VMs blindadas

- Vídeo: [como proteger sua malha de virtualização contra ameaças internas com o Windows Server 2019](https://myignite.techcommunity.microsoft.com/sessions/64690)
- Vídeo: [introdução às máquinas virtuais blindadas no Windows Server 2016](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- Vídeo: [Aprofunde-se em VMs blindadas com o Windows Server 2016 Hyper-V](https://channel9.msdn.com/events/Ignite/2016/BRK3124)
- Vídeo: [implantando VMs blindadas e uma malha protegida com o Windows Server 2016](https://mva.microsoft.com/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)
- Blog: [blog de datacenter e segurança de nuvem privada](/archive/blogs/datacentersecurity/)
- Visão geral: [visão geral de malha protegida e VMs blindadas](Guarded-Fabric-and-Shielded-VMs.md)

## <a name="planning-topics"></a>Tópicos de planejamento

- [Guia de planejamento para hosters](guarded-fabric-planning-for-hosters.md)
- [Guia de planejamento para locatários](guarded-fabric-shielded-vm-planning-for-tenants.md)

## <a name="deployment-topics"></a>Tópicos de implantação

- [Guia de Implantação](guarded-fabric-deploying-hgs-overview.md)
    - [Início rápido](guarded-fabric-deployment-overview.md)
    - [Implantar o HGS](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)
    - [Implantar hosts protegidos](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
        - [Configurando a malha DNS para hosts que se tornarão hosts protegidos](guarded-fabric-configuring-fabric-dns.md)
        - [Implantar um host protegido usando o modo AD](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
        - [Implantar um host protegido usando o modo TPM](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)
        - [Confirmar que os hosts protegidos podem atestar](guarded-fabric-confirm-hosts-can-attest-successfully.md)
        - [VMs blindadas – provedor de serviços de hospedagem implanta hosts protegidos no VMM](/system-center/vmm/guarded-deploy-host)
    - [Implantar VMs blindadas](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
        - [Criar um modelo de VM blindado](guarded-fabric-create-a-shielded-vm-template.md)
        - [Preparar um VHD do auxiliar de blindagem de VM](guarded-fabric-vm-shielding-helper-vhd.md)
        - [Instalar o Microsoft Azure Pack](guarded-fabric-hoster-sets-up-windows-azure-pack.md)
        - [Criar um arquivo de dados de blindagem](guarded-fabric-tenant-creates-shielding-data.md)
        - [Implantar uma VM blindada usando o Pacote do Microsoft Azure](guarded-fabric-shielded-vm-windows-azure-pack.md)
        - [Implantar uma VM blindada usando o Virtual Machine Manager](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="operations-and-management-topic"></a>Tópico de operações e gerenciamento

- [Gerenciando o serviço guardião de host](guarded-fabric-manage-hgs.md)
