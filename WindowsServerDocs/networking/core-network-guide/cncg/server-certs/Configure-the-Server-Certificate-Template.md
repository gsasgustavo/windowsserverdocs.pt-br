---
title: Configurar o modelo de certificado do servidor
description: Saiba como configurar o modelo de certificado que Active Directory serviços de certificados usa como a base para certificados de servidor registrados em servidores na sua rede.
manager: brianlic
ms.topic: article
ms.assetid: 8ff610e2-43ca-407f-a828-06d9366e02f0
ms.author: lizross
author: eross-msft
ms.date: 08/07/2020
ms.openlocfilehash: 94db549130bfa8779739af49c477eca9c401b08f
ms.sourcegitcommit: f8da45df984f0400922a8306855b0adfdaec71af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98038896"
---
# <a name="configure-the-server-certificate-template"></a>Configurar o modelo de certificado do servidor

>Aplica-se a: Windows Server (Canal Semestral), Windows Server 2016

Você pode usar este procedimento para configurar o modelo de certificado que Active Directory &reg; serviços de certificados (AD CS) usa como base para certificados de servidor registrados em servidores na sua rede.

Ao configurar esse modelo, você pode especificar os servidores por Active Directory grupo que deve receber automaticamente um certificado de servidor do AD CS.

O procedimento a seguir inclui instruções para configurar o modelo para emitir certificados para todos os seguintes tipos de servidor:

- Servidores que executam o serviço de acesso remoto, incluindo servidores de gateway de RAS, que são membros do grupo de **Servidores RAS e ias** .
- Servidores que executam o serviço de servidor de diretivas de rede (NPS) que são membros do grupo de **Servidores RAS e ias** .

A associação aos grupos **Administradores de Empresa** e **Admins. do Domínio** do domínio raiz é o mínimo exigido para executar este procedimento.

### <a name="to-configure-the-certificate-template"></a>Para configurar o modelo de certificado

1.  Em CA1, em Gerenciador do Servidor, clique em **ferramentas** e, em seguida, clique em **autoridade de certificação**. O MMC (console de gerenciamento Microsoft) da autoridade de certificação é aberto.

2.  No MMC, clique duas vezes no nome da autoridade de certificação, clique com o botão direito do mouse em **modelos de certificado** e clique em **gerenciar**.

3.  O console modelos de certificado é aberto. Todos os modelos de certificado são exibidos no painel de detalhes.

4.  No painel de detalhes, clique no modelo de **servidor RAS e ias** .

5.  Clique no menu **ação** e, em seguida, clique em **duplicar modelo**. A caixa de diálogo **Propriedades** do modelo é aberta.

6.  Clique na guia **Segurança** .

7.  Na guia **segurança** , em **nomes de grupo ou de usuário**, clique em **Servidores RAS e ias**.

8.  Em **permissões para servidores RAS e ias**, em **permitir**, verifique se o **registro** está selecionado e marque a caixa de seleção **registro automático** . Clique em **OK** e feche o MMC modelos de certificado.

9.  No MMC da autoridade de certificação, clique em **modelos de certificado**. No menu **ação** , aponte para **novo** e clique em **modelo de certificado a ser emitido**. A caixa de diálogo **Ativar Modelos de Certificado** é aberta.

10. Em **habilitar modelos de certificado**, clique no nome do modelo de certificado que você acabou de configurar e, em seguida, clique em **OK**. Por exemplo, se você não alterou o nome do modelo de certificado padrão, clique em **cópia do servidor RAS e ias** e, em seguida, clique em **OK**.



