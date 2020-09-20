---
title: Criar perfis de VPNv2 baseados em OMA-DM para dispositivos Windows 10
description: 'Você pode usar um dos dois métodos para criar perfis de VPNv2 baseados em OMA-DM. '
ms.topic: article
ms.date: 07/13/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: c5619baa5123d0cd611cb9371cd3944fdd91fb3c
ms.sourcegitcommit: 877d6db73d9520e3a23738d6528016235493cff3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90779260"
---
# <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devices"></a>Etapa 7.5. Criar perfis de VPNv2 baseados em OMA-DM para dispositivos Windows 10

>Aplica-se a: Windows Server (canal semestral), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Anterior:** Etapa 7,4. Implantar certificados raiz de acesso condicional no AD local](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)
- [**Em seguida:** Saiba como o acesso condicional para VPN funciona](/windows/access-protection/vpn/vpn-conditional-access)

Nesta etapa, você pode criar perfis de VPNv2 baseados em OMA-DM usando o Intune para implantar uma política de configuração de dispositivo VPN. Se você quiser usar o Microsoft Endpoint Configuration Manager ou o script do PowerShell para criar perfis do VPNv2, consulte [configurações do CSP do VPNv2](/windows/client-management/mdm/vpnv2-csp) para obter mais detalhes.

## <a name="managed-deployment-using-intune"></a>Implantação gerenciada usando o Intune

Tudo o que discutimos nesta seção é o mínimo necessário para que a VPN funcione com acesso condicional. Ele não abrange o túnel dividido, usando WIP, criando perfis de configuração de dispositivo do Intune personalizados para obter AutoVPN funcionando ou SSO. Integre as configurações abaixo no perfil VPN criado anteriormente na [etapa 5. Configure o cliente do Windows 10 Always On conexões VPN](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md).Neste exemplo, estamos integrando-os na política [Configurar o cliente VPN usando o Intune](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune) .

**Forem**

O computador cliente do Windows 10 já foi configurado com uma conexão VPN usando o Intune.


**Procedure**

1. Na portal do Azure, selecione perfis de configuração de **Intune**  >  **dispositivo**  >  **Profiles** do Intune e selecione o perfil VPN que você criou anteriormente em [Configurar o cliente VPN usando o Intune](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune).

2. No editor de políticas, selecione **Propriedades**  >  **configurações**de  >  **VPN base**. Estenda o **XML do EAP** existente para incluir um filtro que forneça ao cliente VPN a lógica de que ele precisa para recuperar o certificado de acesso condicional do AAD do repositório de certificados do usuário, em vez de deixá-lo à chance de permitir que ele use o primeiro certificado descoberto.

    >[!NOTE]
    >Sem isso, o cliente VPN pode recuperar o certificado de usuário emitido da autoridade de certificação local, resultando em uma conexão VPN com falha.

    ![Portal do Intune](../../media/Always-On-Vpn/intune-eap-xml.png)

3. Localize a seção que termina com **\</AcceptServerName>\</EapType>** e insira a seguinte cadeia de caracteres entre esses dois valores para fornecer ao cliente VPN a lógica para selecionar o certificado de acesso condicional do AAD:

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. Selecione a folha **acesso condicional** e alterne o **acesso condicional para esta conexão VPN** para **habilitado**.

   A habilitação dessa configuração altera a configuração ** \<DeviceCompliance> \<Enabled> true \</Enabled> ** no XML do perfil VPNv2.

    ![Acesso condicional para Always On VPN-Properties](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

5. Selecione **OK**.

6. Selecione **atribuições**, em incluir, selecione **grupos a serem incluídos**.

7. Selecione o grupo **usuários VPN** que recebe essa política e selecione **salvar**.

    ![LIMITE para usuários VPN automáticos-atribuições](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## <a name="force-mdm-policy-sync-on-the-client"></a>Forçar a sincronização da política de MDM no cliente

Se o perfil VPN não aparecer no dispositivo cliente, em configurações \\ rede & Internet \\ VPN, você poderá forçar a sincronização da política MDM.

1. Entre em um computador cliente ingressado no domínio como um membro do grupo de **usuários VPN** .

2. No menu Iniciar, insira **conta**e pressione Enter.

3. No painel de navegação esquerdo, selecione **acesso corporativo ou de estudante**.

4. Em acesso corporativo ou de estudante, selecione **conectado a < \domain> MDM**e, em seguida, selecione **informações**.

5. Selecione **sincronizar** e verifique se o perfil VPN aparece em configurações \\ rede & Internet \\ VPN.


## <a name="next-steps"></a>Próximas etapas

Você concluiu a configuração do perfil VPN para usar o acesso condicional do Azure AD.

|Se desejar...  |Em seguida, consulte...  |
|---------|---------|
|Saiba mais sobre como o acesso condicional funciona com VPNs  |[VPN e acesso condicional](/windows/access-protection/vpn/vpn-conditional-access): Esta página fornece mais informações sobre como o acesso condicional funciona com VPNs.      |
|Saiba mais sobre os recursos avançados de VPN  |[Recursos avançados de VPN](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features): Esta página fornece orientação sobre como habilitar filtros de tráfego de VPN, como configurar conexões VPN automáticas usando gatilhos de aplicativo e como configurar o NPS para permitir somente conexões VPN de clientes usando certificados emitidos pelo Azure AD.        |


## <a name="related-topics"></a>Tópicos relacionados

- [CSP VPNv2](/windows/client-management/mdm/vpnv2-csp): Este tópico fornece uma visão geral do VPNv2 CSP. O provedor de serviços de configuração do VPNv2 permite que o servidor MDM (gerenciamento de dispositivo móvel) Configure o perfil VPN do dispositivo.

- [Configurar conexões VPN Always on cliente do Windows 10](./always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md): Este tópico fornece informações sobre as opções e o esquema do ProfileXML e como criar a VPN ProfileXML. Depois de configurar a infraestrutura do servidor, você deve configurar os computadores cliente do Windows 10 para se comunicar com essa infraestrutura com uma conexão VPN.

- [Configurar o cliente VPN usando o Intune](./always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune): Este tópico fornece informações sobre como implantar o acesso remoto do Windows 10 Always on perfis VPN. O Intune agora usa grupos do Azure AD. Se Azure AD Connect tiver sincronizado o grupo de usuários VPN do local para o Azure AD, não haverá necessidade de configurar o cliente VPN usando o Intune.
