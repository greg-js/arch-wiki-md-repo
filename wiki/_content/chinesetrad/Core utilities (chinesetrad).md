**翻譯狀態：** 本文章是 [Core_Utilities](/index.php/Core_Utilities "Core Utilities") 的翻譯版本。最近一次的翻譯時間：2014-01-20。點擊[本連結](https://wiki.archlinux.org/index.php?title=Core_Utilities&diff=0&oldid=293712)查看英文頁面之後的變更。

本文章涉及 GNU/Linux 系統上所謂的「核心」工具，例如 *less* ，*ls* 和 *grep* ，本文聚焦 (但不限於) 在 GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) 軟體包的工具集，並提供各種關於這些工具的建議、技巧與資訊。

## Contents

*   [1 cat](#cat)
*   [2 cron](#cron)
*   [3 grep](#grep)
    *   [3.1 彩色輸出](#.E5.BD.A9.E8.89.B2.E8.BC.B8.E5.87.BA)
*   [4 iconv](#iconv)
*   [5 ip](#ip)
*   [6 less](#less)
    *   [6.1 透過環境變數幫輸出上色](#.E9.80.8F.E9.81.8E.E7.92.B0.E5.A2.83.E8.AE.8A.E6.95.B8.E5.B9.AB.E8.BC.B8.E5.87.BA.E4.B8.8A.E8.89.B2)
    *   [6.2 透過程式幫輸出上色](#.E9.80.8F.E9.81.8E.E7.A8.8B.E5.BC.8F.E5.B9.AB.E8.BC.B8.E5.87.BA.E4.B8.8A.E8.89.B2)
    *   [6.3 用 Vim 代替](#.E7.94.A8_Vim_.E4.BB.A3.E6.9B.BF)
*   [7 locate](#locate)
*   [8 ls](#ls)
*   [9 man](#man)
*   [10 mkdir](#mkdir)
*   [11 mv](#mv)
*   [12 rm](#rm)
*   [13 sed](#sed)
*   [14 seq](#seq)
*   [15 shred](#shred)
*   [16 sudo](#sudo)
*   [17 權限相關工具](#.E6.AC.8A.E9.99.90.E7.9B.B8.E9.97.9C.E5.B7.A5.E5.85.B7)
*   [18 另請參閱](#.E5.8F.A6.E8.AB.8B.E5.8F.83.E9.96.B1)

## cat

[cat](https://en.wikipedia.org/wiki/cat_(Unix) (*catenate*；連接) 是一個連接並顯示文件的標準 Unix 工具。

*   *cat* 並非內建於 shell，在多數場合下 (腳本或考慮效能)，使用[重新導向](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)")會更加方便。事實上 `< *file*` 的效果如同 `cat *file*` 。

*   按照以下結構可直接在某檔案添加多行文字：

```
$ cat << EOF >> *path/file*
*第一行*
...
*最後一行*
EOF

```

*   若您需要以倒反順序顯示檔案，有個工具叫 [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* 倒轉過來)。

## cron

[cron](https://en.wikipedia.org/wiki/cron "wikipedia:cron") 是一個類 Unix 作業系統下按表操課的工作排程程式。

參閱[本文](/index.php/Cron "Cron")。

**註記:** *systemd* 也有辦法做到不少 *cron* 的功能。參閱[相關文章](/index.php/Systemd/Timers#As_a_cron_replacement "Systemd/Timers")。

## grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") (來自 [ed](https://en.wikipedia.org/wiki/ed "wikipedia:ed") 的 *g/re/p*, *global/regular expression/print* (全域、正規表達式、列出)) 是一個最初為 Unix 所寫的命令列文字搜尋工具。*grep* 指令在檔案或標準輸入內搜尋符合給定正規表達式的行，並將結果列在標準輸出。

*   記得 *grep* 可以處理檔案，所以 `cat *file* | grep *pattern*` 這種架構可以更換成 `grep *pattern* *file*`

*   若要抓取 VCS 原始碼，有個以 Perl 寫成的優化工具叫 [ack](https://www.archlinux.org/packages/?name=ack)。參閱[官方網站](http://beyondgrep.com/)。

### 彩色輸出

*grep* 的彩色輸出除了美觀以外，也十分有助於學習 [regexp (正規表達式)](https://en.wikipedia.org/wiki/regexp "wikipedia:regexp") 和 *grep* 功能。

將以下內容寫入您的 shell 設定檔，使用 *grep* 的預設顏色。以 [Bash](/index.php/Bash "Bash") 為例：

 `~/.bashrc`  `alias grep='grep --color=auto'` 

或者設定 `GREP_OPTIONS` [環境變數](/index.php/Environment_variables "Environment variables")，但請留意，這可能會讓某些使用 *grep* 的腳本無法運作 [[1]](http://brainstorm.ubuntu.com/idea/24141/)：

```
export GREP_OPTIONS='--color=auto'

```

加上 `-n` 在輸出標註檔案行號：

```
alias grep='grep -n --color=auto'

```

環境變數 `GREP_COLORS` 可用來指定預設值以外的不同顏色。

## iconv

`iconv` 可將字元編碼轉換成另一種字元集。

以下指令將檔案 `foo` 從 ISO-8859-15 轉換到 UTF-8，並將結果儲存在 `foo.utf`：

```
$ iconv -f ISO-8859-15 -t UTF-8 foo >foo.utf

```

更多資訊請參閱 `man iconv` 。

## ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") 可用來顯示 Linux [IP](https://en.wikipedia.org/wiki/Internet_Protocol "wikipedia:Internet Protocol") 軟體堆疊內物件的相關資訊，如網路裝置、IP 位址、路由表等。各種附帶指令可以操作、設定這些物件。

| 物件 | 目的 | man 頁面 |
| ip addr | 連接埠位址管理 | ip-address |
| ip addrlabel | 連接埠位址標籤管理 | ip-addrlabel |
| ip l2tp | Tunnel Ethernet over IP (L2TPv3) | ip-l2tp |
| ip link | 網路裝置設定 | ip-link |
| ip maddr | 多點傳送位址管理 | ip-maddress |
| ip monitor | 監看 netlink 訊息 | ip-monitor |
| ip mroute | 多點傳送路由快取管理 | ip-mroute |
| ip mrule | 多點傳送路由政策資料庫內的規則 |
| ip neigh | 鄰居/ARP 表管理 | ip-neighbour |
| ip netns | 程序網路命名空間管理 | ip-netns |
| ip ntable | 鄰居表設定 | ip-ntable |
| ip route | 路由表管理 | ip-route |
| ip rule | 路由政策資料庫管理 | ip-rule |
| ip tcp_metrics | 管理 TCP Metrics | ip-tcp_metrics |
| ip tunnel | 隧道設定 | ip-tunnel |
| ip tuntap | 管理 TUN/TAP 裝置 |
| ip xfrm | 管理 IPSec 政策 | ip-xfrm |

help 指令對所有物件有效。舉例來說，輸入 `ip addr help` 將顯示針對位址物件使用的指令語法。

[網路設定](/index.php/Network_configuration "Network configuration")文章顯示在各種常見情境下如何在實際使用 *ip* 指令。

**註記:** 您或許比較熟知的是 [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") 指令，在舊版本的 Linux 上它被用來做介面設定。現在該指令不宜在 Arch Linux 上使用，您應該改使用 *ip* 。

## less

[less](https://en.wikipedia.org/wiki/less_(Unix) 是個終端機分頁程式，可一次一頁的檢視文字檔內容。比起其他的分頁程式如 [more](https://en.wikipedia.org/wiki/more_(command) "wikipedia:more (command)")、[pg](https://en.wikipedia.org/wiki/pg_(Unix) "wikipedia:pg (Unix)")，*less* 提供更完善的介面與[功能集](http://www.greenwoodsoftware.com/less/faq.html)。

### 透過環境變數幫輸出上色

將以下內容加入您的 shell 設定檔：

 `~/.bashrc` 
```
export LESS=-R
export LESS_TERMCAP_me=$(printf '\e[0m')
export LESS_TERMCAP_se=$(printf '\e[0m')
export LESS_TERMCAP_ue=$(printf '\e[0m')
export LESS_TERMCAP_mb=$(printf '\e[1;32m')
export LESS_TERMCAP_md=$(printf '\e[1;34m')
export LESS_TERMCAP_us=$(printf '\e[1;32m')
export LESS_TERMCAP_so=$(printf '\e[1;44;1m')
```

依照喜好更改上面的數值。請參考：[ANSI 控制碼](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors "wikipedia:ANSI escape code")。

### 透過程式幫輸出上色

您可以在 *less* 啟用語法上色。首先安裝 [source-highlight](https://www.archlinux.org/packages/?name=source-highlight)，接著在您的 shell 設定檔加入以下內容：

 `~/.bashrc` 
```
export LESSOPEN="| /usr/bin/source-highlight-esc.sh %s"
export LESS='-R '

```

經常在命令列介面工作的使用者可以安裝 [lesspipe](https://www.archlinux.org/packages/?name=lesspipe)。

使用者可以使用分頁程式列舉壓縮檔內的檔案：

 `$ less *compressed_file*.tar.gz` 
```
==> use tar_file:contained_file to view a file in the archive
-rw------- *username*/*group*  695 2008-01-04 19:24 *compressed_file*/*content1*
-rw------- *username*/*group*   43 2007-11-07 11:17 *compressed_file*/*content2*
*compressed_file*.tar.gz (END)
```

*lesspipe* 也提供 *less* 與檔案互動的能力，讓它不僅可以作文檔檢視，還能夠當作該檔案類型的替代關聯指令使用 (比如說取代 [html2text](https://www.archlinux.org/packages/?name=html2text) 以檢視 HTML)。

安裝 *lesspipe* 之後，需重新登入才能啟用，或是執行

```
source /etc/profile.d/lesspipe.sh

```

### 用 Vim 代替

[Vim](/index.php/Vim "Vim") (*visual editor improved*) 有個腳本可以檢視文字檔、壓縮檔、二進位檔、目錄的內容。將以下內容加入您的 shell 設定檔，將它設定為分頁程式：

 `~/.bashrc`  `alias less='/usr/share/vim/vim74/macros/less.sh'` 

除了 *less.sh* 巨集以外還有一種作法，它依靠 `PAGER` 環境變數。安裝 [vimpager-git](https://aur.archlinux.org/packages/vimpager-git/) 並將以下內容加入您的 shell 設定檔：

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

所有使用 `PAGER` 環境變數的程式 (如 [git](/index.php/Git "Git") ) 將以 *vim* 作為它們的分頁程式。

## locate

[locate](https://en.wikipedia.org/wiki/locate_(Unix) 可用來搜尋檔案系統上的檔案。它會從預先建立的檔案資料庫搜尋，該資料庫由 *updatedb* 或 daemon 產生，並使用遞增編碼 (incremental encoding) 壓縮。它的操作速度遠快於 *find*，但平常需要更新維護資料庫。

請參閱[本文](/index.php/Locate "Locate")。

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") (*list*；列舉) 是 Unix、類 Unix 作業系統上列舉檔案的指令。

*   *ls* 可以列舉[檔案權限](/index.php/File_permissions_and_attributes#Viewing_permissions "File permissions and attributes")。

*   用簡單的別名來啟用彩色輸出。從 `/etc/skel/.bashrc` 複製過來的 `~/.bashrc` 應已出現以下的內容：

	`alias ls='ls --color=auto'`

	下一步是讓 *ls* 的彩色輸出更加完整；例如，不正確的 (孤兒) 軟連結將以紅色表示。將以下內容加入您的 shell 設定檔：

	`eval $(dircolors -b)`

## man

[man](https://en.wikipedia.org/wiki/Man_page "wikipedia:Man page") (*manual page*；手冊頁) 是線上軟體文件的一種格式，常見於 Unix 或類 Unix 作業系統。涵蓋的主題包括電腦程式 (包含函式庫和系統呼叫)，正規標準和慣例，甚至還有抽象概念。請參閱[手冊頁](/index.php/Man_Pages "Man Pages")。

## mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir "wikipedia:mkdir") (*make directory*；建立目錄) 是建立目錄的指令。

*   要建立一個目錄與其樹狀架構，需要加上 `-p`，若否則出現錯誤。通常使用者都知道自己在做什麼，`-p` 可以設為預設值。

	 `alias mkdir='mkdir -p -v'` 

	`-v` 可以顯示詳盡資訊。

*   不需要先建立目錄再使用 *chmod* 更改權限模式，用 `-m` 選項可直接定義新建目錄的存取權限。

**提示：** 若您要建立一個暫存目錄，比較好的替代指令為 [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file") (*make termporary*；建立暫存): `mktemp -p`。

## mv

[mv](https://en.wikipedia.org/wiki/mv "wikipedia:mv") (*move*；移動) 是移動、重新命名檔案與目錄的指令。這個指令有潛在危險，謹慎的作法是限縮它的作用：

```
alias mv=' timeout 8 mv -iv'

```

這個別名在 *mv* 運行超過 8 秒後停止、當刪除三個以上檔案時要求確認、列舉操作過程，且若 shell 的歷史記錄設定為忽略以空格開頭的指令時，不記錄該指令到 shell 的歷史記錄檔案。

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) (*remove*；移除) 是刪除檔案與目錄的指令。

*   這個指令有潛在危險，謹慎的作法是限縮它的作用：

	 `alias rm=' timeout 3 rm -Iv --one-file-system'` 

	這個別名在 *rm* 運行超過 3 秒後停止、當刪除三個以上檔案時要求確認、列舉操作過程、不涉及超過一個檔案系統，且若 shell 的歷史記錄設定為忽略以空格開頭的指令時，不記錄該指令到 shell 的歷史記錄檔案。若您希望一次確認一個檔案，將 `-I` 替換為 `-i`。

	Zsh 的使用者可在 `timeout` 前加上 `noglob`，避免隱性的語法擴大解釋。

*   若要移除空目錄，使用 *rmdir*；若目標內含有檔案，該指令會失敗。

## sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") (*stream editor*；串流編輯器) 是解析並轉換文字的 Unix 工具。

這裡有份 *sed* 一行範例的[清單](http://sed.sourceforge.net/sed1line.txt)。

**提示：** 功能更為強大的替代品有 [AWK](https://en.wikipedia.org/wiki/AWK "wikipedia:AWK") 和 [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") 語言。

## seq

**seq** (*sequence*；數字序列) 是用來產生連續數字序列的工具。Shell 有內建的替代品，可以像[維基百科](https://en.wikipedia.org/wiki/Seq_(Unix) "wikipedia:Seq (Unix)")所解釋的方法來使用它們。

## shred

[shred](https://en.wikipedia.org/wiki/Shred_(Unix) 是安全刪除檔案與目錄的指令。這個指令有潛在危險，謹慎的作法是限縮它的作用：

```
alias shred=' timeout 3 shred -v'

```

這個別名在 *shred* 運行超過 3 秒後停止、列舉操作過程，且若 shell 的歷史記錄設定為忽略以空格開頭的指令時，不記錄該指令到 shell 的歷史記錄檔案。

Zsh 的使用者可在 `timeout` 前加上 `noglob`，避免隱性的語法擴大解釋。

## sudo

[Sudo](https://en.wikipedia.org/wiki/Sudo "wikipedia:Sudo") (*as superuser do*；以超級使用者身分做...) 在類 Unix 作業系統下，用來允許使用者以其他使用者 (通常為超級使用者或 root) 的安全性權限執行程式。參閱 [Sudo](/index.php/Sudo "Sudo")。

## 權限相關工具

*   [chmod](https://en.wikipedia.org/wiki/chmod "wikipedia:chmod") (*change mode*；更改模式) 是一個 Unix shell 指令和一個系統呼叫 (system call) 的名稱。這兩者都用來更改檔案系統物件 (包含檔案與目錄) 的存取權限，以及特定的特殊標籤。

*   [chown](https://en.wikipedia.org/wiki/chown "wikipedia:chown") (*change owner*；更改使用者) 在類 Unix 系統下用來更改檔案的擁有者。

*   [chattr](https://en.wikipedia.org/wiki/chattr "wikipedia:chattr") (*change attributes*；更改屬性) 是 Linux 作業系統下的指令，讓使用者為多種 Linux 檔案系統下的檔案設定特定屬性。

*   [lsattr](https://en.wikipedia.org/wiki/lsattr "wikipedia:lsattr") (*list attributes*；列舉屬性) 是命令列程式，用來列舉 Linux 延伸檔案系統的屬性。

*   `ls -l` 列舉檔案屬性。

這些工具的說明請參閱[檔案權限與屬性](/index.php/File_permissions_and_attributes "File permissions and attributes")一文。更進階的權限操作可參考 [capabilities](/index.php/Using_File_Capabilities_Instead_Of_Setuid "Using File Capabilities Instead Of Setuid") 和 [ACL](/index.php/ACL "ACL")。

## 另請參閱

*   [A sampling of coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - coreutils 的指令簡介