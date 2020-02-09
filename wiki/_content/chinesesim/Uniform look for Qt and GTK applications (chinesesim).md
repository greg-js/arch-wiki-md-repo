<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 介绍](#介绍)
*   [2 Qt和GTK的样式](#Qt和GTK的样式)
    *   [2.1 Breeze](#Breeze)
    *   [2.2 Adwaita](#Adwaita)
    *   [2.3 Kvantum](#Kvantum)
*   [3 主题引擎](#主题引擎)
    *   [3.1 QGtkStyle](#QGtkStyle)
    *   [3.2 QGnomePlatform](#QGnomePlatform)
*   [4 其它策略](#其它策略)
    *   [4.1 GTK2程序拥有KDE的文件对话框](#GTK2程序拥有KDE的文件对话框)
*   [5 问题解决](#问题解决)
    *   [5.1 怎样为每一个工具设置风格?](#怎样为每一个工具设置风格?)
        *   [5.1.1 KDE3 和 QT3 风格](#KDE3_和_QT3_风格)
        *   [5.1.2 QT4 风格](#QT4_风格)
        *   [5.1.3 GTK2 风格](#GTK2_风格)
        *   [5.1.4 GTK1 风格](#GTK1_风格)
    *   [5.2 主题不作用于GTK程序](#主题不作用于GTK程序)
    *   [5.3 系统升级后GTK应用程序不使用svg（breeze）图标](#系统升级后GTK应用程序不使用svg（breeze）图标)
    *   [5.4 Flatpak Qt应用程序不使用Gnome Adwaita黑暗主题](#Flatpak_Qt应用程序不使用Gnome_Adwaita黑暗主题)

## 介绍

基于[Qt](https://en.wikipedia.org/wiki/Qt_(toolkit) 和 [GTK+](/index.php/GTK%2B "GTK+")的程序使用不同的工具包来渲染图形化用户界面，各自带有不同的主题、风格和图标，所以观感就明显有所不同。这篇文章将帮助你体验让你的Qt和GTK+程序看起来更现代化、集成化的桌面。

*   **主题** - 包含一套风格、图标主题和颜色主题。
*   **风格** - 图形布置，观感。
*   **图标主题** - 一套整体的图标。
*   **颜色主题** - 一套连接风格的整体配色。

你可以有多种选择：

*   使用下面列出的每个工具箱中的工具分别修改[GTK and Qt styles](#Styles_for_both_Qt_and_GTK)，以选择外观相似的主题（样式，颜色，图标，光标，字体）。
*   使用特殊的[theme engine](#Theme_engines)，该引擎将对其他图形工具箱的修改作为中介，以匹配您的主要工具箱。

## Qt和GTK的样式

There are widget style sets available for the purpose of integration, where builds are written and provided for both Qt and GTK, all major versions included. With these, you can have one look for all applications regardless of the toolkit they had been written with.

**Tip:** 你可能希望将用户定义的样式应用于root用户的应用, 参考[GTK#Theme not applied to root applications](/index.php/GTK#Theme_not_applied_to_root_applications "GTK") and [Qt#Theme not applied to root applications](/index.php/Qt#Theme_not_applied_to_root_applications "Qt").

**Note:** 从3.16版本开始, GTK 3 [不再支持](https://bbs.archlinux.org/viewtopic.php?pid=1518404#p1518404) non-CSS 主题, 因此，以前的解决方案（例如Oxygen-Gtk）不再是可行的选择，参考[[1]](https://bugs.kde.org/show_bug.cgi?id=340288)。

### Breeze

Breeze是KDE Plasma的默认Qt样式。它可以与Qt5的[breeze](https://www.archlinux.org/packages/?name=breeze)，Qt4的[breeze-kde4](https://aur.archlinux.org/packages/breeze-kde4/)以及GTK 2和GTK 3的[breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk)软件包一起安装。

安装后，您可以挑选[GTK配置工具](/index.php/GTK#Configuration_tools "GTK")更改GTK主题。

如果当前运行的是KDE Plasma，请安装[kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)并从命令行运行它，或转到“系统设置>应用程序样式>GNOME应用程序样式（GTK）”进行GTK程序的样式配置。在GTK样式配置模块之外的“系统设置”中设置的字体，图标主题，光标和小部件样式将仅影响Qt。应该使用前面提到的模块手动设置GTK设置。

### Adwaita

Adwaita是默认的GNOME主题。GTK 3版本包含在[gtk3](https://www.archlinux.org/packages/?name=gtk3)软件包中，而GTK 2版本包含在[gnome-themes-extra](https://www.archlinux.org/packages/?name=gnome-themes-extra)中。 [adwaita-qt](https://github.com/MartinBriza/adwaita-qt)是Adwaita主题的Qt接口。与模仿GTK 2主题的[#QGtkStyle](#QGtkStyle)不同，它提供了本机Qt样式，使其看起来像GTK 3 Adwaita。可以分别安装Qt 4 [adwaita-qt4](https://aur.archlinux.org/packages/adwaita-qt4/)和Qt5[adwaita-qt](https://aur.archlinux.org/packages/adwaita-qt/)版本的软件包。

要将Qt样式设置为默认值：

*   对于Qt4，可以使用*Qt配置*(`qtconfig-qt4`)启用它，在*外观>GUI样式*中选择*adwaita*。或者，编辑`/etc/xdg/Trolltech.conf`（系统范围）或`~/.config/Trolltech.conf`（用户特定）文件：

 `~/.config/Trolltech.conf` 
```
...
[Qt]
style=adwaita
...
```

*   对于Qt 5，可以通过启用以下[环境变量](/index.php/Environment_variables#Graphical_environment "Environment variables")：`QT_STYLE_OVERRIDE=adwaita`。或者，使用[qt5ct](https://www.archlinux.org/packages/?name=qt5ct)软件包。更多详细说明，参考[Qt#Configuration of Qt5 apps under environments other than KDE Plasma](/index.php/Qt#Configuration_of_Qt5_apps_under_environments_other_than_KDE_Plasma "Qt")。

### Kvantum

Kvantum([kvantum-qt5](https://www.archlinux.org/packages/?name=kvantum-qt5))是用于Qt5的可定制的基于SVG的主题引擎，具有多种内置样式，包括一些流行的GTK主题的版本，例如Adapta，Arc，Ambiance和Materia。

## 主题引擎

主题引擎可以认为是从一个或多个工具翻译主题（图标除外）很小的API层。这些引擎为进程添加额外的代码，这种解决方案不是非常精致更多为本来风格优化。

### QGtkStyle

**注意:** QGtkStyle已从[qt5-base](https://www.archlinux.org/packages/?name=qt5-base)中删除 5.7.0 [[2]](https://github.com/qtproject/qtbase/commit/899a815414e95da8d9429a4a4f4d7094e49cfc55)现已添加到[qt5-styleplugins](https://www.archlinux.org/packages/?name=qt5-styleplugins)中[[3]](https://github.com/qtproject/qtstyleplugins/commit/102da7d50231fc5723dba6e72340bef3d29471aa)。

**Warning:** 根据GTK 2主题，此样式可能会导致呈现问题，例如透明字体或小部件不一致。

此Qt样式使用GTK 2渲染所有组件以便于与[GNOME](/index.php/GNOME "GNOME")和类似基于GTK的环境相协调。从Qt 4.5开始，此样式包含在Qt中。它要求安装[gtk2](https://www.archlinux.org/packages/?name=gtk2)并进行配置。

这是Cinnamon，GNOME和Xfce中的默认Qt4样式，也是Cinnamon，GNOME，MATE，LXDE和Xfce中的默认Qt5样式。在其他环境中：

*   For Qt4, it can be enabled with *Qt Configuration* (`qtconfig-qt4`), choose *GTK* under *Appearance > GUI Style*. Alternatively, edit the `/etc/xdg/Trolltech.conf` (system-wide) or `~/.config/Trolltech.conf` (user-specific) file:
*   对于Qt4，可以使用*Qt配置*(`qtconfig-qt4`)启用它，在*外观>GUI样式* 下选择*GTK*。或者，编辑 `/etc/xdg/Trolltech.conf`（系统范围）或`~/.config/Trolltech.conf`（用户特定）文件：

 `~/.config/Trolltech.conf` 
```
...
[Qt]
style=GTK+
...
```

*   对于Qt 5，可以通过安装[qt5-styleplugins](https://www.archlinux.org/packages/?name=qt5-styleplugins)并设置以下[环境变量](/index.php?title=Environment_variables%EF%BC%83Graphical_environment&action=edit&redlink=1 "Environment variables＃Graphical environment (page does not exist)")来启用它：`QT_QPA_PLATFORMTHEME=gtk2`

为了完全统一，请确保配置的[GTK主题](/index.php/GTK#Themes "GTK")同时支持GTK 2和GTK3。如果将Qt配置为使用GTK2后导致首选主题渲染不一致，请安装[gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)，然后选择一个主题。

### QGnomePlatform

Qt 5平台主题适用于Qt应用程序的GNOME外观设置。它可以与[qgnomeplatform](https://aur.archlinux.org/packages/qgnomeplatform/)软件包一起安装，也可以与开发版本的[qgnomeplatform-git](https://aur.archlinux.org/packages/qgnomeplatform-git/)软件包一起安装。它本身不提供Qt样式，而是需要[同时支持Qt and GTK样式](#Styles_for_both_Qt_and_GTK)。

从3.20版开始，此平台主题已在GNOME中自动启用。对于其他系统，可以通过设置以下[environment variable](/index.php/Environment_variables#Graphical_environment "Environment variables")来启用它：`QT_QPA_PLATFORMTHEME=qgnomeplatform`.。

## 其它策略

### GTK2程序拥有KDE的文件对话框

KGtk 是一个包装脚本以 LD_PRELOAD来强制GTK2程序为 KDE 文件对话框 (打开、保存等等）。如果你使用KDE环境且比较喜欢用它的文件对话框，可以从AUR安装kgtk来覆盖GTK程序. 安装后你可以用2种方法使GTK2程序运行kgtk-wrapper(以gimp为例).

直接打开kgtk-wrapper且以GTK2二进制包作为一个参数

```
/usr/local/bin/kgtk-wrapper gimp

```

或

创建一个符号链接到将kgtk链接到二进制GTK2程序，然后你可以运行/usr/local/bin/gimp 来使gimp拥有KDE对话框的。

```
ln -s /usr/local/bin/kgtk-wrapper /usr/local/bin/gimp
/usr/local/bin/gimp

```

## 问题解决

### 怎样为每一个工具设置风格?

你可以在各种桌面环境用以下方式改变主题文件。

#### KDE3 和 QT3 风格

*   Control Center (kcontrol) --> Appearance & Themes --> Style --> Widget Style
*   kde-config --style [name of style]
*   /opt/qt/bin/qtconfig

#### QT4 风格

*   /usr/bin/qtconfig

#### GTK2 风格

*   gtk-chtheme
*   gtk2_prefs
*   switch2 (gtk-theme-switch2 package)

#### GTK1 风格

*   switch (gtk-theme-switch package)

### 主题不作用于GTK程序

如果你安装的风格或主题引擎在某些GTK程序不能显示，很可能你的GTK设置文件因某些原因不能被加载。你可以检查你的系统找到那些文件作如下设置：

```
export | grep gtk

```

通常那些文件设置在 ~/.gtkrc （GTK1）, ~/.gtkrc2.0 或 ~/.gtkrc2.0-kde （GTK2）

新版gtk-qt-engine 使用 ~/.gtkrc2.0-kde 和 ~/.kde/env/gtk-qt-engine.rc.sh 设置输出变量 如果你最近移除了gtk-qt-engine然后试图设置GTK主题，你必有要移除 ~/.kde/env/gtk-qt-engine.rc.sh 然后重启。这样做会使GTK外观使用标准的设置 ~/.gtkrc2.0来代替 ~/.gtkrc2.0-kde

### 系统升级后GTK应用程序不使用svg（breeze）图标

尝试运行下面命令来解决问题：

```
# gdk-pixbuf-query-loaders --update-cache

```

### Flatpak Qt应用程序不使用Gnome Adwaita黑暗主题

如果将主题切换为Adwaita-dark后，Flatpak Qt应用程序仍使用精简版，请安装所需的KStyle：

```
# flatpak install flathub org.kde.KStyle.Adwaita

```