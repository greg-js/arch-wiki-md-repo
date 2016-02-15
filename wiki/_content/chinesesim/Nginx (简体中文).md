**Nginx** (读作"engine X") 由Igor Sysoev(俄罗斯)于2005年编写，是一个免费、开源、高性能的HTTP服务器和反向代理，也可以作为一个IMAP/POP3代理服务器。根据 Netcraft 的 _[April 2015 Web Server Survey](http://news.netcraft.com/archives/2015/04/20/april-2015-web-server-survey.html)_, 现在全世界14.48%的网站使用Nginx，而[Apache](/index.php/Apache "Apache")占38.39%。Nginx因为稳定，丰富的功能集，配置简单，资源占用低而闻名世界。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动服务](#.E5.90.AF.E5.8A.A8.E6.9C.8D.E5.8A.A1)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 FastCGI](#FastCGI)
        *   [3.1.1 PHP 集成](#PHP_.E9.9B.86.E6.88.90)
            *   [3.1.1.1 第一步: PHP 配置](#.E7.AC.AC.E4.B8.80.E6.AD.A5:_PHP_.E9.85.8D.E7.BD.AE)
            *   [3.1.1.2 第二步: php-fpm](#.E7.AC.AC.E4.BA.8C.E6.AD.A5:_php-fpm)
            *   [3.1.1.3 第三步: Nginx 配置](#.E7.AC.AC.E4.B8.89.E6.AD.A5:_Nginx_.E9.85.8D.E7.BD.AE)
    *   [3.2 安装 phpMyAdmin](#.E5.AE.89.E8.A3.85_phpMyAdmin)
*   [4 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [4.1 访问本地的IP重定向到本地主机](#.E8.AE.BF.E9.97.AE.E6.9C.AC.E5.9C.B0.E7.9A.84IP.E9.87.8D.E5.AE.9A.E5.90.91.E5.88.B0.E6.9C.AC.E5.9C.B0.E4.B8.BB.E6.9C.BA)
    *   [4.2 Error: 403 (Permission error)](#Error:_403_.28Permission_error.29)
    *   [4.3 Error: The page you are looking for is temporarily unavailable. Please try again later.](#Error:_The_page_you_are_looking_for_is_temporarily_unavailable._Please_try_again_later.)
    *   [4.4 Error: No input file specified](#Error:_No_input_file_specified)
*   [5 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")位于[官方仓库](/index.php/%E5%AE%98%E6%96%B9%E4%BB%93%E5%BA%93 "官方仓库")的[nginx](https://www.archlinux.org/packages/?name=nginx) 软件包。

```
# pacman -S nginx

```

针对 **Ruby on Rails** 的安装参见 [The Perfect Rails Setup](/index.php/RubyOnRails#Option_C:_The_Perfect_Rails_Setup "RubyOnRails").

## 启动服务

要启动Nginx服务,运行以下命令:

```
# systemctl start nginx

```

要Nginx服务开机时启动,运行以下命令:

```
# systemctl enable nginx

```

[http://127.0.0.1](http://127.0.0.1) 的默认页面是:

```
/usr/share/nginx/html/index.html

```

## 配置

你可以修改在`/etc/nginx/`目录中的文件来更改配置.`/etc/nginx/nginx.conf`是主配置文件.更多的细节可以参考[Nginx 配置范例](http://wiki.nginx.org/NginxConfiguration).

### FastCGI

FastCGI，也称为FCGI，是一个外部服务与Web服务器的接口协议。FastCGI是早期的通用网关接口(CGI)的增强版本。 FastCGI致力于减少网页服务器与CGI程序之间的开销，从而使服务器可以同时处理更多的网页请求。

Nginx为了许多外部工具和服务而引入FastCGI技术，例如[Perl](/index.php?title=Perl&action=edit&redlink=1 "Perl (page does not exist)"), [PHP](/index.php/PHP "PHP") 和 [Python](/index.php/Python "Python")。所以，在FastCGI服务启动之前，它们都是不能使用的。

#### PHP 集成

有不同的方式可以启动PHP FastCGI服务,我们将介绍**php-fpm**.这也是推荐的方案.

##### 第一步: PHP 配置

在`/etc/php/php.ini`中的`open_basedir`中列出包含PHP文件的基本目录,如`/srv/http/`和`/usr/share/webapps/`:

```
open_basedir = /usr/share/webapps/:/srv/http/:/home/:/tmp/:/usr/share/pear/

```

##### 第二步: php-fpm

*   [http://php-fpm.org](http://php-fpm.org)

安装[php-fpm](https://www.archlinux.org/packages/?name=php-fpm).配置文件在`/etc/php/php-fpm.conf`。使用[Systemd](/index.php/Systemd "Systemd") 启动并允许开机启动`php-fpm`

##### 第三步: Nginx 配置

在每一个提供PHP Web应用程序的`server`块中都应该有一个`location`块，类似于下面：

```
 location ~ \.php$ {
      fastcgi_pass   unix:/run/php-fpm/php-fpm.sock;
      fastcgi_index  index.php;
      include        fastcgi.conf;
 }

```

你可以创建一个`/etc/nginx/php.conf`,并保存该配置,然后在需要的时候包含此文件到`server`块:

```
 server = {
     ...
     include  php.conf;
     ...
 }

```

如果你要使用 PHP 处理 .html 和 .htm 文件,你应该类似于这样：

```
 location ~ \.(php|html|htm)$ {
      fastcgi_pass   unix:/var/run/php-fpm/php-fpm.sock;
      fastcgi_index  index.php;
      include        fastcgi.conf;
 }

```

php-fpm 处理非PHP文件，应该明确地在 `/etc/php/php-fpm.conf` 中启用：

```
security.limit_extensions = .php .html .htm

```

如果你更改了配置文件,你需要重新启动php-fpm:

```
# systemctl restart php-fpm

```

**注意**这里的 `fastcgi_pass` 参数,因为它必须是所选择的FastCGI服务器在其配置文件中定义的TCP或Unix套接字.**默认**的 Unix `php-fpm` 是:

```
fastcgi_pass unix:/run/php-fpm/php-fpm.sock;

```

或者,你可以使用常用的TCP套接字,**不是默认**:

```
fastcgi_pass 127.0.0.1:9000;

```

使用Unix域套接字要更好一些。

通常都要包含 `fastcgi.conf` 或者 `fastcgi_params`，因为它们包含了 Nginx 的 FastCGI 设置（使用后者是不推荐的）。它们是安装 Nginx 时附带的。

最后，如果Nginx正在工作，运行以下命令:

```
# systemctl restart nginx

```

如果你想测试 FastCGI 是否可以使用，创建`/usr/share/nginx/html/index.php`，内容为：

```
<?php
  phpinfo ();
?>

```

然后在你的浏览器中访问 [http://127.0.0.1/index.php](http://127.0.0.1/index.php) 查看。

### 安装 phpMyAdmin

请看这篇 wiki 文章: [PhpMyAdmin#NGINX_Configuration](/index.php/PhpMyAdmin#NGINX_Configuration "PhpMyAdmin").

## 疑难解答

### 访问本地的IP重定向到本地主机

解决方法在这: [forum](https://bbs.archlinux.org/viewtopic.php?pid=780561#p780561).

编辑 _/etc/nginx/nginx.conf_ 找到 "server_name localhost" 没有被 # 注释掉的这行, 添加以下内容:

```
server_name_in_redirect off;

```

默认的行为是 nginx 重定向所有请求到在配置中 server_name 指定的值.

### Error: 403 (Permission error)

这极有可能是一个权限错误. 你能肯定无论哪个在 Nginx 配置文件中配置的用户能读取到正确的文件吗?

如果文件位于 home 目录, (例如 `/home/arch/public/webapp`) 而且你能肯定运行 Nginx 的用户有正确的权限(为了测试这个可以暂时把所有文件 chmod 为 777), `/home/arch` 可能是 **chmod 750**, 只需要简单地把它 `chmod` 为 **751**, 这样就应该正常工作了.

**如果你修改过 document root**

如果你确定权限都正确，确定一下你的 document root 目录是非空的。在那儿创建一个 index.html 试一试。

### Error: The page you are looking for is temporarily unavailable. Please try again later.

这是因为 FastCGI server 还没启动。或者socket权限不正确。

### Error: No input file specified

大多是因为你没有在 `SCRIPT_FILENAME` 中包含脚本的全路径. 如果 nginx 上的配置 (`fastcgi_param SCRIPT_FILENAME`) 是正确的, 这种错误意味着 php 加载请求脚本失败. 通常这是一个简单的权限问题, 只需用 root 运行 `php-cgi`

```
# spawn-fcgi -a 127.0.0.1 -p 9000 -f /usr/bin/php-cgi

```

或者可以创建一些组和用户来启动 php-cgi. 例如:

```
# groupadd www
# useradd -g www www
# chmod +w /srv/www/nginx/html
# chown -R www:www /srv/www/nginx/html
# spawn-fcgi -a 127.0.0.1 -p 9000 -u www -g www -f /usr/bin/php-cgi

```

另外一个原因是, `nginx.conf` 的 "location ~ \.php$" 段有错误的 "root" 参数, 请保证在同一个服务器内 "root" 与 "location /" 指向同一个目录. 或者把 root 设为全局, 不在其它的位置部分定义.

记住 php 脚本路径默认是 `/srv/http` ,在 `/etc/php/php.ini` 文件内的变量 `open_basedir` 中定义, 请按需更改。

并且请注意不仅 PHP 脚本要有读取权限，它的路径结构也要有可执行权限，这样 PHP 用户才可以遍历目录。

## 参见

*   [nginx Official Site](http://nginx.net/)
*   [nginx Wiki](http://wiki.nginx.org/Main)
*   [nginx HOWTO](http://calomel.org/nginx.html)
*   [Easy Config Files](http://wiki.gotux.net/config:nginx)