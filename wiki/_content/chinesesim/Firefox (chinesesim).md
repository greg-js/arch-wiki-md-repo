**翻译状态：** 本文是英文页面 [Firefox](/index.php/Firefox "Firefox") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-03，点击[这里](https://wiki.archlinux.org/index.php?title=Firefox&diff=0&oldid=444370)可以查看翻译后英文页面的改动。

[Firefox](https://www.mozilla.org/firefox)（火狐）是[Mozilla](https://www.mozilla.org)（谋智网络）出品的一款图形界面网络浏览器。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 附加组件](#.E9.99.84.E5.8A.A0.E7.BB.84.E4.BB.B6)
*   [3 Configuration](#Configuration)
*   [4 插件](#.E6.8F.92.E4.BB.B6)
    *   [4.1 Gnome Keyring 整合](#Gnome_Keyring_.E6.95.B4.E5.90.88)
    *   [4.2 KDE 整合](#KDE_.E6.95.B4.E5.90.88)
    *   [4.3 拼写检查字典](#.E6.8B.BC.E5.86.99.E6.A3.80.E6.9F.A5.E5.AD.97.E5.85.B8)
    *   [4.4 增加搜索引擎](#.E5.A2.9E.E5.8A.A0.E6.90.9C.E7.B4.A2.E5.BC.95.E6.93.8E)
        *   [4.4.1 arch-firefox-search](#arch-firefox-search)
    *   [4.5 多媒体播放](#.E5.A4.9A.E5.AA.92.E4.BD.93.E6.92.AD.E6.94.BE)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Screenshot of webpage](#Screenshot_of_webpage)
*   [6 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [6.1 Firefox startup takes very long](#Firefox_startup_takes_very_long)
    *   [6.2 Font troubleshooting](#Font_troubleshooting)
    *   [6.3 设置 email 客户端](#.E8.AE.BE.E7.BD.AE_email_.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [6.4 程序关联](#.E7.A8.8B.E5.BA.8F.E5.85.B3.E8.81.94)
        *   [6.4.1 文件关联问题](#.E6.96.87.E4.BB.B6.E5.85.B3.E8.81.94.E9.97.AE.E9.A2.98)
    *   [6.5 Firefox 自动创建 ~/Desktop，但我不需要](#Firefox_.E8.87.AA.E5.8A.A8.E5.88.9B.E5.BB.BA_.7E.2FDesktop.EF.BC.8C.E4.BD.86.E6.88.91.E4.B8.8D.E9.9C.80.E8.A6.81)
    *   [6.6 禁止插件弹窗](#.E7.A6.81.E6.AD.A2.E6.8F.92.E4.BB.B6.E5.BC.B9.E7.AA.97)
    *   [6.7 中键点击问题](#.E4.B8.AD.E9.94.AE.E7.82.B9.E5.87.BB.E9.97.AE.E9.A2.98)
    *   [6.8 Backspace 键无法实现“后退”功能](#Backspace_.E9.94.AE.E6.97.A0.E6.B3.95.E5.AE.9E.E7.8E.B0.E2.80.9C.E5.90.8E.E9.80.80.E2.80.9D.E5.8A.9F.E8.83.BD)
    *   [6.9 无法记录登录信息](#.E6.97.A0.E6.B3.95.E8.AE.B0.E5.BD.95.E7.99.BB.E5.BD.95.E4.BF.A1.E6.81.AF)
    *   [6.10 使用深色GTK主题时文本区域故障](#.E4.BD.BF.E7.94.A8.E6.B7.B1.E8.89.B2GTK.E4.B8.BB.E9.A2.98.E6.97.B6.E6.96.87.E6.9C.AC.E5.8C.BA.E5.9F.9F.E6.95.85.E9.9A.9C)
    *   [6.11 关闭Firefox时不询问是否保存标签](#.E5.85.B3.E9.97.ADFirefox.E6.97.B6.E4.B8.8D.E8.AF.A2.E9.97.AE.E6.98.AF.E5.90.A6.E4.BF.9D.E5.AD.98.E6.A0.87.E7.AD.BE)
    *   [6.12 Firefox 界面字体很难看](#Firefox_.E7.95.8C.E9.9D.A2.E5.AD.97.E4.BD.93.E5.BE.88.E9.9A.BE.E7.9C.8B)
    *   [6.13 Firefox 在某些网页中字体很难看](#Firefox_.E5.9C.A8.E6.9F.90.E4.BA.9B.E7.BD.91.E9.A1.B5.E4.B8.AD.E5.AD.97.E4.BD.93.E5.BE.88.E9.9A.BE.E7.9C.8B)
    *   [6.14 从Marketplace安装桌面应用失败且无错误提示](#.E4.BB.8EMarketplace.E5.AE.89.E8.A3.85.E6.A1.8C.E9.9D.A2.E5.BA.94.E7.94.A8.E5.A4.B1.E8.B4.A5.E4.B8.94.E6.97.A0.E9.94.99.E8.AF.AF.E6.8F.90.E7.A4.BA)
    *   [6.15 Firefox detects the wrong version of my plugin](#Firefox_detects_the_wrong_version_of_my_plugin)
    *   [6.16 Javascript context menu does not appear on some sites](#Javascript_context_menu_does_not_appear_on_some_sites)
    *   [6.17 Firefox does not remember default spell check language](#Firefox_does_not_remember_default_spell_check_language)
    *   [6.18 Some MathML symbols are missing](#Some_MathML_symbols_are_missing)
    *   [6.19 Picture flickers while scrolling](#Picture_flickers_while_scrolling)
    *   [6.20 Tearing video in fullscreen mode](#Tearing_video_in_fullscreen_mode)
    *   [6.21 Firefox looks bad with GTK+ >=3.20](#Firefox_looks_bad_with_GTK.2B_.3E.3D3.20)
*   [7 参见](#.E5.8F.82.E8.A7.81)

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

## 附加组件

Firefox 广为人知的一点是它的大量的附加组件，可以用来添加新功能或更改 Firefox 中已有功能。你可以在 Firefox 中的“附加组件管理器”中查找新附加组件或管理已安装的附加组件。

想查看热门附加组件列表，参见： [按热门度排序的附加组件列表](https://addons.mozilla.org/zh-CN/firefox/extensions/?sort=popular).

## Configuration

Firefox exposes a number of configuration options. To examine them, enter:

```
about:config

```

in the Firefox address bar.

Once set, these affect the user's current profile, and may be synchronized across all devices via [Firefox Sync](https://www.mozilla.org/firefox/sync/). Please note that only a subset of the `about:config` entries are synchronized by this method, and the exact subset may be found by searching for `services.sync.prefs` in `about:config`. Additional preferences and 3rd party preferences may be synchronized by creating new boolean entries prepending the config value with `services.sync.prefs.sync` ([documentation](https://developer.mozilla.org/en-US/docs/Archive/Mozilla/Firefox_Sync/Syncing_custom_preferences) is still applicable.) To synchronize the whitelist for the extension [NoScript](https://addons.mozilla.org/en-US/firefox/addon/noscript/):

```
services.sync.prefs.sync.capability.policy.maonoscript.sites

```

The boolean `noscript.sync.enabled` must be set to true to synchronize the remainder of NoScript's preferences via Firefox Sync.

Firefox also allows configuration for a profile via a `user.js` file: [user.js](http://kb.mozillazine.org/User.js_file) kept in the profile folder, usually `~/.mozilla/firefox/*some name*.default/`. For a useful starting point, see e.g [custom user.js](https://github.com/pyllyukko/user.js) which is targeted at privacy/security conscious users.

One drawback of the above approach is that it is not applied system-wide. Furthermore, this is not useful as a "pre-configuration", since the profile directory is created after first launch of the browser. You can, however, let *firefox* create a new profile and, after closing it again, [copy the contents](https://support.mozilla.org/en-US/kb/back-and-restore-information-firefox-profiles#w_restoring-a-profile-backup) of an already created profile folder into it.

Sometimes it may be desired to lock certain settings, a feature useful in widespread deployments of customized Firefox. In order to create a system-wide configuration, follow the steps outlined in [Locking preferences](http://kb.mozillazine.org/Locking_preferences):

1\. Create `/usr/lib/firefox/defaults/pref/local-settings.js`:

```
pref("general.config.obscure_value", 0);
pref("general.config.filename", "mozilla.cfg");

```

2\. Create `/usr/lib/firefox/mozilla.cfg` (this stores the actual configuration):

```
//
//...your settings...
// e.g to disable Pocket, uncomment the following line
// lockPref("browser.pocket.enabled", false);

```

Please note that the first line must contain exactly `//`. The syntax of the file is similar to that of `user.js`.

## 插件

*参见： [浏览器插件](/index.php/Browser_plugins_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Browser plugins (简体中文)")*

要查看插件使用情况，在Firefox地址栏输入：

```
about:plugins

```

或者使用*工具*菜单中的*附加组件*，选择*插件*标签。

### Gnome Keyring 整合

要整合 Firefox 与 [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring")，安装 Javascript 实现的 [mozilla-extension-gnome-keyring-git](https://aur.archlinux.org/packages/mozilla-extension-gnome-keyring-git/)。要让 firefox-gnome-keyring 使用你的登录 keychain，在 about:config 中设置 extensions.gnome-keyring.keyringName 为 "login" (不含引号)。注意 "login" 的首字母应为小写。

### KDE 整合

**Warning:** Since GTK3 was updated to 3.20.x, there are several broken themes. Including **Breeze**, the recommended theme for integration between KDE and GTK styles. Some of the issues are invisible scroll bars, no text highlight on selection, invisible checkboxes, among others. As a workaround while the themes are upgraded you can do the following after installing [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config), go to `System Settings` -> `Application Style` -> `GNOME Application Style (GTK)` and choose in the **Select a GTK3 Theme** dropdown choose the **Default** theme, also make sure **Show icons in GTK buttons** and **Show icons in GTK** are checked. For further information on the compatibility issue above visit the [GTK3 3.20 upgrade thread](https://bbs.archlinux.org/viewtopic.php?pid=1619076) in the Arch Forums.

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

Firefox会尝试使用[FFmpeg](/index.php/FFmpeg "FFmpeg")播放HTML5的`<audio>`和`<video>`标签内的多媒体内容，需要先安装[FFmpeg](https://www.archlinux.org/packages/?name=FFmpeg)。

重启Firefox。你可以到[Youtube HTML5页面](http://www.youtube.com/html5)或者[这个网页](http://www.quirksmode.org/html5/tests/video.html)来验证软件包正确安装并启用了。

更多配置信息请参阅 [Firefox tweaks#Enable additional media codecs](/index.php/Firefox_tweaks#Enable_additional_media_codecs "Firefox tweaks")。

## Tips and tricks

### Screenshot of webpage

To use Firefox to take a screenshot of a webpage open the developer console using `Shift+F2`. Then type in:

```
screenshot *filename*

```

where *filename* is optional.

To take a screenshot of the entire page, not just the section displayed on the screen, use the `--fullpage` option:

```
screenshot --fullpage *filename*

```

## 疑难解答

### Firefox startup takes very long

If Firefox takes much longer to start up than other browsers, it may be due to lacking configuration of the localhost in `/etc/hosts`. See [Network configuration#Local network hostname resolution](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration") on how to set it up.

### Font troubleshooting

See [Font configuration](/index.php/Font_configuration "Font configuration").

### 设置 email 客户端

一般地，Firefox 会使用像 Gmail 或 Yahoo Mail 这样的 Web 程序打开 `mailto` 链接。要使 Firefox 用你的email 客户端打开 `mailto` 链接，找到 *选项 > 应用程序* 并将 `mailto` 对应的*动作*修改为你的 email 客户端的准确路径，如 `/usr/bin/kmail`。

Outside the browser, `mailto` links are handled by the `x-scheme-handler/mailto` mime type, which can be easily configured with [xdg-mime](/index.php/Xdg-mime "Xdg-mime"). See [Default applications](/index.php/Default_applications "Default applications") for details and alternatives.

### 程序关联

请参考 [Default applications](/index.php/Default_applications "Default applications").

#### 文件关联问题

非 [Gnome](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") 用户可能遇到该问题，安装[libgnome](https://www.archlinux.org/packages/?name=libgnome)即可。

如果使用KDE，还可以这样：

```
ln -s ~/.local/share/applications/mimeapps.list ~/.local/share/applications/mimeinfo.cache

```

这样，Firefox应该严格使用KDE的文件关联设置了。

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

### 使用深色GTK主题时文本区域故障

使用深色[GTK](/index.php/GTK "GTK")主题时，可能看不到某些网站输入框和文本区域的文字（白底白字）。这可能是因为某些网站只设置了背景色或文本色，而Firefox主题使用了一样的颜色。

A work around is to explicitly setting standard colours for all web pages in

可以在`~/.mozilla/firefox/xxxxxxxx.default/chrome/userContent.css`设置所有网页的标准色彩配置。

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

Another workaround is to force Firefox to use a light theme (e.g. "Adwaita:light"):

1.  Copy `/usr/share/applications/firefox.desktop` to `~/.local/share/applications/firefox.desktop` and replace all occurrences of `Exec=firefox` with `Exec=env GTK_THEME=Adwaita:light firefox`.
2.  Close all running instances of Firefox and restart your window manager/desktop environment.

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

### 从Marketplace安装桌面应用失败且无错误提示

安装会静默失败如果没有`~/.local/share/applications`文件夹。

### Firefox detects the wrong version of my plugin

When you close Firefox, the latter saves the current timestamp and version of your plugins inside `pluginreg.dat` located in your profile folder, typically in `~/.mozilla/firefox/*some name*.default/`.

If you upgraded your plugin when Firefox was still running, you will thus have the wrong information inside that file. The next time you will restart Firefox you will get that message `Firefox has prevented the outdated plugin "XXXX" from running on ...` when you will be trying to open content dedicated to that plugin on the web. This problem often appears with the official [Adobe Flash Player plugin](/index.php/Browser_plugins#Flash_Player "Browser plugins") which has been upgraded while Firefox was still running.

The solution is to remove the file `pluginreg.dat` from your profile and that is it. Firefox will not complain about the missing file as it will be recreated the next time Firefox will be closed. [[1]](https://bugzilla.mozilla.org/show_bug.cgi?id=1109795#c16)

### Javascript context menu does not appear on some sites

In `about:config`, unset the `dom.w3c_touch_events.enabled` setting.

### Firefox does not remember default spell check language

The default spell checking language can be set as follows:

1.  Type `about:config` in the address bar.
2.  Set `spellchecker.dictionary` to your language of choice, for instance `en_GB`.
3.  Notice that the for dictionaries installed as a Firefox plugin the notation is `en-GB`, and for [hunspell](https://www.archlinux.org/packages/?name=hunspell) dictionaries the notation is `en_GB`.

When you only have system wide dictionaries installed with [hunspell](https://www.archlinux.org/packages/?name=hunspell), Firefox might not remember your default dictionary language settings. This can be fixed by having at least one [dictionary](https://addons.mozilla.org/firefox/language-tools/) installed as a Firefox plugin. Notice that now you will also have a tab **Dictionaries** in **add-ons**.

Related questions on the **StackExchange** platform: [[2]](http://stackoverflow.com/questions/26936792/change-firefox-spell-check-default-language/29446115), [[3]](http://stackoverflow.com/questions/21542515/change-default-language-on-firefox/29446353), [[4]](http://askubuntu.com/questions/184300/how-can-i-change-firefoxs-default-dictionary/576877)

Related bug reports: [Bugzilla 776028](https://bugzilla.mozilla.org/show_bug.cgi?id=776028), [Ubuntu bug 1026869](https://bugs.launchpad.net/ubuntu/+source/firefox/+bug/1026869)

### Some MathML symbols are missing

You need some Math fonts, namely Latin Modern Math and STIX (see this MDN page: [[5]](https://developer.mozilla.org/en-US/docs/Mozilla/MathML_Project/Fonts#Linux)), to display MathML correctly.

In Arch Linux, these fonts are provided by [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) **and** [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra), but they are not available to fontconfig by default. See [TeX Live#Fonts](/index.php/TeX_Live#Fonts "TeX Live") for details. You can also try other [Math fonts](/index.php/Fonts#Math "Fonts").

### Picture flickers while scrolling

**Note:** Problem available in some MATE desktops

Uncheck the "smooth scrolling" settings:

```
Edit > Settings > Advanced > General > Use smooth scrolling

```

### Tearing video in fullscreen mode

If you are using the Xorg Intel or Nouveau drivers and experience tearing video in fullscreen mode, try [Firefox tweaks#Enable OpenGL Off-Main-Thread Compositing (OMTC)](/index.php/Firefox_tweaks#Enable_OpenGL_Off-Main-Thread_Compositing_.28OMTC.29 "Firefox tweaks").

### Firefox looks bad with GTK+ >=3.20

Firefox (as of version 47) [does not support](https://bugzilla.mozilla.org/show_bug.cgi?id=1264079) GTK+ >=3.20 and may look unsightly as a result. A possible resolution is compiling Firefox against GTK2 instead, see [firefox-gtk2](https://aur.archlinux.org/packages/firefox-gtk2/). Alternatively, you may use [markzz's repository](/index.php/Unofficial_user_repositories#markzz "Unofficial user repositories") for pre-built GTK2 Firefox packages.

## 参见

*   [官方网站](http://www.mozilla.org/firefox/)
*   [Mozilla 基金会](http://www.mozilla.org/)
*   [Firefox Wiki](https://wiki.mozilla.org/Firefox)
*   [Firefox 扩展组件](https://addons.mozilla.org/)
*   [Firefox 主题](https://addons.mozilla.org/zh-CN/firefox/themes/)