Openbox 為一輕量且具高度彈性之視窗管理員，具有廣泛標準支援。其功能於 [官方網站](http://icculus.org/openbox/) 有完整文件說明。本文將提及如何在 Arch Linux 下執行 Openbox。

## Contents

*   [1 安裝](#安裝)
*   [2 單一視窗管理員](#單一視窗管理員)
*   [3 桌面環境視窗管理員](#桌面環境視窗管理員)
    *   [3.1 GNOME](#GNOME)
        *   [3.1.1 GNOME 2.26](#GNOME_2.26)
        *   [3.1.2 GNOME 2.24](#GNOME_2.24)
        *   [3.1.3 GNOME 2.22 及早期版本](#GNOME_2.22_及早期版本)
    *   [3.2 KDE](#KDE)
    *   [3.3 Xfce4](#Xfce4)
*   [4 偏好設定](#偏好設定)
    *   [4.1 手動設定](#手動設定)
    *   [4.2 ObConf](#ObConf)
    *   [4.3 應用程式組態](#應用程式組態)
*   [5 功能表](#功能表)
    *   [5.1 手動組態](#手動組態)
    *   [5.2 MenuMaker](#MenuMaker)
    *   [5.3 Obmenu](#Obmenu)
        *   [5.3.1 Obm-xdg](#Obm-xdg)
    *   [5.4 Python 寫成的 xdg 選單腳本](#Python_寫成的_xdg_選單腳本)
    *   [5.5 Pipe menus](#Pipe_menus)
*   [6 啟動程式](#啟動程式)
*   [7 佈景主題與外觀](#佈景主題與外觀)
    *   [7.1 Openbox 佈景主題](#Openbox_佈景主題)
    *   [7.2 GTK 佈景主題](#GTK_佈景主題)
        *   [7.2.1 GTK2/GTK+](#GTK2/GTK+)
        *   [7.2.2 GTK1](#GTK1)
        *   [7.2.3 GTK 字型](#GTK_字型)
        *   [7.2.4 GTK 圖示](#GTK_圖示)
    *   [7.3 滑鼠游標](#滑鼠游標)
    *   [7.4 桌面圖示](#桌面圖示)
    *   [7.5 桌面桌布](#桌面桌布)
*   [8 建議程式](#建議程式)
    *   [8.1 登入管理員](#登入管理員)
    *   [8.2 Composite desktop](#Composite_desktop)
    *   [8.3 Panels, trays, and pagers](#Panels,_trays,_and_pagers)
        *   [8.3.1 面板](#面板)
        *   [8.3.2 通知區域](#通知區域)
        *   [8.3.3 Pagers](#Pagers)
    *   [8.4 檔案管理員](#檔案管理員)
    *   [8.5 應用程式啟動器](#應用程式啟動器)
        *   [8.5.1 dmenu](#dmenu)
        *   [8.5.2 Gmrun](#Gmrun)
        *   [8.5.3 Bashrun](#Bashrun)
        *   [8.5.4 Launchy](#Launchy)
        *   [8.5.5 LXPanel](#LXPanel)
        *   [8.5.6 gnome-panel](#gnome-panel)
    *   [8.6 剪貼簿管理員](#剪貼簿管理員)
    *   [8.7 RSS-Reader](#RSS-Reader)
*   [9 提示與技巧](#提示與技巧)
    *   [9.1 複製與貼上](#複製與貼上)
    *   [9.2 透明度](#透明度)
    *   [9.3 Xprop values for applications](#Xprop_values_for_applications)
        *   [9.3.1 Xprop for Firefox](#Xprop_for_Firefox)
    *   [9.4 Linking the menu to a command](#Linking_the_menu_to_a_command)
    *   [9.5 Urxvt in the background](#Urxvt_in_the_background)
*   [10 資源](#資源)

## 安裝

Openbox 可由標準套件庫取得：

```
# pacman -S openbox

```

安裝完成後，pacman 會指引您複製預設的 `menu.xml` 和 `rc.xml` 設定檔至 <tt>~/.config/openbox/</tt>，例如：

**Note:** 請以一般使用者身分執行這些動作。

```
$ mkdir -p ~/.config/openbox/
$ cp /etc/xdg/openbox/rc.xml ~/.config/openbox/rc.xml
$ cp /etc/xdg/openbox/menu.xml ~/.config/openbox/menu.xml

```

`rc.xml` 為 Openbox 核心設定檔，用以管理鍵盤快速鍵、佈景主題、虛擬桌面以及其它功能。

當您按下桌面時，`menu.xml` 控制 Openbox 應用程式功能表顯示行為。The default items are pretty sparse, but it's very easy to modify the menu structure to suit your needs. See the menu section below for more details, or visit the [Openbox website](http://icculus.org/openbox/).

## 單一視窗管理員

若要執行 Openbox，只要在 `~/.xinitrc` 底下加入此行：

```
exec openbox-session

```

若您已經使用其它視窗管理員，例如 Xfce，Openbox 不會在登出 X 後啟動，試試移動 autostart 資料夾：

```
mv ~/.config/autostart ~/.config/autostart-bak

```

## 桌面環境視窗管理員

### GNOME

#### GNOME 2.26

***Follow the next guide for GNOME 2.24\. If it fails try this:***

If after installing openbox and trying to log into the 'Gnome/openbox' session but it always fails then you can do the following as one way to achieve running openbox as your window manager every time you log into the 'Gnome' session from your login manager (xdm, gdm, kdm, entrance, slim, etc.)

1.  Log into your Gnome only session (which would still be using metacity as its window manager) if you aren't already.
2.  Install openbox if you have not done so already
3.  Explore your menus to *System → Preferences → Startup Applications* (possibly named 'Session' for older versions of Gnome)
4.  Open Startup Application, select '+ Add' and enter the text as seen in the box below whilst omitting the text behind the #.
5.  Now hit the 'Add' button for that data entry window and make sure the checkbox beside your new entry is selected.
6.  Thus log out of your gnome session and log back in and you should be running openbox as your window manager.
7.  Enjoy!

```
Name:    Openbox Windox Manager          # Can be changed
Command: openbox --replace               # Text should not be removed from this line, but possibly added to it
Comment: Replaces metacity with openbox  # Can be changed

```

This creates an entry in a startup list which is executed by gnome everytime that particular user's gnome-session is started.

#### GNOME 2.24

首先，建立 `/usr/share/applications/openbox.desktop` 並包含下列內容:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=OpenBox
Exec=openbox
NoDisplay=true
# name of loadable control center module
X-GNOME-WMSettingsModule=openbox
# name we put on the WM spec check window
X-GNOME-WMName=OpenBox

```

接著，在 gconf 將 **/desktop/gnome/session/required_components/windowmanager** 設為 **openbox**：

```
$ gconftool-2 -s -t string /desktop/gnome/session/required_components/windowmanager openbox

```

最後，在 GDM session 功能表選擇 **GNOME** session。

#### GNOME 2.22 及早期版本

1.  If you use GDM, select the "GNOME/Openbox" login option
2.  If you use startx, add `exec openbox-gnome-session` to `~/.xinitrc`
3.  From the shell:

```
$ xinit /usr/bin/openbox-gnome-session

```

### KDE

1.  If you use KDM, select the "KDE/Openbox" login option
2.  If you use startx, add `exec openbox-kde-session` to `~/.xinitrc`
3.  From the shell:

```
$ xinit /usr/bin/openbox-kde-session

```

### Xfce4

Log into a normal Xfce4 session. From your terminal of choice, do:

```
$ killall xfwm4 ; openbox & exit

```

This will kill xfwm4, run Openbox, and close the terminal.

Log out, making sure to check the "Save session for future logins" checkbox. On next login, Xfce4 will use Openbox as its WM. To be able to exit the session using xfce4-session, open your file `~/.config/openbox/menu.xml` (if it isn't there, copy it from `/etc/xdg/openbox/menu.xml`).

找到這個項目：

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

將其改為：

```
 <item label="Exit Openbox">
   <action name="Execute">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

否則，在最上層功能表使用 "Exit" 項目會導致 Openbox 終止自身執行，使您陷入沒有視窗管理員的窘境。

If you have an issue changing between virtual desktops with the mouse wheel skipping over virtual desktops, open your `~/.config/openbox/rc.xml` file and move the mouse binds with actions "DesktopPrevious" and "DesktopNext" from the context "Desktop" to the context "Root" (you may need to define the Root context).

If you want to use the Openbox root-menu instead of Xfce's, you may terminate Xfdesktop by running the following command in a terminal:

```
$ xfdesktop --quit

```

然而，若要讓 Xfdesktop 管理桌布以及桌面圖示，必須使用其它公用程式，例如 ROX, 以達成這些功能。

(When terminating Xfdesktop, the above issue with the virtual desktops is no longer a problem.)

## 偏好設定

現階段來說，您有兩種選項修改 Openbox 偏好設定；您可手動編輯 `rc.xml`，或是使用 ObConf 工具。

### 手動設定

若要手動設定 Openbox ，只要以您喜愛的文字編輯器編輯 `~/.config/openbox/rc.xml` 即可。整份設定檔提供大量註解，[full documentation](http://icculus.org/openbox/index.php/Help:Contents) 可從官方網站取得。

### ObConf

[ObConf](http://icculus.org/openbox/index.php/ObConf:About) 是圖形界面的 Openbox 組態管理工具, 能用來設定最常用的組態包括主題, 虛擬桌面, 視窗屬性和視窗/桌面邊界.

若要安裝 ObConf，執行：

```
# pacman -S obconf

```

**Note:** ObConf 無法用來設定鍵盤快速鍵以及某些進階功能。若要進行這些修改，您必須手動編輯 `rc.xml` (see above)。其它選項有 [ObKey](http://code.google.com/p/obkey/) 應用程式（可於 [AUR](/index.php/AUR "AUR") 取得）。

### 應用程式組態

Openbox features per-application settings, allowing you to define rules for your programs. For example, you can:

*   load your web browser on a certain desktop
*   load your terminal without a window border
*   load your torrent client at a certain position on your screen

These are defined in `~/.config/openbox/rc.xml`. As you might expect, the instructions are well-documented within the file itself. Full details can also be found here: [http://icculus.org/openbox/index.php/Help:Applications](http://icculus.org/openbox/index.php/Help:Applications)

## 功能表

The default Openbox menu includes a variety of applications to get you started, but you'll probably want to customize this at some point. There are a number of ways to do so:

### 手動組態

Similar to the `rc.xml` file, you can edit `~/.config/openbox/menu.xml` with your favourite text editor. Although many of the settings are self-explanatory, [full documentation](http://icculus.org/openbox/index.php/Help:Menus) is available.

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) 是能為多種視窗管理器建立 XML 選單檔的強大工具，其中也包括了 Openbox。 MenuMaker 會搜尋電腦可供執行的程式並為其增加到 XML 選單內。 若使用者需要它也能設定排除 Legacy X，GNOME，KDE，或 Xfce 桌面環境套件內隨附的程式。

MenuMaker 可於社群套件庫(AUR)取得：

```
# pacman -S menumaker

```

一旦安裝完成，您可執行下列指令產生完整功能表：

```
$ mmaker -v OpenBox3

```

MenuMaker 預設不會覆蓋現有 menu.xml。如果要這麼做，加上 -f (force) 參數來執行:

```
$ mmaker -vf OpenBox3

```

如果要檢視完整選項，執行 `mmaker --help` 或者 man mmaker，

完成後它會交給你一份相當完全的選單，然後現在就可以手動編輯 menu.xml, 或者懶惰地在安裝軟體時再重新生成選單就好。

### Obmenu

Obmenu 是一套 openbox 專用的圖形界面選單編輯器。 對於不太喜歡編輯 XML 原始碼的人來說，它大概是最好的選擇。

它在社群(community)套件庫內就能取得

```
# pacman -S obmenu

```

安裝完成後，只要執行 `obmenu` 並且加入或移除應用程式。

#### Obm-xdg

<tt>obm-xdg</tt> 是 Obmenu　內附的命令列(command-line)模式工具。它能產生內容是已安裝　GTK/GNOME　程式的分類式子選單。

欲使用 obm-xdg，在`~/.config/openbox/menu.xml`加入下列內容：

```
<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

```

然後執行　`openbox --reconfigure` 來更新 Openbox 選單。隨即就可在主選單內看到 **xdg** 子選單。

**Note:** 如果沒有安裝 GNOME 桌面環境，那還需要再安裝 **gnome-menus** 程式套件才能讓 obm-xdg 正常運作。

### Python 寫成的 xdg 選單腳本

這支腳本可以在 Fedora　的 Openbox 程式套件內找到。 你只需要把它存到某個地方並新增一行選單項。

這是原文作者分享的: [http://pastebin.com/f2f827625](http://pastebin.com/f2f827625) 這是腳本作者原版(head): [http://cvs.fedoraproject.org/viewvc/devel/openbox/xdg-menu?view=markup](http://cvs.fedoraproject.org/viewvc/devel/openbox/xdg-menu?view=markup)

任選一個下載（也許你比較喜歡 head 版）。你可以把它存在作何目錄，原文作者使用 ~/Documents/build/xdg-menu （稍後據此修改選單項目為你的 路徑／檔名。）

然後用順手的編輯器打開 menu.xml 挑個位置加入下列選單項目（當然也能任意修改選單名稱）：
<menu id="apps-menu" label="xdgmenu" execute="python /home/shiki/Documents/build/xdg-menu"/>

儲存檔案，並執行：`openbox --reconfigure`。

### Pipe menus

Openbox (and other WMs like WindowMaker and PekWM) allow you to write scripts that dynamically build menus on the fly. Some examples are system monitors, media player controls, and weather forecasts. Many examples can be found on the openbox [site](http://icculus.org/openbox/index.php/Openbox:Pipemenus).

Xyne has also created a file browser and brisbin33 has one for scanning for / connecting to wireless hot spots (requires netcfg). The relevant forum posts for these utilities are [here](https://bbs.archlinux.org/viewtopic.php?id=77197&p=1) and [here](https://bbs.archlinux.org/viewtopic.php?id=78290)

## 啟動程式

Openbox features support for running programs at startup. This is provided by the "openbox-session" command.

There are two ways to enable autostart:

1.  If you use startx/xinit to log into your X session, edit `~/.xinitrc` and change the line that executes *openbox* to execute **openbox-session** instead.
2.  If you log in with GDM/KDM, then select the *Openbox* session and it will automatically use autostart.

Startup programs are managed in `~/.config/openbox/autostart`. Full instructions and best practices for how to do this are available at the [Openbox website](http://openbox.org/wiki/Help:Autostart).

## 佈景主題與外觀

With the exception of the Openbox Themes topic, the following section is intended for users who have configured Openbox to run as a standalone desktop, without the assistance of GNOME, KDE or Xfce.

### Openbox 佈景主題

Openbox 佈景主題控制視窗邊界外觀，包含標題列以及標題列按鈕。它們也決定應用程式功能表及螢幕顯示 (OSD) 外觀。

附加佈景主題可從標準套件庫取得：

```
# pacman -S openbox-themes

```

This package is by no means definitive. You can download more themes at websites such as:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

下載的佈景主題應該可解壓縮至 <tt>~/.themes</tt> 並且能夠經由 ObConf 工具安裝或選取。

Creating new themes is fairly easy and again [well-documented](http://icculus.org/openbox/index.php/Help:Themes).

For a GUI theme editor, take a look at [ObTheme](http://xyne.archlinux.ca/info/obtheme).

### GTK 佈景主題

#### GTK2/GTK+

GTK+ themes can be managed easily with the **[lxappearance](/index.php/LXDE "LXDE")**, **gtk-chtheme**, or **switch2** utilities. To install, run:

```
# pacman -S lxappearance

```

and/or

```
# pacman -S gtk-chtheme

```

and/or

```
# pacman -S gtk-theme-switch2

```

Now you can simply run `lxappearance`, `gtk-chtheme` or `switch2` to set the desired theme.

#### GTK1

For legacy GTK1 themes, install the **gtk-theme-switch** package:

```
# pacman -S gtk-theme-switch

```

Then run `switch` to select a desired theme.

#### GTK 字型

To manually change the type and size of your fonts, add the following to `~/.gtkrc.mine`:

```
style "user-font"
{
font_name = "[font-name] [size]"
}
widget_class "*" style "user-font"
gtk-font-name = "[font-name] [size]"

```

where `[font-name] [size]` is the desired font and point size. For example:

```
style "user-font"
{
font_name = "DejaVu Sans 8"
}
widget_class "*" style "user-font"
gtk-font-name = "DejaVu Sans 8"

```

Both `font_name` and `gtk-font-name` fields are required for backwards compatibility.

您也可以使用 **gtk-chtheme** 或 **lxappearance** 設定 GTK 字型。請參照上述段落。

#### GTK 圖示

First, extract the desired icon theme to <tt>/usr/share/icons</tt> (system-wide access) or <tt>~/.icons</tt> (local user access), then:

Add the following to `~/.gtkrc.mine`:

```
gtk-icon-theme-name = "[name-of-icon-theme]"

```

where `[name-of-icon-theme]` is the name of the icon theme directory. For example:

```
gtk-icon-theme-name = "Tango"

```

Ensure `~/.gtkrc-2.0` is configured to parse `~/.gtkrc.mine`:

```
# ~/.gtkrc-2.0
# -- THEME AUTO-WRITTEN DO NOT EDIT
include "/usr/share/themes/Rezlooks-Gilouche/gtk-2.0/gtkrc"
include "/home/username/.gtkrc.mine"
# -- THEME AUTO-WRITTEN DO NOT EDIT

```

You can use **lxappearance** to choose GTK icon themes. Please refer to the above section.

### 滑鼠游標

Extract the desired Xcursor theme to either <tt>/usr/share/icons</tt> (system-wide access) or <tt>~/.icons</tt> (local user access). There are also a limited amount of themes available in the community repository that can be installed using pacman.

Add this to `~/.Xdefaults`:

```
Xcursor.theme:   [name-of-cursor-theme]

```

where `[name-of-cursor-theme]` is the name of the cursor theme directory. For example:

```
Xcursor.theme:	Vanilla-DMZ-AA

```

To change the size:

```
Xcursor.size: [size]

```

### 桌面圖示

Openbox does not provide a means to display icons on the desktop. PcmanFM, [ROX](http://rox.sourceforge.net), [iDesk](http://idesk.sourceforge.net), or even Nautilus (and the gnome-settings-daemon) can provide this function.

ROX and PCmanFM have the additional advantage of being lightweight file managers.

### 桌面桌布

Openbox itself does not include a way to change the wallpaper. This can be done easily with programs like [Feh](/index.php/Feh "Feh") or [Nitrogen](/index.php/Nitrogen "Nitrogen"). Other options include ImageMagick, hsetroot and xsetbg.

## 建議程式

There is [list of Lightweight Software](/index.php/Lightweight_Applications "Lightweight Applications") at Arch's wiki, most of them nicely fits with Openbox.

### 登入管理員

[SLiM](http://slim.berlios.de/) provides a lightweight and elegant graphical login solution for standalone Openbox configurations. Refer to Arch's [SLiM](/index.php/SLiM "SLiM") wiki for detailed instructions.

[Qingy](http://qingy.sourceforge.net/) is ultralight and very configurable graphical login. It support login to both console and X Windows sessions. It uses [DirectFB](http://www.directfb.org), therefore it does not start X Windows unless you choose X Windows session. See article about [Qingy](/index.php/Qingy "Qingy") at Arch's wiki.

### Composite desktop

[Xcompmgr](/index.php/Xcompmgr "Xcompmgr") is a lightweight composite manager capable of rendering drop shadows, fading and simple window transparency within Openbox and other window managers.

(It's worth noting that xcompmgr is no longer developed, and so any issues are unlikely to be fixed)

[Cairo Comp Mgr](https://aur.archlinux.org/packages.php?ID=30042) is an alternative.

### Panels, trays, and pagers

There are quite a lot of utilities available that provide a panel (taskbar), system tray, and pager to Openbox. The most common are:

#### 面板

*   [Avant Window Navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")
*   [Cairo-Dock](/index.php/Cairo-Dock "Cairo-Dock")
*   [PyPanel](/index.php/PyPanel "PyPanel")
*   [bmpanel](http://nsf.110mb.com/bmpanel/)
*   [tint2](/index.php/Tint2 "Tint2")
*   [LXPanel](http://www.gnomefiles.org/app.php/LXPanel)
*   [fbpanel](http://fbpanel.sourceforge.net)
*   [PerlPanel](http://perlpanel.org/)
*   [fspanel](http://www.chatjunkies.org/fspanel/)
*   [xfce4-panel](http://www.xfce.org/projects/xfce4-panel/)
*   [gnome-panel](http://developer.gnome.org/arch/gnome/corecomponents/panel/)
*   [wbar](http://code.google.com/p/wbar/)
*   [screenlets](http://www.screenlets.org/)

#### 通知區域

*   [Stalonetray](http://stalonetray.sourceforge.net/)
*   [Trayer](http://download.gna.org/fvwm-crystal/trayer/1.0/)

#### Pagers

*   [Visibility](http://projects.l3ib.org/trac/visibility)
*   [bbpager](http://bbtools.sourceforge.net/)
*   [netwmpager](https://aur.archlinux.org/packages.php?ID=17563)
*   [IPager](http://useperl.ru/ipager/index.en.html)

Make your choice and add it to your startup file. If you wish to set the desktop layout without using a pager, you can use [obsetlayout](https://aur.archlinux.org/packages/obsetlayout/), which is a packaged version of the setlayout tool from the Openbox wiki.

### 檔案管理員

There are many possibilities, but the most popular lightweight file managers are:

*   [Thunar](/index.php/Thunar "Thunar"). Thunar supports auto-mount features and other plugins.
*   [ROX](http://rox.sourceforge.net) (ROX provides desktop icons)

```
# pacman -S rox

```

*   [PCManFM](http://pcmanfm.sourceforge.net) (pcmanfm also provides desktop icons)

```
# pacman -S pcmanfm

```

For even lighter options, consider [Gentoo](http://www.obsession.se/gentoo/) or [emelFM](http://emelfm.sourceforge.net/), both of which use the familiar 'Midnight Commander' two pane layout (these two require Gtk 1.2.x).

當然，您也可以使用 GNOME 的 Nautilus。雖然比上述解決方案來得慢，但它支援 VFS（例：遠端 SSH、FTP 以及 Samba 連線)，具有額外優勢。

### 應用程式啟動器

#### dmenu

Set-up dmenu as described in the [dmenu](/index.php/Dmenu "Dmenu") wiki article. Then, add the following entry to the <keyboard> section `~/.config/openbox/rc.xml` to enable a shortcut to launch dmenu:

```
   <keybind key="W-space">
     <action name="Execute">
       <execute>dmenu_run</execute>
     </action>
   </keybind>

```

#### Gmrun

[gmrun](http://sourceforge.net/projects/gmrun) provides an excellent Run dialog box, similar to the Alt+F2 features found in Gnome and KDE:

```
# pacman -S gmrun

```

Add the following entry to the <keyboard> section `~/.config/openbox/rc.xml` to enable Alt+F2 functionality:

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

#### Bashrun

[bashrun](http://bashrun.sourceforge.net) provides a different, barebones approach to a run dialog, using a specialized bash session within a small xterm window. It is available in the community repository and can be launched through the Alt+F2 style approach mentioned previously. To make bashrun act more like a traditional run dialog, add the following entry to the <applications> section `~/.config/openbox/rc.xml`:

```
   <application name="bashrun">
     <desktop>all</desktop>
     <decor>no</decor>  # switch to yes if you prefer a bordered window
     <focus>yes</focus>
     <skip_pager>yes</skip_pager>
     <layer>above</layer>
   </application>

```

#### Launchy

[Launchy](http://www.launchy.net/) is a less minimalistic approach; it is skinnable and offers more functionality such as a calculator, checking the weather, etc. Originally for Windows, similar to Gnome Do.

```
# pacman -S launchy

```

It is launched by Ctrl+Space key combination.

#### LXPanel

The LXPanel run dialog can be executed with

```
lxpanelctl run

```

#### gnome-panel

The gnome-panel run dialog can be executed with

```
gnome-panel-control --run-dialog

```

### 剪貼簿管理員

You may wish to install a clipboard manager for feature rich copy/paste ability. **xfce4-clipman-plugin, parcellite,** or **glipper-old** may be installed via pacman. Add your choice to autostart. From the terminal, Ctrl+Insert as copy and Shift+Insert as paste generally works as well. You may also copy from terminal with Ctrl+Shift+C, and paste with mouse middle click.

### RSS-Reader

*   [FasterFeeder RSS Reader for Openbox](http://primo-nordica.net/dezza/fasterfeeder.py)

## 提示與技巧

### 複製與貼上

From the terminal, Ctrl+Insert as copy and Shift+Insert as paste generally works as well. You may also copy from terminal with Ctrl+Shift+C, and paste with mouse middle click.

### 透明度

By using the program transset-df, it is virtually the same as [transset](/index.php?title=Transset&action=edit&redlink=1 "Transset (page does not exist)"), (available by: pacman -S transset-df) you can enable transparancy of windows on the fly. For instance by editing the following in `~/.config/openbox/rc.xml` you can have your middle mouse scroll enable and disable transparency by scrolling down and up on the scroll button, respectively, while over the title bar (it is in the <mouse> section):

```
    <context name="Titlebar">
     <mousebind button="Left" action="Press">
       <action name="Focus"/>
       <action name="Raise"/>
     </mousebind>
     <mousebind button="Left" action="Drag">
       <action name="Move"/>
     </mousebind>
     <mousebind button="Left" action="DoubleClick">
       <action name="ToggleMaximizeFull"/>
     </mousebind>
     <mousebind button="Middle" action="Press">
     	<action name="Lower"/> 
       <action name="FocusToBottom"/>
       <action name="Unfocus"/>
     </mousebind>
     <mousebind button="Up" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --inc  </execute>
       </action>
     </mousebind>
     <mousebind button="Down" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --dec </execute>
       </action>
     </mousebind>
     <mousebind button="Right" action="Press">
       <action name="Focus"/>
       <action name="Raise"/>
       <action name="ShowMenu">
         <menu>client-menu</menu>
       </action>
     </mousebind>
   </context>

```

As of now, it only appears to work when no other actions are taken.

### Xprop values for applications

If you use per-application settings frequently, you might find this bash alias handy:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

To use, run **`xp`** and click on the running program that you'd like to define with per-app settings. The result will display only the info that Openbox requires, namely the WM_WINDOW_ROLE and WM_CLASS (name and class) values:

```
[thayer@dublin:~] $ xp
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

#### Xprop for Firefox

For whatever reason, Firefox and its open source equivalents will ignore application rules (e.g. <desktop>) unless `class="Firefox*"` is used, regardless of what xprop reports as the actual WM_CLASS values.

### Linking the menu to a command

Some people would want to link the Openbox main menu, or any other, to a command. This is useful for creating a menu button in a panel, for example. Although Openbox doesn't support this, a very simple script, xdotool, can simulate a keypress by running a command. Xdotool is [available on AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=14789&O=0&L=0&C=0&K=xdotool&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd). To use it, simply add the following code to the <keyboard> section of your `rc.xml`:

```
    <keybind key="A-C-q">
      <action name="ShowMenu">
        <menu>root-menu</menu>
      </action>
    </keybind>

```

Restart/reconfigure Openbox. You can now magically summon your menu at your cursor position by running the following command:

```
# xdotool key ctrl+alt+q

```

Of course, you can change the shortcut to your liking.

### Urxvt in the background

With Openbox, running a terminal as desktop background is easy. You won't need **devilspie** here.

First you must enable transparency, open your `.Xdefaults` file (if it doesn't exist yet, create it in your home folder).

```
URxvt*transparent:true
URxvt*scrollBar:false
URxvt*geometry:124x24    #I don't use the whole screen, if you want a full screen term don't bother with this and see below.
URxvt*borderLess:true
URxvt*foreground:Black   #Font color. My wallpaper is White, you may wish to change this to White.

```

接著編輯您的 `.config/openbox/rc.xml` 檔案：

```
<application name="urxvt">
  <decor>no</decor>
  <focus>yes</focus>
  <position>
    <x>center</x>
    <y>20</y>
  </position>
  <layer>below</layer>
  <desktop>all</desktop>
  <maximized>true</maximized> #Only if you want a full size terminal.
</application>

```

The *magic* comes from the `<layer>below</layer>` line, which place the application under all others. Here Urxvt is displayed on all desktops, change it to your convenience.

## 資源

*   [Openbox Website](http://openbox.org/) – 官方網站
*   [Planet Openbox](http://planetob.openmonkey.com/) – Openbox 新聞入口
*   [Box-Look.org](http://www.box-look.org/) – A good resource for themes and related artwork