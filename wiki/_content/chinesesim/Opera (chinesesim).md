Related articles

*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Firefox](/index.php/Firefox "Firefox")
*   [Chromium](/index.php/Chromium "Chromium")

**翻译状态：** 本文是英文页面 [Opera](/index.php/Opera "Opera") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-3-1，点击[这里](https://wiki.archlinux.org/index.php?title=Opera&diff=0&oldid=469197)可以查看翻译后英文页面的改动。

[Opera](http://www.opera.com)浏览器，是一款自1994年以来由挪威[Opera Software](https://en.wikipedia.org/wiki/Opera_Software "wikipedia:Opera Software")公司开发的免费浏览器软件。该浏览器因曾经最先引入诸如标签式浏览、内置搜索等功能而闻名。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 旧的 Presto 版本](#旧的_Presto_版本)
*   [2 插件](#插件)
    *   [2.1 Adblock](#Adblock)
*   [3 性能调整](#性能调整)
    *   [3.1 禁用功能和服务](#禁用功能和服务)
    *   [3.2 Profile in tmpfs](#Profile_in_tmpfs)
*   [4 外观](#外观)
    *   [4.1 主题](#主题)
    *   [4.2 标题栏](#标题栏)
    *   [4.3 标签模式](#标签模式)
    *   [4.4 字体](#字体)
*   [5 私有标签](#私有标签)
*   [6 辅助功能提示](#辅助功能提示)
    *   [6.1 禁用文本选择](#禁用文本选择)
    *   [6.2 抓取和滚动模式](#抓取和滚动模式)
    *   [6.3 长按链接会在后台标签（扩展程序）中打开它](#长按链接会在后台标签（扩展程序）中打开它)
    *   [6.4 虚拟屏幕键盘 (扩展程序)](#虚拟屏幕键盘_(扩展程序))
*   [7 Security](#Security)
    *   [7.1 Force a password store](#Force_a_password_store)
*   [8 故障排除](#故障排除)
    *   [8.1 NVIDIA 显卡上出现条纹](#NVIDIA_显卡上出现条纹)
    *   [8.2 卧式鼠标滚轮滚动](#卧式鼠标滚轮滚动)
    *   [8.3 启动外部浏览器](#启动外部浏览器)
    *   [8.4 使用 GTK + 2.24.7+ 开始或关闭时，Opera 崩溃的问题](#使用_GTK_+_2.24.7+_开始或关闭时，Opera_崩溃的问题)
    *   [8.5 带有深色GTK +主题的不可读输入字段和地址栏](#带有深色GTK_+主题的不可读输入字段和地址栏)
*   [9 参见](#参见)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [opera](https://www.archlinux.org/packages/?name=opera) 软件包

### 旧的 Presto 版本

现在的 Opera 浏览器使用现代的、开源的 Blick 引擎。你仍然可以通安装 Opera 12.16 即 [opera-legacy](https://aur.archlinux.org/packages/opera-legacy/) 软件包，来使用旧版的 Presto 布局引擎。因安全性及与现代互联网的兼容性，不建议使用Presto布局引擎的Opera。想体验旧版界面可以安装Opera旧成员开发的[Vivaldi](/index.php/Vivaldi "Vivaldi")浏览器。

## 插件

有关不同插件和安装说明的详细信息，请参阅[Browser plugins](/index.php/Browser_plugins "Browser plugins")。注意，Opera不再支持Netscape插件API（NPAPI），而只支持较新的Pepper插件API（PPAPI）。

### Adblock

**提示：** Opera也有一个内置的广告拦截器，可以在设置中启用。

安装 [opera-adblock-complete](https://aur.archlinux.org/packages/opera-adblock-complete/) 软件包以获取 Adblock 支持。

## 性能调整

虽然Opera在现代硬件上运行相当快，但可以进一步调整。有关更多示例，请参阅 [Opera Wiki page](http://operawiki.info/operaperformance)。

### 禁用功能和服务

如要最大化应用程序性能，可以通过[opera:config Preferences Editor.](http://www.opera.com/browser/tutorials/personalize/behavior/)禁用不需要的功能和服务。

一些不需要的功能：

*   **Systray Icon**: 在 opera:config#UserPrefs 中取消选中 *Show Tray Icon*.
*   **BitTorrent**: 在 opera:config#BitTorrent 中取消选中 *Enable* .
*   **Geolocation**: 在 opera:config#Geolocation 中取消选中 *Enable geolocation* .
*   **Multimedia**: 在 opera:config#Multimedia 中取消选中 desired options.
*   **Web Server**: 在 opera:config#Web Server 中取消选中 *Enable* .

为了更容易找到这些选项，只需在地址栏中输入相应的路径（无空格）即可。 例如 `opera:config#UserPrefs|ShowTrayIcon`或者使用内置搜索。

### Profile in tmpfs

将浏览器配置文件重新定位到[tmpfs](/index.php/Tmpfs "Tmpfs")文件系统，包括 `/tmp`，以改进应用程序响应，因为整个配置文件现在都存储在RAM中。另一个好处是减少了磁盘读写操作，其于SSD最为有利。

目前有两种方法：

*   使用[Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon")，自动检测并将Opera配置文件重定位到tmpfs。
*   使用 `-pd`命令行标志告诉Opera在哪里存储其配置文件数据：

```
$ opera -pd /tmp/opera

```

## 外观

### 主题

虽然Opera是跨平台的，但它可以很好地集成到各种Linux桌面环境中。

	Qt

	要使菜单外观与Qt更好地融合，安装并通过`qtconfig`应用您想要的Qt主题。

	KDE

	要使Opera使用KDE图标，您可以安装一个KDE主题，比如[这个](https://addons.opera.com/en/themes/details/aire-kde/?display=en)。

	GTK+

	可以在[这里](http://my.opera.com/community/customize/skins/info/?id=3465).找到一个使用Tango图标的GTK +皮肤。

### 标题栏

通过右键单击选项卡栏，然后取消选中“显示边框”，可以隐藏标题栏。

### 标签模式

Opera原生支持标签级联和平铺模式上。可以通过激活“主”工具栏或通过拖放所需的任何位置上的按钮可以找到适当的按钮 *Menu > Appearance > Buttons > Browser*.

### 字体

可以在 *Settings > Preferences... > Advanced > Fonts*下配置字体.

如果在第一次运行Opera之前已经安装[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)软件包，Opera将默认使用这些字体，而不管本地GTK +选项，GNOME或KDE字体管理指定什么。如要强制已经安装的Opera使用系统设置选项：

*   关闭所有正在运行的Opera实例。
*   卸载 [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) 软件包.
*   移动现有配置文件文件夹： `mv -i ~/.opera ~/.opera.bak`
*   打开Opera，并验证您的字体管理器设置是否已应用。
*   将`~/.opera.bak` 中书签和所需的过滤器文件还原至 `~/.opera`， `operaprefs.ini` 文件除外.
*   如果需要，请重新安装 [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) 软件包.

**Note:** 如果除了数字之外没有文本显示在某些网页上，这可能是字体的问题。 导致这个问题的一个已知问题是 *helvetica* pfb postscript字体。

## 私有标签

要浏览而不留下您访问的网站的明显痕迹，您可以使用私有标签。关闭私有标签时，将删除与该标签相关的以下数据：

*   Cache
*   Cookies
*   History
*   Logins

这与 Chrome/[Chromium](/index.php/Chromium "Chromium") 中的 [--incognito option](http://www.google.com/support/chrome/bin/answer.py?hl=en&answer=95464) 和 [Firefox](/index.php/Firefox "Firefox") 中的 [PrivateBrowsing](https://wiki.mozilla.org/PrivateBrowsing) 很相似.

要从命令行打开新的私有标签，请使用：

```
$ opera -newprivatetab

```

要确保在整个浏览会话期间只使用私有标签页：

*   设置 *Settings > Preferences... > General > Startup > Start without open tabs*.
*   清除 *Settings > Preferences... > General > Home page option* 中的所有条目.
*   启用 *Settings > Preferences... > Advanced > Tabs > Additional tab options... > Allow windows with no tabs*.

要在已经运行Opera时打开一个新窗口进行隐身浏览，您只需按 `Ctrl+Shift+N` 或通过*Menu > New Tabs and Windows > New Private Window*新建私有窗口。所有后续打开的标签也是私有的。

## 辅助功能提示

### 禁用文本选择

在Opera中可以禁用文本选择。 但是，通过JavaScript的文本选择仍然可以工作（例如表单，等等）。可以通过以下方法设置：

```
opera:config#System|DisableTextSelect

```

### 抓取和滚动模式

除了关闭文本选择，抓取和滚动模式使鼠标拖动可以进行页面滚动。 这是非常有用的，特别是当你有一个触摸屏时。复制并粘贴下面的链接即可访问上述设置。

```
opera:config#UserPrefs|ScrollIsPan

```

还可以通过将适当的Opera按钮拖放到工具栏中来即时更改此设置。该按钮可以在 *Menu > Appearance > Buttons > Browser View* 中找到。

### 长按链接会在后台标签（扩展程序）中打开它

可以通过安装[这个](https://addons.opera.com/en/addons/extensions/details/open-in-background-with-long-press/)扩展程序在新的后台标签中打开任何长按的链接。

### 虚拟屏幕键盘 (扩展程序)

有一个允许使用虚拟屏幕键盘的扩展。可以在[这里](https://addons.opera.com/en/addons/extensions/details/virtual-keyboard/)找到更多详细信息和安装链接。

## Security

### Force a password store

Since current Opera uses the same engine as Chromium does, you can force Opera to use a specific password store by launching it with the `--password-store` flag. For more details see [Chromium/Tips and tricks#Force a password store](/index.php/Chromium/Tips_and_tricks#Force_a_password_store "Chromium/Tips and tricks").

## 故障排除

### NVIDIA 显卡上出现条纹

运行以下命令：

```
$ nvidia-settings -a InitialPixmapPlacement=2

```

在某些计算机上， 如果没有运行以上命令，[[1]](http://helion.pl) 运行会极其缓慢，使它成为一个完美的测试网站。

### 卧式鼠标滚轮滚动

Check *Settings > Preferences... > Advanced > Shortcuts > Mouse > Middle-Click Options... > Enable horizontal panning*.

或者

*   Highlight *Settings > Preferences... > Advanced > Shortcuts > Mouse > Opera Standard*.
*   Duplicate *Settings > Preferences... > Advanced > Shortcuts > Mouse > Opera Standard*.
*   Edit... *Settings > Preferences... > Advanced > Shortcuts > Mouse > Copy of Opera Standard*.
*   Search the `Forward` and `Back` input contexts and edit the appropriate button shortcuts to `scroll left` and `scroll right`.
*   Rename *Settings > Preferences... > Advanced > Shortcuts > Mouse > Copy of Opera Standard* as desired.

### 启动外部浏览器

如果Opera不能很好的显示网站，一个解决方案是在外部浏览器中打开当前显示的网页。

**提示：** 以下方法似乎已被弃用，取而代之的方法是通过鼠标右键访问内置 `Open With` 菜单。

*   在`$HOME/.opera/toolbar/standard_toolbar.ini`中，设置 `[Site Navigation Toolbar.content]` 的下一行为:

```
Button0, "Chromium"="Execute program, "chromium, "%u", , "Chromium""

```

*   如果需要 firefox，或者是首选：

```
Button0, "Firefox"="Execute program, "firefox", "%u", , "Firefox""

```

*   在字符串中可以包括任意数量的命令行选项:

```
Button0, "Chromium"="Execute program, "chromium --block-nonsandboxed-plugins --disable-java --incognito --safe-plugins --start-maximized --user-data-dir=/tmp/.chromium", "%u", , "Chromium""

```

### 使用 GTK + 2.24.7+ 开始或关闭时，Opera 崩溃的问题

如果发生此崩溃，您可以通过将 *DialogToolkit* 选项更改为4来解决此问题:

```
opera:config#FileSelector|DialogToolkit

```

这将禁用GTK +样式支持，从而避免该问题。

### 带有深色GTK +主题的不可读输入字段和地址栏

当使用黑色GTK主题时，可能遇到Opera地址栏和具有不可读输入和文本字段的页面（例如，Amazon可以在黑色文本字段背景上具有黑色文本）。这可能是因为网站仅设置背景或文本颜色其中之一，而Opera从主题中获取另一个。

使用安装的全新主题和命令来解决这个问题： `env GTK2_RC_FILES=/usr/share/themes/<light-theme-name/gtk-2.0/gtkrc opera`

要将其设为默认值，请使用首选的文本编辑器编辑文件 `/usr/bin/opera`. 例如， 使用 Opera 12.14:

```
sudo gedit /usr/bin/opera
...
#!/bin/sh
export OPERA_DIR=${OPERA_DIR:-/usr/share/opera}
export OPERA_PERSONALDIR=${OPERA_PERSONALDIR:-$HOME/.opera}
exec /usr/lib/opera/opera "$@"

```

编辑文件并按照示例更改为...

```
/usr/bin/opera
...
#!/bin/sh
export OPERA_DIR=${OPERA_DIR:-/usr/share/opera}
export OPERA_PERSONALDIR=${OPERA_PERSONALDIR:-$HOME/.opera}
env GTK2_RC_FILES=/usr/share/themes/Clearlooks/gtk-2.0/gtkrc /usr/lib/opera/opera "$@"

```

这将使浏览器使用您在上面“Clearlooks”文件 `/usr/bin/opera` 中设置的全新主题，如此问题将得以解决。

## 参见

*   [Opera Wiki](http://operawiki.info/Opera)
*   [Opera Knowledge Base](http://www.opera.com/support/kb/)
*   [Opera For UNIX Forums](http://my.opera.com/community/forums/forum.dml?id=3)
*   [Opera Bug Report](http://www.opera.com/support/bugs/)
*   [Opera Tips](http://www.opera.com/browser/tips/)
*   [Opera Documentation](http://www.opera.com/docs/)
*   [Opera Help](http://help.opera.com/Linux/12.10/en/)