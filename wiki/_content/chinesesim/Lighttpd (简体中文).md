Lighttpd是 一个安全，快速，标准，且非常灵活的网页服务器，并对高性能环境做了最佳化。相较于其他网页服务器它占用的内存很少，且注重CPU负载量。它的进阶功能集 （FastCGI，CGI，验证，输出压缩，网址重写等等）让Lighttpd成为每个试图拜托负载瓶颈的服务器的完美网页服务器软件。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 设置](#.E8.AE.BE.E7.BD.AE)
    *   [2.1 基本设置](#.E5.9F.BA.E6.9C.AC.E8.AE.BE.E7.BD.AE)
    *   [2.2 CGI](#CGI)
    *   [2.3 FastCGI](#FastCGI)
        *   [2.3.1 PHP](#PHP)
            *   [2.3.1.1 Using php-fpm](#Using_php-fpm)
            *   [2.3.1.2 eAccelerator](#eAccelerator)
            *   [2.3.1.3 Try a php page](#Try_a_php_page)
        *   [2.3.2 Ruby on Rails](#Ruby_on_Rails)
        *   [2.3.3 Python FastCGI](#Python_FastCGI)
    *   [2.4 SSL](#SSL)
        *   [2.4.1 Server Name Indication](#Server_Name_Indication)
        *   [2.4.2 Redirect HTTP requests to HTTPS](#Redirect_HTTP_requests_to_HTTPS)
    *   [2.5 Output Compression](#Output_Compression)
*   [3 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [3.1 关于Lighttpd下载.php文件的情况](#.E5.85.B3.E4.BA.8ELighttpd.E4.B8.8B.E8.BD.BD.php.E6.96.87.E4.BB.B6.E7.9A.84.E6.83.85.E5.86.B5)
    *   [3.2 CCS样式列表无法正确显示](#CCS.E6.A0.B7.E5.BC.8F.E5.88.97.E8.A1.A8.E6.97.A0.E6.B3.95.E6.AD.A3.E7.A1.AE.E6.98.BE.E7.A4.BA)
*   [4 参见](#.E5.8F.82.E8.A7.81)

## 安装

Lighttpd可以从[extra]仓库获得:

```
# pacman -S lighttpd

```

## 设置

### 基本设置

lighttpd配置文件： `/etc/lighttpd/lighttpd.conf`。在安装完成后它会自动生成一个用于测试的测试页面。

想要检查 `lighttpd.conf` 中的语法错误，可以使用以下命令来快速查找错误：

```
$ lighttpd -t -f /etc/lighttpd/lighttpd.conf

```

预设配置文件会把这里 `/srv/http/` 指定为提供HTTP服务的文件目录。

测试安装结果：

```
# chmod 755 /srv/http/index.html
# echo 'TestMe!' >> /srv/http/index.html

```

修改日志目录权限:

```
# chown -R http:http /var/log/lighttpd

```

启动服务:

```
# systemctl start lighttpd

```

然后就可以使用浏览器打开网址 `localhost` ，你应该能见到测试页面。

开机自动启动:

```
# systemctl enable lighttpd

```

示例配置文件在 `/usr/share/doc/lighttpd/`。

### CGI

[Common Gateway Interface](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface") (CGI) 脚本对于lighttpd可以开箱即用, 你只需要开启CGI模块, 指定配置文件，并确保指定语言的解释器已经安装。 (如：使用python需要安装 [python](https://www.archlinux.org/packages/?name=python))

创建 `/etc/lighttpd/conf.d/cgi.conf` ，添加以下内容:

```
server.modules += ( "mod_cgi" )

cgi.assign                 = ( ".pl"  => "/usr/bin/perl",
                               ".cgi" => "/usr/bin/perl",
                               ".rb"  => "/usr/bin/ruby",
                               ".erb" => "/usr/bin/eruby",
                               ".py"  => "/usr/bin/python",
                               ".php" => "/usr/bin/php-cgi" )

index-file.names           += ( "index.pl",   "default.pl",
                               "index.rb",   "default.rb",
                               "index.erb",  "default.erb",
                               "index.py",   "default.py",
                               "index.php",  "default.php" )

```

对于PHP脚本，请确认在 `/etc/php/php.ini`添加了下列配置：

```
cgi.fix_pathinfo = 1

```

在你的lighttpd配置文件中`/etc/lighttpd/lighttpd.conf`添加：

```
include "conf.d/cgi.conf"

```

### FastCGI

安装 [fcgi](https://www.archlinux.org/packages/?name=fcgi)，之后你的lighttpd就有了fcgi支持， 以下内容是给需要使用Ruby，PHP或者Python的人的指导。

**注意:** lighttpd现在默认以用户 `http` 运行。

首先复制一份默认配置，从 `/usr/share/doc/lighttpd/config/conf.d/fastcgi.conf` 复制到 `/etc/lighttpd/conf.d`

将以下内容添加到 `/etc/lighttpd/conf.d/fastcgi.conf`

```
server.modules += ( "mod_fastcgi" )

#server.indexfiles += ( "dispatch.fcgi" ) #this is deprecated
index-file.names += ( "dispatch.fcgi" ) #dispatch.fcgi if rails specified

server.error-handler-404   = "/dispatch.fcgi" #too
fastcgi.server = (
    ".fcgi" => (
      "localhost" => ( 
        "socket" => "/run/lighttpd/rails-fastcgi.sock",
        "bin-path" => "/path/to/rails/application/public/dispatch.fcgi"
      )
    )
)

```

然后在 `/etc/lighttpd/lighttpd.conf`中添加:

```
include "conf.d/fastcgi.conf"

```

下面是关于PHP和Ruby on Rails的指导。

#### PHP

安装 [php](https://www.archlinux.org/packages/?name=php) 和 [php-cgi](https://www.archlinux.org/packages/?name=php-cgi) (可以参阅 [PHP](/index.php/PHP "PHP") 、 [LAMP](/index.php/LAMP "LAMP")).

确认php-cgi可以工作： `php-cgi --version`

```
PHP 5.4.3 (cgi-fcgi) (built: May  8 2012 17:10:17)
Copyright (c) 1997-2012 The PHP Group
Zend Engine v2.4.0, Copyright (c) 1998-2012 Zend Technologies

```

如果输出内容与上面相仿则php已经正确安装。

创建一份新的配置文件:

 `/etc/lighttpd/conf.d/fastcgi.conf` 

```
# Make sure to install php and php-cgi. See:                                                             
# https://wiki.archlinux.org/index.php/Fastcgi_and_lighttpd#PHP

server.modules += ("mod_fastcgi")

# FCGI server
# ===========
#
# Configure a FastCGI server which handles PHP requests.
#
index-file.names += ("index.php")
fastcgi.server = ( 
    # Load-balance requests for this path...
    ".php" => (
        # ... among the following FastCGI servers. The string naming each
        # server is just a label used in the logs to identify the server.
        "localhost" => ( 
            "bin-path" => "/usr/bin/php-cgi",
            "socket" => "/tmp/php-fastcgi.sock",
            # breaks SCRIPT_FILENAME in a way that PHP can extract PATH_INFO
            # from it 
            "broken-scriptfilename" => "enable",
            # Launch (max-procs + (max-procs * PHP_FCGI_CHILDREN)) procs, where
            # max-procs are "watchers" and the rest are "workers". See:
            # https://redmine.lighttpd.net/projects/1/wiki/frequentlyaskedquestions#How-many-php-CGI-processes-will-lighttpd-spawn 
            "max-procs" => 4, # default value
            "bin-environment" => (
                "PHP_FCGI_CHILDREN" => "1" # default value
            )
        )
    )   
)

```

在/etc/lighttpd/lighttpd.conf中添加以下内容使新配置能够应用:

 `/etc/lighttpd/lighttpd.conf` 

```
include "conf.d/fastcgi.conf"

```

**注意:** 模块顺序十分重要, 正确地模块加载顺序位于 `/usr/share/doc/lighttpd/config/modules.conf`. 任何错误配置都可能导致 _lighttpd_ 崩溃。

重新加载 lighttpd：

1.  systemctl restart lighttpd

**注意:**

*   如果你在访问php文件时遇到诸如 _No input file found_ 的错误, 有很多原因可以导致这个错误，请参阅 [this FAQ](http://redmine.lighttpd.net/projects/1/wiki/frequentlyaskedquestions#I-get-the-error-No-input-file-specified-when-trying-to-use-PHP) 。
*   确认没有其他模块 (如 `mod_cgi`) 负责处理php文件。

##### Using php-fpm

There is no adaptive spawning anymore in recent lighttpd releases. For dynamic management of PHP processes, you can use [php-fpm](https://www.archlinux.org/packages/?name=php-fpm).

```
# pacman -S php-fpm
# rc.d start php-fpm

```

**Note:** You can configure the number of servers in the pool and tweak other configuration options by editing the file `/etc/php/php-fpm.conf`. More details on _php-fpm_ can be found on the [php-fpm website](http://php-fpm.anight.org/). You should also note that when you make changes to /etc/php/php.ini you will need to restart php-fpm

In `/etc/lighttpd/conf.d/fastcgi.conf` add:

```
server.modules += ( "mod_fastcgi" )

index-file.names += ( "index.php" ) 

fastcgi.server = (
    ".php" => (
      "localhost" => ( 
        "socket" => "/run/php-fpm/php-fpm.sock",
        "broken-scriptfilename" => "enable"
      ))
)

```

##### eAccelerator

Install [eaccelerator](https://aur.archlinux.org/packages/eaccelerator/) from the [AUR](/index.php/Arch_User_Repository "Arch User Repository").

Add own config file for eaccelerator:

 `/etc/php/conf.d/eaccelerator-own.ini` 

```
zlib.output_compression = On
cgi.fix_pathinfo=1
eaccelerator.cache_dir="/home/phpuser/eaccelerator/cache"
```

**Tip:** I additionally set `safe_mod` to `On` in my setup, but this is not required.

##### Try a php page

Create the following php page, name it index.php, and place a copy in both /srv/http/ and /srv/http-ssl/html/

```
<?php
phpinfo();
?>

```

Try navigating with a web browser to both the http and https address of your server. You should see the phpinfo page.

Check eaccelerator caching:

```
# ls -l /home/phpuser/eaccelerator/cache

```

If the above command outputs the following:

```
-rw-------  1 phpuser phpuser 456 2005-05-05 14:53 eaccelerator-277.58081
-rw-------  1 phpuser phpuser 452 2005-05-05 14:53 eaccelerator-277.88081

```

Then eaccelerator is happily caching your php scripts to help speed things up.

#### Ruby on Rails

Install and configure FastCGI. (See [#FastCGI](#FastCGI) above.)

Install [ruby](/index.php/Ruby "Ruby") from [extra] and [ruby-fcgi](https://aur.archlinux.org/packages/ruby-fcgi/) from [AUR](/index.php/AUR "AUR").

Follow instructions on [RubyOnRails](/index.php/RubyOnRails "RubyOnRails").

#### Python FastCGI

Install flup

```
# pacman -S python2-flup

```

Configure:

```
fastcgi.server = (
    ".py" =>
    (
        "python-fcgi" =>
        (
        "socket" => "/run/lighttpd/fastcgi.python.socket",
         "bin-path" => "test.py",
         "check-local" => "disable",
         "max-procs" => 1,
        )
    )
)

```

### SSL

Generate an SSL Cert, e.g. like that:

```
# mkdir /etc/lighttpd/certs
# openssl req -x509 -nodes -days 7300 -newkey rsa:2048 -keyout /etc/lighttpd/certs/www.example.com.pem -out /etc/lighttpd/certs/www.example.com.pem
# chmod 600 /etc/lighttpd/certs/www.example.com.pem

```

Edit `/etc/lighttpd/lighttpd.conf`. To make lighttpd SSL-only (you probably need to set the server port to 443 as well)

```
ssl.engine = "enable" 
ssl.pemfile = "/etc/lighttpd/certs/www.example.com.pem"

```

To enable SSL in addition to normal HTTP

```
$SERVER["socket"] == ":443" {
    ssl.engine                  = "enable" 
    ssl.pemfile                 = "/etc/lighttpd/certs/www.example.com.pem" 
 }

```

If you want to serve different sites, you can change the document root inside the socket conditional:

```
$SERVER["socket"] == ":443" {
    server.document-root = "/srv/ssl" # use your ssl directory here
    ssl.engine                 = "enable"
    ssl.pemfile                = "/etc/lighttpd/certs/www.example.com.pem"  # use the path where you created your pem file
 }

```

or as alternative you can use the scheme conditional to distinguish between secure and normal requests.

```
$HTTP["scheme"] == "https" {
    server.document-root = "/srv/ssl" # use your ssl directory here
    ssl.engine                 = "enable"
    ssl.pemfile                = "/etc/lighttpd/certs/www.example.com.pem"  # use the path where you created your pem file
 }

```

Note that you cannot use the scheme conditional around ssl.engine above, since lighttpd needs to know on what port to enable SSL.

##### Server Name Indication

To use [SNI](http://en.wikipedia.org/wiki/Server_Name_Indication) with lighttpd, simply put additional ssl.pemfile configuration directives inside host conditionals. It seems a default ssl.pemfile is still required, though.

```
$HTTP["host"] == "www.example.org" {
        ssl.pemfile = "/etc/lighttpd/certs/www.example.org.pem" 
    }

```

```
$HTTP["host"] == "mail.example.org" {
        ssl.pemfile = "/etc/lighttpd/certs/mail.example.org.pem" 
    }

```

#### Redirect HTTP requests to HTTPS

You should add "mod_redirect" in server.modules array in `/etc/lighttpd/lighttpd.conf`:

```
server.modules              = (
                                     ...
                                "mod_redirect", 
                                     ...
)

```

```
$SERVER["socket"] == ":80" {
  $HTTP["host"] =~ "example.org" {
    url.redirect = ( "^/(.*)" => "[https://example.org/$1](https://example.org/$1)" )
    server.name                 = "example.org" 
  }
}

```

```
$SERVER["socket"] == ":443" {
  ssl.engine = "enable" 
  ssl.pemfile = "/etc/lighttpd/ssl/server.pem" 
  server.document-root = "..." 
}

```

To redirect all hosts to their secure equivalents use the following in place of the socket 80 configuration above:

```
$SERVER["socket"] == ":80" {
  $HTTP["host"] =~ "(.*)" {
    url.redirect = ( "^/(.*)" => "[https://%1/$1](https://%1/$1)" )
  }
}

```

To redirect all hosts for part of the site (e.g. secure or phpmyadmin):

```
$SERVER["socket"] == ":80" {
  $HTTP["url"] =~ "^/secure" {
    url.redirect = ( "^/(.*)" => "[https://example.com/$1](https://example.com/$1)" )
  }
}

```

### Output Compression

In `/etc/lighttpd/lighttpd.conf` add

```
var.cache_dir           = "/var/cache/lighttpd"

```

Then create directory for a compressed files:

```
# mkdir /var/cache/lighttpd/compress
# chown http:http /var/cache/lighttpd/compress

```

Copy example configuration file:

```
# mkdir /etc/lighttpd/conf.d
# cp /usr/share/doc/lighttpd/config/conf.d/compress.conf /etc/lighttpd/conf.d/

```

Add following in `/etc/lighttpd/lighttpd.conf`:

```
include "conf.d/compress.conf"

```

**Note:** You can not do this (copy compress.conf) and add a needed content in `/etc/lighttpd/lighttpd.conf` instead.

## 疑难解答

### 关于Lighttpd下载.php文件的情况

若Lighttpd仅仅是下载`.php`文件而不是去“初始化”它们，那么你可能没把下面的一些设置写入你的配置文件里`/etc/lighttpd/lighttpd.conf`。

```
server.modules = (
                   "mod_fastcgi",
                 )

fastcgi.server = ( ".php" => ((
                     "bin-path" => "/usr/bin/php-cgi", #depends where your php-cgi has been installed. Default here.
                     "socket" => "/tmp/php.socket",
                     "max-procs" => 2,
                     "bin-environment" => (
                       "PHP_FCGI_CHILDREN" => "16",
                       "PHP_FCGI_MAX_REQUESTS" => "10000"
                     ),
                     "bin-copy-environment" => (
                       "PATH", "SHELL", "USER"
                     ),
                     "broken-scriptfilename" => "enable"
                 )))
```

### CCS样式列表无法正确显示

Lighttpd的默认设置是没有包括CSS的媒体类型的，所以标准的浏览器把text/CSS误以为text/html而混淆彼此，最终什么都没有正确的显示出来。要解决这个问题需要在CSS中增加一条说明。

```
mimetype.assign	= (
  ".html" => "text/html",
  ".txt" => "text/plain",
  ".jpg" => "image/jpeg",
  ".png" => "image/png",
  ".css" => "text/css"
)
```

换行不是必须的，仅仅为了可读性。

## 参见

*   [Lighttpd wiki](http://redmine.lighttpd.net/projects/lighttpd/wiki)