## Contents

*   [1 安裝 DokuWiki](#.E5.AE.89.E8.A3.9D_DokuWiki)
    *   [1.1 DokuWiki 是什麼?](#DokuWiki_.E6.98.AF.E4.BB.80.E9.BA.BC.3F)
    *   [1.2 說在前頭](#.E8.AA.AA.E5.9C.A8.E5.89.8D.E9.A0.AD)
        *   [1.2.1 lighttp 筆記](#lighttp_.E7.AD.86.E8.A8.98)
        *   [1.2.2 DokuWiki 筆記](#DokuWiki_.E7.AD.86.E8.A8.98)
*   [2 安裝 lighttp](#.E5.AE.89.E8.A3.9D_lighttp)
    *   [2.1 PHP, lighttp, 還有 fastcgi](#PHP.2C_lighttp.2C_.E9.82.84.E6.9C.89_fastcgi)
    *   [2.2 組態配置](#.E7.B5.84.E6.85.8B.E9.85.8D.E7.BD.AE)
*   [3 裝上 DokuWiki](#.E8.A3.9D.E4.B8.8A_DokuWiki)
    *   [3.1 下載最新版](#.E4.B8.8B.E8.BC.89.E6.9C.80.E6.96.B0.E7.89.88)
    *   [3.2 預備安裝的檔案](#.E9.A0.90.E5.82.99.E5.AE.89.E8.A3.9D.E7.9A.84.E6.AA.94.E6.A1.88)
    *   [3.3 DokuWiki Specific lighttp Configuration](#DokuWiki_Specific_lighttp_Configuration)
    *   [3.4 重新啟動 lighttp](#.E9.87.8D.E6.96.B0.E5.95.9F.E5.8B.95_lighttp)
    *   [3.5 Install DokuWiki](#Install_DokuWiki)
*   [4 後安裝](#.E5.BE.8C.E5.AE.89.E8.A3.9D)
    *   [4.1 打掃乾淨](#.E6.89.93.E6.8E.83.E4.B9.BE.E6.B7.A8)
    *   [4.2 裝外掛](#.E8.A3.9D.E5.A4.96.E6.8E.9B)
    *   [4.3 要備份](#.E8.A6.81.E5.82.99.E4.BB.BD)
*   [5 延伸閱讀](#.E5.BB.B6.E4.BC.B8.E9.96.B1.E8.AE.80)

## 安裝 DokuWiki

### DokuWiki 是什麼?

"DokuWiki 是一個讓使用者能建立出豐富文件庫，並與標準相容且易用的wiki系統。它提供環境給個人、團隊或公司使用一種簡單但拋耳否的語法格式來創作與協作，並確保檔案資料在wiki之外也能維持內容的結構與可讀性。"

"無次數限制的頁面修訂可讓頁面恢復到先前任一版本，資料也以純文字檔儲存，無需使用資料庫。拋耳否的外掛架構讓系統核心得以擴充與強化。看看功能特色章節瞭解DokuWiki所提供功能的完整描敘。"[[1]](http://wiki.splitbrain.org/wiki:dokuwiki)

另一方面來說，DokuWiki是個由PHP程式語言所編寫、可不使用資料庫的wiki系統。

[想看看一個在跑的例子？](http://www.dokuwiki.org/)

### 說在前頭

接下來的內容會指引你設置DokuWiki在html目錄之下。

若有人可把vhost設置步驟加入的話，請覺得免費去加進來。

#### lighttp 筆記

更多細節請看 [Lighttpd#FastCGI](/index.php/Lighttpd#FastCGI "Lighttpd") 。

html 目錄位於 /srv/http 。這目錄可能不是預設就被建立的，沒有你可以自己產生它。

```
 #mkdir -p /srv/http

```

lighttp 也會產生或使用 http:http 使用者帳號與群組。

```
 #chown http:http /srv/http

```

所有這些設定都能在這個檔案中作修改

```
 /etc/lighttpd/lighttpd.conf

```

#### DokuWiki 筆記

DocuWiki 部份外掛會尋找網頁伺服器的根目錄，而不是DokuWiki的根目錄這會導致一些問題發生。 所有預設外掛都能用下面的方法安裝。

## 安裝 lighttp

### PHP, lighttp, 還有 fastcgi

安裝 PHP [Lighttpd#FastCGI](/index.php/Lighttpd#FastCGI "Lighttpd")

```
 #pacman -S lighttpd fcgi php-cgi

```

加 lighttpd 到你的 rc.conf 裡

```
 DAEMONS=(syslog-ng network netfs crond **lighttpd**)

```

編輯你的 /etc/hosts.allow (加下面這一行)

```
 lighttpd:    ALL

```

啟動你的網頁伺服器 (*sanity check*)

```
 #/etc/rc.d/lighttpd start

```

建測試文件

```
 #echo "Testing lighttpd" > /srv/http/index.html

```

開瀏覽器到 [http://127.0.0.1/，你應該看到測試文件內容。](http://127.0.0.1/，你應該看到測試文件內容。)

要是試了沒有用(也檢查過):

```
chown -R http:http /var/run/lighttpd/

```

停掉網頁伺服器

```
 #/etc/rc.d/lighttpd stop

```

### 組態配置

去註解 /etc/lighttpd/lighttpd.conf 裡的這幾行

```
"mod_fastcgi"

```

```
fastcgi.server             = ( ".php" =>
                               ( "localhost" =>
                                 (
                                   "socket" => "/var/run/lighttpd/php-fastcgi.socket",
                                   "bin-path" => "/usr/bin/php-cgi"
                                 )
                               )
                            )

```

## 裝上 DokuWiki

### 下載最新版

到網站 [DokuWiki download](http://www.splitbrain.org/projects/dokuwiki) 拿到最新版

```
 #tar -C /srv/http -zxvf dokuwiki*.tgz
 #mv /srv/http/dokuwiki-DATE /srv/http/dokuwiki

```

### 預備安裝的檔案

chown DokuWiki 的檔案

```
 #chown -R http:http dokuwiki/

```

(http 是 lighttp 的預設啟動帳號，如果你有改過，把上面指令裡的 user:group 改成 lighttp 指定的 user:group)

### DokuWiki Specific lighttp Configuration

編輯 /etc/lighttpd/lighttpd.conf 依照 [dokuwiki instructions](http://www.dokuwiki.org/install:lighttpd) (可能會包含更新過的資訊)。

在這幾行下面:

```

$HTTP["url"] =~ "\.pdf$" {
  server.range-requests = "disable"
}

```

加上這些內容:

```
# subdir of dokuwiki
# comprised of the subdir of the root dir where dokuwiki is installed
# in this case the root dir is the basedir plus /htdocs/
# Note: be careful with trailing slashes when uniting strings.
# all content on this example server is served from htdocs/ up.
#var.dokudir = var.basedir + "/dokuwiki"
var.dokudir = server.document-root + "/dokuwiki"

# make sure those are always served through fastcgi and never as static files
# deny access completly to these
$HTTP["url"] =~ "/\.ht" { url.access-deny = ( "" ) }
$HTTP["url"] =~ "/_ht" { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/bin/"  { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/data/" { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/inc/"  { url.access-deny = ( "" ) }
$HTTP["url"] =~ "^" + var.dokudir + "/conf/" { url.access-deny = ( "" ) }

```

*這些項目給 dokuwiki 設定基本保全。* lighttpd 不會用到像 apache 的 .htaccess 檔案。 你*可以*不安裝這些設定，但*絕不*建議這麼做。

### 重新啟動 lighttp

開網頁伺服器

```
 #/etc/rc.d/lighttpd start

```

### Install DokuWiki

開瀏覽器到

```
 [http://127.0.0.1/dokuwiki/install.php](http://127.0.0.1/dokuwiki/install.php)

```

## 後安裝

### 打掃乾淨

**設定好組態配置後移除 install.php 檔案！**

```
 #rm /srv/http/dokuwiki/install.php

```

### 裝外掛

許多社群製作的外掛可以在這找到 [here](http://wiki.splitbrain.org/wiki:plugins)

它們可以從網頁界面的 Admin 選單加掛(更新也是)。

### 要備份

如果沒有用資料庫的話備份DokuWiki沒什麼。全部的頁面都是純文字，靠 tar 或 rsync 就能備份。

目前版本(2008-05-05)的目錄結構:

```
 /dokuwiki/data/  =>  所有使用者建立的資料
 /dokuwiki/lib/plugins/  =>  所有使用者加入的外掛

```

## 延伸閱讀

[DokuWiki 主站](http://www.dokuwiki.org/) 會有你可能需要的全部資訊與幫助。