**Status de tradução:** Esse artigo é uma tradução de [R package guidelines](/index.php/R_package_guidelines "R package guidelines"). Data da última tradução: 2018-11-04\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=R_package_guidelines&diff=0&oldid=553077) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Este documento abrange padrões e diretrizes para escrever [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para pacotes [R](/index.php/R "R"). A maioria das informações pode ser obtida consultando o arquivo `DESCRIPTION` do pacote. Você pode obter a maior parte de dentro do R executando `tools::CRAN_package_db()`.

## Contents

*   [1 Nomenclatura de pacote](#Nomenclatura_de_pacote)
*   [2 Versão de pacote](#Vers.C3.A3o_de_pacote)
*   [3 Arch](#Arch)
*   [4 Dependências](#Depend.C3.AAncias)
*   [5 Fonte](#Fonte)
*   [6 Compilação e empacotamento](#Compila.C3.A7.C3.A3o_e_empacotamento)
*   [7 Exemplos](#Exemplos)
    *   [7.1 RcppEigen](#RcppEigen)
    *   [7.2 XML](#XML)

## Nomenclatura de pacote

Pacotes devem ser nomeados `r-pkgname`, sendo *pkgname* retirado do campo `Package` do arquivo `DESCRIPTION`. O nome do pacote deve estar em letras minúsculas.

## Versão de pacote

Pegue no campo `Version`. R permite que os pacotes tenham dois pontos e hífenes em sua versão, isso não é permitido em PKGBUILDs. Converta estes para um período ou sublinhado.

## Arch

Veja [PKGBUILD (Português)#arch](/index.php/PKGBUILD_(Portugu%C3%AAs)#arch "PKGBUILD (Português)"). Se a página web do CRAN do pacote tiver `NeedsCompilation: yes`, é provável que seja específico da arquitetura. Caso contrário, é provável que não.

## Dependências

Os pacotes R listados nos campos `Depends`, `Imports` ou `LinkingTo` no arquivo `DESCRIPTION` de um pacote devem ser listados em [depends](/index.php/PKGBUILD_(Portugu%C3%AAs)#depends "PKGBUILD (Português)").

Os pacotes R listados em `Suggests` devem ser listados como [optdepends](/index.php/Optdepends_(Portugu%C3%AAs) "Optdepends (Português)").

Alguns pacotes requerem ferramentas externas, estas estão listadas em `SystemRequirements`.

O [gcc-fortran](https://www.archlinux.org/packages/?name=gcc-fortran) é necessário como [makedepends](/index.php/PKGBUILD_(Portugu%C3%AAs)#makedepends "PKGBUILD (Português)") para alguns pacotes, mas nem sempre é listado no arquivo `DESCRIPTION`.

## Fonte

Todos os pacotes R disponíveis no CRAN estão disponíveis no site `https://cran.r-project.org/src/contrib/*cranname*_*cranversion*.tar.gz`, sendo *cranname* o nome do pacote no CRAN e *cranversion* a versão cran.

## Compilação e empacotamento

R tem suporte embutido para compilar pacotes, nós só precisamos instalar e copiar o pacote compilado depois:

```
 build(){
     R CMD INSTALL pkg.tar.gz -l "$srcdir"
 }
 package() {
     install -dm0775 "$pkgdir"/usr/lib/R/library
     cp -a --no-preserve=ownership pkgname "$pkgdir"/usr/lib/R/library
 }

```

## Exemplos

### RcppEigen

```
 pkgname=r-rcppeigen
 pkgver=0.3.3.4.0
 pkgrel=1
 pkgdesc="Rcpp Integration for the Eigen Templated Linear Algebra Library"
 arch=('x86_64')
 url="[https://cran.r-project.org/package=RcppEigen](https://cran.r-project.org/package=RcppEigen)"
 license=('GPL')
 depends=('r' 'r-rcpp')
 optdepends=('r-inline' 'r-runit' 'r-pkgkitten')
 source=("[https://cran.r-project.org/src/contrib/RcppEigen_$pkgver.tar.gz](https://cran.r-project.org/src/contrib/RcppEigen_$pkgver.tar.gz)")
 md5sums=('78ee1ef7c6043efa875434ae5fcea2ec')

 build(){
     R CMD INSTALL RcppEigen_"$pkgver".tar.gz -l "$srcdir"
 }
 package() {
     install -dm0755 "$pkgdir"/usr/lib/R/library
     cp -a --no-preserve=ownership RcppEigen "$pkgdir"/usr/lib/R/library
 }

```

### XML

Um exemplo em que o pacote R possui caracteres não permitidos no pkgver:

```
 _cranver=3.98-1.11
 pkgname=r-xml
 pkgver=${_cranver//[:-]/.}
 pkgrel=1
 pkgdesc='Tools for Parsing and Generating XML Within R and S-Plus'
 arch=('x86_64')
 url='[https://cran.r-project.org/package=XML'](https://cran.r-project.org/package=XML')
 license=('BSD')
 depends=('r' 'libxml2')
 optdepends=('r-bitops' 'r-rcurl')
 replaces=('r-cran-xml')
 source=("[https://cran.r-project.org/src/contrib/XML_$_cranver.tar.gz](https://cran.r-project.org/src/contrib/XML_$_cranver.tar.gz)")
 md5sums=('6c67f5730ada3456372520773a920b8e')

 build(){
     R CMD INSTALL XML_"$_cranver".tar.gz -l "$srcdir"
 }
 package() {
     install -dm0755 "$pkgdir"/usr/lib/R/library
     cp -a --no-preserve=ownership XML "$pkgdir"/usr/lib/R/library
 }

```