**翻译状态：** 本文是英文页面 [Xscreensaver](/index.php/Xscreensaver "Xscreensaver") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-02-08，点击[这里](https://wiki.archlinux.org/index.php?title=Xscreensaver&diff=0&oldid=226394)可以查看翻译后英文页面的改动。

Xscreensaver 是 X 窗口系统的屏保和锁屏工具。

## Contents

*   [1 安装XScreenSaver](#.E5.AE.89.E8.A3.85XScreenSaver)
*   [2 配置XScreenSaver](#.E9.85.8D.E7.BD.AEXScreenSaver)
    *   [2.1 DPMS 设置](#DPMS_.E8.AE.BE.E7.BD.AE)
*   [3 启动XScreenSaver](#.E5.90.AF.E5.8A.A8XScreenSaver)
    *   [3.1 单用户环境](#.E5.8D.95.E7.94.A8.E6.88.B7.E7.8E.AF.E5.A2.83)
    *   [3.2 多用户环境](#.E5.A4.9A.E7.94.A8.E6.88.B7.E7.8E.AF.E5.A2.83)
*   [4 锁屏](#.E9.94.81.E5.B1.8F)
*   [5 多媒体程序设置禁用XScreenSaver](#.E5.A4.9A.E5.AA.92.E4.BD.93.E7.A8.8B.E5.BA.8F.E8.AE.BE.E7.BD.AE.E7.A6.81.E7.94.A8XScreenSaver)
    *   [5.1 MPlayer](#MPlayer)
    *   [5.2 XBMC](#XBMC)
    *   [5.3 Adobe Flash/MPlayer/VLC](#Adobe_Flash.2FMPlayer.2FVLC)
*   [6 XScreenSaver用作动态壁纸](#XScreenSaver.E7.94.A8.E4.BD.9C.E5.8A.A8.E6.80.81.E5.A3.81.E7.BA.B8)
    *   [6.1 使用xcompmgr实现XScreenSaver做动态壁纸](#.E4.BD.BF.E7.94.A8xcompmgr.E5.AE.9E.E7.8E.B0XScreenSaver.E5.81.9A.E5.8A.A8.E6.80.81.E5.A3.81.E7.BA.B8)
*   [7 主题设置](#.E4.B8.BB.E9.A2.98.E8.AE.BE.E7.BD.AE)
*   [8 从锁屏画面切换登录用户](#.E4.BB.8E.E9.94.81.E5.B1.8F.E7.94.BB.E9.9D.A2.E5.88.87.E6.8D.A2.E7.99.BB.E5.BD.95.E7.94.A8.E6.88.B7)
    *   [8.1 LXDM](#LXDM)
    *   [8.2 Lightdm](#Lightdm)
*   [9 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 安装XScreenSaver

你可以使用[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")安装位于[软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 的 [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver)软件包.

或者，你可以安装[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")中的一个修改版的xcreensaver（[xscreensaver-arch-logo](https://aur.archlinux.org/packages/xscreensaver-arch-logo/)），安装[xscreensaver-arch-logo](https://aur.archlinux.org/packages/xscreensaver-arch-logo/)相比于前者，有以下几个好处：

1.  因为[makepkg (简体中文)](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")使用源码编译，因此最后得到的软件包会包含针对你机器的优化（前提是你的`/etc/makepkg.conf`中有优化的[CFLAGS](http://wiki.gentoo.org/wiki/Safe_CFLAGS) 和 CXXFLAGS 设置）
2.  该软件包含有Archlinux标识
3.  如果使用的是[GNOME (简体中文)](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)"), 该软件包会在系统设置中提供XScreenSaver的设置项([软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中软件包没有提供)。

## 配置XScreenSaver

全局配置位于`/usr/share/X11/app-defaults/XScreenSaver`。一般标准安装无需编辑该文件。你可以运行xscreensaver-demo个性化配置大部分选项（非全局）。

```
$ xscreensaver-demo

```

### DPMS 设置

XScreenSaver 独立进行显示设备的电源管理 ([DPMS](/index.php/DPMS "DPMS"))，会覆盖 X 本身的设置。要设置挂起、关闭显示器的时间，可以使用 xscreensaver-demo 或编辑配置文件`~/.xscreensaver`,

```
timeout:	1:00:00
cycle:		0:05:00
lock:		False
lockTimeout:	0:00:00
passwdTimeout:	0:00:30
fade:		True
unfade:		False
fadeSeconds:	0:00:03
fadeTicks:	20
dpmsEnabled:	True
dpmsStandby:	2:00:00
dpmsSuspend:	2:00:00
dpmsOff:	4:00:00

```

## 启动XScreenSaver

### 单用户环境

安装软件包之后，xscreensaver需要配置开机自启动。编辑`~/.xinitrc`，加入下面一行代码，这样`xscreensaver`程序就会由桌面环境启动。

```
/usr/bin/xscreensaver -no-splash &

```

注意最后的`&`符号必须添加，这样xscreensaver才会在后台运行。

**注意:** [Xfce](/index.php/Xfce_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xfce (简体中文)")会自启动XScreenSaver，设置在`/etc/xdg/xfce4/xinitrc`，为了保证该设置有效，切记.xinitrc中使用的是 `startxfce4`，而非 `xfce4-session`

```
exec startxfce4

```

### 多用户环境

如果你使用了[登录管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)") (比如 [SLiM](/index.php/SLiM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SLiM (简体中文)"), [GDM](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)"), [KDM](/index.php/KDM "KDM"))，启动XScreenSaver最好是通过登录管理器提供的接口，从而实现多用户之间的切换。例如，使用的是[GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")，则安装 [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver) 和 [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver)，然后仅激活`gnome-screensaver` ，这样当用户离开，屏幕锁定之后，其他用户可以通过XScreenSaver锁屏窗口切换登录。

**注意:** 登录管理器的screensaver可能不具备某些原生XScreenSaver自带功能（例如截屏，使用预定义路径下的照片等）

除了上述办法（即安装登录管理器定制的screensaver）,也可以修改`~/.xscreensaver`（用户设置）或者`/usr/share/X11/app-defaults/XScreenSaver`（全局设置）实现多用户支持。只需要在配置文件中添加：

 `newLoginCommand: /usr/bin/gdmflexiserver` 
**注意:** 该命令用于[GDM](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)")登录管理器，如果使用的是不同的登录管理器，需要对其做相应的更改

## 锁屏

当`xscreensaver`已经启动，你通过下面的命令触发锁屏：

```
$ xscreensaver-command --lock

```

## 多媒体程序设置禁用XScreenSaver

### MPlayer

在`~/.mplayer/config`中加入下面一行代码：

```
heartbeat-cmd="xscreensaver-command -deactivate >&- 2>&- &"

```

### XBMC

XBMC本身并不支持禁用XScreenSaver（尽管XBMC本身具备自己的screensaver）。[AUR](/index.php/Arch_User_Repository "Arch User Repository")中有第三方程序叫做[caffeine-bzr](https://aur.archlinux.org/packages/caffeine-bzr/)的可以实现禁用锁屏的功能。程序启动之后将`xbmc.bin`加入到自动激活应用列表中即可。

### Adobe Flash/MPlayer/VLC

flash本身不支持禁用XScreenSaver，一个叫做[lightsOn](https://github.com/iye/lightsOn)的脚本可以很好的完成这一功能，该脚本支持Firefox、Chromium的flash插件以及Mplayer和VLC。

## XScreenSaver用作动态壁纸

你可以像桌面壁纸一样后台运行`xscreensaver` 首先停止所有控制桌面背景的程序（the root window），之后找到XScreenSaver的目录（通常在`/usr/lib/xscreensaver/`），执行下面的命令：

```
$ /usr/lib/xscreensaver/glslideshow -root &

```

### 使用xcompmgr实现XScreenSaver做动态壁纸

直接运行`xcompmgr`可能会引起错误，所以需要使用`xwinwrap`来运行`xcompmgr`。 你可以在[AUR](/index.php/Arch_User_Repository "Arch User Repository")中找到，名称是[shantz-xwinwrap-bzr](https://aur.archlinux.org/packages/shantz-xwinwrap-bzr/)。

通过下面的命令执行`xwinwrap`

```
$ xwinwrap -b -fs -sp -fs -nf -ov  -- /usr/lib/xscreensaver/glslideshow -root -window-id WID &

```

## 主题设置

XScreenSaver的解锁屏幕可以用[X resources](/index.php/X_resources "X resources")设置主题效果（参考[XScreenSaver resources](/index.php/X_resources#XScreenSaver_resources "X resources")）

## 从锁屏画面切换登录用户

当使用[GDM](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)")或者[KDM](/index.php/KDM "KDM"))登录管理器时，通常xscreensaver锁屏画面中“切换用户”按钮会调用`/usr/bin/gdmflexiserver`来切换登录。其他登录管理器如[LightDM](/index.php/LightDM "LightDM"),[LXDM](/index.php/LXDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDM (简体中文)")也支持该功能。

### LXDM

只需将下面的代码贴到`~/.xscreensaver`就能使用lxdm的切换用户功能。

```
*newLoginCommand: lxdm -c USER_SWITCH

```

### Lightdm

类似地，将下面的代码贴到`~/.xscreensaver`启用多用户切换功能。

```
*newLoginCommand: dm-tool switch-to-greeter

```

## 更多信息

[PanicLock](http://wiki.gotux.net/downloads/paniclock) -- 锁定屏幕并后台关闭任何选定的程序(英文)