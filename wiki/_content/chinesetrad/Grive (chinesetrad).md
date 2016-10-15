Grive 是一個開源的 [Google雲端硬碟](https://en.wikipedia.org/wiki/Google_Drive "wikipedia:Google Drive") 客戶端軟體。

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
*   [2 設定](#.E8.A8.AD.E5.AE.9A)
*   [3 使用方式](#.E4.BD.BF.E7.94.A8.E6.96.B9.E5.BC.8F)
*   [4 Grive 的圖形化界面](#Grive_.E7.9A.84.E5.9C.96.E5.BD.A2.E5.8C.96.E7.95.8C.E9.9D.A2)

## 安裝

Grive 可以從[AUR](/index.php/AUR "AUR")上的 [grive](https://aur.archlinux.org/packages/grive/) 軟體包安裝。

## 設定

選擇一個你想要當作同步Google雲端硬碟用的目錄，像是 `~/Grive`。Google雲端硬碟上的檔案會被下載至設定的目錄，當然在目錄裡的檔案也會被上傳至Google雲端硬碟。

在終端機畫面中，切換工作目錄至選定的目錄，並執行命令

```
grive -a

```

然後跟從畫面中指示設定。

## 使用方式

當你想要同步時，請切換到設定的目錄（剛才設定的同步目錄），之後執行命令：

```
grive

```

Grive 並不支援背景運行，每當你要同步時都要重複執行上方的動作

## Grive 的圖形化界面

[AUR](/index.php/AUR "AUR")中的 [grive-tools](https://aur.archlinux.org/packages/grive-tools/) 軟體包可使Grive具有圖形化界面

Grive Tools 透過GTK界面幫助您設定Google 雲端硬碟的同步。 Grive Tools 包括以下功能: Grive Setup （主要設定，可以設定基本功能已完成執行同步）、 Grive Indicator （應用程式在系統托盤內的設定） 。

注意：在KED中使用 Grive Indicator必須安裝[AUR](/index.php/AUR "AUR")中的 [libappindicator-gtk3](https://www.archlinux.org/packages/?name=libappindicator-gtk3)。