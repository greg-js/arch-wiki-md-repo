相關文章

*   [安裝指南](/index.php/Installation_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Installation guide (正體中文)")
*   [一般建議](/index.php/General_recommendations_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "General recommendations (正體中文)")
*   [新手教學](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide (正體中文)")

本篇很大部分參考了 [Arch Linux Localization (简体中文)](/index.php/Arch_Linux_Localization_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux Localization (简体中文)")。雖然本地化的流程是相似的，但是正體中文化所需要的軟體和設定檔仍和簡體中文化有所不同，故有此篇文章的產生。

## Contents

*   [1 基本中文語系環境](#基本中文語系環境)
    *   [1.1 locale 設置](#locale_設置)
        *   [1.1.1 安裝中文 locale](#安裝中文_locale)
        *   [1.1.2 啟動中文 locale](#啟動中文_locale)
        *   [1.1.3 在圖形介面中啟用中文 locale](#在圖形介面中啟用中文_locale)
    *   [1.2 中文字體](#中文字體)
    *   [1.3 中文輸入法](#中文輸入法)
*   [2 終端機的中文化](#終端機的中文化)
*   [3 軟體的中文化](#軟體的中文化)
    *   [3.1 桌面環境](#桌面環境)
    *   [3.2 Firefox](#Firefox)
    *   [3.3 LibreOffice](#LibreOffice)
    *   [3.4 Calligra (原 KOffice)](#Calligra_(原_KOffice))
    *   [3.5 PDF 閱讀器](#PDF_閱讀器)
    *   [3.6 Vim](#Vim)
*   [4 其他中文化問題](#其他中文化問題)
    *   [4.1 MS Windows 底下的中文檔案名亂碼](#MS_Windows_底下的中文檔案名亂碼)

## 基本中文語系環境

### locale 設置

#### 安裝中文 locale

Linux 透過 locale 來設置不同語系的環境。常用的正體中文 locale 有

```
zh_TW.UTF-8
zh_TW.Big5

```

其中較推薦使用 en_US.UTF-8 和 zh_TW.UTF-8 語系。需要修改 `/etc/locale.gen` 文件，將需要的語系前面的註解 (# 符號)刪除。之後執行 locale-gen 指令即可。

如果要查詢目前系統所使用的語系環境，可以使用 locale 指令。

```
# locale

```

如果要查詢系統所有可用的語系環境，可以使用 locale -a 指令。

```
# locale -a

```

#### 啟動中文 locale

在 Arch Linux 中，透過設置 `/etc/rc.conf` 文件，來設置語系環境。

```
LOCALE=en_US.UTF-8

```

**注意:** 不推薦在這裡設置中文語系，會導致 tty 終端機亂碼。如果要在終端機裡顯示和輸入中文，需安裝 cce、zhcon 或 fbterm

對於一般使用者，還可以在 `~/.bashrc`、`~/.xinitrc` 或是 `~/.xprofile` 中設置語系，其中的不同處在於：

*   .bashrc: 每次透過終端機登入時，讀取並運行其中的設定
*   .xinitrc: 每次透過 startx 登入時，讀取並運行其中的設定
*   .xprofile: 每次透過圖形登入器 (如 gdm) 登入時，讀取並運行其中的設定

#### 在圖形介面中啟用中文 locale

如果是希望在圖形介面有中文環境的話，需要修改 `~/.xinitrc` 或 `~/.xprofile`，加入

```
export LANG=zh_TW.UTF-8
export LC_ALL=zh_TW.UTF-8

```

**注意:** 該方法適用於 slim 或無圖形登入器的場合，如果是 gdm 或 kdm 等可以在 Gnome 或 KDE 中設置語系

### 中文字體

除了設定中文 locale，還要安裝中文字體，才可顯示中文。

常見的免費中文字體有:

*   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont)
*   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei)
*   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai)
*   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming)
*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts)
*   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei)（[AUR](/index.php/AUR "AUR")中）
*   [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite)（[AUR](/index.php/AUR "AUR")中）

系统字體預設安裝到`/usr/share/fonts`。如果没有 root 權限或只打算自己使用某些字體，可以直接復製這些字體到`~/.fonts`目錄（或其子目錄）下面，並把該目錄加入 `/etc/fonts/local.conf` 中。

### 中文輸入法

常用的正體中文輸入法有 [gcin (正體中文)](/index.php/Gcin_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Gcin (正體中文)")、[scim (正體中文)](/index.php/Scim_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Scim (正體中文)") 以及由 gcin 分支出來的 [hime-git](https://aur.archlinux.org/packages/hime-git/) ([AUR](/index.php/AUR "AUR")中)。推薦使用 gcin 或 [hime-git](https://aur.archlinux.org/packages/hime-git/)。可看該輸入法文章，其中有較詳細的介紹。

以使用 gcin 為例，安裝好後在 `~/.xinitrc` 或 `~/.xprofile` 加入以下內容：

```
export XMODIFIERS="@im=gcin"
export XIM_PROGRAM="gcin"
export GTK_IM_MODULE="gcin"
export QT_IM_MODULE="gcin"
gcin &

```

之後即可在圖形介面中輸入中文。

## 終端機的中文化

## 軟體的中文化

### 桌面環境

除了 KDE 以外，其他的桌面環境，已經包括對中文語系環境的支持。對於 KDE 的使用者，如果需要正體中文，請安裝 [kde-l10n-zh_tw](https://www.archlinux.org/packages/?name=kde-l10n-zh_tw)，如果需要簡體中文，請安裝 [kde-l10n-zh_cn](https://www.archlinux.org/packages/?name=kde-l10n-zh_cn)。

**注意:** LXDE 目前只有正體中文支持

### Firefox

正體中文用戶請安裝 [firefox-i18n-zh-tw](https://www.archlinux.org/packages/?name=firefox-i18n-zh-tw)。

簡體中文用戶請安裝 [firefox-i18n-zh-cn](https://www.archlinux.org/packages/?name=firefox-i18n-zh-cn)。

### LibreOffice

正體中文用戶請安裝 [libreoffice-zh-TW](https://www.archlinux.org/packages/?name=libreoffice-zh-TW)。

簡體中文用戶請安裝 [libreoffice-zh-CN](https://www.archlinux.org/packages/?name=libreoffice-zh-CN)。

### Calligra (原 KOffice)

正體中文用戶請安裝 [calligra-l10n-zh_tw](https://www.archlinux.org/packages/?name=calligra-l10n-zh_tw)。

簡體中文用戶請安裝 [calligra-l10n-zh_cn](https://www.archlinux.org/packages/?name=calligra-l10n-zh_cn)。

### PDF 閱讀器

Acrobat Reader:，正體中文用戶請裝 [acroread-cht](https://aur.archlinux.org/packages/acroread-cht/)，簡體中文用戶請安裝 [acroread-chs](https://aur.archlinux.org/packages/acroread-chs/)。

xpdf: 請安裝 [xpdf-chinese-traditional](https://www.archlinux.org/packages/?name=xpdf-chinese-traditional) 和 [xpdf-chinese-simplified](https://www.archlinux.org/packages/?name=xpdf-chinese-simplified)。

poppler: 請安裝 [poppler-data](https://www.archlinux.org/packages/?name=poppler-data)。

### Vim

如果 locale 是 utf8，打開其他編碼的中文文件會有亂碼的問題，需要在 `~/.vimrc`中設定：

```
set fileencodings=ucs-bom,utf-8,big5,gbk,latin1

```

Vim 即會依序按照設定的編碼來打開文件。詳細的設定見 vim 中的幫助文件 `:help fileencodings`。

## 其他中文化問題

### MS Windows 底下的中文檔案名亂碼

是因為掛載的字符集和 locale 不同所致。可以修改 `/etc/fstab` 來修正這個問題。如果 locale 是 utf8 的情形下，可能修改為如下的範例 (請根據自己的實際情形略做修改)：

```
/dev/sdXX  /mnt/win  ntfs  defaults,iocharset=utf8   0 0

```

詳細的 `/etc/fstab` 設定可見 [fstab (正體中文)](/index.php/Fstab_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Fstab (正體中文)")。