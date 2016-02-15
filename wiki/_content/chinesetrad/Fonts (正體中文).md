**翻譯狀態：** 本文章是 [Fonts](/index.php/Fonts "Fonts") 的翻譯版本。最近一次的翻譯時間：2014-01-25。點擊[本連結](https://wiki.archlinux.org/index.php?title=Fonts&diff=0&oldid=285531)查看英文頁面之後的變更。

摘自[維基百科](https://en.wikipedia.org/wiki/Computer_font "wikipedia:Computer font")：

	「**電腦字型** (computer font)，或稱**字型** (font)，是包含字 (glyph)、字元或符號 (如 dingbats) 的電子檔案資料。」

注意，某些字型的授權有訂定合理使用限制。

## Contents

*   [1 字型格式](#.E5.AD.97.E5.9E.8B.E6.A0.BC.E5.BC.8F)
    *   [1.1 常見副檔名](#.E5.B8.B8.E8.A6.8B.E5.89.AF.E6.AA.94.E5.90.8D)
    *   [1.2 其他格式](#.E5.85.B6.E4.BB.96.E6.A0.BC.E5.BC.8F)
*   [2 安裝](#.E5.AE.89.E8.A3.9D)
    *   [2.1 Pacman](#Pacman)
    *   [2.2 建立軟體包](#.E5.BB.BA.E7.AB.8B.E8.BB.9F.E9.AB.94.E5.8C.85)
    *   [2.3 手動安裝](#.E6.89.8B.E5.8B.95.E5.AE.89.E8.A3.9D)
    *   [2.4 手動安裝：進階方式](#.E6.89.8B.E5.8B.95.E5.AE.89.E8.A3.9D.EF.BC.9A.E9.80.B2.E9.9A.8E.E6.96.B9.E5.BC.8F)
    *   [2.5 舊版應用程式](#.E8.88.8A.E7.89.88.E6.87.89.E7.94.A8.E7.A8.8B.E5.BC.8F)
    *   [2.6 Pango 警告訊息](#Pango_.E8.AD.A6.E5.91.8A.E8.A8.8A.E6.81.AF)
    *   [2.7 讓字型搭配 X.Org](#.E8.AE.93.E5.AD.97.E5.9E.8B.E6.90.AD.E9.85.8D_X.Org)
*   [3 終端機字型](#.E7.B5.82.E7.AB.AF.E6.A9.9F.E5.AD.97.E5.9E.8B)
    *   [3.1 預覽和測試](#.E9.A0.90.E8.A6.BD.E5.92.8C.E6.B8.AC.E8.A9.A6)
    *   [3.2 更改預設字型](#.E6.9B.B4.E6.94.B9.E9.A0.90.E8.A8.AD.E5.AD.97.E5.9E.8B)
*   [4 字型軟體包](#.E5.AD.97.E5.9E.8B.E8.BB.9F.E9.AB.94.E5.8C.85)
    *   [4.1 盲文點字](#.E7.9B.B2.E6.96.87.E9.BB.9E.E5.AD.97)
    *   [4.2 國際 (非英語系) 使用者](#.E5.9C.8B.E9.9A.9B_.28.E9.9D.9E.E8.8B.B1.E8.AA.9E.E7.B3.BB.29_.E4.BD.BF.E7.94.A8.E8.80.85)
        *   [4.2.1 阿拉伯和烏爾都文字](#.E9.98.BF.E6.8B.89.E4.BC.AF.E5.92.8C.E7.83.8F.E7.88.BE.E9.83.BD.E6.96.87.E5.AD.97)
        *   [4.2.2 緬甸文字](#.E7.B7.AC.E7.94.B8.E6.96.87.E5.AD.97)
        *   [4.2.3 中日韓越文字](#.E4.B8.AD.E6.97.A5.E9.9F.93.E8.B6.8A.E6.96.87.E5.AD.97)
            *   [4.2.3.1 中文字](#.E4.B8.AD.E6.96.87.E5.AD.97)
            *   [4.2.3.2 日文字](#.E6.97.A5.E6.96.87.E5.AD.97)
            *   [4.2.3.3 韓文字](#.E9.9F.93.E6.96.87.E5.AD.97)
        *   [4.2.4 西里爾文字](#.E8.A5.BF.E9.87.8C.E7.88.BE.E6.96.87.E5.AD.97)
        *   [4.2.5 希臘文字](#.E5.B8.8C.E8.87.98.E6.96.87.E5.AD.97)
        *   [4.2.6 希伯來文字](#.E5.B8.8C.E4.BC.AF.E4.BE.86.E6.96.87.E5.AD.97)
        *   [4.2.7 印地文字](#.E5.8D.B0.E5.9C.B0.E6.96.87.E5.AD.97)
        *   [4.2.8 高棉文字](#.E9.AB.98.E6.A3.89.E6.96.87.E5.AD.97)
        *   [4.2.9 僧伽羅文字](#.E5.83.A7.E4.BC.BD.E7.BE.85.E6.96.87.E5.AD.97)
        *   [4.2.10 塔米爾文字](#.E5.A1.94.E7.B1.B3.E7.88.BE.E6.96.87.E5.AD.97)
        *   [4.2.11 藏文字](#.E8.97.8F.E6.96.87.E5.AD.97)
    *   [4.3 數學字型](#.E6.95.B8.E5.AD.B8.E5.AD.97.E5.9E.8B)
    *   [4.4 Microsoft 字型](#Microsoft_.E5.AD.97.E5.9E.8B)
    *   [4.5 Apple Mac OS X 字型](#Apple_Mac_OS_X_.E5.AD.97.E5.9E.8B)
    *   [4.6 等寬字型](#.E7.AD.89.E5.AF.AC.E5.AD.97.E5.9E.8B)
        *   [4.6.1 TrueType 字型](#TrueType_.E5.AD.97.E5.9E.8B)
        *   [4.6.2 點陣字型](#.E9.BB.9E.E9.99.A3.E5.AD.97.E5.9E.8B)
    *   [4.7 無襯線字型](#.E7.84.A1.E8.A5.AF.E7.B7.9A.E5.AD.97.E5.9E.8B)
    *   [4.8 手寫體](#.E6.89.8B.E5.AF.AB.E9.AB.94)
    *   [4.9 襯線字型](#.E8.A5.AF.E7.B7.9A.E5.AD.97.E5.9E.8B)
    *   [4.10 未分類字型](#.E6.9C.AA.E5.88.86.E9.A1.9E.E5.AD.97.E5.9E.8B)
*   [5 X11 的字型採用順序](#X11_.E7.9A.84.E5.AD.97.E5.9E.8B.E6.8E.A1.E7.94.A8.E9.A0.86.E5.BA.8F)
*   [6 字型別名](#.E5.AD.97.E5.9E.8B.E5.88.A5.E5.90.8D)
*   [7 小提示](#.E5.B0.8F.E6.8F.90.E7.A4.BA)
    *   [7.1 從官方軟體庫安裝字型](#.E5.BE.9E.E5.AE.98.E6.96.B9.E8.BB.9F.E9.AB.94.E5.BA.AB.E5.AE.89.E8.A3.9D.E5.AD.97.E5.9E.8B)
    *   [7.2 應用程式專用的字型快取](#.E6.87.89.E7.94.A8.E7.A8.8B.E5.BC.8F.E5.B0.88.E7.94.A8.E7.9A.84.E5.AD.97.E5.9E.8B.E5.BF.AB.E5.8F.96)
*   [8 另請參閱](#.E5.8F.A6.E8.AB.8B.E5.8F.83.E9.96.B1)

## 字型格式

現今電腦所使用的字型中，絕大部分屬於**點陣** (bitmap) 或**輪廓** (outline)資料格式。

	點陣字型

	由點 (像素) 陣列構成的圖像，代表每種字樣、大小的字 (glyph)。

	輪廓字型

	又稱作**向量** (vector) 字型。使用貝茲曲線 (Bézier curve)、繪圖指引和數學公式描繪每個字，產生的字元可以縮放至任意大小。

### 常見副檔名

*   `bdf`, `bdf.gz` – 點陣字型，_b_itmap _d_istribution _f_ormat 的縮寫，以及用 gzip 壓縮的 `bdf`
*   `pcf`, `pcf.gz` – 點陣字型，_p_ortable _c_ompiled _f_ont 的縮寫，以及用 gzip 壓縮的 `pcf`
*   `psf`, `psfu`, `psf.gz`, `psfu.gz` – 點陣字型，_P_C _s_creen _f_ont 與 _P_C _s_creen _f_ont _U_nicode 的縮寫，以及用 gzip 壓縮的版本 (跟 X.Org 不相容)
*   `pfa`, `pfb` – 輪廓字型，_P_ostScript _f_ont _A_SCII 與 _P_ostScript _f_ont _b_inary 的縮寫。PostScript 字型內建印表機指令。
*   `ttf` – 輪廓字型，_T_rue_T_ype _f_ont 的縮寫。原本設計為 PostScript 字型的替代品。
*   `otf` – 輪廓字型，_O_pen_T_ype _f_ont 的縮寫。TrueType 附帶 PostScript 排版指令。

TrueType 與 OpenType 的技術差異，在大部分的用途之下可被忽略。某些 OpenType 字型使用了 `ttf` 副檔名。

### 其他格式

排版程式 _TeX_ 與字型軟體 _Metafont_ 有它們自己算繪字元的方法。這兩個程式使用的字型副檔名有 `*pk`, `*gf`, `mf` 和 `vf`。

_FontForge_ 字型編輯程式會將字型存為自己的文字檔格式 `sfd`，這是 _s_pline _f_ont _d_atabase 的縮寫。

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

某些字型，像是 [terminus-font](https://www.archlinux.org/packages/?name=terminus-font)，會安裝在 `/usr/share/fonts/local`，這個目錄預設沒有被加進字型路徑。將以下內容加入 `~/.xinitrc`，就可以在 X11 使用這類字型：

```
xset +fp /usr/share/fonts/local
xset fp rehash

```

如果執行第一行指令後出現以下錯誤

```
$ xset +fp /usr/share/fonts/local/
xset:  bad font path element (#0), possible causes are:
    Directory does not exist or has wrong permissions
    Directory missing fonts.dir
    Incorrect font server address or syntax

```

需要執行

```
# cd /usr/share/fonts/local;mkfontdir

```

### 建立軟體包

您應該將管理字型的工作交給 pacman。字型可以打包成一份 Arch 軟體包，還可以透過 [AUR](/index.php/AUR "AUR") 和社群分享。這裡有一個建立基本軟體包的範例。若想要更了解如何組建軟體包，請閱讀 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")。

```
pkgname=ttf-fontname
pkgver=1.0
pkgrel=1
pkgdesc="custom fonts"
arch=('any')
depends=('fontconfig' 'xorg-font-utils')
source=("http://someurl.org/$pkgname.tar.bz2")
install=$pkgname.install

package() {
  install -d "$pkgdir/usr/share/fonts/TTF"
  cp -dpr --no-preserve=ownership "$srcdir/$pkgname/"*.ttf "$pkgdir/usr/share/fonts/TTF/"
}

```

這份 PKGBUILD 假定字型為 TrueType 類型。之後還必須建立一份安裝檔案 (`ttf-fontname.install`) 更新字型快取：

```
post_install() {
  echo -n "Updating font cache... "
  fc-cache -fs >/dev/null
  mkfontscale /usr/share/fonts/TTF /usr/share/fonts/Type1
  mkfontdir /usr/share/fonts/TTF /usr/share/fonts/Type1
  echo "done"
}

post_upgrade() {
  post_install
}

post_remove() {
  post_install
}

```

若需要更方便的 ttf 字型建立方式，可以使用 [AUR](/index.php/AUR "AUR") 提供的 [makefontpkg](https://aur.archlinux.org/packages/makefontpkg/)。

### 手動安裝

要為系統新增一個軟體庫未收錄的字型，建議方法是[#建立軟體包](#.E5.BB.BA.E7.AB.8B.E8.BB.9F.E9.AB.94.E5.8C.85)。採用這個方式讓 pacman 之後能夠移除或升級字型。不過您也可以用手動的方式安裝字型。

若要將字型安裝到系統 (讓所有使用者都能使用)，將字型資料夾移至 `/usr/share/fonts/` 目錄。如果只要為單一使用者安裝字型，則改移至 `~/.fonts/` 目錄。

要讓 X 伺服器可以直接載入字型 (不使用「字型伺服器」)，需要將新增字型的所在目錄加為 FontPath 項目。這個項目位在[您的 Xorg 設定檔案](/index.php/Xorg#Configuration "Xorg") (例如 `/etc/X11/xorg.conf` 或 `/etc/xorg.conf`) 的 _Files_ 區。更多詳細資訊請參閱[#讓字型搭配 X.Org](#.E8.AE.93.E5.AD.97.E5.9E.8B.E6.90.AD.E9.85.8D_X.Org)。

接著更新 fontconfig 字型快取：

```
$ fc-cache -vf

```

### 手動安裝：進階方式

如果您有特殊的字型收集需求：使用商業字型、使用不同格式的字型、安裝/移除字型檔相當頻繁，或只是希望可以更能夠控制存取自己的字型資源，那就相當適合用手動的方式來安裝維護字型。採用這種方案會獲得很多好處：

*   避免重複安裝不同版本、格式的同一種字型家族 (一個常見原因是算繪問題)。
*   字型可使用多個非標準的實體來源 (例如額外的硬碟、分割區)。
*   避免依賴隱晦又佔體積的本地字型來源 (例如 TeX Live & `09-texlive-fonts.conf`，或是從 AUR 抓下來的某個字型集合)；您可能只需要其中 5 種字型，卻連帶安裝其它 55 種不需要的字型。
*   避免字型算繪問題，因為您的 fontconfig 設定檔已被調成和與安裝在系統的那份不同的格式。
*   只要觀察主字型目錄下的內容，就能夠確定系統上有哪種格式的字型家族可供應用程式使用。您不需要複雜、佔用大量資源的字型管理程式；[gtk2fontsel](https://www.archlinux.org/packages/?name=gtk2fontsel) 和基本的指令工具 (如 [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) 軟體包下的 `fc-query`) 就可以將這件差事辦得又快又好。
*   當您安裝或升級單一字型，所有應用程式都可以使用該版本，包含 LaTeX 相關軟體。
*   有必要的話，可以快速啟用 / 停用某個字型家族，因為您知道它們在哪個目錄下 (除錯時很好用)。
*   不需擔心有任何多餘的 `/etc/fonts/conf.avail/nn-foo.conf` fontconfig 檔案會潛在跟您的算繪設定起衝突 (特別是當您使用[自訂的字型設定與修補過的函式庫](/index.php/Font_configuration#Patched_packages "Font configuration"))。
*   長遠來看，可以省下那些因軟體包管理者的失誤，解決問題和清除衝突所浪費的寶貴時間。

實作上有幾種方式，有必要的話可由任何軟體包管理員採用。以下所舉出的實作方式相當有效率，即使字型數目眾多也相當安全。

*   我們要將字型來源位置 (例如 `/usr/share/fonts.avail`：這是我們要存放字型的位置) 和包含字型家族軟連結的目錄 (`/usr/share/fonts`) 給分隔開來。

*   將每個字型家族分別放在一個明確命名的子目錄下。命名規則必須一致且明確，例如這樣：

```
<ttf|otf|t1>-<字型作者或組織(選用)>-<字型家族名稱>

```

字型來源目錄的內容會長得像這樣：

```
$ ls /usr/share/fonts.avail

/usr/share/fonts.avail/otf-heuristica
/usr/share/fonts.avail/ttf-liberation
/usr/share/fonts.avail/ttf-ms-arial
...

```

*   我們不會動到 TeX Live 的字型目錄，以避免 LaTeX 軟體發生任何問題。既然我們可以使用多個位置，我們將在 `/usr/share/fonts` 建立軟連結，讓應用程式可以存取特定的字型家族：

```
# cd /usr/share/fonts
# ln -s ../fonts.avail/otf-heuristica .
# ln -s /opt/texlive/texmf-dist/fonts/truetype/public/opensans ttf-texlive-open.sans

```

結果如下：

```
$ ls /usr/share/fonts

ttf-liberation        -> ..fonts.avail/ttf-liberation
ttf-ms-arial          -> ..fonts.avail/ttf-ms-arial
otf-heuristica        -> ..fonts.avail/otf-heuristica
otf-texlive-tex.gyre  -> /opt/texlive/texmf-dist/fonts/opentype/public/tex-gyre
ttf-texlive-open.sans -> /opt/texlive/texmf-dist/fonts/truetype/public/opensans
...

```

最後，依照慣例執行：

```
# fc-cache && mkfontscale && mkfontdir

```

[TeX Live](/index.php/TeX_Live "TeX Live") Wiki 文章內也有一個類似做法，比較簡單，但較適用於單一使用者的情境，而非全域設定。

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

有時候 X 伺服器會無法成功載入字型資料夾，這時您需要重新掃描所有 `fonts.dir` 檔案：

```
# xset +fp /usr/share/fonts/misc # 告知 X 伺服器新的目錄
# xset fp rehash                # 強制進行新的掃描

```

檢查字型是否被包含進來：

```
$ xlsfonts | grep fontname

```

### Pango 警告訊息

若您的系統有在使用 [Pango](http://www.pango.org/)，它會從 [fontconfig](http://www.freedesktop.org/wiki/Software/fontconfig) 讀取字型來源。

```
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='common'
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='latin'

```

如果您看到與上面類似的錯誤，或者應用程式內的字元變成了方框，您需要新增字型並更新字型快取。這個範例使用 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 字型演示，並以 root 執行以套用至全系統。

```
# pacman -S ttf-liberation
  -- 略過部分輸出，假設安裝已經成功 -- 

# fc-cache -vfs
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

### 讓字型搭配 X.Org

為了讓 [Xorg](/index.php/Xorg "Xorg") 可以找到並使用您新安裝的字型，必須將字型路徑加入 `/etc/X11/xorg.conf` (另一個 X.Org 設定檔也可以)。

這是必須加入 `/etc/X11/xorg.conf` 的範例內容。根據您的字型需求新增/移除路徑。

```
# 讓 X.Org 知道自訂字型目錄
Section "Files"
    FontPath    "/usr/share/fonts/100dpi"
    FontPath    "/usr/share/fonts/75dpi"
    FontPath    "/usr/share/fonts/cantarell"
    FontPath    "/usr/share/fonts/cyrillic"
    FontPath    "/usr/share/fonts/encodings"
    FontPath    "/usr/share/fonts/local"
    FontPath    "/usr/share/fonts/misc"
    FontPath    "/usr/share/fonts/truetype"
    FontPath    "/usr/share/fonts/TTF"
    FontPath    "/usr/share/fonts/util"
EndSection

```

## 終端機字型

[虛擬終端機](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console")使用核心內建字型，預設顯示 ASCII 字元，這兩種設定都可以輕易改變。

終端機字型限定為 256 或 512 個字元。可供使用的字型存放在 `/usr/share/kbd/consolefonts/` 目錄。

鍵盤映射 (Keymap) 是按鍵和電腦使用字元的對應關係表，可以在 `/usr/share/kbd/keymaps/` 的子目錄下找到。

### 預覽和測試

**提示:** 一個整理過的預覽影像資料庫：[Linux 終端機字型截圖](http://alexandre.deverteuil.net/consolefonts/consolefonts.html)。

_showconsolefont_ 指令會以表格形式顯示可用字與字元：

```
$ showconsolefont

```

_setfont_ 工具可以暫時改變字型，讓使用者可以決定是否要採為預設值。只要指定字型名稱即可 (這些字型位於 `/usr/share/kbd/consolefonts/`)：

```
$ setfont Lat2-Terminus16

```

您可以用 `-m` 選項指定使用什麼字元集：

```
$ setfont Lat2-Terminus16 -m 8859-2

```

如果對新換的字型不滿意，用以下指令可以還原至預設字型 (就算終端機顯示亂碼，這個指令依然可以執行 -- 將指令「盲打」進去即可)：

```
$ setfont

```

**註記:** _setfont_ 只作用於目前正在使用的終端機。其它終端機無論活躍與否都不受影響。

### 更改預設字型

`/etc/vconsole.conf` 的 `FONT` 和 `FONT_MAP` 變數可用來改變預設字型。

若要顯示 _Č, ž, đ, š_ 或 _Ł, ę, ą, ś_ 之類的字元，使用 `lat2-16.psfu.gz` 這個字型：

```
FONT=lat2-16

```

這代表使用 ISO/IEC 8859 字元的第二部分，大小設定為 16。您可以使用其它值更改字型大小 (如 `lat2-08`)。您可以在[維基百科的這張表](https://en.wikipedia.org/wiki/ISO/IEC_8859#The_Parts_of_ISO.2FIEC_8859 "wikipedia:ISO/IEC 8859")查詢 8859 規格定義的區域。如果您經常在沒有 X 伺服器的終端機上工作，建議可以使用一種 Terminus 字型。比如說 ter-216b，代表包含 latin-2 部分，大小 16，粗體字。ter-216n 是正常磅數的版本。Terminus 字型大小最大可以到 32。

現在設定適當的字型映射，若使用 lat2-16 則會是：

```
FONT_MAP=8859-2

```

若要為早期的使用者空間套用指定字型，在 `/etc/mkinitcpio.conf` 使用 `keymap` 勾子。更多資訊請參閱 [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio")。

如果開機時字型沒有任何變化，或只變化一下就回復原樣，則有可能是因為圖形驅動啟動時字型被重設，然後終端機被切至幀緩衝 (framebuffer)。提早載入圖形驅動可以避免這個問題。若要在套用 `/etc/vconsole.conf` 之前將幀緩衝準備好，請參閱[核心模式設定#提早啟動 KMS](/index.php/Kernel_Mode_Setting#Early_KMS_start "Kernel Mode Setting")、[[1]](https://bbs.archlinux.org/viewtopic.php?id=145765) 或其它方式。

## 字型軟體包

以下是收錄於官方軟體庫和 [AUR](/index.php/AUR "AUR") 的字型軟體包列表，種類繁多，可依照需求選用。若字型有廣泛的萬國碼 (Unicode) 支援，會加註 "Unicode" 標記，詳情請參閱字型專案或相關的維基百科頁面。

一位 Github 使用者 Ternstor 用 python 腳本產生 [extra](http://ternstor.github.com/archfonts/extra.html), [community](http://ternstor.github.com/archfonts/community.html) 和 [AUR](http://ternstor.github.com/archfonts/aur.html) 庫內字型的 PNG 圖像，您可以在那裡預覽以下所提到的字型。

### 盲文點字

*   [ttf-ubraille](https://www.archlinux.org/packages/?name=ttf-ubraille) - 包含 Unicode **盲文點字**符號的字型

### 國際 (非英語系) 使用者

應用程式與瀏覽器會根據 fontconfig 設定和 Unicode 文字可用的字型來選擇其顯示字型。用指令 `fc-list :lang="雙字母的語言代碼"` 列舉系統安裝了哪些可對應該語言的字型。例如，列舉已經安裝的阿拉伯文字型，以及支援阿拉伯字的字型：

 `$ fc-list :lang=ar | cut -d: -f1` 

```
/usr/share/fonts/TTF/FreeMono.ttf
/usr/share/fonts/TTF/DejaVuSansCondensed.ttf
/usr/share/fonts/truetype/custom/DroidKufi-Bold.ttf
/usr/share/fonts/TTF/DejaVuSansMono.ttf
/usr/share/fonts/TTF/FreeSerif.ttf

```

若要在多國語言的網站 (如維基百科、Arch Linux wiki) 正確描繪字形，安裝這些軟體包：[ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont), [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming), [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk)

#### 阿拉伯和烏爾都文字

*   [ttf-qurancomplex-fonts](https://aur.archlinux.org/packages/ttf-qurancomplex-fonts/) - 位於麥地那的 King Fahd Glorious Quran Printing Complex 製作的字型 _(AUR)_
*   [ttf-amiri](https://aur.archlinux.org/packages/ttf-amiri/) - 一個典型的阿拉伯文謄抄體 (Naskh) 字型，一開始由 Amiria Press 採用 _(AUR)_
*   [ttf-sil-lateef](https://aur.archlinux.org/packages/ttf-sil-lateef/) - 來自 SIL 的 Unicode 阿拉伯文字型 _(AUR)_
*   [ttf-sil-scheherazade](https://aur.archlinux.org/packages/ttf-sil-scheherazade/) - 來自 SIL 的 Unicode 阿拉伯文字型 _(AUR)_
*   [ttf-arabeyes-fonts](https://aur.archlinux.org/packages/ttf-arabeyes-fonts/) - 自由的阿拉伯文字型集合 _(AUR)_

#### 緬甸文字

*   [ttf-myanmar3](https://aur.archlinux.org/packages/ttf-myanmar3/) - 緬甸手寫體字型 _(AUR)_

#### 中日韓越文字

##### 中文字

*   [ttf-tw](https://aur.archlinux.org/packages/ttf-tw/) - 台灣 (中華民國) 教育部標準楷書、宋體字型 _(AUR)_。
*   [cwttf-baseline](https://aur.archlinux.org/packages/cwttf-baseline/)、[cwttf-center](https://aur.archlinux.org/packages/cwttf-center/) - cwTeX 排版系統使用的字型集 (仿宋、粗黑、楷書、明體、圓體)。這兩個軟體包有標點符號位置的區別。
*   [cwtex-q-fonts](https://aur.archlinux.org/packages/cwtex-q-fonts/) - cwTeX 字型集的一些修正 (仍在開發狀態)
*   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) - 無襯線形式的高品質中日韓越 (CJKV) 輪廓字型。
*   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) - 黑體 (無襯線) 的中文輪廓字型，附帶點陣宋體 (也支援部分日韓字元)。
*   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai) - **楷書** (帶有筆觸) Unicode 字型 (建議啟用反鋸齒)
*   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) - **明體** (印刷) Unicode 字型
*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts) - **新宋**字型，之前為 ttf-fireflysung
*   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont) - 點陣宋體 (襯線) 中文字型
*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - 中文、越南文 TrueType 字型

##### 日文字

*   [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont) - 正規的日文哥特體 (無襯線) 與明朝體 (襯線) 字形集；其中一項高品質的開放原始碼字形。openSUSE-ja 的預設字形。
*   [ttf-vlgothic](https://aur.archlinux.org/packages/ttf-vlgothic/) - 日文哥特體字形。Debian/Fedora/Vine Linux 的預設字型 _(AUR)_
*   [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) - 現代哥特體的日文輪廓字型。包含所有日文平假名/片假名、Basic Latin、Latin-1 Supplement、Latin Extended-A、IPA Extensions。另外還有大部分日文漢字、希臘字母、西里爾字與越南文字，可以 7 磅 (等比例) 或 5 磅 (等寬) 字重顯示。 _(AUR)_
*   [ttf-ipa-mona](https://aur.archlinux.org/packages/ttf-ipa-mona/), [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/) - 日文字型，可正確顯示 [2ch 的 Shift JIS 藝術創作](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art")。 _(AUR)_
*   [ttf-sazanami](https://www.archlinux.org/packages/?name=ttf-sazanami) - 自由的日文 TrueType 字型。已經過期無人維護，但在某些環境下可當作備案字型使用。

##### 韓文字

*   [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk) - 韓文 TrueType 字型集合
*   [ttf-alee](https://aur.archlinux.org/packages/ttf-alee/) - 自由的韓文 (諺文；Hangul) TrueType 字型 (_AUR_)
*   [ttf-unfonts-core](https://aur.archlinux.org/packages/ttf-unfonts-core/) - Un 字型 (預設的 Baekmuk 字型較讓人不滿意) (_AUR_)
*   [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/) - 共享體 (Nanum) 系列 TrueType 字型 (_AUR_)
*   [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) - 共享體 (Nanum) 系列 TrueType 等寬字型 (_AUR_)

#### 西里爾文字

另請參閱[#等寬字型](#.E7.AD.89.E5.AF.AC.E5.AD.97.E5.9E.8B)、[#無襯線字型](#.E7.84.A1.E8.A5.AF.E7.B7.9A.E5.AD.97.E5.9E.8B)和[#襯線字型](#.E8.A5.AF.E7.B7.9A.E5.AD.97.E5.9E.8B)

*   [font-arhangai](https://aur.archlinux.org/packages/font-arhangai/) - 蒙古文西里爾字 (_AUR_)
*   [ttf-pingwi-typography](https://aur.archlinux.org/packages/ttf-pingwi-typography/) - PingWi Typography (PWT) 字型 (_AUR_)

#### 希臘文字

幾乎所有 Unicode 字型都包含希臘字元集 (也包含多調變音符號)。某些額外的字型軟體包未包含完整的 Unicode 集，但擁有高品質的希臘字字形 (當然包含拉丁字)：

*   [otf-gfs](https://aur.archlinux.org/packages/otf-gfs/) - 由 Greek Font Society 選用的 OpenType 字型 _(AUR)_
*   [ttf-mgopen](https://aur.archlinux.org/packages/ttf-mgopen/) - 來自 Magenta 的專業 TrueType 字型 _(AUR)_

#### 希伯來文字

*   [culmus](https://aur.archlinux.org/packages/culmus/) - 自由的希伯來文字型集合 _(AUR)_

#### 印地文字

*   [ttf-freebanglafont](https://www.archlinux.org/packages/?name=ttf-freebanglafont) - 孟加拉文字型
*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf) - 印地文 OpenType 字型集合 (包含 ttf-freebanglafont)

	(This one contains a "look of disapproval" that might be more to your liking than the [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont) one mentioned elsewhere in this document)

*   [lohit-fonts](https://aur.archlinux.org/packages/lohit-fonts/) - 來自 Fedora 專案的印地文 TrueType 字型 (包含 Oriya 字型以及更多) _(AUR)_

#### 高棉文字

*   [ttf-khmer](https://www.archlinux.org/packages/?name=ttf-khmer) - 涵蓋高棉語 (Khmer) 文字的字型
*   [Hanuman](http://code.google.com/webfonts/family?family=Hanuman&subset=khmer) ([ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 或 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))

#### 僧伽羅文字

*   [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/) - 僧伽羅文 (Sinhala) Unicode 字型 (_AUR_)

#### 塔米爾文字

*   [ttf-tamil](https://aur.archlinux.org/packages/ttf-tamil/) - 塔米爾文 (Tamil) Unicode 字型 (_AUR_)

#### 藏文字

*   [ttf-tibetan-machine](https://www.archlinux.org/packages/?name=ttf-tibetan-machine) - 藏文 (Tibetan) Machine TTFont

### 數學字型

*   [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica) - Wolfram 公司的 Mathematica 字型
*   [ttf-mathtype](https://aur.archlinux.org/packages/ttf-mathtype/) - MathType 字型 _(AUR)_
*   [ttf-computer-modern-fonts](https://aur.archlinux.org/packages/ttf-computer-modern-fonts/) - _(AUR)_

### Microsoft 字型

參閱[微軟字型](/index.php/MS_Fonts "MS Fonts")。

### Apple Mac OS X 字型

*   [ttf-mac-fonts](https://aur.archlinux.org/packages/ttf-mac-fonts/) - Mac OS X TrueType 字型
*   [ttf-mac](https://aur.archlinux.org/packages/ttf-mac/) - Mac OS X TrueType 字型。這個軟體包沒有內含 ttf 字型 (只有 otf 字型)，使用者必須自備這些字型。

### 等寬字型

有一些建議要給各位。每個使用者所偏好的字型不同，因此要找到您心目中的理想字型，就請多加嘗試。 如果您沒有太多時間，可以閱讀 Dan Benjamin 的部落格文章：[_Top 10 Programming Fonts_](http://hivelogic.com/articles/top-10-programming-fonts) (前十名適合寫程式的字型)。

這裡有 Trevor Lowing 整理的一長串字型清單：[http://www.lowing.org/fonts/](http://www.lowing.org/fonts/) 。

#### TrueType 字型

*   Agave ([ttf-agave](https://aur.archlinux.org/packages/ttf-agave/))
*   [Andalé Mono](https://en.wikipedia.org/wiki/Andal%C3%A9_Mono "wikipedia:Andalé Mono") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Anka/Coder ([ttf-anka-coder](https://aur.archlinux.org/packages/ttf-anka-coder/))
*   [Anonymous Pro](http://www.marksimonson.com/fonts/view/anonymous-pro) ([ttf-anonymous-pro](https://www.archlinux.org/packages/?name=ttf-anonymous-pro)，也包含在 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 和 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [Bitstream Vera Mono](https://en.wikipedia.org/wiki/Bitstream_Vera "wikipedia:Bitstream Vera") ([ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera))
*   [Consolas](https://en.wikipedia.org/wiki/Consolas "wikipedia:Consolas") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)) - Windows 下的編程用字型
*   [Courier New](https://en.wikipedia.org/wiki/Courier_New "wikipedia:Courier New") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Cousine ([ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 或 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS 的 Courier New 替代 (metric-compatible)
*   [DejaVu Sans Mono](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans Mono](https://en.wikipedia.org/wiki/Droid_(font) "wikipedia:Droid (font)") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)，也包含在 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 和 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   Envy Code R ([ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/))
*   [FreeMono](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Inconsolata](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata](https://www.archlinux.org/packages/?name=ttf-inconsolata)) - 極佳的編程用字型
*   [Inconsolata-g](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata-g](https://aur.archlinux.org/packages/ttf-inconsolata-g/)) - 加入一些親近編程人員的調整
*   [Liberation Mono](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - 可代替 Courier New (metric-compatible)
*   [Lucida Console](https://en.wikipedia.org/wiki/Lucida_Console "wikipedia:Lucida Console") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Lucida Typewriter](https://en.wikipedia.org/wiki/Lucida_Typewriter "wikipedia:Lucida Typewriter") (包含於 [jre](https://aur.archlinux.org/packages/jre/) 軟體包)
*   [Monaco](https://en.wikipedia.org/wiki/Monaco_(typeface) "wikipedia:Monaco (typeface)") ([ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco/)) - OSX/Textmate 下知名的編程用字型
*   Monofur ([ttf-monofur](https://aur.archlinux.org/packages/ttf-monofur/))

#### 點陣字型

*   Default 8x16
*   Dina ([dina-font](https://www.archlinux.org/packages/?name=dina-font))
*   [Gohu](http://font.gohu.org/) ([gohufont](https://aur.archlinux.org/packages/gohufont/))
*   Lime ([artwiz-fonts](https://www.archlinux.org/packages/?name=artwiz-fonts))
*   [ProFont](https://en.wikipedia.org/wiki/ProFont "wikipedia:ProFont") ([profont](https://www.archlinux.org/packages/?name=profont))
*   [Proggy Programming Fonts](https://en.wikipedia.org/wiki/Proggy_Programming_Fonts "wikipedia:Proggy Programming Fonts") ([proggyfonts](https://aur.archlinux.org/packages/proggyfonts/))
*   Proggy opti cyrillic ([proggyopticyr-font](https://aur.archlinux.org/packages/proggyopticyr-font/))
*   Tamsyn ([tamsyn-font](https://www.archlinux.org/packages/?name=tamsyn-font))
*   [Terminus](https://en.wikipedia.org/wiki/Terminus_(typeface) "wikipedia:Terminus (typeface)") ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font))
*   Unifont (glyphs like (look of disapproval)) ([bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont))

### 無襯線字型

*   [Andika](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=andika) ([ttf-andika](https://aur.archlinux.org/packages/ttf-andika/)，包含於 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/))
*   [Arial](https://en.wikipedia.org/wiki/Arial "wikipedia:Arial") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Arial Black](https://en.wikipedia.org/wiki/Arial_Black "wikipedia:Arial Black") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Arimo ([ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 或 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS 的 Arial 替代 (metric-compatible)
*   [Calibri](https://en.wikipedia.org/wiki/Calibri "wikipedia:Calibri") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Candara](https://en.wikipedia.org/wiki/Candara "wikipedia:Candara") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) "wikipedia:Constantia (typeface)") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) "wikipedia:Corbel (typeface)") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [DejaVu Sans](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans](https://en.wikipedia.org/wiki/Droid_(font) "wikipedia:Droid (font)") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)，包含於 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 和 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSans](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) "wikipedia:Impact (typeface)") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Sans](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)，品質提升的西里爾字：[ttf-liberastika](https://aur.archlinux.org/packages/ttf-liberastika/)) - 可替代 Arial (metric-compatible)
*   [Linux Biolinum](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine))
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [PT Sans](https://en.wikipedia.org/wiki/PT_Sans "wikipedia:PT Sans") ([ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 或 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - 3 種主要變體：正常、變窄與標題 - Unicode：拉丁字、西里爾字
*   [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) "wikipedia:Tahoma (typeface)") ([ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/))
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Ubuntu-Title](https://en.wikipedia.org/wiki/Ubuntu-Title "wikipedia:Ubuntu-Title") ([ttf-ubuntu-title](https://aur.archlinux.org/packages/ttf-ubuntu-title/))
*   [Ubuntu Font Family](https://en.wikipedia.org/wiki/Ubuntu_Font_Family "wikipedia:Ubuntu Font Family") ([ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family))
*   [Verdana](https://en.wikipedia.org/wiki/Verdana "wikipedia:Verdana") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### 手寫體

*   [Comic Sans](https://en.wikipedia.org/wiki/Comic_Sans "wikipedia:Comic Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### 襯線字型

*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) "wikipedia:Cambria (typeface)") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Charis](https://en.wikipedia.org/wiki/Charis_SIL "wikipedia:Charis SIL") ([ttf-charis](https://aur.archlinux.org/packages/ttf-charis/)，包含於 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode：拉丁字、西里爾字
*   [DejaVu Serif](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Doulos](https://en.wikipedia.org/wiki/Doulos_SIL "wikipedia:Doulos SIL") ([doulos-sil](https://aur.archlinux.org/packages/doulos-sil/)，包含於 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode：拉丁字、西里爾字
*   [Droid Serif](https://en.wikipedia.org/wiki/Droid_(font) "wikipedia:Droid (font)") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)，包含於 [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 和 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSerif](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Gentium](https://en.wikipedia.org/wiki/Gentium "wikipedia:Gentium") ([ttf-gentium](https://www.archlinux.org/packages/?name=ttf-gentium)，包含於 [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode：拉丁字、希臘字、西里爾字、音標字母
*   [Georgia](https://en.wikipedia.org/wiki/Georgia_(typeface) "wikipedia:Georgia (typeface)") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Serif](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Times New Roman 替代 (metric-compatible)
*   [Linux Libertine](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) - Unicode：拉丁字、希臘字、西里爾字、希伯來字
*   [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman "wikipedia:Times New Roman") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Tinos ([ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) 或 [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Chrome/Chromium OS 的 Times New Roman 替代 (metric-compatible)

### 未分類字型

*   [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/) and [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) — a huge collection of free fonts (including ubuntu, inconsolata, droid, etc.) - Note: Your font dialog might get very long as >100 fonts will be added. [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) pulls down the entire Mercurial repository from the upstream Web Fonts project. [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/) pulls from a much smaller and leaner unofficial repository hosted on GitHub. _(AUR)_
*   [ttf-mph-2b-damase](https://www.archlinux.org/packages/?name=ttf-mph-2b-damase) — Covers full plane 1 and several scripts
*   [ttf-symbola](https://www.archlinux.org/packages/?name=ttf-symbola) — Provides emoji and many many other symbols
*   [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/) — Gentium, Charis, Doulos, Andika and Abyssinica from SIL _(AUR)_
*   [font-bh-ttf](https://www.archlinux.org/packages/?name=font-bh-ttf) — X.Org Luxi fonts
*   [ttf-cheapskate](https://www.archlinux.org/packages/?name=ttf-cheapskate) — Font collection from _dustismo.com_
*   [ttf-isabella](https://aur.archlinux.org/packages/ttf-isabella/) — Calligraphic font based on the _Isabella Breviary_ of 1497
*   [ttf-junicode](https://www.archlinux.org/packages/?name=ttf-junicode) — Junius font containing almost complete medieval latin script glyphs
*   arkpandorafonts [ttf-arkpandora](https://aur.archlinux.org/packages/ttf-arkpandora/) — Alternative to Arial and Times New Roman fonts _(AUR)_
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

	所有 _TrueType_ 字型

```
# pacman -S $(pacman -Ssq ttf)

```

### 應用程式專用的字型快取

Matplotlib ([python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib) 或 [python2-matplotlib](https://www.archlinux.org/packages/?name=python2-matplotlib)) 使用自己的字型快取，因此更新字型後記得移除 `$HOME/.matplotlib/fontList.cache`，這樣它才會再產生一次快取並找到新字型 [[2]](http://matplotlib.1069221.n5.nabble.com/getting-matplotlib-to-recognize-a-new-font-td40500.html)。

## 另請參閱

*   [字型設定 (英)](/index.php/Font_configuration "Font configuration")