**翻譯狀態：** 本文章是 [Display_Manager](/index.php/Display_Manager "Display Manager") 的翻譯版本。最近一次的翻譯時間：2014-01-22。點擊[本連結](https://wiki.archlinux.org/index.php?title=Display_Manager&diff=0&oldid=293587)查看英文頁面之後的變更。

相關文章

*   [桌面環境 (英)](/index.php/Desktop_environment "Desktop environment")
*   [視窗管理員 (英)](/index.php/Window_manager "Window manager")
*   [登入時啟動 X](/index.php/Start_X_at_Login_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Start X at Login (正體中文)")

[顯示管理員](https://en.wikipedia.org/wiki/X_display_manager_(program_type) "wikipedia:X display manager (program type)")，又稱登入管理員，在開機過程結束後顯示圖形登入介面，取代原本的 shell。目前顯示管理員的種類如同[視窗管理員](/index.php/Window_manager "Window manager")與[桌面環境](/index.php/Desktop_environment "Desktop environment")般多樣化。每套顯示管理員都有一定量的自訂化與佈景可供使用。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 顯示管理員清單](#顯示管理員清單)
    *   [1.1 終端機](#終端機)
    *   [1.2 圖形介面](#圖形介面)
*   [2 載入顯示管理員](#載入顯示管理員)
    *   [2.1 使用 systemd-logind](#使用_systemd-logind)
*   [3 提示與技巧](#提示與技巧)
    *   [3.1 作業階段清單](#作業階段清單)
    *   [3.2 自動啟動](#自動啟動)
*   [4 已知問題](#已知問題)
    *   [4.1 與 systemd 不相容](#與_systemd_不相容)

## 顯示管理員清單

### 終端機

*   **[CDM](/index.php/CDM "CDM") (終端機顯示管理員)** — 麻雀雖小，五臟俱全的登入管理員，以 bash 寫成

	[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)

*   **[Console TDM](/index.php/Console_TDM "Console TDM")** — *xinit* 的擴充，以純 Bash 撰寫。

	[http://code.google.com/p/t-display-manager/](http://code.google.com/p/t-display-manager/) || [console-tdm](https://aur.archlinux.org/packages/console-tdm/)

### 圖形介面

*   **Entrance** — 以 EFL 為基礎的顯示管理員，目前仍在實驗階段。

	[http://enlightenment.org/](http://enlightenment.org/) || [entrance-git](https://aur.archlinux.org/packages/entrance-git/)

*   **[GDM](/index.php/GDM "GDM")** — [GNOME](/index.php/GNOME "GNOME") 顯示管理員。

	[http://projects.gnome.org/gdm/](http://projects.gnome.org/gdm/) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[KDM](/index.php/KDM "KDM")** — [KDE](/index.php/KDE "KDE") 顯示管理員。

	[http://www.kde.org/](http://www.kde.org/) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **[LightDM](/index.php/LightDM "LightDM")** — 跨桌面環境的顯示管理員，能使用以任何工具集所寫的各種前端。

	[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM) || [lightdm](https://www.archlinux.org/packages/?name=lightdm)

*   **[LXDM](/index.php/LXDM "LXDM")** — [LXDE](/index.php/LXDE "LXDE") 顯示管理員。獨立於 LXDE 桌面環境。

	[http://sourceforge.net/projects/lxdm/](http://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **MDM** — MDM 顯示管理員，GDM 2 的分支。

	[https://github.com/linuxmint/mdm](https://github.com/linuxmint/mdm) || [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)

*   **[Qingy](/index.php/Qingy "Qingy")** — 超輕量、設置富彈性、獨立於 X Windows 的圖形登入 (使用 DirectFB)。

	[http://qingy.sourceforge.net/](http://qingy.sourceforge.net/) || [qingy](https://aur.archlinux.org/packages/qingy/)

*   **SDDM** — 以 QML 為基礎的顯示管理員。

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm), [sddm-qt5](https://aur.archlinux.org/packages/sddm-qt5/)

*   **[SLiM](/index.php/SLiM "SLiM")** — 輕量且優雅的圖形化登入方案。

	[http://slim.berlios.de/](http://slim.berlios.de/) || [slim](https://www.archlinux.org/packages/?name=slim)

*   **[XDM](/index.php/XDM "XDM")** — X 顯示管理員，支援 XDMCP，主機選擇器。

	[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## 載入顯示管理員

執行顯示管理員的守護程序 (如 KDM) 啟用圖形登入：

```
# systemctl enable kdm

```

這樣就可以馬上使用了。如果不行，可能是因為 *default.target* (手動設置或之前安裝的遺留物)：

 `$ ls -l /etc/systemd/system/default.target`  `[...] /etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target` 

直接刪除這個軟連結，*systemd* 將會使用它貯存的 *default.target* (也就是 *graphical.target*)。

```
# rm /etc/systemd/system/default.target

```

啟用 KDM 之後，軟連結 *display-manager.service* 就會設定到 `/etc/systemd/system/` 目錄下：

 `$ ls -l /etc/systemd/system/display-manager.service`  `[...] /etc/systemd/system/display-manager.service -> /usr/lib/systemd/system/kdm.service` 

### 使用 systemd-logind

您可以使用 `loginctl` 檢查使用者作業階段的狀態。所有 [polkit](/index.php/Polkit "Polkit") 動作，如暫停系統或掛載外部硬碟，都可以直接進行。

```
$ loginctl show-session $XDG_SESSION_ID

```

## 提示與技巧

### 作業階段清單

許多顯示管理員會從 `/usr/share/xsessions/` 目錄讀取是否有可用的作業階段。該目錄包含了各桌面環境 (DM) 或視窗管理員 (WM) 的正規[桌面項目檔](https://specifications.freedesktop.org/desktop-entry-spec/latest/)。

若要在顯示管理員的作業階段清單內新增或移除項目，直接在 `/usr/share/xsessions/` 目錄下建立或移除 *.desktop* 檔案。以下為一個典型 *.desktop* 檔案範例：

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

### 自動啟動

多數顯示管理員會參考 `/etc/xprofile`, `~/.xprofile` 以及 `/etc/X11/xinit/xinitrc.d/`。詳情請參閱 [xprofile](/index.php/Xprofile "Xprofile")。

## 已知問題

### 與 systemd 不相容

**警告:** 目前受影響的顯示管理員 (DM) 有 Entrance, MDM, SDDM, [SLiM](/index.php/SLiM "SLiM")

某些顯示管理員由於使用了 PAM 作業階段程序，無法百分之百和 systemd 相容。這會在二次登入時產生多種問題，例如：

*   網路管理員 (NetworkManager) 的小圖示無法作用，
*   無法調整 PulseAudio 的音量，
*   以另一位使用者登入 GNOME 失敗。

更多資訊請參閱以下的錯誤追蹤報告：

*   MDM: [[1]](https://github.com/linuxmint/mdm/issues/32)
*   SDDM: [[2]](https://github.com/sddm/sddm/pull/95) (已於 git master 修復)
*   SLiM: [[3]](https://bugs.archlinux.org/task/34329) [[4]](http://developer.berlios.de/bugs/?func=detailbug&bug_id=19102&group_id=2663)