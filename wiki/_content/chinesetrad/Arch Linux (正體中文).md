**翻譯狀態：** 本文章是 [Arch_Linux](/index.php/Arch_Linux "Arch Linux") 的翻譯版本。最近一次的翻譯時間：2014-07-04。點擊[本連結](https://wiki.archlinux.org/index.php?title=Arch_Linux&diff=0&oldid=304001)查看英文頁面之後的變更。

Arch Linux 是一套獨立開發、支援 [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)")/[x86-64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") 架構的通用 GNU/Linux 發行版本，靈活度高，適合各種用途。Arch 的開發著重於簡易、極簡化，以及優雅的編程。Arch 預設只會安裝一個迷你的基本系統，讓使用者自行組裝心目中最為理想的操作環境，只安裝所需的軟體包以達到目的。官方將不提供 GUI 配置工具，絕大多數的系統設定都將在 shell (文字介面) 和文字編輯器下進行。Arch 基於「漸進式發行」 (rolling-release)，致力走在最前線，並盡其所能地提供所有最新、最穩定的軟體。

## Contents

*   [1 歷史](#.E6.AD.B7.E5.8F.B2)
*   [2 簡潔](#.E7.B0.A1.E6.BD.94)
*   [3 現代化](#.E7.8F.BE.E4.BB.A3.E5.8C.96)
*   [4 軟體打包](#.E8.BB.9F.E9.AB.94.E6.89.93.E5.8C.85)
*   [5 來源完整性](#.E4.BE.86.E6.BA.90.E5.AE.8C.E6.95.B4.E6.80.A7)
*   [6 社群](#.E7.A4.BE.E7.BE.A4)
*   [7 總結](#.E7.B8.BD.E7.B5.90)

## 歷史

	**主文章：[Arch Linux 的歷史](/index.php/History_of_Arch_Linux "History of Arch Linux")**

Arch Linux 的起始作者是加拿大籍程式設計師 Judd Vinet。第一個正式版本 Arch Linux 0.1 於 2002/03/11 釋出。雖然 Arch 是完全獨立的發行版，但它也借鑑了其他發行版本講求簡潔的思想，例如 [Slackware](http://slackware.com)、[CRUX](http://www.crux.nu) 與 [BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution")。2007 年，Judd Vinet 離開專案領導人的位置，由美籍程式設計師 Aaron Griffin 接手領導專案至今。

## 簡潔

Arch Linux 盡可能地符合原本的「類 UNIX」系統：輕量、彈性加簡潔，並嚴格遵守 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")。安裝 Arch 之後，使用者會得到一個於 i686/x86-64 架構下編譯的最小化環境 (無 GUI)：Arch 不會自作聰明地提供多餘的預設軟體包，而是為使用者奠定基礎，讓使用者有個一磚一瓦打造系統的機會，不需要去剔除對自己毫無用處的軟體包。 有了 Arch 的設計哲學與實作，無論是擴充、打造任何類型的系統都變得更容易。**使用者**可以決定自己的 Arch 系統要變成什麼樣子：從小而精簡的終端機器，到大且功能豐富的桌面環境，統統都沒問題。

## 現代化

Arch Linux 致力將軟體保持在最新的穩定版本，並避免出現有任何系統軟體包損壞的狀況。Arch 屬於[漸進式發行](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release")系統，一次安裝、持續更新即可，您不用每次為了新釋出的版本而重新安裝。升級系統也沒有太冗長的步驟，您只需要一項指令，就能讓 Arch 系統維持最新、最前端的狀態。

Arch 內含 GNU/Linux 下很多嶄新的功能可供使用，像是 [systemd](/index.php/Systemd "Systemd") 初始化系統、現在主流的檔案系統 (Ext2/3/4, Reiser, XFS, JFS, BTRFS)、LVM2、軟體 RAID、udev 支援，以及 initcpio (附加 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"))，當然還包括最新版的 Linux 核心。

## 軟體打包

使用 Arch 不得不知 [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)")，這是一套容易使用的[軟體包管理員](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager")，升級整個系統只需一項指令。Pacman 是以 *C* 語言從頭開始撰寫，不僅輕量、簡潔，執行也十分快速。Arch 也提供了與 ports 類似的 [Arch 組建系統 (ABS)](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")，從下載程式原始碼、編譯到安裝都十分簡單，同步也只需一項指令。您甚至可以用一條指令重建整台系統。

Arch 的[官方倉庫](/index.php/Official_repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official repositories (正體中文)")提供了上千種高品質的軟體包，並同時支援 i686 與 x86-64 架構，相信能夠滿足您的軟體需求。另外，Arch 為了鼓勵社群的成長與貢獻，也提供 [Arch 使用者倉庫](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)")，裡頭包含了數千種由使用者自行維護的 PKGBUILD 腳本，只要使用 *makepkg* 程式，從下載源碼、編譯到打包軟體一氣呵成。使用者也可以輕鬆組建、維護他們自己的客製倉庫。

## 來源完整性

Arch 提供最乾淨的軟體，不加任何修補程式；所有軟體包都純粹來自[上游](https://en.wikipedia.org/wiki/upstream_(software_development) "wikipedia:upstream (software development)")原始碼，並完全照軟體作者的意思發布，以避免更新時因版本不符，對系統造成嚴重破壞。只有在非常罕見的情況下，我們才會使用修補程式。

## 社群

Arch 社群非常可靠活躍，也十分歡迎各位的加入。我們鼓勵每位 *Archer* 都能夠參與其中、付出貢獻：幫忙開發核心軟體、維護軟體包、回報/修復[臭蟲](https://bugs.archlinux.org/)、撰寫/潤飾 [ArchWiki 文件](/index.php/Main_page "Main page")，或是到[論壇](https://bbs.archlinux.org/)、[郵遞清單](https://mailman.archlinux.org/mailman/listinfo/)、[IRC 頻道](/index.php/IRC_channels "IRC channels")幫忙解決問題、交換意見、分享知識，甚至自行研發新程式！Arch Linux 已經成為全球許多使用者的首選作業系統，有數個[國際社群](/index.php/International_communities "International communities")提供幫助並以多國語言撰寫文件。

想要成為社群中活躍的一分子嗎？請參閱[加入我們](/index.php/Getting_involved "Getting involved")。

## 總結

總歸一句話：Arch Linux 是個麻雀雖小，五臟俱全的發行版本。它主攻熟悉 Linux® 的使用者，並符合他們的需求。Arch 強大又易於管理，是伺服器、工作站的理想發行版。Arch 是否跟您心目中 GNU/Linux 發行版本一模一樣呢？假如您跟我們有志一同，歡迎您盡情的使用 Arch，融入其中，並加入社群貢獻一份心力。歡迎加入 Arch 的行列！