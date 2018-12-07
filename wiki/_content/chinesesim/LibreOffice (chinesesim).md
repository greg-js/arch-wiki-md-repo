引自 [主页 - LibreOffice](http://zh-cn.libreoffice.org/):

	*LibreOffice是一款功能强大且免费的开源办公软件，它同时支持Windows, Macintosh 和 Linux系统，为你提供六种针对文档编辑和数据处理需求的拥有丰富功能的应用：Writer, Calc, Impress, Draw, Math和Base。*

## Contents

*   [1 安装](#安装)
*   [2 主题](#主题)
    *   [2.1 Firefox 主题](#Firefox_主题)
    *   [2.2 关闭启动LOGO](#关闭启动LOGO)
*   [3 管理扩展](#管理扩展)
*   [4 语言帮助](#语言帮助)
    *   [4.1 拼写检查](#拼写检查)
    *   [4.2 断词换行规则](#断词换行规则)
    *   [4.3 词库](#词库)
    *   [4.4 语法检查](#语法检查)
    *   [4.5 芬兰语拼写检查](#芬兰语拼写检查)
    *   [4.6 对于en-US的离线帮助](#对于en-US的离线帮助)
*   [5 宏的安装](#宏的安装)
*   [6 疑难问题的解决](#疑难问题的解决)
    *   [6.1 更改字体](#更改字体)
    *   [6.2 抗锯齿](#抗锯齿)
    *   [6.3 使用NFSv3共享时突然停止运行](#使用NFSv3共享时突然停止运行)
    *   [6.4 对Java framework错误的修正](#对Java_framework错误的修正)
    *   [6.5 LibreOffice无法检测到你的证书](#LibreOffice无法检测到你的证书)
    *   [6.6 在编辑模式下运行 .pps 文件(没有幻灯片)](#在编辑模式下运行_.pps_文件(没有幻灯片))
    *   [6.7 参考书目的问题](#参考书目的问题)
    *   [6.8 多媒体支持](#多媒体支持)
    *   [6.9 在 Xfwm4 下内容未按照窗口改变自身大小](#在_Xfwm4_下内容未按照窗口改变自身大小)
    *   [6.10 gvfs 映射](#gvfs_映射)

## 安装

[Install](/index.php/Pacman "Pacman") 以下 [official repositories](/index.php/Official_repositories "Official repositories")的其中之一:

*   [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) 是一个feature分支,包含了对新的强化。
*   [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) 是一个维护分支。

**注意:**

*   安装过程中至少需要安装一种语言包。默认的语言为Afrikaans (这是因为它是提供的libreoffice语言包的字母排序首位)。如果你想使用UK-English语言包，请安装 [libreoffice-fresh-en-gb](https://www.archlinux.org/packages/?name=libreoffice-fresh-en-gb)或[libreoffice-still-en-gb](https://www.archlinux.org/packages/?name=libreoffice-still-en-gb), 而不是[libreoffice-fresh-uk](https://www.archlinux.org/packages/?name=libreoffice-fresh-uk)，[libreoffice-still-uk](https://www.archlinux.org/packages/?name=libreoffice-still-uk) (Ukrainian)或者 [libreoffice-fresh-br](https://www.archlinux.org/packages/?name=libreoffice-fresh-br)，[libreoffice-still-br](https://www.archlinux.org/packages/?name=libreoffice-still-br) (Breton)!
*   对于 SDK - 根据自己安装的libreoffice包的情况可以选择 [libreoffice-fresh-sdk](https://www.archlinux.org/packages/?name=libreoffice-fresh-sdk) 或 [libreoffice-still-sdk](https://www.archlinux.org/packages/?name=libreoffice-still-sdk)

*   For Qt 和 GTK+ 可视化工具, 详见 [#主题](#主题).

检查一下pacman显示的可以选择安装的依赖包。Java Runtime Environment 并不是必须的除非你想要使用 Libreoffice Base: 详见[Java](/index.php/Java "Java")。你可能需要[hsqldb2-java](https://aur.archlinux.org/packages/hsqldb2-java/) 来使用 [一些模块](https://wiki.documentfoundation.org/Base#Java_and_HSQLDB) （在Libreoffice Base当中）。

## 主题

详情请参考 [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

LibreOffice 工具包的库按照以下的顺序来检查:

```
gtk3 > gtk > kde4 > generic

```

强制使用某种 VCL UI 接口可以使用以下的一种:

```
SAL_USE_VCLPLUGIN=gen lowriter
SAL_USE_VCLPLUGIN=kde4 lowriter
SAL_USE_VCLPLUGIN=gtk lowriter
SAL_USE_VCLPLUGIN=gtk3 lowriter

```

将 `SAL_USE_VCLPLUGIN` 变量保存到你的shell配置文件在日后将会非常方便, 比如`/etc/bash.bashrc` 或者 `~/.bashrc` 如果你使用的是Bash的话。

**注意:** 新的 GTK3 UI 在 LibreOffice 5.x 中已被默认使用。

然而, 如果它看上去使用的是 Windows 95/98的按钮，请到菜单中的*Tools -> Options...* (将会出现一个选项的窗口), 接着选择*LibreOffice > Accessibility*并且去掉 "Automatically detect high-contrast mode of operating system"前的对勾。

如果这样做之后并没有立即生效, 你可能需要改变以下正在使用的按钮的设置;它同样是在 Options 选项窗口, 在*LibreOffice > View*下有两个 "Icon size and style" 的可弹出选项(下面的那个弹出口需要被设置为除了 "High-contrast" 以外的任何一种选项).

### Firefox 主题

LibreOffice 4.x 系列支持使用 Firefox 主题. 进入 LibreOffice options 并选择 *Personalization > Select Theme*, 接着粘贴你最喜欢的那款主题的URL到下面的框里。一个在对话框里的人性化的按钮将允许你打开你的浏览器进行选择浏览。

主题可以在[Mozilla主题库](https://addons.mozilla.org/en-US/firefox/themes/)中进行浏览。

### 关闭启动LOGO

如果你希望开启libreoffice时启动logo不再出现, 可以打开 `/etc/libreoffice/sofficerc`, 找到`Logo=` 那一行并且设置 `Logo=0`.

**注意:** 这个变量和logo的脚本支持没有什么关系。

## 管理扩展

以下插件可以通过 [official repositories](/index.php/Official_repositories "Official repositories") 获得:

*   [libreoffice-extension-texmaths](https://www.archlinux.org/packages/?name=libreoffice-extension-texmaths)
*   [libreoffice-extension-writer2latex](https://www.archlinux.org/packages/?name=libreoffice-extension-writer2latex)

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

## 疑难问题的解决

### 更改字体

字体可以在LibreOffice的选项里更改。在下拉菜单中，选中 工具 > 选项 > LibreOffice > 字体 。选中 “使用替换表”。在字体框输入 Andale Sans UI 并对于替换选项选择你喜欢的字体。选好后，点击右侧的对勾。然后根据需要在下面的框中选择*自动*或者*只显示屏幕*。选择 OK 。 此外还需要进入 工具 > 选项 > LibreOffice > 视图, 取消选中 "用户界面使用系统字体"。如果你的字体不支持抗锯齿，比如 Arial 字体，你还需要取消选中 "屏幕字体抗锯齿" 。

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

如果 Writer 在打开 *工具 > 文献数据库* 时崩掉, 且出现了以下提示语句:

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