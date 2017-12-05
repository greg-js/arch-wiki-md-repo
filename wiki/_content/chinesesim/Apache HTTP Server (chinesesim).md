Related articles

*   [PHP](/index.php/PHP "PHP")
*   [MySQL](/index.php/MySQL "MySQL")
*   [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin")
*   [Adminer](/index.php/Adminer "Adminer")
*   [XAMPP](/index.php/XAMPP "XAMPP")
*   [mod_perl](/index.php/Mod_perl "Mod perl")

**翻译状态：** 本文是英文页面 [Apache_HTTP_Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-12-04，点击[这里](https://wiki.archlinux.org/index.php?title=Apache_HTTP_Server&diff=0&oldid=500853)可以查看翻译后英文页面的改动。

LAMP是指在许多web 服务器上使用的一个软件组合：Linux,Apache,MySQL/MariaDB以及PHP。

[Apache HTTP 服务器](https://en.wikipedia.org/wiki/Apache_HTTP_Server 栈(**L**inux, **A**pache, **M**ySQL, **P**HP). 本文介绍。本文档描述了怎样安装设置 Apache 网页服务器。以及选择安装 [PHP](/index.php/PHP "PHP")和 [MySQL](/index.php/MySQL "MySQL") 并集成到Apache服务器中。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 高级选项](#.E9.AB.98.E7.BA.A7.E9.80.89.E9.A1.B9)
    *   [2.2 用户目录](#.E7.94.A8.E6.88.B7.E7.9B.AE.E5.BD.95)
    *   [2.3 TLS/SSL](#TLS.2FSSL)
        *   [2.3.1 创建密钥并自签名](#.E5.88.9B.E5.BB.BA.E5.AF.86.E9.92.A5.E5.B9.B6.E8.87.AA.E7.AD.BE.E5.90.8D)
    *   [2.4 Virtual Hosts](#Virtual_Hosts)
        *   [2.4.1 管理多个主机](#.E7.AE.A1.E7.90.86.E5.A4.9A.E4.B8.AA.E4.B8.BB.E6.9C.BA)
*   [3 扩展](#.E6.89.A9.E5.B1.95)
    *   [3.1 PHP](#PHP)
        *   [3.1.1 使用 libphp](#.E4.BD.BF.E7.94.A8_libphp)
        *   [3.1.2 使用 apache2-mpm-worker 和 mod_fcgid](#.E4.BD.BF.E7.94.A8_apache2-mpm-worker_.E5.92.8C_mod_fcgid)
        *   [3.1.3 使用 apache2-mpm-worker 和 mod_fcgid](#.E4.BD.BF.E7.94.A8_apache2-mpm-worker_.E5.92.8C_mod_fcgid_2)
        *   [3.1.4 测试 PHP](#.E6.B5.8B.E8.AF.95_PHP)
    *   [3.2 HTTP2](#HTTP2)
*   [4 问题处理](#.E9.97.AE.E9.A2.98.E5.A4.84.E7.90.86)
    *   [4.1 Apache 的状态和日志](#Apache_.E7.9A.84.E7.8A.B6.E6.80.81.E5.92.8C.E6.97.A5.E5.BF.97)
    *   [4.2 启动后出现 Error: PID file /run/httpd/httpd.pid not readable](#.E5.90.AF.E5.8A.A8.E5.90.8E.E5.87.BA.E7.8E.B0_Error:_PID_file_.2Frun.2Fhttpd.2Fhttpd.pid_not_readable)
    *   [4.3 AH00534: httpd: Configuration error: No MPM loaded.](#AH00534:_httpd:_Configuration_error:_No_MPM_loaded.)
    *   [4.4 AH00072: make_sock: could not bind to address](#AH00072:_make_sock:_could_not_bind_to_address)
    *   [4.5 php.ini 中的 max_execution_time 设置无效](#php.ini_.E4.B8.AD.E7.9A.84_max_execution_time_.E8.AE.BE.E7.BD.AE.E6.97.A0.E6.95.88)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [apache](https://www.archlinux.org/packages/?name=apache).

## 配置

Apache 配置文件位于 `/etc/httpd/conf`，主要的配置文件是 `/etc/httpd/conf/httpd.conf`, 此文件会引用其它文件。

用默认配置可以启动一个简单的服务，有用户访问时会提供目录 `/srv/http` 下的内容。

启动 `httpd.service` [systemd 服务](/index.php/Systemd#Using_units "Systemd")，Apache 就会启动，从浏览器中访问 [http://localhost/](http://localhost/) 会显示一个简单的索引页面。

### 高级选项

请参考 [Apache 完整 directives 配置选项](https://httpd.apache.org/docs/trunk/mod/directives.html) 和 [directive 快速参考](https://httpd.apache.org/docs/trunk/mod/quickreference.htm).

请关注一下 `/etc/httpd/conf/httpd.conf` 中的下面选项:

```
User http

```

	出于安全原因，Apache以root用户身份启动(直接的或者通过启动脚本)后将立即切换为 `/etc/httpd/conf/httpd.conf`中指定的 UID，默认配置是 *http*, 安装时会自动创建此用户。

```
Listen 80

```

	Apach 监听的端口，要被外网访问，请在路由器开放此端口。

	如果是本地调试用，可以用下面命令设置为仅供本地访问 `Listen 127.0.0.1:80`.

```
ServerAdmin you@example.com

```

	管理员的电子邮件，在错误页面会展示给用户。

```
DocumentRoot "/srv/http"

```

	网页的目录.

	如果需要可以修改这个目录，请记得同步修改 `<Directory "/srv/http">` 和`DocumentRoot`,否则访问新位置时可能出现 **403 Error** (缺少权限)问题。不要忘记修改 `Require all denied` 行到 `Require all granted`，否则会出现 **403 Error**. DocumentRoot 目录及其父目录必须有可执行权限，这样再能被服务器进程使用的用户访问到(用 `chmod o+x /path/to/DocumentRoot` 设置)，否则会出现 **403 Error**.

```
AllowOverride None

```

	在 `<Directory>` 段落中的这个设置会让 Apache 完全忽略 `.htaccess` 文件。从 Apache 2.4，这个设置以及是默认的，所以如果要使用 `.htaccess`，亲允许Overide. 如果要在 `.htaccess` 中使用 `mod_rewrite` 或其它设置, 可以指定哪些目录允许覆盖服务器配置。更多信息请访问 [Apache 文档](http://httpd.apache.org/docs/current/mod/core.html#allowoverride).

**Tip:** 可以用 `apachectl configtest` 检查配置文件是否存在问题。

更多设置可以访问 `/etc/httpd/conf/extra/httpd-default.conf`，例如

关闭服务器签名:

```
ServerSignature Off

```

隐藏 Apache 和 PHP 版本等属性:

```
ServerTokens Prod

```

### 用户目录

在默认设置下，可以通过 [http://localhost/~yourusername/](http://localhost/~yourusername/) 访问用户的主目录并显示 `~/public_html` 中的内容 (可以通过 `/etc/httpd/conf/extra/httpd-userdir.conf` 设置). 要禁用这个访问，请注释掉 `/etc/httpd/conf/httpd.conf` 文件中的如下行：

```
Include conf/extra/httpd-userdir.conf

```

请正确设置目录的权限，使得 Apache 可以访问到文件。主目录和 `~/public_html` 必须是可被其它用户执行:

```
$ chmod o+x ~
$ chmod o+x ~/public_html
$ chmod -R o+r ~/public_html

```

重启 `httpd.service` 服务以应用更改。参考 [Umask#Set the mask value](/index.php/Umask#Set_the_mask_value "Umask").

### TLS/SSL

**警告:** 如果计划使用 SSL/TLS，请注意某些版本和实现 [依然](https://weakdh.org/#affected) [有安全漏洞](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS.2FSSL "wikipedia:Transport Layer Security"). 访问 [http://disablessl3.com/](http://disablessl3.com/) 和 [https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html) 可以查看当前的安全漏洞和服务器处理方式。

[OpenSSL](/index.php/OpenSSL "OpenSSL") 提供了 TLS/SSL 支持，默认已经安装在 Arch 中。

在 `/etc/httpd/conf/httpd.conf` 中，取消下面行的注释:

```
LoadModule ssl_module modules/mod_ssl.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
Include conf/extra/httpd-ssl.conf

```

TLS/SSL 需要密钥和认证，如果你有公开域名，可以使用 [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt") 免费获取认证，如果没有，请参考 [#创建密钥并自签名](#.E5.88.9B.E5.BB.BA.E5.AF.86.E9.92.A5.E5.B9.B6.E8.87.AA.E7.AD.BE.E5.90.8D).

获取密钥和认证之后，请将 `/etc/httpd/conf/extra/httpd-ssl.conf` 中的 `SSLCertificateFile` 和 `SSLCertificateKeyFile` 指向对应的文件。如果还生成了 CA 认证链，请将文件名设置到 `SSLCertificateChainFile`.

重启 `httpd.service`.

**Tip:** Mozilla 的 [SSL/TLS 文章](https://wiki.mozilla.org/Security/Server_Side_TLS) 包含了 [Apache 相关](https://wiki.mozilla.org/Security/Server_Side_TLS#Apache) 配置的指南和一个 [自动生成工具](https://mozilla.github.io/server-side-tls/ssl-config-generator/)，可以有助于创建更安全的配置。

#### 创建密钥并自签名

创建一个私钥并自己签名认证，对于不需要 [CSR](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request") 的大部分使用来说已经足够:

```
# cd /etc/httpd/conf
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt -days 1095
# chmod 400 server.key

```

**Note:** -days 参数是可选的，RSA 密钥大小最低是 2048 (default).

如果需要创建 [CSR](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request")，用下面的密钥创建方:

```
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:4096 -out server.key
# chmod 400 server.key
# openssl req -new -sha256 -key server.key -out server.csr
# openssl x509 -req -days 1095 -in server.csr -signkey server.key -out server.crt

```

**Note:** [openssl 手册](https://www.openssl.org/docs/apps/openssl.html) 和 [opnssl 文档](https://www.openssl.org/docs/) 包含了更多信息。

### Virtual Hosts

**Note:** You will need to add a separate <VirtualHost *:443> section for virtual host SSL support. See [#Managing many virtual hosts](#Managing_many_virtual_hosts) for an example file.

如果需要不止一个主机，在 `/etc/httpd/conf/httpd.conf`中注释掉:

```
Include conf/extra/httpd-vhosts.conf

```

在 `/etc/httpd/conf/extra/httpd-vhosts.conf` 中设置虚拟主机，默认文件包含了一个示例。

要在本地机器测试虚拟主机，将虚拟名称加入 `/etc/hosts` 文件:

```
127.0.0.1 domainname1.dom 
127.0.0.1 domainname2.dom

```

重启 `httpd.service` 服务。

#### 管理多个主机

如果要管理的主机非常多，希望更方便的维护，建议为每一个虚拟主机创建一个配置文件并文件存储到一个文件夹中 `/etc/httpd/conf/vhosts`。

创建目录：

```
# mkdir /etc/httpd/conf/vhosts

```

编写单独的配置文件:

```
# nano /etc/httpd/conf/vhosts/domainname1.dom
# nano /etc/httpd/conf/vhosts/domainname2.dom
...

```

在 `/etc/httpd/conf/httpd.conf` 中 `Include` 单独的配置文件:

```
#Enabled Vhosts:
Include conf/vhosts/domainname1.dom
Include conf/vhosts/domainname2.dom

```

通过注释或取消注释可以单独启用或禁用一个虚拟主机。

基本的 vhost 文件：

 `/etc/httpd/conf/vhosts/domainname1.dom` 
```
<VirtualHost *:80>
    ServerAdmin webmaster@domainname1.dom
    DocumentRoot "/home/user/http/domainname1.dom"
    ServerName domainname1.dom
    ServerAlias domainname1.dom
    ErrorLog "/var/log/httpd/domainname1.dom-error_log"
    CustomLog "/var/log/httpd/domainname1.dom-access_log" common

    <Directory "/home/user/http/domainname1.dom">
        Require all granted
    </Directory>
</VirtualHost>

<VirtualHost *:443>
    ServerAdmin webmaster@domainname1.dom
    DocumentRoot "/home/user/http/domainname1.dom"
    ServerName domainname1.dom:443
    ServerAlias domainname1.dom:443
    SSLEngine on
    SSLCertificateFile "/etc/httpd/conf/apache.crt"
    SSLCertificateKeyFile "/etc/httpd/conf/apache.key"
    ErrorLog "/var/log/httpd/domainname1.dom-error_log"
    CustomLog "/var/log/httpd/domainname1.dom-access_log" common

    <Directory "/home/user/http/domainname1.dom">
        Require all granted
    </Directory>
</VirtualHost>
```

## 扩展

### PHP

首先，参考 [PHP](/index.php/PHP "PHP") 页面，完成 PHP 的安装。

有多种方式可以在 Apache 下使用 PHP，[#使用 libphp](#.E4.BD.BF.E7.94.A8_libphp) 最简单，但是扩展性最差，libphp 还需要修改 mpm 模块，可能影响其它扩展，比如和 [#HTTP2](#HTTP2) 不兼容。

#### 使用 libphp

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")软件包 [php-apache](https://www.archlinux.org/packages/?name=php-apache)。

[php-apache](https://www.archlinux.org/packages/?name=php-apache) 中包含的 `libphp7.so` 不支持 `mod_mpm_event`，仅支持 `mod_mpm_prefork`([FS#39218](https://bugs.archlinux.org/task/39218))。需要在 `/etc/httpd/conf/httpd.conf` 中注释掉:

```
#LoadModule mpm_event_module modules/mod_mpm_event.so

```

取消下面行的注释:

```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

不然将发生下面的错误:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.
AH00013: Pre-configuration failed
httpd.service: control process exited, code=exited status=1
```

另一种选择, 你可以使用`mod_proxy_fcgi` ( [使用php-fpm和mod_proxy_fcgi](/index.php/Apache_HTTP_Server#Using_php-fpm_and_mod_proxy_fcgi "Apache HTTP Server")

要启用 PHP，在 `/etc/httpd/conf/httpd.conf` 中添加如下行：

*   将这一行放在`LoadModule` 的末尾：

```
 LoadModule php7_module modules/libphp7.so
 AddHandler php7-script php

```

*   将这一行放到`Include`列表的末尾：

```
 Include conf/extra/php7_module.conf

```

[重启](/index.php/Systemd#Using_units "Systemd") `httpd.service`。

#### 使用 apache2-mpm-worker 和 mod_fcgid

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) 和 [php-cgi](https://www.archlinux.org/packages/?name=php-cgi).

创建目录并建立 PHP 软链接:

```
# mkdir /srv/http/fcgid-bin
# ln -s /usr/bin/php-cgi /srv/http/fcgid-bin/php-fcgid-wrapper

```

取消`/etc/conf.d/apache`中如下行的注释：

```
HTTPD=/usr/sbin/httpd.worker

```

创建 `/etc/httpd/conf/extra/php-fcgid.conf`，包含的内容：

 `/etc/httpd/conf/extra/php-fcgid.conf` 
```
# Required modules: fcgid_module

<IfModule fcgid_module>
    AddHandler php-fcgid .php
    AddType application/x-httpd-php .php
    Action php-fcgid /fcgid-bin/php-fcgid-wrapper
    ScriptAlias /fcgid-bin/ /srv/http/fcgid-bin/
    SocketPath /var/run/httpd/fcgidsock
    SharememPath /var/run/httpd/fcgid_shm
        # If you don't allow bigger requests many applications may fail (such as WordPress login)
        FcgidMaxRequestLen 536870912
        # Path to php.ini – defaults to /etc/phpX/cgi
        DefaultInitEnv PHPRC=/etc/php/
        # Number of PHP childs that will be launched. Leave undefined to let PHP decide.
        #DefaultInitEnv PHP_FCGI_CHILDREN 3
        # Maximum requests before a process is stopped and a new one is launched
        #DefaultInitEnv PHP_FCGI_MAX_REQUESTS 5000
        <Location /fcgid-bin/>
        SetHandler fcgid-script
        Options +ExecCGI
    </Location>
</IfModule>

```

编辑 `/etc/httpd/conf/httpd.conf`，加入：

```
LoadModule fcgid_module modules/mod_fcgid.so
Include conf/extra/httpd-mpm.conf
Include conf/extra/php-fcgid.conf

```

**Note:** 如果之前在 `httpd.conf` 加入了下面内容，请删除它们，已经不再需要：
```
LoadModule php7_module modules/libphp7.so
Include conf/extra/php7_module.conf

```

[重启](/index.php/Restart "Restart") `httpd.service`.

#### 使用 apache2-mpm-worker 和 mod_fcgid

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) 和 [php-cgi](https://www.archlinux.org/packages/?name=php-cgi)。

创建需要的目录并建立软链接:

```
# mkdir /srv/http/fcgid-bin
# ln -s /usr/bin/php-cgi /srv/http/fcgid-bin/php-fcgid-wrapper

```

创建 `/etc/httpd/conf/extra/php-fcgid.conf`，内容是:

 `/etc/httpd/conf/extra/php-fcgid.conf` 
```
# Required modules: fcgid_module

<IfModule fcgid_module>
    AddHandler php-fcgid .php
    AddType application/x-httpd-php .php
    Action php-fcgid /fcgid-bin/php-fcgid-wrapper
    ScriptAlias /fcgid-bin/ /srv/http/fcgid-bin/
    SocketPath /var/run/httpd/fcgidsock
    SharememPath /var/run/httpd/fcgid_shm
        # If you don't allow bigger requests many applications may fail (such as WordPress login)
        FcgidMaxRequestLen 536870912
        # Path to php.ini – defaults to /etc/phpX/cgi
        DefaultInitEnv PHPRC=/etc/php/
        # Number of PHP childs that will be launched. Leave undefined to let PHP decide.
        #DefaultInitEnv PHP_FCGI_CHILDREN 3
        # Maximum requests before a process is stopped and a new one is launched
        #DefaultInitEnv PHP_FCGI_MAX_REQUESTS 5000
    <Location /fcgid-bin/>
        SetHandler fcgid-script
        Options +ExecCGI
    </Location>
</IfModule>

```

编辑 `/etc/httpd/conf/httpd.conf`，启用 actions 模块：

```
LoadModule actions_module modules/mod_actions.so

```

并添加如下配置:

```
LoadModule fcgid_module modules/mod_fcgid.so
Include conf/extra/httpd-mpm.conf
Include conf/extra/php-fcgid.conf

```

[Restart](/index.php/Restart "Restart") `httpd.service`.

#### 测试 PHP

在 apache 文档根目录（即`/srv/http/`或`~public_html`）中创建test.php文件，在其中写入：

```
<?php phpinfo(); ?>

```

然后访问： [http://localhost/test.php](http://localhost/test.php) 或者 [http://localhost/~myname/test.php](http://localhost/~myname/test.php)

高级的配置和扩展，请设置 [PHP](/index.php/PHP "PHP").

### HTTP2

要启用 http2，安装 [nghttp2](https://www.archlinux.org/packages/?name=nghttp2) 软件包。然后取消 `httpd.conf` 中下面行前的注释:

```
LoadModule http2_module modules/mod_http2.so

```

并加入:

```
Protocols h2 http/1.1

```

更多信息请参考 [mod_http2](https://httpd.apache.org/docs/2.4/mod/mod_http2.html) 文档。

## 问题处理

### Apache 的状态和日志

状态信息可以用 [systemctl](/index.php/Systemctl "Systemctl") 查询。

Apache 默认的系统日志位于 `/var/log/httpd/`。

### 启动后出现 Error: PID file /run/httpd/httpd.pid not readable

在 `httpd.conf` 中注释掉 `unique_id_module` 行：

```
#LoadModule unique_id_module modules/mod_unique_id.so

```

### AH00534: httpd: Configuration error: No MPM loaded.

最近的升级需要修改 `httpd.conf` 配置文件，取消下面行前的注释：

 `/etc/httpd/conf/httpd.conf` 
```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

### AH00072: make_sock: could not bind to address

多种都可能导致此问题，最常见的问题是已经有程序监听了设置的端口，通过下面命令确认：

```
# netstat -lnp | grep -e :80 -e :443

```

如该能查到结果，关闭占用端口的程序，然后重试。

还有一个原因是 Apache 没有以 root 执行，运行下面命令看看问题是否依然发生：

```
# httpd -k start

```

最后，可能配置有问题，导致程序同时监听了端口两次，例如下面的配置就有这个问题：

```
Listen 0.0.0.0:80
Listen [::]:80

```

### php.ini 中的 max_execution_time 设置无效

`php.ini` 中的 `max_execution_time` 设置为大于 30 (秒), 还会受到 `503 Service Unavailable` 的话，还需要添加 `ProxyTimeout` 到 `<FilesMatch \.php$>` 段落之前:

 `/etc/httpd/conf/httpd.conf` 
```
ProxyTimeout 300

```

重启 `httpd.service`.

## 参阅

*   [Apache 官方网站](http://www.apache.org/)
*   [Apache wiki](https://wiki.apache.org/httpd/)
*   [生成ssh_test_certificate的教程](http://www.akadia.com/services/ssh_test_certificate.html)
*   [Apache故障排除Wiki](http://wiki.apache.org/httpd/CommonMisconfigurations)