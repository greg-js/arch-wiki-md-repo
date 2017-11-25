相關文章

*   [Arch Linux](/index.php/Arch_Linux_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux (正體中文)")
*   [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")

**翻譯狀態：** 本文章是 [Arch_Compared_to_Other_Distributions](/index.php/Arch_Compared_to_Other_Distributions "Arch Compared to Other Distributions") 的翻譯版本。最近一次的翻譯時間：2014-01-25。點擊[本連結](https://wiki.archlinux.org/index.php?title=Arch_Compared_to_Other_Distributions&diff=0&oldid=293646)查看英文頁面之後的變更。

這個頁面會將 Arch Linux 和其他流行的 GNU/Linux 發行版與類 UNIX 作業系統做個比較。您可以藉由下面的簡短描述，看看 Arch Linux 是否真的符合自己的需要。儘管在比較各家發行版本上有不少評價和說法，但最好的方式還是動手來安裝體驗。

## Contents

*   [1 基於原始碼的發行版](#.E5.9F.BA.E6.96.BC.E5.8E.9F.E5.A7.8B.E7.A2.BC.E7.9A.84.E7.99.BC.E8.A1.8C.E7.89.88)
    *   [1.1 Gentoo Linux](#Gentoo_Linux)
    *   [1.2 Sorcerer/Lunar-Linux/Source Mage](#Sorcerer.2FLunar-Linux.2FSource_Mage)
*   [2 極簡化發行版](#.E6.A5.B5.E7.B0.A1.E5.8C.96.E7.99.BC.E8.A1.8C.E7.89.88)
    *   [2.1 LFS](#LFS)
    *   [2.2 CRUX](#CRUX)
    *   [2.3 Slackware](#Slackware)
*   [3 通用發行版](#.E9.80.9A.E7.94.A8.E7.99.BC.E8.A1.8C.E7.89.88)
    *   [3.1 Debian GNU/Linux](#Debian_GNU.2FLinux)
    *   [3.2 Fedora](#Fedora)
    *   [3.3 Frugalware](#Frugalware)
*   [4 親近初學者的發行版](#.E8.A6.AA.E8.BF.91.E5.88.9D.E5.AD.B8.E8.80.85.E7.9A.84.E7.99.BC.E8.A1.8C.E7.89.88)
    *   [4.1 Ubuntu](#Ubuntu)
    *   [4.2 Mandriva](#Mandriva)
    *   [4.3 openSUSE](#openSUSE)
    *   [4.4 PCLinuxOS](#PCLinuxOS)
*   [5 BSD 系列](#BSD_.E7.B3.BB.E5.88.97)
    *   [5.1 FreeBSD](#FreeBSD)
    *   [5.2 NetBSD](#NetBSD)
    *   [5.3 OpenBSD](#OpenBSD)
*   [6 另請參閱](#.E5.8F.A6.E8.AB.8B.E5.8F.83.E9.96.B1)

## 基於原始碼的發行版

基於原始碼的發行版本的移植性很高，優點是可以根據機器架構與使用計畫來控制、編譯整套 OS 與應用程式，不過缺點就是編譯程式碼會消耗大量時間。所有 Arch 的軟體包都預先以 i686 和 x86_64 架構編譯，比起使用 i486/i586 二進位軟體包的發行版，除了效能潛在提升，且更適合用於安裝。

### Gentoo Linux

*   Arch Linux 和 Gentoo Linux 皆屬於漸進發行系統，在軟體上游釋出新版本後不久就可以獲取軟體包。
*   Gentoo 的軟體包與基本系統會透過使用者自訂的「USE 參數」，由原始碼直接組建而成。Arch 則提供一個類似 ports 的系統來組建軟體包，不過基本系統會以預先組建的 i686/x86_64 二進位檔安裝。總而言之，Arch 的組建與升級比較快速，而 Gentoo 可以達到更具系統的客製化。
*   Arch 支援 i686 和 x86_64 硬體架構，而 Gentoo 官方支援 x86, x86_64, PPC, SPARC, Alpha, ARM, MIPS, HP/PA, S/390, sh 以及 Itanium 硬體架構。
*   Gentoo 的官方軟體包/系統管理工具比 Arch 更為複雜且強大，且 Gentoo 的某些主打功能 (例如 [USE 參數](http://www.gentoo.org/doc/en/handbook/handbook-x86.xml?part=2&chap=2)、[SLOT](http://www.gentoo.org/doc/en/handbook/handbook-x86.xml?part=2&chap=1#doc_chap5)) 是 Arch Linux 所沒有的。這可能和 Arch 主要作為一個基於二進位檔的發行版有關係，但[設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")的不同也是其中一個因素。Arch 較偏向於「架構簡潔」這項原則，並避免無謂的**過度設計** (over-engineering)。
*   由於 Gentoo 和 Arch 預設只安裝基本系統，兩者都被認定為客製化相當具彈性的發行版。一般而言，Gentoo 使用者對 Arch 大部分方面都會感到滿意。

### Sorcerer/Lunar-Linux/Source Mage

*   Sorcerer/Lunar-Linux/Source Mage (SLS) 都是基於原始碼的發行版本，一開始它們是有關聯的。
*   SLS 發行版本使用一套簡單的腳本檔案來建立軟體包的描述單，並使用一個全域的設定檔來設定編譯過程，這和 [Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")相當類似。SLS 工具會做全套的相依性檢查，包括處理選用功能、軟體包追蹤、移除與升級。SLS 不提供二進位軟體包，但回過頭使用之前安裝的軟體包卻相當容易。
*   安裝過程包括從 shell 和 ncurses 選單設定基本系統，並可選擇將基本系統重新編譯。
*   和 Arch 一樣，SLS 沒有預設的 WM (視窗管理員)、DE (桌面環境)、DM (顯示管理員)，基本安裝也不包含 Xorg。但它有一些 X 伺服器的替代品 (X.Org 6.8 或 7, XFree86)。

## 極簡化發行版

極簡化發行版和 Arch 相當類似，有一些共通之處。這類發行版無論何種面向，用技術上的角度來看都相當「簡潔」。

### LFS

*   LFS (Linux From Scratch；從頭打造 Linux) 單純就是一份文件。這份文件指導使用者如何用一些基本軟體組建一個能運作的 GNU/Linux 系統：從獲取原始碼、手動編譯、修補和設定軟體，使用者都必須一手包辦。在組建與自訂基本系統這方面，LFS 相當迷你，且給使用者一個很棒的學習經驗。
*   LFS 不提供線上軟體庫；原始碼必須手動取得，並用 *make* 編譯安裝。(LFS Hints 有提到數種手動管理軟體包的方式)。
*   Arch 不僅提供 LFS 提到的基本軟體，還添加 [systemd](/index.php/Systemd "Systemd") 這套附帶工具，和強大的 [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 軟體包管理員當作本身的基本系統，並且所有的軟體皆預先編譯為適用 i686/x86_64 架構。除了這套小型 Arch 基本系統，Arch 社群與開發人員也提供、維護數千種二進位軟體包，可透過 pacman 以及 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 組建腳本 (由 [Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")處理) 安裝。Arch 還提供 [makepkg](/index.php/Makepkg "Makepkg") 工具，方便組建或自訂 *.pkg.tar.xz* 軟體包，也易於用 pacman 安裝。
*   Judd Vinet 從頭打造了 Arch，並以 C 語言撰寫 pacman。曾經有段期間 Arch 有一個幽默的稱呼：「附帶良好軟體包管理的 Linux」。

### CRUX

*   Judd Vinet 在創造 Arch 之前，使用 CRUX 並對它相當欣賞；這個極簡化發行版由 Per Lidén 創建。在 CRUX 和 BSD 的共同理念啟發下，便從零開始打造出 Arch，並以 C 語言撰寫 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)")。
*   Arch 和 CRUX 有同樣的指導原則：例如對硬體架構的優化、極簡化和秉持 K.I.S.S. 原則。
*   兩者皆擁有類似 ports 的系統，並且和 *BSD 系統一樣，都提供一個小型基本環境供使用者繼續組建。
*   Arch 使用 pacman 管理系統的二進位軟體包，並和 [Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)")無縫搭配。CRUX 則使用一個社群開發的系統 prt-get，與自己的 ports 系統一同處理相依性解析，但所有軟體包皆需要從原始碼組建。(不過 CRUX 的基本安裝會使用二進位包)。
*   Arch 官方支援 x86_64 與 i686，而 CRUX 只支援 x86_64。
*   Arch 使用漸進發行系統，並提供數個二進位包軟體庫以及 [Arch 使用者倉庫](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)")。CRUX 則提供更精簡的官方 ports 系統，加上一個相對而言較小的社群軟體庫。

### Slackware

*   Slackware 和 Arch 十分類似，它們都是致力於優雅與極簡化的發行版本。

*   Slackware 不作任何品牌推銷，並提供完全純淨的軟體包，從 Linux 核心到應用程式皆然。這是 Slackware 相當知名的一點。Arch 一般只有在避免嚴重故障、確保軟體包乾淨編譯的情況下，才會加上自有的修補程式。

*   Slackware 使用 BSD 式的 init 腳本，Arch 則使用 [systemd](/index.php/Systemd "Systemd")。

*   Arch 所提供的 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 軟體包管理系統和 Slackware 的標準工具不同，它會自動解析相依性，並提供更自動化的系統升級。Slackware 的使用者傾向於手動處理相依性問題，依據 Slackware 賦予他們的系統控制等級作出行動，另外 Slackware 在提供預裝函式庫與相依性方面相當傑出。

*   Arch 是漸進發行的系統。Slackware 的發行相對之下比較保少，偏向提供穩定的軟體包。Arch 在這一方面顯得相當「前衛」。

*   Arch Linux 的官方軟體庫提供了數千種二進位軟體包，相較之下 Slackware 的官方軟體庫能提供的軟體包較少。

*   Arch 提供一個類似 ports 的 [Arch 組建系統](/index.php/Arch_Build_System_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Build System (正體中文)"), 以及 [AUR](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)") (數以千計的使用者貢獻 PKGBUILD)。Slackware 也在 [slackbuilds.org](http://www.slackbuilds.org) 提供一個更輕薄的系統，這是 Slackbuilds 的半官方軟體庫，類似 Arch 的 PKGBUILD 概念。一般而言，Slackware 使用者對 Arch 大部分方面都會感到滿意。

## 通用發行版

這些發行版本擁有廣泛的優點與能力，可以勝任絕大部分的作業系統用途。

### Debian GNU/Linux

*   Debian 是上游最大的 Linux 發行版，社群規模更大，提供了穩定 (stable)、測試 (testing) 和不穩定 (unstable) 三條開發分支，提供超過 30,000 高品質的二進位軟體包。相較之下，Arch 提供的二進位軟體包顯得非常稀少。但如果將 AUR 包含進來，兩者的軟體數量其實相當接近。

*   Debian 熱衷於自由軟體，但仍然提供非自由軟體倉庫。Arch 對此較為寬鬆、包容，將是否選擇 GNU 定義的「非自由軟體包」交由使用者決定。

*   Debian 的設計方針著重於穩定、嚴格的測試，並基於其知名的 Debian 社會契約 (Debian social contract)。Arch 則著重於簡潔、極簡化、提供最尖端軟體的設計哲學。Arch 的軟體包版本比 Debian 穩定和測試分支的軟體版本還新，可媲美 Debian 的不穩定分支。

*   Debian 和 Arch 都提供了備受推崇的軟體包管理系統。

*   Arch 屬於漸進發行的系統。Debian 穩定分支則發行「凍結」的軟體包。Debian 不穩定分支也採用漸進發行。

*   Debian 可以用在多種硬體架構，包括 alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390 和 sparc；Arch 官方只支援 i686 與 x86_64，社群移植版只有 arm (例如 Raspberry Pi)。

*   組建外部來源的自訂軟體包這方面，Arch 有一個類似 ports 的軟體包組建系統，提供較快捷的支援。Debian 沒有提供類似的 ports 系統，得依靠本身其龐大的二進位軟體庫。

*   Arch 安裝系統只提供一個小型基本系統，系統設定必須原汁原味的進行；Debian 的安裝提供更自動化的設定，以及數種替代安裝方式。

*   Debian 預設採用 *SysVinit*，不過也可以使用 systemd 與 upstart 設定系統；Arch 則預設使用 [systemd](/index.php/Systemd "Systemd") 以獲得較佳的整體效能。

*   Arch 盡可能的不採用修補程式，以避免任何上游無法檢查的問題；Debian 的使用者群比較廣泛，因此對採用修補程式這件事開放許多。

### Fedora

*   Fedora 屬於社群開發的發行版，但背後有紅帽公司 (Red Hat) 支持；它通常被認為是一個尖端的測試發布系統；Fedora 的軟體包和專案會移植到 RHEL，有時還會被其它發行版採用。Arch 本身也被認為是走在尖端的發行版，不過它採用漸進式發行，且並非其它某個發行版本的測試分支。

*   Fedora 軟體包格式為 RPM，使用 YUM 軟體包管理員，也有官方的圖形軟體包工具可供使用。Arch 使用 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 管理 tar.xz 軟體包，且沒有任何官方支援的圖形前端介面。

*   Fedora 由於堅持只使用自由軟體，官方軟體庫拒絕收錄 MP3 媒體支援和其它非自由軟體，不過這些類型的軟體包可以在第三方軟體庫中找到。Arch 對於 MP3 和非自由軟體採取較為寬鬆的態度，讓使用者自己決定是否採用這些軟體。

*   Fedora 提供很多安裝選擇，包含圖形安裝與極簡化安裝。Fedora "spins" 也提供其它種類的桌面環境選擇，每個種類都附帶一些預設軟體包。另一方面，Arch 只提供幾個腳本來方便小型基本系統的安裝。

*   Fedora 有訂定發行時程，但官方支援透過 FedUp 工具進行跨版本升級。Arch 則採用漸進式發行。

*   **Arch 設計哲學 (Arch Way)** 著重於簡潔、輕量優雅、將選擇權還給使用者；**Fedora 核心價值 (Fedora Core Values)** 著重於自由軟體、社群發展與尖端的系統性革新。

*   Arch 有 ports 系統；Fedora 沒有。

*   **Arch 和 Fedora 都主攻有經驗的使用者與開發者。**兩者皆倡導它們的使用者多為專案的開發出一點力。

*   Fedora 在整合 SELinux、GCJ 編譯包 (用來解除對 Oracle 的 JRE 依類) 和積極的上游貢獻，已經為它贏得許多社群的認可；紅帽公司和 Fedora 開發者是 Linux 核心原始碼的首要貢獻者。

*   Arch Linux 提供了被廣泛認定是最豐富詳盡的發行版 wiki。Fedora wiki 比較符合 "wiki" 原始的用意，是作為開發人員、測試人員和使用者快速交換資訊的平台。它不像 Arch wiki 以終端使用者的知識庫自居。Fedora wiki 比較像是問題追蹤與協作 wiki。

### Frugalware

*   Arch 比較以命令列為導向。

*   Frugalware 預設不支援 JFS 檔案系統。

*   Arch 和 Frugalware 都主打針對 i686 架構優化。

*   Arch 一開始先安裝一個小型環境，接著根據使用者的選擇與需求由 pacman 擴充軟體。Frugalware 則從 DVD 安裝，並由使用者預先選擇預設軟體與桌面環境。

*   Frugalware 有訂定發行時程。Arch 著重於簡潔、極簡化、正確的編程與最尖端的軟體包，並採用漸進發行。

## 親近初學者的發行版

這些親近初學者的發行版本有時會被稱做「新手發行版」，這些發行版有很多共通特性，而 Arch 跟它們一比則顯得格格不入。如果您希望以萬丈高樓平地起的方式來學習 GNU/Linux，Arch 會是個比較好的選擇，因為相較於這些發行版，Arch 只需要安裝少量的軟體包。以下會描述各發行版與 Arch 有何特別不同之處。

### Ubuntu

*   Ubuntu 是一個大受歡迎的發行版，以 Debian 作為基礎，並由 Canonical 公司商業贊助；Arch 則是一個從頭打造、自主開發的系統。

*   Ubuntu 和 Arch 無論是目標或使用者群皆大不相同。Arch 主攻喜好自己動手實作的使用者；Ubuntu 則提供能自動設定的系統，以更親近一般使用者。Arch 以一份基本安裝起頭，由使用者自己打造成他們自己適用的系統，這種設計比起 Ubuntu 顯得簡約許多。一般而言，開發者和愛動手實作的人會比較喜歡 Arch，有不少 Arch 使用者都是從 Ubuntu 起頭，之後跳槽到 Arch。

*   目前 Ubuntu 的開發與推廣重心似乎往觸控型裝置移動；Arch 則堅持以使用者為中心，鼓勵社群合作建立自訂的解決方案。

*   Ubuntu 每隔 6 個月會發行新版本；Arch 屬於漸進式發行，每個月會釋出一份系統映像檔。

*   Arch 提供了類似 ports 的組建系統；Ubuntu 則無。

*   兩方的社群也有些許不同。Arch 社群很小，因此相當鼓勵使用者為發行版作出貢獻。相反地，規模較大的 Ubuntu 社群可以容忍大部分沒有參與開發、打包或維護軟體庫的使用者。

### Mandriva

Mandriva Linux (之前為 Mandrake Linux) 於 1998 創建，目標是做一套每個人都容易上手的 GNU/Linux。它以 RPM 為基礎，使用 urpmi 軟體包管理員。Arch 則採取較簡約的設計，以文字介面為主，較依賴手動設定，並針對中等到進階的使用者群。

### openSUSE

openSUSE 以 RPM 軟體包格式為主，它有備受推崇的 YaST2 圖形介面設定工具，這是可以滿足多數系統設定需求的百寶箱，還包括軟體包管理。Arch 不提供這類型的工具，因為它和 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")相違背。因此，openSUSE 比較適合那些經驗不足的使用者，和希望有較多圖形環境、自動化設定、安裝後可馬上工作的使用者。

### PCLinuxOS

*   PCLinuxOS 是以 Mandriva 為基礎的熱門發行版，它提供一個完整的桌面環境，其設計相當貼近使用者，使用上相當「簡單」。不過它的「簡單」和 Arch 定義的「簡單」大不相同。Arch 的設計是可從頭開始自訂的簡單基本系統，主要客群為進階使用者。

*   PCLOS 使用 apt 軟體包管理員來處理 RPM 軟體包。Arch 使用自己獨立開發的 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 軟體包管理員，軟體包格式為 *.pkg.tar.xz*。

*   PCLOS 的圖形化相當徹底，提供了圖形化硬體設定工具，以及 Synaptic 軟體包管理前端程式，並號稱所有工作都不需經由 shell。Arch 主要依靠命令列來達到更方便的系統設定、管理維護。

*   PCLOS 的建議最低需求 RAM 為 256 MB。相比之下，輕量的 Arch 可以在 RAM 遠低於該大小的系統上執行。一個基本 i686 的 Arch 安裝只需要 64 MB 的 RAM，且可以毫無差錯的在更先進的系統上執行。

## BSD 系列

各家 BSD 始於加州大學柏克萊分校 (UC Berkeley) 的成果，它們都提供了可自由散布並且免費的 UNIX 系統。它們並非 GNU/Linux 發行版，而是類 UNIX 作業系統。因此，雖然 Arch 和各家 BSD 都把基礎與移植系統緊密整合奉為圭臬，但以原始碼的角度來看兩者是毫無任何關係的。*vi* 可能是個例外，Arch 的 *vi* 就是採用原版的 BSD *vi* (多數 BSD 已經不再使用原版的 BSD *vi* 了)。各家 BSD 皆源自原本 AT&T 的 UNIX 程式碼，可算是真正的 UNIX 繼承者。若要了解各種 BSD 版本的更多資訊，可以拜訪它們的官方網站。

### FreeBSD

*   Arch 和 [FreeBSD](http://www.freebsd.org/about.html) 都以二進位檔，以及透過「移植」系統編譯的方式提供軟體。

*   跟其它的 BSD 一樣，FreeBSD 的基本系統是以一個整體的系統來開發的，每個應用程式都必須「移植」到 FreeBSD，並確認可以正常運作。與此對比，GNU/Linux 發行版本如 Arch，則匯集來自許多不同來源的軟體。

*   FreeBSD 授權一般而言更保護「編程者」，而與之對比的 GPL 較保護「程式碼」本身。Arch 是以 GPL 授權發布。

*   在 FreeBSD 就和在 Arch 一樣，決定權就在您 (使用者) 的手上。FreeBSD 的軟體更新度和 Arch 並駕齊驅，也各自擁有大小相近、聰穎、活躍並正經的社群。這或許是到目前為止和 Arch 最有意思的比較了。

*   兩個系統有不少共通點。一般而言，FreeBSD 使用者對 Arch 大部分方面都會感到滿意。

### NetBSD

*   NetBSD 是一個自由、安全且具高度移植性的類 UNIX 開源作業系統，可在超過 50 種平台上使用，上至 64 位元的 Opteron 機器、桌面系統，下至手持與嵌入式裝置。簡潔的設計和進階功能讓它在生產與研究環境下有極佳的表現，且擁有完整來源的使用者支援。透過 pkgsrc 和 NetBSD 軟體集合 (NetBSD Packages Collection) 可以獲取許多應用程式。

*   Arch 的平台支援度遠不及 NetBSD，但在 i686 系統上 Arch 可以提供較多的應用程式。

*   NetBSD 的 pkgsrc 提供基於原始碼的安裝方式，和 Arch 的 ABS 類似；它也可以使用 *pkg_tools* 獲取二進位軟體包。

*   Arch 和 NetBSD 有一些共通點：需要手動設定、極簡化並輕量、都提供移植系統與二進位包、都擁有活躍並正經的開發者與社群。

### OpenBSD

OpenBSD 專案提供自由、跨平台且基於 4.4BSD 的類 UNIX 作業系統。

*   OpenBSD 著重於可移植性、標準化、正確的編程、積極的安全性與整合加密。相較之下，Arch 更著重在簡潔、優雅、極簡化與尖端軟體。OpenBSD 自稱「也許是第一安全的 OS」。

*   Arch 和 OpenBSD 都只提供一個小而優雅的基本安裝。

*   兩者皆提供移植與打包系統，可簡單安裝與管理基本作業系統以外的程式。

*   OpenBSD 核心，以及 shell 和共通工具 (如 *ls*, *cp*, *cat*, *ps*) 這些與使用者相關的程式，都在同一個來源軟體庫下開發。這在諸如 Arch 的 GNU/Linux 系統下相當罕見，但在 BSD 類作業系統中，這是相當稀鬆平常的事。

## 另請參閱

*   [DistroWatch.com](http://distrowatch.com/)