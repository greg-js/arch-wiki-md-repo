**Nginx** (读作"engine X") 由Igor Sysoev(俄罗斯)于2005年编写，是一个免费、开源、高性能的HTTP服务器和反向代理，也可以作为一个IMAP/POP3代理服务器。Nginx因为稳定，丰富的功能集，配置简单，资源占用低而闻名世界。

这篇文章描述了如何设置nginx并且如何通过[#FastCGI](#FastCGI)集成[PHP](/index.php/PHP "PHP").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 启动](#启动)
*   [3 配置](#配置)
    *   [3.1 配置例子](#配置例子)
    *   [3.2 通用配置](#通用配置)
        *   [3.2.1 进程和连接](#进程和连接)
        *   [3.2.2 不同用户间的使用](#不同用户间的使用)
        *   [3.2.3 server代码块](#server代码块)
            *   [3.2.3.1 管理服务器入口](#管理服务器入口)
        *   [3.2.4 TLS](#TLS)
        *   [3.2.5 分用户目录](#分用户目录)
    *   [3.3 FastCGI](#FastCGI)
        *   [3.3.1 PHP实现](#PHP实现)
            *   [3.3.1.1 nginx 配置](#nginx_配置)
                *   [3.3.1.1.1 添加到主配置](#添加到主配置)
                *   [3.3.1.1.2 PHP配置文件](#PHP配置文件)
            *   [3.3.1.2 测试配置](#测试配置)
        *   [3.3.2 CGI 实现](#CGI_实现)
            *   [3.3.2.1 fcgiwrap](#fcgiwrap)
                *   [3.3.2.1.1 多个工人线程](#多个工人线程)
            *   [3.3.2.2 nginx配置](#nginx配置)
*   [4 在chroot环境下安装](#在chroot环境下安装)
    *   [4.1 创建必要的设备](#创建必要的设备)
    *   [4.2 创建必要目录](#创建必要目录)
    *   [4.3 填充chroot](#填充chroot)
    *   [4.4 修改nginx.service来开启chroot](#修改nginx.service来开启chroot)
*   [5 建议和技巧](#建议和技巧)
    *   [5.1 使用 systemd无权限运行](#使用_systemd无权限运行)
    *   [5.2 针对systemd的可选脚本](#针对systemd的可选脚本)
    *   [5.3 Nginx Beautifier （nginx美化器）](#Nginx_Beautifier_（nginx美化器）)
    *   [5.4 更好的头文件管理](#更好的头文件管理)
*   [6 故障排除](#故障排除)
    *   [6.1 配置验证](#配置验证)
    *   [6.2 接入本地IP重定向到localhost](#接入本地IP重定向到localhost)
    *   [6.3 Error: The page you are looking for is temporarily unavailable. Please try again later. (502 Bad Gateway)](#Error:_The_page_you_are_looking_for_is_temporarily_unavailable._Please_try_again_later._(502_Bad_Gateway))
    *   [6.4 Error: No input file specified](#Error:_No_input_file_specified)
    *   [6.5 Warning: Could not build optimal types_hash](#Warning:_Could_not_build_optimal_types_hash)
    *   [6.6 不能指定请求地址](#不能指定请求地址)
*   [7 参见](#参见)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 包 [nginx-mainline](https://www.archlinux.org/packages/?name=nginx-mainline) (主线(mainline)分支:新功能，更新，bug解决) 或者 [nginx](https://www.archlinux.org/packages/?name=nginx) (稳定分支: 只是bug解决).

推荐使用主线分支。使用稳定分支的主要原因是担心新功能的造成的不良影响，比如与第三方模块不兼容或者开发者疏忽导致引入[新功能](https://nginx.org/en/download.html)时出现bug.

**Note:** 所有在[official repositories](/index.php/Official_repositories "Official repositories")可用的模块都需要*nginx*(与*nginx-mainline*相反)作为依赖.你可能需要在下决定选*nginx*还是*nginx-mainline*前，先查看下模块名单。*nginx-mainline*的模块能在[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")找到.

对于在基于chroot环境下的额外安全性，可查阅[#Installation in a chroot](#Installation_in_a_chroot).

## 启动

[Start/enable](/index.php/Start/enable "Start/enable") `nginx.service`.

默认在 [http://127.0.0.1](http://127.0.0.1) 页面服务的页面是 `/usr/share/nginx/html/index.html`.

## 配置

安装nginx后的第一步该干什么写在[用户手册](http://nginx.org/en/docs/beginners_guide.html)里了. 你可以通过编辑在`/etc/nginx/`下的文件来修改配置。主配置文件在`/etc/nginx/nginx.conf`.

更多细节和例子，你可以在 [http://wiki.nginx.org/Configuration](http://wiki.nginx.org/Configuration) 和 [官方文档](http://nginx.org/en/docs/)找到.

下面的例子包含了最常见的使用案例.我们假定你使用的是默认文件路径(`/usr/share/nginx/html`). 如果你改了路径，用你自己的路径替代.

### 配置例子

 `/etc/nginx/nginx.conf` 
```
user http;

# May be equal to `grep processor /proc/cpuinfo | wc -l`
worker_processes auto;
worker_cpu_affinity auto;

# PCRE JIT can speed up processing of regular expressions significantly.
pcre_jit on;

events {
    # Should be equal to `ulimit -n`
    worker_connections 1024;

    # Let each process accept multiple connections.
    multi_accept on;

    # Preferred connection method for newer linux versions.
    use epoll;
}

http {
    server_tokens off; # Disables the “Server” response header
    charset utf-8;

    # Sendfile copies data between one FD and other from within the kernel.
    # More efficient than read() + write(), since the requires transferring
    # data to and from the user space.
    sendfile on;

    # Tcp_nopush causes nginx to attempt to send its HTTP response head in one
    # packet, instead of using partial frames. This is useful for prepending
    # headers before calling sendfile, or for throughput optimization.
    tcp_nopush on;

    # Don't buffer data-sends (disable Nagle algorithm). Good for sending
    # frequent small bursts of data in real time.
    #
    tcp_nodelay on;

    # On Linux, AIO can be used starting from kernel version 2.6.22.
    # It is necessary to enable directio, or otherwise reading will be blocking.
    # aio threads;
    # aio_write on;
    # directio 8m;

    # Caches information about open FDs, freqently accessed files.
    # open_file_cache max=200000 inactive=20s;
    # open_file_cache_valid 60s;
    # open_file_cache_min_uses 2;
    # open_file_cache_errors on;

    # http://nginx.org/en/docs/hash.html
    types_hash_max_size 4096;
    include mime.types;
    default_type application/octet-stream;

    # Logging Settings
    access_log off;

    # Gzip Settings
    gzip on;
    gzip_comp_level 6;
    gzip_min_length 500;
    gzip_proxied expired no-cache no-store private auth;
    gzip_vary on;
    gzip_disable "MSIE [1-6]\.";
    gzip_types
        application/atom+xml
        application/javascript
        application/json
        application/ld+json
        application/manifest+json
        application/rss+xml
        application/vnd.geo+json
        application/vnd.ms-fontobject
        application/x-font-ttf
        application/x-web-app-manifest+json
        application/xhtml+xml
        application/xml
        font/opentype
        image/bmp
        image/svg+xml
        image/x-icon
        text/cache-manifest
        text/css
        text/plain
        text/vcard
        text/vnd.rim.location.xloc
        text/vtt
        text/x-component
        text/x-cross-domain-policy;

    # index index.php index.html index.htm;
    include sites-enabled/*; # See Server blocks
}

```

### 通用配置

#### 进程和连接

你应该为`worker_processes`选一个合适的值. 这项设置最终决定了nginx接受多少连接和它会使用多少处理器。通常来说，把它设置成你系统里的硬件线程数就好了。可选的是，自从 1.3.8 和 1.2.5版本以后， `worker_processes` 接受 `auto` 作为值了, 他会自动检测最优值 ([source](http://nginx.org/en/docs/ngx_core_module.html#worker_processes)).

nginx的最大连接数有下面的公式给出`max_clients = worker_processes * worker_connections`.

#### 不同用户间的使用

默认的, [nginx](https://www.archlinux.org/packages/?name=nginx) 用 `root` 身份运行主进程二用`http`用户运行worker进程. 如果要用其它用户运行worker进程, 改变`nginx.conf`里的`user`参数就好了:

 `/etc/nginx/nginx.conf` 
```
user *user* [*group*];

```

如果组（group）忽略不写的话，就会用和*user*相同的名字来代替

**Tip:** 其实也可以使用[systemd](/index.php/Systemd "Systemd")以`root`身份在没有任何东西运行的情况下运行nginx . 可以看 [#使用 systemd无权限运行](#使用_systemd无权限运行).

#### server代码块

通过使用 `server` 模块，可以实现服务多个域名. 这些模块可以类比为[Apache](/index.php/Apache "Apache")中的"VirtualHosts" . 也可查阅 [上游文献](https://www.nginx.com/resources/wiki/start/topics/examples/server_blocks/).

下面的例子，服务器监听IPv4和IPv6的80端口的进入流量的两个域名，分别是`domainname1.dom` 和`domainname2.dom`:

 `/etc/nginx/nginx.conf` 
```
...
server {
        listen 80;
        listen [::]:80;
        server_name domainname1.dom;
        root /usr/share/nginx/domainname1.dom/html;
        location / {
           index index.php index.html index.htm;
        }
}

server {
        listen 80;
        listen [::]:80;
        server_name domainname2.dom;
        root /usr/share/nginx/domainname2.dom/html;
        ...
}
...

```

[Restart](/index.php/Restart "Restart")(重启) `nginx.service` 来让改变的配置生效.

确保主机名是可以被设置好的DNS服务器比如[BIND](/index.php/BIND "BIND") 或者 [dnsmasq](/index.php/Dnsmasq "Dnsmasq")解析的，或者可以查看下[Network configuration#Local network hostname resolution](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration").

##### 管理服务器入口

把不同的`server`模块放到不同的文件里是可能的.这样的话可以让你很轻易的开启和禁用特定的站点.

创建以下文件夹:

```
# mkdir /etc/nginx/sites-available
# mkdir /etc/nginx/sites-enabled

```

在`sites-available`文件夹下创建一个文件包含一个或更多服务器模块:

 `/etc/nginx/sites-available/example` 
```
server {
    ..
}

```

把 `include sites-enabled/*;`放到`http` 模块的末尾:

 `/etc/nginx/nginx.conf` 
```
...
http {
    ...
    include sites-enabled/*;
}
...

```

如果要启用一个 `server` 模块, 只需要简单的创建一个符号链接:

```
# ln -s /etc/nginx/sites-available/example /etc/nginx/sites-enabled/example

```

如果要移除一个 `server`:

```
# unlink /etc/nginx/sites-enabled/example

```

[Reload](/index.php/Reload "Reload")/[restart](/index.php/Restart "Restart") `nginx.service` 来让配置生效.

#### TLS

[OpenSSL](/index.php/OpenSSL "OpenSSL") 提供了TLS支持并且默认在Arch系统安装时安装了.

**Tip:**

*   你可能需要在配置SSL之前阅读 [ngx_http_ssl_module](http://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl_certificate) 的文档.
*   [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt") 时一个免费的、自动的、开放的证书颁发机构.有一个插件可以从茉莉花请求有效的证书并自动配置的.
*   Mozilla有一篇有用的 [TLS文章](https://wiki.mozilla.org/Security/Server_Side_TLS "mozillawiki:Security/Server Side TLS")，也有一个[自动化工具](https://mozilla.github.io/server-side-tls/ssl-config-generator/)来创建一个更安全的配置.
*   [Cipherli.st](https://cipherli.st) 为大多数现代web服务器提供了强大的 TLS 实现例子和教程.

**Warning:** 如果你打算实现TLS, 你必须知道一些变化和实现 [仍然被攻击时很脆弱](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS.2FSSL "wikipedia:Transport Layer Security")[[1]](https://weakdh.org/#affected). 如果想知道TLS内现存的漏洞和怎样用合适的方法到nginx上，可访问 [https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html)

创建一个私钥和自签名的证书，这对大多数不需要 [CSR](/index.php/OpenSSL#Generate_a_certificate_signing_request "OpenSSL")的安装来说足够了:

```
# mkdir /etc/nginx/ssl
# cd /etc/nginx/ssl
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout server.key -out server.crt -days 1095
# chmod 400 server.key
# chmod 444 server.crt

```

**Note:** `-days` 是可选的并且RSA键大小最低可到2048 (默认值).

如果你需要创建一个CSR, 用下面的教程而不是上面的:

```
# mkdir /etc/nginx/ssl
# cd /etc/nginx/ssl
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:4096 -out server.key
# chmod 400 server.key
# openssl req -new -sha256 -key server.key -out server.csr
# openssl x509 -req -days 1095 -in server.csr -signkey server.key -out server.crt

```

**Note:** 如果你需要更多的 *openssl*选项, 可以阅读它们的 [手册](https://www.openssl.org/docs/apps/openssl.html) 或者读它们的[扩展文档](https://www.openssl.org/docs/).

使用TLS的 `/etc/nginx/nginx.conf` 的基本例子:

 `/etc/nginx/nginx.conf` 
```
http {
    ...
    ssl_ciphers "EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH";
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ..

    # Redirect to HTTPS
    server {
        listen 80;
        server_name localhost;
        return 301 https://$host$request_uri;
    }

    server {
        #listen 80; # Uncomment to also listen for HTTP requests
        listen 443 ssl http2; # HTTP/2 is only possible when using SSL
        server_name localhost;

        ssl_certificate ssl/server.crt;
        ssl_certificate_key ssl/server.key;

        root /usr/share/nginx/html;
        location / {
            index index.html index.htm;
        }
    }
}

```

[Restart](/index.php/Restart "Restart") `nginx.service` 来让配置生效.

#### 分用户目录

如果要复制Apache式的 `~user` URLs 到用户的 `~/public_html` 目录, 可以尝试下面的. (Note: 如果下面的两个规则都用了的话一定要把更清楚地PHP规则放在前面.)

 `/etc/nginx/nginx.conf` 
```
...
server {
    ...
    # PHP in user directories, e.g. http://example.com/~user/test.php
    location ~ ^/~(.+?)(/.+\.php)$ {
        alias          /home/$1/public_html$2;
        fastcgi_pass   unix:/run/php-fpm/php-fpm.sock;
        fastcgi_index  index.php;
        include        fastcgi.conf;
    }

    # User directories, e.g. http://example.com/~user/
    location ~ ^/~(.+?)(/.*)?$ {
        alias     /home/$1/public_html$2;
        index     index.html index.htm;
        autoindex on;
    }
    ...
}
...

```

查阅 [#PHP实现](#PHP实现) 来阅读更多 `nginx`的PHP配置.

重启 `nginx.service` 来启用新配置.

### FastCGI

[FastCGI](https://en.wikipedia.org/wiki/FastCGI "wikipedia:FastCGI"), 也叫 FCGI, 是适用于web服务器和交互式程序的接口的协议. FastCGI 是早期的 [Common Gateway Interface](https://en.wikipedia.org/wiki/Common_Gateway_Interface "wikipedia:Common Gateway Interface") (CGI)的变种; FastCGI的主要目的是减少CGI程序和web服务器交互的开销,来允许服务器同时处理更多网页请求.

FastCGI技术被引进nginx是为了与许多外部工具，比如. [Perl](/index.php/Perl "Perl"), [PHP](/index.php/PHP "PHP") and [Python](/index.php/Python "Python")

#### PHP实现

[PHP-FPM](https://php-fpm.org/) 是建议使用的用作[PHP](/index.php/PHP "PHP")的FastCGI服务器的解决方案.

[Install](/index.php/Install "Install")（安装） [php-fpm](https://www.archlinux.org/packages/?name=php-fpm) 然后确保 [PHP](/index.php/PHP "PHP") 被安装配置正确. PHP-FPM的主要配置文件是 `/etc/php/php-fpm.conf`. 基础使用的话默认配置就足够了.

最后, [enable](/index.php/Enable "Enable") 和 [start](/index.php/Start "Start") `php-fpm.service`.

**Note:**

*   如果你 [用不同的用户运行nginx](#不同用户间的使用), 确保PHP-FPM套接字文件能被这个用户访问，或者通过一个TCP套接字.
*   如果你在chroot的环境下运行nginx (chroot 是 `/srv/nginx-jail`, web页面在 `/srv/nginx-jail/www`), 你必须修改文件 `/etc/php/php-fpm.conf` ，把 `chroot /srv/nginx-jail` 和 `listen = /srv/nginx-jail/run/php-fpm/php-fpm.sock` 两行加入到指令部分 (默认是`[www]`). 如果缺少的话请为套接字文件创建目录。此外, 动态链接到依赖的模块，你需要将这些依赖复制到(比如. 对于php-imagick, 你需要复制ImageMagic的库复制到chroot, 而不是imagick.so他自己).

##### nginx 配置

###### 添加到主配置

当服务一个PHP web程序时，一个PHP-FPM的`location`应该包括在 [#server代码块](#server代码块)里 [[2]](https://www.nginx.com/resources/wiki/start/topics/examples/phpfcgi/),比如.:

 `/etc/nginx/sites-available/example` 
```
server {
    ...

    root /usr/share/nginx/html;
    location / {
        index index.html index.htm;
    }

    location ~ [^/]\.php(/|$) {
        # Correctly handle request like /test.php/foo/blah.php or /test.php/
        fastcgi_split_path_info ^(.+?\.php)(/.*)$;

        try_files $uri $document_root$fastcgi_script_name =404;

        # Mitigate https://httpoxy.org/ vulnerabilities
        fastcgi_param HTTP_PROXY "";

        fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}

```

如果需要用PHP处理其他文件扩展名 (比如. *.html* and *.htm*):

```
location ~ [^/]\.php**|html|htm**(/|$) {
    ...
}

```

非 *.php* 的PHP-FPM扩展处理都需要被直接加入到 `/etc/php/php-fpm.d/www.conf`:

```
security.limit_extensions = .php .html .htm

```

**Note:** 需要注意下 `fastcgi_pass` 参数, 因为它被选定的FastCGI服务器在它的配置文件里定义TCP或Unix套接字. 对应`php-fpm`的**default** (Unix) 套接字是 是:
```
fastcgi_pass unix:/run/php-fpm/php-fpm.sock;

```

你可能想要使用常见的 TCP 套接字, **not default**,

```
fastcgi_pass 127.0.0.1:9000;

```
Unix 的域名套接字应该会快一点.

###### PHP配置文件

如果你使用多个 `server` 块来启用PHP支持, 创建一个PHP配置文件可能更简单:

 `/etc/nginx/php.conf` 
```
location ~ \.php$ {
    ...
}

```

为特定的服务器启用PHP支持, 只需要简单的加入 `include php.conf`就好了:

 `/etc/nginx/nginx.conf` 
```
server {
    server_name example.com;
    ...
    include php.conf;
}

```

##### 测试配置

你需要[restart](/index.php/Restart "Restart") `php-fpm.service` 和 `nginx.service` 服务单元来让配置生效，如果配置之前被改变过的话.

测试FastCGI实现, 在`root`目录下创建一个新的PHP文件，内容是:

```
<?php phpinfo(); ?>

```

把这个文件用浏览器打开，你应该就可以看到现在的PHP配置的信息页了.

#### CGI 实现

这个实现是CGI程序所需要的.

##### fcgiwrap

[Install](/index.php/Install "Install") [fcgiwrap](https://www.archlinux.org/packages/?name=fcgiwrap). 配置文件是 `/usr/lib/systemd/system/fcgiwrap.socket`. [Enable](/index.php/Enable "Enable") 并且 [start](/index.php/Start "Start") `fcgiwrap.socket`.

###### 多个工人线程

如果你想生成多个工人线程建议你使用[multiwatch](https://aur.archlinux.org/packages/multiwatch/), 它会处理崩溃的子进程. 如果你需要使用`spawn-fcgi` 来创建Unix套接字,因为multiwatch无法处理systemd创建的套接字，尽管fcgiwarp它自己在单元文件中直接调用页没有任何问题.

从 `/usr/lib/systemd/system/fcgiwrap.service` 复制单元文件到 `/etc/systemd/system/fcgiwrap.service` (和`fcgiwrap.socket` 单元, 如果存在的话), 修改`ExecStart`行到满足你需要的地方. 下面是使用[multiwatch](https://aur.archlinux.org/packages/multiwatch/)的单元文件. 确保`fcgiwrap.socket` 没有被start（开始）或enable（启用）, 因为他会和这些单元冲突:

 `/etc/systemd/system/fcgiwrap.service` 
```
[Unit]
Description=Simple CGI Server
After=nss-user-lookup.target

[Service]
ExecStartPre=/bin/rm -f /run/fcgiwrap.socket
ExecStart=/usr/bin/spawn-fcgi -u http -g http -s /run/fcgiwrap.sock -n -- /usr/bin/multiwatch -f 10 -- /usr/sbin/fcgiwrap
ExecStartPost=/usr/bin/chmod 660 /run/fcgiwrap.sock
PrivateTmp=true
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

可以自定义 `-f 10` 来改变生成的子进程的数量.

**Warning:** `ExecStartPost`行是需要的，因为当为`spawn-fcgi`使用`-M 660`参数选项时会出现奇怪的情况.这有可能是一个Bug

##### nginx配置

在每个服务了一个CGI程序的`server` 块内都应该有一个像下面的 `location` 块:

```
location ~ \.cgi$ {
     root           /path/to/server/cgi-bin;
     fastcgi_pass   unix:/run/fcgiwrap.sock;
     include        fastcgi.conf;
}

```

```
`fcgiwrap` 的默认套接字文件是 `/run/fcgiwrap.sock`.

```

如果你一直出现 `502 - bad Gateway` 错误,你应该检查你的CGI程序是否宣告了下面内容的mime类型。如果是html，他应该是`Content-type: text/html`.

## 在chroot环境下安装

在[chroot](/index.php/Chroot "Chroot")环境里运行nginx是有一个额外的安全层的.为了最大化安全性chroot环境应该只包括nginx服务器需要的文件，并且所有的文件都应该尽可能有严格的权限，比如像`/usr/bin`这样的文件夹应该不可读和不可写.

Arch默认有一个`http`用户和组来运行服务器chroot将会在`/srv/http`.

创建这个监狱（指chroot环境）的Perl脚本能在[jail.pl gist](https://gist.github.com/4365696)找到. 你可以直接用那个脚本或者跟着这篇文章的指示继续阅读下去. 它应该用root运行. 你需要在它起作用之前取消一行注释.

### 创建必要的设备

nginx需要 `/dev/null`, `/dev/random`, 和 `/dev/urandom`. 为了安装这些需要在chroot环境下创建 `/dev/` 目录和用*mknod*添加设备尽量别挂载所有的`/dev/`来确保, 尽管在chroot受到攻击的情况下, 攻击者必须突破chroot来获取像`/dev/sda1`的重要文件.

**Tip:** 确保 `/srv/http` 挂载了并且没有nodev选项

**Tip:** 查看 [mknod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mknod.1) 和 `ls -l /dev/{null,random,urandom}` 来更好的理解*mknod*选项.

```
# export JAIL=/srv/http
# mkdir $JAIL/dev
# mknod -m 0666 $JAIL/dev/null c 1 3
# mknod -m 0666 $JAIL/dev/random c 1 8
# mknod -m 0444 $JAIL/dev/urandom c 1 9

```

### 创建必要目录

nginx需要大量文件来运转正常. 在把它们拷贝过去之前创建一个文件夹来存储它们。假设你的nginx文档目录在 `/srv/http/www`.

```
# mkdir -p $JAIL/etc/nginx/logs
# mkdir -p $JAIL/usr/{lib,bin}
# mkdir -p $JAIL/usr/share/nginx
# mkdir -p $JAIL/var/{log,lib}/nginx
# mkdir -p $JAIL/www/cgi-bin
# mkdir -p $JAIL/{run,tmp}
# cd $JAIL; ln -s usr/lib lib
# cd $JAIL; ln -s usr/lib lib64
# cd $JAIL/usr; ln -s lib lib64

```

然后挂载 `$JAIL/tmp` 和 `$JAIL/run` 作为tmpfs. 大小应该限制确保攻击者无法吃掉所有的内存.

```
# mount -t tmpfs none $JAIL/run -o 'noexec,size=1M'
# mount -t tmpfs none $JAIL/tmp -o 'noexec,size=100M'

```

为了在重启后保留挂载，下面的入口应该被添加到`/etc/fstab`:

 `/etc/fstab` 
```
 tmpfs   /srv/http/run   tmpfs   rw,noexec,relatime,size=1024k   0       0
 tmpfs   /srv/http/tmp   tmpfs   rw,noexec,relatime,size=102400k 0       0

```

### 填充chroot

首先把简单的文件复制过去.

```
# cp -r /usr/share/nginx/* $JAIL/usr/share/nginx
# cp -r /usr/share/nginx/html/* $JAIL/www
# cp /usr/bin/nginx $JAIL/usr/bin/
# cp -r /var/lib/nginx $JAIL/var/lib/nginx

```

然后复制必要的库过去。使用*ldd*来把它们列出来然后复制到正确的地方。最好是复制而不是链接来确保就算攻击者获取的写权限也服务法修改真实的系统文件.

 `$ ldd /usr/bin/nginx` 
```
linux-vdso.so.1 (0x00007fffc41fe000)
libpthread.so.0 => /usr/lib/libpthread.so.0 (0x00007f57ec3e8000)
libcrypt.so.1 => /usr/lib/libcrypt.so.1 (0x00007f57ec1b1000)
libstdc++.so.6 => /usr/lib/libstdc++.so.6 (0x00007f57ebead000)
libm.so.6 => /usr/lib/libm.so.6 (0x00007f57ebbaf000)
libpcre.so.1 => /usr/lib/libpcre.so.1 (0x00007f57eb94c000)
libssl.so.1.0.0 => /usr/lib/libssl.so.1.0.0 (0x00007f57eb6e0000)
libcrypto.so.1.0.0 => /usr/lib/libcrypto.so.1.0.0 (0x00007f57eb2d6000)
libdl.so.2 => /usr/lib/libdl.so.2 (0x00007f57eb0d2000)
libz.so.1 => /usr/lib/libz.so.1 (0x00007f57eaebc000)
libGeoIP.so.1 => /usr/lib/libGeoIP.so.1 (0x00007f57eac8d000)
libgcc_s.so.1 => /usr/lib/libgcc_s.so.1 (0x00007f57eaa77000)
libc.so.6 => /usr/lib/libc.so.6 (0x00007f57ea6ca000)
/lib64/ld-linux-x86-64.so.2 (0x00007f57ec604000)
```

对于 `/usr/lib` 你可以使用下面的命令:

```
# cp $(ldd /usr/bin/nginx | grep /usr/lib | sed -sre 's/(.+)(\/usr\/lib\/\S+).+/\2/g') $JAIL/usr/lib

```

用下面的命令来复制 `ld-linux-x86-64.so`:

```
# cp /lib64/ld-linux-x86-64.so.2 $JAIL/lib

```

**Note:** 不要尝试复制 `linux-vdso.so`: 他不是真实存在的库，不在`/usr/lib`文件夹里.

复制一些复杂但必要的库和系统文件.

```
# cp /usr/lib/libnss_* $JAIL/usr/lib
# cp -rfvL /etc/{services,localtime,nsswitch.conf,nscd.conf,protocols,hosts,ld.so.cache,ld.so.conf,resolv.conf,host.conf,nginx} $JAIL/etc

```

为chroot创建严格的 user/group文件. 这样只有chroot正常工作所需要的用户才会被chroot知道，其他的users/groups并不会被泄露给攻击者，如果他们已经获取chroot权限的话.

 `$JAIL/etc/group` 
```
http:x:33:
nobody:x:99:

```
 `$JAIL/etc/passwd` 
```
http:x:33:33:http:/:/bin/false
nobody:x:99:99:nobody:/:/bin/false

```
 `$JAIL/etc/shadow` 
```
http:x:14871::::::
nobody:x:14871::::::

```
 `$JAIL/etc/gshadow` 
```
http:::
nobody:::

```

```
# touch $JAIL/etc/shells
# touch $JAIL/run/nginx.pid

```

最后设置权限。应该尽可能把权限设置为不可写 be owned by root and set unwritable.

```
# chown -R root:root $JAIL/

# chown -R http:http $JAIL/www
# chown -R http:http $JAIL/etc/nginx
# chown -R http:http $JAIL/var/{log,lib}/nginx
# chown http:http $JAIL/run/nginx.pid

# find $JAIL/ -gid 0 -uid 0 -type d -print | xargs chmod -rw
# find $JAIL/ -gid 0 -uid 0 -type d -print | xargs chmod +x
# find $JAIL/etc -gid 0 -uid 0 -type f -print | xargs chmod -x
# find $JAIL/usr/bin -type f -print | xargs chmod ug+rx
# find $JAIL/ -group http -user http -print | xargs chmod o-rwx
# chmod +rw $JAIL/tmp
# chmod +rw $JAIL/run

```

如果你的端口绑定为 80 (或者其他在 [1-1023]范围内的端口),给chroot无需root就可绑定的权限.

```
# setcap 'cap_net_bind_service=+ep' $JAIL/usr/bin/nginx

```

### 修改nginx.service来开启chroot

在修改`nginx.service`单元文件之前, 把它复制进 `/etc/systemd/system/` 因为这里的单元文件的优先级比 `/usr/lib/systemd/system/`高. 这样更新nginx救护不爱修改你自定义的 *.service* 文件.

```
# cp /usr/lib/systemd/system/nginx.service /etc/systemd/system/nginx.service

```

systemd单元必须在开启chroot里的nginx之前修改，以http用户的身份，将pid文件放到chroot里.

**Note:** 我不确定pid文件是否需要被放到chroot里.
 `/etc/systemd/system/nginx.service` 
```
 [Unit]
 Description=A high performance web server and a reverse proxy server
 After=syslog.target network.target

 [Service]
 Type=forking
 PIDFile=/srv/http/run/nginx.pid
 ExecStartPre=/usr/bin/chroot --userspec=http:http /srv/http /usr/bin/nginx -t -q -g 'pid /run/nginx.pid; daemon on; master_process on;'
 ExecStart=/usr/bin/chroot --userspec=http:http /srv/http /usr/bin/nginx -g 'pid /run/nginx.pid; daemon on; master_process on;'
 ExecReload=/usr/bin/chroot --userspec=http:http /srv/http /usr/bin/nginx -g 'pid /run/nginx.pid; daemon on; master_process on;' -s reload
 ExecStop=/usr/bin/chroot --userspec=http:http /srv/http /usr/bin/nginx -g 'pid /run/nginx.pid;' -s quit

 [Install]
 WantedBy=multi-user.target
```

**Note:** 用pacman升级nginx并不会升级chroot里的nginx。如果你要升级的话可能需要手动重复上面的步骤。不要忘记更新它链接的库.

你现在可以安全的写在非chroot环境下的nginx安装.

```
# pacman -Rsc nginx

```

如果你不移除非chroot环境的nginx安装，你可能想要确认运行的nginx是不是chroot环境里的, 你可以查询 `/proc/*PID*/root` 链接到哪里. 如果链接到 `/srv/http` 而不是`/`那运行的就是chroot环境下的nginx.

```
# ps -C nginx | awk '{print $1}' | sed 1d | while read -r PID; do ls -l /proc/$PID/root; done

```

## 建议和技巧

### 使用 [systemd](/index.php/Systemd "Systemd")无权限运行

[编辑 nginx.service](/index.php/Systemd#Editing_provided_units "Systemd") 并在 `[Service]`下设置 `User`，还可可选的设置 `Group` :

 `/etc/systemd/system/nginx.service.d/user.conf` 
```
[Service]
User=*user*
Group=*group*
```

我们可以通过强化服务以防止提升特权:

 `/etc/systemd/system/nginx.service.d/user.conf` 
```
[Service]
...
NoNewPrivileges=yes
```

**Tip:** 查看 [systemd.exec(5)](http://www.freedesktop.org/software/systemd/man/systemd.exec.html#User=) 获取更多限权选项.

然后我们需要确保 `*user*`（即前面设置的用户）有权限做它需要做的事:

	Port

	Linux默认不允许非`root`用户的进程绑定低于1024的端口，高于1024的端口可以用: `/etc/nginx/nginx.conf` 
```
server {
        listen 8080;
}

```

**Tip:** 如果你想nginx可以访问80或者443端口，配置你的[firewall](/index.php/Firewall "Firewall")（防火墙）来重定向从80或者443的请求刀nginx监听的端口.

	或者你可以提升nginx进程的CAP_NET_BIND_SERVICE权限，它能允许绑定低于1024的端口: `/etc/systemd/system/nginx.service.d/user.conf` 
```
[Service]
...
CapabilityBoundingSet=
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
AmbientCapabilities=
AmbientCapabilities=CAP_NET_BIND_SERVICE
```

	PID文件

	[nginx](https://www.archlinux.org/packages/?name=nginx) 默认使用 `/run/nginx.pid` . 我们可以创建一个文件夹，*user*有写权限，然后八我们的PID文件放到那里. 一个使用[systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd")的例子: `/etc/tmpfiles.d/nginx.conf`  `d /run/nginx 0775 root *group* - -` 

运行配置:

```
# systemd-tmpfiles --create

```

基于最初的`nginx.service`[Edit](/index.php/Edit "Edit")（编辑）PID的值:

 `/etc/systemd/system/nginx.service.d/user.conf` 
```
[Service]
...
PIDFile=/run/nginx/nginx.pid
ExecStart=
ExecStart=/usr/bin/nginx -g 'pid /run/nginx/nginx.pid; error_log stderr;' 
ExecReload=
ExecReload=/usr/bin/nginx -s reload -g 'pid /run/nginx/nginx.pid;'
```

	`/var/lib/nginx/*`

	一些`/var/lib/nginx`下面的目录需要被以 `root` 运行的nginx的引导. 所以有必要启动整个服务器老这么做, nginx会在一次简单的 [#配置验证](#配置验证)之后自己这么做. 所以只要运行这些中的一个就好啦.

	日志文件& 目录权限

	运行配置测试的步骤会创建一个悬空的`root`拥有的日志文件. 移除`/var/log/nginx`下面的日志文件开始刷新.

	启用nginx服务的用户需要`/var/log/nginx`的写权限. 这可能需要 [改变权限](/index.php/File_permissions_and_attributes#Changing_permissions "File permissions and attributes") 和/或 你系统这个目录的所有权.

现在一切都好了。开始[start](/index.php/Start "Start")（启动） nginx, 然后就可以想用你的非root下的nginx了.

**Tip:** 同样的配置可能还要针对你的 [FastCGI server](#FastCGI) 再做一次.

### 针对systemd的可选脚本

在纯systemd的情况下，你可以享受chroot + systemd的好处. [[3]](http://0pointer.de/blog/projects/changing-roots.html) 基于在下面的文件设置 [用户组](http://wiki.nginx.org/CoreModule#user)一个 pid :

 `/etc/nginx/nginx.conf` 
```
user http;
pid /run/nginx.pid;
```

文件的就绝对路径是`/srv/http/etc/nginx/nginx.conf`.

 `/etc/systemd/system/nginx.service` 
```
[Unit]
Description=nginx (Chroot)
After=syslog.target network.target

[Service]
Type=forking
PIDFile=/srv/http/run/nginx.pid
RootDirectory=/srv/http
ExecStartPre=/usr/sbin/nginx -t -c /etc/nginx/nginx.conf
ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf
ExecReload=/usr/sbin/nginx -c /etc/nginx/nginx.conf -s reload
ExecStop=/usr/sbin/nginx -c /etc/nginx/nginx.conf -s stop

[Install]
WantedBy=multi-user.target
```

没必要设置默认路径，nginx默认加载 `-c /etc/nginx/nginx.conf`,二这也是一个好主意.

作为可选项，你可以在chroot环境下**仅仅**运行 `ExecStart`，`RootDirectoryStartOnly`参数要调成，查看 `yes` [systemd服务手册](http://www.freedesktop.org/software/systemd/man/systemd.service.html) 或者在挂载点生效前启用它，或者一个 [systemd路径](http://www.freedesktop.org/software/systemd/man/systemd.path.html)也行.

 `/etc/systemd/system/nginx.path` 
```
[Unit]
Description=nginx (Chroot) path
[Path]
PathExists=/srv/http/site/Public_html
[Install]
WantedBy=default.target
```

[Enable](/index.php/Enable "Enable")（启用）创建的`nginx.path` 然后把 `/etc/systemd/system/nginx.service`里的`WantedBy=default.target` 变成 `WantedBy=nginx.path` .

单元文件里的`PID文件`允许systemd监控进程(需要绝对路径). 如果这不是你想要的, 你可以改变默认的“一击”类型, 然后删除单元文件里的参照.

### Nginx Beautifier （nginx美化器）

[nginxbeautifier](https://aur.archlinux.org/packages/nginxbeautifier/) 是一个命令行工具，用来美化和格式化nginx配置文件.

### 更好的头文件管理

Nginx有一个非常不直观的头文件管理系统，头文件只能在一个上下文中定义, 任何其它的头文件都会被忽略. 为了补救这个，我们可以安装 [headers-more-nginx](https://github.com/openresty/headers-more-nginx-module#more_set_headers) 模块.

[Install](/index.php/Install "Install") （安装） [nginx-mod-headers-more](https://www.archlinux.org/packages/?name=nginx-mod-headers-more) 包. 这样会把模块安装到`/usr/lib/nginx/modules` 目录下.

如果要加载模块把下面加入到你的nginx配置文件的第一行.

 `/etc/nginx/nginx.conf` 
```
load_module "/usr/lib/nginx/modules/ngx_http_headers_more_filter_module.so";
...
```

## 故障排除

### 配置验证

```
# nginx -t

```

```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

```

### 接入本地IP重定向到localhost

Arch Linux [论坛](https://bbs.archlinux.org/viewtopic.php?pid=780561#p780561)的解决方案.

在 `/etc/nginx/nginx.conf`有一行`server_name localhost` ，前面没有 `#`, 把下面的加入到这一行之下:

```
server_name_in_redirect off;

```

默认行为事nginx将任何请求重定向到配置里`server_name`给定的值里.

### Error: The page you are looking for is temporarily unavailable. Please try again later. (502 Bad Gateway)

这是因为FastCGI服务器还没有开启，或者套接字有错误的权限.

试一试 [这个回答](https://stackoverflow.com/questions/4252368/nginx-502-bad-gateway/16497957#16497957) 来解决502问题.

在Archlinux, 上面提到的配置文件在 `/etc/php/php-fpm.conf`.

### Error: No input file specified

1\. 确定`/etc/php/php.ini`里的 `open_basedir`变量包含正确的路径，要和 `nginx.conf` (通常在`/usr/share/nginx/`)里的`root`变量一致. 当使用[PHP-FPM](http://php-fpm.org/) 作为PHP的FastCGI服务器时, 你可以添加 `fastcgi_param PHP_ADMIN_VALUE "open_basedir=$document_root/:/tmp/:/proc/";` 到`nginx.conf`里的 `location` 代码块里，它能处理PHP文件.

2\. 另一种情况是, `nginx.conf`文件里，`location ~ \.php$`代码块里的错误的 `root` 变量. 确保`root` 指向相同服务器里的`location /`的同样的目录. 或者你直接把root设为全局，不要把它定义到任何地方

3\. 检查权限: 比如. `http` 是用户/组, `755` 是目录权限，`644` 是文件权限. 记住，到`html`目录的路径目录也必须有相同的权限. 可以查看 [File permissions and attributes#Bulk chmod](/index.php/File_permissions_and_attributes#Bulk_chmod "File permissions and attributes") 来批量修改大量文件夹的权限.

4\. 你没有让 `SCRIPT_FILENAME` 包含你脚本的全部路径. 如果nginx的配置 (`fastcgi_param SCRIPT_FILENAME`) 是对的的话, 这种错误意味着PHP无法加载请求的脚本. 通常它知识简单的权限问题, 你可以用root运行php-cgi:

```
# spawn-fcgi -a 127.0.0.1 -p 9000 -f /usr/bin/php-cgi

```

或者你应该创建一个组和用户来开启php-cgi:

```
# groupadd www
# useradd -g www www
# chmod +w /srv/www/nginx/html
# chown -R www:www /srv/www/nginx/html
# spawn-fcgi -a 127.0.0.1 -p 9000 -u www -g www -f /usr/bin/php-cgi

```

5\. 如果你是在chroot的环境下的nginx运行php-fpm，确保`/etc/php-fpm/php-fpm.d/www.conf`里的`chroot` 设置正确(或者 `/etc/php-fpm/php-fpm.conf` 如果是旧版本的话)

### Warning: Could not build optimal types_hash

当开启 `nginx.service`, 进程可能会有下面的日志信息:

```
[warn] 18872#18872: could not build optimal types_hash, you should increase either types_hash_max_size: 1024 or types_hash_bucket_size: 64; ignoring types_hash_bucket_size

```

解决这个警告, 提升`http`代码块的下面的键的值 [[4]](http://nginx.org/en/docs/http/ngx_http_core_module.html#types_hash_max_size) [[5]](http://nginx.org/en/docs/http/server_names.html):

 `/etc/nginx/nginx.conf` 
```
http {
    types_hash_max_size 4096;
    server_names_hash_bucket_size 128;
    ...
}

```

### 不能指定请求地址

来自`systemctl status nginx.service`的全部错误是

```
[emerg] 460#460: bind() to A.B.C.D:443 failed (99: Cannot assign requested address)

```

尽管,你的单元文件配置为用systemd运行在 `network.target` , nginx可能还是企图监听一个配置了但没添加到任何接口的地址. 确保这种情况下手动[start](/index.php/Start "Start") （启动） nginx (从而确保IP地址配置正确). 配置 nginx监听任何地址都会解决这个问题. 如果你的情况是需要监听特定的地址, 一个可能的解决方案是重新配置systemd.

在所有网络配置工作和指定IP地址都结束后开启nginx, 在`nginx.service`里附加 `network-online.target` 到 `After=` 然后 [start/enable](/index.php/Start/enable "Start/enable") `systemd-networkd-wait-online.service`.

## 参见

*   [WebDAV with nginx](/index.php/WebDAV#Nginx "WebDAV")
*   [nginx configuration pitfalls](https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/)
*   [Very good in-depth 2014 look at nginx security and Reverse Proxying](https://calomel.org/nginx.html)
*   [Installing LEMP (nginx, PHP, MySQL with MariaDB engine and PhpMyAdmin) in Arch Linux](http://www.tecmint.com/install-nginx-php-mysql-with-mariadb-engine-and-phpmyadmin-in-arch-linux/)
*   [Using SSL certificates generated with Let's Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt")