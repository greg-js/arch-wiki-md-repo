引自 [主页 - LibreOffice](http://zh-cn.libreoffice.org/):

	_LibreOffice是一款功能强大且免费的开源办公软件，它同时支持Windows, Macintosh 和 Linux系统，为你提供六种针对文档编辑和数据处理需求的拥有丰富功能的应用：Writer, Calc, Impress, Draw, Math和Base。[Support](http://www.libreoffice.org/get-help/)和[documentation](http://www.libreoffice.org/get-help/documentation/)对于我们庞大的且忠实的的社区用户，贡献者和开发者是完全开放的。 [还等什么，加入我们!](http://www.libreoffice.org/get-involved/)_

## Contents

*   [1 LibreOffice同Arch Linux的情缘](#LibreOffice.E5.90.8CArch_Linux.E7.9A.84.E6.83.85.E7.BC.98)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 主题](#.E4.B8.BB.E9.A2.98)
    *   [3.1 Firefox 主题](#Firefox_.E4.B8.BB.E9.A2.98)
    *   [3.2 关闭启动LOGO](#.E5.85.B3.E9.97.AD.E5.90.AF.E5.8A.A8LOGO)
*   [4 管理扩展](#.E7.AE.A1.E7.90.86.E6.89.A9.E5.B1.95)
*   [5 语言帮助](#.E8.AF.AD.E8.A8.80.E5.B8.AE.E5.8A.A9)
    *   [5.1 拼写检查](#.E6.8B.BC.E5.86.99.E6.A3.80.E6.9F.A5)
    *   [5.2 断词换行规则](#.E6.96.AD.E8.AF.8D.E6.8D.A2.E8.A1.8C.E8.A7.84.E5.88.99)
    *   [5.3 词库](#.E8.AF.8D.E5.BA.93)
    *   [5.4 语法检查](#.E8.AF.AD.E6.B3.95.E6.A3.80.E6.9F.A5)
    *   [5.5 芬兰语拼写检查](#.E8.8A.AC.E5.85.B0.E8.AF.AD.E6.8B.BC.E5.86.99.E6.A3.80.E6.9F.A5)
    *   [5.6 对于en-US的离线帮助](#.E5.AF.B9.E4.BA.8Een-US.E7.9A.84.E7.A6.BB.E7.BA.BF.E5.B8.AE.E5.8A.A9)
*   [6 宏的安装](#.E5.AE.8F.E7.9A.84.E5.AE.89.E8.A3.85)
*   [7 LibreOffice的优化](#LibreOffice.E7.9A.84.E4.BC.98.E5.8C.96)
*   [8 疑难问题的解决](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98.E7.9A.84.E8.A7.A3.E5.86.B3)
    *   [8.1 更改字体](#.E6.9B.B4.E6.94.B9.E5.AD.97.E4.BD.93)
    *   [8.2 抗锯齿](#.E6.8A.97.E9.94.AF.E9.BD.BF)
    *   [8.3 使用NFSv3共享时突然停止运行](#.E4.BD.BF.E7.94.A8NFSv3.E5.85.B1.E4.BA.AB.E6.97.B6.E7.AA.81.E7.84.B6.E5.81.9C.E6.AD.A2.E8.BF.90.E8.A1.8C)
    *   [8.4 对Java framework错误的修正](#.E5.AF.B9Java_framework.E9.94.99.E8.AF.AF.E7.9A.84.E4.BF.AE.E6.AD.A3)
    *   [8.5 LibreOffice无法检测到你的证书](#LibreOffice.E6.97.A0.E6.B3.95.E6.A3.80.E6.B5.8B.E5.88.B0.E4.BD.A0.E7.9A.84.E8.AF.81.E4.B9.A6)
    *   [8.6 在编辑模式下运行 .pps 文件(没有幻灯片)](#.E5.9C.A8.E7.BC.96.E8.BE.91.E6.A8.A1.E5.BC.8F.E4.B8.8B.E8.BF.90.E8.A1.8C_.pps_.E6.96.87.E4.BB.B6.28.E6.B2.A1.E6.9C.89.E5.B9.BB.E7.81.AF.E7.89.87.29)
    *   [8.7 参考书目的问题](#.E5.8F.82.E8.80.83.E4.B9.A6.E7.9B.AE.E7.9A.84.E9.97.AE.E9.A2.98)
    *   [8.8 多媒体支持](#.E5.A4.9A.E5.AA.92.E4.BD.93.E6.94.AF.E6.8C.81)
    *   [8.9 在 Xfwm4 下内容未按照窗口改变自身大小](#.E5.9C.A8_Xfwm4_.E4.B8.8B.E5.86.85.E5.AE.B9.E6.9C.AA.E6.8C.89.E7.85.A7.E7.AA.97.E5.8F.A3.E6.94.B9.E5.8F.98.E8.87.AA.E8.BA.AB.E5.A4.A7.E5.B0.8F)
    *   [8.10 gvfs 映射](#gvfs_.E6.98.A0.E5.B0.84)

## LibreOffice同Arch Linux的情缘

对于[OpenOffice.org](/index.php/OpenOffice.org "OpenOffice.org")的官方支持由LibreOffice所取代，它是该工程的 "Document Foundation"分支, 其中包含了对于一些功能的强化和额外的特征。 请参考 [Dropping Oracle OpenOffice (arch-general)](https://mailman.archlinux.org/pipermail/arch-general/2011-March/018819.html).

## 安装

[Install](/index.php/Pacman "Pacman") 以下 [official repositories](/index.php/Official_repositories "Official repositories")的其中之一:

*   [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) 是一个feature分支,包含了对新的强化。
*   [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) 是一个维护分支。

**注意:**

*   安装过程中至少需要安装一种语言包。默认的语言为Afrikaans (这是因为它是提供的libreoffice语言包的字母排序首位)。如果你想使用UK-English语言包，请安装 [libreoffice-en-GB](https://www.archlinux.org/packages/?name=libreoffice-en-GB), 而不是[libreoffice-uk](https://www.archlinux.org/packages/?name=libreoffice-uk) (Ukrainian)或者 [libreoffice-br](https://www.archlinux.org/packages/?name=libreoffice-br) (Breton)!
*   [libreoffice-still-kde4](https://www.archlinux.org/packages/?name=libreoffice-still-kde4) 和 [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome) 分别对应于 Qt 和 GTK+ 可视化工具。详见 [Theme](#Theme) 部分.
*   对于 SDK - 根据自己安装的libreoffice包的情况可以选择 [libreoffice-fresh-sdk](https://www.archlinux.org/packages/?name=libreoffice-fresh-sdk) 或 [libreoffice-still-sdk](https://www.archlinux.org/packages/?name=libreoffice-still-sdk)

检查一下pacman显示的可以选择安装的依赖包。Java Runtime Environment 并不是必须的除非你想要使用 Libreoffice Base: 详见[Java](/index.php/Java "Java")。你可能需要[hsqldb2-java](https://aur.archlinux.org/packages/hsqldb2-java/) 来使用 [一些模块](https://wiki.documentfoundation.org/Base#Java_and_HSQLDB) （在Libreoffice Base当中）。

## 主题

对于 [Qt](/index.php/Qt "Qt") 用户, 请安装 [libreoffice-still-kde4](https://www.archlinux.org/packages/?name=libreoffice-still-kde4), 对于[GTK+](/index.php/GTK%2B "GTK+") 请安装 [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome)。详情请参考 [Uniform_Look_for_Qt_and_GTK_Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications").

LibreOffice v3.5.x 工具包的库按照以下的顺序来检查:

```
gtk > kde4 > generic

```

强制使用某种 VCL UI 接口可以使用以下的一种:

```
SAL_USE_VCLPLUGIN=gen lowriter
SAL_USE_VCLPLUGIN=kde4 lowriter
SAL_USE_VCLPLUGIN=gtk lowriter
SAL_USE_VCLPLUGIN=gtk3 lowriter

```

将 `SAL_USE_VCLPLUGIN` 变量保存到你的shell配置文件在日后将会非常方便, 比如`/etc/bash.bashrc` 或者 `~/.bashrc` 如果你使用的是Bash的话。

**注意:** 新的 GTK3 UI 尚处于试验阶段，只有你在LibreOffice 的主配置栏中将"experimental features"启动之后才会生效。

然而, 如果它看上去使用的是 Windows 95/98的按钮，请到菜单中的_Tools -> Options..._ (将会出现一个选项的窗口), 接着选择_LibreOffice > Accessibility_并且去掉 "Automatically detect high-contrast mode of operating system"前的对勾。

如果这样做之后并没有立即生效, 你可能需要改变以下正在使用的按钮的设置;它同样是在 Options 选项窗口, 在_LibreOffice > View_下有两个 "Icon size and style" 的可弹出选项(下面的那个弹出口需要被设置为除了 "High-contrast" 以外的任何一种选项).

### Firefox 主题

LibreOffice 4.x 系列支持使用 Firefox 主题. 进入 LibreOffice options 并选择 _Personalization > Select Theme_, 接着粘贴你最喜欢的那款主题的URL到下面的框里。一个在对话框里的人性化的按钮将允许你打开你的浏览器进行选择浏览。

主题可以在[Mozilla主题库](https://addons.mozilla.org/en-US/firefox/themes/)中进行浏览。

### 关闭启动LOGO

如果你希望开启libreoffice时启动logo不再出现, 可以打开 `/etc/libreoffice/sofficerc`, 找到`Logo=` 那一行并且设置 `Logo=0`.

**注意:** 这个变量和logo的脚本支持没有什么关系。

## 管理扩展

以下插件可以通过 [official repositories](/index.php/Official_repositories "Official repositories") 获得:

*   [libreoffice-still-extension-nlpsolver](https://www.archlinux.org/packages/?name=libreoffice-still-extension-nlpsolver)
*   [libreoffice-still-extension-wiki-publisher](https://www.archlinux.org/packages/?name=libreoffice-still-extension-wiki-publisher)

对于更多插件, 可以查看 [AUR](/index.php/AUR "AUR"), 内置的 LibreOffice 扩展插件管理, 或者访问 [libreplanet](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List).

## 语言帮助

### 拼写检查

为了开启拼写检查，你需要安装 [hunspell](https://www.archlinux.org/packages/?name=hunspell) 和与语言对应hunspell词典，比如说 英语的[hunspell-en](https://www.archlinux.org/packages/?name=hunspell-en)，德语的[hunspell-de](https://www.archlinux.org/packages/?name=hunspell-de)等等。

### 断词换行规则

为了开启换行规则，你需要安装 [hyphen](https://www.archlinux.org/packages/?name=hyphen) 和与语言对应hyphen规则，比如说 英语的[hyphen-en](https://www.archlinux.org/packages/?name=hyphen-en)，德语的[hyphen-de](https://www.archlinux.org/packages/?name=hyphen-de)等等。

### 词库

对于词库选项, 你需要 [libmythes](https://www.archlinux.org/packages/?name=libmythes) 和一个 mythes 语言词库 (比如英语的 [mythes-en](https://www.archlinux.org/packages/?name=mythes-en) , 德语的 [mythes-de](https://www.archlinux.org/packages/?name=mythes-de) , 等等)).

### 语法检查

为了开启语法检查，你需要安装一个扩展，比如 LanguageTool，可以在[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)"): [libreoffice-extension-languagetool](https://aur.archlinux.org/packages/libreoffice-extension-languagetool/) 找到 或者 [LanguageTool Website](http://www.languagetool.org/)。

其它的语法工具可以在这里 [LibreOffice Extension Page](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List) 或者这里 [OpenOffice's Website](http://lingucomponent.openoffice.org/grammar.html)找到。 不确保所有的OpenOffice扩展都能在LibreOffice下正常工作。

**注意:** Languagetool 使用java并且可能会是LibreOffice短暂地失去响应，特别是在打开文件的时候。幸运的是，这种情况只在LibreOffice首次启动时才有。 LanguageTool在Openjdk6下的表现比在openjdk7下要好，尽管这个问题并没有被确认。

### 芬兰语拼写检查

对于芬兰的用户, 这里有四个包需要安装。按照如下顺序进行安装 [malaga](https://aur.archlinux.org/packages/malaga/), [suomi-malaga-voikko](https://aur.archlinux.org/packages/suomi-malaga-voikko/), [libvoikko](https://www.archlinux.org/packages/?name=libvoikko) 和 [voikko-libreoffice](https://aur.archlinux.org/packages/voikko-libreoffice/).

### 对于en-US的离线帮助

官方源中的 US English 包并不包含历险的帮助文件。需要 en-US 帮助文件的用户可以安装 [libreoffice-still-en-us-help](https://aur.archlinux.org/packages/libreoffice-still-en-us-help/) 或者 [libreoffice-fresh-en-us-help](https://aur.archlinux.org/packages/libreoffice-fresh-en-us-help/) ，参照 [AUR](/index.php/AUR "AUR")中的包。

## 宏的安装

在绝大多数Linux发行版中，宏的默认路径位于:

```
~/.openoffice.org/3/user/Scripts/

```

那么对于 Arch Linux 而言，LibreOffice 的这个目录的路径位于:

```
~/.config/.libreoffice/3/user/Scripts/

```

如果你想要使用宏另一件需要注意的事情是, 你必须有一个生效的JRE, 对于 JRE 的使用是默认的; 但是对于下面关于 LibreOffice 优化的技巧，列出来了如果将JRE使用禁止的方法。

## LibreOffice的优化

一些设置可以提升LibreOffice的读取时间和响应速度。但相对应地也可能增加内存的使用量，所以请小心使用。这些设置可以在 _Tools > Options_ 下找到。

*   在 _Memory_ 选项卡下:
    *   把可撤销步数减少到100以下，20到30步左右是个不错的选择
    *   在_图形缓冲区_， 把 Use for LibreOffice 增加到128MB (默认值为20MB)
    *   把_每个对象的内存_ 增加到20MB (默认值为5MB)。
    *   如果你经常使用 LibreOffice 的话, 检查 _Enable systray Quickstarter_

**注意:** [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome)包必须被安装如果你想启用 quickstarter 选项的话。

*   在 _Advanced_ 选项卡下, 取消选择 _Use a Java runtime environment_

**注意:** 如果只想查看用Java写的功能列表的话, 请参考： [https://wiki.documentfoundation.org/Development/Java](https://wiki.documentfoundation.org/Development/Java).

## 疑难问题的解决

### 更改字体

字体可以在LibreOffice的选项里更改。在下拉菜单中，选中 工具 > 选项 > LibreOffice > 字体 。选中 “使用替换表”。在字体框输入 Andale Sans UI 并对于替换选项选择你喜欢的字体。选好后，点击右侧的对勾。然后根据需要在下面的框中选择_自动_或者_只显示屏幕_。选择 OK 。 此外还需要进入 工具 > 选项 > LibreOffice > 视图, 取消选中 "用户界面使用系统字体"。如果你的字体不支持抗锯齿，比如 Arial 字体，你还需要取消选中 "屏幕字体抗锯齿" 。

### 抗锯齿

执行

```
$ echo "Xft.lcdfilter: lcddefault" | xrdb -merge

```

如需使其永久生效，请添加 `Xft.lcdfilter: lcddefault` 到你的 `~/.Xresources` 文件，并且确保执行 `xrdb -merge ~/.Xresources`。 [[1]](https://bugs.launchpad.net/ubuntu/+source/openoffice.org/+bug/271283/comments/19). 更多信息请查看 [X resources](/index.php/X_resources "X resources")。

如果这样不起作用的话，你也可以尝试添加 `Xft.lcdfilter: lcddefault` 到你的 `~/.Xdefaults` 文件。如果文件不存在请创建一个。

### 使用NFSv3共享时突然停止运行

如果在你试图打开或者保存一个位于NFSv3共享的文档的时候 LibreOffice 停止运行，试着在以 `#` 开头在 `/usr/lib/libreoffice/program/soffice` 中添加以下几行:

```
# file locking now enabled by default
SAL_ENABLE_FILE_LOCKING=1
export SAL_ENABLE_FILE_LOCKING

```

为了避免覆盖更新你可以将 `/usr/lib/libreoffice/program/soffice` 复制到 `/usr/local/bin`. 原始链接为 [点击这里](http://www.crazysquirrel.com/computing/debian/bugs/openoffice-over-nfs.jspx).

### 对Java framework错误的修正

当你试图运行Libreoffice时可能会出现以下错误。

```
[Java framework] Error in function createSettingsDocument (elements.cxx).
javaldx failed!

```

如果是这样的话, 将你的权限赋像这样给 `~/.config/` :

```
# chown -vR username:users ~/.config

```

[参照 Arch Linux forums 上的这篇帖子](https://bbs.archlinux.org/viewtopic.php?id=93168).

### LibreOffice无法检测到你的证书

如果在你为一个文档签名的时候无法查看证书, 你需要取得在 Mozilla Firefox (或者 Thunderbird) 中配置的证书。如果在这之后 LibreOffice 仍然无法显示证书, 设置 `MOZILLA_CERTIFICATE_FOLDER` 环境变量指向你的 Mozilla Firefox (或者 Thunderbird) 文件夹:

```
export MOZILLA_CERTIFICATE_FOLDER=$HOME/.mozilla/firefox/XXXXXX.default/

```

[证书检测](http://wiki.openoffice.org/wiki/Certificate_Detection).

### 在编辑模式下运行 .pps 文件(没有幻灯片)

针对此问题的唯一解决办法就是 将`.pps` 文件重命名为 `.ppt`.

添加以下脚本到你的home目录并且使用它来打开每一个 .pps 文件。 对于通过 email 接收到的 `.pps` 文件，在仅仅需要打开而无需保存时是非常有用的。

```
#!/bin/bash

f=$(mktemp)
cp "$1" "${f}.ppt" && libreoffice "${f}.ppt" && rm -f "${f}.ppt"

```

### 参考书目的问题

如果 Writer 在打开 _工具 > 文献数据库_ 时崩掉, 且出现了以下提示语句:

```
com::sun::star::loader::CannotActivateFactoryException

```

请安装 [libreoffice-base](https://www.archlinux.org/packages/?name=libreoffice-base) ，这是对于一个已知bug的解决办法，请参照 [解决](http://cgit.freedesktop.org/libreoffice/core/commit/?id=1889c1af41650576a29c587a0b2cdeaf0d297587).

### 多媒体支持

如果插入的videos仅仅显示为灰色的框，请首先确认你是否已经安装了必须的 [GStreamer plugins](/index.php/GStreamer#Current_version_plugins "GStreamer")。

### 在 Xfwm4 下内容未按照窗口改变自身大小

如果在 Xfce (或者仅仅使用 Xfwm4) 时你在 LibreOffice 窗口下的内容并未随着窗口变化而改变大小,就类似在这个帖子里描述的: [[2]](https://bbs.archlinux.org/viewtopic.php?id=133137)。请安装 [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome) 来解决这个问题。

### gvfs 映射

如果你需要在 gvfs 映射下打开/保存文档，你需要安装 [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome) .