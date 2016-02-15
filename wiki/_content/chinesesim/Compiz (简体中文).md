**翻译状态：** 本文是英文页面 [Compiz](/index.php/Compiz "Compiz") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-08-14，点击[这里](https://wiki.archlinux.org/index.php?title=Compiz&diff=0&oldid=328840)可以查看翻译后英文页面的改动。

来源于维基百科[Compiz条目](http://zh.wikipedia.org/wiki/Compiz)的解释:

	_Compiz 是第一个由 [OpenGL](http://zh.wikipedia.org/wiki/OpenGL) 驱动的运行于 [X Window System](http://zh.wikipedia.org/wiki/X_Window_System) 上的混合窗口管理器 。Compiz的混合渲染能力使其可以在窗口管理过程中实现多种视觉效果，比如在矩形虚拟桌面上的窗口最小化。_

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 安装0.9系列版本](#.E5.AE.89.E8.A3.850.9.E7.B3.BB.E5.88.97.E7.89.88.E6.9C.AC)
    *   [1.2 安装0.8系列版本](#.E5.AE.89.E8.A3.850.8.E7.B3.BB.E5.88.97.E7.89.88.E6.9C.AC)
    *   [1.3 窗口装饰器](#.E7.AA.97.E5.8F.A3.E8.A3.85.E9.A5.B0.E5.99.A8)
*   [2 开始使用 Compiz](#.E5.BC.80.E5.A7.8B.E4.BD.BF.E7.94.A8_Compiz)
    *   [2.1 启用重要的插件](#.E5.90.AF.E7.94.A8.E9.87.8D.E8.A6.81.E7.9A.84.E6.8F.92.E4.BB.B6)
    *   [2.2 启动 Compiz](#.E5.90.AF.E5.8A.A8_Compiz)
        *   [2.2.1 小工具 Fusion Icon](#.E5.B0.8F.E5.B7.A5.E5.85.B7_Fusion_Icon)
    *   [2.3 让你的桌面环境自动启动Compiz](#.E8.AE.A9.E4.BD.A0.E7.9A.84.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8Compiz)
        *   [2.3.1 KDE4](#KDE4)
            *   [2.3.1.1 使用系统设置](#.E4.BD.BF.E7.94.A8.E7.B3.BB.E7.BB.9F.E8.AE.BE.E7.BD.AE)
            *   [2.3.1.2 Autostart 自动启动链接](#Autostart_.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8.E9.93.BE.E6.8E.A5)
            *   [2.3.1.3 设置 KDEWM 变量](#.E8.AE.BE.E7.BD.AE_KDEWM_.E5.8F.98.E9.87.8F)
        *   [2.3.2 GNOME 桌面环境](#GNOME_.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)
            *   [2.3.2.1 GNOME Shell 和 Cinnamon](#GNOME_Shell_.E5.92.8C_Cinnamon)
            *   [2.3.2.2 Unity](#Unity)
            *   [2.3.2.3 其它的GNOME会话 (Cairo dock 和 Compiz)](#.E5.85.B6.E5.AE.83.E7.9A.84GNOME.E4.BC.9A.E8.AF.9D_.28Cairo_dock_.E5.92.8C_Compiz.29)
            *   [2.3.2.4 GNOME Flashback](#GNOME_Flashback)
        *   [2.3.3 MATE 桌面环境](#MATE_.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)
            *   [2.3.3.1 使用 GSettings](#.E4.BD.BF.E7.94.A8_GSettings)
            *   [2.3.3.2 使用 mate-session-properties](#.E4.BD.BF.E7.94.A8_mate-session-properties)
        *   [2.3.4 Xfce](#Xfce)
            *   [2.3.4.1 修改默认 (故障保护Failsafe) 会话](#.E4.BF.AE.E6.94.B9.E9.BB.98.E8.AE.A4_.28.E6.95.85.E9.9A.9C.E4.BF.9D.E6.8A.A4Failsafe.29_.E4.BC.9A.E8.AF.9D)
            *   [2.3.4.2 Starting Compiz from a restored Xfce session](#Starting_Compiz_from_a_restored_Xfce_session)
            *   [2.3.4.3 Using Xfce application autostart](#Using_Xfce_application_autostart)
        *   [2.3.5 LXDE & LXQt](#LXDE_.26_LXQt)
*   [3 Using Compiz as a standalone window manager](#Using_Compiz_as_a_standalone_window_manager)
    *   [3.1 Starting the session with a display manager](#Starting_the_session_with_a_display_manager)
        *   [3.1.1 Autostarting programs when using a display manager](#Autostarting_programs_when_using_a_display_manager)
    *   [3.2 Starting the session with startx](#Starting_the_session_with_startx)
    *   [3.3 Add a root menu](#Add_a_root_menu)
    *   [3.4 Allow users to shutdown/reboot](#Allow_users_to_shutdown.2Freboot)
    *   [3.5 Utilities](#Utilities)
        *   [3.5.1 Panels & docks](#Panels_.26_docks)
        *   [3.5.2 Run dialog](#Run_dialog)
*   [4 小技巧大放送](#.E5.B0.8F.E6.8A.80.E5.B7.A7.E5.A4.A7.E6.94.BE.E9.80.81)
    *   [4.1 还原原生窗口管理器](#.E8.BF.98.E5.8E.9F.E5.8E.9F.E7.94.9F.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [4.2 启用 Alt+F2 运行对话框](#.E5.90.AF.E7.94.A8_Alt.2BF2_.E8.BF.90.E8.A1.8C.E5.AF.B9.E8.AF.9D.E6.A1.86)
        *   [4.2.1 GNOME Panel](#GNOME_Panel)
        *   [4.2.2 MATE Panel](#MATE_Panel)
        *   [4.2.3 LXDE Panel](#LXDE_Panel)
        *   [4.2.4 Xfce 程序查看器（_Appfinder_）](#Xfce_.E7.A8.8B.E5.BA.8F.E6.9F.A5.E7.9C.8B.E5.99.A8.EF.BC.88Appfinder.EF.BC.89)
        *   [4.2.5 其他的运行对话框功能](#.E5.85.B6.E4.BB.96.E7.9A.84.E8.BF.90.E8.A1.8C.E5.AF.B9.E8.AF.9D.E6.A1.86.E5.8A.9F.E8.83.BD)
*   [5 疑难排解](#.E7.96.91.E9.9A.BE.E6.8E.92.E8.A7.A3)
    *   [5.1 Missing GLX_EXT_texture_from_pixmaps](#Missing_GLX_EXT_texture_from_pixmaps)
        *   [5.1.1 On ATI cards (first solution)](#On_ATI_cards_.28first_solution.29)
        *   [5.1.2 On ATI cards (second solution)](#On_ATI_cards_.28second_solution.29)
        *   [5.1.3 On Intel chips](#On_Intel_chips)
    *   [5.2 Compiz starts without window borders with NVIDIA binary drivers](#Compiz_starts_without_window_borders_with_NVIDIA_binary_drivers)
    *   [5.3 Blank screen on resume from suspend-to-ram using the NVIDIA binary drivers](#Blank_screen_on_resume_from_suspend-to-ram_using_the_NVIDIA_binary_drivers)
    *   [5.4 Poor performance from capable graphics cards](#Poor_performance_from_capable_graphics_cards)
    *   [5.5 Screen flicks with NVIDIA card](#Screen_flicks_with_NVIDIA_card)
    *   [5.6 Compiz effects not working (GConf backend)](#Compiz_effects_not_working_.28GConf_backend.29)
    *   [5.7 Fusion Icon fails to start](#Fusion_Icon_fails_to_start)
    *   [5.8 Alt+F4 keybinding not working (Xfce)](#Alt.2BF4_keybinding_not_working_.28Xfce.29)
    *   [5.9 Emerald refuses to start (crashes with a segfault)](#Emerald_refuses_to_start_.28crashes_with_a_segfault.29)
    *   [5.10 No system bell when Compiz is running](#No_system_bell_when_Compiz_is_running)
    *   [5.11 Compiz crashes when enabling the Gnome Compatibility plugin (GSettings backend)](#Compiz_crashes_when_enabling_the_Gnome_Compatibility_plugin_.28GSettings_backend.29)
*   [6 Known issues](#Known_issues)
    *   [6.1 Xfce panel window buttons are not refreshed when a window changes viewport](#Xfce_panel_window_buttons_are_not_refreshed_when_a_window_changes_viewport)
    *   [6.2 Compiz crashes when enabling the D-Bus plugin](#Compiz_crashes_when_enabling_the_D-Bus_plugin)
*   [7 See also](#See_also)

## 安装

*   2013年5月起， Compiz 在[official repositories](/index.php/Official_repositories "Official repositories")中就[不再可用了](https://mailman.archlinux.org/pipermail/arch-dev-public/2013-May/024956.html)。
*   安装0.9和0.8版本的包可以在[AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")中找到。
*   这两个版本**不能同时安装**。

### 安装0.9系列版本

**注意:** 从 Compiz 0.9.8 开始，所有的Compiz组件（包括CCSM、插件、gtk-window-decorator等）都是当作一个单独项目来开发的。也就是说一个安装包就包括了Compiz的全部组件。

你可以安装[compiz](https://aur.archlinux.org/packages/compiz/)或[compiz-bzr](https://aur.archlinux.org/packages/compiz-bzr/)，其中[compiz-bzr](https://aur.archlinux.org/packages/compiz-bzr/)是开发版本。

Emerald窗口装饰器可以从下面任意一个包安装：[emerald0.9](https://aur.archlinux.org/packages/emerald0.9/)。 附加的Emerald主题可以从[emerald-themes](https://aur.archlinux.org/packages/emerald-themes/)包中安装。

### 安装0.8系列版本

安装以下任意一个包：[compiz-core](https://aur.archlinux.org/packages/compiz-core/)、 [compiz-gtk-standalone](https://aur.archlinux.org/packages/compiz-gtk-standalone/) 或 [compiz-core-mate](https://aur.archlinux.org/packages/compiz-core-mate/)。

需要Compiz设置中心，请安装 [ccsm](https://aur.archlinux.org/packages/ccsm/)。

需要插件，请安装 [compiz-fusion-plugins-main](https://aur.archlinux.org/packages/compiz-fusion-plugins-main/)、 [compiz-fusion-plugins-extra](https://aur.archlinux.org/packages/compiz-fusion-plugins-extra/) 。 并且可选地，可以安装 [compiz-fusion-plugins-unsupported](https://aur.archlinux.org/packages/compiz-fusion-plugins-unsupported/)。

Emerald窗口装饰器可以从 [emerald](https://aur.archlinux.org/packages/emerald/) 包中安装。 需要附加的Emerald主题可以安装 [emerald-themes](https://aur.archlinux.org/packages/emerald-themes/) 。

### 窗口装饰器

**提示:** 想知道更多关于选择与管理主题的情况，请访问：[Compiz configuration#Window decoration themes](/index.php/Compiz_configuration#Window_decoration_themes "Compiz configuration")。

**注意:**

*   大多数的Compiz软件包都会默认提供 gtk-window-decorator （一个GTK窗口装饰器组件）。唯一的例外则是 [compiz-core](https://aur.archlinux.org/packages/compiz-core/) 包中并没有提供窗口装饰器。
*   目前没有任何一个包自动提供 kde-window-decorator （一个KDE窗口装饰器组件）。想要安装它，你需要编辑将要安装的 Compiz 包中的 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 文件，从中打开相关的选项。当你编辑完之后，还需要重新编译并安装 Compiz 包。

窗口装饰器是为程序提供窗口和边框的程序。 不像类似[mutter](https://www.archlinux.org/packages/?name=mutter)之类的窗口管理器， 不像Kwin或者[Xfwm](/index.php/Xfwm "Xfwm")只提供一个唯一的装饰器， Compiz的用户拥有三个选择：Emerald、gtk-window-decorator以及kde-window-decorator。

其中gtk-window-decorator 和 the kde-window-decorator 就包含在 Compiz 的源代码中，并且已经编译好了（如果你的PKGBUILD文件设置妥当的话）。 而Emerald分离在外，是一个独立的装饰器软件。

设置它可以按照如下步骤：

首先，确定你已经安装了你想要在Compiz中使用的装饰器。然后，打开 CCSM （_Compiz Config Setting Manager ，Compiz设置管理器_）。 你可以找到它的图标或者在终端中运行命令： `ccsm`。在设置界面中，找到“效果”部分，并保证“Window Decoration”（_”窗口装饰“_）已经勾选了。 现在，点击“Window Decoration”（_”窗口装饰“_）按钮，并且在”命令“框中输入跟你需要的装饰器相关的命令：

*   `emerald`

*   `gtk-window-decorator`

*   `kde4-window-decorator`

为了让这些改动立即生效，你可能需要在命令的结尾添加 `--replace` 开关。 另外，注销之后再登陆进来也可以让你新设置的装饰器生效。 不过请注意，在CCSM中输入的使用 `--replace` 开关的装饰器命令，会在用户登陆的时候使屏幕闪一下。

## 开始使用 Compiz

### 启用重要的插件

在开始使用Compiz之前， 你需要激活一些提供窗口管理基本功能的插件。 要不然你可能连拖拽窗口都困难，更别说缩放和关闭了。

重要的插件列在了下面：

**提示:** _译者注_ 为了大家看得方便，我把插件的名字保留了英文。因为有时候CCSM里面也会显示英文的插件名称。

**提示:** _译者注_ 插件的中文名称可能翻译得不准确。

*   窗口装饰（_Window Decoration_） —— 提供窗口边框（上一节咱已经讨论过了）
*   窗口移动（_Move Window_）
*   窗口缩放（_Resize Window_）
*   窗口放置（_Place Windows_） —— 设置关于窗口在屏幕上放置的选项
*   程序切换器（_Application Switcher_） —— 提供 Alt+Tab 开启的程序切换器（另外也有一些插件可以实现这个功能，而且具有不同的效果，比如 'Shift Switcher,' 'Static Application Switcher' 等等。并不是所有的切换器都是用 Alt+Tab 快捷键）。
*   OpenGL —— （只在CCSM 0.9版本中可见）。
*   合成（_Composite_） —— （只在CCSM 0.9版本中可见）。

想要在不同的”视口“（[viewports](/index.php/Compiz_configuration#Workspaces_and_Viewports "Compiz configuration")）之间切换，你需要激活以下其中一个插件：

*   桌面立方(_Desktop Cube_）和旋转立方体（_Rotate Cube_） —— 提供一个可以浮空的立方体，每个面都是一个视口（_虚拟桌面_）。
*   桌面墙壁（_Desktop Wall_） —— 视口全部并排陈列在一起（非常类似于[Cinnamon](/index.php/Cinnamon "Cinnamon") 和 [GNOME Shell](/index.php/GNOME_Shell "GNOME Shell") 中的窗口切换效果）。
*   Expo —— 当鼠标移动到屏幕左上角的时候，显示出全部的视口和窗口（_就是Ubuntu Unity里面那种！！_）。这个插件可以单独激活，或者是和前两个一起用不会冲突。

### 启动 Compiz

**注意:** 曾几何时，出现过一个包错误，导致你需要在运行 `compiz --replace` 命令时使用 `ccp` 开关才能正常导入Compiz插件。不过现在这个错误已经修正了，现在已经**没有任何必要**使用 `ccp` 开关。

你可以使用下面的命令启动Compiz：

```
$ compiz --replace &

```

**提示:** 如果 `compiz --replace &` 命令在进入会话时不管用。 试一试没有a花的命令： `compiz --replace`。

我们来过一下常用的Compiz命令行选项吧：

*   `--indirect-rendering`: 使用间接渲染 (AIGLX)
*   `--loose-binding`: 可以解决一些性能问题 (NVIDIA?)
*   `--replace`: 取代现有的窗口管理器（_window-manager_）
*   `--keep-window-hints`: 在可用的视口中保留Gnome窗口管理器的 gconf-settings 设置
*   `--sm-disable`: 禁用会话管理功能

#### 小工具 Fusion Icon

Fusion Icon 是一个托盘小工具，功能是在一个会话中切换Compiz和其他不同的窗口管理器以及装饰器。 **它只和Compiz 0.8版本兼容。** 它可以在 [fusion-icon](https://aur.archlinux.org/packages/fusion-icon/) 包中安装。

你可以用下面的命令运行 fusion-icon ：

```
$ fusion-icon

```

为了确保Fusion-icon确实启动了Compiz，邮件单击它在通知区域的图标，然后选择“select window manager”， 如果“Compiz”还没被选上的话就选上吧。

下面将要讲到的很多方法会在桌面环境启动时自动运行Compiz。你也可以叫桌面环境自动运行fusion-icon来间接自动启动Compiz。 如果你想这样做的话， 只要把Compiz的命令 （通常都是 `compiz --replace &`）改成 `fusion-icon` 就行了。

### 让你的桌面环境自动启动Compiz

#### KDE4

##### 使用系统设置

打开系统设置程序，并找到“系统设置 > 默认程序 > 窗口管理器 > 使用另外的窗口管理器'”然后选择“Compiz”。

如果你需要让Compiz使用你自己设定的选项启动的话，就选择“Compiz custom”，然后新建一个叫做`compiz-kde-launcher` 的脚本，并且在其中添加你希望启动Compiz的命令。 下面是一个例子：

 `/usr/local/bin/compiz-kde-launcher` 

```
#!/bin/bash
LIBGL_ALWAYS_INDIRECT=1
compiz --replace &
wait

```

然后还要让他可运行：

```
$ chmod +x /usr/local/bin/compiz-kde-launcher

```

##### Autostart 自动启动链接

**注意:**

*   如果你想安装 gtk-window-decorator，就不要新建 `compiz.desktop` 文件，因为这回产生一些问题。
*   如果 `compiz.desktop` 已经有了，那你可能需要在 `Exec` 之后添加 `--replace` 。

在KDE自动启动（_Autostart_）目录中添加一个项目。如果它不存在，就新建一个：

 `~/.kde4/Autostart/compiz.desktop` 

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=Compiz
Exec=/usr/bin/compiz --replace
NoDisplay=true
# name of loadable control center module
X-GNOME-WMSettingsModule=compiz
# autostart phase
X-GNOME-Autostart-Phase=WindowManager
X-GNOME-Provides=windowmanager
# name we put on the WM spec check window
X-GNOME-WMName=Compiz
# back compat only
X-GnomeWMSettingsLibrary=compiz
```

##### 设置 KDEWM 变量

作为root用户你需要搞一个小脚本，这样你就可以在启动Compiz的时候添加命令行选项了。

新建一个文件，里面输入启动Compiz的命令，再加上你希望附加的设置。下面是一个例子：

 `/usr/bin/startcompiz` 

```
compiz --replace &

```

**注意:** 你不一定非要把这个脚本叫做 _startcompiz_。只要保证你的脚本的名字不会和系统已有的命令（在`/usr/bin`目录中）弄混就行了。

保证你的脚本可执行：

```
# chmod +x /usr/bin/startcompiz

```

现在你需要新建一个程序来调用你刚刚在 `/usr/bin` 中新建的这个脚本了。

1) 只针对你当前的用户设置:

 `~/.kde4/env/startcompiz.sh`  `KDEWM="compiz"` 

2) 全系统范围内设置:

 `/etc/kde/env/startcompiz.sh`  `KDEWM="compiz"` 
**注意:**

*   如果上面的方法不管用，使用下面的命令可以达到同样的目的：

```
$ export KDEWM="startcompiz"

```

	把它放到你用户的 `~/.bashrc` 文件中去。

*   如果你使用了 `/usr/local/bin` 目录那可能会不管用。那么你需要在脚本中使用绝对路径：

```
$ export KDEWM="/usr/local/bin/startcompiz"

```

#### GNOME 桌面环境

##### GNOME Shell 和 Cinnamon

[GNOME Shell (简体中文)](/index.php/GNOME_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME Shell (简体中文)") 是一个类似 [mutter](https://www.archlinux.org/packages/?name=mutter) 的实现插件。 同样， [Cinnamon](/index.php/Cinnamon "Cinnamon") 插件是一个类似于 [muffin](https://www.archlinux.org/packages/?name=muffin) 窗口管理器的实现。

也就是说，将GNOME Shell 或 Cinnamon 与 Compiz 或者其他窗口管理器同时使用**是不可能的**（因为他们都是窗口管理器！）。

##### Unity

确保 'Ubuntu Unity Plugin' （**Ubuntu Unity 插件**）在 CCSM 中启用了，这样 [Unity](/index.php/Unity "Unity") 才能正确运行。

你只有正确安装了Unity之后，这个插件才会显示在CCSM里面。

##### 其它的GNOME会话 (Cairo dock 和 Compiz)

[gnome-session-compiz](https://aur.archlinux.org/packages/gnome-session-compiz/) 包会在一个 [display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)") 中添加一个新的会话。 只要在你的显示管理器中选择 'gnome-session-compiz' 即可。

请确保 Compiz 以及 Cairo Dock (Taskbar或Panel) 已经正确的设置好了。

在CCSM里面，确保选择了窗口装饰器，已经启用了窗口管理需要的必要插件。详见 [Compiz (简体中文)#启用重要的插件](/index.php/Compiz_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.90.AF.E7.94.A8.E9.87.8D.E8.A6.81.E7.9A.84.E6.8F.92.E4.BB.B6 "Compiz (简体中文)").

下面是一些建议的Cairo Dock的设置：

*   在Cairo Dock上面添加一个应用程序菜单，并且记住它的快捷键绑定。
*   为了舒服，吧应用程序菜单的快捷键绑定到 `Alt+F1` 和 `Alt+F2`。
*   添加时钟、Wifi、网速等等插件图标到Dock上面。
*   添加一个注销按钮：
    *   设置注销命令为 `gnome-session-quit --logout`
    *   设置关机命令为 `gnome-session-quit --power-off`
*   添加Notification Area Old (systray) 图标（**通知区域支持**）到 Cairo Dock。

##### GNOME Flashback

详见：[GNOME Flashback#Alternative window manager](/index.php/GNOME_Flashback#Alternative_window_manager "GNOME Flashback").

#### MATE 桌面环境

##### 使用 GSettings

使用下面的 GSettings 命令可以将默认的窗口管理器 [marco](https://www.archlinux.org/packages/?name=marco) 改为 Compiz。

```
$ gsettings set org.mate.session.required-components windowmanager compiz

```

##### 使用 mate-session-properties

**注意:** 当使用这种方法时，Marco会首先启动，然后自动被Compiz替换。

另一种做法是使用mate-session-properties来启用Compiz。 在终端中输入下面的命令：

```
$ mate-session-properties

```

单击“添加”按钮，并在“命令”文本框中输入 `compiz --replace &` 命令。 名称和介绍栏目并不重要，只是用来说明的，不要在意这些细节。 注销再登陆，Compiz应该就会顺利启动了。

#### Xfce

##### 修改默认 (故障保护Failsafe) 会话

想要设置Xfce的默认会话 (也就是故障保护 Failsafe 会话) ，可以使用 `xfconf-query`:

```
 xfconf-query -c xfce4-session -p /sessions/Failsafe/Client0_Command -t string -t string -s compiz

```

或者可以编辑下面其中之一：

*   用户：`~/.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml`
*   系统：`/etc/xdg/xfce4/xfconf/xfce-perchannel-xml/xfce4-session.xml`

**注意:** 如果 xfce4-session.xml 文件不存在于 `~/.config/xfce4/xfconf/xfce-perchannel-xml` ，你需要去编辑 `/etc/xdg/xfce4/xfconf/xfce-perchannel-xml`中的文件。

将 [Xfwm](/index.php/Xfwm "Xfwm") 的启动命令：

```
 <property name="Client0_Command" type="array">
   <value type="string" value="xfwm4"/>
 </property>

```

替换为：

```
 <property name="Client0_Command" type="array">
   <value type="string" value="compiz"/>
 </property>

```

为了保护默认会话不被覆盖，你可能需要使用：

```
 <property name="general" type="empty">
   ...
   ...
   <property name="SaveOnExit" type="bool" value="false"/>
 </property>

```

然后移除已经存在的会话：

```
$ rm -r ~/.cache/sessions

```

现在你应该注销。请确保“保存默认会话”标签**没有被勾选**，否则刚才的编辑不会生效。 再次登陆，Compiz应该就会运行了。当Compiz正常运行之后，你就可以重新钩上“保存将来的会话”了。

##### Starting Compiz from a restored Xfce session

**Note:** If you clear your saved sessions then you will need to run through the steps of this method again.

By default, Xfce saves its sessions on logout which means that running applications will be restored on login. Therefore, to ensure that Compiz is autostarted with each session, you merely need to ensure that Compiz is running when you logout. To do so, hit `Alt+F2` to start the Xfce run dialog. Then run the command to start Compiz: `compiz --replace &`. Then you just need to logout. When logging out, ensure that the "Save session for future logins" option in the Xfce logout dialog is **ticked**. You should find that Compiz is autostarted in all future sessions.

##### Using Xfce application autostart

**Note:** If this method is used, Xfwm will start first and will then be replaced by Compiz.

In the Xfce main menu navigate to 'Settings' and click on 'Session and Startup.' Click on the 'Application Autostart' tab. Click the add button and in the command section enter the `compiz --replace &` command. The name and comment sections are unimportant and are just there to indicate what the entry does. Log out and log in again and Compiz should start.

**Tip:** When using this method, it is advisable to disable saved sessions otherwise Compiz will be started twice at login which could lead to problems such as the `Alt+F4` keybinding not working. To disable saved sessions, open the 'Session and Startup' menu entry, click on the 'Session' tab and click the 'Clear saved sessions' button. Then, untick the 'Save session for future logins' option in the Xfce logout dialog.

#### LXDE & LXQt

The session files of LXDE and LXQt can be edited to start an alternative [window manager](/index.php/Window_manager "Window manager") (such as Compiz) with the session.

*   For LXDE, see the following section: [LXDE#Replace the default window manager](/index.php/LXDE#Replace_the_default_window_manager "LXDE").
*   For LXQt, see the following section: [LXQt#Replace the default window manager](/index.php/LXQt#Replace_the_default_window_manager "LXQt").

## Using Compiz as a standalone window manager

### Starting the session with a display manager

A standalone Compiz session can be started from a [display manager](/index.php/Display_manager "Display manager"). For most display manager's ([LightDM](/index.php/LightDM "LightDM"), [LXDM](/index.php/LXDM "LXDM"), [GDM](/index.php/GDM "GDM") etc) all that's required is to create a .desktop file in `/usr/share/xsessions` defining the Compiz session. See the article for your display manager to check if this is the case.

Firstly, create the `/usr/share/xsessions` directory if it does not already exist. Then create the .desktop file. A basic example is provided below:

 `/usr/share/xsessions/compiz.desktop` 

```
[Desktop Entry]
Version=1.0
Name=Compiz
Comment=Start a standalone Compiz session
Exec=compiz
Type=Application

```

Then just choose 'Compiz' from your sessions list and log in.

**Note:** Some display managers are stricter than others regarding the syntax of .desktop files. If a Compiz option does not appear in your display manager's session menu you will need to edit your .desktop file to make it compatible. The example above should work in most cases.

#### Autostarting programs when using a display manager

One way in which you could start programs with your Compiz session, when it is started from a [display manager](/index.php/Display_manager "Display manager"), is to use an [xprofile](/index.php/Xprofile "Xprofile") file. The xprofile file is similar in syntax to [xinitrc](/index.php/Xinitrc "Xinitrc") - it can contain commands for programs you wish to start with your session. Most display managers will parse commands from an xprofile file by default.

Alternatively, you could use Compiz's 'Session Management' plugin. This plugin will save running programs on exit and restore them when the session is next started. Simply enable the 'Session Management' plugin in CCSM.

### Starting the session with startx

To start Compiz with the `startx` command, add the following line to your `~/.xinitrc` file:

 `~/.xinitrc` 

```
exec compiz

```

You can also use fusion icon as shown below:

 `~/.xinitrc` 

```
exec fusion-icon

```

You can autostart additional programs (such as a panel) by adding the relevant command to your `~/.xinitrc` file. Below is an example of a `~/.xinitrc` file which starts Compiz, the tint2 panel and the Cairo dock.

 `~/.xinitrc` 

```
tint2 &
cairo-dock &
exec compiz

```

See the [xinitrc](/index.php/Xinitrc "Xinitrc") article for more details.

### Add a root menu

To add a root menu similar to that in [Openbox](/index.php/Openbox "Openbox") and other standalone window managers you can install the [compiz-boxmenu](https://aur.archlinux.org/packages/compiz-boxmenu/) package. This program is a fork of [compiz-deskmenu](https://aur.archlinux.org/packages/compiz-deskmenu/). Among the changes that the fork introduces are the addition of some extra features such as a window list and a recent documents list.

After installing the [compiz-boxmenu](https://aur.archlinux.org/packages/compiz-boxmenu/) package, copy the config files to your home directory as shown below:

```
# cp -R /etc/xdg/compiz /home/_username_/.config
# chown -R _username_:_group_ /home/_username_/.config/compiz

```

where `username` is your username and `group` is the primary group for your user.

Then, open CCSM, navigate to the 'Commands' plugin and in 'Command line 0' enter the command `compiz-boxmenu`. In the 'Key Bindings' tab, set 'Run command 0' to `Control+Space` (you can use the 'Grab key combination' option to simplify this process.)

Now navigate to the 'Viewport Switcher' plugin and click on the 'Desktop-based Viewport Switching' tab. Change the 'Plugin for initiate action' to `core` and change 'Action name for initiate' to `run_command0_key`.

You should now find that a menu appears when you click `Control+Space`. To launch a graphical menu editor, click on the 'Edit' option or run `compiz-boxmenu-editor` in a terminal. If you would prefer to edit your menu manually, open the following file in your favourite editor: `~/.config/compiz/boxmenu/menu.xml`. For your changes to take effect, you must click the 'Reload' option in your menu.

**Warning:** Whilst `Control+Space` is the default keybinding for `compiz-boxmenu` you can assign the menu to other keybindings or mousebindings as well. Take extreme care if doing so as Compiz bindings will take precedence over keybindings of all other programs. For instance, if you assign `compiz-boxmenu` to `Button3` then you may lose right click functionality in all programs. If the keybinding/mousebinding you are attempting to create has any conflicts, `cssm` will notify you.

### Allow users to shutdown/reboot

An unprivileged user should be able to execute commands such as `systemctl poweroff` and `systemctl reboot`. You could assign a keyboard shortcut to one of these commands using the 'Commands' plugin in CCSM. Alternatively, you could create a launcher for one of these commands in [compiz-boxmenu](https://aur.archlinux.org/packages/compiz-boxmenu/) - see above. For more detailed information on shutting down see the following article: [Allow users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown").

### Utilities

#### Panels & docks

There are a number of panels and docks available in Arch however only a few are compatible with Compiz's [viewports](/index.php/Compiz_configuration#Workspaces_and_Viewports "Compiz configuration"). They are listed below:

*   [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel)
*   [mate-panel](https://www.archlinux.org/packages/?name=mate-panel)
*   [perlpanel](https://www.archlinux.org/packages/?name=perlpanel)
*   [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)
*   [cairo-dock](https://www.archlinux.org/packages/?name=cairo-dock)

**Note:** Other [panels and docks](/index.php/List_of_applications#Taskbars_.2F_panels_.2F_docks "List of applications") can be run with Compiz however their desktop pagers will show only one virtual desktop and all window buttons will be shown in all viewports regardless of which viewport the window happens to be in.

#### Run dialog

*   [mate-panel](https://www.archlinux.org/packages/?name=mate-panel) provides a run dialog. To enable it, see the following section: [Compiz#MATE Panel](/index.php/Compiz#MATE_Panel "Compiz").
*   [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel) provides a run dialog. To enable it, see the following section: [Compiz#GNOME Panel](/index.php/Compiz#GNOME_Panel "Compiz").
*   [lxpanel](https://www.archlinux.org/packages/?name=lxpanel) provides a run dialog. To enable it, see the following section: [Compiz#LXDE Panel](/index.php/Compiz#LXDE_Panel "Compiz").

**Note:** The panels mentioned above must be running in order to use their respective run dialogs.

Alternatively you could install one of the following:

*   [xfce4-appfinder](https://www.archlinux.org/packages/?name=xfce4-appfinder) - use the following command to launch a run dialog: `xfce4-appfinder --collapsed`
*   [bbrun](https://www.archlinux.org/packages/?name=bbrun) - use the following command to launch a run dialog: `bbrun -w`
*   [gmrun](https://www.archlinux.org/packages/?name=gmrun) - use the following command to launch a run dialog: `gmrun`
*   [fbrun](https://aur.archlinux.org/packages/fbrun/) - use the following command to launch a run dialog: `fbrun`

In each case, simply map the command to `Alt+F2` (or a key combination of your choice) via the 'Commands' plugin in CCSM.

## 小技巧大放送

### 还原原生窗口管理器

你可以用下面的命令把Compiz改回你桌面环境原生的窗口管理器：

```
_wm_name_ --replace

```

使用 `kwin`、 `metacity` 或 `xfwm4` 替换掉 `wm_name`.

### 启用 Alt+F2 运行对话框

#### GNOME Panel

在CCSM中启用 'Gnome Compatibility' 插件。

#### MATE Panel

有两种方法在Compiz中启动 MATE Panel 中的运行对话框，你自己选吧：

*   在CCSM中启用 'Gnome Compatibility' 插件
*   使用“命令”（_Commands_）插件，设置 `Alt+F2` 快捷键的绑定如下：

```
mate-panel --run-dialog

```

#### LXDE Panel

使用“命令”（_Commands_）插件，设置 `Alt+F2` 快捷键的绑定如下：

```
lxpanelctl run

```

#### Xfce 程序查看器（_Appfinder_）

当在Xfce会话中使用Compiz时，运行对话框（由[xfce4-appfinder](https://www.archlinux.org/packages/?name=xfce4-appfinder)提供）无需任何干预应该管用。

但是如果你是在Compiz独立会话中使用程序查看器的话，请查看这一章节：[Compiz#Run dialog](/index.php/Compiz#Run_dialog "Compiz")。

#### 其他的运行对话框功能

请查看这一章节：[Compiz#Run dialog](/index.php/Compiz#Run_dialog "Compiz")。

## 疑难排解

### Missing GLX_EXT_texture_from_pixmaps

#### On ATI cards (first solution)

You may run into the following error when trying to run Compiz on an ATI card:

```
Missing GLX_EXT_texture_from_pixmap

```

This is because Compiz's binary was compiled against Mesa's OpenGL library rather than ATI's OpenGL library.

Firstly, copy the library into a directory to keep it because ATI's drivers will over write it:

```
$ install -Dm644 /usr/lib/libGL.so.1.2 /usr/lib/mesa/libGL.so.1.2

```

Then you can reinstall your fglrx drivers. Now start Compiz as shown below:

```
LD_PRELOAD=/usr/lib/mesa/libGL.so.1.2 compiz --replace &

```

#### On ATI cards (second solution)

Another possible problem with 'GLX_EXT_texture_from_pixmap' on ATI cards is that the card can only render it indirectly. If so, you have to pass the option to your libgl as shown below:

```
LIBGL_ALWAYS_INDIRECT=1 compiz --replace &

```

(Workaround tested on the following card : ATI Technologies Inc Radeon R250 [Mobility FireGL 9000] (rev 02))

#### On Intel chips

Firstly, check that you're using the intel driver as opposed to i810\. Then, run the following command to run Compiz (This must be used every time).

```
LIBGL_ALWAYS_INDIRECT=true compiz --replace --sm-disable &

```

### Compiz starts without window borders with NVIDIA binary drivers

Firstly, ensure that your window decorator settings are configured correctly - see the following: [Compiz#Starting the window decorator](/index.php/Compiz#Starting_the_window_decorator "Compiz"). If window borders still do not start try adding _Option "AddARGBGLXVisuals" "True"_ and _Option "DisableGLXRootClipping" "True"_ to your "Screen" section in `/etc/X11/xorg.conf.d/20-nvidia.conf`. If window borders still do not load and you have used other Options elsewhere in `/etc/X11/xorg.conf.d/` try commenting them out and using only the aformentioned ARGBGLXVisuals and GLXRootClipping Options.

### Blank screen on resume from suspend-to-ram using the NVIDIA binary drivers

If you receive a blank screen with a responsive cursor upon resume, try disabling sync to vblank. To do so, open CCSM, navigate to the 'OpenGL' plugin and untick the 'Sync to VBlank' option.

### Poor performance from capable graphics cards

**NVIDIA and Intel chips**: If everything is configured correctly but you still have poor performance with some effects, try disabling _CCSM > General Options > Display Settings > Detect Refresh Rate_ and instead choose a value manually.

**NVIDIA chips only**: The inadequate refresh rate with 'Detect Refresh Rate' may be due to an option called 'DynamicTwinView' being enabled by default which plays a factor in accurately reporting the maximum refresh rate that your card and display support. You can disable 'DynamicTwinView' by adding the following line to the "Device" or "Screen" section of your `/etc/X11/xorg.conf.d/20-nvidia.conf`, and then restarting your computer:

```
Option "DynamicTwinView" "False"

```

### Screen flicks with NVIDIA card

To fix this behaviour create the file below:

 `/etc/modprobe.d/nvidia.conf`  `options nvidia NVreg_RegistryDwords="PerfLevelSrc=0x2222"` 

### Compiz effects not working (GConf backend)

If you have installed the gtk-window-decorator, check if the GConf schema was correctly installed:

```
$ gconftool-2 -R /apps/compiz/plugins | grep plugins

```

Make sure that all plugins are listed. If they are not, try to install the Compiz schema manually (do **not** run this command as root):

```
$ gconftool-2 --install-schema-file=/usr/share/gconf/schemas/compiz-decorator-gtk.schemas

```

### Fusion Icon fails to start

If you get an output like this from the command line:

 `$ fusion-icon` 

```
* Detected Session: gnome
* Searching for installed applications...
Traceback (most recent call last):
  File "/usr/bin/fusion-icon", line 57, in <module>
    from FusionIcon.interface import choose_interface
  File "/usr/lib/python2.5/site-packages/FusionIcon/interface.py", line 23, in <module>
    import start
  File "/usr/lib/python2.5/site-packages/FusionIcon/start.py", line 36, in <module>
    config.check()
  File "/usr/lib/python2.5/site-packages/FusionIcon/util.py", line 362, in check
    os.makedirs(self.config_folder)
  File "/usr/lib/python2.5/os.py", line 172, in makedirs
    mkdir(name, mode)
OSError: [Errno 13] Permission denied: '/home/andy/.config/compiz'

```

the problem is with the permission on `~/.config/compiz/`. To fix it, use:

```
# chown -R _username_ /home/_username_/.config/compiz/

```

### Alt+F4 keybinding not working (Xfce)

See the following section: [Compiz#Using Xfce application autostart](/index.php/Compiz#Using_Xfce_application_autostart "Compiz").

### Emerald refuses to start (crashes with a segfault)

You may find that Emerald fails to start with your Compiz session and attempting to start it from a terminal gives you the following output (or something similar):

```
Segmentation fault (core dumped)

```

In this case, the solution is to reset the Emerald theme settings:

```
$ rm -rf ~/.emerald/theme

```

Emerald should now start successfully.

### No system bell when Compiz is running

You may find that the system bell (such as the drip sound played when pressing backspace at the beginning of a line in GNOME or MATE Terminal) will not sound if Compiz is running. See the following [upstream bug report](https://bugs.launchpad.net/ubuntu/+source/compiz/+bug/537703).

For [Pulseaudio](/index.php/Pulseaudio "Pulseaudio") users the following workaround is available:

Append the following lines

```
load-sample-lazy bell /usr/share/sounds/freedesktop/stereo/bell.oga
load-module module-x11-bell sample=bell

```

to your `/etc/pulse/default.pa` file and then restart Pulseaudio.

### Compiz crashes when enabling the Gnome Compatibility plugin (GSettings backend)

If you are using the GSettings backend, you may find that Compiz crashes if you try to enable the 'Gnome Compatibility' plugin. In order to enable this plugin whilst using the GSettings backend you need to open CCSM and navigate to 'Preferences.' Under the header 'Integration' untick the box labelled 'Enable integration into the desktop environment.' After unticking this option, you should find it possible to enable the 'Gnome Compatibility' plugin.

## Known issues

### Xfce panel window buttons are not refreshed when a window changes viewport

You may find that if you right click on a window title and choose an option such as 'Move to Workspace Right' then the window will move but the window button will still be visible in the viewport the window moved from until you switch viewports. See the following [upstream bug report](https://bugzilla.xfce.org/show_bug.cgi?id=10908).

### Compiz crashes when enabling the D-Bus plugin

The D-Bus plugin will cause Compiz to crash if enabled in conjunction with certain other plugins such as the Cube plugin. See the following [upstream bug report](https://bugs.launchpad.net/compiz/+bug/959395).

## See also

*   [Compiz in Launchpad](https://launchpad.net/compiz)
*   [Compiz Home](http://compiz.org), including wiki and forum (website and wiki are unmaintained)
*   [Troubleshooting - Compiz Wiki](http://wiki.compiz.org/Troubleshooting), (wiki is unmaintained)