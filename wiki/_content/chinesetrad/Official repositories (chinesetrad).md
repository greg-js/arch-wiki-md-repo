相關文章

*   [鏡像站 (英)](/index.php/Mirrors "Mirrors")
*   [Arch 使用者倉庫](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)")
*   [非官方使用者倉庫 (英)](/index.php/Unofficial_User_Repositories "Unofficial User Repositories")
*   [PKGBUILD (英)](/index.php/PKGBUILD "PKGBUILD")
*   [makepkg (英)](/index.php/Makepkg "Makepkg")
*   [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)")
*   [Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")

**翻譯狀態：** 本文章是 [Official_Repositories](/index.php/Official_Repositories "Official Repositories") 的翻譯版本。最近一次的翻譯時間：2014-01-24。點擊[本連結](https://wiki.archlinux.org/index.php?title=Official_Repositories&diff=0&oldid=291049)查看英文頁面之後的變更。

[軟體倉庫](https://en.wikipedia.org/wiki/software_repository "wikipedia:software repository")是存放軟體包的地點，安裝過程中可以從這些軟體庫取得軟體包。

**官方倉庫**包含了基本與常用的軟體包，透過 [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 可以輕鬆取得。

這些軟體包有特定的[維護者](/index.php/Package_Maintainer "Package Maintainer")維護。

## Contents

*   [1 軟體倉庫](#.E8.BB.9F.E9.AB.94.E5.80.89.E5.BA.AB)
    *   [1.1 core](#core)
    *   [1.2 extra](#extra)
    *   [1.3 community](#community)
    *   [1.4 multilib](#multilib)
    *   [1.5 testing](#testing)
        *   [1.5.1 community-testing](#community-testing)
        *   [1.5.2 multilib-testing](#multilib-testing)
*   [2 歷史背景](#.E6.AD.B7.E5.8F.B2.E8.83.8C.E6.99.AF)
    *   [2.1 official、unofficial、current 和 extra](#official.E3.80.81unofficial.E3.80.81current_.E5.92.8C_extra)

## 軟體倉庫

### core

這個軟體庫位於[鏡像站](/index.php/Mirror "Mirror")的 `.../core/os/` 目錄下。

core 包含的軟體包有以下用途：

*   啟動 Arch Linux
*   [連上網際網路](/index.php/Network_configuration_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Network configuration (正體中文)")
*   [組建軟體包](/index.php/Creating_packages "Creating packages")
*   管理並修復支援的[檔案系統](/index.php/File_systems "File systems")
*   系統設定程序 (例如 [openssh](https://www.archlinux.org/packages/?name=openssh))

以及上述軟體所需的其他相依軟體 (非必要的 makedepend)

*core* 軟體庫有嚴格的質量要求。一個更新軟體包必須經過開發人員與使用者的審核才會被接受。低使用率的軟體包只需經過合理的公開測試：更新通知、要求審核、視變更程度進行 (一星期以內的) 持續測試、無任何特殊錯誤報告，加上維護人員的審核即可。

**註記:** 若要在沒有網路的環境下建立本地的 *core* 軟體庫 (其他庫也可)，參閱[從 CD/DVD 或 USB 碟安裝軟體包](/index.php/Pacman_tips#Installing_packages_from_a_CD.2FDVD_or_USB_stick "Pacman tips")。

### extra

這個軟體庫位於鏡像站的 `.../extra/os/` 目錄下。

*extra* 包含所有不適合放在 *core* 的軟體包。例如 Xorg、視窗管理員、網路瀏覽器、媒體播放器、程式語言 (如 Python 和 Ruby) 的開發工具，還有更多程式。

### community

這個軟體庫位於鏡像站的 `.../community/os/` 目錄下。

*community* 包含從 [Arch 使用者倉庫](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)")選拔出來的軟體包，這些軟體都獲得相當的投票數，並由[受信任的使用者](/index.php/Trusted_Users "Trusted Users")認養。

### multilib

這個軟體庫位於鏡像站的 `.../multilib/os/` 目錄下。

*multilib* 包含 32 位元的軟體與函式庫，讓 64 位元機器可以執行、組建 32 位元的應用程式 (例如 [wine](https://www.archlinux.org/packages/?name=wine), [skype](https://aur.archlinux.org/packages/skype/))。

更多資訊請參閱 [Multilib](/index.php/Multilib "Multilib")。

### testing

**警告:** 謹慎啟用 *testing* 軟體庫，直接進行更新有可能導致系統損壞。只有當您有足夠的問題處理經驗時再考慮使用。

這個軟體庫位於鏡像站的 `.../testing/os/` 目錄下。

*testing* 包含 *core* 或 *extra* 軟體庫的候選軟體包。

會進入 *testing* 的軟體包有以下特點：

*   用它們更新有讓系統故障的風險，必須先進行測試。

*   它們需要其他軟體包才能組建。這種情況下，所有需要重建的軟體包都會被放進 *testing*，等到全部組建工作完成後，這些軟體包才會被移回原本的軟體庫。

*testing* 是唯一會和其他官方軟體庫產生名稱衝突的軟體庫。一旦啟用，必須將它擺在 `/etc/pacman.conf` 檔案的第一順位。

**註記:** *testing* 不是存放「最新」軟體包的地方。這個軟體庫也被用來暫存有破壞系統風險的更新軟體包：它們可能屬於 *core* 庫，或是在其他方面有極大影響。因此，強烈建議 *testing* 的使用者訂閱 [arch-dev-public 郵件清單](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public)，查看 [testing 軟體庫論壇](https://bbs.archlinux.org/viewforum.php?id=49)，並[回報所有遇到的錯誤](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")。

您必須同時啟用 *community-testing* 才能啟用 *testing* 軟體庫。

#### community-testing

這個軟體庫和 *testing* 類似，不過裡面的軟體包是 *community* 內軟體的候選版本。

您必須同時啟用 *testing* 才能啟用該軟體庫。

#### multilib-testing

這個軟體庫和 *testing* 類似，不過裡面的軟體包是 *multilib* 內軟體的候選版本。

您必須同時啟用 *testing* 才能啟用該軟體庫。

## 歷史背景

### official、unofficial、current 和 extra

大部分的軟體庫分支起因於歷史緣由。一開始，Arch Linux 的使用者相當稀少，當時只有一個 **official** 軟體倉庫 (就是現在的 *core*)。這個倉庫主要存放了 Judd Vinet 選定的應用程式。它設計為包含每個「類型」程式中的一種 ── 一個桌面環境 (DE)、一個主要瀏覽器，以此類推。

當時有些使用者對 Judd 的選擇不甚滿意，因此他們使用容易上手的 [Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")建立自己的軟體包。這些軟體包被放入一個名為 **unofficial** 的軟體倉庫，由 Judd 以外的開發人員維護。最終，兩個軟體倉庫皆獲得開發人員同樣的支持，**official** 和 **unofficial** 這兩個名稱也變得不合時宜。大概在 0.5 版本時期，兩個倉庫更名為 **current** 和 **extra** 。

2007.8.1 版本釋出後不久，*current* 更名為 **core**，以免讓人誤解它包含的內容。現今，所有軟體倉庫在開發人員和社群眼中都具有相同分量，不過 *core* 還是有些不同之處。主要區別在於，安裝光碟和發布快照只使用 *core* 的軟體包。這個倉庫是可以建立一個完整的 Linux 系統，但不一定是你心目中理想的 Linux 系統。

在 0.5/0.6 版本這段期間，有不少軟體包陷入了無人維護的困境。[Jason Chu](https://www.archlinux.org/fellows/#jason) 建立了**受信任使用者倉庫** (Trusted User Repositories)，**受信任使用者**（Trusted User; TU）可以將自己建立的軟體包放進這個非官方軟體庫。另外有個 **staging** 倉庫，裡面的軟體包可被 Arch Linux 的開發人員選進官方軟體庫，但除此之外，開發人員和受信任使用者之間依然存在或多或少的隔閡。

就這樣過了一段時間，直到受信任使用者對他們的軟體倉庫感到厭倦，非信任使用者又期望可以將自己的軟體包與大家分享。[AUR](https://aur.archlinux.org/) 因此誕生。TU 們開始形成更嚴密的組織，如今他們共同維護 **community** 軟體庫。TU 是一個獨立於 Arch Linux 開發人員的組織，兩者沒有太多交流。不過，偶爾有熱門的 *community* 軟體包會被選拔進 *extra*。[AUR](https://aur.archlinux.org/) 也支持允許非信任使用者提供自己的 PKGBUILD。

*core* 軟體庫的 Linux 核心曾[導致很多使用者系統當機](https://www.archlinux.org/news/please-avoid-kernel-261614-1/)，之後 Arch 引入了「core 軟體庫審核機制」。所有 *core* 的軟體包在更新前，必須先放進 **testing** 軟體庫，並經過數名開發人員的審核後，這些更新軟體包才會被放行進 *core*。過了一段時間，發現某些 *core* 軟體包的使用率很低，因此放寬對這些軟體包的審核機制：只要經過使用者簽核，或是沒有任何相關錯誤報告，都當作符合 (非正式的) 標準並接受。

2009 年末至 2010 年初，隨著某些新型檔案系統的出現，也冒出希望在安裝過程支援這些新格式的請求。鑒於 *core* 從來沒有被明確界定過（只是「由開發人員挑選的重要軟體包」），這個軟體庫終於得到一個更精確的定義。