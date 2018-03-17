[Open Watcom](http://www.openwatcom.org/) is a **Fortran/C/C++'** compiler with many cross-compilation targets. Those old enough most likely fondly remember old DOS games ending with the [DOS4GW](https://en.wikipedia.org/wiki/DOS/4G "wikipedia:DOS/4G") extender, where the "W" stands for "watcom". In general it was a [very popular compiler for high-end games](https://en.wikipedia.org/wiki/Watcom_C_compiler "wikipedia:Watcom C compiler") at the time for producing very efficient binaries in memory-constrained environments (like DOS). Watcom [lives on](http://www.openwatcom.com/index.php/History) as Open Watcom, with an [official release](http://www.openwatcom.org/) at version 1.9 and an [unofficial fork](https://github.com/open-watcom) at version 2.0.

## Contents

*   [1 Installation](#Installation)
*   [2 Wmake](#Wmake)
*   [3 Using the Open Watcom package in Wine](#Using_the_Open_Watcom_package_in_Wine)
*   [4 Compilers](#Compilers)
    *   [4.1 16-bit x86 compilers](#16-bit_x86_compilers)
    *   [4.2 32-bit x86 compilers](#32-bit_x86_compilers)
    *   [4.3 Comparisons to other (cross-) compilers](#Comparisons_to_other_.28cross-.29_compilers)
    *   [4.4 Compiler optimization flags and other options](#Compiler_optimization_flags_and_other_options)
    *   [4.5 (Cross-) compilation : Common settings](#.28Cross-.29_compilation_:_Common_settings)
    *   [4.6 Linux](#Linux)
    *   [4.7 DOS (16-bit)](#DOS_.2816-bit.29)
    *   [4.8 DOS (32-bit DOS4GW Extender)](#DOS_.2832-bit_DOS4GW_Extender.29)
    *   [4.9 WIN16](#WIN16)
    *   [4.10 WIN32](#WIN32)
    *   [4.11 OS/2 (16-bit)](#OS.2F2_.2816-bit.29)
    *   [4.12 OS/2 (32-bit)](#OS.2F2_.2832-bit.29)
    *   [4.13 Netware](#Netware)
    *   [4.14 QNX](#QNX)
*   [5 Packaged third-party libraries and utilities](#Packaged_third-party_libraries_and_utilities)
    *   [5.1 Libraries](#Libraries)
    *   [5.2 Extra languages](#Extra_languages)
*   [6 See also](#See_also)

## Installation

The unofficial 2.0 release can be [installed](/index.php/Install "Install") with the [openwatcom-v2](https://aur.archlinux.org/packages/openwatcom-v2/) package.

## Wmake

Open Watcom comes with its own make utility (wmake). On Windows hosts, [CMake](https://en.wikipedia.org/wiki/CMake "wikipedia:CMake") supports generating wmake files. At this moment, it is [unfortunately not possible](http://public.kitware.com/Bug/view.php?id=14793) to generate wmake files for cross compilation with CMake on Linux.

## Using the Open Watcom package in Wine

The [openwatcom-v2](https://aur.archlinux.org/packages/openwatcom-v2/) package includes executables for all supported host platforms by default. This can be quite handy sometimes if one for example wants to debug a cross-compiled binary using the watcom debugger **wd**. In principle, the same could be done also with DOS emulators for example. Steps to set up a WINEPREFIX to use the already existing Watcom install:

*   create a fresh WINEPREFIX (for example $HOME/.watcom) by WINEPREFIX=$HOME/.watcom winecfg
*   cd to $WINEPREFIX/drive_c and make a symlink to /opt/watcom named watcom (ln -s /opt/watcom watcom)
*   run regedit
*   under HKEY_CURRENT_USER/Environment , add the following string variables
*   WATCOM = C:\WATCOM
*   PATH = C:\WATCOM\BINNT
*   EDPATH = C:\WATCOM\EDDAT
*   WIPFC = C:\WATCOM\WIPFC

## Compilers

Open Watcom comes with a very efficient native 16-bit compiler supporting DOS and Win16 targets and a 32-bit x86 compiler targetting many different OSes (NT/Win32, OS/2, NetWare, Linux, ...). There is also experimental support for PowerPC, Alpha AXP, MIPS and SPARC architectures. A [major aim](http://www.openwatcom.org/index.php/Open_Watcom_Reflections_2012-11-19) for the v2 development is support for x86_64 and ARM architectures. The two most obvious "competitors" of Open Watcom would be the GCC-based [MinGW](http://www.mingw.org/) (for Win32-targets) and [DJGPP](http://www.delorie.com/djgpp/) (for DOS targets).

### 16-bit x86 compilers

The 16-bit x86 compilers finds its OS-independent libraries in the **$WATCOM/lib286** directory and its OS-dependent libraries in **$WATCOM/lib286/${target_os}** sub-directory. Some OSes might need extra library paths, which can be added by the **LIBPATH** environment variable.

*   **wcc**: the 16-bit "compile only" C compiler
*   **wpp**: the 16-bit "compile only" C++ compiler
*   **wcl**: the 16-bit "compile and link" utility for C/C++
*   **wfc**: the 16-bit "compile only" Fortran compiler
*   **wfl**: the 16-bit "compile and link" utility for Fortran
*   **owcc**: the POSIX compatible "compile and link" utility. Set CC=owcc in a project depending on GNU makefiles.

### 32-bit x86 compilers

The 32-bit x86 compilers finds its OS-independent libraries in the **$WATCOM/lib386** directory and its OS-dependent libraries in **$WATCOM/lib386/${target_os}** sub-directory. Some OSes might need extra library paths, which can be added by the **LIBPATH** environment variable.

*   **wcc386**: the 32-bit "compile only" C compiler
*   **wpp386**: the 32-bit "compile only" C++ compiler
*   **wcl386**: the 32-bit "compile and link" utility for C/C++
*   **wfc386**: the 32-bit "compile only" Fortran compiler
*   **wfl386**: the 32-bit "compile and link" utility for Fortran
*   **owcc** : the POSIX compatible "compile and link" utility. Set CC=owcc in a project depending on GNU makefiles.

### Comparisons to other (cross-) compilers

A striking difference compared to the [binutils](https://www.archlinux.org/packages/?name=binutils)-based compilers ([gcc](https://www.archlinux.org/packages/?name=gcc), [clang](https://www.archlinux.org/packages/?name=clang), [pcc](https://aur.archlinux.org/packages/pcc/)) when used as a cross compiler is that Open watcom only uses a single compiler (one for each target CPU architecture) and the target OS is determined by a compilation flag (see "cross compiling" below). Further, many OS-independent libraries lives in a generic architecture-specific location ($WATCOM/lib286 and $WATCOM/lib386) and only libraries with OS-specific features are put into OS-specific sub-directories - this is thanks to the Open Watcom C runtime that is distributed together with the compiler. This means that it is very easy to use a single install of Open Watcom as a cross compiler for a wide range of OSes. In contrast, a cross-compile toolchain based on binutils typically requires building a target-specific ["trinity" of binutils, compiler and libc](http://wiki.osdev.org/GCC_Cross-Compiler). Another advantage of Open Watcom as a Win32 cross compiler is that the resulting binaries and libraries integrate nicely with the target OS. For example, [Python compiled with Open Watcom](http://be.org/) can load plugins compiled with [MSVC](https://en.wikipedia.org/wiki/Visual_C%2B%2B "wikipedia:Visual C++"). This is similar to how the different binutils-based compilers (often) can use libraries built with another binutils-based compiler. At this moment, the resulting binaries are not as optimized as those made by GCC.

### Compiler optimization flags and other options

The Watcom compilers do not follow the same standard as GCC for flags (for example, it will not understand -O3 by default). It has a [rich set of options](http://www.users.pjwstk.edu.pl/~jms/qnx/help/watcom/compiler-tools/cpopts.html) to define target architecture, optimizations and other things. Some recommended flags for optimized 16-bit code can be found [here](http://www.ousob.com/ng/wcppug/ng43372.php).

### (Cross-) compilation : Common settings

To cross compile, set the correct environment variables and a compile flag telling the compiler which target is intended. Without compile flags defining target, a native build is assumed.

Common for all targets (from an Arch Linux host):

 `export WATCOM=/opt/watcom`  `export PATH=$WATCOM/binl:$PATH`  `export EDPATH=$WATCOM/eddat`  `export WIPFC=$WATCOM/wipfc` 

A small overview of all build targets can be found [here](http://www.openwatcom.org:4000/@md=c&cd=//&cdf=//depot/V2/src/link/specs.sp&c=Trs@//depot/V2/src/link/specs.sp?ac=64&rev1=3).

### Linux

for C, use compilers: **wcc386**, **wcl386** or **owcc** add **-bt=linux** for wcc386 or **-bcl=linux** for wcl386 or **-blinux** for owcc. Flags not absolutely needed since the compiler assumes a native build if nothing else is added.

 `export INCLUDE=$WATCOM/lh` 

### DOS (16-bit)

add **-bt=dos** for wcc or **-bcl=dos** for wcl or **-bdos** for owcc

 `export INCLUDE=$WATCOM/h` 

### DOS (32-bit DOS4GW Extender)

add **-bt=dos** for wcc386 or **-bt=dos -l=dos4g** for wcl386 or **-bdos4g** for owcc

 `export INCLUDE=$WATCOM/h` 

### WIN16

add **-bt=windows** for wcc or **-bcl=windows** for wcl or **-bwindows** for owcc

 `export INCLUDE=$WATCOM/h:$WATCOM/h/win` 

### WIN32

add **-bt=nt** for wcc386 or **-bcl=nt** for wcl386 or **-bnt** for owcc

 `export INCLUDE=$WATCOM/h:$WATCOM/h/nt` 

### OS/2 (16-bit)

add **-bt=os2** for wcc or **-bcl=os2** for wcl or **-bos2** for owcc

 `export INCLUDE=$WATCOM/h:$WATCOM/h/os21x`  `export LIBPATH=$WATCOM/binp/dll:$LIBPATH` 

### OS/2 (32-bit)

add **-bt=os2** for wcc386 or **-bt=os2 -l=os2v2** for wcl386 or **-bos2v2** for owcc

 `export INCLUDE=$WATCOM/h:$WATCOM/h/os2`  `export LIBPATH=$WATCOM/binp/dll:$LIBPATH` 

### Netware

add **-bt=netware** for wcc386 or **-bcl=netware** for wcl386 or **-bnetware** for owcc

 `export INCLUDE=$WATCOM/h:$WATCOM/novh`  `export LIBPATH=$WATCOM/nlm:$LIBPATH` 

Some packages may need a [| proprietary set of libraries and headers from Novell](http://www.novell.com/coolsolutions/trench/411.html), which have been packaged in AUR: [ow-netware_ndk](https://aur.archlinux.org/packages/ow-netware_ndk/)

### QNX

The Watcom compiler also supports QNX as a target, but since the libraries were not redistributable with the open source Open Watcom distribution, it has not been well-tested ever since. In theory, it might be possible to still compile for QNX if a C library is built for Watcom

## Packaged third-party libraries and utilities

There are many [3rd party libraries and resources](http://openwatcom.org/index.php/User_Resources) ready for Watcom. The packaging should conform to the [MinGW packaging guidelines](/index.php/MinGW_PKGBUILD_Guidelines "MinGW PKGBUILD Guidelines"), but with the difference that they are packaged as much as possible as split packages. One exception to the split package aim is when one target has unique (or proprietary) build dependencies. Pre-packaged libraries and compiler front ends are meant to make it easy for someone to start using the cross compiler. Below are some resources packaged for Arch linux:

### Libraries

*   [ow-zlib](https://aur.archlinux.org/packages/ow-zlib/) || **targets** : **32-bit :** linux, Win32, DOS(4GW), OS/2, Netware **16-bit:** DOS, Win16, OS/2
*   [ow-libbz2](https://aur.archlinux.org/packages/ow-libbz2/)
*   Curses: [ow-curses-win32a](https://aur.archlinux.org/packages/ow-curses-win32a/) : **32-bit:** Win32, DOS(4GW) **16-bit:** DOS, (Win16 a work-in-progress)

### Extra languages

One area where GCC is stronger than Open Watcom is language support. To mitigate this, some [source-to-source compilers](https://en.wikipedia.org/wiki/Source-to-source_compiler "wikipedia:Source-to-source compiler") can be built on/for Watcom.

## See also

The Open Watcom community is relatively small, with moderate activity on [Reddit](http://www.reddit.com/r/OpenWatcom/). The primary discussions are done on the "contributors" and "users.c_cpp" groups on the Open Watcom [newsgroups](news://news.openwatcom.org/) a third option is the user forums on [sourceforge](http://sourceforge.net/p/openwatcom/discussion/).

For continously up-to-date info, check out the Open Watcom v2 [wiki](https://github.com/open-watcom/open-watcom-v2/wiki) on Github.