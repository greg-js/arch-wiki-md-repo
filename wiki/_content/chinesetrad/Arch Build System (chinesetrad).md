相關文章

*   [Arch 打包標準 (英)](/index.php/Arch_packaging_standards "Arch packaging standards")
*   [建立軟體包 (英)](/index.php/Creating_packages "Creating packages")
*   [核心編譯與 ABS (英)](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [PKGBUILD (英)](/index.php/PKGBUILD "PKGBUILD")
*   [makepkg (英)](/index.php/Makepkg "Makepkg")
*   [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)")
*   [官方倉庫](/index.php/Official_repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official repositories (正體中文)")
*   [使用者倉庫](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)")

**翻譯狀態：** 本文章是 [Arch_Build_System](/index.php/Arch_Build_System "Arch Build System") 的翻譯版本。最近一次的翻譯時間：2014-01-30。點擊[本連結](https://wiki.archlinux.org/index.php?title=Arch_Build_System&diff=0&oldid=284196)查看英文頁面之後的變更。

本文提供 Arch 組建系統的概覽，以及帶領初學者進行一遍操作。此文非完整的參考指南！如果需要更多資訊，請參考 man 手冊頁。

**註記:** ABS 一天同步一次，因此它和軟體庫上的版本稍微會有一點差距。

## Contents

*   [1 什麼是 Arch 組建系統？](#什麼是_Arch_組建系統？)
    *   [1.1 什麼是類似 ports 的系統?](#什麼是類似_ports_的系統?)
    *   [1.2 ABS 是類似的概念](#ABS_是類似的概念)
    *   [1.3 ABS 快速瀏覽](#ABS_快速瀏覽)
*   [2 我為什麼要用到 ABS？](#我為什麼要用到_ABS？)
*   [3 如何使用 ABS](#如何使用_ABS)
    *   [3.1 安裝工具](#安裝工具)
    *   [3.2 /etc/abs.conf](#/etc/abs.conf)
    *   [3.3 ABS 樹](#ABS_樹)
        *   [3.3.1 下載 ABS 樹](#下載_ABS_樹)
    *   [3.4 /etc/makepkg.conf](#/etc/makepkg.conf)
        *   [3.4.1 設定 /etc/makepkg.conf 的 PACKAGER 變數](#設定_/etc/makepkg.conf_的_PACKAGER_變數)
            *   [3.4.1.1 顯示所有軟體包 (包含 AUR 軟體包)](#顯示所有軟體包_(包含_AUR_軟體包))
            *   [3.4.1.2 只顯示軟體庫下的軟體包](#只顯示軟體庫下的軟體包)
    *   [3.5 建立組建目錄](#建立組建目錄)
    *   [3.6 組建軟體包](#組建軟體包)
        *   [3.6.1 fakeroot](#fakeroot)

## 什麼是 Arch 組建系統？

Arch 組建系統 (Arch Build System)，縮寫為 **ABS**，是一套類似（BSD）ports 的系統，能從原始碼組建軟體並打包。[Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 是 Arch 下特定的二進制安裝包管理工具（也包括管理那些從 ABS 組建的二進制安裝包），ABS 則是一組工具集，將原始碼編譯為一個可供安裝的 .pkg.tar.gz 軟體包。

### 什麼是類似 ports 的系統?

*Ports* 是 *BSD 下從原始碼組建軟體的自動化系統。系統使用一個 *port* 下載、解壓縮、修補、編譯並安裝給定的軟體。一個 *port* 差不多就是使用者電腦上的一個小目錄，以要安裝的相對應軟體命名，內部有幾個檔案指示如何從原始碼組建、安裝軟體。這讓安裝軟體這回事和在 port 目錄下輸入 `make` 或 `make install clean` 一樣簡單。

### ABS 是類似的概念

ABS 由目錄樹組成 (ABS tree)，位於 `/var/abs` 之下。這個樹包含了許多子目錄，每個子目錄有各自的分類與相對應的軟體包命名。這顆樹表示 (但不包含) 所有**官方 Arch 軟體**，可以透過 SVN 系統取得。您可以將這些以軟體包的名字命名的子目錄稱作 'ABS'，就如同這樣稱呼 'port' 一樣。這些 ABS (或子目錄) 不包含軟體包，也不包含原始碼，只有一份 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 檔案 (有時還會有其他檔案)。PKGBUILD 只是一個 Bash 組建腳本 -- 這份文字檔包含編譯與打包指令，以及下載適合**來源**封存包的 URL。(ABS 最重要的組件就是 PKGBUILD。) 呼叫 ABS 的 [makepkg](/index.php/Makepkg "Makepkg") 指令後，首先軟體會被編譯，接著在組建目錄下**打包**。之後您便可以使用 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 這個 Arch Linux 軟體包管理員來安裝、升級、移除您的新軟體包。

### ABS 快速瀏覽

'ABS' 包含並依賴數個其他組件，因此可被當作這些組件的總稱；雖然在技術上並非完全準確，'ABS' 可以指以下工具所構成的完整工具集：

	ABS 樹

	ABS 目錄架構；(本地) 機器 `/�var/abs/` 目錄下的 SVN 階層。包含數個子目錄，以所有 `/etc/abs.conf` 下指定軟體庫中可用的官方 Arch Linux 軟體命名，但不存放軟體包本身。以 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 安裝 [abs](https://www.archlinux.org/packages/?name=abs) 軟體包，並執行 `abs` 腳本，這顆樹才會被建立。

	[PKGBUILD](/index.php/PKGBUILD "PKGBUILD")

	包含原始碼 URL、編譯與打包指令的 [Bash](/index.php/Bash "Bash") 腳本。

	[makepkg](/index.php/Makepkg "Makepkg")

	ABS shell 指令工具，會閱讀 PKGBUILD、自動下載並編譯原始碼，並根據 `makepkg.conf` 的 `PKGEXT` 行建立 `.pkg.tar*`。您也可以使用 makepkg 建立來自 [AUR](/index.php/AUR_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "AUR (正體中文)") 或第三方來源的自訂軟體包。(參閱[建立軟體包](/index.php/Creating_packages "Creating packages") wiki 文章。)

	[pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)")

	pacman 和 ABS 完全切割，但若需要的話，可以由 makepkg 呼叫或手動執行。用途為安裝、移除組建軟體包與抓取相依軟體包。

	[AUR](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)")

	Arch 使用者倉庫和 ABS 基本上無關，但 (未受支援的) AUR PKGBUILD 可透過 makepkg 組建，編譯和打包軟體。與位於您本地機器上的 ABS 樹不同，AUR 基於網站介面。它包含數千個由使用者貢獻的 PKGBUILD，這些是無法從官方 Arch 軟體庫獲取的軟體。如果您需要組建官方 Arch 樹以外的軟體包，到 AUR 會有機會找得到。

## 我為什麼要用到 ABS？

Arch 組建系統被用來：

*   編譯或重新編譯軟體包，不論任何原因
*   若沒有可用的軟體包，可以從軟體原始碼建立並安裝新軟體包 (參閱[建立軟體包](/index.php/Creating_packages "Creating packages"))
*   已存在軟體包可以自訂以符合您的需求 (啟用或停用選項、修補程式)
*   使用您的編譯器旗標重新組建整套系統，「和 FreeBSD 一樣」 (例如使用 [pacbuilder](/index.php/Pacbuilder "Pacbuilder"))
*   乾淨的組建安裝您自訂的核心 (參閱[核心編譯](/index.php/Kernel_Compilation "Kernel Compilation"))
*   讓核心模組在您自訂的核心下可以運作
*   簡單編譯安裝 Arch 較新、較舊、測試或開發版本的軟體包，只需編輯 PKGBUILD 的版本號

ABS 並非 Arch Linux 下必需功能，但它是相當好用的原始碼編譯自動化工具。

## 如何使用 ABS

使用 abs 組建軟體包由以下步驟組成：

1.  用 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 安裝 [abs](https://www.archlinux.org/packages/?name=abs) 軟體包。
2.  以 root 身分執行 `abs`，和 Arch Linux 伺服器同步以建立 ABS 樹。
3.  將組建檔案 (通常位於 `/var/abs/<倉庫>/<軟體包名稱>`) 複製到組建目錄。
4.  到組建目錄編輯 PKGBUILD (若想要/需要的話)，並執行 **makepkg**。
5.  根據 PKGBUILD 的指令，makepkg 將下載適當的原始碼壓縮包、解壓縮、若有指定則套用修補、根據 `makepkg.conf` 指定的 `CFLAGS` 編譯，最後將組建檔案壓縮為副檔名 `.pkg.tar.gz` 或 `.pkg.tar.xz` 的軟體包。
6.  簡單一步 `pacman -U <.pkg.tar.xz 檔案>` 完成安裝。軟體包移除也交給 pacman 負責。

### 安裝工具

要使用 ABS，首先需要從[官方軟體庫](/index.php/Official_repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official repositories (正體中文)")[安裝](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") [abs](https://www.archlinux.org/packages/?name=abs)。

將會抓取 abs 同步腳本、各種組建腳本以及 [rsync](/index.php/Rsync "Rsync") (若沒有的話會以相依軟體安裝)。

在真正組建任何東西之前，您還需要基本的編譯工具。這些工具被收集於 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 這個[軟體群組](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#安裝軟體群組 "Pacman (正體中文)")。用 pacman 安裝這個群組。

### /etc/abs.conf

以 root 身分編輯 `/etc/abs.conf`，將您想要的軟體庫包含近來。

移除適當軟體庫前面的 `!`。舉例來說：

```
REPOS=(core extra community !testing)

```

### ABS 樹

ABS 樹是 `/var/abs` 下的 SVN 目錄階層，長得像這樣：

```
| -- core/
|     || -- acl/
|     ||     || -- PKGBUILD
|     || -- attr/
|     ||     || -- PKGBUILD
|     || -- abs/
|     ||     || -- PKGBUILD
|     || -- autoconf/
|     ||     || -- PKGBUILD
|     || -- ...
| -- extra/
|     || -- acpid/
|     ||     || -- PKGBUILD
|     || -- apache/
|     ||     || -- PKGBUILD
|     || -- ...
| -- community/
|     || -- ...

```

ABS 樹的架構和軟體包資料庫的架構完全一模一樣：

*   第一層：軟體庫名稱
*   第二層：軟體包名稱的目錄
*   第三層：PKGBUILD (包含組建軟體包所需資訊) 和其他相關檔案 (修補程式，和其他組建軟體包所需檔案)

ABS 目錄下並沒有軟體包的原始碼。**PKGBUILD** 檔案包含了原始碼的下載 URL，在組建軟體包時才會下載過來。因此 abs 樹其實相當小。

#### 下載 ABS 樹

以 root 身分執行：

```
# abs

```

現在，您的 ABS 樹已經建立在 `/var/abs` 下。在 `/etc/abs.conf` 指定的軟體庫，在 ABS 樹下也出現相對應的分支。

abs 指令應該定期執行，以和官方軟體庫同步。單一的 ABS 軟體包檔案也可以用下列指令下載：

```
# abs <倉庫>/<軟體包>

```

這樣您在組建一份軟體包時，就不需要檢查整個 abs 樹。

### /etc/makepkg.conf

`/etc/makepkg.conf` 指定了全域環境變數與編譯器旗標，若您使用 SMP (對稱多處理) 系統，或打算做其他優化的話，可以編輯這個檔案。預設設定值會對 i686 和 x86_64 作優化，在這類型架構的單核 CPU 系統下運作良好。(預設值也適用於 SMP 機器，但編譯時只會使用一個核心/CPU -- 參閱 [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf")。)

#### 設定 /etc/makepkg.conf 的 PACKAGER 變數

`/etc/makepkg.conf` 的 PACKAGER 變數設定是選用但**強烈建議**的步驟。它可以快速偵測哪個軟體包是由您組建/安裝，而非官方維護者！使用來自 community 庫的 [expac](https://www.archlinux.org/packages/?name=expac) 可以輕易達成：

##### 顯示所有軟體包 (包含 AUR 軟體包)

```
$ grep myname /etc/makepkg.conf
PACKAGER="myname <myemail@myserver.com>"

```

```
$ expac "%n %p" | grep "myname" | column -t
archey3 myname
binutils myname
gcc myname
gcc-libs myname
glibc myname
tar myname

```

##### 只顯示軟體庫下的軟體包

這個範例只顯示存在於 `/etc/pacman.conf` 所定義軟體庫的軟體包：

```
$ . /etc/makepkg.conf; grep -xvFf <(pacman -Qqm) <(expac "%n\t%p" | grep "$PACKAGER$" | cut -f1)
binutils
gcc
gcc-libs
glibc
tar

```

### 建立組建目錄

建議另外建立一個組建目錄，作為實際編譯使用；您不應直接在 ABS 樹組建，動到 ABS 樹，否則在每次 ABS 升級時會有資料遺失 (被覆寫)。使用自己的家目錄是個好辦法，有些 Arch 使用者會偏好在 `/var/abs/` 下建立一個 'local' 目錄，由一般使用者擁有。

建立您的組建目錄。例如：

```
$ mkdir -p $HOME/abs

```

從 (`/var/abs/<倉庫>/<軟體包名稱>`) 樹複製 ABS 到組建目錄。

### 組建軟體包

在這個範例，我們將組建 *slim* 顯示管理員。

將 ABS 樹的 slim ABS 複製到組建目錄：

```
$ cp -r /var/abs/extra/slim/ ~/abs

```

切換到組建目錄：

```
$ cd ~/abs/slim

```

修改 PKGBUILD 可新增和移除組件的支援、做修補或更改軟體包版本 (選用)：

```
$ nano PKGBUILD

```

以一般使用者身分執行 makepkg (`-s` 選項會自動處理安裝相依性)：

```
$ makepkg -s

```

**註記:** 若出現缺少的 (make) 相依性，請記得，預設假定所有的 Arch Linux 系統已經安裝 [base](https://www.archlinux.org/groups/x86_64/base/) 群組。當使用 **makepkg** 組建時也假定已安裝 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 群組。參閱[#安裝工具](#安裝工具)。

以 root 身分安裝：

```
# pacman -U slim-1.3.0-2-i686.pkg.tar.xz

```

這樣就完成了。您已經從原始碼組建了 slim，並用 pacman 安裝到您的系統，毫無瑕疵。軟體包移除也可以用 pacman 處理：`pacman -R slim`。

ABS 方法導入了方便性與自動化，也為組建與安裝函式維持完整的透明度和控制 (它們被包進 PKGBUILD 裡面)。

#### fakeroot

基本上，傳統方法 (一般包含 `./configure, make, make install` 步驟) 也會執行相同的步驟，但軟體會被安裝到 *fake root* (偽根目錄) 環境下。(*fake root* 只是組建目錄下一個子目錄，其作用和表現像是系統的根目錄。和 **fakeroot** 程式不同，makepkg 會建立一個假根目錄，並將編譯的二進位檔與相關檔案安裝進來，以 **root** 為檔案擁有者。) 這個 *fake root*，或包含編譯軟體的子目錄樹，接著會被壓縮為副檔名 `.pkg.tar.xz` 的封存檔，又稱「軟體包」。pacman 接著會解壓縮這個軟體包 (安裝) 至系統真正的根目錄 (`/`)。