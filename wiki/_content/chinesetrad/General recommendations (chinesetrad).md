**翻譯狀態：** 本文章是 [General_Recommendations](/index.php/General_Recommendations "General Recommendations") 的翻譯版本。最近一次的翻譯時間：2014-01-22。點擊[本連結](https://wiki.archlinux.org/index.php?title=General_Recommendations&diff=0&oldid=283108)查看英文頁面之後的變更。

相關文章

*   [常見問答集](/index.php/FAQ_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "FAQ (正體中文)")
*   [新手教學](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide (正體中文)")
*   [應用程式清單 (英)](/index.php/List_of_applications "List of applications")

這份註釋索引文件列舉了其他熱門文章和重要資訊，善用這些資源可以幫您新安裝的 Arch 系統提升和新增功能。這裡所列出的頁面需要使用 [pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 從[官方倉庫](/index.php/Official_repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official repositories (正體中文)")安裝額外的軟體包，至於來自非官方的 [Arch 使用者倉庫](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch User Repository (正體中文)")的軟體包，需要配置 [makepkg](/index.php/Makepkg "Makepkg")，另外可搭配 [AUR 幫助程式](/index.php/AUR_helper "AUR helper")使用。因此在繼續之前，應該徹底瞭解軟體包的管理概念。這裡假設讀者已經閱讀[新手教學](/index.php/Beginners%27_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' guide (正體中文)")或[安裝指南](/index.php/Installation_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Installation guide (正體中文)")，按照步驟安裝一個基本的 Arch Linux 系統。

## Contents

*   [1 外觀](#外觀)
    *   [1.1 彩色輸出](#彩色輸出)
        *   [1.1.1 終端機提示符](#終端機提示符)
        *   [1.1.2 核心工具](#核心工具)
        *   [1.1.3 Emacs shell](#Emacs_shell)
        *   [1.1.4 手冊頁](#手冊頁)
    *   [1.2 字型](#字型)
        *   [1.2.1 終端機字型](#終端機字型)
        *   [1.2.2 修補字型軟體包](#修補字型軟體包)
*   [2 影音](#影音)
    *   [2.1 瀏覽器插件](#瀏覽器插件)
    *   [2.2 編解碼器](#編解碼器)
    *   [2.3 音效](#音效)
*   [3 開機](#開機)
    *   [3.1 自動辨識硬體](#自動辨識硬體)
    *   [3.2 開機啟用 Num Lock](#開機啟用_Num_Lock)
    *   [3.3 保留開機訊息](#保留開機訊息)
    *   [3.4 開機啟動 X](#開機啟動_X)
*   [4 改進終端機](#改進終端機)
    *   [4.1 其他 shell](#其他_shell)
    *   [4.2 別名](#別名)
    *   [4.3 為 Bash 附加功能](#為_Bash_附加功能)
    *   [4.4 壓縮檔](#壓縮檔)
    *   [4.5 滑鼠支援](#滑鼠支援)
    *   [4.6 頁面滾動緩衝](#頁面滾動緩衝)
    *   [4.7 作業階段管理](#作業階段管理)
*   [5 輸入裝置](#輸入裝置)
    *   [5.1 鍵盤布局](#鍵盤布局)
    *   [5.2 滑鼠按鈕](#滑鼠按鈕)
    *   [5.3 觸控板](#觸控板)
    *   [5.4 小紅點 (TrackPoints)](#小紅點_(TrackPoints))
*   [6 網路](#網路)
    *   [6.1 時鐘同步](#時鐘同步)
    *   [6.2 DNS 加速](#DNS_加速)
    *   [6.3 DNSSEC 驗證](#DNSSEC_驗證)
    *   [6.4 設定防火牆](#設定防火牆)
*   [7 最佳化](#最佳化)
    *   [7.1 性能測試](#性能測試)
    *   [7.2 性能最佳化](#性能最佳化)
    *   [7.3 固態硬碟](#固態硬碟)
*   [8 軟體包管理](#軟體包管理)
    *   [8.1 pacman 的別名](#pacman_的別名)
    *   [8.2 Arch 建置系統](#Arch_建置系統)
    *   [8.3 Arch 使用者軟體倉庫](#Arch_使用者軟體倉庫)
    *   [8.4 鏡像站](#鏡像站)
*   [9 電源管理](#電源管理)
    *   [9.1 ACPI 事件](#ACPI_事件)
    *   [9.2 CPU 時脈調整](#CPU_時脈調整)
    *   [9.3 筆記型電腦](#筆記型電腦)
    *   [9.4 暫停與休眠](#暫停與休眠)
*   [10 系統管理](#系統管理)
    *   [10.1 權限提升](#權限提升)
    *   [10.2 使用者與群組](#使用者與群組)
    *   [10.3 Windows 網路](#Windows_網路)
    *   [10.4 系統維護](#系統維護)
*   [11 系統服務](#系統服務)
    *   [11.1 檔案索引與查詢](#檔案索引與查詢)
    *   [11.2 本地郵件遞送](#本地郵件遞送)
    *   [11.3 列印](#列印)
*   [12 X 視窗系統](#X_視窗系統)
    *   [12.1 桌面環境](#桌面環境)
    *   [12.2 顯示驅動](#顯示驅動)
    *   [12.3 視窗管理員](#視窗管理員)

## 外觀

這一節包含常見的「美觀」調整，可以增進 Arch 體驗。更多資訊請參閱[美觀分類](/index.php/Category:Eye_candy "Category:Eye candy")。

### 彩色輸出

雖然不少的應用程式已內建彩色輸出，使用一個通用的著色器 (如 `cope`) 也是另外一種方案。從 [AUR](/index.php/AUR_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "AUR (正體中文)") 安裝 [cope-git](https://aur.archlinux.org/packages/cope-git/)。類似的替代方案有 [acoc](https://aur.archlinux.org/packages/acoc/) 和 [cw](https://aur.archlinux.org/packages/cw/)。

#### 終端機提示符

終端機提示符 (PS1) 的客製化十分靈活。參考 [What's your PS1?](https://bbs.archlinux.org/viewtopic.php?id=50885) 這則論壇貼文尋求靈感。Bash 或 Zsh 的使用者也請分別參閱 [Bash 彩色提示符](/index.php/Color_Bash_Prompt "Color Bash Prompt")或 [Zsh#提示符](/index.php/Zsh#Prompts "Zsh")。

#### 核心工具

特定核心工具 (如 `grep` 和 `ls`)的彩色輸出，在[核心工具](/index.php/Core_utilities_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Core utilities (正體中文)")一文中提及。

#### Emacs shell

Emacs 並非一般的文字編輯器，它的知名之處在於功能豐富，其中一項就是當作全功能的 shell 使用。若啟用彩色輸出後出現亂碼，請參考 [Emacs#彩色輸出問題](/index.php/Emacs#Colored_output_issues "Emacs")。

#### 手冊頁

Man 頁 (或手冊頁) 是對 GNU/Linux 使用者手上最有幫助的資源之一。為了增進可讀性，可以設定分頁程式幫文字上色，如 [Man 頁#彩色顯示](/index.php/Man_page#Colored_man_pages "Man page")一文中解釋。

### 字型

[字型](/index.php/Fonts "Fonts")和[字型設定](/index.php/Font_configuration "Font configuration")文章內有不少相關資訊。

#### 終端機字型

若您有不少時間會在虛擬終端機上工作 (不使用 X 伺服器)，可以考慮更改終端機字型以提升可讀性；參閱[字型#終端機字型](/index.php/Fonts#Console_fonts "Fonts")。

#### 修補字型軟體包

有一些字型算繪函式庫適用的修補程式能提供更好的算繪效果；參閱[字型設定#修補程式軟體包](/index.php/Font_configuration#Patched_packages "Font configuration")。

## 影音

[Category:Multimedia](/index.php/Category:Multimedia "Category:Multimedia") 包含額外的多媒體資源。

### 瀏覽器插件

安裝[瀏覽器插件](/index.php/Browser_plugins "Browser plugins") (例如 Adobe Acrobat Reader, Adobe Flash Player 和 Java) 以享受網路的媒體資源和**完整**的瀏覽體驗。

### 編解碼器

[編解碼器](/index.php/Codecs "Codecs")是多媒體應用程式用來將音訊或視訊串流編/解碼的工具。為了能夠播放已編碼的串流，使用者必須確定已安裝相對應的編解碼器。

### 音效

[音效](/index.php/Sound "Sound")由核心的聲音驅動 ([ALSA](/index.php/ALSA "ALSA") 和 [OSS](/index.php/OSS "OSS")) 提供。使用者可以額外安裝設定音效伺服器。

## 開機

這一節包含與開機過程相關的資訊。Arch 開機過程的簡介可以在 [Arch 開機過程](/index.php/Arch_boot_process "Arch boot process")找到。更多請參閱[開機過程分類](/index.php/Category:Boot_process "Category:Boot process")。

### 自動辨識硬體

開機過程中，[udev](/index.php/Udev "Udev") 預設會自動偵測硬體。一種潛在改善開機時間的作法是：停用自動載入模組並手動指定所需模組，如[核心模組#載入](/index.php/Kernel_modules#Loading "Kernel modules")所述。此外，[Xorg](/index.php/Xorg "Xorg") 應能夠自動偵測使用 udev 的所需驅動，不過使用者也有手動設定 X 伺服器的選擇。

### 開機啟用 Num Lock

Num Lock 是多數鍵盤都有的切換鍵。若要在系統開機時啟用 Num Lock 的數字鍵，參閱[開機時啟用 Numlock](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup")。

### 保留開機訊息

開機完成後，螢幕會被清空以顯示登入提示，讓使用者無法收集開機過程的回饋訊息。[停用清理開機訊息](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages")來克服這項限制。

### 開機啟動 X

若圖形介面需要利用 [X](/index.php/X "X") 伺服器，可以考慮在開機階段啟動 X 伺服器，而非登入後再手動啟動。若需要圖形登入介面，請參閱[顯示管理員](/index.php/Display_manager_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Display manager (正體中文)")，或者參閱不需要顯示管理員的方式：[開機時啟動 X](/index.php/Start_X_at_Boot "Start X at Boot")。

## 改進終端機

這一節包含讓終端機程式更實用的小修改。更多資訊請參閱[指令 Shell 分類](/index.php/Category:Command_shells "Category:Command shells")。

### 其他 shell

[Bash](/index.php/Bash "Bash") 是安裝 Arch 系統時預設的 shell；Live 安裝媒體使用的是 [zsh](/index.php/Zsh "Zsh") 附帶 [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) 軟體包。更多可選用的 shell 請參閱[指令 Shell#Shell 清單](/index.php/Command_shell#List_of_shells "Command shell")。

### 別名

使用者可以利用內建的 shell 指令，為常用指令定義捷徑。常見的省時別名可以在 [Bash#別名](/index.php/Bash#Aliases "Bash")找到，這些別名也可以輕鬆轉移至 [zsh](/index.php/Zsh "Zsh")。

### 為 Bash 附加功能

[Bash#提示與技巧](/index.php/Bash#Tips_and_tricks "Bash")有一份 Bash 設定清單，其中包含了補完功能增強、歷史記錄搜尋與 [Readline](/index.php/Readline "Readline") 巨集。

### 壓縮檔

壓縮檔案 (封存檔) 經常在 GNU/Linux 系統上出現。[Tar](/index.php/Tar "Tar") 是一個常用的封存工具，很多使用者應該對它的語法很有印象 (例如 Arch Linux 的軟體包，是單純用 xz 壓縮的 tar 封存包)。其他有用指令請參閱 [Bash#函式](/index.php/Bash#Functions "Bash")。

### 滑鼠支援

在終端機進行複製貼上，除了使用 [GNU Screen](/index.php/GNU_Screen "GNU Screen") 的傳統複製模式，也可以直接使用滑鼠。詳細步驟請參考[終端機滑鼠支援](/index.php/Console_mouse_support "Console mouse support")。

### 頁面滾動緩衝

參考[頁面滾動緩衝](/index.php/Scrollback_buffer "Scrollback buffer")，瞭解如何儲存、檢視被滾出螢幕外的文字。

### 作業階段管理

使用終端機多工器 (如 [tmux](/index.php/Tmux "Tmux") 或 [GNU Screen](/index.php/GNU_Screen "GNU Screen"))，程式可以在由分頁與面板組成的作業階段中執行。這些作業階段可以隨意拆解，因此就算使用者殺掉終端模擬器、終止 [X](/index.php/X "X") 或登出，只要終端機多工伺服器仍在運作，與作業階段相關聯的程式就會繼續在背景執行。若要和程式互動，必須重新連接作業階段。

## 輸入裝置

這一節包含常用輸入裝置的設定提示。更多資訊請參閱[輸入裝置分類](/index.php/Category:Input_devices "Category:Input devices")。

### 鍵盤布局

預設狀況下，非英語系、非標準型的鍵盤通常不會正常運作。虛擬終端機和 [Xorg](/index.php/Xorg "Xorg") 下有各自設定鍵盤映射的必要步驟，分別列於[終端機的鍵盤設定](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console")和[Xorg的鍵盤設定](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg")。

### 滑鼠按鈕

若您使用較進階或罕見的滑鼠，可能會碰到有滑鼠按鈕無法被預設偵測的問題，或者您希望為附加按鍵設定不同的動作。解決步驟請至[讓所有滑鼠按鍵運作](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working")。

### 觸控板

多數筆記型電腦使用 [Synaptics](http://www.synaptics.com/) 或 [ALPS](http://www.alps.com/) 「觸控板」指向裝置。這些觸控板 (以及數種他牌觸控板) 都使用 Synaptics 輸入驅動；安裝與設定詳情請參閱 [Synaptics 觸控板](/index.php/Touchpad_Synaptics "Touchpad Synaptics")。

### 小紅點 (TrackPoints)

參考 [ThinkWiki](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint) 設定小紅點。

## 網路

這一節限定於小型的網路問題。完整指南請前往[網路設定](/index.php/Network_configuration_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Network configuration (正體中文)")。更多資訊請參閱[網路分類](/index.php/Category:Networking "Category:Networking")。

### 時鐘同步

[網路時間協定](/index.php/Network_Time_Protocol "Network Time Protocol") (NTP) 是一種透過封包交換、可變延遲的資料網路同步電腦系統時鐘的協定。

### DNS 加速

建立查詢快取可以加速載入時間。可以利用 [pdnsd](/index.php/Pdnsd "Pdnsd") 這個簡單的 DNS 伺服器。或者安裝 [dnsmasq](/index.php/Dnsmasq "Dnsmasq")，它同時可以把系統變成一台 DHCP 伺服器。

### [DNSSEC](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions "wikipedia:Domain Name System Security Extensions") 驗證

為了讓瀏覽網頁、線上付款、連接 [SSH](/index.php/SSH "SSH") 服務等線上操作更加安全，可以考慮有啟用 [DNSSEC](/index.php/DNSSEC "DNSSEC") 的客戶端軟體，驗證簽署過的 [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") 記錄。

### 設定防火牆

[防火牆](/index.php/Firewalls "Firewalls")在 Linux 網路層上加裝了一層保護。Linux 核心內帶 iptables 這套[狀態檢測防火牆](https://en.wikipedia.org/wiki/Stateful_firewall "wikipedia:Stateful firewall")，它是 [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter") 專案的一部分。iptables 可直接設定，或是透過前端介面的協助。Arch 預設不開啟任何連接埠，且若沒有明確設定，network 守護程序不會自動啟動，因此，如果您沒有打算執行任何需要保護的服務，不太需要特別設定防火牆。

## 最佳化

這一節總結了提升系統、應用程式表現的各種調整、工具和可行選項。

### 性能測試

[性能測試](/index.php/Benchmarking "Benchmarking")會測量系統表現，以統一規範的步驟將結果與其他系統的結果或廣泛認定的標準比對。

### 性能最佳化

[性能最佳化](/index.php/Improving_performance "Improving performance")一文中收集了增進 Arch Linux 效能的資訊。

### 固態硬碟

[固態硬碟](/index.php/Solid_State_Drives "Solid State Drives")一文涵蓋了有關固態硬碟 (SSD) 的各種面向，例如延長 SSD 使用壽命的方式。

## 軟體包管理

這一節包含軟體包管理的幫助資訊。所有使用者都應該熟悉 [Pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 軟體包管理員。更多資訊請參閱[軟體包管理分類](/index.php/Category:Package_management "Category:Package management")。

### pacman 的別名

幫單一或整組指令取別名，在使用終端機時可以有效節省時間。對於那些一再重複且不需大幅度調整參數的指令而言特別好用。各種省時的 pacman 別名已整理在 [Pacman 提示](/index.php/Pacman_tips "Pacman tips")，該文也提到其他建議工具。

### Arch 建置系統

*Ports* 是最初由 BSD 發行版本採用的建置腳本系統，本身為系統內部的目錄樹。每個 port 包含一個腳本，每個腳本存放的目錄直觀地以這些可安裝的第三方應用程式的名稱命名。

[ABS](/index.php/ABS "ABS") 樹也提供了相同的功能。它依靠 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 建置腳本，裡頭包含了給定軟體的資訊：完整性雜湊值、專案 URL、版本；授權與建置步驟。這些 PKGBUILD 腳本之後交給 [makepkg](/index.php/Makepkg "Makepkg") 解析，並產生 pacman 可無瑕疵管理的軟體包。

倉庫內所有的軟體包，加上 AUR 提供的軟體，都會經過 makepkg 重新編譯。

### Arch 使用者軟體倉庫

[ABS](/index.php/ABS "ABS") 樹可以讓使用者自行編譯建置官方倉庫的軟體，而在 [AUR](/index.php/AUR_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "AUR (正體中文)")，您可以編譯建置使用者群提交的軟體包。這是未受 (官方) 支援的建置腳本倉庫，可透過[網路介面](https://aur.archlinux.org/index.php)或 [AUR 幫手程式](/index.php/AUR_helper "AUR helper")存取。

[AUR 幫手程式](/index.php/AUR_helper "AUR helper")提供了 [AUR](/index.php/AUR_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "AUR (正體中文)") 的無縫存取方式。儘管有功能上的差異，但所有的幫手程式都有辦法從非官方倉庫內超過 40'000 個 PKGBUILD 檔案內，輕易搜尋、抓取、建置並安裝軟體。

### 鏡像站

參閱[鏡像站](/index.php/Mirrors "Mirrors")，瞭解如何使用最快速、最新的 Pacman 鏡像站。如該文章內所述，一個良心建議是定期檢查[鏡像站狀態](https://www.archlinux.org/mirrors/status/)與 [Mirror-Status](http://www.archlinux.de/?page=MirrorStatus)，上面有最近同步的鏡像站清單。

## 電源管理

這一節針對的是筆電使用者，以及需要電源管理控制的使用者。更多資訊請參閱[電源管理分類](/index.php/Category:Power_management "Category:Power management")。

總論請參閱[電源管理](/index.php/Power_management "Power management")。

### ACPI 事件

使用者可以設定系統碰到 ACPI 事件時的反應，比如說按下電源鈕或闔上筆電。(建議的) 新方案是採用 [systemd](/index.php/Systemd "Systemd")，參閱[用 systemd 作電源管理](/index.php/Power_management#Power_management_with_systemd "Power management")。舊方案則參閱 [acpid](/index.php/Acpid "Acpid")。

### CPU 時脈調整

目前的處理器可以降低時脈與電壓，以減少廢熱與電源消耗。降低廢熱不僅讓系統更安靜，同時增長硬體壽命。詳情參閱 [CPU 時脈調整](/index.php/CPU_frequency_scaling "CPU frequency scaling")。

### 筆記型電腦

[筆記型電腦分類](/index.php/Category:Laptops "Category:Laptops")下有特定型號筆電的安裝指南。若需要與筆電相關的文章與建議，則參閱[筆記型電腦](/index.php/Laptop "Laptop")。

### 暫停與休眠

參閱主文[暫停與休眠](/index.php/Suspend_and_hibernate "Suspend and hibernate")。

## 系統管理

這一節涉及管理任務與系統管理。更多資訊請參閱[系統管理分類](/index.php/Category:System_administration "Category:System administration")。

### 權限提升

全新安裝的系統只有一個超級使用者帳號，就是 root。不要一貫以 root 身分登入系統，這被廣泛認定是愚蠢且不安全的行為。使用者應該[建立](/index.php/User_Management "User Management")一個一般使用者帳號作為通常使用，只有在進行系統管理時才使用 root 帳號。[su](/index.php/Su "Su") (替換使用者) 指令可以在已登入的環境下用另一位使用者的身分 (通常為 root) 登入，至於 [sudo](/index.php/Sudo "Sudo") 指令會給予暫時的權限提升。

### 使用者與群組

GNU/Linux 利用[使用者與群組](/index.php/Users_and_groups_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Users and groups (正體中文)")達到「存取控制」；管理者可藉由調整群組成員與擁有權，以准許 / 禁止使用者和服務存取系統資源。通常您需要將帳號加入對應群組，才能存取某些週邊裝置 (如 CD/DVD 光碟機和音效硬體)。

### Windows 網路

要建立 Windows 與 Arch Linux 機器之間的網路連線，可以使用 [Samba](/index.php/Samba "Samba")；這是 SMB/CIFS 網路協定的重新實作版本。

閱讀[活動目錄整合](/index.php/Active_Directory_Integration "Active Directory Integration")，設定讓 Arch Linux 機器加入並驗證使用活動目錄 (Active Directory)。

### 系統維護

Arch 是無縫升級的系統，軟體包更迭相當快速，因此使用者得花點時間進行[系統維護](/index.php/System_maintenance "System maintenance")。[增強 Arch Linux 穩定度](/index.php/Enhance_system_stability "Enhance system stability")頁面提供了一些讓 Arch Linux 系統更為穩定的提示。

## 系統服務

這一節涉及守護程序 (daemon)。更多資訊請參閱[守護程序與系統服務分類](/index.php?title=Category:Daemons_and_system_services&action=edit&redlink=1 "Category:Daemons and system services (page does not exist)")。

### 檔案索引與查詢

多數發行版本都內帶 `locate` 指令，可快速搜索檔案。若需要這項功能，建議安裝 [mlocate](https://www.archlinux.org/packages/?name=mlocate)。安裝完成後，需執行 `updatedb` 建立檔案系統索引。

### 本地郵件遞送

預設安裝不會實現郵件同步。要將 Postfix 設定成可遞送本地端的郵件，參閱[以 Postfix進行本地郵件遞送](/index.php/Local_Mail_Delivery_with_Postfix "Local Mail Delivery with Postfix")。其他選項有 [SSMTP](/index.php/SSMTP "SSMTP"), [Msmtp](/index.php/Msmtp "Msmtp") 和 [fdm](/index.php/Fdm "Fdm")。

### 列印

[CUPS](/index.php/CUPS "CUPS") 是標準化的開源列印系統，由 Apple 開發。特定型號的印表機請參閱[印表機分類](/index.php/Category:Printers "Category:Printers")。

## X 視窗系統

[Xorg](/index.php/Xorg "Xorg") 是 X 視窗系統 11 版的公開開源實作版本。大部分需要圖形介面的使用者都會使用 Xorg。一些額外的資源可參閱 [X 伺服器分類](/index.php/Category:X_server "Category:X server")。

### 桌面環境

[Xorg](/index.php/Xorg "Xorg") 提供了建構圖形環境的基本框架，但還需要其他組件才能讓使用者體驗更加完美。諸如 [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE") 和 [Xfce](/index.php/Xfce "Xfce") 這些[桌面環境](/index.php/Desktop_environment "Desktop environment")打包了大範圍的 **X 用戶端**工具，如視窗管理員、面板、檔案管理員、虛擬終端機、文字編輯器、圖示和其他工具。完整的清單與額外資源請參閱[桌面環境分類](/index.php/Category:Desktop_environments "Category:Desktop environments")。

### 顯示驅動

預設的顯示驅動 *vesa* 能夠驅動大部分的顯示卡，不過為對應的 [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel") 或 [NVIDIA](/index.php/NVIDIA "NVIDIA") 產品安裝適當的驅動，可以增進效能並獲得額外的功能。

### 視窗管理員

一個完備的[桌面環境](/index.php/Desktop_environment "Desktop environment")提供完整一致的圖形介面，但會消耗大量的系統資源。對於要求最高效能或簡單環境的使用者，可以考慮用[視窗管理員](/index.php/Window_manager "Window manager")代替，並手動挑選額外的軟體。多數桌面環境也可以直接更換視窗管理員。[動態](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs")、[堆疊](/index.php/Category:Stacking_WMs "Category:Stacking WMs")與[平鋪](/index.php/Category:Tiling_WMs "Category:Tiling WMs")視窗管理員有它們各自處理視窗堆放的方式。