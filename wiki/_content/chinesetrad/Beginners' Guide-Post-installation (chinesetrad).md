**翻譯狀態：** 本文章是 [Beginners'_Guide/Post-installation](/index.php/Beginners%27_Guide/Post-installation "Beginners' Guide/Post-installation") 的翻譯版本。最近一次的翻譯時間：2014-01-17。點擊[本連結](https://wiki.archlinux.org/index.php?title=Beginners'_Guide/Post-installation&diff=0&oldid=292760)查看英文頁面之後的變更。

**提示:** 本文是新手教學的多頁版本。若您希望閱讀完整的指南，請**[點擊這裡](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide (正體中文)")**。

## Contents

*   [1 安裝完成後](#.E5.AE.89.E8.A3.9D.E5.AE.8C.E6.88.90.E5.BE.8C)
    *   [1.1 使用者管理](#.E4.BD.BF.E7.94.A8.E8.80.85.E7.AE.A1.E7.90.86)
    *   [1.2 軟體包管理](#.E8.BB.9F.E9.AB.94.E5.8C.85.E7.AE.A1.E7.90.86)
    *   [1.3 服務管理](#.E6.9C.8D.E5.8B.99.E7.AE.A1.E7.90.86)
    *   [1.4 音效](#.E9.9F.B3.E6.95.88)
    *   [1.5 圖形使用者介面(GUI)](#.E5.9C.96.E5.BD.A2.E4.BD.BF.E7.94.A8.E8.80.85.E4.BB.8B.E9.9D.A2.28GUI.29)
        *   [1.5.1 安裝 X](#.E5.AE.89.E8.A3.9D_X)
        *   [1.5.2 安裝影像驅動](#.E5.AE.89.E8.A3.9D.E5.BD.B1.E5.83.8F.E9.A9.85.E5.8B.95)
        *   [1.5.3 安裝輸入驅動程式](#.E5.AE.89.E8.A3.9D.E8.BC.B8.E5.85.A5.E9.A9.85.E5.8B.95.E7.A8.8B.E5.BC.8F)
        *   [1.5.4 設定 X](#.E8.A8.AD.E5.AE.9A_X)
        *   [1.5.5 測試 X](#.E6.B8.AC.E8.A9.A6_X)
            *   [1.5.5.1 疑難排解](#.E7.96.91.E9.9B.A3.E6.8E.92.E8.A7.A3)
        *   [1.5.6 字型](#.E5.AD.97.E5.9E.8B)
        *   [1.5.7 選擇/安裝圖形介面](#.E9.81.B8.E6.93.87.2F.E5.AE.89.E8.A3.9D.E5.9C.96.E5.BD.A2.E4.BB.8B.E9.9D.A2)
*   [2 附錄](#.E9.99.84.E9.8C.84)

## 安裝完成後

現在，您全新的 Arch Linux 基本系統已經是可以工作的 GNU/Linux 環境了，剩下就有待您的巧手了。若您剛使用 Linux 不久，參考一下新系統包含的[核心工具](/index.php/Core_Utilities_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Core Utilities (正體中文)")會很有幫助。

### 使用者管理

根據[使用者管理](/index.php/Users_and_Groups_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E8.80.85.E7.AE.A1.E7.90.86 "Users and Groups (正體中文)")的說明新增任何 root 以外您需要的使用者帳號。以 root 帳號作為日常使用、或透過 [SSH](/index.php/SSH "SSH") 連接伺服器都不是好的習慣。您應該只在進行管理任務時才使用 root 帳號。

### 軟體包管理

Pacman 是 Arch Linux 的「軟體包管理員」(**pac**kage **man**ager)。請參閱 [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 和 [FAQ#軟體包管理](/index.php/FAQ_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E8.BB.9F.E9.AB.94.E5.8C.85.E7.AE.A1.E7.90.86 "FAQ (正體中文)")瞭解如何安裝、升級並管理軟體包。 由於 [Arch 的設計哲學#正確的程式碼勝過一時的便利](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E6.AD.A3.E7.A2.BA.E7.9A.84.E7.A8.8B.E5.BC.8F.E7.A2.BC.E5.8B.9D.E9.81.8E.E4.B8.80.E6.99.82.E7.9A.84.E4.BE.BF.E5.88.A9 "The Arch Way (正體中文)")，隨著 Arch Linux 的改變，更新系統**之前**需手動介入的狀況是免不了的。 訂閱 [arch-announce 郵遞清單](https://mailman.archlinux.org/mailman/listinfo/arch-announce/)，或在每次更新前檢查首頁的 [Arch 新聞](https://www.archlinux.org/)。您也可以訂閱[這個 RSS 消息源](https://www.archlinux.org/feeds/news/)，或是追蹤 Twitter 上的 [@archlinux](https://twitter.com/archlinux)，都能對您有所幫助。

若您安裝了 Arch Linux x86_64 版本，且打算使用 32 位元的應用程式，或許會想[啟用 [multilib] 倉庫](/index.php/Multilib "Multilib")。

各個倉庫的用途詳情請參閱[官方倉庫](/index.php/Official_Repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official Repositories (正體中文)")。

### 服務管理

Arch Linux 使用 [systemd](/index.php/Systemd "Systemd") 這套 Linux 下的系統服務管理程式來初始化系統。為了維護您的 Arch Linux，請稍微了解一下它的基本概念與操作。所有和 systemd 的互動都可由 `systemctl` 指令完成。更多資訊請詳閱 [systemd#systemctl 基本用法](/index.php/Systemd#Basic_systemctl_usage "Systemd")。

### 音效

[ALSA](/index.php/ALSA "ALSA") 通常一裝完就可使用，通常只需要取消靜音即可。安裝 [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (已包含 `alsamixer`) 並依照[這裡](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")的指示進行。

ALSA 是核心的組件之一，建議使用。若無法使用，[OSS](/index.php/OSS "OSS") 會是個不錯的替代品。若您有進階的音效需求，請參閱[聲音系統](/index.php/Sound_system "Sound system")。

### 圖形使用者介面(GUI)

#### 安裝 X

[X 視窗系統](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (又稱之為 **X11** 或 **X**) 是套網路與顯示通訊協定，提供了以點陣圖顯示的視窗功能，包含了建立「圖形使用介面」 (GUI) 的標準工具集和協定。

安裝 [Xorg](/index.php/Xorg "Xorg") 基本軟體包：

```
# pacman -S xorg-server xorg-server-utils xorg-xinit

```

安裝 [mesa](https://en.wikipedia.org/wiki/Mesa_(computer_graphics) (提供 3D 支援)：

```
# pacman -S mesa

```

#### 安裝影像驅動

**註記:** 若您是以 VirtualBox 安裝 Arch 為客體，就不需安裝影像驅動。請參閱 [Arch Linux 客體](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox")了解安裝與設定「客體附屬工具」(Guest Additions)，並跳到之後的[設定](#.E8.A8.AD.E5.AE.9A_X)部分。

Linux 核心包含了開源影像驅動，支援硬體加速幀緩衝。不過，X11 下 OpenGL 與 2D 加速皆需要使用者區的支援。

若您不曉得您的機器使用什麼顯示晶片組，請執行：

```
$ lspci | grep VGA

```

完整的開源影像驅動清單可從軟體包資料庫中搜尋：

```
$ pacman -Ss xf86-video | less

```

`vesa` 驅動是一般性的模式設定驅動，幾乎在所有 GPU 上都可以運作，但不提供任何 2D 或 3D 加速功能。若更好的驅動沒有找到或載入失敗，Xorg 會退而求其次使用 vesa。安裝 vesa：

```
# pacman -S xf86-video-vesa

```

為了讓影像加速可以運作，並使用 GPU 可設置的所有模式，您需要一個適當的影像驅動程式。請參閱 [Xorg#驅動安裝](/index.php/Xorg#Driver_installation "Xorg")中常見影像驅動表。

#### 安裝輸入驅動程式

Udev 可以毫無問題地偵測您的硬體。`evdev` 驅動 ([xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev)) 是目前的熱插拔輸入驅動，幾乎適用於所有裝置，所以多數情況下您並不需要安裝輸入驅動。`evdev` 已因為 [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 軟體包的相依性而被安裝好了。

筆記型電腦 (或觸控螢幕) 的使用者會需要 [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) 軟體包，以讓觸控板/觸控螢幕作用：

```
# pacman -S xf86-input-synaptics

```

若需要微調觸控板，或是發生觸控板相關的錯誤，請參閱[觸控板](/index.php/Touchpad_Synaptics "Touchpad Synaptics")文章。

#### 設定 X

**警告:** 專有驅動通常需要在安裝之後重啟系統。詳情請參閱 [NVIDIA](/index.php/NVIDIA "NVIDIA") 或 [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")。

Xorg 具備自動偵測，`xorg.conf` 已經不太需要。若您仍希望手動設定 X 伺服器，請參閱 [Xorg](/index.php/Xorg "Xorg") wiki 頁面。

若您使用的鍵盤並非標準[美式](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg")，可能需要[設定鍵盤布局](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg")。

**註記:** `XkbLayout` 的值可能和 `loadkeys` 指令使用的鍵碼不同。`/usr/share/X11/xkb/rules/base.lst` 下有許多鍵盤配置與其變種的清單 (在開頭為 `! layout` 的行之後)。例如，`gb` 對應到「英文(英國)」，對終端機而言就是 `loadkeys uk`。

#### 測試 X

**提示:** 以下為選用步驟。若您是第一次安裝 Arch Linux，或是將 Arch 安裝在不熟悉的硬體上時，可以做個測試。

**註記:** 如果您的輸入裝置在測試中不起作用，請從 [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/) 群組安裝需要的驅動後再試一遍。完整的可用輸入驅動清單可從呼叫 Pacman 搜尋得到 (按 `Q` 離開)：
```
$ pacman -Ss xf86-input | less

```
若您不需要[熱插拔](https://en.wikipedia.org/wiki/Hot-plugging "wikipedia:Hot-plugging")功能，只需安裝 [xf86-input-keyboard](https://www.archlinux.org/packages/?name=xf86-input-keyboard) 或 [xf86-input-mouse](https://www.archlinux.org/packages/?name=xf86-input-mouse)，否則 (建議) 使用 `evdev` 做為輸入驅動。

安裝預設環境：

```
# pacman -S xorg-twm xorg-xclock xterm

```

若您在安裝 Xorg 前新增了非 root 的使用者帳號，該帳號的家目錄下會出現 `.xinitrc` 模版檔，必須將它刪除或註解掉。若選擇刪除，**X** 將以上述安裝的預設環境啟動。

```
$ rm ~/.xinitrc

```

**註記:** 當登入時，X 必須從同一台 tty 上執行，以保存 logind 階段。此由預設的 `/etc/X11/xinit/xserverrc` 控制。

執行下列指令，啟動 Xorg (測試) 階段：

```
$ startx

```

螢幕將出現幾個可移動的視窗，且您的滑鼠應該可以使用。如果您認為 **X** 執行的可圈可點、沒有問題，可以在 **X** 下的終端機輸入 `exit` 離開 **X** 環境，回到文字模式。

```
$ exit

```

若螢幕變成一片漆黑，可以試著切換到不同的虛擬終端機 (如 `Ctrl+Alt+F2`)，並以 root 身分登入(鍵入「root」、按 `Enter`、打入密碼後再按 `Enter` 即可)。

您可以試著殺掉 **X** 伺服器程序：

```
# pkill X

```

沒有作用的話就直接重啟系統：

```
# reboot

```

##### 疑難排解

若發生任何問題，到 `Xorg.0.log` 檢查錯誤。以 `(EE)` 開頭的行位代表錯誤，以 `(WW)` 開頭則代表警告，或許能提供一些問題發生的提示。

```
$ grep EE /var/log/Xorg.0.log

```

若看過 [Xorg](/index.php/Xorg "Xorg") 文章後仍無法解決問題，需要到 Arch Linux 論壇或 IRC 頻道尋求協助的話，記得安裝 [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste)，讓熱心的網友能透過連結了解您的問題：

```
# pacman -S wgetpaste
$ wgetpaste ~/.xinitrc
$ wgetpaste /etc/X11/xorg.conf
$ wgetpaste /var/log/Xorg.0.log

```

**註記:** 在網路上詢問問題時，請記得提供所有相關資訊 (硬體、驅動資訊等)。

#### 字型

預設系統只內含不可擴展的點陣字型，您可能希望安裝一套 TrueType 字型。如果您打算使用一個全方位功能的[桌面環境](/index.php/Desktop_environment "Desktop environment") (如 [KDE](/index.php/KDE "KDE"))，這個步驟就並非必要。DejaVu 是一套適用於一般用途的高品質字型，有良好的 [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") 支援：

```
# pacman -S ttf-dejavu

```

請參閱[字型設定](/index.php/Font_configuration "Font configuration")了解如何設定字型渲染，並參閱[字型](/index.php/Fonts_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Fonts (正體中文)")文章內的字型建議與安裝指示。

#### 選擇/安裝圖形介面

X 視窗系統提供了建立圖形使用者介面 (GUI) 的基本架構。

**註記:** 如何選擇桌面環境 (DE) 或視窗管理員 (WM)，是非常主觀的問題。根據**您自己**的需求選擇最好的環境。您也可以建置屬於自己的桌面環境：只需要一套視窗管理員加上自行選用的幾套軟體就夠了。

*   [視窗管理員](/index.php/Window_manager "Window manager") (WM) 會和 X 視窗系統一同控制程式視窗的位置與樣貌。

*   [桌面環境](/index.php/Desktop_environment "Desktop environment") (DE) 在 X 之上工作，與 X 一同提供完整功能的動態 GUI。一般的桌面環境會提供視窗管理員、圖示、小插件、視窗、工具列、資料夾、桌布、程式套組以及拖拉等功能。

除了手動用 `startx` (來自 [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit)) 啟動 X 以外，請參閱[顯示管理員](/index.php/Display_Manager_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Display Manager (正體中文)")了解登入管理員的使用方式，或是從[登入時啟動 X](/index.php/Start_X_at_Login_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Start X at Login (正體中文)") 了解從既存的虛擬終端機啟動的方式。

## 附錄

好奇 Arch 下有什麼吸引人的應用程式嗎？請參考[應用程式清單](/index.php/List_of_applications "List of applications")。

安裝好 Arch 以後，也歡迎參考[一般建議](/index.php/General_Recommendations_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "General Recommendations (正體中文)")內的設定教學，例如設定觸控板、字型算繪等等。

**[新手教學](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide (正體中文)")**

* * *

[準備](/index.php/Beginners%27_Guide/Preparation_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide/Preparation (正體中文)") >> [安裝](/index.php/Beginners%27_Guide/Installation_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide/Installation (正體中文)") >> **安裝完成後**