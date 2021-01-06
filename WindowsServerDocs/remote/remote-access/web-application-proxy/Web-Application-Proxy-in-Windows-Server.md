---
description: 'Saiba mais sobre: proxy de aplicativo Web no Windows Server'
ms.assetid: 0b3587b2-219f-43d8-88b4-1254eaa8b910
title: Proxy de aplicativo Web no Windows Server
ms.topic: article
ms.author: kgremban
author: eross-msft
ms.date: 12/10/2020
ms.openlocfilehash: 61f4a0aa79cb65f2c4c1bc11cd04d21b1088a243
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947912"
---
# <a name="web-application-proxy-in-windows-server"></a>Proxy de aplicativo Web no Windows Server

>Aplica-se a: Windows Server&reg; 2016

**Esse conteúdo é relevante para a versão local do proxy de aplicativo Web. Para habilitar o acesso seguro a aplicativos locais na nuvem, consulte o conteúdo de [proxy de aplicativo do AD do Azure](/azure/active-directory/manage-apps/application-proxy).**

O conteúdo desta seção descreve as novidades e alterações no proxy de aplicativo Web para o Windows Server 2016. Os novos recursos e as alterações listados aqui são os mais prováveis de ter o maior impacto à medida que você trabalha com a versão prévia.

## <a name="web-application-proxy-new-features"></a>Novos recursos do proxy de aplicativo Web

- Pré-autenticação para publicação de aplicativo básica HTTP

  O HTTP básico é o protocolo de autorização usado por muitos protocolos, incluindo o ActiveSync, para conectar clientes avançados, incluindo smartphones, com sua caixa de correio do Exchange. O proxy de aplicativo Web tradicionalmente interage com AD FS usando redirecionamentos que não tem suporte em clientes do ActiveSync. Essa nova versão do proxy de aplicativo Web fornece suporte para publicar um aplicativo usando HTTP básico habilitando o aplicativo HTTP a receber uma relação de confiança de terceira parte confiável sem declarações para o aplicativo para a Serviço de Federação.

  Para obter mais informações sobre a publicação básica HTTP, consulte [Publicando aplicativos usando AD FS pré-autenticação](../web-application-proxy/../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)

- Publicação do domínio curinga de aplicativos

  Para dar suporte a cenários como o SharePoint 2013, a URL externa para o aplicativo agora pode incluir um curinga para permitir que você publique vários aplicativos de dentro de um domínio específico, por exemplo, https://*. SP-apps. contoso. com. Isso simplificará a publicação de aplicativos do SharePoint.

- Redirecionamento de HTTP para HTTPS

  Para garantir que os usuários possam acessar seu aplicativo, mesmo que eles não digitem HTTPS na URL, o proxy de aplicativo Web agora dá suporte ao redirecionamento de HTTP para HTTPS.

- Publicação HTTP

  Agora é possível publicar aplicativos HTTP usando a pré-autenticação de passagem

- Publicação de aplicativos de gateway de Área de Trabalho Remota

  Para obter mais informações sobre o RDG no proxy de aplicativo Web, consulte [Publicando aplicativos com o SharePoint, Exchange e RDG](../web-application-proxy/Publishing-Applications-with-SharePoint,-Exchange-and-RDG.md)

- Novo log de depuração para melhorar a solução de problemas e o log de serviço aprimorado para a trilha de auditoria completa e tratamento de erro aprimorado

  Para obter mais informações sobre solução de problemas, consulte [Solucionando problemas de proxy de aplicativo Web](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))

- Aprimoramentos da interface do usuário Console do Administrador

- Propagação de endereço IP do cliente para aplicativos de back-end

## <a name="see-also"></a>Consulte Também

-   [Novidades no Windows Server 2016](../../../get-started/whats-new-in-windows-server-2016.md)

-   [Como publicar aplicativos usando a pré-autenticação do AD FS](../web-application-proxy/Publishing-Applications-using-AD-FS-Preauthentication.md)

-   [Como solucionar problemas de proxy de aplicativo Web](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))

