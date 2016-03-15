## Contents

*   [1 安裝及執行](#.E5.AE.89.E8.A3.9D.E5.8F.8A.E5.9F.B7.E8.A1.8C)
    *   [1.1 安裝](#.E5.AE.89.E8.A3.9D)
    *   [1.2 執行](#.E5.9F.B7.E8.A1.8C)
        *   [1.2.1 透過 startx](#.E9.80.8F.E9.81.8E_startx)
        *   [1.2.2 透過 KDM/GDM](#.E9.80.8F.E9.81.8E_KDM.2FGDM)
*   [2 設定](#.E8.A8.AD.E5.AE.9A)
    *   [2.1 選單管理](#.E9.81.B8.E5.96.AE.E7.AE.A1.E7.90.86)
        *   [2.1.1 透過 fluxbox-generate_menu](#.E9.80.8F.E9.81.8E_fluxbox-generate_menu)
        *   [2.1.2 手動修改](#.E6.89.8B.E5.8B.95.E4.BF.AE.E6.94.B9)
    *   [2.2 快捷鍵](#.E5.BF.AB.E6.8D.B7.E9.8D.B5)
    *   [2.3 工作桌面](#.E5.B7.A5.E4.BD.9C.E6.A1.8C.E9.9D.A2)
    *   [2.4 設定背景圖片](#.E8.A8.AD.E5.AE.9A.E8.83.8C.E6.99.AF.E5.9C.96.E7.89.87)
    *   [2.5 佈景主題](#.E4.BD.88.E6.99.AF.E4.B8.BB.E9.A1.8C)
    *   [2.6 自動執行特定軟體](#.E8.87.AA.E5.8B.95.E5.9F.B7.E8.A1.8C.E7.89.B9.E5.AE.9A.E8.BB.9F.E9.AB.94)
    *   [2.7 沒有 xorg.conf 之後](#.E6.B2.92.E6.9C.89_xorg.conf_.E4.B9.8B.E5.BE.8C)
        *   [2.7.1 正確設定鍵盤排列](#.E6.AD.A3.E7.A2.BA.E8.A8.AD.E5.AE.9A.E9.8D.B5.E7.9B.A4.E6.8E.92.E5.88.97)
        *   [2.7.2 停用省電模式](#.E5.81.9C.E7.94.A8.E7.9C.81.E9.9B.BB.E6.A8.A1.E5.BC.8F)
*   [3 視窗標題亂碼](#.E8.A6.96.E7.AA.97.E6.A8.99.E9.A1.8C.E4.BA.82.E7.A2.BC)
*   [4 額外資源](#.E9.A1.8D.E5.A4.96.E8.B3.87.E6.BA.90)

# 安裝及執行

## 安裝

在 extra 套件庫中可以找到fluxbox。

```
# pacman -S fluxbox

```

## 執行

### 透過 startx

編輯 `~/.xinitrc` 加入

```
exec startfluxbox 

```

或者

```
exec fluxbox

```

建議使用 <tt>startfluxbox</tt> ，因為這將會同時執行所有定義在 `~/.fluxbox/startup` 當中的程式。

**Note:** 在 `~/.xinitrc` 當中只能有一行 <tt>exec</tt> 。

如果無法順利啟動，透過設定 LC_ALL 為預設的 "C" ，也許能夠避免這個情形。 [1](https://bbs.archlinux.org/viewtopic.php?t=25797).

### 透過 KDM/GDM

安裝 fluxbox之後，[KDM](/index.php/KDM "KDM") 或 [GDM](/index.php/GDM "GDM") 將會在 session 選單當中自動增加 fluxbox 的選項。在登入時選取 fluxbox就行了。

# 設定

## 選單管理

### 透過 fluxbox-generate_menu

使用 fluxbox 的指令：

```
$ fluxbox-generate_menu

```

這個指令將會根據所安裝的軟體來產生 `~/.fluxbox/menu/`。在 Fluxbox　選單中的 Fluxbox menu / Tools / Regen Menu 也是執行相同的動作。

### 手動修改

編輯`~/.fluxbox/menu`：

```
$ nano ~/.fluxbox/menu

```

根據以下的格式編寫：

```
[exec] (name) {command}

```

如果你想新增子選單：

```
[submenu] (Name)
...
...
[end]

```

編輯完成之後儲存即可，修改選單並不需要重新啟動 fluxbox 。

## 快捷鍵

透過編輯 `~/.fluxbox/keys` 能夠改變以及增加快捷鍵的組合。

*   Control： Control
*   Mod1： Alt
*   Mod4： Meta (大多數是 windows 鍵)

使用 CTRL，ALT以及上下箭頭調整音量的範例：

```
Control Mod1 Up :Exec amixer sset Master,0 5%+  
Control Mod1 Down :Exec amixer sset Master,0 5%-

```

## 工作桌面

Fluxbox 預設提供四個工作桌面，可以透過底部左方的箭頭或是使用鍵盤組合 Ctrl+F1-F4來更換桌面。透過Fluxbox選單中的 Fluxbox Menu/ Workspace List 可以對工作桌面做設定。

## 設定背景圖片

設定背景圖片需要透過額外的軟體來進行設定，使用下列指令來檢查是否已經有安裝這類型的軟體：

```
$ fbsetbg -i

```

如果回應的訊息不是 *hsetroot is a nice wallpapersetter. You won't have any problems.*或類似的話，你需要安裝背景圖片的管理程式來設定背景圖片。你可以使用下列幾個軟體其中一個或是使用其他習慣的軟體。

*   hsetroot
*   eterm
*   feh (lacks menu transparency).

有了必須的軟體之後，就能夠使用fbsetbg來設定背景圖片了

```
$ fbsetbg /path/to/background.image
$ fbsetbg -f /path/to/background.image #全螢幕
$ fbsetbg -c /path/to/background.image #置中
$ fbsetbg -t /path/to/background.image #磁磚填滿
$ fbsetbg -r /path/to/ #從目錄中隨機選取

```

更換佈景主題時，背景圖片會消失，使用下列指令能夠快速將背景圖片設定回復。

```
$ fbsetbg -l

```

## 佈景主題

將所下載的壓縮檔解壓縮到下列的兩個預設路徑之一，就完成安裝：

*   全域 - /usr/share/fluxbox/styles
*   特定使用者 - ~/.fluxbox/styles

## 自動執行特定軟體

startx 的使用者應該將想執行的程式碼放入 `~/.xinitrc` 當中。然而 fluxbox 額外提供了自身的啟動方式。

在 fluxbox 啟動的時候會自動執行 `~/.fluxbox/startup` 。需要依照軟體執行的類型來決定是否增加 & 符號。

範例檔案 ( # 代表註解 )：

```
fbsetbg -l # 設定背景圖片
idesk & # 使用 & 符號使得執行不會馬上結束
xterm & # 使用 & 符號使得執行不會馬上結束
# exec /usr/bin/fluxbox -log ~/.fluxbox/log #fluxbox紀錄檔

```

## 沒有 xorg.conf 之後

因為在多數的情形下，新版的 Xorg 不再需要 xorg.conf。以前在 xorg.conf 當中所做關於鍵盤以及省電模式的設定可以透過下列方式進行調整。

### 正確設定鍵盤排列

在 `~/.fluxbox/startup` 當中加入以下指令藉以啟動特殊字元 (例如：éóíáú) 支援：

```
setxkbmap us -variant intl &

```

詳細語法，請閱讀 man setxkbmap。

修改 `~/.fluxbox/menu`，在選單中加入鍵盤變更的選項：

```
[submenu] (Keyboard)
      [exec] (normal) {setxkbmap us}
      [exec] (international) {setxkbmap us -variant intl}
[end]

```

### 停用省電模式

直接將下列指令加入 `~/.fluxbox/startup` 當中：

```
xset s off -dpms &

```

# 視窗標題亂碼

修改佈景主題中的 `theme.cfg`：

```
menu.title.font:                         AR PL NewSung-9:bold #字型-大小:特效
toolbar.workspace.font:                  AR PL NewSung-10:bold
toolbar.iconbar.focused.font:            AR PL NewSung-8:bold
toolbar.iconbar.unfocused.font:          AR PL NewSung-8
window.font:                             AR PL NewSung-8

```

# 額外資源

*   [Fluxbox Homepage](http://fluxbox.sourceforge.net/)
*   [Gentoo Wiki about Fluxbox](http://wiki.gentoo.org/wiki/Fluxbox)
*   [Themes for Fluxbox](http://box-look.org/)
*   [Fluxbox Wiki](http://fluxbox-wiki.org/)
*   [fbsetbg documentation](http://www.xs4all.nl/~hanb/software/fbsetbg/fbsetbg.html)
*   [Application recommendations](http://archux.com/page/application-recommendations)
*   [Fluxbox Style Guide](/index.php/Fluxbox_Style_Guide "Fluxbox Style Guide")