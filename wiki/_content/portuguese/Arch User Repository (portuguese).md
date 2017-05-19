O Arch User Repository (AUR) ou, em português, Repositório de Usuário do Arch é um repositório dirigido pela comunidade para usuários do Arch. Ele contém descrições de pacotes ([PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")) que permitem a você compilar um pacote de um fonte com o [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e depois instalar via [pacman](/index.php/Pacman_(Portugu%C3%AAs)#Comandos_adicionais "Pacman (Português)"). O AUR foi criado para organizar e compartilhar novos pacotes da comunidade e ajudar a acelerar a inclusão dos pacotes populares no repositório [community](/index.php/Community_(Portugu%C3%AAs) "Community (Português)"). Este documento explica como usuários podem acessar e utilizar o AUR.

Um bom número de novos pacotes que entram para os repositórios oficiais iniciam no AUR. No AUR, usuários são capazes de contribuir com seus próprios pacotes (PKGBUILD e arquivos relacionados). A comunidade do AUR tem a capacidade de votar a favor ou contra os pacotes no AUR. Se um pacote se torna popular o bastante -- desde que tenha uma licença compatível e uma boa técnica de empacotamento -- ele pode ser colocado no repositório *community* (diretamente acessível pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") ou [abs](/index.php/Abs_(Portugu%C3%AAs) "Abs (Português)")).

## Contents

*   [1 Começando](#Come.C3.A7ando)
*   [2 História](#Hist.C3.B3ria)
*   [3 Pesquisando](#Pesquisando)
*   [4 Instalando pacotes](#Instalando_pacotes)
    *   [4.1 Pré-requisitos](#Pr.C3.A9-requisitos)
    *   [4.2 Obtendo arquivos de compilação](#Obtendo_arquivos_de_compila.C3.A7.C3.A3o)
    *   [4.3 Compilando e instalando o pacote](#Compilando_e_instalando_o_pacote)
*   [5 Feedback](#Feedback)
*   [6 Compartilhando e mantendo pacotes](#Compartilhando_e_mantendo_pacotes)
    *   [6.1 Enviando pacotes](#Enviando_pacotes)
        *   [6.1.1 Regras de envio](#Regras_de_envio)
        *   [6.1.2 Autenticação](#Autentica.C3.A7.C3.A3o)
        *   [6.1.3 Criando um novo pacote](#Criando_um_novo_pacote)
        *   [6.1.4 Enviando pacotes](#Enviando_pacotes_2)
    *   [6.2 Mantendo pacotes](#Mantendo_pacotes)
    *   [6.3 Outras requisições](#Outras_requisi.C3.A7.C3.B5es)
*   [7 Repositórios Git para pacotes AUR3](#Reposit.C3.B3rios_Git_para_pacotes_AUR3)
*   [8 Tradução da interface web](#Tradu.C3.A7.C3.A3o_da_interface_web)
*   [9 FAQ](#FAQ)
    *   [9.1 O que é o AUR?](#O_que_.C3.A9_o_AUR.3F)
    *   [9.2 Que tipo de pacote é permitido no AUR?](#Que_tipo_de_pacote_.C3.A9_permitido_no_AUR.3F)
    *   [9.3 Como posso votar em pacotes no AUR?](#Como_posso_votar_em_pacotes_no_AUR.3F)
    *   [9.4 O que é um Trusted User / TU?](#O_que_.C3.A9_um_Trusted_User_.2F_TU.3F)
    *   [9.5 Qual é a diferença entre o Arch User Repository e repositório [community]?](#Qual_.C3.A9_a_diferen.C3.A7a_entre_o_Arch_User_Repository_e_reposit.C3.B3rio_.5Bcommunity.5D.3F)
    *   [9.6 Foo no AUR está desatualizado; o que faço?](#Foo_no_AUR_est.C3.A1_desatualizado.3B_o_que_fa.C3.A7o.3F)
    *   [9.7 Foo no AUR não compila quando eu executo makepkg; o que devo fazer?](#Foo_no_AUR_n.C3.A3o_compila_quando_eu_executo_makepkg.3B_o_que_devo_fazer.3F)
    *   [9.8 Como eu crio um PKGBUILD?](#Como_eu_crio_um_PKGBUILD.3F)
    *   [9.9 Eu tenho um PKGBUILD que queria enviar; alguém pode verificá-lo para ver se ele tem algum erro?](#Eu_tenho_um_PKGBUILD_que_queria_enviar.3B_algu.C3.A9m_pode_verific.C3.A1-lo_para_ver_se_ele_tem_algum_erro.3F)
    *   [9.10 Como que faz para um PKGBUILD ir para o repositório *community*?](#Como_que_faz_para_um_PKGBUILD_ir_para_o_reposit.C3.B3rio_community.3F)
    *   [9.11 Como o posso agilizar processo de repetidas compilações?](#Como_o_posso_agilizar_processo_de_repetidas_compila.C3.A7.C3.B5es.3F)
    *   [9.12 Qual é a diferença entre pacotes foo e foo-git](#Qual_.C3.A9_a_diferen.C3.A7a_entre_pacotes_foo_e_foo-git)
    *   [9.13 Por que foo desapareceu do AUR?](#Por_que_foo_desapareceu_do_AUR.3F)
    *   [9.14 Como eu descubro se algum dos meus pacotes instalados desapareceu do AUR?](#Como_eu_descubro_se_algum_dos_meus_pacotes_instalados_desapareceu_do_AUR.3F)
    *   [9.15 Como eu posso obter uma lista de todos os pacotes do AUR?](#Como_eu_posso_obter_uma_lista_de_todos_os_pacotes_do_AUR.3F)
*   [10 Veja também](#Veja_tamb.C3.A9m)

## Começando

Os usuários podem pesquisar e baixar os PKGBUILDs da [Interface Web do AUR](https://aur.archlinux.org). Esses PKGBUILDs podem ser construídos dentro dos pacotes instaláveis usando [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"), e depois instalados usando pacman.

*   Certifique-se de que o grupo de pacotes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está instalado (`pacman -S --needed base-devel`).
*   Veja o [#FAQ](#FAQ) para respostas das questões mais comuns.
*   Você pode querer ajustar `/etc/makepkg.conf` para melhor otimizar a prioridade do seu processador para a construção dos pacotes do AUR. Uma melhora significante nos tempos de compilação pode ser realizada nos sistemas com processadores multi-cores ao ajustar a variável MAKEFLAGS. Os usuários também podem habilitar otimizações específicas de hardware no GCC por meio da variável CFLAGS. Veja [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") para mais informações.

Também é possível interagir com o AUR por meio de SSH: digite `ssh aur@aur.archlinux.org help` para uma lista de comandos disponíveis.

## História

No começo, havia `ftp://ftp.archlinux.org/incoming` e as pessoas contribuíam simplesmente enviando o PKGBUILD, os arquivos suplementares e o próprio pacote construído para o servidor. O pacote e os arquivos associados mantiveram-se até um [Mantenedor de pacote](/index.php/Arch_terminology_(Portugu%C3%AAs)#Package_maintainer "Arch terminology (Português)") ver o programa e adotá-lo.

Em seguida, os Trusted User Repositories nasceram. Certos indivíduos na comunidade foram habilitados a hospedar seus próprios repositórios para qualquer um usar. O AUR expandiu nesta base, com o objetivo de ser mais flexível e usável. Na verdade, os mantenedores do AUR ainda são referidos como TUs (Trusted Users).

Entre 2015-06-08 e 2015-08-08, o AUR mudou da versão 3.5.1 para 4.0.0, introduzindo o uso de repositórios Git para publicação dos PKGBUILDs.

## Pesquisando

A interface web do AUR pode ser encontrada em [https://aur.archlinux.org/](https://aur.archlinux.org/) e uma interface adequada para acessar o AUR por meio de script pode ser encontrada em [https://aur.archlinux.org/rpc.php](https://aur.archlinux.org/rpc.php).

As consultas pesquisam por nomes de pacotes e descrições por meio de uma comparação LIKE do MySQL. Isto permite critérios de pesquisa mais flexíveis (ex.: tentar pesquisar por `tool%like%grep` em vez de `tool like grep`). Se você precisa pesquisar por uma descrição que contenha `%`, use `\%` como caractere de escape.

## Instalando pacotes

A instalação de pacotes do AUR é um processo relativamente simples. Essencialmente:

1.  Obtenha os arquivos de compilação, incluindo o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e possivelmente outros arquivos necessários, como unidades [systemd](/index.php/Systemd "Systemd") e patches (geralmente não o código em si).
2.  Certifique-se de que o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e os arquivos que o acompanham não são maliciosos ou duvidosos.
3.  Execute `makepkg -si` no diretório onde os arquivos foram salvos. Isso vai baixar o código, resolver as dependências com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), compilá-lo, empacotá-lo e instalar o pacote.

### Pré-requisitos

Primeiro, certifique-se de que as ferramentas necessárias estão instaladas, [instalando](/index.php/Install "Install") o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), o qual inclui [make](https://www.archlinux.org/packages/?name=make) e outras ferramentas necessárias para a compilação do código-fonte.

**Note:** Os pacotes do AUR presumem que o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está instalado, isto é, eles não listarão explicitamente os membros deste grupo como dependências

Em seguida, escolha o diretório de compilação adequado. Um diretório de compilação é apenas um diretório no qual o pacote será feito ou "compilado" e pode ser em qualquer diretório. Os exemplos nas seguintes seções usarão `~/builds` como o diretório de compilação.

### Obtendo arquivos de compilação

Localize o pacote no AUR. Isso pode ser feito usando o recurso de pesquisa (o campo de texto no topo da [página inicial do AUR](https://aur.archlinux.org/)). Ao clicar no nome do aplicativo na lista de resultados de pesquisa, será mostrada uma página de informações sobre o pacote. Leia atentamente a descrição para confirmar que esse é o pacote desejado, veja quando o pacote foi atualizado pela última vez e leia quaisquer comentários.

Há vários métodos para adquirir os arquivos de compilação:

*   Clonar o repositório [git](/index.php/Git "Git") que está rotulado como o "Git Clone URL" em "Detalhes do pacote":

```
$ git clone https://aur.archlinux.org/*nome_pacote*.git

```

	Uma vantagem deste método é que você pode facilmente obter atualizações para o pacote vi `git pull`.

*   Baixar os arquivos de compilação com seu navegadores web clicando no link "Baixar snapshot" sob "Ações do Pacote", no canto direito da tela. Isso vai baixar um arquivo compactado, que deve ser extraído (preferivelmente em um diretório definido a parte para compilações do AUR)

```
$ tar -xvf *nome_pacote*.tar.gz

```

*   Similarmente, você pode baixar um tarball do terminal (e extraí-lo):

```
$ curl -L -O https://aur.archlinux.org/cgit/aur.git/snapshot/*nome_pacote*.tar.gz

```

### Compilando e instalando o pacote

Mude diretórios para o diretório contendo o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") do pacote.

**Warning:** **Verifique com atenção todos os arquivos.** Verifique no `PKGBUILD` e em qualquer arquivo `.install` por comandos maliciosos. `PKGBUILD`s são scripts em [bash](/index.php/Bash "Bash") contendo funções para serem executadas pelo *makepkg*: essas funções podem conter *qualquer* comando válido ou sintaxe Bash válida. Então, é totalmente possível que um `PKGBUILD` contenha comandos perigosos por malícia ou ignorância por parte do autor. Já que o *makepkg* usa *fakeroot* (e nunca deveria ser executado como root), há ainda um certo nível de proteção, mas você nunca deveria contar somente nisso. Em caso de dúvida, não compile o pacote e procure ajuda nos fóruns ou na lista de discussão.

```
$ cd *nome_pacote*
$ nano PKGBUILD
$ nano *nome_pacote*.install

```

Crie o pacote. Depois de confirmar, manualmente, a integridade dos arquivos, execute [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") como usuário normal no diretório de compilação.

```
$ makepkg -si

```

*   `-s`/`--syncdeps` resolve automaticamente e instala quaisquer dependências com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") antes de compilar. Se o pacote depende de outros pacotes do AUR, você precisará instalá-los manualmente primeiro.
*   `-i`/`--install` instala o pacote se ele foi compilado com sucesso. Alternativamente, o pacote compilado pode ser instalado com `pacman -U *pacote*.pkg.tar.xz`.

Outras flags úteis são

*   `-r`/`--rmdeps` remove dependências de tempo de compilação após a compilação, já que elas não mais são necessárias. Porém, essas dependências pode precisar serem reinstaladas da próxima vez que o pacote for atualizado.
*   `-c`/`--clean` limpa os arquivos temporários de compilação após a compilação, já que eles não mais são necessários. Esses arquivos geralmente são necessários apenas ao depurar o processo de compilação.

**Note:** O exemplo acima é apenas um resumo breve do processo de compilação. É **altamente** recomendado ler os artigos [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") para mais detalhes.

## Feedback

A [Interface Web do AUR](https://aur.archlinux.org) possui um recurso de comentários que permite aos usuários enviar sugestões e feedback ao contribuidor do PKGBUILD. Evite colar patches ou PKGBUILDs na seção de comentários. Eles logo tornam-se obsoletos e terminam tomando muito espaço sem necessidade. Ao invés disso, envie por e-mail os arquivos ao mantenedor ou até mesmo use um [pastebin](/index.php/Pastebin "Pastebin").

Uma das atividades mais fáceis para **todos** os usuários do Arch é navegar no AUR e **votar** em seus pacotes prediletos, usando a interface online. Todos os pacotes são elegíveis para serem adotados por um TU (Trusted User) para a inclusão no repositório [community](/index.php/Community_(Portugu%C3%AAs) "Community (Português)"), e a contagem de votos é uma das coisas levadas em consideração nesse processo; votar é do interesse de todos!

## Compartilhando e mantendo pacotes

**Note:** Por favor veja a discussão sobre [escopo da seção AUR4](/index.php/Talk:Arch_User_Repository#Scope_of_the_AUR4_section "Talk:Arch User Repository") antes de fazer alterações nesta seção.

Usuários podem **compartilhar** PKGBUILDs usando o Arch User Repository, o qual não contém pacote binário algum, mas permite aos usuários enviar PKGBUILDs, que podem ser baixados por outros. Esses PKGBUILDs são totalmente não-oficiais e não foram examinados completamente, então eles devem ser usados por sua conta e risco.

### Enviando pacotes

**Warning:** Antes de tentar enviar um pacote, espera-se que você esteja familiarizado com os [Arch Packaging Standards](/index.php/Arch_packaging_standards_(Portugu%C3%AAs) "Arch packaging standards (Português)") (*padrões de empacotamento do Arch*) e todos os artigos sob "Artigos relacionados". **Verifique cuidadosamente** se o que você está enviando está correto. Pacotes que violam as regras podem ser **excluídos** sem qualquer aviso.

Se você de alguma forma esta incerto sobre o pacote ou o processo de compilação/envio mesmo após ler essa seção duas vezes, envie o PKGBUILD para a [lista de discussão do AUR](https://mailman.archlinux.org/mailman/listinfo/aur-general), o [fórum do AUR](https://bbs.archlinux.org/viewforum.php?id=4) nos fóruns do Arch ou peça em nosso [canal IRC](/index.php/IRC_channel "IRC channel") por revisão pública antes de adicioná-lo ao AUR.

#### Regras de envio

Ao enviar um pacote para o AUR, observe as seguintes regras:

*   Os PKGBUILDs enviados não devem compilar quaisquer aplicativos **já disponíveis em qualquer** um dos **repositórios oficiais** de binários sob qualquer circunstâncias. Verifique a [base de dados de pacotes oficiais](https://www.archlinux.org/packages/) pelo pacote. Se qualquer versão dele existir, **não** envie o pacote. Se o pacote oficial está desatualizado, marque-o como tal. Se o pacote oficial está quebrado ou faltando um recurso, por favor preencha um [relatório de erro](https://bugs.archlinux.org/).

	**Exceção** a essa regra estrita pode ser apenas os pacotes tendo **recursos extras** habilitados e/ou **patches** em comparação com aqueles oficiais. Em tal ocasião o `pkgname` deve ser diferente para expressar a diferença. Por exemplo, um pacote para GNU screen contendo o patch de barra lateral poderia ser chamado de `screen-sidebar`. Além do mais, o vetor `provides=('screen')` deve ser usado para evitar conflitos com o pacote oficial.

*   **Verifique no AUR** se o pacote **já existe**. Se ele já tem um mantenedor, alterações podem ser submetidas em comentários para chamar atenção do mantenedor. Se o pacote não tem um mantenedor ou o mantenedor não responde, o pacote pode ser adotado e atualizado como precisar. Não crie pacotes duplicados.

*   Certifique-se de que o pacote que você deseja é **útil**. Alguém mais vai querer usá-lo? Ele é extremamente especializado? Se mais de algumas poucas pessoas achariam esse pacote útil, ele é apropriado para envio.

	Os repositórios do AUR e oficiais servem par pacotes que, em geral, instalam softwares e conteúdo relacionados com software, incluindo um ou mais dos seguintes: executável(is); arquivo(s) de configuração; documentação online ou offline para softwares específicos ou a distribuição Arch Linux como um todo; mídia para ser usada diretamente por software.

*   Envio de **binários** deve ser **evitado** se os fontes estão disponíveis. O AUR não deve conter o tarball binário criado por makepkg, nem deve conter a lista de arquivos.

*   Por favor, adicione uma **linha de comentário** ao topo do arquivo `PKGBUILD` que contém informações sobre os **mantenedores** atuais e **contribuidores** antigos, respeitando o formato a seguir. Lembre-se de disfarçar seu e-mail para protegê-lo contra spam. Linhas adicionais ou desnecessárias são facultativas.

	Se você está assumindo o papel de mantenedor para um PKGBUILD existente, adicione seu nome ao topo desta forma

```
# Maintainer: Seu Nome <endereço at domínio dot tld>

```

	Se houver mantenedores antigos, coloque-os como contribuidores. O mesmo se aplica para quem enviou o pacote, se não foi você. Se você é um comantenedor, adicione os nome de outros mantenedores atuais também.

```
# Maintainer: Seu Nome <endereço at domínio dot tld>
# Maintainer: Nome do Outro Mantenedor <endereço at domínio dot tld>
# Contributor: Nome do Mantenedor Anterior <endereço at domínio dot tld>
# Contributor: Nome do Criador do Pacote <endereço at domínio dot tld>

```

#### Autenticação

Para acesso de escrita para o AUR, você precisar ter um [par de chaves SSH](/index.php/SSH_keys "SSH keys"). O conteúdo da chave pública precisa ser copiada para seu perfil em *Minha conta* e a chave privada correspondente configurada para o endereço `aur.archlinux.org`. Por exemplo:

 `~/.ssh/config` 
```
Host aur.archlinux.org
  IdentityFile ~/.ssh/aur
  User aur
```

Você deve [criar um novo par de chaves](/index.php/SSH_keys#Generating_an_SSH_key_pair "SSH keys") em vez de usar um existente, de forma que você possa seletivamente revogar as chaves caso algo aconteça:

```
$ ssh-keygen -f ~/.ssh/aur

```

**Tip:** Você pode adicionar múltiplas chaves públicas ao seu perfil separando-as com uma nova linha no campo de entrada.

#### Criando um novo pacote

Para criar um novo repositório Git local vazio para um pacote, basta executar `git clone` com o nome de repositório correspondendo ao nome do pacote. Se o pacote ainda não existir no AUR, você verá a seguinte mensagem:

 `$ git clone ssh://aur@aur.archlinux.org/*nome_pacote*.git` 
```
Cloning into '*nome_pacote*'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

**Note:** Quando um pacote do AUR é excluído, o repositório git é mantido, de forma que é possível para um repositório do pacote excluído não estar vazio quando clonado se alguém estiver criando um pacote com o mesmo nome.

Se você já criou um repositório git, você pode simplesmente criar um remoto para o repositório do AUR e então executar "fetch":

```
$ git remote add *nome_remoto* ssh://aur@aur.archlinux.org/*nome_pacote*.git
$ git fetch *nome_remoto*

```

sendo `*nome_remoto*` o nome do remoto para a ser criado (*ex.:* "origin"). Veja o [uso de remotos no Git](/index.php/Git#Using_remotes "Git") para mais informações.

O novo pacote aparecerá no AUR após você executar *push* no primeiro commit. Você pode adicionar os arquivos fontes à cópia local do repositório Git. Veja [#Enviando pacotes](#Enviando_pacotes).

**Warning:** Seus commits do AUR serão autorizados de acordo com seu nome de usuário git e endereço de e-mail e é muito difícil de alterar commits após você ter enviado (veja [FS#45425](https://bugs.archlinux.org/task/45425)). Se você deseja enviar para o AUR sob um nome/e-mail diferente, você pode alterá-los para esse pacote via `git config user.name [...]` e `git config user.email [...]`. Reveja seus commits antes de enviá-los!

#### Enviando pacotes

**Tip:** Para evitar arquivos não rastreados de commits e manter um diretório de trabalho mais limpo possível, exclua todos os arquivos com `.gitignore` e force a adição de arquivos. Veja o [uso de gitignore](/index.php/Dotfiles#Using_gitignore "Dotfiles").

Os procedimentos para envio de pacotes para o AUR é o mesmo de novos pacotes e atualizações de pacotes. Você precisa pelo menos de um [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e um [.SRCINFO](/index.php/.SRCINFO_(Portugu%C3%AAs) ".SRCINFO (Português)") no diretório de nível superior para poder fazer o *push* do seu pacote para o AUR.

Para enviar, adicione o `PKGBUILD`, `.SRCINFO` e quaisquer arquivos auxiliares (como arquivos `.install` ou arquivos fontes locais como `.patch`) à *staging area* com `git add`, faça commit deles para sua árvore local com uma mensagem de commit com `git commit` e, finalmente, publique as alterações para o AUR com `git push`.

Por exemplo:

```
$ makepkg --printsrcinfo > .SRCINFO
$ git add PKGBUILD .SRCINFO
$ git commit -m "*mensagem útil de commit*"
$ git push

```

**Tip:** Se você inicialmente se esqueceu de fazer commit do `.SRCINFO` e adicionou-o em um commit posterior, o AUR ainda rejeitará seus *pushes* porque o `.SRCINFO` deve existir para *todo* commit. Para resolver esse problema, você pode usar [git rebase](https://git-scm.com/docs/git-rebase) com a opção `--root` ou [git filter-branch](https://git-scm.com/docs/git-filter-branch) com a opção `--tree-filter`.

### Mantendo pacotes

*   Verifique os feedback e comentários de outros usuários e tente incorporar quaisquer melhorias que eles sugerirem; considere isso um processo de aprendizado!
*   Por favor, não envie um comentário contendo a versão toda vez que você atualizar o pacote. Isso deixa a seção de comentário usável para o conteúdo valioso mencionado acima. [Auxiliares do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR") são mais adequados para verificar por atualizações.
*   Por favor, não apenas envie e depois esqueça dos pacotes! É trabalho do mantenedor manter o pacote, verificando atualizações e melhorando o PKGBUILD.
*   Se você não quer mais continuar mantendo o pacote por algum motivo, basta abandonar (`disown`) o pacote usando a interface web do AUR e/ou postar uma mensagem na Lista de Discussão do AUR. Se todos os mantenedores de um pacote AUR o abandonarem, ele se tornará um pacote ["órfão"](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=&outdated=&SB=n&SO=a&PP=50&do_Orphans=Orphans).

### Outras requisições

*   Requisições para abandono e requisições para remoção de pacotes podem ser criadas clicando no link "Enviar requisição" sob "Ações do pacote" no lado direito da janela. Isso automaticamente uma notificação de e-mail para o atual mantenedor de pacote e para a [lista de discussão aur-requests](https://mailman.archlinux.org/mailman/listinfo/aur-requests) para debate.
*   Requisições de abandono (*Disownment Requests*) serão concedidas somente após duas semanas se o atual mantenedor não apresentar resposta.
*   Requisições de mesclagem (*Merge Requests*) são para substituir um outro. Usuários ainda terão que reenviar um pacote sob um novo nome e podem requisitar mesclagem dos comentários e votos da versão anterior. Isso tem nada haver com "git merge" e não é similar aos "pull requests" do github.
*   Requisições de remoção (*Removal Requests*) precisam das seguintes informações:
    *   Motivo para exclusão, com pelo menos uma nota curta
        **NOTE:** Um comentário em um pacote não necessariamente demonstra suficiente motivo do porquê um pacote deve ser excluído. Isso porque assim que um TU realiza a exclusão, o único lugar que vai manter a tal informação será o e-mail na lista de discussão do aur-requests.
    *   Incluir detalhes de suporte, como, por exemplo, quando um pacote é fornecido por outro pacote, se você é o mantenedor do pacote, ele foi renomeado e o dono original concordou, etc.
    *   Para requisições de mesclagem: Nome do pacote base para o qual deve ser mescla

Requisições de remoção podem ser negadas, caso em que você provavelmente será aconselhado a abandonar o pacote para a referência de um possível futuro mantenedor.

## Repositórios Git para pacotes AUR3

**Note:** aur-mirror não está mais disponível

O [Arquivo do AUR](https://github.com/aur-archive) no GitHub possui um repositório para cada repositório que estava no AUR 3 durante a migração para o AUR 4.

## Tradução da interface web

Veja [i18n.txt](https://projects.archlinux.org/aurweb.git/tree/doc/i18n.txt) na árvore de arquivos fontes do AUR para informações sobre criação e manutenção de tradução da interface web do AUR.

## FAQ

### O que é o AUR?

O AUR (Arch User Repository) é um lugar para onde a comunidade do Arch Linux pode enviar [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") de aplicativos, bibliotecas, etc., e compartilhá-los com toda a comunidade. Outros usuários poderão então votar pelos seus favoritos para que sejam transferidos para o repositório [community] de forma a serem compartilhados com os usuários do Arch Linux em forma de binário.

### Que tipo de pacote é permitido no AUR?

Os pacotes no AUR são meramente "scripts de compilação", isto é, receitas para a compilação de binários para o pacman. Na maioria dos casos, tudo é permitido, sujeito à [utilidade e escopo das diretrizes](#Regras_de_envio), desde que o pacote esteja em conformidade com os termos de licenciamento do conteúdo. Para outros casos, onde é mencionado que "você não pode vincular" a downloads, por exemplo, conteúdos que não são redistribuíveis, você somente pode usar o nome do arquivo como fonte. Isso significa que e requer que os usuários já tenham o fonte restrito no diretório de compilação antes de compilar o pacote. Quando tiver dúvidas, pergunte.

### Como posso votar em pacotes no AUR?

Registe-se no [site do AUR](https://aur.archlinux.org/) para obter uma opção "Vote neste pacote" enquanto navega nos pacotes. Após se registrar, também é possível votar a partir da linha de comando com [aurvote](https://aur.archlinux.org/packages/aurvote/), [aurvote-git](https://aur.archlinux.org/packages/aurvote-git/) ou [aur-auto-vote-git](https://aur.archlinux.org/packages/aur-auto-vote-git/).

Alternativamente, se você possui uma [autenticação ssh](#Autentica.C3.A7.C3.A3o) configurada como mencionado acima, você pode votar diretamente a partir da linha de comando usando sua chave ssh. Isso significa que você não precisará salvar ou digitar sua senha AUR.

```
ssh aur@aur.archlinux.org vote <NOME_PACOTE>

```

Você pode votar para todos os pacotes AUR instalados com o seguinte:

```
for i in $(pacman -Qqm); do echo Votando para $i; ssh aur vote $i; done

```

### O que é um Trusted User / TU?

Um [(Trusted User)](/index.php/AUR_Trusted_User_Guidelines_(Portugu%C3%AAs) "AUR Trusted User Guidelines (Português)"), abreviado como TU, é uma pessoa que é escolhida para supervisionar o AUR e o repositório [community](/index.php/Community_(Portugu%C3%AAs) "Community (Português)"). Eles são os que mantêm PKGBUILDs populares no *community* e de forma geral mantêm o AUR funcionando.

### Qual é a diferença entre o Arch User Repository e repositório [community]?

O Arch User Repository é onde todos os PKGBUILDs que os usuários submetem são armazenados e têm que ser compilados manualmente com [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"). Quando os PKGBUILDs recebem interesse e suporte suficiente da comunidade, eles são movidos para o repositório [community](/index.php/Community_(Portugu%C3%AAs) "Community (Português)") (mantido pelos TUs), onde os pacotes binários podem ser instalados com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

### Foo no AUR está desatualizado; o que faço?

Para começar, você pode marcar pacotes como desatualizados. Se ele ficar desatualizado por um longo período de tempo, a melhor coisa a ser feita é você mesmo escrever um e-mail para o mantenedor. Se não houver resposta do mantenedor, você pode requisitar que seja tornado órfão. Quando estivermos falando de um pacote que está marcado como desatualizado por mais de 3 meses e em geral não teve atualização por muito tempo, por favor adicione esta informação na sua requisição.

Neste meio tempo, você pode tentar atualizar o pacote você mesmo editando o PKGBUILD - algumas atualizações não exigem qualquer alteração para o processo de compilação ou empacotamento, caso em que apenas atualizar o vetor `pkgver` ou `source` é suficiente.

### Foo no AUR não compila quando eu executo makepkg; o que devo fazer?

Provavelmente está deixando escapar alguma coisa trivial.

1.  [Atualize o sistema](/index.php/Pacman_(Portugu%C3%AAs)#Atualizando_pacotes "Pacman (Português)") antes de compilar qualquer coisa com `makepkg`, pois o problema pode ser que o seu sistema não está atualizado.
2.  Certifique-se de que tem ambos os grupos [base](https://www.archlinux.org/groups/x86_64/base/) e [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) instalados.
3.  Tente usar a opção `-s` com `makepkg` para verificar e instalar todas as dependências necessárias antes de começar o processo de compilação.

Certifique-se de primeiro ler o PKGBUILD e os comentários na página do AUR do pacote em questão. O motivo pode não ser trivial. CFLAGS, LDFLAGS e MAKEFLAGS personalizadas podem causar falhas. Também é possível que o PKGBUILD esteja realmente incorreto para todos. Se não consegue descobrir por si mesmo, relate o problema ao mantenedor. Por exemplo, publique nos comentários da página do AUR os erros que você está recebendo.

### Como eu crio um PKGBUILD?

O melhor recurso é a página wiki sobre [criação de pacotes](/index.php/Criando_pacotes "Criando pacotes"). Lembre-se de olhar no AUR antes de criar o PKGBUILD para evitar retrabalho.

### Eu tenho um PKGBUILD que queria enviar; alguém pode verificá-lo para ver se ele tem algum erro?

Se quiser ter o seu PKGBUILD criticado, publique--o para a [lista de discussão aur-general](https://mailman.archlinux.org/mailman/listinfo/aur-general) para receber feedback dos TUs e de outros membros do AUR. Você também pode conseguir ajuda do [Canal IRC](/index.php/IRC_channel "IRC channel"), #archlinux em irc.freenode.net. Você também pode usar o [namcap](/index.php/Namcap "Namcap") para verificar erros no seu PKGBUILD e no pacote resultante.

### Como que faz para um PKGBUILD ir para o repositório *community*?

Normalmente, são necessários pelo menos 10 votos para que alguma coisa seja transferida para [community](/index.php/Community_(Portugu%C3%AAs) "Community (Português)"). Contudo, se um TU tiver interesse em dar suporte a um pacote, geralmente este será encontrado no repositório.

Atingir o mínimo de votos não é o único requisito, tem que haver um TU interessado em manter o pacote. TUs não são obrigados a mover um pacote para o repositório *community* mesmo se este tiver milhares de votos.

Geralmente, quando um pacote muito popular se mantém no AUR é porque:

*   Arch Linux já possui outra versão de um pacote nos repositórios
*   O pacote é relacionado ao AUR (ex.: um [auxiliar do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR"))
*   Sua licença proíbe redistribuição

Veja também [DeveloperWiki:Community repo candidates](/index.php/DeveloperWiki:Community_repo_candidates "DeveloperWiki:Community repo candidates") e [regras para pacotes entrarem no repositório *community*](/index.php/AUR_Trusted_User_Guidelines_(Portugu%C3%AAs)#Regras_para_a_Entrada_de_Pacotes_no_Reposit.C3.B3rio_.5Bcommunity.5D "AUR Trusted User Guidelines (Português)").

### Como o posso agilizar processo de repetidas compilações?

Se você frequentemente compila códigos que usam gcc - digamos, um pacote git ou SVN - você pode encontrar [ccache](/index.php/Ccache "Ccache"), que é o diminutivo para "compiler cache", útil.

### Qual é a diferença entre pacotes foo e foo-git

Muitos pacotes AUR são apresentados nas versões regulares ("estáveis") e de desenvolvimento ("instáveis"). Um pacote de desenvolvimento geralmente possui um sufixo como `-cvs`, `-svn`, `-git`, `-hg`, `-bzr` ou `-darcs`. Enquanto os pacotes de desenvolvimento não são destinados a usos regulares, eles podem oferecer novos recursos ou correções de erros. Por esses pacotes baixarem o mais novo código-fonte disponível ao executar o `makepkg`, uma versão de pacote para relacionar possíveis atualizações não está diretamente disponível para eles. Da mesma forma, esses pacotes não podem realizar uma verificação de autenticidade da soma de verificação (*checksum*), dependendo dos mantenedor(es) do repositório Git.

Veja também [System maintenance#Use proven software packages](/index.php/System_maintenance#Use_proven_software_packages "System maintenance") ("Use pacotes de software aprovados").

### Por que foo desapareceu do AUR?

Pacotes podem ter sido excluídos, se eles não preencherem as [#Regras de envio](#Regras_de_envio). Veja os [histórico do aur-requests](https://lists.archlinux.org/pipermail/aur-requests/) pelo motivo da exclusão.

Se o pacote costumava existir no AUR3, ele pode não ter sido [migrado para o AUR4](https://lists.archlinux.org/pipermail/aur-general/2015-August/031322.html). Veja os [#Repositórios Git para pacotes AUR3](#Reposit.C3.B3rios_Git_para_pacotes_AUR3) nos quais eles foram preservados.

### Como eu descubro se algum dos meus pacotes instalados desapareceu do AUR?

A forma mais simples é verificar o status HTTP da página AUR do pacote:

```
$ comm -23 <(pacman -Qqm | sort) <(curl [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz) | gzip -cd | sort)

```

Se você está usando um [auxiliar do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR"), você pode abreviar esse script substituindo o comando curl com qualquer outro comando de consulta de AUR por um pacote.

### Como eu posso obter uma lista de todos os pacotes do AUR?

*   [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz)
*   Use `aurpkglist` do [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Veja também

*   [Interface Web do AUR](https://aur.archlinux.org)
*   [Lista de Discussão do AUR](https://lists.archlinux.org/listinfo/aur-general)
*   [Espelho do repositório Git do AUR](http://pkgbuild.com/git/aur-mirror.git/)