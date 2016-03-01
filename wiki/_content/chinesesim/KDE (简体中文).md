**翻译状态：** 本文是英文页面 [KDE](/index.php/KDE "KDE") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-05-05，点击[这里](https://wiki.archlinux.org/index.php?title=KDE&diff=0&oldid=372550)可以查看翻译后英文页面的改动。

摘自 [KDE 软件集](http://www.kde.org/community/whatiskde/softwarecompilation.php) 以及 [获取 KDE 软件](http://www.kde.org/download/)：

	*KDE 软件集是由 KDE 产生的一组为 Linux 及类似操作系统建立一个美丽、功能强大的自由桌面计算环境的框架、工作空间和应用。它包含大量的独立应用程序和一个作为外壳的工作空间以运行这些程序。KDE 程序能在任意桌面环境运行，而且可以集成到您的系统组件。*

KDE 上游维护了一份 [UserBase Wiki](http://userbase.kde.org/)。用户能在那里找到大部分 KDE 应用的详细信息。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 Plasma 桌面](#Plasma_.E6.A1.8C.E9.9D.A2)
    *   [1.2 升级KDE 4到Plasma 5](#.E5.8D.87.E7.BA.A7KDE_4.E5.88.B0Plasma_5)
    *   [1.3 KDE 应用和语言包](#KDE_.E5.BA.94.E7.94.A8.E5.92.8C.E8.AF.AD.E8.A8.80.E5.8C.85)
*   [2 启动 Plasma](#.E5.90.AF.E5.8A.A8_Plasma)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 个性化](#.E4.B8.AA.E6.80.A7.E5.8C.96)
        *   [3.1.1 Plasma 桌面](#Plasma_.E6.A1.8C.E9.9D.A2_2)
            *   [3.1.1.1 主题](#.E4.B8.BB.E9.A2.98)
            *   [3.1.1.2 小工具](#.E5.B0.8F.E5.B7.A5.E5.85.B7)
            *   [3.1.1.3 系统托盘中的声音应用](#.E7.B3.BB.E7.BB.9F.E6.89.98.E7.9B.98.E4.B8.AD.E7.9A.84.E5.A3.B0.E9.9F.B3.E5.BA.94.E7.94.A8)
            *   [3.1.1.4 Adding a Global Menu to the desktop](#Adding_a_Global_Menu_to_the_desktop)
        *   [3.1.2 窗口装饰](#.E7.AA.97.E5.8F.A3.E8.A3.85.E9.A5.B0)
        *   [3.1.3 图标主题](#.E5.9B.BE.E6.A0.87.E4.B8.BB.E9.A2.98)
        *   [3.1.4 Kicker菜单中的Arch Linux Logo图标](#Kicker.E8.8F.9C.E5.8D.95.E4.B8.AD.E7.9A.84Arch_Linux_Logo.E5.9B.BE.E6.A0.87)
        *   [3.1.5 字体](#.E5.AD.97.E4.BD.93)
            *   [3.1.5.1 字体太大或变形](#.E5.AD.97.E4.BD.93.E5.A4.AA.E5.A4.A7.E6.88.96.E5.8F.98.E5.BD.A2)
        *   [3.1.6 空间利用效率](#.E7.A9.BA.E9.97.B4.E5.88.A9.E7.94.A8.E6.95.88.E7.8E.87)
    *   [3.2 网络](#.E7.BD.91.E7.BB.9C)
    *   [3.3 打印](#.E6.89.93.E5.8D.B0)
    *   [3.4 Samba/Windows 的支持](#Samba.2FWindows_.E7.9A.84.E6.94.AF.E6.8C.81)
    *   [3.5 KDE 桌面活动](#KDE_.E6.A1.8C.E9.9D.A2.E6.B4.BB.E5.8A.A8)
    *   [3.6 节能](#.E8.8A.82.E8.83.BD)
    *   [3.7 监视本地文件和目录的变化](#.E7.9B.91.E8.A7.86.E6.9C.AC.E5.9C.B0.E6.96.87.E4.BB.B6.E5.92.8C.E7.9B.AE.E5.BD.95.E7.9A.84.E5.8F.98.E5.8C.96)
*   [4 系统管理](#.E7.B3.BB.E7.BB.9F.E7.AE.A1.E7.90.86)
    *   [4.1 设置键盘布局](#.E8.AE.BE.E7.BD.AE.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
    *   [4.2 KDE 系统设置中配置终止 Xorg-server](#KDE_.E7.B3.BB.E7.BB.9F.E8.AE.BE.E7.BD.AE.E4.B8.AD.E9.85.8D.E7.BD.AE.E7.BB.88.E6.AD.A2_Xorg-server)
    *   [4.3 KCM](#KCM)
*   [5 桌面搜索和语义桌面](#.E6.A1.8C.E9.9D.A2.E6.90.9C.E7.B4.A2.E5.92.8C.E8.AF.AD.E4.B9.89.E6.A1.8C.E9.9D.A2)
    *   [5.1 Baloo](#Baloo)
    *   [5.2 Akonadi](#Akonadi)
        *   [5.2.1 运行不含 Akonadi 的 KDE](#.E8.BF.90.E8.A1.8C.E4.B8.8D.E5.90.AB_Akonadi_.E7.9A.84_KDE)
        *   [5.2.2 禁用 Akonadi](#.E7.A6.81.E7.94.A8_Akonadi)
        *   [5.2.3 配置数据库](#.E9.85.8D.E7.BD.AE.E6.95.B0.E6.8D.AE.E5.BA.93)
*   [6 Phonon](#Phonon)
    *   [6.1 Phonon 是什么？](#Phonon_.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
    *   [6.2 我应该选择哪个后端？](#.E6.88.91.E5.BA.94.E8.AF.A5.E9.80.89.E6.8B.A9.E5.93.AA.E4.B8.AA.E5.90.8E.E7.AB.AF.EF.BC.9F)
*   [7 常用的应用](#.E5.B8.B8.E7.94.A8.E7.9A.84.E5.BA.94.E7.94.A8)
    *   [7.1 Yakuake](#Yakuake)
    *   [7.2 KDE Telepathy](#KDE_Telepathy)
        *   [7.2.1 Use Telegram with KDE Telepathy](#Use_Telegram_with_KDE_Telepathy)
*   [8 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [8.1 Using an alternative window manager in KDE](#Using_an_alternative_window_manager_in_KDE)
        *   [8.1.1 KDE/Openbox Session](#KDE.2FOpenbox_Session)
        *   [8.1.2 Compiz Custom](#Compiz_Custom)
        *   [8.1.3 Re-enabling compositing effects](#Re-enabling_compositing_effects)
    *   [8.2 Integrate Android with the KDE Desktop](#Integrate_Android_with_the_KDE_Desktop)
    *   [8.3 Get notifications for software updates](#Get_notifications_for_software_updates)
    *   [8.4 配置 KWin 成使用 OpenGL ES](#.E9.85.8D.E7.BD.AE_KWin_.E6.88.90.E4.BD.BF.E7.94.A8_OpenGL_ES)
    *   [8.5 Konqueror/Dolphin 文件管理器中开启视频缩略图](#Konqueror.2FDolphin_.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8.E4.B8.AD.E5.BC.80.E5.90.AF.E8.A7.86.E9.A2.91.E7.BC.A9.E7.95.A5.E5.9B.BE)
    *   [8.6 加速应用启动](#.E5.8A.A0.E9.80.9F.E5.BA.94.E7.94.A8.E5.90.AF.E5.8A.A8)
    *   [8.7 隐藏分区](#.E9.9A.90.E8.97.8F.E5.88.86.E5.8C.BA)
    *   [8.8 Konqueror 技巧](#Konqueror_.E6.8A.80.E5.B7.A7)
        *   [8.8.1 禁用页面快捷键的提示（浏览器）](#.E7.A6.81.E7.94.A8.E9.A1.B5.E9.9D.A2.E5.BF.AB.E6.8D.B7.E9.94.AE.E7.9A.84.E6.8F.90.E7.A4.BA.EF.BC.88.E6.B5.8F.E8.A7.88.E5.99.A8.EF.BC.89)
        *   [8.8.2 禁用侧边栏标签（文件管理器）](#.E7.A6.81.E7.94.A8.E4.BE.A7.E8.BE.B9.E6.A0.8F.E6.A0.87.E7.AD.BE.EF.BC.88.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8.EF.BC.89)
        *   [8.8.3 使用 WebKit](#.E4.BD.BF.E7.94.A8_WebKit)
    *   [8.9 Firefox 集成](#Firefox_.E9.9B.86.E6.88.90)
    *   [8.10 设置与当前桌面相同的屏幕保护背景](#.E8.AE.BE.E7.BD.AE.E4.B8.8E.E5.BD.93.E5.89.8D.E6.A1.8C.E9.9D.A2.E7.9B.B8.E5.90.8C.E7.9A.84.E5.B1.8F.E5.B9.95.E4.BF.9D.E6.8A.A4.E8.83.8C.E6.99.AF)
    *   [8.11 Setting lockscreen wallpaper to arbitrary image](#Setting_lockscreen_wallpaper_to_arbitrary_image)
*   [9 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [9.1 Plasma 在 Intel 显卡上崩溃](#Plasma_.E5.9C.A8_Intel_.E6.98.BE.E5.8D.A1.E4.B8.8A.E5.B4.A9.E6.BA.83)
    *   [9.2 有关配置的问题](#.E6.9C.89.E5.85.B3.E9.85.8D.E7.BD.AE.E7.9A.84.E9.97.AE.E9.A2.98)
        *   [9.2.1 重置所有 KDE 配置](#.E9.87.8D.E7.BD.AE.E6.89.80.E6.9C.89_KDE_.E9.85.8D.E7.BD.AE)
        *   [9.2.2 Plasma 桌面行为异常](#Plasma_.E6.A1.8C.E9.9D.A2.E8.A1.8C.E4.B8.BA.E5.BC.82.E5.B8.B8)
        *   [9.2.3 清理缓存以解决升级故障](#.E6.B8.85.E7.90.86.E7.BC.93.E5.AD.98.E4.BB.A5.E8.A7.A3.E5.86.B3.E5.8D.87.E7.BA.A7.E6.95.85.E9.9A.9C)
        *   [9.2.4 清理 akonadi 配置来修复 kmail](#.E6.B8.85.E7.90.86_akonadi_.E9.85.8D.E7.BD.AE.E6.9D.A5.E4.BF.AE.E5.A4.8D_kmail)
    *   [9.3 为了支持和调试获取 KWin 的当前状况](#.E4.B8.BA.E4.BA.86.E6.94.AF.E6.8C.81.E5.92.8C.E8.B0.83.E8.AF.95.E8.8E.B7.E5.8F.96_KWin_.E7.9A.84.E5.BD.93.E5.89.8D.E7.8A.B6.E5.86.B5)
    *   [9.4 KDE4 不能结束载入](#KDE4_.E4.B8.8D.E8.83.BD.E7.BB.93.E6.9D.9F.E8.BD.BD.E5.85.A5)
    *   [9.5 KDE 和 Qt 程序在别的窗口管理器下很难看](#KDE_.E5.92.8C_Qt_.E7.A8.8B.E5.BA.8F.E5.9C.A8.E5.88.AB.E7.9A.84.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8.E4.B8.8B.E5.BE.88.E9.9A.BE.E7.9C.8B)
    *   [9.6 有关图形的故障](#.E6.9C.89.E5.85.B3.E5.9B.BE.E5.BD.A2.E7.9A.84.E6.95.85.E9.9A.9C)
        *   [9.6.1 2D 桌面性能差（或）出现残影](#2D_.E6.A1.8C.E9.9D.A2.E6.80.A7.E8.83.BD.E5.B7.AE.EF.BC.88.E6.88.96.EF.BC.89.E5.87.BA.E7.8E.B0.E6.AE.8B.E5.BD.B1)
            *   [9.6.1.1 GPU 驱动程序问题](#GPU_.E9.A9.B1.E5.8A.A8.E7.A8.8B.E5.BA.8F.E9.97.AE.E9.A2.98)
            *   [9.6.1.2 使用 Raster 引擎跳过问题](#.E4.BD.BF.E7.94.A8_Raster_.E5.BC.95.E6.93.8E.E8.B7.B3.E8.BF.87.E9.97.AE.E9.A2.98)
        *   [9.6.2 3D 桌面性能差](#3D_.E6.A1.8C.E9.9D.A2.E6.80.A7.E8.83.BD.E5.B7.AE)
        *   [9.6.3 有 Nvidia GPU 的系统中桌面混成被禁用](#.E6.9C.89_Nvidia_GPU_.E7.9A.84.E7.B3.BB.E7.BB.9F.E4.B8.AD.E6.A1.8C.E9.9D.A2.E6.B7.B7.E6.88.90.E8.A2.AB.E7.A6.81.E7.94.A8)
        *   [9.6.4 启用混成后全屏时闪烁](#.E5.90.AF.E7.94.A8.E6.B7.B7.E6.88.90.E5.90.8E.E5.85.A8.E5.B1.8F.E6.97.B6.E9.97.AA.E7.83.81)
        *   [9.6.5 启用混成后花屏](#.E5.90.AF.E7.94.A8.E6.B7.B7.E6.88.90.E5.90.8E.E8.8A.B1.E5.B1.8F)
        *   [9.6.6 Display settings lost on reboot (multiple monitors)](#Display_settings_lost_on_reboot_.28multiple_monitors.29)
    *   [9.7 KDE 下的声音问题](#KDE_.E4.B8.8B.E7.9A.84.E5.A3.B0.E9.9F.B3.E9.97.AE.E9.A2.98)
        *   [9.7.1 ALSA 相关的问题](#ALSA_.E7.9B.B8.E5.85.B3.E7.9A.84.E9.97.AE.E9.A2.98)
            *   [9.7.1.1 尝试在 KDE 中播放任何声音时出现 "返回 default" 消息](#.E5.B0.9D.E8.AF.95.E5.9C.A8_KDE_.E4.B8.AD.E6.92.AD.E6.94.BE.E4.BB.BB.E4.BD.95.E5.A3.B0.E9.9F.B3.E6.97.B6.E5.87.BA.E7.8E.B0_.22.E8.BF.94.E5.9B.9E_default.22_.E6.B6.88.E6.81.AF)
            *   [9.7.1.2 使用 GStreamer Phonon 后端时不能播放 MP3 文件](#.E4.BD.BF.E7.94.A8_GStreamer_Phonon_.E5.90.8E.E7.AB.AF.E6.97.B6.E4.B8.8D.E8.83.BD.E6.92.AD.E6.94.BE_MP3_.E6.96.87.E4.BB.B6)
    *   [9.8 Konsole 不保存命令历史](#Konsole_.E4.B8.8D.E4.BF.9D.E5.AD.98.E5.91.BD.E4.BB.A4.E5.8E.86.E5.8F.B2)
    *   [9.9 KDE 在密码提示时每个字母用三颗星表示](#KDE_.E5.9C.A8.E5.AF.86.E7.A0.81.E6.8F.90.E7.A4.BA.E6.97.B6.E6.AF.8F.E4.B8.AA.E5.AD.97.E6.AF.8D.E7.94.A8.E4.B8.89.E9.A2.97.E6.98.9F.E8.A1.A8.E7.A4.BA)
    *   [9.10 Dolphin 和文件对话框启动极慢](#Dolphin_.E5.92.8C.E6.96.87.E4.BB.B6.E5.AF.B9.E8.AF.9D.E6.A1.86.E5.90.AF.E5.8A.A8.E6.9E.81.E6.85.A2)
    *   [9.11 KDE 中 GTK 应用中默认的 PDF 查看器](#KDE_.E4.B8.AD_GTK_.E5.BA.94.E7.94.A8.E4.B8.AD.E9.BB.98.E8.AE.A4.E7.9A.84_PDF_.E6.9F.A5.E7.9C.8B.E5.99.A8)
    *   [9.12 Inotify 文件夹监控上限](#Inotify_.E6.96.87.E4.BB.B6.E5.A4.B9.E7.9B.91.E6.8E.A7.E4.B8.8A.E9.99.90)
*   [10 不稳定版本](#.E4.B8.8D.E7.A8.B3.E5.AE.9A.E7.89.88.E6.9C.AC)
*   [11 Trinity](#Trinity)
*   [12 缺陷](#.E7.BC.BA.E9.99.B7)
*   [13 参见](#.E5.8F.82.E8.A7.81)

## 安装

### Plasma 桌面

**Note:**

*   Plasma 5 和 kde4 [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)不兼容。
*   KDE 4 Plasma 桌面到2015年八月停止维护。

在安装Plasma之前，请确保[Xorg](/index.php/Xorg "Xorg")已经被安装到您的系统中

安装基础包 [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) 或者 完整的[plasma](https://www.archlinux.org/groups/x86_64/plasma/)。 For differences between [plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta) and [plasma](https://www.archlinux.org/groups/x86_64/plasma/) reference [KDE Packages](/index.php/KDE_Packages "KDE Packages"). Alternatively, for a more minimal Plasma installation, install the [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) package.

### 升级KDE 4到Plasma 5

1.  隔离 `multi-user.target` `# systemctl isolate multi-user.target` 
2.  [卸载](/index.php/Pacman "Pacman") kdebase-workspace 软件包 `# pacman -Rc kdebase-workspace` 
3.  [安装](/index.php/Pacman "Pacman") 软件包组[plasma](https://www.archlinux.org/groups/x86_64/plasma/),或者只安装[plasma-meta](https://www.archlinux.org/packages/?name=plasma-meta)软件包.
4.  停用KDM(如果你在使用的话) `# systemctl disable kdm` 然后安装[SDDM](/index.php/SDDM "SDDM") `# systemctl enable sddm` 或其他的 [显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器").
5.  重新启动.

**Note:** Plasma 4 设置并不会自动合并到Plasma 5,所以你要从桌面重新设置.

### KDE 应用和语言包

你能够通过安装[kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/)或者安装[kde-applications-meta](https://www.archlinux.org/packages/?name=kde-applications-meta)基础包具体模块来安装全部的KDE Applications（应用）。 请注意这仅仅安装applications（应用），并没有安装 Plasma 桌面。

如果你需要语言文件，你需要安装通用语言包`kde-l10n-**yourlanguagehere**` (e.g. [kde-l10n-zh_cn](https://www.archlinux.org/packages/?name=kde-l10n-zh_cn) 。你能够参考全部的语言包列表[this link](https://www.archlinux.org/packages/extra/any/kde-l10n/).

## 启动 Plasma

**Tip:**

*   Plasma 5不支持 [KDM](/index.php/KDM "KDM"). KDE 团队 [recommends](http://blog.davidedmundson.co.uk/blog/display_managers_finale)推荐使用 [SDDM](/index.php/SDDM "SDDM") 显示管理，因为他和Plasma 5桌面主题能够很好的整合。
*   推荐编辑`/etc/sddm.conf`使用微风主题，这样能够更好的和Plasma5整合。 参考 [SDDM#Theme settings](/index.php/SDDM#Theme_settings "SDDM")

在你的 [display manager](/index.php/Display_manager "Display manager") 菜单选择“Plasma”启动 Plasma 5 会话 。

你也可以在你的`.xinitrc`文件中添加`exec startkde`，用“startx”来启动 Plasma 桌面。如果你想在登录的时候开启 Xorg 请参考[Start X at login](/index.php/Start_X_at_login "Start X at login").

## 配置

KDE4 配置保存在 `~/.kde4` 目录中,其它配置现在位于标准的`~/.config`目录。如果 KDE 给你带来了很多麻烦或者你只是想全新安装 KDE，那么你只需要备份并重命名这个目录，然后重新启动你的 X 会话，KDE 会使用默认配置文件来重新创建它。如果你想要非常细粒度地控制 KDE 程序，可能需要编辑此目录中的文件。

然而，KDE的配置主要在**“系统设置”**里完成。在桌面上下文菜单中的“桌面设置”里也有一些桌面的其他选项。

其他没有包含在下文中的个性化设置如活动、桌面立方体上的不同壁纸等，请参考[Plasma](/index.php/Plasma "Plasma")的wiki页面。

### 个性化

如何将KDE桌面设置成您个人的样式：使用不同的 Plasma 主题，窗口装饰和图标主题。

#### Plasma 桌面

##### 主题

通过桌面设置的控制面板可以安装[Plasma主题](http://kde-look.org/index.php?xcontentmode=76&PHPSESSID=bba0ae5354c7818b519687ebf5badf0e)。Plasma主题定义了面板和 plasmoids 的样式。简单地安装到整个系统时，官方仓库和[AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go)中有一些主题。

##### 小工具

Plasmoid包含短的脚本（plasmoid scripts）或者编译过的（plasmoid binaries）的KDE应用程序，用于增强桌面的功能。 Plasmoid二进制文件可以从[AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v)上获得的PKGBUILD安装，或者您可以编写自己的PKGBUILD。 最简单的安装Plasmoid脚本的方式是右击面板或桌面：

```
添加部件 > 获得新部件 > 下载新 Plasma 部件

```

将显示 [kde-look.org](http://www.kde-look.org/) 的前端界面，一键就可以安装/卸载/更新三方 plasmoid 脚本。

大部分 plasmoids 都不是 KDE 正式开发者发布。此外还可以安装 Mac OS X 部件、Microsoft Windows Vista/7 部件、Google 部件甚至 SuperKaramba 部件。

##### 系统托盘中的声音应用

从官方源中安装 Kmix (KDE4 [kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix),Plasma 5 是[kmix](https://www.archlinux.org/packages/?name=kmix))，并从应用程序启动器运行。由于默认情况下， KDE 会自动启动以前会话中的程序，这个程序不需要每次登录时手动运行。

**Note:** 要调整 [音量增减的步长](https://bugs.kde.org/show_bug.cgi?id=313579#c28)，将诸如 `VolumePercentageStep=1` 一行添加到 `~/.kde4/share/config/kmixrc` 的 `[Global]` 一节中。

##### Adding a Global Menu to the desktop

Install [appmenu-qt](https://www.archlinux.org/packages/?name=appmenu-qt) from the official repositories and [appmenu-gtk](https://aur.archlinux.org/packages/appmenu-gtk/) and [appmenu-qt5](https://aur.archlinux.org/packages/appmenu-qt5/) from the AUR in order to complete the preliminaries for a Mac OS X style always-on global menu.

*   To get LibreOffice to use the global menu as well, install [libreoffice-extension-menubar](https://aur.archlinux.org/packages/libreoffice-extension-menubar/) from the AUR.
*   [appmenu-gtk](https://aur.archlinux.org/packages/appmenu-gtk/) is orphaned and Canonical has abandoned appmenu-gtk in favor of unity-gtk-module that is depending on Unity desktop. As of October 2014 there is no way of exporting gtk2,3 menus in KDE.
*   There is a patched package, [firefox-ubuntu](https://aur.archlinux.org/packages/firefox-ubuntu/) available in the AUR which has Canonical's patch for getting the global menu to work with the current version of Firefox (as of this writing).

To actually get the global menu, install [kdeplasma-applets-menubar](https://aur.archlinux.org/packages/kdeplasma-applets-menubar/) from the AUR. Create a plasma-panel on top of your screen and add the window menubar applet to the panel. To export the menus to your global menu, go to *System Settings > Application Appearance > Style*. Now click the fine-tuning tab and use the drop-down list to select *only export* as your menubar style.

#### 窗口装饰

[窗口装饰](http://kde-look.org/index.php?xcontentmode=75)可以在

```
系统设置 > 应用程序外观 > 风格

```

中设置。 您也可以在此处点击一下直接下载并安装更多的主题，一些主题可以在[AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v)上找到。

#### 图标主题

KDE4有不多的全系统图标。您可以打开**系统设置 > 应用程序外观 > 图标**并浏览一些新图标或手动安装它们。您可以在[kde-look.org](http://www.kde-look.org/)找到许多图标。

Arch Linux 的官方徽标、图标、CD标签和其它艺术作品都可以在[archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/)软件包中找到。安装后，你可以在`/usr/share/archlinux/`找到这些艺术作品。

#### Kicker菜单中的Arch Linux Logo图标

右击Kicker菜单按钮, 点击“**程序启动器设置**”，接着点击**右边**的图标。然后您可以选择Arch Linux图标或其他图标来代替默认图标。

Arch Linux 官方图库位于 [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/) 软件包，安装后位于

```
/usr/share/archlinux/icons

```

#### 字体

尝试安装 [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) 和 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 软件包。

安装后，确保注销并重新登录。不需要修改*系统设置 > 应用程序外观 > 字体*里的设置。

如果您个人已经设置了[字体](/index.php/Fonts "Fonts")渲染，小心系统设置可能会改变它们的外观。当改变了*系统设置 > 应用程序外观 > 字体*里的设置，系统将可能改写字体配置文件(`fonts.conf`)。

没有办法避免这种情况，但是如果把数值调到了匹配 `fonts.conf` 文件的话，所期望的字体渲染效果将会重新出现（这需要重启您的应用程序，在某些情况下可能需要重启桌面环境）。注意 Gnome 中的字体设置也会有这样的效果。

##### 字体太大或变形

从 *系统设置 > 应用程序外观 > 字体* 将字体 DPI 强制设置为 **96**

如果还是不行请尝试直接通过 Xorg 配置文件设置 DPI。[参见这里](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Setting_DPI_manually "Xorg (简体中文)").

#### 空间利用效率

小屏幕（例如上网本）的用户可以通过改变一些设置来提高KDE的空间利用效率，详细信息请查看 [上游wiki](http://userbase.kde.org/KWin#Using_with_small_screens_(eg_Netbooks))。另外，也可以使用 [KDE's Plasma Netbook](http://www.kde.org/workspaces/plasmanetbook/)，它是一个专为小型轻便的上网本设计的工作空间。

### 网络

你可以从以下工具中选择：

*   NetworkManager 。更多信息请参见 [NetworkManager](/index.php/NetworkManager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#KDE4 "NetworkManager (简体中文)")。
*   Wicd。更多信息请参见 [Wicd](/index.php/Wicd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wicd (简体中文)")。

### 打印

**小贴士:** 使用 [CUPS](/index.php/CUPS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "CUPS (简体中文)") 的 Web 接口进行快速配置。这种方式配置的打印机可以被 KDE 应用使用。

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

**小贴士:** 阅读 [CUPS#CUPS_administration](/index.php/CUPS#CUPS_administration "CUPS") 一文以获取关于如何配置 CUPS 的更多细节。

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

从 KDE 4.6起，KDE 不再管理 CPU 的频率调节，而是假设它由硬件及/或内核来自动管理。从版本 3.3 的内核起，Arch 使用 `ondemand` 作为默认 CPU 频率调速器。多数情况下不需要进行额外的配置。调节频率的细节，请参见[CPU 频率调节](/index.php/CPU_frequency_scaling_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "CPU frequency scaling (简体中文)")。

### 监视本地文件和目录的变化

KDE 现在通过 **kdirwatch**（位于 kdelibs 中）直接从内核中调用 **inotify**，所以不再需要 Gadmin 或者 FAM 了。你可能想安装 AUR 源中的 [kdirwatch](https://aur.archlinux.org/packages/kdirwatch/)，它是一个 kdirwatch 的图形界面前端。

## 系统管理

### 设置键盘布局

要做到这一点，来到：

```
系统设置 > 硬件 > 输入设备 > 键盘

```

可以在第一个标签中，选择键盘的型号。

在“**布局**”标签中，你可以按“添加”按钮选择语言，然后选择想使用的变体和语言。

在“**高级**”标签中，你可以在"Key(s) to change layout"子菜单中选择想要的键盘组合来改变布局。

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
*   [kcm-gtk](https://aur.archlinux.org/packages/kcm-gtk/)
*   [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)

**配置 GRUB 引导程序**

*   [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)

**配置基于 Synaptics 驱动程序的触摸板**

*   [kcm-touchpad](https://www.archlinux.org/packages/?name=kcm-touchpad)
*   [kcm-touchpad-frameworks](https://www.archlinux.org/packages/?name=kcm-touchpad-frameworks) (Plasma 5)

**配置 [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") (UFW)**

*   [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)

**配置 PolicyKit**

*   [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

**配置 Wacom tablets**

*   [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/)

**Systemd 设置**

*   [kcmsystemd](https://www.archlinux.org/packages/?name=kcmsystemd) (Plasma 5)

可从 [kde-apps.org](http://kde-apps.org/index.php?xcontentmode=273) 找到更多的 KCM 。

## 桌面搜索和语义桌面

根据 [维基百科](https://en.wikipedia.org/wiki/Semantic_desktop "wikipedia:Semantic desktop")，*"语义桌面是改变计算机的用户界面和数据处理能力，使得不同应用或任务之间分享变得更容易，过去不能自动处理的数据变得可能（自动处理）的各种想法的总称。"*

截止 KDE 4.13, KDE 对这个概念的实现关系到两个主要软件: Akonadi 和 Baloo 。这些程序检查计算机上的数据，然后建立便于搜索的索引。这样系统就知道您的数据，并使用元数据和用户提供的标签标记这些数据。Baloo 使用 Xapian 保存数据。

### Baloo

要在 KDE 桌面中使用 Baloo 搜索，按 `ALT+F2` 并输入你的查询内容。

By default the Desktop Search KCM exposes only two options: A panel to blacklist folders and, as of 4.13.1, a way to disable it with one click. More advanced configuration options are available through [kcm_baloo_advanced](https://aur.archlinux.org/packages/kcm_baloo_advanced/).

Alternatively you may edit to your `~/.kde4/share/config/baloofilerc` file. For example to disable Baloo add:

```
[Basic Settings]
Indexing-Enabled=false

```

   <small>*Note:* [Basic Settings] *section in* ~/.kde4/share/config/baloofilerc *also supports an* Enabled *entry if you want.*</small>

Once you added additional folders to the blacklist or disabled Baloo entirely, a process named `baloo_file_cleaner` removes all unneeded index files automatically. They are stored under `~/.local/share/baloo/`.

How do I index a removable device? By default every removable device is blacklisted. You just have to remove your device from the blacklist in the KCM panel.

### Akonadi

Akonadi 是系统中本地缓存各种来源的 PIM 数据的一种方法，接着这些数据可以被其它的应用使用。这包含了用户的邮件、联系人、日历、事件、刊物、闹钟、笔记等。

Akonadi 自身并不存储任何数据：存储格式依赖于数据的性质（例如，联系人可能以 vcard 格式存储）。

#### 运行不含 Akonadi 的 KDE

对于想运行不包含 Akonadi 的 KDE 的用户，软件包 [akonadi-fake](https://aur.archlinux.org/packages/akonadi-fake/) 是一个不错的选择。

#### 禁用 Akonadi

请参见 KDE userbase 的[这一节](http://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem)。或者从 [AUR](/index.php/AUR "AUR") 安装 [akonadi-fake](https://aur.archlinux.org/packages/akonadi-fake/).

#### 配置数据库

启动软件包 [kdepim-runtime](https://www.archlinux.org/packages/?name=kdepim-runtime) 中的 `akonaditray`，右键点击它并选择 **配置**。在 Akonadi 服务器配置标签中，你可以：

*   配置 Akonadi 使用 MySQL/MariaDB 服务器
*   配置 Akonadi 使用 PostgreSQL 服务器
*   配置 Akonadi 使用 SQLite

## Phonon

### Phonon 是什么？

摘自 [Wikipedia](https://en.wikipedia.org/wiki/Phonon "wikipedia:Phonon")： *Phonon 是 KDE 4 的多媒体 API。Phonon 允许 KDE 4 独立于任何一个多媒体框架（例如 GStreamer 或者 xine），并在KDE 4的生命周期中提供一份稳定的 API。由于各种原因而产生了它：创建一个简单的 KDE/Qt 风格的多媒体 API、更好地支持 Windows 和 Mac OS X下的原生多媒体框架以及修复无人维护的框架或者 API 或者 ABI 不稳定的问题。*

KDE 中广泛地使用 **Phonon** 于声音（例如系统通知或者 KDE 声音应用）和视频（例如 Dolphin 中的视频缩略图）中。

### 我应该选择哪个后端？

你可以在多个后端中选择，比如 [官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源") 中的 [phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer) 或者 VLC ([phonon-qt4-vlc](https://www.archlinux.org/packages/?name=phonon-qt4-vlc), [phonon-qt5-vlc](https://www.archlinux.org/packages/?name=phonon-qt5-vlc)))，[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 中的MPlayer （[phonon-qt4-mplayer-git](https://aur.archlinux.org/packages/phonon-qt4-mplayer-git/)）、（[phonon-quicktime-git](https://aur.archlinux.org/packages/phonon-quicktime-git/)）以及（[phonon-avkode-git](https://aur.archlinux.org/packages/phonon-avkode-git/)）。

VLC 有最好的上游支持，GStreamer 目前没有很好的维护。可以同时安装多个后端，并在 *系统设置 > 多媒体 > Phonon > 后端* 中进行选择。

**注意:** 根据 [KDE UserBase](http://userbase.kde.org/Phonon#Backend_libraries)，现在Phonon-MPlayer不受维护 。

根据 [KDE-Multimedia 邮件列表中的这封邮件](http://lists.kde.org/?l=kde-multimedia&m=137994906723790&w=2)，相比 GStreamer，用户更应选择 VLC。

## 常用的应用

可以在[这里](http://www.kde.org/applications/)找到官方的 KDE 应用集。

### Yakuake

[Yakuake](/index.php/Yakuake "Yakuake") 提供了一个 Quake-like 终端模拟器，使用 F12 来切换可视的状态。它还支持多标签。可以通过软件包 [yakuake](https://www.archlinux.org/packages/?name=yakuake) 来安装 Yakuake。

### KDE Telepathy

[KDE Telepathy](http://community.kde.org/KTp) 是一个把即时信息功能紧密整合到 KDE 桌面中的项目。它使用 Telepathy 框架作为后端，意在替代 Kopete。

要安装所有 Telepathy 协议，安装 [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) 组。 要使用 KDE Telepathy 客户端，安装 [kde-telepathy-meta](https://www.archlinux.org/packages/?name=kde-telepathy-meta) 软件包，它包含了所有在 [kde-telepathy](https://www.archlinux.org/groups/x86_64/kde-telepathy/) 组中的软件包。

#### Use Telegram with KDE Telepathy

Telegram protocol is avaible using [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), installing [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) or [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/). The username is the Telegram account telephone number (complete with the national prefix '+xx', e.g. '+39' for Germany). The configuration though the GUI may be tricky: if the phone number is not accepted when configuring a new account in the KDE Telepathy client (with an error message complaining about an invalid parameter which prevents the account creation), insert it between single quotes and then remove the quotes manually from the configuration file (`~/.local/share/telepathy/mission-control/accounts.cfg`) after the account creation (if the quotes are not removed after, an authentication error should rise). Note that the configuration file should be edited manually when KDE Telepathy is not running, e.g. when there is no KDE desktop session active, otherwise manual changes may be overwritten by the software.

## 提示和技巧

### Using an alternative window manager in KDE

To use an alternative [window manager](/index.php/Window_manager "Window manager") with KDE open the `systemsettings` panel and navigate to Default Applications > Window Manager > Use a different window manager and select the window manager you wish to use from the list.

#### KDE/Openbox Session

The [openbox](https://www.archlinux.org/packages/?name=openbox) package provides a session for using KDE with [Openbox](/index.php/Openbox "Openbox"). To make use of this session, select *KDE/Openbox* from the [display manager](/index.php/Display_manager "Display manager") menu.

For those starting the session manually, add the following line to your `.xinitrc` file:

```
exec openbox-kde-session

```

#### Compiz Custom

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

### Integrate Android with the KDE Desktop

KDE connect provides several features for you:

*   Share files and URLs to/from KDE from/to any app, without wires.
*   Touchpad emulation: Use your phone screen as your computer's touchpad.
*   Notifications sync (4.3+): Read your Android notifications from the desktop.
*   Shared clipboard: copy and paste between your phone and your computer.
*   Multimedia remote control: Use your phone as a remote for Linux media players.
*   WiFi connection: no usb wire or bluetooth needed.
*   RSA Encryption: your information is safe.

You will need to install KDE Connect both on your computer and on your Android. For PC side, install [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) if you are using KDE4 or if you are using Plasma 5, then you should install [kdeconnect-git](https://aur.archlinux.org/packages/kdeconnect-git/) instead. For Android side, install `KDE Connect` from the [Google Play Store](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp&hl=en) or from [F-Droid](https://f-droid.org/repository/browse/?fdid=org.kde.kdeconnect_tp).

### Get notifications for software updates

Install [apper](https://aur.archlinux.org/packages/apper/) to get notifications about package updates in your KDE system tray and a basic package manager GUI. See the [PackageKit website](http://www.packagekit.org/index.html) for more information.

### 配置 KWin 成使用 OpenGL ES

KWin 版本 4.8 开始，可以使用单独编译的二进制文件 **kwin_gles** 替换 kwin。它与在 OpenGL2 模式下执行的 kwin 基本相同，除了它使用 *egl* 来代替 *glx* 作为原生平台的接口这个小区别。要测试 kwin_gles，你可以在 Konsole 中运行 `kwin_gles --replace`。 如果你想使得这个改变持久化，你必须在 `$(kde4-config --localprefix)/env/` 中创建一个脚本，导出(export) `KDEWM=kwin_gles`。

### Konqueror/Dolphin 文件管理器中开启视频缩略图

对于 Konqueror 和 Dolphin 中的视频缩略图，安装 [kdemultimedia-mplayerthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-mplayerthumbs) 或者 [kdemultimedia-ffmpegthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-ffmpegthumbs)。

### 加速应用启动

用户 Rob 在他的博客中写道，这个“[技巧](http://kdemonkey.blogspot.nl/2008/04/magic-trick.html)”加快了应用程序的启动时间 50-150 毫秒。 要启用这个技巧，在你的 home 目录下面创建这个目录：

```
$ mkdir -p ~/.compose-cache

```

**注意:** 对于这中间发生了什么感到好奇的人来说，这个操作启用了一项前一段时间由 Lubos （以 general KDE speediness 知名） 提出，然后被重写并整合到 libx11 中的优化。应用平时启动时从 `/usr/share/X11/locale/<your locale>/Compose` 读取输入法信息，这个文件很长（对于 en_US.UTF-8 有超过 5000 行），需要不少时间来处理。libX11 可以缓存解析过的信息，以后读取时会快很多。但是它仅在目录存在时才会重用现有的缓存或者在 `~/.compose-cache` 中创建一份新的。

### 隐藏分区

Dolphin 中，简单得只要右键点击 'Places' 边栏中的分区并选择 '隐藏 “分区”'。否则...

如果你想阻止你的内部分区出现在文件管理器中，你可以创建一份 udev 规则，例如 `/etc/udev/rules.d/10-local.rules`：

```
KERNEL=="sda[0-9]", ENV{UDISKS_IGNORE}="1"

```

对于单个分区，也是相同的方法：

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

### Konqueror 技巧

#### 禁用页面快捷键的提示（浏览器）

要在 Konqueror 中禁用那些页面快捷键的提示（网页上按住`CTRL`键），使用 *设置 > 配置 Konqueror > Web 浏览* 并取消勾选 *用 Ctrl 键激活访问键* 或者打开 `~/.kde4/share/config/konquerorrc` 并添加这一部分：

```
[Access Keys]
Enabled=false

```

#### 禁用侧边栏标签（文件管理器）

要禁用左侧的侧边栏标签页，打开 `~/.kde4/share/config/konqsidebartng.rc`，把 `HideTabs` 置为 `true`。

#### 使用 WebKit

WebKit 是一个由 Apple 公司开发的开源浏览器引擎。它衍生自 KHTML 和 KJS 库并作了许多改进。Safari、 Google Chrome 和 rekonq 使用了 WebKit。

可以在 Konqueror 中使用 WebKit 代替 KHTML。首先安装 [kwebkitpart](https://www.archlinux.org/packages/?name=kwebkitpart) 软件包。

然后，运行 Konqueror 之后，访问 *设置 > 配置 Konqueror > 常规 > 默认网页浏览器引擎*，将其设置为 `WebKit`。

### Firefox 集成

参见 [Firefox](/index.php/Firefox#KDE_integration "Firefox")。

### 设置与当前桌面相同的屏幕保护背景

可以修改 Kscreensaver 的默认背景。

默认情况下，KDE [不能](https://bugs.kde.org/show_bug.cgi?id=312828)改变“简单的屏幕锁”的背景，但[有](http://forum.kde.org/viewtopic.php?f=66&t=110039)一种 [解决方法](http://lists.opensuse.org/opensuse-kde/2013-02/msg00082.html)：

 `/usr/share/apps/ksmserver/screenlocker/org.kde.passworddialog/contents/ui/` 
```
[...]
        *#source: theme.wallpaperPathForSize(parent.width, parent.height)*
        source: "1920x1080.jpg"
[...]

```

现在把你当前的背景图片复制到 `"1920x1080.jpg"`。

注意，你必须在每次更新软件包 [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/) 后重复这些步骤。

### Setting lockscreen wallpaper to arbitrary image

Copy an existing wallpaper profile as a template:

```
$ cp -r /usr/share/wallpapers/*ExistingWallpaper* ~/.kde4/share/wallpapers/

```

Change the name of the directory, and edit `metadata.desktop`:

 `~/.kde4/share/wallpapers/*MyWallpaper*/metadata.desktop` 
```
[Desktop Entry]
Name=MyWallpaper
X-KDE-PluginInfo-Name=MyWallpaper
```

Remove existing images (`contents/screenshot.png` and `images/*`):

```
$ rm ~/.kde4/share/wallpapers/MyWallpaper/contents/screenshot.png
$ rm ~/.kde4/share/wallpapers/MyWallpaper/contents/images/*

```

Copy new image in:

```
$ cp *path/to/MyWallpaper.png* MyWallpaper/contents/images/1920x1080.png

```

Edit the metadata profile for the current theme:

 `~/.kde4/share/apps/desktoptheme/MyTheme/metadata.desktop` 
```
[Wallpaper]
defaultWallpaperTheme=NewWallpaper
defaultFileSuffix=.png
defaultWidth=1920
defaultHeight=1080
```

Lock the screen to check that it worked.

**Note:** This method sets the lockscreen background without changing any system-wide settings. For a system-wide change, create the new wallpaper profile in `/usr/share/wallpapers`.

## 故障排除

#### Plasma 在 Intel 显卡上崩溃

根据 [kde-distro-packagers](https://mail.kde.org/pipermail/kde-distro-packagers/2015-August/000088.html) 中的邮件，Intel 显卡驱动使用 SNA 加速时会引起 Plasma 崩溃，出现这种问题时，请 [切换到 UXA](/index.php/Intel_graphics#SNA_issues "Intel graphics") 方式.

### 有关配置的问题

KDE 中许多问题都源自配置文件。解决升级问题的方法之一是使用一份全新的 KDE 配置。

#### 重置所有 KDE 配置

要测试问题是否由配置引起，试着登出来退出 KDE 会话，然后在终端中运行

```
$ cp ~/.kde4 ~/.kde4.safekeeping
$ rm .kde4/{cache,socket,tmp}-$(hostname)

```

"rm" 命令移除的符号链接会由 KDE 自动重建。现在启动一个新的 KDE 会话查看结果。

如果问题已经解决，你将会有一个全新无故障的 ~/.kde4。你可以逐步地把保存的旧配置移回来，并重启你的会话来测试，以鉴别配置文件中有问题的部分。某些文件会以应用名来命名，因此你可能不需要重启 KDE 就能进行测试。

#### Plasma 桌面行为异常

Plasma 故障通常是由不稳定的 **plasmoids** 或者 **plasma themes** 引起的。首先寻找最近安装的 plasmoid 或者 plasma 主题并禁用或者卸载它。

因此，如果你的桌面突然碰到 "locking up"，很可能是由于安装了有问题的组件造成的。如果你不记得故障发生前你安装了什么小部件（有时它可能是一个不寻常的问题），通过逐个移除小部件直到问题不再出现来跟踪这个问题。然后你可以卸载这个小部件，**仅当它是一个官方小部件时**到 bugs.kde.org 填写一份缺陷报告。如果它不是，我推荐你在 kde-look.org 上寻找它的条目并告知小部件的开发者你所碰到的问题（再现它的详细步骤等等）。

如果你找不到问题，也不想丢失 *所有的* KDE 设置，这样办：

```
 rm -r ~/.kde4/share/config/plasma*

```

这个命令将会**删除用户所有与 plasma 相关的配置**，当你重新登录进入 KDE，你将回到 **默认** 设置。你应该知道这个行为**不能撤消**。你应该创建一个备份目录并把所有与 plasma 相关的配置复制进去。

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

### 为了支持和调试获取 KWin 的当前状况

这行命令输出了一份关于 KWin 当前状况的精彩总结，包括使用的选项、使用的 compositing 后端以及相关 OpenGL 驱动的能力。更多信息参见 [Martin的博客](http://blog.martin-graesslin.com/blog/2012/03/on-getting-help-for-kwin-and-helping-kwin/)

qdbus org.kde.kwin /KWin supportInformation

### KDE4 不能结束载入

某些情况下启动 KDE4 时图形驱动可能会发生冲突。这种情形发生在登录之后加载完桌面之前，使得用户在载入屏幕中无限地等待。直到现在，确认受它影响的只有使用[Nvidia 驱动程序](/index.php/NVIDIA "NVIDIA")和 KDE4 的用户。

Nvidia 用户的一种解决方案是编辑 `/home/user/.kde4/share/config/kwinrc` 文件，更改 **[Compositing]** 一节中的选项 **Enabled=true** 为 **false**。要获得更多信息，可以查看[这篇](https://bbs.archlinux.org/viewtopic.php?pid=932598)贴子。

如果你进行了最小安装，请确保你已经安装了[#最小安装](#.E6.9C.80.E5.B0.8F.E5.AE.89.E8.A3.85)中列出的 phonon 后端所需的字体。

### KDE 和 Qt 程序在别的窗口管理器下很难看

如果你不在完整的 KDE 会话之中（特别是你没有运行 "startkde"）使用 KDE 或者 Qt 程序，那么直到 KDE 4.6.1，你需要告诉 Qt 怎么找到 KDE 的样式（Oxygen、QtCurve等等。）。

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

### 有关图形的故障

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

**注意:** 使用更强大的显卡时，尤其是 catalyst 私有驱动（fglrx）时，你也可能碰到这类 3D 桌面性能问题。这个驱动因 3D 加速故障而闻名。访问 [ATI 的 wiki 页面](/index.php/ATI "ATI") 来排除故障。

#### 有 Nvidia GPU 的系统中桌面混成被禁用

有时 KWin 的配置文件（**kwinrc**）中的配置 *可能* 在重新激活 3D 桌面 **OpenGL** 混成时引起问题。这可能是随机产生的，（例如，由于 Xorg 的突然崩溃或重启，文件被损坏了），因此，发生这种情况时，删除你的 `~/.kde4/share/config/kwinrc` 文件并重新登录。KWin 配置将变为 KDE 默认值，故障应该就没有了。

#### 启用混成后全屏时闪烁

从 KDE SC 4.6.0 起，有一个选项为 *系统设置 > 桌面效果 > 高级 > 为全屏窗口挂起桌面特效*，不选中它将使 kwin 禁用 unredirect fullscreen。

#### 启用混成后花屏

**注意:** 最近发布的 KDE 4.11 中添加了数件新的 Vsync 选项，可能对解决花屏有用。

启用混成时 KWin 可能花屏。不要选择位于 *系统设置 > 桌面效果 > 高级 > 避免撕裂(VSync) 中的 VSync 选项。*

私有驱动用户要确保启用了驱动的 VSync 选项（[Catalyst](/index.php/Catalyst "Catalyst") 用户运行 `amdccle`，而 [NVIDIA](/index.php/NVIDIA "NVIDIA") 用户运行 nvidia-settings）。

#### Display settings lost on reboot (multiple monitors)

Installing [kscreen](https://www.archlinux.org/packages/?name=kscreen) might fix the problem unless your screens share the same EDID. Kscreen is the improved screen management software for KDE, more information can be found [here](https://fedoraproject.org/wiki/Changes/KScreen?rd=Features/KScreen).

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

### KDE 在密码提示时每个字母用三颗星表示

可以通过 *系统设置 > 帐户细节 > 密码和用户信息* 将这项设置改为：

*   每个字母用一颗星表示
*   每个字母用三颗星表示
*   不显示

### Dolphin 和文件对话框启动极慢

这可能由 upower 服务引起。如果你的系统中不需要 upower 服务，可以禁用它：

```
  systemctl disable upower
  systemctl mask upower

```

就我所知，使用桌面电脑而非笔记本时，没有副作用。

### KDE 中 GTK 应用中默认的 PDF 查看器

某些情况下，当你安装了 [Inkscape](/index.php/Inkscape "Inkscape")， [Gimp](/index.php/Gimp "Gimp") 或者其它图像程序， GTK 应用（尤其是 [Firefox](/index.php/Firefox "Firefox")）可能不会使用 Okular 作为默认 PDF 应用，它们不会使用 KDE 中配置的默认应用。你可以使用以下命令来使 Okular 再次变成默认应用。

```
$ xdg-mime default kde4-okularApplication_pdf.desktop application/pdf

```

如果你使用别的 PDF 查看应用，或者另一种 mime-type 行为异常，你应该修改 `kde4-okularApplication_pdf.desktop` 和 `application/pdf` 为你需要的相应值。

更多信息，请查看 [Default applications](/index.php/Default_applications "Default applications") wiki 页面。

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

*   [[1]](http://www.kde.org) - KDE 主页
*   [[2]](https://bugs.kde.org) - KDE 缺陷跟踪页
*   [[3]](https://bugs.archlinux.org) - Arch Linux 缺陷跟踪页
*   [[4]](https://projects.kde.org) - KDE 项目