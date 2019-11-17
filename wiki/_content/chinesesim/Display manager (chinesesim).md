相关文章

*   [Start X at login](/index.php/Start_X_at_login "Start X at login")

**翻译状态：** 本文是英文页面 [Display_manager](/index.php/Display_manager "Display manager") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-12-28，点击[这里](https://wiki.archlinux.org/index.php?title=Display_manager&diff=0&oldid=413644)可以查看翻译后英文页面的改动。

[显示管理器](https://en.wikipedia.org/wiki/X_display_manager_(program_type) "wikipedia:X display manager (program type)")或登录管理器是一个在启动最后显示的图形界面。和窗口管理器一样，显示管理器有很多种。通常每个显示管理器都能进行一些定制。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 显示管理器列表](#显示管理器列表)
    *   [1.1 控制台](#控制台)
    *   [1.2 图形界面](#图形界面)
*   [2 加载显示管理器](#加载显示管理器)
    *   [2.1 使用 systemd-logind](#使用_systemd-logind)
*   [3 会话配置](#会话配置)
    *   [3.1 运行 ~/.xinitrc 会话](#运行_~/.xinitrc_会话)
    *   [3.2 没有窗口管理启动应用程序](#没有窗口管理启动应用程序)
*   [4 提示和技巧](#提示和技巧)
    *   [4.1 自动启动](#自动启动)
    *   [4.2 设置语言](#设置语言)

## 显示管理器列表

**注意:** 如果使用 [桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)"),应该尽量使用对应的显示管理器。

### 控制台

*   **[CDM](/index.php/CDM "CDM")** — 控制台显示管理器

	[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)

*   **[Console TDM](/index.php/Console_TDM "Console TDM")** — 扩展自xinit，由纯粹的Bash脚本编写的

	[https://github.com/dopsi/console-tdm](https://github.com/dopsi/console-tdm) || [console-tdm](https://aur.archlinux.org/packages/console-tdm/)

*   **[nodm](/index.php/Nodm "Nodm")** — 支持自动登录的简单显示管理器。

	[https://github.com/spanezz/nodm](https://github.com/spanezz/nodm) || [nodm](https://www.archlinux.org/packages/?name=nodm)

*   **[Ly](/index.php/Ly "Ly")** — 实验阶段的 ncurses 显示管理器。

	[https://github.com/cylgom/ly](https://github.com/cylgom/ly) || [ly-git](https://aur.archlinux.org/packages/ly-git/)

### 图形界面

*   [GDM](/index.php/GDM "GDM"): [GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") 显示管理器 。[http://projects.gnome.org/gdm/](http://projects.gnome.org/gdm/)[gdm](https://www.archlinux.org/packages/?name=gdm)
*   [LightDM](/index.php/LightDM "LightDM"):跨桌面的显示管理器，可以使用各种前端写的任何工具。[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM)[lightdm](https://www.archlinux.org/packages/?name=lightdm)||[lightdm-bzr](https://aur.archlinux.org/packages/lightdm-bzr/)
*   [LXDM](/index.php/LXDM "LXDM"): [LXDE](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)") 显示管理器 (独立于桌面环境) ([lxdm](https://www.archlinux.org/packages/?name=lxdm))
*   **MDM** — 使用在Linux Mint中的显示管理器,GDM2的分支项目。

	[https://github.com/linuxmint/mdm](https://github.com/linuxmint/mdm) || [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)

*   [SDDM](/index.php/SDDM "SDDM")：基于QML的显示管理器，替代 KDE4 的 KDM，推荐搭配 Plamsa5 或 LXQt 使用。[https://github.com/sddm/sddm](https://github.com/sddm/sddm)[sddm](https://www.archlinux.org/packages/?name=sddm)
*   **[XDM](/index.php/XDM "XDM")** — X 显示管理器支持XDMCP（适合服务器的宿主机）.

	[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## 加载显示管理器

通过启动登录管理器（或称显示管理器），即可进行图形界面登录。目前，Arch 提供了 [GDM](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)")、[SLiM](/index.php/SLiM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SLiM (简体中文)")、[XDM](/index.php/XDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "XDM (简体中文)")、[LXDM](/index.php/LXDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDM (简体中文)")、[LightDM](/index.php/LightDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LightDM (简体中文)") 和 [sddm](https://www.archlinux.org/packages/?name=sddm) 的 systemd 服务文件。以 [SDDM](/index.php/SDDM "SDDM") 为例，配置开机启动：

```
# systemctl enable sddm.service

```

执行上述命令后，登录管理器应当能正常工作了。如果不是的话，可能是`default.target` 没有指向`graphical.target`。

启用 [SDDM](/index.php/SDDM "SDDM") 后， `/etc/systemd/system/` 应该创建 `display-manager.service` 软链接，可以用 `--force` 覆盖已有链接。

 `$ file /etc/systemd/system/display-manager.service` 
```
/etc/systemd/system/display-manager.service: symbolic link to /usr/lib/systemd/system/sddm.service

```

### 使用 systemd-logind

可使用 `loginctl` 来查看用户会话的状态。所有 [PolicyKit](/index.php/PolicyKit "PolicyKit") 操作，如挂起系统、挂载外部驱动器，都无需配置即可使用。

```
$ loginctl show-session $XDG_SESSION_ID

```

## 会话配置

多数显示管理器会读取 `/usr/share/xsessions/` 目录已获取可用的会话列表，此目录中包含各个 DM/WM 的标准 [桌面文件](https://specifications.freedesktop.org/desktop-entry-spec/latest/)。

要新建会话，可以在 `/usr/share/xsessions/` 中新建 *.desktop* 后缀的文件，文件示例：

```
[Desktop Entry]
Name=Openbox
Comment=Log in using the Openbox window manager (without a session manager)
Exec=/usr/bin/openbox-session
TryExec=/usr/bin/openbox-session
Icon=openbox.png
Type=Application

```

### 运行 ~/.xinitrc 会话

安装 [xinit-xsession](https://aur.archlinux.org/packages/xinit-xsession/) 后会在显示管理器中提供一个运行 .xinitrc 会话的选项。在显示管理器中选择 `xinitrc` 作为会话，请确保 `~/.xinitrc` 具有执行权限。

### 没有窗口管理启动应用程序

您也可以启动没有窗口修饰、桌面或窗口管理器的会话。例如要启动 [google-chrome](https://aur.archlinux.org/packages/google-chrome/)，在`/usr/share/xsessions/`中创建`web-browser.desktop`：

```
[Desktop Entry]
Name=Web Browser
Comment=Use a web browser as your session
Exec=/usr/bin/google-chrome --auto-launch-at-startup
TryExec=/usr/bin/google-chrome --auto-launch-at-startup
Icon=google-chrome
Type=Application

```

登录后，程序会立即执行 `Exec` 中的设定。关闭程序后，会和退出登录一样，将会回到显示管理器。大部分图形程序都不支持此环境，窗口无法移动或改变大小。

参阅 [xinitrc#Starting applications without a window manager](/index.php/Xinitrc#Starting_applications_without_a_window_manager "Xinitrc").

## 提示和技巧

### 自动启动

许多显示管理器都查询配置文件 `/etc/xprofile`, `~/.xprofile` 和`/etc/X11/xinit/xinitrc.d/`。 更多细节，见[xprofile](/index.php/Xprofile "Xprofile")。

### 设置语言

使用[AccountsService](http://freedesktop.org/wiki/Software/AccountsService/)的显示管理器可以设置用户会话的 [locale](/index.php/Locale "Locale")，设置位置是 `/var/lib/AccountsService/users/$USER`:

```
[User]
Language=*your_locale*

```

*your_locale* 位置替换为locale变量,例如: `en_GB.UTF-8`. 重启显示管理器使变更生效。