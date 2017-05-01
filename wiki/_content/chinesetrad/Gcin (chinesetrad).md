Gcin 是由 Edward Liu 所開發的新一代中文輸入程式，支持各種不同的輸入法，可在大部分的類 Unix 系統下運作，是最受歡迎的中文輸入法之一。剛開始是設計為使用大五碼字集輸入繁體中文的輸入法。它使用 GTK 作為 UI。在台灣Linux界是一個非常普及的,專注在繁體中文的輸入法。它的輸入法字碼表格式幾乎與 xcin 一樣，且附帶一個方便的程式協助 xcin 使用者轉換他們的設定。Gcin 有一個圖形介面的設定工具，可調整一些 gcin 的設定，像是最愛的輸入法和鍵盤設定等等。並且可以讓使用者很直覺地加入其他 gcin 本來沒有包括的或者是其他輸入程式，像是 scim，的輸入法表格。

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
    *   [1.1 安裝其他輸入法表格](#.E5.AE.89.E8.A3.9D.E5.85.B6.E4.BB.96.E8.BC.B8.E5.85.A5.E6.B3.95.E8.A1.A8.E6.A0.BC)
*   [2 設定](#.E8.A8.AD.E5.AE.9A)
    *   [2.1 自動啟動](#.E8.87.AA.E5.8B.95.E5.95.9F.E5.8B.95)
*   [3 使用方法](#.E4.BD.BF.E7.94.A8.E6.96.B9.E6.B3.95)
    *   [3.1 對於 GNOME/GTK+ 2 應用程式](#.E5.B0.8D.E6.96.BC_GNOME.2FGTK.2B_2_.E6.87.89.E7.94.A8.E7.A8.8B.E5.BC.8F)
    *   [3.2 對於其他的應用程式](#.E5.B0.8D.E6.96.BC.E5.85.B6.E4.BB.96.E7.9A.84.E6.87.89.E7.94.A8.E7.A8.8B.E5.BC.8F)
        *   [3.2.1 範例](#.E7.AF.84.E4.BE.8B)
        *   [3.2.2 設定流程](#.E8.A8.AD.E5.AE.9A.E6.B5.81.E7.A8.8B)
    *   [3.3 Additional notes for Wine/Crossover Office](#Additional_notes_for_Wine.2FCrossover_Office)
*   [4 OpenOffice.org and GCIN](#OpenOffice.org_and_GCIN)

## 安裝

只要用 pacman 可以簡單地安裝好 gcin。

```
pacman -S gcin

```

### 安裝其他輸入法表格

待續

## 設定

### 自動啟動

設定 `~/.xprofile` 或者 `/etc/xprofile` (詳：[xprofile](/index.php/Xprofile "Xprofile"))或 `~/.xinitrc` (詳：[xinitrc](/index.php/Xinitrc "Xinitrc"))，來讓 gcin 可以自動執行：

```
export LC_CTYPE=zh_TW.UTF-8
export XMODIFIERS=@im=gcin
gcin &

```

## 使用方法

### 對於 GNOME/GTK+ 2 應用程式

gcin 提供 gtk 輸入模組。因此，所有 gtk2 的應用程式都可直接獲得支持，不需要再做多餘的設定。(gcin 不是 XIM，且會自動啟動)

### 對於其他的應用程式

#### 範例

以下是一個簡單的範例，附加在 `~/.xinitrc` 或者 `~/.xprofile` 檔案內皆可，用以啟動正體中文環境的 xfce4 及 gcin，可根據你的需要來修改這個範例。

```
export LANG="zh_TW.UTF-8"
export LC_CTYPE="zh_TW.UTF-8"
export XMODIFIERS=@im=gcin
export GTK_IM_MODULE="gcin"
export QT_IM_MODULE="gcin"
gcin &
exec startxfce4

```

#### 設定流程

1\. 設定環境變數，將 locale 設定為 utf8，例如：

```
export LC_CTYPE=zh_TW.UTF-8

```

**注意:** 必須要設定 LC_CTYPE 變數，即使 LC_CTYPE 和 LANG 是相同的，否則在非 gtk2 而使用 X 輸入法的應用程式中會無法啟動。

2\. 設定 XMODIFIERS： 一般情形下，使用以下的設定即可。

```
export XMODIFIERS=@im=gcin

```

gcin 預設使用 "gcin" 這個名字。如果有需要，可以用 GCIN_XIM 這個變數來修改，這樣就可以開啟多個 gcin 程式。例如：

```
export GCIN_XIM=gcin_zh
export XMODIFIERS=@im=gcin_zh

```

記住，gtk2 應用程式在沒有 gcin 時會自動開啟 gcin 程式。

3\. 啟動 gcin:

```
gcin &

```

4\. 執行你的應用程式。如果 gcin 被中止 (killed) 了，有可能會造成其他應用程式的崩潰。

### Additional notes for Wine/Crossover Office

1\. If you run wine or Crossover Office, it's better to use Windows 2000 emulation instead of Windows 98, and you have to start gcin and wine/cxoffice with at least LC_CTYPE=zh_TW.utf8, otherwise wine will not be able to show Chinese correctly.

2\. In wine+IE6 with Windows 98 emulation, LC_CTYPE is not enough if you want to input Chinese on the web-pages - you have to set either LANG or LC_ALL to zh_TW.utf8, which slows down wine a lot. However, you can always type Chinese in the location bar or other places and paste it.

## OpenOffice.org and GCIN

如果你使用的不是GNOME的桌面系統，那麼有很高的機會你將無法在OpenOffice.org當中切換gcin的輸入模式。 藉由簡單的更改OpenOffice.org的執行指令，在執行命令之前加入**OOO_FORCE_DESKTOP=gnome**就可以排除這個問題。

例如：將**$ oowrite** 更改為**$ OOO_FORCE_DESKTOP=gnome ooffice**

修改選單中程式執行的命令也能夠達成相同的效果。

[Fluxbox](/index.php/Fluxbox "Fluxbox")或類似視窗管理的軟體，可以將**OOO_FORCE_DESKTOP=gnome**加入`.xinitrc`或是`.xprofile`當中。

* * *

[Project Homepage](http://hyperrate.com/dir.php?eid=67)