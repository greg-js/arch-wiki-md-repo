**翻译状态：** 本文是英文页面 [Firefox](/index.php/Firefox "Firefox") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-04-15，点击[这里](https://wiki.archlinux.org/index.php?title=Firefox&diff=0&oldid=309543)可以查看翻译后英文页面的改动。

[Firefox](http://www.firefox.com)（火狐）是[Mozilla](http://www.mozilla.com)（谋智网络）出品的一款图形界面网络浏览器。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 Firefox变种](#Firefox.E5.8F.98.E7.A7.8D)
*   [2 附加组件](#.E9.99.84.E5.8A.A0.E7.BB.84.E4.BB.B6)
*   [3 插件](#.E6.8F.92.E4.BB.B6)
    *   [3.1 Gnome Keyring 整合](#Gnome_Keyring_.E6.95.B4.E5.90.88)
    *   [3.2 KDE 整合](#KDE_.E6.95.B4.E5.90.88)
    *   [3.3 拼写检查字典](#.E6.8B.BC.E5.86.99.E6.A3.80.E6.9F.A5.E5.AD.97.E5.85.B8)
    *   [3.4 增加搜索引擎](#.E5.A2.9E.E5.8A.A0.E6.90.9C.E7.B4.A2.E5.BC.95.E6.93.8E)
        *   [3.4.1 arch-firefox-search](#arch-firefox-search)
    *   [3.5 多媒体播放](#.E5.A4.9A.E5.AA.92.E4.BD.93.E6.92.AD.E6.94.BE)
*   [4 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [4.1 设置 email 客户端](#.E8.AE.BE.E7.BD.AE_email_.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [4.2 “打开所在文件夹” 错误 (GNOME3)](#.E2.80.9C.E6.89.93.E5.BC.80.E6.89.80.E5.9C.A8.E6.96.87.E4.BB.B6.E5.A4.B9.E2.80.9D_.E9.94.99.E8.AF.AF_.28GNOME3.29)
    *   [4.3 “打开所在文件夹” 错误 (KDE)](#.E2.80.9C.E6.89.93.E5.BC.80.E6.89.80.E5.9C.A8.E6.96.87.E4.BB.B6.E5.A4.B9.E2.80.9D_.E9.94.99.E8.AF.AF_.28KDE.29)
    *   [4.4 Firefox 自动创建 ~/Desktop，但我不需要](#Firefox_.E8.87.AA.E5.8A.A8.E5.88.9B.E5.BB.BA_.7E.2FDesktop.EF.BC.8C.E4.BD.86.E6.88.91.E4.B8.8D.E9.9C.80.E8.A6.81)
    *   [4.5 禁止插件弹窗](#.E7.A6.81.E6.AD.A2.E6.8F.92.E4.BB.B6.E5.BC.B9.E7.AA.97)
    *   [4.6 中键点击问题](#.E4.B8.AD.E9.94.AE.E7.82.B9.E5.87.BB.E9.97.AE.E9.A2.98)
    *   [4.7 Backspace 键无法实现“后退”功能](#Backspace_.E9.94.AE.E6.97.A0.E6.B3.95.E5.AE.9E.E7.8E.B0.E2.80.9C.E5.90.8E.E9.80.80.E2.80.9D.E5.8A.9F.E8.83.BD)
    *   [4.8 无法记录登录信息](#.E6.97.A0.E6.B3.95.E8.AE.B0.E5.BD.95.E7.99.BB.E5.BD.95.E4.BF.A1.E6.81.AF)
    *   [4.9 使用深色GTK主题时文本区域故障](#.E4.BD.BF.E7.94.A8.E6.B7.B1.E8.89.B2GTK.E4.B8.BB.E9.A2.98.E6.97.B6.E6.96.87.E6.9C.AC.E5.8C.BA.E5.9F.9F.E6.95.85.E9.9A.9C)
    *   [4.10 文件关联问题](#.E6.96.87.E4.BB.B6.E5.85.B3.E8.81.94.E9.97.AE.E9.A2.98)
    *   [4.11 关闭Firefox时不询问是否保存标签](#.E5.85.B3.E9.97.ADFirefox.E6.97.B6.E4.B8.8D.E8.AF.A2.E9.97.AE.E6.98.AF.E5.90.A6.E4.BF.9D.E5.AD.98.E6.A0.87.E7.AD.BE)
    *   [4.12 Firefox 界面字体很难看](#Firefox_.E7.95.8C.E9.9D.A2.E5.AD.97.E4.BD.93.E5.BE.88.E9.9A.BE.E7.9C.8B)
    *   [4.13 Firefox 在某些网页中字体很难看](#Firefox_.E5.9C.A8.E6.9F.90.E4.BA.9B.E7.BD.91.E9.A1.B5.E4.B8.AD.E5.AD.97.E4.BD.93.E5.BE.88.E9.9A.BE.E7.9C.8B)
    *   [4.14 解决Firefox中与Google字体有关的字体问题](#.E8.A7.A3.E5.86.B3Firefox.E4.B8.AD.E4.B8.8EGoogle.E5.AD.97.E4.BD.93.E6.9C.89.E5.85.B3.E7.9A.84.E5.AD.97.E4.BD.93.E9.97.AE.E9.A2.98)
    *   [4.15 更新至Firefox 13后菜单无法弹出](#.E6.9B.B4.E6.96.B0.E8.87.B3Firefox_13.E5.90.8E.E8.8F.9C.E5.8D.95.E6.97.A0.E6.B3.95.E5.BC.B9.E5.87.BA)
    *   [4.16 从Marketplace安装桌面应用失败且无错误提示](#.E4.BB.8EMarketplace.E5.AE.89.E8.A3.85.E6.A1.8C.E9.9D.A2.E5.BA.94.E7.94.A8.E5.A4.B1.E8.B4.A5.E4.B8.94.E6.97.A0.E9.94.99.E8.AF.AF.E6.8F.90.E7.A4.BA)
*   [5 参见](#.E5.8F.82.E8.A7.81)

## 安装

[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")中有最新稳定版[firefox](https://www.archlinux.org/packages/?name=firefox)，可以用[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")安装。中文界面请安装简体中文语言包 [firefox-i18n-zh-cn](https://www.archlinux.org/packages/?name=firefox-i18n-zh-cn)。

如果 Firefox 无法进行抗锯齿显示，请安装 [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/) 或 [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) 并查看 [Font_Configuration](/index.php/Font_Configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Font Configuration (简体中文)").

### Firefox变种

*   **[Iceweasel](https://en.wikipedia.org/wiki/Mozilla_Corporation_software_rebranded_by_the_Debian_project#IceWeasel "wikipedia:Mozilla Corporation software rebranded by the Debian project")** — 由 Debian 开发的 Firefox 分支。主要的区别是它不包含任何含有 Mozilla 商标的内容。

	[http://wiki.debian.org/Iceweasel](http://wiki.debian.org/Iceweasel) || [iceweasel](https://aur.archlinux.org/packages/iceweasel/)

**注意:** 关于 Iceweasel 的详情参见 [此帖](http://web.glandium.org/blog/?p=97)(英文)。

*   **[GNU IceCat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat")** — 由 GNU 项目分发的浏览器。 它是完全自由的软件，与 GNU/Linux 兼容，并支持大多数的 Firefox 附加组件。

	[http://www.gnu.org/software/gnuzilla/](http://www.gnu.org/software/gnuzilla/) || [icecat](https://aur.archlinux.org/packages/icecat/)

*   **Firefox KDE** — OpenSUSE 打过补丁的、具有更好的 KDE 集成特性的 Firefox 版本。

	[http://gitorious.org/firefox-kde-opensuse](http://gitorious.org/firefox-kde-opensuse) || [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

*   **Firefox GTK3** — GTK3 版本的 Firefox。

	|| [firefox-gtk3-bin](https://aur.archlinux.org/packages/firefox-gtk3-bin/)

## 附加组件

Firefox 广为人知的一点是它的大量的附加组件，可以用来添加新功能或更改 Firefox 中已有功能。你可以在 Firefox 中的“附加组件管理器”中查找新附加组件或管理已安装的附加组件。

想查看热门附加组件列表，参见： [按热门度排序的附加组件列表](https://addons.mozilla.org/zh-CN/firefox/extensions/?sort=popular).

## 插件

_参见： [浏览器插件](/index.php/Browser_Plugins_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Browser Plugins (简体中文)")_

要查看插件使用情况，在Firefox地址栏输入：

```
about:plugins

```

或者使用_工具_菜单中的_附加组件_，选择_插件_标签。

### Gnome Keyring 整合

从[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")安装 [firefox-gnome-keyring](https://aur.archlinux.org/packages/firefox-gnome-keyring/)。 要让[firefox-gnome-keyring](https://aur.archlinux.org/packages/firefox-gnome-keyring/)使用你的登录 keychain，在 about:config 中设置 extensions.gnome-keyring.keyringName 为 "login" (不含引号)。注意 "login" 的首字母应为小写。

### KDE 整合

*   在 Firefox 中使用 GTK 外观。安装 [oxygen-gtk2](https://www.archlinux.org/packages/?name=oxygen-gtk2) 和 [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)。然后进入系统设置 -> 程序外观 -> GTK，GTK2 主题选择为 oxygen-gtk，勾选显示 GTK 按钮的图标。
*   使用 KDE's KParts 嵌入文件查看器，可以安装 [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin)。
*   可以使用 AUR 中的 [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/) Firefox 变种来集成 KDE 的文件关联系统和文件对话框。这一变种有 OpenSUSE 打的补丁。或者使用 [firefox-kde-global-menu](https://aur.archlinux.org/packages/firefox-kde-global-menu/) 它也可以达到同样的效果，且加入 appmenu 支持。

### 拼写检查字典

选择任意文本，右键为该语言添加字典，重启浏览器即可。

或者从 [官方软件仓库](/index.php/Official_repositories "Official repositories")安装软件包[hunspell](https://www.archlinux.org/packages/?name=hunspell)和其它语言例如 [hunspell-fr](https://www.archlinux.org/packages/?name=hunspell-fr) (法语) or [hunspell-he](https://www.archlinux.org/packages/?name=hunspell-he) (希伯来语)。

默认情况下，Firefox 会在 `/usr/lib/firefox/dictionaries` 生成指向到 hunspell 字典的软链接。如果你不想使用所有语言的字典，可以删掉一部分。注意，Firefox 升级可能会还原这些软链接。

### 增加搜索引擎

到下面网址选择搜索引擎并安装：

*   [https://addons.mozilla.org/zh-CN/firefox/search-tools/](https://addons.mozilla.org/zh-CN/firefox/search-tools/)
*   [http://mycroft.mozdev.org/](http://mycroft.mozdev.org/)

[add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) 扩展可以通过网址直接加入搜索引擎。

如果想自己写一个，到~/.mozilla/firefox/xxx.default/searchplugins/（xxx代表你的账户id)看一看。

#### arch-firefox-search

[arch-firefox-search](https://www.archlinux.org/packages/?name=arch-firefox-search)为Firefox搜索框添加Arch相关内容的搜索引擎（AUR、wiki、论坛……)：

```
# pacman -S arch-firefox-search

```

### 多媒体播放

`media.gstreamer.enabled`为启用时，Firefox会尝试使用[GStreamer](/index.php/GStreamer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GStreamer (简体中文)")播放HTML5的`<audio>`和`<video>`标签内的多媒体内容。你需要安装以下的可选依赖包才能让上述的功能可用：

*   [gstreamer0.10-base-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-base-plugins): 用于解码 vorbis decoding, ogg demuxing
*   [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins): 用于解码 webm 和 mp4 demuxing
*   [gstreamer0.10-bad-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-bad-plugins): 用于解码 aac, vp8 和 opus decoding
*   [gstreamer0.10-ugly-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-ugly-plugins): 用于解码 h.264 和 mp3
*   [gstreamer0.10-ffmpeg](https://www.archlinux.org/packages/?name=gstreamer0.10-ffmpeg): 更多的解码器

重启Firefox。你可以到[Youtube HTML5页面](http://www.youtube.com/html5)或者[这个网页](http://www.quirksmode.org/html5/tests/video.html)来验证软件包正确安装并启用了。

你也可以强制Firefox使用Adobe Flash。方法是在`about:config`中设置`media.gstreamer.enabled`为禁用。

## 疑难解答

### 设置 email 客户端

一般地，Firefox 会使用像 Gmail 或 Yahoo Mail 这样的 Web 程序打开 `mailto` 链接。要使 Firefox 用你的email 客户端打开 `mailto` 链接，找到 _选项 > 应用程序_ 并将 `mailto` 对应的_动作_修改为你的 email 客户端的准确路径，如 `/usr/bin/kmail`。

### “打开所在文件夹” 错误 (GNOME3)

如果你希望 Firefox 用 [Nautilus](/index.php?title=Nautilus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Nautilus (简体中文) (page does not exist)") 来 “打开所在文件夹”，而 [Thunar](/index.php/Thunar_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Thunar (简体中文)") 或 [Wine](/index.php/Wine_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wine (简体中文)") 却运行了，请检查 `~/.local/share/applications/defaults.list` 文件中的这两行:

```
inode/directory=_someprogram_.desktop
x-directory/normal=_someprogram_.desktop

```

如果 _someprogram_ 不是 _nautilus_, 就将其修改为 _nautilus_。

### “打开所在文件夹” 错误 (KDE)

KDE中使用“下载”窗口中的“打开所在文件夹”时，如果 Firefox 没使用设置的文件管理器，先在如下位置进行设置：

	**System Settings -> Default Applications -> File Manager**

如果 Firefox 仍不能使用指定的文件管理器打开文件夹，在`$HOME/.local/share/applications/defaults.list` 中添加：

```
x-directory/normal=kde4-dolphin.desktop;kde4-kfmclient_dir.desktop;
inode/directory=kde4-dolphin.desktop;kde4-kfmclient_dir.desktop;kde4-gwenview.desktop;kde4-filelight.desktop;kde4-cervisia.desktop;

```

### Firefox 自动创建 ~/Desktop，但我不需要

Firefox 默认使用 `~/Desktop` 作为上传和下载目录。要设置为其它目录，创建文件 `~/.config/user-dirs.dirs` 并添加：

```
XDG_DESKTOP_DIR="/home/<user>/"
XDG_DOWNLOAD_DIR="/home/<user>/<dir>"
XDG_TEMPLATES_DIR="/home/<user>/<dir>"
XDG_PUBLICSHARE_DIR="/home/<user>/<dir>"
XDG_DOCUMENTS_DIR="/home/<user>/<dir>"
XDG_MUSIC_DIR="/home/<user>/<dir>"
XDG_PICTURES_DIR="/home/<user>/<dir>"
XDG_VIDEOS_DIR="/home/<user>/<dir>"

```

将 `<user>` 和 `<dir>` 修改为实际目录。

### 禁止插件弹窗

有些插件，如Flash，会忽略浏览器设置，弹出窗口。要阻止这种弹窗：

1.  打开 about:config。
2.  右键添加新的整数项目。
3.  命名为 privacy.popups.disable_from_plugins。
4.  设置为2。

可用值如下：

*   0: 允许所有插件弹窗。
*   1: 允许弹窗，但限制在dom.popup_maximum数值内。
*   2: 禁止插件弹窗。
*   3: 禁止插件弹窗，即使是可信站点。

### 中键点击问题

```
! 此 URL 无效，无法载入，

```

许多人使用中键点击时会莫名跳转到某页面，或者出现上述错误。

问题的原因是，许多类UNIX操作系统设置鼠标中键执行粘贴操作。这与Firefox的功能冲突了（在新窗口打开链接）。可以关闭Firefox的这项功能：

在浏览器地址栏输入：

```
about:config

```

打开并找到**middlemouse.contentLoadURL**项，设置为false。

此外，如果要打开中键点击出现滚轮的功能（Windows默认启用），设置**general.autoScroll**为true。

### Backspace 键无法实现“后退”功能

根据[此文](http://ubuntu.wordpress.com/2006/12/21/fix-firefox-backspace-to-take-you-to-the-previous-page/)，为了修正一个bug，关闭了此功能。开启方法如下：

在浏览器地址栏输入：

```
about:config

```

打开并找到**browser.backspace_action**项，设置为0。

### 无法记录登录信息

有可能是[Firefox profile](http://support.mozilla.com/en-US/kb/Profiles#How_to_find_your_profile)文件夹中的`cookies.sqlite`损坏了。关闭浏览器后删除cookie.sqlite即可：

打开终端输入：

```
$ cd ~/.mozilla/firefox/xxxxxxxx.default/
$ rm -f cookies.sqlite

```

**注意:** xxxxxxxx 表示随机生成的8个字符

重启Firefox检查问题是否解决。

### 使用深色GTK主题时文本区域故障

使用深色[GTK](/index.php/GTK "GTK")主题时，可能看不到某些网站输入框和文本区域的文字（白底白字）。这可能是因为某些网站只设置了背景色或文本色，而Firefox主题使用了一样的颜色。

A work around is to explicitly setting standard colours for all web pages in

可以在`~/.mozilla/firefox/xxxxxxxx.default/chrome/userContent.css`设置所有网页的标准色彩配置。

下列代码设置输入框默认白底黑字，默认设置不会覆盖网站自己的设置：

```
input {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

textarea {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

select {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

```

下列代码强制设置色彩（**设置 > 内容 > 颜色**中的“允许页面选择显示颜色而无需使用上面的设置”）：

```
input {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

textarea {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

select {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

```

请自行修改颜色，或者使用附加组件[Stylish](https://addons.mozilla.org/zh-CN/firefox/addon/2108)。

### 文件关联问题

非 [Gnome](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") 用户可能遇到该问题，安装[libgnome](https://www.archlinux.org/packages/?name=libgnome)即可。

如果使用KDE，还可以这样：

```
ln -s ~/.local/share/applications/mimeapps.list ~/.local/share/applications/mimeinfo.cache

```

这样，Firefox应该严格使用KDE的文件关联设置了。

### 关闭Firefox时不询问是否保存标签

根据[Mozilla Support](http://support.mozilla.com/en-US/questions/767751)：

1.  打开**about:config**。
2.  修改**browser.warnOnQuit**为**true**。
3.  修改**browser.showQuitWarning**为**true**.

### Firefox 界面字体很难看

如果菜单栏的字体很难看，可能是因为 Firefox 找不到好看的字体，请先通过[xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1)软件包安装 Type 1 字体。

### Firefox 在某些网页中字体很难看

某些网页的点阵字体显示效果比较差，可以禁用 X 的点阵字体:

```
$ sudo ln -s /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d/

```

### 解决Firefox中与Google字体有关的字体问题

通过安装以下AUR软件包中提供的Google字体： [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 、 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)，亦可解决Firefox中的一些字体问题。这些字体或许会极大地改善Google Drive应用的外观。

### 更新至Firefox 13后菜单无法弹出

这个问题可能与下面链接中报告的bug有关： [bug](https://bugzilla.mozilla.org/show_bug.cgi?id=787943) 并且可能影响任何在设置输入法时设置了以下环境变量的用户：

```
GTK_IM_MODULE=xim

```

这种情况尤其会出现在使用fcitx 4.0.x版本的用户中（当时fcitx仅支持XIM模块）。 版本更新的fcitx中，XIM模块不被推荐，你应该这样设置环境变量：

```
GTK_IM_MODULE=fcitx

```

更多信息请参考 [Fcitx](/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fcitx (简体中文)") 这一页.

### 从Marketplace安装桌面应用失败且无错误提示

安装会静默失败如果没有`~/.local/share/applications`文件夹。

## 参见

*   [官方网站](http://www.mozilla.org/firefox/)
*   [Mozilla 基金会](http://www.mozilla.org/)
*   [Firefox Wiki](https://wiki.mozilla.org/Firefox)
*   [Firefox 扩展组件](https://addons.mozilla.org/)
*   [Firefox 主题](https://addons.mozilla.org/zh-CN/firefox/themes/)