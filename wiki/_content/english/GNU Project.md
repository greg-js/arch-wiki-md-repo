From [http://www.gnu.org/](http://www.gnu.org/):

	The GNU Project was launched in 1984 to develop the GNU operating system, a complete Unix-like operating system which is free software—software which respects your freedom. Unix-like operating systems are built from a software collection of applications, libraries, and developer tools—plus a program to allocate resources and talk to the hardware, known as a kernel. [...] The combination of GNU and Linux is the GNU/Linux operating system, now used by millions and sometimes incorrectly called simply “Linux”. The name “GNU” is a recursive acronym for “GNU's Not Unix!”

The aim of the GNU Project is to produce a totally free operating system. While the GNU kernel has not reached a stable version, the project has resulted in the creation of many tools that power most Unix-like operating systems. [Arch Linux](/index.php/Arch_Linux "Arch Linux") is such a system, using GNU software like the [GRUB](/index.php/GRUB "GRUB") bootloader, [Bash](/index.php/Bash "Bash") shell, and numerous other utilities and libraries.

## Contents

*   [1 The Base System](#The_Base_System)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Software Collection](#Software_Collection)
*   [2 Development Tools](#Development_Tools)
*   [3 Other Tools](#Other_Tools)
*   [4 See also](#See_also)

## The Base System

At the end of the installation process, an Arch system is nothing more than the Linux Kernel, the GNU toolchain, and a few command line tools. The minimal install normally contains the entire [base](https://www.archlinux.org/groups/x86_64/base/) group.

### Kernel

While [Hurd](http://www.gnu.org/s/hurd/hurd.html), the GNU Kernel, is under active development, there is not yet a stable version. For this reason Arch and most other GNU based systems use the Linux Kernel. The [Arch Hurd Project](/index.php/Arch_Hurd_Project "Arch Hurd Project") aims to port Arch Linux to the Hurd kernel.

### Software Collection

*   **[GRUB](/index.php/GRUB "GRUB")** — bootloader

	[http://www.gnu.org/software/grub/](http://www.gnu.org/software/grub/) || [grub](https://www.archlinux.org/packages/?name=grub)

*   **[glibc](https://en.wikipedia.org/wiki/glibc "wikipedia:glibc")** — C library. "defines the 'system calls' and other basic facilities such as open, malloc, printf, exit..."

	[http://www.gnu.org/software/libc/](http://www.gnu.org/software/libc/) || [glibc](https://www.archlinux.org/packages/?name=glibc)

*   **[binutils](https://en.wikipedia.org/wiki/binutils "wikipedia:binutils")** — "a collection of binary tools"

	[https://www.gnu.org/software/binutils/](https://www.gnu.org/software/binutils/) || [binutils](https://www.archlinux.org/packages/?name=binutils)

*   **[bash](/index.php/Bash "Bash")** — "an sh-compatible shell that incorporates useful features from the Korn shell (ksh) and C shell (csh)"

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[coreutils](/index.php/Coreutils "Coreutils")** — "the basic file, shell and text manipulation utilities of the GNU operating system."

	[https://www.gnu.org/software/coreutils/](https://www.gnu.org/software/coreutils/) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

*   **[gzip](https://en.wikipedia.org/wiki/gzip "wikipedia:gzip")** — "popular data compression program"

	[https://www.gnu.org/software/gzip/](https://www.gnu.org/software/gzip/) || [gzip](https://www.archlinux.org/packages/?name=gzip)

*   **[tar](/index.php/Tar "Tar")** — "provides the ability to create tar archives, as well as various other kinds of manipulation"

	[https://www.gnu.org/software/tar/](https://www.gnu.org/software/tar/) || [tar](https://www.archlinux.org/packages/?name=tar)

## Development Tools

Though not necessary, users have the option of installing the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group for some software development tools. This group is a requirement for building packages from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Among **base-devel** are several members of the [GNU toolchain](https://en.wikipedia.org/wiki/GNU_toolchain "wikipedia:GNU toolchain"), a *"suite of tools used in a serial manner [...] for developing applications and operating systems"*. The key components of this toolchain are:

**compilation and build:** [make](https://www.archlinux.org/packages/?name=make)

**compiler collection:** [gcc](https://www.archlinux.org/packages/?name=gcc)

**linker, assembler and other tools:** [binutils](https://www.archlinux.org/packages/?name=binutils)

	[w:gold (linker)](https://en.wikipedia.org/wiki/gold_(linker) "w:gold (linker)"), [w:GNU Binutils](https://en.wikipedia.org/wiki/GNU_Binutils "w:GNU Binutils"), [w:GNU linker](https://en.wikipedia.org/wiki/GNU_linker "w:GNU linker")

**parser generator:** [bison](https://www.archlinux.org/packages/?name=bison)

**macro processor:** [m4](https://www.archlinux.org/packages/?name=m4)

[GNU Build System](https://en.wikipedia.org/wiki/GNU_build_system "wikipedia:GNU build system") (autotools):

	**automatically configure source code:** [autoconf](https://www.archlinux.org/packages/?name=autoconf)

	**automatically create Makefiles:** [automake](https://www.archlinux.org/packages/?name=automake)

	**library support script:** [libtool](https://www.archlinux.org/packages/?name=libtool)

## Other Tools

Many other optional GNU tools are available in the [official repositories](/index.php/Official_repositories "Official repositories"):

**widget toolkit:** [GTK+](/index.php/GTK%2B "GTK+")

**desktop environment:** [GNOME](/index.php/GNOME "GNOME")

**spreadsheet:** [Gnumeric](/index.php/Gnumeric "Gnumeric")

**image editor:** [GIMP](/index.php/GIMP "GIMP")

**full-screen window manager:** [GNU Screen](/index.php/GNU_Screen "GNU Screen")

## See also

For a list of all current GNU projects, see [All GNU Packages](http://www.gnu.org/software/software.html#allgnupkgs).