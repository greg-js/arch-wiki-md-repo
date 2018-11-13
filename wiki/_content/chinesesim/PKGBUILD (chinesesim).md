相关文章

*   [Arch packaging standards (简体中文)](/index.php/Arch_packaging_standards_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch packaging standards (简体中文)")
*   [Arch Build System (简体中文)](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")
*   [Creating packages (简体中文)](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)")
*   [.SRCINFO](/index.php/.SRCINFO ".SRCINFO")
*   [Category:Package development](/index.php/Category:Package_development "Category:Package development")
*   [Pacman tips (简体中文)](/index.php/Pacman_tips_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman tips (简体中文)")
*   [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")
*   [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")
*   [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")
*   [Pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks")

**翻译状态：** 本文是英文页面 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-16，点击[这里](https://wiki.archlinux.org/index.php?title=PKGBUILD&diff=0&oldid=495729)可以查看翻译后英文页面的改动。

**PKGBUILD**是一个shell脚本，包含 [Arch Linux](/index.php/Arch_Linux "Arch Linux") 在构建软件包时需要的信息。本页面讨论PKGUILD中使用的变量。若要获取PKGBUILD中函数的信息，请参考[创建软件包](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)") 和 [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5).

Arch Linux 用 [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") 创建软件包。当 **makepkg** 运行时，它会在当前目录寻找 `PKGBUILD` 文件，并依照其中的指令去获取依赖文件，编译出 `pkgname.pkg.tar.xz` 文件。生成的包内有二进制文件和安装指令，可以使用 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 进行安装。

`pkgname`，`pkgver`，`pkgrel`和`arch`是必须包含的变量。`license`在构建包时并不强制要求，但若要分享 PKGBUILD文件，推荐加上该变量，否则 `makepkg` 会有警告。

一般来说，这些变量按下面的顺序出现在 PKGBUILD 文件中，但这并不是强制性的，只要使用正确的 [Bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)") 语法就行了。

## Contents

*   [1 软件包名称](#软件包名称)
    *   [1.1 pkgbase](#pkgbase)
    *   [1.2 pkgname](#pkgname)
*   [2 版本](#版本)
    *   [2.1 pkgver](#pkgver)
    *   [2.2 pkgrel](#pkgrel)
    *   [2.3 epoch](#epoch)
*   [3 一般变量](#一般变量)
    *   [3.1 pkgdesc](#pkgdesc)
    *   [3.2 arch](#arch)
    *   [3.3 url](#url)
    *   [3.4 license](#license)
    *   [3.5 groups](#groups)
*   [4 依赖关系](#依赖关系)
    *   [4.1 depends](#depends)
    *   [4.2 optdepends](#optdepends)
    *   [4.3 makedepends](#makedepends)
    *   [4.4 checkdepends](#checkdepends)
*   [5 软件相关性](#软件相关性)
    *   [5.1 provides](#provides)
    *   [5.2 conflicts](#conflicts)
    *   [5.3 replaces](#replaces)
*   [6 其它](#其它)
    *   [6.1 backup](#backup)
    *   [6.2 options](#options)
    *   [6.3 install](#install)
    *   [6.4 changelog](#changelog)
*   [7 源码](#源码)
    *   [7.1 source](#source)
    *   [7.2 noextract](#noextract)
    *   [7.3 validpgpkeys](#validpgpkeys)
*   [8 完整性](#完整性)
    *   [8.1 md5sums](#md5sums)
    *   [8.2 sha1sums](#sha1sums)
    *   [8.3 sha256sums](#sha256sums)
    *   [8.4 sha224sums, sha384sums, sha512sums](#sha224sums,_sha384sums,_sha512sums)
*   [9 参阅](#参阅)

## 软件包名称

### pkgbase

构建拆分包时，可以使用一个可选的全局参考值。pkgbase可以在 makepkg 输出和纯源代码包中指定软件包组。若该变量未被设置，则用pkgname数组的第一个元素充当。此变量不允许以下划线开头。拆分软件包中的所有变量都默认使用全局 PKGBUILD 设置的值。除了`makedepends,source variables, integrity variables`, 其他变量都可以在拆分包的 `package()` 函数中进行额外设置。

### pkgname

软件包的名称，名称由小写字母、数字和任意以下字符组成：`@ . _ + -` (at 符号, 点, 下划线, 加号, 连字符)。字母均为小写且不能以连字符开头。为了保证一致性，`pkgname` 应该匹配源文件 tar 包的名称，比如：源文件包名为 `foobar-2.5.tar.gz`，那么 `pkgname` 应该使用 `pkgname=foobar`。除此之处，`PKGBUILD` 文件所在工作目录也应该与 `pkgname` 想匹配。

拆分包中应该使用数组：`pkgname=('foo' 'bar')`.

## 版本

### pkgver

软件包的版本号，应该与软件原作者发布的版本号一致。它由字母、数字和'.'组成，但*不能*包含连字符'-'，如果原作者在他的版本号中使用了连字符'-'，那么用下划线'_'来替代。举个例子：原版本号“0.99-10”，改写成“0.99_10”。在之后的 PKGBUILD 指令中 `pkgver` 中的下划线可以用下面这个方法替代为连接符：

```
source=("$pkgname-${pkgver//_/-}.tar.gz")

```

**注意:** 如果上游使用时间戳格式的版本，例如 *05102014*，请修改为年份在前的格式 *20141005* (ISO 8601). 否则新版本判断会失效。

**Tip:**

*   非常用变量的顺序可以通过 [pacman](/index.php/Pacman "Pacman") 软件包提供的 [vercmp(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vercmp.8) 进行测试.
*   在 PKGBUILD 中定义`pkgver()`，[makepkg](/index.php/Makepkg "Makepkg") 就可以自动 [更新](http://allanmcrae.com/2013/04/pacman-4-1-released/) 此变量。详情参阅 [VCS package guidelines](/index.php/VCS_package_guidelines "VCS package guidelines").

### pkgrel

发布号，一个正整数，用来区分同一版本软件的多次构建。当软件包随着 `PKGBUILD` 的调整与优化变化时，**释出号**递增 1。而当这个软件包发布一个新版本时，释出号重置为 1。个别软件会使用 *major.minor* 的发布号。

### epoch

**注意:** 若非必要，不要使用此变量

当一个软件的版本编号方式改变，打破正常的版本比较逻辑时, 使用此数值进行强制升级。只要此数值比安装的版本大，就会视作新版本进行升级。

示例：

```
pkgver=5.13
pkgrel=2
epoch=1
```
 `1:5.13-2` 

更多信息参见[pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)。

## 一般变量

### pkgdesc

软件包描述，建议最多80个字符，不要重复软件的名字，除非软件包名和程序名不相同。合理使用关键字以方便搜索。

比如："Nedit is a text editor for X11"应该写成"A text editor for X11"。

### arch

一个架构数组，表示 PKGBUILD 可以编译和使用的架构。Arch 官方仅支持 `x86_64`, 但是其它项目提供了其它架构支持，[Arch Linux 32](https://archlinux32.org/) 提供了 `i686` 支持，[Arch Linux ARM](http://archlinuxarm.org/) 项目提供 `arm` - armv5, `armv6h` - armv6 hardfloat, `armv7h` - armv7 hardfloat, `aarch64` - armv8 64bit 支持。

如果软件包编译后和架构无关(shell脚本、字体、主题、各种扩展等)，请使用 `arch=('any')`. 请注意这个值意味着软件仅需编译一次，然后可以在所有架构上使用。软件包会以 `-any` 为后缀，而不是 `-x86_64` 等.

如果软件包可以在任何架构上编译，但是编译后只能在一个架构中运行，请列出所有支持的架构例如 `arch=('x86_64')`.

### url

软件官方站点的网址

### license

软件发布许可证。软件包仓库 `[core]` 中的 [licenses](https://www.archlinux.org/packages/?name=licenses) 包存放了通用的许可证协议，安装后能在 `/usr/share/licenses/common` 中找到这些许可证协议，比如 `/usr/share/licenses/common/GPL`。如果软件包是发布在这些许可证中的任何一个，这个值应该被设定成许可证的目录名，比如：`license=('GPL')`。如果软件包中没有适用的许可证，可以按下的方法执行：

1.  许可证安装到： `/usr/share/licenses/**pkgname**/` 目录下，例如使用下面命令： `install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE` 
2.  如果许可证的内容仅保存在网站上，那么你需要单独保存一个版本。
3.  把 `custom` 添加到 `license` 列表。或者你可以用 `custom:name of license` 替代 `custom`。一旦某个许可证被官方仓库用于两个以上软件包（包括 `[community]`），它将成为 [licenses](https://www.archlinux.org/packages/?name=licenses) 的一个组成部分。

*   [BSD](https://en.wikipedia.org/wiki/BSD_License "wikipedia:BSD License")、[MIT](https://en.wikipedia.org/wiki/MIT_License "wikipedia:MIT License")、[zlib/png](https://en.wikipedia.org/wiki/ZLIB_license "wikipedia:ZLIB license") 和 [Python](https://en.wikipedia.org/wiki/Python_License "wikipedia:Python License") 是几个例外的情况，它们不能加入 [licenses](https://www.archlinux.org/packages/?name=licenses) 包。在 `license` 列表中还是把它们当成通用协议来对待(`license=('BSD')`, `license=('MIT')`, `license=('ZLIB')` and `license=('Python')`)，但是实际上它们都是私有协议，因为它们都包括了各自的版权条款。任何发布于这四个许可协议的软件包都应该在 `/usr/share/licenses/**pkgname**` 存放它们独有的许可证文件。一些软件包可能不止一个许可证，这种情况下，在 `license` 列表中置入多个值，像`license=('GPL' 'custom:name of license')`。
*   另外，(L)GPL 拥有多个版本。对那个 (L)GPL 软件，约定如下：
    *   (L)GPL - 指代 (L)GPLv2 或之后的任意版本
    *   (L)GPL2 - 仅 (L)GPL2
    *   (L)GPL3 - 指代 (L)GPL3 或之后的任意版本
*   如果最终无法决定使用哪种许可证，[PKGBUILD.proto](https://projects.archlinux.org/pacman.git/tree/proto/PKGBUILD.proto) 建议使用 `unknown`。这种情况下应该联系上游的软件发布者。

**提示：** 有些软件作者没有提供单独的版权文件，而是在 ReadMe.txt 中声明。可以在 `build` 阶段将这些声明提取为单独文件：`sed -n '/**This software**/,/ **thereof.**/p' ReadMe.txt > LICENSE`.

关于自由/开源软件协议的更多信息请参考：

*   [w:Free software licence](https://en.wikipedia.org/wiki/Free_software_licence "w:Free software licence")
*   [w:Comparison of free and open-source software licenses](https://en.wikipedia.org/wiki/Comparison_of_free_and_open-source_software_licenses "w:Comparison of free and open-source software licenses")
*   [A Legal Issues Primer for Open Source and Free Software Projects](https://www.softwarefreedom.org/resources/2008/foss-primer.html)
*   [GNU Project - Various Licenses and Comments about Them](https://www.gnu.org/licenses/license-list.html)
*   [Debian - License information](https://www.debian.org/legal/licenses/)
*   [Open Source Initiative - Licenses by Name](http://www.opensource.org/licenses/alphabetical)

### groups

软件包所在的[组](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages")。例如：当你安装 [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/)，它会安装属于 [kde](https://www.archlinux.org/groups/x86_64/kde/) 组里的所有包。

## 依赖关系

**注意:** 架构相关的变量可以通过下划线加架构的方式指定：`depends_x86_64=()`, `optdepends_x86_64=()`.

### depends

软件的运行时依赖列表。可以使用比较运算符来描述版本限制，如：`depends=('foobar>=1.8.0')`。如有多重限制，你可以重复设置它们[[1]](https://mailman.archlinux.org/pipermail/arch-general/2012-July/029022.html)，像这样：`depends=('foobar>=1.8.0' 'foobar<2.0.0')`

不需要列出你的软件包的二次依赖，比如说：[gtk2](https://www.archlinux.org/packages/?name=gtk2)依赖[glib2](https://www.archlinux.org/packages/?name=glib2)和[glibc](https://www.archlinux.org/packages/?name=glibc)；然而[glib2](https://www.archlinux.org/packages/?name=glib2)本就依赖于[glibc](https://www.archlinux.org/packages/?name=glibc)，那么在[gtk2](https://www.archlinux.org/packages/?name=gtk2)中就不需要把[glibc](https://www.archlinux.org/packages/?name=glibc)加入 depends 列表。

如果依赖的名称写成了库的名称（例如 `depends=('libfoobar.so')`），makepkg 会在编译完成的包中添加依赖这个库的二进制文件所依赖的版本，或者你可以自己加上版本号来停用自动检测（ `depends=('libfoobar.so=2')` ）。

### optdepends

一组不影响软件主要功能，但能提供额外特性的软件包。应该简要说明每个包所能提供的额外功能。有些可选依赖如果不安装，软件包的个别程序可能无法正常使用。

`optdepends`看起来像这样：

```
optdepends=(
  'cups: printing support'
  'sane: scanners support'
  'libgphoto2: digital cameras support'
  'alsa-lib: sound support'
  'giflib: GIF images support'
  'libjpeg: JPEG images support'
  'libpng: PNG images support'
)

```

### makedepends

仅在软件编译时需要的软件包列表。可以像`depends`序列里提到的一样指定最小版本依赖。`depends` 数组里面的软件包默认也是编译时需要的。

在使用makepkg构建软件包时，[base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)组被视为已安装。该组的成员**不应该**出现在`makedepends`列表中。用下面程序查看一个依赖关系是否已经包含在 base-devel 中：

```
$ LC_ALL=C pacman -Si $(pactree -rl ''package'') 2>/dev/null | grep -q "^Groups *:.*base-devel"

```

### checkdepends

运行测试组件时需要，而运行时不需要的包列表。该列表中的包遵循和`depends`相同的格式。这些依赖只在[check()](/index.php/Creating_packages#The_check()_function "Creating packages")函数存在且被makepkg运行时被考虑。

**注意:** 在使用makepkg构建软件包时，[base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)组被视为已安装。该组的成员**不应该**出现在`checkdepends`列表中。

## 软件相关性

**注意:** 架构相关的变量可以通过下划线加架构的方式指定：`provides_x86_64=()`, `conflicts_x86_64=()`.

### provides

这个变量说明当前包能提供的功能（或者像 cron、sh 这样的虚拟包）。只要没有标记为 conflicts，提供相同功能的软件包可以同时安装，

如果你使用这个变量，应当加上所替代软件的版本号（`pkgver`，可能的话还有`pkgrel`）。举例来说，如果你提供一个修改过的 *qt* 包其版本号为 3.3.8，命名为 *qt-foobar*，那么 `provides` 应该写成 `provides=('qt=3.3.8')`。只写成 `provides=('qt')` 会使对 *qt* 有版本依赖的包编译失败。不要把 `pkgname` 加入 provides 序列，它会自动完成的。

### conflicts

与当前软件包发生冲突的包列表。安装此软件时，所有有冲突的软件都会被删除。可以像 depends 那样指定冲突包的版本号。如果你在制作已有的软件包（例如官方源或 AUR ）的替代时，你需要在 `conflicts` 中指定它们与你的包冲突。

有时候，指定所有软件包的冲突很难实现，尤其是当软件包被不同的人维护的时候。所以如果软件包的 `provides` 和其它软件包的 `provides` 提供了相同的功能，就不需要将冲突的包添加进 `conflicts` 组中，例如：

*   [netbeans](https://www.archlinux.org/packages/?name=netbeans) 提供 `netbeans` 。
*   [netbeans-javase](https://aur.archlinux.org/packages/netbeans-javase/) 提供 `netbeans` ，和 `netbeans` 冲突。
*   [netbeans-php](https://aur.archlinux.org/packages/netbeans-php/) 提供 `netbeans` 而且和 `netbeans` 冲突，但是因为它和 [netbeans-javase](https://aur.archlinux.org/packages/netbeans-javase/) 都提供 `netbeans` 而且 [netbeans-javase](https://aur.archlinux.org/packages/netbeans-javase/) 和 `netbeans` 冲突，pacman 可以发现它们相互冲突，于是不必在 `conflicts` 中表示 [netbeans-php](https://aur.archlinux.org/packages/netbeans-php/) 和 [netbeans-javase](https://aur.archlinux.org/packages/netbeans-javase/) 冲突了。

	反过来的例子： [netbeans-javase](https://aur.archlinux.org/packages/netbeans-javase/) 因为和 [netbeans-php](https://aur.archlinux.org/packages/netbeans-php/) 提供相同的功能，于是不必相互冲突。

### replaces

会因安装当前包而取代的包列表，比如：[wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk)中的`replaces=('wireshark')`。`pacman -Sy` 同步软件数据库后，会立刻用软件库中的另一个包替换掉 `replaces`中已安装的包。如果你只是提供已存在包的一个替代品，或者上传到 [AUR](/index.php/AUR "AUR"), 使用`conflicts`和`provides`变量——它们仅在安装冲突包时被检查。

## 其它

### backup

当包被升级或卸载时，应当备份的文件（的名字）。这些文件一般是用户会更改的文件，如（主要是）放置在`/etc`中的配置文件。

列表中的文件应该使用相对路径(如 `etc/pacman.conf`)，而不是绝对路径(如 `/etc/pacman.conf`)。

在升级时，新版本会被命名为`file.pacnew`以避免覆盖旧有且被用户修改过的文件。类似地，当卸载包时，用户修改过的文件会以`file.pacsave`为名而保留下来——除非用`pacman -Rn`命令卸载。

参见[Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files")获取更多信息。

### options

这个变量允许你重置`makepkg`的部分默认（定义在`/etc/makepkg.conf`中的）行为。要设置一个选项必须指定选项名。要反转一个默认行为，在选项前加上**`!`** 。 参见 [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5) 以获取所有可用选项。

### install

`.install` 脚本的名称, 应该和 pkgname 相同。 *pacman* 可以在安装、卸载或升级一个软件包时存储及执行一些特定的脚本。在不同的情况下，脚本会执行下面几个函数。

*   ***pre_install*** - 安装前运行的脚本，可以传递版本号为参数。
*   ***post_install*** - 安装后运行的脚本，可以传递版本号为参数。
*   ***pre_upgrade*** - 升级前运行的脚本，可以按`新版本号`，`旧版本号`的顺序传递参数。
*   ***post_upgrade*** - 升级后运行的脚本，可以按`新版本号`，`旧版本号`的顺序传递参数。
*   ***pre_remove*** - 卸载前运行的脚本，可以传递版本号为参数。
*   ***post_remove*** - 卸载后运行的脚本，可以传递版本号为参数。

每一个函数都是在 pacman 安装目录下通过 chroot 运行。参见[这个帖子](https://bbs.archlinux.org/viewtopic.php?pid=913891).

**提示：** 一个 `.install` 文件模板（原型）位于[/usr/share/pacman/proto.install 这里](https://projects.archlinux.org/pacman.git/plain/proto/proto.install)。

**提示：** [pacman#Hooks](/index.php/Pacman#Hooks "Pacman") 也提供相似的功能。

**Note:** 脚本不要以 `exit` 结束，否则包含的函数无法被执行。

### changelog

软件包 changelog 的名称，要查看安装软件的 changelog：

```
$ pacman -Qc *pkgname*

```

## 源码

### source

构建软件包时需要的文件列表。它必须包含软件源的位置信息，大多数情况下是一个完整的 HTTP 或 FTP 地址。可以在软件源信息中很好的调用前面提到的变量 `pkgname` 和 `pkgver`(如 `source=("https://example.com/$pkgname-$pkgver.tar.gz")`)。

文件也可以放到 `PKGBUILD` 相同目录中，把文件名添加到这个列表中，以相对 `PKGBUILD` 的路径记录。在实际的编译过程开始之前，所有该列表中引用的文件都会被下载或检查是否存在，如果有文件丢失 `makepkg` 就不会继续。

*makepkg* 会自动把 *.sig*, *.sign* 或 *.asc* 结尾的文件当成 PGP 签名，并自动验证源代码文件的完整性。

**注意:**

*   架构相关的变量可以通过下划线加架构的方式指定：`source_x86_64=()`. 记得要同时提供对应的校验和：`sha256sums_x86_64=()`
*   因为所有包的 [SRCDEST](/index.php/Makepkg#Package_output "Makepkg") 的值必须相同，所以下载的文件的文件名需要唯一。你可以为下载的文件指定不同的文件名： `source=('*filename*::*fileuri*')`,选择的 `*filename*` 最好和软件包名相关: `source=("project_name::hg+https://googlefontdirectory.googlecode.com/hg/")` 

### noextract

一些列举于 `source` 中，但不需要在运行`makepkg`时解包的文件。在碰到不能被`/usr/bin/bsdtar`处理的文件或不需要解压的文件时使用。在这些情况下，额外的解包工具（如`unzip`、`p7zip`，[lrzip](https://www.archlinux.org/packages/?name=lrzip)等）应该加入 `makedepends` 序列，并且用[prepare()](/index.php/Creating_packages#The_prepare()_function "Creating packages")函数手动解包。例如：

```
  prepare() {
  lrzip -d *source*.tar.lrz
}

```

注意当 `source` 是一些 URL 时，`noextract` **仅仅**取文件名部分：

```
source=("https://ftp.archlinux.org/other/grub2/grub2_extras_lua_r20.tar.xz")
noextract=('grub2_extras_lua_r20.tar.xz')

```

不提取任何东西时，可以像这样：

```
noextract=("${source[@]%%::*}")

```

### validpgpkeys

PGP 指纹列表。如果使用，*makepkg* 仅接受这里定义的签名，并且忽略密钥环中的值。如果源代码用子密钥签名，*makepkg* 会使用主密钥进行比较。

仅接受完整签名，必须是大写字母而且不能有空白字符。

**Note:** 可以使用 `gpg --list-keys --fingerprint <KEYID>` 查找 key 的指纹.

请参阅 [Makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg") 了解签名效验的详细信息。

## 完整性

**注意:** 架构相关的变量可以通过下划线加架构的方式指定：`depends_x86_64=()`, `optdepends_x86_64=()`.

数组中的变量是 [#source](#source) 数组中对应文件的校验和。可以插入 `SKIP` 跳过某个未测试文件的校验。

Checksums 仅是为了验证下载文件的 *完整性*，而**不是** 它们的 *真实性*: 所以虽然 MD5 算法有 [漏洞](https://en.wikipedia.org/wiki/MD5#Security "wikipedia:MD5")，不能在其它地方使用。在这里却是推荐使用的，因为它的速度比其它算法例如 SHA-2 要快很多。尤其是 `source` 数组中的文件很大时. 如果可能，请尽量在 `source` 数组中加入它们的签名信息。这时就可以跳过完整性校验。

[makepkg](/index.php/Makepkg "Makepkg") 的 `-g`/`--geninteg` 选项可以自动生成校验值，可以通过 `makepkg -g >> PKGBUILD` 命令写入. `updpkgsums` 也可以自动更新 PKGBUILD 中的数值. 两个工具都会自动检测 PKGBUILD 中的算法, 如果没找到就使用 `md5sums`。

要使用的校验算法可以通过 `/etc/makepkg.conf` 中的 `INTEGRITY_CHECK` 选项设置，参考 [makepkg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5).

### md5sums

`source` 列表文件中的 128 位 [MD5](https://en.wikipedia.org/wiki/MD5 "wikipedia:MD5") 校验和。

### sha1sums

`source` 列表文件中 [SHA-1](https://en.wikipedia.org/wiki/SHA-1 "wikipedia:SHA-1") 160位校验和。

### sha256sums

256 位 [SHA-2](https://en.wikipedia.org/wiki/SHA-2 "wikipedia:SHA-2") 校验和。

### sha224sums, sha384sums, sha512sums

SHA-2 校验和列表，有224，384 和 512位。它们都可以替代上述的 `sha256sums`。

## 参阅

*   [PKGBUILD(5) 手册页](https://www.archlinux.org/pacman/PKGBUILD.5.html)
*   [PKGBUILD 示例](http://ix.io/66p)