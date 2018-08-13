## Contents

*   [1 關於SCIM](#.E9.97.9C.E6.96.BCSCIM)
*   [2 安裝SCIM](#.E5.AE.89.E8.A3.9DSCIM)
    *   [2.1 安裝輸入法引擎](#.E5.AE.89.E8.A3.9D.E8.BC.B8.E5.85.A5.E6.B3.95.E5.BC.95.E6.93.8E)
*   [3 配置SCIM](#.E9.85.8D.E7.BD.AESCIM)
    *   [3.1 使用kdm/gdm時自動啟動scim](#.E4.BD.BF.E7.94.A8kdm.2Fgdm.E6.99.82.E8.87.AA.E5.8B.95.E5.95.9F.E5.8B.95scim)

# 關於SCIM

Su Zhe (或 James Su)在為TurboLinux工作的時候，於2001年發起了SCIM專案，該專案的目標是：

*   為當前可用的輸入法庫提供一個統一前端；
*   作為IIIMF輸入法框架的語言引擎；
*   盡可能多地提供各國輸入引擎；
*   盡可能多地支援輸入法協定/介面；
*   盡可能多地支援各種作業系統。

SCIM具有以下特性：

*   使用C++編寫，完全面向物件結構；
*   高度模組化
*   體系結構非常靈活，可以作為其他C/S輸入法環境的動態連結程式庫；
*   簡單的編程介面
*   完全支援i18n UCS4/UTF-8編碼
*   具有許多便利的工具可以加速自身開發
*   具有特性豐富的圖形化面板
*   統一的配置框架

# 安裝SCIM

```
pacman -S scim

```

## 安裝輸入法引擎

目前SCIM包含許多各類的輸入法（有些可能需要一些其他的庫），覆蓋30多種語言，包括中文（簡體、繁體）、日文、韓文及許多歐洲語言：

```
(在[這裏](http://www.scim-im.org/projects/imengines)察看所有支援的語言)

```

中文新酷音（智慧型注音）：

```
pacman -S scim-chewing

```

中文智慧拼音：

```
pacman -S scim-pinyin

```

中文五筆及其它：

```
pacman -S scim-tables

```

日文：

```
pacman -S scim-anthy

```

韓文：

```
pacman -S scim-hangul

```

# 配置SCIM

方法一： 為了讓SCIM在桌面中自動啟動並且正常工作，編輯~/.xinitrc，在啟動桌面環境/視窗管理器的語句前面加入以下內容：

```
export LC_CTYPE="zh_CN.utf8" （請改成你在X下使用的locale，如果沒有合適的locale，請查詢locale-gen相關資訊）
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="scim"
export QT_IM_MODULE="scim"
scim -d

```

現在進入X，scim應該已經啟動了，你可以在圖示上點擊右鍵改變SCIM配置（比如去掉一些不用的輸入法）。在任何程式中按Ctrl-Space就可以使用輸入法了。

## 使用kdm/gdm時自動啟動scim

創建一個新檔~/.xprofile，加入以下內容：

```
export LC_CTYPE="zh_CN.utf8" 
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE=scim
export QT_IM_MODULE=xim
scim -d

```

查看[這裏](https://www.archlinux.org/news/166/)獲得更多官方資訊。

方法二： Gnome用戶可以試一下，編輯/etc/gtk-2.0/gtk.immodules，在最后加入以下內容：

```
 "/usr/lib/gtk-2.0/immodules/im-scim.so" 
 "scim" "SCIM Input Method" "scim" "/usr/share/locale" "ja:ko:zh" 

```

如果LC_CTYPE為en_US.UTF-8，需要把"ja:ko:zh"改成"en:ja:ko:zh"。你可以輸入命令gtk-query-immodules-2.0發現區別。然后重啟。SCIM托盤可能不會顯示，不過設置好輸入法后，按CTRL+空格將顯示輸入條。KDE可能有相似方法。警告：加了"en"，PC啟動后，任務欄可能不顯示。按CTRL+ALT+F1進入SHELL，輸入sudo reboot或reboot重啟。或者用vi或vim編輯/etc/gtk-2.0/gtk.immodules。