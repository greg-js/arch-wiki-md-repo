**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[32-bit](/index.php/32-bit_package_guidelines "32-bit package guidelines") – [CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – <a class="mw-selflink selflink">R</a> – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document covers standards and guidelines on writing [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for [R](/index.php/R "R") packages. Most information can be obtained by looking at the package's `DESCRIPTION` file. You can get most of this from inside R by running `tools::CRAN_package_db()`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Package naming](#Package_naming)
*   [2 Package Version](#Package_Version)
*   [3 Arch](#Arch)
*   [4 Dependencies](#Dependencies)
*   [5 Source](#Source)
*   [6 Build and Package](#Build_and_Package)
    *   [6.1 CRAN](#CRAN)
    *   [6.2 Bioconductor](#Bioconductor)
*   [7 Tips and tricks](#Tips_and_tricks)

## Package naming

Packages should be named `r-pkgname`, where pkgname is taken from the `Package` field from the `DESCRIPTION` file. The package name should be lowercase.

## Package Version

Take it from the `Version` field. R allows packages to have colons and hyphens in their version, this is disallowed in PKGBUILDs. Convert these to a period or underscore.

## Arch

See [PKGBUILD#arch](/index.php/PKGBUILD#arch "PKGBUILD"). If the package's CRAN webpage has `NeedsCompilation: yes` it is likely architecture-specific. Otherwise, it is likely not.

## Dependencies

R packages listed in `Depends`, `Imports`, or the `LinkingTo` fields in a package's `DESCRIPTION` file should be listed under [depends](/index.php/PKGBUILD#depends "PKGBUILD").

R packages listed in `Suggests` should be listed as [optdepends](/index.php/Optdepends "Optdepends").

Some packages require external tools, these are listed under `SystemRequirements`.

[gcc](https://www.archlinux.org/packages/?name=gcc) is needed as a [makedepends](/index.php/Makedepends "Makedepends") if `DESCRIPTION` file tells that `NeedsCompilation: yes`. [gcc-fortran](https://www.archlinux.org/packages/?name=gcc-fortran) is also needed as [depends](/index.php/PKGBUILD#depends "PKGBUILD") for some packages but is not always listed in the `DESCRIPTION` file.

## Source

All R packages available on CRAN are available at the website `https://cran.r-project.org/src/contrib/*cranname*_*cranversion*.tar.gz` where *cranname* is the name of the package on CRAN and *cranversion* the cran version.

## Build and Package

R has built-in support for building packages. Here are two templates of `PKGBUILD`s for two repositories: CRAN and Bioconductor.

### CRAN

```
_cranname=
_cranver=
pkgname=r-${_cranname,,}
pkgver=${_cranver//[:-]/.}
pkgrel=1
pkgdesc=""
arch=()
url="[https://cran.r-project.org/package=${_cranname}](https://cran.r-project.org/package=${_cranname})"
license=()
depends=(r)
makedepends=()
optdepends=()
source=("[https://cran.r-project.org/src/contrib/${_cranname}_${_cranver}.tar.gz](https://cran.r-project.org/src/contrib/${_cranname}_${_cranver}.tar.gz)")
sha256sums=(*)*

build() {
  cd "${srcdir}"

  R CMD INSTALL ${_cranname}_${_cranver}.tar.gz -l ${srcdir}
}

package() {
  cd "${srcdir}"

  install -dm0755 "${pkgdir}/usr/lib/R/library"
  cp -a --no-preserve=ownership "${_cranname}" "${pkgdir}/usr/lib/R/library"
}

```

### Bioconductor

```
_bcname=
_bcver=
pkgname=r-${_bcname,,}
pkgver=${_bcver//[:-]/.}
pkgrel=1
pkgdesc=""
arch=()
url="[https://bioconductor.org/packages/release/bioc/html/${_bcname}.html](https://bioconductor.org/packages/release/bioc/html/${_bcname}.html)"
license=()
depends=(r)
makedepends=()
optdepends=()
source=("[https://bioconductor.org/packages/release/bioc/src/contrib/${_bcname}_${_bcver}.tar.gz](https://bioconductor.org/packages/release/bioc/src/contrib/${_bcname}_${_bcver}.tar.gz)")
sha256sums=(*)*

build() {
  cd "${srcdir}"

  R CMD INSTALL ${_bcname}_${_bcver}.tar.gz -l ${srcdir}
}

package() {
  cd "${srcdir}"

  install -dm0755 "${pkgdir}/usr/lib/R/library"
  cp -a --no-preserve=ownership "${_bcname}" "${pkgdir}/usr/lib/R/library"
}

```

## Tips and tricks

To quickly check if any of your (or another user) R packages in AUR has become outdated you can use [aurrpkgs-git](https://aur.archlinux.org/packages/aurrpkgs-git/) tool (replace *username* with desired value):

```
$ aurrpkgs *username*

```

This tool will show you all outdated packages and new available versions for them.