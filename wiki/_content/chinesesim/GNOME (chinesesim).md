**翻译状态：** 本文是英文页面 [GNOME](/index.php/GNOME "GNOME") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-10-05，点击[这里](https://wiki.archlinux.org/index.php?title=GNOME&diff=0&oldid=400254)可以查看翻译后英文页面的改动。

GNOME (pronounced *gah-nohm* or *nohm*)是一个简单易用的[桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)") .它由[The GNOME Project](https://en.wikipedia.org/wiki/The_GNOME_Project "wikipedia:The GNOME Project") 设计并且完全自由和开源. GNOME是[GNU Project](https://en.wikipedia.org/wiki/GNU_Project "wikipedia:GNU Project")的一部分.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 附加的软件包](#.E9.99.84.E5.8A.A0.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [2 GNOME会话](#GNOME.E4.BC.9A.E8.AF.9D)
*   [3 运行 GNOME](#.E8.BF.90.E8.A1.8C_GNOME)
    *   [3.1 图形界面登录](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E7.99.BB.E5.BD.95)
    *   [3.2 手动启动](#.E6.89.8B.E5.8A.A8.E5.90.AF.E5.8A.A8)
    *   [3.3 Wayland 中的 GNOME 应用程序](#Wayland_.E4.B8.AD.E7.9A.84_GNOME_.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
*   [4 导览](#.E5.AF.BC.E8.A7.88)
    *   [4.1 重启 GNOME shell](#.E9.87.8D.E5.90.AF_GNOME_shell)
    *   [4.2 GNOME Shell 崩溃](#GNOME_Shell_.E5.B4.A9.E6.BA.83)
    *   [4.3 遗留名称](#.E9.81.97.E7.95.99.E5.90.8D.E7.A7.B0)
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
*   [6 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [6.1 键盘](#.E9.94.AE.E7.9B.98)
        *   [6.1.1 登陆打开NumLock键](#.E7.99.BB.E9.99.86.E6.89.93.E5.BC.80NumLock.E9.94.AE)
        *   [6.1.2 热键选择](#.E7.83.AD.E9.94.AE.E9.80.89.E6.8B.A9)
        *   [6.1.3 打开键盘开关命令](#.E6.89.93.E5.BC.80.E9.94.AE.E7.9B.98.E5.BC.80.E5.85.B3.E5.91.BD.E4.BB.A4)
        *   [6.1.4 XkbOptions键盘选项](#XkbOptions.E9.94.AE.E7.9B.98.E9.80.89.E9.A1.B9)
        *   [6.1.5 De-bind Windows key](#De-bind_Windows_key)
    *   [6.2 磁盘](#.E7.A3.81.E7.9B.98)
    *   [6.3 从菜单隐藏的应用程序](#.E4.BB.8E.E8.8F.9C.E5.8D.95.E9.9A.90.E8.97.8F.E7.9A.84.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [6.4 截屏记录](#.E6.88.AA.E5.B1.8F.E8.AE.B0.E5.BD.95)
    *   [6.5 截图](#.E6.88.AA.E5.9B.BE)
    *   [6.6 注销延迟](#.E6.B3.A8.E9.94.80.E5.BB.B6.E8.BF.9F)
    *   [6.7 禁用动画](#.E7.A6.81.E7.94.A8.E5.8A.A8.E7.94.BB)
    *   [6.8 Retina (HiDPI) display support](#Retina_.28HiDPI.29_display_support)
    *   [6.9 密码和密钥 (PGP Keys)](#.E5.AF.86.E7.A0.81.E5.92.8C.E5.AF.86.E9.92.A5_.28PGP_Keys.29)
    *   [6.10 终端](#.E7.BB.88.E7.AB.AF)
        *   [6.10.1 更改默认的终端大小](#.E6.9B.B4.E6.94.B9.E9.BB.98.E8.AE.A4.E7.9A.84.E7.BB.88.E7.AB.AF.E5.A4.A7.E5.B0.8F)
        *   [6.10.2 新终端采用当前目录](#.E6.96.B0.E7.BB.88.E7.AB.AF.E9.87.87.E7.94.A8.E5.BD.93.E5.89.8D.E7.9B.AE.E5.BD.95)
        *   [6.10.3 Pad the terminal](#Pad_the_terminal)
        *   [6.10.4 禁用光标闪烁](#.E7.A6.81.E7.94.A8.E5.85.89.E6.A0.87.E9.97.AA.E7.83.81)
        *   [6.10.5 关闭终端时，禁用确认窗口](#.E5.85.B3.E9.97.AD.E7.BB.88.E7.AB.AF.E6.97.B6.EF.BC.8C.E7.A6.81.E7.94.A8.E7.A1.AE.E8.AE.A4.E7.AA.97.E5.8F.A3)
    *   [6.11 鼠标中键](#.E9.BC.A0.E6.A0.87.E4.B8.AD.E9.94.AE)
    *   [6.12 启用按钮和菜单图标](#.E5.90.AF.E7.94.A8.E6.8C.89.E9.92.AE.E5.92.8C.E8.8F.9C.E5.8D.95.E5.9B.BE.E6.A0.87)
    *   [6.13 使用自定义的色彩和渐变色的桌面背景](#.E4.BD.BF.E7.94.A8.E8.87.AA.E5.AE.9A.E4.B9.89.E7.9A.84.E8.89.B2.E5.BD.A9.E5.92.8C.E6.B8.90.E5.8F.98.E8.89.B2.E7.9A.84.E6.A1.8C.E9.9D.A2.E8.83.8C.E6.99.AF)
    *   [6.14 渐变背景](#.E6.B8.90.E5.8F.98.E8.83.8C.E6.99.AF)
    *   [6.15 自定义 GNOME 会话](#.E8.87.AA.E5.AE.9A.E4.B9.89_GNOME_.E4.BC.9A.E8.AF.9D)
*   [7 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [7.1 Gnome Shell 界面卡死](#Gnome_Shell_.E7.95.8C.E9.9D.A2.E5.8D.A1.E6.AD.BB)
    *   [7.2 Incorrect application defaults](#Incorrect_application_defaults)
    *   [7.3 Tracker & Documents do not list any local files](#Tracker_.26_Documents_do_not_list_any_local_files)
    *   [7.4 Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts)
    *   [7.5 Cannot change settings in dconf-editor](#Cannot_change_settings_in_dconf-editor)
    *   [7.6 When an extension breaks the shell](#When_an_extension_breaks_the_shell)
    *   [7.7 扩展在 GNOME 3 升级后不工作了](#.E6.89.A9.E5.B1.95.E5.9C.A8_GNOME_3_.E5.8D.87.E7.BA.A7.E5.90.8E.E4.B8.8D.E5.B7.A5.E4.BD.9C.E4.BA.86)
    *   [7.8 只有 conky 运行时键盘快捷方式不工作](#.E5.8F.AA.E6.9C.89_conky_.E8.BF.90.E8.A1.8C.E6.97.B6.E9.94.AE.E7.9B.98.E5.BF.AB.E6.8D.B7.E6.96.B9.E5.BC.8F.E4.B8.8D.E5.B7.A5.E4.BD.9C)
    *   [7.9 Unable to apply stored configuration for monitors](#Unable_to_apply_stored_configuration_for_monitors)
    *   [7.10 一致的光标主题](#.E4.B8.80.E8.87.B4.E7.9A.84.E5.85.89.E6.A0.87.E4.B8.BB.E9.A2.98)
    *   [7.11 Windows cannot be modified with Alt-Key + mouse-button](#Windows_cannot_be_modified_with_Alt-Key_.2B_mouse-button)
    *   [7.12 加载速度慢的系统图标/慢GDM登录](#.E5.8A.A0.E8.BD.BD.E9.80.9F.E5.BA.A6.E6.85.A2.E7.9A.84.E7.B3.BB.E7.BB.9F.E5.9B.BE.E6.A0.87.2F.E6.85.A2GDM.E7.99.BB.E5.BD.95)
    *   [7.13 Artifacts when maximizing windows](#Artifacts_when_maximizing_windows)
    *   [7.14 Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics)
    *   [7.15 Window opens behind other windows when using multiple monitors](#Window_opens_behind_other_windows_when_using_multiple_monitors)
    *   [7.16 锁定按钮无法重新启用触摸板](#.E9.94.81.E5.AE.9A.E6.8C.89.E9.92.AE.E6.97.A0.E6.B3.95.E9.87.8D.E6.96.B0.E5.90.AF.E7.94.A8.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [7.17 GNOME Shell键盘源菜单不可见](#GNOME_Shell.E9.94.AE.E7.9B.98.E6.BA.90.E8.8F.9C.E5.8D.95.E4.B8.8D.E5.8F.AF.E8.A7.81)
    *   [7.18 鼠标指针丢失](#.E9.BC.A0.E6.A0.87.E6.8C.87.E9.92.88.E4.B8.A2.E5.A4.B1)
    *   [7.19 在会话菜单中没有重启按钮时，屏幕被锁定](#.E5.9C.A8.E4.BC.9A.E8.AF.9D.E8.8F.9C.E5.8D.95.E4.B8.AD.E6.B2.A1.E6.9C.89.E9.87.8D.E5.90.AF.E6.8C.89.E9.92.AE.E6.97.B6.EF.BC.8C.E5.B1.8F.E5.B9.95.E8.A2.AB.E9.94.81.E5.AE.9A)
    *   [7.20 pulseaudio系统原因延误GNOME和GDM](#pulseaudio.E7.B3.BB.E7.BB.9F.E5.8E.9F.E5.9B.A0.E5.BB.B6.E8.AF.AFGNOME.E5.92.8CGDM)
    *   [7.21 GNOME crashes when trying to reorder applications in the GNOME Shell Dash](#GNOME_crashes_when_trying_to_reorder_applications_in_the_GNOME_Shell_Dash)
*   [8 参见](#.E5.8F.82.E8.A7.81)

## 安装

以下两个软件包（组）均包含 GNOME 的组件：

**gnome** 包组包含基本桌面环境和软件，以提供标准的 GNOME 体验。

**gnome-extra** 包组包含剩余的可选工具，例如文本编辑器、压缩文件管理器、光盘烧录工具、邮件客户端、游戏、开发工具及其它非必需的软件。这些软件与 GNOME 桌面的集成很好。假如您不想安装 GNOME 全部的软件包，在安装它的时候注意看软件包描述（或者你可以先安装再删除他们）。

**Note:** *mutter* acts as a composite manager for the desktop, employing hardware graphics acceleration to provide effects aimed at reducing screen clutter. The GNOME session manager automatically detects if your video driver is capable of running GNOME Shell and if not, falls back to software rendering using *llvmpipe*.

### 附加的软件包

上面提到的包组不包括这些包：

*   **[Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — A simple user interface to access [libvirt](/index.php/Libvirt "Libvirt") virtual machines.

	[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **GNOME Initial Setup** — A simple, easy, and safe way to prepare a new system.

	[https://github.com/GNOME/gnome-initial-setup](https://github.com/GNOME/gnome-initial-setup) || [gnome-initial-setup](https://www.archlinux.org/packages/?name=gnome-initial-setup)

*   **GNOME PackageKit** — Collection of graphical tools for PackageKit to be used in the GNOME desktop.

	[https://github.com/GNOME/gnome-packagekit](https://github.com/GNOME/gnome-packagekit) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **[Nemiver](https://en.wikipedia.org/wiki/Nemiver "wikipedia:Nemiver")** — A C/C++ debugger.

	[https://wiki.gnome.org/Apps/Nemiver](https://wiki.gnome.org/Apps/Nemiver) || [nemiver](https://www.archlinux.org/packages/?name=nemiver)

*   **[Software](https://en.wikipedia.org/wiki/GNOME_Software "wikipedia:GNOME Software")** — Lets you install and update applications and system extensions.

	[https://wiki.gnome.org/Apps/Software/](https://wiki.gnome.org/Apps/Software/) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

## GNOME会话

GNOME 有三个可用的会话，都使用 GNOME Shell

*   **GNOME** 是默认会话, 有创新的布局
*   **GNOME Classic** 的桌面布局类似于传统的GNOME 2, using pre-activated extensions and parameters. [[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) Hence it is more a customized GNOME Shell than a truly distinct mode
*   **GNOME on Wayland** GNOME Shell 在新的Wayland协议上运行. 而传统的 X 应用程序在Xwayland上运行

## 运行 GNOME

GNOME可以通过 [显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")以图形方式启动,或者从控制台手动启动。 为优化桌面整合, 建议使用[GDM (简体中文)](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)") (GNOME显示管理器)。 注意 [启用](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") 一个显示管理器(例如GDM)意味着Xorg将会以root权限运行.

**注意:** 如果不使用 GDM，你将无法体验到对锁屏的原生支持，因此你不得不使用另一个屏幕锁来提供类似功能，参见[Xmonad (简体中文)#GNOME 3 and xmonad](/index.php/Xmonad_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#GNOME_3_and_xmonad "Xmonad (简体中文)").

### 图形界面登录

可以在登录管理器中选择 *GNOME',* GNOME Classic *或* GNOME on Wayland *作为登录选项。*

### 手动启动

*   对于标准的GNOME会话， 在`~/.xinitrc` 中添加：`exec gnome-session`.
*   对于经典的gnome会话，在 `~/.xinitrc` 中添加：{bc|export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME export GNOME_SHELL_SESSION_MODE=classic exec gnome-session --session=gnome-classic}}

**注意:** 最好把gnome--session之前的应用注释掉，我之前因为没有注释掉`twm`（另一个窗口管理器）导致启动gnome失败

我现在的`/etc/X11/xinit/xinitrc`如下：

```
#twm &
#xclock -geometry 50x50-1+1 &
#xterm -geometry 80x50+494+51 &
#xterm -geometry 80x20+494-0 &
#exec xterm -geometry 80x66+0+0 -name login
exec gnome-session
```

改完`~/.xinitrc` ，即可用`startx` 启动Gnome (see [xinitrc](/index.php/Xinitrc "Xinitrc") for additional details, such as preserving the logind session). After setting up the `~/.xinitrc` file it can also be arranged to [Start X at login](/index.php/Start_X_at_login "Start X at login").

**Note:** Wayland 上的Gnome需要r [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) 包， 不能使用 *startx* 和`~/.xinitrc`，而是要运行 `gnome-session --session=gnome-wayland`. 更多参见 [Wayland](/index.php/Wayland "Wayland").

### Wayland 中的 GNOME 应用程序

根据当前的默认情况，GNOME 应用程序会利用 XWayland，以传统 X 应用程序的方式运行。若需在 Wayland 下测试 GNOME 应用，请以命令行方式运行程序，并加上以下前缀： `env GDK_BACKEND=wayland <command>`。

**Note:** 可以设置全局的 Wayland 环境，使用 `env GDK_BACKEND=wayland gnome-session --session=gnome-wayland`。 但是现在无法工作—— *gnome-session* 会立即闪退.

请查看以下页面以了解开发进展： [GNOME Applications under Wayland](https://wiki.gnome.org/Initiatives/Wayland/Applications/).

## 导览

您可以阅读这篇文章： [GNOME Shell cheat sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet) 以了解如何高效地使用 GNOME shell，它展示了 GNOME shell 的特色与使用快捷键。文章内容包括怎么切换任务，使用键盘，窗口控制，使用面板，预览模式等。 部分常用的快捷键：

*   `Super`： 进入预览模式
*   `Super` + `m`： 显示消息托盘
*   `Super` + `a`：显示应用程序菜单
*   `Alt` + `F2`：输入命令以快速启动应用
*   `Alt` + `F2`，然后输入 `r` 或 `restart`，再 `Enter`：重启 GNOME shell。这一条在你遇到 shell 图形界面错误时十分有用。

### 重启 GNOME shell

当修改过界面之后你可能需要重启 GNOME shell。你可以重新登陆，不过有一个简单快捷的方法。 按 `Alt` + `F2` 再输入 `r` 再 `Enter`

### GNOME Shell 崩溃

一些特定的微调或者经常性重启 Shell 会导致 shell 在将要重启的时候崩溃。这个时候你必须做好心理准备，然后强制注销。有一些修改，例如在***GNOME Shell*** 和 ***fallback mode,*** 之间切换，不能简单地使用 r 重启；必须重登陆来应用这个效果。

丑话说在前面，在重启 shell 前请先把有用的文档保存（或者关闭）。虽然这不是必要的，因为窗口和文档在重启了 shell 之后应该还在。

### 遗留名称

**注意:** 一些GNOME程序在文档和关于对话框的名称已更改，但可执行文件的名称却没有。这样的应用程序在下面表格列出.

**提示:** 在搜索栏中搜索的应用程序的遗留名称将成功返回现在的应用程序，例如搜索*nautilus*将返回*Files*.

| Current | Legacy |
| [Files](/index.php/Files "Files") | Nautilus |
| [Web](/index.php/GNOME_Web "GNOME Web") | Epiphany |
| Videos | Totem |
| Main Menu | Alacarte |
| Document Viewer | Evince |
| Disk Usage Analyser | Baobab |
| Image Viewer | EoG (Eye of GNOME) |
| [Passwords and Keys](/index.php/GNOME_Keyring "GNOME Keyring") | Seahorse |

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

如果系统已有配置好的 [NTP 守护进程](https://wiki.archlinux.org/index.php/Network_Time_Protocol_daemon_(简体中文))，它同样会对 GNOME 桌面环境起作用。如果需要，您也可以手动控制进行同步。

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

#### 网络

[NetworkManager](/index.php/NetworkManager "NetworkManager") is the native tool of the GNOME project to control network settings from the shell. It is installed by default as a dependency for [tracker](https://www.archlinux.org/packages/?name=tracker) package, which is a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group, and just needs to be [enabled](/index.php/NetworkManager#Enable_NetworkManager "NetworkManager").

While any other [network manager](/index.php/List_of_applications/Internet#Network_managers "List of applications/Internet") can be used as well, NetworkManager provides the full integration via the shell network settings and a status indicator applet [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (not required for GNOME).

#### 在线帐户

Backends for the GNOME messaging application [empathy](https://www.archlinux.org/packages/?name=empathy) as well as the GNOME Online Accounts section of the System Settings panel are provided in a separate group: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). See [#Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts). Some online accounts, such as [ownCloud](/index.php/OwnCloud "OwnCloud"), require [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) to be installed for full functionality in GNOME applications such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") and GNOME Documents [[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### 搜索

The GNOME shell has a search that can be quickly accessed by pressing the `Super` key and starting to type. The [tracker](https://www.archlinux.org/packages/?name=tracker) package is installed by default as a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group and provides an indexing application and metadata database. It can be configured with the *Search and Indexing* menu item; monitor status with *tracker-control*. It is started automatically by *gnome-session* when the user logs in. Indexing can be started manually with `tracker-control -s`. Search settings can also be configured in the *System Settings* panel.

The Tracker database can be queried using the *tracker-sparql* command. View its manual page `man tracker-sparql` for more information.

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

**注意:** 在GNOME 3.16中，Mutter不再使用metacity主题。相反，标题栏的装饰主题使用GTK+。

改变标题栏的高度，创建以下文件，调整填充所需：

 `~/.config/gtk-3.0/gtk.css` 
```
.header-bar.default-decoration {
    padding-top: 3px;
    padding-bottom: 3px;
}

.header-bar.default-decoration .button.titlebutton {
    padding-top: 2px;
    padding-bottom: 2px;
}

```

标题栏的高度也可以通过选择一个较小的字体。默认情况下，字体设置为Cantarell Bold 11。您可能希望将字体设置为较小的，例如Sans Bold 10\. 你可以这样使用以下GSettings命令来完成：

```
$ gsettings set org.gnome.desktop.wm.preferences titlebar-font 'Sans Bold 10'

```

###### 标题栏按钮重新排序

设置 GNOME 窗口管理器顺序 (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**提示:** 冒号表示窗口标题栏的按钮会出现在哪一方

###### 最大化时隐藏标题栏

*   [Install](/index.php/Install "Install") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). It changes a default setting in the window manager, so as to automatically hide the titlebar on legacy (non-headerbar) apps when they are maximized or tiled to the side.

*   [Install](/index.php/Install "Install") [maximus](https://aur.archlinux.org/packages/maximus/). To start the application, execute *maximus* from a terminal. When running, the daemon will automatically maximize windows. It will undecorate maximized windows and redecorate them when they are unmaximized. If you do not want all windows to start maximized, run `maximus -m` instead. Note that this will only work with windows decorated by the window manager; applications that use client-side decoration such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") will not be undecorated when maximized.

##### GNOME Shell主题

The theme of GNOME Shell itself is configurable. To use a Shell theme, firstly ensure that you have the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package installed. Then enable the *User Themes* extension, either through GNOME Tweak Tool or through the [GNOME Shell Extensions](https://extensions.gnome.org) webpage. Shell themes can then be loaded and selected using the GNOME Tweak Tool.

There are a number of GNOME Shell themes available [in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d).

Shell themes can also be downloaded from [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=191).

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

**注意:** 通过 The GNOME Shell browser plugin（即 [extensions.gnome.org](https://extensions.gnome.org)）安装扩展的方法暂时无法在 Chrome/Chromium 35 或更高的版本上进行。用户应当采用其它对网页安装更兼容的浏览器进行安装，如 [Firefox (简体中文)](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)") 或 [GNOME/Web](/index.php/GNOME/Web "GNOME/Web")。

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

要启动登录某些应用程序, copy the relevant `.desktop` file from `/usr/share/applications/` to `~/.config/autostart/`. 可以使用Tweak Tool.来达到同样的效果。

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

GNOME TWEAK Tool 自 3.17.1 开始，可以**阻止** *systemd* 在“合上盖子”这一 ACPI 事件发生后采取默认行动。[[3]](http://ftp.gnome.org/pub/GNOME/sources/gnome-tweak-tool/3.17/gnome-tweak-tool-3.17.1.news) 若想要**阻止** *systemd* 的默认行为，打开 Tweak Tool，在“电源”标签页下选择“合上盖子后不待机”的选项。此选项意味着在盖子合上后，系统将不会默认待机，而是不采取任何措施。如果选择了此选项，一个自启动项目`~/.config/autostart/ignore-lid-switch-tweak.desktop`将会被创建，用于阻止*systemd*的默认行为。

如果你在合上盖子后既不希望系统待机，也不希望系统不动于衷，你首先要确保你并没有打开上述的选项，然后再配置*systemd*的`HandleLidSwitch=*默认行为*`选项，详见[Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management")中的说明。

##### 修改电池电量严重不足时的行为

系统设置面板只允许用户在电量不足时，要么“待机”要么“休眠”。如果要选择其他的行为，比如“不采取任何措施”，打开`dconf-editor`，转到`org.gnome.settings-daemon.plugins.power`中，并编辑`"critical-battery-action"`，将其值设置为`"nothing"`。

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

## 提示与技巧

其他GNOME系统设置和提示。

### 键盘

#### 登陆打开NumLock键

运行以下命令：

```
$ gsettings set org.gnome.settings-daemon.peripherals.keyboard numlock-state on

```

#### 热键选择

很多的快捷键可以通过系统设置菜单中更改. 例如，重新启用“显示桌面快捷键：

*System settings* > *Keyboard* > *Shortcuts* > *Navigation* > *Hide all normal windows*

However, certain hotkeys cannot be changed directly via system settings. In order to change these keys, use *dconf-editor*. An example of particular note is the hotkey `Alt-` + ``` (the key above `Tab` on US keyboard layouts). In GNOME Shell it is pre-configured to cycle through windows of an application, however it is also a hotkey often used in the [Emacs](/index.php/Emacs "Emacs") editor. It can be changed by opening *dconf-editor* and modifying the *switch-group* key found in `org.gnome.desktop.wm.keybindings`.

It is possible to manually change the keys via an application's so-called **accel** map file. Where it is to be found is up to the application: For instance, Thunar's is at `~/.config/Thunar/accels.scm`, whereas Files's is located at `~/.config/nautilus/accels` and `~/.gnome2/accels/nautilus` on old release.

The file should contain a list of possible hotkeys, each unchanged line commented out with a leading ";" that has to be removed for a change to become active. For example to replace the hotkey used by Files to move files to the trash folder, change the line:

```
; (gtk_accel_path "<Actions>/DirViewActions/Trash" "<Primary>Delete")

```

to this:

```
(gtk_accel_path "<Actions>/DirViewActions/Trash" "Delete")

```

The file is regenerated regularly so do not comment the file. The uncommented line will stay but every comment you add will be lost.

#### 打开键盘开关命令

To have keyboard shortcut **Alt** + **Shift** switch keyboards:

Open Gnome-Tweak-Tool (or Keyboard Settings, in GNOME 3.16) and set *Typing* > *Modifiers-only input sources* > *select Alt-shift*. For more information see also the forum [thread](https://bbs.archlinux.org/viewtopic.php?id=152127).

#### XkbOptions键盘选项

Using the **dconf-editor**, navigate to the key named `org.gnome.desktop.input-sources.xkb-options` and add desired XkbOptions (e.g. *caps:swapescape*) to the list.

See `/usr/share/X11/xkb/rules/xorg` for all XkbOptions and `/usr/share/X11/xkb/symbols/*` for the respective descriptions.

**Note:** To enable the `Ctrl+Alt+Backspace` combination to terminate Xorg, use the [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool). Within the **Tweak Tool**, navigate to *Typing > Key sequence to kill the X server* and select the option `Ctrl+Alt+Backspace` from the dropdown menu.

#### De-bind Windows key

默认情况下，“Windows键”将打开GNOMEshelly预览模式。 You can unbind this key by running the command below

```
$ gsettings set org.gnome.mutter overlay-key 'Foo'

```

### 磁盘

GNOME提供磁盘实用程序来操作的存储驱动器设置。这是它的一些特点：

*   **Enable write cache** is a feature that most hard drives provide. Data is cached and allocated at chosen times to improve system performance. Not recommended unless the computer has a backup battery pack or is a laptop as data would be lost on power failure.

	*Settings* > *Drive Settings* > *Write Cache* > **On**

*   **Automatic Mount Options** can mount drives and partitions that are GPT based - will use default, recommended options.

**Warning:** This setting erases related [fstab](/index.php/Fstab "Fstab") entries

	*Partition Settings* > *Edit Mount Options* > *Automatic Mount Options* > **On**

### 从菜单隐藏的应用程序

**Tip:** Desktop entries can be hidden by editing the `.desktop` files themselves. See [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries").

Use the *Main Menu* application (provided by the [alacarte](https://www.archlinux.org/packages/?name=alacarte) package) to hide any applications you do not wish to show in the menu.

### 截屏记录

GNOME features built-in screencast recording with the **Ctrl** + **Shift** + **Alt** + **R** key combination. A red circle is displayed in the bottom right corner of the screen when the recording is in progress. After the recording is finished, a file named `Screencast from %d%u-%c.webm` is saved in the Videos directory. In order to use the screencast feature the gst plugins need to be installed.

### 截图

默认保存目录:

```
$ gsettings set org.gnome.gnome-screenshot auto-save-directory file:///home/*USER*/Desktop

```

Check the *gnome-screenshot* manual page for more options.

### 注销延迟

去掉注销的确认和 60 秒的延迟： 这个对话框一般出现在你用状态菜单注销的时候。这个修改对于 关机 也生效。这个不是全局修改，只对使用该命令的用户生效。使用该命令立即生效。

```
$ gsettings set org.gnome.SessionManager logout-prompt false

```

### 禁用动画

To disable Shell animations (such as "Show Applications" and the wave animation in the top left activities hot corner), run:

```
$ gsettings set org.gnome.desktop.interface enable-animations false

```

### Retina (HiDPI) display support

GNOME introduced HiDPI support in version 3.10\. If your display does not provide the correct screen size through EDID, this can lead to incorrectly scaled UI elements. As a workaround you can open *dconf-editor* and find the key `scaling-factor` in `org.gnome.desktop.interface`. Set it to `1` to get the standard scale.

Also see [HiDPI](/index.php/HiDPI "HiDPI").

### 密码和密钥 (PGP Keys)

You can use the Passwords and Keys program (*seahorse*) to create a PGP key as it is a front end for [GnuPG](/index.php/GnuPG "GnuPG") and installs it as dependency. This may be useful in the future (for instance if to encrypt a file). Create a key as shown below (the process may take about 10 minutes):

*File* > *New* > *PGP Key* > *Name* > *Email* > *Defaults* > *Passphrase*.

### 终端

#### 更改默认的终端大小

新终端的默认大小可以在*编辑 > 配置文件首选项* 中调整

#### 新终端采用当前目录

By default new terminals open in the `$HOME` directory. To have new terminals adopt the current working directory: `source /etc/profile.d/vte.sh`. Add the command to the shell configuration to retain the behaviour.

#### Pad the terminal

To pad the terminal (create a small, invisible border between the window edges and the terminal contents) create the file below:

 `~/.config/gtk-3.0/gtk.css` 
```
VteTerminal,
TerminalScreen {
    padding: 10px 10px 10px 10px;
    -VteTerminal-inner-border: 10px 10px 10px 10px;
}
```

#### 禁用光标闪烁

Since GNOME 3.8 and the migration to GSettings and DConf the key required to modify in order to disable the blinking cursor in the Terminal differs slightly in contrast to the old GConf key. To disable the blinking cursor in GNOME 3.8 and above use:

```
$ gsettings set org.gnome.desktop.interface cursor-blink false

```

To disable the blinking cursor in Terminal only use (make sure profile uid is correct one):

```
$ dconf write /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/cursor-blink-mode "'off'"

```

Note that `gnome-settings-daemon`, from the package of the same name, must be running for this and other settings changes to take effect in GNOME applications - see [GNOME#Configuration](/index.php/GNOME#Configuration "GNOME").

#### 关闭终端时，禁用确认窗口

试图关闭该窗口，而一个以root身份登录时，终端将始终显示一个确认窗口。为了避免这种情况，执行以下命令：

```
$ gsettings set org.gnome.Terminal.Legacy.Settings confirm-close false

```

### 鼠标中键

By default, GNOME 3 disables middle mouse button emulation regardless of [Xorg](/index.php/Xorg "Xorg") settings (**Emulate3Buttons**). To enable middle mouse button emulation use:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### 启用按钮和菜单图标

Since GTK+ 3.10, the GSettings key 'menus-have-icons' has been deprecated. Icons in buttons and menus can still be enabled by setting the following overrides:

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

### 使用自定义的色彩和渐变色的桌面背景

使用自定义颜色和渐变为您的桌面背景，您首先需要设置一个透明的图片或其他不存在的图片作为您的桌面背景。例如，下面的命令将设置一个不存在的图片为背景。

```
$ gsettings set org.gnome.desktop.background picture-uri none

```

在这一点上，桌面背景应该是一个平坦的颜色-默认的颜色设置为深蓝色。

对于不同的平面彩色你只需要改变的主要颜色设置：

```
$ gsettings set org.gnome.desktop.background primary-color <my color>

```

where <my color> is a hex value (such as *ffffff* for white).

对于颜色渐变，你也需要改变次要颜色设置 `org.gnome.desktop.background secondary-color` 并选择一个阴影类型。举例来说，如果你想有一个horizontal gradient，执行以下命令：

```
$ gsettings set org.gnome.desktop.background color-shading-type horizontal

```

如果你是使用一个透明的图片作为你的背景，你可以通过执行以下设置的透明度：

```
$ gsettings set org.gnome.desktop.background picture-opacity <value>

```

数值在100和1之间（最大不透明度为100）。

### 渐变背景

GNOME 可以在特定的时间间隔之间的使用不同的壁纸。 这是通过创建一个XML文件，指定要使用的图片和时间间隔完成的。有关创建这些文件的详细信息，请参阅下面的 [article](http://www.linuxjournal.com/content/create-custom-transitioning-background-your-gnome-228-desktop).

可替代地，一些工具可用自动化过程：

*   **mkwlppr** — This script creates XML files that can act as dynamic wallpapers for GNOME by referring to multiple wallpapers.

	[http://pastebin.com/019G2rCy](http://pastebin.com/019G2rCy) || see [mkwlppr](http://pastebin.com/019G2rCy)

*   **[Wallpapoz](/index.php/Wallpapoz "Wallpapoz")** — Wallpapoz is a tool that provides dynamic wallpapers for GNOME and Xfce desktops.

	[https://vajrasky.wordpress.com/](https://vajrasky.wordpress.com/) || [wallpapoz](https://aur.archlinux.org/packages/wallpapoz/)

*   **CreBS** — A Python/GTK application used to create and set desktop wallpaper slideshows for GNOME.

	[http://www.obfuscatepenguin.net/](http://www.obfuscatepenguin.net/) || [crebs](https://aur.archlinux.org/packages/crebs/)

对于设置XML文件作为默认的背景，参阅 [#Lock screen and background](#Lock_screen_and_background).

### 自定义 GNOME 会话

It is possible to create custom GNOME sessions which use the GNOME session manager but start different sets of components ([Openbox](/index.php/Openbox "Openbox") with [tint2](/index.php/Tint2 "Tint2") instead of GNOME Shell for example).

Two files are required for a custom GNOME session: a session file in `/usr/share/gnome-session/sessions/` which defines the components to be started and a [desktop entry](/index.php/Desktop_entry "Desktop entry") in `/usr/share/xsessions` which is read by the [display manager](/index.php/Display_manager "Display manager"). An example session file is provided below:

 `/usr/share/gnome-session/sessions/gnome-openbox.session` 
```
[GNOME Session]
Name=GNOME Openbox
RequiredComponents=openbox;tint2;gnome-settings-daemon;

```

And an example desktop file:

 `/usr/share/xsessions/gnome-openbox.desktop` 
```
[Desktop Entry]
Name=GNOME Openbox
Exec=gnome-session --session=gnome-openbox

```

**Note:** GNOME Session calls upon the `.desktop` files of each of the components to be started. If a component you wish to start does not provide a `.desktop` file, you must create a suitable desktop entry in a directory such as `/usr/local/share/applications`.

## 故障排除

### Gnome Shell 界面卡死

如果 Gnome Shell 的界面卡死了（可能是由于某些外观调整异常、某个扩展出问题，或内存不足），你可能就连按下 `Alt` + `F2` 并输入 **r** 的机会都没有。这时，请试着切换到另一个 TTY（**Ctrl** + **Alt** + **F2**） 上，并输入命令`pkill -HUP gnome-shell`。Gnome Shell 将重新启动，可能需要个几十秒。这样的重启方式不会注销已登录的用户，因此所有的程序也将继续运行。不过，保存你正在编辑文件总是个好主意。

如果这也不行，那你可能得重新启动 [Xorg](/index.php/Xorg "Xorg") 服务器。如果你通过终端登录，输入 `pkill X`；如果你通过 GDM 登录，输入 `systemctl restart gdm`。但需要注意的是，重启 Xorg 服务器会导致已登录的用户被注销，因此请确保在这之前已经设法保存你所有的文件。

### Incorrect application defaults

When installing applications for the first time you may find that GNOME has the wrong application associated to a certain protocols - for instance, *easytag* becomes the folder handler instead of [GNOME Files](/index.php/GNOME_Files "GNOME Files").

For GNOME Files see the following page: [GNOME Files#Files is no longer the default file manager](/index.php/GNOME_Files#Files_is_no_longer_the_default_file_manager "GNOME Files").

For Document Viewer, run the following command:

```
$ xdg-mime default evince.desktop application/pdf

```

For other applications, default handler settings are detailed on the following page: [Default applications](/index.php/Default_applications "Default applications").

Optionally, you can [install](/index.php/Install "Install") [gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/). It will place your configuration file at `/etc/gnome/defaults.list`.

### Tracker & Documents do not list any local files

In order for Tracker (and, therefore, Documents) to detect your local files, they must be stored in an [XDG compliant directory](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html) (such as 'Documents' or 'Music'). For more information, see [Xdg user directories](/index.php/Xdg_user_directories "Xdg user directories").

You can also configure Tracker to recursively search inside specific directories such as your home directory. These settings can be made using `tracker-preferences`.

### Unable to add accounts in Empathy and GNOME Online Accounts

Empathy, the engine behind integrated messaging, GNOME Online Accounts, and all other system settings based on messaging accounts will not function correctly unless the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group of packages or at least one of the backends ([telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble), or [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), for example) is [installed](/index.php/Install "Install"). View descriptions of *telepathy* components on the [freedesktop.org telepathy wiki](http://telepathy.freedesktop.org/wiki/Components).

**Note:** [Avahi](/index.php/Avahi "Avahi") daemon is required for connecting with the People Nearby account, and also in order for some desktop extensions to work correctly like [Chat Status](https://extensions.gnome.org/extension/746/chat-status/)

### Cannot change settings in dconf-editor

When one cannot set settings in [dconf](https://www.archlinux.org/packages/?name=dconf), it is possible their dconf user settings are corrupt. In this case it is best to delete the user dconf files in `~/.config/dconf/user*` and set the settings in dconf-editor after.

### When an extension breaks the shell

When enabling shell extensions causes GNOME breakage, you should first remove the *user-theme* and *auto-move-windows* extensions from their installation directory.

The installation directory could be one of `~/.local/share/gnome‑shell/extensions`, `/usr/share/gnome‑shell/extensions` or `/usr/local/share/gnome‑shell/extensions`. Removing these two extension-containing folders may fix the breakage. Otherwise, isolate the problem extension with trial‑and‑error.

Removing or adding an extension-containing folder to the aforementioned directories removes or adds the corresponding extension to your system. Details on GNOME Shell extensions are available at the [GNOME web site.](https://live.gnome.org/GnomeShell/Extensions)

If you have trouble with uninstalling an extension via [extensions.gnome.org/local](https://extensions.gnome.org/local/), then probably they have been installed as system-wide extensions with the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package. Removing the package again obviously affects all user accounts.

### 扩展在 GNOME 3 升级后不工作了

**Note:** Please bear in mind that whilst the methods below will allow you to **try** and activate an extension with an unsupported version of GNOME Shell, it is by no means a guarantee that the extension will work successfully. The most likely outcome of trying to activate such an extension is that GNOME Shell will crash and then restart.

Before trying the workarounds below, check if an update is available for the extension by visiting [extensions.gnome.org/local](https://extensions.gnome.org/local).

If there is no update for your current GNOME version yet, use the following command to disable version validation for extensions:

```
$ gsettings set org.gnome.shell disable-extension-version-validation true

```

Alternatively, you could modify the extension itself, changing the supported shell version to satisfy the version validation. See the method below.

找到扩展的安装目录，可能是 `~/.local/share/gnome-shell/extensions` 或 `/usr/share/gnome-shell/extensions`.

编辑扩展子文件夹中的每一个 **`metadata.json`**

| Insert: | `"shell-version": ["3.x"]` |
| Instead of (for example): | `"shell-version": ["3.4"]` |

`"3.x"` 是最好的选择，这个表示扩展能在所有 ***3.x*** GNOME Shell版本下工作。

### 只有 conky 运行时键盘快捷方式不工作

gnome-shell 键盘快捷方式(如 Alt+F2,Alt+F1 和多媒体键快捷方式)当只有 conky 运行时不会工作。然而如果另一个程序(例如 gedit)在运行，键盘快捷方式就可以工作了。

解决方式：编辑 .conkyrc

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type dock
own_window_class Conky
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

### Unable to apply stored configuration for monitors

If you encounter this message try to disable the *xrandr* `gnome-settings-daemon plugin`:

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

### 一致的光标主题

See [Cursor themes#Desktop environments](/index.php/Cursor_themes#Desktop_environments "Cursor themes").

### Windows cannot be modified with Alt-Key + mouse-button

In GNOME 3.6 and above, the mouse button modifier (the key that allows you to drag a window from a location other than the titlebar) is the `Super` key instead of the `Alt` key which was used in the past. The change was made in response to the following [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=607797).

To change the mouse button modifier back to the `Alt` key, execute the following:

```
$ gsettings set org.gnome.desktop.wm.preferences mouse-button-modifier '<Alt>'  

```

**Note:** It is not possible to change this with *System settings* > *Keyboard* > *Shortcuts*

### 加载速度慢的系统图标/慢GDM登录

Problems with the loading of system icons, such the ones in the title bar of Files, might be solved by [installing](/index.php/Pacman#Installing_specific_packages "Pacman") (or re-installing) the [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2) package.

Re-installing the aforementioned package may also fix repeated occurrences of the "Oh no! Something has gone wrong!" error screen and/or very slow loading and login with GDM as described in the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1414157).

### Artifacts when maximizing windows

Maximizing windows may cause artifacts as of GNOME 3.12.0 - see the following [forum thread](https://bbs.archlinux.org/viewtopic.php?id=183617) and [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=728385). A solution is detailed in the following section: [#Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics).

### Tear-free video with Intel HD Graphics

	Intel TearFree

Enabling the [Xorg Intel TearFree option](/index.php/Intel_Graphics#Tear-free_video "Intel Graphics") is a known workaround for tearing problems on Intel adapters. However, the way this option acts makes it redundant with the use of a compositor (it increases memory consumption and lowers performance, see [the original bug report's final comment](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)).

	DRI3

According to [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c2), DRI3 includes the `buffer_age` extension that allows GNOME Shell's Mutter compositor to sync windows to vblank in an efficient way. DRI3 support is not compiled in to the mesa package, so you have to recompile [mesa](https://www.archlinux.org/packages/?name=mesa) with `--enable-dri3` in the `./configure` flags (see [ABS](/index.php/ABS "ABS")). Then enable it in the Xorg driver:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "DRI"    "3"
EndSection
```

	Mutter tweaks

**Note:** This workaround has been [reported](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c0) to have side effects and may not fix tearing in all cases.

GNOME Shell's Mutter compositor has a tweak known to address tearing problems (see [the original suggestion for this fix](https://bugzilla.gnome.org/show_bug.cgi?id=657071#c1) and its mention in [the Freedesktop bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c59)). To enable this tweak, append the following line to `/etc/environment`: `CLUTTER_PAINT=disable-clipped-redraws:disable-culling`. Then restart the Xorg server.

### Window opens behind other windows when using multiple monitors

This is possibly a bug in GNOME Shell which causes new windows to open behind others. To fix this issue, one can run the following command:

```
$ gsettings set org.gnome.shell.overrides workspaces-only-on-primary false

```

### 锁定按钮无法重新启用触摸板

Some laptops have a touchpad lock button that disables the touchpad so that users can type without worrying about touching the touchpad. Currently, it appears that although GNOME can lock the touchpad by pressing this button, it cannot unlock it. If the touchpad gets locked you can run the following to unlock it:

```
$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### GNOME Shell键盘源菜单不可见

A menu showing the keyboard input sources (for example 'en' for an English keyboard layout) should be visible next to the status area containing icons for network, volume and power sources. If the keyboard sources menu is not visible, this is probably because you have configured your [Xorg](/index.php/Xorg "Xorg") keyboard layout in a way which GNOME does not recognise.

To ensure that the menu is visible, remove any Xorg keyboard configuration you might have created and set the keyboard locale using [localectl](/index.php/Keyboard_configuration_in_Xorg#Using_localectl "Keyboard configuration in Xorg").

Upon running the command and then logging out, you should find that the keyboard input sources menu is visible in GDM and in the GNOME Shell desktop. See [Input sources in GNOME](http://blogs.gnome.org/mclasen/2012/09/21/input-sources-in-gnome/) for more information.

### 鼠标指针丢失

When using a separate [window manager](/index.php/Window_manager "Window manager") with *gnome-settings-daemon*, the mouse cursor may vanish. Run:

```
$ gsettings set org.gnome.settings-daemon.plugins.cursor active false

```

### 在会话菜单中没有重启按钮时，屏幕被锁定

If [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") is installed, ensure that it is not running at startup, see [GNOME#Startup applications](/index.php/GNOME#Startup_applications "GNOME").

### pulseaudio系统原因延误GNOME和GDM

If you are running [PulseAudio](/index.php/PulseAudio "PulseAudio") in system-wide mode, the PulseAudio 7.0 upgrade breaks [GDM](/index.php/GDM "GDM") and GNOME. See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=203051) for more information.

### GNOME crashes when trying to reorder applications in the GNOME Shell Dash

The dash is the "toolbar" that appears, by default, [on the left](https://en.wikipedia.org/wiki/GNOME_Shell#Design_components "wikipedia:GNOME Shell") when you click Activities. Applications can be reordered in the dash by dragging and dropping. If this fails, and/or causes GNOME to crash, try [changing your icon theme](https://bbs.archlinux.org/viewtopic.php?id=171689).

## 参见

*   [官方网站](http://www.gnome.org/)
*   [GNOME-shell扩展](http://extensions.gnome.org/)
*   主题、图标和壁纸：
    *   [GNOME Art](http://art.gnome.org/)
    *   [GNOME Look](http://www.gnome-look.org/)
*   GTK/GNOME 程序：
    *   [GNOME Files](http://www.gnomefiles.org/)
    *   [GNOME Project Listing](http://www.gnome.org/projects/)
*   [自定义GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html)