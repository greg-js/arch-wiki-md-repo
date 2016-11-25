**翻译状态：** 本文是英文页面 [Avant_Window_Navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-11-16，点击[这里](https://wiki.archlinux.org/index.php?title=Avant_Window_Navigator&diff=0&oldid=235592)可以查看翻译后英文页面的改动。

[Avant Window Navigator](https://launchpad.net/awn) (AWN) 是用 C 语言书写的轻量级 dock 程序。它支持启动器、任务列表和第三方 applets。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 可选依赖](#.E5.8F.AF.E9.80.89.E4.BE.9D.E8.B5.96)
    *   [1.2 Compositing](#Compositing)
*   [2 运行 Awn](#.E8.BF.90.E8.A1.8C_Awn)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 外部 applets](#.E5.A4.96.E9.83.A8_applets)
        *   [4.1.1 DockbarX](#DockbarX)
*   [5 更多资源](#.E6.9B.B4.E5.A4.9A.E8.B5.84.E6.BA.90)

## 安装

*   **Avant Window Navigator** 可以通过[官方软件仓库](/index.php/Official_repositories "Official repositories")中的软件包[avant-window-navigator](https://aur.archlinux.org/packages/avant-window-navigator/)进行安装。
*   要得到可选的小应用，需要安装 [awn-extras-applets](https://aur.archlinux.org/packages/awn-extras-applets/)。

### 可选依赖

大多数小应用需要一些额外的包，它们作为可选依赖列出。确保在启用小应用之前安装它们：

| Applet name | Dependencies | Optional dependences |
| animal-farm | [fortune-mod](https://www.archlinux.org/packages/?name=fortune-mod) |
| battery | [upower](https://www.archlinux.org/packages/?name=upower) |
| comics | [python2-feedparser](https://www.archlinux.org/packages/?name=python2-feedparser) [python2-rsvg](https://www.archlinux.org/packages/?name=python2-rsvg) |
| cairo-clock | [python2-rsvg](https://www.archlinux.org/packages/?name=python2-rsvg) | [python2-dateutil](https://www.archlinux.org/packages/?name=python2-dateutil) |
| calendar | [python2-dateutil](https://www.archlinux.org/packages/?name=python2-dateutil) [python2-gdata](https://www.archlinux.org/packages/?name=python2-gdata) [python2-vobject](https://aur.archlinux.org/packages/python2-vobject/) |
| cpufreq | [gnome-applets](https://www.archlinux.org/packages/?name=gnome-applets) |
| dialect | [python-xklavier](https://aur.archlinux.org/packages/python-xklavier/) |
| feeds | [python2-feedparser](https://www.archlinux.org/packages/?name=python2-feedparser) |
| hardware-sensors | [python2-rsvg](https://www.archlinux.org/packages/?name=python2-rsvg) | [hddtemp](https://www.archlinux.org/packages/?name=hddtemp) [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) |
| media-control | [banshee](https://aur.archlinux.org/packages/banshee/) |
| media-player | [gstreamer0.10-python](https://www.archlinux.org/packages/?name=gstreamer0.10-python) |
| mail | [python2-feedparser](https://www.archlinux.org/packages/?name=python2-feedparser) |
| slickswitcher | [python2-wnck](https://www.archlinux.org/packages/?name=python2-wnck) | [python2-gconf](https://www.archlinux.org/packages/?name=python2-gconf) |
| stacks | [python2-libgnome](https://www.archlinux.org/packages/?name=python2-libgnome) [python2-gnomedesktop](https://www.archlinux.org/packages/?name=python2-gnomedesktop) |
| thinkhdaps | [python2-pyinotify](https://www.archlinux.org/packages/?name=python2-pyinotify) |
| tomboy-applet | [tomboy](https://www.archlinux.org/packages/?name=tomboy) |
| volume-control | [gstreamer0.10-python](https://www.archlinux.org/packages/?name=gstreamer0.10-python) |

### Compositing

为了充分利用 Avant Window Navigator及其主题，你需要安装并正确的配置一个支持 composite 的管理器，例如 [Compiz](/index.php/Compiz "Compiz"), [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") 或 [Cairo Compmgr](/index.php/Cairo_Compmgr "Cairo Compmgr") 。如果你在一个桌面环境，如[GNOME](/index.php/GNOME "GNOME"), [Xfce](/index.php/Xfce "Xfce") 或者 [KDE](/index.php/KDE "KDE") 中运行Awn，只需要在系统设置中启用 composite 管理器或者桌面特效即可。 X 中的 [composite](/index.php/Composite "Composite") 选项默认是开启的。

## 运行 Awn

在后台运行 Awn ：

```
$ avant-window-navigator &

```

想要在启动时运行 Awn，运行 Awn, 右键单击，选择 **Dock Preferences > Preferences** 然后选中 **Start Awn automatically**。

也可以添加下面的命令到[自动启动](/index.php/Autostarting#Graphical "Autostarting")文件:

```
`avant-window-navigator --startup &`

```

## 配置

想要配置Awn applet、主题和通用设置，运行：

```
$ awn-settings

```

或者右键点击 dock 选择 **Dock Preferences**.

## 提示与技巧

### 外部 applets

#### DockbarX

你可能想尝试一下 [DockbarX](https://launchpad.net/dockbar)，一个任务管理器 applet ，带有高级行为设置和窗口预览支持。可以通过 [AUR](/index.php/AUR "AUR") 中的软件包 [dockbarx](https://aur.archlinux.org/packages/dockbarx/) 得到.

## 更多资源

*   [Awn wiki](http://wiki.awn-project.org/)
*   [Awn forum](http://awn.planetblur.org/)
*   [Awn launchpad](https://launchpad.net/awn)