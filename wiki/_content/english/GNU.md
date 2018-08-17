Related articles

*   [Arch Linux](/index.php/Arch_Linux "Arch Linux")
*   [Core utilities](/index.php/Core_utilities "Core utilities")

From [Wikipedia](https://en.wikipedia.org/wiki/GNU "wikipedia:GNU"):

	GNU is an operating system and an extensive collection of computer software. GNU is composed wholly of free software, most of which is licensed under the GNU Project's own General Public License (GPL). GNU is a recursive acronym for "GNU's Not Unix!".

Because the GNU kernel, [Hurd](https://www.gnu.org/s/hurd/hurd.html), is not production-ready [[1]](https://www.gnu.org/software/hurd/hurd/status.html) GNU is usually used with the Linux kernel. [Arch Linux](/index.php/Arch_Linux "Arch Linux") is such a GNU/Linux distribution, using GNU software like the [Bash](/index.php/Bash "Bash") shell, the GNU coreutils, the GNU toolchain and numerous other utilities and libraries. This page does not attempt to list all of the [nearly 400](https://www.gnu.org/software/software.html#allgnupkgs) GNU packages and only highlights some.

## Contents

*   [1 Texinfo](#Texinfo)
*   [2 Base system](#Base_system)
*   [3 Toolchain](#Toolchain)
    *   [3.1 Build system](#Build_system)
*   [4 Other software](#Other_software)
*   [5 See also](#See_also)

## Texinfo

GNU software is documented using the [Texinfo](https://en.wikipedia.org/wiki/Texinfo "wikipedia:Texinfo") typesetting syntax. You can view Info documents using the `info` program, provided by the [texinfo](https://www.archlinux.org/packages/?name=texinfo) package, which is part of [base](https://www.archlinux.org/groups/x86_64/base/).

While most GNU software also provides [man pages](/index.php/Man_page "Man page"), the Info documents tend to be more comprehensive.

## Base system

*   **[GRUB](/index.php/GRUB "GRUB")** — GRUB is the bootloader from the GNU project.

	[https://www.gnu.org/software/grub/](https://www.gnu.org/software/grub/) || [grub](https://www.archlinux.org/packages/?name=grub)

*   **[bash](/index.php/Bash "Bash")** — It is an sh-compatible shell that incorporates useful features from the Korn shell (ksh) and C shell (csh).

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[coreutils](/index.php/Coreutils "Coreutils")** — coreutils provides the basic file, shell and text manipulation utilities of the GNU operating system.

	[https://www.gnu.org/software/coreutils/](https://www.gnu.org/software/coreutils/) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

*   **[gzip](https://en.wikipedia.org/wiki/gzip "wikipedia:gzip")** — gzip is both a file format and a software application for compression and decompression.

	[https://www.gnu.org/software/gzip/](https://www.gnu.org/software/gzip/) || [gzip](https://www.archlinux.org/packages/?name=gzip)

*   **[tar](/index.php/Tar "Tar")** — It provides the ability to create or decompress tar archives, as well as various other kinds of manipulation.

	[https://www.gnu.org/software/tar/](https://www.gnu.org/software/tar/) || [tar](https://www.archlinux.org/packages/?name=tar)

## Toolchain

Most tools of the [GNU toolchain](https://en.wikipedia.org/wiki/GNU_toolchain "wikipedia:GNU toolchain") are in the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group, except *glibc* which is in [base](https://www.archlinux.org/groups/x86_64/base/) and *gdb* which is in neither group.

*   **[GNU make](https://en.wikipedia.org/wiki/Make_(software) "wikipedia:Make (software)")** — GNU make utility to maintain groups of programs.

	[http://www.gnu.org/software/make](http://www.gnu.org/software/make) || [make](https://www.archlinux.org/packages/?name=make)

*   **[GCC](https://en.wikipedia.org/wiki/GNU_Compiler_Collection "wikipedia:GNU Compiler Collection")** — The GNU Compiler Collection - C and C++ frontends.

	[https://gcc.gnu.org/](https://gcc.gnu.org/) || [gcc](https://www.archlinux.org/packages/?name=gcc)

*   **[GNU C Library](https://en.wikipedia.org/wiki/GNU_C_Library "wikipedia:GNU C Library")** — GNU's implementation of the C library.

	[https://www.gnu.org/software/libc/](https://www.gnu.org/software/libc/) || [glibc](https://www.archlinux.org/packages/?name=glibc) (part of [base](https://www.archlinux.org/groups/x86_64/base/))

*   **[GNU Binutils](https://en.wikipedia.org/wiki/GNU_Binutils "wikipedia:GNU Binutils")** — A set of programs to assemble and manipulate binary and object files. Includes [ld](https://en.wikipedia.org/wiki/GNU_linker "wikipedia:GNU linker").

	[https://www.gnu.org/software/binutils/](https://www.gnu.org/software/binutils/) || [binutils](https://www.archlinux.org/packages/?name=binutils)

*   **[GNU bison](https://en.wikipedia.org/wiki/GNU_bison "wikipedia:GNU bison")** — The GNU general-purpose parser generator.

	[https://www.gnu.org/software/bison/bison.html](https://www.gnu.org/software/bison/bison.html) || [bison](https://www.archlinux.org/packages/?name=bison)

*   **[GNU m4](https://en.wikipedia.org/wiki/GNU_m4 "wikipedia:GNU m4")** — The GNU macro processor.

	[https://www.gnu.org/software/m4/](https://www.gnu.org/software/m4/) || [m4](https://www.archlinux.org/packages/?name=m4)

*   **[GDB](https://en.wikipedia.org/wiki/GNU_Debugger "wikipedia:GNU Debugger")** — The GNU Debugger.

	[https://www.gnu.org/software/gdb/](https://www.gnu.org/software/gdb/) || [gdb](https://www.archlinux.org/packages/?name=gdb)

### Build system

From [Wikipedia](https://en.wikipedia.org/wiki/GNU_build_system "wikipedia:GNU build system"):

	The GNU Build System, also known as the Autotools, is a suite of programming tools designed to assist in making source code packages portable to many Unix-like systems.

*   **[GNU Autoconf](https://en.wikipedia.org/wiki/Autoconf "wikipedia:Autoconf")** — Tool for automatically configuring source code.

	[http://www.gnu.org/software/autoconf](http://www.gnu.org/software/autoconf) || [autoconf](https://www.archlinux.org/packages/?name=autoconf)

*   **[GNU Automake](https://en.wikipedia.org/wiki/Automake "wikipedia:Automake")** — Tool for automatically creating Makefiles.

	[http://www.gnu.org/software/automake](http://www.gnu.org/software/automake) || [automake](https://www.archlinux.org/packages/?name=automake)

*   **[GNU Libtool](https://en.wikipedia.org/wiki/GNU_Libtool "wikipedia:GNU Libtool")** — A generic library support script.

	[http://www.gnu.org/software/libtool](http://www.gnu.org/software/libtool) || [libtool](https://www.archlinux.org/packages/?name=libtool)

## Other software

Many other optional GNU tools are available in the [official repositories](/index.php/Official_repositories "Official repositories"):

*   [GNOME](/index.php/GNOME "GNOME"), a desktop environment
*   [GIMP](/index.php/GIMP "GIMP"), an image editor
*   [GTK+](/index.php/GTK%2B "GTK+"), a widget toolkit
*   [Gnumeric](/index.php/Gnumeric "Gnumeric"), a spreadsheet software
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"), a partition manager
*   [GNU Screen](/index.php/GNU_Screen "GNU Screen"), a terminal multiplexer
*   [GNU nano](/index.php/GNU_nano "GNU nano"), a command-line text editor
*   [GNU Emacs](/index.php/GNU_Emacs "GNU Emacs"), an extensible, customizable, self-documenting text editor
*   [GnuPG](/index.php/GnuPG "GnuPG"), an OpenPGP implementation
*   [GNU Octave](/index.php/GNU_Octave "GNU Octave"), a scientific programming language

## See also

*   [https://www.gnu.org/](https://www.gnu.org/)
*   [The GNU Manifesto](https://www.gnu.org/gnu/manifesto)
*   [Wikipedia:List of GNU packages](https://en.wikipedia.org/wiki/List_of_GNU_packages "wikipedia:List of GNU packages")
*   The [Arch Hurd Project](https://archhurd.org/) aims to port Arch Linux to the Hurd kernel.