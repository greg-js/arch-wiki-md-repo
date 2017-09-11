**翻译状态：** 本文是英文页面 [Font_Configuration](/index.php/Font_Configuration "Font Configuration") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-06-07，点击[这里](https://wiki.archlinux.org/index.php?title=Font_Configuration&diff=0&oldid=229345)可以查看翻译后英文页面的改动。

相关文章

*   [字体](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fonts (简体中文)")
*   [Java Runtime Environment Fonts](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")
*   [MS Fonts](/index.php/MS_Fonts "MS Fonts")
*   [Font configuration/Examples](/index.php/Font_configuration/Examples "Font configuration/Examples")

Fontconfig 是一个为应用程序提供可用 [字体](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fonts (简体中文)") 的程序库，也可用来配置字体渲染效果，参见[fontconfig](https://www.archlinux.org/packages/?name=fontconfig) 软件包和 [Wikipedia:Fontconfig](https://en.wikipedia.org/wiki/Fontconfig "wikipedia:Fontconfig")。Free type 库([freetype2](https://www.archlinux.org/packages/?name=freetype2) 软件包)就是以此为配置基础来渲染字体。

尽管 Fontconfig 已经是当今 Linux 字体界的标准，但是仍有一部分应用使用更加原始的字体显示方法，[X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description")。

Arch Linux 上的字体渲染包支持有字节码解释器(BCI)的*freetype2*。为了更好的字体渲染，特别是在 LCD 显示器上，一些补丁包也添加到库中，参见下面的 [#补丁包](#.E8.A1.A5.E4.B8.81.E5.8C.85)。[#Infinality](#Infinality) 包同时支持自动微调和亚像素渲染，允许在无须重新编译的情况下微调LCD滤光器，而且在粗体字下自动微调仍然表现良好。

## Contents

*   [1 字体路径](#.E5.AD.97.E4.BD.93.E8.B7.AF.E5.BE.84)
*   [2 Fontconfig配置](#Fontconfig.E9.85.8D.E7.BD.AE)
    *   [2.1 预设](#.E9.A2.84.E8.AE.BE)
    *   [2.2 抗锯齿](#.E6.8A.97.E9.94.AF.E9.BD.BF)
    *   [2.3 微调](#.E5.BE.AE.E8.B0.83)
        *   [2.3.1 字节码解释器(BCI)](#.E5.AD.97.E8.8A.82.E7.A0.81.E8.A7.A3.E9.87.8A.E5.99.A8.28BCI.29)
        *   [2.3.2 自动微调器](#.E8.87.AA.E5.8A.A8.E5.BE.AE.E8.B0.83.E5.99.A8)
        *   [2.3.3 微调样式](#.E5.BE.AE.E8.B0.83.E6.A0.B7.E5.BC.8F)
    *   [2.4 亚像素渲染](#.E4.BA.9A.E5.83.8F.E7.B4.A0.E6.B8.B2.E6.9F.93)
        *   [2.4.1 LCD过滤器](#LCD.E8.BF.87.E6.BB.A4.E5.99.A8)
        *   [2.4.2 高级LCD过滤器说明](#.E9.AB.98.E7.BA.A7LCD.E8.BF.87.E6.BB.A4.E5.99.A8.E8.AF.B4.E6.98.8E)
    *   [2.5 取消粗体字的自动微调功能](#.E5.8F.96.E6.B6.88.E7.B2.97.E4.BD.93.E5.AD.97.E7.9A.84.E8.87.AA.E5.8A.A8.E5.BE.AE.E8.B0.83.E5.8A.9F.E8.83.BD)
    *   [2.6 只对较大的字体打开反锯齿功能](#.E5.8F.AA.E5.AF.B9.E8.BE.83.E5.A4.A7.E7.9A.84.E5.AD.97.E4.BD.93.E6.89.93.E5.BC.80.E5.8F.8D.E9.94.AF.E9.BD.BF.E5.8A.9F.E8.83.BD)
    *   [2.7 字体替换](#.E5.AD.97.E4.BD.93.E6.9B.BF.E6.8D.A2)
    *   [2.8 禁用点阵字型](#.E7.A6.81.E7.94.A8.E7.82.B9.E9.98.B5.E5.AD.97.E5.9E.8B)
    *   [2.9 禁用点阵字体的缩放](#.E7.A6.81.E7.94.A8.E7.82.B9.E9.98.B5.E5.AD.97.E4.BD.93.E7.9A.84.E7.BC.A9.E6.94.BE)
    *   [2.10 为不完善的字体构建粗体风格和斜体风格](#.E4.B8.BA.E4.B8.8D.E5.AE.8C.E5.96.84.E7.9A.84.E5.AD.97.E4.BD.93.E6.9E.84.E5.BB.BA.E7.B2.97.E4.BD.93.E9.A3.8E.E6.A0.BC.E5.92.8C.E6.96.9C.E4.BD.93.E9.A3.8E.E6.A0.BC)
    *   [2.11 改变规则重定义机制](#.E6.94.B9.E5.8F.98.E8.A7.84.E5.88.99.E9.87.8D.E5.AE.9A.E4.B9.89.E6.9C.BA.E5.88.B6)
    *   [2.12 fontconfig配置的例子](#fontconfig.E9.85.8D.E7.BD.AE.E7.9A.84.E4.BE.8B.E5.AD.90)
*   [3 补丁包](#.E8.A1.A5.E4.B8.81.E5.8C.85)
    *   [3.1 Infinality](#Infinality)
    *   [3.2 Ubuntu](#Ubuntu)
    *   [3.3 恢复到未打补丁的包](#.E6.81.A2.E5.A4.8D.E5.88.B0.E6.9C.AA.E6.89.93.E8.A1.A5.E4.B8.81.E7.9A.84.E5.8C.85)
*   [4 没有fontconfig支持的应用程序](#.E6.B2.A1.E6.9C.89fontconfig.E6.94.AF.E6.8C.81.E7.9A.84.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
*   [5 字体问题解决方法](#.E5.AD.97.E4.BD.93.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3.E6.96.B9.E6.B3.95)
    *   [5.1 字体扭曲](#.E5.AD.97.E4.BD.93.E6.89.AD.E6.9B.B2)
    *   [5.2 较旧的GTK和QT应用程序](#.E8.BE.83.E6.97.A7.E7.9A.84GTK.E5.92.8CQT.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
*   [6 资源](#.E8.B5.84.E6.BA.90)

## 字体路径

由于应用程序需要知道它们所使用的字体的位置，所以必须对字体做良好的编目，以便于应用程序更好更快的访问它们。

Fontconfig包含的字体路径是`/usr/share/fonts/`和`~/.fonts/`(Fontconfig会递归访问上述目录)。为了简化管理和安装过程，当需要[添加字体](/index.php/Fonts#Installation "Fonts")时，推荐使用上述路径。

查看Fontconfig所包含的字体：

```
$ fc-list : file

```

参见[fc-list(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fc-list.1)以获得更多输出格式方面的信息。

通过考察Xorg的log文件来检查Xorg包含的字体路径:

```
$ grep /fonts /var/log/Xorg.0.log

```

**提示：** 你也可以通过命令`xset q`检查Xorg包含的字体路径。

需要明确的是，Xorg不会像Fontconfig一样递归搜索`/usr/share/fonts/`目录。如果要增加一个目录，必须使用一个完整目录：

```
Section "Files"
    FontPath     "/usr/share/fonts/local/"
EndSection

```

如果你想把字体路径设置到每一位用户，你可以通过添加下面的配置代码到文件`~/.xinitrc`，这样可以将字体路径添加进或者移除出默认的路径中：

```
xset +fp /usr/share/fonts/local/           # Prepend a custom font path to Xorg's list of known font paths
xset -fp /usr/share/fonts/sucky_fonts/     # Remove the specified font path from Xorg's list of known font paths

```

如果要查看Xorg包含的字体，可以使用这个命令`xlsfonts`, 这个命令来自包[xorg-xlsfonts](https://www.archlinux.org/packages/?name=xorg-xlsfonts)。

## Fontconfig配置

通过对`$XDG_CONFIG_HOME/fontconfig/fonts.conf`的修改可以完成对某个用户的配置, 而对`/etc/fonts/local.conf`的修改则可以完成对每一位用户的配置． 如果用户的单独配置和全局配置不同，系统优先使用前者. 这些文件共用相同的语法.

**Note:** 配置文件和目录: `~/.fonts.conf`, `~/.fonts.conf.d` 和 `~/.fontconfig/*.cache-*` 从fontconfig 2.10.1开始已经被废弃([upstream commit](http://cgit.freedesktop.org/fontconfig/commit/?id=8c255fb185d5651b57380b0a9443001e8051b29d)) 未来的版本也不会默认读取这些文件当作配置依据. 分别用 `$XDG_CONFIG_HOME/fontconfig/fonts.conf`, `$XDG_CONFIG_HOME/fontconfig/conf.d` 和`$XDG_CACHE_HOME/fontconfig/*.cache-*` 来代替.

Fontconfig 把所有的配置都放在一个中心文件中 (`/etc/fonts/fonts.conf`). 这个文件会在fontconfig更新时被替换，注意你不应该编辑这个文件. 字体设置重要的程序会引用这个文件以获得当前字体配置和渲染配置．这个文件是一系列配置规则的集合包括全局配置文件(`/etc/fonts/local.conf`), 预设的配置 `/etc/fonts/conf.d/`, 和用户的配置文件 (`$XDG_CONFIG_HOME/fontconfig/fonts.conf`).

**Note:** 有一些桌面环境 (比如说 [GNOME](/index.php/GNOME "GNOME") 和 [KDE](/index.php/KDE "KDE")) 使用 *Font Control Panel* 会自动生成和重写用户字体配置文件. 对于这些桌面环境, 最好配合已定义的字体配置来得到需要的显示效果．

配置文件使用[XML](https://en.wikipedia.org/wiki/XML "wikipedia:XML")格式并且需要一些格式头:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- settings go here -->

</fontconfig>

```

文中的配置示例省略了这些标签．

在线的字体配置请点击[此处](http://wenq.org/cloud/fcdesigner_local.html)。

### 预设

预设配置放在目录`/etc/fonts/conf.avail`中. 当给它们创建了[符号链接](https://en.wikipedia.org/wiki/Symbolic_link "wikipedia:Symbolic link"), 这些配置就被激活了．不管是对某一个用户还是全局配置, 这一规则是相同的．在`/etc/fonts/conf.d/README`中有描述. 这些预设会通过匹配它们原先它们的单独设置文件来覆盖配置．

举个例子，为了打开全局亚像素RGB渲染:

```
# cd /etc/fonts/conf.d
# ln -s ../conf.avail/10-sub-pixel-rgb.conf

```

为单个独立用户配置:

```
$ mkdir $XDG_CONFIG_HOME/fontconfig/conf.d
$ ln -s /etc/fonts/conf.avail/10-sub-pixel-rgb.conf $XDG_CONFIG_HOME/fontconfig/conf.d

```

### 抗锯齿

[字体光栅化](https://en.wikipedia.org/wiki/Font_rasterization "wikipedia:Font rasterization")将矢量字体数据转化为位图数据以显示在屏幕上． 最后的效果可能由于[走样](https://en.wikipedia.org/wiki/Aliasing "wikipedia:Aliasing")会出现锯齿. [抗锯齿](https://en.wikipedia.org/wiki/Anti-aliasing "wikipedia:Anti-aliasing")默认被打开，这样可以增加字体边缘的分辨率.

```
  <match target="font">
    <edit name="antialias" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

### 微调

[字体微调](https://en.wikipedia.org/wiki/Font_hinting "wikipedia:Font hinting") (也叫做instructing) 是利用精确的指令来调整字体显示的轮廓，这样就可以用离散的网格来显示我们需要的线条, 比如说像素网格．字体在[DPI](https://en.wikipedia.org/wiki/Dots_per_inch "wikipedia:Dots per inch")达到300之前不可能正确的显示．我们有两种微调的方法可以用.

#### 字节码解释器(BCI)

当用BCI方法时，TrueType字体里的指令就会被唤醒并用FreeTypes的解释器来渲染，这在自带良好微调指令的字体上工作的很好．

打开normal hinting:

```
  <match target="font">
    <edit name="hinting" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

#### 自动微调器

自动微调器方法就是微调全自动并且忽视任何内嵌的微调指令，起初这种方法是缺省配置的，因为以前的TrueType2字体都是有专利保护限制，没办法用BCI方法微调，但是现在这些专利都已经过期，所以限制也就没有了，当然也就是没有多大意义用自动微调这种方法了。但是它对内嵌微调指令不完整或者干脆没有的字体非常管用，相对的，如果字体自身有良好的微调指令，这种方法就绝对不提倡了。现如今，一般字体都有不错的微调指令，所以自动微调器这种方法就没多大用武之地。

打开自动微调(auto-hinting):

```
  <match target="font">
    <edit name="autohint" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

#### 微调样式

微调样式就是微调时可以采用的款式，包括`hintfull`, `hintmedium`, `hintslight` 还有 `hintnone`。至于效果，`hintslight`可以较好的保持字体的形态但是在像素网格里的排列会有些模糊，`hintfull`则相反，排列清晰但字体的体态就不慎清楚。所以如果用BCI微调法，就推荐用`hintfull`，自动微调的话就`hintslight`了。

```
  <match target="font">
    <edit name="hintstyle" mode="assign">
      <const>hintfull</const>
    </edit>
  </match>

```

**Note:** Some applications, like [GNOME 3](/index.php/GNOME "GNOME") may [override default hinting settings.](#Troubleshooting)

### 亚像素渲染

如今生产的显示器大部分用的是红绿蓝（RGB）规范，也有用**BGR**, **V-RGB** (vertical), 或者 **V-BGR**规范的（具体什么类型可以[这里](http://www.lagom.nl/lcd-test/subpixel.php)查看）。为了正确显示字体，Fontconfig得知道你的显示器具体类型。

打开亚像素渲染:

```
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>rgb</const>
    </edit>
  </match>

```

**Note:** Subpixel rendering effectively triples the horizontal (or vertical) resolution for fonts by making use of subpixels. The autohinter and subpixel rendering are not designed to work together and should not be used in combination without the [Infinality](#Infinality:_the_generic_way) patch set.

#### LCD过滤器

当使用亚像素渲染时，你最好启用LCD过滤器，这个是设计用来减少彩色边纹现象的，具体解释参见FreeType 2 API参考里的[LCD filtering](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html)。它的各个不同选项的描述位于[FT_LcdFilter](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html#FT_LcdFilter)，具体实例看[LCD filter test](http://www.spasche.net/files/lcdfiltering/)。

`lcddefault`这个选项对大多数用户都适用，其他选项则都有某一特定的用途：`lcdlight`对那些字体看起来太粗或者模糊的超管用，`lcdlegacy`嘛可用来对付Cairo字体，而`lcdnone`的意思则是完全禁用`LCD过滤器`功能。

```
  <match target="font">
    <edit mode="assign" name="lcdfilter">
      <const>lcddefault</const>
    </edit>
  </match>

```

#### 高级LCD过滤器说明

如果对内置的`LCD过滤器`不满意，那可以自己对字体渲染来一个360度微调，只要修改下硬编码了的过滤器|filters并创建一个自定义的freetype2软件包就可以了。[Arch Build System](/index.php/Arch_Build_System "Arch Build System")就是用来从源文件创建并安装软件包的一个工具。

首先，以root用户刷新下freetype2的PKGBUILD文件：

```
# abs extra/freetype2

```

**Note:** 下面这个示例以`/var/abs/build`作为编译目录，请根据各自的ABS设置值来替换。

然后切换回普通用户，下载并解压freetype2软件包：

```
$ cd /var/abs/build
$ cp -r ../extra/freetype2 .
$ cd freetype2
$ makepkg -o

```

接着编辑一下`src/freetype-VERSION/src/base/ftlcdfil.c`这个文件，看看`default_filter[5]`这个变量是怎么定义的：

```
static const FT_Byte  default_filter[5] =
    { 0x10, 0x40, 0x70, 0x40, 0x10 };

```

上面这个变量定义了一个应用于rendered glyph的低通过滤器|filter，请根据需要修改，然后保存、创建并安装这个自定义软件包：

```
$ makepkg -e
$ sudo pacman -Rd freetype2
$ sudo pacman -U freetype2-VERSION-ARCH.pkg.tar.xz

```

最后重启机器或者重启X服务器，`lcddefault`这个过滤器字体渲染的效果应该就出来了。

### 取消粗体字的自动微调功能

`自动微调`使用了很复杂的方法来渲染字体，但常常把粗体字弄得太宽了，好在有一个方法，可以让`自动微调`在粗体字上不起作用的同时而不影响其他字体：

```
...
<match target="font">
    <test name="weight" compare="more">
        <const>medium</const>
    </test>
    <edit name="autohint" mode="assign">
        <bool>false</bool>
    </edit>
</match>
...

```

### 只对较大的字体打开反锯齿功能

有些用户更偏爱锐利一点的渲染效果而不是反锯齿那样的：

```
...
<match target="font">
    <edit name="antialias" mode="assign">
        <bool>false</bool>
    </edit>
</match>

<match target="font" >
    <test name="size" qual="any" compare="more">
        <double>12</double>
    </test>
    <edit name="antialias" mode="assign">
        <bool>true</bool>
    </edit>
</match>

<match target="font" >
    <test name="pixelsize" qual="any" compare="more">
        <double>16</double>
    </test>
    <edit name="antialias" mode="assign">
        <bool>true</bool>
    </edit>
</match>
...

```

### 字体替换

最可靠的方法是添加像下面那样的一个XML片段。关键点在于*使用“binding”属性可以有更好的效果*，例如在Firefox你可能只想替换字体但并不想改变被替换字体的属性。下面的例子演示的是Georgia如何被Ubuntu字体替换掉的：

```
...
 <match target="pattern">
   <test qual="any" name="family"><string>georgia</string></test>
   <edit name="family" mode="assign" binding="same"><string>Ubuntu</string></edit>
 </match>
...

```

另外一种方法是设置“优先”字体，但是*这只有在原字体系统缺失的情况下才有效*，这种情况真发生了的话，设定的字体就会把它换了：

```
...
< !-- Replace Helvetica with Bitstream Vera Sans Mono -->
< !-- Note, an alias for Helvetica should already exist in default conf files -->
<alias>
    <family>Helvetica</family>
    <prefer><family>Bitstream Vera Sans Mono</family></prefer>
    <default><family>fixed</family></default>
</alias>
...

```

### 禁用点阵字型

想禁用点阵字体（这个经常是在因为字体缺失而被回滚使用，却导致字体被渲染得很像素化）可以使用`70-no-bitmaps.conf`（fontconfig缺省情况没有内置这个文件）：

```
# cd /etc/fonts/conf.d
# rm 70-yes-bitmaps.conf
# ln -s ../conf.avail/70-no-bitmaps.conf

```

下面的就一行效果也一样：

```
# ln -s /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d/

```

可能你并没有`70-yes-bitmaps.conf`这个文件，所以也就无须什么删除了。 利用下面这个配置文件，你就可以决定用什么字体来替换点阵字体了：

 `~/.config/fontconfig/conf.d/29-replace-bitmap-fonts.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
    <!-- Replace generic bitmap font names by generic font families -->
    <match target="pattern" name="family">
        <test name="family" qual="any">
            <string>Helvetica</string>
        </test>
        <edit mode="assign" name="family">
            <string>Arial</string>
            <string>Liberation Sans</string>
            <string>sans-serif</string>
        </edit>
    </match>
    <match target="pattern" name="family">
        <test name="family" qual="any">
            <string>Courier</string>
        </test>
        <edit mode="assign" name="family">
            <string>Courier New</string>
            <string>Liberation Mono</string>
            <string>monospace</string>
        </edit>
    </match>
    <match target="pattern" name="family">
        <test name="family" qual="any">
            <string>Times</string>
        </test>
        <edit mode="assign" name="family">
            <string>Times New Roman</string>
            <string>Liberation Serif</string>
            <string>serif</string>
        </edit>
    </match>
</fontconfig>

```

禁用所有字体里的点阵字型：
 `~/.config/fontconfig/conf.d/20-no-embedded.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="font">
    <edit name="embeddedbitmap" mode="assign">
      <bool>false</bool>
    </edit>
  </match>
</fontconfig>

```

只禁用特定字体里的点阵字型：

```
<match target="font">
  <test qual="any" name="family">
    <string>Monaco</string>
  </test>
  <edit name="embeddedbitmap"><bool>false</bool></edit>
</match>

```

### 禁用点阵字体的缩放

如果要禁用点阵字体的缩放功能（这个经常会把字搞得很模糊），请删除 `/etc/fonts/conf.d/10-scale-bitmap-fonts.conf`.

### 为不完善的字体构建粗体风格和斜体风格

Freetype字体可以自动为没有*斜体*和**粗体**的字体创建*斜体*和**粗体**，但这只会在应用程序明确地提出这样请求下生效。但现有的程序很少会发出这样的请求，这版讲述如何手动强制生成缺少的字体风格。

按照如下描述编辑`/usr/share/fonts/fonts.cache-1`。因为执行`fc-cache`时会覆盖`/usr/share/fonts/fonts.cache-1`，所以编辑前请先备份`/usr/share/fonts/fonts.cache-1`到其他地方。

假设已经安装了Dupree字体：

```
"dupree.ttf" 0 "Dupree:style=Regular:slant=0:weight=80:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

复制上面一行，并将`style=Regular`改为`style=Bold`或者其他你想要的字体风格（粗体用Bold，斜体用Italic）。同时，若需要斜体的将`slant=0`改为`slant=100`，需要粗体的将`weight=80` 改为`weight=200`，或者你可以将两句组合起来来生成***粗体和斜体***的风格，其中一个示例如下:

```
"dupree.ttf" 0 "Dupree:style=Bold Italic:slant=100:weight=200:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

现在将以下内容添加到`$XDG_CONFIG_HOME/fontconfig/fonts.conf`文件中:

```
...
<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
         <!-- other fonts here .... -->
     </test>
     <test name="weight" compare="more_eq"><int>140</int></test>
     <edit name="embolden" mode="assign"><bool>true</bool></edit>
</match>

<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
        <!-- other fonts here .... -->
    </test>
    <test name="slant" compare="more_eq"><int>80</int></test>
    <edit name="matrix" mode="assign">
        <times>
            <name>matrix</name>
                <matrix>
                    <double>1</double><double>0.2</double>
                    <double>0</double><double>1</double>
                </matrix>
        </times>
    </edit>
</match>
...

```

**提示：** 使用了参数 'embolden' 可以令原来就存在粗体的字体变得更粗

### 改变规则重定义机制

Fontconfig按照文件名中的数字顺序来处理`/etc/fonts/conf.d`里的文件，这样子数值高的规则或者文件就可以覆盖掉低的，但是有时容易让人对什么文件最后处理产生疑惑。

依照下例所示改变一下顺序，以确保“个人配置文件”永远被最后处理：

```
# cd /etc/fonts/conf.d
# mv 50-user.conf 99-user.conf

```

上面这个更改在大部分情况下是非必要的，因为用户本来就被赋予了足够的控制权来设置他喜欢的字体属性、微调和反锯齿，以及把某个字体设置为一个普通字体家族的别名等等。

### fontconfig配置的例子

Fongconfig的配置文件示例请参考这个[页面](/index.php/Font_configuration/Examples "Font configuration/Examples").

下面是一个简单的上手例子：

 `/etc/fonts/local.conf` 
```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
 <match target="font">

  <edit mode="assign" name="rgba">
   <const>rgb</const>
  </edit>

  <edit mode="assign" name="hinting">
   <bool>true</bool>
  </edit>

  <edit mode="assign" name="hintstyle">
   <const>hintfull</const>
  </edit>

  <edit mode="assign" name="antialias">
   <bool>true</bool>
  </edit>

  <edit mode="assign" name="lcdfilter">
    <const>lcddefault</const>
  </edit>

 </match>
</fontconfig>

```

## 补丁包

These patched packages are available in the [AUR](/index.php/Arch_User_Repository "Arch User Repository"). A few considerations:

*   Configuration is usually necessary.
*   The new font rendering will not kick in until applications restart.
*   Applications which [statically link](https://en.wikipedia.org/wiki/Static_library "wikipedia:Static library") to a library will not be affected by patches applied to the system library.

### Infinality

The infinality patchset aims to greatly improve freetype2 font rendering. It adds multiple new capabilities.

*   [Home page](http://www.infinality.net/blog/infinality-freetype-patches/)
*   [Forum](http://www.infinality.net/forum/)
*   [Short article about infinality (contains screenshots)](http://www.webupd8.org/2013/06/better-font-rendering-in-linux-with.html)

Infinality's settings are all configurable at runtime via environment variables in `/etc/profile.d/infinality-settings.sh`, and include the following:

*   **Emboldening Enhancement**: Disables Y emboldening, producing a much nicer result on fonts without bold versions. Works on native TT hinter and autohinter.
*   **Auto-Autohint**: Automatically forces autohint on fonts that contain no TT instructions.
*   **Autohint Enhancement**: Makes autohint snap horizontal stems to pixels. Gives a result that appears like a well-hinted truetype font, but is 100% patent-free (as far as I know).
*   **Customized FIR Filter**: Select your own [filter values](http://www.infinality.net/forum/viewtopic.php?f=2&t=19) at run-time. Works on native TT hinter and autohinter.
*   **Stem Alignment**: Aligns bitmap glyphs to optimized pixel boundaries. Works on native TT hinter and autohinter.
*   **Pseudo Gamma Correction**: Lighten and darken glyphs at a given value, below a given size. Works on native TT hinter and autohinter.
*   **Embolden Thin Fonts**: Embolden thin or light fonts so that they are more visible. Works on autohinter.
*   **Force Slight Hinting**: Force slight hinting even when programs want full hinting. If you use the local.conf I provide (included in infinality-settings fedora package) you will notice nice improvements on @font-face fonts.
*   **ChromeOS Style Sharpening**: ChromeOS uses a patch to sharpen the look of fonts. This is now included in the infinality patchset.

A number of presets are included and can be used by setting the USE_STYLE variable in `/etc/profile.d/infinality-settings.sh`.

[freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/) can be installed from the [AUR](/index.php/Arch_User_Repository "Arch User Repository"). Additionally, if you are using [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2) from [multilib], replace it with [lib32-freetype2-infinality](https://aur.archlinux.org/packages/lib32-freetype2-infinality/) from the AUR. The AUR also contains a Git version of freetype2 that builds the latest development snapshot of freetype2 with the Infinality patchset: [freetype2-infinality-git](https://aur.archlinux.org/packages/freetype2-infinality-git/), [lib32-freetype2-infinality-git](https://aur.archlinux.org/packages/lib32-freetype2-infinality-git/).

It is recommended to also install [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) to enable selection of predefined font substitution styles and antialiasing settings, apart from the rendering settings of the engine itself. After doing so, you can select the font style (win7, winxp, osx, linux, ...) with:

```
# infctl setstyle

```

If you set e.g. win7 or osx you need the corresponding fonts installed.

**Note:** Default infinality settings can cause some programs to display fonts at 72 DPI instead of 96\. If you notice a problem open /etc/fonts/infinality/infinality.conf search for the section on DPI and change 72 to 96\. This problem can specifically affect conky causing the fonts to appear smaller than they should. Thus not aligning properly with images.

**Note:** *The README for [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) says that /etc/fonts/local.conf should either not exist, or have no infinality-related configurations in it. The local.conf is now obsolete and completely replaced by this configuration.*

for more information see this article: [http://www.infinality.net/forum/viewtopic.php?f=2&t=77](http://www.infinality.net/forum/viewtopic.php?f=2&t=77)

### Ubuntu

Ubuntu adds extra configurations, and occasionally patches to the font rendering libraries.

Install the patched packages from the [AUR](/index.php/Arch_User_Repository "Arch User Repository"), the package names are: [freetype2-ubuntu](https://aur.archlinux.org/packages/freetype2-ubuntu/) [fontconfig-ubuntu](https://aur.archlinux.org/packages/fontconfig-ubuntu/) [libxft-ubuntu](https://aur.archlinux.org/packages/libxft-ubuntu/) [cairo-ubuntu](https://aur.archlinux.org/packages/cairo-ubuntu/).

The global configuration will need to be added. See [#Example fontconfig configurations](#Example_fontconfig_configurations) for a starting point.

### 恢复到未打补丁的包

To restore the unpatched packages, reinstall the originals:

```
# pacman -S --asdeps freetype2 libxft cairo fontconfig

```

## 没有fontconfig支持的应用程序

Some applications like [URxvt](/index.php/URxvt "URxvt") will ignore fontconfig settings. This is very apparent when using the infinality patches which are heavily reliant on proper configuration. You can work around this by using `~/.Xresources`, but it is not nearly as flexible as fontconfig. Example (see [#Fontconfig configuration](#Fontconfig_configuration) for explanations of the options):

 `~/.Xresources` 
```
Xft.autohint: 0
Xft.lcdfilter:  lcddefault
Xft.hintstyle:  hintfull
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

```

Make sure the settings are loaded properly when X starts with `xrdb -q` (see [Xresources](/index.php/Xresources "Xresources") for more information).

## 字体问题解决方法

### 字体扭曲

**Note:** 96 DPI is not a standard. You should use your monitor's actual DPI to get proper font rendering, especially when using subpixel rendering.

If fonts are still unexpectedly large or small, poorly proportioned or simply rendering poorly, fontconfig may be using the incorrect DPI.

Fontconfig should be able to detect DPI parameters as discovered by the Xorg server. You can check the automatically discovered DPI with `xdpyinfo`:

 `$ xdpyinfo | grep dots`  `  resolution:    102x102 dots per inch` 
**Note:** To use the *xdpyinfo* command, you must install the package [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo).

If the DPI is detected incorrectly (usually due to an incorrect monitor EDID), you can specify it manually in the Xorg configuration, see [Xorg#Display size and DPI](/index.php/Xorg#Display_size_and_DPI "Xorg"). This is the recommended solution, but it may not work with buggy drivers.

Fontconfig will default to the Xft.dpi variable if it is set. Xft.dpi is usually set by desktop environments (usually to Xorg's DPI setting) or manually in `~/.Xdefaults` or `~/.Xresources`. Use xrdb to query for the value:

 `$ xrdb -query | grep dpi`  `Xft.dpi:	102` 

Those still having problems can fall back to manually setting the DPI used by fontconfig:

```
...
<match target="pattern">
   <edit name="dpi" mode="assign"><double>102</double></edit>
</match>
...

```

### 较旧的GTK和QT应用程序

Modern GTK apps enable Xft by default but this was not the case before version 2.2\. If it is not possible to update these applications, force Xft for old [GNOME](/index.php/GNOME "GNOME") applications by adding to `~/.bashrc`:

```
export GDK_USE_XFT=1

```

For older QT applications:

```
export QT_XFT=true

```

## 资源

*   [Fonts in X11R6.8.2](http://www.x.org/X11R6.8.2/doc/fonts.html) - Official Xorg font information
*   [FreeType 2 Overview](http://freetype.sourceforge.net/freetype2/)
*   [Gentoo font-rendering thread](https://forums.gentoo.org/viewtopic-t-723341.html)