Esse artigo objetiva auxiliar usuários na criação de seus próprios pacotes usando o [sistema de compilação](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)") "tipo *ports*" do Arch Linux, também para enviou ao [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Ele cobre criação de um [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") – um arquivo de descrição de compilação de pacote carregado pelo `makepkg` para criar um pacote binário a partir do fonte. Se já estiver em posse de um `PKGBUILD`, veja [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"). Para instruções sobre regras e formas existentes para melhorar a qualidade de pacote, veja [Padrões de empacotamento do Arch](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch").

## Contents

*   [1 Visão Geral](#Vis.C3.A3o_Geral)
    *   [1.1 Pacotes meta e grupos](#Pacotes_meta_e_grupos)
*   [2 Preparação](#Prepara.C3.A7.C3.A3o)
    *   [2.1 Pré-requisito de software](#Pr.C3.A9-requisito_de_software)
    *   [2.2 Baixe e teste a instalação](#Baixe_e_teste_a_instala.C3.A7.C3.A3o)
*   [3 Criação de um PKGBUILD](#Cria.C3.A7.C3.A3o_de_um_PKGBUILD)
    *   [3.1 Definindo as variáveis do PKGBUILD](#Definindo_as_vari.C3.A1veis_do_PKGBUILD)
    *   [3.2 Funções do PKGBUILD](#Fun.C3.A7.C3.B5es_do_PKGBUILD)
        *   [3.2.1 prepare()](#prepare.28.29)
        *   [3.2.2 pkgver()](#pkgver.28.29)
        *   [3.2.3 build()](#build.28.29)
        *   [3.2.4 check()](#check.28.29)
        *   [3.2.5 package()](#package.28.29)
*   [4 Teste do PKGBUILD e pacote](#Teste_do_PKGBUILD_e_pacote)
    *   [4.1 Verificando sanidade do pacote](#Verificando_sanidade_do_pacote)
*   [5 Enviando pacotes para o AUR](#Enviando_pacotes_para_o_AUR)
*   [6 Resumo](#Resumo)
    *   [6.1 Avisos](#Avisos)
*   [7 Diretrizes mais detalhadas](#Diretrizes_mais_detalhadas)
*   [8 Veja também](#Veja_tamb.C3.A9m)

## Visão Geral

Pacotes no Arch Linux são compilados usando o utilitário [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e as informações armazenadas em um arquivo [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"). Quando `makepkg` é executado, ele pesquisa por um `PKGBUILD` no diretório atual e segue as instruções nele para obter os arquivos necessários e/ou compilá-los para serem empacotados dentro do arquivo de pacote (`pkgname.pkg.tar.xz`). O pacote resultante contém arquivos binários e instruções de instalação prontos para serem instalados pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

Um pacote do Arch é nada mais que um pacote tar, ou "tarball", comprimido usando xz, que contém os seguintes arquivos gerados pelo makepkg:

*   Os arquivos binários para serem instalados.
*   `.PKGINFO`: contém todos os metadados necessários pelo pacman para lidar com pacotes, dependências, etc.
*   `.MTREE`: contém *hashes* e *timestamps* dos arquivos, que são incluídos na base de dados local de forma que o pacman possa verificar a integridade do pacote.
*   `.INSTALL`: um arquivo opcional usado para executar comandos após o estágio instalação/atualização/remoção. (Esse arquivo está presente apenas se especificado no `PKGBUILD`.)
*   `.Changelog`: um arquivo opcional mantido pelo mantenedor do pacote documentando as chances do pacote. (Ele não está presente em todos pacotes.)

### Pacotes meta e grupos

Um grupo de pacotes é um conjunto de pacotes relacionados, definido pelo empacotador, que pode ser instalado ou desinstalado simultaneamente usando o nome de grupo como um substituto para cada nome de pacote individual. Enquanto um grupo não é um pacote, ele pode ser instalado de forma similar a um pacote, veja [Pacman (Português)#Instalando grupos de pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_grupos_de_pacotes "Pacman (Português)") e [PKGBUILD (Português)#groups](/index.php/PKGBUILD_(Portugu%C3%AAs)#groups "PKGBUILD (Português)").

Um pacote meta, frequentemente (mas nem sempre) intitulado com o sufixo *-meta*, fornece funcionalidade similar a um grupo de pacotes no sentido que ele permite múltiplos pacotes relacionados serem instalados ou desinstalados simultaneamente. Pacotes meta podem ser instalados como qualquer outro pacote, veja [Pacman (Português)#Instalando pacotes específicos](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_pacotes_espec.C3.ADficos "Pacman (Português)"). A única diferença entre um pacote meta e um pacote comum é que um pacote meta é vazio e existe apenas para fazer um vínculo de pacotes relacionados por meio de dependências.

A vantagem de um pacote meta, comparado com um grupo, é que quaisquer novos pacotes membros serão instalados quando o pacote meta em si for atualizado com um novo conjunto de dependências. Isso é um contraste a um grupo em que novos membros de grupos não serão instalados automaticamente. A desvantagem de um pacote meta é que ele não é tão flexível quanto um grupo — você pode escolher quais membros do grupo você deseja instalar, mas não pode escolher qual dependência do pacote meta você deseja instalar. Da mesma forma, você pode desinstalar membros do grupo sem ter que remover todo o grupo, porém você não pode remover dependências de pacotes meta sem ter que desinstalar o pacote meta em si.

## Preparação

### Pré-requisito de software

Primeiro se certifique de que as ferramentas necessárias estão instaladas. [Instalar](/index.php/Instale "Instale") o grupo de pacotes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) deve ser o suficiente; ele inclui **make** e ferramentas adicionais necessárias para compilar a partir do código-fonte.

Uma das ferramentas chaves para compilar pacotes é o [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") (fornecido pelo [pacman](https://www.archlinux.org/packages/?name=pacman)), que faz o seguinte:

1.  Verifica se as dependências do pacote estão instaladas.
2.  Baixa os arquivos fontes dos servidores especificados.
3.  Desempacota os arquivos fontes.
4.  Compila o software e instala-o sob um ambiente *fakeroot*.
5.  Remove os símbolos de binários e bibliotecas.
6.  Gera o arquivo meta do pacote que é incluído em cada pacote.
7.  Comprime o ambiente *fakeroot* em um arquivo de pacote.
8.  Armazena o arquivo de pacote no diretório de destino configurado, o qual é o diretório de trabalho atual por padrão.

### Baixe e teste a instalação

Baixe o tarball fonte do software se você deseja empacotá-lo, extraí-lo e seguir as etapas do autor para instalar o programa. Tome nota de todos os comandos e/ou etapas necessários para compilar e instalar. Você estará repetindo os mesmos comandos no arquivo *PKGBUILD*.

A maioria dos autores de software seguem o ciclo de compilação em 3 etapas:

```
./configure
make
make install

```

Esse é um bom momento para se certificar o programa está funcionando corretamente.

## Criação de um PKGBUILD

Quando você executa `makepkg`, ele vai procurar por um arquivo `PKGBUILD` no diretório de trabalho atual. Se um arquivo `PKGBUILD` for localizado, ele vai baixar o código-fonte do software e compilá-lo de acordo com as instruções especificadas no arquivo `PKGBUILD`. As instruções devem ser completamente interpretáveis pelo shell [Bash](https://en.wikipedia.org/wiki/pt:Bash "wikipedia:pt:Bash"). Após concluir com sucesso, os binários resultantes e metadados do pacote, isto é, informações de versão e dependências do pacote, são empacotados em um arquivo de pacote `pkgname.pkg.tar.xz` que pode ser instalado com `pacman -U *<arquivo de pacote>*`.

Para começar com um novo pacote, você deve primeiro criar um diretório de trabalho vazio, mudar para aquele diretório, e criar um arquivo `PKGBUILD`. Você pode copiar o protótipo de PKGBUILD do diretório `/usr/share/pacman/` para seu diretório de trabalho ou copiar um `PKGBUILD` de um pacote similar. A última opção pode ser útil se você só precisar alterar algumas opções.

### Definindo as variáveis do PKGBUILD

Exemplos de PKGBUILDs estão localizados em `/usr/share/pacman/`. Uma explicação das variáveis possíveis no `PKGBUILD` pode ser encontrada no artigo [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)").

*makepkg* define duas variáveis que você não deve usar como parte do processo de compilação e instalação:

	`srcdir`

	aponta para o diretório no qual *makepkg* extrai e cria links simbólicos no vetor fonte.

	`pkgdir`

	aponta para o diretório no qual *makepkg* empacota o software instalado, o qual se torna o diretório raiz de seu pacote compilado.

Todos eles contêm caminhos *absolutos*, o que significa que você não tem que se preocupar com seu diretório de trabalho, se você usar essas variáveis adequadamente.

**Note:** *makepkg*, e portanto as funções `build()` e `package()`, são feitas para serem não interativas. Utilitários interativos ou scripts chamados naquelas funções podem quebrar o *makepkg*, principalmente se for invocada com registro de log de compilação habilitado (`-L`). (Veja [FS#13214](https://bugs.archlinux.org/task/13214).)

**Note:** Com exceção do *Maintainer* atual do pacote, pode haver mantenedores anteriores listados acima como *Contributors*.

### Funções do PKGBUILD

Há cinco funções, listadas aqui na ordem em que elas são executadas, se todas elas existirem. Se uma não existir, ela é simplesmente ignorada.

**Note:** Note que isso não se aplica à função `package()`, já que ela é exigida em todo PKGBUILD

#### prepare()

Nessa função, comandos que são usados para preparar fontes para compilação são executados, tal como [patching](/index.php/Patching_in_ABS "Patching in ABS"). Essa função é executada após a extração do pacote, antes do [pkgver()](#pkgver.28.29) e a função de compilação. Se a extração for ignorada (`makepkg -e`), então `prepare()` não é executada.

**Note:** (De `man PKGBUILD`) A função é executada no modo `bash -e`, o que significa que qualquer comando que sair com um status não-zero fará com que a função saia.

#### pkgver()

`pkgver()` é executado após os fontes serem obtidos, extraídos e o [prepare()](#prepare.28.29) executado. Então, você pode atualizar a variável *pkgver* durante um estágio do makepkg.

Isso é particularmente útil se você estiver [fazendo pacote git/svn/hg/etc.](/index.php/VCS_PKGBUILD_Guidelines "VCS PKGBUILD Guidelines"), nos quais o processo de compilação pode se manter o mesmo, mas o fonte não puder ser atualizado todo dia, ou toda hora. A forma antiga de fazer isso é colocar a data no campo *pkgver* que, se o software não fosse atualizado, makepkg ainda iria recompilá-lo pensando que a versão foi alterada. Alguns comandos úteis para isso são `git describe`, `hg identify -ni`, etc. Por favor, teste antes de enviar um PKGBUILD, já que uma falha na função `pkgver()` pode parar um processo de compilação.

**Note:** pkgver não pode conter espaços ou hífens (`-`). Usar sed para corrigir isso é comum.

#### build()

Agora você precisa implementar a função `build()` no arquivo `PKGBUILD`. Essa função usa comandos comuns de shell com sintaxe [Bash](https://en.wikipedia.org/wiki/pt:Bash "wikipedia:pt:Bash") para compilar automaticamnete o software e criar um diretório `pkg` para instalar o software. Isso permite que o *makepkg* empacote arquivos sem ter que examinar seu sistema de arquivos.

A primeira etapa na função `build()` é alterar para o diretório criado ao descompactar o tarball fonte. *makepkg* vai alterar o diretório atual para `$srcdir` antes de executar a função `build()`. Por tanto, na maioria dos casos, como sugerido no `/usr/share/pacman/PKGBUILD.proto`, o primeiro comando se parece com isso:

```
cd "$pkgname-$pkgver"

```

Agora, você precisa listar os mesmos comandos que você usou quando compilou manualmente o software. A função `build()`, essencialmente, automatiza tudo que você fez manualmente e compila o software no ambiente *fakeroot* de compilação. SE o software que você está empacotando usa um script de compilação, é uma boa prática usar `--prefix=/usr` ao compilar pacotes para o pacman. Muitos softwares instalam arquivos relativos ao diretório `/usr/local`, o que deve ser feito apenas se você está compilando manualmente do fonte. Todos os pacotes do Arch Linux devem usar o diretório `/usr`. Como visto no arquivo `/usr/share/pacman/PKGBUILD.proto`, as próximas duas linhas geralmente se parecem com isso:

```
./configure --prefix=/usr
make

```

**Note:** Se seu software não precisa compilar nada, NÃO use a função `build()`. A função `build()` não é obrigatória, mas a função `package()` é.

#### check()

Lugar para as chamadas de `make check` ou rotinas de teste similares. É altamente recomendado ter um `check()` já que ela ajuda a se certificar que o software foi compilado corretamente e funciona bem com suas dependências.

Usuários que não precisam dela (e ocasionalmente mantenedores que não corrigem um pacote para isso passar) podem desabilitá-la usando `BUILDENV+=('!check')` no PKGBUILD/makepkg.conf ou chamar `makepkg` com a opção `--nocheck`.

#### package()

A etapa final é colocar os arquivos compilados em um diretório no qual *makepkg* possa obtê-los para criar um pacote. Isso por padrão é o diretório `pkg`—um ambiente *fakeroot* simples. O diretório `pkg` replica a hierarquia do sistema de arquivos raiz dos caminhos de instalação do software. Se você tiver que colocar arquivos manualmente sob a raiz de seu sistema de arquivos, você deveria instalá-los no diretório `pkg` sob a mesma estrutura. Por exemplo, se você deseja instalar um arquivo no `/usr/bin`, ele deveria ser colocado sob `$pkgdir/usr/bin`. Muito poucos procedimentos de instalação exibem que o usuário copie diversos arquivos manualmente. Em vez disso, para a maioria dos softwares, chamar `make install` servirá. A linha final deve se parecer com o seguinte para instalar corretamente o software no diretório `pkg`:

```
make DESTDIR="$pkgdir/" install

```

**Note:** Algumas vezes é caso do `DESTDIR` não ser usado no `Makefile`; em vez disso, você pode precisar usar `prefix`. Se o pacote é compilado com *autoconf* / *automake*, use `DESTDIR`; isso é o que está [documentado](https://www.gnu.org/software/automake/manual/automake.html#Install) nos manuais. Se `DESTDIR` não funcionar, tente compilar com `make prefix="$pkgdir/usr/" install`. Se isso não funcionar, você terá que olhar mais profundamente nos comandos de instalação que são executados por "`make <...> install`".

Alguns casos estranhos, softwares esperam ser executados de um único diretório. Em tais casos, é sábio copiá-los para `$pkgdir/opt`.

Com uma certa frequência o processo de instalação criará um subdiretório dentro do diretório `pkg`. Se ele não criar, porém, *makepkg* vai gerar vários erros e você precisará criar manualmente os subdiretórios adicionando os comandos `mkdir -p` apropriados na função `build()` antes do procedimento de instalação ser executado.

Em pacotes antigos, não havia uma função `package()`. Então, arquivos eram colocados no diretório *pkg* no final da função `build()`. Se `package()` estiver presente, `build()` executa via *fakeroot*. Em novos pacotes, `package()` é exigido e executa via *fakeroot*, e `build()` executa sem quaisquer privilégios em especial.

`makepkg --repackage` executa apenas a função `package()`, então ele cria um arquivo `*.pkg.*` sem compilar o pacote. Isso pode economizar tempo, por exemplo, se você tiver alterado apenas a variável `depends` do pacote.

**Note:** A função `package()` é a única função exigida em um PKGBUILD. Se você só precisa copiar arquivos para seus respectivos diretórios para instalar um programa, não coloque isso na função `build()`, e sim na função `package()`.

**Note:** Criar links simbólicos é um processo ligeiramente estranho na função `package()`. Usando a abordagem ingênua `ln -s "${pkgdir}/de/foo" "${pkgdir}/para/goo"` vai resultar em um link simbólico para o diretório de compilação. A forma apropriada de criar um link é criá-lo apontando para uma fonte inicialmente quebrada, `ln -s "/de/foo" "${pkgdir}/para/goo"`. Uma vez o pacote esteja instalado, o link vai apontar para o lugar correto.

## Teste do PKGBUILD e pacote

Na medida em que você escreve a função `build()`, você vai querer testar suas alterações frequentemente para se assegurar de que não há falhas. Você pode fazer isso usando o comando `makepkg` no diretório contendo o arquivo `PKGBUILD`. Com um `PKGBUILD` formatado corretamente, makepkg vai criar um pacote; com um `PKGBUILD` quebrado ou incompleto, ele vai gerar erros.

Se makepkg finalizar com sucesso, ele vai colocar um arquivo chamado `pkgname-pkgver.pkg.tar.xz` em seu diretório de trabalho. Esse pacote pode ser instalado com o comando `pacman -U`. Porém, só porque um aquivo de pacote foi compilado não significa que ele está totalmente funcional. Ele pode conter apenas o diretório e nenhum arquivo se, por exemplo, um prefixo foi especificado equivocadamente. Você pode usar as funções de consulta do pacman para exibir uma lista de aquivos contidos no pacote e as dependências que ele exige com `pacman -Qlp [arquivo do pacote]` e `pacman -Qip [arquivo de pacote]`, respectivamente.

Se o pacote parecer estar bom, então você está pronto! Porém, se você planeja lançar o arquivo `PKGBUILD`, é imperativo que você verifique, e verifique de novo, o conteúdo do vetor `depends`.

Além disso, certifique-se de que os binários do pacote realmente são *executados* sem falha alguma! É irritante lançar um pacote que contém todos os arquivos necessários, mas trava por causa de alguma opção de configuração obscura que não funciona bem com o resto do sistema. Se você vai apenas compilar pacotes para o seu próprio sistema, você não precisa se preocupar tanto sobre a etapa de verificação de qualidade, pois, no final das contas, você é a única pessoa que sofrerá pelos equívocos.

### Verificando sanidade do pacote

Após testar a funcionalidade do pacote, verifique-o por erros usando o [namcap](/index.php/Namcap "Namcap"):

```
$ namcap PKGBUILD
$ namcap *<nome do arquivo do pacote>*.pkg.tar.xz

```

Namcap vai:

1.  Verificar o conteúdo do PKGBUILD por erros comuns e hierarquia de arquivos do pacote por arquivos desnecessários/colocados em lugar indevido
2.  Varrer todos os arquivos ELF no pacote usando `ldd`, relatando automaticamente quais pacotes com as bibliotecas compartilhadas estão faltando no `depends` e quais podem ser omitidas como dependências transitivas
3.  Pesquisar heuristicamente por dependências em falta ou redundantes

e muito mais. Se habitue a verificar seus pacotes com namcap para evitar de ter que corrigir os erros mais simples após envio do pacote.

## Enviando pacotes para o AUR

Por favor, leia [AUR (Português)#Enviando pacotes](/index.php/AUR_(Portugu%C3%AAs)#Enviando_pacotes "AUR (Português)") para uma descrição detalhada do processo de envio.

## Resumo

1.  Baixe o tarball fonte do software que você deseja empacotar.
2.  Tente compilar o pacote e instalá-lo em um diretório arbitrário.
3.  Copie o protótipo `/usr/share/pacman/PKGBUILD.proto` e renomeie-o para `PKGBUILD` em um diretório de trabalho temporário.
4.  Edite o `PKGBUILD` de acordo com as necessidades do seu pacote.
5.  Execute `makepkg` e veja se o pacote resultante é compilado corretamente.
6.  Se não, repita as últimas duas etapas.

### Avisos

*   Antes de você automatizar o processo de compilação do pacote, você deve tê-lo feito manualmente pelo menos uma vez, a menos que você saiba *exatamente* o que você está fazendo *desde já*, caso em que você não precisaria estar lendo isso em primeiro lugar. Infelizmente, apesar de uma boa quantidade de autores de programas seguirem o ciclo de compilação de 3 etapas de "`./configure`; `make`; `make install`", não é sempre que isso ocorre e as coisas podem dar muito errado se você tiver que aplicar patches para fazer tudo funcionar. Regra do polegar: Se você não puder fazer o programa compilar a partir do tarball fonte e fazê-lo ser instalado para um subdiretório temporário definido, você não precisa se quer empacotá-lo. Não há nenhum pozinho mágico no `makepkg` que faça os problemas do código-fonte sumirem.
*   Em alguns casos, os pacotes nem mesmo estão disponíveis e você tem que usar alguma coisa como `sh installer.run` para fazê-los funcionar. Você terá que fazer uma boa pesquisa (ler os READMEs, instruções de INSTALL, páginas man, talvez ebuilds do Gentoo ou outros instaladores de pacote, possivelmente até os MAKEFILEs ou o código-fonte) para fazê-lo funcionar. Em alguns casos realmente sérios, você tem que editar os arquivos fontes para fazê-los funcionar. Porém, `makepkg` precisa ser completamente autônomo, com nenhuma entrada de usuário. Portanto, se você precisa editar os makefiles, você pode ter juntar um patch personalizado ao `PKGBUILD` e instalá-lo de dentro da função `prepare()`, ou você pode ter que usar alguns comandos `sed` de dentro da função `prepare()`.

## Diretrizes mais detalhadas

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

## Veja também

*   [Como criar corretamente um arquivo de patch](https://bbs.archlinux.org/viewtopic.php?id=91408).
*   [Arch Linux Classroom IRC Logs com aulas sobre criação de PKGBUILDs](https://archwomen.org/media/project_classroom/classlogs/).
*   [Abordagem com Fakeroot para instalação de pacote](http://www.linuxfromscratch.org/hints/downloads/files/fakeroot.txt)