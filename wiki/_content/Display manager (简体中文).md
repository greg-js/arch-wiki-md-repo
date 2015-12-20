# Display manager (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

相关文章

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login")

**翻译状态：** 本文是英文页面 [Display_manager](/index.php/Display_manager "Display manager") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-7-27，点击[这里](https://wiki.archlinux.org/index.php?title=Display_manager&diff=0&oldid=399021)可以查看翻译后英文页面的改动。

[显示管理器](https://en.wikipedia.org/wiki/X_display_manager_(program_type) "wikipedia:X display manager (program type)")或登录管理器是一个在启动最后显示的图形界面。和窗口管理器一样，显示管理器有很多种。通常每个显示管理器都能进行一些定制。

## Contents

*   [1 显示管理器列表](#.E6.98.BE.E7.A4.BA.E7.AE.A1.E7.90.86.E5.99.A8.E5.88.97.E8.A1.A8)
    *   [1.1 控制台](#.E6.8E.A7.E5.88.B6.E5.8F.B0)
    *   [1.2 图形界面](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2)
*   [2 加载显示管理器](#.E5.8A.A0.E8.BD.BD.E6.98.BE.E7.A4.BA.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.1 使用 systemd-logind](#.E4.BD.BF.E7.94.A8_systemd-logind)
*   [3 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [3.1 第二次注销时崩溃](#.E7.AC.AC.E4.BA.8C.E6.AC.A1.E6.B3.A8.E9.94.80.E6.97.B6.E5.B4.A9.E6.BA.83)
*   [4 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [4.1 会话列表](#.E4.BC.9A.E8.AF.9D.E5.88.97.E8.A1.A8)
    *   [4.2 没有窗口管理启动应用程序](#.E6.B2.A1.E6.9C.89.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.90.AF.E5.8A.A8.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [4.3 自动启动](#.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8)
    *   [4.4 设置语言](#.E8.AE.BE.E7.BD.AE.E8.AF.AD.E8.A8.80)
*   [5 已知问题](#.E5.B7.B2.E7.9F.A5.E9.97.AE.E9.A2.98)
    *   [5.1 不兼容在systemd](#.E4.B8.8D.E5.85.BC.E5.AE.B9.E5.9C.A8systemd)

## 显示管理器列表

**注意:** 如果使用 [桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)"),应该尽量使用对应的显示管理器。

### 控制台

*   [CDM](/index.php/CDM "CDM"): 控制台显示管理器 (available in the [AUR](/index.php/AUR "AUR"): [cdm-git](https://aur.archlinux.org/packages/cdm-git/)<sup><small>AUR</small></sup>)
*   **[Console TDM](/index.php/Console_TDM "Console TDM")** — Extension for _xinit_ written in pure Bash.

[http://code.google.com/p/t-display-manager/](http://code.google.com/p/t-display-manager/) || [console-tdm](https://aur.archlinux.org/packages/console-tdm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/console-tdm)]</sup>

### 图形界面

*   **[Entrance](/index.php/Enlightenment "Enlightenment")** — An EFL based display manager, highly experimental.

[http://enlightenment.org/](http://enlightenment.org/) || [entrance-git](https://aur.archlinux.org/packages/entrance-git/)<sup><small>AUR</small></sup>

*   [GDM](/index.php/GDM "GDM"): [GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") 显示管理器 。[http://projects.gnome.org/gdm/](http://projects.gnome.org/gdm/)[gdm](https://www.archlinux.org/packages/?name=gdm)
*   [KDM](/index.php/KDM "KDM"): [KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)") 显示管理器 ([kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)<sup><small>AUR</small></sup>）
*   [LightDM](/index.php/LightDM "LightDM"):Ubuntu 开发的 GDM 替代品，使用 WebKit。跨桌面的显示管理器，可以使用各种前端写的任何工具。[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM)[lightdm](https://www.archlinux.org/packages/?name=lightdm)||[lightdm-bzr](https://aur.archlinux.org/packages/lightdm-bzr/)<sup><small>AUR</small></sup>
*   [LXDM](/index.php/LXDM "LXDM"): [LXDE](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)") 显示管理器 (独立于桌面环境) ([lxdm](https://www.archlinux.org/packages/?name=lxdm))
*   **MDM** — MDM 显示管理器使用在Linux Mint, a fork of GDM 2.

[https://github.com/linuxmint/mdm](https://github.com/linuxmint/mdm) || [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)<sup><small>AUR</small></sup>

*   [SDDM](/index.php/SDDM "SDDM")：基于QML的显示管理器并继承于KDE4的KDM，适用于Plasma。[https://github.com/sddm/sddm](https://github.com/sddm/sddm)[sddm](https://www.archlinux.org/packages/?name=sddm)
*   [SLiM](/index.php/SLiM "SLiM"): 简单登录管理器 ([slim](https://www.archlinux.org/packages/?name=slim))

    **Warning:** slim登录管理器已经停止开发，不推荐使用

*   [wdm](/index.php/Wdm "Wdm"): WINGs 显示管理器 ([wdm](https://aur.archlinux.org/packages/wdm/)<sup><small>AUR</small></sup>)
*   **[XDM](/index.php/XDM "XDM")** — X 显示管理器支持XDMCP, host chooser.

[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## 加载显示管理器

通过启动登录管理器（或称显示管理器），即可进行图形界面登录。目前，Arch 提供了 [GDM](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)")、[KDM](/index.php/KDM "KDM")、[SLiM](/index.php/SLiM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SLiM (简体中文)")、[XDM](/index.php/XDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "XDM (简体中文)")、[LXDM](/index.php/LXDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDM (简体中文)")、[LightDM](/index.php/LightDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LightDM (简体中文)") 和 [sddm](https://www.archlinux.org/packages/?name=sddm) 的 systemd 服务文件。以 KDM 为例，配置开机启动：

```
# systemctl enable kdm.service

```

执行上述命令后，登录管理器应当能正常工作了。如果不是的话，很可能是因为你修改了`default.target`。默认情况应当如下：

 `# ls -l /etc/systemd/system/default.target`  `/etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target` 

删除被修改的 `default.target` 即可，systemd 会自动使用默认配置（即 `graphical.target`）：

```
# rm /etc/systemd/system/default.target

```

### 使用 systemd-logind

可使用 `loginctl` 来查看用户会话的状态。所有 [PolicyKit](/index.php/PolicyKit "PolicyKit") 操作，如挂起系统、挂载外部驱动器，都无需配置即可使用。

```
$ loginctl show-session $XDG_SESSION_ID

```

## 疑难解答

### 第二次注销时崩溃

切换到 Systemd 之后，有些显示管理器会在第二次注销时崩溃。需要在配置文件中加入 pam，下面是 sddm 的示例：

 `/etc/pam.d/sddm` 

```
...
session 	required 	pam_systemd.so

```

## 提示和技巧

### 会话列表

Many display managers read available sessions from `/usr/share/xsessions/` directory. It contains standard [desktop entry files](http://standards.freedesktop.org/desktop-entry-spec/latest/) for each DM/WM.

To add/remove entries to your display manager's session list; create/remove the _.desktop_ files in `/usr/share/xsessions/` as desired. A typical _.desktop_ file will look something like:

```
[Desktop Entry]
Encoding=UTF-8
Name=Openbox
Comment=Log in using the Openbox window manager (without a session manager)
Exec=/usr/bin/openbox-session
TryExec=/usr/bin/openbox-session
Icon=openbox.png
Type=XSession

```

### 没有窗口管理启动应用程序

You can also launch an application without any decoration, desktop, or window management. For example to launch [google-chrome](https://aur.archlinux.org/packages/google-chrome/)<sup><small>AUR</small></sup> create a `web-browser.desktop` file in `/usr/share/xsessions/` like this:

```
[Desktop Entry]
Encoding=UTF-8
Name=Web Browser
Comment=Use a web browser as your session
Exec=/usr/bin/google-chrome --auto-launch-at-startup
TryExec=/usr/bin/google-chrome --auto-launch-at-startup
Icon=google-chrome

```

In this case, once you login, the application set with `Exec` will be launched immediately. When you close the application, you will be taken back to the login manager (same as logging out of a normal DE/WM).

It is important to remember that most graphical applications are not intended to be launched this way and you might have manual tweaking to do or limitations to live with (there is no window manager, so do not expect to be able to move or resize _any_ windows, including dialogs; nonetheless, you might be able to set the window geometry in the application's configuration files).

See also [xinitrc#Starting applications without a window manager](/index.php/Xinitrc#Starting_applications_without_a_window_manager "Xinitrc").

### 自动启动

Most of display managers sources `/etc/xprofile`, `~/.xprofile` and `/etc/X11/xinit/xinitrc.d/`. For more details, see [xprofile](/index.php/Xprofile "Xprofile").

### 设置语言

For display manager's that use [AccountsService](http://freedesktop.org/wiki/Software/AccountsService/) the display manager [locale](/index.php/Locale "Locale") can be set by editing `/var/lib/AccountsService/users/$USER`:

```
[User]
Language=_your_locale_

```

where _your_locale_ is a value such as `en_GB.UTF-8`.

Restart your display manager for the changes to take effect.

## 已知问题

### 不兼容在systemd

_Affected DMs: Entrance, MDM_

Some display managers are not fully compatible with systemd, because they reuse the PAM session process. It causes various problems on second login, e.g.:

*   NetworkManager applet does not work,
*   PulseAudio volume cannot be adjusted,
*   login failed into GNOME with another user.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Display_manager_(简体中文)&oldid=412801](https://wiki.archlinux.org/index.php?title=Display_manager_(简体中文)&oldid=412801)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Display managers (简体中文)](/index.php/Category:Display_managers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Display managers (简体中文)")