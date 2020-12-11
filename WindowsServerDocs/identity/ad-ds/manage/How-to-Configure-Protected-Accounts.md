---
description: 'Saiba mais sobre: orientação sobre como configurar contas protegidas'
ms.assetid: 70c99703-ff0d-4278-9629-b8493b43c833
title: Diretrizes sobre como configurar contas protegidas
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 1e4aff28a2212b678770cb9f78400e1db48cf8ec
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049614"
---
# <a name="guidance-about-how-to-configure-protected-accounts"></a>Diretrizes sobre como configurar contas protegidas

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Com ataques PtH (passagem de hash), um invasor pode autenticar em um servidor ou serviço remoto usando um hash de NTLM subjacente da senha de um usuário (ou outros derivados de credenciais). A Microsoft publicou anteriormente as [diretrizes](https://www.microsoft.com/download/details.aspx?id=36036) para atenuar os ataques de passagem de hash.  O Windows Server 2012 R2 inclui novos recursos para ajudar a mitigar esses ataques. Para obter mais informações sobre outros recursos de segurança que ajudam a proteger contra roubo de credenciais, consulte [proteção e gerenciamento de credenciais](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn408190(v=ws.11)). Este tópico explica como configurar os seguintes recursos novos:

-   [Usuários protegidos](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_AddtoProtectedUsers)

-   [Políticas de autenticação](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_CreateAuthNPolicies)

-   [Silos de política de autenticação](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_CreateAuthNPolicySilos)

Existem medidas para ajudar a evitar o roubo de credenciais adicionais integradas ao Windows 8.1 e Windows Server 2012 R2, abordadas nos seguintes tópicos:

-   [Modo de administrador restrito para Área de Trabalho Remota](/archive/blogs/kfalde/restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2)

-   [Proteção do LSA](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn408187(v=ws.11))

## <a name="protected-users"></a><a name="BKMK_AddtoProtectedUsers"></a>Usuários protegidos
Usuários protegidos é um novo grupo de segurança global ao qual é possível adicionar usuários novos ou existentes. Os dispositivos Windows 8.1 e hosts Windows Server 2012 R2 têm comportamento especial com membros desse grupo para fornecer melhor proteção contra roubo de credenciais. Para um membro do grupo, um dispositivo Windows 8.1 ou um host do Windows Server 2012 R2 não armazena em cache as credenciais que não têm suporte para usuários protegidos. Os membros desse grupo não terão proteção adicional se estiverem conectados a um dispositivo que executa uma versão do Windows anterior à Windows 8.1.

Os membros do grupo de usuários protegidos que estão conectados a dispositivos Windows 8.1 e hosts Windows Server 2012 R2 *não podem mais* usar:

-   Delegação de credencial padrão (CredSSP) - credenciais em texto simples não são armazenadas em cache mesmo se a política **Permitir credenciais de delegação padrão** for habilitada

-   Windows Digest - credenciais em texto simples não serão armazenadas em cache mesmo se habilitadas

-   NTLM - NTOWF não é armazenado em cache

-   Chaves de Kerberos a longo prazo - o TGT de Kerberos é adquirido no logon e não pode ser readquirido automaticamente

-   Entrar offline - o verificador de logon armazenado em cache não é criado

Se o nível funcional do domínio for Windows Server 2012 R2, os membros do grupo não poderão mais:

-   Autenticar usando autenticação NTLM

-   Usar suites de criptografia DES (padrão de criptografia de dados) ou RC4 na pré-autenticação do Kerberos

-   Ser delegado com delegação restrita ou irrestrita

-   Renovar tíquetes de usuário (TGTs) além do tempo de vida inicial de quatro horas

Para adicionar usuários ao grupo, você pode usar [ferramentas de interface do usuário](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753515(v=ws.11)) , como centro administrativo do Active Directory (ADAC) ou Active Directory usuários e computadores, ou uma ferramenta de linha de comando, como o [grupo dsmod](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc732423(v=ws.11)), ou o cmdlet[Add-ADGroupMember](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617210(v=technet.10)) do Windows PowerShell. As contas para serviços e computadores *não devem* ser membros do grupo usuários protegidos. A associação a essas contas não oferece proteções locais, pois a senha ou certificado sempre está disponível no host.

> [!WARNING]
> As restrições de autenticação não possuem solução alternativa, o que significa que membros de grupos altamente privilegiados como os grupos Administradores de Empresa e Admins. do Domínio estão sujeitos às mesmas restrições que outros membros do grupo Usuários protegidos. Se todos os membros desses grupos forem adicionados ao grupo de usuários protegidos, será possível que todas essas contas sejam bloqueadas. Você nunca deve adicionar todas as contas altamente privilegiadas ao grupo de usuários protegidos até que tenha testado completamente o impacto potencial.

Os membros do grupo Usuários Protegidos devem poder se autenticar usando Kerberos com AES. Este método pede chaves AES para a conta do Active Directory. O administrador interno não tem uma chave AES, a menos que a senha tenha sido alterada em um controlador de domínio que execute o Windows Server 2008 ou posterior. Além disso, qualquer conta, que tenha uma senha que tenha sido alterada em um controlador de domínio que executa uma versão anterior do Windows Server, é bloqueada. Portanto, siga estas práticas recomendadas:

-   Não teste em domínios, a menos que **todos os controladores de domínio executem o Windows Server 2008 ou posterior**.

-   **Altere a senha** de todas as contas criadas *antes* da criação do domínio. Senão, essas contas não poderão ser autenticadas.

-   **Altere a senha** para cada usuário antes de adicionar a conta ao grupo de usuários protegidos ou verifique se a senha foi alterada recentemente em um controlador de domínio que executa o Windows Server 2008 ou posterior.

### <a name="requirements-for-using-protected-accounts"></a><a name="BKMK_Prereq"></a>Requisitos para usar contas protegidas
Contas protegidas possuem os seguintes requisitos para implantação:

-   Para fornecer restrições do lado do cliente para usuários protegidos, os hosts devem executar o Windows 8.1 ou o Windows Server 2012 R2. Um usuário precisa apenas entrar com uma conta membro do grupo Usuários protegidos. Nesse caso, o grupo usuários protegidos pode ser criado [transferindo a função de emulador PDC (controlador de domínio primário)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816944(v=ws.10)) para um controlador de domínio que executa o Windows Server 2012 R2. Depois de o objeto do grupo ser replicado para outros controladores de domínio, a função do emulador de PDC pode se hospedada em um controlador de domínio que executa uma versão anterior do Windows Server.

-   Para fornecer restrições do lado do controlador de domínio para usuários protegidos, isso é restringir o uso da autenticação NTLM e outras restrições, o nível funcional do domínio deve ser o Windows Server 2012 R2. Para obter mais informações sobre os níveis funcionais, consulte [noções básicas sobre níveis funcionais de Active Directory Domain Services (AD DS)](../active-directory-functional-levels.md).

### <a name="troubleshoot-events-related-to-protected-users"></a><a name="BKMK_TrubleshootingEvents"></a>Solução de problemas de eventos relacionados a Usuários protegidos
Esta seção aborda os novos logs para ajudar solucionar problemas de eventos relacionados aos Usuários protegidos e demonstra como os Usuários protegidos podem representar mudanças nas soluções de problemas de expiração de TGT e de delegação.

#### <a name="new-logs-for-protected-users"></a>Novos logs para Usuários protegidos

Dois novos logs administrativos operacionais estão disponíveis para ajudar a solucionar problemas de eventos relacionados a usuários protegidos: log do cliente protegido e falhas do usuário protegido-log do controlador de domínio. Esses novos logs encontram-se no Visualizador de Eventos e estão desabilitados por padrão. Para habilitar um log, clique em **Logs de aplicativos e serviços**, depois em **Microsoft**, **Windows**, **Autenticação**, clique no nome do log e em **Ação** (ou então, clique com o botão direito no log) e clique em **Habilitar log**.

Para obter mais informações sobre eventos nesses logs, consulte [políticas de autenticação e silos de política de autenticação](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486813(v=ws.11)).

#### <a name="troubleshoot-tgt-expiration"></a>Solução de problemas de expiração de TGT
Normalmente, o controlador de domínio define o tempo de vida de TGT e sua renovação com base na política de domínio, conforme mostrado na janela Editor de Gerenciamento de Política de Grupo a seguir.

![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTExpiration.png)

Para **Usuários protegidos**, as configurações a seguir são embutidas em código:

-   Tempo de vida máximo para tíquete de usuário: 240 minutos

-   Tempo de vida máximo para renovação de tíquete de usuário: 240 minutos

#### <a name="troubleshoot-delegation-issues"></a>Solução de problemas de delegação
Anteriormente, se uma tecnologia que usa delegação de Kerberos falhasse, a conta cliente era verificada para ver se **Conta sensível à segurança, não pode ser delegada** estava definido. Contudo, se a conta for um membro de **Usuários protegidos**, ela pode não ter esta definição configurada no ADAC (Centro Administrativo do Active Directory). Por isso, verifique as definições de associações de grupo ao solucionar problemas de delegação.

![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TshootDelegation.gif)

### <a name="audit-authentication-attempts"></a><a name="BKMK_AuditAuthNattempts"></a>Auditar tentativas de autenticação
Para auditar tentativas explicitamente para os membros do grupo **Usuários protegidos**, você pode continuar a coletar eventos de auditoria de log de segurança ou os dados dos novos logs administrativos operacionais. Para obter mais informações sobre esses eventos, consulte [políticas de autenticação e silos de política de autenticação](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486813(v=ws.11))

### <a name="provide-dc-side-protections-for-services-and-computers"></a><a name="BKMK_ProvidePUdcProtections"></a>Fornecer proteções do lado do controlador de domínio a serviços e computadores
Contas de serviços e computadores não podem ser membros do **Usuários protegidos**. Esta seção explica quais proteções baseadas no controlador de domínio podem ser oferecidas a tais contas:

-   Rejeitar autenticação NTLM: somente por meio de [políticas de bloqueio NTLM](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/jj865674(v=ws.10))

-   Rejeitar o padrão de criptografia de dados (DES) na pré-autenticação de Kerberos: os controladores de domínio do Windows Server 2012 R2 não aceitam DES para contas de computador, a menos que estejam configurados para DES somente porque cada versão do Windows lançada com o Kerberos também oferece suporte a RC4.

-   Rejeitar RC4 na pré-autenticação do Kerberos: não configurável.

    > [!NOTE]
    > Embora seja possível [alterar a configuração de tipos de criptografia com suporte](/archive/blogs/openspecification/windows-configurations-for-kerberos-supported-encryption-type), não é recomendável alterar essas configurações para contas de computador sem teste no ambiente de destino.

-   Restringir tíquetes de usuário (TGTs) a um tempo de vida inicial de 4 horas: usar políticas de autenticação.

-   Negar delegação com delegação irrestrita ou restrita: para restringir uma conta, abra Centro Administrativo do Active Directory (ADAC) e marque a caixa de seleção a **conta é confidencial e não pode ser delegada** .

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TshootDelegation.gif)

## <a name="authentication-policies"></a><a name="BKMK_CreateAuthNPolicies"></a>Políticas de autenticação
Políticas de autenticação é um novo contêiner no AD DS que contém objetos de política de autenticação. As políticas de autenticação podem especificar configurações que ajudam a reduzir o risco de roubo de credenciais, tais como restringir o tempo de vida de TGT das contas ou adicionar outras condições relacionadas a declarações.

No Windows Server 2012, o controle de acesso dinâmico introduziu uma classe de objeto de escopo de floresta Active Directory chamada de política de acesso central para fornecer uma maneira fácil de configurar servidores de arquivos em toda a organização. No Windows Server 2012 R2, uma nova classe de objeto chamada diretiva de autenticação (objectClass msDS-AuthNPolicies) pode ser usada para aplicar a configuração de autenticação a classes de conta em domínios do Windows Server 2012 R2. As classes da conta do Active Directory são:

-   Usuário

-   Computador

-   Conta de serviço gerenciado e Conta de serviço gerenciado de grupo (GMSA)

### <a name="quick-kerberos-refresher"></a>Atualizador rápido do Kerberos
O protocolo de autenticação Kerberos consiste em três tipos de trocas, também conhecidas como subprotocolos:

![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_KerbRefresher.gif)

-   A troca de serviço de autenticação (AS) (KRB_AS_*)

-   A troca de Serviço de concessão de tíquete (TGS) (KRB_TGS_*)

-   A troca entre Cliente/servidor (AP) (KRB_AP_*)

O as Exchange é onde o cliente usa a senha da conta ou a chave privada para criar um pré-registro para solicitar um tíquete de concessão de tíquete (TGT). Isso ocorre no momento da entrada do usuário ou na primeira vez que um tíquete de serviço é necessário.

A troca de TGS é onde o TGT da conta é usado para criar um autenticador para solicitar um tíquete de serviço. Isso ocorre quando uma conexão autenticada é necessária.

A troca AP ocorre geralmente como dados dentro do protocolo do aplicativo e não é afetada pelas políticas de autenticação.

Para obter informações mais detalhadas, consulte [como funciona o protocolo de autenticação Kerberos versão 5](/previous-versions/windows/it-pro/windows-server-2003/cc772815(v=ws.10)).

### <a name="overview"></a>Visão geral
As políticas de autenticação complementam o grupo Usuários Protegidos ao oferecer uma maneira de aplicar restrições configuráveis a contas, além de fornecer restrições a contas para serviços e computadores. As políticas de autenticação são impostas durante as trocas AS ou TGS.

Você pode restringir a autenticação inicial ou a troca AS configurando:

-   Um tempo de vida de TGT

-   As condições de controle de acesso para restringir a entrada do usuário, devendo ser cumpridas pelos dispositivos que enviam a troca AS

![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictAS.gif)

Você pode restringir as solicitações de tíquete de serviço por meio da troca TGS configurando:

-   As condições de controle de acesso que devem ser cumpridas pelo cliente (usuário, serviço ou computador) ou dispositivo que enviam a troca TGS

### <a name="requirements-for-using-authentication-policies"></a><a name="BKMK_ReqForAuthnPolicies"></a>Requisitos para usar políticas de autenticação

|Política|Requisitos|
|----------|----------------|
|Fornecer tempos de vida de TGT personalizados| Domínios de conta de nível funcional de domínio do Windows Server 2012 R2|
|Entrada de usuário restrita|-Domínios de conta de nível funcional de domínio do Windows Server 2012 R2 com suporte ao controle de acesso dinâmico<br />-Dispositivos Windows 8, Windows 8.1, Windows Server 2012 ou Windows Server 2012 R2 com suporte ao controle de acesso dinâmico|
|Restringir a emissão de tíquetes de serviço com base na conta de usuário e grupos de segurança| Domínios de recurso de nível funcional de domínio do Windows Server 2012 R2|
|Restringir a emissão de tíquetes de serviço com base nas declarações de usuário ou conta de dispositivo, grupos de segurança ou declarações| Domínios de recurso de nível funcional de domínio do Windows Server 2012 R2 com suporte a controle de acesso dinâmico|

### <a name="restrict-a-user-account-to-specific-devices-and-hosts"></a>Restringir uma conta de usuário a dispositivos e hosts específicos
Uma conta de alto valor com privilégio administrativo deve ser membro do grupo **Usuários Protegidos**. Por padrão, nenhuma conta é membro do grupo **Usuários protegidos**. Antes de adicionar contas ao grupo, configure o suporte ao controlador de domínio e crie uma política de auditoria para garantir que não haja problemas de bloqueio.

#### <a name="configure-domain-controller-support"></a>Configurar suporte ao controlador de domínio

O domínio da conta do usuário deve estar no nível funcional do domínio do Windows Server 2012 R2 (DFL). Verifique se todos os controladores de domínio são do Windows Server 2012 R2 e, em seguida, use Active Directory domínios e relações de confiança para [aumentar o DFL para o](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753104(v=ws.11)) Windows Server 2012 R2.

**Para configurar o suporte ao Controle de Acesso Dinâmico**

1.  Em Política de controladores de domínio padrão, clique em **Habilitado** para habilitar **Suporte KDC para declarações, autenticação composta e proteção do Kerberos** em Configuração do Computador | Modelos Administrativos | Sistema | KDC.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_EnableKDCClaims.gif)

2.  Em **Opções**, na caixa de listagem suspensa, escolha **Sempre fornecer declarações**.

    > [!NOTE]
    > **Com suporte** também pode ser configurado, mas como o domínio está no Windows Server 2012 R2 DFL, ter os DCS sempre fornecem declarações permitirá que as verificações de acesso baseadas em declarações do usuário ocorram ao usar dispositivos e hosts sem reconhecimento de declaração para se conectar a serviços com reconhecimento de declaração.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AlwaysProvideClaims.png)

    > [!WARNING]
    > A configuração de **solicitações de autenticação desprotegidas de falha** resultará em falhas de autenticação de qualquer sistema operacional que não ofereça suporte à proteção Kerberos, como o Windows 7 e sistemas operacionais anteriores, ou sistemas operacionais que comecem com o Windows 8, que não foram explicitamente configurados para dar suporte a ele.

#### <a name="create-a-user-account-audit-for-authentication-policy-with-adac"></a>Criar uma auditoria de conta de usuário para política de autenticação com o ADAC

1.  Abra o ADAC (Centro Administrativo do Active Directory).

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_OpenADAC.gif)

    > [!NOTE]
    > O nó de **autenticação** selecionado é visível para domínios que estão no Windows Server 2012 R2 DFL. Se o nó não aparecer, tente novamente usando uma conta de administrador de domínio de um domínio que esteja no Windows Server 2012 R2 DFL.

2.  Clique em **Políticas de autenticação** e em **Nova** para criar uma nova política.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicy.gif)

    As políticas de autenticação devem possuir um nome de exibição e são impostas por padrão.

3.  Para criar uma política somente para auditoria, clique em **Somente restrições de política de auditoria**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicyAuditOnly.gif)

    As políticas de autenticação são aplicadas com base no tipo de conta do Active Directory. Uma única política pode ser aplicada a todos os três tipos de conta ao configurar as definições de cada tipo. Os tipos de conta são:

    -   Usuário

    -   Computador

    -   Conta de serviço gerenciado e conta de serviço gerenciado de grupo

    Se você estender o esquema com as novas entidades que podem ser usadas pelo KDC, o novo tipo de conta será classificado de acordo com o tipo de conta derivada mais próximo.

4.  Para configurar um tempo de vida de TGT para contas de usuário, marque a caixa de seleção **Especificar um tempo de vida do Tíquete de Concessão de Tíquete para contas de usuário** e digite o tempo em minutos.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTLifetime.gif)

    Por exemplo, se você deseja obter um tempo de vida de TGT máximo de 10 horas, digite **600** como mostrado. Se o tempo de vida de TGT não for configurado, se a conta for membro do grupo **Protected Users**, o tempo de vida de TGT e sua renovação serão de quatro horas. Senão, o tempo de vida de TGT e sua renovação baseiam-se na política do domínio como indicado na janela Editor de Gerenciamento de Política de Grupo para o domínio com configurações padrão.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTExpiration.png)

5.  Para restringir a conta de usuário a certos dispositivos, clique em **Editar** para definir as condições pedidas pelo dispositivo.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_EditAuthNPolicy.gif)

6.  Na janela **Editar condições de controle de acesso**, clique em **Adicionar uma condição**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCondition.png)

##### <a name="add-computer-account-or-group-conditions"></a>Adicionar conta de computador ou condições de grupo

1.  Para configurar contas de computador ou grupos, na lista suspensa, escolha a caixa de listagem suspensa **Membro de cada uma** e mude para **Membro de qualquer uma**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompMember.png)

    > [!NOTE]
    > Este controle de acesso define as condições do dispositivo ou host do qual o usuário entra. Na terminologia de controle de acesso, a conta do computador para o dispositivo ou host é o usuário, e é por isso que **Usuário** é a única opção.

2.  Clique em **Adicionar itens**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompAddItems.png)

3.  Para alterar os tipos de objeto, clique em **Tipos de objeto**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjects.gif)

4.  Para escolher objetos de computador no Active Directory, clique em **Computadores** e em **OK**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjectsComputers.gif)

5.  Digite o nome dos computadores para restringir o usuário e clique em **Verificar nomes**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjectsCompName.gif)

6.  Clique em OK e crie quaisquer outras condições desejadas para a conta de computador.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompAddConditions.png)

7.  Ao concluir, clique em **OK** e as condições definidas serão exibidas na conta do computador.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompDone.png)

##### <a name="add-computer-claim-conditions"></a>Adicionar condições de declaração de computador

1.  Para configurar declarações de computador, vá para a lista suspensa Grupo para escolher a declaração.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaim.gif)

    As declarações somente estarão disponíveis se já tiverem sido provisionadas na floresta.

2.  Digite o nome do OU e a conta de usuário deverá ser restrita ao tentar entrar.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaimOUName.gif)

3.  Ao concluir, clique em OK e a caixa mostrará as condições definidas.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaimComplete.gif)

##### <a name="troubleshoot-missing-computer-claims"></a>Solução de problemas de declarações de computador faltantes
Se a declaração foi provisionada, mas não está disponível, pode ter sido configurada somente para classes **Computador**.

Digamos que você quisesse restringir a autenticação com base na UO (unidade organizacional) do computador, que já estava configurada, mas apenas para classes de **computador** .

![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictComputers.gif)

Para que a declaração esteja disponível para restringir a entrada do Usuário no dispositivo, marque a caixa de seleção **Usuário**.

![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictUsersComputers.gif)

#### <a name="provision-a-user-account-with-an-authentication-policy-with-adac"></a>Provisione uma conta de usuário com uma política de autenticação com o ADAC

1.  Na conta de **Usuário**, clique em **Política**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicy.gif)

2.  Marque a caixa de seleção **Atribuir uma política de autenticação a esta conta**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicyAssign.gif)

3.  Em seguida, escolha a política de autenticação a ser aplicada ao usuário.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicySelect.png)

#### <a name="configure-dynamic-access-control-support-on-devices-and-hosts"></a>Configurar suporte a Controle de Acesso Dinâmico em dispositivos e hosts
Você pode configurar os tempos d vida de TGT sem configurar o DAC (Controle de Acesso Dinâmico). O DAC somente é necessário para verificar AllowedToAuthenticateFrom e AllowedToAuthenticateTo.

Usando o Editor de Política de Grupo ou de Política de Grupo Local, habilite o **Suporte a cliente Kerberos para declarações, autenticação composta e proteção do Kerberos** em Configuração do Computador | Modelos Administrativos | Sistema | Kerberos:

![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_KerbClientDACSupport.gif)

### <a name="troubleshoot-authentication-policies"></a><a name="BKMK_TroubleshootAuthnPolicies"></a>Solução de problemas de políticas de autenticação

#### <a name="determine-the-accounts-that-are-directly-assigned-an-authentication-policy"></a>Determinar as contas às quais uma Política de autenticação é diretamente atribuída
A seção de contas na Política de autenticação mostra que as contas que possuem políticas diretamente aplicadas.

![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AccountsAssigned.gif)

#### <a name="use-the-authentication-policy-failures---domain-controller-administrative-log"></a>Usar as falhas da política de autenticação-log administrativo do controlador de domínio
Uma nova **falha de política de autenticação – log administrativo do controlador de domínio** em **logs de aplicativos e serviços**  >  a autenticação **do Microsoft**  >  **Windows**  >   foi criada para facilitar a descoberta de falhas devido a políticas de autenticação. Este log fica desabilitado por padrão. Para habilitá-lo, clique com o botão direito no nome do log e clique em **Habilitar log**. Os novos eventos são muito semelhantes com relação ao conteúdo aos eventos de TGT de Kerberos e auditoria de tíquete de serviço. Para obter mais informações sobre esses eventos, consulte [políticas de autenticação e silos de política de autenticação](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486813(v=ws.11)).

### <a name="manage-authentication-policies-by-using-windows-powershell"></a><a name="BKMK_ManageAuthnPoliciesUsingPSH"></a>Gerenciar as políticas de autenticação usando o Windows PowerShell
Este comando cria uma política de autenticação chamada **TestAuthenticationPolicy**. O parâmetro **UserAllowedToAuthenticateFrom** especifica os dispositivos aos quais o usuário pode autenticar-se com uma cadeia SDDL no arquivo chamado someFile.txt.

```
PS C:\> New-ADAuthenticationPolicy testAuthenticationPolicy -UserAllowedToAuthenticateFrom (Get-Acl .\someFile.txt).sddl
```

Este comando obtém todas as políticas de autenticação correspondentes ao filtro especificado no parâmetro **Filter**.

```
PS C:\> Get-ADAuthenticationPolicy -Filter "Name -like 'testADAuthenticationPolicy*'" -Server Server02.Contoso.com

```

Este comando modifica a descrição e as propriedades **UserTGTLifetimeMins** da política de autenticação especificada.

```
PS C:\> Set-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1 -Description "Description" -UserTGTLifetimeMins 45
```

Este comando remove a política de autenticação especificada pelo parâmetro **Identity**.

```
PS C:\> Remove-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1
```

Este comando usa o cmdlet **Get-ADAuthenticationPolicy** com o parâmetro **Filter** para obter todas as políticas de autenticação que não estão sendo impostas. O conjunto de resultados é canalizado para o cmdlet **Remove-ADAuthenticationPolicy**.

```
PS C:\> Get-ADAuthenticationPolicy -Filter 'Enforce -eq $false' | Remove-ADAuthenticationPolicy
```

## <a name="authentication-policy-silos"></a><a name="BKMK_CreateAuthNPolicySilos"></a>Silos de política de autenticação
Os Silos de política de autenticação são um novo contêiner (objectClass msDS-AuthNPolicySilos) no AD DS para contas de usuário, computador e serviço. Eles ajudam a proteger contas de alto valor. Embora todas as organizações precisem proteger membros dos grupos Administradores de Empresa, Admins. do Domínio e Administradores de Esquema devido ao fato de que essas contas podem ser usadas por um invasor para acessar qualquer coisa presente na floresta, outras contas também podem precisar de proteção.

Algumas organizações isolam as cargas de trabalho criando contas específicas para elas e aplicando configurações de Política de grupo para limitar a entrada interativa local e remota e os privilégios administrativos. Os silos de política de autenticação complementam este trabalho ao criar uma maneira para definir uma relação entre as contas de Usuário, Computador e Serviço gerenciada. As contas podem pertencer somente a um silo. Você pode configurar uma política de autenticação para cada tipo de conta a fim de controlar:

1.  O tempo de vida de TGT não renovável

2.  As condições de controle de acesso para retornar o TGT (observação: não pode ser aplicado a sistemas, pois a proteção do Kerberos é necessária)

3.  As condições de controle de acesso para retornar o tíquete de serviço

Além disso, as contas pertencentes a um silo de política de autenticação possuem uma declaração de silo, que pode ser usada por recursos equipados para declarações como servidores de arquivos para controlar o acesso.

Um novo descritor de segurança pode ser configurado para controlar a emissão de tíquete de serviço com base no:

-   Usuário, grupos de segurança do usuário e/ou declarações do usuário

-   Dispositivo, grupo de segurança do dispositivo e/ou declarações do dispositivo

Obter essas informações para os DCs do recurso requer o controle de acesso dinâmico:

-   Declarações de usuário:

    -   Clientes do Windows 8 ou posterior com suporte ao Controle de Acesso Dinâmico

    -   Domínio de conta com suporte ao Controle de Acesso Dinâmico e declarações

-   Dispositivo e/ou seu grupo de segurança:

    -   Clientes do Windows 8 ou posterior com suporte ao Controle de Acesso Dinâmico

    -   Recurso configurado para autenticação composta

-   Declarações do dispositivo:

    -   Clientes do Windows 8 ou posterior com suporte ao Controle de Acesso Dinâmico

    -   Domínio de dispositivo com suporte ao Controle de Acesso Dinâmico e declarações

    -   Recurso configurado para autenticação composta

As políticas de autenticação podem ser aplicadas a todos os membros de um silo de política de autenticação em vez de contas individuais, ou políticas de autenticações separadas podem ser aplicadas a diferentes tipos de contas em um mesmo silo. Por exemplo, uma política de autenticação pode ser aplicada a contas de usuário com altos privilégios e outra política pode ser aplicada a contas de serviço. Pelo menos uma política de autenticação deverá ser criada antes da criação do silo de política de autenticação.

> [!NOTE]
> Uma política de autenticação pode ser aplicada aos membros de um silo de política de autenticação, ou então, aplicada independentemente dos silos para restringir um escopo específico de contas. Por exemplo, para proteger uma única conta ou um pequeno conjunto de contas, uma política pode ser definida nessas contas sem adicionar a conta a um silo.

Você pode criar um silo de política de autenticação usando Centro Administrativo do Active Directory ou o Windows PowerShell. Por padrão, um silo de política de autenticação apenas audita políticas de silo, o que é equivalente a especificar o parâmetro **WhatIf** nos cmdlets do Windows PowerShell. Neste caso, as restrições do silo de políticas não são aplicadas, mas as auditorias são geradas, a fim de indicar se ocorreriam falhas durante a aplicação das restrições.

#### <a name="to-create-an-authentication-policy-silo-by-using-active-directory-administrative-center"></a>Para criar um silo de política de autenticação usando o Centro Administrativo do Active Directory

1.  Abra o **Centro Administrativo do Active Directory**, clique em **Autenticação**, clique com o botão direito em **Silos de política de autenticação**, clique em **Novo** e em **Silo de política de autenticação**.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CreateNewAuthNPolicySilo.gif)

2.  Em **Nome de exibição**, digite um nome para o silo. Em **Contas permitidas**, clique em **Adicionar**, digite os nomes das contas e clique em **OK**. Você pode especificar contas de usuários, computadores ou serviço. Em seguida, especifique se deseja usar uma única política para todas as entidades ou um política separada para cada tipo de entidade, bem como o nome das políticas em questão.

    ![contas protegidas](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicySiloDisplayName.gif)

### <a name="manage-authentication-policy-silos-by-using-windows-powershell"></a><a name="BKMK_ManageAuthnSilosUsingPSH"></a>Gerenciar os silos de política de autenticação usando o Windows PowerShell
Este comando cria um objeto do silo de política de autenticação e o impõe.

```
PS C:\>New-ADAuthenticationPolicySilo -Name newSilo -Enforce
```

Este comando obtém todos os silos de política de autenticação correspondentes ao filtro especificado pelo parâmetro **Filter**. A saída é então repassada ao cmdlet **Format-Table** para exibir o nome da política e o valor de **Enforce** em cada política.

```
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Name -like "*silo*"' | Format-Table Name, Enforce -AutoSize

Name  Enforce
----  -------
silo     True
silos   False

```

Este comando usa o cmdlet **Get-ADAuthenticationPolicySilo** com o parâmetro **Filter** para obter todos os silos de política de autenticação não impostos e canalizar o resultado do filtro para o cmdlet **Remove-ADAuthenticationPolicySilo**.

```
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Enforce -eq $False' | Remove-ADAuthenticationPolicySilo
```

Este comando concede acesso ao silo de política de autenticação chamado *Silo* para a conta de usuário chamada *User01*.

```
PS C:\>Grant-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01
```

Este comando revoga o acesso ao silo de política de autenticação chamado *Silo* para a conta de usuário chamada *User01*. Como o parâmetro **Confirm** está definido como **$False**, nenhuma mensagem de confirmação é exibida.

```
PS C:\>Revoke-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01 -Confirm:$False
```

Este primeiro exemplo usa o cmdlet **Get-ADComputer** para obter todas as contas de computador correspondentes ao filtro especificado pelo parâmetro **Filter**. A saída deste comando é repassada para o **Set-ADAccountAuthenticatinPolicySilo** para atribuir o silo de política de autenticação chamado *Silo* e a política de autenticação chamada *AuthenticationPolicy02* a ele.

```
PS C:\>Get-ADComputer -Filter 'Name -like "newComputer*"' | Set-ADAccountAuthenticationPolicySilo -AuthenticationPolicySilo Silo -AuthenticationPolicy AuthenticationPolicy02
```
