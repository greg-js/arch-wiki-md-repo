**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

[Go](https://en.wikipedia.org/wiki/pt:Go_(linguagem_de_programa%C3%A7%C3%A3o) também encontra suporte no Arch Linux.

O pacote [go](https://www.archlinux.org/packages/?name=go) contém a ferramenta **go** (para executar `go fix`, `go build` etc). Também há [gcc-go](https://www.archlinux.org/packages/?name=gcc-go) que fornece `gccgo`.

## Contents

*   [1 Diretrizes gerais](#Diretrizes_gerais)
    *   [1.1 Nomenclatura](#Nomenclatura)
    *   [1.2 Empacotamento](#Empacotamento)
*   [2 Exemplos de PKGBUILDs](#Exemplos_de_PKGBUILDs)
    *   [2.1 Exemplo de PKGBUILD para um aplicativo escrito em Go](#Exemplo_de_PKGBUILD_para_um_aplicativo_escrito_em_Go)
        *   [2.1.1 Exemplos de pacotes](#Exemplos_de_pacotes)
    *   [2.2 Exemplo de PKGBUILD para quando apenas um único arquivo fonte está disponível](#Exemplo_de_PKGBUILD_para_quando_apenas_um_.C3.BAnico_arquivo_fonte_est.C3.A1_dispon.C3.ADvel)
        *   [2.2.1 Exemplos de pacotes](#Exemplos_de_pacotes_2)
    *   [2.3 Exemplos de PKGBUILDs para bibliotecas Go que também incluem executáveis](#Exemplos_de_PKGBUILDs_para_bibliotecas_Go_que_tamb.C3.A9m_incluem_execut.C3.A1veis)
        *   [2.3.1 Usando *go get*](#Usando_go_get)
        *   [2.3.2 Usando *go get*](#Usando_go_get_2)

## Diretrizes gerais

### Nomenclatura

*   For applications written in Go, use the name of the application as the package name, in lowercase.
    *   Be creative if the name is already taken.
*   For PKGBUILDS that uses the "go" tool to download the package, only add "-git" to the package name if it is not built from a tarball or a from a tagged release (but from trunk/HEAD).
    *   Similarly for mercurial packages, only add "-hg" to the package name if it is not a release-revision.
    *   Extend this pattern for other version control systems.
    *   The go tool has its own logic for which branch or tag it should use. See `go get --help`.
*   Consider adding the name of the author to the package name if there are several applications that are named the same, like [dcpu16-kballard](https://aur.archlinux.org/packages/dcpu16-kballard/).
    *   In general, the most popular packages should be allowed to use the shortest or "best" name.
*   Postfixes to the package names (like `-hg`, `-git` or `-svn`) are optional if there are no official releases from the project in question. On one hand, it is common to use them when the package downloads from a VCS. On the other hand, most Go projects do not have any release-tarballs, only the repo which is used for branching/tagging the official release, if it is not *trunk*. Also, `go get`, which is the "official" way to install Go modules, uses the repositories directly. Use your better judgement.

### Empacotamento

*   Go projects are either just library files, just executables or both. Choose the appropriate way of packaging them. There are several examples below.
*   Some Go applications or libraries have not been updated to the latest version of Go yet.
    *   Running `go build -fix` may often work, but it may have to be fixed by the developer. Report an issue upstream if this is the case.
*   Several Go projects do not have a version number or a license file.
    *   Use license=('unknown') and report an issue to the developer if a license file is missing.
    *   Use version "0.1", "1" or the git-revision (or equivalent for other version control systems) if the version number is missing.
    *   Alternatively, use the current date as the version number, in this form `YYYYMMDD`.

## Exemplos de PKGBUILDs

### Exemplo de PKGBUILD para um aplicativo escrito em Go

```
# Maintainer: NAME <EMAIL>

pkgname=PACKAGE NAME
pkgver=1.2.3
pkgrel=1
pkgdesc="PACKAGE DESCRIPTION"
arch=('x86_64' 'i686')
url="http://SERVER/$pkgname/"
license=('MIT')
makedepends=('go')
options=('!strip' '!emptydirs')
source=("http://SERVER/$pkgname/$pkgname-$pkgver.tar.gz")
sha256sums=('00112233445566778899aabbccddeeff')

build() {
  cd "$pkgname-$pkgver"

  go build
}

package() {
  cd "$pkgname-$pkgver"

  install -Dm755 "$pkgname-$pkgver" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
```

#### Exemplos de pacotes

*   [gendesk](https://www.archlinux.org/packages/?name=gendesk)
*   [dcpu16](https://aur.archlinux.org/packages/dcpu16/)

### Exemplo de PKGBUILD para quando apenas um único arquivo fonte está disponível

```
# Maintainer: NAME <EMAIL>

pkgname=PACKAGE NAME
pkgver=1.2.3
pkgrel=1
pkgdesc="PACKAGE DESCRIPTION"
arch=('x86_64' 'i686')
url="http://SERVER/$pkgname/"
license=('GPL3')
makedepends=('go')
options=('!strip' '!emptydirs')
source=("http://SERVER/$pkgname/$pkgname.go")
sha256sums=('00112233445566778899aabbccddeeff')

build() {
  go build -o "$pkgname"
}

package() {
  install -Dm755 "$pkgname" "$pkgdir/usr/bin/$pkgname"
}

# vim:set ts=2 sw=2 et:
```

#### Exemplos de pacotes

*   [gorun](https://aur.archlinux.org/packages/gorun/)

### Exemplos de PKGBUILDs para bibliotecas Go que também incluem executáveis

#### Usando *go get*

This is the recommended way, instead of the method below.

Here is a way that relies on go get.

You probably will not need to modify the build() or package() functions at all, only the variables at the top (pkgname etc).

If this does not work, test with go get first.

**Note:** Remove `/...` if the PKGBUILD fails!

```
# Maintainer: NAME <EMAIL>

pkgname=codesearch
pkgver=20120515
pkgrel=1
pkgdesc="Code indexing and search written in Go"
arch=('x86_64' 'i686')
url="https://github.com/google/codesearch"
license=('BSD')
depends=('go')
makedepends=('mercurial')
options=('!strip' '!emptydirs')
_gourl=github.com/google/codesearch

build() {
  GOPATH="$srcdir" go get -fix -v -x ${_gourl}/...
}

check() {
  GOPATH="$GOPATH:$srcdir" go test -v -x ${_gourl}/...
}

package() {
  mkdir -p "$pkgdir/usr/bin"
  install -p -m755 "$srcdir/bin/"* "$pkgdir/usr/bin"

  mkdir -p "$pkgdir/$GOPATH"
  cp -Rv --preserve=timestamps "$srcdir/"{src,pkg} "$pkgdir/$GOPATH"

  # Package license (if available)
  for f in LICENSE COPYING LICENSE.* COPYING.*; do
    if [ -e "$srcdir/src/$_gourl/$f" ]; then
      install -Dm644 "$srcdir/src/$_gourl/$f" \
        "$pkgdir/usr/share/licenses/$pkgname/$f"
    fi
  done
}

# vim:set ts=2 sw=2 et:
```

Thanks to Rémy Oudompheng‎ for this one.

#### Usando *go get*

Here is another way that relies on `go get`.

You probably will not need to modify the build() or package() functions at all, only the variables at the top (pkgname etc).

If this does not work, test with `go get` first.

```
# Maintainer: NAME <EMAIL>

pkgname=PACKAGE NAME
pkgver=1.2.3
pkgrel=1
pkgdesc="PACKAGE DESCRIPTION"
arch=('x86_64' 'i686')
url="http://SERVER/$pkgname/"
license=('MIT')
makedepends=('go' 'git')
options=('!strip' '!emptydirs')
_gourl=SERVER.NET/PATH/MODULENAME

build() {
  export GOROOT=/usr/lib/go

  rm -rf build
  mkdir -p build/go
  cd build/go

  for f in "$GOROOT/"*; do
    ln -s "$f"
  done

  rm pkg
  mkdir pkg
  cd pkg

  for f in "$GOROOT/pkg/"*; do
    ln -s "$f"
  done

  platform=`for f in "$GOROOT/pkg/"*; do echo \`basename $f\`; done|grep linux`

  rm -f "$platform"
  mkdir "$platform"
  cd "$platform"

  for f in "$GOROOT/pkg/$platform/"*.h; do
    ln -s "$f"
  done

  export GOROOT="$srcdir/build/go"
  export GOPATH="$srcdir/build"

  go get -fix "$_gourl"

  # Prepare executable
  if [ -d "$srcdir/build/src" ]; then
    cd "$srcdir/build/src/$_gourl"
    go build -o "$srcdir/build/$pkgname"
  else
    echo 'Old sources for a previous version of this package are already present!'
    echo 'Build in a chroot or uninstall the previous version.'
    return 1
  fi
}

package() {
  export GOROOT="$GOPATH"

  # Package go package files
  for f in "$srcdir/build/go/pkg/"* "$srcdir/build/pkg/"*; do
    # If it's a directory
    if [ -d "$f" ]; then
      cd "$f"
      mkdir -p "$pkgdir/$GOROOT/pkg/`basename $f`"
      for z in *; do
        # Check if the directory name matches
        if [ "$z" == `echo $_gourl | cut -d/ -f1` ]; then
          cp -r $z "$pkgdir/$GOROOT/pkg/`basename $f`"
        fi
      done
      cd ..
    fi
  done

  # Package source files
  if [ -d "$srcdir/build/src" ]; then
    mkdir -p "$pkgdir/$GOROOT/src/pkg"
    cp -r "$srcdir/build/src/"* "$pkgdir/$GOROOT/src/pkg/"
    find "$pkgdir" -depth -type d -name .git -exec rm -r {} \;
  fi

  # Package license (if available)
  for f in LICENSE COPYING; do
    if [ -e "$srcdir/build/src/$_gourl/$f" ]; then
      install -Dm644 "$srcdir/build/src/$_gourl/$f" \
        "$pkgdir/usr/share/licenses/$pkgname/$f"
    fi
  done

  # Package executables
  if [ -e "$srcdir/build/$pkgname" ]; then
    install -Dm755 "$srcdir/build/$pkgname" \
      "$pkgdir/usr/bin/$pkgname"
  fi
}

# vim:set ts=2 sw=2 et:
```