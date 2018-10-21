Related articles

*   [Arch Linux (简体中文)](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")
*   [Core utilities (简体中文)](/index.php/Core_utilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Core utilities (简体中文)")

From [Wikipedia](https://en.wikipedia.org/wiki/GNU "wikipedia:GNU"):

	GNU 是一种操作系统和一种电脑软件的广泛集合. GNU 完全由免费软件组成, 它们中的大多数都有GNU项目自己的普遍公共合格证（GPL）的许可. GNU "GNU's Not Unix!"的递归缩写.

因为GNU内核, [Hurd](https://www.gnu.org/s/hurd/hurd.html), 还没能生产 [[1]](https://www.gnu.org/software/hurd/hurd/status.html) GNU 通常使用 Linux 内核. [Arch Linux](/index.php/Arch_Linux "Arch Linux") 就是这样一种 GNU/Linux 发行版, 使用的是比如说 [Bash](/index.php/Bash "Bash") shell, GNU 核心工具, the GNU 工具链和许多其他工具和库. 这个页面不打算列出所有 [将近400个](https://www.gnu.org/software/software.html#allgnupkgs) GNU 包，只列出一些重要的.

## Contents

*   [1 Texinfo](#Texinfo)
*   [2 基本系统](#.E5.9F.BA.E6.9C.AC.E7.B3.BB.E7.BB.9F)
*   [3 Toolchain](#Toolchain)
    *   [3.1 Build system](#Build_system)
*   [4 Other software](#Other_software)
*   [5 See also](#See_also)

## Texinfo

GNU 软件是用 [Texinfo](https://en.wikipedia.org/wiki/Texinfo "wikipedia:Texinfo") 排版语法来编排的. 你可以通过`info` 程序查阅info文档, 这由 [texinfo](https://www.archlinux.org/packages/?name=texinfo) 包提供, 这是 [base](https://www.archlinux.org/groups/x86_64/base/)的一部分.

大部分GNU软件都提供了 [man pages](/index.php/Man_page "Man page"), 这个Info文档更全面.

## 基本系统

*   **[GRUB](/index.php/GRUB "GRUB")** — GRUB 是来自 GNU 项目的引导程序.

	[https://www.gnu.org/software/grub/](https://www.gnu.org/software/grub/) || [grub](https://www.archlinux.org/packages/?name=grub)

*   **[Bash](/index.php/Bash "Bash")** — It is an sh-compatible shell that incorporates useful features from the Korn shell (ksh) and C shell (csh).

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[Coreutils](/index.php/Coreutils "Coreutils")** — Coreutils provides the basic file, shell and text manipulation utilities of the GNU operating system.

	[https://www.gnu.org/software/coreutils/](https://www.gnu.org/software/coreutils/) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

*   **[gzip](https://en.wikipedia.org/wiki/gzip "wikipedia:gzip")** — gzip is both a file format and a software application for compression and decompression.

	[https://www.gnu.org/software/gzip/](https://www.gnu.org/software/gzip/) || [gzip](https://www.archlinux.org/packages/?name=gzip)

*   **[tar](/index.php/Tar "Tar")** — It provides the ability to create or decompress tar archives, as well as various other kinds of manipulation.

	[https://www.gnu.org/software/tar/](https://www.gnu.org/software/tar/) || [tar](https://www.archlinux.org/packages/?name=tar)

## Toolchain

Most tools of the [GNU toolchain](https://en.wikipedia.org/wiki/GNU_toolchain "wikipedia:GNU toolchain") are in the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group, except *glibc* which is in [base](https://www.archlinux.org/groups/x86_64/base/) and GDB which is in neither group.

*   **[GNU make](https://en.wikipedia.org/wiki/Make_(software) "wikipedia:Make (software)")** — GNU make utility to maintain groups of programs.

	[http://www.gnu.org/software/make](http://www.gnu.org/software/make) || [make](https://www.archlinux.org/packages/?name=make)

*   **[GCC](/index.php/GCC "GCC")** — The GNU Compiler Collection - C and C++ frontends.

	[https://gcc.gnu.org/](https://gcc.gnu.org/) || [gcc](https://www.archlinux.org/packages/?name=gcc)

*   **[glibc](https://en.wikipedia.org/wiki/GNU_C_Library "wikipedia:GNU C Library")** — GNU's implementation of the C library.

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
*   [GNU Readline](/index.php/Readline "Readline"), a line-editing library for command-line interfaces

## See also

*   [https://www.gnu.org/](https://www.gnu.org/)
*   [The GNU Manifesto](https://www.gnu.org/gnu/manifesto)
*   [Wikipedia:List of GNU packages](https://en.wikipedia.org/wiki/List_of_GNU_packages "wikipedia:List of GNU packages")
*   The [Arch Hurd Project](https://archhurd.org/) aims to port Arch Linux to the Hurd kernel.