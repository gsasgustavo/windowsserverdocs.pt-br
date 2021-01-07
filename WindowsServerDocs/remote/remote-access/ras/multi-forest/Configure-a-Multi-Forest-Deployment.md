---
title: Configure a Multi-Forest Deployment
description: Saiba como configurar uma implantação de várias florestas de acesso remoto em vários cenários possíveis.
manager: brianlic
ms.topic: article
ms.assetid: 3c8feff2-cae1-4376-9dfa-21ad3e4d5d99
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 0c66decd8b1704852c2ed3c62a185b877f7b88b8
ms.sourcegitcommit: 605a9b46b74b2c7a9116e631e902467ea02a6e70
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97965648"
---
# <a name="configure-a-multi-forest-deployment"></a>Configure a Multi-Forest Deployment

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Este tópico descreve como configurar uma implantação de várias florestas do Acesso Remoto em vários cenários possíveis. Todos os cenários pressupõem que o DirectAccess esteja implantado em uma única floresta chamada Forest1 e que você o esteja configurando para operar com uma nova floresta chamada Forest2.

## <a name="access-resources-from-forest2"></a><a name="AccessForest2"></a>Acessar recursos da Forest2
Neste cenário, o DirectAccess já está implantado na Forest1 e está configurado para permitir que os clientes da Forest1 acessem a rede corporativa. Por padrão, os clientes conectados via DirectAccess só podem acessar os recursos da Forest1 e não podem acessar nenhum servidor da Forest2.

#### <a name="to-enable-directaccess-clients-to-access-resources-from-forest2"></a>Para habilitar os clientes do DirectAccess a acessar os recursos da Forest2

1.  Se o sufixo DNS da Forest2 não fizer parte do sufixo DNS da Forest1, adicione regras de NRPT com os sufixos dos domínios na Forest2 e, opcionalmente, adicione os sufixos dos domínios na Forest2 à lista de pesquisa de sufixos DNS.

2.  Adicione os prefixos IPv6 internos relevantes na Forest2 se o IPv6 estiver implantado na rede interna.

## <a name="enable-clients-from-forest2-to-connect-via-directaccess"></a><a name="EnableForest2DA"></a>Habilitar clientes da Forest2 a se conectarem via DirectAccess
Neste cenário, você configura a implantação do Acesso Remoto para permitir que os clientes da Forest2 acessem a rede corporativa. Pressupõe-se que você tenha criado os grupos de segurança necessários para os computadores cliente na Forest2.

#### <a name="to-allow-clients-from-forest2-to-access-the-corporate-network"></a>Para permitir que os clientes da Forest2 acessem a rede corporativa

1.  Adicione o grupo de segurança dos clientes da Forest2.

2.  Se o sufixo DNS de Forest2 não fizer parte do sufixo DNS de Forest1, adicione regras NRPT com os sufixos do domínio dos clientes no Forest2 para habilitar o acesso aos controladores de domínio para autenticação e, opcionalmente, adicione os sufixos dos domínios em Forest2 à lista de pesquisa de sufixos DNS.

3.  Adicione os prefixos IPv6 internos na Forest2 para habilitar o DirectAccess a criar o túnel IPsec para os controladores de domínio para fins de autenticação.

4.  Atualize a lista de servidores de gerenciamento.

## <a name="add-entry-points-from-forest2"></a><a name="AddEPForest2"></a>Adicionar pontos de entrada da Forest2
Neste cenário, o DirectAccess está implantado em uma configuração multissite na Forest1, e você quer adicionar um servidor de acesso remoto, chamado DA2, da Forest2 como um ponto de entrada para a implantação multissite existente do DirectAccess.

#### <a name="to-add-a-remote-access-server-from-forest2-as-an-entry-point"></a>Para adicionar um servidor de acesso remoto da Forest2 como um ponto de entrada

1.  Verifique se o administrador do Acesso Remoto tem permissões suficientes para criar GPOs no domínio do DA2 e se ele é um administrador local no DA2.

2.  Adicione o DA2 como um ponto de entrada.

3.  Adicione regras de NRPT com os sufixos dos domínios na Forest2 para habilitar o acesso aos controladores de domínio para fins de autenticação e, opcionalmente, adicione os sufixos dos domínios na Forest2 à lista de pesquisa de sufixos DNS.

4.  Se necessário, adicione os prefixos IPv6 internos relevantes na Forest2 para habilitar o Acesso Remoto a estabelecer o túnel IPsec para os recursos corporativos e garantir o funcionamento correto das sondas de NCSI.

5.  Atualize a lista de servidores de gerenciamento.

## <a name="configure-otp-in-a-multi-forest-deployment"></a><a name="OTPMultiForest"></a>Configurar a OTP em uma implantação de várias florestas
Observe os seguintes termos ao configurar a OTP em uma implantação de várias florestas:

-   Raiz CA-The floresta (s) da árvore PKI principal.

-   Enterprise CA-All outras CAs.

-   O recurso Forest-The floresta que contém a CA raiz e é considerado como ' Gerenciando forest\domain '.

-   Conta Forest-All outras florestas na topologia.

O script do PowerShell, PKISync.ps1, é necessário para este procedimento. Consulte [AD CS: PKISync.ps1 Script for Cross-forest Certificate Enrollment (AD CS: script PKISync.ps1 para registro de certificado entre florestas)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff961506(v=ws.10)).

> [!NOTE]
> Este tópico inclui cmdlets do Windows PowerShell de exemplo que podem ser usados para automatizar alguns dos procedimentos descritos. Para obter mais informações, confira [Usando os Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).

### <a name="configure-cas-as-certificate-publishers"></a><a name="BKMK_CertPub"></a>Configurar ACs como editores de certificados

1.  Habilite o suporte à referência de LDAP em todas as ACs corporativas de todas as florestas executando o seguinte comando em um prompt de comando com privilégios elevados:

    ```
    certutil -setreg Policy\EditFlags +EDITF_ENABLELDAPREFERRALS
    ```

2.  Adicione todas as contas de computadores de ACs corporativas aos grupos de segurança Editores de Certificados do Active Directory em cada uma das florestas de contas.

3.  Reinicie todos os serviços certsvc em todos os computadores de ACs de todas as florestas executando o seguinte comando em um prompt de comando com privilégios elevados:

    ```
    net stop certsvc && net start certsvc
    ```

4.  Extraia o certificado de AC raiz executando o seguinte comando em um prompt de comando com privilégios elevados:

    ```
    certutil -config <Computer-Name>\<Root-CA-Name> -ca.cert <root-ca-cert-filename.cer>
    ```

    (Se você executar o comando na AC raiz, poderá omitir as informações de conexão,-config <Computer-Name>\\<root-CA-Name>)

    1.  Importe o certificado de AC raiz da etapa anterior para a AC da floresta de contas executando o seguinte comando em um prompt de comando com privilégios elevados:

        ```
        certutil -dspublish -f <root-ca-cert-filename.cer> RootCA
        ```

    2.  Conceder ao recurso modelos de certificado de floresta permissões de leitura/gravação para a \<Account Forest\> \\ conta de administrador do<\> .

    3.  Extraia todos os certificados de AC corporativa da floresta de recursos executando o seguinte comando em um prompt de comando com privilégios elevados:

        ```
        certutil -config <Computer-Name>\<Enterprise-CA-Name> -ca.cert <enterprise-ca-cert-filename.cer>
        ```

        (Se você executar o comando na AC raiz, poderá omitir as informações de conexão,-config <Computer-Name>\\<root-CA-Name>)

    4.  Importe os certificados de AC corporativa da etapa anterior para a AC da floresta de contas executando os seguintes comandos em um prompt de comando com privilégios elevados:

        ```
        certutil -dspublish -f <enterprise-ca-cert-filename.cer> NTAuthCA
        certutil -dspublish -f <enterprise-ca-cert-filename.cer> SubCA
        ```

    5.  Da lista de modelos de certificado emitidos, remova os modelos de certificado de OTP da floresta de contas.

### <a name="delete-and-import-otp-certificate-templates"></a><a name="BKMK_DelImp"></a>Excluir e importar modelos de certificado de OTP

1.  Exclua da floresta de contas, ou seja, da Forest2, os modelos de certificado de OTP.

2.  Copie os modelos de certificado e objetos Oid da floresta de recursos para cada uma das florestas de contas, usando os seguintes comandos do PowerShell:

    ```
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Template -cn <DA OTP registration authority template common name>.
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Template -cn <Secure DA OTP logon certificate template common name>.
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Oid -f
    ```

### <a name="publish-otp-certificate-templates"></a><a name="BKMK_Publish"></a>Publicar modelos de certificado de OTP

-   Emita os modelos de certificado que você acabou de importar em todas as ACs de florestas de contas.

### <a name="extract-and-synchronize-the-ca"></a><a name="BKMK_Extract"></a>Extrair e sincronizar a AC

1.  Extraia todos os certificados de AC corporativa das florestas de contas executando os seguintes comandos em um prompt de comando com privilégios elevados:

    ```
    certutil -config <Computer-Name>\<Enterprise-CA-Name> -ca.cert <enterprise-ca-cert-filename.cer>
    ```

2.  Sincronize as ACs entre florestas, das florestas de contas para a floresta de recursos, usando o seguinte comando do PowerShell:

    ```
    .\PKISync.ps1 -sourceforest <account forest DNS> -targetforest <resource forest DNS> -type CA -cn <enterprise CA sanitized name> -f
    ```

3.  Sincronize as ACs entre florestas, da floresta de recursos para as florestas de contas, usando o seguinte comando do PowerShell:

    ```
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type CA -cn <enterprise CA sanitized name> -f
    ```

## <a name="configuration-procedures"></a>Procedimentos de configuração
As seções a seguir contêm os procedimentos de configuração referentes às implantações dos cenários acima. Depois de concluir um procedimento, retorne ao cenário para continuar.

### <a name="add-nrpt-rules-and-dns-suffixes"></a><a name="NRPT_DNSSearchSuffix"></a>Adicionar regras de NRPT e sufixos DNS
Os clientes que se conectam via DirectAccess à rede corporativa usam a NRPT (Tabela de Políticas de Resolução de Nomes) para determinar qual servidor DNS deve ser usado para resolver o endereço dos diversos recursos. Isso permite que o cliente resolva endereços de recursos corporativos e o ajuda a manter uma classificação adequada 'dentro da rede corporativa/fora da rede corporativa', necessária para manter o funcionamento do DirectAccess. As ferramentas de configuração do DirectAccess detectam automaticamente o sufixo DNS raiz da Forest1 e o adicionam à tabela NRPT. Porém, os sufixos FQDN da Forest2 não são adicionados automaticamente à tabela NRPT e precisam ser adicionados manualmente pelo administrador do Acesso Remoto.

A lista de pesquisa de sufixos DNS permite que os clientes usem nomes de rótulos curtos em vez de FQDNs. As ferramentas de configuração do Acesso Remoto adicionam automaticamente todos os domínios da Forest1 à lista de pesquisa de sufixos DNS. Para habilitar os clientes a usar nomes de rótulos curtos para os recursos da Forest2, é preciso adicioná-los manualmente.

##### <a name="to-add-a-dns-suffix-to-the-nrpt-table-and-domain-suffixes-to-the-dns-suffix-search-list"></a>Para adicionar um sufixo DNS à tabela NRPT e sufixos de domínio à lista de pesquisa de sufixos DNS

1.  No painel central do Console de Gerenciamento de Acesso Remoto, na área **Etapa 3: Servidores de Infraestrutura**, clique em **Editar**.

2.  Na página **Servidor de Local de Rede**, clique em **Avançar**.

3.  Na página **DNS**, especifique na tabela os sufixos de nome adicionais que fazem parte da rede corporativa na Forest2. Em **Endereço do Servidor DNS**, especifique o endereço do servidor DNS manualmente ou clicando em **Detectar**. Se você não inserir o endereço, as novas entradas serão aplicadas como isenções NRPT. Em seguida, clique em **Próximo**.

4.  Opcional: na página **Lista de Pesquisa de Sufixos DNS**, adicione sufixos DNS inserindo um sufixo na caixa **Novo Sufixo** e clicando em **Adicionar**. Em seguida, clique em **Próximo**.

5.  Na página **Gerenciamento**, clique em **Concluir**.

6.  No painel central do Console de Gerenciamento de Acesso Remoto, clique em **Concluir**.

7.  Na caixa de diálogo **Avaliação do Acesso Remoto**, clique em **Aplicar**.

8.  Na caixa de diálogo **Aplicando Configurações do Assistente de Configuração de Acesso Remoto**, clique em **Fechar**.

### <a name="add-internal-ipv6-prefix"></a><a name="IPv6Prefix"></a>Adicionar prefixo IPv6 interno

> [!NOTE]
> A adição de um prefixo IPv6 interno só é relevante quando o IPv6 está implantado na rede interna.

O Acesso Remoto gerencia uma lista de prefixos IPv6 para recursos corporativos. Apenas os recursos com esses prefixos IPv6 podem ser acessados pelos clientes conectados via DirectAccess. Como o console de gerenciamento de acesso remoto e os comandos do Windows PowerShell adicionam automaticamente os prefixos IPv6 de Forest1 e podem não adicionar os prefixos de outras florestas, você deve adicionar manualmente os prefixos ausentes de Forest2.

##### <a name="to-add-an-ipv6-prefix"></a>Para adicionar um prefixo IPv6

1.  No painel central do Console de Gerenciamento de Acesso Remoto, na área **Etapa 2: Servidor de Acesso Remoto**, clique em **Editar**.

2.  No Assistente para Configuração do Servidor de Acesso Remoto, clique em **Configuração de Prefixo**.

3.  Na página **Configuração de Prefixo**, em **Prefixos IPv6 da rede interna**, adicione outros prefixos IPv6 separados por ponto e vírgula; por exemplo, 2001:db8:1::/64;2001:db8:2::/64. Em seguida, clique em **Próximo**.

4.  Na página **Autenticação**, clique em **Concluir**.

5.  No painel central do Console de Gerenciamento de Acesso Remoto, clique em **Concluir**.

6.  Na caixa de diálogo **Avaliação do Acesso Remoto**, clique em **Aplicar**.

7.  Na caixa de diálogo **Aplicando Configurações do Assistente de Configuração de Acesso Remoto**, clique em **Fechar**.

### <a name="add-client-security-groups"></a><a name="SGs"></a>Adicionar grupos de segurança de cliente
Para permitir que computadores cliente com Windows 8 do Forest2 acessem recursos por meio do DirectAccess, você deve adicionar o grupo de segurança do Forest2 à implantação de acesso remoto.

##### <a name="to-add-windows-8-client-security-groups"></a>Para adicionar grupos de segurança de cliente do Windows 8

1.  No painel central do Console de Gerenciamento de Acesso Remoto, na área **Etapa 1: Clientes Remotos**, clique em **Editar**.

2.  No Assistente de Instalação do Cliente do DirectAccess, clique em **Selecionar Grupos** e depois, na página **Selecionar Grupos**, clique em **Adicionar**.

3.  Na caixa de diálogo **Selecionar Grupos**, selecione os grupos de segurança que contêm computadores cliente do DirectAccess. Em seguida, clique em **Próximo**.

4.  Na página **Assistente de Conectividade de Rede**, clique em **Concluir**.

5.  No painel central do Console de Gerenciamento de Acesso Remoto, clique em **Concluir**.

6.  Na caixa de diálogo **Avaliação do Acesso Remoto**, clique em **Aplicar**.

7.  Na caixa de diálogo **Aplicando Configurações do Assistente de Configuração de Acesso Remoto**, clique em **Fechar**.

Para permitir que computadores cliente do Windows 7 do Forest2 acessem recursos por meio do DirectAccess quando o multissite estiver habilitado, você deverá adicionar o grupo de segurança do Forest2 à implantação de acesso remoto para cada ponto de entrada. Para obter informações sobre como adicionar grupos de segurança do Windows 7, consulte a descrição da página de **suporte do cliente** em 3,6. Habilite a implantação multissite.

### <a name="refresh-the-management-servers-list"></a><a name="RefreshMgmtServers"></a>Atualizar a lista de servidores de gerenciamento
O Acesso Remoto descobre automaticamente, em todas as florestas, os servidores de infraestrutura que contêm GPOs de configuração do DirectAccess. Caso o DirectAccess tenha sido implantado em um servidor da Forest1, o GPO de servidor será criado no respectivo domínio na Forest1. Se você tiver habilitado o acesso ao DirectAccess para clientes da Forest2, o GPO de cliente será criado em um domínio da Forest2.

O processo de descoberta automática de servidores de infraestrutura é necessário para permitir o acesso por meio do DirectAccess aos controladores de domínio e ao Microsoft Endpoint Configuration Manager. Você precisa iniciar o processo manualmente.

##### <a name="to-refresh-the-management-servers-list"></a>Para atualizar a lista de servidores de gerenciamento

1.  No Console de Gerenciamento de Acesso Remoto, clique em **Configuração** e depois, no painel **Tarefas**, clique em **Atualizar Servidores de Gerenciamento**.

2.  Na caixa de diálogo **Atualizando Servidores de Gerenciamento**, clique em **Fechar**.

