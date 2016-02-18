**Sup** 是一套爲了擁有大量郵件使用者所開發，嶄新且強大的郵件客戶端程式。您可以將它想成 Mutt 和 Gmail 的混合體，擁有非常快速地操作和搜尋，標籤，自動通訊錄管理，支援大量帳號，以及更多功能。

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
*   [2 設定](#.E8.A8.AD.E5.AE.9A)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
*   [4 備份和復原](#.E5.82.99.E4.BB.BD.E5.92.8C.E5.BE.A9.E5.8E.9F)
*   [5 按鍵綁定列表](#.E6.8C.89.E9.8D.B5.E7.B6.81.E5.AE.9A.E5.88.97.E8.A1.A8)
    *   [5.1 inbox-mode 下的按鍵綁定](#inbox-mode_.E4.B8.8B.E7.9A.84.E6.8C.89.E9.8D.B5.E7.B6.81.E5.AE.9A)
    *   [5.2 thread-index-mode 下的按鍵綁定](#thread-index-mode_.E4.B8.8B.E7.9A.84.E6.8C.89.E9.8D.B5.E7.B6.81.E5.AE.9A)
    *   [5.3 thread-view-mode 下的按鍵綁定](#thread-view-mode_.E4.B8.8B.E7.9A.84.E6.8C.89.E9.8D.B5.E7.B6.81.E5.AE.9A)
    *   [5.4 contact-list-mode 下的按鍵綁定](#contact-list-mode_.E4.B8.8B.E7.9A.84.E6.8C.89.E9.8D.B5.E7.B6.81.E5.AE.9A)
    *   [5.5 line-cursor-mode 下的按鍵綁定](#line-cursor-mode_.E4.B8.8B.E7.9A.84.E6.8C.89.E9.8D.B5.E7.B6.81.E5.AE.9A)
    *   [5.6 scroll-mode 下的按鍵綁定](#scroll-mode_.E4.B8.8B.E7.9A.84.E6.8C.89.E9.8D.B5.E7.B6.81.E5.AE.9A)
    *   [5.7 全域按鍵綁定](#.E5.85.A8.E5.9F.9F.E6.8C.89.E9.8D.B5.E7.B6.81.E5.AE.9A)
*   [6 疑難排解](#.E7.96.91.E9.9B.A3.E6.8E.92.E8.A7.A3)
    *   [6.1 因爲 Illegal instruction (core dumped) 而當掉](#.E5.9B.A0.E7.88.B2_Illegal_instruction_.28core_dumped.29_.E8.80.8C.E7.95.B6.E6.8E.89)
*   [7 另請參閱](#.E5.8F.A6.E8.AB.8B.E5.8F.83.E9.96.B1)

## 安裝

從 [AUR](/index.php/AUR_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "AUR (正體中文)") 安裝 [sup-git](https://aur.archlinux.org/packages/sup-git)。 不過開發團隊建議您用以下方式安裝：

```
$ gem install sup

```

好讓您直接從開發團隊那兒取得最新版本。

## 設定

Sup 附帶一款名爲 `sup-config` 的簡便設定工具。要使用它，請在終端機內執行它然後完成下面列出的幾項步驟：

1.  輸入您的全名。
2.  輸入您的主要電子郵件信箱，以及任何額外的電子郵件信箱。
3.  輸入您簽名檔的位置，如果您擁有的話。
4.  輸入您要用來撰寫新郵件的編輯器，以及任何您該傳入的參數。
5.  新增您郵件的來源，包括：
    1.  mbox 檔案
    2.  maildir 資料夾

支援遠端來源 (POP3, IMAP, IMAPS, 和 mbox + ssh) 的功能已經在 0.12 版釋出時移除。

Sup 目前專注於 MUA (mail user agent) 之功能且不自行處理下載郵件的工作。您可以使用像是 offlineimap, fetchmail, 和 rsync 等工具來將電子郵件傳送到本機系統的 mbox 或 maildir 資料夾。

[sup wiki 內的示範](https://github.com/sup-heliotrope/sup/wiki/Complete-gmail-configuration) 簡介了如何使用 offlineimap 設定 gmail+imap 來源。[Mutt#POP3](/index.php/Mutt_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87)#POP3 "Mutt (正體中文)") 子章節介紹一些額外的郵件傳送方法。

在新增好電子郵件來源後，`sup-config` 會執行 `sup-sync` 指令來匯入郵件到您的信箱內。

## 使用

執行 `sup` 指令來開啓 Sup 郵件客戶端程式。該程式應該會顯示由 `sup-config` 匯入的訊息。

對新使用者來說最該記得的按鍵就是 `?` 按鍵。在任何時間點它都會顯示所有的鍵盤指令，提示新使用者該如何導覽程式。

使用箭頭鍵或是 `j` 和 `k` 鍵巡覽討論串 (`Shift+j` 和 `Shift+k` 的功能如同 Page Up 和 Page Down 鍵)。按下 Tab 鍵，則能在有新訊息的討論串中快速穿梭。Sup 預設並不會讀入所有討論串；按下 `Shift+m` 將讀取更多討論串 (更多訊息將被自動讀取直到視窗被填滿)。

選擇欲檢視的討論串然後按下 `Enter` 鍵即可檢視它。在檢視討論串時，如果想要展開或摺疊某一訊息，請選擇該訊息然後按下 `Enter` 鍵。按下 `Shift+n` 將只展開新訊息 (同預設畫面) 或 `Shift+e` 切換所有訊息的狀態。按下 `o` 將顯示或隱藏部分訊息內容 (像是簽名檔)。

按下 `n` 和 `p` 鍵巡覽討論串內的訊息。按下 `h` 鍵顯示訊息的標頭。

按下 `b` 鍵循環切換緩衝，或者按下 `;` 鍵檢視已開啓緩衝的清單。按下 `x` 鍵抹殺某個緩衝。

按下 `a` 鍵封存討論串。這會將該討論串從 inbox 內隱藏直到其他人回覆它，到時候它就會重新出現。按下 `&` 鍵抹殺討論串。這等同於 Gmail 中的 "靜音" 功能，即使有人回覆該討論串它依然會被隱藏。該討論串將永遠不會出現在 inbox 內，不過依然能在搜尋結果找到它。

按下 `*` 鍵替討論串標記星號。按下 `Shift+s` 鍵將討論串標記爲垃圾訊息。Sup 並沒有任何內建的垃圾訊息分類器；要做到這個功能，可以考慮像是 [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) 之類的程式。

按下 `t` 鍵標記討論串。按下 `l` 鍵替討論串內的訊息加上標籤。按下 `Shift+l` 鍵搜尋標籤。輸入欲搜尋的標籤後按下 `Enter` 鍵或是直接按下 `Enter` 鍵來列出所有標籤。按下 `\` 鍵將執行全文字搜尋。

按下 `Shift+c` 鍵來檢視聯絡人清單。要對清單中的人寄送電子郵件，選擇他或她的姓名然後按下 `Enter` 鍵。

## 備份和復原

備份電子郵件非常重要。爲了保證您不會弄丟任何東西，第一要先備份來源，像是 mbox 檔案和 maildir 目錄，然後執行：

```
$ sup-dump > *檔案名稱*

```

這將會備份所有訊息狀態到文字檔案內。要從文字檔案內復原您的訊息狀態，只要執行：

```
$ sup-sync [<來源>+] --restored --restore *檔案名稱*

```

謹記，上面的指令只會備份和復原訊息狀態。訊息本身需要另行備份。

## 按鍵綁定列表

### inbox-mode 下的按鍵綁定

```
a：封存討論串 (從 inbox 中移除)
A：封存討論串 (從 inbox 中移除) 且標記爲已讀

```

### thread-index-mode 下的按鍵綁定

```
   M：再讀取 20 份討論串
  !!：讀取所有討論串 (可能會列出很多討論串)
  ^G：取消目前的搜尋
   @：刷新畫面    
   *：標記星號/取消星號整個討論串內的訊息
   N：切換討論串內所有訊息的未讀/已讀狀態
   l：編輯或新增討論串的標籤
   e：編輯訊息 (僅可對草稿使用)
   S：標記/取消標記討論串爲垃圾郵件
   d：刪除/取消刪除討論串
   &：抹殺討論串 (再也不會出現在 inbox)
   $：馬上儲存變更
 tab：跳到下一個新討論串
   r：回覆討論串內最新的訊息
   f：轉寄討論串內最新的訊息
   t：標記/取消標記所選的討論串
   T：標記/取消標記所有的討論串
   g：標記符合的討論串
+, =：套用下一個操作到所有已標記的討論串
   #：強制所有已標記的討論串合併成一個討論串
   u：重做上一個操作

```

### thread-view-mode 下的按鍵綁定

```
      h：切換詳細標頭
      H：顯示完整訊息標頭
      V：顯示完整訊息 (原生格式)
<enter>：開啓/摺疊或啓動項目
      E：開啓/摺疊所有訊息
      e：編輯草稿
      y：寄出草稿
      l：替討論串編輯或新增標籤
      o：開啓/摺疊訊息中所有的引用
      n：跳到下一個開啓的訊息
      p：跳到前一個開啓的訊息
      z：對齊目前訊息在緩衝中的位置
      *：替訊息標記星號/取消標記星號
      N：切換訊息的未讀/已讀狀態
      r：恢復一個訊息
      f：轉寄訊息或附件
      i：編輯某人的別名/暱稱
      D：將訊息視爲新郵件來編輯
      s：儲存訊息/附件到磁碟
      S：從特定人士搜尋訊息
      m：編寫訊息給某人
      (：訂閱/取消訂閱郵件清單
      )：訂閱/取消訂閱郵件清單
      |：將訊息或附件重導給 shell 指令
     .a：封存該討論串然後抹殺緩衝
     .d：刪除該討論串然後抹殺緩衝
     .s：標記該討論串爲垃圾訊息然後抹殺緩衝
     .N：標記該討論串爲未讀然後抹殺緩衝
     ,a：封存該討論串，抹殺緩衝，然後檢視下一個
     ,d：刪除該討論串，抹殺緩衝，然後檢視下一個
     ,s：標記該討論串爲垃圾訊息，抹殺緩衝，然後檢視下一個
     ,N：標記該討論串爲未讀，抹殺緩衝，然後檢視下一個
     ,n：抹殺緩衝，然後檢視下一個
     ]a：封存該討論串，抹殺緩衝，然後檢視前一個
     ]d：刪除該討論串，抹殺緩衝，然後檢視前一個
     ]s：標記該討論串爲垃圾訊息，抹殺緩衝，然後檢視前一個
     ]N：標記該討論串爲未讀，抹殺緩衝，然後檢視前一個
     ]n：抹殺緩衝，然後檢視前一個

```

### contact-list-mode 下的按鍵綁定

```
   M：再讀取 10 個聯絡人
   D：放棄通訊錄然後重新讀取
a, i：編輯聯絡人的代稱或是姓名
   t：標記/取消標機該行
   +：套用下一個操作到所有已標記的項目
   S：從特定人士開始搜尋訊息

```

### line-cursor-mode 下的按鍵綁定

```
<down arrow>, j：將遊標向下移動一行
  <up arrow>, k：將遊標向上移動一行
        <enter>：選擇該項目

```

### scroll-mode 下的按鍵綁定

```
                        J, ^E：向下一行
                        K, ^Y：向上一行
              <left arrow>, h：向左一排
                <right arrow>：向右一排
     <page down>, <space>, ^F：向下一頁
<page up>, p, <backspace>, ^B：向上一頁
                           ^D：向下半頁
                           ^U：向上半頁
                 <home>, ^, 1：跳到頁首
                     <end>, 0：跳到頁尾
                            [：跳到左邊
                            /：在目前的緩衝內搜尋
                            n：跳到下個緩衝內搜尋到的項目

```

### 全域按鍵綁定

```
   q：離開 Sup，但是需要確認
   Q：直接離開 Sup
   ?：顯示幫助
   b：切換到下一個緩衝
   B：切換到前一個緩衝
   x：抹殺目前的緩衝
   ;：列出所有緩衝
   C：列出通訊錄
  ^L：重繪畫面
\, F：搜尋所有訊息
   U：顯示所有未讀訊息
   L：列出標籤
   P：輪查有無新訊息
m, c：撰寫新訊息
  ^G：什麼也不做
   R：編輯最近的訊息草稿

```

## 疑難排解

### 因爲 Illegal instruction (core dumped) 而當掉

`sup` 使用一套名爲 [Xapian](http://xapian.org/) 的搜尋引擎，且它被編譯爲使用 SSE2 指令集。如果您的 CPU 不支援 SSE2 指令集，您將碰上錯誤訊息：

```
   Illegal instruction (core dumped)

```

要解決這問題，您必須在編譯 Xapian 時加入 `--disable-sse` 選項。

1\. 查看 [ruby-xapian-ruby](https://aur.archlinux.org/packages/ruby-xapian-ruby/) 的 `PKGBUILD` 您可以得知它從 [https://rubygems.org/gems/xapian-ruby](https://rubygems.org/gems/xapian-ruby) 下載了一份 gem。下載那份 gem。

2\. 執行這些指令

```
   gem unpack xapian-ruby.gem
   gem unpack --spec xapian-ruby.gem
   mv xapian-ruby.gemspec xapian-ruby/
   cd xapian-ruby

```

3\. 您需要編輯 `Rakefile`。您的目標是修改兩行有執行設定參數的指令。您所要做的就是將 `--disable-sse` 加到這些設定指令後面：

```
   system! "./configure --prefix=#{prefix} --exec-prefix=#{prefix} --disable-sse"
   system! "./configure --prefix=#{prefix} --exec-prefix=#{prefix} --with-ruby --disable-sse"

```

然後儲存所做的修改。

4\. 執行

```
   gem build xapian-ruby.gemspec
   gem install --local xapian-ruby.gem

```

這樣應該能解決舊歀 CPU 不能執行 Xapian 的問題。附帶一提，如果您第一次執行 `sup-config` 且正確地完成所有設定，卻依然得到下列錯誤訊息

```
   This Sup version expects a v4 index, but you have an existing v0 index. Please run sup-dump to save your labels, move /home/user/.sup/xapian out of the way, and run sup-sync --restore. (RuntimeError)
   Rats, that failed. You may have to do it manually.

```

那麼您可能也碰上了該問題，嘗試執行其他如 `sup` 或 `sup-dump` 等執行檔，看看有無顯示 Illegal instruction (core dumped) 的錯誤訊息。

## 另請參閱

*   [網站](http://supmua.org/)
*   [Wiki](https://github.com/sup-heliotrope/sup/wiki)
*   [README](https://github.com/sup-heliotrope/sup/blob/develop/README.md)
*   [FAQ](https://github.com/sup-heliotrope/sup/blob/develop/doc/FAQ.txt)
*   [哲學闡述](https://github.com/sup-heliotrope/sup/blob/develop/doc/Philosophy.txt)