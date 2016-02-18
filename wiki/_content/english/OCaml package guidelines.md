**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – **OCaml** – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Writing [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for software written in [OCaml](https://en.wikipedia.org/wiki/OCaml "wikipedia:OCaml").

## Contents

*   [1 Package naming](#Package_naming)
*   [2 File placement](#File_placement)
    *   [2.1 Libraries](#Libraries)
    *   [2.2 OASIS](#OASIS)
*   [3 OCaml bytecode and levels](#OCaml_bytecode_and_levels)
*   [4 Example PKGBUILD](#Example_PKGBUILD)

## Package naming

For libraries, use `ocaml-*modulename*`. For applications, use the program name. In either case, the name should be entirely lowercase.

## File placement

### Libraries

OCaml libraries should be installed under `/usr/lib/ocaml`. Installation in `/usr/lib/ocaml/site-lib` is deprecated.

OCaml libraries should be installed using [ocaml-findlib](https://www.archlinux.org/packages/?name=ocaml-findlib). `ocaml-findlib` includes library metadata in the package that makes it easy to manage libraries. It is a de-facto standard and a lot of OCaml software now requires it.

`ocaml-findlib` extracts necessary data from a file named `META` that should be included in the source archive. If this file is not included, one should either be obtained from the corresponding Debian, Ubuntu, or Fedora package, or created for the package by the maintainer. A request to include the file should also be made to the upstream developers of the package.

The `OCAMLFIND_DESTDIR` variable should be used when installing packages with `ocaml-findlib`. See the example PKGBUILD below for details.

### OASIS

OCaml packages that install executables using OASIS ignore `DESTDIR`. This is a known limitation of OASIS ([issue #852](https://forge.ocamlcore.org/tracker/?func=detail&atid=294&aid=852&group_id=54)). One way to enable `DESTDIR`-like functionality is to run the `configure` script with the `--destdir` argument, like so:

```
build() {
    cd "${srcdir}/${srcname}-${pkgver}"
    ./configure --prefix /usr --destdir "$pkgdir"

    # build commands
}
```

## OCaml bytecode and levels

OCaml can run code on multiple "levels", the top level interprets OCaml Code without compiling, the bytecode level creates machine independent bytecode and the native level creates machine code binaries (just like C/C++).

When building OCaml Packages you need to be aware if the build process is compiling native machine code, bytecode, or as in many cases both. This creates a number of situations which can cause problems with package options and the right dependencies.

If bytecode is produced at all then the PKGBUILD must contain the following to protect the bytecode:

```
options=('!strip')

```

If the package does not contain bytecode and only distributes a binary, then `ocaml` is not needed as a dependency, but it of course is required as a makedepends since the `ocaml` package provides the OCaml compiler. If the package contains both native code and bytecode then `ocaml` should be a dependency and a makedepends.

OCaml code is rarely (if ever) distributed as bytecode only and will almost always include native code: the only case where using *any* as the *arch* is advisable is when only un-compiled source code is distributed, usually with a library, though many libraries still distribute native code.

The moral of the story here is to be aware of what it is you are distributing, chances are your package contains both native machine code and bytecode.

## Example PKGBUILD

```
# Contributor: Your Name <youremail@domain.com>

pkgname=ocaml-<package name>
pkgver=4.2
pkgrel=1
license=(*)*
arch=('i686' 'x86_64')
pkgdesc="An OCaml Package"
url=""
depends=('ocaml')
makedepends=('ocaml-findlib')
source=()
options=('!strip')
md5sums=()

OCAMLFIND_DESTDIR="${pkgdir}$(ocamlfind printconf destdir)"

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  mkdir -p "$OCAMLFIND_DESTDIR"
  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  env DESTDIR="${pkgdir}" \
    OCAMLFIND_DESTDIR="$OCAMLFIND_DESTDIR" \
    make install
}
```

Keep in mind that many OCaml Packages will often need extra parameters passed to make and make install. Also remember to remove the *'!strip'* option and change the architecture if the package does not produce bytecode.