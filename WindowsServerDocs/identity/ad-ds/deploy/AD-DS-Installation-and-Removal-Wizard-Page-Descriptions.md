---
ms.assetid: ac727bd1-a892-47ed-a7ba-439b34187d4e
title: Descrições das páginas do assistente de instalação e remoção do AD DS
description: Fornece descrições para os controles nas páginas do assistente a seguir que compõem a instalação e a remoção da função de servidor AD DS no Gerenciador do Servidor.
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 5c7918cba2031e9542379a0a7145fb895458c823
ms.sourcegitcommit: 2ede79efbadd109099bb6fdb744796adde123922
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2021
ms.locfileid: "98923696"
---
# <a name="ad-ds-installation-and-removal-wizard-page-descriptions"></a>Descrições das páginas do assistente de instalação e remoção do AD DS

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Este tópico fornece descrições dos controles localizados nas seguintes páginas do assistente que abrange a instalação e a remoção da função de servidor AD DS no Gerenciador do Servidor.

-   [Configuração de Implantação](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DepConfigPage)

-   [Opções de Controlador de Domínio](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)

-   [Opções de DNS](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)

-   [Opções de RODC](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RODCOptionsPage)

-   [Opções adicionais](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdditionalOptionsPage)

-   [Caminhos](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Paths)

-   [Opções de preparação](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_AdprepCreds)

-   [Examinar Opções](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ViewInstallOptionsPage)

-   [Verificação de pré-requisitos](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_PrerqCheckPage)

-   [Resultados](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_Results)

-   [Credenciais de Remoção de Função](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalCredsPage)

-   [Opções e Avisos de Remoção de AD DS](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_RemovalOptionsPage)

-   [Nova Senha do Administrador](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_NewAdminPwdPage)

-   [Confirmar Seleções de Remoção de Função](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_ConfirmRoleRemovalPage)

## <a name="deployment-configuration"></a><a name="BKMK_DepConfigPage"></a>Configuração de implantação
O Gerenciador do Servidor começa cada instalação de controlador de domínio na página **Configuração de Implantação**. As demais opções e campos exigidos mudam nessa página e nas páginas subsequentes, dependendo da operação de implantação selecionada. Por exemplo, se você criar uma nova floresta, a página **Opções de preparação** não será exibida, mas se você instalar o primeiro controlador de domínio que executa o Windows Server 2012 em uma floresta ou domínio existente.

Alguns testes de validação são executados nessa página e, mais tarde, serão executados novamente como parte das verificações de pré-requisitos. Por exemplo, se você tentar instalar o primeiro controlador de domínio do Windows Server 2012 em uma floresta que tenha um nível funcional do Windows 2000, um erro aparecerá nessa página.

As opções a seguir são exibidas quando uma nova floresta é criada.

![Captura de tela da página configuração de implantação do assistente de configuração do Active Directory Domain Services mostrando as opções que aparecem quando você cria uma nova floresta.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Forest.gif)

-   Ao criar uma nova floresta, especifique um nome para o domínio raiz da floresta. O nome de domínio raiz da floresta não pode ter um rótulo único (por exemplo, deve ser "contoso.com" em vez de "contoso"). E deve usar as convenções de nomenclatura permitidas para domínios DNS. É possível especificar um IDN (Nome de Domínio Internacionalizado). Para saber mais sobre as convenções de nomenclatura de domínio DNS, consulte o artigo [KB 909264](https://support.microsoft.com/kb/909264).

-   Não crie novas florestas do Active Directory usando um nome igual ao nome DNS externo. Por exemplo, se sua URL de DNS de Internet for http: \/ /contoso.com, você deverá escolher um nome diferente para a floresta interna para evitar futuros problemas de compatibilidade. Esse nome deve ser exclusivo e de uso improvável no tráfego da Web; por exemplo, corp.contoso.com.

-   Você precisa ser membro do grupo Administradores no servidor em que será criada uma nova floresta.

Para obter mais informações sobre como criar uma floresta, consulte [instalar um novo Windows Server 2012 Active Directory floresta &#40;nível 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).

As opções a seguir são exibidas quando uma nova floresta é criada.

![Captura de tela da página configuração de implantação do assistente de configuração do Active Directory Domain Services mostrando as opções que aparecem quando você cria um novo domínio.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_ChildDomain.gif)

> [!NOTE]
> Ao criar um novo domínio de árvore, você precisa especificar o nome do domínio raiz da floresta, em vez do nome do domínio pai. As demais páginas e opções do assistente são as mesmas.

-   Clique em **Selecionar** para procurar o domínio pai ou a árvore do Active Directory ou digite um nome válido de domínio pai ou árvore. Depois, digite o nome do novo domínio em **Novo nome de domínio**.

-   Domínio de árvore: forneça um nome válido e totalmente qualificado de domínio raiz; o nome não pode conter apenas uma palavra e deve usar os requisitos de nome de domínio DNS.

-   Domínio filho: forneça um nome válido e com rótulo simples para o domínio filho; o nome deve usar os requisitos de nome de domínio DNS.

-   O Assistente de Configuração dos Serviços de Domínio Active Directory solicitará as credenciais de domínio se as suas credenciais atuais não forem de domínio. Clique em **Alterar** para fornecer as credenciais de domínio.

Para obter mais informações sobre como criar um domínio, consulte [instalar um novo Windows Server 2012 Active Directory domínio filho ou de árvore &#40;nível 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).

As opções a seguir são exibidas quando você adiciona um novo controlador de domínio a um domínio existente.

![Captura de tela da página configuração de implantação do assistente de configuração do Active Directory Domain Services mostrando as opções que aparecem quando você adiciona um novo controlador de domínio a um domínio existente.](./media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DeploymentConfiguration_Replica.gif)

-   Clique em **Selecionar** para procurar o domínio ou digite um nome de domínio válido.

-   O Gerenciador do Servidor solicitará credenciais válidas, se necessário. A instalação de um controle de domínio adicional exige associação ao grupo Admins. do Domínio.

    Além disso, a instalação do primeiro controlador de domínio que executa o Windows Server 2012 em uma floresta requer credenciais que incluem associações de grupo nos grupos Administradores de empresa e administradores de esquema. O Assistente de Configuração dos Serviços de Domínio Active Directory avisará você se as suas credenciais não tiverem as permissões ou as associações de grupo adequadas.

Para obter mais informações sobre como adicionar um controlador de domínio a um domínio existente, consulte [instalar um controlador de domínio de réplica do Windows Server 2012 em um domínio existente &#40;nível 200&#41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).

## <a name="domain-controller-options"></a><a name="BKMK_DCOptionsPage"></a>Opções do controlador de domínio
Ao criar uma nova floresta, este será o conteúdo da página Opções do Controlador de Domínio:

![Captura de tela da página Opções do controlador de domínio do assistente de configuração do Active Directory Domain Services mostrando as opções que aparecem quando você cria uma nova floresta.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Forest.gif)

-   Os níveis funcionais de floresta e domínio são definidos como Windows Server 2012 por padrão.

    Há um novo recurso disponível no nível funcional do domínio do Windows Server 2012: o suporte para o controle de acesso dinâmico e a política de modelo administrativo do KDC de proteção Kerberos tem duas configurações (sempre fornecer declarações e falhas de solicitações de autenticação não protegidas) que exigem o nível funcional do domínio do Windows Server 2012. Para obter mais informações, consulte "suporte para declarações, autenticação composta e proteção Kerberos" em [novidades na autenticação Kerberos](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831747(v=ws.11)).
    O nível funcional de floresta do Windows Server 2012 não fornece novos recursos, mas garante que qualquer novo domínio criado na floresta operará automaticamente no nível funcional de domínio do Windows Server 2012. O nível funcional de domínio do Windows Server 2012 não fornece nenhum outro recurso novo ao lado do suporte para controle de acesso dinâmico e proteção Kerberos, mas garante que qualquer controlador de domínio no domínio execute o Windows Server 2012. Para obter mais informações sobre outros recursos que estão disponíveis em diferentes níveis funcionais, consulte [Noções básicas sobre níveis funcionais dos AD DS (Serviços de Domínio do Active Directory)](../active-directory-functional-levels.md).

    Além dos níveis funcionais, um controlador de domínio que executa o Windows Server 2012 fornece recursos adicionais que não estão disponíveis em um controlador de domínio que executa uma versão anterior do Windows Server. Por exemplo, um controlador de domínio que executa o Windows Server 2012 pode ser usado para clonagem do controlador de domínio virtual, enquanto um controlador de domínio que executa uma versão anterior do Windows Server não pode.

-   O servidor DNS é selecionado por padrão quando você cria uma nova floresta. O primeiro controlador de domínio na floresta deve ser um servidor GC (de catálogo global) e não pode ser um RODC (controlador de domínio somente leitura).

-   A senha DSRM ( Modo de Restauração dos Serviços de Diretório) é necessária para fazer logon em um controlador de domínio em que o AD DS esteja em execução. A senha especificada deve cumprir a política de senha aplicada ao servidor, a qual, por padrão, não exige uma senha forte, somente uma senha que não esteja em branco. Escolha sempre uma senha forte e complexa. Para saber mais sobre como sincronizar a senha DSRM com a senha de uma conta de usuário de domínio, consulte o artigo [KB 961320](https://support.microsoft.com/kb/961320).

Para obter mais informações sobre como criar uma floresta, consulte [instalar um novo Windows Server 2012 Active Directory floresta &#40;nível 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).

Ao criar um domínio filho, este será o conteúdo da página Opções do Controlador de Domínio:

![Captura de tela da página Opções do controlador de domínio do assistente de configuração do Active Directory Domain Services mostrando as opções que aparecem quando você está criando um domínio filho.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Child.gif)

-   O nível funcional do domínio é definido como Windows Server 2012 por padrão. Você pode especificar qualquer outro valor que seja pelo menos o valor do nível funcional de floresta ou superior.

-   As opções configuráveis de controlador de domínio incluem **Servidor DNS** e **Catálogo Global**; não é possível configurar um controlador de domínio somente leitura como o primeiro controlador de domínio em um novo domínio.

    A Microsoft recomenda que todos os controladores de domínio forneçam serviços DNS e de catálogo global para alta disponibilidade em ambientes distribuídos, e é por isso que o assistente habilita essas opções, por padrão, na criação de um novo domínio.

-   A página **Opções do Controlador de Domínio** também permite que você escolha o **nome de site** lógico do Active Directory, na configuração da floresta. Por padrão, o site é selecionado com a sub-rede mais correta. Se houver apenas um site, ele será selecionado automaticamente.

    > [!IMPORTANT]
    > Se o servidor não pertencer a uma sub-rede Active Directory e houver mais de um site, nada será selecionado e o botão **Avançar** ficará indisponível até você selecionar um site na lista.

Para obter mais informações sobre como criar um domínio, consulte [instalar um novo Windows Server 2012 Active Directory domínio filho ou de árvore &#40;nível 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).

Se estiver adicionando um controlador de domínio a um domínio, este será o conteúdo da página Opções do Controlador de Domínio:

![Captura de tela da página Opções do controlador de domínio do assistente de configuração do Active Directory Domain Services mostrando as opções que aparecem quando você está adicionando um controlador de domínio a um domínio.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DCOptions_Replica.gif)

-   As opções configuráveis de controlador de domínio incluem **servidor DNS** e **Catálogo Global** e o **controlador de domínio somente leitura**.

    A Microsoft recomenda que todos os controladores de domínio forneçam serviços DNS e de catálogo global para alta disponibilidade em ambientes distribuídos, e é por isso que o assistente habilita essas opções, por padrão. Para saber mais sobre a implantação de RODCs, consulte o [Guia de Implantação e Planejamento do Controlador de Domínio Somente Leitura](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771744(v=ws.10)).

Para obter mais informações sobre como adicionar um controlador de domínio a um domínio existente, consulte [instalar um controlador de domínio de réplica do Windows Server 2012 em um domínio existente &#40;nível 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).

## <a name="dns-options"></a><a name="BKMK_DNSOptionsPage"></a>Opções de DNS
Se você instalar o servidor DNS, a seguinte página **Opções de DNS** será exibida:

![Captura de tela da página opções de DNS do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_DNSOptions_Replica.gif)

Quando o servidor DNS é instalado, a delegação registra esse ponto no servidor DNS como autoritativo para a zona a ser criada na zona DNS (Sistema de Nomes de Domínio). A delegação registra a autoridade de resolução de nome de transferência e fornece a referência correta a outros clientes e servidores DNS dos novos servidores que estão se tornando autoritativos da nova zona. Estes registros de recursos incluem:

-   Um registro de recurso de NS (servidor de nomes) para efetuar a delegação. Esse registro de recurso comunica que o servidor chamado ns1.na.example.microsoft.com é um servidor autoritativo do subdomínio delegado.

-   Um registro de recurso de host (A ou AAAA) também conhecido como registro de União deve estar presente para resolver o nome do servidor especificado no registro de recurso do servidor de nomes (NS) para seu endereço IP. O processo de resolver o nome do host nesse registro de recurso para o servidor DNS delegado no registro de recurso do servidor de nomes, às vezes, é chamado de "caça a registros cola".

O Assistente de Configuração dos Serviços de Domínio Active Directory pode criá-los automaticamente. O assistente verifica se os registros adequados existem na zona DNS pai depois que você clica em **Avançar** na página **Opções do Controlador de Domínio**. Se o assistente não puder verificar a existência dos registros no domínio pai, o assistente dará a você a opção de criar automaticamente uma nova delegação DNS para um novo domínio (ou atualizar a delegação existente) e continuar com a instalação do novo controlador de domínio.

Outra alternativa é criar esses registros de delegação DNS antes de instalar o servidor DNS. Para criar uma delegação de zona, abra o **Gerenciador DNS**, clique com o botão direito do mouse no domínio pai e depois clique em **Nova Delegação**. Siga as etapas do Assistente de Nova Delegação para criar a delegação.

O processo de instalação tenta criar a delegação para assegurar que os computadores de outros domínios possam resolver consultas DNS para hosts, incluindo controladores de domínio e computadores membro, no subdomínio DNS. Observe que os registros de delegação podem ser criados automaticamente somente em servidores DNS da Microsoft. Se a zona pai de domínio DNS residir em servidores DNS de terceiros (por exemplo, BIND), um aviso informando que não foi possível criar registros de delegação DNS aparecerá na página Comprovação de requisitos anteriores. Para saber mais sobre esse aviso, consulte [Problemas conhecidos relacionados à instalação de AD DS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754463(v=ws.10)).

Delegações entre o domínio pai e o subdomínio que está sendo promovido podem ser criadas e validadas antes ou depois da instalação. Não há motivo para atrasar a instalação de um novo controlador de domínio porque você não pode criar ou atualizar a delegação DNS.

Para obter mais informações sobre delegação, consulte [noções básicas](https://go.microsoft.com/fwlink/?LinkId=164773) sobre a delegação de zona ( https://go.microsoft.com/fwlink/?LinkId=164773) . Se a delegação de zona não for possível na sua situação, talvez você possa considerar outros métodos para fornecer resolução de nome de outros domínios para os hosts do seu domínio. Por exemplo, o administrador DNS de outro domínio poderia configurar o encaminhamento condicional, zonas de stub ou zonas secundárias para resolver nomes no seu domínio. Para mais informações, consulte os seguintes tópicos:

-   [Noções básicas sobre tipos de zona](https://go.microsoft.com/fwlink/?LinkID=157399) (https://go.microsoft.com/fwlink/?LinkID=157399)

-   [Noções básicas sobre zonas de stub](https://go.microsoft.com/fwlink/?LinkId=164776) (https://go.microsoft.com/fwlink/?LinkId=164776)

-   [Noções básicas sobre encaminhadores](https://go.microsoft.com/fwlink/?LinkId=164778) (https://go.microsoft.com/fwlink/?LinkId=164778)

## <a name="rodc-options"></a><a name="BKMK_RODCOptionsPage"></a>Opções de RODC
As opções a seguir são exibidas quando um RODC (controlador de domínio somente leitura) é instalado.

![Captura de tela da página de opções do RODC do assistente de configuração do Active Directory Domain Services mostrando as opções que aparecem quando você instala um controlador de domínio somente leitura.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_RODCOptions.gif)

-   As contas de administrador delegadas obtêm permissões administrativas locais para o RODC. Esses usuários podem operar com privilégios equivalentes ao grupo Administradores do computador local. Eles não são membros do grupo Admins. do Domínio ou dos grupos Administradores embutidos no domínio. Essa opção é útil para a administração de filiais de delegação, mas sem emitir permissões administrativas de domínio. Não é preciso configurar a delegação de administração. Para saber mais, consulte [Separação de função de administrador](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753170(v=ws.10)).

-   A Política de Replicação de Senha age como uma ACL (lista de controle de acesso). Ela determina se um RODC deve ter permissão para armazenar uma senha no cache. Depois que o RODC recebe um logon de usuário ou computador autenticado, ele consulta a Política de Replicação de Senha para determinar se a senha da conta deve ser armazenada em cache. A mesma conta poderá, então, executar logons subsequentes com mais eficiência.

    A PRP (Política de Replicação de Senha) lista as contas cujas senhas estão autorizadas para armazenamento em cache e as contas cujas senhas foram explicitamente recusadas para esse tipo de armazenamento. A lista das contas de usuário e computador que podem ser armazenadas no cache não obriga o RODC a armazenar no cache as senhas dessas contas. Um administrador pode, por exemplo, especificar antecipadamente todas as contas que o RODC armazenará no cache. Dessa forma, o RODC poderá autenticar tais contas, mesmo que o link WAN para o site do hub esteja offline.

    Todos os usuários ou computadores que não estiverem autorizados (inclusive os implícitos) ou que foram recusados não armazenarão suas senhas no cache. Se esses usuários ou computadores não tiverem acesso ao controlador de domínio gravável, eles não poderão acessar recursos ou funcionalidade fornecidos pelo AD DS. Para saber mais sobre a PRP, consulte  [Política de Replicação de Senha](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730883(v=ws.10)). Para saber mais sobre o gerenciamento da PRP, consulte [Administrando a Política de Replicação de Senha](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754646(v=ws.10)).

Para obter mais informações sobre a instalação de RODCs, consulte [instalar um Windows Server 2012 Active Directory Read-Only controlador de domínio &#40;RODC&#41; &#40;nível 200&#41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md).

## <a name="additional-options"></a><a name="BKMK_AdditionalOptionsPage"></a>Opções adicionais
A opção a seguir aparecerá na página **Opções Adicionais** se você criar um novo domínio:

![Captura de tela da página opções adicionais do assistente de configuração de Active Directory Domain Services mostrando as opções que aparecem se você estiver criando um novo domínio.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Child.gif)

As opções a seguir aparecerão na página **Opções Adicionais** se você instalar um controlador de domínio adicional em um domínio existente:

![Captura de tela da página opções adicionais do assistente de configuração de Active Directory Domain Services mostrando as opções que aparecem se você instalar um controlador de domínio adicional em um domínio existente.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_AdditionalOptions_Replica.gif)

-   Você pode especificar um controlador de domínio como a fonte de replicação ou permitir que o assistente selecione qualquer controlador de domínio como a fonte de replicação.

-   Também é possível optar pela instalação do controlador de domínio usando uma mídia de backup e escolhendo a opção Instalar da mídia (IFM). Se a mídia de instalação estiver armazenada localmente, a opção **Instalar da mídia** permitirá que você procure o local do arquivo. A opção de procura não está disponível para instalação remota. Você pode clicar em **Verificar** para garantir que o caminho fornecido é de uma mídia válida. A mídia usada pela opção IFM deve ser criada com Backup do Windows Server ou Ntdsutil.exe de outro computador com Windows Server 2012 existente somente. Você não pode usar um sistema operacional Windows Server 2008 R2 ou anterior para criar mídia para um controlador de domínio do Windows Server 2012. Se a mídia for protegida por SYSKEY, o Gerenciador do Servidor solicitará a senha da imagem durante a verificação.

Para obter mais informações sobre como criar um domínio, consulte [instalar um novo Windows Server 2012 Active Directory domínio filho ou de árvore &#40;nível 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md). Para obter mais informações sobre como adicionar um controlador de domínio a um domínio existente, consulte [instalar um controlador de domínio de réplica do Windows Server 2012 em um domínio existente &#40;nível 200&#41;](../../ad-ds/deploy/../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).

## <a name="paths"></a><a name="BKMK_Paths"></a>Caminhos
As opções a seguir aparecem na página **Rotas**.

![Captura de tela da página caminhos do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_Paths.gif)

-   A página **Rotas** permite substituir os locais de pasta padrão do banco de dados AD DS, os logs de transação de banco de dados e o compartilhamento SYSVOL. Os locais padrão estão sempre em %systemroot%.

Especifique o local do banco de dados AD DS (NTDS.DIT), dos arquivos de log e do SYSVOL. Para uma instalação local, é possível procurar o local onde você quer armazenar os arquivos.

## <a name="preparation-options"></a><a name="BKMK_AdprepCreds"></a>Opções de preparação
![Captura de tela da página opções de preparação do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PreparationOptions.gif)

Se, no momento, você não estiver conectado com credenciais suficientes para executar os comandos adprep.exe. e for necessário executar o adprep para concluir a instalação do AD DS, você será solicitado a fornecer as credenciais para executar adprep.exe. A Adprep deve ser executada para adicionar o primeiro controlador de domínio que executa o Windows Server 2012 a um domínio ou floresta existente. Mais especificamente:

-   A adprep/forestprep deve ser executada para adicionar o primeiro controlador de domínio que executa o Windows Server 2012 a uma floresta existente. Esse comando deve ser executado por um membro do grupo Administradores Corporativos, Administradores de Esquema e Administradores de Domínio do domínio que hospeda o mestre do esquema. Para esse comando ser concluído com êxito, deve haver conectividade entre o computador em que você executa o comando e o mestre do esquema da floresta.

-   O adprep/domainprep deve ser executado para adicionar o primeiro controlador de domínio que executa o Windows Server 2012 a um domínio existente. Esse comando deve ser executado por um membro do grupo Admins. do domínio do domínio em que você está instalando o controlador de domínio que executa o Windows Server 2012. Para esse comando ser concluído com êxito, deve haver conectividade entre o computador em que você executa o comando e o mestre da infraestrutura do domínio.

-   O adprep /rodcprep deve ser executado para adicionar o primeiro RODC a uma floresta existente. Esse comando deve ser executado por um membro do grupo Administradores Corporativos. Para esse comando ser concluído com êxito, deve haver conectividade entre o computador em que você executa o comando e o mestre da infraestrutura do domínio.

Para obter mais informações sobre o Adprep.exe, consulte [Integração do Adprep.exe](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep) e [Executando o Adprep.exe](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)).

## <a name="review-options"></a><a name="BKMK_ViewInstallOptionsPage"></a>Examinar Opções
![Captura de tela da página opções de revisão do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_ReviewOptions.gif)

-   A página **Opções de revisão** permite que você valide suas configurações e se assegure de que elas cumprem os requisitos, antes de iniciar a instalação. Esta não é a última oportunidade de interromper a instalação usando o Gerenciador do Servidor. Essa página simplesmente permite que você examine e confirme suas configurações antes de continuar.

-   A página **Opções de revisão** do Gerenciador do Servidor também oferece um botão **Exibir Script** para criar um arquivo de texto Unicode contendo a configuração atual de ADDSDeployment como um script simples do Windows PowerShell. Isso permite que você use a interface gráfica do Gerenciador do Servidor como um estúdio de implantação do Windows PowerShell. Use o Assistente de Configuração dos Serviços de Domínio do Active Directory para configurar opções, exportar a configuração e então cancelar o assistente. Esse processo cria um exemplo válido e sintaticamente correto para modificações adicionais ou uso direto.

## <a name="prerequisites-check"></a><a name="BKMK_PrerqCheckPage"></a>Verificação de pré-requisitos
![Captura de tela da página verificação de pré-requisitos do assistente de configuração de Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_PrerequisitesCheck.gif)

Alguns dos avisos apresentados nessa página incluem:

-   Controladores de domínio que executam o Windows Server 2008 ou posterior têm uma configuração padrão para "permitir algoritmos de criptografia compatíveis com o Windows NT 4" que impede algoritmos de criptografia mais fracos ao estabelecer sessões de canal seguras. Para saber mais sobre o impacto potencial e uma solução alternativa, consulte o artigo [KB 942564](https://support.microsoft.com/kb/942564).

-   A delegação DNS não pôde ser criada, nem atualizada. Para saber mais, consulte [Opções DNS](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage).

-   A verificação de pré-requisitos exige chamadas WMI. Poderá haver falhas se estiverem bloqueadas por regras de firewall, e isso retornará um erro de servidor RPC indisponível.

Para obter mais informações sobre verificações de pré-requisito específicas que são executadas para a instalação do AD DS, consulte [Testes de pré-requisito](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_ADDSInstallPrerequisiteTests).

## <a name="results"></a><a name="BKMK_Results"></a>Resultados
![Captura de tela da página resultados do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_SMI_SMResultsBeta.gif)

Nessa página, é possível revisar os resultados da instalação.

Você também pode optar por reiniciar o servidor de destino após a conclusão do assistente, porém, se houver êxito na instalação, o servidor será sempre reiniciado, independentemente da opção que você escolher. Em alguns casos, após a conclusão do assistente em um servidor de destino que não foi ingressado no domínio antes da instalação, o estado do sistema do servidor de destino poderá tornar o servidor inatingível na rede, ou o estado do sistema poderá impedir você de obter as permissões para gerenciar o servidor remoto.

Se não for possível reiniciar o servidor de destino, reinicie-o manualmente. Ferramentas como shutdown.exe ou Windows PowerShell não podem reiniciá-lo. Os Serviços de Área de Trabalho Remota podem ser usados para fazer logon e desligar remotamente o servidor de destino.

## <a name="role-removal-credentials"></a><a name="BKMK_RemovalCredsPage"></a>Credenciais de Remoção de Função
![Captura de tela da página credenciais do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Credentials.gif)

Você pode configurar opções de rebaixamento na página **Credenciais**. Forneça as credenciais necessárias à execução do rebaixamento na lista a seguir:

-   O rebaixamento de um controlador de domínio adicional exige credenciais de Admin. do Domínio. A seleção **da remoção forçada do controlador de domínio** rebaixa o controlador de domínio sem remover os metadados do objeto do controlador de domínio do Active Directory.

    > [!IMPORTANT]
    > Não selecione essa opção, a menos que o controlador de domínio não possa contatar outros controladores de domínio e *não haja outra maneira razoável* de solucionar o problema de rede. O rebaixamento forçado resulta em metadados órfãos no Active Directory, nos controladores de domínio remanescentes na floresta. Além disso, todas as alterações que não foram replicadas nesse controlador de domínio, como senhas ou novas contas de usuário, serão perdidas definitivamente. Metadados órfãos são a principal causa da significativa porcentagem de casos no Atendimento ao Cliente da Microsoft para AD DS, Exchange, SQL e outros softwares. Se você forçar o rebaixamento de um controlador de domínio, *execute* manual e imediatamente a limpeza dos metadados. Para conhecer as etapas, examine [Limpar metadados do servidor](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816907(v=ws.10)).

-   O rebaixamento do último controlador de domínio em um domínio exige associação ao grupo Administradores Corporativos, pois esse processo remove o domínio propriamente dito (e se este for o último domínio da floresta, removerá a floresta). O Gerenciador do Servidor informará se o atual controlador de domínio for o último no domínio. Selecione **Último controlador de domínio no domínio** para confirmar que esta é a condição do controlador de domínio.

Para obter mais informações sobre como remover AD DS, consulte [remover Active Directory Domain Services (nível 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) e [rebaixar controladores de domínio e domínios &#40;nível 200&#41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).

## <a name="ad-ds-removal-options-and-warnings"></a><a name="BKMK_RemovalOptionsPage"></a>Opções e Avisos de Remoção de AD DS
Se precisar de ajuda na página Opções de revisão, consulte Opções de revisão

Se o controlador de domínio hospeda funções adicionais, como uma função de servidor DNS ou um servidor de catálogo global, a seguinte página de aviso será exibida:

![Captura de tela da página avisos do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_Warnings.gif)

Clique em **Continuar remoção** para reconhecer que as funções adicionais só serão disponibilizadas depois que você clicar em **Avançar** para continuar.

Se você forçar a remoção de um controlador de domínio, todas as alterações de objeto Active Directory que não foram replicadas para outros controladores de domínio no domínio serão perdidas. Além disso, se o controlador de domínio hospedar funções de mestres de operações, o catálogo global ou a função de servidor DNS, as operações essenciais no domínio e na floresta poderão ser impactadas da seguinte forma. Antes de remover um controlador de domínio que hospeda qualquer função de mestre de operações, tente transferir a função para outro controlador de domínio. Se não for possível transferir a função, primeiro remova os Serviços de Domínio Active Directory desse computador e então use Ntdsutil.exe para executar a função. Use Ntdsutil no controlador de domínio que contém a função a ser executada; se possível, use um parceiro de replicação recente do mesmo site como esse controlador de domínio. Para saber mais sobre transferência e execução de funções de mestres de operações, consulte o [artigo 255504](https://go.microsoft.com/fwlink/?LinkId=80395) na Base de Dados de Conhecimento Microsoft. Caso o assistente não possa determinar se o controlador de domínio hospeda uma função de mestre de operações, execute o comando netdom.exe para determinar se esse controlador de domínio executa alguma função de mestre de operações.

-   Catálogo global: os usuários talvez tenham problemas ao fazer logon nos domínios da floresta. Antes de remover um servidor de catálogo global, verifique se há servidores de catálogo global suficientes na floresta e no site para atender aos logons de usuários. Se necessário, designe outro servidor de catálogo global e atualize clientes e aplicativos com as novas informações.

-   Servidor DNS: todos os dados DNS armazenados nas zonas integradas ao Active Directory serão perdidos. Após a remoção do AD DS, esse servidor DNS não poderá mais executar resolução de nomes para as zonas DNS que foram integradas ao Active Directory. Portanto, recomendamos que você atualize a configuração DNS de todos os computadores que, no momento, fazem referência ao endereço IP desse servidor DNS para resolução de nomes, usando o endereço IP de um novo servidor DNS.

-   Mestre de infraestrutura: clientes do domínio podem ter dificuldade para localizar objetos em outros domínios. Antes de continuar, transfira a função de mestre de infraestrutura para um controlador de domínio que não seja um servidor de catálogo global.

-   Mestre de RID: você pode ter problemas para criar novas contas de usuário, contas de computador e grupos de segurança. Antes de continuar, transfira a função de mestre de RID para um controlador de domínio no mesmo domínio desse controlador de domínio.

-   Emulador de PDC (controlador de domínio primário): as operações executadas pelo emulador de PDC, como atualizações de Política de Grupo e redefinições de senhas para contas não AD DS, não funcionarão adequadamente. Antes de continuar, transfira a função de mestre de emulador de PDC para um controlador de domínio que esteja no mesmo domínio desse controlador de domínio.

-   Mestre de esquema: você não poderá mais modificar o esquema dessa floresta. Antes de continuar, transfira a função de mestre de esquema para um controlador de domínio no domínio raiz da floresta.

-   Mestre de nomeação de domínio: você não poderá mais adicionar domínios ou removê-los dessa floresta. Antes de continuar, transfira a função de mestre de nomeação de domínio para um controlador de domínio no domínio raiz da floresta.

-   Todas as partições do diretório de aplicativos nesse controlador de domínio do Active Directory serão removidas. Se um controlador de domínio contiver a última réplica de uma ou mais partições do diretório de aplicativos, quando a operação de remoção for concluída, essas partições não existirão mais.

Tenha em mente que o domínio não existirá mais após a desinstalação dos Serviços de Diretório Active Directory do último controlador de domínio do domínio.

Se o controlador de domínio for um servidor DNS delegado para hospedar a zona DNS, a seguinte página fornecerá a opção de remover o servidor DNS da delegação de zona DNS.

![Captura de tela da página opções de remoção do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_RemovalOptions.gif)

Para obter mais informações sobre como remover AD DS, consulte [remover Active Directory Domain Services (nível 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) e [rebaixar controladores de domínio e domínios &#40;nível 200&#41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).

## <a name="new-administrator-password"></a><a name="BKMK_NewAdminPwdPage"></a>Nova Senha do Administrador
A página **nova senha do administrador** exige que você forneça uma senha para a conta de administrador do computador local, depois que o rebaixamento for concluído e o computador se tornar um servidor membro do domínio ou um computador do grupo de trabalho.

![Captura de tela da página nova senha do administrador do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_NewAdminPwd.gif)

Para obter mais informações sobre como remover AD DS, consulte [remover Active Directory Domain Services (nível 100)](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c) e [rebaixar controladores de domínio e domínios &#40;nível 200&#41;](Demoting-Domain-Controllers-and-Domains--Level-200-.md).

## <a name="review-options-page"></a><a name="BKMK_ConfirmRoleRemovalPage"></a>Página de opções de revisão
A página **Opções de revisão** fornece a possibilidade de exportar as definições de configuração para rebaixamento em um script do Windows PowerShell, assim você pode automatizar outros rebaixamentos. Clique em **Rebaixar** para remover AD DS.

![Captura de tela da página de opções de revisão final do assistente de configuração do Active Directory Domain Services.](media/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions/ADDS_RRW_ReviewOptions.gif)

