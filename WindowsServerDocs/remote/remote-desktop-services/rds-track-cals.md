---
title: Controlar suas Licenças de Acesso para Cliente de Serviços de Área de Trabalho Remota (RDS CALs)
description: Saiba como controlar CALs em sua implantação do RDS.
ms.topic: article
ms.assetid: 80d82d30-3ad0-4a8c-9a9b-2773c47eee19
author: lizap
ms.author: elizapo
ms.date: 05/11/2017
manager: dongill
ms.openlocfilehash: 7804b0339a9c086a6e68dd83d63b0da5ff292665
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954813"
---
# <a name="track-your-remote-desktop-services-client-access-licenses-rds-cals"></a>Controlar suas Licenças de Acesso para Cliente de Serviços de Área de Trabalho Remota (RDS CALs)

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2019, Windows Server 2016

É possível usar a ferramenta Gerenciador de Licenciamento de Área de Trabalho Remota para criar relatórios para acompanhar as CALs de RDS por Usuário que foram lançadas por um servidor de licenças de Área de Trabalho Remota.

> [!NOTE]
>  Se você estiver usando o Azure AD Domain Services em seu ambiente, a ferramenta Gerenciador de Licenciamento de Área de Trabalho Remota não funcionará para obter CALs por Usuário. Em vez disso, você precisa acompanhar o licenciamento manualmente, por meio de eventos de logon, sondagem de conexões ativas de Área de Trabalho Remota por meio do Agente de Conexão ou outro mecanismo que funciona para você.

Use as seguintes etapas para gerar um relatório de CALs por Usuário:

1. No Gerenciador de Licenciamento de Área de Trabalho Remota, clique com o botão direito do mouse no servidor de licença, clique em **Criar Relatório** e, em seguida, clique em **Uso de CAL por Usuário**.
2. Defina o escopo do relatório – selecione um dos seguintes:
   - Domínio inteiro – o domínio no qual o servidor de licença é um membro.
   - Unidade organizacional – qualquer UO dentro do domínio no qual o servidor de licença é um membro.
   - Domínio inteiro e todos os domínios confiáveis – pode incluir domínios em outras florestas. Se você selecionar esta opção, isso poderá aumentar o tempo necessário para criar o relatório.

   A seleção feita determina quais contas de usuário no AD DS são pesquisadas para obter informações de CAL por Usuário aos Serviços de Área de Trabalho Remota para gerar o relatório.
3. Clique em **Criar Relatório**. O relatório é criado e será exibida uma mensagem para confirmar que o relatório foi criado com êxito. Clique em **OK** para fechar a mensagem.

O relatório que você criou aparece na seção de relatórios sob o nó para o servidor de licença. Esse relatório fornece as seguintes informações:

- Data e hora em que o relatório foi criado
- O escopo do relatório (por exemplo, domínio, UO = Sales ou todos os domínios confiáveis)
- O número de CALs de RDS por Usuário que estão instaladas no servidor de licença
- O número de CALs por RDS por Usuário que foram emitidas pelo servidor de licença específico para o escopo do relatório

Você também pode salvar o relatório como um arquivo CSV em uma localização de pasta no computador. Para salvar o relatório, clique com o botão direito do mouse no relatório que você deseja salvar, clique em Salvar como e, em seguida, especifique o nome do arquivo e a localização para salvar o relatório.

Os relatórios que você cria são listados no nó de relatórios sob o nó para o servidor de licença no Gerenciador de Licenciamento de Área de Trabalho Remota. Se não precisar mais de um relatório, você poderá excluí-lo.
