**翻译状态：** 本文是英文页面 [Dynamic_Kernel_Module_Support](/index.php/Dynamic_Kernel_Module_Support "Dynamic Kernel Module Support") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-11-17，点击[这里](https://wiki.archlinux.org/index.php?title=Dynamic_Kernel_Module_Support&diff=0&oldid=407892)可以查看翻译后英文页面的改动。

来自 [Wikipedia](https://en.wikipedia.org/wiki/Dynamic_Kernel_Module_Support "wikipedia:Dynamic Kernel Module Support"):

	**动态内核模块支持** (**DKMS**) 是一个可以从位于内核源码树之外的内核模块源代码编译生成内核模块的程序框架。它可以使得在升级内核时，通过DKMS管理的内核模块自动重新构建以适应新的内核版本。

## Contents

*   [1 影响](#.E5.BD.B1.E5.93.8D)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 升级](#.E5.8D.87.E7.BA.A7)
*   [4 使用方法](#.E4.BD.BF.E7.94.A8.E6.96.B9.E6.B3.95)
    *   [4.1 列出内核模块](#.E5.88.97.E5.87.BA.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [4.2 重新构建模块](#.E9.87.8D.E6.96.B0.E6.9E.84.E5.BB.BA.E6.A8.A1.E5.9D.97)
    *   [4.3 移除模块](#.E7.A7.BB.E9.99.A4.E6.A8.A1.E5.9D.97)
*   [5 创建DKMS包](#.E5.88.9B.E5.BB.BADKMS.E5.8C.85)
    *   [5.1 包名](#.E5.8C.85.E5.90.8D)
    *   [5.2 依赖](#.E4.BE.9D.E8.B5.96)
    *   [5.3 源代码构建位置](#.E6.BA.90.E4.BB.A3.E7.A0.81.E6.9E.84.E5.BB.BA.E4.BD.8D.E7.BD.AE)
    *   [5.4 打补丁](#.E6.89.93.E8.A1.A5.E4.B8.81)
    *   [5.5 .install 中模块的自动加载](#.install_.E4.B8.AD.E6.A8.A1.E5.9D.97.E7.9A.84.E8.87.AA.E5.8A.A8.E5.8A.A0.E8.BD.BD)
    *   [5.6 namcap 输出](#namcap_.E8.BE.93.E5.87.BA)
    *   [5.7 例子](#.E4.BE.8B.E5.AD.90)
        *   [5.7.1 PKGBUILD](#PKGBUILD)
        *   [5.7.2 dkms.conf](#dkms.conf)
        *   [5.7.3 .install](#.install)
*   [6 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

## 影响

使用DKMS的_积极作用_是通过DKMS管理的内核模块可以在升级内核时被自动重新编译。这意味这你不再需要等待某个公司，项目组或者包维护者释出新版本的内核模块。

_消极作用_是DKMS破坏了Pacman数据库，因为这样一来重新构建后的内核模块不再属于任何一个包，所以Pacman就不能再追逐它们。不过理论上，可以通过添加钩子函数来对此支持(see: [FS#2985](https://bugs.archlinux.org/task/2985))。

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [dkms](https://www.archlinux.org/packages/?name=dkms) 包

要想使DKMS模块可以在内核升级后重启时被自动重新构建，需要先开启`dkms`系统服务。

有许多位于内核源码树之外的内核模块都有DKMS变体;有一些位于[official repositories](https://www.archlinux.org/packages/?&q=dkms)，大多数可以在这儿[AUR](https://aur.archlinux.org/packages/?SeB=n&K=dkms)找到。下面列出的是一小部分有DKMS变体的软件包

*   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst"): [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/)
*   [NVIDIA](/index.php/NVIDIA "NVIDIA"):
    *   [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms)
    *   [nvidia-304xx-dkms](https://www.archlinux.org/packages/?name=nvidia-304xx-dkms)
    *   [nvidia-173xx-dkms](https://aur.archlinux.org/packages/nvidia-173xx-dkms/)
    *   [nvidia-96xx-dkms](https://aur.archlinux.org/packages/nvidia-96xx-dkms/)
*   [VirtualBox](/index.php/VirtualBox "VirtualBox"), section [VirtualBox#Hosts running a custom kernel](/index.php/VirtualBox#Hosts_running_a_custom_kernel "VirtualBox")
*   [VMware](/index.php/VMware "VMware"), section [VMware#Using DKMS to manage the modules](/index.php/VMware#Using_DKMS_to_manage_the_modules "VMware")

## 升级

即使内核模块经常会在某个内核的大更新时被重新构建，不过也有某些特定时候需要对模块进行升级来处理内核变动，修复bug或者添加必要的新特性，这是可以考虑在重启系统之前升级DKMS包。

## 使用方法

如何手动调用DKMS：

可以通过执行以下命令来使能使用DKMS时的Tab补全：

```
# source /usr/share/bash-completion/completions/dkms

```

### 列出内核模块

列出当前模块的状态，版本，包括源码树内的模块：

```
$ dkms status

```

### 重新构建模块

为当前内核重新构建所有的模块：

```
# dkms autoinstall -k

```

或者重新构建某个特定的模块：

```
# dkms autoinstall -k 3.16.4-1-ARCH

```

为当前内核构建一个特定的模块（例如: 对于当前内核）：

```
# dkms install -m nvidia -v 334.21

```

或者简单地：

```
# dkms install nvidia/334.21

```

构建一个可以兼容所有内核版本的模块：

```
# dkms install nvidia/334.21 --all

```

### 移除模块

移除一个内核模块（旧的内核模块并不会被自动移除）：

```
# dkms remove -m nvidia -v 331.49 --all

```

或者简单的：

```
# dkms remove nvidia/331.49 --all

```

如果你卸载了[dkms](https://www.archlinux.org/packages/?name=dkms)包，那么以前构建内核模块使用的相关文件信息就会丢失。如果这样，去`/usr/lib/modules/KERNELVERSION-ARCH`下删除不再需要的文件和目录。

## 创建DKMS包

这儿的一些的指导方针可以在创建一个新的DKMS包时作为参考。

### 包名

DKMS的包的命名方式是：原始包名加"_-dkms_"后缀。

The variable `$_pkgname` is often used below `$pkgname` to describe the package name minus the "_-dkms_" suffix (e.g. `_pkgname=${pkgname%-*}`). This is useful to help keep similarities between the original package PKGBUILD and the DKMS variant.

### 依赖

Dependencies should be inherited from the original version with [dkms](https://www.archlinux.org/packages/?name=dkms) added and [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) removed (as it is listed by the dkms pacakge as _optional_).

### 源代码构建位置

构建模块所需源代码需要放在（这是DKMS构建模块时使用的默认目录）：

```
/usr/src/_PACKAGE_NAME_-_PACKAGE_VERSION_

```

In the package directory, a DKMS configuration tells DKMS how to build the module (`dkms.conf`), including the variables `PACKAGE_NAME` and `PACKAGE_VERSION`.

*   `PACKAGE_NAME` - the actual project name (usually `$_pkgname` or `$_pkgbase`).
*   `PACKAGE_VERSION` - by convention this should also be the `$pkgver`.

### 打补丁

为内核模块源代码打补丁既可以直接在PKGBUILD中进行，也可以通过`dkms.conf`来进行。

### .install 中模块的自动加载

模块的加载和卸载必须由用户自己来执行，设想一下，某个模块可能在加载的时候崩溃。

### namcap 输出

[namcap](/index.php/Namcap "Namcap") （它会试图检查一个包中的一般性错误和不符合标准的设定）在任何包中最好至少使用一次。然而，[namcap](/index.php/Namcap "Namcap")至今仍然没有针对DKMS的特殊方针做更新。

例如，默认情况下,DKMS使用`/usr/src/`，不过Namcap认为这不是一个标准目录，不符合这个[reference](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard "wikipedia:Filesystem Hierarchy Standard")。

### 例子

这儿有个根据包名字和版本来对`dkms.conf`进行编辑的例子。

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
md5sums=(_use 'updpkgsums'_)

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

此时可以使用`dkms install`而不是`depmod`来安装内核模块（`dkms install`依赖`dkms build`，而`dkms build`依赖`dkms add`）：

 `amazing-dkms.install` 

```
# old version (without -$pkgrel): ${1%%-*}
# new version (without -$pkgrel): ${2%%-*}

post_install() {
    dkms install _amazing_/${1%%-*}
}

pre_upgrade() {
    pre_remove ${2%%-*}
}

post_upgrade() {
    post_install ${1%%-*}
}

pre_remove() {
    dkms remove _amazing_/${1%%-*} --all
}

```

**Tip:** To keep DKMS packages closer to their non-DKMS counterparts: avoid cluttering up package files with DKMS-specific stuff (e.g. version numbers that need updating).

## 相关链接

*   [Linux Journal: Exploring Dynamic Kernel Module Support](http://www.linuxjournal.com/article/6896)