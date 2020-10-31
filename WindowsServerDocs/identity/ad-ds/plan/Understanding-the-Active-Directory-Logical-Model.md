---
ms.assetid: 62708b2e-4090-4cf7-8ae6-a557f31f561f
title: Noções básicas do modelo lógico do Active Directory
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 0bc7b55e404172c785db03a640aceea056595fcf
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070928"
---
# <a name="understanding-the-active-directory-logical-model"></a>Noções básicas do modelo lógico do Active Directory

>Aplica-se a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Projetar sua estrutura lógica para Active Directory Domain Services (AD DS) envolve a definição das relações entre os contêineres em seu diretório. Essas relações podem ser baseadas em requisitos administrativos, como a delegação de autoridade, ou podem ser definidas por requisitos operacionais, como a necessidade de controlar a replicação.

Antes de projetar sua estrutura lógica de Active Directory, é importante entender o modelo lógico Active Directory. AD DS é um banco de dados distribuído que armazena e gerencia informações sobre recursos de rede, bem como dados específicos do aplicativo de aplicativos habilitados para diretório. AD DS permite que os administradores organizem elementos de uma rede (como usuários, computadores e dispositivos) em uma estrutura de confinamento hierárquica. O contêiner de nível superior é a floresta. Em florestas são domínios, e dentro de domínios são UOs (unidades organizacionais). Isso é chamado de modelo lógico porque é independente dos aspectos físicos da implantação, como o número de controladores de domínio necessários em cada topologia de domínio e rede.

## <a name="active-directory-forest"></a>Floresta do Active Directory
Uma floresta é uma coleção de um ou mais domínios Active Directory que compartilham uma estrutura lógica comum, esquema de diretório (definições de classe e atributo), configuração de diretório (informações de site e replicação) e catálogo global (recursos de pesquisa em toda a floresta). Os domínios na mesma floresta são automaticamente vinculados a relações de confiança transitivas bidirecionais.

## <a name="active-directory-domain"></a>Domínio do Active Directory
Um domínio é uma partição em uma floresta Active Directory. O particionamento de dados permite que as organizações repliquem dados somente para onde for necessário. Dessa forma, o diretório pode ser dimensionado globalmente em uma rede com largura de banda disponível limitada. Além disso, o domínio dá suporte a várias outras funções principais relacionadas à administração, incluindo:

-   Identidade de usuário em toda a rede. Os domínios permitem que as identidades de usuário sejam criadas uma vez e referenciadas em qualquer computador ingressado na floresta em que o domínio está localizado. Os controladores de domínio que compõem um domínio são usados para armazenar contas de usuário e credenciais de usuário (como senhas ou certificados) com segurança.

-   Autenticação. Os controladores de domínio fornecem serviços de autenticação para usuários e fornecem dados de autorização adicionais, como associações de grupo de usuários, que podem ser usados para controlar o acesso a recursos na rede.

-   Relações de confiança. Os domínios podem estender os serviços de autenticação para usuários em domínios fora de sua própria floresta por meio de relações de confiança.

-   Replicação. O domínio define uma partição do diretório que contém dados suficientes para fornecer serviços de domínio e, em seguida, os Replica entre os controladores de domínio. Dessa forma, todos os controladores de domínio são pares em um domínio e são gerenciados como uma unidade.

## <a name="active-directory-organizational-units"></a>Active Directory unidades organizacionais
As UOs podem ser usadas para formar uma hierarquia de contêineres em um domínio. As UOs são usadas para agrupar objetos para fins administrativos, como a aplicação de Política de Grupo ou delegação de autoridade. O controle (em uma UO e os objetos dentro dele) é determinado pelas listas de controle de acesso (ACLs) na UO e nos objetos da UO. Para facilitar o gerenciamento de um grande número de objetos, o AD DS dá suporte ao conceito de delegação de autoridade. Por meio da delegação, os proprietários podem transferir controle administrativo completo ou limitado sobre objetos para outros usuários ou grupos. A delegação é importante porque ajuda a distribuir o gerenciamento de um grande número de objetos em várias pessoas que são confiáveis para executar tarefas de gerenciamento.



