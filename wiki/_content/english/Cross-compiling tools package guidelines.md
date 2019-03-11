**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – <a class="mw-selflink selflink">Cross</a> – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 What is cross compiling?](#What_is_cross_compiling?)
*   [2 Important note](#Important_note)
*   [3 Version compatibility](#Version_compatibility)
*   [4 Building a cross compiler](#Building_a_cross_compiler)
*   [5 Package naming](#Package_naming)
*   [6 File placement](#File_placement)
*   [7 Example](#Example)
*   [8 Hows and whys](#Hows_and_whys)
    *   [8.1 Why not installing into /opt?](#Why_not_installing_into_/opt?)
    *   [8.2 What is that *out-of-path executables* thing?](#What_is_that_out-of-path_executables_thing?)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 What to do if compilation fails without clear message?](#What_to_do_if_compilation_fails_without_clear_message?)
    *   [9.2 What does this error [error message] means?](#What_does_this_error_[error_message]_means?)
    *   [9.3 Why do files get installed in wrong places?](#Why_do_files_get_installed_in_wrong_places?)
*   [10 See also](#See_also)

**Tip:** As alternative for creation of cross-compiler packages you could use [crosstool-ng](http://crosstool-ng.org/) and create you own toolchain in fully automated way. crosstool-ng can be found on [crosstool-ng](https://aur.archlinux.org/packages/crosstool-ng/).

## What is cross compiling?

Cross compiling is producing run time binary format other than the default format the compiler is tuned for. A confusing example is [elf](https://en.wikipedia.org/wiki/https://en.wikipedia.org/wiki/Executable_and_Linkable_Format "wikipedia:https://en.wikipedia.org/wiki/Executable and Linkable Format") and [a.out](https://en.wikipedia.org/wiki/https://en.wikipedia.org/wiki/a.out "wikipedia:https://en.wikipedia.org/wiki/a.out"). Most, if not all, Linux machines compilers will, by default, produce an elf. Since that is the native Linux format. Most of them are able to produce an a.out format with a one or two command line options. Even though it is rather easy to produce with the native Linux compilers an a.out, this is still, per stricter definition, a cross compiling process.

To emphasize a common mistake, one can cross compile for the same hardware architecture the compiler is run on. Compiling on Linux x86_64 machine to be run on an MS x86_64 machine is cross compiling.

## Important note

This page describes the new way of doing things, inspired by the following packages:

*   [mingw-w64-gcc](https://aur.archlinux.org/packages/mingw-w64-gcc/) and other packages from `mingw-w64-*` series
*   [arm-none-eabi-gcc](https://www.archlinux.org/packages/?name=arm-none-eabi-gcc) and other packages from `arm-none-eabi-*` series
*   [arm-wince-cegcc-gcc](https://aur.archlinux.org/packages/arm-wince-cegcc-gcc/) and other packages from `arm-wince-cegcc-*` series

## Version compatibility

**Warning:** Using incompatible versions of packages for toolchain compilation leads to inevitable failures. By default consider **all** versions incompatible.

The following strategies allows you to select compatible versions of gcc, binutils, kernel and C library:

*   General rules:
    *   there is a correlation between gcc and binutils releases, use simultaneously released versions;
    *   it is better to use latest kernel headers to compile libc but use `--enable-kernel` switch (specific to glibc, other C libraries may use different conventions) to enforce work on older kernels;
*   [Official repositories](/index.php/Official_repositories "Official repositories"): you may have to apply additional fixes and hacks, but versions used by Arch Linux (or it's architecture-specific forks) most probably can be made to work together;
*   Software documentation: all GNU software have `README` and `NEWS` files, documenting things like minimal required versions of dependencies;
*   Other distributions: they too do cross-compilation
*   [http://clfs.org](http://clfs.org) covers steps, necessary for building cross-compiler and mentions somewhat up-to-date versions of dependencies.

## Building a cross compiler

The general approach to building a cross compiler is:

1.  binutils: Build a cross-binutils, which links and processes for the target architecture
2.  headers: Install a set of C library and kernel headers for the target architecture
    1.  use [linux-api-headers](https://www.archlinux.org/packages/?name=linux-api-headers) as reference and pass `ARCH=*target-architecture*` to **make**
    2.  create libc headers package (process for Glibc is described [here](http://sources.redhat.com/ml/crossgcc/2003-06/msg00170.html))
3.  gcc-stage-1: Build a basic (stage 1) gcc cross-compiler. This will be used to compile the C library. It will be unable to build almost anything else (because it can't link against the C library it doesn't have).
4.  libc: Build the cross-compiled C library (using the stage 1 cross compiler).
5.  gcc-stage-2: Build a full (stage 2) C cross-compiler

The source of the headers and libc will vary across platforms.

**Tip:** Exact procedure varies greatly, depending on your needs. For example, if you want to create a "clone" of an Arch Linux system with the same versions of kernel and glibc, you can skip building headers and pass `--with-build-sysroot=/` to `configure`.

## Package naming

The package name shall **not** be prefixed with the word `cross-` (it was previously proposed, but was not adopted in official packages, probably due to additional length of names), and shall consist of the package name, prefixed by [GNU triplet](https://wiki.debian.org/Multiarch/Tuples "debian:Multiarch/Tuples") without vendor field or with "unknown" in vendor field; example: `arm-linux-gnueabihf-gcc`. If shorter naming convention exists (e.g. `mips-gcc`), it may be used, but this is not recommended.

## File placement

Latest versions of gcc and binutils use non-conflicting paths for sysroot and libraries. Executables shall be placed into `/usr/bin/`, to prevent conflicts here, prefix all of them with architecture name.

Typically, `./configure` would have at least following parameters:

```
_target=*your_target*
_sysroot=/usr/lib/${_target}
...
./configure \
    --prefix=${_sysroot} \
    --sysroot=${_sysroot} \
    --bindir=/usr/bin
```

where `*your_target*` can be, e.g., "i686-pc-mingw32".

## Example

This is PKGBUILD for binutils for MinGW. Things worth noticing are:

*   specifying root directory of the cross-environment
*   usage of `${_pkgname}` , `${_target}` and `${_sysroot}` variables to make the code more readable
*   removal of the duplicated/conflicting files

```
# Maintainer: Allan McRae <allan@archlinux.org>

# cross toolchain build order: binutils, headers, gcc (pass 1), w32api, mingwrt, gcc (pass 2)

_target=i686-pc-mingw32
_sysroot=/usr/lib/${_target}

pkgname=${_target}-binutils
_pkgname=binutils
pkgver=2.19.1
pkgrel=1
pkgdesc="MinGW Windows binutils"
arch=('i686' 'x86_64')
url="http://www.gnu.org/software/binutils/"
license=('GPL')
depends=('glibc>=2.10.1' 'zlib')
options=('!libtool' '!distcc' '!ccache')
source=(http://ftp.gnu.org/gnu/${_pkgname}/${_pkgname}-${pkgver}.tar.bz2)
md5sums=('09a8c5821a2dfdbb20665bc0bd680791')

build() {
  cd ${srcdir}/${_pkgname}-${pkgver}
  mkdir binutils-build && cd binutils-build

  ../configure --prefix=${_sysroot} --bindir=/usr/bin \
    --with-sysroot=${_sysroot} \
    --build=$CHOST --host=$CHOST --target=${_target} \
    --with-gcc --with-gnu-as --with-gnu-ld \
    --enable-shared --without-included-gettext \
    --disable-nls --disable-debug --disable-win32-registry
  make
  make DESTDIR=${pkgdir}/ install

  # clean-up cross compiler root
  rm -r ${pkgdir}/${_sysroot}/{info,man}
}

```

**Note:** During cross-toolchain building always execute `configure` and **make** commands from dedicated directory (so-called out-of-tree compilation) and remove whole `src` directory after slightest change in [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

## Hows and whys

### Why not installing into `/opt`?

Two reasons:

1.  First, according to File Hierarchy Standard, these files just belong somewhere to `/usr`. Period.
2.  Second, installing into `/opt` is a last measure when there is no other option.

### What is that *out-of-path executables* thing?

This weird thing allows easier cross-compiling. Sometimes, project Makefiles do not use `CC` & co. variables and instead use **gcc** directly. If you just want to try to cross-compile such project, editing the Makefile could be a very lengthy operation. However, changing the `$PATH` to use "our" executables first is a very quick solution. You would then run `PATH=/usr/*arch*/bin/:$PATH make` instead of `make`.

## Troubleshooting

### What to do if compilation fails without clear message?

For error, occurred during running `configure`, read `$srcdir/*pkgname*-build/config.log`. For error, occurred during compilation, scroll console log up or search for word "error".

### What does this error [error message] means?

Most probably you made some of non-obvious errors:

*   Too many or too few configuration flags. Try to use already proven set of flags.
*   Dependencies are corrupted. For example misplaced or missing binutils files may result in cryptic error during gcc configuration.
*   You did not add `export CFLAGS=""` to your `build()` function (see [bug 25672](http://gcc.gnu.org/bugzilla/show_bug.cgi?id=25672) in GCC Bugzilla).
*   Some `--prefix`/`--with-sysroot` combination may require directories to be writable (non-obvious from clfs guides).
*   sysroot does nor yet has kernel/libc headers.
*   If google-fu does not help, immediately abandon current configuration and try more stable/proven one.

### Why do files get installed in wrong places?

Various methods of running generic `make install` line results in different results. For example, some make targets may not provide `DESTDIR` support and instead require `install_root` usage. The same for `tooldir`, `prefix` and other similar arguments. Sometimes providing parameters as arguments instead of environment variables, e.g

```
./configure CC=arm-elf-gcc

```

instead of

```
CC=arm-elf-gcc ./configure

```

and vice versa may result in different outcomes (often caused by recursive self-invocation of configure/make).

## See also

*   [http://wiki.osdev.org/GCC_Cross-Compiler](http://wiki.osdev.org/GCC_Cross-Compiler)