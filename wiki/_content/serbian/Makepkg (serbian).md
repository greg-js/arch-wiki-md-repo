makepkg is used for compiling and building packages suitable for installation with [pacman](/index.php/Pacman "Pacman"), Arch Linux's package manager. makepkg is a script that automates the building of packages; it can download and validate source files, check dependencies, configure build-time settings, compile the sources, install into a temporary root, make customizations, generate meta-info, and package everything together.

makepkg is provided by the [pacman](https://www.archlinux.org/packages/?name=pacman) package.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Architecture, compile flags](#Architecture.2C_compile_flags)
    *   [1.2 Package output](#Package_output)
*   [2 Usage](#Usage)
*   [3 Tips and Tricks](#Tips_and_Tricks)
    *   [3.1 WARNING:Referencing $srcdir in PKGBUILD](#WARNING:Referencing_.24srcdir_in_PKGBUILD)

## Configuration

`/etc/makepkg.conf` is the main configuration file for makepkg. Most users will wish to fine-tune makepkg configuration options prior to building any packages.

### Architecture, compile flags

The MAKEFLAGS, CFLAGS and CXXFLAGS options are used by *make*, *gcc*, and *g++* whilst compiling software with makepkg. By default, these options generate generic packages that can be installed on a wide range of machines. A performance improvement can be achieved by tuning compilation for the host machine. The downside is that packages compiled specifically for the host's processor may not run on others.

 `/etc/makepkg.conf` 
```
...

#########################################################################
# ARCHITECTURE, COMPILE FLAGS
#########################################################################
#
CARCH="x86_64"
CHOST="x86_64-unknown-linux-gnu"

#-- Exclusive: will only run on x86_64
# -march (or -mcpu) builds exclusively for an architecture
# -mtune optimizes for an architecture, but builds for whole processor family
CFLAGS="-march=x86-64 -mtune=generic -O2 -pipe"
CXXFLAGS="-march=x86-64 -mtune=generic -O2 -pipe"
LDFLAGS="-Wl,--hash-style=gnu -Wl,--as-needed"
#-- Make Flags: change this for DistCC/SMP systems
#MAKEFLAGS="-j2"

...

```

The default makepkg.conf CFLAGS and CXXFLAGS are compatible with all machines within their respective architectures.

Further optimizing for CPU type can theoretically enhance performance since `-march=` enables all available instruction sets and improves scheduling for a particular CPU. This is especially noticeable when rebuilding optimized applications (For example: Audio/Video encoding tools.) that take heavy advantage of newer instructions sets not enabled when using the default options (or packages) provided by Arch Linux.

On 64bit, there are rarely measurable real world performance gains for "typical" unoptimized programs (i.e bash) since the bulk of instructions that end up getting generated for those are most likely already used anyway.

As of version 4.3.0, the gcc compiler offers the `-march=native` switch that enables CPU auto-detection and automatically selects optimizations supported by the local machine at gcc runtime. To use it, just modify the default settings by changing the CFLAGS and CXXFLAGS lines as follows:

```
CFLAGS="-march=native -O2 -pipe"
CXXFLAGS="${CFLAGS}"

```

To see the difference between the default options provided (on 64bit) and `-march=native` use something like this:

```
echo | gcc -E -dM -march=x86-64 -mtune=generic - > /tmp/gccflags1
echo | gcc -E -dM -march=native - > /tmp/gccflags2
diff /tmp/gccflags1 /tmp/gccflags2

```

```
diff results on a AMD Barcelona CPU:

```

```
> #define __POPCNT__ 1
48a50
> #define __ABM__ 1
81a84
> #define __amdfam10__ 1
91a95
> #define __3dNOW__ 1
94a99,100
> #define __SSE4A__ 1
> #define __amdfam10 1
97a104
> #define __3dNOW_A__ 1
111d117
< #define __k8 1
143d148
< #define __k8__ 1
178a184
> #define __tune_amdfam10__ 1
194a201
> #define __GCC_HAVE_SYNC_COMPARE_AND_SWAP_16 1
203a211
> #define __SSE3__ 1

```

As you can see, using `-march=native` instead of the defaults enabled SSE3 among quite a few other things.

See the gcc man page for a complete list of available options. The Gentoo [Compilation Optimization Guide](http://www.gentoo.org/doc/en/gcc-optimization.xml) and [Safe Cflags](http://wiki.gentoo.org/wiki/Safe_CFLAGS) wiki article provide more in-depth information.

The MAKEFLAGS option can be used to specify additional options for make. Users with multi-core/multi-processor systems can specify the number of jobs to run simultaneously. Generally `-j2`, plus 1 for each additional core/processor is an adequate choice. Some PKGBUILD's specifically override this with `-j1`, because of race conditions in certain versions or simply because it's not supported in the first place. Packages that fail to build because of this should be reported on the bug tracker after making sure that the error is indeed being caused by your MAKEFLAGS.

```
MAKEFLAGS="-j3"

```

See the make man page for a complete list of available options.

**Note:** Do keep in mind that not all package Makefiles will use your exported variables. Some of them override them in the original Makefiles or the PKGBUILD.

### Package output

Next, one can configure where source files and packages should be placed and identify themselves as the packager. This step is optional; packages will be created in the working directory where makepkg is run by default.

 `/etc/makepkg.conf` 
```
...

#########################################################################
# PACKAGE OUTPUT
#########################################################################
#
# Default: put built package and cached source in build directory
#
#-- Destination: specify a fixed directory where all packages will be placed
#PKGDEST=/home/packages
#-- Source cache: specify a fixed directory where source files will be cached
#SRCDEST=/home/sources
#-- Source packages: specify a fixed directory where all src packages will be placed
#SRCPKGDEST=/home/srcpackages
#-- Packager: name/email of the person or organization building packages
#PACKAGER="John Doe <john@doe.com>"

...

```

For example, create the directory:

```
$ mkdir /home/$USER/packages

```

Then modify the PKGDEST variable in `/etc/makepkg.conf` accordingly.

The PACKAGER variable will set the *packager* value within compiled packages' `.PKGINFO` metadata file. By default, user-compiled packages will display:

 `$ pacman -Qi package` 
```
...
Packager       : Unknown Packager
...

```

Afterwards:

 `$ pacman -Qi package` 
```
...
Packager       : John Doe <john@doe.com>
...

```

This is useful if multiple users will be compiling packages on a system, or you are otherwise distributing your packages to other users.

## Usage

Before continuing, ensure the "base-devel" group is installed. Packages belonging to this group are not required to be listed as dependencies in [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") files. Install the "base-devel" group by issuing (as root):

```
# pacman -S base-devel

```

**Note:** Before complaining about missing (make)dependencies, remember that the "base" group is assumed to be installed on all Arch Linux systems. The group "base-devel" is assumed to be installed when building with makepkg.

To build a package, one must first create a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), or build script, as described in [Creating packages](/index.php/Creating_packages "Creating packages"), or obtain one from the [ABS tree](/index.php/Arch_Build_System "Arch Build System"), [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), or some other source.

**Warning:** Only build/install packages from trusted sources.

Once in possession of a `PKGBUILD`, change to the directory where it is saved and issue the following command to build the package described by said `PKGBUILD`:

```
$ makepkg

```

To have makepkg clean out leftover files and folders, such as files extracted to the $srcdir, add the following option. This is useful for multiple builds of the same package or updating the package version, while using the same build folder. It prevents obsolete and remnant files from carrying over to the new builds.

```
$ makepkg -c

```

If required dependencies are missing, makepkg will issue a warning before failing. To build the package and install needed dependencies automatically, simply use the command:

```
$ makepkg -s

```

Note that these dependencies must be available in the configured repositories; see [pacman#Repositories](/index.php/Pacman#Repositories "Pacman") for details. Alternatively, one can manually install dependencies prior to building (`pacman -S --asdeps dep1 dep2`).

Once all dependencies are satisfied and the package builds successfully, a package file (`pkgname-pkgver.pkg.tar.xz`) will be created in the working directory. To install, run (as root):

```
# pacman -U pkgname-pkgver.pkg.tar.xz

```

Alternatively, to install, using the `-i` flag is an easier way of running `pacman -U pkgname-pkgver.pkg.tar.xz`, as in:

```
$ makepkg -i

```

## Tips and Tricks

### WARNING:Referencing $srcdir in PKGBUILD

Somehow, $srcdir of $pkgdir ended up in one of the installed files in your package.

To identify which files, run the following from the makepkg build dir:

```
grep -R "$(pwd)/src" pkg/

```

[Link](http://www.mail-archive.com/arch-general@archlinux.org/msg15561.html) to discussion thread.