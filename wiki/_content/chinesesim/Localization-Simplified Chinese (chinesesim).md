相关文章

*   [Installation guide (简体中文)](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")
*   [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")
*   [Beginners' Guide (简体中文)](/index.php/Beginners%27_Guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Beginners' Guide (简体中文)")

依据「[Arch 之道](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")」：我们不会为你配置好一切，因为“喜好和需求，每人皆不同”，但是会尽量确保让配置时方便和简单。事实上，甚至远比使用某些Linux中文版本容易。

本文尽可能提供了各种常见软件的中文化指导。但实际应用中，你可能遇到各种各样的麻烦。遇到了麻烦，不要气馁，解决问题本身就是一种乐趣。你可以通过各种渠道寻求帮助：

*   [Google](http://www.google.com/ncr)等搜索引擎
*   [Arch官方论坛](https://bbs.archlinux.org/)
*   [Ubuntu中文论坛Arch专区](http://forum.ubuntu.org.cn/viewforum.php?f=155)
*   [IRC频道:#archlinux-cn](irc://irc.freenode.net/#archlinux-cn)

## Contents

*   [1 基本中文支持](#基本中文支持)
    *   [1.1 locale设置](#locale设置)
    *   [1.2 安装中文locale](#安装中文locale)
    *   [1.3 启用中文locale](#启用中文locale)
        *   [1.3.1 单独在图形界面启用中文locale](#单独在图形界面启用中文locale)
        *   [1.3.2 图形界面用户设置全面的中文](#图形界面用户设置全面的中文)
    *   [1.4 中文字体](#中文字体)
        *   [1.4.1 安装字体](#安装字体)
        *   [1.4.2 中文字体配置](#中文字体配置)
            *   [1.4.2.1 修正简体中文显示为异体（日文）字形](#修正简体中文显示为异体（日文）字形)
            *   [1.4.2.2 fontconfig设置](#fontconfig设置)
    *   [1.5 中文输入法](#中文输入法)
*   [2 终端中文支持](#终端中文支持)
    *   [2.1 引导中文支持](#引导中文支持)
    *   [2.2 终端中文支持](#终端中文支持_2)
    *   [2.3 终端中文输入支持](#终端中文输入支持)
*   [3 软件中文化配置](#软件中文化配置)
    *   [3.1 Firefox](#Firefox)
    *   [3.2 Libreoffice](#Libreoffice)
    *   [3.3 Calligra (原 Koffice)](#Calligra_(原_Koffice))
    *   [3.4 PDF阅读器](#PDF阅读器)
    *   [3.5 Java](#Java)
    *   [3.6 vim](#vim)
    *   [3.7 中文视频字幕](#中文视频字幕)
        *   [3.7.1 Mplayer](#Mplayer)
        *   [3.7.2 xine](#xine)
        *   [3.7.3 gstreamer](#gstreamer)
    *   [3.8 LaTeX](#LaTeX)
*   [4 乱码问题](#乱码问题)
    *   [4.1 文件名乱码](#文件名乱码)
    *   [4.2 文件内容乱码](#文件内容乱码)
    *   [4.3 zip压缩包乱码](#zip压缩包乱码)
    *   [4.4 MP3文件标签乱码](#MP3文件标签乱码)
    *   [4.5 Windows分区下的中文文件名乱码](#Windows分区下的中文文件名乱码)
    *   [4.6 Samba乱码](#Samba乱码)
    *   [4.7 ftp乱码](#ftp乱码)
*   [5 翻译软件](#翻译软件)

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
zh_TW.BIG-5
zh_TW.UTF-8

```

推荐使用UTF-8的locale。对于glibc（>=2.3.6），需要修改`/etc/locale.gen`文件来设定系统中可以使用的locale（取消对应项前的注释符号「`#`」即可）：

```
en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8

```

然后执行`locale-gen`命令，便可以在系统中使用这些locale。可以通过`locale`命令来查看当前使用的locale：亦可通过`locale -a`命令来查看目前可以使用的locale；

### 启用中文locale

Arch Linux中，通过`/etc/locale.conf`文件设置全局有效的locale：

```
LANG=en_US.UTF-8

```

**警告:** 不推荐在此设置中文locale，会导致tty乱码；在tty下亦可显示和输入中文，但需要安装cce、zhcon或[fbterm](https://github.com/felixonmars/aur3-mirror/tree/master/fbterm)；

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

#### 图形界面用户设置全面的中文

添加如下内容到文件`~/.xprofile`文件中

```
export LC_ALL="zh_CN.UTF-8"

```

**注意:** 图形界面用户使用

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
*   [adobe-source-han-serif-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-cn-fonts)
*   [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk)

系统字体将默认安装到`/usr/share/fonts`。如果没有root权限或只打算自己使用某些字体，可以直接复制这些字体到`~/.fonts`目录（或其子目录）下面，并把该路径加入/etc/fonts/local.conf中。具体参见后面章节。

另见：[[2]](http://wiki.debian.org.hk/w/Where_can_I_find_fonts_for_GNU/Linux)

#### 中文字体配置

##### 修正简体中文显示为异体（日文）字形

安装的Noto Sans CJK 或 adobe source han sans otc fonts（思源黑体） 或 adobe source han serif otc fonts（思源宋体）后，在某些情况下（框架未定义地区）汉字字形与标准形态不符，例如门、关、复等字字形与规范中文不符。

这是因为每个程序中可以设置不同的默认字体，比如Arial或者Tohamo，而这些字体的属性由fontconfig控制，其使用顺序是据地区代码以A-Z字母表顺序成默认排序，由于 ja-JP 在 zh_{CN,HK,SG,TW} 之前，故优先显示日文字形。

**提示：** 若欲解决Chromium/Chrome中的异体字形问题，应首先在chrome://settings/fonts中将几个字体选项调成Noto xxx CJK SC。如无效再尝试下述三种方案 [[3]](http://tieba.baidu.com/p/4879946717)

可选用以下方法解决（以简体中文为例）：

*   安装根据地区打包的字体，例如简体中文用户安装思源黑体简体中文包[adobe-source-han-sans-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-cn-fonts)、[adobe-source-han-serif-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-cn-fonts)或者[noto-fonts-sc](https://aur.archlinux.org/packages/noto-fonts-sc/)。(推荐，此方法最简单）
*   在`locale.conf`中添加**LANG=zh_CN.UTF-8**，以将简体中文设置为默认语言。由于对[Locale (简体中文)](/index.php/Locale_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Locale (简体中文)")定义了框架内地区（即 CJK 优先度），使得默认的优先级被忽略。
*   手动调整优先级，将中文字形调整到日文字形之前。[[4]](http://tieba.baidu.com/p/4879946717)

修改或创建文件`/etc/fonts/conf.avail/64-language-selector-prefer.conf`,

noto-fonts-cjk用户：

```
 <?xml version="1.0"?>
 <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
 <fontconfig>
 <alias>
 <family>sans-serif</family>
 <prefer>
 <family>Noto Sans CJK SC</family>
 <family>Noto Sans CJK TC</family>
 <family>Noto Sans CJK JP</family>
 </prefer>
 </alias>
 <alias>
 <family>monospace</family>
 <prefer>
 <family>Noto Sans Mono CJK SC</family>
 <family>Noto Sans Mono CJK TC</family>
 <family>Noto Sans Mono CJK JP</family>
 </prefer>
 </alias>
 </fontconfig>

```

adobe-source-han-sans-otc-fonts用户：

```
 <?xml version="1.0"?>
 <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
 <fontconfig>
 <alias>
 <family>sans-serif</family>
 <prefer>
 <family>Source Han Sans SC</family>
 <family>Source Han Sans TC</family>
 <family>Source Han Sans HW</family>
 <family>Source Han Sans K</family>
 </prefer>
 </alias>
 <alias>
 <family>monospace</family>
 <prefer>
 <family>Source Han Sans SC</family>
 <family>Source Han Sans TC</family>
 <family>Source Han Sans HW</family>
 <family>Source Han Sans K</family>
 </prefer>
 </alias>
 </fontconfig>

```

若`/etc/fonts`目录下有`conf.d/`目录，则在该目录中创建指向`/etc/fonts/conf.avail/64-language-selector-prefer.con`的同名软链接：

```
 # ln -s /etc/fonts/conf.avail/64-language-selector-prefer.conf /etc/fonts/conf.d/64-language-selector-prefer.conf

```

然后更新字体缓存即可生效：

```
 # fc-cache -fv

```

执行以下命令检查，如果出现`NotoSansCJK-Regular.ttc: "Noto Sans CJK SC" "Regular"`则表示设置成功：

```
 # fc-match -s |grep 'Noto Sans CJK'

```

##### fontconfig设置

fontconfig的设置文件是`~/.fonts.conf`（用户）或者`/etc/fonts/conf.d`（全局）。推荐修改前者。

关于中文字体设置，参见：[Fonts (简体中文)](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fonts (简体中文)")、[Font configuration (简体中文)](/index.php/Font_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Font configuration (简体中文)")。

[Font Configuration (简体中文)/中文字体配置范例](/index.php/Font_Configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/%E4%B8%AD%E6%96%87%E5%AD%97%E4%BD%93%E9%85%8D%E7%BD%AE%E8%8C%83%E4%BE%8B "Font Configuration (简体中文)/中文字体配置范例")提供了中文字体fontconfig示范。

另见：

*   [fontconfig用户手册](http://www.chinalinuxpub.com/read.php?wid=634)
*   [Debian中文支持](http://wiki.linux.org.hk/w/Make_Debian_support_Chinese)
*   [[5]](http://www.higherorder.org/wiki/Fontconfig)

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

### Firefox

简体中文用户安装 [firefox-i18n-zh-cn](https://www.archlinux.org/packages/?name=firefox-i18n-zh-cn)

繁体中文用户安装 [firefox-i18n-zh-tw](https://www.archlinux.org/packages/?name=firefox-i18n-zh-tw)

### Libreoffice

简体中文用户安装 [libreoffice-fresh-zh-cn](https://www.archlinux.org/packages/?name=libreoffice-fresh-zh-cn) 或 [libreoffice-still-zh-cn](https://www.archlinux.org/packages/?name=libreoffice-still-zh-cn)

繁体中文用户安装 [libreoffice-fresh-zh-tw](https://www.archlinux.org/packages/?name=libreoffice-fresh-zh-tw) 或 [libreoffice-still-zh-cn](https://www.archlinux.org/packages/?name=libreoffice-still-zh-cn)

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

xine也可以显示中文字幕，但需要制作自己的中文字体。具体可以参考：[[6]](http://forum.ubuntu.org.cn/about2760.html)。

#### gstreamer

在totem 1.4.0，由于使用gstreamer0.10，应该是可以自动加载同名的srt字幕。

### LaTeX

首先需要安装CJK包，然后需要安装合适的字体。具体可以参考：[[7]](http://www.ctex.org)。

## 乱码问题

避免乱码基本原则：使用utf-8代替gbk/gb2312。

### 文件名乱码

安装 [convmv](https://www.archlinux.org/packages/?name=convmv)，使用`convmv`命令转换编码格式。示例：

```
convmv -f GBK -t UTF-8 --notest --nosmart file

```

`-f`指定原始编码，`-t`指定输出编码。使用`convmv --list`可查询所有支持的编码。 `--notest`表示非测试而是要进行转码（如果不使用该参数只会打印出转换结果而不会实际转码），`--smart`表示如果已经是UTF-8则忽略。

### 文件内容乱码

使用`iconv`命令转换格式。示例：

```
iconv -f GBK -t UTF-8 -o new-file origin-file

```

`-f`指定原始编码，`-t`指定输出编码。使用`iconv -l`可查询所有支持的编码。`-o`指定输出文件。

### zip压缩包乱码

避免方法：非utf8编码环境下(一般windwos下的中文环境即是）不使用zip进行压缩（建议使用7z)。 解决方案：安装使用[unzip-iconv](https://aur.archlinux.org/packages/unzip-iconv/)或者[unzip-natspec](https://aur.archlinux.org/packages/unzip-natspec/)取代原版的[unzip](https://www.archlinux.org/packages/?name=unzip)来解压缩，示例：

```
 unzip -O gbk file.zip

```

file.zip是压缩文件，gbk是该文件的编码格式，以-O指定（原版unzip无-O选项）。

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

## 翻译软件

*   [sdcv](https://www.archlinux.org/packages/?name=sdcv)（命令行的星际译王）和[ydcv](https://www.archlinux.org/packages/?name=ydcv)命令行的有道词典。
*   [youdao-dict](https://aur.archlinux.org/packages/youdao-dict/)：有道词典（图形界面），屏幕取词翻译。
*   [goldendict](https://www.archlinux.org/packages/?name=goldendict)：默认都不带字典，可下载相应字典包（支持Babylon的词库格式.BGL，已经不再维护的StarDict的词库格式（.ifo/.dict/.idx/.syn），Dictd的词库格式（.index/.dict(.dz) ，ABBYY Lingvo 的词库格式（.dsl/.lsa/.dat），mdict的词库格式等等。可在互联网上下载这些词典的词库文件导入的goldendict使用（可能有版权问题）。
*   [moedict](https://aur.archlinux.org/packages/moedict/)一个跨多平台的汉语词典，除汉字、词、成语等，还包含客家话、闽南话、简单的外文翻译、笔顺书写等等，[萌典在线地址](https://www.moedict.tw/%E8%90%8C)。
*   [linedict](https://aur.archlinux.org/packages/linedict/)一个通过爬取有道翻译网页得到结果的在线英汉词典,部分支持英汉翻译，模仿dmenu在屏幕顶端显示结果，使用方便，由于[ydcv](https://www.archlinux.org/packages/?name=ydcv)使用的api将在2017年底失效，而有道新的api有免费使用次数限制，linedict是一个较好的替代品