**翻譯狀態：** 本文章是 [FAQ](/index.php/FAQ "FAQ") 的翻譯版本。最近一次的翻譯時間：2014-01-24。點擊[本連結](https://wiki.archlinux.org/index.php?title=FAQ&diff=0&oldid=290026)查看英文頁面之後的變更。

除了下面列舉的 Q&A，也建議閱讀 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")以及 [Arch Linux 簡介](/index.php/Arch_Linux_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux (正體中文)")這兩篇文章，裡面包含了許多跟 Arch Linux 有關的知識。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 一般](#一般)
    *   [1.1 Q) Arch Linux 是什麼？](#Q)_Arch_Linux_是什麼？)
    *   [1.2 Q) 有什麼理由會讓我想要使用 Arch？](#Q)_有什麼理由會讓我想要使用_Arch？)
    *   [1.3 Q) 是什麼理由讓我對 Arch 望而卻步？](#Q)_是什麼理由讓我對_Arch_望而卻步？)
    *   [1.4 Q) Arch 基於哪一套發行版本？](#Q)_Arch_基於哪一套發行版本？)
    *   [1.5 Q) 我是一個徹頭徹尾的 Linux 新手，我該選擇用 Arch 嗎？](#Q)_我是一個徹頭徹尾的_Linux_新手，我該選擇用_Arch_嗎？)
    *   [1.6 Q) 安裝 Arch 真的很浪費時間跟力氣，到論壇發問還被一直噹「不會看手冊啊」](#Q)_安裝_Arch_真的很浪費時間跟力氣，到論壇發問還被一直噹「不會看手冊啊」)
    *   [1.7 Q) Arch 是設計作為伺服器用途的嗎？桌面用途？還是工作站用途？](#Q)_Arch_是設計作為伺服器用途的嗎？桌面用途？還是工作站用途？)
    *   [1.8 Q) 我真的很喜歡 Arch，可以請開發團隊實現某某功能嗎？](#Q)_我真的很喜歡_Arch，可以請開發團隊實現某某功能嗎？)
    *   [1.9 Q) 什麼時候會釋出新版本？](#Q)_什麼時候會釋出新版本？)
    *   [1.10 Q) Arch Linux 很穩定嗎？它會不會常常壞掉？](#Q)_Arch_Linux_很穩定嗎？它會不會常常壞掉？)
    *   [1.11 Q) 我覺得 Arch 需要更多的曝光率 (例如廣告)](#Q)_我覺得_Arch_需要更多的曝光率_(例如廣告))
    *   [1.12 Q) 我覺得 Arch 需要更多開發人員](#Q)_我覺得_Arch_需要更多開發人員)
    *   [1.13 Q) 我的網路連線跟其他作業系統比起來慢上不少，這是為什麼啊？](#Q)_我的網路連線跟其他作業系統比起來慢上不少，這是為什麼啊？)
    *   [1.14 Q) Arch 怎麼把我的 RAM 都用光了？](#Q)_Arch_怎麼把我的_RAM_都用光了？)
    *   [1.15 Q) 我磁碟內的空間都跑到哪裡去了？](#Q)_我磁碟內的空間都跑到哪裡去了？)
*   [2 軟體包管理](#軟體包管理)
    *   [2.1 Q) 我想知道某某檔案隸屬於於哪一個軟體包。](#Q)_我想知道某某檔案隸屬於於哪一個軟體包。)
    *   [2.2 Q) 我在某個軟體包內找到了一個錯誤。我該怎麼做呢？](#Q)_我在某個軟體包內找到了一個錯誤。我該怎麼做呢？)
    *   [2.3 Q) Arch 軟體包需要一套獨特的副檔名。".pkg.tar.gz"、".pkg.tar.xz" 太長，還會跟其他檔案搞混](#Q)_Arch_軟體包需要一套獨特的副檔名。".pkg.tar.gz"、".pkg.tar.xz"_太長，還會跟其他檔案搞混)
    *   [2.4 Q) 我覺得 Pacman 需要一個函式庫，方便其他程式去存取軟體的相關資訊](#Q)_我覺得_Pacman_需要一個函式庫，方便其他程式去存取軟體的相關資訊)
    *   [2.5 Q) 為何 pacman 沒有一個官方的 GUI 前端？](#Q)_為何_pacman_沒有一個官方的_GUI_前端？)
    *   [2.6 Q) Pacman 還需要增加某某特性！](#Q)_Pacman_還需要增加某某特性！)
    *   [2.7 Q) 我覺得 Arch 需要一個穩定的分支](#Q)_我覺得_Arch_需要一個穩定的分支)
    *   [2.8 Q) Arch 底下這幾個軟體倉庫有什麼不同？](#Q)_Arch_底下這幾個軟體倉庫有什麼不同？)
    *   [2.9 Q) 我剛才安裝了某某軟體包。我該如何啟動它？](#Q)_我剛才安裝了某某軟體包。我該如何啟動它？)
    *   [2.10 Q) 怎麼官方軟體倉庫裡面的共享函式庫都只有一個版本？](#Q)_怎麼官方軟體倉庫裡面的共享函式庫都只有一個版本？)
    *   [2.11 Q) 要是我執行 "pacman -Syu"，共享函式庫更新了，依靠該庫的程式卻尚未更新，那該怎麼辦？](#Q)_要是我執行_"pacman_-Syu"，共享函式庫更新了，依靠該庫的程式卻尚未更新，那該怎麼辦？)
    *   [2.12 Q) 有沒有可能發生主核心升級，驅動程式卻尚未更新的狀況？](#Q)_有沒有可能發生主核心升級，驅動程式卻尚未更新的狀況？)
    *   [2.13 Q) Arch 有使用軟體包簽章嗎？](#Q)_Arch_有使用軟體包簽章嗎？)
    *   [2.14 Q) 升級之前需要作什麼事？](#Q)_升級之前需要作什麼事？)
*   [3 安裝](#安裝)
    *   [3.1 Q) 我覺得 Arch 需要一個 GUI 安裝程式](#Q)_我覺得_Arch_需要一個_GUI_安裝程式)
    *   [3.2 Q) 我已經安裝好 Arch，現在正在文字介面 (shell)，我該怎麼辦呢？](#Q)_我已經安裝好_Arch，現在正在文字介面_(shell)，我該怎麼辦呢？)
    *   [3.3 Q) 我該使用什麼桌面環境和視窗管理員呢？](#Q)_我該使用什麼桌面環境和視窗管理員呢？)
    *   [3.4 Q) Arch 跟其他「精簡」的發行版有什麼不同？](#Q)_Arch_跟其他「精簡」的發行版有什麼不同？)
*   [4 其他](#其他)
    *   [4.1 Q) 我一直看到 AUR 這個字彙，那到底是什麼啊？](#Q)_我一直看到_AUR_這個字彙，那到底是什麼啊？)
    *   [4.2 Q) 為什麼當我要看影片時，螢幕就變成一片綠？](#Q)_為什麼當我要看影片時，螢幕就變成一片綠？)
    *   [4.3 Q) 拼字檢查把我寫的文章都標成錯字！](#Q)_拼字檢查把我寫的文章都標成錯字！)

## 一般

### Q) Arch Linux 是什麼？

**A)** 請參閱 [Arch Linux 簡介](/index.php/Arch_Linux_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux (正體中文)")。

### Q) 有什麼理由會讓我想要使用 Arch？

**A)** 在讀過 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")，了解箇中道理之後，如果您願意展開心胸了解 DIY「手把手」的作風，並要求/希望一個簡單、優雅、高度自訂、尖端且通用的 GNU/Linux 發行版本的話，您應該會喜歡上 Arch。

### Q) 是什麼理由讓我對 Arch 望而卻步？

**A)** 若以下有任何理由適用於您，那您可能跟 Arch 八字不合：

*   讀過 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")，但不認同其中道理。
*   沒有能力/時間/需求去使用一套「DIY」的 GNU/Linux 發行版本。
*   需要 x86_64 與 i686 以外的架構支援。
*   堅持使用**只**提供 GNU 自由軟體的發行版本。
*   認為一個作業系統要能夠自我設定、開箱即用、預先包裝完整的軟體與桌面環境，才夠格叫作業系統。
*   不想要一個走向最尖端且採用漸進式發行的 GNU/Linux 發行版本。
*   很滿意自己現在使用的 OS。
*   想要一個主攻其他使用者群的 OS。
*   還沒瘋到要去使用 Allan 開發的 OS。(?)

### Q) Arch 基於哪一套發行版本？

**A)** Arch 並非其他任何 GNU/Linux 發行版本的分支。Arch 是個獨立發展、從頭開始打造的 GNU/Linux 發行版本。Arch 的作者 Judd Vinet 在創造 Arch 之前使用的是 Crux，那是一個又棒又簡約的發行版本，作者是 Per Lidén。Judd Vinet 很欣賞 Crux，加上被 Crux 的概念所啟發，就開始一磚一瓦打造出 Arch，用 C 語言撰寫出 pacman。

### Q) 我是一個徹頭徹尾的 Linux 新手，我該選擇用 Arch 嗎？

**A)** 對於這個問題，各方有諸多見解。Arch 較偏向於經驗豐富的 Linux 使用者，但也有部分人認為：Arch 對企圖心旺盛的新手而言不失為一個好開始。假如您是一名打算使用 Arch 的新手，在此提醒您！您必須願意花上大量的時間學習一套新系統，並認清一個事實：Arch 是一套自己徒手打造的 DIY 發行版。從系統的組裝、控制到裝點，全部都要靠使用者一手包辦。有很多問題想問嗎？請試著先 Google 一下、讀完本 FAQ 後面的內容、搜尋論壇和 Arch Wiki 內豐富的文件，自己先好好研究一下問題的根源與處置方式。*這也就是為什麼我們為您創建了這些第一手的資料來源。*截至目前為止，已經有數千小時被*貢獻*於編纂這些優良的資訊。

建議閱讀：Arch Linux [新手教學](/index.php/Beginners%27_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' guide (正體中文)")

### Q) 安裝 Arch 真的很浪費時間跟力氣，到論壇發問還被一直噹「不會看手冊啊」

**A)** Arch 是設計給特定使用者族群使用的發行版本。也許 Arch 真的不適合您。請再參考一次[上面的需求](#Q)_我是一個徹頭徹尾的_Linux_新手，我該選擇用_Arch_嗎？)吧。

### Q) Arch 是設計作為伺服器用途的嗎？桌面用途？還是工作站用途？

**A)** Arch 並非針對特定用途所設計。真的要說的話，Arch 針對的是特定的*使用者*。Arch 的目標是有能力的使用者，他們喜愛 Arch 的 DIY 性質，並活用這些特質，打造出滿足自己專有用途的系統。所以在 Arch 的目標使用群手中，它幾乎等同於萬能。許多人將 Arch 用於他們的桌面電腦和工作站。當然啦，archlinux.org 也是在 Arch 上運行的。

### Q) 我真的很喜歡 Arch，可以請開發團隊實現某某功能嗎？

**A)** 先別著急，先問問您自己是否讀過 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")？您有提供功能建議/解決方式嗎？它有遵循 Arch 哲學中的「簡約」（minimalism）和「正確的設計勝過便捷」（code-correctness over convenience）嗎？歡迎您加入社群，貢獻自己的程式碼/解決方式。如果您的貢獻獲得社群和開發團隊的肯定，那就有機會被採用進 Arch。貢獻與程式碼/工具的分享，正是 Arch 社群的活力來源。

### Q) 什麼時候會釋出新版本？

**A)** Arch Linux 的釋出版本其實就只是 [core] 軟體倉庫的快照版本，通常會在每月的前半段發布。

由於 Arch 的設計為「漸進更新」，只需一個指令，每一套 Arch Linux 系統都能保持最新最尖端的狀態。很明顯地，發行新版本對 Arch 而言不是什麼了不起的大事，畢竟軟體的更新日新月異，新版本釋出不久就過期了。想取得最新的 Arch Linux 版本嗎？不必重新安裝，只要執行 `pacman -Syu` 指令，您的系統就跟新安裝的 Arch 一模一樣，也因為這個原因，新的 Arch Linux 釋出版本並不會明顯添增全新或令人興奮的功能，嶄新且迷人的功能會與軟體一同更新，並且可以由 `pacman -Syu` 指令立刻取得。

### Q) Arch Linux 很穩定嗎？它會不會常常壞掉？

**A)** 簡單一句話：它的穩定性取決於*您*。

*您*從基本的底層環境開始，組裝自己專屬的 Arch 系統，而且*您*操作著系統的每一次更新。假設有一台大而笨重、參雜過多無用軟體、工具組以及桌面環境的系統，顯然比那些更小更簡單的系統，更有可能因為某個上游的改動而遭遇到設定上的問題。Arch 的目標是有能力又積極的使用者。基本的 UNIX 知識、良好的系統維護，以及升級的實施，在系統穩定性中也佔了很大的因素。另外，Arch 的軟體包都沒有私加補丁，程式若發生問題，多數都得歸咎於上游。

因此，*使用者*必須對其個人系統的穩定性負最終的責任。是使用者自己決定何時升級、是否加入必要的變更。向社群尋求協助也能立即得到回應。Arch 和其他發行版本不同的地方在於：Arch 是一套貨真價實的 DIY 發行版本。抱怨系統毀損不僅誤導且毫無幫助，畢竟Arch 的開發者沒必要為上游的更動負起責任。

### Q) 我覺得 Arch 需要更多的曝光率 (例如廣告)

**A)** Arch 已經得到足夠的曝光率。「大」並不是 Arch Linux 的目標，而是提供一套優雅、簡約、走在研發尖端的發行版本。簡潔與正確的設計才是我們該注重的地方。健全與持久的成長，才是培養我們目標使用者群的自然之道。

### Q) 我覺得 Arch 需要更多開發人員

**A)** 大致上是的。有空的話也一起來幫忙吧！參觀我們的[論壇](https://bbs.archlinux.org)、[IRC 頻道](/index.php/IRC_channel "IRC channel")以及[郵件清單](https://mailman.archlinux.org/mailman/listinfo/)，看有什麼需要完成的地方。參加論壇的「社群貢獻」(Community Contributions) 子版面是個好的開始。

### Q) 我的網路連線跟其他作業系統比起來慢上不少，這是為什麼啊？

**A)** 您的網路有設定正確嗎？檢查一下新手指南的[網域名稱](/index.php/Beginners%27_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#域名 "Beginners' guide (正體中文)")和[設定網路](/index.php/Beginners%27_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#配置網路 "Beginners' guide (正體中文)")。

要注意的是 Arch Linux 並沒有啟用[流量整形](https://en.wikipedia.org/wiki/Traffic_shaping "wikipedia:Traffic shaping")功能。因此，只要有一個程式(無論是 P2P 或基本的主從式連線)因為某些原因佔滿了您的網路連線頻寬，您的網路就會堵塞，拖慢其他程式的執行，甚至出現逾時錯誤。解決方案之一是使用[防火牆](/index.php/Firewalls "Firewalls")(Shorewall 或 Vuurmuur)；[iproute2](https://www.archlinux.org/packages/?name=iproute2) 也有一些現成腳本(如[這份 Wondershaper 的衍生](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos))也可以幫忙為網路層塑身。

### Q) Arch 怎麼把我的 RAM 都用光了？

**A)** 基本上 RAM 未使用就等於浪費了 RAM。

很多新手會注意到，Linux 核心處理記憶體的方式跟他們以往的認知有很大的不同。既然從 RAM 存取資料比儲存裝置快上不少，Linux 核心乾脆把最近常存取的資料做成快取丟進記憶體。只有在系統快用光記憶體，新的資料又要進來時才會被消除。

造成這種困擾的罪魁禍首也許就是這個 `free` 指令：

 `$ free -m` 
```
             total       used       free     shared    buffers     cached
Mem:          1009        741        267          0        104        359
-/+ buffers/cache:        278        731
Swap:         1537          0       1537
```

重點在 `-/+ buffers/cache:` 這一行：它記錄了實際上「正在使用」的記憶體量，以及「可供使用」的記憶體量(並非「未使用」)。

在上面的例子裡，這一台總 RAM 為 1G 的筆記型電腦，看似已經花掉 741M 的 RAM，恐怕再開個網頁瀏覽器、幾台終端機就全部用光光了！但是，只要檢查剛剛強調的那一行，「正在使用中」的 RAM 量其實只有 278M，事實上還有 731M 「可用空間」給新的資料。其中有 104M 當作資料緩衝區、359M 用來存放快取資料，這兩者都可以在有需求時馬上清空。全部的記憶體空間只有 267M 是「完全」沒有任何資料存放的。

這一切都是為了更好的性能！

若上述的資訊激起了您的好奇心，歡迎參考[這篇文章](http://www.linuxjournal.com/article/2770)！在這也提供一個專門解釋該現象的網站：[Help! Linux ate my RAM!](http://www.linuxatemyram.com)

### Q) 我磁碟內的空間都跑到哪裡去了？

**A)** 檢查一下您的系統吧。這裡有一些[不錯的工具程式](/index.php/Common_Applications#Disk_usage_display "Common Applications")可以幫助您找到問題的根源。

## 軟體包管理

### Q) 我想知道某某檔案隸屬於於哪一個軟體包。

**A)** 您可以用 [pkgfile](/index.php/Pkgfile "Pkgfile") 尋找。

如以下範例：

```
$ pkgfile [檔案名稱]

```

### Q) 我在某個軟體包內找到了一個錯誤。我該怎麼做呢？

**A)** 首先，您需要弄明白這個錯誤是不是 Arch 團隊可以修復的。有時候問題並不來自 Arch，例如 Firefox 當掉了，問題可能出自於開發它的 Mozilla 團隊，像這種的都叫做「上游問題」。若您確定這是 Arch 的問題，可以嘗試以下的步驟：

1.  在論壇搜尋一下，看是否已經有人注意到它。
2.  發一篇內含詳細資訊的[臭蟲報告](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")到 [https://bugs.archlinux.org](https://bugs.archlinux.org) 。
3.  若您願意的話，在論壇上發一篇詳細的問題報告文，並註明這個問題**已被回報過**。這樣可避免其他人也回報了相同的錯誤。

### Q) Arch 軟體包需要一套獨特的副檔名。".pkg.tar.gz"、".pkg.tar.xz" 太長，還會跟其他檔案搞混

**A)** 這已經在 Arch 郵件清單內討論過了。有人建議使用 `.pac` 副檔名。但根據目前所知，現在還沒有更換軟體包副檔名的打算。來聽 Arch 開發人員 Tobias Kieslich 是怎麼說的：「*Arch 軟體包單純**就是**用 gzip 壓縮過的* [xz] *打包文件！您只要手中有任何支援 tar 的解壓縮程式，我們的軟體包都可以打開來研究、修改。另外，大多數應用程式都可以自動偵測出 Arch 軟體包的 MIME 類型。*」

### Q) 我覺得 Pacman 需要一個函式庫，方便其他程式去存取軟體的相關資訊

**A)** 自版本 3.0.0 起，pacman 已經成為 libalpm (Arch Linux 軟體管理函式庫) 的前端介面。libalpm 函式庫可以接受其他的前端，也包含 GUI 前端。

### Q) 為何 pacman 沒有一個官方的 GUI 前端？

**A)** 若您已經讀過 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")和 [Arch Linux 簡介](/index.php/Arch_Linux_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux (正體中文)")，就會知道 Arch 的開發團隊基本上不會提供 GUI 這種東西。但您也可以試試其他 Arch 玩家開發的工具。請參閱 [Pacman GUI 前端](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends")列舉的 GUI 工具。

### Q) Pacman 還需要增加某某特性！

**A)** 讀過 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")和 [Arch Linux 簡介](/index.php/Arch_Linux_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux (正體中文)")了嗎？Arch 的哲學是「保持簡潔」。若您覺得這個點子沒有跟「簡潔」相違背，且值得推廣的話，歡迎到我們的[論壇](https://bbs.archlinux.org/)討論。也歡迎您參觀一下[問題回報區](https://bugs.archlinux.org)；這裡也是提出新功能的重要據點。

但言歸正傳，要讓 pacman、Arch Linux 增加新功能，最好的辦法還是自己動手寫個補丁。您的貢獻有可能不會被官方接受，但說不定會有不少好心人士幫您測試、修整喔！

### Q) 我覺得 Arch 需要一個穩定的分支

**A)** 請參閱 [ArchServer](http://www.archserver.org/)。

### Q) Arch 底下這幾個軟體倉庫有什麼不同？

**A)** 請參閱[官方軟體倉庫](/index.php/Official_repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official repositories (正體中文)")。

### Q) 我剛才安裝了某某軟體包。我該如何啟動它？

**A)** 如果您有使用桌面環境，如 [KDE](/index.php/KDE "KDE") 或 [GNOME](/index.php/GNOME "GNOME")，程式理當自動出現在選單內。若您打算從終端機執行程式，卻不知道執行檔的名稱，使用：

```
$ pacman -Qlq **軟體包名稱** | grep /usr/bin/

```

### Q) 怎麼官方軟體倉庫裡面的共享函式庫都只有一個版本？

**A)** 不少發行版本 (如 Debian) 都會將不同版本號的共享函式庫視為不同的軟體包存放：`libfoo1`, `libfoo2`, `libfoo3` 等等。對程式來說，無論編譯時是使用哪一種版本的 `libfoo`，它們都可以安裝在同一台系統內。

跟 Debian 不一樣，Arch 採用了「滾動發行」，也時常走在發行版本的最前線。前線發行版最明顯的一個特點，就是軟體倉庫內的軟體皆為最新版；對於 Arch 這樣的發行版而言，官方只會支援所有軟體的最新版本。省去支援過時軟體的力氣，軟體維護人員可以花較多時間確保新版本如實運作。在共享函式庫的上游發布新版本之後，我們便馬上將它加入軟體倉庫，所有受此函式庫影響的程式都會被重建，以搭配新版的函式庫。

### Q) 要是我執行 "pacman -Syu"，共享函式庫更新了，依靠該庫的程式卻尚未更新，那該怎麼辦？

**A)** 這種情況絕對不可能會發生。假設官方軟體倉庫內有個叫 `foobaz` 的應用程式，它需要靠新版本的共享函式庫 `libbaz` 才可成功構建，這兩者將會被一同升級。要是構建失敗，`foobaz` 會因為版本相依性不符 (如 *libbaz 1.5*)，在 `libbaz` 的升級過程中被 pacman 移除。

假如 `foobaz` 是您自行構建的 AUR 軟體包，請確認是否安裝新版本的 `libbaz`，再重新構建一遍 `foobaz`。如果還是失敗的話，請向 `foobaz` 的開發者回報錯誤。

### Q) 有沒有可能發生主核心升級，驅動程式卻尚未更新的狀況？

**A)** 不可能。主核心更新 (如 *linux 3.5.0-1* 升至 *linux 3.6.0-1*)，所有支援的核心驅動程式也會跟著一起重建更新。但要是您的系統有安裝未支援的驅動程式 (如 [catalyst](https://aur.archlinux.org/packages/catalyst/))，當需要升級 Linux 核心時，您必須自行更新這些驅動程式，否則可能導致系統毀損。

### Q) Arch 有使用軟體包簽章嗎？

**A)** 是的。[pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 版本 4 已經實作出軟體包簽章的功能。更多資訊請參閱[軟體包簽章](/index.php/Package_signing "Package signing")。

### Q) 升級之前需要作什麼事？

**A)** 在升級 Arch Linux，按下 Enter 以前，先檢查首頁的 [Arch 新聞](https://www.archlinux.org/)、[公告清單](https://mailman.archlinux.org/mailman/listinfo/arch-announce/)，可以的話再加上[論壇](https://bbs.archlinux.org/)和[郵遞清單](https://mailman.archlinux.org/mailman/listinfo/)。任何特殊步驟都會在這些地方貼文說明。

## 安裝

### Q) 我覺得 Arch 需要一個 GUI 安裝程式

**A)** 安裝程式並未被開發人員/使用者排在高優先順序，畢竟安裝不是每天都要做的事(可以參考其他有關「無縫發行」的文章)。[安裝指南](/index.php/Installation_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Installation guide (正體中文)")和[新手教學](/index.php/Beginners%27_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' guide (正體中文)")內已經更新了完整的指令安裝方式。若您還時對安裝程式有興趣的話，

### Q) 我已經安裝好 Arch，現在正在文字介面 (shell)，我該怎麼辦呢？

**A)** 請參閱 Arch Linux 的[新手教學](/index.php/Beginners%27_guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' guide (正體中文)")。

### Q) 我該使用什麼桌面環境和視窗管理員呢？

**A)** 既然有這麼多種可以使用，就用最符合你需求的那一套吧。可以參考[桌面環境](/index.php/Desktop_environment "Desktop environment")、[視窗管理員](/index.php/Window_manager "Window manager")這些文章。

### Q) Arch 跟其他「精簡」的發行版有什麼不同？

**A)** 某些發行版會提供最小安裝方式，這跟 Arch 的安裝手法有些相似。不過要注意的是：

1.  Arch *打從藍圖起*就被設計為一個輕量、小型的基本環境。
2.  *唯一*安裝 Arch 的方式就是從基本架構開始堆砌。
3.  從基本系統到整個發行版本，Arch 都繼承了 K.I.S.S. 的設計理念，讓 Arch 能獨到的適合它的目標使用者群。
4.  安裝服務和軟體時，需要手冊和互動式的使用者設定。不像其他發行版本會自動設定服務、啟動行為，Arch 的哲學注重給予使用者特權，讓他們能夠放手一搏、自行處理。
5.  Arch 軟體包的設計力求精簡。使用者在安裝程式時，只會簡單告知有*選用*相依程式的存在，不會自動安裝它們，這樣才能讓 Arch 變的輕量點。
6.  Arch 提供了優良、完整的文件，幫助使用者打造自己的系統。

## 其他

### Q) 我一直看到 AUR 這個字彙，那到底是什麼啊？

**A)** 請參閱 [Arch 使用者倉庫#FAQ](/index.php/Arch_User_Repository_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#FAQ "Arch User Repository (正體中文)")。

### Q) 為什麼當我要看影片時，螢幕就變成一片綠？

**A)** 您的色深設定錯誤了。舉例來說，它應該要是 24 而不是 16。

### Q) 拼字檢查把我寫的文章都標成錯字！

**A)** 您是否有安裝 [aspell](https://www.archlinux.org/packages/?name=aspell) 字典？用 `pacman -Ss aspell` 查看是否有您適用的語言字典可供下載。

要是安裝字典檔沒辦法解決問題，那這很可能是 `enchant` 造成。檢查已知的字典檔案：

 `$ aspell dicts` 
```
en
en_GB
...etc
```

若有列出您所要的語言字典，就把它加進 `/usr/share/enchant/enchant.ordering`。根據以上的範例，那將會是：

```
en_GB:aspell

```