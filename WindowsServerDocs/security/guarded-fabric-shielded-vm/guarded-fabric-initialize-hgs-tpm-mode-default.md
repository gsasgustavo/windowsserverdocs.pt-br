---
title: Inicializar o cluster HGS usando o modo TPM em uma nova floresta dedicada (padrão)
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 2a89ffb238b631fc24035f2b18a57c614003c644
ms.sourcegitcommit: 8c0a419ae5483159548eb0bc159f4b774d4c3d85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235823"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-a-new-dedicated-forest-default"></a>Inicializar o cluster HGS usando o modo TPM em uma nova floresta dedicada (padrão)

> Aplica-se a: Windows Server 2019, Windows Server (canal semestral), Windows Server 2016

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  Execute [Initialize-HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/initialize-hgsserver) em uma janela do PowerShell com privilégios elevados no primeiro nó HgS. A sintaxe desse cmdlet dá suporte a várias entradas diferentes, mas as duas invocações mais comuns estão abaixo:

    -   Se você estiver usando arquivos PFX para seus certificados de assinatura e criptografia, execute os seguintes comandos:

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
        ```

    -   Se você estiver usando certificados não exportáveis instalados no repositório de certificados local, execute o comando a seguir. Se você não souber as impressões digitais de seus certificados, poderá listar os certificados disponíveis executando `Get-ChildItem Cert:\LocalMachine\My` .

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' -TrustTpm
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>Próxima etapa

> [!div class="nextstepaction"]
> [Instalar certificados de raiz do TPM](guarded-fabric-install-trusted-tpm-root-certificates.md)
