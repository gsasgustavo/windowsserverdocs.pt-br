---
title: Instalar a autoridade de certificação
description: Saiba como instalar Active Directory serviços de certificados para que você possa registrar um certificado de servidor em servidores que estejam executando o servidor de políticas de rede, o serviço de roteamento e acesso remoto ou ambos.
manager: brianlic
ms.topic: article
ms.assetid: 4acdc3ad-078e-45cc-b54c-e9456e0c90f5
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 1e5c093a0c465f1f29cc8fd4606928515ae24091
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98038546"
---
# <a name="install-the-certification-authority"></a>Instalar a autoridade de certificação

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para instalar Active Directory serviços de certificados (AD CS) para que você possa registrar um certificado do servidor em servidores que estejam executando o servidor de diretivas de rede (NPS), o serviço de roteamento e acesso remoto (RRAS) ou ambos.

> [!IMPORTANT]
> -   Antes de instalar Active Directory serviços de certificados, você deve nomear o computador, configurar o computador com um endereço IP estático e ingressar o computador no domínio. Para obter mais informações sobre como realizar essas tarefas, consulte o [Guia de rede](../../core-network-guide.md)do Windows Server 2016 Core.
> -   Para executar este procedimento, o computador no qual você está instalando o AD CS deve estar associado a um domínio no qual o AD DS (Serviços de Domínio Active Directory) esteja instalado.

A associação aos grupos **Administradores de Empresa** e **Admins. do Domínio** do domínio raiz é o mínimo exigido para executar este procedimento.

> [!NOTE]
> Para executar esse procedimento usando o Windows PowerShell, abra o Windows PowerShell e digite o comando a seguir e pressione ENTER.
>
> `Add-WindowsFeature Adcs-Cert-Authority -IncludeManagementTools`
>
> Após a instalação do AD CS, digite o comando a seguir e pressione ENTER.
>
> `Install-AdcsCertificationAuthority -CAType EnterpriseRootCA`

### <a name="to-install-active-directory-certificate-services"></a>Para instalar os Serviços de Certificados do Active Directory

> [!TIP]
> Se você quiser usar o Windows PowerShell para instalar Active Directory serviços de certificados, consulte [install-AdcsCertificationAuthority](/powershell/module/adcsdeployment/install-adcscertificationauthority) para obter cmdlets e parâmetros opcionais.

1.  Faça logon como membro do grupo Administradores de Empresa e do grupo Admins. do Domínio do domínio raiz.

2.  No Gerenciador do Servidor, clique em **Gerenciar** e depois em **Adicionar Funções e Recursos**. O Assistente para Adicionar Funções e Recursos é aberto.

3.  Em **Antes de Começar**, clique em **Avançar**.

    > [!NOTE]
    > A página **Antes de Começar** do Assistente para Adicionar Funções e Recursos não é exibida quando você marca a opção **Ignorar esta página por padrão** quando o Assistente para Funções e Recursos foi executado.

4.  Em **Selecionar Tipo de Instalação**, verifique se **Instalação baseada em função ou recurso** está marcada e clique em **Avançar**.

5.  Em **Selecionar servidor de destino**, verifique se **Selecionar um servidor no pool de servidores** está marcada. Em **Pool de Servidores**, verifique se o computador local está selecionado. Clique em **Próximo**.

6.  Em **selecionar funções de servidor**, em **funções**, selecione **Active Directory serviços de certificados**. Quando for solicitado a adicionar os recursos necessários, clique em **Adicionar recursos** e, em seguida, clique em **Avançar**.

7.  Em **selecionar recursos**, clique em **Avançar**.

8.  Em **Active Directory serviços de certificados**, leia as informações fornecidas e clique em **Avançar**.

9. Em **Confirmar seleções de instalação**, clique em **Instalar**. Não feche o assistente durante o processo de instalação. Quando a instalação for concluída, clique em **configurar Active Directory serviços de certificados no servidor de destino**. O assistente de configuração do AD CS é aberto. Leia as informações de credenciais e, se necessário, forneça as credenciais para uma conta que seja membro do grupo Administradores de empresa. Clique em **Próximo**.

10. Em **serviços de função**, clique em **autoridade de certificação** e em **Avançar**.

11. Na página **tipo de instalação** , verifique se **Enterprise CA** está selecionado e clique em **Avançar**.

12. Na página **especificar o tipo da autoridade de certificação** , verifique se **AC raiz** está selecionada e clique em **Avançar**.

13. Na página **especificar o tipo da chave privada** , verifique se **criar uma nova chave privada** está selecionado e clique em **Avançar**.

14. Na página **criptografia para autoridade de certificação** , mantenha as configurações padrão para CSP (**RSA # provedor de armazenamento de chaves de software da Microsoft**) e algoritmo de hash (**SHA2**) e determine o melhor comprimento de caractere de chave para sua implantação. Comprimentos de caracteres de chave grandes fornecem segurança ideal; no entanto, eles podem afetar o desempenho do servidor e podem não ser compatíveis com os aplicativos herdados. É recomendável que você mantenha a configuração padrão de 2048. Clique em **Próximo**.

15. Na página **nome da autoridade de certificação** , mantenha o nome comum sugerido para a autoridade de certificação ou altere o nome de acordo com seus requisitos. Verifique se você tem certeza de que o nome da autoridade de certificação é compatível com suas convenções de nomenclatura e fins, porque você não pode alterar o nome da autoridade de certificação depois de ter instalado o AD CS. Clique em **Próximo**.

16. Na página **período de validade** , em **especificar o período de validade**, digite o número e selecione um valor de hora (anos, meses, semanas ou dias). A configuração padrão de cinco anos é recomendada. Clique em **Próximo**.

17. Na página **banco de dados de CA** , em **especificar os locais do banco de dados**, especifique o local da pasta para o banco de dados do certificado e o log do banco de dados do certificado Se você especificar localizações diferentes do padrão, verifique se as pastas estão protegidas com ACLs (listas de controle de acesso) que impedem que usuários ou computadores não autorizados acessem os arquivos de log e o banco de dados da autoridade de certificação. Clique em **Próximo**.

18. Em **confirmação**, clique em **Configurar** para aplicar suas seleções e, em seguida, clique em **Fechar**.
