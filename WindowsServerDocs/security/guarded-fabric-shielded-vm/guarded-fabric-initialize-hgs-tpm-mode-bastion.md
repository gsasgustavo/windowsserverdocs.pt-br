---
description: 'Saiba mais sobre: inicializar o cluster HGS usando o modo TPM em uma floresta de bastiões existente'
title: Inicializar o cluster HGS usando o modo TPM em uma floresta de bastiões
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: de96fa3a0ad8ce4b76bd4b3c0d484bc448906ae6
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049744"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-an-existing-bastion-forest"></a>Inicializar o cluster HGS usando o modo TPM em uma floresta de bastiões existente

>Aplica-se a: Windows Server 2019, Windows Server (canal semestral), Windows Server 2016

Active Directory Domain Services será instalado no computador, mas deverá permanecer não configurado.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

Antes de continuar, verifique se você pré-testeu os objetos de cluster para o serviço guardião de host e concedeu ao usuário conectado **controle total** sobre os objetos VCO e CNO no Active Directory.
O nome do objeto de computador virtual precisa ser passado para o `-HgsServiceName` parâmetro e o nome do cluster para o `-ClusterName` parâmetro.

> [!TIP]
> Verifique novamente os controladores de domínio do AD para garantir que seus objetos de cluster tenham sido replicados para todos os DCs antes de continuar.

Se você estiver usando certificados baseados em PFX, execute os seguintes comandos no servidor HGS:

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
```

Se você estiver usando certificados instalados no computador local (como certificados com suporte do HSM e certificados não exportáveis), use os `-SigningCertificateThumbprint` `-EncryptionCertificateThumbprint` parâmetros e em vez disso.

## <a name="next-step"></a>Próxima etapa

> [!div class="nextstepaction"]
> [Instalar certificados de raiz do TPM](guarded-fabric-install-trusted-tpm-root-certificates.md)
