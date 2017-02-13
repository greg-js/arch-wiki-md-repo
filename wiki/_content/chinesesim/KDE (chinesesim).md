**翻译状态：** 本文是英文页面 [KDE](/index.php/KDE "KDE") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-22，点击[这里](https://wiki.archlinux.org/index.php?title=KDE&diff=0&oldid=447056)可以查看翻译后英文页面的改动。

KDE 软件集是由 Plasma [桌面环境](/index.php/Desktop_environment "Desktop environment")、支持库和框架 (KDE Frameworks)、和应用组成。KDE 上游维护了一份 [UserBase Wiki](http://userbase.kde.org/)。用户能在那里找到大部分 KDE 应用的详细信息。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 Plasma 桌面](#Plasma_.E6.A1.8C.E9.9D.A2)
    *   [1.2 升级KDE 4到Plasma 5](#.E5.8D.87.E7.BA.A7KDE_4.E5.88.B0Plasma_5)
    *   [1.3 KDE 应用和语言包](#KDE_.E5.BA.94.E7.94.A8.E5.92.8C.E8.AF.AD.E8.A8.80.E5.8C.85)
*   [2 启动 Plasma](#.E5.90.AF.E5.8A.A8_Plasma)
    *   [2.1 Wayland](#Wayland)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 主题](#.E4.B8.BB.E9.A2.98)
    *   [3.2 Qt 和 GTK+ 应用外观](#Qt_.E5.92.8C_GTK.2B_.E5.BA.94.E7.94.A8.E5.A4.96.E8.A7.82)
    *   [3.3 小工具](#.E5.B0.8F.E5.B7.A5.E5.85.B7)
    *   [3.4 系统托盘中的声音应用](#.E7.B3.BB.E7.BB.9F.E6.89.98.E7.9B.98.E4.B8.AD.E7.9A.84.E5.A3.B0.E9.9F.B3.E5.BA.94.E7.94.A8)
    *   [3.5 窗口装饰](#.E7.AA.97.E5.8F.A3.E8.A3.85.E9.A5.B0)
    *   [3.6 图标主题](#.E5.9B.BE.E6.A0.87.E4.B8.BB.E9.A2.98)
    *   [3.7 字体](#.E5.AD.97.E4.BD.93)
        *   [3.7.1 字体太大或变形](#.E5.AD.97.E4.BD.93.E5.A4.AA.E5.A4.A7.E6.88.96.E5.8F.98.E5.BD.A2)
    *   [3.8 网络](#.E7.BD.91.E7.BB.9C)
    *   [3.9 打印](#.E6.89.93.E5.8D.B0)
    *   [3.10 Samba/Windows 的支持](#Samba.2FWindows_.E7.9A.84.E6.94.AF.E6.8C.81)
    *   [3.11 KDE 桌面活动](#KDE_.E6.A1.8C.E9.9D.A2.E6.B4.BB.E5.8A.A8)
    *   [3.12 节能](#.E8.8A.82.E8.83.BD)
    *   [3.13 监视本地文件和目录的变化](#.E7.9B.91.E8.A7.86.E6.9C.AC.E5.9C.B0.E6.96.87.E4.BB.B6.E5.92.8C.E7.9B.AE.E5.BD.95.E7.9A.84.E5.8F.98.E5.8C.96)
    *   [3.14 程序自启动](#.E7.A8.8B.E5.BA.8F.E8.87.AA.E5.90.AF.E5.8A.A8)
*   [4 系统管理](#.E7.B3.BB.E7.BB.9F.E7.AE.A1.E7.90.86)
    *   [4.1 KDE 系统设置中配置终止 Xorg-server](#KDE_.E7.B3.BB.E7.BB.9F.E8.AE.BE.E7.BD.AE.E4.B8.AD.E9.85.8D.E7.BD.AE.E7.BB.88.E6.AD.A2_Xorg-server)
    *   [4.2 KCM](#KCM)
*   [5 桌面搜索](#.E6.A1.8C.E9.9D.A2.E6.90.9C.E7.B4.A2)
    *   [5.1 Baloo](#Baloo)
    *   [5.2 Web 浏览器](#Web_.E6.B5.8F.E8.A7.88.E5.99.A8)
        *   [5.2.1 Konqueuor 和 Rekonq](#Konqueuor_.E5.92.8C_Rekonq)
        *   [5.2.2 Firefox](#Firefox)
        *   [5.2.3 Qupzilla](#Qupzilla)
*   [6 PIM](#PIM)
    *   [6.1 Akonadi](#Akonadi)
        *   [6.1.1 运行不含 Akonadi 的 KDE](#.E8.BF.90.E8.A1.8C.E4.B8.8D.E5.90.AB_Akonadi_.E7.9A.84_KDE)
        *   [6.1.2 禁用 Akonadi](#.E7.A6.81.E7.94.A8_Akonadi)
        *   [6.1.3 配置数据库](#.E9.85.8D.E7.BD.AE.E6.95.B0.E6.8D.AE.E5.BA.93)
*   [7 Phonon](#Phonon)
    *   [7.1 Phonon 是什么？](#Phonon_.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
    *   [7.2 我应该选择哪个后端？](#.E6.88.91.E5.BA.94.E8.AF.A5.E9.80.89.E6.8B.A9.E5.93.AA.E4.B8.AA.E5.90.8E.E7.AB.AF.EF.BC.9F)
*   [8 常用的应用](#.E5.B8.B8.E7.94.A8.E7.9A.84.E5.BA.94.E7.94.A8)
    *   [8.1 Yakuake](#Yakuake)
    *   [8.2 KDE Telepathy](#KDE_Telepathy)
        *   [8.2.1 Use Telegram with KDE Telepathy](#Use_Telegram_with_KDE_Telepathy)
*   [9 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [9.1 使用其他窗口管理器](#.E4.BD.BF.E7.94.A8.E5.85.B6.E4.BB.96.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
        *   [9.1.1 KDE/Openbox 会话](#KDE.2FOpenbox_.E4.BC.9A.E8.AF.9D)
        *   [9.1.2 Compiz 设置](#Compiz_.E8.AE.BE.E7.BD.AE)
        *   [9.1.3 Re-enabling compositing effects](#Re-enabling_compositing_effects)
    *   [9.2 Integrate Android](#Integrate_Android)
    *   [9.3 获取软件包更新提醒](#.E8.8E.B7.E5.8F.96.E8.BD.AF.E4.BB.B6.E5.8C.85.E6.9B.B4.E6.96.B0.E6.8F.90.E9.86.92)
    *   [9.4 配置 KWin 成使用 OpenGL ES](#.E9.85.8D.E7.BD.AE_KWin_.E6.88.90.E4.BD.BF.E7.94.A8_OpenGL_ES)
    *   [9.5 Konqueror/Dolphin 文件管理器中开启视频缩略图](#Konqueror.2FDolphin_.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8.E4.B8.AD.E5.BC.80.E5.90.AF.E8.A7.86.E9.A2.91.E7.BC.A9.E7.95.A5.E5.9B.BE)
    *   [9.6 加速应用启动](#.E5.8A.A0.E9.80.9F.E5.BA.94.E7.94.A8.E5.90.AF.E5.8A.A8)
    *   [9.7 显示器分辨率 / 多显示器配置](#.E6.98.BE.E7.A4.BA.E5.99.A8.E5.88.86.E8.BE.A8.E7.8E.87_.2F_.E5.A4.9A.E6.98.BE.E7.A4.BA.E5.99.A8.E9.85.8D.E7.BD.AE)
    *   [9.8 Open application launcher with Super key (Windows key)](#Open_application_launcher_with_Super_key_.28Windows_key.29)
*   [10 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [10.1 Plasma 在 Intel 显卡上崩溃](#Plasma_.E5.9C.A8_Intel_.E6.98.BE.E5.8D.A1.E4.B8.8A.E5.B4.A9.E6.BA.83)
    *   [10.2 有关配置的问题](#.E6.9C.89.E5.85.B3.E9.85.8D.E7.BD.AE.E7.9A.84.E9.97.AE.E9.A2.98)
        *   [10.2.1 Plasma 桌面行为异常](#Plasma_.E6.A1.8C.E9.9D.A2.E8.A1.8C.E4.B8.BA.E5.BC.82.E5.B8.B8)
        *   [10.2.2 清理缓存以解决升级故障](#.E6.B8.85.E7.90.86.E7.BC.93.E5.AD.98.E4.BB.A5.E8.A7.A3.E5.86.B3.E5.8D.87.E7.BA.A7.E6.95.85.E9.9A.9C)
        *   [10.2.3 清理 akonadi 配置来修复 kmail](#.E6.B8.85.E7.90.86_akonadi_.E9.85.8D.E7.BD.AE.E6.9D.A5.E4.BF.AE.E5.A4.8D_kmail)
    *   [10.3 Fix empty IMAP inbox](#Fix_empty_IMAP_inbox)
    *   [10.4 为了支持和调试获取 KWin 的当前状况](#.E4.B8.BA.E4.BA.86.E6.94.AF.E6.8C.81.E5.92.8C.E8.B0.83.E8.AF.95.E8.8E.B7.E5.8F.96_KWin_.E7.9A.84.E5.BD.93.E5.89.8D.E7.8A.B6.E5.86.B5)
    *   [10.5 KDE 和 Qt 程序在别的窗口管理器下很难看](#KDE_.E5.92.8C_Qt_.E7.A8.8B.E5.BA.8F.E5.9C.A8.E5.88.AB.E7.9A.84.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8.E4.B8.8B.E5.BE.88.E9.9A.BE.E7.9C.8B)
    *   [10.6 KF5/Qt5 应用在 i3/fvwm/awesome 中不显示图标](#KF5.2FQt5_.E5.BA.94.E7.94.A8.E5.9C.A8_i3.2Ffvwm.2Fawesome_.E4.B8.AD.E4.B8.8D.E6.98.BE.E7.A4.BA.E5.9B.BE.E6.A0.87)
    *   [10.7 有关图形的故障](#.E6.9C.89.E5.85.B3.E5.9B.BE.E5.BD.A2.E7.9A.84.E6.95.85.E9.9A.9C)
        *   [10.7.1 Plasma keeps crashing with legacy Nvidia](#Plasma_keeps_crashing_with_legacy_Nvidia)
        *   [10.7.2 Applications don't refresh properly](#Applications_don.27t_refresh_properly)
        *   [10.7.3 2D 桌面性能差（或）出现残影](#2D_.E6.A1.8C.E9.9D.A2.E6.80.A7.E8.83.BD.E5.B7.AE.EF.BC.88.E6.88.96.EF.BC.89.E5.87.BA.E7.8E.B0.E6.AE.8B.E5.BD.B1)
            *   [10.7.3.1 GPU 驱动程序问题](#GPU_.E9.A9.B1.E5.8A.A8.E7.A8.8B.E5.BA.8F.E9.97.AE.E9.A2.98)
            *   [10.7.3.2 使用 Raster 引擎跳过问题](#.E4.BD.BF.E7.94.A8_Raster_.E5.BC.95.E6.93.8E.E8.B7.B3.E8.BF.87.E9.97.AE.E9.A2.98)
        *   [10.7.4 3D 桌面性能差](#3D_.E6.A1.8C.E9.9D.A2.E6.80.A7.E8.83.BD.E5.B7.AE)
        *   [10.7.5 有 Nvidia GPU 的系统中桌面混成被禁用](#.E6.9C.89_Nvidia_GPU_.E7.9A.84.E7.B3.BB.E7.BB.9F.E4.B8.AD.E6.A1.8C.E9.9D.A2.E6.B7.B7.E6.88.90.E8.A2.AB.E7.A6.81.E7.94.A8)
        *   [10.7.6 启用混成后全屏时闪烁](#.E5.90.AF.E7.94.A8.E6.B7.B7.E6.88.90.E5.90.8E.E5.85.A8.E5.B1.8F.E6.97.B6.E9.97.AA.E7.83.81)
        *   [10.7.7 Display settings lost on reboot (multiple monitors)](#Display_settings_lost_on_reboot_.28multiple_monitors.29)
    *   [10.8 KDE 下的声音问题](#KDE_.E4.B8.8B.E7.9A.84.E5.A3.B0.E9.9F.B3.E9.97.AE.E9.A2.98)
        *   [10.8.1 ALSA 相关的问题](#ALSA_.E7.9B.B8.E5.85.B3.E7.9A.84.E9.97.AE.E9.A2.98)
            *   [10.8.1.1 尝试在 KDE 中播放任何声音时出现 "返回 default" 消息](#.E5.B0.9D.E8.AF.95.E5.9C.A8_KDE_.E4.B8.AD.E6.92.AD.E6.94.BE.E4.BB.BB.E4.BD.95.E5.A3.B0.E9.9F.B3.E6.97.B6.E5.87.BA.E7.8E.B0_.22.E8.BF.94.E5.9B.9E_default.22_.E6.B6.88.E6.81.AF)
            *   [10.8.1.2 使用 GStreamer Phonon 后端时不能播放 MP3 文件](#.E4.BD.BF.E7.94.A8_GStreamer_Phonon_.E5.90.8E.E7.AB.AF.E6.97.B6.E4.B8.8D.E8.83.BD.E6.92.AD.E6.94.BE_MP3_.E6.96.87.E4.BB.B6)
    *   [10.9 Konsole 不保存命令历史](#Konsole_.E4.B8.8D.E4.BF.9D.E5.AD.98.E5.91.BD.E4.BB.A4.E5.8E.86.E5.8F.B2)
    *   [10.10 Inotify 文件夹监控上限](#Inotify_.E6.96.87.E4.BB.B6.E5.A4.B9.E7.9B.91.E6.8E.A7.E4.B8.8A.E9.99.90)
    *   [10.11 自动挂载NFS卷时卡死](#.E8.87.AA.E5.8A.A8.E6.8C.82.E8.BD.BDNFS.E5.8D.B7.E6.97.B6.E5.8D.A1.E6.AD.BB)
    *   [10.12 Locale warning when installing packages in Konsole](#Locale_warning_when_installing_packages_in_Konsole)
    *   [10.13 多显示器问题](#.E5.A4.9A.E6.98.BE.E7.A4.BA.E5.99.A8.E9.97.AE.E9.A2.98)
*   [11 不稳定版本](#.E4.B8.8D.E7.A8.B3.E5.AE.9A.E7.89.88.E6.9C.AC)
*   [12 Trinity](#Trinity)
*   [13 缺陷](#.E7.BC.BA.E9.99.B7)
*   [14 参见](#.E5.8F.82.E8.A7.81)

## 安装

### Plasma 桌面

Plasma 4 已经停止维护，而且不能和 Plasma 5 同时安装。

在安装Plasma之前，请确保[Xorg](/index.php/Xorg "Xorg")已经被安装到您的系统中

安装基础包 [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) 或者 完整的[plasma](https://www.archlinux.org/groups/x86_64/plasma/)。 关于 [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) 和 [plasma](https://www.archlinux.org/groups/x86_64/plasma/)两者的不同请参阅这里 [KDE Packages](/index.php/KDE_Packages "KDE Packages")。如果想要最小化安装Plasma，可以安装 [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) 包。

### 升级KDE 4到Plasma 5

1.  隔离 `multi-user.target` `# systemctl isolate multi-user.target` 
2.  [卸载](/index.php/Pacman "Pacman") kdebase-workspace 软件包 `# pacman -Rc kdebase-workspace` 
3.  [安装](/index.php/Pacman "Pacman") 软件包组[plasma](https://www.archlinux.org/groups/x86_64/plasma/),或者只安装[plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta)软件包.
4.  停用KDM(如果你在使用的话) `# systemctl disable kdm` 然后安装[SDDM](/index.php/SDDM "SDDM") `# systemctl enable sddm` 或其他的 [显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器").
5.  重新启动或 [启动](/index.php/Start "Start") `sddm.service`.

**Note:** Plasma 4 设置并不会自动合并到Plasma 5,所以你要从桌面重新设置.

### KDE 应用和语言包

你能够通过安装[kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/)或者安装[kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta)基础包具体模块来安装全部的KDE Applications（应用）。请注意这仅仅安装applications（应用），并没有安装 Plasma 桌面。

如果你需要语言文件，你需要安装语言包`kde-l10n-**yourlanguagehere**` (e.g. [kde-l10n-zh_cn](https://www.archlinux.org/packages/?name=kde-l10n-zh_cn) 。你可以在这里[this link](https://www.archlinux.org/packages/extra/any/kde-l10n/)查阅所有可用的语言)

## 启动 Plasma

**Tip:**

*   Plasma 5不支持 [KDM](/index.php/KDM "KDM"). KDE 团队 [recommends](http://blog.davidedmundson.co.uk/blog/display_managers_finale)推荐使用 [SDDM](/index.php/SDDM "SDDM") 显示管理，因为它和Plasma 5桌面主题能够很好的整合。
*   推荐编辑`/etc/sddm.conf`使用微风主题，这样能够更好的和Plasma5整合。 参考 [SDDM#Theme settings](/index.php/SDDM#Theme_settings "SDDM")

在你的 [display manager](/index.php/Display_manager "Display manager") 菜单选择“Plasma”启动 Plasma 5 会话 。

你也可以在你的`.xinitrc`文件中添加`exec startkde`，用“startx”来启动 Plasma 桌面。如果你想在登录的时候开启 Xorg 请参考[Start X at login](/index.php/Start_X_at_login "Start X at login").

### Wayland

Plasma 5.6 已经可以在 [Wayland](/index.php/Wayland "Wayland") 上使用，但是有一些问题存在。[[1]](https://blog.martin-graesslin.com/blog/2016/03/february-kwinwayland-update-all-about-input/) 多屏幕支持还有问题.

*   要从显示管理器启动 Plasma Wayland 会话，安装软件包 [plasma-wayland-session](https://www.archlinux.org/packages/?name=plasma-wayland-session)，Wayland 会话会出现在显示管理器中。
*   要从终端启动 Plasma Wayland 会话，执行 `startplasmacompositor`.

## 配置

大部分配置现在位于标准的`~/.config`目录，有些程序还在使用 `~/.kde4` 目录。KDE的配置主要在**“系统设置”**里完成，可以通过 systemsettings5 启动。

其他没有包含在下文中的个性化设置如活动、桌面立方体上的不同壁纸等，请参考[Plasma](/index.php/Plasma "Plasma")的wiki页面。

### 主题

[Plasma 主题](http://kde-look.org/index.php?xcontentmode=76)定义面板和 Plasma 看起来的样子。官方资料库和 [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go) 提供了很多主题，这样你就能够很简单的安装它。

通过桌面设置控制面板来安装主题是最简单的方法了：

```
 Workspace Theme > Desktop Theme > Get new Themes

```

如果你安装，卸载，或者简单的点击一下更新第三方 Plasma 脚本，这都将为 [kde-look.org](http://www.kde-look.org/) 呈现出一个更好的前端。

### Qt 和 GTK+ 应用外观

**提示：** 为了 Qt 和 GTK 主题的一致性，请参见 [外观统一的 QT 和 GTK 应用](/index.php?title=%E5%A4%96%E8%A7%82%E7%BB%9F%E4%B8%80%E7%9A%84_QT_%E5%92%8C_GTK_%E5%BA%94%E7%94%A8&action=edit&redlink=1 "外观统一的 QT 和 GTK 应用 (page does not exist)")。

	Qt4

对于有一个一致的外观的Qt4应用程序，您需要安装[breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4)，然后从{ { IC | qtconfig - Qt4的} }中挑选微风作为图形用户界面风格。

	GTK+

目前 GTK 中没有 breeze-based 主题。在 GTK 中推荐外形美观的主题是[gtk-theme-orion](https://aur.archlinux.org/packages/gtk-theme-orion/)。安装然后在 System Settings / Application Style / GNOME Application Style 中选 Orion 作为 GTK2 and GTK3 主题。

### 小工具

Plasmoid包含短的脚本（plasmoid scripts）或者编译过的（plasmoid binaries）的KDE应用程序，用于增强桌面的功能。 Plasmoid二进制文件可以从[AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v)上获得的PKGBUILD安装，或者您可以编写自己的PKGBUILD。 最简单的安装Plasmoid脚本的方式是右击面板或桌面：

```
添加部件 > 获得新部件 > 下载新 Plasma 部件

```

将显示 [kde-look.org](http://www.kde-look.org/) 的前端界面，一键就可以安装/卸载/更新三方 plasmoid 脚本。

大部分 plasmoids 都不是 KDE 正式开发者发布。此外还可以安装 Mac OS X 部件、Microsoft Windows Vista/7 部件、Google 部件甚至 SuperKaramba 部件。

### 系统托盘中的声音应用

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa) 或 [kmix](https://www.archlinux.org/packages/?name=kmix) (从程序启动器启动 Kmix)

**Note:** 要调整 [音量增减的步长](https://bugs.kde.org/show_bug.cgi?id=313579#c28)，将诸如 `VolumePercentageStep=1` 一行添加到 `~/.kde4/share/config/kmixrc` 的 `[Global]` 一节中。

### 窗口装饰

[窗口装饰](http://kde-look.org/index.php?xcontentmode=75)可以在

```
系统设置 > 应用程序外观 > 风格

```

中设置。 您也可以在此处点击一下直接下载并安装更多的主题，一些主题可以在[AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v)上找到。

### 图标主题

安装的图标可以在 *System Settings > Icons* 中找到.

### 字体

尝试安装 [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) 和 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 软件包。

安装后，确保注销并重新登录。不需要修改*系统设置 > 应用程序外观 > 字体*里的设置。

如果您个人已经设置了[字体](/index.php/Fonts "Fonts")渲染，小心系统设置可能会改变它们的外观。当改变了*系统设置 > 应用程序外观 > 字体*里的设置，系统将可能改写字体配置文件(`fonts.conf`)。

没有办法避免这种情况，但是如果把数值调到了匹配 `fonts.conf` 文件的话，所期望的字体渲染效果将会重新出现（这需要重启您的应用程序，在某些情况下可能需要重启桌面环境）。注意 Gnome 中的字体设置也会有这样的效果。

#### 字体太大或变形

从 *系统设置 > 应用程序外观 > 字体* 将字体 DPI 强制设置为 **96**

如果还是不行请尝试直接通过 Xorg 配置文件设置 DPI。[参见这里](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Setting_DPI_manually "Xorg (简体中文)").

### 网络

你可以从以下工具中选择：

*   NetworkManager 。更多信息请参见 [NetworkManager](/index.php/NetworkManager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#KDE_4 "NetworkManager (简体中文)")。
*   Wicd。更多信息请参见 [Wicd](/index.php/Wicd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wicd (简体中文)")。

### 打印

**提示：** 使用 [CUPS](/index.php/CUPS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "CUPS (简体中文)") 的 Web 接口进行快速配置。这种方式配置的打印机可以被 KDE 应用使用。

你也可以在 **系统设置 > 打印机配置** 中配置打印机。要使用这种配置方式，必须首先安装 [kdeutils-print-manager](https://www.archlinux.org/packages/?name=kdeutils-print-manager) 和 [cups](https://www.archlinux.org/packages/?name=cups) 软件包。

avahi-daemon 和 cupsd 守护进程必须事先启动，否则，你将看到下面的错误信息：

 `服务“打印机配置”没有提供带有关键字 “system-config-printer-kde/system-config-printer-kde.py” 的接口 “KCModule” 工厂不支持创建指定类型的组件。` 

如果碰到了下面的错误，你需要给予用户管理打印机的权限：

 `CUPS 操作中出错： “cups-authorization-canceled”。` 

CUPS 在 `/etc/cups/cups-files.conf` 中设置（权限）：

Adding `lpadmin` to `/etc/group` and then to the `SystemGroup` directive in `/etc/cups/cups-files.conf` allows anyone in the `lpadmin` group to configure printers. Do *not* add the `lp` group to the `SystemGroup` directive, or printing will fail.

```
# groupadd -g107 lpadmin

```
 `/etc/cups/cups-files.conf` 
```
# Administrator user group...
SystemGroup sys root lpadmin
```

**提示：** 阅读 [CUPS#CUPS_administration](/index.php/CUPS#CUPS_administration "CUPS") 一文以获取关于如何配置 CUPS 的更多细节。

### Samba/Windows 的支持

如果你想使用 Windows 服务，安装 [Samba](/index.php/Samba_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Samba (简体中文)") (软件包 [samba](https://www.archlinux.org/packages/?name=samba))。

可以通过下面的方式配置 Samba 共享：

```
 系统设置 > 共享 > Windows 共享

```

或者

Dolphin 中右键点击你想要配置的文件夹，然后选择 **属性 > 共享**。

### KDE 桌面活动

KDE 桌面活动是基于 Plasma 的类似于“虚拟桌面”的一组 Plasma 组件，如果你有多于一个屏幕或者桌面，你可以独立地配置这些组件。

在你的桌面上，点击 Cashew Plasmoid，然后在弹出的窗口中点击“活动”。

在屏幕的底端将会出现一栏，包含现有的 Plasma 桌面活动。点击对应的图标就可以在它们之间切换。

### 节能

KDE 集成了一个名为 "**电源管理**"的节能服务，它可以调整系统的节能配置文件及/或（如果支持的话）屏幕的亮度。

**Note:** Powerdevil 可能无法 [覆盖](/index.php/Power_management#Power_managers "Power management") 所有的 logind 设置(例如笔记本翻盖动作). 请修改 [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

### 监视本地文件和目录的变化

KDE 现在通过 **kdirwatch**（位于 kdelibs 中）直接从内核中调用 **inotify**，所以不再需要 Gadmin 或者 FAM 了。

### 程序自启动

Plasma can autostart applications and run scripts on startup and shutdown. To autostart an application, start `systemsettings` and navigate to *Startup and Shutdown* -> *Autostart* and add the program or shell script of your choice. For applications, a `.desktop` file will be created, for shell scripts, a symlink will be created.

*   Programs can be autostarted on login only, whilst shell scripts can also be run on shutdown or even before Plasma itself starts.
*   Shell scripts will only be run if they are marked executable.

Place [Desktop entries](/index.php/Desktop_entries "Desktop entries") (i.e. `.desktop` files) here:

	`~/.config/autostart`

	for starting applications at login.

Place or symlink shell scripts in one of the following directories:

	`~/.config/plasma-workspace/env`

	for executing scripts at login before launching Plasma.

	`~/.config/autostart-scripts`

	for executing scripts at login.

	`~/.config/plasma-workspace/shutdown`

	for executing scripts on shutdown.

## 系统管理

### KDE 系统设置中配置终止 Xorg-server

找到子菜单：

```
   系统设置 > 硬件 > 输入设备 > 键盘 > 高级（标签） > "Key Sequence to kill the X server" 

```

然后选中复选框。

### KCM

KCM 意为 KDE 控制模块（**KC**onfig **M**odule）。这些模块在系统设置中提供了界面，帮助你配置系统。

**配置 GTK 应用程序的外观和风格**

*   [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)
*   [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)

**配置 GRUB 引导程序**

*   [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)

**配置 [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") (UFW)**

*   [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)

**配置 PolicyKit**

*   [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

**配置 Wacom tablets**

*   [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/)

**Systemd 设置**

*   [systemd-kcm](https://www.archlinux.org/packages/?name=systemd-kcm)

可从 [kde-apps.org](http://kde-apps.org/index.php?xcontentmode=273) 找到更多的 KCM 。

## 桌面搜索

KDE 使用 Baloo 实现文件索引和查找。

### Baloo

要在 KDE 桌面中使用 Baloo 搜索，按 `ALT+F2` 并输入你的查询内容。

By default the Desktop Search KCM exposes only two options: A panel to blacklist folders and a way to disable it with one click. More advanced configuration options are available through [kcm_baloo_advanced](https://aur.archlinux.org/packages/kcm_baloo_advanced/).

Alternatively you can edit your `~/.config/baloofilerc` file ([info](https://community.kde.org/Baloo/Configuration)). Additionally the `balooctl` process can also be used. In order to disable Baloo run `balooctl disable`.

Once you added additional folders to the blacklist or disabled Baloo entirely, a process named `baloo_file_cleaner` removes all unneeded index files automatically. They are stored under `~/.local/share/baloo/`.

How do I index a removable device? By default every removable device is blacklisted. You just have to remove your device from the blacklist in the KCM panel.

### Web 浏览器

#### Konqueuor 和 Rekonq

Konqueror 支持两种渲染引擎 – KHTML 和 QtWebKit (通过 [kwebkitpart](https://www.archlinux.org/packages/?name=kwebkitpart) 包) – Rekonq 只支持 QtWebKit. KHTML 开发在Qt迁移到WebKit后已经中止, 但由于兼容性原因仍然保留. QtWebKit, in turn, has since been [deprecated](https://www.mail-archive.com/development@qt-project.org/msg18866.html) by the Qt Project and replaced by [Chromium](/index.php/Chromium "Chromium")-based Qt WebEngine which is currently not supported by either Konqueror or Rekonq.

A successor named Fiber is currently in development, which will use Chromium's engine.

#### Firefox

Firefox 可以通过配置以和 Plasma 更好地集成. 参考 [Firefox KDE integration](/index.php/Firefox#KDE_integration "Firefox") 获取具体内容.

#### Qupzilla

Qupzilla ([qupzilla](https://www.archlinux.org/packages/?name=qupzilla)) 是一个包含 Plasma 集成特性的 Qt web 浏览器. Qupzilla 2.0 将使用 Qt WebEngine 来替代 WebKit.

## PIM

KDE 提供了自己的个人信息管理应用栈，包括电子邮件，联系人，日历等.

### Akonadi

Akonadi 是系统中本地缓存各种来源的 PIM 数据的一种方法，接着这些数据可以被其它的应用使用。这包含了用户的邮件、联系人、日历、事件、刊物、闹钟、笔记等。

Akonadi 自身并不存储任何数据：存储格式依赖于数据的性质（例如，联系人可能以 vcard 格式存储）。

#### 运行不含 Akonadi 的 KDE

对于想运行不包含 Akonadi 的 KDE 的用户，软件包 [akonadi-fake](https://aur.archlinux.org/packages/akonadi-fake/) 是一个不错的选择。

#### 禁用 Akonadi

请参见 KDE userbase 的[这一节](http://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem)。

#### 配置数据库

启动软件包 [kdepim-runtime](https://www.archlinux.org/packages/?name=kdepim-runtime) 中的 `akonaditray`，右键点击它并选择 **配置**。在 Akonadi 服务器配置标签中，你可以：

*   配置 Akonadi 使用 MySQL/MariaDB 服务器
*   配置 Akonadi 使用 PostgreSQL 服务器
*   配置 Akonadi 使用 SQLite

## Phonon

### Phonon 是什么？

摘自 [Wikipedia](https://en.wikipedia.org/wiki/Phonon_(software) "wikipedia:Phonon (software)")： *Phonon 是 KDE 的多媒体 API, 提供了多个多媒体框架的抽象，为 KDE 和一些 QT 程序提供多媒体流处理功能。*

KDE 中广泛地使用 **Phonon** 于声音（例如系统通知或者 KDE 声音应用）和视频（例如 Dolphin 中的视频缩略图）中。

### 我应该选择哪个后端？

你可以在 [GStreamer](/index.php/GStreamer "GStreamer") 和 [VLC](/index.php/VLC "VLC") 之间做选择–每个后端都有 Qt4 和 Qt5 版本 ([phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer), [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) – [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)).

根据 [KDE-Multimedia 邮件列表中的这封邮件](http://lists.kde.org/?l=kde-multimedia&m=137994906723790&w=2)， 上游建议使用 VLC 后端，但是很多 Linux 发行版 (例如 Kubuntu 和 Fedora-KDE ) 选择 GStreamer，因为它可以更方便的去掉专利 MPEG codecs。它们的 [功能](http://community.kde.org/Phonon/FeatureMatrix)有稍许不同。

之前还有一些后端，但是因为缺乏维护，已经从 Arch 中删除。

*   可以同时安装多个后端，并在 *系统设置 > 多媒体 > Phonon > 后端*(Plasma 4) 或 *System Settings > Multimedia > Backend*(Plasma 5) 中进行选择。
*   根据 [KDE 这个帖子](https://forum.kde.org/viewtopic.php?f=250&t=126476&p=335080), VLC 后端不支持 [ReplayGain](https://en.wikipedia.org/wiki/ReplayGain "wikipedia:ReplayGain")。

## 常用的应用

可以在[这里](http://www.kde.org/applications/)找到官方的 KDE 应用集。

### Yakuake

[Yakuake](/index.php/Yakuake "Yakuake") 提供了一个 Quake-like 终端模拟器，使用 F12 来切换可视的状态。它还支持多标签。可以通过软件包 [yakuake](https://www.archlinux.org/packages/?name=yakuake) 来安装 Yakuake。

### KDE Telepathy

[KDE Telepathy](http://community.kde.org/KTp) 是一个把即时信息功能紧密整合到 KDE 桌面中的项目。它使用 Telepathy 框架作为后端，意在替代 Kopete。

要安装所有 Telepathy 协议，安装 [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) 组。 要使用 KDE Telepathy 客户端，安装 [kde-telepathy-meta](https://www.archlinux.org/packages/?name=kde-telepathy-meta) 软件包，它包含了所有在 [telepathy-kde](https://www.archlinux.org/groups/x86_64/telepathy-kde/) 组中的软件包。

#### Use Telegram with KDE Telepathy

Telegram protocol is available using [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), installing [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) or [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) and [telepathy-morse-git](https://aur.archlinux.org/packages/telepathy-morse-git/). The username is the Telegram account telephone number (complete with the national prefix '+xx', e.g. '+49' for Germany). The configuration through the GUI may be tricky: if the phone number is not accepted when configuring a new account in the KDE Telepathy client (with an error message complaining about an invalid parameter which prevents the account creation), insert it between single quotes and then remove the quotes manually from the configuration file (`~/.local/share/telepathy/mission-control/accounts.cfg`) after the account creation (if the quotes are not removed after, an authentication error should rise). Note that the configuration file should be edited manually when KDE Telepathy is not running, e.g. when there is no KDE desktop session active, otherwise manual changes may be overwritten by the software.

## 提示和技巧

### 使用其他窗口管理器

你可能会想使用除 KWin 外的其他窗口管理器, 比如导致绕过 [black screen with PRIME](/index.php/PRIME#Black_screen_with_GL-based_compositors "PRIME") 的 DRI bug.

要在KDE中使用其他 [window manager](/index.php/Window_manager "Window manager")， 打开 `systemsettings` 面板后进入 Default Applications > Window Manager > Use a different window manager 并从列表中选择你用使用的窗口管理器.

#### KDE/Openbox 会话

软件包 [openbox](https://www.archlinux.org/packages/?name=openbox) 为在plasma下使用 [Openbox](/index.php/Openbox "Openbox") 提供了会话. 要使用这个会话，请在 [display manager](/index.php/Display_manager "Display manager") 菜单中选择 *KDE/Openbox* .

若要手动启动会话，请将下面这行添加到你的 `.xinitrc` 文件中:

```
exec openbox-kde-session

```

#### Compiz 设置

If you need to run Compiz with custom options and switches select *Compiz custom* and then create a script called `compiz-kde-launcher` and add to it the commands you wish to use to start Compiz. See the example below:

 `/usr/local/bin/compiz-kde-launcher` 
```
#!/bin/bash
LIBGL_ALWAYS_INDIRECT=1
compiz --replace &
wait

```

Then make it executable:

```
$ chmod +x /usr/local/bin/compiz-kde-launcher

```

#### Re-enabling compositing effects

Where replacing Kwin with a window manager the does not provide a Compositor (such as Openbox), any desktop compositing effects e.g. transparency will be lost. In this case, install and run a separate Composite manager to provide the effects such as [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") or [Compton](/index.php/Compton "Compton").

### Integrate Android

KDE connect provides several features for you:

*   Share files and URLs to/from KDE from/to any app, without wires.
*   Touchpad emulation: Use your phone screen as your computer's touchpad.
*   Notifications sync (4.3+): Read your Android notifications from the desktop.
*   Shared clipboard: copy and paste between your phone and your computer.
*   Multimedia remote control: Use your phone as a remote for Linux media players.
*   WiFi connection: no usb wire or bluetooth needed.
*   RSA Encryption: your information is safe.

You will need to install KDE Connect both on your computer and on your Android. For PC side, install [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) package. For Android side, install `KDE Connect` from [Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) or from [F-Droid](https://f-droid.org/repository/browse/?fdid=org.kde.kdeconnect_tp).

### 获取软件包更新提醒

安装 [apper](https://aur.archlinux.org/packages/apper/) 后可以从KDE系统托盘中获取软件包更新提醒以及一个基础的软件包管理工具GUI. 参考 [PackageKit website](http://www.packagekit.org/index.html) 获取更多信息.

### 配置 KWin 成使用 OpenGL ES

设置环境变量 `KWIN_COMPOSE` 为 'O2ES' 以强制使用 OpenGL ES 后端. 请注意 OpenGL ES 未被所有驱动支持.

### Konqueror/Dolphin 文件管理器中开启视频缩略图

对于 Konqueror 和 Dolphin 中的视频缩略图，安装 [kdemultimedia-mplayerthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-mplayerthumbs) 或者 [kdemultimedia-ffmpegthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-ffmpegthumbs)。

### 加速应用启动

用户 Rob 在他的博客中写道，这个“[技巧](http://kdemonkey.blogspot.nl/2008/04/magic-trick.html)”加快了应用程序的启动时间 50-150 毫秒。 要启用这个技巧，在你的 home 目录下面创建这个目录：

```
$ mkdir -p ~/.compose-cache

```

**注意:** 对于这中间发生了什么感到好奇的人来说，这个操作启用了一项前一段时间由 Lubos （以 general KDE speediness 知名） 提出，然后被重写并整合到 libx11 中的优化。应用平时启动时从 `/usr/share/X11/locale/<your locale>/Compose` 读取输入法信息，这个文件很长（对于 en_US.UTF-8 有超过 5000 行），需要不少时间来处理。libX11 可以缓存解析过的信息，以后读取时会快很多。但是它仅在目录存在时才会重用现有的缓存或者在 `~/.compose-cache` 中创建一份新的。

### 显示器分辨率 / 多显示器配置

要在 Plasma 5 中启用分辨率和多显示器管理, 请安装 [kscreen](https://www.archlinux.org/packages/?name=kscreen). 它在 System Settings/Display and Monitor 中添加了更多选项.

### Open application launcher with Super key (Windows key)

Install and start [ksuperkey](https://aur.archlinux.org/packages/ksuperkey/). Now assign Alt + F1 as hot key. The Super Key will now open the application launcher. You can add ksuperkey to the autostart if you don't want to start it manually.

## 故障排除

#### Plasma 在 Intel 显卡上崩溃

根据 [kde-distro-packagers](https://mail.kde.org/pipermail/kde-distro-packagers/2015-August/000088.html) 中的邮件，Intel 显卡驱动使用 SNA 加速时会引起 Plasma 崩溃，出现这种问题时，请 [切换到 UXA](/index.php/Intel_graphics#SNA_issues "Intel graphics") 方式.

### 有关配置的问题

KDE 中许多问题都源自配置文件。

#### Plasma 桌面行为异常

Plasma 故障通常是由不稳定的 **plasmoids** 或者 **plasma themes** 引起的。首先寻找最近安装的 plasmoid 或者 plasma 主题并禁用或者卸载它。

因此，如果你的桌面突然碰到 "locking up"，很可能是由于安装了有问题的组件造成的。如果你不记得故障发生前你安装了什么小部件（有时它可能是一个不寻常的问题），通过逐个移除小部件直到问题不再出现来跟踪这个问题。然后你可以卸载这个小部件，**仅当它是一个官方小部件时**到 bugs.kde.org 填写一份缺陷报告。如果它不是，我推荐你在 kde-look.org 上寻找它的条目并告知小部件的开发者你所碰到的问题（再现它的详细步骤等等）。

如果你找不到问题，也不想丢失 *所有的* KDE 设置，这样办：

```
 $ for j in plasma*; do mv -- "$j" "${j%}.bak"; done

```

This command will **rename all Plasma related configs** to *.bak (e.g. `plasmarc.bak`) of your user and when you will relogin into Plasma, you will have the **default** settings back. To undo that action, remove the .bak file extension. If you already have *.bak files, rename, move, or delete them first. It is highly recommended that you create regular backups anyway. See [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") for a list of possible solutions.

#### 清理缓存以解决升级故障

故障可能由旧的缓存导致。有时，升级后旧缓存可能会产生奇怪的、难以调试的行为，例如关不掉的 shell、改变各种设置时失去响应、以及像 ark 不能运行解压 rar / zip 文件或者 amarok 不能识别音乐等各种其它问题。这个办法也能解决 KDE 和 Qt 程序在升级后变得难看的问题。

用以下命令来重建缓存：

```
 $ rm ~/.config/Trolltech.conf
 $ kbuildsycoca4 --noincremental

```

但愿你的故障已被修复。 [引用](https://bbs.archlinux.org/viewtopic.php?id=135301)。

#### 清理 akonadi 配置来修复 kmail

首先保证没有运行 KMail。然后备份配置文件：

```
$ mv ~/.local/share/akonadi  ~/.local/share/akonadi-old
$ mv ~/.config/akonadi ~/.config/akonadi-old

```

启动 *系统设置 > 个人信息* 并删除所有资源。回到 Dolphin 中移除原始的 `~/.local/share/akonadi` 和 `~/.config/akonadi` - 所作的备份保证你可以在必要时恢复它们。

现在回到 系统设置 页面并小心地添加必要的资源。你应该看到读取你邮件目录的资源。然后启动 Kontact/KMail 查看它是否正常运作。

### Fix empty IMAP inbox

For some IMAP accounts, kmail will show the inbox as a container with all other folders of this account inside. Kmail does not show messages in the inbox container but in all other subfolders [[2]](https://bugs.kde.org/show_bug.cgi?id=284172). To solve this problem simply disable the server side subscribition in the kmail account settings.

### 为了支持和调试获取 KWin 的当前状况

这行命令输出了一份关于 KWin 当前状况的精彩总结，包括使用的选项、使用的 compositing 后端以及相关 OpenGL 驱动的能力。更多信息参见 [Martin的博客](http://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/)

qdbus org.kde.kwin /KWin supportInformation

### KDE 和 Qt 程序在别的窗口管理器下很难看

如果你不在完整的 Plasma 会话之中（特别是你没有运行 "startkde"）使用 KDE 或者 Qt 程序，那么直到 Plasma 4.6.1，你需要告诉 Qt 怎么找到 KDE 的样式（Oxygen、QtCurve等等。）。

你只需要设置 QT_PLUGIN_PATH 环境变量。即，写入

```
export QT_PLUGIN_PATH=$HOME/.kde4/lib/kde4/plugins/:/usr/lib/kde4/plugins/

```

到你的 `/etc/profile` （或者如果你没有 root 权限 `~/.profile`）。qtconfig 然后应该就能找到你的 kde 样式，然后所有东西应该就美观了！

另外，你可以把 Qt 样式目录链接到 KDE 样式：

```
 # ln -s /usr/lib/kde4/plugins/styles/ /usr/lib/qt4/pluginlib32-libdbusmenu-glibs/styles

```

在 Gnome 中，你可以尝试安装软件包 libgnomeui。

### KF5/Qt5 应用在 i3/fvwm/awesome 中不显示图标

参考 [Qt#Configuration of Qt5 apps under environments other than KDE](/index.php/Qt#Configuration_of_Qt5_apps_under_environments_other_than_KDE "Qt").

### 有关图形的故障

#### Plasma keeps crashing with legacy Nvidia

This is caused by a [bug in Plasma](https://bugs.kde.org/show_bug.cgi?id=348753) when using the Nvidia-304xx driver. Rather than disabling compositing, create a file `kwin.sh` in `~/.config/plasma-workspace/env/` with the following contents:

```
#!/bin/sh	
export KWIN_EXPLICIT_SYNC=0

```

Then go to *system-settings > Startup and Shutdown > Autostart* and *Check/Add* the script as a pre-KDE startup file.

#### Applications don't refresh properly

If you use 3D-accelerated composition with [Intel](/index.php/Intel "Intel"), you might find that the Plasma panel and other applications don't refresh properly (stay frozen). Some Intel drivers have [problems with EGL](https://bugzilla.redhat.com/show_bug.cgi?id=1259475). Go to System Settings under *Display and Monitor* -> *Compositor*. Set *OpenGL interface* to OpenGL 3.1\. If that does not work, see [Intel graphics#SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics") for alternative solutions.

#### 2D 桌面性能差（或）出现残影

##### GPU 驱动程序问题

请确保你已经安装了适当的显卡驱动，这样你的桌面至少有 2D 加速。遵照这些文章：[ATI](/index.php/ATI "ATI")、[NVIDIA](/index.php/NVIDIA "NVIDIA")、[Intel](/index.php/Intel_graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel graphics (简体中文)")，以获得更多信息来保证一切正常。 开源的 ATI 和 Intel 驱动程序和私有的（二进制）Nvidia 驱动程序理论上应该能提供最好的 2D 和 3D 加速。

##### 使用 Raster 引擎跳过问题

如果这不能解决你的问题，你的驱动可能未提供好的 **XRender** 加速，而现在的 Qt 绘图引擎默认依赖于它。

只有使用`-graphicssystem raster`命令行参数调用程序时，才能在运行时修改绘图引擎。要默认使用此渲染引擎，需要用同样的配置选项`-graphicssystem raster`重新编译 Qt。

Raster 绘图引擎使用 CPU 而不是 GPU 来处理大多数的绘制。在个别系统上，你可能获得更好的性能。这仅是为了对应糟糕的 Linux 驱动程序堆栈而采取的变通方法。CPU为通用计算优化，而GPU专门为绘图操作进行了很多优化。因此，仅当你碰到了问题或者你的 GPU 比 CPU 慢得多时才使用 Raster 引擎，否则使用 XRender 更好。

从 Qt 4.7+ 起，不再需要重新编译 Qt。只需要导出 **QT_GRAPHICSSYSTEM=raster**，或者 "opengl"， 或者 "native" （这是默认值）。Raster 依赖于 CPU，OpenGL 依赖于 GPU 以及很好的驱动支持，而 Native 仅仅使用 X11 rendering (mixture, usually)。

**最好的和自动的实施方法** 是从 AUR 中安装 [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/) 并通过：

```
 系统设置 > Qt Graphics System

```

进行配置。

要获得更多信息，访问这个 [KDE Developer 博客条目](http://apachelog.wordpress.com/2010/09/05/qt-graphics-system-kcm/) 及/或这个 [Qt Developer 博客条目](http://labs.trolltech.com/blogs/2009/12/18/qt-graphics-and-performance-the-raster-engine/)。

#### 3D 桌面性能差

KDE 一开始启用了桌面效果。旧的显卡可能不够支持 3D 桌面加速。你可以禁用桌面效果通过

```
系统设置 > 桌面效果

```

并且使用 `Alt+Shift+F12` 切换桌面效果。

**注意:** 使用更强大的显卡时，也可能碰到这类 3D 桌面性能问题。请确保显示驱动已经正确安装。

#### 有 Nvidia GPU 的系统中桌面混成被禁用

有时 KWin 的配置文件（**kwinrc**）中的配置 *可能* 在重新激活 3D 桌面 **OpenGL** 混成时引起问题。这可能是随机产生的，（例如，由于 Xorg 的突然崩溃或重启，文件被损坏了），因此，发生这种情况时，删除你的 `~/.kde4/share/config/kwinrc` 文件并重新登录。KWin 配置将变为 KDE 默认值，故障应该就没有了。

#### 启用混成后全屏时闪烁

从 KDE SC 4.6.0 起，有一个选项为 *系统设置 > 桌面效果 > 高级 > 为全屏窗口挂起桌面特效*，不选中它将使 kwin 禁用 unredirect fullscreen。

#### Display settings lost on reboot (multiple monitors)

There is a [bug](https://bugs.kde.org/show_bug.cgi?id=346961) in kscreen that makes it forget dual screen settings after reboot with certain displays.

A possible workaround is to uninstall [kscreen](https://www.archlinux.org/packages/?name=kscreen) and specify your screen setup in a xorg.conf file instead:

*   See [Multihead#RandR](/index.php/Multihead#RandR "Multihead") for using the [RandR](https://en.wikipedia.org/wiki/RandR "wikipedia:RandR") [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") extension.
*   For Nouveau you can use the template at [Nouveau#Dual Head](/index.php/Nouveau#Dual_Head "Nouveau"), just edit it to suit your setup.
*   For the proprietary nvidia driver you can use the [nvidia-settings](/index.php/NVIDIA#Using_NVIDIA_Settings "NVIDIA") utility as root to write the config file.

### KDE 下的声音问题

#### ALSA 相关的问题

**注意:** 首先保证你已经安装了 [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib) 和 [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils)。

##### 尝试在 KDE 中播放任何声音时出现 "返回 default" 消息

当你碰到这些消息：

	音频回放设备 *声音设备的名称* 不工作。

	返回 default。

访问：

```
 系统设置 > 多媒体 > Phonon

```

并在每一栏中都把名称为 "**default**" 的设备设置在所有其它设备的上面。

##### 使用 GStreamer Phonon 后端时不能播放 MP3 文件

安装 GStreamer libav 插件（软件包[gst-libav](https://www.archlinux.org/packages/?name=gst-libav)）可以解决问题。如果仍然碰到，你可以尝试安装另一个软件包，例如 [phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc)，改为使用 Phonon 后端。然后，请确保它是首选的后端，通过：

```
 系统设置 > 多媒体 > Phonon > 后端（选项卡）

```

### Konsole 不保存命令历史

默认情况下，只有当你在终端中输入 'exit' 时保存命令历史记录，而当你用角上的 'x' 关闭 Konsole 时它不会发生。 要启用每条命令执行后的自动保存，你需要在你的 .bashrc 文件中添加这些行：

```
shopt -s histappend
[[ "${PROMPT_COMMAND}" ]] && PROMPT_COMMAND="$PROMPT_COMMAND;history -a" || PROMPT_COMMAND="history -a"

```

### Inotify 文件夹监控上限

如果看到下面警告:

```
KDE Baloo Filewatch service reached the inotify folder watch limit. File changes may be ignored.

```

就需要增加 inotify 文件夹监控上限：

```
# echo 10000 > /proc/sys/fs/inotify/max_user_watches

```

永久设置可以创建文件`/etc/sysctl.d/90-inotify.conf`：

```
#increase inotify watch limit
fs.inotify.max_user_watches = 10000

```

### 自动挂载NFS卷时卡死

对 [NFS](/index.php/NFS "NFS") 卷使用 [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") 可能导致卡死，见 [bug report upstream](https://bugs.kde.org/show_bug.cgi?id=354137).

### Locale warning when installing packages in Konsole

```
 mandb: can't set the locale; make sure $lc_* and $lang are correct

```

By default, Konsole sets $LANG to en_US.US-ASCII. If you haven't generated that locale, then mandb can't use it. In your Konsole profile settings, click "Environment" and then add a line for LANG=en_US.UTF-8 or whatever your locale should be.

### 多显示器问题

当前版本的 KDE Plasma 在设置多显示器时有一些问题, 可能导致Plasma不可用. 参考 [报告](https://bugs.kde.org/show_bug.cgi?id=356225) 和 [报告](https://bugs.kde.org/show_bug.cgi?id=356720).

这些 bug 在上游/git KDE Plasma 构建中已经解决, 可以通过 [plasma-desktop-git](https://aur.archlinux.org/packages/plasma-desktop-git/) 或 [plasma-git-meta](https://aur.archlinux.org/packages/plasma-git-meta/) 来安装 - 记住这些包会和当前版本冲突 - 建议你先移除它们:

```
 # pacman -R plasma-meta

```

[unstable releases](/index.php/Official_repositories#kde-unstable "Official repositories") 可能也包含了所需的补丁 (不确定).

## 不稳定版本

KDE 到了 beta 或者 RC milestone 时，“不稳定的” KDE 软件包被上传到 [kde-unstable] 软件源。它们会待在里面直到宣布 KDE 稳定版本，然后会移到 [extra] 中。

添加 [kde-unstable] 源：

 `/etc/pacman.conf` 
```
[kde-unstable]
 Include = /etc/pacman.d/mirrorlist
```

1.  请加到 [extra] 前，否则 [pacman](/index.php/Pacman "Pacman") 会优先使用 extra repository 中的软件包。
2.  kde-unstable 基于 testing。因此，你需要按以下的顺序启用这些软件源：**kde-unstable, testing, core, extra, community-testing, community**。
3.  要更新以前安装的 KDE，运行： `pacman -Syu` or `pacman -S kde-unstable/kde`
4.  如果你没有安装 KDE，你可能在使用 groups 来安装它时碰到困难（pacman的限制）
5.  **订阅并阅读 arch-dev-public 邮件列表**
6.  如果你发现任何问题，确保 [你报告缺陷](#.E5.8F.91.E8.A1.8C.E7.89.88.E5.92.8C.E4.B8.8A.E6.B8.B8.E7.BC.BA.E9.99.B7.E6.B1.87.E6.8A.A5)。

## Trinity

自从 KDE 4.x 发布之后，开发放弃了 KDE 3.5.x 的支持。 Trinity 桌面环境是 KDE 3 的一个分支，由 Timothy Pearson 开发（[trinitydesktop.org](http://trinitydesktop.org/)）。此项目致力于保留 KDE3.5 的使用方式，同时解决了 KDE 3.5.10 中存在的一些问题。[Trinity](/index.php/Trinity "Trinity")中包含更多信息。

## 缺陷

如果你发现微小或者严重的缺陷，你应该访问 [the Arch Bug Tracker](https://bugs.archlinux.org) 或/和 [KDE Bug Tracker](http://bugs.kde.org) 来汇报它们。确保你清楚想要汇报什么。

如果你碰到了任何问题并在 Arch 论坛上讨论，首先确保你已经使用一个良好的同步镜像 **完全** 更新了你的系统（检查 [这里](https://www.archlinux.de/?page=MirrorStatus)） 或者尝试 [Reflector](/index.php/Reflector_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Reflector (简体中文)")。

## 参见

*   [[3]](http://www.kde.org) - KDE 主页
*   [[4]](https://bugs.kde.org) - KDE 缺陷跟踪页
*   [[5]](https://bugs.archlinux.org) - Arch Linux 缺陷跟踪页
*   [[6]](https://projects.kde.org) - KDE 项目