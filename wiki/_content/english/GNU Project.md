From [http://www.gnu.org/](http://www.gnu.org/)

	_The GNU Project was launched in 1984 to develop the GNU operating system, a complete Unix-like operating system which is free software—software which respects your freedom._

	_Unix-like operating systems are built from a software collection of applications, libraries, and developer tools—plus a program to allocate resources and talk to the hardware, known as a kernel. [...]_

	_The combination of GNU and Linux is the GNU/Linux operating system, now used by millions and sometimes incorrectly called simply “Linux”._

	_The name “GNU” is a recursive acronym for “GNU's Not Unix!”_

The aim of the GNU Project is to produce a totally free operating system. While the GNU kernel has not reached a stable version, the project has resulted in the creation of many tools that power most Unix-like operating systems. [Arch Linux](/index.php/Arch_Linux "Arch Linux") is such a system, using GNU software like the [GRUB](/index.php/GRUB "GRUB") bootloader, [Bash](/index.php/Bash "Bash") shell, and numerous other utilities and libraries.

## Contents

*   [1 The Base System](#The_Base_System)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Software Collection](#Software_Collection)
*   [2 Development Tools](#Development_Tools)
*   [3 Other Tools](#Other_Tools)
*   [4 Links](#Links)

## The Base System

At the end of the installation process, an Arch system is nothing more than the Linux Kernel, the GNU toolchain, and a few command line tools. The minimal install normally contains the entire [base](https://www.archlinux.org/groups/x86_64/base/) group.

### Kernel

While [Hurd](http://www.gnu.org/s/hurd/hurd.html), the GNU Kernel, is under active development, there is not yet a stable version. For this reason Arch and most other GNU based systems use the Linux Kernel. The [Arch Hurd Project](/index.php/Arch_Hurd_Project "Arch Hurd Project") aims to port Arch Linux to the Hurd kernel.

### Software Collection

**bootloader:** [GRUB](/index.php/GRUB "GRUB") is the standard bootloader for Arch Linux, which is now maintained by [GNU](http://www.gnu.org/software/grub/).

**C library:** [glibc](https://www.archlinux.org/packages/?name=glibc) is _"the library which defines the `system calls' and other basic facilities such as open, malloc, printf, exit..."_[[1]](http://www.gnu.org/software/libc/)

**binary utilities:** [binutils](https://www.archlinux.org/packages/?name=binutils) provides the _"collection of programming tools for the manipulation of object code in various object file formats"_[[2]](http://en.wikipedia.org/wiki/GNU_Binutils).

**shell:** [Bash](/index.php/Bash "Bash"), another GNU based application[[3]](http://www.gnu.org/software/bash/), is the default shell.

**core utilities:** The [coreutils](https://www.archlinux.org/packages/?name=coreutils) package contains _"the basic file, shell and text manipulation utilities"_[[4]](http://www.gnu.org/software/coreutils/).

**compression:** [gzip](https://www.archlinux.org/packages/?name=gzip) and [Tar](/index.php/Tar "Tar") handle many packages for GNU/Linux systems. For example, those from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") come as [Gzipped](http://www.gnu.org/software/gzip/) [tarballs](http://www.gnu.org/software/tar/).

## Development Tools

Though not necessary, users have the option of installing the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group for some software development tools. This group is a requirement for building packages from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Among **base-devel** are several members of the [GNU toolchain](https://en.wikipedia.org/wiki/GNU_toolchain "wikipedia:GNU toolchain"), a _"suite of tools used in a serial manner [...] for developing applications and operating systems"_. The key components of this toolchain are:

**compilation and build:** [make](https://www.archlinux.org/packages/?name=make)

**compiler collection:** [gcc](https://www.archlinux.org/packages/?name=gcc)

**linker, assembler and other tools:** [binutils](https://www.archlinux.org/packages/?name=binutils)

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

**image editor:** [GIMP](/index.php/Multimedia#GIMP "Multimedia")

**full-screen window manager:** [GNU Screen](/index.php/GNU_Screen "GNU Screen")

## Links

For a list of all current GNU projects, see [All GNU Packages](http://www.gnu.org/software/software.html#allgnupkgs)