**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[32-bit](/index.php/32-bit_package_guidelines "32-bit package guidelines") – [CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – <a class="mw-selflink selflink">Haskell</a> – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document aims to cover standards and guidelines for producing good [Haskell](/index.php/Haskell "Haskell") [packages](/index.php/Creating_packages "Creating packages") on Arch.

Until this document is written, contact [User:Felixonmars](/index.php/User:Felixonmars "User:Felixonmars")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Package naming](#Package_naming)
*   [2 Architecture](#Architecture)
*   [3 Source](#Source)
*   [4 Rebuild order](#Rebuild_order)
*   [5 PKGBUILD library example](#PKGBUILD_library_example)

## Package naming

For Haskell libraries, use `haskell-*libraryname*` usually the same name as on [hackage](https://hackage.haskell.org/).

**Note:** The package name should be entirely lowercase.

## Architecture

See [PKGBUILD#arch](/index.php/PKGBUILD#arch "PKGBUILD").

Every Haskell library or program is architecture-dependent.

## Source

The preferred source of a Haskell program or library is from [hackage](https://hackage.haskell.org). [PKGBUILD#source](/index.php/PKGBUILD#source "PKGBUILD") `source=()` array should use the following URL template:

	`https://hackage.haskell.org/packages/archive/$_hkgname/$pkgver/$_hkgname-$pkgver.tar.gz`

Note that a custom _hkgname variable is used instead of pkgname since Haskell packages are generally prefixed with haskell-. This variable can generically be defined as follows:

```
_hkgname=stm-delay

```

## Rebuild order

When a Haskell library changes it's build flags or is updated all dependent packages need to be rebuild.

## PKGBUILD library example

Packaging a Haskell library is different from packaging a Haskell program, the libraries packaged in Arch Linux are meant to be used by packaged Haskell programs.

 `PKGBUILD` 
```
# Contributor: Your Name <youremail@domain.com>
_hkgname=stm-delay
pkgname=haskell-stm-delay
arch=('x86_64')
url="https://hackage.haskell.org/package/$hkgname"
depends=(ghc-libs)
makedepends=(ghc)
source=("https://hackage.haskell.org/packages/archive/$_hkgname/$pkgver/$_hkgname-$pkgver.tar.gz")

build() {
  cd $_hkgname-$pkgver    

  runhaskell Setup configure -O --enable-shared --enable-executable-dynamic --disable-library-vanilla \
    --prefix=/usr --docdir=/usr/share/doc/$pkgname --enable-tests \
    --dynlibdir=/usr/lib --libsubdir=\$compiler/site-local/\$pkgid \
    --ghc-option=-optl-Wl\,-z\,relro\,-z\,now \
    --ghc-option='-pie'

  runhaskell Setup build
  runhaskell Setup register --gen-script
  runhaskell Setup unregister --gen-script
  sed -i -r -e "s|ghc-pkg.*update[^ ]* |&'--force' |" register.sh
  sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}

check() {
  cd $_hkgname-$pkgver
  runhaskell Setup test
}

package() {
  cd $_hkgname-$pkgver

  install -D -m744 register.sh "$pkgdir"/usr/share/haskell/register/$pkgname.sh
  install -D -m744 unregister.sh "$pkgdir"/usr/share/haskell/unregister/$pkgname.sh
  runhaskell Setup copy --destdir="$pkgdir"
  install -D -m644 "LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  rm -f "${pkgdir}/usr/share/doc/${pkgname}/LICENSE"
}

```