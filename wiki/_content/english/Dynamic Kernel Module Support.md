From [Wikipedia](https://en.wikipedia.org/wiki/Dynamic_Kernel_Module_Support "wikipedia:Dynamic Kernel Module Support"):

	**Dynamic Kernel Module Support** (**DKMS**) is a program/framework that enables generating Linux kernel modules whose sources generally reside outside the kernel source tree. The concept is to have DKMS modules automatically rebuilt when a new kernel is installed.

## Contents

*   [1 Effects](#Effects)
*   [2 Installation](#Installation)
*   [3 Upgrades](#Upgrades)
*   [4 Usage](#Usage)
    *   [4.1 List modules](#List_modules)
    *   [4.2 Rebuild modules](#Rebuild_modules)
    *   [4.3 Remove modules](#Remove_modules)
*   [5 DKMS package creation](#DKMS_package_creation)
    *   [5.1 Package name](#Package_name)
    *   [5.2 Dependencies](#Dependencies)
    *   [5.3 Build source location](#Build_source_location)
    *   [5.4 Patching](#Patching)
    *   [5.5 Module loading automatically in .install](#Module_loading_automatically_in_.install)
    *   [5.6 namcap output](#namcap_output)
    *   [5.7 Example](#Example)
        *   [5.7.1 PKGBUILD](#PKGBUILD)
        *   [5.7.2 dkms.conf](#dkms.conf)
        *   [5.7.3 .install](#.install)
*   [6 See also](#See_also)

## Effects

The *positive effect* of using DKMS is that modules are often able to be rebuilt when the kernel is upgrading. This means that a user does not have to wait for a company, project, or package maintainer to release a new version of the module.

Since the introduction of [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman"), the rebuilt of the modules is handled automatically when a kernel is upgraded. See also [#Upgrades](#Upgrades).

## Installation

[Install](/index.php/Install "Install") the [dkms](https://www.archlinux.org/packages/?name=dkms) package and the headers for your kernel (for the standard kernel this would be [linux-headers](https://www.archlinux.org/packages/?name=linux-headers)).

A good number of modules that lie outside the kernel source tree have a DKMS variant; a few are hosted in the [official repositories](https://www.archlinux.org/packages/?&q=dkms), most are found in the [AUR](https://aur.archlinux.org/packages/?SeB=n&K=dkms). Listed below are a few of the software packages that have a DKMS variant with additional links to dedicated sections where available:

*   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst"): [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/)
*   [NVIDIA](/index.php/NVIDIA "NVIDIA"):
    *   [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms)
    *   [nvidia-304xx-dkms](https://www.archlinux.org/packages/?name=nvidia-304xx-dkms)
    *   [nvidia-173xx-dkms](https://aur.archlinux.org/packages/nvidia-173xx-dkms/)
    *   [nvidia-96xx-dkms](https://aur.archlinux.org/packages/nvidia-96xx-dkms/)
    *   [nvidia-grsec-dkms](https://aur.archlinux.org/packages/nvidia-grsec-dkms/)
*   [VirtualBox](/index.php/VirtualBox "VirtualBox"):
    *   [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms)
    *   [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms)
*   [VMware](/index.php/VMware "VMware"), section [VMware#Using DKMS to manage the modules](/index.php/VMware#Using_DKMS_to_manage_the_modules "VMware")

## Upgrades

Though the rebuilt of the DKMS modules is usually seamless during a kernel upgrade, it may still happen that the rebuilt fails. You should pay extra attention to pacman's output! This applies in particular if the system relies on the DKMS module to boot successfully and/or if you use DKMS with a custom kernel not in the [Official repositories](/index.php/Official_repositories "Official repositories").

To deal with changes in the kernel, fix bugs, or add necessary features consider upgrading the DKMS package before rebooting.

## Usage

Usage for invoking DKMS manually.

Tab-completion is available by doing:

```
# source /usr/share/bash-completion/completions/dkms

```

### List modules

To list the current status of modules, versions and kernels within the tree:

```
# dkms status

```

### Rebuild modules

Rebuild all modules for the currently running kernel:

```
# dkms autoinstall

```

or for a specific kernel:

```
# dkms autoinstall -k 3.16.4-1-ARCH

```

To build a *specific* module for the currently running kernel:

```
# dkms install -m nvidia -v 334.21

```

or simply:

```
# dkms install nvidia/334.21

```

To build a module for *all* kernels:

```
# dkms install nvidia/334.21 --all

```

### Remove modules

To remove a module (old ones are not automatically removed):

```
# dkms remove -m nvidia -v 331.49 --all

```

or simply:

```
# dkms remove nvidia/331.49 --all

```

If the package [dkms](https://www.archlinux.org/packages/?name=dkms) is removed the information regarding previous module build files is lost. If this is the case, go through `/usr/lib/modules/KERNELVERSION-ARCH` and delete or files and directories no longer in use.

## DKMS package creation

Here are some guidelines to follow when creating a DKMS package.

### Package name

DKMS packages are named by appending "*-dkms*" to the original package name.

The variable `$_pkgname` is often used below `$pkgname` to describe the package name minus the "*-dkms*" suffix (e.g. `_pkgname=${pkgname%-*}`). This is useful to help keep similarities between the original package PKGBUILD and the DKMS variant.

### Dependencies

Dependencies should be inherited from the original version with [dkms](https://www.archlinux.org/packages/?name=dkms) added and [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) removed (as it is listed by the dkms package as *optional*).

### Build source location

Build sources should go into (this is the default build directory for DKMS):

```
/usr/src/*PACKAGE_NAME*-*PACKAGE_VERSION*

```

In the package directory, a DKMS configuration tells DKMS how to build the module (`dkms.conf`), including the variables `PACKAGE_NAME` and `PACKAGE_VERSION`.

*   `PACKAGE_NAME` - the actual project name (usually `$_pkgname` or `$_pkgbase`).
*   `PACKAGE_VERSION` - by convention this should also be the `$pkgver`.

### Patching

The sources can be patched either directly in the PKGBUILD or through `dkms.conf`.

### Module loading automatically in .install

Loading and unloading modules should be left to the user. Consider the possibility a module may crash when loaded.

### namcap output

[namcap](/index.php/Namcap "Namcap") (which attempts to check for common mistakes and non-standard decisions in a package) is good practice to use at least once on *any* package; however, it has not yet been updated for DKMS specific guidelines.

For example, DKMS uses `/usr/src/` by default, but Namcap believes this to be a non-standard directory, a little contrary to its [reference](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard "wikipedia:Filesystem Hierarchy Standard").

### Example

Here is an example package that edits `dkms.conf` according to the package name and version.

#### PKGBUILD

 `PKGBUILD` 
```
# Maintainer: foo <foo(at)gmail(dot)com>
# Contributor: bar <bar(at)gmai(dot)com>

_pkgbase=amazing
pkgname=amazing-dkms
pkgver=1
pkgrel=1
pkgdesc="The Amazing kernel modules (DKMS)"
arch=('i686' 'x86_64')
url="[https://www.amazing.com/](https://www.amazing.com/)"
license=('GPL2')
depends=('dkms')
conflicts=("${_pkgbase}")
install=${pkgname}.install
source=("${url}/files/tarball.tar.gz"
        'dkms.conf'
        'linux-3.14.patch')
md5sums=(*use 'updpkgsums'*)

build() {
  cd ${_pkgbase}-${pkgver}

  # Patch
  patch -p1 -i "${srcdir}"/linux-3.14.patch

  # Build
  msg2 "Starting ./configure..."
  ./configure

  msg2 "Starting make..."
  make
}

package() {
  # Install
  msg2 "Starting make install..."
  make DESTDIR="${pkgdir}" install

  # Copy dkms.conf
  install -Dm644 dkms.conf "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf

  # Set name and version
  sed -e "s/@_PKGBASE@/${_pkgbase}/" \
      -e "s/@PKGVER@/${pkgver}/" \
      -i "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf

  # Copy sources (including Makefile)
  cp -r ${_pkgbase}/* "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/
}
```

#### dkms.conf

 `dkms.conf` 
```
PACKAGE_NAME="@_PKGBASE@"
PACKAGE_VERSION="@PKGVER@"
MAKE[0]="make --uname_r=$kernelver"
CLEAN="make clean"
BUILT_MODULE_NAME[0]="@_PKGBASE@"
DEST_MODULE_LOCATION[0]="/kernel/drivers/misc"
AUTOINSTALL="yes"
```

#### .install

Instead of `depmod` now `dkms install` can be used (it depends on `dkms build`, which depends on `dkms add`):

 `amazing-dkms.install` 
```
# old version (without -$pkgrel): ${1%%-*}
# new version (without -$pkgrel): ${2%%-*}

post_install() {
    dkms install *amazing*/${1%%-*}
}

pre_upgrade() {
    pre_remove ${2%%-*}
}

post_upgrade() {
    post_install ${1%%-*}
}

pre_remove() {
    dkms remove *amazing*/${1%%-*} --all
}

```

**Tip:** To keep DKMS packages closer to their non-DKMS counterparts: avoid cluttering up package files with DKMS-specific stuff (e.g. version numbers that need updating).

## See also

*   [Linux Journal: Exploring Dynamic Kernel Module Support](http://www.linuxjournal.com/article/6896)