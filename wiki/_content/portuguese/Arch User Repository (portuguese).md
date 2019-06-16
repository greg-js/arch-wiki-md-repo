**Status de tradução:** Esse artigo é uma tradução de [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Data da última tradução: 2019-05-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_User_Repository&diff=0&oldid=573753) na versão em inglês.

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

Um bom número de novos pacotes que entram para os repositórios oficiais iniciam no AUR. No AUR, usuários são capazes de contribuir com seus próprios pacotes (`PKGBUILD` e arquivos relacionados). A comunidade do AUR tem a capacidade de votar a favor os pacotes no AUR. Se um pacote se torna popular o bastante -- desde que tenha uma licença compatível e uma boa técnica de empacotamento -- ele pode ser colocado no repositório *community* (diretamente acessível pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") ou [abs](/index.php/Abs_(Portugu%C3%AAs) "Abs (Português)")).

**Atenção:** Os pacotes do AUR são conteúdo produzido por usuário sem suporte oficial. Qualquer uso dos arquivos fornecidos está por sua própria conta e risco.

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
    *   [5.1 Comentando em pacotes](#Comentando_em_pacotes)
    *   [5.2 Votando em pacotes](#Votando_em_pacotes)
    *   [5.3 Marcando pacotes como desatualizados](#Marcando_pacotes_como_desatualizados)
*   [6 Compartilhando e mantendo pacotes](#Compartilhando_e_mantendo_pacotes)
    *   [6.1 Enviando pacotes](#Enviando_pacotes)
        *   [6.1.1 Regras de envio](#Regras_de_envio)
        *   [6.1.2 Autenticação](#Autenticação)
        *   [6.1.3 Criando repositórios de pacote](#Criando_repositórios_de_pacote)
    *   [6.2 Publicando novo conteúdo de pacote](#Publicando_novo_conteúdo_de_pacote)
    *   [6.3 Mantendo pacotes](#Mantendo_pacotes)
    *   [6.4 Outras requisições](#Outras_requisições)
        *   [6.4.1 Excluir](#Excluir)
        *   [6.4.2 Mesclar](#Mesclar)
        *   [6.4.3 Tornar órfão](#Tornar_órfão)
    *   [6.5 Promovendo pacotes ao repositório community](#Promovendo_pacotes_ao_repositório_community)
*   [7 Verificando pacotes](#Verificando_pacotes)
*   [8 Tradução da interface web](#Tradução_da_interface_web)
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

Os usuários podem pesquisar e baixar os `PKGBUILD`s da [Interface Web do AUR](https://aur.archlinux.org). Esses `PKGBUILD`s podem ser construídos dentro dos pacotes instaláveis usando *makepkg*, e depois instalados usando *pacman*.

*   Certifique-se de que o grupo de pacotes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está todo instalado (`pacman -S --needed base-devel`).
*   Veja o [#FAQ](#FAQ) para respostas das questões mais comuns.
*   Você pode querer ajustar `/etc/makepkg.conf` para melhor otimizar a prioridade do seu processador para a construção dos pacotes do AUR. Uma melhora significante nos tempos de compilação pode ser realizada nos sistemas com processadores multi-cores ao ajustar a variável `MAKEFLAGS`. Os usuários também podem habilitar otimizações específicas de hardware no [GCC](/index.php/GCC "GCC") por meio da variável `CFLAGS`. Veja [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") para mais informações.

Também é possível interagir com o AUR por meio de SSH: digite `ssh aur@aur.archlinux.org help` para uma lista de comandos disponíveis.

## História

No começo, havia `ftp://ftp.archlinux.org/incoming` e as pessoas contribuíam simplesmente enviando o `PKGBUILD`, os arquivos suplementares e o próprio pacote construído para o servidor. O pacote e os arquivos associados mantiveram-se até um [Mantenedor de pacote](/index.php/Arch_terminology_(Portugu%C3%AAs)#Package_maintainer "Arch terminology (Português)") ver o programa e adotá-lo.

Em seguida, os Trusted User Repositories nasceram. Certos indivíduos na comunidade foram habilitados a hospedar seus próprios repositórios para qualquer um usar. O AUR expandiu nesta base, com o objetivo de ser mais flexível e usável. Na verdade, os mantenedores do AUR ainda são referidos como TUs (Trusted Users).

Entre 2015-06-08 e 2015-08-08, o AUR mudou da versão 3.5.1 para 4.0.0, introduzindo o uso de repositórios Git para publicação dos `PKGBUILD`s. Os pacotes existentes foram descartados, a menos que migrados manualmente para a nova infraestrutura por seus mantenedores.

## Repositórios Git para pacotes AUR3

O [Arquivo do AUR](https://github.com/aur-archive) no GitHub possui um repositório para cada repositório que estava no AUR 3 durante a migração para o AUR 4 em Agosto de 2015. Alternativamente, há o repositório [aur3-mirror](https://github.com/felixonmars/aur3-mirror/) que fornece o mesmo conteúdo.

## Instalando pacotes

A instalação de pacotes do AUR é um processo relativamente simples. Essencialmente:

1.  Obtenha os arquivos de compilação, incluindo o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e possivelmente outros arquivos necessários, como unidades [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") e patches (geralmente não o código em si).
2.  Certifique-se de que o `PKGBUILD` e os arquivos que o acompanham não são maliciosos ou duvidosos.
3.  Execute `makepkg -si` no diretório onde os arquivos foram salvos. Isso vai baixar o código, resolver as dependências com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), compilá-lo, empacotá-lo e instalar o pacote.

**Nota:** É *sua responsabilidade* acompanhar atualizações de pacotes no AUR; o *pacman* só acompanha [repositórios de binários](/index.php/Pacman_(Portugu%C3%AAs)#Repositórios_e_espelhos "Pacman (Português)"). Quando pacotes nos repositórios oficiais são atualizados, você precisará recompilar quaisquer pacotes do AUR que dependam deles.

### Pré-requisitos

Primeiro, certifique-se de que as ferramentas necessárias estão instaladas, [instalando](/index.php/Instale "Instale") todo o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), o qual inclui [make](https://www.archlinux.org/packages/?name=make) e outras ferramentas necessárias para a compilação do código-fonte.

**Nota:** Os pacotes do AUR presumem que o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está instalado, isto é, eles não listarão explicitamente os membros deste grupo como dependências

Em seguida, escolha o diretório de compilação adequado. Um diretório de compilação é apenas um diretório no qual o pacote será feito ou "compilado" e pode ser em qualquer diretório. Os exemplos nas seguintes seções usarão `~/builds` como o diretório de compilação.

### Obtendo arquivos de compilação

Localize o pacote no AUR. Isso pode ser feito usando o campo de pesquisa no topo da [página inicial do AUR](https://aur.archlinux.org/). Ao clicar no nome do aplicativo na lista de resultados de pesquisa, será mostrada uma página de informações sobre o pacote. Leia atentamente a descrição para confirmar que esse é o pacote desejado, veja quando o pacote foi atualizado pela última vez e leia quaisquer comentários.

Há vários métodos para adquirir os arquivos de compilação:

*   Opção 1: Clonar o repositório [git](/index.php/Git "Git") que está rotulado como o "Git Clone URL" em "Detalhes do pacote". Esse é o método preferível.

```
$ git clone https://aur.archlinux.org/*nome_pacote*.git

```

	Uma vantagem deste método é que você pode facilmente obter atualizações para o pacote vi `git pull`.

*   Opção 2: Baixar os arquivos de compilação com seu navegadores web clicando no link "Baixar snapshot" sob "Ações do Pacote", no canto direito da tela. Isso vai baixar um arquivo compactado, que deve ser extraído (preferivelmente em um diretório definido a parte para compilações do AUR)

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

**Atenção:** Verifique cuidadosamente o `PKGBUILD`, qualquer arquivo *.install* e quaisquer outros arquivos no repositório git do pacote para comandos maliciosos ou perigosos. Em caso de dúvida, não crie o pacote e nem [peça conselho](/index.php/General_troubleshooting#Additional_support "General troubleshooting") no fórum ou na lista de discussão. Código malicioso foi encontrado em pacotes antes. [[1]](https://lists.archlinux.org/pipermail/aur-general/2018-July/034151.html)

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
*   `-i`/`--install` instala o pacote se ele foi compilado com sucesso. Alternativamente, o pacote compilado pode ser instalado com `pacman -U *nome_pacote*.pkg.tar.xz`.

Outras flags úteis são

*   `-r`/`--rmdeps` remove dependências de tempo de compilação após a compilação, já que elas não mais são necessárias. Porém, essas dependências pode precisar serem reinstaladas da próxima vez que o pacote for atualizado.
*   `-c`/`--clean` limpa os arquivos temporários de compilação após a compilação, já que eles não mais são necessários. Esses arquivos geralmente são necessários apenas ao depurar o processo de compilação.

**Nota:** O exemplo acima é apenas um resumo breve do processo de compilação. É **altamente** recomendado ler os artigos [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") para mais detalhes.

## Feedback

O AUR fornece várias formas para usuários se comunicarem com mantenedores de pacote, desde que eles criem uma conta na [Interface Web do AUR](https://aur.archlinux.org).

### Comentando em pacotes

Os comentários permitem que os usuários forneçam sugestões ou respondam a atualizações e mantenedores para responder aos usuários ou fazer anúncios. Há suporte à sintaxe [Python-Markdown](https://python-markdown.github.io/), que fornece a sintaxe [Markdown](https://en.wikipedia.org/wiki/pt:Markdown "wikipedia:pt:Markdown") básica para formatação. Os mantenedores podem fixar comentários clicando no botão de tachinha no canto superior direito.

**Nota:**

*   A implementação do markdown tem algumas [diferenças](https://python-markdown.github.io/#differences) ocasionais com as [regras de sintaxe](https://daringfireball.net/projects/markdown/syntax) oficiais.
*   Hashes de commit para o repositório [Git](/index.php/Git "Git") do pacote e referências a tíquetes do [Flyspray](/index.php/Flyspray "Flyspray") são convertidos para links automaticamente.
*   Comentários longos são recolhidos e podem ser expandidos sob demanda.

**Dica:** Evite colar patches ou `PKGBUILD`s na seção de comentários; eles rapidamente se tornam obsoletos e acabam desnecessariamente ocupando muito espaço. Em vez disso, envie esses arquivos por e-mail para o mantenedor, ou use um [pastebin](/index.php/Pastebin "Pastebin").

### Votando em pacotes

Uma das atividades mais fáceis para **todos** os usuários do Arch é navegar no AUR e **votar** em seus pacotes prediletos, usando a interface online. Todos os pacotes são elegíveis para serem adotados por um TU (Trusted User) para a inclusão no [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community"), e a contagem de votos é uma das coisas levadas em consideração nesse [processo](#Promovendo_pacotes_ao_repositório_community); votar é do interesse de todos!

Enquanto estiver logado, na página do AUR para um pacote, você pode clicar em "Votar neste pacote" em "Ações do Pacote" à direita. Também é possível votar a partir da linha de comando com [aurvote](https://aur.archlinux.org/packages/aurvote/), [aurvote-git](https://aur.archlinux.org/packages/aurvote-git/), [aur-auto-vote-git](https://aur.archlinux.org/packages/aur-auto-vote-git/) ou [aurvote-utils](https://aur.archlinux.org/packages/aurvote-utils/).

Alternativamente, se você tiver configurado a [autenticação ssh](#Autenticação), pode votar diretamente na linha de comando usando sua chave ssh e evitar a necessidade de salvar ou digitar sua senha do AUR.

```
ssh aur@aur.archlinux.org vote *nome_pacote*

```

### Marcando pacotes como desatualizados

Enquanto estiver logado, na página do AUR para um pacote, você pode clicar em "Marcar como desatualizado" em "Ações do pacote" à direita. Você também deve deixar um comentário indicando os detalhes do motivo pelo qual o pacote está desatualizado, de preferência incluindo links para um anúncio de lançamento ou um novo tarball de lançamento. Além disso, tente entrar em contato com o mantenedor diretamente por e-mail. Se não houver resposta após *duas semanas*, você poderá registrar uma solicitação para [tornar órfão](#Tornar_órfão) o pacote.

**Nota:** [Pacotes VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") não são considerados como desatualizados quando o `*pkgver*` muda; não marque-os, pois o mantenedor vai simplesmente desmarcar o pacote e ignorar você.

## Compartilhando e mantendo pacotes

Usuários podem compartilhar `PKGBUILD`s usando o Arch User Repository, o qual não contém pacote binário algum, mas permite aos usuários enviar `PKGBUILD`s, que podem ser baixados por outros. Esses `PKGBUILD`s são totalmente não-oficiais e não foram examinados completamente, então eles devem ser usados por sua conta e risco.

### Enviando pacotes

**Atenção:** Antes de tentar enviar um pacote, espera-se que você esteja familiarizado com os [Arch Packaging Standards](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch") (*padrões de empacotamento do Arch*) e todos os artigos sob "Artigos relacionados". Verifique cuidadosamente se o que você está enviando está correto. Pacotes que violam as regras podem ser excluídos sem qualquer aviso.

Se você de alguma forma esta incerto sobre um pacote ou o processo de compilação/envio mesmo após ler essa seção duas vezes, [envie o PKGBUILD para revisão](#Verificando_pacotes).

#### Regras de envio

Ao enviar um pacote para o AUR, observe as seguintes regras:

*   Os `PKGBUILD`s enviados devem estar em conformidade com os termos de licenciamento do conteúdo a ser empacotado. Nos casos em que é mencionado que "você não pode vincular" a downloads, ou seja, conteúdos que não são redistribuíveis, você pode usar apenas o nome do arquivo como fonte. Isso significa e exige que os usuários já tenham o fonte restrite no diretório de compilação antes de criar o pacote. Em caso de dúvida, pergunte.

*   Os `PKGBUILD`s enviados não devem duplicar os aplicativos em qualquer um dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"). Verifique a [base de dados oficial de pacotes](https://www.archlinux.org/packages/); se o pacote existir, **não** envie uma duplicata. Se o pacote oficial estiver desatualizado, sinalize-o como tal. Se o pacote oficial está quebrado, ou faltando um recurso padrão, por favor, envie um [relatório de erro](https://bugs.archlinux.org/).

	A única exceção a isso é para pacotes com recursos *extras* habilitados e/ou patches em comparação com os oficiais, caso em que `*pkgbase*` deve ser diferente para expressar isso. Por exemplo, um pacote para o GNU Screen contendo o patch da barra lateral poderia ser chamado de `screen-sidebar`. Além disso, o array `provides=('screen')` deve ser usado para evitar conflitos com o pacote oficial.

*   Não crie pacotes duplicados. [Verifique o AUR](#Começando) para ver se o pacote já existe. Se ele já tem um mantenedor, alterações podem ser submetidas em comentários para chamar atenção do mantenedor. Se o pacote não tem um mantenedor ou o mantenedor não responde, o pacote pode ser adotado e atualizado como precisar.

*   Certifique-se de que o pacote que você deseja é **útil**. Alguém mais vai querer usá-lo? Ele é extremamente especializado? Se mais de algumas poucas pessoas achariam esse pacote útil, ele é apropriado para envio.

	Os repositórios do AUR e oficiais servem par pacotes que, em geral, instalam softwares e conteúdo relacionados com software, incluindo um ou mais dos seguintes: executável(is); arquivo(s) de configuração; documentação online ou offline para softwares específicos ou a distribuição Arch Linux como um todo; mídia para ser usada diretamente por software.

*   Não use `replaces` em um `PKGBUILD` do AUR a menos que o pacote seja renomeado, por exemplo, quando *Ethereal* se tornou *Wireshark*. Se o pacote for uma versão alternativa **de um pacote já existente**, use `conflicts` (e `provides` se esse pacote for requerido por outras pessoas). A principal diferença é: após a sincronização (-Sy), o pacman imediatamente deseja substituir um pacote (alvo de substituição) instalado ao encontrar um pacote com os `replaces` correspondentes em qualquer lugar de seus repositórios; O `conflicts`, por outro lado, só é avaliado na instalação do pacote, que geralmente é o comportamento desejado, porque é menos invasivo.

*   O envio de binários *deve ser evitado* se os fontes estiverem disponíveis. O AUR não deve conter tarballs binários criados pelo makepkg, nem deve conter suas listas de arquivos. Consulte as [diretrizes de pacotes de aplicativos não livres](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres#Nomenclatura_de_pacotes "Diretrizes de pacotes de aplicativos não livres") em relação aos pacotes que redistribuem [deliverables](https://en.wikipedia.org/wiki/Deliverable em relação aos pacotes que redistribuir binários java.

*   Adicione uma [linha de comentário](http://man7.org/linux/man-pages/man1/bash.1.html#COMMENTS) ao topo do arquivo `PKGBUILD` que contém informações sobre os **mantenedores** atuais e **contribuidores** antigos, respeitando o formato a seguir. Lembre-se de disfarçar seu e-mail para protegê-lo contra spam. Linhas adicionais ou desnecessárias são facultativas.

	Se você está assumindo o papel de mantenedor para um `PKGBUILD` existente, adicione seu nome ao topo desta forma

```
# Maintainer: Seu Nome <endereço at domínio dot tld>

```

	Se houver mantenedores antigos, liste-os como contribuidores. O mesmo se aplica para quem enviou o pacote, se não foi você. Se você é um comantenedor, adicione os nome de outros mantenedores atuais também.

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

**Nota:** O repositório não estará vazio, se `*pkgbase*` corresponde a um pacote excluído.

Se você já tem um pacote, [inicialize-o](/index.php/Git#Getting_a_Git_repository "Git") como um repositório Git, se ainda não for um, e adicione um remoto do AUR:

```
$ git remote add *rótulo* ssh://aur@aur.archlinux.org/*pkgbase*.git

```

Então, faça um [fetch](/index.php/Git#Using_remotes "Git") deste remoto para inicializá-lo no AUR.

**Nota:** Use [pull e rebase](https://git-scm.com/docs/git-pull#git-pull---rebasefalsetruemergespreserveinteractive) para resolver conflitos se o `*pkgbase*` corresponder a um pacote excluído.

### Publicando novo conteúdo de pacote

**Atenção:** Seus commits terão como autor seu [nome e endereço de e-mail Git globais](/index.php/Git#Configuration "Git"). É muito difícil de alterar commits após você realizar o *push* ([FS#45425](https://bugs.archlinux.org/task/45425)). Se você deseja fazer o push para o AUR sob credenciais diferentes, você pode alterá-los por pacote com `git config user.name "..."` e `git config user.email "..."`.

Para enviar ou atualizar um pacote, [adicione](/index.php/Git#Staging_changes "Git") *pelo menos* o [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") e [.SRCINFO](/index.php/.SRCINFO ".SRCINFO"), e quaisquer arquivos novos ou modificados de [.install](/index.php/PKGBUILD_(Portugu%C3%AAs)#install "PKGBUILD (Português)"), [patches](/index.php/Aplica%C3%A7%C3%A3o_de_patch_em_pacotes "Aplicação de patch em pacotes") ououtros [arquivos fontes locais](/index.php/PKGBUILD_(Portugu%C3%AAs)#source "PKGBUILD (Português)"); [Faça commit](/index.php/Git#Committing_changes "Git") deles com uma mensagem de commit significativa e, finalmente, faça um [push](/index.php/Git#Push_to_a_repository "Git") das alterações para o AUR.

**Dica:** Para manter o diretório de trabalho e os commits o mais limpo possível, crie um [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5) que exclua todos os arquivos e adicione forçadamente os arquivos conforme necessário.

Por exemplo:

```
$ makepkg --printsrcinfo > .SRCINFO
$ git add -f PKGBUILD .SRCINFO
$ git commit -m "*mensagem útil de commit*"
$ git push

```

**Nota:**

*   Depois de modificar um pacote, exceto por pequenas alterações (como consertar um erro de digitação) que não exigirão a reinstalação do pacote, atualize sua [versão](/index.php/PKGBUILD#Version "PKGBUILD").
*   Regere `.SRCINFO` após atualizar tais metadados do `PKGBUILD` para publicá-lo no AUR.
*   Se o `.SRCINFO` foi adicionado antes do seu primeiro commit, adicione-o realizando o [rebase com --root](https://git-scm.com/docs/git-rebase#git-rebase---root) ou [filtrando a árvore](https://git-scm.com/docs/git-filter-branch#git-filter-branch---tree-filterltcommandgt), de forma que o AUR permita seu push inicial.

### Mantendo pacotes

*   Verifique os feedback e comentários de outros usuários e tente incorporar quaisquer melhorias que eles sugerirem; considere isso um processo de aprendizado!
*   Por favor, não envie um comentário contendo a versão toda vez que você atualizar o pacote. Isso deixa a seção de comentário usável para o conteúdo valioso mencionado acima.
*   Por favor, não apenas envie e depois esqueça dos pacotes! É trabalho do mantenedor manter o pacote, verificando atualizações e melhorando o `PKGBUILD`.
*   Se você não deseja continuar mantendo o pacote por algum motivo, basta tornar órfão o pacote clicando em "Abandonar pacote" sob "Ações do pacote" no lado direito da página AUR e/ou postar uma mensagem na Lista de Discussão do AUR. Se todos os mantenedores de um pacote AUR o abandonarem, ele se tornará um pacote ["órfão"](https://aur.archlinux.org/packages/?SB=n&do_Orphans=Orphans).

### Outras requisições

Requisições para [excluir](#Excluir), [mesclar](#Mesclar) e [tornar órfão](#Tornar_órfão) podem ser criadas clicando no link "Enviar requisição" sob "Ações do pacote" à direita da tela. Isso vai enviar uma notificação de e-mail para o atual mantenedor e para a [lista de discussão aur-requests](https://mailman.archlinux.org/mailman/listinfo/aur-requests) para debate. Um [Trusted User](/index.php/Trusted_User_(Portugu%C3%AAs) "Trusted User (Português)") vai então aceitar ou rejeitar a requisição.

#### Excluir

**Dica:** Em inglês, esse tipo de requisição é comumente referido como *Deletion request*

Você pode pedir para *não mais listar* um `*pkgbase*` do AUR. Uma nota curta explicando o motivo pelo qual a exclusão é necessária, bem como detalhes de suporte (como quando um pacote é fornecido por outro pacote, se você for o mantenedor, ele é renomeado e o proprietário original concordou, etc).

**Nota:**

*   Não é suficiente explicar porquê um pacote deve ser excluído apenas em seus comentários, pois assim que um TU realiza a exclusão, o único lugar que vai manter a tal informação será o e-mail na lista de discussão do aur-requests.
*   Requisições para excluir podem ser negadas, caso em que, se você for o mantenedor, você provavelmente será aconselhado a tornar órfão o pacote para permitir a adoção por outro mantenedor.
*   Após um pacote ser "excluído", seu repositório [git](/index.php/Git "Git") permanece disponível para [clonagem](#Obtendo_arquivos_de_compilação).

#### Mesclar

**Dica:** Em inglês, esse tipo de requisição é comumente referido como *Merge request*

Você pode requisitar a exclusão de um `*pkgbase*` e transferência de seus votos e comentários para outro `*pkgbase*`. O nome do pacote alvo da mesclagem é necessário.

**Nota:** Isso tem nada a ver com 'git merge' ou merge requests do GitLab.

#### Tornar órfão

**Dica:** Em inglês, esse tipo de requisição é comumente referido como *Orphan request*

Você pode requisitar que um `*pkgbase*` se seja tornado órfão, ou seja, que o mantenedor atual perca esta posição. Essas requisições serão concedidas após duas semanas se o mantenedor atual não reagir.

### Promovendo pacotes ao repositório community

Quando os pacotes AUR recebem bastante interesse da comunidade e o suporte de um [Trusted User](/index.php/Trusted_User_(Portugu%C3%AAs) "Trusted User (Português)"), eles podem ser adotados no [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community") (mantido pelos TUs), do qual os pacotes binários podem ser instalados usando [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

Geralmente, pelo menos 10 [votos](#Votando_em_pacotes) são necessários para que alguma coisa se mova para *community*. No entanto, se uma TU quiser dar suporte a um pacote, ele geralmente será encontrado no repositório.

Votos suficientes não são o único requisito; tem que haver um TU disposto a manter o pacote. Os TUs não são obrigados a adotar um pacote, mesmo que tenha milhares de votos.

Geralmente, quando um pacote muito popular fica no AUR é porque:

*   Arch Linux já tem outra versão de um pacote nos repositórios.
*   Sua licença proíbe redistribuição.
*   Ele ajuda a obter `PKGBUILD`s enviados pelos usuários ([auxiliares do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR")).

Veja também [[Diretrizes de Trusted User do AUR#Regras para a Entrada de Pacotes no Repositório [community]|Regras para a Entrada de Pacotes no Repositório community]].

## Verificando pacotes

Se você está tendo problemas para criar um pacote, leia seu [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e os comentários em sua página AUR. É possível que um `PKGBUILD` esteja quebrado para todos. Se você não conseguir descobrir sozinho, informe ao mantenedor (por exemplo, [publicando os erros que você está recebendo nos comentários na página AUR](#Comentando_em_pacotes)). Você também pode procurar ajuda no fórum [AUR Issues, Discussion & PKGBUILD Requests](https://bbs.archlinux.org/viewforum.php?id=38).

Para evitar problemas causados por sua configuração de sistema particular, compile pacotes em um [chroot limpo](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot"). Se o processo de compilação ainda falhar em um chroot limpo, o problema provavelmente está no `PKGBUILD`.

Veja [Criando pacotes#Verificando sanidade do pacote](/index.php/Criando_pacotes#Verificando_sanidade_do_pacote "Criando pacotes") para como usar o *namcap* para depurar pacotes. Se você quiser ter um `PKGBUILD` revisado, poste-o na [lista de discussão aur-general](https://mailman.archlinux.org/mailman/listinfo/aur-general) para obter feedback dos TUs e outros membros do AUR, ou no fórum [Creating & Modifying Packages](https://bbs.archlinux.org/viewforum.php?id=4). Você também pode procurar ajuda no [canal IRC](/index.php/Canal_IRC "Canal IRC") [#archlinux-aur](ircs://chat.freenode.net/archlinux-aur) no [Freenode](https://freenode.net/)

Evite armadilhas comuns:

1.  Certifique-se que seu ambiente de compilação está atualizado [atualizando](/index.php/Pacman_(Portugu%C3%AAs)#Atualizando_pacotes "Pacman (Português)") antes de compilar qualquer coisa.
2.  Certifique-se que você tenha os grupos [base](https://www.archlinux.org/groups/x86_64/base/) e [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) instalados.
3.  Use a opção `-s` com *makepkg* para verificar e instalar todas as dependências necessárias antes de iniciar o processo de compilação.
4.  Tente a [configuração padrão do makepkg](https://git.archlinux.org/svntogit/packages.git/tree/trunk/makepkg.conf?h=packages/pacman).
5.  Veja [Makepkg (Português)#Solução de problemas](/index.php/Makepkg_(Portugu%C3%AAs)#Solução_de_problemas "Makepkg (Português)") para problemas comuns.

## Tradução da interface web

Veja [i18n.txt](https://projects.archlinux.org/aurweb.git/tree/doc/i18n.txt) na árvore de arquivos fontes do AUR para informações sobre criação e manutenção de tradução da interface web do AUR.

## FAQ

### O que é o AUR?

O AUR (Arch User Repository) é um lugar para onde a comunidade do Arch Linux pode enviar [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") de aplicativos, bibliotecas, etc., e compartilhá-los com toda a comunidade. Outros usuários poderão então votar pelos seus favoritos para que sejam transferidos para o [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community") de forma a serem compartilhados com os usuários do Arch Linux em forma de binário.

### Que tipo de pacote é permitido no AUR?

Para a maioria dos casos, tudo é permitido, sujeito às [#Regras de envio](#Regras_de_envio).

### Como posso votar em pacotes no AUR?

Veja [#Votando em pacotes](#Votando_em_pacotes).

### O que é um Trusted User / TU?

Um [(Trusted User)](/index.php/AUR_Trusted_User_Guidelines_(Portugu%C3%AAs) "AUR Trusted User Guidelines (Português)"), abreviado como TU, é uma pessoa que é escolhida para supervisionar o AUR e o [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community"). Eles são os que mantêm `PKGBUILD`s populares no *community* e de forma geral mantêm o AUR funcionando.

### Qual é a diferença entre o Arch User Repository e repositório [community]?

Os pacotes AUR são mantidos pelos membros da comunidade e fornecidos em formato fonte, enquanto os pacotes no [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community") são mantidos pelos [Trusted Users](/index.php/Trusted_Users_(Portugu%C3%AAs) "Trusted Users (Português)") e fornecidos em formato binário pré-compilado. Veja [#Promovendo pacotes ao repositório community](#Promovendo_pacotes_ao_repositório_community) para mais informações.

### Foo no AUR está desatualizado; o que devo fazer?

Veja [#Marcando pacotes como desatualizados](#Marcando_pacotes_como_desatualizados).

Neste meio tempo, você pode tentar atualizar o pacote você mesmo editando o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") localmente. Ás vezes, atualizações não exigem qualquer alteração para o processo de compilação ou empacotamento, caso em que apenas atualizar o vetor `pkgver` ou `source` é suficiente.

### Foo no AUR não compila quando eu executo makepkg; o que devo fazer?

Provavelmente está deixando escapar alguma coisa trivial; veja [#Verificando pacotes](#Verificando_pacotes).

### ERRO: Uma ou mais assinaturas PGP não puderam ser verificadas!; o que eu devo fazer?

Veja [Makepkg (Português)#ERRO: Uma ou mais assinaturas PGP não puderam ser verificadas!; o que eu devo fazer?](/index.php/Makepkg_(Portugu%C3%AAs)#ERRO:_Uma_ou_mais_assinaturas_PGP_não_puderam_ser_verificadas!;_o_que_eu_devo_fazer? "Makepkg (Português)").

### Como eu crio um PKGBUILD?

Certifique-se de verificar o AUR para evitar esforços duplicados, e então veja [criando pacotes](/index.php/Criando_pacotes "Criando pacotes").

### Eu tenho um PKGBUILD que queria enviar; alguém pode verificá-lo para ver se ele tem algum erro?

Há vários canais disponíveis para você enviar seu pacote para revisão; veja [#Verificando pacotes](#Verificando_pacotes).

### Como que faz para um PKGBUILD ir para o repositório *community*?

Veja [#Promovendo pacotes ao repositório community](#Promovendo_pacotes_ao_repositório_community).

### Como o posso agilizar processo de repetidas compilações?

Veja [Makepkg (Português)#Melhorando os tempos de compilação](/index.php/Makepkg_(Portugu%C3%AAs)#Melhorando_os_tempos_de_compilação "Makepkg (Português)").

### Qual é a diferença entre pacotes foo e foo-git

Muitos pacotes AUR vêm em versões "estáveis" e "instáveis" de desenvolvimento. Os pacotes de desenvolvimento geralmente têm um [sufixo](/index.php/Diretrizes_de_pacotes_VCS#Diretrizes "Diretrizes de pacotes VCS") denotando seu [Sistema de controle de versões](/index.php/Version_Control_System "Version Control System") e não se destinam ao uso regular, mas podem oferecer novos recursos ou correções de erros. Como esses pacotes só fazem o download da última fonte disponível quando você executa o *makepkg*, o `pkgver` no AUR não reflete as mudanças do upstream. Da mesma forma, esses pacotes não podem realizar uma soma de verificação de autenticidade em nenhuma [fonte VCS](/index.php/Diretrizes_de_pacotes_VCS#Fontes_VCS "Diretrizes de pacotes VCS").

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
*   Use *aurpkglist* do [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Veja também

*   [Interface Web do AUR](https://aur.archlinux.org)
*   [Lista de Discussão do AUR](https://lists.archlinux.org/listinfo/aur-general)
*   [DeveloperWiki:AUR Cleanup Day](/index.php/DeveloperWiki:AUR_Cleanup_Day "DeveloperWiki:AUR Cleanup Day")