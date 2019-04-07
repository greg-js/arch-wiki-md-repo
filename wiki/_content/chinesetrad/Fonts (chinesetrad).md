相關文章

*   [字型設定 (英)](/index.php/Font_configuration "Font configuration")
*   [Java 執行環境字型 (英)](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")
*   [微軟字型 (英)](/index.php/MS_Fonts "MS Fonts")
*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")

**翻譯狀態：** 本文章是 [Fonts](/index.php/Fonts "Fonts") 的翻譯版本。最近一次的翻譯時間：2014-01-25。點擊[本連結](https://wiki.archlinux.org/index.php?title=Fonts&diff=0&oldid=285531)查看英文頁面之後的變更。

摘自[維基百科](https://en.wikipedia.org/wiki/Computer_font "wikipedia:Computer font")：

	「**電腦字型** (computer font)，或稱**字型** (font)，是包含字 (glyph)、字元或符號 (如 dingbats) 的電子檔案資料。」

注意，某些字型的授權有訂定合理使用限制。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 字型格式](#字型格式)
    *   [1.1 常見副檔名](#常見副檔名)
    *   [1.2 其他格式](#其他格式)
*   [2 安裝](#安裝)
    *   [2.1 Pacman](#Pacman)
    *   [2.2 建立軟體包](#建立軟體包)
    *   [2.3 手動安裝](#手動安裝)
    *   [2.4 舊版應用程式](#舊版應用程式)
    *   [2.5 Pango 警告訊息](#Pango_警告訊息)
*   [3 終端機字型](#終端機字型)
    *   [3.1 預覽和測試](#預覽和測試)
    *   [3.2 持續性的設定](#持續性的設定)
*   [4 字型軟體包](#字型軟體包)
    *   [4.1 古文字](#古文字)
    *   [4.2 盲文點字](#盲文點字)
    *   [4.3 表情符號(顏文字)](#表情符號(顏文字))
    *   [4.4 國際 (非英語系) 使用者](#國際_(非英語系)_使用者)
        *   [4.4.1 阿拉伯和烏爾都文字](#阿拉伯和烏爾都文字)
        *   [4.4.2 緬甸文](#緬甸文)
        *   [4.4.3 中日韓越文字](#中日韓越文字)
            *   [4.4.3.1 Pan-CJK](#Pan-CJK)
            *   [4.4.3.2 中文字](#中文字)
            *   [4.4.3.3 日文字](#日文字)
            *   [4.4.3.4 韓文字](#韓文字)
        *   [4.4.4 希臘文字](#希臘文字)
        *   [4.4.5 希伯來文字](#希伯來文字)
        *   [4.4.6 印地文字](#印地文字)
        *   [4.4.7 高棉文字](#高棉文字)
        *   [4.4.8 僧伽羅文字](#僧伽羅文字)
        *   [4.4.9 塔米爾文字](#塔米爾文字)
        *   [4.4.10 藏文字](#藏文字)
    *   [4.5 數學字型](#數學字型)
    *   [4.6 Microsoft 字型](#Microsoft_字型)
    *   [4.7 Apple Mac OS X 字型](#Apple_Mac_OS_X_字型)
    *   [4.8 等寬字型](#等寬字型)
        *   [4.8.1 TrueType 字型](#TrueType_字型)
        *   [4.8.2 點陣字型](#點陣字型)
    *   [4.9 無襯線字型](#無襯線字型)
    *   [4.10 手寫體](#手寫體)
    *   [4.11 襯線字型](#襯線字型)
    *   [4.12 未分類字型](#未分類字型)
*   [5 X11 的字型採用順序](#X11_的字型採用順序)
*   [6 字型別名](#字型別名)
*   [7 小提示](#小提示)
    *   [7.1 從官方軟體庫安裝字型](#從官方軟體庫安裝字型)
    *   [7.2 應用程式專用的字型快取](#應用程式專用的字型快取)
*   [8 另請參閱](#另請參閱)

## 字型格式

現今電腦所使用的字型中，絕大部分屬於**點陣** (bitmap) 或**輪廓** (outline)資料格式。

	點陣字型

	由點 (像素) 陣列構成的圖像，代表每種字樣、大小的字 (glyph)。

	輪廓字型

	又稱作**向量** (vector) 字型。使用貝茲曲線 (Bézier curve)、繪圖指引和數學公式描繪每個字，產生的字元可以縮放至任意大小。

### 常見副檔名

*   `bdf`, `bdf.gz` – 點陣字型，*b*itmap *d*istribution *f*ormat 的縮寫，以及用 gzip 壓縮的 `bdf`
*   `pcf`, `pcf.gz` – 點陣字型，*p*ortable *c*ompiled *f*ont 的縮寫，以及用 gzip 壓縮的 `pcf`
*   `psf`, `psfu`, `psf.gz`, `psfu.gz` – 點陣字型，*P*C *s*creen *f*ont 與 *P*C *s*creen *f*ont *U*nicode 的縮寫，以及用 gzip 壓縮的版本 (跟 X.Org 不相容)
*   `pfa`, `pfb` – 輪廓字型，*P*ostScript *f*ont *A*SCII 與 *P*ostScript *f*ont *b*inary 的縮寫。PostScript 字型內建印表機指令。
*   `ttf` – 輪廓字型，*T*rue*T*ype *f*ont 的縮寫。原本設計為 PostScript 字型的替代品。
*   `otf` – 輪廓字型，*O*pen*T*ype *f*ont 的縮寫。TrueType 附帶 PostScript 排版指令。

TrueType 與 OpenType 的技術差異，在大部分的用途之下可被忽略。某些 OpenType 字型使用了 `ttf` 副檔名。

### 其他格式

排版程式 *TeX* 與字型軟體 *Metafont* 有它們自己算繪字元的方法。這兩個程式使用的字型副檔名有 `*pk`, `*gf`, `mf` 和 `vf`。

*FontForge* 字型編輯程式會將字型存為自己的文字檔格式 `sfd`，這是 *s*pline *f*ont *d*atabase 的縮寫。

[SVG](http://www.w3.org/TR/SVG/fonts.html) 格式也有一套自己的字型描述方法。

## 安裝

安裝字型的方式有很多種。

### Pacman

透過 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 可以安裝啟用軟體庫的字型。使用以下指令搜尋可供使用的字型：

```
$ pacman -Ss font

```

或只搜尋 `ttf` 字型：

```
$ pacman -Ss ttf

```

### 建立軟體包

您應該將管理字型的工作交給 pacman。字型可以打包成一份 Arch 軟體包，還可以透過 [AUR](/index.php/AUR "AUR") 和社群分享。這裡有一個建立基本軟體包的範例。若想要更了解如何組建軟體包，請閱讀 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")。

字型檔案的家族名稱可以使用 `fc-query` 指令取得。例如： `fc-query -f '%{family[0]}
' /path/to/file`。使用的格式請參考 FcPatternFormat(3) 手冊之說明。

 `PKGBUILD` 
```
pkgname=fontname-fonts
pkgver=1.0
pkgrel=1
pkgdesc="一些關於此字型之描述"
arch=('any')
depends=('fontconfig' 'xorg-font-utils')
source=("http://someurl.org/$pkgname.tar.bz2")
install=$pkgname.install

package() {
  install -Dm644 $pkgname/font.otf "$pkgdir"/usr/share/fonts/family_name/font.otf
  install -Dm644 $pkgname/font_bold.otf "$pkgdir"/usr/share/fonts/family_name/font_bold.otf
}

```
 `fontname-fonts.install` 
```
post_install() {
  fc-cache -s
}

post_upgrade() {
  post_install
}

post_remove() {
  post_install
}

```

### 手動安裝

要為系統新增一個軟體庫未收錄的字型，建議方法是[#建立軟體包](#建立軟體包)。採用這個方式讓 pacman 之後能夠移除或升級字型。不過您也可以用手動的方式安裝字型。

若要將字型安裝到系統 (讓所有使用者都能使用)，將字型資料夾移至 `/usr/share/fonts/` 目錄。為了使得這些字型檔案能夠被所有使用者讀取，使用 [chmod](/index.php/Chmod "Chmod") 指令設定正確的權限：檔案至少必須是 `0444`，而目錄則是 `0555`。若要安裝給單一使用者，則將自行檔案安裝於 `~/.local/share/fonts` 目錄。(注意：`~/.fonts/` 的用法已經不被支援了)

要讓 X 伺服器可以直接載入字型 (不使用「字型伺服器」)，需要將新增字型的所在目錄加為 FontPath 項目。這個項目位在[您的 Xorg 設定檔案](/index.php/Xorg#Configuration "Xorg") (例如 `/etc/X11/xorg.conf` 或 `/etc/xorg.conf`) 的 *Files* 區。更多詳細資訊請參閱[#舊版應用程式](#舊版應用程式)。

接著更新 fontconfig 字型快取：

```
$ fc-cache -vf

```

### 舊版應用程式

對於不支援 fontconfig 的舊版應用程式 (例如 GTK+ 1.x 應用程式和 `xfontsel`)，必須在字型目錄下建立索引：

```
$ mkfontscale
$ mkfontdir

```

或者，用一行指令將多個資料夾包含進來：

```
$ for dir in /font/dir1/ /font/dir2/; do xset +fp $dir; done && xset fp rehash

```

又或者，若字型被安裝在不同的子資料夾如 `/usr/share/fonts` ：

```
$ for dir in * ; do if [  -d  "$dir"  ]; then cd "$dir";xset +fp "$PWD" ;mkfontscale; mkfontdir;cd .. ;fi; done && xset fp rehash

```

有時候 X 伺服器會無法成功載入字型資料夾，這時您需要重新掃描所有 `fonts.dir` 檔案：

```
# xset +fp /usr/share/fonts/misc # 告知 X 伺服器新的目錄
# xset fp rehash                # 強制進行新的掃描

```

檢查字型是否被包含進來：

```
$ xlsfonts | grep fontname

```

**Note:** 許多套件在安裝時會自動設定Xorg以使用字型，若是這種情況，則不需要執行本步驟。

這也可以在 `/etc/X11/xorg.conf` 或是 `/etc/X11/xorg.conf.d` 設定檔中全域設置。

以下是一個必須要加到 `/etc/X11/xorg.conf` 檔案中的例子。請依照特定字型的需求自行增減設定中的路徑。

```
# Let X.Org know about the custom font directories
Section "Files"
    FontPath    "/usr/share/fonts/100dpi"
    FontPath    "/usr/share/fonts/75dpi"
    FontPath    "/usr/share/fonts/cantarell"
    FontPath    "/usr/share/fonts/cyrillic"
    FontPath    "/usr/share/fonts/encodings"
    FontPath    "/usr/share/fonts/misc"
    FontPath    "/usr/share/fonts/truetype"
    FontPath    "/usr/share/fonts/TTF"
    FontPath    "/usr/share/fonts/util"
EndSection

```

### Pango 警告訊息

若您的系統有在使用 [Pango](http://www.pango.org/)，它會從 [fontconfig](http://www.freedesktop.org/wiki/Software/fontconfig) 讀取字型來源。

```
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='common'
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='latin'

```

如果您看到與上面類似的錯誤，或者應用程式內的字元變成了方框，您需要新增字型並更新字型快取。這個範例使用 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 字型演示(成功安裝此套件之後)，並以 root 執行以套用至全系統。

```
# fc-cache
/usr/share/fonts: caching, new cache contents: 0 fonts, 3 dirs
/usr/share/fonts/TTF: caching, new cache contents: 16 fonts, 0 dirs
/usr/share/fonts/encodings: caching, new cache contents: 0 fonts, 1 dirs
/usr/share/fonts/encodings/large: caching, new cache contents: 0 fonts, 0 dirs
/usr/share/fonts/util: caching, new cache contents: 0 fonts, 0 dirs
/var/cache/fontconfig: cleaning cache directory   
fc-cache: succeeded

```

您可以測試預設字型是否已經設置：

```
# fc-match
LiberationMono-Regular.ttf: "Liberation Mono" "Regular"

```

## 終端機字型

**Note:** 本節是關於 [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console")。對於提供更多功能的其他的終端機(支援全 Unicode 字型、現代的顯示卡等等)，請參考 [fbterm](/index.php/Fbterm "Fbterm") 、 [KMSCON](/index.php/KMSCON "KMSCON") 或之類的相關專案。

預設的條件下 [虛擬終端機](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") 使用核心內建的字型與 [CP437](https://en.wikipedia.org/wiki/CP437 "wikipedia:CP437") 字元表， 但這是很容易修改的。

[Linux 虛擬終端機](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console") 預設使用 UTF-8 編碼，但由於使用了標準的 VGA 相容偵緩衝，一個虛擬終端機被限制只能使用標準的 256 或 512 個字符。若一個字型超過 256 個字符，則色彩就會從 16 種降級到 8 種。為了指配正確的符號以顯示給訂的 Unicode，便需要一種特殊的轉換表，*unimap*。現在大多數虛擬終端機字型都有內建這個功能，傳統上則需要分開載入。

[kbd](https://www.archlinux.org/packages/?name=kbd) 套件提供了改變虛擬終端機字型及字型對應的工具。可用的字型被存放在 `/usr/share/kbd/consolefonts/` 目錄中，這些副檔名為 *.psfu* or *.psfu.gz* 的檔案具有內建的 Unicode 轉換表。

Keymaps, the connection between the key pressed and the character used by the computer, are found in the subdirectories of `/usr/share/kbd/keymaps/`, see [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") for details.

鍵盤映射 (Keymap) 是按鍵和電腦使用字元的對應關係表，可以在 `/usr/share/kbd/keymaps/` 的子目錄下找到。詳細資訊請參照 [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") 。

**Note:** 替換這些字型可能造成某些問題，因為有些程式預期標準的 VGA 風格字型，如某些畫線的圖形軟體。

### 預覽和測試

**提示：** 一個整理過的預覽影像資料庫：[Linux 終端機字型截圖](http://alexandre.deverteuil.net/pages/consolefonts)。

*showconsolefont* 指令會以表格形式顯示可用字與字元：

```
$ showconsolefont

```

*setfont* 工具可以暫時改變字型，讓使用者認為那是固定的字型。只要指定字型名稱即可 (這些字型位於 `/usr/share/kbd/consolefonts/`)，例如：

```
$ setfont lat2-16 -m 8859-2

```

需注意字型名稱的大小寫呈現，不可混淆。如果對新換的字型不滿意，用以下指令可以還原至預設字型 (就算終端機顯示亂碼，這個指令依然可以執行，將指令「盲打」進去即可)：

```
$ setfont

```

**註記:** *setfont* 只作用於目前正在使用的終端機。其它終端機無論活躍與否都不受影響。

### 持續性的設定

`/etc/vconsole.conf` 的 `FONT` 用來在開機時設定字型，對於所有的虛擬終端機都是固定的，詳情請參見 [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) 的說明。

若要顯示 *Č, ž, đ, š* 或 *Ł, ę, ą, ś* 之類的字元，使用 `lat2-16.psfu.gz` 這個字型：

 `/etc/vconsole.conf` 
```
...
 FONT=lat2-16
 FONT_MAP=8859-2
```

這代表使用 ISO/IEC 8859 字元的第二部分，大小設定為 16。您可以使用其它值更改字型大小 (如 `lat2-08`)。您可以在[維基百科的這張表](https://en.wikipedia.org/wiki/ISO/IEC_8859#The_Parts_of_ISO.2FIEC_8859 "wikipedia:ISO/IEC 8859")查詢 8859 規格定義的區域。

若要為早期的使用者空間套用指定字型，在 `/etc/mkinitcpio.conf` 使用 `keymap` 的設定。更多資訊請參閱 [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio")。

如果開機時字型沒有任何變化，或只變化一下就回復原樣，則有可能是因為圖形驅動啟動時字型被重設，然後終端機被切至幀緩衝 (framebuffer)。提早載入圖形驅動可以避免這個問題。若要在套用 `/etc/vconsole.conf` 之前將幀緩衝準備好，請參閱[核心模式設定#提早啟動 KMS](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting")、[[2]](https://bbs.archlinux.org/viewtopic.php?id=145765) 或其它方式。

## 字型軟體包

以下是收錄於官方軟體庫和 [AUR](/index.php/AUR "AUR") 的字型軟體包列表，種類繁多，可依照需求選用。若字型有廣泛的萬國碼 (Unicode) 支援，會加註 "Unicode" 標記，詳情請參閱字型專案或相關的維基百科頁面。

一位 Github 使用者 Ternstor 用 python 腳本產生含有所有官方及 AUR 套件庫字型的 PNG 圖像的 HTML 文件，請參照 [[3]](https://github.com/ternstor/distrofonts/blob/master/archfonts.py) 。

### 古文字

*   [ttf-ancient-fonts](https://aur.archlinux.org/packages/ttf-ancient-fonts/) - 包含了許多古文明字型的 Unicode 符號集合

### 盲文點字

*   [ttf-ubraille](https://aur.archlinux.org/packages/ttf-ubraille/) - 包含 Unicode **盲文點字**符號的字型

### 表情符號(顏文字)

設計用來表示表情的圖形化符號集合。

*   emojione-color-fontAUR - a complete, independent, open-source emoji set focused on design correctness
*   twemoji-color-fontAUR - Twitter's open-sourced emoji glyphs
*   ttf-symbola - provides many Unicode symbols, including emoji, in outline style
*   noto-fonts-emoji - Google's own emoji font, like on Android or Google Hangouts

部份新增的符號在 Noto 字型中的顯示不佳。

### 國際 (非英語系) 使用者

應用程式與瀏覽器會根據 fontconfig 設定和 Unicode 文字可用的字型來選擇其顯示字型。用指令 `fc-list :lang="雙字母的語言代碼"` 列舉系統安裝了哪些可對應該語言的字型。例如，列舉已經安裝的阿拉伯文字型，以及支援阿拉伯字的字型：

 `$ fc-list -f '%{file}
' :lang=ar` 
```
/usr/share/fonts/TTF/FreeMono.ttf
/usr/share/fonts/TTF/DejaVuSansCondensed.ttf
/usr/share/fonts/truetype/custom/DroidKufi-Bold.ttf
/usr/share/fonts/TTF/DejaVuSansMono.ttf
/usr/share/fonts/TTF/FreeSerif.ttf

```

若要在多國語言的網站 (如維基百科、Arch Linux wiki) 正確描繪字形，請安裝下列軟體包組合之一：

*   Google 的 [Noto](http://www.google.com/get/noto/) 以支援所有語言為目標。[安裝](/index.php/Install "Install") [noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts)、 [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk) 以及 [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji)。
*   另外一個能夠良好涵蓋多語言環境的字型組合是 [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)、[ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) 以及 [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk)。

#### 阿拉伯和烏爾都文字

*   [ttf-amiri](https://aur.archlinux.org/packages/ttf-amiri/) - A classical Arabic typeface in Naskh style poineered by Amiria Press
*   [ttf-qurancomplex-fonts](https://aur.archlinux.org/packages/ttf-qurancomplex-fonts/) - Fonts by King Fahd Glorious Quran Printing Complex in al-Madinah al-Munawwarah
*   [ttf-qurancomplex-fonts](https://aur.archlinux.org/packages/ttf-qurancomplex-fonts/) - 位於麥地那的 King Fahd Glorious Quran Printing Complex 製作的字型
*   [ttf-arabeyes-fonts](https://aur.archlinux.org/packages/ttf-arabeyes-fonts/) - Collection of free Arabic fonts
*   [ttf-sil-lateef](https://aur.archlinux.org/packages/ttf-sil-lateef/) - 來自 SIL 的 Unicode 阿拉伯文字型
*   [ttf-sil-scheherazade](https://aur.archlinux.org/packages/ttf-sil-scheherazade/) - 來自 SIL 的 Unicode 阿拉伯文字型
*   [ttf-urdufonts](https://aur.archlinux.org/packages/ttf-urdufonts/) - Urdu fonts (Jameel Noori Nastaleeq (+kasheeda), Nafees Web Naskh, PDMS Saleem Quran Font) and font configuration to set Jameel Noori Nastaleeq as default font for Urdu

#### 緬甸文

*   [ttf-my-paduk](https://aur.archlinux.org/packages/ttf-my-paduk/) - Padauk font for Myanmar/Birmania
*   [ttf-myanmar-fonts](https://aur.archlinux.org/packages/ttf-myanmar-fonts/) - 121 Fonts from myordbok.com

#### 中日韓越文字

##### Pan-CJK

*   思源字體：Adobe與Google合資開發的，囊括簡體中文、繁體中文、日文、韓文字形和來自 Source Sans 字體家族的拉丁文、希臘文和西里爾文字形的 OpenType 字體。
    *   [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts) - 思源黑體，無襯線字體。
    *   [adobe-source-han-serif-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-otc-fonts) - 思源宋體，襯線字體。

*   [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk) - Google Noto CJK 字體， 提供簡體中文、繁體中文、日文、韓文一致的設計和外觀。它是基於 [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts) 重貼的商標。

*   文泉驛字體
    *   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) - 文泉驛微米黑，無襯線形式字體。
    *   [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite) - 文泉驛微米黑light版（筆畫更細）。

*   [ttf-i.bming](https://aur.archlinux.org/packages/ttf-i.bming/) - 舊字體風格的中日韓存先字體

##### 中文字

*   思源字體
    *   [adobe-source-han-serif-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-cn-fonts) - 思源宋體簡體中文部分
    *   [adobe-source-han-serif-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-tw-fonts) - 思源宋體繁體中文部分
    *   [adobe-source-han-sans-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-cn-fonts) - 思源黑體簡體中文部分
    *   [adobe-source-han-sans-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-tw-fonts) - 思源黑體繁體中文部分

*   noto中文字體
    *   [noto-fonts-sc](https://aur.archlinux.org/packages/noto-fonts-sc/) - Noto 簡體中文字體
    *   [noto-fonts-tc](https://aur.archlinux.org/packages/noto-fonts-tc/) - Noto 繁體中文字體

*   文泉驛字體
    *   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) - 文泉驛正黑體，黑體 (無襯線) 的中文輪廓字體，附帶文泉驛點陣宋體 (也支持部分日韓字符)。
    *   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont) - 文泉驛點陣宋體 (襯線) 中文字體。

*   文鼎字體
*   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai) - **楷書** (帶有筆觸) Unicode 字體 (推荐啟用反鋸齒)
*   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) - **明體** (印刷) Unicode 字體

*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts) - **新宋**字體，之前為 ttf-fireflysung

*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - 中文、越南文 TrueType 字體

*   台灣中華民國教育部標准字體
    *   [ttf-tw](https://aur.archlinux.org/packages/ttf-tw/) - 台灣教育部發行的標准楷書、宋體字體。
    *   [ttf-twcns-fonts](https://aur.archlinux.org/packages/ttf-twcns-fonts/) - 台灣中華民國教育部發行的[NS11643標准的中文交換碼全字庫](http://data.gov.tw/node/5961)，包含明體、正宋體及正楷體。

*   windows中文字體
    *   [ttf-ms-win8-zh_cn](https://aur.archlinux.org/packages/ttf-ms-win8-zh_cn/) - windows8簡體中文字體。
    *   [ttf-ms-win8-zh_tw](https://aur.archlinux.org/packages/ttf-ms-win8-zh_tw/) - windows8繁體中文字體。
    *   [ttf-ms-win10-zh_cn](https://aur.archlinux.org/packages/ttf-ms-win10-zh_cn/) - windows10簡體中文字體。
    *   [ttf-ms-win10-zh_tw](https://aur.archlinux.org/packages/ttf-ms-win10-zh_tw/) - windows10繁體中文字體。

##### 日文字

*   [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont) - 正規的日文哥特體 (無襯線) 與明朝體 (襯線) 字形集；其中一項高品質的開放原始碼字形。openSUSE-ja 的預設字形。
*   [ttf-vlgothic](https://aur.archlinux.org/packages/ttf-vlgothic/) - 日文哥特體字形。Debian/Fedora/Vine Linux 的預設字型
*   [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) - 現代哥特體的日文輪廓字型。包含所有日文平假名/片假名、Basic Latin、Latin-1 Supplement、Latin Extended-A、IPA Extensions。另外還有大部分日文漢字、希臘字母、西里爾字與越南文字，可以 7 磅 (等比例) 或 5 磅 (等寬) 字重顯示。
*   [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/) - 日文字型，可正確顯示 [2ch 的 Shift JIS 藝術創作](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art")。
*   [ttf-sazanami](https://www.archlinux.org/packages/?name=ttf-sazanami) - 自由的日文 TrueType 字型。已經過期無人維護，但在某些環境下可當作備案字型使用。

##### 韓文字

*   [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk) - 韓文 TrueType 字型集合
*   [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/) - 共享體 (Nanum) 系列 TrueType 字型
*   [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) - 共享體 (Nanum) 系列 TrueType 等寬字型

#### 希臘文字

幾乎所有 Unicode 字型都包含希臘字元集 (也包含多調變音符號)。某些額外的字型軟體包未包含完整的 Unicode 集，但擁有高品質的希臘字字形 (當然包含拉丁字)：

*   [otf-gfs](https://aur.archlinux.org/packages/otf-gfs/) - 由 Greek Font Society 選用的 OpenType 字型
*   [ttf-mgopen](https://aur.archlinux.org/packages/ttf-mgopen/) - 來自 Magenta 的專業 TrueType 字型

#### 希伯來文字

*   [culmus](https://aur.archlinux.org/packages/culmus/) - 自由的希伯來文字型集合

#### 印地文字

*   [ttf-freebanglafont](https://aur.archlinux.org/packages/ttf-freebanglafont/) - 孟加拉文字型
*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf) - 印地文 OpenType 字型集合 (包含 ttf-freebanglafont)

	(This one contains a "look of disapproval" that might be more to your liking than the [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont) one mentioned elsewhere in this document)

*   [lohit-fonts](https://aur.archlinux.org/packages/lohit-fonts/) - 來自 Fedora 專案的印地文 TrueType 字型 (包含 Oriya 字型以及更多)

#### 高棉文字

*   [ttf-khmer](https://www.archlinux.org/packages/?name=ttf-khmer) - 涵蓋高棉語 (Khmer) 文字的字型
*   [Hanuman](http://code.google.com/webfonts/family?family=Hanuman&subset=khmer) ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))

#### 僧伽羅文字

*   [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/) - 僧伽羅文 (Sinhala) Unicode 字型

#### 塔米爾文字

*   [ttf-tamil](https://aur.archlinux.org/packages/ttf-tamil/) - 塔米爾文 (Tamil) Unicode 字型

#### 藏文字

*   [ttf-tibetan-machine](https://www.archlinux.org/packages/?name=ttf-tibetan-machine) - 藏文 (Tibetan) Machine TTFont

### 數學字型

*   [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica) - Wolfram 公司的 Mathematica 字型
*   [ttf-mathtype](https://aur.archlinux.org/packages/ttf-mathtype/) - MathType 字型
*   [ttf-computer-modern-fonts](https://aur.archlinux.org/packages/ttf-computer-modern-fonts/)

### Microsoft 字型

參閱[微軟字型](/index.php/MS_Fonts "MS Fonts")。

### Apple Mac OS X 字型

*   [ttf-mac-fonts](https://aur.archlinux.org/packages/ttf-mac-fonts/) - Mac OS X TrueType 字型

### 等寬字型

有一些建議要給各位。每個使用者所偏好的字型不同，因此要找到您心目中的理想字型，就請多加嘗試。 如果您沒有太多時間，可以閱讀 Dan Benjamin 的部落格文章：[*Top 10 Programming Fonts*](http://hivelogic.com/articles/top-10-programming-fonts) (前十名適合寫程式的字型)。

這裡有 Trevor Lowing 整理的一長串字型清單：[http://www.lowing.org/fonts/](http://www.lowing.org/fonts/) 。

#### TrueType 字型

*   [Andalé Mono](https://en.wikipedia.org/wiki/Andal%C3%A9_Mono "wikipedia:Andalé Mono") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Anonymous Pro](http://www.marksimonson.com/fonts/view/anonymous-pro) ([ttf-anonymous-pro](https://www.archlinux.org/packages/?name=ttf-anonymous-pro)，也包含在 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [Bitstream Vera Mono](https://en.wikipedia.org/wiki/Bitstream_Vera "wikipedia:Bitstream Vera") ([ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera))
*   [Consolas](https://en.wikipedia.org/wiki/Consolas "wikipedia:Consolas") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)) - Windows 下的編程用字型
*   [Courier New](https://en.wikipedia.org/wiki/Courier_New "wikipedia:Courier New") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Cousine ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS 的 Courier New 替代 (metric-compatible)
*   [DejaVu Sans Mono](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans Mono](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)，也包含在 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   Envy Code R ([ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/))
*   [FreeMono](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Inconsolata](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata](https://www.archlinux.org/packages/?name=ttf-inconsolata)) - 極佳的編程用字型
*   [Inconsolata-g](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata-g](https://aur.archlinux.org/packages/ttf-inconsolata-g/)) - 加入一些親近編程人員的調整
*   [Liberation Mono](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - 可代替 Courier New (metric-compatible)
*   [Lucida Console](https://en.wikipedia.org/wiki/Lucida_Console "wikipedia:Lucida Console") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Lucida Typewriter](https://en.wikipedia.org/wiki/Lucida_Typewriter "wikipedia:Lucida Typewriter") (包含於 [jre](https://aur.archlinux.org/packages/jre/) 軟體包)
*   [Monaco](https://en.wikipedia.org/wiki/Monaco_(typeface) ([ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco/)) - OSX/Textmate 下知名的編程用字型
*   Monofur ([ttf-monofur](https://aur.archlinux.org/packages/ttf-monofur/))

#### 點陣字型

*   Default 8x16
*   Dina ([dina-font](https://www.archlinux.org/packages/?name=dina-font))
*   [Gohu](http://font.gohu.org/) ([gohufont](https://aur.archlinux.org/packages/gohufont/))
*   Lime ([artwiz-fonts](https://aur.archlinux.org/packages/artwiz-fonts/))
*   [ProFont](https://en.wikipedia.org/wiki/ProFont "wikipedia:ProFont") ([profont](https://www.archlinux.org/packages/?name=profont))
*   [Proggy Programming Fonts](https://en.wikipedia.org/wiki/Proggy_Programming_Fonts "wikipedia:Proggy Programming Fonts") ([proggyfonts](https://aur.archlinux.org/packages/proggyfonts/))
*   Tamsyn ([tamsyn-font](https://www.archlinux.org/packages/?name=tamsyn-font))
*   [Terminus](https://en.wikipedia.org/wiki/Terminus_(typeface) ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font))
*   Unifont (glyphs like (look of disapproval)) ([bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont))

### 無襯線字型

*   [Andika](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=andika) ([ttf-andika](https://aur.archlinux.org/packages/ttf-andika/)，包含於 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/))
*   [Arial](https://en.wikipedia.org/wiki/Arial "wikipedia:Arial") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Arial Black](https://en.wikipedia.org/wiki/Arial_Black "wikipedia:Arial Black") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Arimo ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS 的 Arial 替代 (metric-compatible)
*   [Calibri](https://en.wikipedia.org/wiki/Calibri "wikipedia:Calibri") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Candara](https://en.wikipedia.org/wiki/Candara "wikipedia:Candara") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [DejaVu Sans](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)，包含於 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSans](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Sans](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - 可替代 Arial (metric-compatible)
*   [Linux Biolinum](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine))
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [PT Sans](https://en.wikipedia.org/wiki/PT_Sans "wikipedia:PT Sans") ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - 3 種主要變體：正常、變窄與標題 - Unicode：拉丁字、西里爾字
*   [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) ([ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/))
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Ubuntu Font Family](https://en.wikipedia.org/wiki/Ubuntu_Font_Family "wikipedia:Ubuntu Font Family") ([ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family))
*   [Verdana](https://en.wikipedia.org/wiki/Verdana "wikipedia:Verdana") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### 手寫體

*   [Comic Sans](https://en.wikipedia.org/wiki/Comic_Sans "wikipedia:Comic Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### 襯線字型

*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Charis](https://en.wikipedia.org/wiki/Charis_SIL "wikipedia:Charis SIL") (包含於 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode：拉丁字、西里爾字
*   [DejaVu Serif](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Doulos](https://en.wikipedia.org/wiki/Doulos_SIL "wikipedia:Doulos SIL") (包含於 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode：拉丁字、西里爾字
*   [Droid Serif](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)，包含於 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSerif](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Gentium](https://en.wikipedia.org/wiki/Gentium "wikipedia:Gentium") ([ttf-gentium](https://www.archlinux.org/packages/?name=ttf-gentium)，包含於 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode：拉丁字、希臘字、西里爾字、音標字母
*   [Georgia](https://en.wikipedia.org/wiki/Georgia_(typeface) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Serif](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Times New Roman 替代 (metric-compatible)
*   [Linux Libertine](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) - Unicode：拉丁字、希臘字、西里爾字、希伯來字
*   [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman "wikipedia:Times New Roman") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Tinos ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS 的 Times New Roman 替代 (metric-compatible)

### 未分類字型

*   [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/) — a huge collection of free fonts (including ubuntu, inconsolata, droid, etc.) - Note: Your font dialog might get very long as >100 fonts will be added.
*   [ttf-mph-2b-damase](https://aur.archlinux.org/packages/ttf-mph-2b-damase/) — Covers full plane 1 and several scripts
*   [ttf-symbola](https://aur.archlinux.org/packages/ttf-symbola/) — Provides emoji and many many other symbols
*   [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/) — Gentium, Charis, Doulos, Andika and Abyssinica from SIL
*   [font-bh-ttf](https://www.archlinux.org/packages/?name=font-bh-ttf) — X.Org Luxi fonts
*   [ttf-cheapskate](https://aur.archlinux.org/packages/ttf-cheapskate/) — Font collection from *dustismo.com*
*   [ttf-junicode](https://www.archlinux.org/packages/?name=ttf-junicode) — Junius font containing almost complete medieval latin script glyphs
*   [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) — IBM Courier and Adobe Utopia sets of [PostScript fonts](https://en.wikipedia.org/wiki/PostScript_fonts "wikipedia:PostScript fonts")

## X11 的字型採用順序

Fontconfig 會自動選擇符合目前需求的字型。這麼說好了，假設有一個包含英文和中文的視窗，如果預設字型不支援中文，就會換成有中文字支援的字型來顯示。

Fontconfig 透過 `$XDG_CONFIG_HOME/fontconfig/fonts.conf`，讓每個使用者都可以設定自己的偏好順序。 如果您希望在自己偏好的襯線字體後面加上一種中文字型當候補，檔案會看起來像這樣：

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
<alias>
   <family>serif</family>
   <prefer>
     <family>您偏好的拉丁字襯線字型名稱</family>
     <family>您的中文字型名稱</family>
   </prefer>
 </alias>
</fontconfig>

```

您也可以新增無襯線和等寬字型的部分。更多資訊可參考 fontconfig 手冊。

## 字型別名

Linux 下有數個字型別名，實際上它們指向別的真實字型，這是為了讓所有應用程式使用的字型能夠相似。最常見的別名有：`serif` 襯線字型 (如 DejaVu Serif)；`sans-serif` 無襯線字型 (如 DejaVu Sans)；以及 `monospace` 等寬字型 (如 DejaVu Sans Mono)。不過這些別名所代表的字型可能會有變化，且通常它們不會顯示在 KDE 和其他桌面環境的字型管理工具之中。

若要查詢別名所代表的字型，執行：

```
$ fc-match monospace
DejaVuSansMono.ttf: "DejaVu Sans Mono" "Book"

```

在上面的範例中，`DejaVuSansMono.ttf` 是 monospace 別名所指向的字型。

## 小提示

### 從官方軟體庫安裝字型

您可以將**官方軟體倉庫**有提供的字型全部抓下來安裝。

	所有字型

```
# pacman -S $(pacman -Ssq font)

```

	所有 *TrueType* 字型

```
# pacman -S $(pacman -Ssq ttf)

```

### 應用程式專用的字型快取

Matplotlib ([python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib) 或 [python2-matplotlib](https://www.archlinux.org/packages/?name=python2-matplotlib)) 使用自己的字型快取，因此更新字型後記得移除 `$HOME/.matplotlib/fontList.cache`，這樣它才會再產生一次快取並找到新字型 [[4]](http://matplotlib.1069221.n5.nabble.com/getting-matplotlib-to-recognize-a-new-font-td40500.html)。

## 另請參閱

*   [字型設定 (英)](/index.php/Font_configuration "Font configuration")