**翻译状态：** 本文是英文页面 [Dynamic_Kernel_Module_Support](/index.php/Dynamic_Kernel_Module_Support "Dynamic Kernel Module Support") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-07-17，点击[这里](https://wiki.archlinux.org/index.php?title=Dynamic_Kernel_Module_Support&diff=0&oldid=512538)可以查看翻译后英文页面的改动。

来自 [Wikipedia](https://en.wikipedia.org/wiki/Dynamic_Kernel_Module_Support "wikipedia:Dynamic Kernel Module Support"):

	动态内核模块支持(DKMS) 是一个程序框架，可以编译内核代码树之外的模块。升级内核时，通过 DKMS 管理的内核模块可以被自动重新构建以适应新的内核版本。

这意味这你不再需要等待某个公司，项目组或者包维护者释出新版本的内核模块。自从 Pacman 支持 [钩子](/index.php/Pacman#Hooks "Pacman") 之后，内核更新时就会自动生成和安装新的软件包。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 升级](#.E5.8D.87.E7.BA.A7)
*   [3 使用方法](#.E4.BD.BF.E7.94.A8.E6.96.B9.E6.B3.95)
    *   [3.1 列出内核模块](#.E5.88.97.E5.87.BA.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [3.2 重新构建模块](#.E9.87.8D.E6.96.B0.E6.9E.84.E5.BB.BA.E6.A8.A1.E5.9D.97)
    *   [3.3 移除模块](#.E7.A7.BB.E9.99.A4.E6.A8.A1.E5.9D.97)
*   [4 创建DKMS包](#.E5.88.9B.E5.BB.BADKMS.E5.8C.85)
    *   [4.1 包名](#.E5.8C.85.E5.90.8D)
    *   [4.2 依赖](#.E4.BE.9D.E8.B5.96)
    *   [4.3 源代码构建位置](#.E6.BA.90.E4.BB.A3.E7.A0.81.E6.9E.84.E5.BB.BA.E4.BD.8D.E7.BD.AE)
    *   [4.4 打补丁](#.E6.89.93.E8.A1.A5.E4.B8.81)
    *   [4.5 .install 中模块的自动加载](#.install_.E4.B8.AD.E6.A8.A1.E5.9D.97.E7.9A.84.E8.87.AA.E5.8A.A8.E5.8A.A0.E8.BD.BD)
    *   [4.6 namcap 输出](#namcap_.E8.BE.93.E5.87.BA)
    *   [4.7 例子](#.E4.BE.8B.E5.AD.90)
        *   [4.7.1 PKGBUILD](#PKGBUILD)
        *   [4.7.2 dkms.conf](#dkms.conf)
        *   [4.7.3 .install](#.install)
*   [5 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [dkms](https://www.archlinux.org/packages/?name=dkms) 包和内核的头文件，标准内核的头文件可以用软件包 [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) 安装。

有许多位于内核源码树之外的内核模块都有DKMS变体;有一些位于[官方软件仓库](https://www.archlinux.org/packages/?&q=dkms)，大多数可以在[AUR](https://aur.archlinux.org/packages/?SeB=n&K=dkms)找到。

## 升级

**Note:** [Pacman](/index.php/Pacman "Pacman") 在重新编译 DKMS 模块时不会自动重新编译依赖，所以如果出现 dkms 模块之间的依赖，有可能出现编译错误，例如 [zfs-dkms](https://aur.archlinux.org/packages/zfs-dkms/) [FS#52901](https://bugs.archlinux.org/task/52901). [dkms-sorted](https://aur.archlinux.org/packages/dkms-sorted/) 软件包试图解决这个问题，此软件包可以直接替换 `dkms`，为了处理方便，请在安装任何 DKMS 模块前安装此软件包。

虽然在内核升级是，DKMS 的编译自动执行，但是依然有可能编译报错。所以需要特别注意 pacman 的输出。当系统需要这些模块才能启动，或者使用不在 [官方软件仓库](/index.php/Official_repositories "Official repositories") 中的内核时，需要额外注意。

## 使用方法

如何手动调用DKMS：

可以通过执行以下命令来使能使用DKMS时的Tab补全：

```
# source /usr/share/bash-completion/completions/dkms

```

### 列出内核模块

列出当前模块的状态，版本，包括源码树内的模块：

```
# dkms status

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

创建一个新的DKMS包时，可以参考下面的指导方针。

### 包名

DKMS的包的命名方式是：原始包名加"*-dkms*"后缀。

通常在 `$pkgname` 后面使用 `$_pkgname` 记录不包含 "*-dkms*" 后缀的软件包名 (例如 `_pkgname=${pkgname%-*}`). 这样可以在原始的软件包 PKGBUILD 和 DKMS 编译文件之间保持相似性。

### 依赖

依赖的包应该是原来软件包的基础上，加上 [dkms](https://www.archlinux.org/packages/?name=dkms)， 删除 [linux-headers](https://www.archlinux.org/packages/?name=linux-headers)，内核头文件已经是 dkms 的可选依赖。

### 源代码构建位置

构建模块所需源代码需要放在（这是DKMS构建模块时使用的默认目录）：

```
/usr/src/*PACKAGE_NAME*-*PACKAGE_VERSION*

```

在软件包目录，要包含一个 `dkms.conf` 配置文件，告诉 DKMS 如何编译。这个配置文件需要包含：

*   `PACKAGE_NAME` - 实际的项目名称，通常使用 `$_pkgname` 或 `$_pkgbase`.
*   `PACKAGE_VERSION` - 通常使用 `$pkgver`.

### 打补丁

为内核模块源代码打补丁既可以直接在PKGBUILD中进行，也可以通过`dkms.conf`来进行。

### .install 中模块的自动加载

模块的加载和卸载必须由用户自己来执行，设想一下，某个模块可能在加载的时候崩溃。

现在已经不需要单独执行 `depmod` 更新内核模块的依赖。Pacman 现在会自动执行 `dkms install` 和 `dkms remove` 钩子。`dkms install` 会确保过程结束时执行 `depmod`。`dkms install` 依赖 `dkms build` (针对当前内核编译源码)，build 依赖 `dkms add` (添加从 `/var/lib/dkms/<package>/<version>/source` 到 `/usr/src/<package>` 的链接)。

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
md5sums=(*use 'updpkgsums'*)

build() {
  cd ${_pkgbase}-${pkgver}

  # Patch
  patch -p1 -i "${srcdir}"/linux-3.14.patch
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

pacman 已经支持 DKMS 钩子，不需要在 .install 文件中指定 DKMS 额外配置，pacman 会自动执行 `dkms install` 和 `dkms remove`。

## 相关链接

*   [Linux Journal: 探寻动态内核模块支持](http://www.linuxjournal.com/article/6896)