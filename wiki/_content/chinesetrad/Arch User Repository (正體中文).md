Arch 使用者軟體倉庫 (AUR) 是由社群推動的使用者軟體庫。它包含了軟體包描述單 ([PKGBUILD](/index.php/PKGBUILD "PKGBUILD"))，可以用 [makepkg](/index.php/Makepkg "Makepkg") 從原始碼編譯軟體包，並透過 [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 安裝。 透過 AUR 可以在社群間分享、組織新進軟體包，熱門的軟體包有機會被收錄進 [community](#community) 軟體庫。這份文件將解釋如何存取、使用 AUR。

官方軟體庫中有不少發跡於 AUR 的新軟體包。在 AUR 下，使用者可以貢獻自己的軟體包組建資料 (PKGBUILD 與相關檔案)。AUR 社群可以投票支持/反對 AUR 的軟體包。若一個軟體包變得熱門 — 加上授權相容和優良的打包技術 — 就有機會被收錄進 _community_ 軟體庫 (可直接透過 [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 或 [ABS](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)") 存取)。

## Contents

*   [1 入門知識](#.E5.85.A5.E9.96.80.E7.9F.A5.E8.AD.98)
*   [2 歷史](#.E6.AD.B7.E5.8F.B2)
*   [3 搜尋](#.E6.90.9C.E5.B0.8B)
*   [4 軟體包安裝](#.E8.BB.9F.E9.AB.94.E5.8C.85.E5.AE.89.E8.A3.9D)
    *   [4.1 預備條件](#.E9.A0.90.E5.82.99.E6.A2.9D.E4.BB.B6)
    *   [4.2 獲取組建檔案](#.E7.8D.B2.E5.8F.96.E7.B5.84.E5.BB.BA.E6.AA.94.E6.A1.88)
    *   [4.3 組建軟體包](#.E7.B5.84.E5.BB.BA.E8.BB.9F.E9.AB.94.E5.8C.85)
    *   [4.4 安裝軟體包](#.E5.AE.89.E8.A3.9D.E8.BB.9F.E9.AB.94.E5.8C.85)
*   [5 回饋](#.E5.9B.9E.E9.A5.8B)
*   [6 軟體包分享與維護](#.E8.BB.9F.E9.AB.94.E5.8C.85.E5.88.86.E4.BA.AB.E8.88.87.E7.B6.AD.E8.AD.B7)
    *   [6.1 提交軟體包](#.E6.8F.90.E4.BA.A4.E8.BB.9F.E9.AB.94.E5.8C.85)
    *   [6.2 維護軟體包](#.E7.B6.AD.E8.AD.B7.E8.BB.9F.E9.AB.94.E5.8C.85)
    *   [6.3 其他要求](#.E5.85.B6.E4.BB.96.E8.A6.81.E6.B1.82)
*   [7 community 軟體庫](#community_.E8.BB.9F.E9.AB.94.E5.BA.AB)
*   [8 Git 軟體庫](#Git_.E8.BB.9F.E9.AB.94.E5.BA.AB)
*   [9 FAQ](#FAQ)
    *   [9.1 什麼是 AUR？](#.E4.BB.80.E9.BA.BC.E6.98.AF_AUR.EF.BC.9F)
    *   [9.2 AUR 許可什麼類型的軟體包？](#AUR_.E8.A8.B1.E5.8F.AF.E4.BB.80.E9.BA.BC.E9.A1.9E.E5.9E.8B.E7.9A.84.E8.BB.9F.E9.AB.94.E5.8C.85.EF.BC.9F)
    *   [9.3 我要如何投票給 AUR 軟體包？](#.E6.88.91.E8.A6.81.E5.A6.82.E4.BD.95.E6.8A.95.E7.A5.A8.E7.B5.A6_AUR_.E8.BB.9F.E9.AB.94.E5.8C.85.EF.BC.9F)
    *   [9.4 什麼是 TU？](#.E4.BB.80.E9.BA.BC.E6.98.AF_TU.EF.BC.9F)
    *   [9.5 Arch 使用者倉庫和 _community_ 的不同？](#Arch_.E4.BD.BF.E7.94.A8.E8.80.85.E5.80.89.E5.BA.AB.E5.92.8C_community_.E7.9A.84.E4.B8.8D.E5.90.8C.EF.BC.9F)
    *   [9.6 要多少個投票推薦才會讓 PKGBUILD 進入 _community_？](#.E8.A6.81.E5.A4.9A.E5.B0.91.E5.80.8B.E6.8A.95.E7.A5.A8.E6.8E.A8.E8.96.A6.E6.89.8D.E6.9C.83.E8.AE.93_PKGBUILD_.E9.80.B2.E5.85.A5_community.EF.BC.9F)
    *   [9.7 如何建立一份 PKGBUILD？](#.E5.A6.82.E4.BD.95.E5.BB.BA.E7.AB.8B.E4.B8.80.E4.BB.BD_PKGBUILD.EF.BC.9F)
    *   [9.8 我確定 "foo" 在 _community_ 庫，可是執行 "pacman -S foo" 卻失敗了。](#.E6.88.91.E7.A2.BA.E5.AE.9A_.22foo.22_.E5.9C.A8_community_.E5.BA.AB.EF.BC.8C.E5.8F.AF.E6.98.AF.E5.9F.B7.E8.A1.8C_.22pacman_-S_foo.22_.E5.8D.BB.E5.A4.B1.E6.95.97.E4.BA.86.E3.80.82)
    *   [9.9 AUR 的某個軟體已經過期，我該怎麼做？](#AUR_.E7.9A.84.E6.9F.90.E5.80.8B.E8.BB.9F.E9.AB.94.E5.B7.B2.E7.B6.93.E9.81.8E.E6.9C.9F.EF.BC.8C.E6.88.91.E8.A9.B2.E6.80.8E.E9.BA.BC.E5.81.9A.EF.BC.9F)
    *   [9.10 我打算提交一份 PKGBUILD，有沒有好心人可以幫忙檢查有沒有錯誤？](#.E6.88.91.E6.89.93.E7.AE.97.E6.8F.90.E4.BA.A4.E4.B8.80.E4.BB.BD_PKGBUILD.EF.BC.8C.E6.9C.89.E6.B2.92.E6.9C.89.E5.A5.BD.E5.BF.83.E4.BA.BA.E5.8F.AF.E4.BB.A5.E5.B9.AB.E5.BF.99.E6.AA.A2.E6.9F.A5.E6.9C.89.E6.B2.92.E6.9C.89.E9.8C.AF.E8.AA.A4.EF.BC.9F)
    *   [9.11 我從 AUR 下載某個軟體，執行 makepkg 卻無法編譯；我該怎麼做？](#.E6.88.91.E5.BE.9E_AUR_.E4.B8.8B.E8.BC.89.E6.9F.90.E5.80.8B.E8.BB.9F.E9.AB.94.EF.BC.8C.E5.9F.B7.E8.A1.8C_makepkg_.E5.8D.BB.E7.84.A1.E6.B3.95.E7.B7.A8.E8.AD.AF.EF.BC.9B.E6.88.91.E8.A9.B2.E6.80.8E.E9.BA.BC.E5.81.9A.EF.BC.9F)
    *   [9.12 重復性的組建過程有什麼方法可以加速？](#.E9.87.8D.E5.BE.A9.E6.80.A7.E7.9A.84.E7.B5.84.E5.BB.BA.E9.81.8E.E7.A8.8B.E6.9C.89.E4.BB.80.E9.BA.BC.E6.96.B9.E6.B3.95.E5.8F.AF.E4.BB.A5.E5.8A.A0.E9.80.9F.EF.BC.9F)
    *   [9.13 我該如何存取未支援的軟體包？](#.E6.88.91.E8.A9.B2.E5.A6.82.E4.BD.95.E5.AD.98.E5.8F.96.E6.9C.AA.E6.94.AF.E6.8F.B4.E7.9A.84.E8.BB.9F.E9.AB.94.E5.8C.85.EF.BC.9F)
    *   [9.14 如何在不使用網頁介面的情況下上傳資料至 AUR？](#.E5.A6.82.E4.BD.95.E5.9C.A8.E4.B8.8D.E4.BD.BF.E7.94.A8.E7.B6.B2.E9.A0.81.E4.BB.8B.E9.9D.A2.E7.9A.84.E6.83.85.E6.B3.81.E4.B8.8B.E4.B8.8A.E5.82.B3.E8.B3.87.E6.96.99.E8.87.B3_AUR.EF.BC.9F)
*   [10 另請參閱](#.E5.8F.A6.E8.AB.8B.E5.8F.83.E9.96.B1)

## 入門知識

使用者可以從 [AUR 網路介面](https://aur.archlinux.org)搜尋並下載各種軟體的 PKGBUILD。使用 [makepkg](/index.php/Makepkg "Makepkg") 可以將這些 PKGBUILD 組建成軟體包，並使用 pacman 安裝。

*   確定已經安裝 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 群組的軟體包 (`pacman -S --needed base-devel`)。
*   本文後面的章節有更多相關資訊，以及安裝 AUR 軟體包的簡短教學。
*   有關 AUR 軟體的升級與相關事件，請至 [AUR 網頁介面](https://aur.archlinux.org)。您可以在那裡找到統計數據和 AUR 可用軟體包的最新清單。
*   常見問題請參考 [#FAQ](#FAQ)。
*   在組建 AUR 軟體包之前，可以考慮調整 `/etc/makepkg.conf`，讓編譯器能針對您的處理器作效能優化。多核處理器的系統可以調整 MAKEFLAGS 變數，這樣編譯效率可以獲得明顯提升。使用者也可以透過 CFLAGS 變數來啟用 GCC 對特定硬體的優化。更多資訊請參閱 [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf")。

## 歷史

以下提到的項目已經成為過去式。它們已被 AUR 取代並不再使用。

一開始有個站點 `ftp://ftp.archlinux.org/incoming`，貢獻的使用者將他們的 PKGBUILD、需要的補充檔案以及組建出來的軟體包上傳至伺服器。軟體包和相關檔案會留在伺服器上，直到有[軟體包維護者](/index.php/Package_Maintainer "Package Maintainer")願意認養它為止。

之後，受信任使用者軟體庫 (Trusted User Repositories) 誕生了。社群中只有特定的成員可以放上自己的軟體庫供大家使用。AUR 就是這種基礎的延伸，目的是讓它變得更有彈性、更易於使用。事實上，AUR 維護者仍然被稱作是 TU (Trusted Users；受信任使用者)。

## 搜尋

AUR 網頁介面請到[這裡](https://aur.archlinux.org/), 一個適合透過腳本檔存取 AUR 的介面 (範例) 可參考[這裡](https://aur.archlinux.org/rpc.php)。

查詢功能透過 MySQL LIKE 比較來搜尋軟體包名稱和描述。這可以讓搜尋規則更有彈性 (例如，嘗試搜尋 `tool%like%grep`，而非 `tool like grep`)。如果您需要搜尋包含 `%` 的描述，記得加上逃脫字元，像這樣：`\%`。

## 軟體包安裝

從 AUR 安裝軟體包相對而言容易。基本上：

1.  獲取壓縮包，其中包含 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 和其他所需檔案，像是 systemd-units 和修補程式 (但通常不會有原始碼)。
2.  用 `tar -xzf foo.tar.gz` 將壓縮包解壓縮 (放在專門用來組建 AUR 的資料夾會比較好)。
3.  在存放這些檔案的目錄下執行 `makepkg` (`makepkg -s` 會自動以 pacman 解決相依性問題)。原始碼將會被下載、編譯並打包。
4.  在 `src/` 找尋 README 檔，上面可能有之後需要的資訊。
5.  以 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 安裝產生的軟體包：

	 `# pacman -U /path/to/pkg.tar.xz` 

[AUR 幫手程式](/index.php/AUR_helpers "AUR helpers")提供對 AUR 的無縫存取。它們的功能種類眾多，但都能夠輕易搜尋、抓取 AUR 上的 PKGBUILD，並組建、安裝軟體。這些腳本檔案都可以在 AUR 下找到。

**警告:** 在安裝來自 AUR 的組建材料這方面，從來沒有、且將來也不會有一個「官方」機制。**所有 AUR 的使用者應該要對組建過程相當熟悉。**

### 預備條件

首先，確認已經安裝所需工具。有軟體包群組 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 應該就足夠了；它提供了 [make](https://www.archlinux.org/packages/?name=make) 和其他編譯原始碼所需要的工具。

**警告:** AUR 的軟體包會假設 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 群組已經安裝，且 AUR 軟體包不會將這個群組下的軟體包列進相依性，即使沒有這些軟體包就無法組建。在報告組建失敗之前，請確認這個群組已經安裝。

```
# pacman -S --needed base-devel

```

接著選擇適當的組建目錄。組建目錄只是軟體包被建立、「組建」的所在目錄，它可以是任何一個目錄。常用目錄的範例：

```
~/builds

```

或者若使用 ABS ([Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)"))：

```
/var/abs/local

```

更多 ABS 的相關資訊請閱讀 [Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")一文。範例將會使用 `~/builds` 作為組建目錄。

### 獲取組建檔案

在 AUR 透過搜尋功能 ([AUR 首頁](https://aur.archlinux.org/)頂端的文字欄位) 找到軟體包。點擊搜尋清單上的應用程式名稱，會出現該軟體包的資訊頁面。閱讀描述以確認這是您需要的軟體包，檢查該軟體包版本是否為最新，並閱讀留言。

點擊右手邊 "Package actions" 的 "Download tarball" 連結下載所需組建檔案。這個檔案應該要存在組建目錄，或是下載後複製到組建目錄。在這個範例，檔案的名稱為 "foo.tar.gz" (若該軟體包有被正常提交，標準格式為 「**軟體包名稱**.tar.gz」)。

或者您可以從終端機直接下載壓縮包，首先更換目錄到組建目錄：

```
$ cd ~/builds
$ curl -O https://aur.archlinux.org/packages/fo/foo/foo.tar.gz

```

### 組建軟體包

將目錄換到組建目錄，並解壓縮先前下載的軟體包：

```
$ cd ~/builds
$ tar -xvzf foo.tar.gz

```

這樣就會在組建目錄下建立一個名為 "foo" 的目錄。

**警告:** **謹慎檢查所有檔案。** `cd` 進入新建目錄，並謹慎檢查 `PKGBUILD` 以及任何 `.install` 檔案，看有沒有任何有害指令。`PKGBUILD` 為 bash 腳本檔，包含要給 `makepkg` 執行的函式：這些函式可包含「任何」符合 Bash 語法的有效指令，因此 `PKGBUILD` 因惡意或過失行為而包含危險指令是絕對有可能的事。`makepkg` 使用 fakeroot (絕對不會以 root 執行) 而有相當的保護，但您不應該一直靠它來保障安全性。若對某軟體包有任何疑問，先不要進行組建，到論壇或郵件清單尋求建議。

```
$ cd foo
$ nano PKGBUILD
$ nano foo.install

```

建立軟體包。手動確認檔案的完整性後，以一般使用者身分執行 [makepkg](/index.php/Makepkg "Makepkg")。

```
$ makepkg -s

```

加上 `-s` 將以 [sudo](/index.php/Sudo "Sudo") 安裝所需相依性。如果不想使用 sudo，事前手動安裝所需相性，並拿掉上面指令的 `-s`。

### 安裝軟體包

使用 pacman 安裝軟體包。現在應該已建立一份壓縮檔：

```
<程式名稱>-<程式版本號>-<程式修訂版號>-<架構>.pkg.tar.xz

```

用 pacman 的「升級」(upgrade) 指令安裝此軟體包：

```
# pacman -U foo-0.1-1-i686.pkg.tar.xz   

```

這些手動安裝的軟體包被稱為外來軟體包 — 就是來自非任何 pacman 所知軟體庫的軟體包。列舉所有外來軟體包：

```
$ pacman -Qm 

```

**註記:** 以上的範例只提供軟體包組建過程的簡略摘要。[makepkg](/index.php/Makepkg "Makepkg") 和 [ABS](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)") 頁面會提供更詳盡的資訊，相當建議新進 Arch 的使用者參閱。

## 回饋

[AUR 網頁介面](https://aur.archlinux.org)有留言功能，是使用者向 PKGBUILD 貢獻者提供建議、回饋或改進的平台。避免直接在留言區貼上修補程式碼或 PKGBUILD：它們很快就會過期，並佔用太多版面。可以將這些檔案放在 email 寄給維護者，或是使用 [pastebin](/index.php/Pastebin_Clients "Pastebin Clients")。

對**所有** Arch 使用者來說，一個最簡單的參與就是瀏覽 AUR，透過線上介面**投票**給喜歡的軟體包。所有軟體包都有機會被 TU 認養，收錄進 [community](#community) 軟體庫，而得票數就是其中一項考量；每個人的投票都是有用的！

## 軟體包分享與維護

使用者可以透過 Arch 使用者軟體庫 (AUR) **分享** PKGBUILD。它不包含任何二進位軟體包，但允許使用者上傳 PKGBUILD 供其他人下載。這些 PKGBUILD 不受官方支援，且尚未完全審核，若要使用必須先考慮相關風險。

### 提交軟體包

**警告:** 在提交軟體包以前，您必須熟知 [Arch 打包標準](/index.php/Arch_packaging_standards "Arch packaging standards")，以及該文最後列舉的所有文章。

登入 AUR 網頁介面後，使用者可以將軟體包的組建檔案放在一個目錄下，用 gzip 壓縮為封存檔 (`.tar.gz`) 後[提交](https://aur.archlinux.org/pkgsubmit.php)。封存檔內的目錄應包含 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")、[.AURINFO](/index.php/.AURINFO ".AURINFO")，任何 `.install` 檔案、修補程式等等。(**絕對**不能包含二進位檔)。若您有安裝 [Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")，`/var/abs` 下有許多範例可供參考。

用以下指令來建立封存檔：

```
$ makepkg --source

```

注意，這是以 gzip 壓縮的封存檔；假設您要上傳名為 _libfoo_ 的軟體包，建立的封存檔應該會像這樣：

 `$ tar tf libfoo-0.1-1.src.tar.gz` 

```
libfoo/
libfoo/PKGBUILD
libfoo/libfoo.install
```

提交軟體包時應遵守以下規則：

*   Check the [official package database](https://www.archlinux.org/packages/) for the package. If **any version** of it exists, **do not** submit the package. If the official package is out-of-date, flag it as such. If the official package is broken or is lacking a feature, then please file a [bug report](https://bugs.archlinux.org/).
*   Check the AUR for the package. If it is currently maintained, changes can be submitted in a comment for the maintainer's attention. If it is unmaintained, the package can be adopted and updated as required. Do not create duplicate packages.
*   Verify carefully that what you are uploading is correct. All contributors must read and adhere to the [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") when writing PKGBUILDs. This is essential to the smooth running and general success of the AUR. Remember that you are not going to earn any credit or respect from your peers by wasting their time with a bad PKGBUILD.
*   Packages that contain binaries or that are very poorly written may be deleted without warning.
*   If you are unsure about the package (or the build/submission process) in any way, submit the PKGBUILD to the [AUR mailing list](https://mailman.archlinux.org/mailman/listinfo/aur-general) or the [AUR forum](https://bbs.archlinux.org/viewforum.php?id=4) on the Arch forums for public review before adding it to the AUR.
*   Make sure the package is useful. Will anyone else want to use this package? Is it extremely specialized? If more than a few people would find this package useful, it is appropriate for submission.
*   The AUR and official repositories are intended for packages which install generally software and software-related content, including one or more of the following: executable(s); config file(s); online or offline documentation for specific software or the Arch Linux distribution as a whole; media intended to be used directly by software.
*   Gain some experience before submitting packages. Build a few packages to learn the process and then submit.
*   If you submit a `package.tar.gz` with a file named `package` in it you will get an error: "Could not change to directory `/home/aur/unsupported/package/package`". To resolve this, rename the file named `package` to something else; for example, `package.rc`. When it is installed in the `pkg` directory, you may rename it back to `package`.

### 維護軟體包

*   If you maintain a package and want to update the PKGBUILD for your package just resubmit it.
*   Check for feedback and comments from other users and try to incorporate any improvements they suggest; consider it a learning process!
*   Please do not just submit and forget about packages! It is the maintainer's job to maintain the package by checking for updates and improving the PKGBUILD.
*   If you do not want to continue to maintain the package for some reason, `disown` the package using the AUR web interface and/or post a message to the AUR Mailing List.

### 其他要求

*   Disownment requests and removal requests go to the [aur-general mailing list](https://mailman.archlinux.org/mailman/listinfo/aur-general) for [Trusted Users](/index.php/Trusted_Users "Trusted Users") and other users to decide upon.
*   **Include package name and URL to AUR page**, preferably with a footnote [1].
*   Disownment requests will be granted two weeks after the current maintainer has been contacted by email and did not react.
*   **Package merging has been implemented**, users still have to resubmit a package under a new name and may request merging of the old version's comments and votes on the mailing list.
*   Removal requests require the following information:
    *   Package name and URL to AUR page
    *   Reason for deletion, at least a short note
        **Notice:** A package's comments does not sufficiently point out the reasons why a package is up for deletion. Because as soon as a TU takes action, the only place where such information can be obtained is the aur-general mailing list.
    *   Include supporting details, like when a package is provided by another package, if you are the maintainer yourself, it is renamed and the original owner agreed, etc.

Removal requests can be disapproved, in which case you will likely be advised to disown the package for a future packager's reference.

## community 軟體庫

_community_ 軟體庫由[受信任使用者](/index.php/Trusted_Users "Trusted Users")維護，包含來自 AUR 的熱門軟體包。預設 `/etc/pacman.conf` 已經啟用該庫。若 _community_被停用或移除，可以將這兩行取消註解/加入：

 `/etc/pacman.conf` 

```
...
[community]
Include = /etc/pacman.d/mirrorlist
...
```

這個軟體庫和 AUR 不同，它內含二進位軟體包，可以用 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 直接安裝，其組建檔案也可以透過 [ABS](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)") 存取。如果開發者認為某些軟體包對發行版具有重要性，它們甚至會被移到 _core_ 或 _extra_ 庫。

使用者也可以編輯 `/etc/abs.conf` 存取 _community_ 組建檔案，在 `REPOS` 一行啟用 _community_ 庫。

## Git 軟體庫

有一個 AUR 的 Git 軟體庫由 Thomas Dziedzic 維護，提供軟體包歷史。該庫一天至少會更新一次。複製這個軟體庫 (數百 MB)：

```
$ git clone git://pkgbuild.com/aur-mirror.git

```

更多資訊：[網頁介面](http://pkgbuild.com/git/aur-mirror.git/)、[論壇貼文](https://bbs.archlinux.org/viewtopic.php?id=113099)。

## FAQ

### 什麼是 AUR？

AUR (Arch 使用者倉庫) 是 Arch Linux 社群可以上傳應用程式、函式庫等等的 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 並與整個社群分享的地方。成員可以為自己喜歡的軟體投下一票，讓這些軟體有機會被移進 _community_ 軟體庫，讓所有 Arch Linux 使用者都可以取得二進位形式的軟體包。

### AUR 許可什麼類型的軟體包？

AUR 上的軟體包就是「組建腳本」，上面記載如何建立可讓 pacman 使用的二進位包。多數情況下，只要符合上述用途與方針，且符合內容的授權條款，就會獲得許可。For other cases, where it is mentioned that "you may not link" to downloads, i.e. contents that are not redistributable, you may only use the file name itself as the source. This means and requires that users already have the restricted source in the build directory prior to building the package. When in doubt, ask.

### 我要如何投票給 AUR 軟體包？

到 [AUR 網站](https://aur.archlinux.org/)上註冊後，當瀏覽軟體包時會出現 "Vote for this package" (投給這個軟體包) 選項。

### 什麼是 TU？

[TU (受信任使用者)](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") 是獲選管理 AUR 和 _community_ 軟體庫的人士。他們管理 _community_ 下的熱門 PKGBUILD，並保持 AUR 的運作。

### Arch 使用者倉庫和 _community_ 的不同？

Arch 使用者倉庫是存放使用者所提交的 PKGBUILD，必須手動以 [makepkg](/index.php/Makepkg "Makepkg") 組建。當 PKGBUILD 得到足夠的社群喜好與 TU 的支持，就會被移進 _community_ 軟體庫 (由 TU 維護)，裡頭的軟體包為二進位格式，可用 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 安裝。

### 要多少個投票推薦才會讓 PKGBUILD 進入 _community_？

通常要至少 10 票以上，軟體才有機會被移進 _community_。不過，如果有一位 TU 打算支援某軟體包，該軟體包就有可能會出現在軟體庫內。

### 如何建立一份 PKGBUILD？

[建立軟體包](/index.php/Creating_packages "Creating packages")是最好的來源。在建立 PKGBUILD 之前，記得到 AUR 查看是否有類似項目，避免重複勞動。

### 我確定 "foo" 在 _community_ 庫，可是執行 "pacman -S foo" 卻失敗了。

您可能沒有在 `/etc/pacman.conf` 啟用 _community_。將相關的行取消註解即可。 如果您的 `/etc/pacman.conf` 已經啟用了 _community_，先執行 `pacman -Syu` 同步快取並更新系統，再嘗試安裝 _foo_。

### AUR 的某個軟體已經過期，我該怎麼做？

剛入門的使用者可以先將軟體包標記已過期。如果該軟體包已過期一段時間，最好的辦法是 email 給維護者。若二個星期後維護者沒有回覆，且您有意願維護該軟體的話，可以向 aur-general 郵件清單發送郵件，通知 TU 標記該 PKGBUILD 為孤兒。如果軟體包的過期標記存在超過 3 個月，且很久未更新的話，請將它加入您的孤兒請求內。

### 我打算提交一份 PKGBUILD，有沒有好心人可以幫忙檢查有沒有錯誤？

如果您想讓大家評論您的 PKGBUILD，把它貼到 aur-general 郵件清單，讓 TU 和 AUR 的成員可以發表他們的看法。也可以從 [IRC 頻道](/index.php/ArchChannel "ArchChannel")，位於 irc.freenode.net 的 #archlinux 獲得幫助。您也可以使用 [namcap](/index.php/Namcap "Namcap") 檢查 PKGBUILD 和產生的軟體包是否有任何錯誤。

### 我從 AUR 下載某個軟體，執行 makepkg 卻無法編譯；我該怎麼做？

您可能是少了某些基本的東西。

1.  用 `makepkg` 編譯任何東西之前，先執行 `pacman -Syyu`；很有可能是您的系統尚未完全更新。
2.  確定您已經安裝 "base" 和 "base-devel" 群組下的軟體包。
3.  嘗試在 `makepkg` 後加上 "`-s`" 選項，在開始組建以前檢查並安裝所有需要的相依軟體包。

確認先閱讀過 PKGBUILD，以及 AUR 該軟體包頁面的留言。 問題的根源有時不那麼明顯。自訂的 CFLAGS, LDFLAGS 和 MAKEFLAGS 可能會導致編譯失敗。也有可能是 PKGBUILD 本身的問題。如果您無法自行推敲出問題所在，直接向負責的維護者回報：例如在 AUR 頁面上留言，貼上錯誤訊息。

### 重復性的組建過程有什麼方法可以加速？

如果您經常使用 gcc 編譯程式碼 - 比如說 git 或 SVN 軟體包 - [ccache](/index.php/Ccache "Ccache") (compiler cache 的簡寫) 或許會對您有用處。

### 我該如何存取未支援的軟體包？

參閱[#軟體包安裝](#.E8.BB.9F.E9.AB.94.E5.8C.85.E5.AE.89.E8.A3.9D)

### 如何在不使用網頁介面的情況下上傳資料至 AUR？

您可以使用 [burp](https://www.archlinux.org/packages/?name=burp), _aurploader_ ([python3-aur](https://aur.archlinux.org/packages/python3-aur/)) 或 [aurup](https://aur.archlinux.org/packages/aurup/) — 它們是命令列下的程式。

## 另請參閱

*   [AUR 網頁介面](https://aur.archlinux.org)
*   [AUR 郵件清單](https://www.archlinux.org/mailman/listinfo/aur-general)