**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – <a class="mw-selflink selflink">Go</a> – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This document covers standards and guidelines on writing [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for [Go](/index.php/Go "Go").

## Contents

*   [1 General guidelines](#General_guidelines)
    *   [1.1 Package naming](#Package_naming)
*   [2 Dependencies](#Dependencies)
    *   [2.1 Prepare](#Prepare)
*   [3 Building](#Building)
    *   [3.1 Flags and build options](#Flags_and_build_options)
    *   [3.2 Pre 1.11 building](#Pre_1.11_building)
    *   [3.3 Post 1.11 building](#Post_1.11_building)
*   [4 Sample PKGBUILDs](#Sample_PKGBUILDs)
    *   [4.1 Basic PKGBUILD](#Basic_PKGBUILD)
    *   [4.2 PKGBUILD with GOPATH and dep](#PKGBUILD_with_GOPATH_and_dep)
*   [5 Example Packages](#Example_Packages)

## General guidelines

### Package naming

For [Go](/index.php/Go "Go") library modules, use `go-*modulename*`. Also use the prefix if the package provides a program that is strongly coupled to the Go ecosystem. For other applications, use only the program name.

**Note:** The package name should be entirely lowercase.

## Dependencies

Go packages currently use the `vendor/` folder to handle dependencies in projects. These are usually managed by one of several dependency manager projects. If one is used for the package, this step should be performed in the [prepare()](/index.php/Creating_packages#prepare.28.29 "Creating packages") function of the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

	Dependency managers in the repositories

*   [dep](https://www.archlinux.org/packages/?name=dep)
*   [godep](https://www.archlinux.org/packages/?name=godep)
*   [glide](https://www.archlinux.org/packages/?name=glide)

### Prepare

We create a directory `$srcdir/gopath` for [$GOPATH](/index.php/Go#$GOPATH "Go") and copy over the source to this directory. It should be noted that this step might not be needed if the project provides a sane `Makefile` for the project and sets this up.

```
prepare(){
  mkdir -p "gopath/src/github.com/pkgbuild-example"
  ln -rTsf "${pkgname}-${pkgver}" "gopath/src/github.com/pkgbuild-example"

  # the dependencies can be fetched here if needed
  cd "gopath/src/github.com/pkgbuild-example/$pkgname"
  dep ensure
}

```

## Building

There are two go packages in the repositories that you can build towards; [go](https://www.archlinux.org/packages/?name=go) and [go-pie](https://www.archlinux.org/packages/?name=go-pie). All packages should preferably be built towards [go-pie](https://www.archlinux.org/packages/?name=go-pie) as this enables us to deliver secure binaries. However, as upstream might have bugs, building towards [go](https://www.archlinux.org/packages/?name=go) should be a last resort.

### Flags and build options

Most Makefiles written for go applications do not respect the `LDFLAGS` provided by build systems, this causes Go binaries to not be compiled with RELRO. This needs to be patched into the Makefile, or the Makefile should be omitted. If there is an Makefile involved, you have 3 options to support RELRO.

*   Patch Makefile
*   Skip Makefile completely and use `go build`
*   Export `GOFLAGS` - This is less desirable as we are dropping flags from `LDFLAGS`.

For [reproducible builds](https://reproducible-builds.org/) it's important that the binaries are stripped of the build path using the `-trimpath` flags.

```
# LDFLAGS into the GOFLAGS env variable.
export GOFLAGS="-gcflags=all=-trimpath=${PWD} -asmflags=all=-trimpath=${PWD} -ldflags=-extldflags=-zrelro -ldflags=-extldflags=-znow"

# LDFLAGS defined in go build.
go build \
    -gcflags "all=-trimpath=${PWD}" \
    -asmflags "all=-trimpath=${PWD}" \
    -ldflags "-extldflags ${LDFLAGS}" \
    .

```

**Note:** For the sake of brevity, these flags are omitted in the examples below.

### Pre 1.11 building

When building go packages with [$GOPATH](/index.php/Go#$GOPATH "Go") there are a few problems one can encounter. Usually the project delivers a `Makefile` that can be used and should be used. There are cases where you still need to setup a `$GOPATH` in the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). The following snippet sets up an appropriate `GOPATH` inside `$srcdir/gopath` one can use to build packages. A new directory is used as some go dependency managers does wierd things if it discovers the project in the root of the `$GOPATH`.

**Note:** These builds should have `$GOPATH` stripped from the binary.

```
prepare(){
  mkdir -p "gopath/src/github.com/pkgbuild-example"
  ln -rTsf "${pkgname}-${pkgver}" "gopath/src/github.com/pkgbuild-example/$pkgbuild"

  # the dependencies can be fetched here if needed
  cd "gopath/src/github.com/pkgbuild-example/$pkgname"
  dep ensure
}

build(){
  export GOPATH="$srcdir/gopath"
  cd "gopath/src/github.com/pkgbuild-example/$pkgname"
  go install -v .
}

```

Note that `install` and `build` and can do recursive builds if you have a `cmd/` subdirectory with multiple binaries: `go install -v github.com/pkgbuild-example/cmd/...`

### Post 1.11 building

Go 1.11 introduces [go modules](https://github.com/golang/go/wiki/Modules). This omits the need to setup `GOPATH` and we can build directly in the directory. Projects like these have a `go.mod` and `go.sum` file defined.

**Note:** These builds needs `$PWD` stripped from the binary.

```
build(){
  cd "$pkgname-$pkgver"
  go build .
}

```

## Sample PKGBUILDs

### Basic PKGBUILD

```
pkgname=foo
pkgver=0.0.1
pkgrel=1
pkgdesc="Go PKGBUILD Example"
arch=('x86_64' 'i686')
url="http://example.org/$pkgname/"
license=('GPL')
makedepends=('go-pie')
source=("http://example.org/$pkgname/$pkgname-$pkgver.tar.gz")
sha256sums=('00112233445566778899aabbccddeeff')

build() {
  cd "$pkgname-$pkgver"
  go build \
    -gcflags "all=-trimpath=${PWD}" \
    -asmflags "all=-trimpath=${PWD}" \
    -ldflags "-extldflags ${LDFLAGS}" \
    -o "$pkgname" .
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm755 "$pkgname" "$pkgdir/usr/bin/$pkgname"
}

```

### PKGBUILD with GOPATH and dep

```
pkgname=foo
pkgver=0.0.1
pkgrel=1
pkgdesc="Go PKGBUILD Example"
arch=('x86_64' 'i686')
url="http://example.org/$pkgname/"
license=('GPL')
makedepends=('go-pie' 'dep')
source=("http://example.org/$pkgname/$pkgname-$pkgver.tar.gz")
sha256sums=('00112233445566778899aabbccddeeff')

prepare(){
  mkdir -p gopath/src/example.org/foo
  ln -rTsf "${pkgname}-${pkgver}" gopath/src/example.org/foo

  cd "gopath/src/example.org/foo"
  dep ensure
}

build() {
  export GOPATH="$srcdir/gopath"
  cd "$GOPATH/src/example.org/foo
  go install \
    -gcflags "all=-trimpath=${GOPATH}" \
    -asmflags "all=-trimpath=${GOPATH}" \
    -ldflags "-extldflags ${LDFLAGS}" \
    -v ./...
}

check() {
  export GOPATH="$srcdir/gopath"
  cd "$GOPATH/src/example.org/foo
  go test ./...
}

package() {
  install -Dm755 "gopath/bin/$pkgname" "$pkgdir/usr/bin/$pkgname"
}

```

## Example Packages

*   [dep](https://www.archlinux.org/packages/?name=dep)
*   [gopass](https://www.archlinux.org/packages/?name=gopass)
*   [delve](https://www.archlinux.org/packages/?name=delve)
*   [gitea](https://www.archlinux.org/packages/?name=gitea)
*   [git-lfs](https://www.archlinux.org/packages/?name=git-lfs)