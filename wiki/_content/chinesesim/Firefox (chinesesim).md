相关文章

*   [浏览器插件](/index.php/Browser_Plugins_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Browser Plugins (简体中文)")
*   [Firefox tweaks](/index.php/Firefox_tweaks "Firefox tweaks")
*   [Chromium](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)")
*   [Opera](/index.php/Opera "Opera")

**翻译状态：** 本文是英文页面 [Firefox](/index.php/Firefox "Firefox") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-02-03，点击[这里](https://wiki.archlinux.org/index.php?title=Firefox&diff=0&oldid=444370)可以查看翻译后英文页面的改动。

[Firefox](https://www.mozilla.org/firefox)（火狐）是[Mozilla](https://www.mozilla.org)（谋智网络）出品的一款图形界面网络浏览器。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 附加组件](#.E9.99.84.E5.8A.A0.E7.BB.84.E4.BB.B6)
    *   [3.1 Gnome Keyring 整合](#Gnome_Keyring_.E6.95.B4.E5.90.88)
    *   [3.2 KDE 整合](#KDE_.E6.95.B4.E5.90.88)
    *   [3.3 拼写检查字典](#.E6.8B.BC.E5.86.99.E6.A3.80.E6.9F.A5.E5.AD.97.E5.85.B8)
    *   [3.4 增加搜索引擎](#.E5.A2.9E.E5.8A.A0.E6.90.9C.E7.B4.A2.E5.BC.95.E6.93.8E)
        *   [3.4.1 arch-firefox-search](#arch-firefox-search)
    *   [3.5 多媒体播放](#.E5.A4.9A.E5.AA.92.E4.BD.93.E6.92.AD.E6.94.BE)
        *   [3.5.1 Open-with extension](#Open-with_extension)
*   [4 小技巧](#.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [4.1 网页截图](#.E7.BD.91.E9.A1.B5.E6.88.AA.E5.9B.BE)
*   [5 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [5.1 Firefox 启动时间太长](#Firefox_.E5.90.AF.E5.8A.A8.E6.97.B6.E9.97.B4.E5.A4.AA.E9.95.BF)
    *   [5.2 字体问题](#.E5.AD.97.E4.BD.93.E9.97.AE.E9.A2.98)
    *   [5.3 设置 email 客户端](#.E8.AE.BE.E7.BD.AE_email_.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [5.4 文件关联](#.E6.96.87.E4.BB.B6.E5.85.B3.E8.81.94)
    *   [5.5 Firefox 自动创建 ~/Desktop，但我不需要](#Firefox_.E8.87.AA.E5.8A.A8.E5.88.9B.E5.BB.BA_.7E.2FDesktop.EF.BC.8C.E4.BD.86.E6.88.91.E4.B8.8D.E9.9C.80.E8.A6.81)
    *   [5.6 禁止插件弹窗](#.E7.A6.81.E6.AD.A2.E6.8F.92.E4.BB.B6.E5.BC.B9.E7.AA.97)
    *   [5.7 中键点击问题](#.E4.B8.AD.E9.94.AE.E7.82.B9.E5.87.BB.E9.97.AE.E9.A2.98)
    *   [5.8 Backspace 键无法实现“后退”功能](#Backspace_.E9.94.AE.E6.97.A0.E6.B3.95.E5.AE.9E.E7.8E.B0.E2.80.9C.E5.90.8E.E9.80.80.E2.80.9D.E5.8A.9F.E8.83.BD)
    *   [5.9 无法记录登录信息](#.E6.97.A0.E6.B3.95.E8.AE.B0.E5.BD.95.E7.99.BB.E5.BD.95.E4.BF.A1.E6.81.AF)
    *   [5.10 使用深色 GTK+ 主题时文本区域故障](#.E4.BD.BF.E7.94.A8.E6.B7.B1.E8.89.B2_GTK.2B_.E4.B8.BB.E9.A2.98.E6.97.B6.E6.96.87.E6.9C.AC.E5.8C.BA.E5.9F.9F.E6.95.85.E9.9A.9C)
    *   [5.11 关闭Firefox时不询问是否保存标签](#.E5.85.B3.E9.97.ADFirefox.E6.97.B6.E4.B8.8D.E8.AF.A2.E9.97.AE.E6.98.AF.E5.90.A6.E4.BF.9D.E5.AD.98.E6.A0.87.E7.AD.BE)
    *   [5.12 从Marketplace安装桌面应用失败且无错误提示](#.E4.BB.8EMarketplace.E5.AE.89.E8.A3.85.E6.A1.8C.E9.9D.A2.E5.BA.94.E7.94.A8.E5.A4.B1.E8.B4.A5.E4.B8.94.E6.97.A0.E9.94.99.E8.AF.AF.E6.8F.90.E7.A4.BA)
    *   [5.13 Firefox 错误地认为插件过时](#Firefox_.E9.94.99.E8.AF.AF.E5.9C.B0.E8.AE.A4.E4.B8.BA.E6.8F.92.E4.BB.B6.E8.BF.87.E6.97.B6)
    *   [5.14 在一些网页中，Javascript 上下文菜单不显示](#.E5.9C.A8.E4.B8.80.E4.BA.9B.E7.BD.91.E9.A1.B5.E4.B8.AD.EF.BC.8CJavascript_.E4.B8.8A.E4.B8.8B.E6.96.87.E8.8F.9C.E5.8D.95.E4.B8.8D.E6.98.BE.E7.A4.BA)
    *   [5.15 Firefox 不保存默认的拼写检查语言](#Firefox_.E4.B8.8D.E4.BF.9D.E5.AD.98.E9.BB.98.E8.AE.A4.E7.9A.84.E6.8B.BC.E5.86.99.E6.A3.80.E6.9F.A5.E8.AF.AD.E8.A8.80)
    *   [5.16 一些 MathML 符号消失了](#.E4.B8.80.E4.BA.9B_MathML_.E7.AC.A6.E5.8F.B7.E6.B6.88.E5.A4.B1.E4.BA.86)
    *   [5.17 滚动时图片闪烁](#.E6.BB.9A.E5.8A.A8.E6.97.B6.E5.9B.BE.E7.89.87.E9.97.AA.E7.83.81)
    *   [5.18 全屏模式下视频断裂](#.E5.85.A8.E5.B1.8F.E6.A8.A1.E5.BC.8F.E4.B8.8B.E8.A7.86.E9.A2.91.E6.96.AD.E8.A3.82)
    *   [5.19 GTK+ >=3.20 时 Firefox 看起来很丑](#GTK.2B_.3E.3D3.20_.E6.97.B6_Firefox_.E7.9C.8B.E8.B5.B7.E6.9D.A5.E5.BE.88.E4.B8.91)
*   [6 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [firefox](https://www.archlinux.org/packages/?name=firefox).中文界面请安装简体中文语言包 [firefox-i18n-zh-cn](https://www.archlinux.org/packages/?name=firefox-i18n-zh-cn)。

其它变种：

*   **Firefox Extended Support Release** — 长期支持版本

	[https://www.mozilla.org/firefox/organizations/](https://www.mozilla.org/firefox/organizations/) || [firefox-esr](https://aur.archlinux.org/packages/firefox-esr/) or [firefox-esr-bin](https://aur.archlinux.org/packages/firefox-esr-bin/)

*   **Firefox Beta** — 前沿版本

	[https://www.mozilla.org/firefox/channel/#beta](https://www.mozilla.org/firefox/channel/#beta) || [firefox-beta](https://aur.archlinux.org/packages/firefox-beta/) or [firefox-beta-bin](https://aur.archlinux.org/packages/firefox-beta-bin/)

*   **Firefox Developer Editi/Aurora** — 开发者版本

	[https://www.mozilla.org/firefox/channel/#developer](https://www.mozilla.org/firefox/channel/#developer) || [firefox-aurora](https://aur.archlinux.org/packages/firefox-aurora/)

*   **Firefox Nightly** — 每日构建的测试版本

	[https://nightly.mozilla.org/](https://nightly.mozilla.org/) || [firefox-nightly](https://aur.archlinux.org/packages/firefox-nightly/)

*   **Firefox KDE** — OpenSUSE 打过补丁的、具有更好的 KDE 集成特性的 Firefox 版本。

	[https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox](https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox) || [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

*   除了不同的编译渠道，有些特殊的分支版本提供了一些特殊功能，参考 [List of applications#Gecko-based](/index.php/List_of_applications#Gecko-based "List of applications").

[这里](https://wiki.mozilla.org/Releases)包含了不同版本的说明.

## 配置

Firefox有许多可用的配置选项。要检查它们，请在Firefox地址栏中输入：

```
 about：config

```

一旦设置，这些就会影响用户的当前配置文件，并可能通过Firefox Sync跨设备同步。请注意，只有`about:config`条目的一部分被这个方法同步，并且可以通过在`about:config`中搜索services.sync.prefs找到确切的子集。可以通过创建新的布尔条目来同步其他偏好设置和第三方偏好设置，并在`services.sync.prefs.sync`前添加config值。同步NoScript扩展名的白名单：

```
 services.sync.prefs.sync.capability.policy.maonoscript.sites

```

必须将`boolean noscript.sync.enabled`设置为`true`才能通过Firefox Sync同步NoScript的其他偏好设置。

Firefox还允许通过`user.js`文件配置一个配置文件：`user.js`保存在配置文件文件夹中，通常是`~/.mozilla/firefox/xxxxxxx.default/`。 上述方法的一个缺点是不能在系统范围内应用。此外，由于配置文件目录是在首次启动浏览器之后创建的，因此这不适用于预配置。不过，你可以让 Firefox创建一个新的配置文件，并在关闭它之后，将已经创建的配置文件文件夹的内容复制进去。

有时可能需要锁定某些设置，这是一项在定制的Firefox的广泛部署中非常有用的功能。要创建系统范围配置，请按照“锁定”首选项中列出的步骤操作：

1.创建/usr/lib/firefox/defaults/pref/local-settings.js：

```
 pref（“general.config.obscure_value”，0）;
 pref（“general.config.filename”，“mozilla.cfg”）;

```

2.创建/usr/lib/firefox/mozilla.cfg（这存储实际配置）：

请注意，第一行必须包含//。该文件的语法与user.js的语法很相似。

## 附加组件

*参见： [浏览器插件](/index.php/Browser_plugins_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Browser plugins (简体中文)")*

Firefox 广为人知的一点是它的大量的附加组件，可以用来添加新功能或更改 Firefox 中已有功能。你可以在 Firefox 中的“附加组件管理器”中查找新附加组件或管理已安装的附加组件。

要查看插件使用情况，在Firefox地址栏输入：

```
about:plugins

```

或者使用*工具*菜单中的*附加组件*，选择*插件*标签。

### Gnome Keyring 整合

要整合 Firefox 与 [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")，安装 Javascript 实现的 [mozilla-extension-gnome-keyring-git](https://aur.archlinux.org/packages/mozilla-extension-gnome-keyring-git/)。要让 firefox-gnome-keyring 使用你的登录 keychain，在 about:config 中设置 extensions.gnome-keyring.keyringName 为 "login" (不含引号)。注意 "login" 的首字母应为小写。

### KDE 整合

**警告:** 由于GTK3更新到3.20.x，有一些主题不能正常使用（包括Breeze，推荐的一个KDE和GTK间的整合主题）。 其中的一些问题是滚动条不可见，不选中的文本高亮显示，隐藏的复选框等等。 若要解决这个问题，安装kde-gtk-config后，进入系统设置 - >应用程序样式 - > GNOME应用程序样式（GTK），然后在选择GTK3主题下拉菜单中选择默认主题。 有关上述兼容性问题的更多信息，请访问Arch Forums中的有关GTK3 3.20 更新的帖子。

*   在 Firefox 中使用 GTK 外观。安装 [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) 和 [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)。然后进入系统设置 -> 程序外观 -> GTK，GTK2/GTK3 主题选择为 Breeze，勾选显示 GTK 按钮的图标。

*   使用 KDE's KParts 嵌入文件查看器，可以安装 [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin)。

*   可以使用 AUR 中的 [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/) Firefox 变种来集成 KDE 的文件关联系统和文件对话框。

*   有些插件也提供了其它整合，比如集成 [KWallet](https://addons.mozilla.org/firefox/addon/kde-wallet-password-integratio/), [Unityfox Revived](https://addons.mozilla.org/firefox/addon/unityfox-revived/), 和 [Plasma 通知](https://addons.mozilla.org/firefox/addon/plasmanotify/).

### 拼写检查字典

选择任意文本，右键为该语言添加字典，重启浏览器即可。

或者从 [官方软件仓库](/index.php/Official_repositories "Official repositories")安装软件包[hunspell](https://www.archlinux.org/packages/?name=hunspell)和其它语言例如 [hunspell-fr](https://www.archlinux.org/packages/?name=hunspell-fr) (法语) or [hunspell-he](https://www.archlinux.org/packages/?name=hunspell-he) (希伯来语)。

默认情况下，Firefox 会在 `/usr/lib/firefox/dictionaries` 生成指向到 hunspell 字典的软链接。如果你不想使用所有语言的字典，可以删掉一部分。注意，Firefox 升级可能会还原这些软链接。

### 增加搜索引擎

到下面网址选择搜索引擎并安装：

*   [https://addons.mozilla.org/firefox/search-tools/](https://addons.mozilla.org/firefox/search-tools/)
*   [http://mycroft.mozdev.org/](http://mycroft.mozdev.org/)

[add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) 扩展可以通过网址直接加入搜索引擎。

#### arch-firefox-search

[arch-firefox-search](https://www.archlinux.org/packages/?name=arch-firefox-search)为Firefox搜索框添加Arch相关内容的搜索引擎（AUR、wiki、论坛……)：

```
# pacman -S arch-firefox-search

```

### 多媒体播放

Firefox会尝试使用[FFmpeg](/index.php/FFmpeg "FFmpeg")播放HTML5的`<audio>`和`<video>`标签内的多媒体内容，需要先安装[ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg)。

重启Firefox。你可以到[Youtube HTML5页面](http://www.youtube.com/html5)或者[这个网页](http://www.quirksmode.org/html5/tests/video.html)来验证软件包正确安装并启用了。

更多配置信息请参阅 [Firefox tweaks#Enable additional media codecs](/index.php/Firefox_tweaks#Enable_additional_media_codecs "Firefox tweaks")。

Starting with version 54, Firefox uses [PulseAudio](/index.php/PulseAudio "PulseAudio") for audio playback and capture. For sound to work, you need to install the [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) package.

In case, for whatever reason, [PulseAudio](/index.php/PulseAudio "PulseAudio") is not an option for you, you can use [apulse](/index.php/Advanced_Linux_Sound_Architecture#PulseAudio_compatibility "Advanced Linux Sound Architecture") instead. To make this work, it is necessary to exclude `/dev/snd/` from Firefox' sandboxing by adding it to the comma-separated list in `about:config`:

```
security.sandbox.content.write_path_whitelist

```

**Note:** The trailing slash on `/dev/snd/` is important, otherwise apulse will report "Permission denied" errors.

If you are using Firefox 58 or above and have no audio even when using apulse, try adding `16` to `security.sandbox.content.syscall_whitelist` in `about:config`

#### Open-with extension

1.  Install [Open-with](https://addons.mozilla.org/firefox/addon/open-with/) add-on.
2.  Open `about:openwith`, select *Add...*
3.  In the dialog select a video streaming capable player (e.g. [/usr/bin/mpv](/index.php/Mpv "Mpv")).
4.  (Optional step) Add needed arguments to the player (e.g. you may want `--force-window --ytdl` for *mpv*)
5.  (Optional step) Choose how to display the dialogs using the left panel.
6.  Right click on links or visit pages containing videos. If the site is supported, the player will open as expected.

The same procedure can be used to associate video downloaders such as *youtube-dl*.

## 小技巧

### 网页截图

要使用 Firefox 进行网页截图，使用 `Shift+F2` 打开开发者控制台。然后输入：

```
screenshot *filename*

```

其中 *filename* 是可选的。

要对整个页面进行截图而不仅仅是当前屏幕，使用 `--fullpage` 选项：

```
screenshot --fullpage *filename*

```

## 疑难解答

### Firefox 启动时间太长

如果 Firefox 启动时间比其它浏览器更长，这可能是因为 `/etc/hosts` 里没有设置 localhost。查看 [Network configuration#Local network hostname resolution](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration") 了解怎么设置。

### 字体问题

查看 [Font configuration](/index.php/Font_configuration "Font configuration").

### 设置 email 客户端

一般地，Firefox 会使用像 Gmail 或 Yahoo Mail 这样的 Web 程序打开 `mailto` 链接。要使 Firefox 用你的email 客户端打开 `mailto` 链接，找到 *选项 > 应用程序* 并将 `mailto` 对应的*动作*修改为你的 email 客户端的准确路径，如 `/usr/bin/kmail`。

`mailto`链接由`x-scheme-handler/mailto` mime类型处理，可以使用`xdg-mime`轻松配置。 有关详细信息和备选方法，请参阅『默认应用程序』

### 文件关联

请参考 [Default applications](/index.php/Default_applications "Default applications").

### Firefox 自动创建 ~/Desktop，但我不需要

Firefox 默认使用 `~/Desktop` 作为上传和下载目录。按 [XDG user directories](/index.php/XDG_user_directories "XDG user directories") 中的说明修改 `XDG_DESKTOP_DIR`.

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

### 使用深色 GTK+ 主题时文本区域故障

使用深色 [GTK+](/index.php/GTK%2B "GTK+") 主题时，可能看不到某些网站输入框和文本区域的文字（例如：Amazon 会显示白底白字）。这可能是因为某些网站只设置了背景色或文本色，而 Firefox 主题使用了一样的颜色。[Text Contrast for Dark Themes](https://addons.mozilla.org/firefox/addon/text-contrast-for-dark-themes/) 扩展可以根据需要正确的设置颜色.

另一种方法是在 `~/.mozilla/firefox/xxxxxxxx.default/chrome/userContent.css` 明确地设置所有网页的标准色彩或者使用 [stylish](https://addons.mozilla.org/firefox/addon/stylish/) 插件.

**Note:** 如果你想让地址栏和搜索栏都是白色，删除前两个 `:not` CSS 选择器.

```
input:not(.urlbar-input):not(.textbox-input):not(.form-control):not([type='checkbox']) {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

#downloads-indicator-counter {
    color: white;
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

还可以强制 Firefox 使用亮色的主题 (例如 "Adwaita:light")：

1.  把 `/usr/share/applications/firefox.desktop` 复制到 `~/.local/share/applications/firefox.desktop`，然后将所有的 `Exec=firefox` 替换成 `Exec=env GTK_THEME=Adwaita:light firefox`.
2.  关闭所有的 Firefox 实例然后重启窗口管理器/桌面环境.

### 关闭Firefox时不询问是否保存标签

根据[Mozilla Support](http://support.mozilla.com/en-US/questions/767751)：

1.  打开**about:config**。
2.  修改**browser.warnOnQuit**为**true**。
3.  修改**browser.showQuitWarning**为**true**.

### 从Marketplace安装桌面应用失败且无错误提示

安装会静默失败如果没有`~/.local/share/applications`文件夹。

### Firefox 错误地认为插件过时

关闭Firefox时，后者会将当前的时间戳和插件版本保存在配置文件文件夹中的pluginreg.dat中，通常在 `~/.mozilla/firefox/some name.default/` 中。

如果Firefox在运行时升级了插件，则会在该文件中包含错误的信息。 当你下一次重启 Firefox 时，会报告一个错误『Firefox已经阻止了过时的插件“插件名称”在运行』。这个问题通常出现在官方的Adobe Flash Player插件上，而Firefox在运行时已经升级。

解决方案是从您的配置文件中删除文件pluginreg.dat。事实上，Firefox不会由于丢失的文件而停止运行，因为下次Firefox关闭时，它将被重新创建。 [[1]](https://bugzilla.mozilla.org/show_bug.cgi?id=1109795#c16)

### 在一些网页中，Javascript 上下文菜单不显示

在 `about:config` 取消 `dom.w3c_touch_events.enabled` 设置.

### Firefox 不保存默认的拼写检查语言

默认的拼写检查语言可以用下面的方式设置：

1.  在地址栏中打开 `about:config`.
2.  把 `spellchecker.dictionary` 设置为你的语言，例如 `en_GB`.
3.  注意对于 Firefox 安装的词典插件来说，符号是 `en-GB`，而对于 [hunspell](https://www.archlinux.org/packages/?name=hunspell) 词典来说，符号是 `en_GB`.

当你只有 [hunspell](https://www.archlinux.org/packages/?name=hunspell) 词典时, Firefox 可能不会保存你默认的词典语言设置。要解决这个问题，你可以添加至少一个 [词典](https://addons.mozilla.org/firefox/language-tools/) 插件. 注意现在附加组件中也会有词典栏.

**StackExchange** 上的相关问题: [[2]](http://stackoverflow.com/questions/26936792/change-firefox-spell-check-default-language/29446115), [[3]](http://stackoverflow.com/questions/21542515/change-default-language-on-firefox/29446353), [[4]](http://askubuntu.com/questions/184300/how-can-i-change-firefoxs-default-dictionary/576877)

相关的漏洞报告: [Bugzilla 776028](https://bugzilla.mozilla.org/show_bug.cgi?id=776028), [Ubuntu bug 1026869](https://bugs.launchpad.net/ubuntu/+source/firefox/+bug/1026869)

### 一些 MathML 符号消失了

你需要一些数学字体，比如 Latin Modern Math 和 STIX (查看这个 MDN 页面: [[5]](https://developer.mozilla.org/en-US/docs/Mozilla/MathML_Project/Fonts#Linux)) 以正确的显示 MathML.

在 Arch Linux 中，[texlive-core](https://www.archlinux.org/packages/?name=texlive-core) 和 [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra) 提供了这些字体，但是默认情况下设置字体却无法使用它们. 详情参见 [TeX Live#Fonts](/index.php/TeX_Live#Fonts "TeX Live"). 你也可以尝试 [Math fonts](/index.php/Fonts#Math "Fonts").

### 滚动时图片闪烁

**Note:** 在一些 MATE 桌面下会出现

设置中取消选中 "smooth scrolling"：

```
编辑 > 设置 > 高级 > 通用 > 使用平滑滚动

```

### 全屏模式下视频断裂

如果你使用 Xorg Intel 或者 Nouveau 驱动并且感觉全屏模式下视频有撕裂感，试试 [Firefox tweaks#Enable OpenGL Off-Main-Thread Compositing (OMTC)](/index.php/Firefox_tweaks#Enable_OpenGL_Off-Main-Thread_Compositing_.28OMTC.29 "Firefox tweaks").

### GTK+ >=3.20 时 Firefox 看起来很丑

**Note:** Firefox 在 53 版本中移除了 GTK2 支持， 并且会在 2018 年年中之前一直支持 ESR 52 版本.

Firefox (从 47 版本开始) [不支持](https://bugzilla.mozilla.org/show_bug.cgi?id=1264079) GTK+ >=3.20 并且可能看起来很难看。一种办法是编译 Firefox 取消 GTK2 支持, 参见 [firefox-esr-gtk2](https://aur.archlinux.org/packages/firefox-esr-gtk2/). 另外，你可以使用 [markzz's repository](/index.php/Unofficial_user_repositories#markzz "Unofficial user repositories") 或者 [archlinuxcn's](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") (x86_64 only) 的预编译 GTK2 Firefox 包.

## 参见

*   [官方网站](http://www.mozilla.org/firefox/)
*   [Mozilla 基金会](http://www.mozilla.org/)
*   [Firefox Wiki](https://wiki.mozilla.org/Firefox)
*   [Firefox 扩展组件](https://addons.mozilla.org/)
*   [Firefox 主题](https://addons.mozilla.org/zh-CN/firefox/themes/)