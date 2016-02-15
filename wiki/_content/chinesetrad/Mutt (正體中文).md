Mutt是一個基於文本的郵件用戶端，因其具有強大的特性而聲名赫赫。儘管Mutt已經是一個十多年前的老東西了，但對於相當多的高級用戶來說，仍然是郵件用戶端之必選。不幸的是，Mutt會默認安裝一套複雜的快鍵綁定（keybindings），令人頭痛；說明文檔又長篇大論，足令人心悸。本指南將幫助那些普通用戶來安裝和運行Mutt，並幫助他（她）們按照自己的喜好，對Mutt作出初步的設定。

## Contents

*   [1 趕快開始吧](#.E8.B6.95.E5.BF.AB.E9.96.8B.E5.A7.8B.E5.90.A7)
    *   [1.1 哪些是Mutt不會做的](#.E5.93.AA.E4.BA.9B.E6.98.AFMutt.E4.B8.8D.E6.9C.83.E5.81.9A.E7.9A.84)
    *   [1.2 安裝Mutt](#.E5.AE.89.E8.A3.9DMutt)
*   [2 設置 IMAP 方式接收電郵](#.E8.A8.AD.E7.BD.AE_IMAP_.E6.96.B9.E5.BC.8F.E6.8E.A5.E6.94.B6.E9.9B.BB.E9.83.B5)
    *   [2.1 設置OfflineIMAP](#.E8.A8.AD.E7.BD.AEOfflineIMAP)
    *   [2.2 讓 Mutt 配合 offlineimap 收信](#.E8.AE.93_Mutt_.E9.85.8D.E5.90.88_offlineimap_.E6.94.B6.E4.BF.A1)
*   [3 設置POP方式接收電郵](#.E8.A8.AD.E7.BD.AEPOP.E6.96.B9.E5.BC.8F.E6.8E.A5.E6.94.B6.E9.9B.BB.E9.83.B5)
    *   [3.1 配置 GetMail](#.E9.85.8D.E7.BD.AE_GetMail)
    *   [3.2 讓 Mutt 配合 GetMail 收信](#.E8.AE.93_Mutt_.E9.85.8D.E5.90.88_GetMail_.E6.94.B6.E4.BF.A1)
*   [4 郵件排序](#.E9.83.B5.E4.BB.B6.E6.8E.92.E5.BA.8F)
*   [5 用 SMTP 協議發送電郵](#.E7.94.A8_SMTP_.E5.8D.94.E8.AD.B0.E7.99.BC.E9.80.81.E9.9B.BB.E9.83.B5)
    *   [5.1 配置 msmtp](#.E9.85.8D.E7.BD.AE_msmtp)
    *   [5.2 讓 Mutt 配合 msmtp 發送電郵](#.E8.AE.93_Mutt_.E9.85.8D.E5.90.88_msmtp_.E7.99.BC.E9.80.81.E9.9B.BB.E9.83.B5)
    *   [5.3 郵件簽名](#.E9.83.B5.E4.BB.B6.E7.B0.BD.E5.90.8D)
    *   [5.4 用Firefox查看URL鏈接](#.E7.94.A8Firefox.E6.9F.A5.E7.9C.8BURL.E9.8F.88.E6.8E.A5)
    *   [5.5 Mutt 和 Vim](#Mutt_.E5.92.8C_Vim)
*   [6 一點引導](#.E4.B8.80.E9.BB.9E.E5.BC.95.E5.B0.8E)
    *   [6.1 有沒有同時支持 IMAP 和 POP 方式收信的工具呢？](#.E6.9C.89.E6.B2.92.E6.9C.89.E5.90.8C.E6.99.82.E6.94.AF.E6.8C.81_IMAP_.E5.92.8C_POP_.E6.96.B9.E5.BC.8F.E6.94.B6.E4.BF.A1.E7.9A.84.E5.B7.A5.E5.85.B7.E5.91.A2.EF.BC.9F)
    *   [6.2 有沒有同時支持 IMAP 和 POP 方式收信，還能郵件排序的呢？](#.E6.9C.89.E6.B2.92.E6.9C.89.E5.90.8C.E6.99.82.E6.94.AF.E6.8C.81_IMAP_.E5.92.8C_POP_.E6.96.B9.E5.BC.8F.E6.94.B6.E4.BF.A1.EF.BC.8C.E9.82.84.E8.83.BD.E9.83.B5.E4.BB.B6.E6.8E.92.E5.BA.8F.E7.9A.84.E5.91.A2.EF.BC.9F)
    *   [6.3 自動生成 mutt 配置文件](#.E8.87.AA.E5.8B.95.E7.94.9F.E6.88.90_mutt_.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)

## 趕快開始吧

### 哪些是Mutt不會做的

Mutt是一個用戶級的電郵代理(MUA)，這個程式就是被寫出來觀看電郵用的。寫它的是時候，並不是用來收、發和過濾電郵的。它要依賴外部程式來做這些事。在此Wiki中，我們將在POP3/IMAP協議下，使用 offlineimap 或者 getmail 來收郵件，用 procmail 來過濾郵件，並用 msmtp 來發送郵件。

### 安裝Mutt

通過一個簡單的命令 `pacman -S mutt` 就能安裝 Mutt了。

## 設置 IMAP 方式接收電郵

Mutt 已經內建支援 IMAP 方式，卻不會自己下載電郵來離線使用（除非設置好它）。本小節講述了如何用[OfflineIMAP](http://software.complete.org/offlineimap) 來將電郵下載到本地文件夾中，然後用Mutt來處理這些郵件。

### 設置OfflineIMAP

首先要啟用Community程式庫，並通過一個簡單的命令 `pacman -S offlineimap` 來安裝 OfflineIMAP。 現在你要按自己的需要來設置好它。創建一個文件`~/.offlineimaprc` 並用你中意的編輯器來編輯它。下面是一個配置文件的例示。可按自己的需要來編輯它。

```
[general]
accounts = myaccount
# 郵件帳戶在本地電腦上的稱謂名，將它改為你任何你想要的名字
ui = Curses.Blinkenlights
# Blinky樣式的控制臺輸出，讓你知道發生了什么。
# ui = Noninteractive.Quiet
# 如果啟用此行，則不會輸出任何東西。最適宜cronjobs 在幕後運行了。

[Account myaccount]
# 這裡的“myaccount”就是你在剛剛在上面改過的稱謂名了。
localrepository = mylocal
# 這裡是特定的稱謂名“myaccount”之下的本地郵件暫存處的名字，起個自己喜歡的名字。
remoterepository = myremote
# 這裡是特定的稱謂名“myaccount”之下的遠程郵件暫存處的名字，起個自己喜歡的名字,比如：Gmail。
# autorefresh = 5
# 如果啟用此行，則每隔五分鐘抓取一下電郵

[Repository mylocal]
# 這裡的“mylocal”就是你在剛剛在上面改過的本地郵件暫存處的名字。
type = Maildir
# 在本地存儲郵件的方式。當然只支持 Maildir 方式。
localfolders = ~/Mail
# 指定~/Mail這個文件夾來跟電郵服務器同步電郵。當然必須事先創建好這個文件夾了，不過文件夾的名字可改為你任何你想要的名字。

[Repository myremote]
# 這裡的“myremote”就是你在剛剛在上面改過的遠程郵件暫存處的名字。
type = IMAP
# 遠程郵箱的類型。當前僅支持 IMAP 類型的郵箱。
remotehost = imap.myhost.com
# 連接什么地方的電郵呢？比如Gmail郵箱就是：imap.gmail.com
ssl = yes
# 啟用安全的 SSL 支持，需事先安裝OpenSSL。
# remoteport = 993
# 如果郵箱能支持的話，就一定要啟用，這將指定一個特定的加密通訊埠：993。否則將使用缺省的普通通訊埠，也起不到加密的作用了。
remoteuser = myremoteusername
# 就是你的郵箱登入名啦。
remotepass = myremotepassword
# 郵箱的密碼。 -- 當然，像這樣直接列出密碼，是不太安全。所以你要確信該文件只有你才有讀取權限。還有更好的辦法，不過就請自行參看OfflineIMAP的手冊吧。
```

這是能讓你運行起來的最少設置了。更多高級的特性，請參閱[OfflineIMAP的主頁](http://software.complete.org/offlineimap)，再返回頭看一看[offlineimaprc註解](http://software.complete.org/offlineimap/browser/offlineimap.conf).

現在就快要準備好運行 OfflineIMAP 了。
創建一個已經在 offlineimaprc 中定義好的目錄，就像這樣： `mkdir ~/Mail` 。然後運行 `offlineimap` 。你的電郵就會同步到本地電腦上了。如果出了什么錯，就仔細查看一下錯誤消息。通常 OfflineIMAP 提示的錯誤消息有比較詳盡的文字說明。
如果能夠成功運行，那么可以啟用 `# ui = Noninteractive.Quiet` 這一行，以關閉提示信息。

### 讓 Mutt 配合 offlineimap 收信

若要配合配合 offlineimap 收信，那么本地存儲郵件的方式，只能是 Maildir 方式。 MailDir 的好處在於其格式的通用性和標準化.幾乎每一個 MUA 都能處理 MailDirs ，而 Mutt 當然也支持得很棒。現在用你的編輯器打開 `~/.muttrc` 並將下面這幾行添加進入：

```
set mbox_type=Maildir
#設置郵件存儲方式為：Maildir
set folder=~/Mail
#設置郵件的存儲目錄為：~/Mail ，這個目錄跟上面 offlineimaprc  中設置的 localfolders 目錄必須是一致的。否則 offlineimap 收到的信，Mutt 是找不到的。
set spoolfile=+/INBOX
#將接收/閱讀新郵件的目錄設置為：~/Mail/INBOX 。因為 offlineimap 會默認把新郵件放到 INBOX 這個目錄中。該行也可以這樣寫：set spoolfile = "+INBOX" ，這种寫法跟上面是一樣的含義。
set mbox = "+inbox"
#新郵件閱讀後，轉移到 ~/Mail/inbox 這個目錄。
set record = "+sent"
#郵件被成功發送後，轉移到 ~/Mail/sent 這個目錄。
set postponed = "+draft"
#郵件如果暫時不能發送或要推遲發送，就轉移到 ~/Mail/draft 這個目錄。
set header_cache=~/Mail/.hcache
#設置郵件頭的暫存目錄

macro index G "!/usr/bin/offlineimap \n" "Checking mails......"
#設置一個快捷鍵：G ，來調用 offlineimap 查閱新電郵
```

這是一個最精簡的配置文件了，能讓你訪問你的 Maildir，並在收件箱（INBOX）中檢查新電郵。這個配置也對電郵的郵件頭作了暫存，從而加速郵件的列示過程。也許你的安裝包沒有開啟暫存功能，不過Arch 的安裝包一定是開啟了的。注意這項功能真的對 OfflineIMAP 有相當影響。它總是在從郵件服務器同步電郵。 `spoolfile` 告訴Mutt從本地哪個目錄來得到新電郵。你可能還想添加更多的 Spoolfiles，例如郵件列表（Mailing List）所在的目錄。或者你想添加其它什么東西，但這就超出了這份文檔的范圍了，還請自行參閱手冊 `man mutt` 。

當然，我們也最好事先創建好配置文件中的那些郵件儲存目錄。然後就可以鍵入指令： `mutt` 來收信和閱讀信件了。

就這樣了。別忘了將每一樣設置都調整到你喜歡的樣子。自己努力解決吧。

## 設置POP方式接收電郵

### 配置 GetMail

先安裝[getmail](http://pyropus.ca/software/getmail/)。它在`[extra]` 程式庫中.

```
 pacman -S getmail

```

現在創建目錄： `~/.getmail/`。用編輯器打開`~/.getmail/getmailrc` 。

這裡有一個例子 `getmailrc` ，用的是Gmail帳戶。

```
[retriever]
type = SimplePOP3SSLRetriever
server = pop.gmail.com
username = username@gmail.com
port = 995
password = password

[destination]
type = Maildir
path = ~/mail/
```

你可以將它調整為你自己的POP3服務配置。

在本指南中，我們將把郵件以 `maildir` 的格式存放起來。兩個主要的郵箱格式分別是 `mbox` 和`maildir` 。其差別主要在於： `mbox` 是存儲著所有郵件及其郵件頭的一個文件；而 `maildir` 是一個目錄樹，每個郵件都是一個單獨的文件，這往往能提升運行速度。

`maildir` 只是一個文件夾，裡面有 `cur` ， `new` 和 `tmp` 這三個文件夾。

```
   mkdir -p ~/mail/{cur,new,tmp}

```

現在可以運行getmail了。如果它正常工作了，就可以為getmail創建一個計劃任務（cronjob），讓它每過幾分鐘/小時就運行一次。鍵入 `crontab -e` 命令來編輯cronjobs，輸入以下內容：

```
 */30 * * * * /usr/bin/getmail

```

此設置可以每隔三十分鐘，運行一次`getmail` 。

### 讓 Mutt 配合 GetMail 收信

配置文件的內容跟上面是大同小異的。也許要單獨指定 spoolfile 的目錄。自己試試吧。

## 郵件排序

[Procmail](http://www.procmail.org/) 是一個極其強大的排序工具。鑒于此篇Wiki的目地，我們將做一些基本排序設置，來拋磚引玉。

先安裝procmail。它在 `[extra]` 程式庫中。

```
 pacman -S procmail

```

用哪個工具來接收電郵，就必須對哪個工具的配置文件進行編輯。
遺憾的是，上文中談到的 offlineimap 當前無法配合 procmail 來使用。它只負責從 IMAP 服務器上同步電郵，故需事先在 IMAP 服務器上作好相關的設定（如果電郵服務器支援的話）。

這裡以 getmail 這個工具為例，它必須要配置 `getmailrc` ，使你收郵件的時候，通過procmail來處理。可添加：

```
[destination]
type = MDA_external
path = /usr/bin/procmail
```

現在用編輯器打開 `~/.procmailrc` 。下面將對來自happy-kangaroos 郵件列表，以及來自親朋好友的所有電郵作一個排序，每個人都有各自的Maildir。

```
#指定郵件目錄
MAILDIR=~/Mail
#酌情填寫閱讀新郵件的目錄
DEFAULT=$MAILDIR/INBOX/
#指定處理時的記錄文件
LOGFILE=$MAILDIR/procamil_log

#所有發往happy-kangaroos@nicehost.com的電郵，放入 happy-kangaroos 目錄。
:0:
* ^To: happy-kangaroos@nicehost.com
happy-kangaroos/

#所有來自loveydovey@iheartyou.net的電郵，放入 lovey-dovey 目錄。
:0:
* ^From: loveydovey@iheartyou.net
lovey-dovey/
```

保存 `.procmailrc` 後，運行getmail，看看它是否在適當的目錄中對你的郵件成功排序了。

## 用 SMTP 協議發送電郵

無論你是用 POP 還是 IMAP 協議來接收電郵，都可能要用到 SMTP 協議來發送郵件。
這裡選擇 msmtp 這個工具來幫助我們發送郵件。

### 配置 msmtp

[Msmtp](http://msmtp.sourceforge.net/)是一個很簡單易用的SMTP用戶端，安全性也不錯。它在`[extra]`程式庫中。

```
 pacman -S msmtp

```

用編輯器打開 `~/.msmtprc` 。下面以 Gmail 帳戶為例來配置 `.msmtprc` :

```
account default
# 我們可能會有不少電郵帳戶，也許每個帳戶都使用不同的方式來發送電郵，default 表示這是當前用戶的缺省郵件帳戶發送方式。

host smtp.gmail.com
port 587
# 這是 Gmail 的 TLS 通訊埠
# port 465
# 這是 Gmail 的 SSL 通訊埠
protocol smtp

auth on
# 允許 SMTP 驗證
tls on
# 允許 TLS/SSL 加密連接，以保證電郵安全。如果指定了 Gmail 的 TLS 通訊埠，
#那么它必須：要麼使用 tls_trust_file 指定一個信任的服務器證書， 要麼就關閉
#tls_certcheck （易受到中間人攻擊）。不是每一台電郵服務器都支持 TLS 隧道加密方式 。
#有個別的服務器只能實現 SSL 加密，它會要求 tls on 的同時，關閉掉 tls_starttls 。
tls_trust_file ~/TRUST_CERT_FILE.crt
# ca-certificates.crt 就是個可信任證書，對 Gmail 而言。
#tls_certcheck off
#如果沒有可信任的服務器證書，就只好啟用上面這行了。
# tls_starttls off
# 啟用 TLS 保護下的 SMTP 隧道。缺省情況下就是打開的。需要指定 Gmail 的 TLS 通訊埠。

from username@gmail.com
user username@gmail.com
password mypassword

```

編輯好配置文件後，還需要設定它的權限為：僅用戶本人才能有此文件的讀寫權限：

 `chmod 600 ~/.msmtprc` 

用 1.4.11 版的 msmtp 時，必然要涉及到設定 TLS 。 [msmtp, TLS, and ArchLinux](http://mychael.gotdns.com/blog/2007/04/18/msmtp-tls-and-archlinux/) 對于如何配置 msmtp 的認証作出了指導。
如果你確實不知道上哪裡去找 ca-certificates.crt 這個 Gmail 信任的根證書，那么就 [自己申請一個吧](http://www.thawte.com/roots/)。不然，你就只能以 SSL 方式來連接 Gmail ；如果一定要用 TLS 方式，那也要設置 `tls_certcheck off`

### 讓 Mutt 配合 msmtp 發送電郵

如果是按照上文所述，已經對 `~/.muttrc` 作了一些配置，那么還要再添加一些設置，才能在 Mutt 程式中發送電郵：

```
set realname='YOUR NAME'

set sendmail="/usr/bin/msmtp"

# 配合 procmail ，分別指定不同來源電郵的接收目錄，也就是 Mutt 讀取電郵的目錄。
mailboxes +INBOX +lovey-dovey +happy-kangaroos
```

現在，啟動 mutt。你會在 `~/mail/INBOX` 看到所有的郵件。按下 `m`鍵來撰寫郵件， (它會使用 `EDITOR` 環境變量中定義好的編輯器。如果這個變量還沒有被設定，那麽可鍵入 `export EDITOR=/path/to/yourfavorite/editor` 。想要測試一下，可以給自己發一封郵件。
寫好信後，在你的編輯器中保存它。再返回到Mutt中，它會顯示出這封郵件的消息。按 `y` 來發送它。如果都正常，那麽就恭喜了！你能用Mutt了！不過呢，要實現Mutt真正強大的能力，還要作一些進一步的定制才行啊。

一份關于使用與定制Mutt的指南：

*   [My first mutt](http://mutt.blackfish.org.uk/) (由Bruno Postle維護)
*   [The Woodnotes Guide to the Mutt Email Client](http://www.therandymon.com/woodnotes/mutt/using-mutt.html) (由Randall Wood維護)

[xterminus](/index.php/User:Xterminus "User:Xterminus") 是mutt社區中相當活躍的人。可以從 [Code and Configs Page](http://xtermin.us/code/#muttstuff) 找到他的個人配置文件。如果你有什麽特別的問題，請隨意在 [the irc channel](/index.php/ArchChannel "ArchChannel") 上提問。

### 郵件簽名

在你的家目錄（$HOME）中創建一個 `.signature` 文件。你的簽名會在附在郵件的後面。

### 用Firefox查看URL鏈接

你可以在$HOME創建一個 `./mutt` 目錄，如果沒有的話。 再創建一個名為 macros 的文件。 加入下面的內容：

```
 macro pager \cb <pipe-entry>'urlview'<enter> 'Follow links with urlview'

```

然後必需要安裝 urlview ，它在 [AUR] 倉庫中，可用

在$HOME創建一個 .urlview 配置文件，并加入下面的內容：

```
REGEXP (((http|https|ftp|gopher)|mailto)[.:][^ >"\t]*|www\.[-a-z0-9.]+)[^ .,;\t>">\):]
COMMAND firefox %s 

```

當用Mutt閱讀郵件時，點擊 ctrl+b ，將會列出郵件中所有的超級鏈接 urls 。用箭頭按鍵上下翻動它們，然後在要訪問的鏈接上點擊 enter 。Firefox 將啟動，并訪問那個站點了。

當然，urlview 配置文件中的“firefox”完全可以用任意網頁網頁瀏覽器來替換，比如：swiftfox, elinks, w3m，等等。

### Mutt 和 Vim

要將文本的寬度限制在 72 個字符， 可編輯你的 .vimrc 文件，并加入：

```
au BufRead /tmp/mutt-* set tw=72

```

這樣，Vim 只有在你使用 Mutt 的時候，都會有上面的行為了。

要設置另外一個臨時文件目錄，如 ~/.tmp，可在你的 .muttrc 文件中加上一行，如下所示：

```
set tmpdir="~/.tmp"

```

要重新格式化一個調整過的文本，可參看 Vim 的幫助文件：

```
:h 10.7

```

## 一點引導

### 有沒有同時支持 IMAP 和 POP 方式收信的工具呢？

有，那就是 fetchmail. 安裝方法： pacman -S fetchmail

它是一個更加強大的電郵接收工具，見[Fetchmail](http://fetchmail.berlios.de/) ，它支援包括 POP 和 IMAP 在內的多種協議，也能支援 procmail 。

### 有沒有同時支持 IMAP 和 POP 方式收信，還能郵件排序的呢？

有，那就是 FDM (Fetch and Deliver Mail) 安裝方法： pacman -S fdm

它是一個輕量級的電郵接收和排序工具，可以替代 fetchmail + procmail. 參見 [FDM](http://fdm.sourceforge.net/)，還有論壇上的文章：[fdm - a new procmail & fetchmail & esmtp](https://bbs.archlinux.org/viewtopic.php?id=27858)

### 自動生成 mutt 配置文件

mutt 配置文件比較複雜，不過現在有一個工具可幫助生成配置文件，可自行參閱 [muttrc builder](http://www.muttrcbuilder.org/builder-cgi.pl)