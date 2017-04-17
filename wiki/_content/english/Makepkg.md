[makepkg](https://projects.archlinux.org/pacman.git/tree/scripts/makepkg.sh.in) is a script to automate the building of packages. The requirements for using the script are a build-capable Unix platform and a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

*makepkg* is provided by the [pacman](https://www.archlinux.org/packages/?name=pacman) package.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Packager information](#Packager_information)
    *   [1.2 Package output](#Package_output)
    *   [1.3 Signature checking](#Signature_checking)
*   [2 Usage](#Usage)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Creating optimized packages](#Creating_optimized_packages)
        *   [3.1.1 MAKEFLAGS](#MAKEFLAGS)
    *   [3.2 Package hardening](#Package_hardening)
    *   [3.3 Show packages with specific packager](#Show_packages_with_specific_packager)
    *   [3.4 Improving compile times](#Improving_compile_times)
        *   [3.4.1 tmpfs](#tmpfs)
        *   [3.4.2 ccache](#ccache)
    *   [3.5 Generate new checksums](#Generate_new_checksums)
    *   [3.6 Create uncompressed packages](#Create_uncompressed_packages)
    *   [3.7 Utilizing multiple cores on compression](#Utilizing_multiple_cores_on_compression)
    *   [3.8 Build 32-bit packages on a 64-bit system](#Build_32-bit_packages_on_a_64-bit_system)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Makepkg sometimes fails to sign a package without asking for signature passphrase](#Makepkg_sometimes_fails_to_sign_a_package_without_asking_for_signature_passphrase)
    *   [4.2 CFLAGS/CXXFLAGS/CPPFLAGS in makepkg.conf do not work for QMAKE based packages](#CFLAGS.2FCXXFLAGS.2FCPPFLAGS_in_makepkg.conf_do_not_work_for_QMAKE_based_packages)
    *   [4.3 Specifying install directory for QMAKE based packages](#Specifying_install_directory_for_QMAKE_based_packages)
    *   [4.4 WARNING: Package contains reference to $srcdir](#WARNING:_Package_contains_reference_to_.24srcdir)
*   [5 See also](#See_also)

## Configuration

See `man makepkg.conf` for details on configuration options for makepkg.

The system configuration is available in `/etc/makepkg.conf`, but user-specific changes can be made in `$XDG_CONFIG_HOME/pacman/makepkg.conf` or `~/.makepkg.conf`. It is recommended to review the configuration prior to building packages.

### Packager information

Each package is tagged with metadata identifying amongst others also the *packager*. By default, user-compiled packages are marked with `Unknown Packager`. If multiple users will be compiling packages on a system, or you are otherwise distributing your packages to other users, it is convenient to provide real contact. This can be done by setting the `PACKAGER` variable in `makepkg.conf`.

To check this on an installed package:

 `$ pacman -Qi *package*` 
```
[...]
Packager       : John Doe <john@doe.com>
[...]

```

To automatically produce signed packages, also set the `GPGKEY` variable in `makepkg.conf`.

### Package output

By default, *makepkg* creates the package tarballs in the working directory and downloads source data directly to the `src/` directory. Custom paths can be configured, for example to keep all built packages in `~/build/packages/` and all sources in `~/build/sources/`.

Configure the following `makepkg.conf` variables if needed:

*   `PKGDEST` — directory for storing resulting packages
*   `SRCDEST` — directory for storing [source](/index.php/PKGBUILD#source "PKGBUILD") data (symbolic links will be placed to `src/` if it points elsewhere)
*   `SRCPKGDEST` — directory for storing resulting source packages (built with `makepkg -S`)

### Signature checking

**Note:** The signature checking implemented in *makepkg* does not use pacman's keyring, instead relying on the user's keyring.[[1]](http://allanmcrae.com/2015/01/two-pgp-keyrings-for-package-management-in-arch-linux/)

If a signature file in the form of `.sig` or `.asc` is part of the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") source array, *makepkg* automatically attempts to [verify](/index.php/GnuPG#Verify_a_signature "GnuPG") it. In case the user's keyring does not contain the needed public key for signature verification, *makepkg* will abort the installation with a message that the PGP key could not be verified.

If a needed public key for a package is missing, the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") will most likely contain a [validpgpkeys](/index.php/PKGBUILD#validpgpkeys "PKGBUILD") entry with the required key IDs. You can [import](/index.php/GnuPG#Import_a_public_key "GnuPG") it manually, or you can find it [on a keyserver](/index.php/GnuPG#Use_a_keyserver "GnuPG") and import it from there.

## Usage

Before continuing, [install](/index.php/Install "Install") the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group. Packages belonging to this group are **not** required to be listed as build-time dependencies (*makedepends*) in [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") files. In addition, the [base](https://www.archlinux.org/groups/x86_64/base/) group is assumed to be installed on **all** Arch systems.

**Note:**

*   Make sure [sudo](/index.php/Sudo "Sudo") is configured properly for commands passed to [pacman](/index.php/Pacman "Pacman").
*   Running *makepkg* itself as root is [disallowed](https://lists.archlinux.org/pipermail/pacman-dev/2014-March/018911.html).[[2]](https://projects.archlinux.org/pacman.git/tree/NEWS) Besides how a `PKGBUILD` may contain arbitrary commands, building as root is generally considered unsafe.[[3]](https://bbs.archlinux.org/viewtopic.php?id=67561) Users who have no access to a regular user account should run makepkg as the [nobody user](http://allanmcrae.com/2015/01/replacing-makepkg-asroot/).

To build a package, one must first create a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), or build script, as described in [Creating packages](/index.php/Creating_packages "Creating packages"). Existing scripts are available from the [ABS tree](/index.php/Arch_Build_System "Arch Build System") or the [AUR](/index.php/AUR "AUR"). Once in possession of a `PKGBUILD`, change to the directory where it is saved and issue the following command to build the package described by said `PKGBUILD`:

```
$ makepkg

```

If required dependencies are missing, *makepkg* will issue a warning before failing. To build the package and install needed dependencies, add the flag `-s`/`--syncdeps`:

```
$ makepkg -s

```

Adding the `-r`/`--rmdeps` flag causes *makepkg* to remove the make dependencies later, which are no longer needed. If constantly building packages, consider using [Pacman/Tips and tricks#Removing unused packages (orphans)](/index.php/Pacman/Tips_and_tricks#Removing_unused_packages_.28orphans.29 "Pacman/Tips and tricks") once in a while instead.

**Note:**

*   These dependencies must be available in the configured repositories; see [pacman#Repositories and mirrors](/index.php/Pacman#Repositories_and_mirrors "Pacman") for details. Alternatively, one can manually install dependencies prior to building (`pacman -S --asdeps *dep1* *dep2*`).
*   Only global values are used when installing dependencies, i.e any override done in a split package's packaging function will not be used. [[4]](https://patchwork.archlinux.org/patch/2271/)

Once all dependencies are satisfied and the package builds successfully, a package file (`*pkgname*-*pkgver*.pkg.tar.xz`) will be created in the working directory. To install, use `-i`/`--install` (same as `pacman -U *pkgname*-*pkgver*.pkg.tar.xz`):

```
$ makepkg -i

```

To clean up leftover files and folders, such as files extracted to the `$srcdir`, add the option `-c`/`--clean`. This is useful for multiple builds of the same package or updating the package version, while using the same build folder. It prevents obsolete and remnant files from carrying over to the new builds:

```
$ makepkg -c

```

For more, see [makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html).

## Tips and tricks

### Creating optimized packages

A performance improvement of the packaged software can be achieved by enabling compiler optimizations for the host machine. The downside is that packages compiled for a specific processor architecture will not run correctly on other machines. On x86_64 machines, there are rarely significant enough real world performance gains that would warrant investing the time to rebuild official packages.

However, it is very easy to reduce performance by using "nonstandard" compiler flags. Many compiler optimizations are only useful in certain situations and should not be indiscriminately applied to every package. Unless you can verify/benchmark that something is faster, there is a very good chance it is not! The Gentoo [Compilation Optimization Guide](http://www.gentoo.org/doc/en/gcc-optimization.xml) and [Safe CFLAGS](http://wiki.gentoo.org/wiki/Safe_CFLAGS) wiki article provide more in-depth information about compiler optimization.

The options passed to a C/C++ compiler (e.g. [gcc](https://www.archlinux.org/packages/?name=gcc) or [clang](https://www.archlinux.org/packages/?name=clang)) are controlled by the `CFLAGS`, `CXXFLAGS`, and `CPPFLAGS` environment variables. Similarly, the [make](https://www.archlinux.org/packages/?name=make) build system uses `MAKEFLAGS`. For use in the Arch build system, *makepkg* exposes these environment variables as configuration options in `makepkg.conf`. The default values are configured to produce generic packages that can be installed on a wide range of machines.

**Note:** Keep in mind that not all build systems use the variables configured in `makepkg.conf`. For example, *cmake* disregards the preprocessor options environment variable, `CPPFLAGS`. Consequently, many [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") contain workarounds with options specific to the build system used by the packaged software.

GCC can automatically detect and enable safe architecture-specific optimizations. To use this feature, first remove any `-march` and `-mtune` flags, then add `-march=native`. For example,

```
CFLAGS="-march=native -O2 -pipe -fstack-protector-strong"
CXXFLAGS="${CFLAGS}"

```

To see what flags this enables on your machine, run:

```
$ gcc -march=native -v -Q --help=target

```

**Note:**

*   If you specify different value than `-march=native`, then `-Q --help=target` **will not** work as expected.[[5]](https://bbs.archlinux.org/viewtopic.php?pid=1616694#p1616694) You need to go through a compilation phase to find out which options are really enabled. See [Find CPU-specific options](https://wiki.gentoo.org/wiki/Safe_CFLAGS#Find_CPU-specific_options) on Gentoo wiki for instructions.
*   To find out the optimal options for a **32 bit** x86 architecture, you can use the script [gcccpuopt](https://github.com/pixelb/scripts/blob/master/scripts/gcccpuopt).

#### MAKEFLAGS

The `MAKEFLAGS` option can be used to specify additional options for make. Users with multi-core/multi-processor systems can specify the number of jobs to run simultaneously. This can be accomplished with the use of *nproc* to determine the number of available processors, e.g. `MAKEFLAGS="-j$(nproc)"`. Some [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") specifically override this with `-j1`, because of race conditions in certain versions or simply because it is not supported in the first place. Packages that fail to build because of this should be [reported](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") on the bug tracker (or in the case of [AUR](/index.php/AUR "AUR") packages, to the package maintainer) after making sure that the error is indeed being caused by your `MAKEFLAGS`.

See `man make` for a complete list of available options.

### Package hardening

[Install](/index.php/Install "Install") the [hardening-wrapper](https://www.archlinux.org/packages/?name=hardening-wrapper) package. This wraps gcc, g++, etc. such that there are context-dependent hardening flags. These flags can be controlled in `/etc/hardening-wrapper.conf`.

To enable all hardening flags:

 `/etc/hardening-wrapper.conf` 
```
HARDENING_BINDNOW=1
HARDENING_PIE=1
HARDENING_FORTIFY=2
HARDENING_RELRO=1
HARDENING_STACK_CHECK=1
HARDENING_STACK_PROTECTOR=2
```

After installation, you will need to [source](/index.php/Source "Source") your `/etc/profile` or log out and log back in. To verify you are using the wrapper:

```
$ which gcc
/usr/lib/hardening-wrapper/bin/gcc

```

Now simply follow the normal process in creating packages.

To check that the hardened flags have been used, [install](/index.php/Install "Install") the [checksec](https://www.archlinux.org/packages/?name=checksec) package, which can check individual executables or recursively check a directory. For example:

```
$ checksec --dir /tmp/makepkg/dwm/pkg/dwm/usr/bin
RELRO           STACK CANARY      NX            PIE             RPATH      RUNPATH      FORTIFY Checked         Total   Filename
Full RELRO      Canary found      NX enabled    PIE enabled     No RPATH   No RUNPATH   Yes     4               6       /tmp/makepkg/dwm/pkg/dwm/usr/bin/dwm

```

### Show packages with specific packager

This shows all packages installed on the system with the packager named *packagername*:

```
$ expac "%n %p" | grep "*packagername*" | column -t

```

This shows all packages installed on the system with the packager set in the `/etc/makepkg` variable `PACKAGER`. This shows only packages that are in a repository defined in `/etc/pacman.conf`.

```
$ . /etc/makepkg.conf; grep -xvFf <(pacman -Qqm) <(expac "%n\t%p" | grep "$PACKAGER$" | cut -f1)

```

### Improving compile times

#### tmpfs

As compiling requires many I/O operations and handling of small files, moving the working directory to a [tmpfs](/index.php/Tmpfs "Tmpfs") may bring improvements in build times.

The `BUILDDIR` variable can be temporarily exported to *makepkg* to set the build directory to an existing tmpfs. For example:

```
$ BUILDDIR=/tmp/makepkg makepkg

```

**Warning:** Avoid compiling larger packages in tmpfs to prevent running out of memory.

Persistent configuration can be done in `makepkg.conf` by uncommenting the `BUILDDIR` option, which is found at the end of the `BUILD ENVIRONMENT` section in the default `/etc/makepkg.conf` file. Setting its value to e.g. `BUILDDIR=/tmp/makepkg` will make use of the Arch's default `/tmp` [tmpfs](/index.php/Tmpfs "Tmpfs").

**Note:**

*   The [tmpfs](/index.php/Tmpfs "Tmpfs") folder must be mounted without the `noexec` option, else it will prevent build scripts or utilities from being executed.
*   Keep in mind that any package compiled in [tmpfs](/index.php/Tmpfs "Tmpfs") will not persist across reboot. Consider setting the [PKGDEST](#Package_output) option appropriately to move the built package automatically to another (persistent) directory.

#### ccache

The use of [ccache](/index.php/Ccache "Ccache") can improve build times by caching the results of compilations.

### Generate new checksums

Run the following command in the same directory as the PKGBUILD file to generate new checksums:

```
$ updpkgsums

```

### Create uncompressed packages

If you do not mind having larger package files, you can speed up both packaging and installation by having makepkg produce uncompressed packages. Set `PKGEXT='.pkg.tar'` in `/etc/makepkg.conf`.

### Utilizing multiple cores on compression

[xz](https://www.archlinux.org/packages/?name=xz) supports [symmetric multiprocessing (SMP)](https://en.wikipedia.org/wiki/Symmetric_multiprocessing "wikipedia:Symmetric multiprocessing") via the `--threads` flag to speed up compression. For example, to let makepkg use as many CPU cores as possible to compress packages, edit `COMPRESSXZ` array in `/etc/makepkg.conf`:

```
COMPRESSXZ=(xz -c -z - **--threads=0**)

```

### Build 32-bit packages on a 64-bit system

**Warning:** Errors have been reported when using this method to build the [linux](https://www.archlinux.org/packages/?name=linux) package. The [chroot method](/index.php/Install_bundled_32-bit_system_in_64-bit_system "Install bundled 32-bit system in 64-bit system") is preferred and has been verified to work for building the kernel packages.

First, enable the [multilib](/index.php/Multilib "Multilib") repository and [install](/index.php/Install "Install") [multilib-devel](https://www.archlinux.org/groups/x86_64/multilib-devel/). Reply yes when asked about removing the conflicting `gcc` and `gcc-libs` packages; gcc-multilib is capable of building both 64-bit and 32-bit software.

Then create a 32-bit configuration file

 `~/.makepkg.i686.conf` 
```
CARCH="i686"
CHOST="i686-unknown-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector-strong"
CXXFLAGS="${CFLAGS}"
LDFLAGS="-m32 -Wl,-O1,--sort-common,--as-needed,-z,relro"
```

and invoke makepkg as such

```
$ linux32 makepkg --config ~/.makepkg.i686.conf

```

## Troubleshooting

### Makepkg sometimes fails to sign a package without asking for signature passphrase

With [gnupg 2.1](https://www.gnupg.org/faq/whats-new-in-2.1.html), gpg-agent no longer has to be started manually and will be started automatically on the first invokation of gpg. Thus if you do not manually start gpg-agent, makepkg will start it. The problem is that makepkg runs gpg inside a fakeroot, so gpg-agent is also started in that same environment. This leads to bad behavior. A possible solution is to manually start the gpg-agent, either on boot or by command (see [GnuPG#gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG") for ways to do this), before you run makepkg, but this also can be unreliable: [FS#49946](https://bugs.archlinux.org/task/49946).

In the meantime if you do not wish to experiment with your gpg-agent configuration, simply use makepkg *without* signing, and sign the packages afterwards with `gpg --detach-sign *name*.pkg.tar.xz`.

### CFLAGS/CXXFLAGS/CPPFLAGS in makepkg.conf do not work for QMAKE based packages

Qmake automatically sets the variable `CFLAGS` and `CXXFLAGS` according to what it thinks should be the right configuration. In order to let qmake use the variables defined in the makepkg configuration file, you must edit the PKGBUILD and pass the variables [QMAKE_CFLAGS_RELEASE](http://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cflags-release) and [QMAKE_CXXFLAGS_RELEASE](http://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cxxflags-release) to qmake. For example:

 `PKGBUILD` 
```
...

build() {
  cd "$srcdir/$_pkgname-$pkgver-src"
  qmake-qt4 "$srcdir/$_pkgname-$pkgver-src/$_pkgname.pro" \
    PREFIX=/usr \
    QMAKE_CFLAGS_RELEASE="${CFLAGS}"\
    QMAKE_CXXFLAGS_RELEASE="${CXXFLAGS}"

  make
}

...

```

Alternatively, for a system wide configuration, you can create your own `qmake.conf` and set the [QMAKESPEC](http://doc.qt.io/qt-5/qmake-environment-reference.html#qmakespec) environment variable.

### Specifying install directory for QMAKE based packages

The makefile generated by qmake uses the environment variable INSTALL_ROOT to specify where the program should be installed. Thus this package function should work:

 `PKGBUILD` 
```
...

package() {
	cd "$srcdir/${pkgname%-git}"
	make INSTALL_ROOT="$pkgdir" install
}

...

```

Note, that qmake also has to be configured appropriately. For example put this in your .pro file:

 `YourProject.pro` 
```
...

target.path = /usr/local/bin
INSTALLS += target

...

```

### WARNING: Package contains reference to $srcdir

Somehow, the literal strings `$srcdir` or `$pkgdir` ended up in one of the installed files in your package.

To identify which files, run the following from the *makepkg* build directory:

```
$ grep -R "$(pwd)/src" pkg/

```

[Link](http://www.mail-archive.com/arch-general@archlinux.org/msg15561.html) to discussion thread.

## See also

*   [makepkg(8) Manual Page](https://www.archlinux.org/pacman/makepkg.8.html)
*   [makepkg.conf(5) Manual Page](https://www.archlinux.org/pacman/makepkg.conf.5.html)
*   [A Brief Tour of the Makepkg Process](https://gist.github.com/Earnestly/bebad057f40a662b5cc3)
*   [makepkg source code](https://projects.archlinux.org/pacman.git/tree/scripts/makepkg.sh.in)