# Apache HTTP Server (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Apache HTTP Server (简体中文)#](https://wiki.archlinux.org/index.php/Talk:Apache_HTTP_Server_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)))

**翻译状态：** 本文是英文页面 [LAMP](/index.php/LAMP "LAMP") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-11-21，点击[这里](https://wiki.archlinux.org/index.php?title=LAMP&diff=0&oldid=236184)可以查看翻译后英文页面的改动。

LAMP是指在许多web 服务器上使用的一个软件组合：Linux,Apache,MySQL/MariaDB以及PHP。本文档描述了怎样在Archlinux系统上安装设置Apache网页服务器。以及选择安装PHP和MariaDB并集成到Apache服务器中。

如果只是用来开发和测试， [Xampp](/index.php/Xampp "Xampp") 可能更简便一些。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 Apache](#Apache)
        *   [2.1.1 用户目录](#.E7.94.A8.E6.88.B7.E7.9B.AE.E5.BD.95)
        *   [2.1.2 SSL](#SSL)
        *   [2.1.3 Virtual Hosts](#Virtual_Hosts)
        *   [2.1.4 高级选项](#.E9.AB.98.E7.BA.A7.E9.80.89.E9.A1.B9)
    *   [2.2 PHP](#PHP)
        *   [2.2.1 高级选项](#.E9.AB.98.E7.BA.A7.E9.80.89.E9.A1.B9_2)
        *   [2.2.2 与apache2-mpm-worker和mod_fcgid一起使用php5](#.E4.B8.8Eapache2-mpm-worker.E5.92.8Cmod_fcgid.E4.B8.80.E8.B5.B7.E4.BD.BF.E7.94.A8php5)
    *   [2.3 MariaDB](#MariaDB)
*   [3 参见](#.E5.8F.82.E8.A7.81)
*   [4 链接](#.E9.93.BE.E6.8E.A5)

## 安装

```
# pacman -S apache php php-apache mysql

```

你可以只单独安装Apache，PHP或者MySQL，也可以安装所有包。这个文档假设你安装全部，当然你可以忽略任何部分。

**注意:** 新默认用户和用户组: 取代了原先的用户组group "nobody" ,现在默认以user/group "http" 来运行Apache。根据这个变化，需要调整httpd.conf，虽然仍然能够用nobody来运行httpd。

## 配置

### Apache

出于安全原因，Apache以root用户身份启动(直接的或者通过启动脚本)后将立即切换为 `/etc/httpd/conf/httpd.conf`中指定的UID/GID。

*   通过寻找如下命令的输出中的http来判断http user的存在：

```
 # grep http /etc/passwd

```

*   如果还不存在用户http，创建他：

```
 # useradd -d /srv/http -r -s /bin/false -U http

```

这将创建一个以目录/srv/http/为家目录的http用户，作为系统帐号（-r），使用bogus shell（-s /bin/false）并且创建一个相同名称的用户组（-U）。

*   按照你的喜好更改`httpd.conf` 和 `extra/httpd-default.conf` 。。出于安全原因，你可能想将 `extra/httpd-default.conf`中的 **ServerTokens Full** 改为 **ServerTokens Prod** 并且将 **ServerSignature On** 改为 **ServerSignature Off** 。

*   [启动](/index.php/Daemons#Starting_manually "Daemons") **httpd** (Apache 的守护进程).

```
 # systemctl start httpd

```

Apache现在应该在运行中了。通过使用浏览器访问http://localhost/ 来测试之。。应该有一个简单的Apache测试页面出现。如果你得到一个403错误，注释掉`/etc/httpd/conf/httpd.conf`中的如下行:

```
Include conf/extra/httpd-userdir.conf

```

*   可以在系统 [启动时自动启动](/index.php/Daemons#Starting_on_boot "Daemons") **httpd**进程。

```
 # systemctl enable httpd

```

#### 用户目录

*   如果你不希望用户目录在web上可以访问 (即， 机器上的`~/public_html` 在web上以 [http://localhost/~user/](http://localhost/~user/) 访问 -注意，你可以在`/etc/httpd/conf/extra/httpd-userdir.conf`文件中修改它所指向的目录)， 注释掉 `/etc/httpd/conf/httpd.conf` 文件中的如下行，他们默认时激活的：

```
 Include conf/extra/httpd-userdir.conf

```

*   你应该确保你的家目录权限时合适的以便Apache能够访问它。你的家目录和 `~/public_html/` 应该可以被其他用户执行。这样应该就可以了：

```
 $ chmod o+x ~
 $ chmod o+x ~/public_html

```

*   更安全的通过apache共享你的家目录的方法时将用户 **http** 添加到你的家目录所属的用户组中。 例如，如果你的家目录和他的子目录属于**piter**用户组，你需要做的就是：

```
 $ usermod -aG piter http

```

*   当然了，你还需要开放`~/`目录， `~/public_html`以及他们所有的子目录的‘读’权限和‘写’权限给这个组（在我们的例子中时用户组**piter**）。 如下这样做(**根据自己的情况修改命令**):

```
 $ chmod g+xr-w /home/_yourusername_
 $ chmod -R g+xr-w /home/_yourusername_/public_html

```

**注意:** 使用此种方法你不必为了将权限开放给用户http而开放权限给所有的用户。只有用户**http**和同属于**piter**用户组的其他用户可以访问你的家目录

并重启**httpd**.

#### SSL

创建自签名的证书（你可以改变密钥长度和有效天数）

```
# cd /etc/httpd/conf
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:4096 -out server.key
# openssl req -new -key server.key -out server.csr
# cp server.key server.key.org
# openssl rsa -in server.key.org -out server.key
# openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

```

在 `/etc/httpd/conf/httpd.conf`中，取消如下行的注释：

```
Include conf/extra/httpd-ssl.conf

```

并重启**httpd**。

#### Virtual Hosts

如果你需要不止一个主机，确保你有

```
# Virtual hosts
Include conf/extra/httpd-vhosts.conf

```

在 `/etc/httpd/conf/httpd.conf`文件中.

参考下面的例子，在 `/etc/httpd/conf/extra/httpd-vhosts.conf`中设置你的虚拟主机：

```
NameVirtualHost *:80

#this first virtualhost enables: [http://127.0.0.1](http://127.0.0.1), or: [http://localhost](http://localhost), 
#to still go to /srv/http/*index.html(otherwise it will 404_error).
#the reason for this: once you tell httpd.conf to include extra/httpd-vhosts.conf, 
#ALL vhosts are handled in httpd-vhosts.conf(including the default one),
# E.G. the default virtualhost in httpd.conf is not used and must be included here, 
#otherwise, only domainname1.dom & domainname2.dom will be accessible
#from your web browser and NOT [http://127.0.0.1](http://127.0.0.1), or: [http://localhost](http://localhost), etc.
#

<VirtualHost *:80>
    DocumentRoot "/srv/http"
    ServerAdmin root@localhost
    ErrorLog "/var/log/httpd/127.0.0.1-error_log"
    CustomLog "/var/log/httpd/127.0.0.1-access_log" common
    <Directory /srv/http/>
		    DirectoryIndex index.htm index.html
		    AddHandler cgi-script .cgi .pl
		    Options ExecCGI Indexes FollowSymLinks MultiViews +Includes
		    AllowOverride None
		    Order allow,deny
		    allow from all
	</Directory>
</VirtualHost>

<VirtualHost *:80>
    ServerAdmin your@domainname1.dom
    DocumentRoot "/home/username/yoursites/domainname1.dom/www"
    ServerName domainname1.dom
    ServerAlias domainname1.dom
    <Directory /home/username/yoursites/domainname1.dom/www/>
		    DirectoryIndex index.htm index.html
		    AddHandler cgi-script .cgi .pl
		    Options ExecCGI Indexes FollowSymLinks MultiViews +Includes
		    AllowOverride None
		    Order allow,deny
		    allow from all
	</Directory>
</VirtualHost>

<VirtualHost *:80>
    ServerAdmin your@domainname2.dom
    DocumentRoot "/home/username/yoursites/domainname2.dom/www"
    ServerName domainname2.dom
    ServerAlias domainname2.dom
    <Directory /home/username/yoursites/domainname2.dom/www/>
		    DirectoryIndex index.htm index.html
		    AddHandler cgi-script .cgi .pl
		    Options ExecCGI Indexes FollowSymLinks MultiViews +Includes
		    AllowOverride None
		    Order allow,deny
		    allow from all
	</Directory>
</VirtualHost>

```

将你的虚拟主机的名称添加到你的 /etc/hosts 文件（如果bind已经在为这些域名服务了，则非必需，但是加上也无妨）：

```
127.0.0.1	domainname1.dom
127.0.0.1	domainname2.dom
```

并重启**httpd**。

如果你将虚拟主机设定在你的用户目录中，有时这会干扰Apache的'Userdir'设定。注释掉以下行以避免此问题：

```
# User home directories
#Include conf/extra/httpd-userdir.conf
```

如上所述，确保你有合适的权限：

```
# chmod 0775 /home/yourusername/

```

如果你有非常多的虚拟主机并且希望轻松的激活或禁用他们，建议你为每一个虚拟主机创建一个配置文件并且将所有的这些配置文件存储到一个文件夹中，如：`/etc/httpd/conf/vhosts`。

首先创建这个文件夹：

```
# mkdir /etc/httpd/conf/vhosts

```

然后将单个的配置文件放到里面：

```
# nano /etc/httpd/conf/vhosts/domainname1.dom
# nano /etc/httpd/conf/vhosts/domainname2.dom
...

```

最后一步，"Include"单个的配置文件们到你的 `/etc/httpd/conf/httpd.conf`文件：

```
#Enabled Vhosts:
Include conf/vhosts/domainname1.dom
#Include conf/vhosts/domainname1.dom
```

你可以通过注释或去注释来激活或禁用单个的虚拟主机。

#### 高级选项

你也许会对 `/etc/httpd/conf/httpd.conf`中的这些选项感兴趣：

```
# Listen 80

```

这是Apache监听的端口。为了跨路由器的访问，你需要转发这个端口。

如果你只是用于本地开发，你可能希望她只能被你自己的计算机访问。那么将这一行改为：

```
# Listen 127.0.0.1:80

```

这是管理员的电子邮件地址，该地址可以在错误页面等处见到：

```
# ServerAdmin sample@sample.com

```

这是存放你的网页文件的目录：

```
# DocumentRoot "/srv/http"

```

如果愿意，可以修改，不过不要忘了同时修改

```
<Directory "/srv/http">

```

为你所修改的文档根目录，否则当你试图访问新的文档根目录时可能会得到一个403错误（缺少权限）。不要忘记修改"Deny from all"行，否则你也可能遇到403错误。

```
# AllowOverride None

```

`<Directory>`部分中的这条指令将使得Apache完全忽略.htaccess文件。如果你希望使用重写模块或.htaccess文件中的其他设定，你可以允许那个文件中声明的>指令覆盖服务器配置。请参考 [http://httpd.apache.org/docs/current/mod/core.html#allowoverride](http://httpd.apache.org/docs/current/mod/core.html#allowoverride) 以获得更多信息。

**注意:** 如果你对自己的配置文件有问题，你可以用如下命令让apache来检查一下你的配置文件：`apachectl configtest`

### PHP

*   从官方源[安装](/index.php/Pacman "Pacman") [php-apache](https://www.archlinux.org/packages/?name=php-apache)。

*   在`/etc/httpd/conf/httpd.conf`中添加如下行：

将这一行放在`LoadModule`列表中 `LoadModule dir_module modules/mod_dir.so` 之后的任意地方：

```
 LoadModule php5_module modules/libphp5.so

```

将这一行放到`Include`列表的末尾：

```
 Include conf/extra/php5_module.conf

```

确保`<IfModule mime_module>`部分中的如下行被取消注释：

```
 TypesConfig conf/mime.types

```

取消如下行的注释（可选）：

```
 MIMEMagicFile conf/magic

```

*   将这一行添加到`/etc/httpd/conf/mime.types`中：

```
 application/x-httpd-php5		php php5

```

**注意:** 如果你在Apache的模块目录（`/etc/httpd/modules`）中没有看到`libphp5.so`，你可能忘了安装[php-apache](https://www.archlinux.org/packages/?name=php-apache)。

**注意:** [本段来源](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server") 你可能会碰到这一bug ([FS#39218](https://bugs.archlinux.org/task/39218)) [php-apache](https://www.archlinux.org/packages/?name=php-apache)中的`libphp5.so`无法同`mod_mpm_event`一起使用。 此时应当使用 `mod_mpm_prefork` 作为代替。不然将发生下面的错误:

```
Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.
AH00013: Pre-configuration failed
httpd.service: control process exited, code=exited status=1
```

要使用 `mod_mpm_prefork`，编辑`/etc/httpd/conf/httpd.conf`将

 `LoadModule mpm_event_module modules/mod_mpm_event.so` 

替换成

 `LoadModule mpm_prefork_module modules/mod_mpm_prefork.so` 

另一种选择, 你可以使用`mod_proxy_fcgi` ( [使用php-fpm和mod_proxy_fcgi](/index.php/Apache_HTTP_Server#Using_php5_with_php-fpm_and_mod_proxy_fcgi "Apache HTTP Server") ).

*   如果你的`文件根目录`不是`/srv/http`，将其添加到`/etc/php/php.ini`的`open_basedir`部分，如下：

```
 open_basedir=/srv/http/:/home/:/tmp/:/usr/share/pear/:/path/to/documentroot

```

*   [重启](/index.php/Systemd#Using_units "Systemd") **httpd**。

*   测试PHP：在你的apache文档根目录（即`/srv/http/`或`~public_html`）中创建test.php文件，在其中写入：

```
<?php phpinfo(); ?>

```

看它是否能用： [http://localhost/test.php](http://localhost/test.php) 或者 [http://localhost/~myname/test.php](http://localhost/~myname/test.php)

如果PHP代码没有被执行（你看到了：<html>...</html>），检查一下`/etc/httpd/conf/httpd.conf`看你是否将你的根目录“Includes”到“Options”行中。

如果还不行，检查<IfModule mime_module>部分中`TypesConfig conf/mime.types` 是否被取消注释，你可以尝试将以下行添加到httpd.conf中的<IfModule mime_module>部分中：

```
AddHandler application/x-httpd-php .php

```

#### 高级选项

*   建议你在`/etc/php/php.ini`中将你的时区设置为这样：([时区列表](http://www.php.net/manual/en/timezones.php))

 `date.timezone = Asia/Shanghai` 

*   如果你想显示出错信息以调试你的PHP代码，将`/etc/php/php.ini`中的`display_errors`设置为`On`：

```
display_errors=On

```

*   如果你想使用libGD模块，安装{{}Pkg|php-gd}并且将`/etc/php/php.ini`中的`extension=gd.so`取消注释：

**注意:** php-gd 需要 libpng，libjpeg和freetype2

```
extension=gd.so

```

**注意:** 看清楚你注释的是哪一行，这个扩展有时会在你需要注释掉的那一行之前的解释性的注释中被提到

*   如果你需要mcrypt模块，安装[php-mcrypt](https://www.archlinux.org/packages/?name=php-mcrypt)并且取消`/etc/php/php.ini`中`extension=mcrypt.so`的注释：

```
extension=mcrypt.so

```

*   如果你需要，记得在`/etc/httpd/conf/extra/php5_module.conf`中为.phtml添加一个文件处理器：

```
DirectoryIndex index.php index.phtml index.html

```

#### 与apache2-mpm-worker和mod_fcgid一起使用php5

取消`/etc/conf.d/apache`中如下行的注释：

```
HTTPD=/usr/sbin/httpd.worker

```

取消`/etc/httpd/conf/httpd.conf`中如下行的注释：

```
Include conf/extra/httpd-mpm.conf

```

安装mod_fcgid和php-cgi包：

```
# pacman -S mod_fcgid php-cgi

```

创建`/etc/httpd/conf/extra/php5_fcgid.conf`，写入以下内容：

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
        PHP_Fix_Pathinfo_Enable 1
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

为PHP包装器创建需要的目录和符号链接：

```
# mkdir /srv/http/fcgid-bin
# ln -s /usr/bin/php-cgi /srv/http/fcgid-bin/php-fcgid-wrapper

```

编辑 `/etc/httpd/conf/httpd.conf`：

```
#LoadModule php5_module modules/libphp5.so
LoadModule fcgid_module modules/mod_fcgid.so
Include conf/extra/php5_fcgid.conf

```

确保`/etc/php/php.ini`中的如下指令被启用：

```
cgi.fix_pathinfo=1

```

并重启 **httpd**。

**注意:** Apache2.4（[AUR package](https://aur.archlinux.org/package.php?ID=60719)中可用）中已经可以与PHP-FPM（以及新的event MPM）一起使用[mod_proxy_fcgi](http://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html)（官方发行版的一部分）。参见[configuration example](http://wiki.apache.org/httpd/PHP-FPM)

### MariaDB

*   按照[MariaDB](/index.php/MariaDB "MariaDB")中所述配置MySQL/MariaDB。

*   至少取消`/etc/php/php.ini`中如下注释的一行：

```
;extension=pdo_mysql.so
;extension=mysqli.so

```

**警告:** 从 PHP 5.5 开始，`mysql.so` 被 [废弃](http://www.php.net/manual/de/migration55.deprecated.php)，若启用，会导致大量错误消息充斥日志文件。

*   可以加入有较少权限的 Mysql 用户以执行 Mysql 脚本，或者编辑`/etc/mysql/my.cnf`，取消 `skip-networking` 行注释，这样 Mysql 只允许本地访问。重启 Mysql 后修改生效。

*   [重启](/index.php/Systemd#Using_units "Systemd") **httpd**.

*   通过编辑`/etc/mysql/my.cnf`文件，取消`skip-networking`行的注释可以使MySQL服务器只能通过本地主机访问。

**Tip:** 可以安装[phpmyadmin](/index.php/PhpMyAdmin "PhpMyAdmin"), [adminer](/index.php/Adminer "Adminer") 或者 [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench) 来配合数据库的工作。

## 参见

*   [MariaDB](/index.php/MariaDB "MariaDB") - 关于MariaDB的的文章
*   [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") - LAMP环境下典型的MySQL Web前端
*   [Adminer](/index.php/Adminer "Adminer") - 一个课用于MySQL，PostgreSQL，SQLite，MS SQL和Oracle的功能全面的数据库管理工具
*   [Xampp](/index.php/Xampp "Xampp") - 支持PHP，Perl和MySQL的自包含的web服务器
*   [mod_perl](/index.php/Mod_perl "Mod perl") - Apache + Perl

## 链接

*   [Apache 官方网站](http://www.apache.org/)
*   [PHP官方网站](http://www.php.net/)
*   [MariaDB官方网站](https://mariadb.org/)
*   [生成ssh_test_certificate的教程](http://www.akadia.com/services/ssh_test_certificate.html)
*   [Apache故障排除Wiki](http://wiki.apache.org/httpd/CommonMisconfigurations)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Apache_HTTP_Server_(简体中文)&oldid=411410](https://wiki.archlinux.org/index.php?title=Apache_HTTP_Server_(简体中文)&oldid=411410)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server (简体中文)](/index.php/Category:Web_server_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Web server (简体中文)")