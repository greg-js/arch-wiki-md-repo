**翻译状态：** 本文是英文页面 [Enlightenment](/index.php/Enlightenment "Enlightenment") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-02-03，点击[这里](https://wiki.archlinux.org/index.php?title=Enlightenment&diff=0&oldid=464174)可以查看翻译后英文页面的改动。

## Contents

*   [1 Enlightenment](#Enlightenment)
    *   [1.1 安装](#.E5.AE.89.E8.A3.85)
        *   [1.1.1 从 AUR 安装](#.E4.BB.8E_AUR_.E5.AE.89.E8.A3.85)
    *   [1.2 启动 Enlightenment](#.E5.90.AF.E5.8A.A8_Enlightenment)
        *   [1.2.1 Entrance](#Entrance)
        *   [1.2.2 手动启动 Enlightenment](#.E6.89.8B.E5.8A.A8.E5.90.AF.E5.8A.A8_Enlightenment)
    *   [1.3 配置](#.E9.85.8D.E7.BD.AE)
        *   [1.3.1 网络](#.E7.BD.91.E7.BB.9C)
        *   [1.3.2 Polkit 代理](#Polkit_.E4.BB.A3.E7.90.86)
        *   [1.3.3 集成 GNOME 密钥环](#.E9.9B.86.E6.88.90_GNOME_.E5.AF.86.E9.92.A5.E7.8E.AF)
        *   [1.3.4 系统托盘](#.E7.B3.BB.E7.BB.9F.E6.89.98.E7.9B.98)
        *   [1.3.5 通知](#.E9.80.9A.E7.9F.A5)
    *   [1.4 主题](#.E4.B8.BB.E9.A2.98)
        *   [1.4.1 GTK+](#GTK.2B)
    *   [1.5 模块和小部件](#.E6.A8.A1.E5.9D.97.E5.92.8C.E5.B0.8F.E9.83.A8.E4.BB.B6)
        *   [1.5.1 "外部" 模块](#.22.E5.A4.96.E9.83.A8.22_.E6.A8.A1.E5.9D.97)
    *   [1.6 默认键绑定](#.E9.BB.98.E8.AE.A4.E9.94.AE.E7.BB.91.E5.AE.9A)
    *   [1.7 排错](#.E6.8E.92.E9.94.99)
        *   [1.7.1 合成](#.E5.90.88.E6.88.90)
        *   [1.7.2 字体看不清楚](#.E5.AD.97.E4.BD.93.E7.9C.8B.E4.B8.8D.E6.B8.85.E6.A5.9A)
        *   [1.7.3 背光总是较暗](#.E8.83.8C.E5.85.89.E6.80.BB.E6.98.AF.E8.BE.83.E6.9A.97)
        *   [1.7.4 光标主题不一致](#.E5.85.89.E6.A0.87.E4.B8.BB.E9.A2.98.E4.B8.8D.E4.B8.80.E8.87.B4)
        *   [1.7.5 背景图片](#.E8.83.8C.E6.99.AF.E5.9B.BE.E7.89.87)
*   [2 Enlightenment DR16](#Enlightenment_DR16)
    *   [2.1 安装 E16](#.E5.AE.89.E8.A3.85_E16)
    *   [2.2 基本设置](#.E5.9F.BA.E6.9C.AC.E8.AE.BE.E7.BD.AE)
        *   [2.2.1 启动、重启、停止脚本](#.E5.90.AF.E5.8A.A8.E3.80.81.E9.87.8D.E5.90.AF.E3.80.81.E5.81.9C.E6.AD.A2.E8.84.9A.E6.9C.AC)
        *   [2.2.2 合成器（Compositor）](#.E5.90.88.E6.88.90.E5.99.A8.EF.BC.88Compositor.EF.BC.89)
*   [3 参考资料](#.E5.8F.82.E8.80.83.E8.B5.84.E6.96.99)
*   [4 配置输入法](#.E9.85.8D.E7.BD.AE.E8.BE.93.E5.85.A5.E6.B3.95)
    *   [4.1 ibus](#ibus)

## Enlightenment

这个软件包提供了 [Enlightenment](https://www.enlightenment.org/) 的[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")及其构建库 EFL（Enlightenment Foundation Libraries）。后者提供了额外的桌面环境特性，如工具包、对象画布和抽象对象。Enlightenment 从 2005 年开始开发，2011 年 2 月发布 1.0 稳定版本。

### 安装

可[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")同名软件包 [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) 。

还可以安装 [terminology](https://www.archlinux.org/packages/?name=terminology)，这是一个基于 EFL 的终端仿真器。

#### 从 AUR 安装

**警告:** 其中某些软件包使用不稳定的开发版代码，请风险自担。

开发版的软件包源码及其依赖的包构建文件可以从 [enlightenment-git](https://aur.archlinux.org/packages/enlightenment-git/) 下载。 以下是基于 EFL 的应用，大部份是开发版本，尚未正式发布：

*   [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) – Ecrire 文本编辑器
*   [elbow-git](https://aur.archlinux.org/packages/elbow-git/) – Elbow 浏览器
*   [eluminance-git](https://aur.archlinux.org/packages/eluminance-git/) – Eluminance 图片浏览器
*   [enjoy-git](https://aur.archlinux.org/packages/enjoy-git/) – [Enjoy](https://trac.enlightenment.org/e/wiki/Enjoy) 音乐播放器
*   [eperiodique](https://aur.archlinux.org/packages/eperiodique/) – [Eperiodique](http://eperiodique.sourceforge.net/) periodic 表格查看器
*   [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) – [Ephoto](https://trac.enlightenment.org/e/wiki/Ephoto) 图片查看器
*   [epymc-git](https://aur.archlinux.org/packages/epymc-git/) – E Python 多媒体中心
*   [equate-git](https://aur.archlinux.org/packages/equate-git/) – Equate 计算器
*   [eruler-git](https://aur.archlinux.org/packages/eruler-git/) – Eruler 屏幕尺和测量工具
*   [efbb-git](https://aur.archlinux.org/packages/efbb-git/) – Escape from Booty Bay 类似《愤怒的小鸟》的游戏
*   [elemines-git](https://aur.archlinux.org/packages/elemines-git/) – [Elemines](http://elemines.sourceforge.net/) 《扫雷》类型的游戏
*   [espionage-git](https://aur.archlinux.org/packages/espionage-git/) – Espionage D-Bus 监测器
*   [ev-git](https://aur.archlinux.org/packages/ev-git/) – ev 简单图片查看器
*   [rage](https://aur.archlinux.org/packages/rage/) and [rage-git](https://aur.archlinux.org/packages/rage-git/) – Rage 视频播放器

### 启动 Enlightenment

从你惯用的[显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器")选择*Enlightenment* ，或配置好 [xinitrc](/index.php/Xinitrc "Xinitrc") 从控制台启动。

#### Entrance

**警告:** Entrance 为实验性版本，还不被 systemd 完全支持 ，请风险自担。

Enlightenment 提供了一个名为 Entrance 的新显示管理器，由 [entrance-git](https://aur.archlinux.org/packages/entrance-git/) 提供。Entrance 十分精巧，它用 `/etc/entrance.conf` 管理配置。可以通过 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") 启用 `entrance.service` 服务来使用它。

#### 手动启动 Enlightenment

如果选择从控制台手工启动，把下列内容加入 `~/.xinitrc` 文件：

 `~/.xinitrc` 
```
exec enlightenment_start

```

然后就可以输入 `startx` 来启动 Enlightenment。详见 [xinitrc](/index.php/Xinitrc_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinitrc (简体中文)")。

### 配置

Enlightenment 提供了一个精巧的配置系统，可以从主菜单中选择“设置”子菜单进入。

#### 网络

**ConnMan**

Enlightenment 首选的网络管理器是 [ConnMan](/index.php/Connman "Connman") ，包名： [connman](https://www.archlinux.org/packages/?name=connman) 。配置方法参见：[Connman](/index.php/Connman "Connman")。

为实现更多的配置，还可以安装 Econnman （AUR 中的 [econnman](https://aur.archlinux.org/packages/econnman/) 或 [econnman-git](https://aur.archlinux.org/packages/econnman-git/)）及其相关依赖包。

**把 ConnMan 添加到书架**

1.  设置 -> 扩展 -> 模块
2.  系统
3.  连接管理器（Connection Manager）
4.  加载（选中并点击*加载*）
5.  在屏幕底部书架点击右键
6.  进入书架 -> 内容
7.  滚动项目列表找到 *ConnMan*
8.  点击*添加*

**NetworkManager**

你也可以使用 [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) 来管理网络连接。参见 [NetworkManager (简体中文)](/index.php/NetworkManager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NetworkManager (简体中文)")。

你可能还需要 [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) 的帮助。把它加入自动启动，这样每次进桌面就能看到它在系统托盘中。方法：*设置 > 全部 > 应用程序 > 启动应用程序 > 系统*，激活*网络*。

如果没有[#系统托盘](#.E7.B3.BB.E7.BB.9F.E6.89.98.E7.9B.98)，网络可以正常连接但指示器将不显示。

#### Polkit 代理

Enlightenment does not ship with a [graphical polkit authentication agent](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.BA.AB.E4.BB.BD.E8.AE.A4.E8.AF.81.E7.BB.84.E4.BB.B6 "Polkit (简体中文)"). If you want to access some privileged actions (e.g. mount a filesystem on a system device), you have to install one and autostart it. For that you should go to *Settings Panel > Apps > Startup Applications > System* and activate it. There is an EFL based authentication agent available in the AUR, [polkit-efl-git](https://aur.archlinux.org/packages/polkit-efl-git/).

#### 集成 GNOME 密钥环

It is possible to use gnome-keyring in Enlightenment. However, at the time of writing, you need a small hack to make it work in full. First, you must tell Enlightenment to autostart gnome-keyring. For that you should go to *Settings Panel > Apps > Startup Applications > System* and activate *Certificate and Key Storage*, *GPG Password Agent*, *SSH Key Agent* and "Secret Storage Service". After this, you should edit your `~/.pam_environment` and add the following:

```
       #Set gnome-keyring as the ssh authentication agent
       SSH_AUTH_SOCK=/run/user/${UID}/keyring/ssh

```

This "hack" is used to override the automatic setting of the variable by "enlightenment-start" from "ssh-agent" to gnome-keyring.

More information on this topic in the [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") article.

#### 系统托盘

**注意:** Since Enlightenment 20, Xembed support has been removed [[1]](https://twitter.com/_enlightenment_/status/538000507315314688) meaning that many 'legacy' applets can no longer be displayed in the Systray. To use these applets, you will need to use a standalone system tray application such as [stalonetray](https://www.archlinux.org/packages/?name=stalonetray) instead.

Enlightenment has support for a system tray but it is disabled by default. To enable the system tray, open the Enlightenment main menu, navigate to the *Settings* submenu and click on the *Modules* option. Scroll down until you see the *Systray* option. Highlight that option and click the *Load* button. Now that the module has been loaded, it can be added to the shelf. Right click on the shelf you wish to add the Systray to, hightlight the *Shelf* submenu and click on the *Contents* option. Scroll down until you see *Systray*. Highlight that option and click the *Add* button.

#### 通知

Enlightenment provides a notification server through its Notification extension.

*   Notifications may be displayed in any corner of the "screen" as defined below
*   Available screen policies are Primary Screen, Current Screen, All Screens, and Xinerama
*   Notifications may be filtered based on urgency (Low, Normal, or Critical in any combination)
*   A default notification timeout may be set and optionally enforced for all notifications
*   The notification server may also optionally ignore replace ID requests

### 主题

More themes to customize the look of Enlightenment are available from:

*   [exchange.enlightenment.org](http://exchange.enlightenment.org/theme)
*   [e17-stuff.org](http://e17-stuff.org/index.php?xcontentmode=7000)
*   [relighted.c0n.de](http://relighted.c0n.de/#100) for the default theme in 200 different colors
*   [git.enlightenment.org](http://git.enlightenment.org/themes) (git clone the theme you like, run 'make' and you end up with a .edj theme file)
*   [packages.bodhilinux.com](http://packages.bodhilinux.com/bodhi/pool/stable/b/) has a good collection (you will need to extract the .edj file from the .deb; bsdtar will do this and is part of the base ArchLinux install). A nice catalog can be seen at [their wiki](https://web.archive.org/web/20140120083020/http://art.bodhilinux.com/doku.php?id=bodhi_e17_themes_v3).

You can install the themes (coming in .edj format) using the theme configuration dialog or by moving them to `~/.e/e/themes`.

**注意:** Enlightenment does not provide a stable theme API, and there have been numerous theme API changes over the years, even after E17 was released. Themes that have not been updated regularly are unlikely to work.

**提示：** To make GTK and Qt applications match the default theme of Enlightenment you can download a theme like the [E17 GTK theme](http://gnome-look.org/content/show.php/?content=163472), place it in `~/.themes/` and select application themes from Enlightenments settings, and set it to that, this will make all GTK2 and GTK3 applications match the default Enlightenment theme, you can then configure Qt applications (or configure Qt's default settings) to use the Gtk+ theme so it will mimic the theme your GTK applications are using, this way you can make sure most applications will blend in perfectly with your default enlightenment theme. 参阅[Qt 与 GTK 应用程序外观一致化](/index.php/Qt_%E4%B8%8E_GTK_%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E5%A4%96%E8%A7%82%E4%B8%80%E8%87%B4%E5%8C%96 "Qt 与 GTK 应用程序外观一致化")。

#### GTK+

To alter the GTK+ theme, go to *Settings > All > Look > Application Theme*.

### 模块和小部件

	Module

	Name used in enlightenment to refer to the "backing" code for a gadget.

	Gadget

	Front-end or user interface that should help the end users of Enlightenment do something.

Many Modules provide Gadgets that can be added to your desktop or on a shelf. Some Modules (such as CPUFreq) only provide a single Gadget while others (such as Composite) provide additional features without any gadgets. Note that certain gadgets such as Systray can only be added to a shelf while others such as Moon can only be loaded on the desktop.

#### "外部" 模块

**警告:** 这些第三方模块不被官方开发者支持。它们直接来自 git ，因而随时可能工作异常。请风险自担。

Beyond the modules described here, more "extra" modules are available from [e-modules-extra-git](https://aur.archlinux.org/packages/e-modules-extra-git/).

**Places**

Places is a gadget that will help you browse files on various devices you might plug into your computer, like phones, cameras, or other various storage devices you might plug into the usb port.

Available from [places-git](https://aur.archlinux.org/packages/places-git/).

**注意:** This module is no longer required for auto-mounting external devices in Enlightenment

**Scale Windows**

The *Scale Windows* module, which requires compositing to be enabled, adds several features. The scale windows effect shrinks all open windows and brings them all into view. This is known in "Mission Control" in macOS. The scale pager effect zooms out and shows all desktops as a wall, like the compiz expo plugin. Both can be added to the desktop as a gadget or bound to a key binding, mouse binding or screen edge binding.

Some people like to change the standard window selection key binding `ALT + Tab` to use Scale Windows to select windows. To change this setting, you navigate to *Menu > Settings > Settings Panel > Input > Keys*. From here, you can set any key binding you would like.

To replace the window selection key binding functionality with Scale Windows, scroll through the left panel until you find the *ALT* section and then find and select `ALT + Tab`. Then, scroll through the right panel looking for the "Scale Windows" section and choose either *Select Next* or *Select Next (All)* depending on whether you would like to see windows from only the current desktop or from all desktops and click *Apply* to save the binding.

Available from [comp-scale-git](https://aur.archlinux.org/packages/comp-scale-git/).

### 默认键绑定

<caption>Some default Enlightenment keybindings</caption>
| Shift + F10 | Maximize Vertically |
| Ctrl + Menu | Show "Clients" (windows) Menu |
| Alt + Escape | Show "Everything Launcher" (apps, windows, etc) |
| Win + Left | Maximize Left |
| Win + Right | Maximize Right |
| Alt + Shift + F10 | Maximize Horizontally |
| Alt + Shift + Left | Flip to the Desktop on the Left |
| Alt + Shift + Right | Flip to the Desktop on the Right |
| Ctrl + Alt + D | Show the desktop |
| Ctrl + Alt + F | Toggle Fullscreen |
| Ctrl + Alt + I | Toggle iconic mode |
| Ctrl + Alt + K | Kill window |
| Ctrl + Alt + L | Lock the desktop |
| Ctrl + Alt + N | Maximize Window |
| Ctrl + Alt + R | Toggle Shade up |
| Ctrl + Alt + W | Window menu |
| Ctrl + Alt + X | Close a window |
| Ctrl + Alt + Down | Lower |
| Ctrl + Alt + Up | Raise |
| Ctrl + Alt + Left | Flip to desktop on left |
| Ctrl + Alt + Right | Flip to desktop on right |
| Ctrl + Alt + Delete | End session dialog |
| Ctrl + Alt + Insert | Launch the default terminal |

### 排错

If you find some unexpected behavior, there are a few things you can do:

1.  try to see if the same behavior exists with the default theme
2.  disable any 3rd party modules you may have installed
3.  backup `~/.e` and remove it (e.g. `mv ~/.e ~/.e.back`)

If you are sure you found a bug please report it [directly upstream](https://phab.enlightenment.org/maniphest/task/create/).

#### 合成

When the configuration needs to be reset and the settings windows can no longer be approached, configuration for the compositor can be reset using the hardcoded keybinding `Ctrl + Alt + Shift + Home`.

#### 字体看不清楚

If fonts are too small and your screen is unreadable, be sure the right font packages are installed. [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) and [ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera) are valid candidates.

You can set scaling under *Settings > Settings Panel > Look > Scaling*.

#### 背光总是较暗

You may find that Enlightenment routinely dims the backlight to 30% on logout and will only restore it to 100% when you log into another Enlightenment session. This is especially problematic when using another desktop environment alongside Enlightenment as the backlight will not automatically be restored to its normal level when using that desktop environment. To fix this issue, open the Enlightenment *Settings Panel* and, under the *Look* tab, click on the *Composite* option. Tick the *Don't fade backlight* box and click *OK*.

#### 光标主题不一致

You may find that the cursor theme for the desktop is different to the one used in applications such as [Firefox (简体中文)](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)"). This is because desktop applications are using X cursor themes whilst Enlightenment has its own set of cursor themes. For consistency, you can set Enlightenment to always use the X cursor theme. To do this, open the Enlightenment *Settings Panel* and click on the *Input* tab. Click on the *Mouse* option. Change the theme from *Enlightenment* to *X* and click *OK*. You should now find that the same cursor theme is used everywhere. If the X cursor theme itself is not always consistent, see [光标主题](/index.php/Cursor_themes_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#XDG_.E8.A7.84.E5.88.99 "Cursor themes (简体中文)")

#### 背景图片

You have to copy the desired wallpapers into `~/.e/e/backgrounds/`

MMB or RMB anywhere on the desktop will give access to the settings, select `/Desktop/Backgrounds/`

Any new image copied in the `~/.e/e/backgrounds/` folder will get the list of available backgrounds auto-updated. Select desired wallpaper from drop-down menu. Inside the appropriate tabs in the global settings, you can adjust things like tiling of the background image, filling screen and such.

## Enlightenment DR16

Enlightenment, Development Release 16 was first released in 2000, and reached version 1.0 in 2009\. Originally, the DR16 stood for the 0.16 version of the Enlightenment project. You'll find it as "Enlightenment16" now in the Arch repositories, it is still under development today, regularly updated by its maintainer Kim 'kwo' Woelders. With compositing, shadows and transparencies, E16 kept all of the speed that presided over its foundation by original author Carsten "Rasterman" Haitzler but with up to date refinement.

### 安装 E16

Install [enlightenment16](https://www.archlinux.org/packages/?name=enlightenment16).

See `/usr/share/doc/e16/e16.html` for in depth documentation. The man page is at `man e16`, not `man enlightenment`, and only gives startup options.

### 基本设置

Most configuration files for E16 reside in `~/.e16` and are text-based, editable at will. That includes the Menus too.

Shortcut keys can be either modified by hand, or with the e16keyedit software provided as source on the [sourceforge](http://sourceforge.net/projects/enlightenment/) page of the e16 project, or from the [e16keyedit](https://aur.archlinux.org/packages/e16keyedit/) package. Note that the keyboard shortcuts file is not created in `~/.e16` by default. You can copy the packaged version to your home directory if you wish to make changes:

```
$ cp /usr/share/e16/config/bindings.cfg ~/.e16

```

#### 启动、重启、停止脚本

Create an Init, a Start and a Stop folder in your `~/.e16` folder: any .sh script found there will either be executed at Startup (from Init folder), at each Restart (from Start folder), or at Shutdown (from Stop folder); provided you allowed it trough the MMB / settings / session / <enable scripts> button and made them executable with `chmod +x **yourscript.sh**`. Typical examples involves starting pulseaudio or your favorite network manager applet.

#### 合成器（Compositor）

阴影、透明等等特效位于 Composite 项下的 MMB 或 RMB / 设置。

## 参考资料

*   [Enlightenment 主页](http://www.enlightenment.org/)
*   [Enlightenment Exchange](http://exchange.enlightenment.org/)
*   [Enlightenment 开发者文档](http://docs.enlightenment.org/)
*   [Bodhi Guide to Enlightenment](http://www.bodhilinux.com/e17guide/e17guideEN/)
*   [E17-Stuff](http://www.e17-stuff.org/)
*   [DR16 下载资源](http://sourceforge.net/projects/enlightenment/)
*   [Enlightenment 用户邮件列表](https://lists.sourceforge.net/lists/listinfo/enlightenment-users)
*   [Enlightenment 开发者邮件列表](https://lists.sourceforge.net/lists/listinfo/enlightenment-devel)
*   [irc://irc.freenode.net#e](irc://irc.freenode.net#e)

## 配置输入法

**注意:** 为方便简体中文用户，本节内容暂予保留

E17 内置了输入法支持的模块，支持的输入法有 iiimf 、scim 和 uim 。使用这些输入法的配置在

```
Settings -> Settings Panel -> Language -> Input Method Settings -> Advanced

```

System 配置中，使用者只需选择即可。使用其他输入法的用户可以在 Personal 配置中添加。

### ibus

ibus 的配置参数为：

```
Input Method Parameters:
 Name              ibus
 Execute Command   /usr/bin/ibus-daemon --xim
 Setup Command     /usr/bin/ibus-setup

```

```
Exported Environment Variables:
 GTK_IM_MODULE     ibus
 QT_IM_MODULE      ibus
 XMODIFIERS        @im=ibus

```