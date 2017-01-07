依据「[Arch 之道](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")」：我们不会为你配置好一切，因为“喜好和需求，每人皆不同”，但是会尽量确保让配置时方便和简单。事实上，甚至远比使用某些Linux中文版本容易。

本文尽可能提供了各种常见软件的中文化指导。但实际应用中，你可能遇到各种各样的麻烦。遇到了麻烦，不要气馁，解决问题本身就是一种乐趣。你可以通过各种渠道寻求帮助：

*   [Google](http://www.google.com/ncr)等搜索引擎
*   [Arch官方论坛](https://bbs.archlinux.org/)
*   [Ubuntu中文论坛Arch专区](http://forum.ubuntu.org.cn/viewforum.php?f=155)
*   [Linuxsir论坛Arch讨论区](http://www.linuxsir.org/bbs/forum96.html)
*   [IRC频道:#archlinux-cn](irc://irc.freenode.net/#archlinux-cn)

## Contents

*   [1 基本中文支持](#.E5.9F.BA.E6.9C.AC.E4.B8.AD.E6.96.87.E6.94.AF.E6.8C.81)
    *   [1.1 locale设置](#locale.E8.AE.BE.E7.BD.AE)
    *   [1.2 安装中文locale](#.E5.AE.89.E8.A3.85.E4.B8.AD.E6.96.87locale)
    *   [1.3 启用中文locale](#.E5.90.AF.E7.94.A8.E4.B8.AD.E6.96.87locale)
        *   [1.3.1 单独在图形界面启用中文locale](#.E5.8D.95.E7.8B.AC.E5.9C.A8.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E5.90.AF.E7.94.A8.E4.B8.AD.E6.96.87locale)
    *   [1.4 中文字体](#.E4.B8.AD.E6.96.87.E5.AD.97.E4.BD.93)
        *   [1.4.1 安装字体](#.E5.AE.89.E8.A3.85.E5.AD.97.E4.BD.93)
        *   [1.4.2 中文字体配置](#.E4.B8.AD.E6.96.87.E5.AD.97.E4.BD.93.E9.85.8D.E7.BD.AE)
        *   [1.4.3 fontconfig设置](#fontconfig.E8.AE.BE.E7.BD.AE)
    *   [1.5 中文输入法](#.E4.B8.AD.E6.96.87.E8.BE.93.E5.85.A5.E6.B3.95)
*   [2 终端中文支持](#.E7.BB.88.E7.AB.AF.E4.B8.AD.E6.96.87.E6.94.AF.E6.8C.81)
    *   [2.1 引导中文支持](#.E5.BC.95.E5.AF.BC.E4.B8.AD.E6.96.87.E6.94.AF.E6.8C.81)
    *   [2.2 终端中文支持](#.E7.BB.88.E7.AB.AF.E4.B8.AD.E6.96.87.E6.94.AF.E6.8C.81_2)
    *   [2.3 终端中文输入支持](#.E7.BB.88.E7.AB.AF.E4.B8.AD.E6.96.87.E8.BE.93.E5.85.A5.E6.94.AF.E6.8C.81)
*   [3 软件中文化配置](#.E8.BD.AF.E4.BB.B6.E4.B8.AD.E6.96.87.E5.8C.96.E9.85.8D.E7.BD.AE)
    *   [3.1 桌面环境](#.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)
    *   [3.2 Firefox](#Firefox)
    *   [3.3 Libreoffice](#Libreoffice)
    *   [3.4 Calligra (原 Koffice)](#Calligra_.28.E5.8E.9F_Koffice.29)
    *   [3.5 PDF阅读器](#PDF.E9.98.85.E8.AF.BB.E5.99.A8)
    *   [3.6 Java](#Java)
    *   [3.7 vim](#vim)
    *   [3.8 中文视频字幕](#.E4.B8.AD.E6.96.87.E8.A7.86.E9.A2.91.E5.AD.97.E5.B9.95)
        *   [3.8.1 Mplayer](#Mplayer)
        *   [3.8.2 xine](#xine)
        *   [3.8.3 gstreamer](#gstreamer)
    *   [3.9 LaTeX](#LaTeX)
*   [4 其他中文化问题](#.E5.85.B6.E4.BB.96.E4.B8.AD.E6.96.87.E5.8C.96.E9.97.AE.E9.A2.98)
    *   [4.1 MP3文件标签乱码](#MP3.E6.96.87.E4.BB.B6.E6.A0.87.E7.AD.BE.E4.B9.B1.E7.A0.81)
    *   [4.2 Windows分区下的中文文件名乱码](#Windows.E5.88.86.E5.8C.BA.E4.B8.8B.E7.9A.84.E4.B8.AD.E6.96.87.E6.96.87.E4.BB.B6.E5.90.8D.E4.B9.B1.E7.A0.81)
    *   [4.3 Samba乱码](#Samba.E4.B9.B1.E7.A0.81)
    *   [4.4 ftp乱码](#ftp.E4.B9.B1.E7.A0.81)
    *   [4.5 翻译软件](#.E7.BF.BB.E8.AF.91.E8.BD.AF.E4.BB.B6)

## 基本中文支持

要正确显示中文，必需设置正确的locale并安装合适的中文字体。

### locale设置

### 安装中文locale

Linux中通过locale来设置程序运行的不同环境。常用的中文locale有（最直观的分别是可显示字的数量）：

```
zh_CN.GB2312
zh_CN.GBK
zh_CN.GB18030
zh_CN.UTF-8
zh_TW
zh_TW.UTF-8

```

推荐使用UTF-8的locale。对于glibc（>=2.3.6），需要修改`/etc/locale.gen`文件来设定系统中可以使用的locale（取消对应项前的注释符号「`#`」即可）：

```
en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8

```

然后执行locale-gen命令，便可以在系统中使用这些locale。可以通过`locale`命令来查看当前使用的locale：亦可通过`locale -a`命令来查看目前可以使用的locale；

### 启用中文locale

Arch Linux中，通过`/etc/locale.conf`文件设置全局有效的locale：

```
LANG=en_US.UTF-8

```

**警告:** 不推荐在此设置中文locale，会导致tty乱码；在tty下亦可显示和输入中文，但需要安装cce、zhcon或[fbterm](https://www.archlinux.org/packages/?name=fbterm)；

**提示：** 如欲为内核打中文补丁，可参见[[1]](http://blog.chinaunix.net/space.php?uid=436750&do=blog&id=2123586)；

对于特定用户，还可以在`~/.bashrc`、`~/.xinitrc`或`~/.xprofile`中设置自己的用户环境。不同之处在于：

*   .bashrc: 每次**终端登录时**读取并运用里面的设置。
*   .xinitrc: 每次**startx启动X界面时**读取并运用里面的设置
*   .xprofile: 每次**使用gdm等图形登录时**读取并运用里面的设置

#### 单独在图形界面启用中文locale

不推荐`/etc/locale.conf`使用全局中文locale，会导致tty乱码。

如前面所说，可以在`~/.xinitrc`或`~/.xprofile`单独设置中文locale。添加如下内容到上述文件最前端注释之后（如果不确定使用哪个文件，可以都添加）：

```
export LANG=zh_CN.UTF-8
export LANGUAGE=zh_CN:en_US
export LC_CTYPE=en_US.UTF-8

```

**注意:** 若欲将此三行放至`~/.xinitrc`中，请注意将其放在`exec *_example_WM_or_DE_*`行之前；此为常见错误；

**注意:** 该方法适用于slim或者无登陆管理器的用户，GDM和KDM用户可以在Gnome或KDE设置中选择语言。

### 中文字体

#### 安装字体

除了设置好locale，还需要安装中文字体。

常用的免费（GPL或兼容版权）中文字体有：

*   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei)
*   [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite)
*   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont)
*   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei)
*   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai)
*   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming)
*   [adobe-source-han-sans-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-cn-fonts)

系统字体将默认安装到`/usr/share/fonts`。如果没有root权限或只打算自己使用某些字体，可以直接复制这些字体到`~/.fonts`目录（或其子目录）下面，并把该路径加入/etc/fonts/local.conf中。具体参见后面章节。

另见：[[2]](http://wiki.debian.org.hk/w/Where_can_I_find_fonts_for_GNU/Linux)

#### 中文字体配置

安装好字体以后，字体显示效果可能不堪入目。需要对fontconfig和某些程序进行调整。

fontconfig是字体选择的接口，你可以用它去控制单个字体或者字体族的属性，比如hint或者autohint。

另外每个程序中可以设置不同的默认字体，比如Arial或者Tohamo。这些字体的属性由fontconfig控制。所以当字体显示不满意时，首先需要判断是调整字体的种类还是字体的属性。

#### fontconfig设置

fontconfig的设置文件是`~/.fonts.conf`（用户）或者`/etc/fonts/conf.d`（全局）。推荐修改前者。

关于中文字体设置，参见：[Fonts (简体中文)](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fonts (简体中文)")、[Font configuration (简体中文)](/index.php/Font_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Font configuration (简体中文)")。

[Font Configuration (简体中文)/中文字体配置范例](/index.php/Font_Configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/%E4%B8%AD%E6%96%87%E5%AD%97%E4%BD%93%E9%85%8D%E7%BD%AE%E8%8C%83%E4%BE%8B "Font Configuration (简体中文)/中文字体配置范例")提供了中文字体fontconfig示范。

另见：

*   [fontconfig用户手册](http://www.chinalinuxpub.com/read.php?wid=634)
*   [Debian中文支持](http://wiki.linux.org.hk/w/Make_Debian_support_Chinese)
*   [[3]](http://www.higherorder.org/wiki/Fontconfig)

### 中文输入法

常用的中文输入法平台有[IBus](/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "IBus (简体中文)")、[fcitx](/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fcitx (简体中文)")和[scim](/index.php/Smart_Common_Input_Method_platform_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Smart Common Input Method platform (简体中文)")。具体安装配置参见各自条目。

**注意:** scim现在维护滞后，不推荐使用。

## 终端中文支持

### 引导中文支持

请见 [grub2](/index.php/GRUB2_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GRUB2 (简体中文)")

### 终端中文支持

请见 [fbterm](/index.php/Fbterm_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fbterm (简体中文)")

### 终端中文输入支持

请参见 [fbterm](/index.php/Fbterm_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fbterm (简体中文)")

## 软件中文化配置

### 桌面环境

除[KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")外，各大桌面环境已经包含了中文语言文件。[KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")的中文包需要额外安装：[kde-l10n-zh_cn](https://www.archlinux.org/packages/?name=kde-l10n-zh_cn)

### Firefox

简体中文用户安装 [firefox-i18n-zh-cn](https://www.archlinux.org/packages/?name=firefox-i18n-zh-cn)

繁体中文用户安装 [firefox-i18n-zh-tw](https://www.archlinux.org/packages/?name=firefox-i18n-zh-tw)

### Libreoffice

简体中文用户安装 [libreoffice-fresh-zh-CN](https://www.archlinux.org/packages/?name=libreoffice-fresh-zh-CN) 或 [libreoffice-still-zh-CN](https://www.archlinux.org/packages/?name=libreoffice-still-zh-CN)

繁体中文用户安装 [libreoffice-fresh-zh-TW](https://www.archlinux.org/packages/?name=libreoffice-fresh-zh-TW) 或 [libreoffice-still-zh-CN](https://www.archlinux.org/packages/?name=libreoffice-still-zh-CN)

### Calligra (原 Koffice)

简体中文用户安装 [calligra-l10n-zh_cn](https://www.archlinux.org/packages/?name=calligra-l10n-zh_cn)

繁体中文用户安装 [calligra-l10n-zh_tw](https://www.archlinux.org/packages/?name=calligra-l10n-zh_tw)

### PDF阅读器

多数PDF查看器已经支持中文。但也有部分需要安装额外的语言包：

Arcobat： AUR版本的中文包为[acroread-chs](https://aur.archlinux.org/packages/acroread-chs/)、[acroread-cht](https://aur.archlinux.org/packages/acroread-cht/)。

okular、evince等poppler相关的阅读器及Inkscape、Krita、MyPaint等可以处理pdf的图像处理工具：需要安装 [poppler-data](https://www.archlinux.org/packages/?name=poppler-data)

### Java

对于Sun Java用户，在`/opt/java/jre/lib/fonts`中建立fallback目录，然后链接或拷贝若干中文字体到该目录就能使java程序正确显示中文。例如，在已经安装jre和ttf-fireflysung 的情况下，使用root权限执行下面的命令即可：

```
ln -s /usr/share/fonts/TTF/odosung.ttc /opt/java/jre/lib/fonts/fallback/
cd /opt/java/jre/lib/fonts/fallback/
mkfontdir
mkfontscale

```

如果是openjdk6，需要复制`/usr/lib/jvm/java-6-openjdk/jre/lib/fontconfig.properties.src`到`/usr/lib/jvm/java-6-openjdk/jre/lib/fontconfig.properties`，并修改这个文件中的字体位置，因为文泉驿的地址指错了。

### vim

如果locale是utf8编码，用vim打开其他中文编码的文件可能会乱码。需要在`~/.vimrc`做如下设置：

```
set fileencodings=utf8,cp936,gb18030,big5

```

### 中文视频字幕

#### Mplayer

要使mplayer正确显示字幕，关键是要使字幕文件的编码和mplayer config里使用的编码相一致。字幕文件编码为gbk，则subcp=cp936;字幕文件编码为utf-8,则subcp=utf8。如果字幕文件编码为utf-8,而设置成subcp=cp936,则会出现部分乱码的情况。另一种更为简单的方法是设置成subcp=enca:zh:ucs-2，由enca负责字幕的编码显示问题。

修改`~/.mplayer/config`：

```
font='文泉驿正黑'
subcp=enca:zh:ucs-2

```

使用下面的命令手动加载字幕：

```
mplayer xxx.avi -sub xxxxx.srt

```

如果使用图形前端（比如SMPlayer），会更简单一些，只要在设置对话框里设定缺省字幕编码和字体即可。

#### xine

xine也可以显示中文字幕，但需要制作自己的中文字体。具体可以参考：[[4]](http://forum.ubuntu.org.cn/about2760.html)。

#### gstreamer

在totem 1.4.0，由于使用gstreamer0.10，应该是可以自动加载同名的srt字幕。

### LaTeX

首先需要安装CJK包，然后需要安装合适的字体。具体可以参考：[[5]](http://www.ctex.org)。

## 其他中文化问题

### MP3文件标签乱码

对于用gstreamer做后端的播放器，如Rhythmbox,totem，设置如下的环境变量后即可正确读取mp3中GBK编码的ID3 tag：

```
export GST_ID3_TAG_ENCODING=GBK:UTF-8:GB18030
export GST_ID3V2_TAG_ENCODING=GBK:UTF-8:GB18030

```

对于Beep media player，可以在pefenrence->plugins->media中选中MPEG Audio plugin然后点击下方的Penfenrences,此时会出现一个对话框，选择title，将Disable ID3v2和Convert non-UTF8 ID3 tags to UTF8前的选择框选中。然后在ID3 encoding中填入 gbk。这样bmp就能正确显示GBK编码的ID3 tag。

Quod Libet播放器支持tag编辑及设置ID3v2编码。可以在~/.quodlibet/config中设置

```
id3encoding = gbk

```

注意：Quod Libet默认支持utf8编码

最为彻底的解决方法为将编码为gbk的id3 tag转化为utf8编码。首先安装mutagen，然后利用下面的命令转换：

```
mid3iconv -e gbk XXX.mp3

```

### Windows分区下的中文文件名乱码

一般是因为挂载的字符集与locale不同，可以修改/etc/fstab（如果不了解请仔细阅读相关文档）。如果locale是utf8，修改为：

```
/dev/sdxx /media/win ntfs defaults,iocharset=utf8 0 0

```

如果locale是GBK，则应该是：

```
/dev/sdxx /media/win ntfs defaults,iocharset=cp936 0 0

```

### Samba乱码

用Arch作为Samba服务器时，在`/etc/samba/smb.conf`中加入下面一行就可以解决Windows客户端乱码问题：

```
unix charset=gb2312

```

### ftp乱码

很多ftp站点是GBK编码。如果使用UTF8的locale，下载的文件名可能会乱码。对于lftp，在`.lftp/rc`下做如下设置：

```
set ftp:charset "gbk"
set file:charset "UTF-8"

```

对于gftp，可以在`.gftp/gftprc`中做如下设置即可：

```
remote_charsets=gb2312

```

但下载下来的文件名仍然是乱码，需要打补丁编译。补丁地址为: [http://www.teatime.com.tw/%7Etommy/linux/gftp_remote_charsets.patch](http://www.teatime.com.tw/%7Etommy/linux/gftp_remote_charsets.patch)

### 翻译软件

目前有两个选择：星际译王或者goldendict，这两者默认都不带字典，所以安装完软件后，需要下载相应字典。 下面介绍安装星际译王： 先安装[stardict](https://www.archlinux.org/packages/?name=stardict)软件包：

```
pacman -S stardict

```

stardict默认是不带字典的，需要去[[6]](http://stardict.sourceforge.net/)下载字典安装。安装方法如下：

```
tar -xjvf testdict.tar.bz2
mv testdict /usr/share/stardict/dic

```

安装TTS发音，stardict默认是不带发音的，需要下载。下载安装方法如下：

```
wget [http://stardict-3.googlecode.com/files/WyabdcRealPeopleTTS.tar.bz2](http://stardict-3.googlecode.com/files/WyabdcRealPeopleTTS.tar.bz2)
tar -xjvf WyabdcRealPeopleTTS.tar.bz2
mv WyabdcRealPeopleTTS /usr/share

```

重新启动stardict

推荐使用：

*   xdict英汉字典
*   Merriam Webster 10th dictionary
*   牛津现代英汉双解辞典(正体中文)
*   朗道英汉词典(正体中文)