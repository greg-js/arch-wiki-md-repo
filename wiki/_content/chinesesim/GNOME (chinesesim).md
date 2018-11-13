相关文章

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [GTK+](/index.php/GTK%2B "GTK+")
*   [GDM](/index.php/GDM "GDM")
*   [GNOME/Tips and tricks (简体中文)](/index.php/GNOME/Tips_and_tricks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME/Tips and tricks (简体中文)")
*   [GNOME/Troubleshooting (简体中文)](/index.php/GNOME/Troubleshooting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME/Troubleshooting (简体中文)")
*   [GNOME/Files](/index.php/GNOME/Files "GNOME/Files")
*   [GNOME/Gedit](/index.php/GNOME/Gedit "GNOME/Gedit")
*   [GNOME/Web](/index.php/GNOME/Web "GNOME/Web")
*   [GNOME/Evolution](/index.php/GNOME/Evolution "GNOME/Evolution")
*   [GNOME/Flashback](/index.php/GNOME/Flashback "GNOME/Flashback")
*   [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring")
*   [Cinnamon](/index.php/Cinnamon "Cinnamon")
*   [MATE](/index.php/MATE "MATE")
*   [Official repositories#gnome-unstable](/index.php/Official_repositories#gnome-unstable "Official repositories")

**翻译状态：** 本文是英文页面 [GNOME](/index.php/GNOME "GNOME") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-06-19，点击[这里](https://wiki.archlinux.org/index.php?title=GNOME&diff=0&oldid=526892)可以查看翻译后英文页面的改动。

[GNOME](https://www.gnome.org/)（读音是 *gah-nohm* 或 *nohm*）是一个简单易用的[桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")。它是由 [GNOME 项目](https://en.wikipedia.org/wiki/zh:GNOME%E8%A8%88%E5%8A%83 而不是 [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)") 进行显示。

## Contents

*   [1 安装](#安装)
*   [2 GNOME 会话](#GNOME_会话)
*   [3 运行 GNOME](#运行_GNOME)
    *   [3.1 图形界面启动](#图形界面启动)
    *   [3.2 手动启动](#手动启动)
        *   [3.2.1 Xorg 会话](#Xorg_会话)
        *   [3.2.2 Wayland 会话](#Wayland_会话)
    *   [3.3 Wayland 中的 GNOME 应用程序](#Wayland_中的_GNOME_应用程序)
*   [4 浏览](#浏览)
*   [5 遗留名称](#遗留名称)
*   [6 配置](#配置)
    *   [6.1 GNOME 系统设置](#GNOME_系统设置)
        *   [6.1.1 色彩](#色彩)
        *   [6.1.2 夜间模式](#夜间模式)
        *   [6.1.3 日期与时间](#日期与时间)
        *   [6.1.4 默认应用程序](#默认应用程序)
        *   [6.1.5 鼠标和触摸板](#鼠标和触摸板)
        *   [6.1.6 网络](#网络)
        *   [6.1.7 在线帐户](#在线帐户)
        *   [6.1.8 搜索](#搜索)
    *   [6.2 高级设置](#高级设置)
        *   [6.2.1 外观](#外观)
            *   [6.2.1.1 GTK+主题和图标主题](#GTK+主题和图标主题)
                *   [6.2.1.1.1 全局暗色主题](#全局暗色主题)
            *   [6.2.1.2 窗口管理器主题](#窗口管理器主题)
                *   [6.2.1.2.1 标题栏的高度](#标题栏的高度)
                *   [6.2.1.2.2 标题栏按钮重新排序](#标题栏按钮重新排序)
                *   [6.2.1.2.3 最大化时隐藏标题栏](#最大化时隐藏标题栏)
            *   [6.2.1.3 GNOME Shell主题](#GNOME_Shell主题)
            *   [6.2.1.4 菜单图标](#菜单图标)
        *   [6.2.2 桌面](#桌面)
            *   [6.2.2.1 桌面图标](#桌面图标)
            *   [6.2.2.2 锁屏和背景](#锁屏和背景)
        *   [6.2.3 扩展](#扩展)
        *   [6.2.4 输入法](#输入法)
        *   [6.2.5 字体](#字体)
        *   [6.2.6 自启动应用程序](#自启动应用程序)
        *   [6.2.7 电源](#电源)
            *   [6.2.7.1 配置合上盖子时的行为](#配置合上盖子时的行为)
            *   [6.2.7.2 修改电池电量严重不足时的行为](#修改电池电量严重不足时的行为)
        *   [6.2.8 通过应用文件夹整理应用](#通过应用文件夹整理应用)
*   [7 参见](#参见)

## 安装

有两个软件组可用：

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) 包含基本的桌面环境和一些集成良好的[应用程序](https://wiki.gnome.org/Apps)；

*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) 包含其他 GNOME 应用，包括压缩文件管理器、[文本编辑器](/index.php/Gedit "Gedit")和一些游戏。请注意，这个组建立在 [gnome](https://www.archlinux.org/groups/x86_64/gnome/) 组之上。

基础桌面环境由 [GNOME Shell](https://en.wikipedia.org/wiki/zh:GNOME_Shell 窗口管理器的插件——组成。它可以通过 [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) 单独安装。

**注意:** *mutter* 充当桌面的混成管理器。它利用硬件图形加速来提供减少屏幕杂乱的效果。GNOME 会话管理器会自动检测显卡驱动是否能够运行 GNOME Shell，如果不行则用 *llvmpipe* 软件渲染。

## GNOME 会话

GNOME 有三个可用的会话，都使用 GNOME Shell。

*   **GNOME** 是使用 Wayland 的默认会话，传统 X 应用将通过 Xwayland 运行。
*   **GNOME Classic** 的桌面布局类似于传统的 GNOME 2, 使用预先激活的插件和参数。[[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) 因此，它更像是一个定制的 GNOME Shell，而不是一个完全独立的模式。
*   **GNOME on Xorg** 使用 Xorg 运行 GNOME Shell。

## 运行 GNOME

GNOME 可以通过[显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")以图形方式启动，也可以从控制台手动启动。

**注意:** GNOME 的锁屏功能由 GDM 提供支持。如果没有使用 GDM 启动 GNOME，则需要使用另一个屏幕锁定器来提供此功能。详见[List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security")。

### 图形界面启动

从显示管理器会话菜单中选择 *GNOME*, *GNOME Classic* 或 *GNOME on Xorg* 。

### 手动启动

#### Xorg 会话

*   对于 GNOME on Xorg 会话，在 `~/.xinitrc` 中添加：`exec gnome-session`。
*   对于 GNOME Classic 会话，在 `~/.xinitrc` 中添加：
    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

修改完 `~/.xinitrc` 后，即可使用 `startx` 启动 GNOME（有关其他详细信息，例如如何保留 logind 会话，详见 [xinitrc](/index.php/Xinit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinit (简体中文)")）。设置完 `~/.xinitrc` 后，也可以设定[在登录时自动启动X](/index.php/Xinit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#在启动时自动启用_X "Xinit (简体中文)")。

#### Wayland 会话

**注意:**

*   [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) 软件包提供的 X 服务器仍然需要用于运行尚未移植到 [Wayland](/index.php/Wayland_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wayland (简体中文)") 的应用程序。
*   使用专有 NVIDIA 驱动的 Wayland 会话目前的性能非常差：[FS#53284](https://bugs.archlinux.org/task/53284)。

可以使用 `XDG_SESSION_TYPE=wayland dbus-run-session gnome-session` 手动启动 Wayland 会话。

若要在 tty1 登录时启动，将以下内容添加到 `.bash_profile` 中：

```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]] && [[ -z $XDG_SESSION_TYPE ]]; then
  XDG_SESSION_TYPE=wayland exec dbus-run-session gnome-session
fi

```

### Wayland 中的 GNOME 应用程序

在使用 *GNOME* 会话时，GNOME 应用程序将使用 Wayland 运行。[GNOME Applications under Wayland](https://wiki.gnome.org/Initiatives/Wayland/Applications/) 中列出了 GNOME 应用程序在 Wayland 下的当前状态。若要调试，[GTK+ 手册](https://developer.gnome.org/gtk3/stable/gtk-running.html) 列出了选项和环境变量。

## 浏览

[GNOME Shell cheat sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet) 中解释了如何高效地使用 GNOME shell，它展示了 GNOME shell 的特色和快捷键，包括切换任务，使用键盘，窗口控制，面板，概览模式等等。以下是部分常用的快捷键：

*   `Super` + `m`：显示消息托盘
*   `Super` + `a`：显示应用程序菜单
*   `Alt-` + `Tab`：切换当前使用的应用
*   `Alt-` + ``` (美式键盘 `Tab` 上面的按键)：切换前台应用程序的窗口
*   `Alt` + `F2`，然后输入 `r` 或 `restart`：在图形界面出问题时重启界面（仅用于 X/传统 模式，不适用于 Wayland 模式）。

## 遗留名称

**注意:** 一些 GNOME 程序在文档和对话框中的名称已经更改，但执行文件名称却没有。下面表格列出了一些这样的应用程序。

**提示：** 在搜索栏中搜索应用的遗留名称将成功找到对应的应用，例如搜索 *nautilus* 将返还 *文件*。

| 当前 | 遗留 |
| [文件](/index.php/Files "Files") | Nautilus |
| [Web](/index.php/GNOME/Web "GNOME/Web") | Epiphany |
| 视频 | Totem |
| 主菜单 | Alacarte |
| 文档查看器 | Evince |
| 磁盘使用情况分析器 | Baobab |
| 图像查看器 | EoG (Eye of GNOME) |
| [密码和密钥](/index.php/GNOME/Keyring "GNOME/Keyring") | Seahorse |

## 配置

GNOME 系统设置面板（gnome-control-center）和 GNOME 应用使用 [dconf](https://en.wikipedia.org/wiki/Dconf "wikipedia:Dconf") 配置系统存储设置。

您可以使用 `gsettings` 或 `dconf` 命令行工具直接访问 dconf 数据库。这也可以让你修改用户界面不公开的设置。

直到 GNOME 3.24，设置由 GNOME 设置进程应用，其也可以在 GNOME 会话之外通过以下命令运行：

```
 $ nohup /usr/lib/gnome-settings-daemon/gnome-settings-daemon > /dev/null &

```

然而 GNOME 3.24 通过几个相互独立的设置插件 `/usr/lib/gnome-settings-daemon/gsd-*` 取代了 GNOME 设置进程。这些插件通过 `/etc/xdg/autostart` (org.gnome.SettingsDaemon.*.desktop) 下的桌面文件进行控制。如果需要在 GNOME 会话之外运行这些插件，您需要复制或编辑相应的[桌面条目](/index.php/Desktop_entries_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop entries (简体中文)")到 `~/.config/autostart`。

配置通常是用户特定的，本文将不介绍如何为多个用户创建配置模板。

### GNOME 系统设置

#### 色彩

`colord` 守护进程会读取显示器的 EDID 信息并提取出合适的色彩配置内容。大多数情况下，色彩配置都是正确的，不需要额外设置；但是对于某些偏差情况或使用较旧的显示器时，可以把色彩配置文件放在 `~/.local/share/icc/` 下并被指向。

#### 夜间模式

GNOME 内置了类似于 [Redshift](/index.php/Redshift "Redshift") 的蓝光过滤功能。夜间模式可以在设置面板中启动及自定义启动时间。此外，夜间模式的开尔文温度可以使用以下 dconf 设置进行调整，5000 是一个示例值：

```
$ gsettings set org.gnome.settings-daemon.plugins.color night-light-temperature 5000

```

#### 日期与时间

如果系统已有配置好的 [网络时间协议 守护进程](/index.php/Network_Time_Protocol_daemon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network Time Protocol daemon (简体中文)")，它同样会对 GNOME 起作用。如果需要，同步设置可以在菜单内设为手动控制。

如果需要在顶栏内显示日期，请运行：

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

另外，如果需要在顶栏的日历中显示周数，请运行：

```
$ gsettings set org.gnome.shell.calendar show-weekdate true

```

#### 默认应用程序

首次安装 GNOME 时，您可能会发现某些协议由错误的应用程序处理。比如说，视频被 *totem* 打开而不是以前使用的 [VLC](/index.php/VLC "VLC")。某些关联可以通过系统设置进行设置：*详细信息* > *默认应用程序*。

有关其他协议和方法，请参阅[默认应用程序](/index.php/Default_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Default applications (简体中文)")进行配置。

#### 鼠标和触摸板

大多数触摸板设置可以通过系统设置进行设置：*设备* > *鼠标和触摸板*。

根据您的设备，其他配置可能可用，但不会显示在默认界面内，例如不同的触摸板点击方法：

 `$ gsettings range org.gnome.desktop.peripherals.touchpad click-method` 
```
enum
'default'
'none'
'areas'
'fingers'
```

手动设置:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad click-method 'fingers'

```

或通过 [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks)。

**Note:** GNOME 不支持 [synaptics](/index.php/Synaptics "Synaptics") 并默认使用 [libinput](/index.php/Libinput "Libinput")。参考 [这个缺陷报告](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12)。

#### 网络

[NetworkManager](/index.php/NetworkManager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NetworkManager (简体中文)") 是 GNOME 项目下用于控制网络设置的工具。 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) 软件包并[启用](/index.php/%E5%90%AF%E7%94%A8 "启用") `NetworkManager.service` 单元。

虽然可以使用任何其他[网络管理器](/index.php/Network_manager "Network manager")，但 NetworkManager 可以通过网络设置和状态指示器 [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)（ GNOME不需要 ）整合到桌面环境当中。

#### 在线帐户

GNOME聊天程序[empathy](https://www.archlinux.org/packages/?name=empathy)的后端以及GNOME系统设置面板中的在线账户部分由另一个软件包组[telepathy提供](https://www.archlinux.org/groups/x86_64/telepathy%E6%8F%90%E4%BE%9B/)。相关请看[Unable to add accounts in Empathy and GNOME Online Accounts](/index.php/GNOME/Troubleshooting#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts "GNOME/Troubleshooting")部分提供的帮助。部分在线账户，比如[ownCloud](/index.php/OwnCloud "OwnCloud")，需要安装[gvfs-gos](https://www.archlinux.org/packages/?name=gvfs-gos)以在GNOME应用比如[GNOME Files](/index.php/GNOME_Files "GNOME Files")以及GNOME文档中发挥全部功能。相关链接：[[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### 搜索

GNOME shell在按下`Super`键并开始输入时会启动搜索。[tracker](https://www.archlinux.org/packages/?name=tracker)软件包默认作为[gnome](https://www.archlinux.org/groups/x86_64/gnome/)组的一部分被安装。它提供一个应用和数据的索引数据库。它可以被“搜索及索引”菜单项配置，通过"tracker-control"监视状态。它在用户登录时自动被"gnome-session"启动。索引可以被`tracker-control -s`手动启动。搜索设置也可以在“系统设置面板”配置。

Tracker数据库可以通过"tracker-sparql“命令查询。更多信息请访问它的手册页[tracker-sparql(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tracker-sparql.1)

### 高级设置

#### 外观

##### GTK+主题和图标主题

除了以下所述的直接从底层修改主题的方法，您也可以使用 gnome-tweak-tool 工具进行修改。 安装一个新的主题和图标集，分别添加相关的`~/.local/share/themes` 或者 `~/.local/share/icons` respectively (add to `/usr/share/` instead of `~/.local/share/` for the themes to be available systemwide.) 他们和其他GUI设置也可以在 `~/.config/gtk-3.0/settings.ini`中定义:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-theme-name = Adwaita
# next option is applicable only if selected theme supports it
gtk-application-prefer-dark-theme = true
# set font name and dimension
gtk-font-name = Sans 10

```

其他主题的站点:

*   [DeviantArt](http://www.deviantart.com/browse/all/customization/skins/linuxutil/desktopenv/gnome/gtk3/).
*   [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=167).
*   [GTK3 themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gtk3&do_Search=Go).
*   [Cursor themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=xcursor&do_Search=Go&PP=50&SB=v&SO=d).
*   [Icon themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=icon-theme&do_Search=Go&PP=50&SB=v&SO=d).

一旦安装，就可以使用 GNOME Tweak Tool或GSettings -参阅下面的GSettings命令：

对于GTK+主题：

```
$ gsettings set org.gnome.desktop.interface gtk-theme *theme-name*

```

对于图标主题

```
$ gsettings set org.gnome.desktop.interface icon-theme *theme-name*

```

###### 全局暗色主题

GNOME默认使用Adwaita light主题，不过暗色主题(称之为全局黑色主题)也存在并可通过the Tweaks或者是编辑GTK+ 3设置文件 - 详细访问 [GTK+#Dark theme variant](/index.php/GTK%2B#Dark_theme_variant "GTK+")。一些应用比如图像查看器（“eog”）默认使用暗色主题。值得注意的是，全局黑色主题只对GTK+ 3应用有效；部分GTK+ 3应用也许只有对全局主题的部分支持。未来也许将添加对全局暗色主题对Qt及GTK+ 2的支持。

##### 窗口管理器主题

窗口管理器的主题跟随GTK+ 主题。不赞成使用`org.gnome.desktop.wm.preferences theme`设置主题，并且这样也会被GNOME忽视。

###### 标题栏的高度

**Note:** 下面配置会修改 GNOME 终端和 Chromium 的标题栏高度，但是不会影响 Nautilus。
 `~/.config/gtk-3.0/gtk.css` 
```
headerbar.default-decoration {
 padding-top: 0px;
 padding-bottom: 0px;
 min-height: 0px;
 font-size: 0.6em;
}

headerbar.default-decoration button.titlebutton {
 padding: 0px;
 min-height: 0px;
}

```

更多信息请阅读 [[3]](https://ask.fedoraproject.org/en/question/10035/shrink-title-bar/?answer=86149#post-id-86149).

###### 标题栏按钮重新排序

设置 GNOME 窗口管理器顺序 (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**提示：** 冒号表示窗口标题栏的按钮会出现在哪一方

###### 最大化时隐藏标题栏

*   [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [gnome-shell-extension-pixel-saver-git](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver-git/)或[gnome-shell-extension-pixel-saver](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver/)。最大化的窗口的标题栏将与活动栏整合以节省空间。

*   [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/)。它改变窗口管理器的默认设置以在应用最大化或平铺至一边时自动在传统（无顶栏）的应用中隐藏标题栏。

*   [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [maximus](https://aur.archlinux.org/packages/maximus/)。启动该应用，在终端中输入"maximus"。运行时，守护进程将自动最大化窗口。它将关闭最大化窗口的装饰并在其取消最大化时重启装饰。如果您不想要所有窗口启动时最大化，那么运行`maximus - m`。注意，该应用只对窗口管理器装饰的应用有效； 使用自己装饰的应用比如[GNOME Files](/index.php/GNOME_Files "GNOME Files")最大化时不会被关闭装饰。

##### GNOME Shell主题

GNOME Shell本身的主题是可配置的。首先确认您已安装[gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions)软件包以应用Shell主题。然后通过GNOME Tweaks或通过[GNOME Shell Extensions](https://extensions.gnome.org) 网站启用“User Themes”扩展。Shel主题可以通过使用GNOME Tweaks软件加载并选用。

[AUR中](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d)中有大量可用的GNOME Shell主题。

Shell主题也可在[gnome-look.org](http://gnome-look.org/)下载。

##### 菜单图标

默认的GNOME设置不在菜单上显示图标。要在菜单上显示图标，运行以下命令：

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

#### 桌面

各种桌面设置可以应用。

##### 桌面图标

GNOME 3.28之前，桌面图标通过[Files](/index.php/Files "Files")在桌面上绘制一个透明的带图标的窗口实现。在GNOME 3.28中，该功能被移除，桌面图标不再在GNOME上可用。可能的方案包括使用[Nemo](/index.php/Nemo "Nemo")（GNOME File的一个分支，目前仍支持桌面图标）或安装[gnome-shell-extension-desktop-icons](https://aur.archlinux.org/packages/gnome-shell-extension-desktop-icons/)插件以部分复刻GNOME 3.26以下支持的桌面图标功能。更多信息请访问[Arch forum thread](https://bbs.archlinux.org/viewtopic.php?id=235633)。

##### 锁屏和背景

在设置桌面及锁屏背景的时候，注意Picture标签下只显示`~/Pictures`文件夹下的图片。如果您想使用不在该文件夹下的图片，请使用下列命令：

对于桌面背景：

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///path/to/my/picture.jpg'

```

对于锁屏背景

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///path/to/my/picture.jpg'

```

#### 扩展

**注意:** GNOME Shell browser 插件可以让用户从[extensions.gnome.org](https://extensions.gnome.org)安装扩展，支持 [Firefox (简体中文)](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)") 和 [GNOME/Web](/index.php/GNOME/Web "GNOME/Web")，要在 Google Chrome/Chromium, Opera 和 Vivaldi 中使用，需要安装 [chrome-gnome-shell-git](https://aur.archlinux.org/packages/chrome-gnome-shell-git/).

GNOME Shell 可以使用第三方扩展来定制。这些扩展提供了一些额外的功能，如：提供一个可以一直显示的 Dock、更换 Shell 的主题，等等。

名为 [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) 的软件包提供了一组由 The GNOME Project 维护，被当做 GNOME 计划的一部分的扩展，其中许多扩展被用在了 GNOME Classic 会话环境中。（最新版本的扩展你可以用他的代码 snapshot）[列表在这里](https://www.archlinux.org/packages/?sort=&q=gnome-shell-extension&maintainer=&last_update=&flagged=&limit=50)

```
 $ pacman -Ss gnome-shell-extension

```

另外，有许多扩展被收集并托管在了[extensions.gnome.org](https://extensions.gnome.org) 上。你可以在浏览器中浏览扩展列表，并轻松地一键点击来安装、管理、启用扩展。你可以在 [这里](https://extensions.gnome.org/about/)找到有关插件的更多信息。

你也可以在 [AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-extension&do_Search=Go)里面找到一些有用的扩展。当然，它们大多也可以在 [extensions.gnome.org](https://extensions.gnome.org) 找到。一些值得一提的是：

*   [gnome-shell-extension-lockkeys-git](https://aur.archlinux.org/packages/gnome-shell-extension-lockkeys-git/) 一个指示 NumLock/CapsLock 激活情况的扩展。
*   [gnome-shell-extension-weather-git](https://aur.archlinux.org/packages/gnome-shell-extension-weather-git/) 一个可以显示天气通知的扩展。
*   [gnome-shell-extension-nohotcorner-git](https://aur.archlinux.org/packages/gnome-shell-extension-nohotcorner-git/) 一个禁用“Hot Corner”功能的拓展。
*   [gnome-shell-extension-insensitive-message-tray-git](https://aur.archlinux.org/packages/gnome-shell-extension-insensitive-message-tray-git/) 使鼠标在屏幕底部激活信息托盘的行为变迟钝的拓展。
*   [Alternative Status Menu](https://extensions.gnome.org/extension/5/alternative-status-menu/) 让你的用户菜单里显示休眠和关机的扩展。

另外，想要在屏幕底部显示一个任务栏，但又不想使用 GNOME Classic 的用户可以考虑使用 Window list 扩展 (由 [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) 提供).

在安装完一个扩展之后可能需要[重启 GNOME shell](#重启_GNOME_shell)  。故障排除信息参照[安装扩展导致GNOME停止工作](#安装扩展导致GNOME停止工作)。

#### 输入法

GNOME集成了的通过[IBus](/index.php/IBus "IBus")的输入法, 只有[ibus](https://www.archlinux.org/packages/?name=ibus)和添加想要的输入法引擎 (例如:[ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) for Intelligent Pinyin) 需要安装，安装后，输入法引擎可以加入GNOME的区域和语言设置键盘布局。

#### 字体

**提示：** 如果您把"Scaling factor"调至1.00以上的某值，辅助功能菜单将自动启用

GNOME可以设置窗体标题，界面（应用），文档及等宽字体。查看Tweaks下的字体选项卡以获得相关选项。

对于字体渲染来说，RGBA可能适合更多的显示器类型，如果字体看起来过分拥挤，可以将字体渲染调至“Slight”或“None”。

#### 自启动应用程序

要登录自启某些应用程序, copy the relevant `.desktop` file from `/usr/share/applications/` to `~/.config/autostart/`. [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) 支持管理 autostart-entries。

**提示：** 如果Tweaks中自启动应用选项下加号按钮为灰色不可用，尝试在终端下通过 `gnome-tweak-tool`命令启动Tweaks。详情访问 [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**注意:** "gnome-session-properties"对话框可以通过[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/) 添加

#### 电源

你可能希望修改基本的电源管理设置（以下的设置以笔记本电脑用户为例，请按需调整）：

```
$ gsettings set org.gnome.settings-daemon.plugins.power button-power *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout *3600*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout *1800*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type *hibernate*
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen *true*

```

如需在合上盖子后依然保持显示器开启：

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

GNOME 3.24中不建议使用以下设置：

```
org.gnome.settings-daemon.plugins.power button-hibernate
org.gnome.settings-daemon.plugins.power button-power
org.gnome.settings-daemon.plugins.power button-sleep
org.gnome.settings-daemon.plugins.power button-suspend
org.gnome.settings-daemon.plugins.power critical-battery-action

```

##### 配置合上盖子时的行为

GNOME TWEAK Tool 自 3.17.1 开始，可以**阻止** *systemd* 在“合上盖子”这一 ACPI 事件发生后采取默认行动。[[4]](http://ftp.gnome.org/pub/GNOME/sources/gnome-tweak-tool/3.17/gnome-tweak-tool-3.17.1.news) 若想要**阻止** *systemd* 的默认行为，打开 Tweak Tool，在“电源”标签页下选择“合上盖子后不待机”的选项。此选项意味着在盖子合上后，系统将不会默认待机，而是不采取任何措施。如果选择了此选项，一个自启动项目`~/.config/autostart/ignore-lid-switch-tweak.desktop`将会被创建，用于阻止*systemd*的默认行为。

如果你在合上盖子后既不希望系统待机，也不希望系统不动于衷，你首先要确保你并没有打开上述的选项，然后再配置*systemd*的`HandleLidSwitch=*默认行为*`选项，详见[Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management")中的说明。

##### 修改电池电量严重不足时的行为

设置面板不提供对电池电量严重不足行为的设置。这些设置也从dconf中移除。不过它们现在由uppower管理。按需编辑`/etc/UPower/Upower.conf`中upower设置。

 `/etc/UPower/UPower.conf` 
```
PercentageLow=10
PercentageCritical=3
PercentageAction=2
CriticalPowerAction=HybridSleep
```

#### 通过应用文件夹整理应用

{{提示| [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) 脚本允许您通过创建`~/.local/share/applications-categories`}下与分类同名的文件并在文件中包含您想包括在内的应用。或者，您可以使其在没有文件夹的情况下遍历各个应用直到您摁下ctrl-c或遍历完应用，然后输入想要的文件夹名称}

在**dconf-editor**中导航至 `org.gnome.desktop.app-folders` 并设置`folder-children`的值为一个由逗号分隔的文件夹的序列:

```
['Utilities', 'Sundry']

```

使用`gsettings`加入应用:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

上述命令将`alacarte.desktop`及`dconf-editor.desktop`加入到Sundry文件夹。 该命令也创建`org.gnome.desktop.app-folders.folders.Sundry`。

要显示文件夹名称（如果其在应用上部没有显示名称）：

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

应用也可以通过它们的分类整理 (在它们的*.desktop*文件中):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

如果某一个应用不想被加入某一文件夹，运行下列命令以设置例外:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

详情参考[app-folders schema](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in.in).

## 参见

*   [官方网站](http://www.gnome.org/)
*   [GNOME-shell 扩展](http://extensions.gnome.org/)
*   主题、图标和壁纸：
    *   [GNOME Art](http://art.gnome.org/)
    *   [GNOME 外观](http://www.gnome-look.org/)
*   GTK/GNOME 程序：
    *   [GNOME 文件管理](http://www.gnomefiles.org/)
    *   [GNOME 项目列表](http://www.gnome.org/projects/)
*   [自定义 GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html)
*   GNOME 代码和镜像:
    *   [GNOME Git 仓库](https://git.gnome.org/browse/)
    *   [GNOME Github 镜像](https://github.com/GNOME)