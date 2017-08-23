KDE 是一個功能豐富的桌面環境，以其整合良好的應用程式聞名，如 Konqueror、Dolphin、Plasma、KWrite 和 Konsole。

## Contents

*   [1 KDE SC 4.5 Arch Linux 註記](#KDE_SC_4.5_Arch_Linux_.E8.A8.BB.E8.A8.98)
    *   [1.1 KDE 4.5 Archlinux 套件的特殊資訊](#KDE_4.5_Archlinux_.E5.A5.97.E4.BB.B6.E7.9A.84.E7.89.B9.E6.AE.8A.E8.B3.87.E8.A8.8A)
*   [2 安裝 KDE 4.5 Software Compilation](#.E5.AE.89.E8.A3.9D_KDE_4.5_Software_Compilation)
    *   [2.1 安裝全套的 KDE SC](#.E5.AE.89.E8.A3.9D.E5.85.A8.E5.A5.97.E7.9A.84_KDE_SC)
    *   [2.2 最小安裝](#.E6.9C.80.E5.B0.8F.E5.AE.89.E8.A3.9D)
*   [3 啟動 KDE](#.E5.95.9F.E5.8B.95_KDE)
    *   [3.1 使用 KDM (KDE Display Manager)](#.E4.BD.BF.E7.94.A8_KDM_.28KDE_Display_Manager.29)
        *   [3.1.1 作為一個守護進程啟動 KDM](#.E4.BD.9C.E7.82.BA.E4.B8.80.E5.80.8B.E5.AE.88.E8.AD.B7.E9.80.B2.E7.A8.8B.E5.95.9F.E5.8B.95_KDM)
        *   [3.1.2 透過 /etc/inittab 啟動 KDM [*最佳*]](#.E9.80.8F.E9.81.8E_.2Fetc.2Finittab_.E5.95.9F.E5.8B.95_KDM_.5B.E6.9C.80.E4.BD.B3.5D)
    *   [3.2 使用 xinitrc](#.E4.BD.BF.E7.94.A8_xinitrc)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 個人化](#.E5.80.8B.E4.BA.BA.E5.8C.96)
        *   [4.1.1 Plasma 桌面](#Plasma_.E6.A1.8C.E9.9D.A2)
            *   [4.1.1.1 主題](#.E4.B8.BB.E9.A1.8C)
            *   [4.1.1.2 元件](#.E5.85.83.E4.BB.B6)
        *   [4.1.2 視窗外框](#.E8.A6.96.E7.AA.97.E5.A4.96.E6.A1.86)
        *   [4.1.3 KDE 4 Theme Integration with GTK Applications](#KDE_4_Theme_Integration_with_GTK_Applications)
            *   [4.1.3.1 Automatic procedure](#Automatic_procedure)
            *   [4.1.3.2 Manual procedure](#Manual_procedure)
            *   [4.1.3.3 圖示](#.E5.9C.96.E7.A4.BA)
        *   [4.1.4 圖示主題](#.E5.9C.96.E7.A4.BA.E4.B8.BB.E9.A1.8C)
        *   [4.1.5 Arch Linux Logo Icon in Kicker menu](#Arch_Linux_Logo_Icon_in_Kicker_menu)
        *   [4.1.6 字型](#.E5.AD.97.E5.9E.8B)
        *   [4.1.7 空間效率](#.E7.A9.BA.E9.96.93.E6.95.88.E7.8E.87)
            *   [4.1.7.1 All sorts of *bars](#All_sorts_of_.2Abars)
            *   [4.1.7.2 Plasma](#Plasma)
            *   [4.1.7.3 KWin](#KWin)
    *   [4.2 網絡/列印](#.E7.B6.B2.E7.B5.A1.2F.E5.88.97.E5.8D.B0)
    *   [4.3 Samba/Windows 支援](#Samba.2FWindows_.E6.94.AF.E6.8F.B4)
    *   [4.4 KDE 桌面活動](#KDE_.E6.A1.8C.E9.9D.A2.E6.B4.BB.E5.8B.95)
    *   [4.5 省電](#.E7.9C.81.E9.9B.BB)
        *   [4.5.1 如何啟用一般的省電](#.E5.A6.82.E4.BD.95.E5.95.9F.E7.94.A8.E4.B8.80.E8.88.AC.E7.9A.84.E7.9C.81.E9.9B.BB)
        *   [4.5.2 How to enable Cpufreq based powersaving](#How_to_enable_Cpufreq_based_powersaving)
*   [5 系統管理](#.E7.B3.BB.E7.B5.B1.E7.AE.A1.E7.90.86)
    *   [5.1 設定鍵盤排版，以便切換輸入語言](#.E8.A8.AD.E5.AE.9A.E9.8D.B5.E7.9B.A4.E6.8E.92.E7.89.88.EF.BC.8C.E4.BB.A5.E4.BE.BF.E5.88.87.E6.8F.9B.E8.BC.B8.E5.85.A5.E8.AA.9E.E8.A8.80)
    *   [5.2 Terminate Xorg-server through KDE system settings](#Terminate_Xorg-server_through_KDE_system_settings)
*   [6 桌面搜尋和語義學桌面](#.E6.A1.8C.E9.9D.A2.E6.90.9C.E5.B0.8B.E5.92.8C.E8.AA.9E.E7.BE.A9.E5.AD.B8.E6.A1.8C.E9.9D.A2)
    *   [6.1 Soprano](#Soprano)
    *   [6.2 Nepomuk](#Nepomuk)
    *   [6.3 Akonadi](#Akonadi)
    *   [6.4 Strigi 搜尋](#Strigi_.E6.90.9C.E5.B0.8B)
*   [7 KDM (KDE Desktop Manager)](#KDM_.28KDE_Desktop_Manager.29)
    *   [7.1 KDM Xserver 檔案](#KDM_Xserver_.E6.AA.94.E6.A1.88)
    *   [7.2 配置 KDM](#.E9.85.8D.E7.BD.AE_KDM)
        *   [7.2.1 使用者配置 KDM 的問題](#.E4.BD.BF.E7.94.A8.E8.80.85.E9.85.8D.E7.BD.AE_KDM_.E7.9A.84.E5.95.8F.E9.A1.8C)
*   [8 Phonon](#Phonon)
    *   [8.1 什麼是 Phonon？](#.E4.BB.80.E9.BA.BC.E6.98.AF_Phonon.EF.BC.9F)
    *   [8.2 Which backend should I choose ?](#Which_backend_should_I_choose_.3F)
*   [9 使用 WebKit 在 Konqueror](#.E4.BD.BF.E7.94.A8_WebKit_.E5.9C.A8_Konqueror)
    *   [9.1 什麼是 WebKit？](#.E4.BB.80.E9.BA.BC.E6.98.AF_WebKit.EF.BC.9F)
    *   [9.2 如何用於 konqueror](#.E5.A6.82.E4.BD.95.E7.94.A8.E6.96.BC_konqueror)
*   [10 疑難解答](#.E7.96.91.E9.9B.A3.E8.A7.A3.E7.AD.94)
    *   [10.1 KHotkeys 問題](#KHotkeys_.E5.95.8F.E9.A1.8C)
    *   [10.2 Enabling thumbnails under Konqueror and Dolphin file managers](#Enabling_thumbnails_under_Konqueror_and_Dolphin_file_managers)
    *   [10.3 I encounter problems with automounting (or) KDE behaves strangely for no apparent reason](#I_encounter_problems_with_automounting_.28or.29_KDE_behaves_strangely_for_no_apparent_reason)
    *   [10.4 圖形的相關問題](#.E5.9C.96.E5.BD.A2.E7.9A.84.E7.9B.B8.E9.97.9C.E5.95.8F.E9.A1.8C)
        *   [10.4.1 2D桌面效能低落（或）2D 出現假影](#2D.E6.A1.8C.E9.9D.A2.E6.95.88.E8.83.BD.E4.BD.8E.E8.90.BD.EF.BC.88.E6.88.96.EF.BC.892D_.E5.87.BA.E7.8F.BE.E5.81.87.E5.BD.B1)
        *   [10.4.2 Konsole is slow in applications like vim](#Konsole_is_slow_in_applications_like_vim)
        *   [10.4.3 低落的 3D 桌面效能](#.E4.BD.8E.E8.90.BD.E7.9A.84_3D_.E6.A1.8C.E9.9D.A2.E6.95.88.E8.83.BD)
            *   [10.4.3.1 KDE 4.5 specific graphics' issues](#KDE_4.5_specific_graphics.27_issues)
    *   [10.5 KDE 下的聲音問題](#KDE_.E4.B8.8B.E7.9A.84.E8.81.B2.E9.9F.B3.E5.95.8F.E9.A1.8C)
        *   [10.5.1 ALSA 相關問題](#ALSA_.E7.9B.B8.E9.97.9C.E5.95.8F.E9.A1.8C)
            *   [10.5.1.1 "Falling back to default" messages when trying to listen to any sound in KDE](#.22Falling_back_to_default.22_messages_when_trying_to_listen_to_any_sound_in_KDE)
            *   [10.5.1.2 I cannot play mp3 files when having Gstreamer backend in Qt Phonon](#I_cannot_play_mp3_files_when_having_Gstreamer_backend_in_Qt_Phonon)
            *   [10.5.1.3 Amarok "waits" before playing any track](#Amarok_.22waits.22_before_playing_any_track)
        *   [10.5.2 OSS4 相關問題](#OSS4_.E7.9B.B8.E9.97.9C.E5.95.8F.E9.A1.8C)
    *   [10.6 Arch linux 特定的打包問題](#Arch_linux_.E7.89.B9.E5.AE.9A.E7.9A.84.E6.89.93.E5.8C.85.E5.95.8F.E9.A1.8C)
    *   [10.7 我想要一個最小化安裝的 KDE。當我安裝套件後並登入 KDE，但沒有面板出現](#.E6.88.91.E6.83.B3.E8.A6.81.E4.B8.80.E5.80.8B.E6.9C.80.E5.B0.8F.E5.8C.96.E5.AE.89.E8.A3.9D.E7.9A.84_KDE.E3.80.82.E7.95.B6.E6.88.91.E5.AE.89.E8.A3.9D.E5.A5.97.E4.BB.B6.E5.BE.8C.E4.B8.A6.E7.99.BB.E5.85.A5_KDE.EF.BC.8C.E4.BD.86.E6.B2.92.E6.9C.89.E9.9D.A2.E6.9D.BF.E5.87.BA.E7.8F.BE)
    *   [10.8 我想要在我的系統安裝一個全新的 KDE。我應該怎麼做？](#.E6.88.91.E6.83.B3.E8.A6.81.E5.9C.A8.E6.88.91.E7.9A.84.E7.B3.BB.E7.B5.B1.E5.AE.89.E8.A3.9D.E4.B8.80.E5.80.8B.E5.85.A8.E6.96.B0.E7.9A.84_KDE.E3.80.82.E6.88.91.E6.87.89.E8.A9.B2.E6.80.8E.E9.BA.BC.E5.81.9A.EF.BC.9F)
    *   [10.9 Plasma 桌面行為奇怪，但我不知道該怎麼辦](#Plasma_.E6.A1.8C.E9.9D.A2.E8.A1.8C.E7.82.BA.E5.A5.87.E6.80.AA.EF.BC.8C.E4.BD.86.E6.88.91.E4.B8.8D.E7.9F.A5.E9.81.93.E8.A9.B2.E6.80.8E.E9.BA.BC.E8.BE.A6)
*   [11 其他 KDE 專案](#.E5.85.B6.E4.BB.96_KDE_.E5.B0.88.E6.A1.88)
    *   [11.1 Chakra 專案](#Chakra_.E5.B0.88.E6.A1.88)
        *   [11.1.1 Split KDE packages](#Split_KDE_packages)
        *   [11.1.2 Chakra 專案 Arch Live CD](#Chakra_.E5.B0.88.E6.A1.88_Arch_Live_CD)
        *   [11.1.3 Passing from KDEmod to [extra]'s KDE](#Passing_from_KDEmod_to_.5Bextra.5D.27s_KDE)
    *   [11.2 KDE unstable](#KDE_unstable)
        *   [11.2.1 KDEmod testing/unstable](#KDEmod_testing.2Funstable)
        *   [11.2.2 KDE unstable (快照)](#KDE_unstable_.28.E5.BF.AB.E7.85.A7.29)
            *   [11.2.2.1 非官方的 kde-unstable](#.E9.9D.9E.E5.AE.98.E6.96.B9.E7.9A.84_kde-unstable)
            *   [11.2.2.2 半官方的 kde-unstable](#.E5.8D.8A.E5.AE.98.E6.96.B9.E7.9A.84_kde-unstable)
    *   [11.3 KDE Legacy](#KDE_Legacy)
        *   [11.3.1 Downgrading to KDEmod3 from KDE 4](#Downgrading_to_KDEmod3_from_KDE_4)
        *   [11.3.2 Unofficial community repository for KDEmod3](#Unofficial_community_repository_for_KDEmod3)
*   [12 Bugs](#Bugs)
    *   [12.1 Common bugs](#Common_bugs)
    *   [12.2 發行版和上游的錯誤回報](#.E7.99.BC.E8.A1.8C.E7.89.88.E5.92.8C.E4.B8.8A.E6.B8.B8.E7.9A.84.E9.8C.AF.E8.AA.A4.E5.9B.9E.E5.A0.B1)
*   [13 外部鏈接](#.E5.A4.96.E9.83.A8.E9.8F.88.E6.8E.A5)

## KDE SC 4.5 Arch Linux 註記

**KDE 4.5** Software Compilation is the current major release of KDE that includes a number of improvements and bug fixes. The new Arch package set for KDE makes it possible to only install those applications you like.

Important features of the Archlinux KDE SC in short:

*   **Split packages**; for more Information see [KDE Packages](/index.php/KDE_Packages "KDE Packages").
*   You can use different Phonon backends, like Gstreamer or Xine
*   Meta packages ensure a smooth upgrade and emulate the old monolith packages for those who prefer them.

Important hints for upgraders:

*   Always check if your mirror is **up to date**.
*   pacman will ask you to replace **all** kde packages with kde-meta packages.
*   **Do not force an update**. If pacman complains about conflicts please **file a bug report**.
*   You can remove the meta packages and the sub packages you do not need after the update.
*   If you do not like split packages just keep using the kde-meta packages.

	Information about upstream changes are be available [here](http://kde.org/announcements/4.5)

### KDE 4.5 Archlinux 套件的特殊資訊

*   KDEpim has seen no new release, please continue to use version 4.4.5\. KDEpim 4.5 shall be released with KDE 4.5.1
*   Due to incompatibility with ruby 1.9, ruby kdebindings are not provided
*   Webkit support in konqueror is provided by kwebkitpart
*   KDM is now started as the kdm user
*   Upstream removed five translations: csb, mai, mk, si and tg

## 安裝 KDE 4.5 Software Compilation

### 安裝全套的 KDE SC

要安裝全部的 KDE 設定，首先要**完整升級您的系統**:

```
pacman -Syu

```

然後：

```
pacman -S kde

```

如果你需要語言檔案：

```
pacman -S kde-l10n-您的語言

```

例如 kde-l10n-**de**，就是德語。

如果你需要安裝正體中文,你可以安裝 kde-l10n-zh_tw

```
pacman -S kde-l10n-zh_tw

```

**Note:** KDE 4.x 是**模塊化**的，你可以安裝自己偏愛的 KDE 應用程式，而不必安裝所有的套件。請見 [KDE Packages](/index.php/KDE_Packages "KDE Packages") 獲得更多資訊。

### 最小安裝

如果你想有一個最小安裝的 KDE SC，這裡有一個範例：

```
pacman -S kdebase-workspace kdebase-konsole

```

## 啟動 KDE

啟動 KDE 的方法，取決於你的喜好。基本上有兩種方式啟動 KDE。使用 **KDM** 或 **xinitrc**。

### 使用 KDM (KDE Display Manager)

*It is highly recommended to get familiar with the [full article](/index.php/Display_manager "Display manager") concerning display managers, before you make any changes.*

#### 作為一個守護進程啟動 KDM

增加 "**kdm**" (不需要雙引號) 到 daemons 陣列裡面, 設定檔案的路徑在 **`/etc/rc.conf`**

```
DAEMONS=(dbus hal syslog-ng network netfs crond ... **kdm**)

```

#### 透過 /etc/inittab 啟動 KDM [*最佳*]

編輯 **`/etc/inittab`** 並註釋掉：

```
#id:3:initdefault:

[...]

#x:5:respawn:/usr/bin/xdm -nodaemon

```

然後去掉下面的註釋：

```
id:5:initdefault:

[...]

x:5:respawn:/usr/bin/kdm -nodaemon

```

**Note:** 這兩種方法 KDM 會自動加載 Xorg。

### 使用 xinitrc

***xinitrc** 的觀念在 [這裡](/index.php/Xinitrc "Xinitrc") 有非常完整的解釋*

編輯 **`/home/`**`*你的帳號*`**`/.xinitrc`**. 然後取消下面這行的註解:

```
exec startkde 

```

經過重開機或登出重新登入, Xorg (**startx** 或 **xinit**) 中的指令將在KDE啟動的時候自動執行.

**警告:** By doing this you won't have restart/shutdown functions enabled in your KDE menu.

**注意:** 如果你想要在boot的時候啟動Xorg, 請參考 [Start X at login](/index.php/Start_X_at_login "Start X at login") 一文.

## 配置

**Note:** 配置 KDE 主要是使用'**系統設定'**。當你右擊桌面時，'桌面設定'還有一些其他的選項可用於桌面。

For other personalization options not covered below such as activities, different wallpapers on one cube, etc please refer to the [Plasma](/index.php/Plasma "Plasma") wiki page.

### 個人化

如何建立您個人風格的 KDE 桌面，使用不同的 Plasma 主題、視窗外框和圖示主題。

#### Plasma 桌面

[Plasma](/index.php/Plasma "Plasma") 是一種桌面整合技術。提供多種功能，從顯示壁紙到新增元件到桌面。

##### 主題

可以透過桌面設定控制面板安裝[Plasma 主題](http://kde-look.org/index.php?xcontentmode=76&PHPSESSID=bba0ae5354c7818b519687ebf5badf0e)。Plasma 主題定義您的面板和 plasmoids 的外觀。如果你想要用系統安裝他們，主題可以在官方套件庫和 [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go) 中找到。

##### 元件

Plasmoids 是一個小腳本或程式碼寫成的 KDE 應用程式，可以以非常愉快的方式提升您桌面的功能。基於 KDE 的 Plasma 技術。您能夠顯示系統關鍵資訊像*剩餘硬碟空間*或*網絡連接監視器*。 取得更多元件的最簡單的方法，是左鍵點擊一個面板或桌面：

```
新增元件 -> 取得新元件 -> 下載元件

```

這會呈現出一個不錯的 [kde-look.org](http://www.kde-look.org/) 前端。並只需點擊一下滑鼠，就可讓您（反）安裝元件。 [套件庫](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v)也可取得它們。

#### 視窗外框

[視窗外框](http://kde-look.org/index.php?xcontentmode=75)可以修改，藉由

```
系統設定 -> 應用程序外觀 -> 風格

```

在這裡，您只要按一下就可以直接下載和安裝更多的主題。有些可以用 [AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v) 取得。

#### KDE 4 Theme Integration with GTK Applications

To better integrate GTK and KDE 4 themes, you can use **QtCurve**.

```
pacman -S qtcurve-gtk2 qtcurve-kde4

```

Or you can download a GTK theme that matches your version of KDE [here](http://kde-look.org/content/show.php?content=103741). This theme comes closer to the original Oxygen and is updated frequently.

##### Automatic procedure

To change the GTK theme to QtCurve or something else a few applications are available:

```
pacman -S lxappearance
pacman -S gtk-theme-switch2
pacman -S gtk-chtheme

```

Then change the theme of your choice in the respective application:

```
lxappearance
gtk-theme-switch2
gtk-chtheme

```

##### Manual procedure

To manually change the GTK theme to QtCurve, you need to create the file `~/.gtkrc-2.0-kde4` with the following content:

```
include "/usr/share/themes/QtCurve/gtk-2.0/gtkrc"
include "/etc/gtk-2.0/gtkrc"

style "user-font"
{
    font_name="Sans Serif"
}
widget_class "*" style "user-font" 
gtk-theme-name="QtCurve"

```

Then you need to create the symbolic link `~/.gtkrc-2.0`:

```
ln -s .gtkrc-2.0-kde4 .gtkrc-2.0

```

If you want also specify a font, you can add (and adapt) the following line to the file:

```
 gtk-font-name="Sans Serif 9"

```

##### 圖示

If you're using Oxygen icons and want a consistent look in GTK open/save dialogs, you can install an [oxygenrefit2](https://aur.archlinux.org/packages.php?O=0&K=oxygenrefit2-icon-theme&do_Search=Go) icon theme from AUR and set it as your GTK icon theme. Add the theme to the `~/.gtkrc-2.0` file or you can use lxappearance and set it.

```
gtk-icon-theme-name="OxygenRefit2"

```

There are also a couple GTK themes built on the [gtk-kde42-oxygen-theme Oxygen style](https://aur.archlinux.org/packages.php?ID=24329) that can also do this.

#### 圖示主題

Not many full system icons themes are available for KDE 4\. You can open up **System Settings > Application Appearance > Icons** and browse for new ones or install them manually. Many of them can be found on [kde-look.org](http://www.kde-look.org/).

#### Arch Linux Logo Icon in Kicker menu

Right-Click on the Kicker menu button, press "**Application launcher settings**" and then press the icon on the **right**. Then you may choose Arch Linux icon or any other icon that will replace the default one.

#### 字型

如果預設情況下，KDE 的字型看起來不佳，嘗試安裝 [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) 和 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 套件。安裝之後，一定要登出並重新登入。您不必修改 KDE 系統設定中"字型"面板的任何設定。

If you have personally set up how your [Fonts](/index.php/Fonts "Fonts") render, be aware that System Settings may alter their appearance. When you go **System Settings > Appearance > Fonts** System Settings will likely alter your font configuration file (`fonts.conf`). There is no way to prevent this but if you set the values to match your `fonts.conf` file the expected font rendering will return (it will require you to restart your application or in a few cases for you to have to restart your desktop). Note too that Gnomes' Font Preferences will also do this if you use both desktop environments.

#### 空間效率

KDE is often **critizised** for being bloated. The user might get this perception from seeing **many toolbars and pretty big scaled icons in the applications**. One thing that improved the situation was the new Kwin-Theme that came with KDE SC 4.4.* with the more elegant buttons that one can also resize. **KDE Apps allows to hide many toolbars, menubars and statusbars**.

##### All sorts of *bars

Most toolbars of a program can be removed in the menubar-entry "**Settings**". There you often can hide the statusbar and often all toolbars. The last step should be to remove the menubar itself via **Ctrl + M**. If you do not want to remove any bars you can still make them smaller or remove the text via:

```
System-Settings -> Appearance -> Style -> Tab "Finetuning" ->  "Main toolbar text", "secondary toolbar text"

```

Since most aspect ratios of modern flat screens are wider than 4:3 it could be reasonable to put the toolbar **at the left or right of a window** to artificially stretch windows more to the monitors aspect ratio.

##### Plasma

There are also some settings and modifications you can apply to your plasmoids to make KDE less space wasting. For example, the "Digital Clock" wastes more space than the "Analogue Clock". The little plasma icon ("Casheew") that one can see in the panel can be hidden by locking the widgets via rightklicking onto the panel. If you have got many tasks in your task-manager you should consider using *Smooth-tasks*. This alternative task-manager allows you to just display the icons of a task thus using less space but still maintaining the ability of the user to distinguish the different tasks.

```
Install [smooth-tasks](https://aur.archlinux.org/packages.php?ID=29410) from the [AUR](/index.php/AUR "AUR").

```

After installing and substituting it with the original task-manager you should have a deep look at the settings since they are much broader. one way of using the features of smooth-tasks could be to only display the icons of tasks and move the panel to the left or right of the screen. This is most usefull on widescreens. On very small screens it could be reasonable to set the bottom-panel to auto-hide completely. For netbooks there exists a special form factor to make a better use of the screen:

```
System-Settings -> Desktop -> Workspace -> Form factor

```

##### KWin

The windows decorations can also be resized by making the buttons in the decoration smaller thus making the whole top border smaller:

```
System Settings -> Appearance -> Windows -> Button size

```

You could also remove the side-border of all windows via:

```
System Settings -> Appearance -> Windows -> Border size

```

### 網絡/列印

KDE SC 4.5 已經加入 NetworkManager 支援。請見 [NetworkManager](/index.php/NetworkManager#KDE4 "NetworkManager") 了解更多資訊。

### Samba/Windows 支援

如果你想要訪問 Windows 服務：

```
pacman -S samba

```

然後，您可以配置您的 Samba 共享，透過

```
 系統設定 > 共享 > Samba

```

### KDE 桌面活動

KDE are Plasma based "virtual desktop"-like set of Plasma Widgets where you can independently configure widgets as if you had more than one screens/desktops. Since KDE 4.5, the feature of changing Desktop Activities has been simplified.

On your desktop, click the Cashew Plasmoid and on the pop-up window press "Activities".

A plasma bar will appear at the bottom of the screen which presents you the current Plasma Desktop Activities which exist. You can then navigate between them by pressing their correspondent icon.

### 省電

KDE 整合了省電服務，稱為"*Powerdevil電源管理'*"，可以調整省電系統配置或螢幕的亮度（如果支援）。

#### 如何啟用一般的省電

進入系統設定>電源管理。 進入設定檔管理員，進入"當市電電源已插上時"（或電池選項）勾選"省電"。在"編輯設定檔">"省電"，勾選"開啟系統省電模式"，然後按套用。

#### How to enable Cpufreq based powersaving

Since KDE 4.5, [Powerdevil doesn't handle CPU power schemes through Cpufreq](http://lists.kde.org/?l=kde-devel&m=126800277431817&w=2). CPU is being used by using the hardware or/and kernel "**ondemand**" governor power scheme and that's the official way to have the system's power management handled, according to the guidelines by the kernel power-management devs.

**Warning:** Using Cpufreq in order to handle your CPU power schemes, that means, controlling it through software, IS NOT suggested for use since modern CPUs are capable of powersaving through their BIOSes. [Visit this link](http://www.codon.org.uk/~mjg59/power/good_practices.html) for more info on good power management practices.

If you do want, you still can use Cpufreq for your system which is accessible through the **Solid Device Framework**.

So in order to do that, follow these steps:

1\. You need to create a script for every Cpufreq governor you want to be used. In this example, you will now create a script to enable the powersaving governor.

Create a script in /usr/bin

```
 # touch /usr/bin/kde-cpufreq-powersave

```

Add these in the script

```
 #!/bin/bash
 solid-powermanagement set cpufreq powersave

```

Make it executable

```
 # chmod +x /usr/bin/kde-cpufreq-powersave

```

2\. Install cpufrequtils

```
pacman -S cpufrequtils

```

and make sure you have your CPU's cpufreq module loaded. For more information on this, visit [this article](/index.php/Cpufreq "Cpufreq").

3\. Then, in **System Settings > Power Management**, go to "Edit Profiles" > "Powersave", and make sure that "Enable System power saving" is enabled.

After that, press the file dialog button next to the phrase "When loading profile execute" and choose the script you have just created. Now, each time you choose the Powersaving profile through Powerdevil, Cpufreq will force the powersaving governor.

You can do the same for other profiles and governors.

## 系統管理

### 設定鍵盤排版，以便切換輸入語言

In order to do that, navigate to

```
   System Settings > Input Devices > Keyboard

```

There you may choose your keyboard model at first.

**Note:** It is preferable that, if you use Evdev, that means Xorg automatic configuration for keyboards, you should choose "Evdev-managed keyboard".

In the "**Layouts**" tab, you choose the languages you may want to use by pressing the "Add Layout" button and therefore the variant and the language. In the "**Advanced**" tab, you can choose the keyboard combination you want in order to change the layouts in the "Key(s) to change layout" sub-menu.

### Terminate Xorg-server through KDE system settings

Navigate to

```
   System Settings > Input Devices > Keyboard > Advanced (tab) > "Key Sequence to terminate X server" submenu

```

and tick the checkbox.

## 桌面搜尋和語義學桌面

Most users who freshly install KDE are wondering what functionality the following four pieces of software are able to offer. Most features are still somehow hidden under the hood and yet not many applications featured in the KDE SC are using these interfaces. This capter intends to first explain the features and then convince the user of the power these tools offer once properly integrated into KDE. The following sections are more or less a roughly shortened version of [[this blogpost](http://thomasmcguire.wordpress.com/2009/10/03/akonadi-nepomuk-and-strigi-explained/).

### Soprano

Soprano is a library for QT that is able to process RDF data. This is semantic data. Semantic data is a special kind of metadata which is much more flexible than metadata you might know from MP3-Tags or Meta-Tags in HTML since RDF data more resembles the structure of a spoken sentence, thus allowing a much wider field of ways dealing with them. Soprano stores semantic data in a backend and allows low level access to this data.

### Nepomuk

Nepomuk is somehow the glue between Soprano and the KDE Desktop and thus the user. Nepomuk allows to tag the files with various entries and offers an API for the applications featured in KDE SC. It is enabled by default. Nepomuk can be turned on and off in

```
System Settings -> "Advanced" Tab -> Desktop Search

```

### Akonadi

Akonadi is one of the ways of getting data into Nepomuk. Its intention is to gather all kinds of PIM data from KMail, KAdressbook or Kopete. It collects chat contacts, email adresses, email attachments and email contents. First of all it feeds Nepomuk with this data but moreover does also provide a centralized accesspoint for all this data.

### Strigi 搜尋

Strigi is another way of feeding data into Nepomuk. It preverably indexes the users home-folder. Indexing means that it not only gathers filenames but also information about your music collection or tagged downloads you did with Kget. The Strigi search is also integrated into KDEs launcher which can be accessed via: `Alt` + `F2`

By default, Dolphin has a search bar on top-right where you may type what you want to be found from Strigi's index.

**Note:** Strigi has implications for resource usage on your computer - CPU, memory, disk access, disk space, battery life. If Strigi is too resource-hungry for you, you can turn it off in "**System Settings > Advanced > Desktop Search**".

Strigi folder indexing can be configured in:

```
System Settings -> "Advanced" Tab -> Desktop Search

```

## KDM (KDE Desktop Manager)

### KDM Xserver 檔案

An example configuration for KDM can be found at **/usr/share/config/kdm/kdmrc**. See **/usr/share/doc/HTML/en/kdm/kdmrc-ref.docbook** for all options.

### 配置 KDM

您可以訪問**系統設定 > 登入畫面**進行修改。當你按下"套用"時，會出現一個 **KDE Polkit 授權**視窗要求您提供 root 密碼，才能完成修改。

#### 使用者配置 KDM 的問題

If you seem not to be able to KDM settings when launching System Settings as user, press

`Alt` + `F2`

and type

```
 kdesu systemsettings

```

In the pop-up kdesu window, enter your root password and wait for System Settings to be launched.

**Note:** Since you have launched it as root, be careful when changing your settings. All settings configuration in root-launched System Settings are saved under /root/.kde4 and not under ~/.kde4 (your home location).

In the System Settings window, go to Login Screen.

## Phonon

### 什麼是 Phonon？

*Phonon is the multimedia API for KDE 4\. Phonon was created to allow KDE 4 to be independent of any single multimedia framework such as GStreamer or xine and to provide a stable API for KDE 4's lifetime. It was done for various reasons: to create a simple KDE/Qt style multimedia API, to better support native multimedia frameworks on Windows and Mac OS X, and to fix problems of frameworks becoming unmaintained or having API or ABI instability.*

from Wikipedia.

**Phonon** is being widely used within KDE, for both audio (e.g., the System notifications or KDE audio apps) and video (e.g., the Dolphin video thumbnails).

### Which backend should I choose ?

You can choose between various backends, like Gstreamer, Xine ( [phonon-xine](https://www.archlinux.org/packages/?q=phonon) ) or VLC ( [phonon-vlc](https://www.archlinux.org/packages/?q=phonon-vlc) ).

## 使用 WebKit 在 Konqueror

### 什麼是 WebKit？

WebKit is an open source browser engine developped by Apple Inc. It is used by Safari and Google Chrome. WebKit is a derivative from the KHTML and KJS libraries and contain many improvements.

### 如何用於 konqueror

It is possible to use WebKit in Konqueror instead of KHTML. First install the kwebkitpart package :

```
 pacman -S kwebkitpart

```

Then execute the following command

```
 keditfiletype text / html

```

In the window that opens go to the "Embedding" tab. Move the entry "WebKit" up to the top of the list and then hit the "OK" button and restart Konqueror.

## 疑難解答

### KHotkeys 問題

Ιf **khotkeys** does not work, make sure you have a fully updated system first. You can also create ~/.kde4/Autostart/reloadkhotkeys.sh with contents

```
#!/bin/bash
(sleep 3 && qdbus org.kde.kded /modules/khotkeys reread_configuration) &

```

and then do a

```
chmod u+x ~/.kde4/Autostart/reloadkhotkeys.sh

```

then logout & login.

### Enabling thumbnails under Konqueror and Dolphin file managers

For thumbnails of videos in konqueror and dolphin:

```
 pacman -S kdemultimedia-mplayerthumbs

```

### I encounter problems with automounting (or) KDE behaves strangely for no apparent reason

Since the new X-Server 1.8 arrived in the stable repos some users got the impression that HAL (Hardware Abstraction Layer) might not be needed anymore at all. But for a fully functional KDE-Desktop it is neccessary to run hal:

```
/etc/rc.d/hal start

```

For ease of use you should add it to your daemons list in */etc/rc.conf*:

```
DAEMONS=( .. @hal ..)

```

It is no problem to start HAL in the background to shave some time of boot. If you are using udev to automatically mount your drives with an udev-rule without running hal you should take note of the fact that these mounted drives will **not** be recognized by KDE. So no entry of this device will show up in Dolphin and Device Notifier won't notify you either.

### 圖形的相關問題

#### 2D桌面效能低落（或）2D 出現假影

請確保您的顯示卡有安裝適當的驅動程式，為了使您的桌面至少有 2D 加速。參考這些文章了解更多資訊：[ATI](/index.php/ATI "ATI")、[NVIDIA](/index.php/NVIDIA "NVIDIA")、[Intel](/index.php/Intel "Intel")了解更多資訊，以確保一切都正確無誤。 The open source ATI and Intel drivers and the proprietary Nvidia driver should provide the best 2D acceleration.

If this doesn't solve your problems, maybe your driver doesn't provide a good XRender acceleration which the current QT painter engine relies on by default. You can change the painter engine to software based only by invoking the application with the "-graphicssystem raster" command line. This rendering engine can be set as the default one by recompiling QT with the same as configure option, "-graphicssystem raster".

#### Konsole is slow in applications like vim

This is a problem that is caused by slow glyph rendering. You can solve this by switching to a scalable font like Bitstream Vera Sans Mono.

#### 低落的 3D 桌面效能

KDE 預設啟用桌面特效。較舊的顯示卡對於 3D 桌面加速可能會不夠用。您可以關閉桌面特效

```
系統設定 > 桌面 

```

或者您可以開關桌面特效，藉由 `Alt` + `Shift` + `F12`

**Note:** You may encounter such problems with 3D desktop performance even when using a more powerful graphics card, but using catalyst proprietary driver (fglrx). This driver is known for having issues with 3D acceleration. Visit [the ATi Wiki page](/index.php/ATI "ATI") for more troubleshooting.

##### KDE 4.5 specific graphics' issues

Many users who use the ATI and Intel open-source drivers have encountered several performance regressions with the latest KWin update in KDE 4.5\. Please try one of the following workarounds (in order of merit) if you have such a problem (via System Settings > Desktop Effects > Advanced):

*   Add **export LIBGL_ALWAYS_INDIRECT=1** to */etc/profile*
    *   Optionally (because the above already forces this), *uncheck* **Enable direct rendering** under *OpenGL Options*
    *   Reboot (and we mean reboot - don't try to restart the X server)
*   Use **XRender** as the *Compositing type*
*   Disable Desktop Effects (compositing) altogether

See upstream bug report: [https://bugs.kde.org/show_bug.cgi?id=241402](https://bugs.kde.org/show_bug.cgi?id=241402)

### KDE 下的聲音問題

#### ALSA 相關問題

**Note:** First make sure you have **alsa-lib** and **alsa-utils** installed.

##### "Falling back to default" messages when trying to listen to any sound in KDE

When you encounter such messages:

	The audio playback device *<name-of-the-sound-device>* does not work.

	Falling back to default

Go to

```
System Settings > Multimedia

```

and set the device named "**default**" above all the other devices in each box you see.

##### I cannot play mp3 files when having Gstreamer backend in Qt Phonon

That can be solved by installing gstreamer0.10-plugins

```
 pacman -S gstreamer0.10-plugins

```

You can also change the backend used by Phonon, by installing the phonon-xine

```
 pacman -S phonon-xine

```

if you encounter problems that are not solved after installing gstreamer plugins. Then choose Xine in

```
 System Settings > Multimedia > Backend (tab)

```

(it may have been autoselected after installing phonon-xine)

##### Amarok "waits" before playing any track

If you have encountered this error, the problem is backend specific. In order to solve this problem, change Amarok's backend from **gstreamer** to **xine**.

#### OSS4 相關問題

如果您有安裝 OSS4 並遇到問題，你應該注意到 Kmix 的開發者仍然在整合 OSSv4 支援。這裡有一個仍然是實驗性的[AUR 套件](https://aur.archlinux.org/packages.php?ID=29286)。 Arch uses phonon with the Gstreamer backend that should work for most applications. Alternately you could try [phonon with Xine](/index.php/KDE#I_can.27t_play_mp3_files_when_having_Gstreamer_backend_in_Qt_Phonon "KDE").

### Arch linux 特定的打包問題

Due to some changes on the packages or pacman problems, there could be some problems during upgrading. Please read the sections below, if you have a problem.

### 我想要一個最小化安裝的 KDE。當我安裝套件後並登入 KDE，但沒有面板出現

如果你想要一個最小化安裝的 KDE。登入並聽到登入音效，但沒有其他的事發生。可能是因為沒有安裝 Plasma 的二進位檔。這些都包含在

```
  kdebase-workspace

```

安裝這個套件，並重新啟動 Xorg。

### 我想要在我的系統安裝一個全新的 KDE。我應該怎麼做？

只要重新命名 KDE 的設定目錄就可（以防萬一您之後需要）：

```
mv ~/.kde4 ~/.kde4-backup

```

### Plasma 桌面行為奇怪，但我不知道該怎麼辦

Plasma 問題主要是由於不穩定的 **plasmoids** 或 **plasma 主題**所造成的。首先，找到您最新安裝的 plasmoid 或 plasma 主題，並停用它，甚至將它刪除。 如果你不能發現問題，但你不希望失去所有的 KDE 設定，這樣做：

```
rm -r ~/.kde4/share/config/plasma*

```

這個命令會**刪除你的使用者的所有 plasma 相關設定**，當你將重新登入 KDE，將會回到你的**預設**設定。

## 其他 KDE 專案

### Chakra 專案

**Warning:** Chakra Project may soon **split** from Arch's main system. You should be informed on Chakra Project's news and devs' decisions on [Chakra Project website](http://chakra-project.org/).

#### Split KDE packages

[The Chakra Project](http://chakra-project.org/) is a community-based modular version of KDE 4 and Live CD project, which includes a number of UI enhancements for KDE 4.x. Visit [the Chakra Project Wiki main page](http://chakra-project.org/wiki/index.php/Main_Page) for more information.

#### Chakra 專案 Arch Live CD

The Chakra Project also provides a full featured Live CD, which has the latest stable KDEmod4 packages included. You may visit [the Chakra Project Live CD webpage](http://chakra-project.org/download-iso.html) in order to find more information.

#### Passing from KDEmod to [extra]'s KDE

**Note:** You do have instructions for passing from **[extra]'**s KDE4 to KDEmod4 [here](http://chakra-project.org/download-kdemod.html).

Both flavours of KDE provide the same Desktop Environment, so if you install the one or the other, in the same upstream version, there should not be any problem regarding plasmoids, themes, styles or any KDE related application.

So, if you want, for any reason, to pass from KDEmod to **[extra]'**s KDE, do:

```
 pacman -Rd kdemod

```

OR

```
 pacman -Rd kdemod-uninstall

```

and it should be removed, but with the **-d** argument, the KDE dependent packages **are not** uninstalled, but only the Desktop Environment. But, if you want to **completelly** remove any KDEmod specific application/plasmoid/style etc too, do

```
 pacman -Rcns kdemod

```

and then make sure that everything has been uninstalled:

```
 pacman -Q | grep kde

```

**Note:** If you want to use the same KDE specific settings from the previous KDEmod installation, move or rename ~/**.kdemod4** to ~/**.kde4**

After this, you may have KDEmod uninstalled.

Then, follow [this](/index.php/KDE#Installing_KDE_4.5 "KDE").

### KDE unstable

#### KDEmod testing/unstable

You may visit [this webpage](http://chakra-project.org/repos.html) and see which repos can you add in **pacman.conf** in order to test the KDEmod unstable packages.

#### KDE unstable (快照)

##### 非官方的 kde-unstable

The member **ProgDan** has created a repo where he uploads the testing KDE packages when a new **upstream snapshot** is out. You may visit [this topic](https://bbs.archlinux.org/viewtopic.php?id=76245) for more information.

##### 半官方的 kde-unstable

When KDE is reaching beta or RC milestone, KDE "unstable" packages are uploaded to the [kde-unstable] repo.

You may add it by adding:

```
[kde-unstable]
Include = /etc/pacman.d/mirrorlist

```

in **`/etc/pacman.conf`**

They stay there until KDE is declared stable and passes to [extra].

Make sure [you make bug reports](/index.php/KDE#Distro_and_Upstream_bug_report "KDE") if you find any issues.

Read [this section](/index.php/DeveloperWiki:KDE#Users "DeveloperWiki:KDE") in the wiki as well.

### KDE Legacy

#### Downgrading to KDEmod3 from KDE 4

For those people who decide that KDE 4 is still not yet "ready" for them, there is a website about how to downgrade to a version of KDE 3.5 called **kdemod3**:

*   [KDEmod3](http://chakra-project.org/download-kdemod3.html)

**Warning**: There have been issues reported regarding Libjpeg7, that caused KDEmod3 to behave strangely. In order to solve that, install [libjpeg6](https://aur.archlinux.org/packages/libjpeg6/) [libpng12 from AUR](https://aur.archlinux.org/packages.php?ID=33795). The libs **libjpeg6** and **libpng12** can be safely installed along side the current libraries. You will also want to update [poppler-qt3 from AUR](https://aur.archlinux.org/packages.php?ID=19338). The only conflict you will find is a conflict between poppler and poppler-qt3 during poppler updates. **poppler-qt3** is a dependency for the kdemod3-kdegraphics-kpdf package, but as a work-around you can simply remove poppler-qt3 with the --nodeps flag, complete the Arch update of poppler and then reinstall poppler-qt3\. More info [here](http://chakra-project.org/bbs/viewtopic.php?id=1097)

**Warning:** KDE 3 is no longer maintained and supported by the KDE developers. KDEmod3 is no longer maintained by the Chakra Projects developers. Use it on your own risk, regarding any bugs, performance issues or security risks.

#### Unofficial community repository for KDEmod3

[In this thread](https://bbs.archlinux.org/viewtopic.php?id=97612) you may find info on a rebuild of the unsupported KDEmod3.

## Bugs

### Common bugs

If you think you found something that seems like bug, please see [Common_Issues](/index.php?title=Common_Issues&action=edit&redlink=1 "Common Issues (page does not exist)") and regarding that: KDE 4 config files are usually located at

```
~/.kde4/share/config/

```

and for app-specific configs

```
~/.kde4/share/apps/

```

### 發行版和上游的錯誤回報

It is preferrable that if you find a minor or serious bug, you should visit [the Arch Bug Tracker](https://bugs.archlinux.org) or/and [KDE Bug Tracker](http://bugs.kde.org) in order to report that. Make sure that you be clear on what you want to report.

If you have any issue and you write about in on the Arch forums, first make sure that you have **FULLY** updated your system using a good sync mirror (check [here](https://www.archlinux.de/?page=MirrorStatus)) or try **reflector**.

## 外部鏈接

*   [KDE Homepage](http://www.kde.org)
*   [KDE Bug Tracker](http://bugs.kde.org)
*   [Arch Linux Bug Tracker](https://bugs.archlinux.org)
*   [KDE WebSVN](http://websvn.kde.org)