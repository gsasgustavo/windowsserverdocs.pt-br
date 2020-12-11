# <a name="contributing-to-windows-server-technical-documentation"></a>Documentação técnica do Contribute para o Windows Server

Obrigado por seu interesse na documentação técnica do Windows Server! Agradecemos seus comentários, edições e adições a nossos documentos. Há dois locais separados onde mantemos o conteúdo técnico do Windows Server. Um dos locais é público (windowsserverdocs) enquanto o outro é privado (windowsserverdocs-PR). Quem você está determina em qual local você contribui:

- **Não sou um funcionário da Microsoft.** Como funcionário que não seja da Microsoft, você deve contribuir para o local público. Para obter informações sobre como fazer isso, continue lendo este artigo.

- **Sou um funcionário da Microsoft.** Como funcionário da Microsoft, você tem opções, com base no que está tentando fazer:

    - **Crie um artigo novo.** Para criar um novo artigo, você deve criar e configurar sua conta e ferramentas do GitHub, bifurcar e clonar o repositório windowsserverdocs-PR, configurar sua ramificação remota, criar o artigo e, finalmente, criar uma nova solicitação de pull para aprovação e publicação. Para estas instruções, consulte o artigo [criar novos artigos do Windows Server usando o GitHub e Visual Studio Code](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/create-new-using-github.md) .

    - **Faça grandes alterações em um artigo existente.** Para fazer alterações substanciais em um artigo existente, você pode seguir as instruções no artigo [Editar um servidor do Windows existente usando o GitHub e Visual Studio Code](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/edit-existing-using-github.md) .

    - **Faça alterações secundárias em um artigo existente.** Para fazer alterações secundárias em um artigo existente, você pode seguir as instruções contidas no artigo [atualizar artigos existentes do Windows Server usando um navegador da Web e o GitHub](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/github-browser-updates.md) .

## <a name="sign-a-cla"></a>Assinar um CLA

Todos os colaboradores que são **_não_* _ um funcionário da Microsoft devem [assinar um contrato de licenciamento de contribuição da Microsoft (CLA)](https://cla.microsoft.com/) antes de editar os repositórios da Microsoft. Se você já editou nos repositórios da Microsoft no passado, parabéns!
Você já concluiu essa etapa.

## <a name="editing-topics"></a>Editando tópicos

Tentamos tornar a edição de um arquivo público existente o mais simples possível.

### <a name="to-edit-a-topic"></a>Para editar um tópico

1. Vá para a página https://docs.microsoft.com/windows-server que você deseja atualizar e, em seguida, selecione _ * editar * *.

    ![Web do GitHub, mostrando o link editar](media/contribute-link.png)

2. Entre (ou Inscreva-se em) uma conta do GitHub.

    Você deve ter uma conta do GitHub para chegar à página que permite editar um tópico.

3. Selecione o ícone de **lápis** (na caixa vermelha) para editar o conteúdo.

    ![Web do GitHub, mostrando o ícone de lápis na caixa vermelha](media/pencil-icon.png)

4. Usando a linguagem de redução, faça as alterações no tópico. Para obter informações sobre como editar o conteúdo usando a redução, consulte:

    - **Se você estiver vinculado à organização da Microsoft no github:** [Guia do colaborador do Windows Server](https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/Contributor-guide)

    - **Se você for externo à Microsoft:** [redução de dominar](https://guides.github.com/features/mastering-markdown/)

5. Faça a alteração sugerida e, em seguida, selecione **Visualizar alterações** para verificar se ela parece correta.

    ![Web do GitHub, mostrando a guia Visualizar alterações](media/preview-changes.png)

6. Quando terminar de editar o tópico, role até a parte inferior da página, digite um nome descritivo para sua bifurcação e clique em **propor alteração de arquivo** para criar a bifurcação em sua conta do GitHub pessoal.

    ![Web do GitHub, mostrando o botão propor alteração de arquivo](media/propose-file-change.png)

    A tela **comparando alterações** é exibida para ver quais são as alterações entre a bifurcação e o conteúdo original.

7. Na tela **comparando alterações** , você verá se há problemas com o arquivo no qual você está fazendo check-in.

    Se não houver nenhum problema, você verá a mensagem, **capaz de Mesclar**.

    ![Web do GitHub, mostrando a tela comparando alterações](media/compare-changes.png)

8. Selecione **Criar solicitação de pull**.

    As solicitações de pull permitem que você informe aos outros sobre as alterações que você enviou para um Branch em um repositório no GitHub. Depois que uma solicitação de pull é aberta, você pode discutir e examinar as alterações potenciais com os colaboradores e adicionar confirmações de acompanhamento antes que suas alterações sejam mescladas no Branch base. Para obter mais informações, consulte [about pull requests](https://help.github.com/articles/about-pull-requests)

9. Insira um título e uma descrição para dar ao aprovador o contexto apropriado sobre o que está na solicitação.

10. Role até a parte inferior da página, certificando-se de que apenas os arquivos alterados estejam nessa solicitação de pull. Caso contrário, você pode substituir as alterações de outras pessoas.

11. Selecione **criar solicitação de pull** novamente para realmente enviar a solicitação de pull.

    A solicitação pull é enviada ao gravador do tópico e suas edições são revisadas. Se sua solicitação for aceita, suas atualizações serão publicadas.

## <a name="resources"></a>Recursos

- Você pode usar seu editor de texto favorito para editar a redução. Recomendamos [Visual Studio Code](https://code.visualstudio.com/), um editor de software livre leve gratuito da Microsoft.
