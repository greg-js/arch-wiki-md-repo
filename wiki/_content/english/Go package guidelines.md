**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – **Go** – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

[Go](https://en.wikipedia.org/wiki/Go_(programming_language) is well supported on Arch Linux.

The [go](https://www.archlinux.org/packages/?name=go) package contains the **go** tool (for running `go fix`, `go build` etc). There is also [gcc-go](https://www.archlinux.org/packages/?name=gcc-go) which provides `gccgo`.

[go-makepkg](https://github.com/seletskiy/go-makepkg) tool provides easy way of packaging Go programs without need of crafting PKGBUILD files manually.

## Contents

*   [1 General guidelines](#General_guidelines)
    *   [1.1 Naming](#Naming)
    *   [1.2 Packaging](#Packaging)
*   [2 Sample PKGBUILDs](#Sample_PKGBUILDs)
    *   [2.1 Sample PKGBUILD for an application written in Go](#Sample_PKGBUILD_for_an_application_written_in_Go)
        *   [2.1.1 Sample packages](#Sample_packages)
    *   [2.2 Sample PKGBUILD for when only a single source file is available](#Sample_PKGBUILD_for_when_only_a_single_source_file_is_available)
        *   [2.2.1 Sample packages](#Sample_packages_2)
    *   [2.3 Sample PKGBUILDs for Go libraries that also includes executables](#Sample_PKGBUILDs_for_Go_libraries_that_also_includes_executables)
        *   [2.3.1 Using *go get*](#Using_go_get)
        *   [2.3.2 Using *go get*](#Using_go_get_2)

## General guidelines

### Naming

*   For applications written in Go, use the name of the application as the package name, in lowercase.
    *   Be creative if the name is already taken.
*   For PKGBUILDS that uses the "go" tool to download the package, only add "-git" to the package name if it is not built from a tarball or a from a tagged release (but from trunk/HEAD).
    *   Similarly for mercurial packages, only add "-hg" to the package name if it is not a release-revision.
    *   Extend this pattern for other version control systems.
    *   The go tool has its own logic for which branch or tag it should use. See `go get --help`.
*   Consider adding the name of the author to the package name if there are several applications that are named the same, like [dcpu16-kballard](https://aur.archlinux.org/packages/dcpu16-kballard/).
    *   In general, the most popular packages should be allowed to use the shortest or "best" name.
*   Postfixes to the package names (like `-hg`, `-git` or `-svn`) are optional if there are no official releases from the project in question. On one hand, it is common to use them when the package downloads from a VCS. On the other hand, most Go projects do not have any release-tarballs, only the repo which is used for branching/tagging the official release, if it is not *trunk*. Also, `go get`, which is the "official" way to install Go modules, uses the repositories directly. Use your better judgement.

### Packaging

*   Go projects are either just library files, just executables or both. Choose the appropriate way of packaging them. There are several examples below.
*   Some Go applications or libraries have not been updated to the latest version of Go yet.
    *   Running `go build -fix` may often work, but it may have to be fixed by the developer. Report an issue upstream if this is the case.
*   Several Go projects do not have a version number or a license file.
    *   Use license=('unknown') and report an issue to the developer if a license file is missing.
    *   Use version "0.1", "1" or the git-revision (or equivalent for other version control systems) if the version number is missing.
    *   Alternatively, use the current date as the version number, in this form `YYYYMMDD`.

## Sample PKGBUILDs

### Sample PKGBUILD for an application written in Go

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

#### Sample packages

*   [gendesk](https://www.archlinux.org/packages/?name=gendesk)
*   [dcpu16](https://aur.archlinux.org/packages/dcpu16/)

### Sample PKGBUILD for when only a single source file is available

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

#### Sample packages

*   [gorun](https://aur.archlinux.org/packages/gorun/)

### Sample PKGBUILDs for Go libraries that also includes executables

#### Using *go get*

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

#### Using *go get*

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