**翻译状态：** 本文是英文页面 [MediaWiki](/index.php/MediaWiki "MediaWiki") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-01-17，点击[这里](https://wiki.archlinux.org/index.php?title=MediaWiki&diff=0&oldid=563549)可以查看翻译后英文页面的改动。

**Note:** MediaWiki 还没有完全支持 PHP 7.3。[[1]](https://www.mediawiki.org/wiki/Compatibility#PHP)[[2]](https://phabricator.wikimedia.org/project/view/3494/)

[MediaWiki](https://www.mediawiki.org/wiki/MediaWiki) 是一个免费、开源的维基软件，用 [PHP](/index.php/PHP "PHP") 写成；原本是为维基百科开发的。它也给 archwiki 提供了帮助。（详情查看 [Special:Version](/index.php/Special:Version "Special:Version") 和 [GitHub repository](https://github.com/archlinux/archwiki)）。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 Configuration](#Configuration)
    *   [2.1 PHP](#PHP)
    *   [2.2 网站服务器](#网站服务器)
        *   [2.2.1 Apache](#Apache)
        *   [2.2.2 Nginx](#Nginx)
        *   [2.2.3 Lighttpd](#Lighttpd)
    *   [2.3 数据库](#数据库)
    *   [2.4 LocalSettings.php](#LocalSettings.php)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 数学 (texvc)](#数学_(texvc))
    *   [3.2 Unicode](#Unicode)
    *   [3.3 VisualEditor](#VisualEditor)

## 安装

为了运行 MediaWiki 你需要三个组件：

*   [mediawiki](https://www.archlinux.org/packages/?name=mediawiki) 包，[PHP](/index.php/PHP "PHP") 会作为它的依赖安装
*   一个网站服务器 – [Apache](/index.php/Apache "Apache")、[Nginx](/index.php/Nginx "Nginx") 或者 [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   一个数据库系统 – [MySQL](/index.php/MySQL "MySQL")、[PostgreSQL](/index.php/PostgreSQL "PostgreSQL") 或者 [SQLite](/index.php/SQLite "SQLite")

如果要在 [XAMPP](/index.php/XAMPP "XAMPP") 上安装 MediaWiki，参见 [mw:Manual:Installing MediaWiki on XAMPP](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki_on_XAMPP "mw:Manual:Installing MediaWiki on XAMPP")

## Configuration

The steps to achieve a working MediaWiki configuration involve editing the PHP settings and adding the MediaWiki configuration snippets.

### PHP

MediaWiki 需要 `iconv` 插件，所以需要把 `/etc/php/php.ini` 里面的 `extension=iconv` 取消注释。

可选插件：

*   为了渲染缩略图，安装 [ImageMagick](/index.php/ImageMagick "ImageMagick") 或者 [php-gd](https://www.archlinux.org/packages/?name=php-gd)（二选一）。如果安装的是后者，需要取消注释 `extension=gd`。
*   为了更高效率的 [Unicode normalization](https://www.mediawiki.org/wiki/Unicode_normalization_considerations "mw:Unicode normalization considerations")，安装 [php-intl](https://www.archlinux.org/packages/?name=php-intl) 并取消注释 `extension=intl`。

启用你的数据库管理系统的 API：

*   如果是 [MariaDB](/index.php/MariaDB "MariaDB")，取消注释`extension=mysqli`。
*   如果是 [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")，安装 [php-pgsql](https://www.archlinux.org/packages/?name=php-pgsql) 并取消注释 `extension=pgsql`。
*   如果是 [SQLite](/index.php/SQLite "SQLite")，安装 [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) 并取消注释 `extension=pdo_sqlite`。

Second, tweak the session handling or you might get a fatal error (`PHP Fatal error: session_start(): Failed to initialize storage module[...]`) by finding the `session.save_path` path. A good choice can be `/var/lib/php/sessions` or `/tmp/`.

 `/etc/php/php.ini`  `session.save_path = "/var/lib/php/sessions"` 

如果那个目录不存在，你要手动创建它，并更改权限：

```
# mkdir -p /var/lib/php/sessions/
# chown http:http /var/lib/php/sessions
# chmod go-rwx /var/lib/php/sessions

```

如果你使用了 [PHP's open_basedir](/index.php/PHP#Configuration "PHP") 并想 [允许文件上传](https://www.mediawiki.org/wiki/Manual:Configuring_file_uploads "mw:Manual:Configuring file uploads")，你需要把 `/var/lib/mediawiki/` 添加到里面去 ([mediawiki](https://www.archlinux.org/packages/?name=mediawiki) 为 `images/` 创建了指向 `/var/lib/mediawiki/` 的符号链接)。

### 网站服务器

#### Apache

按照 [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server") 配置 PHP。

复制 `/etc/webapps/mediawiki/apache.example.conf` 到 `/etc/httpd/conf/extra/mediawiki.conf` 并按需要修改它。 添加下面这一行到 `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/mediawiki.conf

```

[重启](/index.php/Restart "Restart") `httpd.service`。

**Note:** 默认示例文件 `/etc/webapps/mediawiki/apache.example.conf` 会覆盖 PHP 的 open_basedir 设置，可能会和其他页面产生冲突。 可以通过把以 `php_admin_value` 开头的行移到 `<Directory>` 标签之间来避免这个问题。而如果你运行了多个依赖同一个 server 的应用，你可以把这个值添加到 `/etc/php/php.ini` 里的 open_basedir 里，而不仅仅是放在 `/etc/httpd/conf/extra/mediawiki.conf` 里。

#### Nginx

对于 [Nginx](/index.php/Nginx "Nginx")，请创建这样的一个文件：

 `/etc/nginx/mediawiki.conf` 
```
location / {
   index index.php;
   try_files $uri $uri/ @mediawiki;
}
location @mediawiki {
   rewrite ^/(.*)$ /index.php;
}
location ~ \.php5?$ {
   include /etc/nginx/fastcgi_params;
   fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
   fastcgi_index index.php5;
   fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
   try_files $uri @mediawiki;
}
location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
   try_files $uri /index.php;
   expires max;
   log_not_found off;
}
# Restrictions based on the .htaccess files
location ^~ ^/(cache|includes|maintenance|languages|serialized|tests|images/deleted)/ {
   deny all;
}
location ^~ ^/(bin|docs|extensions|includes|maintenance|mw-config|resources|serialized|tests)/ {
   internal;
}
location ^~ /images/ {
   try_files $uri /index.php;
}
location ~ /\. {
   access_log off;
   log_not_found off; 
   deny all;
}

```

请确保 [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) 已安装并 [start](/index.php/Start "Start") 了。

在`/etc/nginx/nginx.conf`添加一个 server 块，类似这样的：

 `/etc/nginx/nginx.conf` 
```
server {
  listen 80;
  server_name mediawiki;
  root /usr/share/webapps/mediawiki;
  index index.php;
  charset utf-8;
# For correct file uploads
  client_max_body_size    100m; # Equal or more than upload_max_filesize in /etc/php/php.ini
  client_body_timeout     60;
  include mediawiki.conf;

}

```

最后，[restart](/index.php/Restart "Restart") `nginx.service` 和 `php-fpm.service`。

#### Lighttpd

You should have [Lighttpd](/index.php/Lighttpd "Lighttpd") installed and configured. "mod_alias" and "mod_rewrite" in server.modules array of lighttpd is required. Append to the lighttpd configuration file the following lines

 `/etc/lighttpd/lighttpd.conf` 
```
alias.url += ("/mediawiki" => "/usr/share/webapps/mediawiki/")
url.rewrite-once += (
                "^/mediawiki/wiki/upload/(.+)" => "/mediawiki/wiki/upload/$1",
                "^/mediawiki/wiki/$" => "/mediawiki/index.php",
                "^/mediawiki/wiki/([^?]*)(?:\?(.*))?" => "/mediawiki/index.php?title=$1&$2"
)

```

[Restart](/index.php/Restart "Restart") the `lighttpd.service` daemon.

### 数据库

按照你所需要的数据库管理系统（DBMS）的文章配置数据库服务器：[MySQL](/index.php/MySQL "MySQL")、[PostgreSQL](/index.php/PostgreSQL "PostgreSQL") 或者 [SQLite](/index.php/SQLite "SQLite")。

如果你在[下一步](#LocalSettings.php)里提供了数据库的 root 密码，MediaWiki会自动创建数据库。否则你就需要手动创建数据库，详情参考： [upstream instructions](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki#Create_a_database "mw:Manual:Installing MediaWiki")。

### LocalSettings.php

在浏览器里打开 wiki 的 url (通常是 `http://*your_server*/mediawiki/`) 并进行初始化配置。参考[upstream instructions](https://www.mediawiki.org/wiki/Manual:Config_script "mw:Manual:Config script")的步骤。

生成的 `LocalSettings.php` 文件是用来下载的，保存它到 `/usr/share/webapps/mediawiki/LocalSettings.php`。这个文件记录了你的 wiki 的配置，升级 [mediawiki](https://www.archlinux.org/packages/?name=mediawiki) 包是不会覆盖它的。

## Tips and tricks

### 数学 (texvc)

通常来说，安装 [texvc](https://www.archlinux.org/packages/?name=texvc) 并在配置文件里启用它就可以了：

```
$wgUseTeX = true;

```

如果遇到问题，尝试提高以下的 shell 命令限制值：

```
$wgMaxShellMemory = 8000000;
$wgMaxShellFileSize = 1000000;
$wgMaxShellTime = 300;
```

### Unicode

请确保 php、 apache 和 mysql 都用的是 UTF-8 编码。否则你可能遇到因为编码不匹配导致的奇怪bug。

### VisualEditor

The VisualEditor MediaWiki extension provides a rich-text editor for MediaWiki. Follow [mw:Extension:VisualEditor](https://www.mediawiki.org/wiki/Extension:VisualEditor "mw:Extension:VisualEditor") to install it.

You will also need the [Parsoid](https://www.mediawiki.org/wiki/Parsoid "mw:Parsoid") Node.js backend, which is available from the [AUR](/index.php/AUR "AUR") as [parsoid-git](https://aur.archlinux.org/packages/parsoid-git/).

Adjust the path to MediaWiki in `/usr/share/webapps/parsoid/api/localsettings.js`:

```
parsoidConfig.setInterwiki( 'localhost', 'http://localhost/mediawiki/api.php' );

```

After that [enable](/index.php/Enable "Enable") and start `parsoid.service`.

Alternatively, one may also use the [parsoid](https://aur.archlinux.org/packages/parsoid/) package, and configure the service via the yaml file, where the following lines should be present:

 `/usr/share/webapps/parsoid/config.yaml` 
```
uri: `'http://localhost/mediawiki/api.php'`
domain: 'localhost'

```

The matching part in the mediawiki settings:

 `/usr/share/webapps/mediawiki/LocalSettings.php` 
```
$wgVirtualRestConfig['modules']['parsoid'] = array(
  // URL to the Parsoid instance - use port 8142 if you use the Debian package - the parameter 'URL' was first used but is now deprecated (string)
  'url' => 'http://localhost:8000/',
  // Parsoid "domain" (string, optional) - MediaWiki >= 1.26
  'domain' => 'localhost',
  // Parsoid "prefix" (string, optional) - deprecated since MediaWiki 1.26, use 'domain'
  'prefix' => 'localhost',
  // Forward cookies in the case of private wikis (string or false, optional)
  'forwardCookies' => false,
  // request timeout in seconds (integer or null, optional)
  'timeout' => null,
  // Parsoid HTTP proxy (string or null, optional)
  'HTTPProxy' => null,
  // whether to parse URL as if they were meant for RESTBase (boolean or null, optional)
  'restbaseCompat' => null,
);

```

After configuration, the `parsoid` service may be started (restarted) and (if not done yet) enabled.