---
description: 'Saiba mais sobre: pré-requisitos para hosts protegidos'
title: Pré-requisitos de host protegido
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 6f6a4e111e5622ab0a78041e4e94c76f0a8acb13
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049774"
---
# <a name="prerequisites-for-guarded-hosts"></a>Pré-requisitos para hosts protegidos

>Aplica-se a: Windows Server 2019, Windows Server (canal semestral), Windows Server 2016

Examine os pré-requisitos do host para o modo de atestado escolhido e clique na próxima etapa para adicionar hosts protegidos.

## <a name="tpm-trusted-attestation"></a>TPM-atestado confiável

Os hosts protegidos que usam o modo TPM devem atender aos seguintes pré-requisitos:

-   **Hardware**: um host é necessário para a implantação inicial. Para testar a migração dinâmica do Hyper-V para VMs blindadas, você deve ter pelo menos dois hosts.

    Os hosts devem ter:

    - IOMMU e conversão de endereços de segundo nível (SLAT)
    - TPM 2.0
    - UEFI 2.3.1 ou posterior
    - Configurado para inicialização usando UEFI (não BIOS ou modo "herdado")
    - Inicialização segura habilitada

-   **Sistema operacional**: Windows Server 2016 Datacenter Edition ou posterior

    > [!IMPORTANT]
    > Certifique-se de instalar a [atualização cumulativa mais recente](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history).

-   **Função e recursos**: função Hyper-v e o recurso de suporte do Hyper-v do guardião de host. O recurso de suporte do Hyper-V do guardião de host está disponível somente nas edições do datacenter do Windows Server.

> [!WARNING]
> O recurso de suporte do Hyper-V do guardião de host permite a proteção baseada em virtualização de integridade de código que pode ser incompatível com alguns dispositivos.
> É altamente recomendável testar essa configuração em seu laboratório antes de habilitar esse recurso.
> Deixar de fazer isso pode resultar em falhas inesperadas, inclusive perda de dados ou um erro de tela azul (também chamado de erro de parada).
> Para obter mais informações, consulte [hardware compatível com a proteção baseada em virtualização do Windows Server de integridade de código](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md).

**Próxima etapa:**
> [!div class="nextstepaction"]
> [Capturar informações do TPM](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)

## <a name="host-key-attestation"></a>Atestado de chave de host

Os hosts protegidos que usam o atestado de chave de host devem atender aos seguintes pré-requisitos:

- **Hardware**: qualquer servidor capaz de executar o Hyper-V começando com o Windows Server 2019
- **Sistema operacional**: Windows Server 2019 Datacenter Edition
- **Função e recursos**: função Hyper-v e o recurso de suporte do Hyper-v do guardião de host

O host pode ser Unido a um domínio ou a um grupo de trabalho.

Para o atestado de chave de host, o HGS deve estar executando o Windows Server 2019 e operando com o atestado v2. Para obter mais informações, consulte [pré-requisitos do HgS](guarded-fabric-prepare-for-hgs.md#prerequisites).

**Próxima etapa:**
> [!div class="nextstepaction"]
> [Criar um par de chaves](guarded-fabric-create-host-key.md)

## <a name="admin-trusted-attestation"></a>Administrador-atestado confiável

>[!IMPORTANT]
>O atestado confiável de administrador (modo de anúncio) é preterido a partir do Windows Server 2019. Para ambientes em que o atestado do TPM não é possível, configure o [atestado de chave do host](#host-key-attestation). O atestado de chave de host fornece garantia semelhante ao modo AD e é mais simples de configurar.

Os hosts do Hyper-V devem atender aos seguintes pré-requisitos para o modo AD:

-   **Hardware**: qualquer servidor capaz de executar o Hyper-V começando com o Windows Server 2016. Um host é necessário para a implantação inicial. Para testar a migração dinâmica do Hyper-V para VMs blindadas, você precisa de pelo menos dois hosts.

-   **Sistema operacional**: Windows Server 2016 Datacenter Edition

    > [!IMPORTANT]
    > Instale a [atualização cumulativa mais recente](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history).

-   **Função e recursos**: função Hyper-v e o recurso de suporte do Hyper-v do guardião de host, que está disponível somente no Windows Server 2016 Datacenter Edition.

> [!WARNING]
> O recurso de suporte do Hyper-V do guardião de host permite a proteção baseada em virtualização de integridade de código que pode ser incompatível com alguns dispositivos.
> É altamente recomendável testar essa configuração em seu laboratório antes de habilitar esse recurso.
> Deixar de fazer isso pode resultar em falhas inesperadas, inclusive perda de dados ou um erro de tela azul (também chamado de erro de parada).
> Para obter mais informações, consulte [hardware compatível com a proteção baseada em virtualização do Windows Server 2016 de integridade de código](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md).

**Próxima etapa:**
> [!div class="nextstepaction"]
> [Posicionar hosts protegidos em um grupo de segurança](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
