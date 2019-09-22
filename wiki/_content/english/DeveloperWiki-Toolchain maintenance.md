This page is intended to contain all relevant information to bootstrap the toolchain on Arch Linux, including any issues that are expected to be found, as well as providing documentation on the build order when new versions of important toolchain packages are released.

The toolchain build order is as follows:

linux-api-headers -> glibc -> binutils -> gcc -> binutils -> glibc

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Linux Api Headers](#Linux_Api_Headers)
*   [2 GNU C Library](#GNU_C_Library)
*   [3 GNU Binutils](#GNU_Binutils)
*   [4 GNU Compiler Collection](#GNU_Compiler_Collection)

## Linux Api Headers

Provided by [linux-api-headers](https://www.archlinux.org/packages/?name=linux-api-headers).

It is the first step on the toolchain.

## GNU C Library

Provided by [glibc](https://www.archlinux.org/packages/?name=glibc).

Second step of the toolchain, also, it needs to be rebuilt after a new gcc rebuild.

There are some packages that require a rebuild after a new glibc, regardless of a so bump, such as [valgrind](https://www.archlinux.org/packages/?name=valgrind).

## GNU Binutils

Provided by [binutils](https://www.archlinux.org/packages/?name=binutils).

Third step of the toolchain, also it needs to be rebuilt twice on new glibc releases and also after a new gcc release.

## GNU Compiler Collection

Provided by [gcc](https://www.archlinux.org/packages/?name=gcc).

Last (or first) step of the toolchain, and vital to building its entirety. Its update triggers a binutils and glibc rebuild, as well as other packages, like [linux](https://www.archlinux.org/packages/?name=linux) itself and [libtool](https://www.archlinux.org/packages/?name=libtool)