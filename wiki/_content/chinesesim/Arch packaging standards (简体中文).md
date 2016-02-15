**任何提交的 PKGBUILD 都不能编译已经位于官方二进制软件包仓库的程序，除非和官方打包版本相比增加或开启了新的功能。这时 pkgname 列应该不同。**

当为Arch Linux构建软件包时,您应该遵循以下的**软件包指导原则**，如果您想贡献你的软件包至Arch Linux时,您应该更加遵循软件包指导原则。同时需要阅读[PKGBUILD](https://archlinux.org/pacman/PKGBUILD.5.html) 和 [makepkg](https://archlinux.org/pacman/makepkg.8.html) 手册。

## Contents

*   [1 PKGBUILD样例](#PKGBUILD.E6.A0.B7.E4.BE.8B)
    *   [1.1 打包规则](#.E6.89.93.E5.8C.85.E8.A7.84.E5.88.99)
*   [2 软件包命名](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E5.91.BD.E5.90.8D)
*   [3 目录](#.E7.9B.AE.E5.BD.95)
*   [4 Makepkg 的任务](#Makepkg_.E7.9A.84.E4.BB.BB.E5.8A.A1)
    *   [4.1 架构](#.E6.9E.B6.E6.9E.84)
        *   [4.1.1 软件包授权](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E6.8E.88.E6.9D.83)
        *   [4.1.2 提交软件包至AUR](#.E6.8F.90.E4.BA.A4.E8.BD.AF.E4.BB.B6.E5.8C.85.E8.87.B3AUR)
*   [5 特殊包补充手册](#.E7.89.B9.E6.AE.8A.E5.8C.85.E8.A1.A5.E5.85.85.E6.89.8B.E5.86.8C)

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
md5sums=() #generate with 'makepkg -g'

build() {
  cd "$srcdir/$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}
```

可以从 pacman 和 abs 的 `/usr/share/pacman` 中找到其它原型。

### 打包规则

*   **永远别**将软件包安装至`/usr/local`
*   **除非没有就不行，否则绝对不要在`PKGBUILD`中自定义和使用新的变量**，以避免和makepkg本身的变量**冲突**。即便在非用不可的情况下，我们也强烈建议**给自定义变量名前加上下划线** (`_`)。例如： `_customvariable=` 

    AUR无法检测自定义变量的使用，所以无法自动替换自定义变量值。通常这种错误发生在source 变量数组上，比如说：

     `http://downloads.sourceforge.net/directxwine/$patchname.$patchver.diff.bz2` 

    这种情况下AUR是无法正确找到下载位置的。

*   任何情况下都要**避免**使用`/usr/libexec/`，而用`/usr/lib/${pkgname}/`取代。
*   在包信息文件中的`packager`字段可以通过修改`/etc/makepkg.conf`文件由编译者自定义编译选项。使用 `~/.makepkg.conf`也可以达到此目的。
*   所有安装过程中所需输出的重要的信息，都可以放到**.install 文件中**.比如说如果某软件包需要扩展的安装步骤才能正常运行，你可以将这些步骤的介绍包含在.install文件中。
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

*   在填写**软件包描述（description）**时，请不要使用下定义的方式。比如说, "Nedit is a text editor for X11" 就可以简写为"A text editor for X11". 顺便注意保持descriptions在80个字以内.
*   尽量保持`PKGBUILD`文件中**每行**不超过100字符。
*   如果可能的话, 从`PKGBUILD`文件中**去掉空行**（没有设置变量值的行）(如`provides`、`replaces`等)
*   通常实践建议按照上文中的`PKGBUILD`示例**安排各变量顺序**。当然这不是强制性的，这里唯一强制要求的是满足**正确的bash语法**。

## 软件包命名

*   软件包应当仅包含**字母或数字**;所有的字母应当保持**小写**.
*   软件包版本号应当**和作者发行版号保持一致**. 如果需要的话，版本号可以包含字母（比如：nmap的版本就是2.54BETA32）。 **版本号里不能包含连字符**，只能允许字母、数字、下划线、点号。
*   Package releases（软件包发行号） 仅用于**特指Arch的软件包**. 这就允许在新版包发布的时候，用户选择新旧不同的版本来编译., **发布号从1开始**. 然后由于软件包可能被修补， 软件包将会被 **重（打包）发布** ，然后**发行号将会增加**。 当新版本发布的时候，发行号（release）自动回到1。 软件包发布标记和**软件包版本标记遵从同样的规则**.

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

## [Makepkg](/index.php/Makepkg "Makepkg") 的任务

当您使用makepkg为您自己构建软件包时，makepkg会自动执行如下功能：

1.  检查软件包的**依赖**和**构建依赖**是否安装
2.  从服务器中**下载源码**文件
3.  校验源码文件的**完整性**
4.  **解压** 源码文件
5.  打上必要的 **补丁（patch）**
6.  **构建** 软件并以fake root身份安装
7.  从可执行文件中**去掉**符号标记
8.  从可执行文件中**去掉**调试标记
9.  从软件包中**去掉** `/usr/doc`, `/usr/info`, `/usr/share/doc`, and `/usr/share/info`目录
10.  生成**包信息文件**（包含软件包的基本信息）
11.  **压缩** fake root成为软件包文件（*.pkg.tar.xz）
12.  将生成的软件包文件**保存**在配置的目的目录中（默认在当前目录）

### 架构

_arch_ 数组应该包含 _i686_ 和/或 _x86_64_ ，取决于软件可以构建的目标架构。也可以使用 _any_ 生成那些架构无关的包。

#### 软件包授权

license数组用于官方仓库中说明软件包的使用授权协议。当然你所制作的包里也可以用。 用法如下：

*   我们已经在core仓库创建了一个licenses包，以存储常用的授权协议文件。他们被安装在/usr/share/licenses/common 比如 /usr/share/licenses/common/GPL。如果软件包的授权符合GPL授权协议，此时license变量就可以直接设置成该目录的名称，即：license=('GPL')
*   如果licenses包不包含你的软件包的授权文件,你必须执行以下几步：
    1.  先将授权协议文件放到 /usr/share/licenses/$pkgname/ 下，比如 /usr/share/licenses/dibfoo/COPYING.
    2.  如果源代码不包含授权文件，授权协议文件只在其网站上公布。那么就要先把他复制下来，然后像上面那样放置到指定位置（别忘了给个合适的文件名）。
    3.  将licenses变量设置为 'custom' 。当然你也可以设置为 'custom:"授权类型"'.
*   一旦某个授权协议在官方仓库（包括[community]仓库）中使用了多次，那该协议应该就很普遍了
*   MIT、BSD、zlib/libpng和Python的授权协议比较特殊。准确说他们不是'通常'所说的授权协议。。由于这几种协议自身规定的可变性，他们这些协议下的每一个软件都可以有他们自己的版权协议。对此我们仍然使用license=MIT之类的写法来定义，同时将软件包自己独立的授权协议放置到/usr/share/licenses/$pkgname/。

*   有些包可能在多个授权协议下发布。这种情况下，可以在license变量数组里包含多个说明。比如说： license=("GPL" "custom:一些商业协议")。 对大多数软件包而言，这些授权协议所适用的情况有多种，同种情况下协议间相互抵制. 当pacman分辨这些软件包时，会将双（多）重协议理解成满足其一即可，而且通常情况下会选择GPL或BSD协议，而忽略其他已经列出来的的授权.
*   (L)GPL拥有很多不一样的版本，对于(L)GPL软件，license中的值对应的关系如下：
    *   (L)GPL - (L)GPLv2 或其后的版本
    *   (L)GPL2 - 仅(L)GPL2
    *   (L)GPL3 - (L)GPL3 或其后的版本

#### 提交软件包至AUR

在提交任何软件包到AUR前，请注意以下内容：

1.  任何情况下，**一定不要**提交用于编译官方二进制仓库已有软件包的PKGBUILDs ，如果所提交的软件包拥有启用了的扩展特性以及（或者）针对官方包的补丁则例外。如果是这样，应该在pkgname中简单明了表明不同点。比如说：提交一个包含sidebar补丁的screen的PKGBUILD,应该命名为screen-sidebar（或者别的）。 并且在PKGBUILDd **provides**数组变量中加上('screen')，以表示本软件包和官方的screen冲突。
2.  为了保证已提交给AUR包的安全，请**记住**正确填写`md5sum`字段. `md5sum`可以用`makepkg -g`命令生成.
3.  请在`PKGBUILD`文件顶部按照下列格式**添加一行注释**，注意修饰一下你的 email 地址避免被 spam 骚扰： `# Contributor: Your Name <your.email>` 
4.  核实软件包的**依赖关系** (例如运行`ldd`以检测软件包调用的动态链接库). TU团队**强烈**建议使用[Jason Chu](https://www.archlinux.org/fellows/#jason)所写的`namcap`工具集，来分析你的软件包. `namcap`将会告诉你错误的权限、缺失/多余的依赖和其他常规错误。你可以使用`pacman`安装`namcap`。 记住`namcap`可以既可以用来检测 pkg.tar.gz 文件，也可以用于PKGBUILDs。
5.  **依赖**问题是最常见的打包错误。 Namcap可以协助检测他们,但不一定全对。最好的方法还是查看源代码里面的文档以及程序的发布网站
6.  在你的PKGBUILD中**不要使用<tt>replaces</tt>**，除非你希望重命名你的软件包（比如_Ethereal_ 更名为_Wireshark_）。 如果你仅仅是提供一个已有版本的更迭版， 使用<tt>conflicts</tt> (如果该软件包还被其他包依赖的话还有<tt>provides</tt> )。 主要的不同是：在同步(-Sy)数据库后,pacman如果遇到含有replace字段的软件包，就会立刻取代已安装的符合replase变量值的软件包，不管他是哪个仓库的； 另一方面，<tt>conflicts</tt>仅仅在你真正安装的时候才会去取代相应的包，这种行为通常是用户所期望的因为它具有更少的侵入性。
7.  所有上传到AUR的文件应该打包到 **压缩的tar包文件**中，里面是一个目录，包含着**`PKGBUILD`**文件的目录和其他**编译所需的添加文件** (补丁,安装文件等)。例如：

    ```
    foo/PKGBUILD
    foo/foo.install
    foo/foo_bar.diff
    foo/foo.rc.conf
    ```

    压缩包的文件名应该包含软件包的名称，例如：foo.tar.gz

    压缩包**不应该**包含由makepkg创建的二进制包,也不应该包含到文件列表中

## 特殊包补充手册

请先阅读上面的手册—— 大多数的重点内容都在此页上面部分列出来了，他们将不会在下面这些手册中重复出现。这些特殊的手册是为了作为一些特殊类型的包的补充手册，而不是取代本手册。

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")