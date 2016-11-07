**翻译状态：** 本文是英文页面 [Fonts](/index.php/Fonts "Fonts") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-14，点击[这里](https://wiki.archlinux.org/index.php?title=Fonts&diff=0&oldid=450802)可以查看翻译后英文页面的改动。

引自 [维基百科](https://en.wikipedia.org/wiki/zh:%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%AD%97%E4%BD%93 "wikipedia:zh:计算机字体")："**计算机字体**（computer font），简称**字体**（font），是包含有一套字形与字符的电子数据文件。"

注意：部分字体在许可协议中规定了使用时的法律限制。

## Contents

*   [1 字体类型](#.E5.AD.97.E4.BD.93.E7.B1.BB.E5.9E.8B)
    *   [1.1 常见格式](#.E5.B8.B8.E8.A7.81.E6.A0.BC.E5.BC.8F)
    *   [1.2 其它格式](#.E5.85.B6.E5.AE.83.E6.A0.BC.E5.BC.8F)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 Pacman](#Pacman)
    *   [2.2 创建字体包](#.E5.88.9B.E5.BB.BA.E5.AD.97.E4.BD.93.E5.8C.85)
    *   [2.3 手动安装字体](#.E6.89.8B.E5.8A.A8.E5.AE.89.E8.A3.85.E5.AD.97.E4.BD.93)
        *   [2.3.1 手动安装：高级模式](#.E6.89.8B.E5.8A.A8.E5.AE.89.E8.A3.85.EF.BC.9A.E9.AB.98.E7.BA.A7.E6.A8.A1.E5.BC.8F)
        *   [2.3.2 过老的应用程序](#.E8.BF.87.E8.80.81.E7.9A.84.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [2.4 Pango 警告](#Pango_.E8.AD.A6.E5.91.8A)
*   [3 终端字体](#.E7.BB.88.E7.AB.AF.E5.AD.97.E4.BD.93)
    *   [3.1 预览和测试](#.E9.A2.84.E8.A7.88.E5.92.8C.E6.B5.8B.E8.AF.95)
    *   [3.2 持久性配置](#.E6.8C.81.E4.B9.85.E6.80.A7.E9.85.8D.E7.BD.AE)
*   [4 字体包](#.E5.AD.97.E4.BD.93.E5.8C.85)
    *   [4.1 盲文点字](#.E7.9B.B2.E6.96.87.E7.82.B9.E5.AD.97)
    *   [4.2 数学和符号字体](#.E6.95.B0.E5.AD.A6.E5.92.8C.E7.AC.A6.E5.8F.B7.E5.AD.97.E4.BD.93)
    *   [4.3 非英文使用者](#.E9.9D.9E.E8.8B.B1.E6.96.87.E4.BD.BF.E7.94.A8.E8.80.85)
        *   [4.3.1 中日韩越文字](#.E4.B8.AD.E6.97.A5.E9.9F.A9.E8.B6.8A.E6.96.87.E5.AD.97)
            *   [4.3.1.1 Pan-CJK](#Pan-CJK)
            *   [4.3.1.2 中文字](#.E4.B8.AD.E6.96.87.E5.AD.97)
            *   [4.3.1.3 日文字](#.E6.97.A5.E6.96.87.E5.AD.97)
            *   [4.3.1.4 韩文字](#.E9.9F.A9.E6.96.87.E5.AD.97)
        *   [4.3.2 阿拉伯和乌尔都文字](#.E9.98.BF.E6.8B.89.E4.BC.AF.E5.92.8C.E4.B9.8C.E5.B0.94.E9.83.BD.E6.96.87.E5.AD.97)
        *   [4.3.3 波斯文字](#.E6.B3.A2.E6.96.AF.E6.96.87.E5.AD.97)
        *   [4.3.4 缅甸文字](#.E7.BC.85.E7.94.B8.E6.96.87.E5.AD.97)
        *   [4.3.5 西里尔文字](#.E8.A5.BF.E9.87.8C.E5.B0.94.E6.96.87.E5.AD.97)
        *   [4.3.6 希腊文字](#.E5.B8.8C.E8.85.8A.E6.96.87.E5.AD.97)
        *   [4.3.7 希伯来文字](#.E5.B8.8C.E4.BC.AF.E6.9D.A5.E6.96.87.E5.AD.97)
        *   [4.3.8 印地文字](#.E5.8D.B0.E5.9C.B0.E6.96.87.E5.AD.97)
        *   [4.3.9 高棉文字](#.E9.AB.98.E6.A3.89.E6.96.87.E5.AD.97)
        *   [4.3.10 僧伽罗文字](#.E5.83.A7.E4.BC.BD.E7.BD.97.E6.96.87.E5.AD.97)
        *   [4.3.11 塔米尔文字](#.E5.A1.94.E7.B1.B3.E5.B0.94.E6.96.87.E5.AD.97)
        *   [4.3.12 藏文字](#.E8.97.8F.E6.96.87.E5.AD.97)
    *   [4.4 Microsoft 字体](#Microsoft_.E5.AD.97.E4.BD.93)
    *   [4.5 Apple OS X 字体](#Apple_OS_X_.E5.AD.97.E4.BD.93)
    *   [4.6 等宽字体](#.E7.AD.89.E5.AE.BD.E5.AD.97.E4.BD.93)
        *   [4.6.1 TrueType 字体](#TrueType_.E5.AD.97.E4.BD.93)
        *   [4.6.2 点阵字体](#.E7.82.B9.E9.98.B5.E5.AD.97.E4.BD.93)
    *   [4.7 无衬线字体](#.E6.97.A0.E8.A1.AC.E7.BA.BF.E5.AD.97.E4.BD.93)
    *   [4.8 手写体](#.E6.89.8B.E5.86.99.E4.BD.93)
    *   [4.9 衬线字体](#.E8.A1.AC.E7.BA.BF.E5.AD.97.E4.BD.93)
    *   [4.10 未分类字体](#.E6.9C.AA.E5.88.86.E7.B1.BB.E5.AD.97.E4.BD.93)
*   [5 X11中的字体回滚顺序](#X11.E4.B8.AD.E7.9A.84.E5.AD.97.E4.BD.93.E5.9B.9E.E6.BB.9A.E9.A1.BA.E5.BA.8F)
*   [6 字体别名](#.E5.AD.97.E4.BD.93.E5.88.AB.E5.90.8D)
*   [7 小提示](#.E5.B0.8F.E6.8F.90.E7.A4.BA)
    *   [7.1 列出已安装字体](#.E5.88.97.E5.87.BA.E5.B7.B2.E5.AE.89.E8.A3.85.E5.AD.97.E4.BD.93)
    *   [7.2 应用程序专用的字体高速缓冲](#.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E4.B8.93.E7.94.A8.E7.9A.84.E5.AD.97.E4.BD.93.E9.AB.98.E9.80.9F.E7.BC.93.E5.86.B2)
*   [8 参见](#.E5.8F.82.E8.A7.81)

## 字体类型

现今计算机使用的绝大多数字体，都是属于**点阵字体**或者**轮廓字体**二者之一。

	点阵字体

	每种字形的每种形式和每种尺寸的图像都由点或者像素组成的矩阵构成。由于位图的原故，点阵字体很难进行缩放，特定的点阵字体只能清晰地显示在相应的字号下。但对于 12-16 px 的小号汉字来说，点阵字体往往比其它类型的字体在屏幕上有更好的显示效果。

	轮廓字体或称矢量字体

	使用贝塞尔曲线、绘图指令和数学公式来描述每种字形，使得字体可以适应各种尺寸。

### 常见格式

*   `bdf` 与 `bdf.gz` – 点阵字体，**b**itmap **d**istribution **f**ormat（位图布局格式）的缩写，后者表示以 gzip 压缩的 `bdf`。
*   `pcf` 与 `pcf.gz` – 点阵字体， **p**ortable **c**ompiled **f**ont（可移植编译字体）的缩写，后者表示以 gzip 压缩的 `pcf`。
*   `psf`，`psfu`与`psf.gz`，`psfu.gz` – 点阵字体，前两者分别是 **P**C **s**creen **f**ont（电脑屏幕字体）与 **P**C **s**creen **f**ont **U**nicode（Unicode 电脑屏幕字体）的缩写。两者分别表示用 gzip 压缩的 `psf` 与 {{ic|psfu}（不适用于 X.Org）。
*   `pfa` 与 `pfb` – 矢量字体，分别是 **P**ostScript **f**ont **A**SCII 与 **P**ostScript **f**ont **b**inary 的缩写。PostScript 字体内带有打印指令。
*   `ttf` – outline，**T**rue**T**ype 字体。作为 PostScript 字体的替代。
*   `otf` – outline，**O**pen**T**ype 字体。带有 PostScript 打印指令的 TrueType 字体。

在多数情况下，TrueType 和 OpenType 的技术差异可以忽略，一些带有 `ttf` 扩展的字体实际上是 OpenType 字体。

### 其它格式

排版程序 **TeX** 和配套的字体软件 **Metafont** 用它们自己的方法渲染字体。部分用于这两个程序的字体的文件后缀有 `*pk`, `*gf`, `mf` 与 `vf`。

**FontForge**，一个字体编辑程序，可以用自己的格式来储存字体，例如 `sfd` （*s*pline *f*ont *d*atabase）。

[SVG](http://www.w3.org/TR/SVG/fonts.html) 格式也有自己的字体描述方法。

## 安装

你可以使用多种方法安装字体。

### Pacman

有效的源中的字体和字体集可以使用 [pacman](/index.php/Pacman "Pacman") 来安装。 可以使用以下方式查找字体:

```
$ pacman -Ss font

```

或者也可以只查找 `ttf` 字体:

```
$ pacman -Ss ttf

```

### 创建字体包

如果您想用 pacman 来管理你自己的字体，可以创建一个 Arch 软件包。这些包也可以在 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 中与社区成员分享。下面是一个创建软件包的基本样例。您还可以参考 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 来获取更多有关创建软件包的资料。

```
pkgname=ttf-fontname
pkgver=1.0
pkgrel=1
pkgdesc="custom fonts"
arch=(any)
depends=(fontconfig xorg-font-utils)
source=("http://someurl.org/$pkgname.tar.bz2")
install=$pkgname.install

package() {
  install -d "$pkgdir/usr/share/fonts/TTF"
  install -m644 "$srcdir/$pkgname/"*.ttf "$pkgdir/usr/share/fonts/TTF/"
}

```

PKGBUILD 推断这些字体是 TrueType 字体。需要创建一个安装文件 (`ttf-fontname.install`) 以便更新字体缓存：

```
post_install() {
  echo -n "Updating font cache... "
  fc-cache >/dev/null -f
  mkfontscale /usr/share/fonts/TTF
  mkfontdir   /usr/share/fonts/TTF
  echo done
}

post_upgrade() {
  post_install
}

post_remove() {
  post_install
}

```

如果想更方便地从TTFs创建自己的包，可以使用 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 中的 [makefontpkg](https://aur.archlinux.org/packages/makefontpkg/)。

### 手动安装字体

要安装不在源中的字体，推荐的方法请参考[#创建字体包](#.E5.88.9B.E5.BB.BA.E5.AD.97.E4.BD.93.E5.8C.85)。这样使得 pacman 在以后能够更新或者移除它们。当然字体也可以通过手工方式安装。

要在系统范围内（对所有用户有效）安装字体，请将文件夹移动到 `/usr/share/fonts/` 目录。这些文件需要对每个用户而言都是可读的，使用 [chmod](/index.php/Chmod "Chmod") 来设置合理的权限 (比如，文件至少为 `0444` ，而目录至少为 `0555`)。要为单个用户安装字体，请使用 `~/.local/share/fonts` (`~/.fonts/` 现在已经过时了)。 要让 Xserver 能直接载入字体（而不使用某些**字体服务**），就需要将新增字体的目录加入到 FontPath 中。它位于[您的 Xorg 设置目录](/index.php/Xorg#Configuration "Xorg")中（例如 `/etc/X11/xorg.conf` 或 `/etc/xorg.conf`) 中。更多详细内容请查阅[#X.Org 中的字体](#X.Org_.E4.B8.AD.E7.9A.84.E5.AD.97.E4.BD.93)

然后更新 fontconfig 的字体缓存：

```
$ fc-cache -vf

```

#### 手动安装：高级模式

如果您有特殊的字体收集需求，例如使用商业字体、使用不同格式的字体、安装/删除字体相当频繁，或只是希望可以更能够控制访问自己的字体资源，那就相当适合用手动的方式来安装维护字体。采用这种方案会获得很多好处：

*   避免重复安装不同版本、格式的同一种字体集 (经常容易导致渲染问题)。
*   字体可使用多个非标准的实体来源 (例如额外的硬盘、分区)。
*   避免依赖隐晦又占体积的本地字体来源（例如 TeX Live & `09-texlive-fonts.conf`，或是 AUR 中的某个字体包）；使用这些字体来源时，您可能只需要其中的 5 种字体，却必须连带安装其它 55 种不需要的字体。
*   避免字体渲染问题，在您的 fontconfig 配置文件已被修改成与安装在系统的那份不同的格式。
*   只要观察主字体目录下的内容，就能够确定系统上有哪种格式的字体集可供应用程序使用。您不需要复杂、占用大量资源的字体管理程序；[gtk2fontsel](https://www.archlinux.org/packages/?name=gtk2fontsel) 和基本的指令工具 (如 [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) 软件包下的 `fc-query`) 就可以将这件差事办得又快又好。
*   当您安装或升级单一字体，所有应用程序都可以使用新版本字体，包括 LaTeX 相关软件。
*   有必要的话，可以快速启用 / 停用某个字体集，因为您知道它们在哪个目录下（调试时很好用）。
*   不需担心有任何多余的 `/etc/fonts/conf.avail/nn-foo.conf` fontconfig 文件会可能与您的渲染设置起冲突 (特别是当您使用[自定的字体设置与修补过的函式库](/index.php/Font_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.A1.A5.E4.B8.81.E5.8C.85 "Font configuration (简体中文)")时)。
*   长远来看，可以省下那些因软件包管理器的失误，解决问题和清除冲突所浪费的宝贵时间。

实际操作上有几种方式，有必要的话可任由软件包管理员采用。以下所举出的操作方式相当有效率，即使字体数目众多也相当安全。

*   我们要将字体来源位置 (例如 `/usr/share/fonts.avail`：这是我们要存放字体的位置) 和包含字体集软链接的目录 (`/usr/share/fonts`) 给分隔开来。

*   将每个字体集分别放在一个明确命名的子目录下。命名规则必须一致且明确，例如这样：

```
<ttf|otf|t1>-<字体作者或组织(选用)>-<字体集名称>

```

字体来源目录的内容会长得像这样：

```
$ ls /usr/share/fonts.avail

/usr/share/fonts.avail/otf-heuristica
/usr/share/fonts.avail/ttf-liberation
/usr/share/fonts.avail/ttf-ms-arial
...

```

*   我们不会涉及到 TeX Live 的字体目录，以避免 LaTeX 软件发生任何问题。既然我们可以使用多个位置，我们将在 `/usr/share/fonts` 创建软链接，让应用程序可以访问特定的字体集：

```
# cd /usr/share/fonts
# ln -s ../fonts.avail/otf-heuristica .
# ln -s /opt/texlive/texmf-dist/fonts/truetype/public/opensans ttf-texlive-open.sans

```

结果如下：

```
$ ls /usr/share/fonts

ttf-liberation        -> ..fonts.avail/ttf-liberation
ttf-ms-arial          -> ..fonts.avail/ttf-ms-arial
otf-heuristica        -> ..fonts.avail/otf-heuristica
otf-texlive-tex.gyre  -> /opt/texlive/texmf-dist/fonts/opentype/public/tex-gyre
ttf-texlive-open.sans -> /opt/texlive/texmf-dist/fonts/truetype/public/opensans
...

```

最后，依照惯例执行：

```
# fc-cache && mkfontscale && mkfontdir

```

[TeX Live](/index.php/TeXLive_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "TeXLive (简体中文)") Wiki 文章内也有一个类似做法，比较简单，但更适用于单一用户的情形，而非全局设置。

#### 过老的应用程序

过老而不支持 fontconfig 的应用程序（例如 GTK+ 1.x 应用，及 `xfontsel`），需要在字体目录创建索引：

```
$ mkfontscale
$ mkfontdir

```

或在一条命令中包含多个目录：

```
$ for dir in /font/dir1/ /font/dir2/; do xset +fp $dir; done && xset fp rehash

```

或者如果字体被安装在一个不同的子文件夹，比如在 `/usr/share/fonts` 下:

```
$ for dir in * ; do if [  -d  "$dir"  ]; then cd "$dir";xset +fp "$PWD" ;mkfontscale; mkfontdir;cd .. ;fi; done && xset fp rehash

```

有时候 X server 可能会不能成功加载字体目录，这时你需要重新扫描 `fonts.dir` 文件:

```
# xset +fp /usr/share/fonts/misc # Inform the X server of new directories
# xset fp rehash                # Forces a new rescan

```

查询字体是否已经生效，可以使用:

```
$ xlsfonts | grep fontname

```

**注意:** 许多软件包会自动配置 Xorg 安装时需要的字体。若这样，便可跳过此步。

为了让 [Xorg](/index.php/Xorg "Xorg") 找到并使用你新安装的字体，你必须把字体路径加入到 `/etc/X11/xorg.conf`（另一个 X.Org 配置文件或许也可以）。

这个例子演示了必须加入到 `/etc/X11/xorg.conf` 中的代码片断。请根据你的实际需要添加或删除路径。

```
# 让 X.Org 知道自定义字体目录
Section "Files"
    FontPath    "/usr/share/fonts/100dpi"
    FontPath    "/usr/share/fonts/75dpi"
    FontPath    "/usr/share/fonts/cantarell"
    FontPath    "/usr/share/fonts/cyrillic"
    FontPath    "/usr/share/fonts/encodings"
    FontPath    "/usr/share/fonts/local"
    FontPath    "/usr/share/fonts/misc"
    FontPath    "/usr/share/fonts/truetype"
    FontPath    "/usr/share/fonts/TTF"
    FontPath    "/usr/share/fonts/util"
EndSection

```

### Pango 警告

当你的系统中安装了[Pango](http://www.pango.org/)，它会从 [fontconfig](http://www.freedesktop.org/wiki/Software/fontconfig) 查找字体来源。

```
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='common'
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='latin'

```

如果你看到类似的错误，或在应用程序中看到方块而不是文字，这表示你需要添加字体并更新字体缓存。以下示例使用[ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)字体讲解如何解决这个问题。使用 root 权限运行如下命令可以使字体在系统范围内生效。

```
# pacman -S ttf-liberation
  -- output abbreviated, assumes installation succeeded -- 

# fc-cache -vfs
/usr/share/fonts: caching, new cache contents: 0 fonts, 3 dirs
/usr/share/fonts/TTF: caching, new cache contents: 16 fonts, 0 dirs
/usr/share/fonts/encodings: caching, new cache contents: 0 fonts, 1 dirs
/usr/share/fonts/encodings/large: caching, new cache contents: 0 fonts, 0 dirs
/usr/share/fonts/util: caching, new cache contents: 0 fonts, 0 dirs
/var/cache/fontconfig: cleaning cache directory   
fc-cache: succeeded

```

你可以这样测试一个正在设置的默认字体：

```
# fc-match
LiberationMono-Regular.ttf: "Liberation Mono" "Regular"

```

## 终端字体

**注意:** 这部分是关于 [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console")。如果您想获取其它的更加丰富的关于终端的解决方案 (完备的 Unicode 字体, 现代的图形化配适器，等等。), 请参照 [fbterm](/index.php/Fbterm "Fbterm"), [KMSCON](/index.php/KMSCON "KMSCON") 或者类似的项目.

默认情况下, [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") 使用内核的内置字体，其包含 [CP437](https://en.wikipedia.org/wiki/CP437 "wikipedia:CP437") 字体集, 但是这个设置可以非常容易改变.

[Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console") 默认使用 UTF-8 编码, 但是由于使用的是标准的兼容 VGA 的帧缓存, 终端字体限定为 256 或 512 个字形。如果字体超出了256个字形, 那么颜色的数量就会从 16 减少到 8。为了针对给定的 Unicode z值分配正确的可显示符号，一种特殊的翻译映射，通常叫做 *unimap*,是必须的。 就目前来看大多数终端字体都具有内置的 *unimap*, 但是历史上它是需要被单独载入的。

```
[kbd](https://www.archlinux.org/packages/?name=kbd) 包提供了改变虚拟终端字体和字体映射的工具。可以使用的字体存储在 `/usr/share/kbd/consolefonts/` 目录下, 那些以 *.psfu* 或者 *.psfu.gz* 结尾的具有一个内嵌的 Unicode 翻译映射。

```

键盘映射 (Keymap) 是按键和计算机使用字符的对应关系表，可以在 `/usr/share/kbd/keymaps/` 的子目录下找到，详情请查看 [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") 。

**注意:** Replacing the font can cause issues with programs that expect a standard VGA-style font, such as those using line drawing graphics.

### 预览和测试

1.  REDIRECT [Template:Tip (简体中文)](/index.php/Template:Tip_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Template:Tip (简体中文)")

*showconsolefont* 指令会以表格形式显示可用字与字符：

```
$ showconsolefont

```

*setfont* 工具可以暂时改变字体，让用户可以决定是否要设为永久性设置。只要指定字体名称即可 (这些字体位于 `/usr/share/kbd/consolefonts/`)，比如：

```
$ setfont lat2-16

```

如果对新换的字体不满意，可以用以下指令撤消至默认字体 (就算终端显示乱码，这个指令依然可以执行，将指令「盲打」进去即可)：

```
$ setfont

```

**注意:** *setfont* 只作用于当前正在使用的终端。其它终端无论活跃与否都不受影响。

### 持久性配置

`/etc/vconsole.conf` 的 `FONT` 变量可以用来在启动时设置字体, 对于所有的终端都具有持久性作用。详情请查看 `man 5 vconsole.conf` 。

若要显示 *Č, ž, đ, š* 或 *Ł, ę, ą, ś* 之类的字符，请使用 `lat2-16.psfu.gz` 这个字体：

 `/etc/vconsole.conf` 
```
...
FONT=lat2-16
```

这代表使用 ISO/IEC 8859 字符的第二部分，尺寸设置为 16。您可以使用其它值更改字体尺寸 (如 `lat2-08`)。您可以在[Wikipedia的这张表](https://en.wikipedia.org/wiki/ISO/IEC_8859#The_Parts_of_ISO.2FIEC_8859 "wikipedia:ISO/IEC 8859")查询 8859 规范定义的本地。

若要为早期的用户空间套用指定字体，请在 `/etc/mkinitcpio.conf` 使用 `consolefont` 勾子。更多信息请参阅 [Mkinitcpio (简体中文)#钩子(HOOKS)](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E9.92.A9.E5.AD.90.28HOOKS.29 "Mkinitcpio (简体中文)")。

如果开机时字体没有任何变化，或只变化一下就恢复原样，则有可能是因为显卡驱动引导时字体被复位，然后终端被切至帧缓冲 (framebuffer)。提早装入图形驱动可以避免这个问题。若要在套用 `/etc/vconsole.conf` 之前将帧缓冲准备好，请参阅[核心模式设置#提早引导 KMS](/index.php/Kernel_mode_setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#KMS_.E6.97.A9.E5.90.AF.E5.8A.A8 "Kernel mode setting (简体中文)")、[[2]](https://bbs.archlinux.org/viewtopic.php?id=145765) 或其它方式。

## 字体包

以下是官方源和 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 中提供的安装包列表以供参考。支持 Unicode 的字体都标注上了“Unicode”字样。欲知详情请查看具体项目或维基百科。

Github用户Ternstor编写了一段python脚本，可以通过在 AUR 和官方源中所有字体的 PNG 图像产生 HTML 文件: [[3]](https://github.com/ternstor/distrofonts/blob/master/archfonts.py).

### 盲文点字

*   [ttf-ubraille](https://www.archlinux.org/packages/?name=ttf-ubraille) - 包含 Unicode **盲文点字**符号的字体。

### 数学和符号字体

*   [ttf-symbola](https://www.archlinux.org/packages/?name=ttf-symbola) - 提供许多 Unicode 符号，包括 Emoji
*   [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica) - Wolfram 公司的 Mathematica 字体
*   [texlive-core](https://www.archlinux.org/packages/?name=texlive-core), [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra) 包含许多数学字体，如拉丁符号。
*   [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji) - Google 的 emoji 字体
*   [ttf-mathtype](https://aur.archlinux.org/packages/ttf-mathtype/) - MathType 字体
*   [ttf-computer-modern-fonts](https://aur.archlinux.org/packages/ttf-computer-modern-fonts/), [otf-cm-unicode](https://aur.archlinux.org/packages/otf-cm-unicode/) - [Computer Modern](https://en.wikipedia.org/wiki/Computer_Modern "wikipedia:Computer Modern") (of TeX fame)
*   [otf-latin-modern](https://aur.archlinux.org/packages/otf-latin-modern/), [otf-latinmodern-math](https://aur.archlinux.org/packages/otf-latinmodern-math/) -Computer Modern fonts 的改进版本
*   [otf-xits](https://aur.archlinux.org/packages/otf-xits/) - STIX 字体的 OpenType 实现，以及对从右到左的书写支持。
*   [emojione-color-font](https://aur.archlinux.org/packages/emojione-color-font/) -完整、独立、开源的 Emoji 字体集，专心于设计正确
*   [twemoji-color-font](https://aur.archlinux.org/packages/twemoji-color-font/) - Twitter 的开源 Emoji 字形

### 非英文使用者

应用程序与浏览器会根据 fontconfig 设置和 Unicode 文字可用的字体来选择其显示字体。用指令 `fc-list :lang="双字母的语言代码"` 枚举系统安装了哪些可对应该语言的字体。例如，枚举已经安装的阿拉伯文字体，以及支持阿拉伯字的字体：

 `$ fc-list :lang=ar | cut -d: -f1` 
```
/usr/share/fonts/TTF/FreeMono.ttf
/usr/share/fonts/TTF/DejaVuSansCondensed.ttf
/usr/share/fonts/truetype/custom/DroidKufi-Bold.ttf
/usr/share/fonts/TTF/DejaVuSansMono.ttf
/usr/share/fonts/TTF/FreeSerif.ttf

```

若要在多国语言的网站（如Wikipedia、Arch Linux Wiki）中正确显示字形，需要安装下列一项软件包：

*   谷歌的 [Noto](http://www.google.com/get/noto/) 字体家族旨在支持所有语言。请安装 [noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts), [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk) 和 [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji) 软件包。
*   An alternative set of fonts which has a good coverage of languages is [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont) with [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) and [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk).

#### 中日韩越文字

##### Pan-CJK

*   [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk) - Google Noto CJK 字体， 提供简体中文、繁体中文、日文、韩文一致的设计和外观。它是基于 [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts) 重贴的商标。
*   [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts) - 思源黑体， 是由 Adobe 与 Google 合资开发的，囊括简体中文、繁体中文、日文、韩文字形和来自 Source Sans 字体家族的拉丁文、希腊文和西里尔文字形的高质量无衬线 OpenType 字体。

##### 中文字

*   [adobe-source-han-sans-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-cn-fonts) - 思源黑体简体中文部分
*   [adobe-source-han-sans-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-tw-fonts) - 思源黑体繁体中文部分
*   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) - 文泉驿微米黑，无衬线形式的高质量中日韩越 (CJKV) 轮廓字体。
*   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) - 文泉驿正黑，黑体 (无衬线) 的中文轮廓字体，附带文泉驿点阵宋体 (也支持部分日韩字符)。
*   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai) - **楷书** (带有笔触) Unicode 字体 (推荐启用反锯齿)
*   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) - **明体** (印刷) Unicode 字体
*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts) - **新宋**字体，之前为 ttf-fireflysung
*   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont) - 文泉驿点阵宋体 (衬线) 中文字体
*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - 中文、越南文 TrueType 字体
*   [ttf-tw](https://aur.archlinux.org/packages/ttf-tw/) - （繁体）台湾教育部发行的标准楷书、宋体字体

##### 日文字

*   [adobe-source-han-sans-jp-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-jp-fonts) - 思源黑体日文部分
*   [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont) - 正式的日文哥特体（无衬线）与明朝体 （衬线）字形集，高质量的开源字体之一，openSUSE-ja 的默认字形。
*   [ttf-hanazono](https://www.archlinux.org/packages/?name=ttf-hanazono) - 一款免费的日文汉字字体，Mincho（衬线）风格。
*   [ttf-sazanami](https://www.archlinux.org/packages/?name=ttf-sazanami) - 自由的日文 TrueType 字体。已经过期无人维护，但在某些环境下可当作备用字体使用。
*   [ttf-vlgothic](https://aur.archlinux.org/packages/ttf-vlgothic/) - 日文哥特体字形。Debian/Fedora/Vine Linux 的默认字体
*   [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) - 现代哥特体的日文轮廓字体。包含所有日文平假名/片假名、Basic Latin、Latin-1 Supplement、Latin Extended-A、IPA Extensions。另外还有大部分日文汉字、希腊字母、西里尔字与越南文字，可以 7 磅 (等比例) 或 5 磅 (等宽) 字重显示。
*   [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/) - 日文字体，可正确显示 [2ch 的 Shift JIS 艺术创作](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art")。

##### 韩文字

*   [adobe-source-han-sans-kr-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-kr-fonts) - 思源黑体韩文部分
*   [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk) - 韩文 TrueType 字体集合
*   [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/) - Nanum 系列 TrueType 字体
*   [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) - Nanum 系列 TrueType 等宽字体
*   [ttf-d2coding](https://aur.archlinux.org/packages/ttf-d2coding/) - 由 Naver 制作的 TrueType 等宽字体
*   [spoqa-han-sans](https://aur.archlinux.org/packages/spoqa-han-sans/) - 由 Spoqa 定制的 Source Han Sans 字体。

#### 阿拉伯和乌尔都文字

*   [ttf-qurancomplex-fonts](https://aur.archlinux.org/packages/ttf-qurancomplex-fonts/) - 位于麦地那的 King Fahd Glorious Quran Printing Complex 制作的字体
*   [ttf-amiri](https://aur.archlinux.org/packages/ttf-amiri/) - 一个典型的阿拉伯文誊抄体 (Naskh) 字体，一开始由 Amiria Press 采用
*   [ttf-sil-lateef](https://aur.archlinux.org/packages/ttf-sil-lateef/) - 来自 SIL 的 Unicode 阿拉伯文字体
*   [ttf-sil-scheherazade](https://aur.archlinux.org/packages/ttf-sil-scheherazade/) - 来自 SIL 的 Unicode 阿拉伯文字体
*   [ttf-arabeyes-fonts](https://aur.archlinux.org/packages/ttf-arabeyes-fonts/) - 自由的阿拉伯文字体集合
*   [ttf-urdufonts](https://aur.archlinux.org/packages/ttf-urdufonts/) - Urdu 字体

#### 波斯文字

*   [ttf-irfonts](https://aur.archlinux.org/packages/ttf-irfonts/) - 伊朗信息与通信技术高级理事会(SCICT)的官方标准波斯字体集
*   [ttf-borna](https://aur.archlinux.org/packages/ttf-borna/) - Borna Rayaneh 波斯 B 字体系列
*   [ttf-x2](https://aur.archlinux.org/packages/ttf-x2/) - X 系列 2 字体是建立在开源可使用的字体基础上并扩展支持波斯语，阿拉伯语，乌尔都语，普什图语，达里语，乌兹别克语，库尔德语，维吾尔语，老土耳其（奥斯曼）和现代土耳其（罗马）.
*   [ttf-iran-nastaliq](https://aur.archlinux.org/packages/ttf-iran-nastaliq/) - 由伊朗信息高级理事会公布的一款 Unicode 书法字体

#### 缅甸文字

*   [ttf-myanmar-fonts](https://aur.archlinux.org/packages/ttf-myanmar-fonts/) - 源自myordbok.com的121款字体*(AUR)*

#### 西里尔文字

另请参阅[#等宽字体](#.E7.AD.89.E5.AE.BD.E5.AD.97.E4.BD.93)、[#无衬线字体](#.E6.97.A0.E8.A1.AC.E7.BA.BF.E5.AD.97.E4.BD.93)和[#衬线字体](#.E8.A1.AC.E7.BA.BF.E5.AD.97.E4.BD.93)

*   [ttf-paratype](https://aur.archlinux.org/packages/ttf-paratype/) - ParaType类别的字体: sans, serif, mono, 扩展的西里尔和拉丁文字, OFL 认证

#### 希腊文字

几乎所有 Unicode 字体都包含希腊代码集 (也包含多调变音符号)，某些额外字体包虽然未包含完整的 Unicode 集，但拥有高质量的希腊字字形 (也包含拉丁字)：

*   [otf-gfs](https://aur.archlinux.org/packages/otf-gfs/) - 由 Greek Font Society 选用的 OpenType 字体
*   [ttf-mgopen](https://aur.archlinux.org/packages/ttf-mgopen/) - 来自 Magenta 的专业 TrueType 字体

#### 希伯来文字

*   [culmus](https://aur.archlinux.org/packages/culmus/) - 自由的希伯来文字体集合

#### 印地文字

*   [ttf-freebanglafont](https://www.archlinux.org/packages/?name=ttf-freebanglafont) - 孟加拉文字体
*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf) - 印地文 OpenType 字体集合 (包含 ttf-freebanglafont)

	(This one contains a "look of disapproval" that might be more to your liking than the [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont) one mentioned elsewhere in this document)

*   [lohit-fonts](https://aur.archlinux.org/packages/lohit-fonts/) - 来自 Fedora 专案的印地文 TrueType 字体 (包含 Oriya 字体以及更多)
*   [ttf-devanagarifonts](https://aur.archlinux.org/packages/ttf-devanagarifonts/) - 梵文TrueType字体(包含 283 种字体)
*   [ttf-gujrati-fonts](https://aur.archlinux.org/packages/ttf-gujrati-fonts/) - TTF 古吉拉特 fonts (Avantika,Gopika,Shree768)
*   [ttf-gurmukhi-fonts_sikhnet](https://aur.archlinux.org/packages/ttf-gurmukhi-fonts_sikhnet/) - TrueType Gurmukhi fonts (gurbaniwebthick,prabhki)
*   [ttf-gurmukhi_punjabi](https://aur.archlinux.org/packages/ttf-gurmukhi_punjabi/) - TTF Gurmukhi / Punjabi (contains 252 fonts)
*   [ttf-kannada-font](https://aur.archlinux.org/packages/ttf-kannada-font/) - Kannada, the language of Karnataka state in India
*   [ttf-tamil](https://aur.archlinux.org/packages/ttf-tamil/) - Tamil Unicode fonts

#### 高棉文字

*   [ttf-khmer](https://www.archlinux.org/packages/?name=ttf-khmer) - 涵盖高棉语 (Khmer) 文字的字体
*   [Hanuman](https://www.google.com/fonts/specimen/Hanuman) ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))

#### 僧伽罗文字

*   [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/) - 僧伽罗文 (Sinhala) Unicode 字体

#### 塔米尔文字

*   [ttf-tamil](https://aur.archlinux.org/packages/ttf-tamil/) - 塔米尔文 (Tamil) Unicode 字体

#### 藏文字

*   [ttf-tibetan-machine](https://www.archlinux.org/packages/?name=ttf-tibetan-machine) - 藏文 (Tibetan) Machine TTFont

### Microsoft 字体

参阅[微软字体](/index.php/Microsoft_fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Microsoft fonts (简体中文)")。

### Apple OS X 字体

*   [ttf-mac-fonts](https://aur.archlinux.org/packages/ttf-mac-fonts/) - Mac OS X TrueType 字体
*   [ttf-mac](https://aur.archlinux.org/packages/ttf-mac/) - Mac OS X TrueType 字体。这个软件包没有内含 ttf 字体 (只有 otf 字体)，用户必须自备这些字体。

### 等宽字体

建议：每位用户偏爱的字体不尽不同，如想找到您心目中的理想字体，还请多加尝试。 如果您没有太多时间，可以阅读 Dan Benjamin 博客的文章：[十大最适合编程的字体](http://hivelogic.com/articles/top-10-programming-fonts)（英文）。

这里内还有 Trevor Lowing 整理的一长串字体清单：[http://www.lowing.org/fonts/](http://www.lowing.org/fonts/) （英文）。

Slant 上的字体图片比较: [最好的编程字体是什么？](http://www.slant.co/topics/67/~what-are-the-best-programming-fonts)（英文）

还有 Stack Overflow 上的带一些图片的回答： [推荐编程字体](http://stackoverflow.com/questions/4689/recommended-fonts-for-programming)（英文）。

#### TrueType 字体

*   Agave ([ttf-agave](https://aur.archlinux.org/packages/ttf-agave/))
*   [Andalé Mono](https://en.wikipedia.org/wiki/zh:Andal%C3%A9_Mono "wikipedia:zh:Andalé Mono") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Anka/Coder ([ttf-anka-coder](https://aur.archlinux.org/packages/ttf-anka-coder/))
*   [Anonymous Pro](http://www.marksimonson.com/fonts/view/anonymous-pro) ([ttf-anonymous-pro](https://www.archlinux.org/packages/?name=ttf-anonymous-pro)，也包含在 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 和 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [Bitstream Vera Mono](https://en.wikipedia.org/wiki/zh:Bitstream_Vera "wikipedia:zh:Bitstream Vera") ([ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera))
*   [Consolas](https://en.wikipedia.org/wiki/zh:Consolas "wikipedia:zh:Consolas") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)) - Windows 下的编程用字体
*   [Courier New](https://en.wikipedia.org/wiki/zh:Courier "wikipedia:zh:Courier") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Cousine ([ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/) 或 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 或 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS 的 Courier New 替换 (metric-compatible)
*   [DejaVu Sans Mono](https://en.wikipedia.org/wiki/zh:DejaVu%E5%AD%97%E4%BD%93 "wikipedia:zh:DejaVu字体") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans Mono](https://en.wikipedia.org/wiki/zh:Droid "wikipedia:zh:Droid") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)，也包含在 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 和 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   Envy Code R ([ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/))
*   Fantasque Sans Mono ([ttf-fantasque-sans](https://aur.archlinux.org/packages/ttf-fantasque-sans/) 或 [ttf-fantasque-sans-git](https://aur.archlinux.org/packages/ttf-fantasque-sans-git/))
*   [FreeMono](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Inconsolata](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata](https://www.archlinux.org/packages/?name=ttf-inconsolata)) - 极佳的编程用字体
*   [Inconsolata-g](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata-g](https://aur.archlinux.org/packages/ttf-inconsolata-g/)) - 加入一些亲近编程人员的调整
*   [Liberation Mono](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - 取代 Courier New，基于Cousine (metric-compatible)。
*   [Lucida Typewriter](https://en.wikipedia.org/wiki/Lucida_Typewriter "wikipedia:Lucida Typewriter") (包含于 [jre](https://aur.archlinux.org/packages/jre/) 软件包)
*   [Monaco](https://en.wikipedia.org/wiki/zh:Monaco "wikipedia:zh:Monaco") ([ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco/)) - OSX/Textmate 下知名的编程用字体
*   Monofur ([ttf-monofur](https://aur.archlinux.org/packages/ttf-monofur/))
*   [Source Code Pro](https://en.wikipedia.org/wiki/Source_Code_Pro "wikipedia:Source Code Pro") ([adobe-source-code-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-code-pro-fonts))

#### 点阵字体

*   Default 8x16
*   Dina ([dina-font](https://www.archlinux.org/packages/?name=dina-font))
*   [Gohu](http://font.gohu.org/) ([gohufont](https://aur.archlinux.org/packages/gohufont/))
*   Lime ([artwiz-fonts](https://www.archlinux.org/packages/?name=artwiz-fonts))
*   [ProFont](https://en.wikipedia.org/wiki/ProFont "wikipedia:ProFont") ([profont](https://www.archlinux.org/packages/?name=profont))
*   [Proggy Programming Fonts](https://en.wikipedia.org/wiki/Proggy_Programming_Fonts "wikipedia:Proggy Programming Fonts") ([proggyfonts](https://aur.archlinux.org/packages/proggyfonts/))
*   Proggy opti cyrillic ([proggyopticyr-font](https://aur.archlinux.org/packages/proggyopticyr-font/))
*   Tamsyn ([tamsyn-font](https://www.archlinux.org/packages/?name=tamsyn-font))
*   [Terminus](http://terminus-font.sourceforge.net/) ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font))
*   Unifont (glyphs like (look of disapproval)) ([bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont))

### 无衬线字体

*   [Andika](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=andika) ([ttf-andika](https://aur.archlinux.org/packages/ttf-andika/)，包含于 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/))
*   [Arial](https://en.wikipedia.org/wiki/zh:Arial "wikipedia:zh:Arial") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Arial Black](https://en.wikipedia.org/wiki/zh:Arial "wikipedia:zh:Arial") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Arimo ([ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/) 或 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 或 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS 的 Arial 替换 (metric-compatible)
*   [Calibri](https://en.wikipedia.org/wiki/zh:Calibri "wikipedia:zh:Calibri") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Candara](https://en.wikipedia.org/wiki/zh:Candara "wikipedia:zh:Candara") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [DejaVu Sans](https://en.wikipedia.org/wiki/zh:DejaVu%E5%AD%97%E4%BD%93 "wikipedia:zh:DejaVu字体") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans](https://en.wikipedia.org/wiki/zh:Droid "wikipedia:zh:Droid") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)，包含于 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 和 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSans](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Sans](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)，取代 Arial, 基于 Arimo (metric-compatible)
*   [Linux Biolinum](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine))
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [PT Sans](https://en.wikipedia.org/wiki/PT_Sans "wikipedia:PT Sans") ([ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 或 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - 3 种主要变体：正常、变窄与标题 - Unicode：拉丁字、西里尔字
*   [Source Sans Pro](https://en.wikipedia.org/wiki/Source_Sans_Pro "wikipedia:Source Sans Pro") ([adobe-source-sans-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-sans-pro-fonts))
*   [Tahoma](https://en.wikipedia.org/wiki/zh:Tahoma_(typeface) ([ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/))
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Ubuntu-Title](https://en.wikipedia.org/wiki/Ubuntu-Title "wikipedia:Ubuntu-Title") ([ttf-ubuntu-title](https://aur.archlinux.org/packages/ttf-ubuntu-title/))
*   [Ubuntu Font Family](https://en.wikipedia.org/wiki/Ubuntu_Font_Family "wikipedia:Ubuntu Font Family") ([ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family))
*   [Verdana](https://en.wikipedia.org/wiki/zh:Verdana "wikipedia:zh:Verdana") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### 手写体

*   [Comic Sans](https://en.wikipedia.org/wiki/zh:Comic_Sans "wikipedia:zh:Comic Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### 衬线字体

*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Charis](https://en.wikipedia.org/wiki/Charis_SIL "wikipedia:Charis SIL") ([ttf-charis](https://aur.archlinux.org/packages/ttf-charis/)，包含于 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode：拉丁字、西里尔字
*   [DejaVu Serif](https://en.wikipedia.org/wiki/zh:DejaVu%E5%AD%97%E4%BD%93 "wikipedia:zh:DejaVu字体") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Doulos](https://en.wikipedia.org/wiki/Doulos_SIL "wikipedia:Doulos SIL") ([doulos-sil](https://aur.archlinux.org/packages/doulos-sil/)，包含于 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode：拉丁字、西里尔字
*   [Droid Serif](https://en.wikipedia.org/wiki/zh:Droid "wikipedia:zh:Droid") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)，包含于 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 和 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSerif](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Gentium](https://en.wikipedia.org/wiki/Gentium "wikipedia:Gentium") ([ttf-gentium](https://www.archlinux.org/packages/?name=ttf-gentium)，包含于 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode：拉丁字、希腊字、西里尔字、音标字母
*   [Georgia](https://en.wikipedia.org/wiki/zh:Georgia_(%E5%AD%97%E5%9E%8B) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Serif](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - 取代 Times New Roman，基于Tinos (metric-compatible)
*   [Linux Libertine](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) - Unicode：拉丁字、希腊字、西里尔字、希伯来字
*   [Times New Roman](https://en.wikipedia.org/wiki/zh:Times_New_Roman "wikipedia:zh:Times New Roman") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Tinos ([ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/) 或 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 或 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS 的 Times New Roman 替换 (metric-compatible)

### 未分类字体

*   [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/) 与 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) — 一个免费字体的大合集（囊括里 ubuntu、inconsolata、droid 等字体）-注意：如果安装这个包，您的系统内将添加 100 多个字体，这将会使您的字体对话框变得很长。[ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 会从上游网络字体项目中拖下整个 Mercurial 库。[ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)则会从 Git 中拖下一个更小，更精简的非官方库。*(AUR)*
*   [ttf-mph-2b-damase](https://www.archlinux.org/packages/?name=ttf-mph-2b-damase) — Covers full plane 1 and several scripts
*   [ttf-symbola](https://www.archlinux.org/packages/?name=ttf-symbola) — 提供了绘文字及其它一些符号。
*   [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/) — STL 内的 Gentium, Charis, Doulos, Andika and Abyssinica *(AUR)*
*   [font-bh-ttf](https://www.archlinux.org/packages/?name=font-bh-ttf) — X.Org Luxi 字体
*   [ttf-cheapskate](https://www.archlinux.org/packages/?name=ttf-cheapskate) — 从 *dustismo.com* 收集来的字体库
*   [ttf-isabella](https://aur.archlinux.org/packages/ttf-isabella/) — 一款书法字体，基于 1497 年的 *Isabella Breviary*
*   [ttf-junicode](https://www.archlinux.org/packages/?name=ttf-junicode) — Junius 字体，几乎包括了所有中世纪的拉丁文字形
*   arkpandorafonts [ttf-arkpandora](https://aur.archlinux.org/packages/ttf-arkpandora/) — Arial 与 Times New Roman 字体的一个替代字体 *(AUR)*
*   [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) — IBM Courier 和 Adobe Utopia 的 [PostScript 字体](https://en.wikipedia.org/wiki/PostScript_fonts "wikipedia:PostScript fonts")

## X11中的字体回滚顺序

Fontconfig 会自动选择一个符合当前场景的字体。也就是说，如果有人正在浏览一个既有英文又有中文的窗口，而默认的字体不支持中文，它会自动切换到另一种字体以便显示中文。

Fontconfig 让每个用户能够通过`$XDG_CONFIG_HOME/fontconfig/fonts.conf`来调整字体被使用的顺序。 如果你想要在最喜欢的Serif字体之后使用某个特定的中文字体，你的配置文件看起来会是这样：

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
<alias>
   <family>serif</family>
   <prefer>
     <family>你喜欢的拉丁衬线字体名称</family>
     <family>你的中文衬线字体名称</family>
   </prefer>
 </alias>
</fontconfig>

```

当然你也可以为 Sans-serif和 monospace 字体像上面一样添加一段。更多信息请参考 fontconfig 说明。

## 字体别名

在 Linux 系统中有几种字体别名，它们实际代表着别的字体，这样以达到让应用程序的字体看起来类似。最常见的别名有：`serif` 代表一种[衬线体](https://en.wikipedia.org/wiki/zh:%E8%A1%AC%E7%BA%BF%E4%BD%93 "wikipedia:zh:衬线体")（关于衬线体与非衬线体概念请参考[UbuntuCN:字体#基础知识](http://wiki.ubuntu.org.cn/%E5%AD%97%E4%BD%93#.E5.9F.BA.E7.A1.80.E7.9F.A5.E8.AF.86)——译注）（例如 DejaVu Serif、宋体）；`sans-serif`代表一种[无衬线体](https://en.wikipedia.org/wiki/zh:%E6%97%A0%E8%A1%AC%E7%BA%BF%E4%BD%93 "wikipedia:zh:无衬线体")（例如 DejaVu Sans 和各种黑体）；而`monospace` 则代表[等宽字体](https://en.wikipedia.org/wiki/zh:%E7%AD%89%E5%AE%BD%E5%AD%97%E4%BD%93 "wikipedia:zh:等宽字体")（例如 DejaVu Sans Mono）。 然而，这些别名所代表的字体有可能会变化，而且通常 KDE 和其他桌面环境中的字体管理工具不会显示其内在联系。

如果想通过别名反向查找是哪种字体被展现出来，运行：

```
$ fc-match monospace
DejaVuSansMono.ttf: "DejaVu Sans Mono" "Book"

```

在这种情况下 Monospace 别名展现的是 DejaVuSansMono.ttf 字体。

## 小提示

### 列出已安装字体

你可以使用以下命令来列出当前系统中所有已安装字体的字体：

```
$ fc-list

```

### 应用程序专用的字体高速缓冲

Matplotlib ([python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib) 或 [python2-matplotlib](https://www.archlinux.org/packages/?name=python2-matplotlib)) 使用自己的字体高速缓冲，因此更新字体后记得删除 `$HOME/.matplotlib/fontList.cache`，`$HOME/.cache/matplotlib/fontList.cache`, `$HOME/.sage/matplotlib-1.2.1/fontList.cache` 等文件。这样它才会再一次产生高速缓冲并找到新字体 [[4]](http://matplotlib.1069221.n5.nabble.com/getting-matplotlib-to-recognize-a-new-font-td40500.html)。

## 参见

*   [State of Text Rendering](http://behdad.org/text/)