**Status de tradução:** Esse artigo é uma tradução de [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Data da última tradução: 2019-01-27\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_User_Repository&diff=0&oldid=564909) na versão em inglês.

Artigos relacionados

*   [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")
*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")
*   [.SRCINFO](/index.php/.SRCINFO_(Portugu%C3%AAs) ".SRCINFO (Português)")
*   [Interface RPC do Aurweb](/index.php/Interface_RPC_do_Aurweb "Interface RPC do Aurweb")
*   [Diretrizes de Trusted User do AUR](/index.php/Diretrizes_de_Trusted_User_do_AUR "Diretrizes de Trusted User do AUR")
*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais")
*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")
*   [Auxiliares do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR")

O Arch User Repository (AUR) ou, em português, Repositório de Usuário do Arch é um repositório dirigido pela comunidade para usuários do Arch. Ele contém descrições de pacotes ([PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")) que permitem a você compilar um pacote de um fonte com o [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e depois instalar via [pacman](/index.php/Pacman_(Portugu%C3%AAs)#Comandos_adicionais "Pacman (Português)"). O AUR foi criado para organizar e compartilhar novos pacotes da comunidade e ajudar a acelerar a inclusão dos pacotes populares no [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community"). Este documento explica como usuários podem acessar e utilizar o AUR.

Um bom número de novos pacotes que entram para os repositórios oficiais iniciam no AUR. No AUR, usuários são capazes de contribuir com seus próprios pacotes (PKGBUILD e arquivos relacionados). A comunidade do AUR tem a capacidade de votar a favor os pacotes no AUR. Se um pacote se torna popular o bastante -- desde que tenha uma licença compatível e uma boa técnica de empacotamento -- ele pode ser colocado no repositório *community* (diretamente acessível pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") ou [abs](/index.php/Abs_(Portugu%C3%AAs) "Abs (Português)")).

**Atenção:** Os pacotes do AUR são conteúdo produzido por usuário. Qualquer uso dos arquivos fornecidos está por sua própria conta e risco.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Começando](#Começando)
*   [2 História](#História)
*   [3 Repositórios Git para pacotes AUR3](#Repositórios_Git_para_pacotes_AUR3)
*   [4 Instalando pacotes](#Instalando_pacotes)
    *   [4.1 Pré-requisitos](#Pré-requisitos)
    *   [4.2 Obtendo arquivos de compilação](#Obtendo_arquivos_de_compilação)
    *   [4.3 Compilando e instalando o pacote](#Compilando_e_instalando_o_pacote)
*   [5 Feedback](#Feedback)
*   [6 Compartilhando e mantendo pacotes](#Compartilhando_e_mantendo_pacotes)
    *   [6.1 Enviando pacotes](#Enviando_pacotes)
        *   [6.1.1 Regras de envio](#Regras_de_envio)
        *   [6.1.2 Autenticação](#Autenticação)
        *   [6.1.3 Criando repositórios de pacote](#Criando_repositórios_de_pacote)
    *   [6.2 Publicando novo conteúdo de pacote](#Publicando_novo_conteúdo_de_pacote)
    *   [6.3 Mantendo pacotes](#Mantendo_pacotes)
    *   [6.4 Outras requisições](#Outras_requisições)
*   [7 Tradução da interface web](#Tradução_da_interface_web)
*   [8 Sintaxe de comentário](#Sintaxe_de_comentário)
*   [9 FAQ](#FAQ)
    *   [9.1 O que é o AUR?](#O_que_é_o_AUR?)
    *   [9.2 Que tipo de pacote é permitido no AUR?](#Que_tipo_de_pacote_é_permitido_no_AUR?)
    *   [9.3 Como posso votar em pacotes no AUR?](#Como_posso_votar_em_pacotes_no_AUR?)
    *   [9.4 O que é um Trusted User / TU?](#O_que_é_um_Trusted_User_/_TU?)
    *   [9.5 Qual é a diferença entre o Arch User Repository e repositório [community]?](#Qual_é_a_diferença_entre_o_Arch_User_Repository_e_repositório_[community]?)
    *   [9.6 Foo no AUR está desatualizado; o que devo fazer?](#Foo_no_AUR_está_desatualizado;_o_que_devo_fazer?)
    *   [9.7 Foo no AUR não compila quando eu executo makepkg; o que devo fazer?](#Foo_no_AUR_não_compila_quando_eu_executo_makepkg;_o_que_devo_fazer?)
    *   [9.8 ERRO: Uma ou mais assinaturas PGP não puderam ser verificadas!; o que eu devo fazer?](#ERRO:_Uma_ou_mais_assinaturas_PGP_não_puderam_ser_verificadas!;_o_que_eu_devo_fazer?)
    *   [9.9 Como eu crio um PKGBUILD?](#Como_eu_crio_um_PKGBUILD?)
    *   [9.10 Eu tenho um PKGBUILD que queria enviar; alguém pode verificá-lo para ver se ele tem algum erro?](#Eu_tenho_um_PKGBUILD_que_queria_enviar;_alguém_pode_verificá-lo_para_ver_se_ele_tem_algum_erro?)
    *   [9.11 Como que faz para um PKGBUILD ir para o repositório *community*?](#Como_que_faz_para_um_PKGBUILD_ir_para_o_repositório_community?)
    *   [9.12 Como o posso agilizar processo de repetidas compilações?](#Como_o_posso_agilizar_processo_de_repetidas_compilações?)
    *   [9.13 Qual é a diferença entre pacotes foo e foo-git](#Qual_é_a_diferença_entre_pacotes_foo_e_foo-git)
    *   [9.14 Por que foo desapareceu do AUR?](#Por_que_foo_desapareceu_do_AUR?)
    *   [9.15 Como eu descubro se algum dos meus pacotes instalados desapareceu do AUR?](#Como_eu_descubro_se_algum_dos_meus_pacotes_instalados_desapareceu_do_AUR?)
    *   [9.16 Como eu posso obter uma lista de todos os pacotes do AUR?](#Como_eu_posso_obter_uma_lista_de_todos_os_pacotes_do_AUR?)
*   [10 Veja também](#Veja_também)

## Começando

Os usuários podem pesquisar e baixar os PKGBUILDs da [Interface Web do AUR](https://aur.archlinux.org). Esses PKGBUILDs podem ser construídos dentro dos pacotes instaláveis usando [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"), e depois instalados usando pacman.

*   Certifique-se de que o grupo de pacotes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está todo instalado (`pacman -S --needed base-devel`).
*   Veja o [#FAQ](#FAQ) para respostas das questões mais comuns.
*   Você pode querer ajustar `/etc/makepkg.conf` para melhor otimizar a prioridade do seu processador para a construção dos pacotes do AUR. Uma melhora significante nos tempos de compilação pode ser realizada nos sistemas com processadores multi-cores ao ajustar a variável MAKEFLAGS. Os usuários também podem habilitar otimizações específicas de hardware no GCC por meio da variável CFLAGS. Veja [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") para mais informações.

Também é possível interagir com o AUR por meio de SSH: digite `ssh aur@aur.archlinux.org help` para uma lista de comandos disponíveis.

## História

No começo, havia `ftp://ftp.archlinux.org/incoming` e as pessoas contribuíam simplesmente enviando o PKGBUILD, os arquivos suplementares e o próprio pacote construído para o servidor. O pacote e os arquivos associados mantiveram-se até um [Mantenedor de pacote](/index.php/Arch_terminology_(Portugu%C3%AAs)#Package_maintainer "Arch terminology (Português)") ver o programa e adotá-lo.

Em seguida, os Trusted User Repositories nasceram. Certos indivíduos na comunidade foram habilitados a hospedar seus próprios repositórios para qualquer um usar. O AUR expandiu nesta base, com o objetivo de ser mais flexível e usável. Na verdade, os mantenedores do AUR ainda são referidos como TUs (Trusted Users).

Entre 2015-06-08 e 2015-08-08, o AUR mudou da versão 3.5.1 para 4.0.0, introduzindo o uso de repositórios Git para publicação dos PKGBUILDs. Os pacotes existentes foram descartados, a menos que migrados manualmente para a nova infraestrutura por seus mantenedores.

## Repositórios Git para pacotes AUR3

O [Arquivo do AUR](https://github.com/aur-archive) no GitHub possui um repositório para cada repositório que estava no AUR 3 durante a migração para o AUR 4 em Agosto de 2015. Alternativamente, há o repositório [aur3-mirror](https://github.com/felixonmars/aur3-mirror/) que fornece o mesmo conteúdo.

## Instalando pacotes

A instalação de pacotes do AUR é um processo relativamente simples. Essencialmente:

1.  Obtenha os arquivos de compilação, incluindo o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e possivelmente outros arquivos necessários, como unidades [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") e patches (geralmente não o código em si).
2.  Certifique-se de que o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e os arquivos que o acompanham não são maliciosos ou duvidosos.
3.  Execute `makepkg -si` no diretório onde os arquivos foram salvos. Isso vai baixar o código, resolver as dependências com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), compilá-lo, empacotá-lo e instalar o pacote.

**Nota:** O AUR não possui suporte, então qualquer pacote que você instalar é *sua responsabilidade* atualizar, e não do pacman. Se os pacotes nos repositórios oficiais forem atualizados, você precisará recompilar quaisquer pacotes do AUR que dependam daquelas bibliotecas.

### Pré-requisitos

Primeiro, certifique-se de que as ferramentas necessárias estão instaladas, [instalando](/index.php/Instale "Instale") todo o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), o qual inclui [make](https://www.archlinux.org/packages/?name=make) e outras ferramentas necessárias para a compilação do código-fonte.

**Nota:** Os pacotes do AUR presumem que o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está instalado, isto é, eles não listarão explicitamente os membros deste grupo como dependências

Em seguida, escolha o diretório de compilação adequado. Um diretório de compilação é apenas um diretório no qual o pacote será feito ou "compilado" e pode ser em qualquer diretório. Os exemplos nas seguintes seções usarão `~/builds` como o diretório de compilação.

### Obtendo arquivos de compilação

Localize o pacote no AUR. Isso pode ser feito usando o campo de pesquisa no topo da [página inicial do AUR](https://aur.archlinux.org/). Ao clicar no nome do aplicativo na lista de resultados de pesquisa, será mostrada uma página de informações sobre o pacote. Leia atentamente a descrição para confirmar que esse é o pacote desejado, veja quando o pacote foi atualizado pela última vez e leia quaisquer comentários.

Há vários métodos para adquirir os arquivos de compilação:

*   Clonar o repositório [git](/index.php/Git "Git") que está rotulado como o "Git Clone URL" em "Detalhes do pacote". Esse é o método preferível.

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

```
$ cd *nome_pacote*

```

**Atenção:** Verifique cuidadosamente o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), qualquer arquivo *.install* e quaisquer outros arquivos no repositório git do pacote para comandos maliciosos ou perigosos. Em caso de dúvida, não crie o pacote e nem [peça conselho](/index.php/General_troubleshooting#Additional_support "General troubleshooting") no fórum ou na lista de discussão. Código malicioso foi encontrado em pacotes antes. [[1]](https://lists.archlinux.org/pipermail/aur-general/2018-July/034151.html)

Veja o conteúdo de todos os arquivos fornecidos. Por exemplo, para usar o paginador *less* para ver `PKGBUILD`:

```
$ less PKGBUILD

```

**Dica:** Se você está atualizando um pacote, você pode querer olhar as mudanças desde o último commit.

*   Para ver as mudanças desde o último commit, você pode usar `git show`.
*   Para ver mudanças desde o último commit usando *vimdiff*, execute `git difftool @~..@ vimdiff`. A vantagem do *vimdiff* é que você vê todo o conteúdo de cada arquivo junto com os indicadores do que foi alterado.

Crie o pacote. Depois de confirmar, manualmente, o conteúdo dos arquivos, execute [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") como usuário normal no diretório de compilação.

```
$ makepkg -si

```

*   `-s`/`--syncdeps` resolve automaticamente e instala quaisquer dependências com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") antes de compilar. Se o pacote depende de outros pacotes do AUR, você precisará instalá-los manualmente primeiro.
*   `-i`/`--install` instala o pacote se ele foi compilado com sucesso. Alternativamente, o pacote compilado pode ser instalado com `pacman -U *pacote*.pkg.tar.xz`.

Outras flags úteis são

*   `-r`/`--rmdeps` remove dependências de tempo de compilação após a compilação, já que elas não mais são necessárias. Porém, essas dependências pode precisar serem reinstaladas da próxima vez que o pacote for atualizado.
*   `-c`/`--clean` limpa os arquivos temporários de compilação após a compilação, já que eles não mais são necessários. Esses arquivos geralmente são necessários apenas ao depurar o processo de compilação.

**Nota:** O exemplo acima é apenas um resumo breve do processo de compilação. É **altamente** recomendado ler os artigos [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") para mais detalhes.

## Feedback

A [Interface Web do AUR](https://aur.archlinux.org) possui um recurso de comentários que permite aos usuários enviar sugestões e feedback ao contribuidor do PKGBUILD. Evite colar patches ou PKGBUILDs na seção de comentários. Eles logo tornam-se obsoletos e terminam tomando muito espaço sem necessidade. Ao invés disso, envie por e-mail os arquivos ao mantenedor ou até mesmo use um [pastebin](/index.php/Pastebin "Pastebin").

Uma das atividades mais fáceis para **todos** os usuários do Arch é navegar no AUR e **votar** em seus pacotes prediletos, usando a interface online. Todos os pacotes são elegíveis para serem adotados por um TU (Trusted User) para a inclusão no [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community"), e a contagem de votos é uma das coisas levadas em consideração nesse processo; votar é do interesse de todos!

## Compartilhando e mantendo pacotes

Usuários podem **compartilhar** PKGBUILDs usando o Arch User Repository, o qual não contém pacote binário algum, mas permite aos usuários enviar PKGBUILDs, que podem ser baixados por outros. Esses PKGBUILDs são totalmente não-oficiais e não foram examinados completamente, então eles devem ser usados por sua conta e risco.

### Enviando pacotes

**Atenção:** Antes de tentar enviar um pacote, espera-se que você esteja familiarizado com os [Arch Packaging Standards](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch") (*padrões de empacotamento do Arch*) e todos os artigos sob "Artigos relacionados". **Verifique cuidadosamente** se o que você está enviando está correto. Pacotes que violam as regras podem ser **excluídos** sem qualquer aviso.

Se você de alguma forma esta incerto sobre o pacote ou o processo de compilação/envio mesmo após ler essa seção duas vezes, envie o PKGBUILD para a [lista de discussão do AUR](https://mailman.archlinux.org/mailman/listinfo/aur-general), o [fórum do AUR](https://bbs.archlinux.org/viewforum.php?id=4) nos fóruns do Arch ou peça em nosso [canal IRC](/index.php/Canal_IRC "Canal IRC") por revisão pública antes de adicioná-lo ao AUR.

#### Regras de envio

Ao enviar um pacote para o AUR, observe as seguintes regras:

*   Os PKGBUILDs enviados não devem compilar quaisquer aplicativos **já disponíveis em qualquer** um dos **repositórios oficiais** de binários sob qualquer circunstâncias. Verifique a [base de dados de pacotes oficiais](https://www.archlinux.org/packages/) pelo pacote. Se qualquer versão dele existir, **não** envie o pacote. Se o pacote oficial está desatualizado, marque-o como tal. Se o pacote oficial está quebrado ou faltando um recurso, por favor preencha um [relatório de erro](https://bugs.archlinux.org/).

	**Exceção** a essa regra estrita pode ser apenas os pacotes tendo **recursos extras** habilitados e/ou **patches** em comparação com aqueles oficiais. Em tal ocasião o `pkgname` deve ser diferente para expressar a diferença. Por exemplo, um pacote para GNU screen contendo o patch de barra lateral poderia ser chamado de `screen-sidebar`. Além do mais, o vetor `provides=('screen')` deve ser usado para evitar conflitos com o pacote oficial.

*   **Verifique no AUR** se o pacote **já existe**. Se ele já tem um mantenedor, alterações podem ser submetidas em comentários para chamar atenção do mantenedor. Se o pacote não tem um mantenedor ou o mantenedor não responde, o pacote pode ser adotado e atualizado como precisar. Não crie pacotes duplicados.

*   Certifique-se de que o pacote que você deseja é **útil**. Alguém mais vai querer usá-lo? Ele é extremamente especializado? Se mais de algumas poucas pessoas achariam esse pacote útil, ele é apropriado para envio.

	Os repositórios do AUR e oficiais servem par pacotes que, em geral, instalam softwares e conteúdo relacionados com software, incluindo um ou mais dos seguintes: executável(is); arquivo(s) de configuração; documentação online ou offline para softwares específicos ou a distribuição Arch Linux como um todo; mídia para ser usada diretamente por software.

*   Não use `replaces` em um PKGBUILD do AUR a menos que o pacote seja renomeado, por exemplo, quando *Ethereal* se tornou *Wireshark*. Se o pacote for uma versão alternativa **de um pacote já existente**, use `conflicts` (e `provides` se esse pacote for requerido por outras pessoas). A principal diferença é: após a sincronização (-Sy), o pacman imediatamente deseja substituir um pacote (alvo de substituição) instalado ao encontrar um pacote com os `replaces` correspondentes em qualquer lugar de seus repositórios; O `conflicts`, por outro lado, só é avaliado na instalação do pacote, que geralmente é o comportamento desejado, porque é menos invasivo.

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

**Dica:** Você pode adicionar múltiplas chaves públicas ao seu perfil separando-as com uma nova linha no campo de entrada.

#### Criando repositórios de pacote

Se você está [criando um novo pacote](/index.php/Criando_pacotes "Criando pacotes") do zero, estabeleça um repositório Git local e um remoto no AUR [clonando](/index.php/Git#Getting_a_Git_repository "Git") o [pkgbase](/index.php/PKGBUILD_(Portugu%C3%AAs)#pkgbase "PKGBUILD (Português)") desejado. Se o pacote ainda não existir, o seguinte aviso é esperado:

 `$ git clone ssh://aur@aur.archlinux.org/*nome_pacote*.git` 
```
Cloning into '*pkgbase*'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

**Nota:** O repositório não estará vazio, se `*pkgbase*` corresponde a um pacote [excluído](#Outras_requisições).

Se você já tem um pacote, [inicialize-o](/index.php/Git#Getting_a_Git_repository "Git") como um repositório Git, se ainda não for um, e adicione um remoto do AUR:

```
$ git remote add *rótulo* ssh://aur@aur.archlinux.org/*pkgbase*.git

```

Então, faça um [fetch](/index.php/Git#Using_remotes "Git") deste remoto para inicializá-lo no AUR.

**Nota:** Use [pull e rebase](https://git-scm.com/docs/git-pull#git-pull---rebasefalsetruemergespreserveinteractive) para resolver conflitos se o `*pkgbase*` corresponder a um pacote excluído.

### Publicando novo conteúdo de pacote

**Atenção:** Seus commits terão como autor seu [nome e endereço de e-mail Git globais](/index.php/Git#Configuration "Git"). É muito difícil de alterar commits após você realizar o *push* ([FS#45425](https://bugs.archlinux.org/task/45425)). Se você deseja fazer o push para o AUR sob credenciais diferentes, você pode alterá-los por pacote com `git config user.name "..."` e `git config user.email "..."`.

Ao lançar uma nova versão do software empacotado, atualize as variáveis [pkgver](/index.php/PKGBUILD_(Portugu%C3%AAs)#pkgver "PKGBUILD (Português)") ou [pkgrel](/index.php/PKGBUILD_(Portugu%C3%AAs)#pkgrel "PKGBUILD (Português)") para notificar todos os usuários que uma atualização é necessária. Não atualize esses valores se apenas pequenas alterações no [PKGBUILD (Português)](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), como a correção de um erro de digitação, estiverem sendo publicadas.

Certifique-se de regerar o [.SRCINFO](/index.php/.SRCINFO_(Portugu%C3%AAs) ".SRCINFO (Português)") sempre que metadados do `PKGBUILD` forem alterados, tal como atualizações de `pkgver()`; do contrário, o AUR não vai mostrar os números de versão atualizados.

Para enviar ou atualizar um pacote, [adicione](/index.php/Git#Staging_changes "Git") *pelo menos* o `PKGBUILD` e `.SRCINFO`, e quaisquer arquivos auxiliares novos ou modificados (como arquivos [*.install*](/index.php/PKGBUILD_(Portugu%C3%AAs)#install "PKGBUILD (Português)") ou [arquivos fontes locais](/index.php/PKGBUILD_(Portugu%C3%AAs)#source "PKGBUILD (Português)") como [patches](/index.php/Patching_packages "Patching packages")) à *staging area* com `git add`, faça commit deles para sua árvore local com uma mensagem de commit com `git commit`, faça [commit](/index.php/Git#Committing_changes "Git") com uma mensagem de commit significativa e, finalmente, faça um [push](/index.php/Git#Push_to_a_repository "Git") das alterações para o AUR.

Por exemplo:

```
$ makepkg --printsrcinfo > .SRCINFO
$ git add PKGBUILD .SRCINFO
$ git commit -m "*mensagem útil de commit*"
$ git push

```

**Nota:** Se o `.SRCINFO` foi incluído em seu primeiro commit, adicione-o realizando o [rebase com --root](https://git-scm.com/docs/git-rebase#git-rebase---root) ou [filtrando a árvore](https://git-scm.com/docs/git-filter-branch#git-filter-branch---tree-filterltcommandgt), de forma que o AUR permita seu push inicial.

**Dica:** Para manter o diretório de trabalho e os commits o mais limpo possível, crie um [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5) exclua todos os arquivos e adicione forçadamente os arquivos conforme necessário.

### Mantendo pacotes

*   Verifique os feedback e comentários de outros usuários e tente incorporar quaisquer melhorias que eles sugerirem; considere isso um processo de aprendizado!
*   Por favor, não envie um comentário contendo a versão toda vez que você atualizar o pacote. Isso deixa a seção de comentário usável para o conteúdo valioso mencionado acima.
*   Por favor, não apenas envie e depois esqueça dos pacotes! É trabalho do mantenedor manter o pacote, verificando atualizações e melhorando o PKGBUILD.
*   Se você não quer mais continuar mantendo o pacote por algum motivo, basta abandonar (`disown`) o pacote usando a interface web do AUR e/ou postar uma mensagem na Lista de Discussão do AUR. Se todos os mantenedores de um pacote AUR o abandonarem, ele se tornará um pacote ["órfão"](https://aur.archlinux.org/packages/?SB=n&do_Orphans=Orphans).

### Outras requisições

Requisições para excluir, mesclar e tornar órfão podem ser criadas clicando no link "Enviar requisição" sob "Ações do pacote" no lado direito da janela. Isso automaticamente uma notificação de e-mail para o atual mantenedor de pacote e para a [lista de discussão aur-requests](https://mailman.archlinux.org/mailman/listinfo/aur-requests) para debate. [Trusted Users](/index.php/Trusted_Users_(Portugu%C3%AAs) "Trusted Users (Português)") vão então aceitar ou rejeitar a requisição.

*   Requisições para tornar órfão (*Orphan requests*, em inglês) serão concedidas somente após duas semanas se o atual mantenedor não apresentar resposta.
*   Requisições para mesclar (*Merge requests*, em inglês) são para excluir o pacote base e transferir os votos e comentários para outro pacote base. O nome do pacote base para onde será mesclado deve ser informado. Note que isso tem nada haver com "git merge" ou com as "Merge Requests" do GitLab.
*   Requisições para excluir (*Deletion requests*, em inglês) precisam das seguintes informações:
    *   Uma nota curta explicando o motivo para exclusão. Note que um comentário em um pacote não necessariamente demonstra suficiente motivo do porquê um pacote deve ser excluído. Isso porque assim que um TU realiza a exclusão, o único lugar que vai manter a tal informação será o e-mail na lista de discussão do aur-requests.
    *   Detalhes de suporte, como, por exemplo, quando um pacote é fornecido por outro pacote, se você é o mantenedor do pacote, ele foi renomeado e o dono original concordou, etc.
    *   Requisições para excluir podem ser negadas, caso em que, se você for o mantenedor do pacote, você provavelmente será aconselhado a tornar órfão o pacote para permitir a adoção por outro empacotador.
    *   Após um pacote ser excluído, seu repositório Git permanece disponível no AUR.

## Tradução da interface web

Veja [i18n.txt](https://projects.archlinux.org/aurweb.git/tree/doc/i18n.txt) na árvore de arquivos fontes do AUR para informações sobre criação e manutenção de tradução da interface web do AUR.

## Sintaxe de comentário

Há suporte à sintaxe do [Python-Markdown](https://python-markdown.github.io/) nos comentários. Ela fornece uma sintaxe [Markdown](https://en.wikipedia.org/wiki/Markdown "wikipedia:Markdown") básica para formatar comentários. Note que essa implementação possui algumas [diferenças](https://python-markdown.github.io/#differences) em relação às [regras de sitaxe](https://daringfireball.net/projects/markdown/syntax) oficiais. Hashes de commit para o repositório Git do pacote e referências a chamados do Flyspray são convertidos automaticamente em links. Comentários longos são encolhidos e podem ser expandidos sob demanda.

## FAQ

### O que é o AUR?

O AUR (Arch User Repository) é um lugar para onde a comunidade do Arch Linux pode enviar [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") de aplicativos, bibliotecas, etc., e compartilhá-los com toda a comunidade. Outros usuários poderão então votar pelos seus favoritos para que sejam transferidos para o [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community") de forma a serem compartilhados com os usuários do Arch Linux em forma de binário.

### Que tipo de pacote é permitido no AUR?

Os pacotes no AUR são meramente "scripts de compilação", isto é, receitas para a compilação de binários para o pacman. Na maioria dos casos, tudo é permitido, sujeito à [utilidade e escopo das diretrizes](#Regras_de_envio), desde que o pacote esteja em conformidade com os termos de licenciamento do conteúdo. Para outros casos, onde é mencionado que "você não pode vincular" a downloads, por exemplo, conteúdos que não são redistribuíveis, você somente pode usar o nome do arquivo como fonte. Isso significa que e requer que os usuários já tenham o fonte restrito no diretório de compilação antes de compilar o pacote. Quando tiver dúvidas, pergunte.

### Como posso votar em pacotes no AUR?

Registe-se no [site do AUR](https://aur.archlinux.org/) para obter uma opção "Vote neste pacote" enquanto navega nos pacotes. Após se registrar, também é possível votar a partir da linha de comando com [aurvote](https://aur.archlinux.org/packages/aurvote/), [aurvote-git](https://aur.archlinux.org/packages/aurvote-git/) ou [aur-auto-vote-git](https://aur.archlinux.org/packages/aur-auto-vote-git/).

Alternativamente, se você possui uma [autenticação ssh](#Autenticação) configurada como mencionado acima, você pode votar diretamente a partir da linha de comando usando sua chave ssh. Isso significa que você não precisará salvar ou digitar sua senha AUR.

```
ssh aur@aur.archlinux.org vote <NOME_PACOTE>

```

### O que é um Trusted User / TU?

Um [(Trusted User)](/index.php/AUR_Trusted_User_Guidelines_(Portugu%C3%AAs) "AUR Trusted User Guidelines (Português)"), abreviado como TU, é uma pessoa que é escolhida para supervisionar o AUR e o [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community"). Eles são os que mantêm PKGBUILDs populares no *community* e de forma geral mantêm o AUR funcionando.

### Qual é a diferença entre o Arch User Repository e repositório [community]?

O Arch User Repository é onde todos os PKGBUILDs que os usuários submetem são armazenados e têm que ser compilados manualmente com [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"). Quando os PKGBUILDs recebem interesse e suporte suficiente da comunidade, eles são movidos para o [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community") (mantido pelos TUs), onde os pacotes binários podem ser instalados com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

### Foo no AUR está desatualizado; o que devo fazer?

Primeiro, você deve sinalizar o pacote como desatualizado (*out-of-date*), indicando detalhes sobre por que o pacote está desatualizado, de preferência incluindo links para o anúncio de lançamento ou o novo lançamento de tarball. Você também deve tentar contactar o mantenedor diretamente por e-mail. Se não houver resposta do mantenedor após *duas semanas*, você pode apresentar uma solicitação para tornar o pacote *órfão*. Isso significa que você pede a um [Trusted User](/index.php/Trusted_User "Trusted User") para destituir o mantenedor de um pacote base. Isso deve ser feito somente se o pacote exigir a ação do mantenedor, que ele/ela não está respondendo e você já tentou contatá-lo anteriormente.

Neste meio tempo, você pode tentar atualizar o pacote você mesmo editando o PKGBUILD localmente. Ás vezes, atualizações não exigem qualquer alteração para o processo de compilação ou empacotamento, caso em que apenas atualizar o vetor `pkgver` ou `source` é suficiente.

**Nota:** [Pacotes VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") não são considerados desatualizados quando o pkgver altera, então não sinalize-os pois o mantenedor irá simplesmente retirar a sinalização e ignorar você. Mantenedores do AUR não devem fazer commits para meramente incrementar o pkgver.

### Foo no AUR não compila quando eu executo makepkg; o que devo fazer?

Provavelmente está deixando escapar alguma coisa trivial.

1.  [Atualize o sistema](/index.php/Pacman_(Portugu%C3%AAs)#Atualizando_pacotes "Pacman (Português)") antes de compilar qualquer coisa com `makepkg`, pois o problema pode ser que o seu sistema não está atualizado.
2.  Certifique-se de que tem ambos os grupos [base](https://www.archlinux.org/groups/x86_64/base/) e [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) instalados.
3.  Tente usar a opção `-s` com `makepkg` para verificar e instalar todas as dependências necessárias antes de começar o processo de compilação.

Certifique-se de primeiro ler o PKGBUILD e os comentários na página do AUR do pacote em questão. O motivo pode não ser trivial. CFLAGS, LDFLAGS e MAKEFLAGS personalizadas podem causar falhas. Também é possível que o PKGBUILD esteja realmente incorreto para todos. Se não consegue descobrir por si mesmo, relate o problema ao mantenedor. Por exemplo, publique nos comentários da página do AUR os erros que você está recebendo.

Para verificar se o PKGBUILD está quebrado, ou seu sistema está configurado incorretamente, considere compilar em um chroot limpo. Ele compilará seu pacote em um ambiente limpo do Arch Linux, com apenas dependências (de compilação) instaladas e sem personalização do usuário. Para fazer isso [instale](/index.php/Instale "Instale") [devtools](https://www.archlinux.org/packages/?name=devtools) e execute `extra-x86_64-build` ao invés de `makepkg`. Para pacotes [multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)"), execute `multilib-build`. Veja [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") para mais informações. Se o processo de compilação ainda falhar em um chroot limpo, o problema provavelmente está no PKGBUILD.

### ERRO: Uma ou mais assinaturas PGP não puderam ser verificadas!; o que eu devo fazer?

É muito provável que você não tenha as chaves públicas necessárias no seu chaveiro pessoal para verificar os arquivos baixados. Se um ou mais arquivos .sig forem baixados durante a criação do pacote, o [makepkg verificará automaticamente o(s) arquivo(s) correspondente(s) com a chave pública de seu signatário](/index.php/Makepkg_(Portugu%C3%AAs)#Verificação_de_assinatura "Makepkg (Português)"). Se você não tiver a chave necessária no seu chaveiro pessoal, o *makepkg* não fará a verificação.

A maneira recomendada para lidar com este problema é importar a chave pública requerida, ou [manualmente](/index.php/GnuPG#Import_a_public_key "GnuPG") ou [de um servidor de chaves](/index.php/GnuPG#Use_a_keyserver "GnuPG"). Geralmente, você pode simplesmente encontrar a impressão digital das chaves públicas necessárias na seção [validpgpkeys](/index.php/PKGBUILD_(Portugu%C3%AAs)#validpgpkeys "PKGBUILD (Português)") do [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)").

### Como eu crio um PKGBUILD?

O melhor recurso é a página wiki sobre [criação de pacotes](/index.php/Criando_pacotes "Criando pacotes"). Lembre-se de olhar no AUR antes de criar o PKGBUILD para evitar retrabalho.

### Eu tenho um PKGBUILD que queria enviar; alguém pode verificá-lo para ver se ele tem algum erro?

Se quiser ter o seu PKGBUILD analisado, publique-o na [lista de discussão aur-general](https://mailman.archlinux.org/mailman/listinfo/aur-general) para receber feedback dos TUs e de outros membros do AUR. Você também pode conseguir ajuda do [Canal IRC](/index.php/Canal_IRC "Canal IRC"), #archlinux-aur em irc.freenode.net. Você também pode usar o [namcap](/index.php/Namcap_(Portugu%C3%AAs) "Namcap (Português)") para verificar erros no seu PKGBUILD e no pacote resultante.

### Como que faz para um PKGBUILD ir para o repositório *community*?

Normalmente, são necessários pelo menos 10 votos para que alguma coisa seja transferida para o [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community"). Contudo, se um TU tiver interesse em dar suporte a um pacote, geralmente este será encontrado no repositório.

Atingir o mínimo de votos não é o único requisito, tem que haver um TU interessado em manter o pacote. TUs não são obrigados a mover um pacote para o repositório *community* mesmo se este tiver milhares de votos.

Geralmente, quando um pacote muito popular se mantém no AUR é porque:

*   Arch Linux já possui outra versão de um pacote nos repositórios
*   Sua licença proíbe redistribuição
*   Ajuda a obter PKGBUILDs submetidos pelo usuário. [Auxiliares do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR"), por definição, [não possuem suporte](https://bbs.archlinux.org/viewtopic.php?pid=828310#p828310).

Veja também [regras para pacotes entrarem no repositório *community*](/index.php/AUR_Trusted_User_Guidelines_(Portugu%C3%AAs)#Regras_para_a_Entrada_de_Pacotes_no_Repositório_[community] "AUR Trusted User Guidelines (Português)").

### Como o posso agilizar processo de repetidas compilações?

Veja [Makepkg (Português)#Melhorando os tempos de compilação](/index.php/Makepkg_(Portugu%C3%AAs)#Melhorando_os_tempos_de_compilação "Makepkg (Português)").

### Qual é a diferença entre pacotes foo e foo-git

Muitos pacotes AUR são apresentados nas versões regulares ("estáveis") e de desenvolvimento ("instáveis"). Um pacote de desenvolvimento geralmente possui um sufixo como `-cvs`, `-svn`, `-git`, `-hg`, `-bzr` ou `-darcs`. Enquanto os pacotes de desenvolvimento não são destinados a usos regulares, eles podem oferecer novos recursos ou correções de erros. Por esses pacotes baixarem o mais novo código-fonte disponível ao executar o `makepkg`, uma versão de pacote para relacionar possíveis atualizações não está diretamente disponível para eles. Da mesma forma, esses pacotes não podem realizar uma verificação de autenticidade da soma de verificação (*checksum*), dependendo dos mantenedor(es) do repositório Git.

Veja também [Manutenção do sistema#Use pacotes de software aprovados](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Use_pacotes_de_software_aprovados "Manutenção do sistema").

### Por que foo desapareceu do AUR?

É possível que o pacote tenha sido adotado por um TU e agora esteja no [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community").

Pacotes podem ter sido excluídos, se eles não preencherem as [#Regras de envio](#Regras_de_envio). Veja os [histórico do aur-requests](https://lists.archlinux.org/pipermail/aur-requests/) pelo motivo da exclusão.

Se o pacote costumava existir no AUR3, ele pode não ter sido [migrado para o AUR4](https://lists.archlinux.org/pipermail/aur-general/2015-August/031322.html). Veja os [#Repositórios Git para pacotes AUR3](#Repositórios_Git_para_pacotes_AUR3) nos quais eles foram preservados.

### Como eu descubro se algum dos meus pacotes instalados desapareceu do AUR?

A forma mais simples é verificar o status HTTP da página AUR do pacote:

```
$ comm -23 <(pacman -Qqm | sort) <(curl [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz) | gzip -cd | sort)

```

### Como eu posso obter uma lista de todos os pacotes do AUR?

*   [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz)
*   Use `aurpkglist` do [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Veja também

*   [Interface Web do AUR](https://aur.archlinux.org)
*   [Lista de Discussão do AUR](https://lists.archlinux.org/listinfo/aur-general)
*   [DeveloperWiki:AUR Cleanup Day](/index.php/DeveloperWiki:AUR_Cleanup_Day "DeveloperWiki:AUR Cleanup Day")