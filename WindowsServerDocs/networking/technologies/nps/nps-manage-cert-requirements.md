---
title: Configurar modelos de certificado para requisitos de PEAP e EAP
description: Este tópico fornece informações sobre como usar certificados com o servidor de políticas de rede e acesso remoto no Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 2af0a1df-5c44-496b-ab11-5bc340dc96f0
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 4f1680c37510a0a45dfc4ce1ce34ca62859a8f09
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97948982"
---
# <a name="configure-certificate-templates-for-peap-and-eap-requirements"></a>Configurar modelos de certificado para requisitos de PEAP e EAP

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Todos os certificados que são usados para autenticação de acesso à rede com \- segurança de camada de transporte \( EAP TLS, segurança de protocolo de autenticação \- \) extensível protegidas \- \( PEAP \- TLS \) e PEAP \- Microsoft Challenge Handshake Authentication Protocol versão 2 \( MS \- CHAP v2 \) devem atender aos requisitos para certificados X. 509 e trabalhar para conexões que usam SSL/TLS (camada de soquete seguro/segurança em nível de transporte). Os certificados de cliente e de servidor têm requisitos adicionais.

>[!IMPORTANT]
>Este tópico fornece instruções para configurar modelos de certificado. Para usar essas instruções, é necessário que você tenha implantado sua própria PKI de infraestrutura de chave pública \( \) com Active Directory serviços de certificados \( AD CS \) .

## <a name="minimum-server-certificate-requirements"></a>Requisitos mínimos de certificado do servidor

Com o PEAP \- MS \- CHAP v2, PEAP \- TLS ou EAP \- TLS como o método de autenticação, o NPS deve usar um certificado de servidor que atenda aos requisitos mínimos de certificado do servidor.

Os computadores cliente podem ser configurados para validar certificados de servidor usando a opção **validar certificado do servidor** no computador cliente ou no política de grupo.

O computador cliente aceita a tentativa de autenticação do servidor quando o certificado do servidor atende aos seguintes requisitos:

- O nome da entidade contém um valor. Se você emitir um certificado para o servidor que executa o NPS (servidor de diretivas de rede) que tem um nome de entidade em branco, o certificado não estará disponível para autenticar o NPS. Para configurar o modelo de certificado com um nome de entidade:

    1. Abra os Modelos de Certificado.
    2. No painel de detalhes, clique com o botão direito do mouse no modelo de certificado que você deseja alterar e clique em **Propriedades** .
    3. Clique na guia **nome da entidade** e, em seguida, clique em **criar com base nessa Active Directory informações**.
    4. Em **formato de nome da entidade**, selecione um valor diferente de **nenhum**.

- O certificado do computador no servidor se encadeia a uma AC (autoridade de certificação) raiz confiável e não falha em nenhuma das verificações executadas pelo CryptoAPI e que são especificadas na política de acesso remoto ou na diretiva de rede.

- O certificado de computador para o servidor NPS ou VPN é configurado com a finalidade de autenticação de servidor em extensões EKU (uso estendido de chave). (O identificador de objeto para autenticação de servidor é 1.3.6.1.5.5.7.3.1.)

- Configure o certificado do servidor com a configuração de criptografia necessária:

    1. Abra os Modelos de Certificado.
    2. No painel de detalhes, clique com o botão direito do mouse no modelo de certificado que você deseja alterar e clique em **Propriedades**.
    3. Clique na guia **criptografia** e certifique-se de configurar o seguinte:
       - **Categoria do provedor:** Provedor de armazenamento de chaves
       - **Nome do algoritmo:** RSA
       - **Provedores:** Provedor Microsoft Platform crypto
       - **Tamanho mínimo da chave:** 2048
       - **Algoritmo de hash:** SHA2
    4. Clique em **Avançar**.

- A extensão de nome alternativo da entidade (SubjectAltName), se usada, deve conter o nome DNS do servidor. Para configurar o modelo de certificado com o nome DNS (sistema de nomes de domínio) do servidor de registro:

    1. Abra os Modelos de Certificado.
    2. No painel de detalhes, clique com o botão direito do mouse no modelo de certificado que você deseja alterar e clique em **Propriedades** .
    3. Clique na guia **nome da entidade** e, em seguida, clique em **criar com base nessa Active Directory informações**.
    4. Em **incluir essas informações em nome de entidade alternativo**, selecione **nome DNS**.

Ao usar PEAP e EAP-TLS, o NPSs exibirá uma lista de todos os certificados instalados no repositório de certificados do computador, com as seguintes exceções:

- Os certificados que não contêm a finalidade de autenticação de servidor em extensões EKU não são exibidos.

- Os certificados que não contêm um nome de entidade não são exibidos.

- Os certificados de logon e de cartão inteligente com base no registro não são exibidos.

Para obter mais informações, consulte [implantar certificados de servidor para implantações com e sem fio 802.1 x](../../core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments.md).

## <a name="minimum-client-certificate-requirements"></a>Requisitos mínimos de certificado do cliente

Com EAP-TLS ou PEAP-TLS, o servidor aceita a tentativa de autenticação de cliente quando o certificado atende aos seguintes requisitos:

- O certificado do cliente é emitido por uma autoridade de certificação corporativa ou mapeado para uma conta de usuário ou computador no Active Directory Domain Services \( AD DS \) .

- O certificado de usuário ou computador no cliente encadeia a uma AC raiz confiável, inclui a finalidade de autenticação de cliente em extensões EKU \( o identificador de objeto para autenticação de cliente é 1.3.6.1.5.5.7.3.2 \) e não faz a falha das verificações executadas pelo CryptoAPI e especificadas na política de acesso remoto ou política de rede nem nas verificações de identificador de objeto de certificado especificadas na política de rede do NPS.

- O cliente 802.1 X não usa certificados baseados no registro que sejam certificados de logon de cartão inteligente ou protegidos por senha.

- Para certificados de usuário, a extensão SubjectAltName do nome alternativo da entidade \( \) no certificado contém o UPN do nome principal do usuário \( \) . Para configurar o UPN em um modelo de certificado:

    1. Abra os Modelos de Certificado.
    2. No painel de detalhes, clique com o botão direito do mouse no modelo de certificado que você deseja alterar e clique em **Propriedades**.
    3. Clique na guia **nome da entidade** e, em seguida, clique em **criar com base nessa Active Directory informações**.
    4. Em **incluir essas informações em nome de entidade alternativo**, selecione **\( UPN \) nome da entidade de usuário**.

- Para certificados de computador, a extensão SubjectAltName do nome alternativo \( \) da entidade no certificado deve conter o FQDN do nome de domínio totalmente qualificado \( \) do cliente, que também é chamado de *nome DNS*. Para configurar esse nome no modelo de certificado:

    1. Abra os Modelos de Certificado.
    2. No painel de detalhes, clique com o botão direito do mouse no modelo de certificado que você deseja alterar e clique em **Propriedades**.
    3. Clique na guia **nome da entidade** e, em seguida, clique em **criar com base nessa Active Directory informações**.
    4. Em **incluir essas informações em nome de entidade alternativo**, selecione **nome DNS**.

Com \- o PEAP TLS e o EAP \- TLS, os clientes exibem uma lista de todos os certificados instalados no snap-in de certificados, com as seguintes exceções:

- Os clientes sem fio não exibem certificados baseados no registro e de logon de cartão inteligente.

- Clientes sem fio e clientes VPN não exibem certificados protegidos por senha.

- Os certificados que não contêm a finalidade de autenticação de cliente em extensões EKU não são exibidos.


Para obter mais informações sobre o NPS, consulte [servidor de diretivas de rede (NPS)](nps-top.md).