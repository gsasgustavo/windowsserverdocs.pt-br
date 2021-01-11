---
title: Introdução ao cliente Web
description: Descreve como entrar no cliente Web da Área de Trabalho Remota.
ms.author: helohr
ms.date: 08/27/2019
ms.topic: article
author: Heidilohr
ms.localizationpriority: medium
ms.openlocfilehash: 7307a4daa3f620f4b7dfc5d0103f0e75715fc1d8
ms.sourcegitcommit: e57536e28902ae52d3040141bbd2aa00e91bbdd3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97644676"
---
# <a name="get-started-with-the-web-client"></a>Introdução ao cliente Web

O cliente Web da Área de Trabalho Remota permite usar um navegador da Web compatível para acessar recursos remotos da sua organização (aplicativos e áreas de trabalho) publicados pelo administrador. Será possível interagir com áreas de trabalho e aplicativos remotos, da mesma forma que com um PC local, independentemente da sua localização, sem precisar alternar para um PC desktop diferente. Após o administrador configurar os recursos remotos, para estar pronto para começar, será necessário apenas o domínio, nome de usuário, senha, a URL do seu administrador enviada a você e um navegador da Web com suporte.

>[!NOTE]
>Curioso sobre as novas versões para o cliente Web? Confira [O que há de novo para o cliente Web da Área de Trabalho Remota?](web-client-whatsnew.md)

## <a name="what-youll-need-to-use-the-web-client"></a>O que você precisará para usar o cliente Web

* Para o cliente Web, será necessário um PC executando o Windows, macOS, ChromeOS ou Linux. Não há suporte para dispositivos móveis no momento.
* Um navegador moderno, como o Microsoft Edge, Internet Explorer 11, Google Chrome, Safari ou Mozilla Firefox (v55.0 e posterior).
* A URL que seu administrador enviou a você.

>[!NOTE]
>A versão do Internet Explorer do cliente Web não tem áudio até presente momento.
>Safari pode exibir uma tela cinza se o navegador for redimensionado ou entrar em tela inteira várias vezes.

## <a name="start-using-the-remote-desktop-client"></a>Começar a usar o cliente da Área de Trabalho Remota

Para entrar no cliente, acesse a URL que o administrador lhe enviou. Na página de entrada, insira seu nome de usuário e domínio no formato ```DOMAIN\username```, insira sua senha e, em seguida, selecione **Entrar**.

>[!NOTE]
>Ao entrar no cliente Web, você concorda que seu PC está em conformidade com a política de segurança da sua organização.

Depois de entrar, o cliente levará você até a guia **Todos os recursos**, que contém todos os itens publicados para você em um ou mais grupos recolhíveis, como o grupo "Recursos de trabalho". Você verá vários ícones representando os aplicativos, áreas de trabalho ou pastas que contêm mais aplicativos ou áreas de trabalho que o administrador disponibilizou para o grupo de trabalho. É possível voltar a esta guia a qualquer momento para iniciar os recursos adicionais.

Para começar a usar um aplicativo ou área de trabalho, selecione o item que quer usar, insira o mesmo nome de usuário e senha que você usou para entrar no cliente Web, se for solicitado e, em seguida, selecione **Enviar**. Também é possível que seja exibida uma caixa de diálogo de consentimento para acessar recursos locais, como área de transferência e impressora. É possível optar por não redirecionar qualquer uma delas, ou selecione **Permitir** para usar as configurações padrão. Aguarde até que o cliente web estabeleça a conexão e, em seguida, comece a usar o recurso como você faria normalmente.

Quando tiver terminado, é possível encerrar a sessão selecionando o botão **Sair** na barra de ferramentas na parte superior da tela ou fechando a janela do navegador.

## <a name="web-client-keyboard-shortcuts"></a>Atalhos de teclado do cliente Web

A tabela a seguir descreve combinações de teclas alternativas para injetar teclas de atalho padrão do Windows na sessão remota.

|Tecla de atalho |Descrição |
|-------------|------------|
|(Windows) CTRL + ALT + END</br>(macOS) fn + control + option + delete|Injeta CTRL + ALT + Del na sessão remota.|
|ALT + F3       |Injeta a tecla Windows na sessão remota.|    

## <a name="printing-from-the-remote-desktop-web-client"></a>Imprimir a partir do cliente Web da Área de Trabalho Remota

Siga estas etapas para imprimir a partir do cliente Web:

1. Inicie o processo de impressão como faria normalmente no aplicativo do qual você quer imprimir.
2. Quando solicitado a escolher uma impressora, selecione **Impressora Virtual da Área de Trabalho Remota**.
3. Depois de escolher suas preferências, selecione **Imprimir**.
4. O navegador irá gerar um arquivo PDF do trabalho de impressão.
5. Você pode optar por abrir o PDF e imprimir o conteúdo na impressora local ou salvá-lo no PC para uso posterior.

## <a name="copy-and-paste-from-the-remote-desktop-web-client"></a>Copiar e colar a partir do cliente Web da Área de Trabalho Remota

O cliente Web atualmente oferece suporte para copiar e colar somente texto. Arquivos não podem ser copiados ou colados de e para o cliente Web. Além disso, somente é possível usar **Ctrl+C** e **Ctrl+V** para copiar e colar o texto.

## <a name="use-an-input-method-editor-ime-in-the-remote-session"></a>Usar um IME (Editor de Método de Entrada) na sessão remota

Siga estas etapas para usar um Editor de Método de Entrada para inserir caracteres complexos na sessão remota:

1. Selecione o ícone de engrenagem na barra de navegação para abrir o painel lateral de **Configurações**.
2. Defina a alternância **Habilitar Editor de Método de Entrada** como **Ativado**.
3. Escolha seu layout de teclado IME preferido no menu suspenso.

Você precisa ter um Editor de Método de Entrada instalado e habilitado na sessão remota.

## <a name="get-help-with-the-web-client"></a>Obter ajuda com o cliente Web

Caso tenha encontrado um problema que não pode ser resolvido com as informações deste artigo, é possível obter ajuda com o cliente Web enviando o endereço por email na página Sobre do cliente Web.
