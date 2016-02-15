**翻譯狀態：** 本文章是 [FAQ](/index.php/FAQ "FAQ") 的翻譯版本。最近一次的翻譯時間：2014-01-24。點擊[本連結](https://wiki.archlinux.org/index.php?title=FAQ&diff=0&oldid=290026)查看英文頁面之後的變更。

除了下面列舉的 Q&A，也建議閱讀 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")以及 [Arch Linux 簡介](/index.php/Arch_Linux_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux (正體中文)")這兩篇文章，裡面包含了許多跟 Arch Linux 有關的知識。

## Contents

*   [1 一般](#.E4.B8.80.E8.88.AC)
    *   [1.1 Q) Arch Linux 是什麼？](#Q.29_Arch_Linux_.E6.98.AF.E4.BB.80.E9.BA.BC.EF.BC.9F)
    *   [1.2 Q) 有什麼理由會讓我想要使用 Arch？](#Q.29_.E6.9C.89.E4.BB.80.E9.BA.BC.E7.90.86.E7.94.B1.E6.9C.83.E8.AE.93.E6.88.91.E6.83.B3.E8.A6.81.E4.BD.BF.E7.94.A8_Arch.EF.BC.9F)
    *   [1.3 Q) 是什麼理由讓我對 Arch 望而卻步？](#Q.29_.E6.98.AF.E4.BB.80.E9.BA.BC.E7.90.86.E7.94.B1.E8.AE.93.E6.88.91.E5.B0.8D_Arch_.E6.9C.9B.E8.80.8C.E5.8D.BB.E6.AD.A5.EF.BC.9F)
    *   [1.4 Q) Arch 基於哪一套發行版本？](#Q.29_Arch_.E5.9F.BA.E6.96.BC.E5.93.AA.E4.B8.80.E5.A5.97.E7.99.BC.E8.A1.8C.E7.89.88.E6.9C.AC.EF.BC.9F)
    *   [1.5 Q) 我是一個徹頭徹尾的 Linux 新手，我該選擇用 Arch 嗎？](#Q.29_.E6.88.91.E6.98.AF.E4.B8.80.E5.80.8B.E5.BE.B9.E9.A0.AD.E5.BE.B9.E5.B0.BE.E7.9A.84_Linux_.E6.96.B0.E6.89.8B.EF.BC.8C.E6.88.91.E8.A9.B2.E9.81.B8.E6.93.87.E7.94.A8_Arch_.E5.97.8E.EF.BC.9F)
    *   [1.6 Q) 安裝 Arch 真的很浪費時間跟力氣，到論壇發問還被一直噹「不會看手冊啊」](#Q.29_.E5.AE.89.E8.A3.9D_Arch_.E7.9C.9F.E7.9A.84.E5.BE.88.E6.B5.AA.E8.B2.BB.E6.99.82.E9.96.93.E8.B7.9F.E5.8A.9B.E6.B0.A3.EF.BC.8C.E5.88.B0.E8.AB.96.E5.A3.87.E7.99.BC.E5.95.8F.E9.82.84.E8.A2.AB.E4.B8.80.E7.9B.B4.E5.99.B9.E3.80.8C.E4.B8.8D.E6.9C.83.E7.9C.8B.E6.89.8B.E5.86.8A.E5.95.8A.E3.80.8D)
    *   [1.7 Q) Arch 是設計作為伺服器用途的嗎？桌面用途？還是工作站用途？](#Q.29_Arch_.E6.98.AF.E8.A8.AD.E8.A8.88.E4.BD.9C.E7.82.BA.E4.BC.BA.E6.9C.8D.E5.99.A8.E7.94.A8.E9.80.94.E7.9A.84.E5.97.8E.EF.BC.9F.E6.A1.8C.E9.9D.A2.E7.94.A8.E9.80.94.EF.BC.9F.E9.82.84.E6.98.AF.E5.B7.A5.E4.BD.9C.E7.AB.99.E7.94.A8.E9.80.94.EF.BC.9F)
    *   [1.8 Q) 我真的很喜歡 Arch，可以請開發團隊實現某某功能嗎？](#Q.29_.E6.88.91.E7.9C.9F.E7.9A.84.E5.BE.88.E5.96.9C.E6.AD.A1_Arch.EF.BC.8C.E5.8F.AF.E4.BB.A5.E8.AB.8B.E9.96.8B.E7.99.BC.E5.9C.98.E9.9A.8A.E5.AF.A6.E7.8F.BE.E6.9F.90.E6.9F.90.E5.8A.9F.E8.83.BD.E5.97.8E.EF.BC.9F)
    *   [1.9 Q) 什麼時候會釋出新版本？](#Q.29_.E4.BB.80.E9.BA.BC.E6.99.82.E5.80.99.E6.9C.83.E9.87.8B.E5.87.BA.E6.96.B0.E7.89.88.E6.9C.AC.EF.BC.9F)
    *   [1.10 Q) Arch Linux 很穩定嗎？它會不會常常壞掉？](#Q.29_Arch_Linux_.E5.BE.88.E7.A9.A9.E5.AE.9A.E5.97.8E.EF.BC.9F.E5.AE.83.E6.9C.83.E4.B8.8D.E6.9C.83.E5.B8.B8.E5.B8.B8.E5.A3.9E.E6.8E.89.EF.BC.9F)
    *   [1.11 Q) 我覺得 Arch 需要更多的曝光率 (例如廣告)](#Q.29_.E6.88.91.E8.A6.BA.E5.BE.97_Arch_.E9.9C.80.E8.A6.81.E6.9B.B4.E5.A4.9A.E7.9A.84.E6.9B.9D.E5.85.89.E7.8E.87_.28.E4.BE.8B.E5.A6.82.E5.BB.A3.E5.91.8A.29)
    *   [1.12 Q) 我覺得 Arch 需要更多開發人員](#Q.29_.E6.88.91.E8.A6.BA.E5.BE.97_Arch_.E9.9C.80.E8.A6.81.E6.9B.B4.E5.A4.9A.E9.96.8B.E7.99.BC.E4.BA.BA.E5.93.A1)
    *   [1.13 Q) 我的網路連線跟其他作業系統比起來慢上不少，這是為什麼啊？](#Q.29_.E6.88.91.E7.9A.84.E7.B6.B2.E8.B7.AF.E9.80.A3.E7.B7.9A.E8.B7.9F.E5.85.B6.E4.BB.96.E4.BD.9C.E6.A5.AD.E7.B3.BB.E7.B5.B1.E6.AF.94.E8.B5.B7.E4.BE.86.E6.85.A2.E4.B8.8A.E4.B8.8D.E5.B0.91.EF.BC.8C.E9.80.99.E6.98.AF.E7.82.BA.E4.BB.80.E9.BA.BC.E5.95.8A.EF.BC.9F)
    *   [1.14 Q) Arch 怎麼把我的 RAM 都用光了？](#Q.29_Arch_.E6.80.8E.E9.BA.BC.E6.8A.8A.E6.88.91.E7.9A.84_RAM_.E9.83.BD.E7.94.A8.E5.85.89.E4.BA.86.EF.BC.9F)
    *   [1.15 Q) 我磁碟內的空間都跑到哪裡去了？](#Q.29_.E6.88.91.E7.A3.81.E7.A2.9F.E5.85.A7.E7.9A.84.E7.A9.BA.E9.96.93.E9.83.BD.E8.B7.91.E5.88.B0.E5.93.AA.E8.A3.A1.E5.8E.BB.E4.BA.86.EF.BC.9F)
*   [2 軟體包管理](#.E8.BB.9F.E9.AB.94.E5.8C.85.E7.AE.A1.E7.90.86)
    *   [2.1 Q) 我想知道某某檔案隸屬於於哪一個軟體包。](#Q.29_.E6.88.91.E6.83.B3.E7.9F.A5.E9.81.93.E6.9F.90.E6.9F.90.E6.AA.94.E6.A1.88.E9.9A.B8.E5.B1.AC.E6.96.BC.E6.96.BC.E5.93.AA.E4.B8.80.E5.80.8B.E8.BB.9F.E9.AB.94.E5.8C.85.E3.80.82)
    *   [2.2 Q) 我在某個軟體包內找到了一個錯誤。我該怎麼做呢？](#Q.29_.E6.88.91.E5.9C.A8.E6.9F.90.E5.80.8B.E8.BB.9F.E9.AB.94.E5.8C.85.E5.85.A7.E6.89.BE.E5.88.B0.E4.BA.86.E4.B8.80.E5.80.8B.E9.8C.AF.E8.AA.A4.E3.80.82.E6.88.91.E8.A9.B2.E6.80.8E.E9.BA.BC.E5.81.9A.E5.91.A2.EF.BC.9F)
    *   [2.3 Q) Arch 軟體包需要一套獨特的副檔名。".pkg.tar.gz"、".pkg.tar.xz" 太長，還會跟其他檔案搞混](#Q.29_Arch_.E8.BB.9F.E9.AB.94.E5.8C.85.E9.9C.80.E8.A6.81.E4.B8.80.E5.A5.97.E7.8D.A8.E7.89.B9.E7.9A.84.E5.89.AF.E6.AA.94.E5.90.8D.E3.80.82.22.pkg.tar.gz.22.E3.80.81.22.pkg.tar.xz.22_.E5.A4.AA.E9.95.B7.EF.BC.8C.E9.82.84.E6.9C.83.E8.B7.9F.E5.85.B6.E4.BB.96.E6.AA.94.E6.A1.88.E6.90.9E.E6.B7.B7)
    *   [2.4 Q) 我覺得 Pacman 需要一個函式庫，方便其他程式去存取軟體的相關資訊](#Q.29_.E6.88.91.E8.A6.BA.E5.BE.97_Pacman_.E9.9C.80.E8.A6.81.E4.B8.80.E5.80.8B.E5.87.BD.E5.BC.8F.E5.BA.AB.EF.BC.8C.E6.96.B9.E4.BE.BF.E5.85.B6.E4.BB.96.E7.A8.8B.E5.BC.8F.E5.8E.BB.E5.AD.98.E5.8F.96.E8.BB.9F.E9.AB.94.E7.9A.84.E7.9B.B8.E9.97.9C.E8.B3.87.E8.A8.8A)
    *   [2.5 Q) 為何 pacman 沒有一個官方的 GUI 前端？](#Q.29_.E7.82.BA.E4.BD.95_pacman_.E6.B2.92.E6.9C.89.E4.B8.80.E5.80.8B.E5.AE.98.E6.96.B9.E7.9A.84_GUI_.E5.89.8D.E7.AB.AF.EF.BC.9F)
    *   [2.6 Q) Pacman 還需要增加某某特性！](#Q.29_Pacman_.E9.82.84.E9.9C.80.E8.A6.81.E5.A2.9E.E5.8A.A0.E6.9F.90.E6.9F.90.E7.89.B9.E6.80.A7.EF.BC.81)
    *   [2.7 Q) 我覺得 Arch 需要一個穩定的分支](#Q.29_.E6.88.91.E8.A6.BA.E5.BE.97_Arch_.E9.9C.80.E8.A6.81.E4.B8.80.E5.80.8B.E7.A9.A9.E5.AE.9A.E7.9A.84.E5.88.86.E6.94.AF)
    *   [2.8 Q) Arch 底下這幾個軟體倉庫有什麼不同？](#Q.29_Arch_.E5.BA.95.E4.B8.8B.E9.80.99.E5.B9.BE.E5.80.8B.E8.BB.9F.E9.AB.94.E5.80.89.E5.BA.AB.E6.9C.89.E4.BB.80.E9.BA.BC.E4.B8.8D.E5.90.8C.EF.BC.9F)
    *   [2.9 Q) 我剛才安裝了某某軟體包。我該如何啟動它？](#Q.29_.E6.88.91.E5.89.9B.E6.89.8D.E5.AE.89.E8.A3.9D.E4.BA.86.E6.9F.90.E6.9F.90.E8.BB.9F.E9.AB.94.E5.8C.85.E3.80.82.E6.88.91.E8.A9.B2.E5.A6.82.E4.BD.95.E5.95.9F.E5.8B.95.E5.AE.83.EF.BC.9F)
    *   [2.10 Q) 怎麼官方軟體倉庫裡面的共享函式庫都只有一個版本？](#Q.29_.E6.80.8E.E9.BA.BC.E5.AE.98.E6.96.B9.E8.BB.9F.E9.AB.94.E5.80.89.E5.BA.AB.E8.A3.A1.E9.9D.A2.E7.9A.84.E5.85.B1.E4.BA.AB.E5.87.BD.E5.BC.8F.E5.BA.AB.E9.83.BD.E5.8F.AA.E6.9C.89.E4.B8.80.E5.80.8B.E7.89.88.E6.9C.AC.EF.BC.9F)
    *   [2.11 Q) 要是我執行 "pacman -Syu"，共享函式庫更新了，依靠該庫的程式卻尚未更新，那該怎麼辦？](#Q.29_.E8.A6.81.E6.98.AF.E6.88.91.E5.9F.B7.E8.A1.8C_.22pacman_-Syu.22.EF.BC.8C.E5.85.B1.E4.BA.AB.E5.87.BD.E5.BC.8F.E5.BA.AB.E6.9B.B4.E6.96.B0.E4.BA.86.EF.BC.8C.E4.BE.9D.E9.9D.A0.E8.A9.B2.E5.BA.AB.E7.9A.84.E7.A8.8B.E5.BC.8F.E5.8D.BB.E5.B0.9A.E6.9C.AA.E6.9B.B4.E6.96.B0.EF.BC.8C.E9.82.A3.E8.A9.B2.E6.80.8E.E9.BA.BC.E8.BE.A6.EF.BC.9F)
    *   [2.12 Q) 有沒有可能發生主核心升級，驅動程式卻尚未更新的狀況？](#Q.29_.E6.9C.89.E6.B2.92.E6.9C.89.E5.8F.AF.E8.83.BD.E7.99.BC.E7.94.9F.E4.B8.BB.E6.A0.B8.E5.BF.83.E5.8D.87.E7.B4.9A.EF.BC.8C.E9.A9.85.E5.8B.95.E7.A8.8B.E5.BC.8F.E5.8D.BB.E5.B0.9A.E6.9C.AA.E6.9B.B4.E6.96.B0.E7.9A.84.E7.8B.80.E6.B3.81.EF.BC.9F)
    *   [2.13 Q) Arch 有使用軟體包簽章嗎？](#Q.29_Arch_.E6.9C.89.E4.BD.BF.E7.94.A8.E8.BB.9F.E9.AB.94.E5.8C.85.E7.B0.BD.E7.AB.A0.E5.97.8E.EF.BC.9F)
    *   [2.14 Q) 升級之前需要作什麼事？](#Q.29_.E5.8D.87.E7.B4.9A.E4.B9.8B.E5.89.8D.E9.9C.80.E8.A6.81.E4.BD.9C.E4.BB.80.E9.BA.BC.E4.BA.8B.EF.BC.9F)
*   [3 安裝](#.E5.AE.89.E8.A3.9D)
    *   [3.1 Q) 我覺得 Arch 需要一個 GUI 安裝程式](#Q.29_.E6.88.91.E8.A6.BA.E5.BE.97_Arch_.E9.9C.80.E8.A6.81.E4.B8.80.E5.80.8B_GUI_.E5.AE.89.E8.A3.9D.E7.A8.8B.E5.BC.8F)
    *   [3.2 Q) 我已經安裝好 Arch，現在正在文字介面 (shell)，我該怎麼辦呢？](#Q.29_.E6.88.91.E5.B7.B2.E7.B6.93.E5.AE.89.E8.A3.9D.E5.A5.BD_Arch.EF.BC.8C.E7.8F.BE.E5.9C.A8.E6.AD.A3.E5.9C.A8.E6.96.87.E5.AD.97.E4.BB.8B.E9.9D.A2_.28shell.29.EF.BC.8C.E6.88.91.E8.A9.B2.E6.80.8E.E9.BA.BC.E8.BE.A6.E5.91.A2.EF.BC.9F)
    *   [3.3 Q) 我該使用什麼桌面環境和視窗管理員呢？](#Q.29_.E6.88.91.E8.A9.B2.E4.BD.BF.E7.94.A8.E4.BB.80.E9.BA.BC.E6.A1.8C.E9.9D.A2.E7.92.B0.E5.A2.83.E5.92.8C.E8.A6.96.E7.AA.97.E7.AE.A1.E7.90.86.E5.93.A1.E5.91.A2.EF.BC.9F)
    *   [3.4 Q) Arch 跟其他「精簡」的發行版有什麼不同？](#Q.29_Arch_.E8.B7.9F.E5.85.B6.E4.BB.96.E3.80.8C.E7.B2.BE.E7.B0.A1.E3.80.8D.E7.9A.84.E7.99.BC.E8.A1.8C.E7.89.88.E6.9C.89.E4.BB.80.E9.BA.BC.E4.B8.8D.E5.90.8C.EF.BC.9F)
*   [4 其他](#.E5.85.B6.E4.BB.96)
    *   [4.1 Q) 我一直看到 AUR 這個字彙，那到底是什麼啊？](#Q.29_.E6.88.91.E4.B8.80.E7.9B.B4.E7.9C.8B.E5.88.B0_AUR_.E9.80.99.E5.80.8B.E5.AD.97.E5.BD.99.EF.BC.8C.E9.82.A3.E5.88.B0.E5.BA.95.E6.98.AF.E4.BB.80.E9.BA.BC.E5.95.8A.EF.BC.9F)
    *   [4.2 Q) 為什麼當我要看影片時，螢幕就變成一片綠？](#Q.29_.E7.82.BA.E4.BB.80.E9.BA.BC.E7.95.B6.E6.88.91.E8.A6.81.E7.9C.8B.E5.BD.B1.E7.89.87.E6.99.82.EF.BC.8C.E8.9E.A2.E5.B9.95.E5.B0.B1.E8.AE.8A.E6.88.90.E4.B8.80.E7.89.87.E7.B6.A0.EF.BC.9F)
    *   [4.3 Q) 拼字檢查把我寫的文章都標成錯字！](#Q.29_.E6.8B.BC.E5.AD.97.E6.AA.A2.E6.9F.A5.E6.8A.8A.E6.88.91.E5.AF.AB.E7.9A.84.E6.96.87.E7.AB.A0.E9.83.BD.E6.A8.99.E6.88.90.E9.8C.AF.E5.AD.97.EF.BC.81)

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

**A)** 對於這個問題，各方有諸多見解。Arch 較偏向於經驗豐富的 Linux 使用者，但也有部分人認為：Arch 對企圖心旺盛的新手而言不失為一個好開始。假如您是一名打算使用 Arch 的新手，在此提醒您！您必須願意花上大量的時間學習一套新系統，並認清一個事實：Arch 是一套自己徒手打造的 DIY 發行版。從系統的組裝、控制到裝點，全部都要靠使用者一手包辦。有很多問題想問嗎？請試著先 Google 一下、讀完本 FAQ 後面的內容、搜尋論壇和 Arch Wiki 內豐富的文件，自己先好好研究一下問題的根源與處置方式。_這也就是為什麼我們為您創建了這些第一手的資料來源。_截至目前為止，已經有數千小時被_貢獻_於編纂這些優良的資訊。

建議閱讀：Arch Linux [新手教學](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide (正體中文)")

### Q) 安裝 Arch 真的很浪費時間跟力氣，到論壇發問還被一直噹「不會看手冊啊」

**A)** Arch 是設計給特定使用者族群使用的發行版本。也許 Arch 真的不適合您。請再參考一次[上面的需求](#Q.29_.E6.88.91.E6.98.AF.E4.B8.80.E5.80.8B.E5.BE.B9.E9.A0.AD.E5.BE.B9.E5.B0.BE.E7.9A.84_Linux_.E6.96.B0.E6.89.8B.EF.BC.8C.E6.88.91.E8.A9.B2.E9.81.B8.E6.93.87.E7.94.A8_Arch_.E5.97.8E.EF.BC.9F)吧。

### Q) Arch 是設計作為伺服器用途的嗎？桌面用途？還是工作站用途？

**A)** Arch 並非針對特定用途所設計。真的要說的話，Arch 針對的是特定的_使用者_。Arch 的目標是有能力的使用者，他們喜愛 Arch 的 DIY 性質，並活用這些特質，打造出滿足自己專有用途的系統。所以在 Arch 的目標使用群手中，它幾乎等同於萬能。許多人將 Arch 用於他們的桌面電腦和工作站。當然啦，archlinux.org 也是在 Arch 上運行的。

### Q) 我真的很喜歡 Arch，可以請開發團隊實現某某功能嗎？

**A)** 先別著急，先問問您自己是否讀過 [Arch 的設計哲學](/index.php/The_Arch_Way_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "The Arch Way (正體中文)")？您有提供功能建議/解決方式嗎？它有遵循 Arch 哲學中的「簡約」（minimalism）和「正確的設計勝過便捷」（code-correctness over convenience）嗎？歡迎您加入社群，貢獻自己的程式碼/解決方式。如果您的貢獻獲得社群和開發團隊的肯定，那就有機會被採用進 Arch。貢獻與程式碼/工具的分享，正是 Arch 社群的活力來源。

### Q) 什麼時候會釋出新版本？

**A)** Arch Linux 的釋出版本其實就只是 [core] 軟體倉庫的快照版本，通常會在每月的前半段發布。

由於 Arch 的設計為「漸進更新」，只需一個指令，每一套 Arch Linux 系統都能保持最新最尖端的狀態。很明顯地，發行新版本對 Arch 而言不是什麼了不起的大事，畢竟軟體的更新日新月異，新版本釋出不久就過期了。想取得最新的 Arch Linux 版本嗎？不必重新安裝，只要執行 `pacman -Syu` 指令，您的系統就跟新安裝的 Arch 一模一樣，也因為這個原因，新的 Arch Linux 釋出版本並不會明顯添增全新或令人興奮的功能，嶄新且迷人的功能會與軟體一同更新，並且可以由 `pacman -Syu` 指令立刻取得。

### Q) Arch Linux 很穩定嗎？它會不會常常壞掉？

**A)** 簡單一句話：它的穩定性取決於_您_。

_您_從基本的底層環境開始，組裝自己專屬的 Arch 系統，而且_您_操作著系統的每一次更新。假設有一台大而笨重、參雜過多無用軟體、工具組以及桌面環境的系統，顯然比那些更小更簡單的系統，更有可能因為某個上游的改動而遭遇到設定上的問題。Arch 的目標是有能力又積極的使用者。基本的 UNIX 知識、良好的系統維護，以及升級的實施，在系統穩定性中也佔了很大的因素。另外，Arch 的軟體包都沒有私加補丁，程式若發生問題，多數都得歸咎於上游。

因此，_使用者_必須對其個人系統的穩定性負最終的責任。是使用者自己決定何時升級、是否加入必要的變更。向社群尋求協助也能立即得到回應。Arch 和其他發行版本不同的地方在於：Arch 是一套貨真價實的 DIY 發行版本。抱怨系統毀損不僅誤導且毫無幫助，畢竟Arch 的開發者沒必要為上游的更動負起責任。

### Q) 我覺得 Arch 需要更多的曝光率 (例如廣告)

**A)** Arch 已經得到足夠的曝光率。「大」並不是 Arch Linux 的目標，而是提供一套優雅、簡約、走在研發尖端的發行版本。簡潔與正確的設計才是我們該注重的地方。健全與持久的成長，才是培養我們目標使用者群的自然之道。

### Q) 我覺得 Arch 需要更多開發人員

**A)** 大致上是的。有空的話也一起來幫忙吧！參觀我們的[論壇](https://bbs.archlinux.org)、[IRC 頻道](/index.php/IRC_channel "IRC channel")以及[郵件清單](https://mailman.archlinux.org/mailman/listinfo/)，看有什麼需要完成的地方。參加論壇的「社群貢獻」(Community Contributions) 子版面是個好的開始。

### Q) 我的網路連線跟其他作業系統比起來慢上不少，這是為什麼啊？

**A)** 您的網路有設定正確嗎？檢查一下新手指南的[網域名稱](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E5.9F.9F.E5.90.8D "Beginners' Guide (正體中文)")和[設定網路](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#.E8.A8.AD.E5.AE.9A.E7.B6.B2.E8.B7.AF "Beginners' Guide (正體中文)")。

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

**A)** 檢查一下您的系統吧。這裡有一些[不錯的工具程式](/index.php/Common_Applications#Disk_usage_display_programs "Common Applications")可以幫助您找到問題的根源。

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

**A)** 這已經在 Arch 郵件清單內討論過了。有人建議使用 `.pac` 副檔名。但根據目前所知，現在還沒有更換軟體包副檔名的打算。來聽 Arch 開發人員 Tobias Kieslich 是怎麼說的：「_Arch 軟體包單純**就是**用 gzip 壓縮過的_ [xz] _打包文件！您只要手中有任何支援 tar 的解壓縮程式，我們的軟體包都可以打開來研究、修改。另外，大多數應用程式都可以自動偵測出 Arch 軟體包的 MIME 類型。_」

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

**A)** 請參閱[官方軟體倉庫](/index.php/Official_Repositories_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Official Repositories (正體中文)")。

### Q) 我剛才安裝了某某軟體包。我該如何啟動它？

**A)** 如果您有使用桌面環境，如 [KDE](/index.php/KDE "KDE") 或 [GNOME](/index.php/GNOME "GNOME")，程式理當自動出現在選單內。若您打算從終端機執行程式，卻不知道執行檔的名稱，使用：

```
$ pacman -Qlq **軟體包名稱** | grep /usr/bin/

```

### Q) 怎麼官方軟體倉庫裡面的共享函式庫都只有一個版本？

**A)** 不少發行版本 (如 Debian) 都會將不同版本號的共享函式庫視為不同的軟體包存放：`libfoo1`, `libfoo2`, `libfoo3` 等等。對程式來說，無論編譯時是使用哪一種版本的 `libfoo`，它們都可以安裝在同一台系統內。

跟 Debian 不一樣，Arch 採用了「滾動發行」，也時常走在發行版本的最前線。前線發行版最明顯的一個特點，就是軟體倉庫內的軟體皆為最新版；對於 Arch 這樣的發行版而言，官方只會支援所有軟體的最新版本。省去支援過時軟體的力氣，軟體維護人員可以花較多時間確保新版本如實運作。在共享函式庫的上游發布新版本之後，我們便馬上將它加入軟體倉庫，所有受此函式庫影響的程式都會被重建，以搭配新版的函式庫。

### Q) 要是我執行 "pacman -Syu"，共享函式庫更新了，依靠該庫的程式卻尚未更新，那該怎麼辦？

**A)** 這種情況絕對不可能會發生。假設官方軟體倉庫內有個叫 `foobaz` 的應用程式，它需要靠新版本的共享函式庫 `libbaz` 才可成功構建，這兩者將會被一同升級。要是構建失敗，`foobaz` 會因為版本相依性不符 (如 _libbaz 1.5_)，在 `libbaz` 的升級過程中被 pacman 移除。

假如 `foobaz` 是您自行構建的 AUR 軟體包，請確認是否安裝新版本的 `libbaz`，再重新構建一遍 `foobaz`。如果還是失敗的話，請向 `foobaz` 的開發者回報錯誤。

### Q) 有沒有可能發生主核心升級，驅動程式卻尚未更新的狀況？

**A)** 不可能。主核心更新 (如 _linux 3.5.0-1_ 升至 _linux 3.6.0-1_)，所有支援的核心驅動程式也會跟著一起重建更新。但要是您的系統有安裝未支援的驅動程式 (如 [catalyst](https://aur.archlinux.org/packages/catalyst/))，當需要升級 Linux 核心時，您必須自行更新這些驅動程式，否則可能導致系統毀損。

### Q) Arch 有使用軟體包簽章嗎？

**A)** 是的。[pacman](/index.php/Pacman_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Pacman (正體中文)") 版本 4 已經實作出軟體包簽章的功能。更多資訊請參閱[軟體包簽章](/index.php/Package_signing "Package signing")。

### Q) 升級之前需要作什麼事？

**A)** 在升級 Arch Linux，按下 Enter 以前，先檢查首頁的 [Arch 新聞](https://www.archlinux.org/)、[公告清單](https://mailman.archlinux.org/mailman/listinfo/arch-announce/)，可以的話再加上[論壇](https://bbs.archlinux.org/)和[郵遞清單](https://mailman.archlinux.org/mailman/listinfo/)。任何特殊步驟都會在這些地方貼文說明。

## 安裝

### Q) 我覺得 Arch 需要一個 GUI 安裝程式

**A)** 安裝程式並未被開發人員/使用者排在高優先順序，畢竟安裝不是每天都要做的事(可以參考其他有關「無縫發行」的文章)。[安裝指南](/index.php/Installation_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Installation Guide (正體中文)")和[新手教學](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide (正體中文)")內已經更新了完整的指令安裝方式。若您還時對安裝程式有興趣的話，可以考慮使用 [Archboot](/index.php/Archboot "Archboot")。

### Q) 我已經安裝好 Arch，現在正在文字介面 (shell)，我該怎麼辦呢？

**A)** 請參閱 Arch Linux 的[新手教學](/index.php/Beginners%27_Guide_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Beginners' Guide (正體中文)")。

### Q) 我該使用什麼桌面環境和視窗管理員呢？

**A)** 既然有這麼多種可以使用，就用最符合你需求的那一套吧。可以參考[桌面環境](/index.php/Desktop_environment "Desktop environment")、[視窗管理員](/index.php/Window_manager "Window manager")這些文章。

### Q) Arch 跟其他「精簡」的發行版有什麼不同？

**A)** 某些發行版會提供最小安裝方式，這跟 Arch 的安裝手法有些相似。不過要注意的是：

1.  Arch _打從藍圖起_就被設計為一個輕量、小型的基本環境。
2.  _唯一_安裝 Arch 的方式就是從基本架構開始堆砌。
3.  從基本系統到整個發行版本，Arch 都繼承了 K.I.S.S. 的設計理念，讓 Arch 能獨到的適合它的目標使用者群。
4.  安裝服務和軟體時，需要手冊和互動式的使用者設定。不像其他發行版本會自動設定服務、啟動行為，Arch 的哲學注重給予使用者特權，讓他們能夠放手一搏、自行處理。
5.  Arch 軟體包的設計力求精簡。使用者在安裝程式時，只會簡單告知有_選用_相依程式的存在，不會自動安裝它們，這樣才能讓 Arch 變的輕量點。
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