---
title: EAP (protocolo de autenticação extensível) para acesso à rede
description: Este tópico apresenta informações sobre as configurações padrão de EAP (Extensible Authentication Protocol) que você pode usar para configurar computadores baseados no Windows.
author: khdownie
ms.author: v-kedow
ms.topic: conceptual
ms.date: 12/28/2020
ms.openlocfilehash: a1db4a4fc78496068e3f0525de0f72d9dd569d06
ms.sourcegitcommit: e2dadc9b0c227a489a945bbc531aca5e101f18cd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97804348"
---
# <a name="extensible-authentication-protocol-eap-for-network-access"></a>EAP (protocolo de autenticação extensível) para acesso à rede

> Aplica-se a: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10, Windows 8.1

O EAP (protocolo de autenticação extensível) é uma estrutura arquitetônica que fornece extensibilidade para métodos de autenticação para tecnologias de acesso à rede protegidas comumente usadas, como o acesso sem fio baseado em IEEE 802.1 X, o acesso com fio baseado em IEEE 802.1 X e conexões de protocolo PPP (PPP), como VPN (rede virtual privada). O EAP não é um método de autenticação como o MS-CHAP v2, mas sim uma estrutura no cliente de acesso e no servidor de autenticação que permite aos fornecedores de rede desenvolver e instalar facilmente novos métodos de autenticação conhecidos como métodos EAP.

## <a name="authentication-methods"></a>Métodos de autenticação

Este tópico contém informações específicas sobre configuração dos seguintes métodos de autenticação em EAP. Observe que os métodos de autenticação EAP usados em métodos EAP encapsulados são comumente conhecidos como **métodos internos** ou **tipos de EAP**.

- **EAP protegido (PEAP)**

  Esta seção contém informações de configuração para os dois métodos EAP internos padrão fornecidos com o PEAP.

  - Protocolo EAP-TLS (Transport Layer Security)

     Aparecendo como **cartão inteligente ou outras propriedades de certificado** no sistema operacional, o EAP-TLS pode ser implantado como um método interno para PEAP ou como um método EAP autônomo. Quando é configurado como método de autenticação interno, as definições de configuração do EAP-TLS são idênticas às definições usadas para implantar o EAP-TLS como método externo, com a diferença de que ele é configurado para operar no PEAP. Para obter detalhes de configuração, consulte [cartão inteligente ou outros itens de configuração de propriedades de certificado](#smart-card-or-other-certificate-properties-configuration-items).

  - MS-CHAP v2 (EAP-Microsoft Challenge Handshake Authentication Protocol versão 2)

     EAP-MS-CHAP v2 de senha segura é um tipo de EAP que pode ser usado com o PEAP para autenticação de rede baseada em senha. O EAP-MsCHAP V2 também pode ser usado como um método autônomo para VPN, mas somente como um método interno de PEAP para sem fio.

- **Protocolo EAP-TTLS (Tunneled Transport Layer Security)**

- **EAP-SIM (Subscriber Identity Module), EAP- AKA (Authentication and Key Agreement), e EAP-AKA' (AKA Prime)**

  Permite a autenticação usando cartões SIM e é implementado quando um cliente adquire um plano de serviço de banda larga sem fio de uma operadora de rede móvel. Como parte do plano, o cliente normalmente recebe um perfil móvel que é pré-configurado para autenticação SIM.

  Este tópico fornece informações sobre o seguinte:

  - [Definições de configuração de EAP-SIM](#eap-sim-configuration-settings)
  - [Definições de configuração de EAP-AKA e EAP-AKA](#eap-aka-configuration-settings)

## <a name="eap-tls-peap-and-eap-ttls"></a>EAP-TLS, PEAP e EAP-TTLS

Você pode acessar as propriedades do EAP para acesso sem fio e com fio autenticado 802.1X das seguintes formas:

- Ao configurar as extensões das Políticas de Rede com Fio (IEEE 802.3) e das Políticas de Rede sem Fio (IEEE 802.11) na Política de Grupo.

- Ao configurar manualmente conexões com ou sem fio em computadores cliente.

Você pode acessar as propriedades do EAP para conexões VPN das seguintes formas:

- Usando o Kit de administração do Gerenciador de conexões (CMAK) para configurar as conexões VPN.

- Configurando manualmente conexões VPN em computadores cliente.

Por padrão, você pode definir configurações do EAP para os seguintes métodos de autenticação para acesso com fio autenticado 802.1X, acesso sem fio autenticado 802.1X e VPN:

- Microsoft: cartão inteligente ou outro certificado (EAP-TLS)
- Microsoft: EAP protegido (PEAP)
- Microsoft: EAP-TTLS

Além disso, o método de autenticação de rede MS-CHAP-V2 está disponível para VPN por padrão.

## <a name="protected-eap-properties-configuration-settings"></a>Definições de configuração de propriedades EAP protegidas

Esta seção lista as configurações que podem ser configuradas para EAP protegido.

   > [!IMPORTANT]
   > A implantação do mesmo tipo de método de autenticação para PEAP e EAP cria uma vulnerabilidade de segurança. Quando você implantar PEAP e EAP (que não é protegido), não use o mesmo tipo de autenticação. Por exemplo, se você implantar o PEAP-TLS, não implante também o EAP-TLS.

### <a name="verify-the-servers-identity-by-validating-the-certificate"></a>Verificar a identidade do servidor Validando o certificado

Este item especifica que o cliente verifica se os certificados de servidor apresentados ao computador cliente têm as assinaturas corretas, não expiraram e foram emitidos por uma autoridade de certificação (CA) raiz confiável. A configuração padrão é "Enabled". **Se você desabilitar essa caixa de seleção, os computadores cliente não poderão verificar a identidade dos servidores durante o processo de autenticação. Se a autenticação do servidor não ocorrer, os usuários ficarão expostos a riscos de segurança graves, incluindo a possibilidade de que os usuários possam se conectar inadvertidamente a uma rede não autorizada.**

### <a name="connect-to-these-servers"></a>Conectar-se a estes servidores

Este item permite que você especifique o nome para servidores de serviço RADIUS (RADIUS) que fornecem autenticação e autorização de rede. Observe que você deve digitar o nome **exatamente** como ele aparece no campo **assunto** de cada certificado de servidor RADIUS ou usar expressões regulares para especificar o nome do servidor. A sintaxe completa da expressão regular pode ser usada para especificar o nome do servidor, mas para diferenciar uma expressão regular com a cadeia de caracteres literal, você deve usar pelo menos um "" na cadeia de caracteres especificada. Por exemplo, você pode especificar nps.example.com para especificar o servidor RADIUS nps1.example.com ou nps2.example.com.

Mesmo que nenhum servidor RADIUS seja especificado, o cliente verificará se o certificado desse servidor foi emitido por uma autoridade de certificação raiz confiável.

Padrões:

- Com fio e sem fio = não habilitado
- VPN = habilitado

### <a name="trusted-root-certification-authorities"></a>Autoridades de Certificação Confiáveis

Este item lista as autoridades de certificação raiz confiáveis. A lista é criada a partir das CAs raiz confiáveis que estão instaladas no computador e nos repositórios de certificados do usuário. Você pode especificar quais certificados de autoridade de certificação raiz confiáveis que os suplicantes usarão para determinar se confiam em seus servidores, como seu servidor que executa o NPS ou o servidor de provisionamento. Se nenhuma autoridade de certificação raiz confiável for selecionada, o cliente 802.1X verificará se o certificado do computador do servidor RADIUS foi emitido por uma autoridade de certificação raiz confiável instalada. Se uma ou várias autoridades de certificação raiz confiável forem selecionadas, o cliente 802.1X verificará se o certificado do computador do servidor RADIUS foi emitido por uma autoridade de certificação raiz confiável selecionada. Mesmo que nenhuma autoridade de certificação raiz confiável esteja selecionada, o cliente verificará se o certificado do servidor RADIUS foi emitido por uma autoridade de certificação raiz confiável.

Se você tiver uma infraestrutura de chave pública (PKI) na sua rede e tiver usado uma autoridade de certificação para emitir certificados para os servidores RADIUS, seu certificado da autoridade de certificação será automaticamente adicionado à lista de autoridades de certificação raiz confiáveis.

Você também pode comprar um certificado de uma autoridade de certificação que não seja da Microsoft. Algumas das autoridades de certificação raiz confiáveis que não são da Microsoft fornecem softwares com os certificados comprados que instalam automaticamente o certificado no repositório de certificados **Autoridades de Certificação Raiz Confiáveis**. Nesse caso, a autoridade de certificação raiz confiável aparece automaticamente na lista de autoridades de certificação raiz confiáveis.

   > [!NOTE]
   > Não especifique um certificado de autoridade de certificação raiz confiável que ainda não esteja listado nos repositórios de certificados **Autoridades de Certificação Raiz Confiáveis** dos computadores clientes para o **Usuário Atual** e **Computador Local**. Se você designar um certificado que não esteja instalado nos computadores cliente, a autenticação falhará.

Padrão = não habilitado, nenhuma autoridade de certificação raiz confiável selecionada

### <a name="notifications-before-connecting"></a>Notificações antes da conexão

Este item especifica se o usuário será notificado se o nome do servidor ou o certificado raiz não for especificado ou se a identidade do servidor não puder ser verificada.

Por padrão, as seguintes opções são fornecidas:

- Caso 1: **Não pedir para o usuário autorizar novos servidores ou autoridades de certificação confiáveis** especifica que:

  - Se o nome do servidor não estiver na lista **Conectar a estes servidores**
  - ou o certificado raiz for localizado, mas não estiver selecionado na lista de **Autoridades de Certificação Raiz Confiáveis** em **Propriedades PEAP**
  - ou o certificado raiz não for localizado no computador

  o usuário não será notificado, e a tentativa de conexão irá falhar.

- Caso 2: **Informar o usuário se o nome do servidor ou certificado raiz não for especificado** especifica que:

  - Se o nome do servidor não estiver na lista **Conectar a estes servidores**
  - ou o certificado raiz for localizado, mas não estiver selecionado na lista de **Autoridades de Certificação Raiz Confiáveis** em **Propriedades PEAP**

  em seguida, o usuário será avisado se deseja aceitar o certificado raiz. Se o usuário aceitar o certificado, a autenticação continuará. Se o usuário rejeitar o certificado, a tentativa de conexão irá falhar. Nessa opção, se o certificado raiz não estiver presente no computador, o usuário não será notificado e as tentativas de conexão falharão.

- Caso 3: **informe ao usuário se a identidade do servidor não pode ser verificada** especifica se:

  - Se o nome do servidor não estiver na lista **Conectar a estes servidores**
  - ou o certificado raiz for localizado, mas não estiver selecionado na lista de **Autoridades de Certificação Raiz Confiáveis** em **Propriedades PEAP**
  - ou o certificado raiz não for localizado no computador

  em seguida, o usuário será avisado se deseja aceitar o certificado raiz. Se o usuário aceitar o certificado, a autenticação continuará. Se o usuário rejeitar o certificado, a tentativa de conexão irá falhar.

### <a name="select-authentication-method"></a>Selecionar método de autenticação

Este item permite que você selecione o tipo de EAP a ser usado com o PEAP para autenticação de rede. Por padrão, dois tipos de EAP estão disponíveis, **senha segura (EAP-MSCHAP v2)** e **cartão inteligente ou outro certificado (EAP-TLS)**. No entanto, o EAP é um protocolo flexível que permite a inclusão de métodos adicionais de EAP e não está restrito a esses dois tipos.

Para obter mais informações, consulte:

- [Itens de configuração de propriedades de senha segura (EAP-MSCHAP v2)](#secure-password-properties-configuration-items)

- [Cartões inteligentes ou outros itens de configuração de propriedades de certificado](#smart-card-or-other-certificate-properties-configuration-items)

Padrão = senha segura (EAP-MSCHAP v2)

### <a name="configure"></a>Configurar

Este item fornece acesso às configurações de propriedade para o tipo de EAP especificado. 

### <a name="enable-fast-reconnect"></a>Habilitar reconexão rápida

Habilita a capacidade de criar uma associação de segurança nova ou atualizada com mais eficiência ou em um número menor de viagens de ida e volta, no caso em que uma associação de segurança foi estabelecida anteriormente.

Para conexões VPN, a Reconexão Rápida usa a tecnologia IKEv2 para fornecer conectividade VPN contínua e consistente quando os usuários perdem temporariamente a conexão com a Internet. Os usuários que se conectam usando banda larga móvel sem fio terão mais benefícios com esse recurso.

Um exemplo desse benefício é um cenário comum em que um usuário está viajando em um trem, usa uma placa de banda larga móvel sem fio para se conectar à Internet e estabelece uma conexão VPN com a rede corporativa.

Toda vez que o trem passa por um túnel, a conexão com a Internet é perdida. Quando o trem está fora do túnel, a placa de banda larga móvel sem fio reconecta-se automaticamente à Internet.

A reconexão rápida restabelece automaticamente as conexões VPN ativas quando a conectividade com a Internet é restabelecida. Embora a reconexão possa levar vários segundos para ocorrer, ela é realizada de forma transparente para os usuários.

Padrão = habilitado

### <a name="enforce-network-access-protection"></a>Impor a proteção de acesso à rede

Esse item especifica que antes de as conexões com uma rede serem permitidas, as verificações de integridade do sistema são executadas em suplicantes de EAP para determinar se atendem aos requisitos de integridade do sistema.

Padrão = não habilitado

### <a name="disconnect-if-server-does-not-present-cryptobinding-tlv"></a>Desconectar se o servidor não tiver TLV com ligação de criptografia

Este item especifica que os clientes de conexão devem encerrar o processo de autenticação de rede se o servidor RADIUS não apresentar um TLV (tipo-tamanho-valor) de cryptobinding. O TLV com ligação de criptografia aumenta a segurança do túnel de TLS em PEAP combinando as autenticações de método interno e externo para que os invasores não consigam executar ataques man-in-the-middle redirecionando uma autenticação MS-CHAP v2 usando o canal PEAP.

Padrão = não habilitado

### <a name="enable-identity-privacy-windows-8-only"></a>Habilitar Privacidade de identidade (somente Windows 8)

Especifica se os clientes são configurados de modo que não possam enviar sua identidade antes de o cliente autenticar o servidor RADIUS e, como opção, fornece um local para digitar um valor de identidade anônima. Por exemplo, se você selecionar **Habilitar Privacidade de identidade** e digitar "convidado" como o valor de identidade anônima, a resposta de identidade para um usuário com identidade alice@example será guest@example . Se você selecionar **Habilitar Privacidade de identidade** , mas não fornecer um valor de identidade anônima, a resposta de identidade para o usuário alice@example será @example .

Essa configuração se aplica somente a computadores que executam o Windows 8 e versões anteriores.

Padrão = não habilitado

## <a name="secure-password-properties-configuration-items"></a>Itens de configuração de propriedades de senha de segurança

**A verificação usar automaticamente o nome de logon e a senha do Windows (e o domínio, se houver)** especifica que o nome de entrada e a senha do Windows atuais baseados no usuário são usados como credenciais de autenticação de rede.

Padrões:

- Com fio e sem fio = habilitado
- VPN = não habilitado

## <a name="smart-card-or-other-certificate-properties-configuration-items"></a>Cartões inteligentes ou outros itens de configuração de propriedades de certificado

Esta seção lista os itens que podem ser configurados para EAP-TLS.

### <a name="use-my-smart-card"></a>Usar meu cartão inteligente

Este item especifica que os clientes que fazem solicitações de autenticação devem apresentar um certificado de cartão inteligente para autenticação de rede.

Padrões:

- Com fio e sem fio = não habilitado
- VPN = habilitado

### <a name="use-a-certificate-on-this-computer"></a>Usar um certificado neste computador

Este item especifica que os clientes de autenticação devem usar um certificado localizado no repositório de certificados do **computador local** ou do **usuário atual** .

Padrões:

- Com fio e sem fio = habilitado
- VPN = não habilitado

### <a name="use-simple-certificate-selection-recommended"></a>Usar seleção de certificado simples (recomendado)

Este item especifica se o Windows filtra os certificados que são improvável de atender aos requisitos de autenticação. Isso serve para limitar a lista de certificados disponíveis ao solicitar que o usuário selecione um certificado.

Padrões:

- Com fio e sem fio = habilitado
- VPN = não habilitado

### <a name="advanced"></a>Avançado

Esse item abre a caixa de diálogo **Configurar seleção de certificado** . Para obter mais informações sobre como **Configurar a seleção de certificado**, consulte [configurar novos itens de configuração de seleção de certificado](#configure-new-certificate-selection-configuration-items).

### <a name="verify-the-servers-identity-by-validating-the-certificate"></a>Verificar a identidade do servidor validando o certificado

Este item especifica que o cliente verifica se os certificados de servidor apresentados ao computador cliente têm as assinaturas corretas, não expiraram e foram emitidos por uma autoridade de certificação (CA) raiz confiável. **Não desabilite essa caixa de seleção ou os computadores cliente não poderão verificar a identidade de seus servidores durante o processo de autenticação. Se a autenticação do servidor não ocorrer, os usuários ficarão expostos a riscos de segurança graves, incluindo a possibilidade de que os usuários possam se conectar inadvertidamente a uma rede não autorizada.**

Padrão = habilitado

### <a name="connect-to-these-servers"></a>Conectar-se a estes servidores

Esse item permite que você especifique o nome para servidores RADIUS que fornecem autenticação e autorização de rede. Observe que você deve digitar o nome **exatamente** como ele aparece no campo assunto de cada certificado de servidor RADIUS ou usar expressões regulares para especificar o nome do servidor. A sintaxe completa da expressão regular pode ser usada para especificar o nome do servidor, mas para diferenciar uma expressão regular com a cadeia de caracteres literal, você deve usar pelo menos um "" na cadeia de caracteres especificada. Por exemplo, você pode especificar nps.example.com para especificar o servidor RADIUS nps1.example.com ou nps2.example.com.

Mesmo que nenhum servidor RADIUS seja especificado, o cliente verificará se o certificado desse servidor foi emitido por uma autoridade de certificação raiz confiável.

Padrões:

- Com fio e sem fio = não habilitado
- VPN = habilitado

### <a name="trusted-root-certification-authorities"></a>Autoridades de certificação raiz confiáveis

Este item lista as **autoridades de certificação raiz confiáveis**. A lista é criada a partir das CAs raiz confiáveis que estão instaladas nos repositórios de certificados do computador e do usuário. Você pode especificar os certificados de autoridade de certificação raiz confiáveis que os suplicantes usarão para determinar se confiam em seus servidores, como seu servidor executando NPS ou o servidor de provisionamento. Se nenhuma autoridade de certificação raiz confiável for selecionada, o cliente 802.1X verificará se o certificado do computador do servidor RADIUS foi emitido por uma autoridade de certificação raiz confiável instalada. Se uma ou várias autoridades de certificação raiz confiável forem selecionadas, o cliente 802.1X verificará se o certificado do computador do servidor RADIUS foi emitido por uma autoridade de certificação raiz confiável selecionada.

Se você tiver uma infraestrutura de chave pública (PKI) na sua rede e tiver usado uma autoridade de certificação para emitir certificados para os servidores RADIUS, seu certificado da autoridade de certificação será automaticamente adicionado à lista de autoridades de certificação raiz confiáveis.

Você também pode comprar um certificado de uma autoridade de certificação que não seja da Microsoft. Algumas das autoridades de certificação raiz confiáveis que não são da Microsoft fornecem softwares com os certificados comprados que instalam automaticamente o certificado no repositório de certificados **Autoridades de Certificação Raiz Confiáveis**. Nesse caso, a autoridade de certificação raiz confiável aparece automaticamente na lista de autoridades de certificação raiz confiáveis. Mesmo que nenhuma autoridade de certificação raiz confiável esteja selecionada, o cliente verificará se o certificado do servidor RADIUS foi emitido por uma autoridade de certificação raiz confiável.

Não especifique um certificado de autoridade de certificação raiz confiável que ainda não esteja listado nos repositórios de certificados **Autoridades de Certificação Raiz Confiáveis** dos computadores clientes para o **Usuário Atual** e **Computador Local**.

   > [!NOTE]
   > Se você designar um certificado que não esteja instalado nos computadores cliente, a autenticação falhará.

Padrão = não habilitado, nenhuma autoridade de certificação raiz confiável selecionada.

### <a name="view-certificate"></a>Exibir certificado

Este item permite que você exiba as propriedades do certificado selecionado.

### <a name="do-not-prompt-user-to-authorize-new-servers-or-trusted-certification-authorities"></a>Não solicitar ao usuário autorização para novos servidores ou autoridades de certificação confiáveis

Este item impede que o usuário seja solicitado a confiar em um certificado de servidor se esse certificado estiver configurado incorretamente, ainda não for confiável ou ambos (se habilitado). É recomendável selecionar essa caixa de seleção para simplificar a experiência do usuário e impedi-lo de escolher inadvertidamente confiar em um servidor implantado por um invasor.

Padrão = não habilitado

### <a name="use-a-different-user-name-for-the-connection"></a>Usar um nome de usuário diferente para a conexão

Este item especifica se deve ser usado um nome de usuário para autenticação que seja diferente do nome de usuário no certificado.

Padrão = não habilitado

## <a name="configure-new-certificate-selection-configuration-items"></a>Configurar Nova Seleção de Certificado - itens de configuração

Use **Nova Seleção de Certificado** para configurar os critérios que os computadores clientes usam para selecionar automaticamente o certificado correto no computador cliente para fins de autenticação. Quando a configuração é fornecida aos computadores clientes da rede por meio de Políticas de Rede com Fio (IEEE 802.3), Políticas de Rede sem Fio (IEEE 802.11) ou pelo Kit de Administração do Gerenciador de conexões (CMAK) para VPN, os clientes são automaticamente provisionados com os critérios de autenticação especificados.

Esta seção lista os itens de configuração para a **nova seleção de certificado**, juntamente com uma descrição de cada um.

### <a name="certificate-issuer"></a>Emissor do certificado

Este item especifica se a filtragem do emissor do certificado está habilitada.

Padrão = não selecionado

### <a name="certificate-issuer-list"></a>ListaEmissor do Certificado

Usada para especificar um ou vários emissores para os certificados.

Lista os nomes de todos os emissores para os quais há certificados de autoridade de certificação presentes no repositório de certificados **Autoridades de Certificação Raiz Confiáveis** ou **Autoridades de Certificação Intermediárias** da conta do computador local.

- Inclui todas as autoridades de certificação raiz e intermediárias.

- Contém somente os emissores para os quais há certificados válidos correspondentes presentes no computador (por exemplo, certificados que não estejam expirados ou revogados).

A lista final de certificados permitidos para autenticação contém apenas aqueles que foram emitidos por um dos emissores selecionados nesta lista.

Padrão = nenhum selecionado

### <a name="extended-key-usage-eku"></a>Uso Estendido de Chave (EKU)

Você pode selecionar **todas as finalidades**, **autenticação de cliente**, **qualquer finalidade** ou qualquer combinação delas. Especifica que, quando uma combinação é selecionada, todos os certificados que satisfazem a pelo menos uma das três condições são considerados válidos para fins de autenticação do cliente no servidor. Se a filtragem EKU estiver habilitada, será necessário selecionar uma das opções; caso contrário, o controle do comando **OK** será desabilitado.

Padrão = não habilitado

### <a name="all-purpose"></a>Todas as Finalidades

Quando selecionado, esse item especifica que os certificados que têm o EKU de **todas as finalidades** são considerados certificados válidos para a finalidade de autenticar o cliente no servidor.

Padrão = selecionado quando o **uso estendido de chave (EKU)** é selecionado

### <a name="client-authentication"></a>Autenticação de cliente

Quando selecionado, esse item especifica que os certificados que têm o EKU de **autenticação de cliente** e a lista especificada de EKUs são considerados certificados válidos para a finalidade de autenticar o cliente para o servidor.

Padrão = selecionado quando o **uso estendido de chave (EKU)** é selecionado

### <a name="any-purpose"></a>Qualquer Finalidade

Quando selecionado, este item especifica que todos os certificados que têm qualquer EKU de **finalidade** e a lista especificada de EKUs são considerados certificados válidos para a finalidade de autenticar o cliente para o servidor.

Padrão = selecionado quando o **uso estendido de chave (EKU)** é selecionado

### <a name="add"></a>Adicionar

Esse item abre a caixa de diálogo **selecionar EKUs** , que permite adicionar EKUs padrão, personalizado ou específico do fornecedor à **autenticação do cliente** ou a qualquer lista de **finalidade** .

Padrão = nenhum EKU listado

### <a name="remove"></a>Remover

Este item remove o EKU selecionado da lista **autenticação do cliente** ou **qualquer finalidade** .

Padrão = N/D

   > [!NOTE]
   > Quando **Emissor de Certificado** e **Uso Estendido de Chave (EKU)** estão habilitados, somente os certificados que satisfazem às duas condições são considerados válidos para fins de autenticação do cliente no servidor.

## <a name="select-ekus"></a>Selecionar EKUs

Você pode selecionar um EKU na lista fornecida ou adicionar um novo.

| Item          | Detalhes |
| :------------ | :------ |
| **Adicionar**       | Abre a caixa de diálogo **Adicionar ou editar EKU** , que permite que você defina e adicione EKUs personalizado. Em **Selecione os EKUs da lista abaixo**, selecione um EKU na lista e clique em **OK** para adicionar o EKU à lista **Autenticação de Cliente** ou **Qualquer Finalidade**. |
| **Editar**      | Abre a caixa de diálogo **Adicionar ou editar EKU** e permite que você edite EKUs personalizado que você adicionou. Você não pode editar os EKUs padrão predefinidos. |
| **Removerr**    | Remove o EKU personalizado selecionado da lista de EKUs na caixa de diálogo **selecionar EKUs** . Você não pode remover os EKUs padrão predefinidos. |

## <a name="add-or-edit-eku"></a>Adicionar ou Editar EKU

| Item          | Detalhes |
| :------------ | :------ |
| **Insira o nome de EKU** | Fornece um local para digitar o nome do EKU personalizado. |
| **Insira o OID EKU** | Fornece um local para digitar o OID do EKU. Somente números, separadores e “.” são permitidos. É permitido inserir curingas. Nesse caso, todos os OIDs filhos na hierarquia são permitidos. Por exemplo, se você informar 1.3.6.1.4.1.311.*, serão permitidos 1.3.6.1.4.1.311.42 e 1.3.6.1.4.1.311.42.2.1 |

## <a name="ttls-configuration-items"></a>TTLS - itens de configuração

EAP-TTLS é um método de túnel EAP com base em padrões que oferece suporte à autenticação mútua e fornece um túnel seguro para autenticação de inclusão de cliente usando métodos EAP e outros protocolos legados. A adição de EAP-TTLS no Windows Server 2012 fornece apenas o suporte do lado do cliente, com a finalidade de dar suporte à interoperação com os servidores RADIUS mais comumente implantados que oferecem suporte a EAP-TTLS.

Esta seção lista os itens que podem ser configurados para EAP-TTLS.

### <a name="enable-identity-privacy-windows-8-only"></a>Habilitar Privacidade de identidade (somente Windows 8)

Este item especifica que os clientes estão configurados para que não possam enviar sua identidade antes que o cliente tenha autenticado o servidor RADIUS e, opcionalmente, forneça um local para digitar um valor de identidade anônima. Por exemplo, se você selecionar **Habilitar Privacidade de identidade** e digitar "convidado" como o valor de identidade anônima, a resposta de identidade para um usuário com alice@example identidade guest@example será. Se você selecionar **Habilitar Privacidade de identidade** , mas não fornecer um valor de identidade anônima, a resposta de identidade para o usuário alice@example será @example .

Essa configuração se aplica somente a computadores que executam o Windows 8.

Padrão = não habilitado

### <a name="connect-to-these-servers"></a>Conectar-se a estes servidores

Este item permite que você especifique o nome para servidores RADIUS que fornecem autenticação e autorização de rede. Observe que você deve digitar o nome **exatamente** como ele aparece no campo assunto de cada certificado de servidor RADIUS ou usar expressões regulares para especificar o nome do servidor. A sintaxe completa da expressão regular pode ser usada para especificar o nome do servidor. Mas para diferenciar uma expressão regular com a cadeia de caracteres literal, você deve usar pelo menos um * na cadeia de caracteres especificada. Por exemplo, você pode especificar nps*.exemplo.com para especificar o nps1.exemplo.com ou nps2.exemplo.com do servidor RADIUS. Mesmo que nenhum servidor RADIUS seja especificado, o cliente verificará se o certificado desse servidor foi emitido por uma autoridade de certificação raiz confiável.

Padrão = nenhum

### <a name="trusted-root-certification-authorities"></a>Autoridades de Certificação Confiáveis

Este item lista as **autoridades de certificação raiz confiáveis**. A lista é criada a partir das CAs raiz confiáveis que estão instaladas nos repositórios de certificados do computador e do usuário. Você pode especificar os certificados de autoridade de certificação raiz confiáveis que os suplicantes usarão para determinar se confiam em seus servidores, como seu servidor executando NPS ou o servidor de provisionamento. Se nenhuma autoridade de certificação raiz confiável for selecionada, o cliente 802.1X verificará se o certificado do computador do servidor RADIUS foi emitido por uma autoridade de certificação raiz confiável instalada. Se uma ou várias autoridades de certificação raiz confiável forem selecionadas, o cliente 802.1X verificará se o certificado do computador do servidor RADIUS foi emitido por uma autoridade de certificação raiz confiável selecionada. Mesmo que nenhuma autoridade de certificação raiz confiável esteja selecionada, o cliente verificará se o certificado do servidor RADIUS foi emitido por uma autoridade de certificação raiz confiável.

Se você tiver uma infraestrutura de chave pública (PKI) na sua rede e tiver usado uma autoridade de certificação para emitir certificados para os servidores RADIUS, seu certificado da autoridade de certificação será automaticamente adicionado à lista de autoridades de certificação raiz confiáveis. Se a opção for selecionada, seu certificado de autoridade de certificação raiz será instalado em um computador cliente quando os computadores forem associados ao domínio.

Você também pode comprar um certificado de uma autoridade de certificação que não seja da Microsoft. Algumas das autoridades de certificação raiz confiáveis que não são da Microsoft fornecem softwares com os certificados comprados que instalam automaticamente o certificado no repositório de certificados **Autoridades de Certificação Raiz Confiáveis**. Nesse caso, a autoridade de certificação raiz confiável aparece automaticamente na lista de autoridades de certificação raiz confiáveis.

Não especifique um certificado de autoridade de certificação raiz confiável que ainda não esteja listado nos repositórios de certificados **Autoridades de Certificação Raiz Confiáveis** dos computadores clientes para o **Usuário Atual** e **Computador Local**.

   > [!NOTE]
   > Se você designar um certificado que não esteja instalado nos computadores cliente, a autenticação falhará.

Padrão = não habilitado, nenhuma autoridade de certificação raiz confiável selecionada

### <a name="do-not-prompt-user-if-unable-to-authorize-server"></a>Não perguntar ao usuário se não puder autorizar o servidor

Este item especifica (quando não selecionado) que se a validação do certificado do servidor falhar devido a qualquer uma das seguintes razões, o usuário receberá uma solicitação para aceitar ou rejeitar o servidor:

- Um certificado raiz para o certificado do servidor não é encontrado ou selecionado na lista **Autoridades de Certificação Raiz Confiáveis**.
- Um ou mais certificados raiz intermediários na cadeia de certificados não são encontrados.
- O nome do assunto no certificado do servidor não corresponde a nenhum dos servidores especificados na lista **Conectar-se a estes servidores**.

Padrão = não selecionado

### <a name="select-a-non-eap-method-for-authentication"></a>Selecionar um método não EAP para autenticação

Especifica se um tipo não EAP ou EAP é usado para autenticação. Se **selecionar um método não EAP para autenticação** estiver selecionado, **Selecione um método EAP para autenticação** está desabilitado. Se a opção **Selecionar um método não EAP para autenticação** for selecionada, os seguintes tipos de autenticação não EAP serão fornecidos na lista suspensa:

- PAP
- CHAP
- MS-CHAP
- MS-CHAP v2

Padrões:

- Selecionar um método não EAP para autenticação = habilitado
- Tipo não EAP = PAP

### <a name="automatically-use-my-windows-logon-name-and-password"></a>Usar automaticamente o meu nome e a minha senha de logon do Windows

Quando habilitado, este item usa as credenciais de entrada do Windows. Esta marca de seleção é habilitada somente quando **MS-CHAP v2** é selecionado na lista suspensa **Selecionar um método não EAP para autenticação**. **Usar automaticamente meu nome de logon e senha do Windows** está desabilitado para os tipos de autenticação **PAP**, **CHAP** e **MS-CHAP** .

### <a name="select-an-eap-method-for-authentication"></a>Selecionar um método EAP para autenticação

Este item especifica se um tipo de EAP ou um tipo não EAP é usado para autenticação. Se **selecionar um método EAP para autenticação** estiver selecionado, **Selecione um método não EAP para autenticação** está desabilitado. Se a opção **Selecionar um método não EAP para autenticação** for selecionada, os seguintes tipos de autenticação não EAP serão fornecidos por padrão na lista suspensa:

- Microsoft: Cartão Inteligente ou outro Certificado
- Microsoft: MS-CHAP v2
- MS-CHAP
- MS-CHAP v2

   > [!NOTE]
   > A lista suspensa **selecionar um método EAP para autenticação** enumerará todos os métodos EAP instalados no servidor, com exceção dos métodos **PEAP** e de túnel **rápido** . Os tipos EAP são listados na ordem em que são descobertos pelo computador.

### <a name="configure"></a>Configurar

Abre a caixa de diálogo de propriedades do tipo EAP especificado. Para obter detalhes sobre os tipos de EAP padrão, consulte itens de configuração de [Propriedades de cartão inteligente ou outros itens de configuração de propriedade de certificado](#smart-card-or-other-certificate-properties-configuration-items) ou de [senha segura (EAP-MSCHAP v2)](#secure-password-properties-configuration-items).

## <a name="eap-sim-configuration-settings"></a>Definições de configuração de EAP-SIM

O EAP-SIM é usado na distribuição de chaves de sessão e autenticação para sistemas GSM (Global System for Mobile Communications). EAP-SIM é definido em RFC 4186.

A tabela a seguir lista as definições de configuração para EAP-SIM.

| Item                                                                           | Descrição |
| :----------------------------------------------------------------------------- | :---------- |
| **Usar chaves de Criptografia fortes**                                                     | Se selecionada, especifica que o perfil usa criptografia forte. |
| **Não revelar a identidade real no servidor quando a identidade do pseudônimo estiver disponível** | Quando habilitada, força o cliente a falhar na autenticação quando as solicitações do servidor por identidade permanente no cliente têm uma identidade de pseudônimo. As identidades de pseudônimos são usadas na privacidade de identidades, de modo que o identidade real ou permanente de um usuário não seja revelada durante a autenticação. |
| **Habilitar uso de realms**                                                     | Fornece um local para digitação do nome do realm. Se esse campo for deixado em branco com a **habilitação do uso de territórios** selecionados, o realm será derivado da IMSI (identidade do assinante móvel internacional) usando o realm 3GPP.org, conforme descrito no projeto de parceria de 3ª geração (3GPP) Standard 23, 3 v 6.8.0. |
| **Especificar um realm**                                                            | Fornece um local para digitar o nome do Realm |

## <a name="eap-aka-configuration-settings"></a>Definições de configuração de EAP-AKA

EAP-AKA para UMTS (Universal Mobile Telecommunications System) é usado na distribuição de chaves de sessão e autenticação usando USIM (Universal Subscriber Identity Module) UMTS. EAP-AKA é definido em RFC 4187.

A tabela a seguir lista as definições de configuração para EAP-AKA.

| Item                                                                           | Descrição |
| :----------------------------------------------------------------------------- | :---------- |
| **Não revelar a identidade real no servidor quando a identidade do pseudônimo estiver disponível** | Quando habilitada, força o cliente a falhar na autenticação quando as solicitações do servidor por identidade permanente no cliente têm uma identidade de pseudônimo. As identidades de pseudônimos são usadas na privacidade de identidades, de modo que o identidade real ou permanente de um usuário não seja revelada durante a autenticação. |
| **Habilitar uso de realms**                                                     | Fornece um local para digitação do nome do realm. Se esse campo for deixado em branco com a **habilitação do uso de territórios** selecionados, o realm será derivado da IMSI (identidade do assinante móvel internacional) usando o realm 3GPP.org, conforme descrito no projeto de parceria de 3ª geração (3GPP) Standard 23, 3 v 6.8.0. |
| **Especificar um realm**                                                            | Fornece um local para digitação do nome do realm. |

## <a name="eap-aka-configuration-settings"></a>Definições de configuração de EAP-AKA

EAP- AKA' é uma versão modificada de EAP-AKA, usada para conceder acesso a redes com base em 3GPP usando padrões que não sejam 3GPP, como:

- WiFi - às vezes chamada de fidelidade sem fio

- EVDO (Evolution-Data Optimized)

- WiMax (Worldwide Interoperability for Microwave Access)

EAP-AKA' é definido em RFC 5448.

A tabela a seguir lista as definições de configuração para EAP-AKA '.

| Item                                                                           | Descrição |
| :----------------------------------------------------------------------------- | :---------- |
| **Não revelar a identidade real no servidor quando a identidade do pseudônimo estiver disponível** | Quando habilitada, força o cliente a falhar na autenticação quando as solicitações do servidor por identidade permanente no cliente têm uma identidade de pseudônimo. As identidades de pseudônimos são usadas na privacidade de identidades, de modo que o identidade real ou permanente de um usuário não seja revelada durante a autenticação. |
| **Habilitar uso de realms**                                                     | Fornece um local para digitação do nome do realm. Se esse campo for deixado em branco com a **habilitação do uso de territórios** selecionados, o realm será derivado da IMSI (identidade do assinante móvel internacional) usando o realm 3GPP.org, conforme descrito no projeto de parceria de 3ª geração (3GPP) Standard 23, 3 v 6.8.0. |
| **Especificar um realm**                                                            | Fornece um local para digitação do nome do realm. |
| **Ignorar incompatibilidade de nome de rede**                                               | O cliente compara o nome da rede conhecido com o nome enviado pelo servidor RADIUS durante a autenticação. Se houver incompatibilidade, será ignorada se essa opção for selecionada. Se não estiver selecionada, haverá falha de autenticação. |
| **Habilitar Reautenticação Rápida**                                               | Especifica que a reautenticação rápida está habilitada. Esse recurso é útil quando a autenticação SIM é realizada com frequência. As chaves de criptografia derivadas da autenticação completa são reutilizadas. Como resultado, o algoritmo SIM não precisa ser executado em cada tentativa de autenticação, e o número de operações de rede resultantes das tentativas frequentes de autenticação é reduzido. |

## <a name="additional-resources"></a>Recursos adicionais

Para obter informações adicionais sobre as configurações sem fio autenticadas no Política de Grupo, consulte [Gerenciando as novas configurações de políticas de rede sem fio (IEEE 802,11)](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh994701(v=ws.11))

Para obter informações adicionais sobre configurações com fio autenticadas no Política de Grupo, consulte [Gerenciando as novas configurações de políticas de rede com fio (IEEE 802,3)](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831813(v=ws.11))

Para obter informações sobre configurações avançadas para acesso com fio autenticado e acesso sem fio autenticado, consulte [Advanced Security Settings for Wired and Wireless Network Policies](/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh994696(v=ws.11)).
