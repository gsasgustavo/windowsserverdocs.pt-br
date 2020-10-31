---
title: Atualizações de Componentes do Active Directory Domain Services
description: Este documento discute as atualizações de componente AD DS para o Windows Server 2012 R2
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 09/08/2017
ms.topic: article
ms.assetid: a3a91034-a4da-4ad7-93f8-0cd2ec3e7824
ms.openlocfilehash: a5ed47dae3cab9c026656fcccedae30a42325681
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93069798"
---
# <a name="active-directory-domain-services-component-updates"></a>Atualizações de Componentes do Active Directory Domain Services

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2

Este módulo apresenta os componentes que receberam atualizações secundárias nos Serviços de Diretório e Espaços de Identidade.


| Sobre o autor |
|------------------|
|   **Autor:**    |
|     **Biografia:**     |
| **Colaboradores** |
|  **Revisores**   |

> [!NOTE]
> Este documento foi criado por um engenheiro de atendimento ao cliente da Microsoft e é destinado a administradores e arquitetos de sistemas experientes que procuram explicações técnicas mais profundas para recursos e soluções no Windows Server 2012 R2 do que aquelas geralmente oferecidas em tópicos do TechNet. No entanto, ele não passou pelas mesmas etapas de edição que eles, por isso a linguagem pode parecer que menos refinada do que a geralmente encontrada no TechNet.

### <a name="what-you-will-learn"></a>O que você aprenderá
Depois de concluir este módulo, você será capaz de:

-   Explicar as atualizações de componente feitas nas áreas dos Serviços de Diretório e Tecnologia de Identidade no Windows Server 2012 R2

    -   [Exclusividade de SPN e UPN](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)

    -   [Reinicialização automática do Winlogon Sign-On &#40;ARSO&#41;](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)

    -   [Atestado de chave de TPM](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)

    -   [Cmdlets do Windows PowerShell de backup e restauração de AC](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)

    -   [Auditoria de processo de linha de comando](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)

    -   [Proteção e gerenciamento de credenciais](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn408190(v=ws.11))

    -   [Atualizações de componentes dos Serviços de Diretório](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md)

        -   [Níveis funcionais de domínio e de floresta](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)

        -   [NTFRS preterido](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)

        -   [Alterações do otimizador de consultas LDAP](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)

        -   [Melhorias no evento 1644](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)

        -   [Melhoria da taxa de transferência de replicação do Active Directory](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)
