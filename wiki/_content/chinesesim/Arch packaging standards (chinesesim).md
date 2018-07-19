**翻译状态：** 本文是英文页面 [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-05-17，点击[这里](https://wiki.archlinux.org/index.php?title=Arch+packaging+standards&diff=0&oldid=507402)可以查看翻译后英文页面的改动。

当为Arch Linux构建软件包时,您应该遵循以下的**软件包指导原则**，如果您想贡献你的软件包至Arch Linux时,您应该更加遵循软件包指导原则。同时需要阅读[PKGBUILD](https://archlinux.org/pacman/PKGBUILD.5.html) 和 [makepkg](https://archlinux.org/pacman/makepkg.8.html) 手册。

## Contents

*   [1 PKGBUILD样例](#PKGBUILD.E6.A0.B7.E4.BE.8B)
*   [2 打包规则](#.E6.89.93.E5.8C.85.E8.A7.84.E5.88.99)
*   [3 软件包命名](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E5.91.BD.E5.90.8D)
*   [4 目录](#.E7.9B.AE.E5.BD.95)
*   [5 Makepkg 的任务](#Makepkg_.E7.9A.84.E4.BB.BB.E5.8A.A1)
*   [6 架构](#.E6.9E.B6.E6.9E.84)
*   [7 授权协议](#.E6.8E.88.E6.9D.83.E5.8D.8F.E8.AE.AE)
*   [8 特殊包补充手册](#.E7.89.B9.E6.AE.8A.E5.8C.85.E8.A1.A5.E5.85.85.E6.89.8B.E5.86.8C)

## PKGBUILD样例

```
# Maintainer: Your Name <youremail@domain.com>
pkgname=NAME
pkgver=VERSION
pkgrel=1
pkgdesc=""
arch=()
url=""
license=('GPL')
groups=()
depends=()
makedepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=($pkgname-$pkgver.tar.gz)
noextract=()
md5sums=() #autofill using updpkgsums

build() {
  cd "$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}
```

可以从 pacman 和 abs 的 `/usr/share/pacman` 中找到其它原型。

## 打包规则

*   **永远别**将软件包安装至`/usr/local`
*   **除非没有就不行，否则绝对不要在`PKGBUILD`中自定义和使用新的变量**，以避免和 makepkg 本身的变量**冲突**。
*   即便在非用不可的情况下，我们也强烈建议**给自定义变量名前加上下划线** (`_`)。例如： `_customvariable=` 
*   任何情况下都要**避免**使用`/usr/libexec/`，应该使用`/usr/lib/${pkgname}/`。
*   包信息文件中的`packager`字段可以通过修改`/etc/makepkg.conf`文件由编译者进行自定义。使用 `~/.makepkg.conf`也可以达到此目的。
*   所有安装过程中所需输出的重要的信息，都可以放到**.install 文件中**.比如说如果某软件包需要扩展的安装步骤才能正常运行，你可以将这些步骤的介绍包含在.install文件中。
*   **Dependencies** 是最容易出现错误的地方。请花时间仔细核对，例如对动态可执行文件执行 `ldd`，检查脚本需要的工具，查看软件文档等。[namcap](/index.php/Namcap "Namcap") PKGBUILD 和生成的打包文件，报告权限错误、缺少依赖、过多依赖等常见问题。
*   任何运行该软件包不需要，或者该软件包的通用功能不需要的**可选的依赖**不要加入到depends中，这些信息应该加入**optdepends** 数组，例如：

```
optdepends=('cups: printing support'
            'sane: scanners support'
            'libgphoto2: digital cameras support'
            'alsa-lib: sound support'
            'giflib: GIF images support'
            'libjpeg: JPEG images support'
            'libpng: PNG images support')
```

	例子取自 `extra` 中的 **wine** 软件包。这些信息在安装和升级时会自动打印，所以**不要**将这些信息加入 .install 文件。

*   在填写**软件包描述（description）**时，请不要使用下定义的方式。比如说, "Nedit is a text editor for X11" 就可以简写为"A text editor for X11". 顺便注意保持descriptions在80个字符以内.
*   尽量保持`PKGBUILD`文件中**每行**不超过100字符。
*   如果可能的话, 从`PKGBUILD`文件中**去掉空行**（没有设置变量值的行）(如`provides`、`replaces`等)</li>
*   通常实践建议按照上文中的`PKGBUILD`示例**安排各变量顺序**。当然这不是强制性的，这里唯一强制要求的是满足**正确的bash语法**。
*   变量名可能包含空格时，请使用引号，例如`"$pkgdir"` 和 `"$srcdir"`.
*   请确保软件包的**完整性**，确保 [校验变量](/index.php/PKGBUILD#Integrity "PKGBUILD") 包含正确的数值，可以通过 {ic|updpkgsums}} 工具进行更新。

## 软件包命名

*   软件包应当仅包含**字母或数字**以及`@`, `.`, `_`, `+`, `-`，不能以 `-` 和 `.` 开头，所有的字母应当保持**小写**.
*   软件包的名称不应该包含上游的主版本号，例如如果上游软件包是 libfoo v2.3.4，不应该命名为 libfoo2。这样在上游发布新的大版本时，就可以保留软件包名和依赖可以保持不变。只有个别软件包是例外，例如图形库 GTK 和 Qt。这些软件升级后，应用程序需要花很长时间和经历才能移植完成，所以系统需要同时安装多个版本，软件包名应该包含大版本号，比如 gtk2, gtk3, qt4, qt5\. 如果出现大部分软件包都可以同步升级，只有个别软件没有被 移植的情况，可以把老的软件包命名为 libfoo1，而新的软件包继续使用 libfoo。
*   软件包版本号应当**和作者发行版号保持一致**. 如果需要的话，版本号可以包含字母（比如：nmap的版本就是2.54BETA32）。**版本号里不能包含连字符**，只能允许字母、数字、下划线、点号。
*   Package releases（软件包发行号） **仅和 Arch 相关**. 这样用户就可以区分不同的编译版本。**发布号从1开始**,软件包将会被重新（打包）发布时 ，**发行号将会增加1**。当新版本发布的时候，发行号（release）自动回到1。软件包发布标记和软件包版本标记遵从同样的规则。

## 目录

*   **配置文件** 应该放置到`/etc` 目录.如果有多个配置文件，可以使用**子目录**，以保持 /etc 简洁. 即 /etc/{pkgname}/，{pkgname}代表软件包的名称 (或者其他合适的名称, 比如apache使用的就是 `/etc/httpd/`).

*   软件包文件应该安装在下列 **常用目录**:

| `/etc` | **系统关键**配置文件 |
| `/usr/bin` | 二进制文件 |
| `/usr/lib` | 库 |
| `/usr/include` | 头文件 |
| `/usr/lib/{pkg}` | 模块，插件等 |
| `/usr/share/doc/{pkg}` | 应用程序文档 |
| `/usr/share/info` | GNU Info 系统文件 |
| `/usr/share/man` | 手册 |
| `/usr/share/{pkg}` | 程序数据 |
| `/var/lib/{pkg}` | 应用持久数据 |
| `/etc/{pkg}` | `{pkg}`的配置文件 |
| `/opt/{pkg}` | 大的独立程序，例如 Java |

*   软件包不应该在下面目录添加任何文件:
    *   `/bin`
    *   `/sbin`
    *   `/dev`
    *   `/home`
    *   `/srv`
    *   `/media`
    *   `/mnt`
    *   `/proc`
    *   `/root`
    *   `/selinux`
    *   `/sys`
    *   `/tmp`
    *   `/var/tmp`
    *   `/run`

## [Makepkg](/index.php/Makepkg "Makepkg") 的任务

当您使用makepkg为您自己构建软件包时，makepkg会自动执行如下功能:

*   检查软件包的**依赖**和**构建依赖**是否安装
*   从服务器中下载源码文件
*   校验源码文件的完整性
*   解压源码文件
*   打上必要的 **补丁（patch）**
*   **构建** 软件并以fake root身份安装
*   从可执行文件中**去掉**符号标记
*   从可执行文件中**去掉**调试标记
*   **Compresses** manual and, or info pages
*   生成**包信息文件**（包含软件包的基本信息）
*   **压缩** fake root成为软件包文件（*.pkg.tar.xz）
*   生成的软件包文件**保存**在配置的目的目录中（默认在当前目录）

## 架构

如果该软件包是针对特定架构编译的，那么 *arch* 数组应该包含 *x86_64* ，否则使用 *any* 生成那些架构无关的包。

## 授权协议

请参考 [PKGBUILD (简体中文)#license](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#license "PKGBUILD (简体中文)")

## 特殊包补充手册

请先阅读上面的手册—— 大多数的重点内容都在此页上面部分列出来了，他们将不会在下面这些手册中重复出现。这些特殊的手册是为了作为一些特殊类型的包的补充手册，而不是取代本手册。

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

提交到 AUR 的软件包必须额外满足 [AUR 提交守则](/index.php/Arch_User_Repository#Rules_of_submission "Arch User Repository").