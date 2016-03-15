**警告:** 目前 SLiM 尚未和 [Systemd](/index.php/Systemd "Systemd") 完全相容，第二次登入會引發各種問題。詳情參閱[顯示管理員#與 systemd 不相容](/index.php/Display_Manager_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E8.88.87_systemd_.E4.B8.8D.E7.9B.B8.E5.AE.B9 "Display Manager (正體中文)")。

[SLiM](http://slim.berlios.de/) is an acronym for Simple Login Manager. SLiM is simple, lightweight and easily configurable. SLiM is used by some because it does not require the dependencies of [GNOME](/index.php/GNOME "GNOME") or [KDE](/index.php/KDE "KDE") and can help make a lighter system for users that like to use lightweight desktops like [Xfce](/index.php/Xfce "Xfce"), [Openbox](/index.php/Openbox "Openbox"), and [Fluxbox](/index.php/Fluxbox "Fluxbox").

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
*   [2 設定](#.E8.A8.AD.E5.AE.9A)
    *   [2.1 啟用 SLiM](#.E5.95.9F.E7.94.A8_SLiM)
    *   [2.2 單一環境](#.E5.96.AE.E4.B8.80.E7.92.B0.E5.A2.83)
    *   [2.3 多重環境](#.E5.A4.9A.E9.87.8D.E7.92.B0.E5.A2.83)
    *   [2.4 佈景主題](#.E4.BD.88.E6.99.AF.E4.B8.BB.E9.A1.8C)
        *   [2.4.1 雙螢幕設定](#.E9.9B.99.E8.9E.A2.E5.B9.95.E8.A8.AD.E5.AE.9A)
*   [3 其它選項](#.E5.85.B6.E5.AE.83.E9.81.B8.E9.A0.85)
    *   [3.1 變更鼠標](#.E8.AE.8A.E6.9B.B4.E9.BC.A0.E6.A8.99)

## 安裝

安裝 SLiM：

```
# pacman -S slim

```

## 設定

How to load at startup, start your desktop environment, add themes...

### 啟用 SLiM

藉由修改 `rc.conf` daemon 陣列或 `inittab`，可於啟動時載入 SLiMa。詳見 [Display manager](/index.php/Display_manager "Display manager") 取得細節。

### 單一環境

若要設定 SLiM 載入特定環境，編輯 `~/.xinitrc` 以載入您的桌面環境：

```
#!/bin/sh

#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

exec [session-command]

```

將 `[session-command]` 取代為合適的 session 指令。一些不同桌面啟動指令範例：

```
exec openbox-session
exec fluxbox (or exec startfluxbox)
exec startxfce4
exec gnome-session
exec startkde
exec fvwm2
exec awesome

```

若您的環境未在此處列出，參照合適的 wiki 頁面。

### 多重環境

To be able to choose from multiple desktop environments, SLiM can be setup to log you into whichever you choose.

Put a case statement similar to this one in your `~/.xinitrc` file and edit the sessions variable in `/etc/slim.conf` to match the names that trigger the case statement. You can choose the session at login time by pressing F1\. Note that this feature is experimental.

```
# The following variable defines the session which is started if the user doesn't explicitly select a session
# Source: http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample

DEFAULT_SESSION=twm

case $1 in
kde)
	exec startkde
	;;
xfce4)
	exec startxfce4
	;;
icewm)
	icewmbg &
	icewmtray &
	exec icewm
	;;
wmaker)
	exec wmaker
	;;
blackbox)
	exec blackbox
	;;
*)
	exec $DEFAULT_SESSION
	;;
esac

```

### 佈景主題

安裝 [slim-themes](https://www.archlinux.org/packages/?name=slim-themes) 套件：

```
# pacman -S slim-themes archlinux-themes-slim

```

[archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) 套件包含數個不同佈景主題。目錄 `/usr/share/slim/themes` 尋找可用佈景主題。在 `/etc/slim.conf` 找到 'current_theme'，輸入佈景主題名稱：

```
#current_theme       default
current_theme       archlinux-simplyblack

```

To preview a theme run if no instance of the Xorg server is running by:

```
$ slim -p /usr/share/slim/themes/<theme name>

```

若要關閉，於登入處鍵入 "exit" 後按下 Enter。

附加佈景主題套件可於 [AUR](/index.php/AUR "AUR") 找到。

#### 雙螢幕設定

您可在 /usr/share/slim/themes/<your-theme>/slim.theme 自訂 slim 佈景主題，將原有百分比值：

```
input_panel_x           50%
input_panel_y           50%

```

改為像素值：

```
# These settings set the "archlinux-simplyblack" panel in the center of my 1440x900 left screen
input_panel_x           495
input_panel_y           325

```

若您的佈景主題包含背景圖片，您可使用 background_style 設定（'stretch'、'tile'、'center' 或 'color'）使其正確顯示。觀看 [very simple and clear official documentation about slim themes](http://slim.berlios.de/themes_howto.php) 取得更多細節。

## 其它選項

您可能會想試試的一些選項。

### 變更鼠標

若您想將預設 X 鼠標改為較新的設計，有 [slim-cursor](https://aur.archlinux.org/packages/slim-cursor/) 套件可用。

安裝完成後，編輯 `/etc/slim.conf` 取消註解此行：

```
cursor   left_ptr

```

This will give you a normal arrow instead.