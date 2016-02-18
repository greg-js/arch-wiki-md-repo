**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – **Free Pascal** – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This page explains on how to write [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") for software built with the [Free Pascal Compiler (FPC)](http://freepascal.org). There currently exists two options for building software of Linux, as well as a handful of options for building software on other targets using FPC cross compilers:

## Contents

*   [1 Arch Linux](#Arch_Linux)
*   [2 Cross compilers](#Cross_compilers)
*   [3 Free Pascal](#Free_Pascal)
    *   [3.1 Package naming](#Package_naming)
    *   [3.2 Helpful snippets](#Helpful_snippets)
    *   [3.3 Packaging](#Packaging)
        *   [3.3.1 Cross compiling](#Cross_compiling)

#### Arch Linux

*   [fpc](https://www.archlinux.org/packages/?name=fpc) is available in the official Arch community repository and provides a compiler targetting only your host CPU (i686 or x86_64).
*   [fpc-multilib](https://aur.archlinux.org/packages/fpc-multilib/) is available from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") which provides an x86_64 host compiler targetting both i686 and x86_64 CPU Linuxes. This will also provide the [ppcross386](https://aur.archlinux.org/packages/ppcross386/) FPC compiler driver package.

#### Cross compilers

*   [fpc-arm-android-rtl](https://aur.archlinux.org/packages/fpc-arm-android-rtl/) for ARM-based Android (beta)
*   [fpc-arm-linux-rtl](https://aur.archlinux.org/packages/fpc-arm-linux-rtl/) for ARM-based Linux
*   [fpc-arm-wince-rtl](https://aur.archlinux.org/packages/fpc-arm-wince-rtl/) for MS Windows CE
*   [fpc-i386-android-rtl](https://aur.archlinux.org/packages/fpc-i386-android-rtl/) for 32-bit Intel based Android (beta)
*   [fpc-i386-freebsd-rtl](https://aur.archlinux.org/packages/fpc-i386-freebsd-rtl/) for 32-bit Intel FreeBSD
*   [fpc-i386-win32-rtl](https://aur.archlinux.org/packages/fpc-i386-win32-rtl/) for 32-bit MS Windows
*   [fpc-powerpc-linux-rtl](https://aur.archlinux.org/packages/fpc-powerpc-linux-rtl/) for 32-bit PowerPC-based Linux
*   [fpc-sparc-linux-rtl](https://aur.archlinux.org/packages/fpc-sparc-linux-rtl/) for SPARC-based Linux
*   [fpc-x86_64-win64-rtl](https://aur.archlinux.org/packages/fpc-x86_64-win64-rtl/) for 64-bit MS Windows

## Free Pascal

### Package naming

The project name alone is usually sufficient. However, in the case of cross-compiling, the package should be prefixed with `fpc32-` when targetting i686 Linux from multilib and named in the format of `fpc-*cpu*-*system*-*pkgname*` when targetting non-Arch Linux systems.

### Helpful snippets

*   Determine FPC's version and the CPU and OS of the units to output:

```
_unitdir=`fpc -iSP`-`fpc -iSO`
_fpcver=`fpc -iV`

```

### Packaging

Please adhere to the following when making an FPC-based package:

*   always add [fpc](https://www.archlinux.org/packages/?name=fpc) to either `makedepends` or `depends`
*   always put all compiled units (*.a, *.compiled, *.o, *.ppu, *.res, *.rst) under `/usr/lib/fpc/*$_fpcver*/units/*$arch*-linux`
*   add `staticlibs` to `options` if installing an import library

#### Cross compiling

*   always add the corresponding cross compiler package mentioned above (`fpc-*cpu*-*system*-rtl` or [fpc-multilib](https://aur.archlinux.org/packages/fpc-multilib/) for multilib) to `depends`
*   always add `!strip` to `options` for non-Unix-based systems
*   always put all compiled units (*.a, *.compiled, *.o, *.ppu, *.res, *.rst) under `/usr/lib/fpc/*$_fpcver*/units/*$_unitdir*` (or if multilib, `/usr/lib/fpc/*$_fpcver*/units/i386-linux`)
*   always use `any` (`x86_64` if multilib) as the architecture
*   add `staticlibs` to `options` if installing an import library