**翻译状态：** 本文是英文页面 [PhpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-06-22，点击[这里](https://wiki.archlinux.org/index.php?title=PhpMyAdmin&diff=0&oldid=526922)可以查看翻译后英文页面的改动。

[phpMyAdmin](http://www.phpmyadmin.net/)是一个基于网页的，帮助管理MySQL数据库的Apache/PHP前端。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 运行](#.E8.BF.90.E8.A1.8C)
    *   [2.1 PHP](#PHP)
    *   [2.2 Apache](#Apache)
    *   [2.3 Lighttpd](#Lighttpd)
    *   [2.4 Nginx](#Nginx)
        *   [2.4.1 子域名](#.E5.AD.90.E5.9F.9F.E5.90.8D)
        *   [2.4.2 子目录](#.E5.AD.90.E7.9B.AE.E5.BD.95)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 使用安装脚本](#.E4.BD.BF.E7.94.A8.E5.AE.89.E8.A3.85.E8.84.9A.E6.9C.AC)
    *   [3.2 添加blowfish_secret passphrase](#.E6.B7.BB.E5.8A.A0blowfish_secret_passphrase)
    *   [3.3 启用配置存储](#.E5.90.AF.E7.94.A8.E9.85.8D.E7.BD.AE.E5.AD.98.E5.82.A8)
        *   [3.3.1 创建数据库](#.E5.88.9B.E5.BB.BA.E6.95.B0.E6.8D.AE.E5.BA.93)
        *   [3.3.2 创建数据库用户](#.E5.88.9B.E5.BB.BA.E6.95.B0.E6.8D.AE.E5.BA.93.E7.94.A8.E6.88.B7)
    *   [3.4 启用templates catching](#.E5.90.AF.E7.94.A8templates_catching)
*   [4 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 软件包 [phpmyadmin](https://www.archlinux.org/packages/?name=phpmyadmin)。

## 运行

### PHP

确保PHP的[MySQL](/index.php/PHP_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#MySQL.2FMariaDB "PHP (简体中文)")扩展已经被启用。

你也可以启用`bz2`和`zip`扩展以支持压缩。

**注意:** 如果在`php.ini`中设置了`open_basedir`，`/etc/weppapps/`必须加入`open_basedir`。

### Apache

按照[Apache HTTP Server (简体中文)#PHP](/index.php/Apache_HTTP_Server_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#PHP "Apache HTTP Server (简体中文)")设置PHP。 创建Apache配置文件：

 `/etc/httpd/conf/extra/phpmyadmin.conf` 
```
Alias /phpmyadmin "/usr/share/webapps/phpMyAdmin"
<Directory "/usr/share/webapps/phpMyAdmin">
    DirectoryIndex index.php
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>
```

在`/etc/httpd/conf/httpd.conf`加入配置文件：

```
# phpMyAdmin configuration
Include conf/extra/phpmyadmin.conf

```

**注意:** 默认情况下，每个可以访问Web服务器的人都可以通过这个URL访问phpMyAdmin登录页面。要改变此设置，编辑`/etc/httpd/conf/extra/phpmyadmin.conf`。例如，你只想从本地访问phpMyAdmin，将`Require all granted`改为`Require local`。注意，这将禁止远程访问phpMyAdmin，如果你想安全地远程访问phpMyAdmin，你可以设置一个[加密的SOCKS通道](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.8A.A0.E5.AF.86_Socks_.E9.80.9A.E9.81.93 "Secure Shell (简体中文)")。

### Lighttpd

配置[Lighttpd](/index.php/Lighttpd "Lighttpd")，确保能正常使用PHP，并且启用`mod_alias`。

在配置文件中为phpmyadmin加入下列alias：

```
 alias.url = ( "/phpmyadmin" => "/usr/share/webapps/phpMyAdmin/")

```

### Nginx

确保正确配置[FastCGI](/index.php/Nginx#FastCGI "Nginx").

#### 子域名

参考[nginx#PHP configuration file](/index.php/Nginx#PHP_configuration_file "Nginx")，为php创建一个单独的配置文件，并使用一个服务器块，例如：

server {

```
    server_name     phpmyadmin.<domain.tld>;
    root    /usr/share/webapps/phpMyAdmin;
    index   index.php;
    include php.conf;
}

```

#### 子目录

这可以通过`https://domain.tld/phpMyAdmin`访问phpMyAdmin：

 `/etc/nginx/sites-available/domain.tld` 
```
location /phpMyAdmin {
   server_name domain.tld;
   listen 443 ssl http2;
   root /srv/http/domain.tld;
   index index.php;  

   location / {
      try_files $uri $uri/ =404;
   }

   # Deny static files
   location ~ ^/phpMyAdmin/(README|LICENSE|ChangeLog|DCO)$ {
      deny all;
   }

   # Deny .md files
   location ~ ^/phpMyAdmin/(.+\.md)$ {
      deny all;
   }

   # Deny setup directories
   location ~ ^/phpMyAdmin/(doc|sql|setup)/ {
      deny all;
   }

   #FastCGI config for phpMyAdmin
   location ~ /phpMyAdmin/(.+\.php)$ {
      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
      fastcgi_pass   unix:/run/php-fpm/php-fpm.sock;
      fastcgi_index  index.php;
      include        fastcgi.conf;
   }
}

```

## 配置

主配置文件位于`/etc/webapps/phpmyadmin/config.inc.php`。

如果[MySQL](/index.php/MySQL "MySQL")服务器不在本机上，添加如下行:

```
$cfg['Servers'][$i]['host'] = 'localhost';

```

### 使用安装脚本

要使用phpMyAdmin安装脚本（例如http://localhost/phpmyadmin/setup），确保`http`用户可以写入`/usr/share/webapps/phpMyAdmin`。

```
# mkdir /usr/share/webapps/phpMyAdmin/config
# chown http:http /usr/share/webapps/phpMyAdmin/config
# chmod 750 /usr/share/webapps/phpMyAdmin/config

```

### 添加blowfish_secret passphrase

需要设置一个32位的字符串从而充分地使用blowfish算法，从而避免……（配置文件现在需要一个短语密码）的错误。

(blowfish_secret)*:*

 `/etc/webapps/phpmyadmin/config.inc.php`  `$cfg['blowfish_secret'] = '...';` 

### 启用配置存储

例如table linking,change tracking,PDF creation,bookmarking queries的附加功能默认是被禁用的，并且会提示The phpMyAdmin configuration storage is not completely configured, some extended features have been deactivated.

**注意:** 下面的例子将`controluser`假设为**pma**，controlpass假设为**pmapass**。

在`/etc/webapps/phpmyadmin/config.inc.php`取消注释(移除开头的//)，并按需更改为所需的凭据：

 `/etc/webapps/phpmyadmin/config.inc.php` 
```
/* User used to manipulate with storage */
// $cfg['Servers'][$i]['controlhost'] = 'my-host';
// $cfg['Servers'][$i]['controlport'] = '3306';
$cfg['Servers'][$i]['controluser'] = 'pma';
$cfg['Servers'][$i]['controlpass'] = 'pmapass';

/* Storage database and tables */
$cfg['Servers'][$i]['pmadb'] = 'phpmyadmin';
$cfg['Servers'][$i]['bookmarktable'] = 'pma__bookmark';
$cfg['Servers'][$i]['relation'] = 'pma__relation';
$cfg['Servers'][$i]['table_info'] = 'pma__table_info';
$cfg['Servers'][$i]['table_coords'] = 'pma__table_coords';
$cfg['Servers'][$i]['pdf_pages'] = 'pma__pdf_pages';
$cfg['Servers'][$i]['column_info'] = 'pma__column_info';
$cfg['Servers'][$i]['history'] = 'pma__history';
$cfg['Servers'][$i]['table_uiprefs'] = 'pma__table_uiprefs';
$cfg['Servers'][$i]['tracking'] = 'pma__tracking';
$cfg['Servers'][$i]['userconfig'] = 'pma__userconfig';
$cfg['Servers'][$i]['recent'] = 'pma__recent';
$cfg['Servers'][$i]['favorite'] = 'pma__favorite';
$cfg['Servers'][$i]['users'] = 'pma__users';
$cfg['Servers'][$i]['usergroups'] = 'pma__usergroups';
$cfg['Servers'][$i]['navigationhiding'] = 'pma__navigationhiding';
$cfg['Servers'][$i]['savedsearches'] = 'pma__savedsearches';
$cfg['Servers'][$i]['central_columns'] = 'pma__central_columns';
$cfg['Servers'][$i]['designer_settings'] = 'pma__designer_settings';
$cfg['Servers'][$i]['export_templates'] = 'pma__export_templates';
```

##### 创建数据库

有两种方法来创建需要的表：

*   使用phpMyAdmin导入 `/usr/share/webapps/phpMyAdmin/sql/create_tables.sql`。
*   在命令行中执行`mysql -u root -p < /usr/share/webapps/phpMyAdmin/sql/create_tables.sql`。

##### 创建数据库用户

要赋予`controluser`所需的权限，执行如下的查询：

**注意:** 确保将所有的`pma`和`pmapass`替换为在`config.inc.php`设置的值。如果正在为远程数据库配置，还需将`localhost`改为适当的主机。

```
GRANT USAGE ON mysql.* TO 'pma'@'localhost' IDENTIFIED BY 'pmapass';
GRANT SELECT (
    Host, User, Select_priv, Insert_priv, Update_priv, Delete_priv,
    Create_priv, Drop_priv, Reload_priv, Shutdown_priv, Process_priv,
    File_priv, Grant_priv, References_priv, Index_priv, Alter_priv,
    Show_db_priv, Super_priv, Create_tmp_table_priv, Lock_tables_priv,
    Execute_priv, Repl_slave_priv, Repl_client_priv
    ) ON mysql.user TO 'pma'@'localhost';
GRANT SELECT ON mysql.db TO 'pma'@'localhost';
GRANT SELECT ON mysql.host TO 'pma'@'localhost';
GRANT SELECT (Host, Db, User, Table_name, Table_priv, Column_priv)
    ON mysql.tables_priv TO 'pma'@'localhost';

```

In order use the bookmark and relation features, set the following permissions:

```
GRANT SELECT, INSERT, UPDATE, DELETE ON phpmyadmin.* TO 'pma'@'localhost';

```

重新登录以启用新功能。

### 启用templates catching

在`/etc/webapps/phpmyadmin/config.inc.php`添加如下行：

```
 $cfg['TempDir'] = '/tmp/phpmyadmin'

```

## 参见

*   [Wikipedia](https://en.wikipedia.org/wiki/phpMyAdmin "wikipedia:phpMyAdmin")