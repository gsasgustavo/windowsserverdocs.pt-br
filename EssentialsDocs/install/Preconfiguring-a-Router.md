---
title: Pré-configurando um Roteador
description: Descreve como usar o Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 9153ac90-bb0c-4b8d-93b2-e2121ed13636
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 79ffa14cfabc26afd87c0771f7412c98e661421d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626158"
---
# <a name="preconfiguring-a-router"></a>Pré-configurando um Roteador

>Aplica-se a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Em geral, uma nova instalação do sistema operacional requer um roteador habilitado para a Internet e um firewall para conexão da rede interna do cliente com a Internet. Se você fornecer um roteador como valor adicional com um servidor pré-configurado, será possível tomar medidas extras para pré-configurar o roteador e proporcionar uma melhor experiência do usuário.

 O roteador deve ter o DHCP ativado. O servidor deve ser atribuído a um endereço IP estático. Isso pode ser feito através de reservas DHCP de um endereço IP ou da atribuição de um endereço IP fora do intervalo de endereço DHCP.

 Você também deve predefinir as configurações de encaminhamento de porta no roteador para encaminhar as portas específicas da interface externa do roteador ao endereço do servidor na rede interna. A tabela a seguir lista a configuração recomendada.

|Definição de configuração|Detalhes|
|---------------------------|-------------|
|DHCP|Ativado|
|Encaminhamento de porta|Encaminhe as portas a seguir para o endereço do servidor:<br /><br /> -80 (para a configuração hospedada, use apenas 443)<br />-443|
|Suporte UPnP|Você deve habilitar o suporte a UPnP para fornecer a configuração de roteador mais fácil para o cliente e a melhor experiência do cliente durante a instalação.<br /><br /> **AVISO:** A arquitetura UPnP pode representar um risco de segurança se ela for deixada habilitada.|

 Além das configurações básicas de pré-configuração do roteador, é possível realizar as seguintes tarefas para fornecer uma experiência do usuário mais integrada para gerenciar o roteador:

-   Estenda o Dashboard fornecendo um suplemento do servidor que permite aos usuários gerenciar o roteador por meio de uma interface de usuário personalizada.

-   Estenda os alertas de integridade de modo que quaisquer alertas do roteador possam ser vistos no Visualizador de Alertas.

-   Se o roteador suportar diversas sub-redes, o endereço IP do servidor deverá ser enviado como um servidor DNS até DHCP.

-   Se o roteador tiver um recurso de controle de acesso integrado para &reg; os serviços de domínio Active Directory, você poderá automatizar a integração de Active Directory durante a configuração inicial do servidor. Você também deve expor esse recurso através do suplemento de gerenciamento do roteador no Dashboard.

> [!NOTE]
>  Para obter mais informações sobre como configurar conexões sem fio, consulte [Configurar Suporte a uma Rede Sem Fio](Configure-Support-for-a-Wireless-Network.md).

## <a name="see-also"></a>Consulte Também
 [Introdução com o Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) [criando e personalizando a imagem](Creating-and-Customizing-the-Image.md) [personalizações adicionais](Additional-Customizations.md) [preparando a imagem para](Preparing-the-Image-for-Deployment.md) [testar a implantação da experiência do cliente](Testing-the-Customer-Experience.md)