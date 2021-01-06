---
title: Funções, serviços de função e recursos que não estão em contêineres do Server Core-Windows Server, versão 1803
description: Saiba mais sobre as funções e os recursos que removemos da imagem de contêiner do Server Core para o Windows Server.
ms.mktglfcycl: manage
ms.sitesec: library
author: pronichkin
ms.author: artemp
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.topic: conceptual
ms.openlocfilehash: 058a976a20e09cf46b57ec39af6c7f5b0cc30fdf
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947162"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>Funções, serviços de função e recursos que não estão em contêineres do Server Core-Windows Server, versão 1803

> Aplica-se a: Windows Server, versão 1803

No Windows Server, versão 1803, [reduzimos o tamanho geral da imagem de contêiner do Server Core para **1,58 GB**](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/). A maneira como fizemos isso é otimizando a arquitetura e removendo as coisas que você não precisa em um [contêiner do Server Core](/virtualization/windowscontainers/about/). Alguns eram coisas que não funcionavam em contêineres, alguns eram funções e recursos que ninguém está usando.

> [!IMPORTANT]
> Nós os removemos da imagem de **contêiner** do Server Core, e não do [próprio Server Core](server-core-roles-and-services.md).

Aqui está a lista completa de recursos e funções removidas da imagem de contêiner do Server Core:

<div style='font-size:9.0pt'>

<br>ADCertificateServicesRole
<br>AuthManager
<br>Bitlocker-Utilities
<br>BitLocker
<br>BITS
<br>BITSExtensions-Upload
<br>CCFFilter
<br>CertificateEnrollmentPolicyServer
<br>CertificateEnrollmentServer
<br>Certificadosservices
<br>ClientForNFS-Infrastructure
<br>Contêineres
<br>CoreFileServer
<br>DataCenterBridging-LLDP-ferramentas
<br>DataCenterBridging
<br>Dedup-Core
<br>DeviceHealthAttestationService
<br>DFSN-Server
<br>DFSR-Infrastructure-edição
<br>DirectoryServices-ADAM
<br>DirectoryServices-DomainController
<br>DiskIo-QoS
<br>EnhancedStorage
<br>FailoverCluster-AdminPak
<br>FailoverCluster-AutomationServer
<br>FailoverCluster-CmdInterface
<br>FailoverCluster-FullServer
<br>FailoverCluster-PowerShell
<br>File-Services
<br>FileServerVSSAgent
<br>FRS-Infrastructure
<br>FSRM-infraestrutura-serviços
<br>FSRM-Infrastructure
<br>HardenedFabricEncryptionTask
<br>HostGuardian
<br>HostGuardianService-Package
<br>IdentityServer-SecurityTokenService
<br>IPAMClientFeature
<br>IPAMServerFeature
<br>iSCSITargetServer-PowerShell
<br>iSCSITargetServer
<br>iSCSITargetStorageProviders
<br>iSNS_Service
<br>Licenças
<br>LightweightServer
<br>Microsoft-Hyper-V-Management-clientes
<br>Microsoft-Hyper-V-offline
<br>Microsoft-Hyper-V-online
<br>Microsoft-Hyper-V
<br>Microsoft-Windows-FCI-Client-Package
<br>Microsoft-Windows-GroupPolicy-ServerAdminTools-Update
<br>Microsoft-Windows-Subsystem-Linux
<br>MSRDC-Infrastructure
<br>MultipathIo
<br>NetworkController
<br>NetworkControllerTools
<br>NetworkDeviceEnrollmentServices
<br>NetworkLoadBalancingFullServer
<br>NetworkVirtualization
<br>OnlineRevocationServices
<br>P2P-PnrpOnly
<br>PeerDist
<br>Imprimindo-cliente-gui
<br>Printing-LPDPrintService
<br>Imprimindo-Server-Foundation-Features
<br>Imprimindo-servidor-função
<br>QWAVE
<br>RasRoutingProtocols
<br>Serviços de área de trabalho remota
<br>RemoteAccess
<br>RemoteAccessMgmtTools
<br>RemoteAccessPowerShell
<br>RemoteAccessServer
<br>ResumeKeyFilter
<br>RightsManagementServices-Role
<br>RightsManagementServices
<br>RMS-Federation
<br>SBMgr-interface do usuário
<br>ServerCore-drivers-geral-WOW64
<br>ServerCore-drivers-geral
<br>ServerForNFS-Infrastructure
<br>ServerManager-Core-RSAT-recurso-ferramentas
<br>ServerMediaFoundation
<br>ServerMigration
<br>SessionDirectory
<br>SetupAndBootEventCollection
<br>ShieldedVMToolsAdminPack
<br>SMB1Protocol-Server
<br>SmbDirect
<br>SMBHashGeneration
<br>SmbWitness
<br>SNMP
<br>SoftwareLoadBalancer
<br>Armazenamento-réplica-AdminPack
<br>Storage-Replica
<br>TPM-PSH-cmdlets
<br>UpdateServices-Database
<br>UpdateServices-Services
<br>UpdateServices-WidDatabase
<br>UpdateServices
<br>VmHostAgent
<br>VolumeActivation-função completa
<br>Aplicativo Web-proxy
<br>WebAccess
<br>Enrollservices
<br>Windows-Defender
<br>WindowsServerBackup
<br>WindowsStorageManagementService
<br>WINSRuntime
<br>WMISnmpProvider
<br>WorkFolders-Server
<br>WSS-pacote-produto

</div>