## Contents

*   [1 安裝 xorg](#.E5.AE.89.E8.A3.9D_xorg)
    *   [1.1 不使用 xorg.conf](#.E4.B8.8D.E4.BD.BF.E7.94.A8_xorg.conf)
        *   [1.1.1 不使用xorg.conf設定非美式鍵盤排列](#.E4.B8.8D.E4.BD.BF.E7.94.A8xorg.conf.E8.A8.AD.E5.AE.9A.E9.9D.9E.E7.BE.8E.E5.BC.8F.E9.8D.B5.E7.9B.A4.E6.8E.92.E5.88.97)
*   [2 設定 xorg](#.E8.A8.AD.E5.AE.9A_xorg)
    *   [2.1 xorgconfig](#xorgconfig)
    *   [2.2 hwd](#hwd)
    *   [2.3 Post-editing](#Post-editing)
*   [3 執行 Xorg](#.E5.9F.B7.E8.A1.8C_Xorg)
*   [4 啟動 X (/usr/X11R6/bin/startx) 時的微調](#.E5.95.9F.E5.8B.95_X_.28.2Fusr.2FX11R6.2Fbin.2Fstartx.29_.E6.99.82.E7.9A.84.E5.BE.AE.E8.AA.BF)

## 安裝 xorg

1.  請先確定你已經設定好 pacman 並更新完畢套件清單. [Pacman](/index.php/Pacman "Pacman")

2.  如果你正在使用其他的 x-server，也請先把他結束關閉。 `Ctrl+Alt+Backspace`

3.  如果你的系統使用其他非 xorg 內建支援的影像卡驅動程式，例如 NVidia 或是 ATI 驅動程式，請參閱 (註一)

安裝 xorg 其實非常簡單:

```
# pacman -S xorg

```

如果 xorg 安裝成功，接下來就是產生一個 `xorg.conf` 設定檔，告訴 xorg 你的系統所使用的硬體配備為何。 (註二)

* * *

(註一) 如果你的系統使用了非 xorg 內建的其他顯示卡驅動程式，這些驅動程式可能會和 xorg 在安裝時起衝突。我們建議你先把這些驅動程式移除，然後再安裝 xorg。當 xorg 成功安裝完畢後，你可以再把這些驅動程式安裝進來。如果你沒辦法在安裝 xorg 前先把這些驅動程式移除，你可以在安裝 xorg 時，試看看使用 pacman 的強制安裝參數 `-S --force`.

(註二) 你也可以使用另一個設定用的程式 `xorgcfg`。這個程式也可支援純文字模式下的顯示，請在執行時加入參數 `-textmode` .

* * *

### 不使用 xorg.conf

較新版本的 Xorg 在大多數的情形下能夠有效的藉由[HAL](/index.php/HAL "HAL")的幫助來偵測硬體。因此`xorg.conf`也成為非必需的選項了。也許在開始的階段先忽略`xorg.conf`的設定，而在有特殊需求的時候再來編輯`xorg.conf`會是一個比較好的作法。

如果還沒有安裝hal，請先安裝hal：

```
# pacman -S hal

```

啟動hal：

```
# /etc/rc.d/hal start

```

將hal加入`/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`的 DAEMONS= 之中：

啟動 X：

```
$ startx

```

或

```
$ xinit

```

如果 **X** 順利啟動了，您可以參考`Xorg.0.log`來建立您的xorg.conf檔案。

如果 無法順利偵測類似nvidia的顯示卡，那麼參考下列的設定建立一個最基本的`xorg.conf`：

```
Section "ServerLayout"
   Identifier     "Layout0"
   Screen      0  "Screen0" 0 0
EndSection

Section "Files"
   FontPath "/usr/share/fonts/local/"
EndSection

Section "Device"
   Identifier     "Device0"
   Driver         "nvidia"
   VendorName     "NVIDIA Corporation"
   BoardName      "GeForce Go 7300"
EndSection

Section "Screen"
   Identifier     "Screen0"
   Device         "Device0"
EndSection

```

#### 不使用xorg.conf設定非美式鍵盤排列

```
# cp /usr/share/hal/fdi/policy/10osvendor/10-keymap.fdi /etc/hal/fdi/policy/

```

開啟 `/etc/hal/fdi/policy/10-keymap.fdi` 並且在`input.xkb.layout`編輯"us"成為你想要的排列方式，如果有需要的話，同時編輯`input.xkb.variant`。

在 X 當中執行

```
$ setxkbmap pl 

```

(請將pl換成你所之前所編輯的鍵盤排列方式)，鍵盤排列應該變更了。 你可以透過例如將這行指令加入`~/.xinitrc`當中(啟動視窗管理員之前)的方式，使得每次進入 X 鍵盤排列都不需手動輸入指令。

## 設定 xorg

在開始使用 xorg 前，你必須先告訴它你的系統所使用的螢幕，顯示卡，滑鼠和鍵盤等硬體配備為何。要達到這個目的，你可以使用 `xorgconfig` 或是 `hwd` 這兩種方法中的一種。

### xorgconfig

開始執行 xorgconfig:

```
# xorgconfig

```

這個指令將可幫你產生一個 xorg 的設定檔 : `xorg.conf`。

逐一回答設定程式提出的問題後，設定程式將會自動為你產生一個設定檔。請特別注意關於滑鼠設定的相關問題。xorgconfig 內預設的裝置是在 `/dev/mouse`。所以，你必須把這一項改為 `/dev/input/mice`。否則的話，你可能會在啟動 X 時出現 X 整個當住了的問題。

這個設定程式並不是很完美，但是至少他能夠提供你一個很基本的設定檔。在這之後，如果你覺得有需要對你的設定進行修改，你可以直接手動來編輯和設定。

### hwd

hwd 是個由 Arch Linux 社群的成員所寫的程式。這個程式的主要功能是偵測你的系統內所有的硬體規格，但是他的功能不止於此，你也可以使用他來幫你設定 你的 X 伺服器。很幸運的是，與 `xorgconf` 比起來， hwd 是個很簡單並直接的工具，你使用 hwd 來設定硬體規格時時，你並不需要回答一堆問題。

要使用 hwd 前，請先用 pacman 來安裝程式:

```
# pacman -S hwd

```

現在，以 root 的權限，執行這個程式，並使用 _-x_ 這個參數要求他自動產生一個適用於你的系統的 `xorg.conf` 檔案:

```
# hwd -x

```

使用 '-x' 這個參數所產生的檔案並不會把原本系統內 xorg 的設定檔覆蓋過去。新產生的檔案將會被命名為 `/etc/X11/xorg.conf.hwd` (此外，你也可以在執行 hwd 時直接使用 _-xa_ 這個參數。這樣一來，hwd 所產生的設定檔將會直接把原本的 xorg.conf給覆蓋過去)。要使用新產生的設定檔，你必須手動更改他的名稱：

```
mv xorg.conf.hwd xorg.conf

```

請注意，如果你的系統內已經有一個 xorg.conf 的檔案，你可能需要先把這個檔案備份為其他名稱，再執行檔案搬移的指令。

### Post-editing

Ok，現在我們已經有一個可用的 `xorg.conf` 設定檔，但是你可能想要對他手動自行修改一番。那就讓我們拿出你最喜愛的文字編輯程式 (例如 vim)，開始對他動手對腳吧 (要修改 xorg.conf，你需要使用到 root 的權限)！

```
# vim /etc/X11/xorg.conf

```

如果你的滑鼠上有個滾輪，同時你希望能正常使用這個功能，請參閱 [如何設定滑鼠上的滾輪](/index.php/%E5%A6%82%E4%BD%95%E8%A8%AD%E5%AE%9A%E6%BB%91%E9%BC%A0%E4%B8%8A%E7%9A%84%E6%BB%BE%E8%BC%AA "如何設定滑鼠上的滾輪") 這一篇教學指南。

有些人可能需要手動設定他們的螢幕顯示的大小。請在 `"Monitor"` 這一區段下，就在 `VertRefresh` 這個指示元後，以 mm 為單位，正確設定你要使用的顯示大小:

```
VertRefresh 50-70
DisplaySize 305 230

```

如果你希望使用第三廠商提供的顯示卡驅動程式，請至少先確定你的系統在使用 xorg 內建的驅動程式時可以正常運作沒問題。除非你需要用到一些特殊的功能，例如一些遊戲會用到的 3D 硬體加速功能，雙螢幕顯示，或是電視輸出的功能等等，一般來說，xorg 應該可以在不需要任何其他驅動程式下正常並流暢的執行。

如果你需要安裝 NVidia 的驅動程式，請參閱 [NVIDIA](/index.php/NVIDIA "NVIDIA") 這一篇教學指南。

關於字型的設定，請參閱 [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration") 這一篇教學指南。

## 執行 Xorg

要執行 Xorg，你只需要簡單的鍵入

```
$ startx

```

基本預設的 X 環境其實非常簡略 (bare)，在一般的情況下，你可能會想要安裝一些視窗管理程式 (window managers) 或是桌面環境 (desktop environments) 來補強 X 的功能。

如果在啟動 X 時發生問題，請檢查在 `/var/log/Xorg.0.log` 下的 log 檔。注意檢查 log 中以 _(EE)_ (代表錯誤) 開始的訊息，還有以 _(WW)_ (代表警告) 開始的訊息，這些訊息可能在你找出問題所在時有點幫助。

## 啟動 X (/usr/X11R6/bin/startx) 時的微調

更多關於 X 的啟動參數，請參閱

```
$ man Xserver

```

下面這些選項都必須加在 defaultserverargs 這個變數之後.

禁止 X 聽取 TCP 的訊息:

```
-nolisten tcp

```

當 X 啟動時，以一個全黑的畫面取代原本灰灰的背景圖:

```
-br

```

啟動關於 16 bit 的字型的 deferred glyph 的載入:

```
-deferglyphs 16

```

請編輯下面這個 script 檔案來改變這些參數的設定值 /usr/X11R6/bin/startx