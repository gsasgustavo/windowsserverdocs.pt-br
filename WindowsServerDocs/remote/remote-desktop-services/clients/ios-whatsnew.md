---
title: Novidades do cliente para iOS
description: Saiba mais sobre as recentes alterações no cliente da Área de Trabalho Remota para iOS
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 11/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: beb97113165127c50c815ccca8a667a1654215fa
ms.sourcegitcommit: 5fc77b4325a18d8c22385d899b14fe724a662347
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361163"
---
# <a name="whats-new-in-the-ios-client"></a>Novidades do cliente para iOS

Atualizamos regularmente o [cliente da Área de Trabalho Remota para iOS](remote-desktop-ios.md), adicionando novos recursos e corrigindo problemas. Você encontrará as atualizações mais recentes nesta página.

## <a name="how-to-report-issues"></a>Como relatar problemas

Temos o compromisso de tornar o cliente da Área de Trabalho Remota para iOS o melhor possível, por isso valorizamos seus comentários. Você pode relatar problemas em **Ajuda** > **Relatar um Problema**.

## <a name="updates-for-version-1020"></a>Atualizações para a versão 10.2.0

*Data da publicação: 06/11/2020*

Nessa versão, solucionamos alguns problemas de compatibilidade com o iOS e o iPadOS 14. Além disso, fizemos as seguintes correções e atualizações de recurso:

- Foram solucionadas as falhas no iOS e no iPadOS que ocorriam quando a entrada era inserida por meio de um teclado.
- Foram adicionados os atalhos Cmd+S e Cmd+N para acessar os processos "Adicionar Workspace" e "Adicionar PC", respectivamente.
- Foi adicionado o atalho Cmd+F para invocar a interface do usuário de Pesquisa na Central de Conexões.
- Foram adicionados os comandos "Expandir Tudo" e "Recolher Tudo" à guia Workspaces.
- Foi resolvido um bug que causava um erro de protocolo 0xD06 quando o Outlook era executado como um aplicativo remoto.
- O teclado na tela agora desaparecerá quando você rolar pelos resultados da pesquisa na Central de Conexões.
- Foi atualizada a animação usada ao focalizar os ícones do workspace com um ponteiro de mouse ou trackpad no iPadOS 14.

## <a name="updates-for-version-1014"></a>Atualizações da versão 10.1.4

*Data da publicação: 06/11/2020*

Reunimos algumas correções de bug e pequenas atualizações de recurso para essa versão 10.1.4. Confira as novidades:

- Foi resolvido um problema em que o cliente relatava uma mensagem de erro 0x5000007 ao tentar se conectar a um servidor de Gateway de Área de Trabalho Remota.
- As senhas de conta de usuário atualizadas na interface do usuário da credencial agora são salvas após um logon bem-sucedido.
- Foi resolvido um problema em que a seleção múltipla e de intervalo com o mouse ou trackpad (Ctrl + clique e Shift + clique) não funcionavam de maneira consistente.
- Foi resolvido um bug em que os aplicativos exibidos na interface do usuário do alternador na sessão estavam fora de sincronia com a sessão remota.
- Foram feitas algumas alterações estéticas ao layout dos cabeçalhos de workspace da Central de Conexões.
- Foi aprimorada a visibilidade dos botões de teclado na tela para os panos de fundo escuros.
- Foi corrigido um bug de localização na caixa de diálogo desconectar.

## <a name="updates-for-version-1013"></a>Atualizações da versão 10.1.3

*Data da publicação: 06/11/2020*

Reunimos algumas correções de bug e atualizações de recurso para essa versão 10.1.3. Confira as novidades:

- O modo de entrada (modo Ponteiro do Mouse ou Toque) agora é global em todas as conexões de PC e de aplicativo remoto ativas.
- Foi corrigido um problema que impedia que o redirecionamento de microfone funcionasse consistentemente.
- Foi corrigido um bug que fazia com que a saída de áudio fosse reproduzida no fone de ouvido do iPhone em vez de no alto-falante interno.
- O cliente agora dá suporte à troca automática de saída de áudio entre os auto-falantes internos do iPhone ou do iPad, os alto-falantes Bluetooth e o Airpods.
- O áudio agora continua a ser reproduzido em segundo plano quando sai do cliente ou quando o dispositivo é bloqueado.
- O modo de entrada muda automaticamente para o modo Toque ao usar um mouse SwiftPoint em iPhones ou iPads (que não estejam executando o iPadOS versão 13.4 ou posterior).
- Foram corrigidos problemas de saída de gráficos que ocorriam quando o servidor era configurado para usar o modo de tela inteira do AVC444.
- Foram corrigidos alguns bugs de VoiceOver.
- A ação de percorrer uma panorâmica em uma sessão ampliada ao usar um mouse externo ou trackpad agora funciona de maneira diferente. Para aplicar panorâmica em uma sessão ampliada com um mouse ou trackpad externo, selecione o botão de panorâmica e, em seguida, arraste o cursor do mouse para longe enquanto mantém o botão do mouse pressionado. Para percorrer a panorâmica no modo Toque, pressione o botão de panorâmica e, em seguida, mova o dedo. A sessão ficará atrelada ao seu dedo e o acompanhará. No modo Ponteiro do Mouse, empurre o cursor do mouse virtual contra os lados da tela.

## <a name="updates-for-version-1012"></a>Atualizações para a versão 10.1.2

*Data da publicação 17/8/2020*

Nesta atualização, abordamos problemas que foram relatados na atualização da versão 10.1.1.

- Correção de uma falha que ocorreu para alguns usuários ao assinar um feed da Área de Trabalho Virtual do Windows usando autenticação não agenciada.
- Corrigido o layout de ícones do espaço de trabalho no iPhone X, iPhone XS e iPhone 11 Pro.

## <a name="updates-for-version-1011"></a>Atualizações da versão 10.1.1

*Data da publicação: 06/11/2020*

Aqui está o que incluímos nesta versão:

- Foi corrigido um bug que impedia a digitação em coreano.
- Foi adicionado suporte para as teclas F1 a F12, Home, End, PgUp e PgDn em teclados de hardware.
- Foi resolvido um bug que dificultava a movimentação do cursor do mouse para a parte superior da tela no modo em letterbox em dispositivos iPadOS.
- Foi resolvido um problema no qual pressionar Backspace após o espaço excluía dois caracteres.
- Foi corrigido um bug que fazia com que o cursor do mouse no iPadOS aparecesse sobre o cursor do mouse do cliente na Área de Trabalho Remota no modo "Tocar para Clicar".
- Foi resolvido um problema que impedia conexões a alguns servidores de Gateway de Área de Trabalho Remota (código de erro 0x30000064).
- Foi corrigido um bug que fazia com que o cursor do mouse fosse mostrado na interface do usuário do alternador na sessão em dispositivos iOS com o uso de um mouse SwiftPoint.
- Foi redimensionado o cursor do mouse do cliente de Área de Trabalho Remota para ser consistente com o fator de escala do cliente atual.
- O cliente agora verifica a conectividade de rede antes de iniciar um recurso de workspace ou uma conexão de computador.
- O pressionamento do botão de escape remapeado ou de Cmd+. agora cancela qualquer solicitação de credenciais.
- Adicionamos algumas animações e aperfeiçoamentos que aparecem quando você move o cursor do mouse em iPads executando o iPadOS 13.4 ou posterior.

## <a name="updates-for-version-1010"></a>Atualizações da versão 10.1.0

*Data da publicação: 06/11/2020*

Veja as novidades dessa versão:

- Se você estiver usando o iPadOS 13.4 ou posterior, agora poderá controlar a sessão remota com um mouse ou trackpad.
- Agora, o cliente dá suporte aos seguintes gestos do Apple Magic Mouse 2 e do Apple Magic Trackpad 2: clicar com o botão esquerdo do mouse, arrastar para a esquerda, clicar com o botão direito do mouse, arrastar para a direita, rolagem horizontal e vertical e zoom local.
- Para mouses externos, o cliente agora dá suporte aos gestos de clicar com o botão esquerdo do mouse, arrastar para a esquerda, clicar com o botão direito do mouse, arrastar para a direita, clicar com o botão central e rolar verticalmente.
- O cliente agora dá suporte a atalhos de teclado que usam as teclas Ctrl, Alt ou Shift com o mouse ou trackpad, incluindo seleção múltipla e de intervalo.
- O cliente agora dá suporte ao recurso "Toque para Clicar" para o trackpad.
- Atualizamos o gesto de clique com o botão direito do mouse do modo Ponteiro do Mouse para pressionar e manter pressionado (não pressionar, segurar e soltar). No cliente do iPhone, adicionamos um pouco de resposta tátil ao detectar o gesto de clique com o botão direito do mouse.
- Foi adicionada uma opção para desabilitar a imposição de NLA em **Configurações do iOS** > **Cliente da Área de Trabalho Remota**.
- O comando Control + Shift + Escape foi mapeado para Ctrl + Shift + Esc, em que o Escape é gerado usando uma tecla remapeada no iPadOS ou Command+.
- Command + F foi mapeado para Ctrl + F.
- Foi corrigido um problema em que o botão central do mouse do SwiftPoint não funcionava no iPadOS versão 13.3.1 ou anterior e no iOS.
- Foram corrigidos alguns bugs que impediam o cliente de reconhecer o URI "rdp:".
- Foi resolvido um problema em que a interface do usuário do alternador de imersão na sessão mostrava entradas de aplicativo desatualizadas se uma desconexão fosse iniciada pelo servidor.
- O cliente agora dá suporte à versão integrada do Azure Resource Manager da Área de Trabalho Virtual do Windows.

## <a name="updates-for-version-1007"></a>Atualizações para a versão 10.0.7

*Data da publicação: 29/4/2020*

Nesta atualização, adicionamos a capacidade de classificar a exibição de lista de computadores (disponível no iPhone) por nome ou horário da última conexão.

## <a name="updates-for-version-1006"></a>Atualizações para a versão 10.0.6

*Data da publicação: 31/3/2020*

É hora de uma atualização rápida com algumas correções de bugs. Veja as novidades dessa versão:

- Foram corrigidos diversos problemas de acessibilidade do VoiceOver.
- Corrigido um problema em que os usuários não podiam se conectar com credenciais de turco.
- As sessões exibidas na interface do usuário para alternativa agora são ordenadas por quando elas foram iniciadas.
- A seleção do botão Voltar na Central de Conexão agora leva você de volta para a última sessão ativa.
- Os mouses Swiftpoint agora são liberados ao alternar saindo do cliente para outro aplicativo.
- Melhor interoperabilidade com o serviço de área de trabalho virtual do Windows.
- Correção de falhas que estavam aparecendo no relatório de erros.

Agradecemos todos os comentários enviados para nós por meio da App Store, do aplicativo e do email. Além disso, agradecemos especialmente a todos que trabalharam conosco para diagnosticar problemas.

## <a name="updates-for-version-1005"></a>Atualizações da versão 10.0.5

*Data da publicação: 09/03/20*

Reunimos algumas correções de bug e atualizações de recurso para essa versão 10.0.5. Confira as novidades:

- Os arquivos RDP abertos agora são importados automaticamente (procure a alternância em Configurações gerais).
- Agora você pode abrir arquivos RDP baseados no iCloud que ainda não foram baixados no aplicativo Arquivos.
- Agora a sessão remota pode se estender embaixo do indicador Início em iPhones (procure a alternância nas configurações de Exibição).
- Adição de suporte para digitar caracteres compostos com vários pressionamentos de tecla, como é.
- Adição de suporte para o teclado flutuante na tela do iPad.
- Adição de suporte para ajustar as propriedades de câmeras redirecionadas em uma sessão remota.
- Correção de um bug no reconhecedor de gesto que fazia o cliente ficar sem resposta quando se conectava a uma sessão remota.
- Agora você pode entrar no modo Alternância de Aplicativos apenas deslizando o dedo para cima (exceto quando você está no modo Toque com a sessão estendida para a área do indicador Início).
- O indicador Início agora ficará oculto automaticamente quando conectado a uma sessão remota e será exibido novamente quando você tocar na tela.
- Adição de um atalho do teclado para acessar as configurações do aplicativo no Centro de Conexão ( **Command + ,** ).
- Adição de um atalho do teclado para atualizar todos os workspaces no Centro de Conexão ( **Command + R** ).
- Conexão do atalho do teclado do sistema para Escape quando conectado a uma sessão remota ( **Command + .** ).
- Correção de cenários em que o teclado na tela do Windows na sessão remota era muito pequeno.
- Implementação do foco de teclado automático em todo o Centro de Conexão para tornar a entrada de dados mais contínua.
- Pressionar **Enter** em uma solicitação de credenciais agora faz o prompt ser ignorado e o fluxo atual retomado.
- Correção de um cenário em que o cliente falhava ao pressionar Shift + Option + tecla de seta para a Esquerda, para Cima ou para Baixo.
- Correção de uma falha que ocorria ao remover um dispositivo SwiftPoint.
- Correção de outras falhas relatadas para nós pelos usuários desde a última versão.

Gostaríamos de agradecer todos que relataram bugs e trabalharam conosco para diagnosticar problemas.

## <a name="updates-for-version-1004"></a>Atualizações da versão 10.0.4

*Data da publicação: 03/02/20*

É hora de outra atualização! Queremos agradecer todos que relataram bugs e trabalharam conosco para diagnosticar problemas. Estas são as novidades dessa versão:

- Agora a interface do usuário de confirmação é mostrada ao excluir contas de usuário e gateways.
- A interface do usuário de pesquisa no Centro de Conexão foi ligeiramente refeita.
- A dica de nome de usuário, se existir, agora é mostrada na interface do usuário da solicitação de credenciais ao iniciar de um arquivo RDP ou URI.
- Correção de um problema em que o teclado na tela estendida se estendia embaixo do entalhe do iPhone.
- Correção de um bug em que teclados externos paravam de funcionar após serem desconectado e reconectados.
- Adição de suporte para a tecla Esc em teclados externos.
- Correção de um bug em que caracteres ingleses eram exibidos ao digitar caracteres chineses.
- Correção de um bug em que alguma entrada de chinês permanecia na sessão remota após a exclusão.
- Correção de outras falhas relatadas para nós pelos usuários desde a última versão.

Agradecemos todos os seus comentários enviados para nós por meio da App Store, de comentários no aplicativo e do email. Continuaremos nos concentrando em aprimorar esse aplicativo a cada versão.

## <a name="updates-for-version-1003"></a>Atualizações da versão 10.0.3

*Data da publicação: 16/01/20*

É 2020 e hora do nosso primeiro lançamento do ano, o que significa que há novos recursos e correções de bug. Veja o que está incluído nessa atualização:

- Suporte para iniciar conexões de arquivos RDP e URIs RDP.
- Os cabeçalhos do workspace agora podem ser recolhidos.
- Agora há suporte para a aplicação de zoom e panorâmica ao mesmo tempo no modo Ponteiro do Mouse.
- Um gesto de pressionar e segurar no modo Ponteiro do Mouse agora vai disparar um clique com o botão direito do mouse na sessão remota.
- Remoção do gesto de forçar toque para clicar com o botão direito do mouse no modo Ponteiro do Mouse.
- A tela de alternador na sessão agora dá suporte à desconexão, mesmo que nenhum aplicativo esteja conectado.
- Agora há suporte para light dismiss na tela de alternador na sessão.
- Computadores e aplicativos não são mais reordenados automaticamente na tela de alternador na sessão.
- Ampliação da área de teste de clique para o menu de reticências do modo de exibição de miniatura do computador.
- A página de configurações Dispositivos de Entrada agora contém um link para os dispositivos com suporte.
- Correção de um bug que fez a interface do usuário de permissões Bluetooth ser exibida repetidamente no momento da inicialização para alguns usuários.
- Correção de outras falhas relatadas para nós pelos usuários desde a última versão.

## <a name="updates-for-version-1002"></a>Atualizações da versão 10.0.2

*Data da publicação: 20/12/19*

Estamos trabalhando bastante para corrigir bugs e adicionar recursos úteis. Veja as novidades dessa versão:

- Suporte para entrada em japonês e chinês em teclados de hardware.
- A exibição de lista de computadores agora mostra o nome amigável da conta de usuário associada, se houver.
- A interface do usuário de permissões na experiência de primeira execução agora é renderizada corretamente no modo claro.
- Correção de uma falha que acontecia sempre que alguém pressionava as teclas Option e seta para cima ou para baixo ao mesmo tempo em um teclado de hardware.
- Atualização do layout de teclado na tela usado na interface do usuário de prompt de senha para facilitar a localização da tecla Barra invertida.
- Correção de outras falhas relatadas para nós pelos usuários desde a última versão.

## <a name="updates-for-version-1001"></a>Atualizações da versão 10.0.1

*Data da publicação: 15/12/19*

Veja as novidades dessa versão:

- Suporte para o serviço de Área de Trabalho Virtual do Windows.
- Atualização da interface do usuário do Centro de Conexão.
- Atualização da interface do usuário na sessão.

## <a name="updates-for-version-1000"></a>Atualizações para a versão 10.0.0

*Data da publicação: 13/12/2019*

Já faz mais de um ano desde a última atualização do Cliente de Área de Trabalho Remota para iOS. No entanto, estamos de volta com uma nova e empolgante atualização e haverá muito mais atualizações a serem feitas regularmente daqui em diante. Veja as novidades da versão 10.0.0:

- Suporte para o serviço de Área de Trabalho Virtual do Windows.
- Uma nova interface do usuário do centro de conexão.
- Uma nova interface do usuário na sessão que pode alternar entre computadores e aplicativos conectados.
- Novo layout para o teclado virtual auxiliar.
- Suporte ao teclado externo aprimorado.
- Suporte ao mouse Bluetooth SwiftPoint.
- Suporte ao redirecionamento de microfone.
- Suporte ao redirecionamento de armazenamento local.
- Suporte ao redirecionamento de câmera (disponível somente para Windows 10, versão 1809 ou posterior).
- Suporte para novos dispositivos iPhone e iPad.
- Suporte a temas claros e escuros.
- Controle se o seu telefone pode ser bloqueado quando conectado a um PC ou aplicativo remoto.
- Agora você pode recolher a barra de conexão em sessão pressionando e segurando o botão do logotipo da Área de Trabalho Remota.

## <a name="updates-for-version-8142"></a>Atualizações para a versão 8.1.42

*Data da publicação: 20/06/2018*

- Correção de bugs e melhorias de desempenho.

## <a name="updates-for-version-8141"></a>Atualizações para a versão 8.1.41

*Data da publicação: 28/03/2018*

- Atualizações para solucionar a correção de criptografia Oracle CredSSP descrita em CVE-2018-0886.
