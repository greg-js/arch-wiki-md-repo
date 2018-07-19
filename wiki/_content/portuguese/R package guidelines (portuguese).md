**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

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

Packages should be named `r-pkgname`, where pkgname is taken from the `Package` field from the `DESCRIPTION` file. The package name should be lowercase.

## Versão de pacote

Take it from the `Version` field. R allows packages to have colons and hyphens in their version, this is disallowed in PKGBUILDs. Convert these to a period or underscore.

## Arch

See [PKGBUILD#arch](/index.php/PKGBUILD#arch "PKGBUILD"). If the package's CRAN webpage has `NeedsCompilation: yes` it is likely architecture-specific. Otherwise, it is likely not.

## Dependências

R packages listed in `Depends`, `Imports`, or the `LinkingTo` fields in a package's `DESCRIPTION` file should be listed under depends.

R packages listed in `Suggests` should be listed as optdepends.

Some packages require external tools, these are listed under `SystemRequirements`.

[gcc-fortran](https://www.archlinux.org/packages/?name=gcc-fortran) is needed as a makedepends for some packages but is not always listed in the `DESCRIPTION` file.

## Fonte

All R packages available on CRAN are available at the website `[https://cran.r-project.org/src/contrib/cranname_cranversion.tar.gz](https://cran.r-project.org/src/contrib/cranname_cranversion.tar.gz)` where cranname is the name of the package on CRAN and cranversion the cran version.

## Compilação e empacotamento

R has built-in support for building packages, we just need to install and copy over the built package afterwards:

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

An example where the R package has characters not allowed in pkgver:

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