**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Este documento cobre a criação de [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para módulos perl distribuídos pelo CPAN, a Comprehensive Perl Authors Network. Este documento tem como público-alvo aqueles que deseja empacotar módulos perl.

## Contents

*   [1 Convenções de empacotamento do Arch Linux](#Conven.C3.A7.C3.B5es_de_empacotamento_do_Arch_Linux)
    *   [1.1 Nomes de pacotes](#Nomes_de_pacotes)
    *   [1.2 Colocação de arquivos no pacote](#Coloca.C3.A7.C3.A3o_de_arquivos_no_pacote)
    *   [1.3 Arquitetura](#Arquitetura)
    *   [1.4 Automação](#Automa.C3.A7.C3.A3o)
*   [2 Exemplos de PKGBUILD](#Exemplos_de_PKGBUILD)
*   [3 Mecanismos de módulo CPAN](#Mecanismos_de_m.C3.B3dulo_CPAN)
    *   [3.1 Módulos](#M.C3.B3dulos)
    *   [3.2 Distribuições](#Distribui.C3.A7.C3.B5es)
    *   [3.3 CPAN](#CPAN)
    *   [3.4 Dependências de módulos](#Depend.C3.AAncias_de_m.C3.B3dulos)
    *   [3.5 Definição de dependências](#Defini.C3.A7.C3.A3o_de_depend.C3.AAncias)
    *   [3.6 Informações meta](#Informa.C3.A7.C3.B5es_meta)
*   [4 Módulos instaláveis](#M.C3.B3dulos_instal.C3.A1veis)
    *   [4.1 ExtUtils::MakeMaker](#ExtUtils::MakeMaker)
    *   [4.2 Module::Build](#Module::Build)
    *   [4.3 Module::Build::Tiny](#Module::Build::Tiny)
    *   [4.4 Module::Install](#Module::Install)
    *   [4.5 Variáveis de ambiente](#Vari.C3.A1veis_de_ambiente)
        *   [4.5.1 PERL_MM_USE_DEFAULT](#PERL_MM_USE_DEFAULT)
        *   [4.5.2 PERL_AUTOINSTALL](#PERL_AUTOINSTALL)
        *   [4.5.3 PERL_MM_OPT](#PERL_MM_OPT)
        *   [4.5.4 PERL_MB_OPT](#PERL_MB_OPT)
        *   [4.5.5 MODULEBUILDRC](#MODULEBUILDRC)
        *   [4.5.6 PERL5LIB](#PERL5LIB)
        *   [4.5.7 PERL_LOCAL_LIB_ROOT](#PERL_LOCAL_LIB_ROOT)
*   [5 Problemas com perl instalado pelo usuário](#Problemas_com_perl_instalado_pelo_usu.C3.A1rio)

## Convenções de empacotamento do Arch Linux

As seguintes convenções devem ser usadas para manter os pacotes de módulos perl consistentes. Esta seção serve como uma introdução ao conceito de empacotamento de perl, do ponto de vista do Arch Linux; isto é, gerenciamento de pacotes e administração do sistema. Em um esforço para agradar o leitor [TL;DR](https://en.wikipedia.org/wiki/TL;DR "w:TL;DR"), o material mais fácil e/ou mais popular está no topo.

### Nomes de pacotes

Para módulos, o nome do pacote deve começar com `perl-` e o resto do nome deve ser construído a partir do nome do módulo, convertendo-o em letras minúsculas e, em seguida, substituindo os dois pontos por hífenes. Por exemplo, o nome do pacote correspondente a `HTML::Parser` será `perl-html-parser`. Os aplicativos Perl devem ter o mesmo nome do aplicativo, mas em letras minúsculas.

### Colocação de arquivos no pacote

Os pacotes Perl devem instalar os arquivos do módulo em `/usr/lib/perl5/$version/vendor_perl/` (use `perl -V:vendorarch` em scripts), ou `/usr/share/perl5/vendor_perl/`. Isso é feito configurando o parâmetro de linha de comando `INSTALLDIRS` para `vendor` como mostrado abaixo. Nenhum arquivo deve ser armazenado em `/usr/lib/perl5/$version/site_perl/`, pois esse diretório é reservado para uso pelo administrador do sistema para instalar pacotes Perl fora do sistema de gerenciamento de pacotes. Quando um usuário instala módulos em todo o sistema usando o shell *cpan*, os módulos acabam nos subdiretórios site-perl.

Os arquivos `perllocal.pod` e `.packlist` também não devem estar presentes; isso é cuidado pelo exemplo de PKGBUILD descrito abaixo.

### Arquitetura

Na maioria dos casos, o vetor `arch` deve conter `'any'` porque a maioria dos pacotes Perl são independentes de arquitetura. Os módulos XS são compilados em bibliotecas carregadas dinamicamente (arquivos .so) e devem explicitamente configurar sua arquitetura para `('x86_64')` para indicar que eles são dependentes da arquitetura quando construídos. Um módulo XS geralmente contém um ou mais arquivos .xs que geram dinamicamente arquivos .c.

### Automação

Um plugin para o shell CPAN de segunda geração, CPANPLUS, está disponível no pacote perl-cpanplus-dist-arch do repo da comunidade. Este plugin empacota distribuições rapidamente quando elas são instaladas pelo CPANPLUS. A documentação on-line está disponível em [https://metacpan.org/release/CPANPLUS-Dist-Arch](https://metacpan.org/release/CPANPLUS-Dist-Arch)

## Exemplos de PKGBUILD

Um exemplo de PKGBUILD pode ser encontrado em [[1]](https://git.archlinux.org/abs.git/tree/prototypes/PKGBUILD-perl.proto).

Os dois exemplos a seguir do PKGBUILD usam técnicas, introduzidas nesta página, destinadas a tornar um PKGBUILD mais resiliente a problemas mais sofisticados. Como existem dois estilos de scripts de construção, há dois exemplos de PKGBUILDS. O primeiro PKGBUILD é um exemplo de como empacotar uma distribuição que usa `Makefile.PL`. O segundo PKGBUILD pode ser usado como ponto de partida para uma distribuição que usa `Build.PL`.

 `PKGBUILD` 
```
# Contributor: Your Name <youremail@domain.com>
pkgname=perl-foo-bar
pkgver=1.0
pkgrel=1
pkgdesc='This packages the Foo-Bar distribution, containing the Foo::Bar module!'
_dist=Foo-Bar
arch=('any')
url="https://metacpan.org/release/$_dist"
license=('GPL' 'PerlArtistic')
depends=(perl)
options=('!emptydirs' purge)
source=("http://search.cpan.org/CPAN/authors/id/BAZ/$_dist-$pkgver.tar.gz")
md5sums=(...)

build() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_LOCAL_LIB_ROOT
  export PERL_MM_USE_DEFAULT=1 PERL_AUTOINSTALL=--skipdeps
  /usr/bin/perl Makefile.PL
  make
}

check() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_LOCAL_LIB_ROOT
  export PERL_MM_USE_DEFAULT=1
  make test
}

package() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_LOCAL_LIB_ROOT
  make install INSTALLDIRS=vendor DESTDIR="$pkgdir"
}

```
 `PKGBUILD` 
```
# Contributor: Your Name <youremail@domain.com>
pkgname=perl-foo-bar
pkgver=1.0
pkgrel=1
pkgdesc='This packages the Foo-Bar distribution, containing the Foo::Bar module!'
_dist=Foo-Bar
arch=('any')
url="https://metacpan.org/release/$_dist"
license=('GPL' 'PerlArtistic')
depends=(perl)
options=('!emptydirs' purge)
source=("http://search.cpan.org/CPAN/authors/id/BAZ/$_dist-$pkgver.tar.gz")
md5sums=(...)

build() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_MB_OPT PERL_LOCAL_LIB_ROOT
  export PERL_MM_USE_DEFAULT=1 MODULEBUILDRC=/dev/null
  /usr/bin/perl Build.PL
  ./Build
}

check() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_MB_OPT PERL_LOCAL_LIB_ROOT
  export PERL_MM_USE_DEFAULT=1
  ./Build test
}

package() {
  cd "$srcdir/$_dist-$pkgver"
  unset PERL5LIB PERL_MM_OPT PERL_MB_OPT PERL_LOCAL_LIB_ROOT
  ./Build install --installdirs=vendor --destdir="$pkgdir"
}

```

A justificativa para a complexidade adicional desses PKGBUILDs é apresentada nas seções abaixo.

## Mecanismos de módulo CPAN

Há uma série de mecanismos cuidadosamente projetados, e não tão cuidadosamente, que trabalham juntos para criar o sistema de módulos. Ao fazer uso do CPAN, os procedimentos devem ser seguidos para buscar o código-fonte de um módulo, criar esse módulo buscado e inseri-lo no software do sistema para execução posterior. Para entender como os módulos devem ser empacotados, isso ajuda imensamente se entendermos como os módulos funcionam sem qualquer envolvimento dos pacotes pacman e Arch Linux. Nosso objetivo, no final, é tentar ser o mais discreto possível, melhorando a organização e a consistência do produto final.

### Módulos

Os módulos são declarados com a palavra-chave `package` no perl. Os módulos estão contidos em um arquivo `.pm` (pronuncia-se como "dót-pi-em"). Embora seja possível, mais de um módulo (`package`) está no arquivo. Os módulos têm namespaces separados por `::` (dois pontos duplos), como: `Archlinux::Module`. Ao carregar um módulo, os `::`s são substituídos por separadores de diretórios. Por exemplo: `Archlinux/Module.pm` será carregado para o módulo `Archlinux::Module`.

O módulos principais estão incluídos com uma instalação do perl. Alguns módulos principais estão *apenas* disponíveis empacotados com o perl. Outros módulos ainda podem ser baixados e instalados separadamente do CPAN.

### Distribuições

*Distributions* também são conhecidas como *dist* ou*package* no CPAN-lingo, sendo um equivalente a um pacote do Arch Linux neste site. Distribuições são arquivos `.tar.gz` cheios de arquivos. Esses arquivos contêm principalmente arquivos de módulo .pm, testes para os módulos incluídos, documentação para os módulos e o que for necessário.

Normalmente, uma distribuição contém um módulo primário com o mesmo nome. Às vezes isso não é verdade, como na distribuição do Template-Toolkit. O pacote mais recente, `Template-Toolkit-2.22.tar.gz`, para o `Template-Toolkit` dist, não contém o módulo `Template::Toolkit`!

Às vezes, porque as distribuições são nomeadas conforme um módulo principal, seus nomes são usados de forma intercambiável e ficam confusos. No entanto, às vezes é útil considerá-los uma entidade separada (como no caso do Template-Toolkit).

### CPAN

Cada espelho CPAN contém índices que listam as distribuições no CPAN, os módulos nos dists e o nome do autor que carregou o dist. Estes são simplesmente arquivos de texto. O índice mais útil está no arquivo `/modules.dlocaches.details.txt.gz` disponível em cada espelho do CPAN. O termo "pacotes" aqui se refere à palavra-chave `package` na própria linguagem perl, não algo similar aos pacotes pacman. O shell CPAN, chamado de letras minúsculas, em itálico *cpan*, é simplesmente o venerável script perl que navega nos índices para encontrar o módulo que você deseja instalar.

Os módulos são encontrados na lista `02packages.details.txt.gz`. Na mesma linha que o nome do módulo/pacote está o caminho para o tarball de distribuição que contém o módulo. Quando você pede ao *cpan* para instalar um módulo, ele irá procurar o módulo e instalar a distribuição relevante. Como a distribuição está instalando, irá gerar uma lista de dependências do módulo. *Cpan* tentará carregar cada dependência de módulo no intérprete perl. Se um módulo da versão fornecida não puder ser carregado, o processo será repetido.

O shell *cpan* não precisa se preocupar com qual versão do módulo necessário está sendo instalado. O *cpan* pode confiar no fato de que a última versão do módulo deve satisfazer os requisitos do módulo original que começou a instalar em primeiro lugar. Somente as versões mais recentes dos módulos são listadas no arquivo de detalhes dos pacotes. Infelizmente, para o autor do pacote perl, nem sempre podemos confiar no fato de que nossos pacotes oferecem a versão mais recente de uma distribuição perl e os módulos contidos nela. A verificação de dependência do Pacman é muito mais estática e fortemente aplicada.

### Dependências de módulos

Perl tem uma maneira única de definir dependências em comparação com sistemas similares, como *eggs* de python e *gems* de ruby. *Eggs* definem dependências de outros eggs. *Gems* dependem de *gems*. Dists de perl dependem de módulos. Os módulos só estão disponíveis nas distribuições CPAN, de modo que as distribuições perl dependem apenas indiretamente das distribuições. Os módulos podem definir suas próprias versões independentes das distribuições dentro do código-fonte do módulo. Isso é feito definindo uma variável *package* chamada `$VERSION`. Ao usar *strict* e *warnings*, isso é definido com a nossa palavra-chave. Por exemplo:

```
package Foo::Module;
use warnings;
use strict;
our $VERSION = '1.00';
```

Os módulos podem alterar suas versões da maneira que quiserem e até mesmo ter uma versão diferente da versão de distribuição. A utilidade disso é questionável, mas é importante ter em mente. Versões de módulo são mais difíceis de determinar fora do interpretador perl e requerem análise do próprio código perl e talvez até mesmo carregar o módulo em perl. A vantagem é que, dentro do módulo perl, as versões do módulo são fáceis de determinar. Por exemplo:

```
use Foo::Module;
print $Foo::Module::VERSION, "
";

```

### Definição de dependências

Onde estão as dependências definidas nas distribuições perl? Elas são "definidas" dentro do script `Makefile.PL` ou `Build.PL`. Por exemplo, dentro do script `Makefile.PL`, a função `WriteMakeFile` é chamada para gerar o `Makefile` assim:

```
use ExtUtils::MakeMaker;
WriteMakeFile(
    'NAME' => 'ArchLinux::Module',
    'VERSION' => '0.01',
    'PREREQ_PM' => { 'POSIX' => '0.01' },
);

```

Este é um exemplo artificial, mas é importante entender que as dependências não são finais até que o script `Makefile.PL` ou `Build.PL` seja executado. Dependências são especificadas em tempo de execução, o que significa que elas podem ser alteradas ou modificadas usando todo o poder do perl. Isso significa que o autor do módulo pode adicionar, remover ou alterar versões de dependências antes da instalação da distribuição. Alguns autores de módulos usam isso para fazer coisas excessivamente inteligentes, como depender de módulos apenas se eles estiverem instalados. Algumas dists multiplataformas também dependem de módulos específicos do sistema quando instalados em sistemas operacionais diferentes.

Como exemplo, a distribuição CPANPLUS procura por plugins CPANPLUS::Dist que estão atualmente instalados. Se algum plug-in estiver instalado para a versão atualmente instalada do CPANPLUS, ele será incluído nos pré-requisitos do novo CPANPLUS. Não sei bem por quê. Felizmente para o perl empacotador, a maioria das dependências é estática, como no exemplo acima, que requer o módulo POSIX com uma versão mínima de 0.01.

### Informações meta

Os arquivos meta são incluídos em distribuições recentes que contêm meta-informações sobre distribuições, como nome, autor, descrição abstrata e requisitos do módulo. Anteriormente, havia arquivos `META.yml` no formato YAML, mas, mais recentemente, a mudança foi feita para arquivos `META.json` no formato JSON. Esses arquivos podem ser editados manualmente, mas com mais frequência eles são gerados automaticamente pelos scripts `Makefile.PL` ou `Build.PL` ao empacotar uma distribuição para lançamento. A última especificação é descrita nas [documentações online do CPAN::Meta::Spec](http://search.cpan.org/perldoc?CPAN::Meta::Spec).

Lembre-se que as dependências podem ser alteradas em tempo de execução! Por esse motivo, outro meta arquivo é gerado após a execução do script de compilação. Este segundo meta arquivo é chamado `MYMETA.json` e reflete as alterações feitas no script em tempo de execução e pode ser diferente do arquivo meta gerado quando a distribuição foi empacotada para o CPAN.

Distribuições idosas no CPAN não possuem nenhum arquivo meta. Esses lançamentos antigos são anteriores à ideia do arquivo META.yml e descrevem apenas seus pré-requisitos em seu `Makefile.PL`.

## Módulos instaláveis

Um dos maiores pontos fortes do perl é o grande número de módulos disponíveis no CPAN. Não muito surpreendentemente, existem também vários módulos diferentes usados para instalar... bem... módulos! Há mais de uma maneira de fazer isso! Eu não estou ciente de um nome padrão para esses tipos de módulos, então eu os chamei de "Módulos de Instalação".

Estes módulos estão preocupados com a compilação da distribuição e instalação dos arquivos do módulo, sempre que o usuário preferir. Isso parece simples, mas considerando o número de diferentes sistemas em que perl é executado, isso pode se tornar complexo. Todos os módulos de instalação colocam um arquivo de código perl dentro do tarball dist. A execução deste script perl iniciará o processo de compilação e instalação. O script sempre termina com o sufixo `.PL` e é denominado "Script de compilação" na lista abaixo.

### ExtUtils::MakeMaker

	Script de compilação

	`Makefile.PL`

	Link no CPAN

	[http://search.cpan.org/dist/ExtUtils-MakeMaker](http://search.cpan.org/dist/ExtUtils-MakeMaker)

O módulo mais antigo e original para a instalação de módulos é o `ExtUtils::MakeMaker`. A principal desvantagem deste módulo é que ele requer que o programa `make` compile e instale tudo. Isso pode não parecer um grande problema para os usuários do Linux, mas é um verdadeiro aborrecimento para as pessoas do Windows!

### Module::Build

	Script de instalação

	`Build.PL`

	Link no CPAN

	[http://search.cpan.org/dist/Module-Build](http://search.cpan.org/dist/Module-Build)

A principal vantagem do Module::Build é que ele é puro perl. Isto significa que não requer que um programa `make` seja instalado para você compilar/instalar módulos. Sua adoção foi complicada porque se o `Module::Build` ainda não estivesse instalado, você não poderia executar o script `Build.PL` incluído! Este não é um problema com versões recentes do perl porque `Module::Build` é um módulo central. (**NOTE** A partir do perl 5.22, o Module::Build não será mais um módulo central)

### Module::Build::Tiny

	Script de compilação

	`Build.PL`

	Link no CPAN

	[http://search.cpan.org/dist/Module-Build-Tiny](http://search.cpan.org/dist/Module-Build-Tiny)

Esta é outra ferramenta de compilação de puro perl. Como interface, implementa um subconjunto da interface do Module::Build, em particular, requer traços antes de seus argumentos (Module::Build aceita com e sem) e não suporta `.modulebuildrc`.

### Module::Install

	Script de compilação

	`Makefile.PL`

	Link no CPAN

	[http://search.cpan.org/dist/Module-Install](http://search.cpan.org/dist/Module-Install)

Outro módulo moderno de compilação/instalação, `Module::Install` ainda requer que o programa `make` seja instalado para funcionar. `MI` foi criado para substituir `MakeMaker`, para resolver algumas das deficiências do `MakeMaker`. Ironicamente, isso depende do `MakeMaker` para operar. Os arquivos `Makefile.PL` que são gerados pelo `MI` são muito diferentes e são implementados usando uma linguagem simples específico do domínio.

Uma característica muito interessante é que o `Module::Install` empacota uma *cópia completa* de si mesmo no arquivo de distribuição. Por causa disso, ao contrário de `MakeMaker` ou `M::B`, você não precisa que `Module::Install` esteja instalado em seu sistema.

Outra característica muito original é a instalação automática. *Embora não seja recomendado pelos autores de `Module::Install`, esse recurso é usado com bastante frequência*. Quando o autor do módulo habilita a auto-instalação para sua distribuição, `Module::Install` irá procurar e instalar quaisquer módulos de pré-requisito que não estejam instalados quando o `Makefile.PL` for executado. Este recurso é ignorado quando `Module::Install` detecta que está sendo executado por `CPAN` ou `CPANPLUS`. No entanto, esse recurso não é ignorado quando executado dentro... oh, eu não sei ... um **PKGBUILD**! Espero que você possa ver como um programa permissivo do perl baixando e instalando módulos a qualquer momento, dentro de um PKGBUILD, possa ser um problema. Veja a variável de ambiente [#PERL_AUTOINSTALL](#PERL_AUTOINSTALL) para ver como corrigir isso.

### Variáveis de ambiente

Diversas variáveis de ambiente podem afetar o modo como os módulos são construídos ou instalados. Alguns têm um efeito muito dramático e podem causar problemas se forem mal compreendidos. Um usuário avançado pode estar usando essas variáveis de ambiente. Algumas delas quebrarão um PKGBUILD desavisado ou causarão um comportamento inesperado.

#### PERL_MM_USE_DEFAULT

Quando esta variável é definida para um valor verdadeiro, o módulo de instalação fingirá que a resposta padrão foi dada para qualquer pergunta que normalmente faria. Isso não "sempre" funciona, mas todos os módulos de instalação o honram. *Isso não significa que o autor do módulo irá!*

#### PERL_AUTOINSTALL

Você pode passar argumentos adicionais de linha de comando para o `Makefile.PL` do `Module::Install` com essa variável. Para desativar a instalação automática (*altamente recomendado*), atribua `--skipdeps` a este.

 `export PERL_AUTOINSTALL='--skipdeps'` 

#### PERL_MM_OPT

Você pode passar argumentos adicionais de linha de comando a `Makefile.PL` e/ou `Build.PL` com essa variável. Por exemplo, você pode instalar módulos em seu diretório pessoal usando:

 `export PERL_MM_OPT=INSTALLBASE=~/perl5` 

#### PERL_MB_OPT

Essa é a mesma coisa que `PERL_MM_OPT`, exceto por ser apenas para `Module::Build`. Por exemplo, você poderia instalar módulos em seu diretório pessoal usando:

 `export PERL_MB_OPT=--install_base=~/perl5` 

#### MODULEBUILDRC

`Module::Build` permite que você sobrescreva seus argumentos de linha de comando com um arquivo rc. O padrão deste é `~/.modulebuildrc`. É considerado obsoleto no conjunto de ferramentas perl. Você pode sobrescrever qual arquivo usa definindo o caminho para o arquivo rc em `MODULEBUILDRC`. Os paranoicos podem definir `MODULEBUILDRC` para `/dev/null` ... apenas por precaução.

#### PERL5LIB

Os diretórios pesquisados por bibliotecas podem ser configurados pelo usuário (especialmente se eles estiverem usando `Local::Lib`) definindo `PERL5LIB`. Isso deve ser apagado antes de compilar.

#### PERL_LOCAL_LIB_ROOT

Se o usuário estiver usando `Local::Lib`, então `PERL_LOCAL_LIB_ROOT` será definido. Isso deve ser apagado antes de compilar.

## Problemas com perl instalado pelo usuário

Um problema sutil é que os programadores avançados de perl podem gostar de ter múltiplas versões de perl instaladas. Isso é útil para testar a compatibilidade com versões anteriores em programas criados. Também há benefícios de velocidade para compilar seu próprio interpretador perl personalizado (p. ex., sem threads). Outra razão para um *perl* personalizado é simplesmente porque o pacote perl do Arch Linux às vezes fica atrás de versões perl. O usuário pode estar experimentando o perl mais recente ... quem sabe?

Se o usuário tiver um executável personalizado do perl em seu `$PATH`, o perl personalizado será executado quando o usuário digita o comando *perl* na shell. Na verdade, o perl personalizado será executado dentro do `PKGBUILD` também! Isso pode levar a problemas traiçoeiros que são difíceis de entender.

O problema reside nos módulos XS compilados. Esses módulos ligam perl e C. Como tal, eles devem usar a API C internal do perl para realizar essa ponte. A API C do perl muda um pouco entre diferentes versões do perl. Se o usuário tiver uma versão diferente do perl do que o perl do sistema (`/usr/bin/perl`), então qualquer módulo XS compilado com o perl do usuário será incompatível com o perl do sistema. Ao tentar usar o módulo XS compilado com o perl do sistema, o módulo vai falhar em carregar com um erro de vinculação.

Uma solução simples é sempre usar o caminho absoluto do interpretador perl do sistema (`/usr/bin/perl`) ao executar perl no `PKGBUILD`.