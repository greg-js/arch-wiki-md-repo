**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – <a class="mw-selflink selflink">MinGW</a> – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This page expains how to write [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for software running on Windows using GCC. There are two options to build software for Windows on Linux:

*   [mingw-w64](https://mingw-w64.org): provides 32 and 64-bit toolchains with secure crt, Vista+ API, DDK (ReactOS), and DirectX (WINE) support. For a full list of supported features and differences with the old MinGW.org, see [here](https://sourceforge.net/p/mingw-w64/wiki2/Feature%20list/). Available from the AUR by installing [mingw-w64-gcc](https://aur.archlinux.org/packages/mingw-w64-gcc/).
*   [MinGW](http://www.mingw.org/): provides 32-bit toolchains with limited DirectX support. It also suffers from long-standing breakage in the implementation of thread-local storage and the floating point library support. It has been removed from the official repositories and the AUR.

## Contents

*   [1 Package naming](#Package_naming)
*   [2 Packaging](#Packaging)
*   [3 Examples](#Examples)
    *   [3.1 Autotools](#Autotools)
    *   [3.2 CMake](#CMake)

## Package naming

A package for mingw-w64 should be named `mingw-w64-*pkgname*`. If a static variant of the package is being built, suffix the package name with `-static` (see below for the cases where this is necessary).

## Packaging

Packaging for cross platform packages can be fairly tricky as there are many different build systems and low-level quirks. Take a note of the following things though:

*   always add [mingw-w64-crt](https://aur.archlinux.org/packages/mingw-w64-crt/) to `depends`, unless it depends on another package which implicitly depends on it
*   always add [mingw-w64-gcc](https://aur.archlinux.org/packages/mingw-w64-gcc/) to `makedepends`, unless using [mingw-w64-configure](https://aur.archlinux.org/packages/mingw-w64-configure/) or [mingw-w64-cmake](https://aur.archlinux.org/packages/mingw-w64-cmake/)
*   always add `!strip`, `staticlibs` and `!buildflags` to `options`
*   always use the original `pkgdesc` and append `(mingw-w64)` to the end of `pkgdesc`
*   always use and follow the original `pkgver` of the official package
*   always build both 32-bit and 64-bit versions of libraries
*   always put all stuff under the `/usr/i686-w64-mingw32` and `/usr/x86_64-w64-mingw32` prefix
*   always use `any` as the architecture (except the package contains executables which must run on the build system)
*   always build both shared and static binaries, unless they conflict
*   consider removing unneeded documentation (`rm -r $pkgdir/usr/i686-w64-mingw32/share/{doc,info,man}`, `rm -r $pkgdir/usr/x86_64-w64-mingw32/share/{doc,info,man}`)
*   consider using [mingw-w64-configure](https://aur.archlinux.org/packages/mingw-w64-configure/) for building with configure scripts
*   consider using [mingw-w64-cmake](https://aur.archlinux.org/packages/mingw-w64-cmake/) for building with CMake
*   consider using [mingw-w64-qt5-base](https://aur.archlinux.org/packages/mingw-w64-qt5-base/) or [mingw-w64-qt4](https://aur.archlinux.org/packages/mingw-w64-qt4/) for building with QMake
*   consider using compilation flags `-D_FORTIFY_SOURCE=2 -O2 -pipe -fno-plt -fexceptions --param=ssp-buffer-size=4` (usually named CFLAGS, CXXFLAGS) when no proper build system is provided
*   consider explicitly stripping symbols with `${_arch}-strip` in `package()`'s for-loop as demonstrated in the below PKGBUILD examples.
    *   consider using the [find](/index.php/Find "Find") command to iterate over `$pkgdir` since not all DLLs, static libraries, or executables may reside in their appropriate locations.
        *   if the binary is a DLL, use `${_arch}-strip --strip-unneeded *.dll`
        *   if the binary is a static lib, use `${_arch}-strip -g *.a`
*   if a package is modular (requires certain build dependencies, but said dependencies are optional to the end user) add these to `makedepends` and `optdepends`. Be sure to subtract them from `depends` if updating an existing package. Example of this in use: [mingw-w64-ruby](https://aur.archlinux.org/packages/mingw-w64-ruby/), [mingw-w64-allegro](https://aur.archlinux.org/packages/mingw-w64-allegro/)
*   if a package installs a `$pkgdir/usr/${_arch}/bin/*-config` script, symlink it to `$pkgdir/usr/bin/${_arch}-*-config`
*   if a package uses autoconf, explicitly set `--build="$CHOST"` for `configure` to workaround [autoconf bug #108405](//savannah.gnu.org/support/?108405) or use [mingw-w64-configure](https://aur.archlinux.org/packages/mingw-w64-configure/)

As mentioned above, the files should all be installed into `/usr/i686-w64-mingw32` and `/usr/x86_64-w64-mingw32`. Specifically, all DLLs should be put into `/usr/*-w64-mingw32/bin` as they are dynamic libraries needed at runtime. Their corresponding `.dll.a` files should go into `/usr/*-w64-mingw32/lib`. Please delete any unnecessary documentation and perhaps other files from `/usr/share`. Cross-compilations packages are not meant for the user but only for the compiler and binary distribution, and as such you should try to make them as small as possible.

Always try to match the `pkgver` in your mingw-w64 packages to the `pkgver` of the corresponding regular packages in the official Arch Linux repos (not the testing repos). This ensures that the cross-compiled software works exactly the same way on Windows without any unexpected bugs. If packages in Arch are out-of-date, there usually is a good reason and you should still follow the Arch version instead of using the most recent upstream release. If the corresponding native package is in the AUR, you need not follow this version policy, as many AUR packages are often orphaned or left unmaintained.

## Examples

The following examples will try to cover some of the most common conventions and build systems.

### Autotools

```
pkgname=mingw-w64-foo
pkgver=1.0
pkgrel=1
pkgdesc="Foo bar (mingw-w64)"
arch=('any')
url="http://www.foo.bar"
license=('GPL')
makedepends=('mingw-w64-configure')
depends=('mingw-w64-crt')
options=('!strip' '!buildflags' 'staticlibs')
source=("http://www.foo.bar/foobar.tar.gz")
sha256sums=('8f32d4617390d1c2d16f26a27ab60d97807b35440d45891fa340fc2648b04406')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  cd "${srcdir}/foo-$pkgver/"
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-configure ..
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/foo-$pkgver/build-${_arch}"
    make DESTDIR="${pkgdir}" install
    ${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
  done
}

```

### CMake

```
pkgname=mingw-w64-foo
pkgver=1.0
pkgrel=1
pkgdesc="Foo bar (mingw-w64)"
arch=('any')
url="http://www.foo.bar"
license=('GPL')
makedepends=('mingw-w64-cmake')
depends=('mingw-w64-crt')
options=('!strip' '!buildflags' 'staticlibs')
source=("http://www.foo.bar/foobar.tar.gz")
sha256sums=('8f32d4617390d1c2d16f26a27ab60d97807b35440d45891fa340fc2648b04406')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() { 
  cd "$srcdir/foo-$pkgver/"
  for _arch in ${_architectures}; do
    mkdir -p build-${_arch} && pushd build-${_arch}
    ${_arch}-cmake ..
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/foo-$pkgver/build-${_arch}"
    make DESTDIR="${pkgdir}" install
    ${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a
  done
}

```