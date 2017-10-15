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

**翻译状态：** 本文是英文页面 [GNOME](/index.php/GNOME "GNOME") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-21，点击[这里](https://wiki.archlinux.org/index.php?title=GNOME&diff=0&oldid=451075)可以查看翻译后英文页面的改动。

[GNOME](https://www.gnome.org/)（读音是*gah-nohm* 或 *nohm*）是一个简单易用的[桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")。它是由 [GNOME 项目组](https://en.wikipedia.org/wiki/The_GNOME_Project 而不是 [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)") 进行显示。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 附加的软件包](#.E9.99.84.E5.8A.A0.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [2 GNOME 会话](#GNOME_.E4.BC.9A.E8.AF.9D)
*   [3 运行 GNOME](#.E8.BF.90.E8.A1.8C_GNOME)
    *   [3.1 图形界面启动](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E5.90.AF.E5.8A.A8)
    *   [3.2 手动启动](#.E6.89.8B.E5.8A.A8.E5.90.AF.E5.8A.A8)
        *   [3.2.1 Xorg 会话](#Xorg_.E4.BC.9A.E8.AF.9D)
        *   [3.2.2 Wayland 会话](#Wayland_.E4.BC.9A.E8.AF.9D)
    *   [3.3 Wayland 中的 GNOME 应用程序](#Wayland_.E4.B8.AD.E7.9A.84_GNOME_.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
*   [4 浏览](#.E6.B5.8F.E8.A7.88)
    *   [4.1 遗留名称](#.E9.81.97.E7.95.99.E5.90.8D.E7.A7.B0)
*   [5 配置](#.E9.85.8D.E7.BD.AE)
    *   [5.1 GNOME 系统设置](#GNOME_.E7.B3.BB.E7.BB.9F.E8.AE.BE.E7.BD.AE)
        *   [5.1.1 色彩设置](#.E8.89.B2.E5.BD.A9.E8.AE.BE.E7.BD.AE)
        *   [5.1.2 日期与时间](#.E6.97.A5.E6.9C.9F.E4.B8.8E.E6.97.B6.E9.97.B4)
        *   [5.1.3 默认应用程序](#.E9.BB.98.E8.AE.A4.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
        *   [5.1.4 鼠标和触摸板](#.E9.BC.A0.E6.A0.87.E5.92.8C.E8.A7.A6.E6.91.B8.E6.9D.BF)
        *   [5.1.5 网络](#.E7.BD.91.E7.BB.9C)
        *   [5.1.6 在线帐户](#.E5.9C.A8.E7.BA.BF.E5.B8.90.E6.88.B7)
        *   [5.1.7 搜索](#.E6.90.9C.E7.B4.A2)
    *   [5.2 高级设置](#.E9.AB.98.E7.BA.A7.E8.AE.BE.E7.BD.AE)
        *   [5.2.1 外观](#.E5.A4.96.E8.A7.82)
            *   [5.2.1.1 GTK+主题和图标主题](#GTK.2B.E4.B8.BB.E9.A2.98.E5.92.8C.E5.9B.BE.E6.A0.87.E4.B8.BB.E9.A2.98)
                *   [5.2.1.1.1 全局暗色主题](#.E5.85.A8.E5.B1.80.E6.9A.97.E8.89.B2.E4.B8.BB.E9.A2.98)
            *   [5.2.1.2 窗口管理器主题](#.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8.E4.B8.BB.E9.A2.98)
                *   [5.2.1.2.1 标题栏的高度](#.E6.A0.87.E9.A2.98.E6.A0.8F.E7.9A.84.E9.AB.98.E5.BA.A6)
                *   [5.2.1.2.2 标题栏按钮重新排序](#.E6.A0.87.E9.A2.98.E6.A0.8F.E6.8C.89.E9.92.AE.E9.87.8D.E6.96.B0.E6.8E.92.E5.BA.8F)
                *   [5.2.1.2.3 最大化时隐藏标题栏](#.E6.9C.80.E5.A4.A7.E5.8C.96.E6.97.B6.E9.9A.90.E8.97.8F.E6.A0.87.E9.A2.98.E6.A0.8F)
            *   [5.2.1.3 GNOME Shell主题](#GNOME_Shell.E4.B8.BB.E9.A2.98)
            *   [5.2.1.4 Icons on menu](#Icons_on_menu)
        *   [5.2.2 桌面](#.E6.A1.8C.E9.9D.A2)
            *   [5.2.2.1 桌面上的图标](#.E6.A1.8C.E9.9D.A2.E4.B8.8A.E7.9A.84.E5.9B.BE.E6.A0.87)
            *   [5.2.2.2 锁屏和背景](#.E9.94.81.E5.B1.8F.E5.92.8C.E8.83.8C.E6.99.AF)
        *   [5.2.3 扩展](#.E6.89.A9.E5.B1.95)
        *   [5.2.4 输入法](#.E8.BE.93.E5.85.A5.E6.B3.95)
        *   [5.2.5 字体](#.E5.AD.97.E4.BD.93)
        *   [5.2.6 启动应用程序](#.E5.90.AF.E5.8A.A8.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
        *   [5.2.7 电源](#.E7.94.B5.E6.BA.90)
            *   [5.2.7.1 配置合上盖子时的行为](#.E9.85.8D.E7.BD.AE.E5.90.88.E4.B8.8A.E7.9B.96.E5.AD.90.E6.97.B6.E7.9A.84.E8.A1.8C.E4.B8.BA)
            *   [5.2.7.2 修改电池电量严重不足时的行为](#.E4.BF.AE.E6.94.B9.E7.94.B5.E6.B1.A0.E7.94.B5.E9.87.8F.E4.B8.A5.E9.87.8D.E4.B8.8D.E8.B6.B3.E6.97.B6.E7.9A.84.E8.A1.8C.E4.B8.BA)
        *   [5.2.8 Sort applications into application (app) folders](#Sort_applications_into_application_.28app.29_folders)
*   [6 参见](#.E5.8F.82.E8.A7.81)

## 安装

以下两个软件组均包含 GNOME 的组件：

*   [gnome](https://www.archlinux.org/groups/x86_64/gnome/) 组包含基本的桌面环境和良好集成的[应用程序](https://wiki.gnome.org/Apps)；

*   [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/) 组包含其他的 GNOME 应用，包括[文本编辑器](/index.php/Gedit "Gedit")、压缩文件管理器、磁盘管理器以及一些游戏。 [gnome](https://www.archlinux.org/groups/x86_64/gnome/) 软件组是这个组的基础。

基础桌面环境包含了 [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell 窗口管理器的插件。它可以通过软件包 [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) 单独安装。

**注意:** *mutter* 是 gnome 桌面的混合管理器。它利用硬件加速减少屏幕杂乱。GNOME 会话管理器会自动检测显卡驱动是否足以运行 GNOME Shell，如果不行则用 *llvmpipe* 软件绘制。

### 附加的软件包

上面提到的软件组不包括以下软件包：

*   **[Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — 访问 [libvirt](/index.php/Libvirt "Libvirt") 虚拟机的用户接口。

	[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **Games** — GNOME 的游戏启动器。

	[https://wiki.gnome.org/Apps/Games](https://wiki.gnome.org/Apps/Games) || [gnome-games](https://www.archlinux.org/packages/?name=gnome-games)

*   **GNOME Initial Setup** — 准备新系统的简单、易用和安全的工具。

	[https://github.com/GNOME/gnome-initial-setup](https://github.com/GNOME/gnome-initial-setup) || [gnome-initial-setup](https://www.archlinux.org/packages/?name=gnome-initial-setup)

*   **GNOME MultiWriter** — 一次性将ISO文件写入多个USB设备。

	[https://wiki.gnome.org/Apps/MultiWriter](https://wiki.gnome.org/Apps/MultiWriter) || [gnome-multi-writer](https://www.archlinux.org/packages/?name=gnome-multi-writer)

*   **GNOME PackageKit** — GNOME 的 PackageKit 图形工具集。

	[https://github.com/GNOME/gnome-packagekit](https://github.com/GNOME/gnome-packagekit) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **[Nemiver](https://en.wikipedia.org/wiki/Nemiver "wikipedia:Nemiver")** — C/C++ 调试器。

	[https://wiki.gnome.org/Apps/Nemiver](https://wiki.gnome.org/Apps/Nemiver) || [nemiver](https://www.archlinux.org/packages/?name=nemiver)

*   **Recipes** — GNOME 的食谱管理应用。

	[https://wiki.gnome.org/Apps/Recipes](https://wiki.gnome.org/Apps/Recipes) || [gnome-recipes](https://www.archlinux.org/packages/?name=gnome-recipes)

*   **Simple Scan** — 简单的扫描工具。

	[https://launchpad.net/simple-scan](https://launchpad.net/simple-scan) || [simple-scan](https://www.archlinux.org/packages/?name=simple-scan)

*   **[Software](https://en.wikipedia.org/wiki/GNOME_Software "wikipedia:GNOME Software")** — 安装和更新软件和系统扩展。

	[https://wiki.gnome.org/Apps/Software/](https://wiki.gnome.org/Apps/Software/) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

## GNOME 会话

GNOME 有三个可用的会话，都使用 GNOME Shell。

*   **GNOME** 是使用 Wayland 的默认会话，传统X应用将通过 Xwayland 运行。
*   **GNOME Classic** 的桌面布局类似于传统的GNOME 2, 使用预先激活的插件和参数。[[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) 因此，它更像是一个定制的 GNOME Shell，而不是完全独立的模式。
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

修改完 `~/.xinitrc` 后，即可使用 `startx` 启动 GNOME（有关其他详细信息，例如如何保留 logind 会话，详见 [xinitrc](/index.php/Xinitrc "Xinitrc")）。设置完 `~/.xinitrc` 后，也可以设定[在登录时启动X](/index.php/Start_X_at_login "Start X at login")。

#### Wayland 会话

**注意:**

*   [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) 软件包提供的X服务器仍然需要用于运行尚未移植到 [Wayland](/index.php/Wayland_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wayland (简体中文)") 的应用程序。
*   使用专有 NVIDIA 驱动的 Wayland 目前拥有非常差的性能：[FS#53284](https://bugs.archlinux.org/task/53284)。

可以用 `XDG_SESSION_TYPE=wayland dbus-run-session gnome-session` 手动启动 Wayland 会话。

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
*   `Alt` + `F2`：输入命令以快速启动应用
*   `Alt` + `F2`，然后输入 `r` 或 `restart`：重启界面如果图形界面出了问题（仅用于 X/传统 模式，不用于 Wayland 模式）。

### 遗留名称

**注意:** 一些 GNOME 程序在文档和对话框中的名称已经更改，但执行文件名称却没有。下面表格列出了一些这样的应用程序。

**提示：** 在搜索栏中搜索应用程序的遗留名称将成功找到要找应用程序，例如搜索 *nautilus* 将返回 *Files*。

| 当前 | 遗留 |
| [Files](/index.php/Files "Files") | Nautilus |
| [Web](/index.php/GNOME/Web "GNOME/Web") | Epiphany |
| Videos | Totem |
| Main Menu | Alacarte |
| Document Viewer | Evince |
| Disk Usage Analyser | Baobab |
| Image Viewer | EoG (Eye of GNOME) |
| [Passwords and Keys](/index.php/GNOME/Keyring "GNOME/Keyring") | Seahorse |

## 配置

GNOME 3 是重新设计的，但是像大多数大型软件项目一样，他是很多不同时间的部分组装起来的。他没有一个 **无所不包** 的配置工具。新的 *系统设置* 比以前的控制面板有很大的改进。 *系统设置* 组织得很好，但是你可能想要更深层次地改变外观。

以前你所熟悉的配置工具现在有的好用，有的不好用了。有些设置选项隐藏着，不太容易找到。许多设置将会，或已经迁移到了新的工具上。你需要了解应当去哪里寻找适当的设置项，才能更好地配置 GNOME 外观。

GNOME 桌面环境依赖于一个存储配置的数据库后端（DConf）来存储 GNOME 与 GNOME 应用的设置。安装桌面环境时，GNOME 提供一套默认的配置，而各类应用程序向数据库中添加它们自己的配置。

对用户来说，最基础而直观的配置方式莫过于使用 GNOME 系统设置面板（gnome-control-center），以及 GNOME 应用程序各自的首选项（preferences）面板。如果您愿意，直接在 DConf 数据库中进行修改与配置总是可行的，尤其是在某些设置选项没有暴露在用户界面的情况下，直接修改可以更改某些隐藏选项。

GNOME 的这些配置通常是用户间相互独立的。以下文字仅供单用户配置所用，并没有提及更改全局配置模板的方法。

### GNOME 系统设置

系统设置工具包括了一些最基础的 GNOME 环境配置选项。

#### 色彩设置

`colord` 守护进程读取显示器的 [EDID](https://zh.wikipedia.org/wiki/EDID)信息，并提取出合适的色彩配置内容。大多数情况下，自动色彩配置都是正确的，不需要额外设置；但是对于可能出现的偏差情况，例如使用较旧的显示器时，您可以将色彩配置文件放在 `~/.local/share/icc/` 下，并在设置面板里启用。

#### 日期与时间

如果系统已有配置好的 [NTP 守护进程](/index.php/Network_Time_Protocol_daemon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network Time Protocol daemon (简体中文)")，它同样会对 GNOME 桌面环境起作用。如果需要，您也可以手动控制进行同步。

如需在顶栏显示日期，请运行：

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

另外，如需在 shell 的日历中显示周数，请运行：

```
$ gsettings set org.gnome.shell.calendar show-weekdate true

```

当然，以上配置均可以在 `gnome-tweak-tool` 里完成。

#### 默认应用程序

Upon installing GNOME for the first time, you may find that the wrong applications are handling certain protocols. For example, *totem* opens videos instead of a previously used [VLC](/index.php/VLC "VLC"). Some of the associations can be set from system settings via: *System* > *Details* > *Default applications*.

For other protocols and methods see [Default applications](/index.php/Default_applications "Default applications") for configuration.

#### 鼠标和触摸板

为了帮助减少触摸板的干扰，你可能希望实现以下设置：

*   禁用触摸板，打字时
*   禁用滚动
*   禁用点击

**Note:** GNOME 目前不再支持 [synaptics](/index.php/Synaptics "Synaptics")，请使用 [libinput](/index.php/Libinput "Libinput"). 参考 [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12).

#### 网络

[NetworkManager](/index.php/NetworkManager "NetworkManager") is the native tool of the GNOME project to control network settings from the shell. It is installed by default as a dependency for [tracker](https://www.archlinux.org/packages/?name=tracker) package, which is a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group, and just needs to be [enabled](/index.php/NetworkManager#Enable_NetworkManager "NetworkManager").

While any other [network manager](/index.php/List_of_applications/Internet#Network_managers "List of applications/Internet") can be used as well, NetworkManager provides the full integration via the shell network settings and a status indicator applet [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (not required for GNOME).

#### 在线帐户

Backends for the GNOME messaging application [empathy](https://www.archlinux.org/packages/?name=empathy) as well as the GNOME Online Accounts section of the System Settings panel are provided in a separate group: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). See [#Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts). Some online accounts, such as [ownCloud](/index.php/OwnCloud "OwnCloud"), require [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) to be installed for full functionality in GNOME applications such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") and GNOME Documents [[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### 搜索

The GNOME shell has a search that can be quickly accessed by pressing the `Super` key and starting to type. The [tracker](https://www.archlinux.org/packages/?name=tracker) package is installed by default as a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group and provides an indexing application and metadata database. It can be configured with the *Search and Indexing* menu item; monitor status with *tracker-control*. It is started automatically by *gnome-session* when the user logs in. Indexing can be started manually with `tracker-control -s`. Search settings can also be configured in the *System Settings* panel.

The Tracker database can be queried using the *tracker-sparql* command. View its manual page [tracker-sparql(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tracker-sparql.1) for more information.

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

GNOME will use the Adwaita light theme by default however a dark variant of this theme (called the Global Dark Theme) also exists and can be selected using the Tweak Tool or by editing the GTK+ 3 settings file - see [GTK+#Dark theme variant](/index.php/GTK%2B#Dark_theme_variant "GTK+"). Some applications such as Image Viewer (*eog*) use the dark theme by default. It should be noted that the Global Dark Theme only works with GTK+ 3 applications; some GTK+ 3 applications may only have partial support for the Global Dark theme. Qt and GTK+ 2 support for the Global Dark Theme may be added in the future.

##### 窗口管理器主题

The window manager theme (the style of the window titlebars) can be set using the GNOME Tweak Tool or the following GSettings command:

```
$ gsettings set org.gnome.desktop.wm.preferences theme *theme-name*

```

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

*   [Install](/index.php/Install "Install") [gnome-shell-extension-pixel-saver-git](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver-git/) or [gnome-shell-extension-pixel-saver](https://aur.archlinux.org/packages/gnome-shell-extension-pixel-saver/). Maximized windows get the title bar merged into the activity bar, saving precious pixels.

*   [Install](/index.php/Install "Install") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). It changes a default setting in the window manager, so as to automatically hide the titlebar on legacy (non-headerbar) apps when they are maximized or tiled to the side.

*   [Install](/index.php/Install "Install") [maximus](https://aur.archlinux.org/packages/maximus/). To start the application, execute *maximus* from a terminal. When running, the daemon will automatically maximize windows. It will undecorate maximized windows and redecorate them when they are unmaximized. If you do not want all windows to start maximized, run `maximus -m` instead. Note that this will only work with windows decorated by the window manager; applications that use client-side decoration such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") will not be undecorated when maximized.

##### GNOME Shell主题

The theme of GNOME Shell itself is configurable. To use a Shell theme, firstly ensure that you have the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package installed. Then enable the *User Themes* extension, either through GNOME Tweak Tool or through the [GNOME Shell Extensions](https://extensions.gnome.org) webpage. Shell themes can then be loaded and selected using the GNOME Tweak Tool.

There are a number of GNOME Shell themes available [in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d).

Shell themes can also be downloaded from [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=191).

##### Icons on menu

The default GNOME schema doesn't display any icon on menus. To display icons on menus, issue the following command.

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

#### 桌面

各种桌面设置可以应用。

##### 桌面上的图标

参阅 [GNOME Files#Desktop Icons](/index.php/GNOME_Files#Desktop_Icons "GNOME Files").

##### 锁屏和背景

When setting the Desktop or Lock screen background, it is important to note that the Pictures tab will only display pictures located in `/home/*username*/Pictures` folder. If you wish to use a picture not located in this folder, use the commands indicated below.

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

在安装完一个扩展之后可能需要[重启 GNOME shell](#.E9.87.8D.E5.90.AF_GNOME_shell) 。故障排除信息参照[安装扩展导致GNOME停止工作](#.E5.AE.89.E8.A3.85.E6.89.A9.E5.B1.95.E5.AF.BC.E8.87.B4GNOME.E5.81.9C.E6.AD.A2.E5.B7.A5.E4.BD.9C)。

#### 输入法

GNOME集成了的通过[IBus](/index.php/IBus "IBus")的输入法, 只有[ibus](https://www.archlinux.org/packages/?name=ibus)和添加想要的输入法引擎 (例如:[ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) for Intelligent Pinyin) 需要安装，安装后，输入法引擎可以加入GNOME的区域和语言设置键盘布局。

#### 字体

**Tip:** If you set the *Scaling factor* to a value above 1.00, the Accessibility menu will be automatically enabled.

Fonts can be set for Window titles, Interface (applications), Documents and Monospace. See the Fonts tab in the Tweak Tool for the relevant options.

For hinting, RGBA will likely be desired as this fits most monitors types, and if fonts appear too blocked reduce hinting to *Slight* or *None*.

#### 启动应用程序

要启动登录某些应用程序, copy the relevant `.desktop` file from `/usr/share/applications/` to `~/.config/autostart/`. [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) 支持管理 autostart-entries。

**Tip:** If the plus sign button in the Tweak Tool's Startup Applications section is unresponsive, try start the Tweak Tool from the terminal using the following command: `gnome-tweak-tool`. See the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Note:** The *gnome-session-properties* dialog was removed as of GNOME 3.12\. It can be added back by [installing](/index.php/Install "Install") the [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/) package.

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

##### 配置合上盖子时的行为

GNOME TWEAK Tool 自 3.17.1 开始，可以**阻止** *systemd* 在“合上盖子”这一 ACPI 事件发生后采取默认行动。[[4]](http://ftp.gnome.org/pub/GNOME/sources/gnome-tweak-tool/3.17/gnome-tweak-tool-3.17.1.news) 若想要**阻止** *systemd* 的默认行为，打开 Tweak Tool，在“电源”标签页下选择“合上盖子后不待机”的选项。此选项意味着在盖子合上后，系统将不会默认待机，而是不采取任何措施。如果选择了此选项，一个自启动项目`~/.config/autostart/ignore-lid-switch-tweak.desktop`将会被创建，用于阻止*systemd*的默认行为。

如果你在合上盖子后既不希望系统待机，也不希望系统不动于衷，你首先要确保你并没有打开上述的选项，然后再配置*systemd*的`HandleLidSwitch=*默认行为*`选项，详见[Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management")中的说明。

##### 修改电池电量严重不足时的行为

The settings panel does not provide an option for changing the critical battery level action. These settings have been removed from dconf as well. They are now managed by upower. Edit the upower settings in `/etc/UPower/UPower.conf`. Find these settings and adjust to your needs.

 `/etc/UPower/UPower.conf` 
```
PercentageLow=10
PercentageCritical=3
PercentageAction=2
CriticalPowerAction=HybridSleep
```

#### Sort applications into application (app) folders

**Tip:** The [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) script allows you to manage folders through the creation of files in `~/.local/share/applications-categories` named after each category and containing a list of the desktop files belonging to apps you'd like to have inside. Optionally, you can have it cycle through each app without a folder and input the desired category until you ctrl-c or run out of apps.

In the **dconf-editor** navigate to `org.gnome.desktop.app-folders` and set the value of `folder-children` to an array of comma separated folder names:

```
['Utilities', 'Sundry']

```

Add applications using `gsettings`:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

This adds the applications `alacarte.desktop` and `dconf-editor.desktop` to the Sundry folder. This will also create the folder `org.gnome.desktop.app-folders.folders.Sundry`.

To name the folder (if it has no name that appears at the top of the applications):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

Applications can also be sorted by their category (specified in their *.desktop* file):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

If certain applications matching a category are not wanted in a certain folder, exclusions can be set:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

For further information, refer to the [app-folders schema](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in.in).

## 参见

*   [官方网站](http://www.gnome.org/)
*   [GNOME-shell扩展](http://extensions.gnome.org/)
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