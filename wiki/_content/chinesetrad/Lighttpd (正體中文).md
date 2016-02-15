_[Lighttpd](http://trac.lighttpd.net/)是一個安全，快速，標準，且非常靈活的網頁伺服器，並對高性能環境做了最佳化。相較於其他網頁伺服器它佔用的記憶體很少，注重CPU負載量。它的進階功能集（FastCGI的，CGI的，權威性，輸出壓縮，網址重寫等等）讓lighttpd成為每個遭受負載問題的伺服器的完美網頁伺服器軟體。_

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
*   [2 組態](#.E7.B5.84.E6.85.8B)
    *   [2.1 基本設定](#.E5.9F.BA.E6.9C.AC.E8.A8.AD.E5.AE.9A)
    *   [2.2 FastCGI, PHP, Ruby on Rails, 及其它](#FastCGI.2C_PHP.2C_Ruby_on_Rails.2C_.E5.8F.8A.E5.85.B6.E5.AE.83)

## 安裝

Lighttpd可在extra倉庫取得:

```
# pacman -S lighttpd

```

# 組態

### 基本設定

lighttpd組態檔：`/etc/lighttpd/lighttpd.conf`。它預設會產生一個可用的測試頁面。

預設組態檔指定 `/srv/http/` 為提供服務的文件目錄。

它可能會需要加入http的使用者和群組，如果你還沒有的話。 另外使用者也需要擁有`/var/log/lighttpd`目錄的寫入權限，所以我們讓它成為目錄的擁有者：

```
# groupadd http
# adduser http
# chown -R http /var/log/lighttpd

```

測試安裝結果：

```
# /etc/rc.d/lighttpd start
# touch /srv/http/index.html
# chmod 755 /srv/http/index.html
# echo 'TestMe!' >> /srv/http/index.html

```

然後用瀏覧器開啟網址 `localhost` ，你應該會見到測試頁面。

你可能想把lighttpd加到`/etc/rc.conf`的daemons列表，在開機時啟動伺服器。

### FastCGI, PHP, Ruby on Rails, 及其它

其它lighttpd的額外元件的設定與組態可參考下列文章：

*   [Lighttpd#SSL](/index.php/Lighttpd#SSL "Lighttpd")
*   [Lighttpd#FastCGI](/index.php/Lighttpd#FastCGI "Lighttpd")