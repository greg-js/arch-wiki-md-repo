# Opera (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Firefox](/index.php/Firefox "Firefox")
*   [Chromium](/index.php/Chromium "Chromium")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**本页面或部分需要翻译，部分内容可能已经与英文文章脱节。如果您希望贡献翻译，请访问[简体中文翻译组](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")。**

**附注:** please use the first argument of the template to provide more detailed indications.

[Opera](http://www.opera.com)浏览器，是一款自1994年以来由挪威 [Opera Software](https://en.wikipedia.org/wiki/Opera_Software "wikipedia:Opera Software")公司开发的免费浏览器软件。该浏览器因曾经最先引入诸如标签式浏览、内置搜索等功能而闻名。

Opera 浏览器仍在不断开发创新。它的特色功能包括集成的邮件客户端、一键保存书签、标签栈（一种特别的标签组织方式）以及对 [HTML5](https://en.wikipedia.org/wiki/HTML5 "wikipedia:HTML5") 的良好支持。

Opera 是跨平台浏览器，可以在 Windows, Mac 和 Linux 上运行。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 插件](#.E6.8F.92.E4.BB.B6)
    *   [2.1 Adobe Flash](#Adobe_Flash)
    *   [2.2 Java 支持](#Java_.E6.94.AF.E6.8C.81)
    *   [2.3 Adblock](#Adblock)
*   [3 性能调整](#.E6.80.A7.E8.83.BD.E8.B0.83.E6.95.B4)
    *   [3.1 禁用功能和服务](#.E7.A6.81.E7.94.A8.E5.8A.9F.E8.83.BD.E5.92.8C.E6.9C.8D.E5.8A.A1)
        *   [3.1.1 禁用电子邮件客户端](#.E7.A6.81.E7.94.A8.E7.94.B5.E5.AD.90.E9.82.AE.E4.BB.B6.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [3.1.2 禁用 ARGB, LIRC and mailto links](#.E7.A6.81.E7.94.A8_ARGB.2C_LIRC_and_mailto_links)
    *   [3.2 提高Flash性能](#.E6.8F.90.E9.AB.98Flash.E6.80.A7.E8.83.BD)
        *   [3.2.1 .xinitrc 例子](#.xinitrc_.E4.BE.8B.E5.AD.90)
        *   [3.2.2 命令行例子](#.E5.91.BD.E4.BB.A4.E8.A1.8C.E4.BE.8B.E5.AD.90)
    *   [3.3 Profile in tmpfs](#Profile_in_tmpfs)
*   [4 外观](#.E5.A4.96.E8.A7.82)
    *   [4.1 主题](#.E4.B8.BB.E9.A2.98)
    *   [4.2 标题栏](#.E6.A0.87.E9.A2.98.E6.A0.8F)
    *   [4.3 标签模式](#.E6.A0.87.E7.AD.BE.E6.A8.A1.E5.BC.8F)
    *   [4.4 字体](#.E5.AD.97.E4.BD.93)
*   [5 私有标签](#.E7.A7.81.E6.9C.89.E6.A0.87.E7.AD.BE)
*   [6 辅助提示](#.E8.BE.85.E5.8A.A9.E6.8F.90.E7.A4.BA)
    *   [6.1 禁用文本选择](#.E7.A6.81.E7.94.A8.E6.96.87.E6.9C.AC.E9.80.89.E6.8B.A9)
    *   [6.2 Grab and scroll mode](#Grab_and_scroll_mode)
    *   [6.3 Long pressing a link opens it in a background tab (extension)](#Long_pressing_a_link_opens_it_in_a_background_tab_.28extension.29)
    *   [6.4 虚拟屏幕键盘 (扩展)](#.E8.99.9A.E6.8B.9F.E5.B1.8F.E5.B9.95.E9.94.AE.E7.9B.98_.28.E6.89.A9.E5.B1.95.29)
*   [7 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [7.1 NVIDIA 显卡上出现条纹](#NVIDIA_.E6.98.BE.E5.8D.A1.E4.B8.8A.E5.87.BA.E7.8E.B0.E6.9D.A1.E7.BA.B9)
    *   [7.2 卧式鼠标滚轮滚动](#.E5.8D.A7.E5.BC.8F.E9.BC.A0.E6.A0.87.E6.BB.9A.E8.BD.AE.E6.BB.9A.E5.8A.A8)
    *   [7.3 启动外部浏览器](#.E5.90.AF.E5.8A.A8.E5.A4.96.E9.83.A8.E6.B5.8F.E8.A7.88.E5.99.A8)
    *   [7.4 Opera crashes when starting or closing with GTK+ 2.24.7+](#Opera_crashes_when_starting_or_closing_with_GTK.2B_2.24.7.2B)
    *   [7.5 Unreadable input fields and address bar with dark GTK+ themes](#Unreadable_input_fields_and_address_bar_with_dark_GTK.2B_themes)
*   [8 See Also](#See_Also)

## 安装

Opera 26 已经在 2014 年 12 月上旬发布；它仅仅提供了 64 位版本。作为一个里程碑，从此以后，旧的私有 Presto 排版引擎被更先进且开源的 Blink 引擎所替代。之前的 12.16 版本仍然支持 32 位系统。

Opera 可以在 [官方软件仓库安装](/index.php/Official_repositories "Official repositories")。官方仓库为 x86_64 架构的系统提供新的 Blink 版本 Opera，而为 i686 架构的系统提供旧的 Presto 版本的 Opera。

12.16 版 Opera 同样可以在 [AUR](/index.php/AUR "AUR")：[opera-legacy](https://aur.archlinux.org/packages/opera-legacy/)<sup><small>AUR</small></sup> 中找到，包含 x86_64 以及 i686 架构的支持。

## 插件

Opera可以使用大多数主流浏览器所支持的，基于Netscape的插件。 详见 [Browser plugins](/index.php/Browser_plugins "Browser plugins"). opera的插件选项见 _Settings > Preferences... > Advanced > Content > Plug-in Options_.

### Adobe Flash

请见: [Browser plugins#Flash Player](/index.php/Browser_plugins#Flash_Player "Browser plugins")

### Java 支持

请见 the main article: [Browser plugins#Java (IcedTea)](/index.php/Browser_plugins#Java_.28IcedTea.29 "Browser plugins")

### Adblock

可以安装 [AUR](/index.php/AUR "AUR") 中 [opera-adblock-complete](https://aur.archlinux.org/packages/opera-adblock-complete/)<sup><small>AUR</small></sup> 软件包以获得 Adblock 支持。

## 性能调整

尽管 Opera 在现代的机器上运行速度已经相当不错，其实它仍有性能调优的空间。请阅读 [Opera Wiki page](http://operawiki.info/operaperformance) 以了解详情。

### 禁用功能和服务

其中最大限度地提高应用的性能的关键是禁用不需要的功能和服务通过本地[opera:config Preferences Editor.](http://www.opera.com/browser/tutorials/personalize/behavior/)

一些不需要的功能：

*   **Systray Icon**: uncheck _Show Tray Icon_ under opera:config#UserPrefs.
*   **BitTorrent**: uncheck _Enable_ under opera:config#BitTorrent.
*   **Geolocation**: uncheck _Enable geolocation_ under opera:config#Geolocation.
*   **Multimedia**: unckeck desired options under opera:config#Multimedia.
*   **Web Server**: uncheck _Enable_ under opera:config#Web Server.

为了更简单的找到它，我们把这些选项的相应（没有空格）路径写在地址栏中。 例如 `opera:config#UserPrefs|ShowTrayIcon`或者使用内置搜索。

#### 禁用电子邮件客户端

其他命令行选项可用于进一步控制浏览器的功能和服务。不使用默认的内部电子邮件客户端启动Opera：

```
$ opera -nomail

```

另外，如果你想永久禁止内部电子邮件客户端，你可以取消选中opera:config#UserPrefs下的' '显示电子邮件客户端_选项。_

#### 禁用 ARGB, LIRC and mailto links

没有[ARGB](https://en.wikipedia.org/wiki/ARGB "wikipedia:ARGB") (32-bit)的视觉效果开启Opera。 [LIRC](http://www.lirc.org/) infrared control support and with `mailto:` 禁用链接：

```
$ opera -noargb -nolirc -nomaillinks

```

### 提高Flash性能

为了提高Flash的性能，在启动Opera之前你要设置以下环境变量，在[xinitrc](/index.php/Xinitrc "Xinitrc"), 或者 [~/.bash_profile](/index.php/Bash "Bash")中export条目，或者全系统改变`/etc/profile`：

```
 OPERAPLUGINWRAPPER_PRIORITY=0
 OPERA_KEEP_BLOCKED_PLUGIN=1

```

另外一个能帮你解决Flash问题的环境变量：

```
GDK_NATIVE_WINDOWS=1

```

看博客[Linux上的Flash问题?](http://my.opera.com/ruario/blog/flash-problems-on-linux)去添加细节。

#### .xinitrc 例子

 `~/.xinitrc` 

```
...
export OPERAPLUGINWRAPPER_PRIORITY=0
export OPERA_KEEP_BLOCKED_PLUGIN=0
...

```

#### 命令行例子

使用命令行变量作为Opera：

```
$ OPERAPLUGINWRAPPER_PRIORITY=0 OPERA_KEEP_BLOCKED_PLUGIN=1 opera &

```

### Profile in tmpfs

Relocate the browser profile to a [tmpfs](/index.php/Fstab#tmpfs "Fstab") filesystem, including `/tmp` for improvements in application response as the entire profile is now stored in RAM. Another benefit is a reduction in disk read and write operations, of which SSDs benefit the most.

There are currently two ways of doing this:

*   using [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon"), that automatically detects and relocates the Opera profile to tmpfs.
*   using the `-pd` command-line flag to tell Opera where to store its profile data:

```
$ opera -pd /tmp/opera

```

## 外观

### 主题

虽然Opera是跨平台的，但是它可以在不同版本的 Linux 桌面环境中工作得很好。

Qt

安装并通过应用`qtconfig`来使用你的 Qt，这样可以使你的菜单更加丰富。

KDE

你能够安装一个像[这样](http://my.opera.com/community/customize/skins/info/?id=8141)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2014-04-05]</sup>的主题使你的 Opera 使用KDE的图标。

GTK+

一个很棒的使用 Tango 图标的主题[clicked here](http://my.opera.com/community/customize/skins/info/?id=3465)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2014-04-05]</sup>.

### 标题栏

在标签栏点击鼠标右键取消选中“显示边框”可以隐藏标题栏。

### 标签模式

Opera原生支持标签级联和平铺模式上。可以通过激活“主”工具栏或通过拖放所需的任何位置上的按钮可以找到适当的按钮 _Menu > Appearance > Buttons > Browser_.

### 字体

可以在 _Settings > Preferences... > Advanced > Fonts_下配置字体.

如果在第一次运行Opera之前已经安装[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup>软件包。不管是由本地 GTK+ 选项[GNOME](/index.php/GNOME "GNOME")还是 KDE 字体管理器指定，Opera都将使用默认字体配置。要强制已经安装的Opera使用系统设置选项：

*   Close all running instances of Opera.
*   Un-install the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup> package.
*   Move the existing profile folder: `mv -i ~/.opera ~/.opera.bak`
*   Run an instance of Opera and verify that your font manager settings have been applied.
*   Restore bookmarks and desired filter files from `~/.opera.bak` to `~/.opera` except for the `operaprefs.ini` file.
*   Re-install the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup> package, if desired.

**Note:** If no text except numbers is showing on some of the webpages that might be a problem with the fonts. A known issue that causes this problem is the _helvetica_ pfb postscript fonts.

## 私有标签

如果你要浏览你访问过却没有留下明显痕迹的网站节点，你可以使用私有标签。当你关闭私有标签的时候，下面相关的数据将被删除：

*   Cache
*   Cookies
*   History
*   Logins

在 [--incognito option](http://www.google.com/support/chrome/bin/answer.py?hl=en&answer=95464) Chrome/[Chromium](/index.php/Chromium "Chromium")和 [PrivateBrowsing](https://wiki.mozilla.org/PrivateBrowsing) [Firefox](/index.php/Firefox "Firefox")这是很相似的.

使用命令行去打开一个私有标签：

```
$ opera -newprivatetab

```

为了确保整个会话持续时间只有私有标签使用：

*   Set _Settings > Preferences... > General > Startup > Start without open tabs_.
*   Clear any entries in _Settings > Preferences... > General > Home page option_.
*   Enable _Settings > Preferences... > Advanced > Tabs > Additional tab options... > Allow windows with no tabs_.

当你已经Opera的时候，你想打开一个私有标签，你能按 `Ctrl+Shift+N` 或者查看 _Menu > New Tabs and Windows > New Private Window_. 随后打开的所有标签也是私有的。

## 辅助提示

### 禁用文本选择

在Opera上可以禁用文本选择。然而，JavaScript的文本选择将一直工作(例如 in forms, etc.). 通过以下方法设置：

```
opera:config#System|DisableTextSelect

```

### Grab and scroll mode

Besides setting text selection off, grab and scroll mode makes page scrolling possible with mouse dragging. It is very useful, especially when you have a touchscreen. Copy and paste the link bellow to get to the mentioned setting.

```
opera:config#UserPrefs|ScrollIsPan

```

It is also possible to change this setting on the fly by dragging and dropping the appropriate Opera button into a toolbar. The button can be found in _Menu > Appearance > Buttons > Browser View_.

### Long pressing a link opens it in a background tab (extension)

It is possible to open up any long-clicked link in a new background tab by installing [this](https://addons.opera.com/en/addons/extensions/details/open-in-background-with-long-press/) extension.

### 虚拟屏幕键盘 (扩展)

有一个允许使用虚拟屏幕键盘的扩展。可以在 [here](https://addons.opera.com/en/addons/extensions/details/virtual-keyboard/)上找到更进一步的细节和安装链接。

## 故障排除

### NVIDIA 显卡上出现条纹

运行下面的命令：

```
$ nvidia-settings -a InitialPixmapPlacement=2

```

在某些计算机上， [http://helion.pl](http://helion.pl) 运行及其缓慢，使它成为一个完美的测试节点。

### 卧式鼠标滚轮滚动

Check _Settings > Preferences... > Advanced > Shortcuts > Mouse > Middle-Click Options... > Enable horizontal panning_.

or

*   Highlight _Settings > Preferences... > Advanced > Shortcuts > Mouse > Opera Standard_.
*   Duplicate _Settings > Preferences... > Advanced > Shortcuts > Mouse > Opera Standard_.
*   Edit... _Settings > Preferences... > Advanced > Shortcuts > Mouse > Copy of Opera Standard_.
*   Search the `Forward` and `Back` input contexts and edit the appropriate button shortcuts to `scroll left` and `scroll right`.
*   Rename _Settings > Preferences... > Advanced > Shortcuts > Mouse > Copy of Opera Standard_ as desired.

### 启动外部浏览器

如果Opera不能很好的显示网站，一个解决方案是在外部浏览器中显示当前显示的网页。

**Note:** The following method appears to be deprecated in favor of the built-in `Open With` menu accessed via the right mouse button.

*   在`$HOME/.opera/toolbar/standard_toolbar.ini`中设置下面的行`[Site Navigation Toolbar.content]`:

```
Button0, "Chromium"="Execute program, "chromium, "%u", , "Chromium""

```

*   如果需要 firefox，或者是首选：

```
Button0, "Firefox"="Execute program, "firefox", "%u", , "Firefox""

```

*   任意数量的命令行选项可以被包括在字符串中:

```
Button0, "Chromium"="Execute program, "chromium --block-nonsandboxed-plugins --disable-java --incognito --safe-plugins --start-maximized --user-data-dir=/tmp/.chromium", "%u", , "Chromium""

```

### Opera crashes when starting or closing with GTK+ 2.24.7+

If this crash occurs, you can work around it by changing the _DialogToolkit_ option to 4:

```
opera:config#FileSelector|DialogToolkit

```

This will disable GTK+ styling support and hence avoid the issue.

### Unreadable input fields and address bar with dark GTK+ themes

When using a dark GTK theme, one might encounter Opera address bar and Internet pages with unreadable input and text fields (e.g. Amazon can have black text on black text field background). This can happen because the site only sets either background or text color, and Opera takes the other one from the theme.

Using an installed clear theme and a command help to work around the problem: `env GTK2_RC_FILES=/usr/share/themes/<light-theme-name/gtk-2.0/gtkrc opera`

to turn it as default, use a prefered text editor and edit the file `/usr/bin/opera`. e.g. using Opera 12.14:

```
sudo gedit /usr/bin/opera
...
#!/bin/sh
export OPERA_DIR=${OPERA_DIR:-/usr/share/opera}
export OPERA_PERSONALDIR=${OPERA_PERSONALDIR:-$HOME/.opera}
exec /usr/lib/opera/opera "$@"

```

edit the file and follow the example changing to...

```
/usr/bin/opera
...
#!/bin/sh
export OPERA_DIR=${OPERA_DIR:-/usr/share/opera}
export OPERA_PERSONALDIR=${OPERA_PERSONALDIR:-$HOME/.opera}
env GTK2_RC_FILES=/usr/share/themes/Clearlooks/gtk-2.0/gtkrc /usr/lib/opera/opera "$@"

```

this will make the browser use a clear theme that you set in the file `/usr/bin/opera` that was used in the above example the theme "Clearlooks" and the problems will be solved.

## See Also

*   [Opera Wiki](http://operawiki.info/Opera)
*   [Opera Knowledge Base](http://www.opera.com/support/kb/)
*   [Opera For UNIX Forums](http://my.opera.com/community/forums/forum.dml?id=3)
*   [Opera Bug Report](http://www.opera.com/support/bugs/)
*   [Opera Tips](http://www.opera.com/browser/tips/)
*   [Opera Documentation](http://www.opera.com/docs/)
*   [Opera Help](http://help.opera.com/Linux/12.10/en/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Opera_(简体中文)&oldid=415172](https://wiki.archlinux.org/index.php?title=Opera_(简体中文)&oldid=415172)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web browser (简体中文)](/index.php/Category:Web_browser_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Web browser (简体中文)")