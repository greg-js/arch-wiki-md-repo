Related articles

*   [Gitolite](/index.php/Gitolite "Gitolite")
*   [Ruby on Rails](/index.php/Ruby_on_Rails "Ruby on Rails")

这是来自 [Gitlab的主页](https://about.gitlab.com/):

	GitLab 提供 git 仓储管理、代码查阅、问题追踪、动态监控和维基. 企业在本地安装Gitlab并用LDAP和活动目录服务器连接以进行安全的身份验证和授权。单个GitLab服务器可以处理超过25,000个用户，但也可以使用多个活动服务器创建高可用性设置。

你可以在 [GitLab.com](https://gitlab.com/)找到实时版本的例子.

## Contents

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 初步说明](#初步说明)
    *   [2.2 GitLab](#GitLab)
    *   [2.3 为Unicorn自定义端口](#为Unicorn自定义端口)
    *   [2.4 秘密字符串](#秘密字符串)
    *   [2.5 Redis](#Redis)
    *   [2.6 数据库后端](#数据库后端)
        *   [2.6.1 PostgreSQL](#PostgreSQL)
        *   [2.6.2 MariaDB](#MariaDB)
    *   [2.7 防火墙](#防火墙)
    *   [2.8 初始化Gitlab数据库](#初始化Gitlab数据库)
    *   [2.9 调整修改位](#调整修改位)
*   [3 开始并测试Gitlab](#开始并测试Gitlab)
*   [4 每次更新时升级数据库](#每次更新时升级数据库)
*   [5 更多配置](#更多配置)
    *   [5.1 基本的 SSH](#基本的_SSH)
    *   [5.2 自定义SSH连接](#自定义SSH连接)
    *   [5.3 HTTPS/SSL](#HTTPS/SSL)
        *   [5.3.1 改变Gitlab配置](#改变Gitlab配置)
        *   [5.3.2 Let's Encrypt(让我们加密吧)](#Let's_Encrypt(让我们加密吧))
    *   [5.4 Web服务器配置](#Web服务器配置)
        *   [5.4.1 Node.js](#Node.js)
        *   [5.4.2 Nginx](#Nginx)
        *   [5.4.3 Apache](#Apache)
    *   [5.5 Gitlab-workhorse](#Gitlab-workhorse)
*   [6 Useful Tips](#Useful_Tips)
    *   [6.1 Hidden options](#Hidden_options)
    *   [6.2 Backup and restore](#Backup_and_restore)
    *   [6.3 Sending mails from Gitlab via SMTP](#Sending_mails_from_Gitlab_via_SMTP)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 HTTPS is not green (gravatar not using https)](#HTTPS_is_not_green_(gravatar_not_using_https))
    *   [7.2 Errors after updating](#Errors_after_updating)
    *   [7.3 Gitlab-Unicorn cannot access non-default repositories directory](#Gitlab-Unicorn_cannot_access_non-default_repositories_directory)
    *   [7.4 Failed to connect to Gitaly](#Failed_to_connect_to_Gitaly)
*   [8 See also](#See_also)

## 安装

**Note:** 这篇文章优先覆盖非https安装和配置Gitlab. 如果需要，查阅[#Advanced Configuration](#Advanced_Configuration) 来设置SSL.

Gitlab需要 [Redis](/index.php/Redis "Redis") 和数据库后端. 如果你计划在同一个机器运行的话, 首先得安装 [MySQL](/index.php/MySQL "MySQL") 或者 [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

[Install](/index.php/Install "Install") [gitlab](https://www.archlinux.org/packages/?name=gitlab) 包.

为了接受邮件通知, 一个邮件服务器必须被安装和配置. 查阅 [Category:Mail server](/index.php/Category:Mail_server "Category:Mail server") 获取更多细节.

## 配置

### 初步说明

Gitlab包括多种组件, 可查阅 [架构概览页](https://docs.gitlab.com/ce/development/architecture.html).

[gitlab](https://www.archlinux.org/packages/?name=gitlab) 包会以更接近标准Linux公约的方式安装Gitlab:

| 描述 | [GitLab's Official](https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md) | [gitlab](https://www.archlinux.org/packages/?name=gitlab) |
| 配置文件 GitShell | `/home/git/gitlab-shell/config.yml` | `/etc/webapps/gitlab-shell/config.yml` |
| 配置文件 GitLab | `/home/git/gitlab/config/gitlab.yml` | `/etc/webapps/gitlab/gitlab.yml` |
| 用户 (家目录) | `git` (`/home/git`) | `gitlab` (`/var/lib/gitlab`) |

**Tip:** 如果你熟悉 [Arch Build System](/index.php/Arch_Build_System "Arch Build System") 你可以编辑PKGBUILD和相关文件来改变gitlab的家目录到你喜欢的位置.

### GitLab

编辑 `/etc/webapps/gitlab/gitlab.yml` 并至少设置下面的参数:

**Note:** `hostname` 和 `port` 被用于 `git clone [http://hostname:port](http://hostname:port)` 的例子中.

**Hostname:** 在 `gitlab:` 区里设置 `host:` - 把 `localhost` 换成 `yourdomain.com` (**注意:** 不要加 '[http://'](http://') 或者后面的斜线) - 到你的完全合格的域名.

**Port:** `port:` 可能会让你很困扰. 这不是Gitlab服务器运行的端口(unicorn) ; 这是用户通过浏览器初次连接的端口. 基本上, 如果你有意让用户通过他们的浏览器访问 'yourdomain.com' , 而且不用附加端口号, 把 `port:` 设成 `80`. 如果你想让用户输入比如 'yourdomain.com:3425' 这样的东西到浏览器, 那么你就得设置 `port:` 成 `3425`. 你也会得 **设置你的网络服务器** 来监听那个端口.

**Timezone (时区，可选):** `time_zone:` 参数是可选的, 但是它可能对强制Gitlab应用的区域有用.

最后设置正确的 [permissions](/index.php/Permissions "Permissions") 到 *uploads*（上传） 目录:

```
# chmod 700 /var/lib/gitlab/uploads

```

### 为Unicorn自定义端口

GitLab Unicorn 是处理大多数用户请求的主要组件. 默认的, 它监听 `127.0.0.1:8080` 地址，并且能通过 `/etc/webapps/gitlab/unicorn.rb` 文件来改变:

 `/etc/webapps/gitlab/unicorn.rb` 
```
listen "/run/gitlab/gitlab.socket", :backlog => 1024
listen "**127.0.0.1:8080**", :tcp_nopush => true
```

如果 Unicorn 地址被改变, 其它与Unicorn交流的组件的配置也需要被更新:

*   对于 GitLab Shell, 在 `/etc/webapps/gitlab-shell/config.yml`更新 `gitlab_url` 变量.

**Tip:** 根据注释里的配置文件, UNIX 套接字能通过 URL转义斜杠(/) (即. `http+unix://%2Frun%2Fgitlab%2Fgitlab.socket` 对应默认的 `/run/gitlab/gitlab.socket`). 额外的, 未转义斜杠能用来指定 [相关URL根路径](https://docs.gitlab.com/ce/install/relative_url.html) (例如. `/gitlab`).

*   对于 GitLab Workhorse, [edit](/index.php/Edit "Edit") `gitlab-workhorse.service` 并更新 `-authBackend` 选项.

### 秘密字符串

确定 `/etc/webapps/gitlab/secret` 和 `/etc/webapps/gitlab-shell/secret` 文件包含了些什么. 它们的内容应该被保密因为它们会被用作生成认证令牌等.

比如, 能够通过下面的命令生成随机字符串:

```
# hexdump -v -n 64 -e '1/1 "%02x"' /dev/urandom > /etc/webapps/gitlab/secret
# chown root:gitlab /etc/webapps/gitlab/secret
# chmod 640 /etc/webapps/gitlab/secret

```

```
# hexdump -v -n 64 -e '1/1 "%02x"' /dev/urandom > /etc/webapps/gitlab-shell/secret
# chown root:gitlab /etc/webapps/gitlab-shell/secret
# chmod 640 /etc/webapps/gitlab-shell/secret

```

### Redis

为了提供足够的性能，你可能需要一个缓存数据库. [安装](/index.php/Redis#Installation "Redis") 并 [配置](/index.php/Redis#Configuration "Redis") 一个redis实例, 注意专用于通过套接字监听的部分.

*   添加 `gitlab` 用户到 `redis` [user group](/index.php/User_group "User group").

*   更新配置文件:

 `/etc/webapps/gitlab/resque.yml` 
```
development: unix:/run/redis/redis.sock
test: unix:/run/redis/redis.sock
production: unix:/run/redis/redis.sock
```
 `/etc/webapps/gitlab-shell/config.yml` 
```
# Redis settings used for pushing commit notices to gitlab
redis:
  bin: /usr/bin/redis-cli
  host: 127.0.0.1
  port: 6379
  # pass: redispass # Allows you to specify the password for Redis
  database: 5 # Use different database, default up to 16
  socket: /run/redis/redis.sock # **uncomment** this line
  namespace: resque:gitlab
```

### 数据库后端

在Gitlab运行之前需要一个数据库后端. GitLab [建议](https://docs.gitlab.com/ce/install/installation.html#6-database) 使用 PostgreSQL.

#### PostgreSQL

登录 PostgreSQL 并创造 `gitlabhq_production` 数据库和它的用户一起. 记得改变 `your_username_here` 和 `your_password_here` 到你的真正的值:

```
# psql -d template1

```

```
template1=# CREATE USER your_username_here WITH PASSWORD 'your_password_here';
template1=# ALTER USER your_username_here SUPERUSER;
template1=# CREATE DATABASE gitlabhq_production OWNER your_username_here;
template1=# \q
```

**Note:** 创建超级用户的目的是Gitlab在视图变得"智能"并安装扩展(并不仅仅在它的命名区间创建).并且它只被Postgresql的超级用户允许.

用新用户连接到新数据库来确定它有用:

```
# psql -d gitlabhq_production

```

复制 PostgreSQL 文件 ，在配置它之前 (覆盖默认的 MySQL 配置文件):

```
# cp /usr/share/doc/gitlab/database.yml.postgresql /etc/webapps/gitlab/database.yml

```

打开新的 `/etc/webapps/gitlab/database.yml` 并设置 `username:` 和 `password:`的值. 比如:

 `/etc/webapps/gitlab/database.yml` 
```
#
# PRODUCTION
#
production:
  adapter: postgresql
  encoding: unicode
  database: gitlabhq_production
  pool: 10
  username: your_username_here
  password: "your_password_here"
  # host: localhost
  # port: 5432
  # socket: /tmp/postgresql.sock
...

```

对于我们的目的 (除非你知道你在干什么),你不必担心配置列在 `/etc/webapps/gitlab/database.yml`的其它数据库. 我们只需要设置生产的数据库来让Gitlab工作.

#### MariaDB

**Warning:** 通过MariaDB使用Gitlab是 [不推荐的](https://docs.gitlab.com/ce/install/database_mysql.html). 你可能会碰到像 `Specified key was too long; max key length is 767 bytes` 的问题，当你试图使用[MariaDB](/index.php/MariaDB "MariaDB").

为了设置 MySQL (MariaDB) 你需要创建一个数据库叫做`gitlabhq_production` ，和一个对数据库有全部权限的用户一起 (默认: `gitlab`) :

 `$ mysql -u root -p` 
```
mysql> CREATE DATABASE `gitlabhq_production` DEFAULT CHARACTER SET `utf8` COLLATE `utf8_unicode_ci`;
mysql> CREATE USER 'gitlab'@'localhost' IDENTIFIED BY 'password';
mysql> GRANT ALL ON `gitlabhq_production`.* TO 'gitlab'@'localhost';
mysql> \q
```

用新用户连接新数据库:

```
$ mysql -u **gitlab** -p -D gitlabhq_production

```

在配置MySQL模板文件前复制它:

```
# cp /usr/share/doc/gitlab/database.yml.mysql /etc/webapps/gitlab/database.yml

```

下一步你需要打开 `/etc/webapps/gitlab/database.yml` 并为 `gitlabhq_production`设置 `username:` 和 `password:` :

 `/etc/webapps/gitlab/database.yml` 
```
#
# PRODUCTION
#
production:
  adapter: mysql2
  encoding: utf8
  collation: utf8_general_ci
  reconnect: false
  database: gitlabhq_production
  pool: 10
  username: **username**
  password: **"password"**
  # host: localhost
  # socket: /run/mysqld/mysqld.sock # If running MariaDB as socket
...

```

它不应该被设为全局可读，比如只有运行在`gitlab`下的进程才有读/写权限:

```
# chmod 600 /etc/webapps/gitlab/database.yml
# chown gitlab:gitlab /etc/webapps/gitlab/database.yml

```

获取更多信息和其它创建/管理MySQL数据库的办法, 查阅 [MariaDB documentation](https://mariadb.org/docs/) 和 [GitLab official (generic) install guide](https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md).

### 防火墙

如果你想通过[iptables](/index.php/Iptables "Iptables") 防火墙给予Gitlab安装过程直接权限, 你可能需要调整端口和网络地址:

```
# iptables -A tcp_inbound -p TCP -s **192.168.1.0/24** --destination-port **80** -j ACCEPT

```

启用 API-access:

```
# iptables -A tcp_inbound -p TCP -s **192.168.1.0/24** --destination-port **8080** -j ACCEPT

```

如果你在一个路由器后面, 别忘了转发这个端口到Gitlab服务器端口, 如果你想运行 WAN-access的话.

### 初始化Gitlab数据库

在初始化数据库之前开启 [Redis](/index.php/Redis "Redis") 服务器和 `gitlab-gitaly.service` .

初始化数据库并激活更多特性:

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake gitlab:setup RAILS_ENV=production"

```

最后运行下面的命令来检查你的安装:

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake gitlab:env:info RAILS_ENV=production"
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake gitlab:check RAILS_ENV=production"

```

**Note:**

*   *gitlab:env:info* 和 *gitlab:check* 命令会显示一个和Git相关的严重的错误. 这是正常的.
*   *gitlab:check* 会显示缺少初始化脚本. 这也没什么好担心的, 因为 [systemd](/index.php/Systemd "Systemd") 服务文件会被相应使用 (而这Gitlab无法识别).

### 调整修改位

(如果用户和组所有权没有正确配置的话Gitlab检查不会通过)

```
# chmod -R ug+rwX,o-rwx /var/lib/gitlab/repositories/
# chmod -R ug-s /var/lib/gitlab/repositories
# find /var/lib/gitlab/repositories/ -type d -print0 | xargs -0 chmod g+s

```

## 开始并测试Gitlab

确定 [MySQL](/index.php/MySQL "MySQL")或 [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") 和 [Redis](/index.php/Redis "Redis") 运行和设置正确.

然后 [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `gitlab.target`.

现在你可以通过访问 [http://localhost:8080](http://localhost:8080) 或者 [http://yourdomain.com来测试你的Gitlab](http://yourdomain.com来测试你的Gitlab), 你可能会被提示创建密码:

```
username: root
password: You'll be prompted to create one on your first visit.

```

查阅[#Troubleshooting](#Troubleshooting) 和在 `/usr/share/webapps/gitlab/log/` 目录下的日志文件来 排除故障.

## 每次更新时升级数据库

在更新 [gitlab](https://www.archlinux.org/packages/?name=gitlab) 包后, 需要升级数据库:

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake db:migrate RAILS_ENV=production"

```

之后, 之后重启Gitlab相关服务:

```
# systemctl daemon-reload
# systemctl restart gitlab-sidekiq gitlab-unicorn gitlab-workhorse gitlab-gitaly

```

## 更多配置

### 基本的 SSH

在完成了基本安装后, 为用户设置ssh权限. [OpenSSH](/index.php/OpenSSH "OpenSSH")的配置会在下面描述. [其它SSH客户端和服务器](/index.php/Secure_Shell#Other_SSH_clients_and_servers "Secure Shell") 需要不同的调整.

获取添加用户SSH秘钥的建议，过程在[GitLab](https://docs.gitlab.com/ee/ssh/) 网站里描述的很好了. 你可以在 `/var/lib/gitlab/log/gitlab-shell.log`检查管理员日志来确认用户SSH秘钥被正确提交了. 在这些事件之后, GitLab 添加这些秘钥到*authorized_keys* 文件里，它在 `/var/lib/gitlab/.ssh/authorized_keys`.

测试秘钥的常见方法 (比如: `$ ssh -T git@*YOUR_SERVER*`) 需要一点额外配置才能正常工作. 在 `/etc/webapps/gitlab/gitlab.yml` (默认用户: `gitlab`)里配置的用户必须添加到服务器的sshd配置文件,除此之外还有几个其它改变 :

 `/etc/ssh/sshd_config` 
```
PubkeyAuthentication   yes
AuthorizedKeysFile     %h/.ssh/authorized_keys

```

更新配置文件之后, 重启ssh守护进程:

```
# systemctl restart sshd

```

测试用户SSH米哟啊 (可选添加 -v 来查看额外信息):

```
$ ssh -T **gitlab**@*YOUR_SERVER*

```

### 自定义SSH连接

如果你在一个非标准端口运行SSH，你必须改变Gitlab用户的SSH配置:

 `/var/lib/gitlab/.ssh/config` 
```
host localhost      # Give your setup a name (here: override localhost)
user gitlab         # Your remote git user
port 2222           # Your port number
hostname 127.0.0.1; # Your server name or IP
```

你还必须在 `/etc/webapps/gitlab/gitlab.yml` 文件里改变相应的选项 (比如. ssh_user, ssh_host, admin_uri) .

### HTTPS/SSL

#### 改变Gitlab配置

修改 `/etc/webapps/gitlab/shell.yml` 那样到你的Gitlab站点的URL就会以 `https://`开头. 修改 `/etc/webapps/gitlab/gitlab.yml` 那样 `https:` 设置就会被设为 `true`.

查阅 [Apache HTTP Server#TLS](/index.php/Apache_HTTP_Server#TLS "Apache HTTP Server") 和 [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt").

#### Let's Encrypt(让我们加密吧)

验证你的URL, Let's Encrypt的过程会试图用像 `https://gitlab.*YOUR_SERVER_FQDN*/.well-known/acme-challenge/*A_LONG_ID*`的东西连接你的Gitlab服务器. 但是, 因为Gitlab配置, 每个到 `gitlab.*YOUR_SERVER_FQDN*` 的请求会被重定向到一个代理 (gitlab-workhorse) 而它无法处理这个URL.

为了绕过这个问题, 你可以使用 Let's Encrypt的webroot配置, 在 `/srv/http/letsencrypt/`设置webroot.

除此之外, 强迫到Gitlab的Let's Encrypt请求重定向到这个webroot可通过添加下面的:

 `/etc/http/conf/extra/gitlab.conf` 
```
Alias "/.well-known"  "/srv/http/letsencrypt/.well-known"
RewriteCond   %{REQUEST_URI}  !/\.well-known/.*

```

### Web服务器配置

如果你想把Gitlab集成进一个运行的服务器而不是用它的内置http服务器Unicorn，那么按照这些说明操作.

##### Node.js

你可以轻松在443端口设置http代理来代理到8080端口的Gitlab程序的流量，通过为Node.js使用http-master. 在你创建你的域名的 OpenSSL 秘钥并获取你的CA 证书 (或自己设置的)后, 然后去 [https://github.com/CodeCharmLtd/http-master](https://github.com/CodeCharmLtd/http-master) 来学习使用https代理到Gitlab的请求多容易. http-master 建立在 [node-http-proxy](https://github.com/nodejitsu/node-http-proxy)之上.

#### Nginx

查阅 [Nginx#Configuration](/index.php/Nginx#Configuration "Nginx") 获取基本的 *nginx* 配置信息和 [Nginx#TLS](/index.php/Nginx#TLS "Nginx") 来启用 HTTPS. 在这个部分的例子假设服务器区块是用 [Nginx#Managing server entries](/index.php/Nginx#Managing_server_entries "Nginx")管理的.

创建和编辑基于下面代码的配置. 查阅 [upstream GitLab repository](https://gitlab.com/gitlab-org/gitlab-ce/tree/master/lib/support/nginx)获取更多例子.

 `/etc/nginx/servers-available/gitlab` 
```
upstream gitlab-workhorse {
  server unix:/run/gitlab/gitlab-workhorse.socket fail_timeout=0;
}

server {
  listen 80;
  #listen 443 ssl; # uncomment to enable ssl
  server_name example.com

  #ssl_certificate ssl/example.com.crt;
  #ssl_certificate_key ssl/example.com.key;

  location / {
      # unlimited upload size in nginx (so the setting in GitLab applies)
      client_max_body_size 0;

      # proxy timeout should match the timeout value set in /etc/webapps/gitlab/unicorn.rb
      proxy_read_timeout 60;
      proxy_connect_timeout 60;
      proxy_redirect off;

      proxy_set_header Host $http_host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-Ssl on;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;

      proxy_pass http://gitlab-workhorse;
  }

  error_page 404 /404.html;
  error_page 422 /422.html;
  error_page 500 /500.html;
  error_page 502 /502.html;
  error_page 503 /503.html;
  location ~ ^/(404|422|500|502|503)\.html$ {
    root /usr/share/webapps/gitlab/public;
    internal;
  }
}

```

#### Apache

安装并配置 [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server"). 你可以使用这些 [upstream recipes](https://gitlab.com/gitlab-org/gitlab-recipes/tree/master/web-server/apache) 来开始Gitlab虚拟主机的配置文件.

对于SSL配置查阅 [Apache HTTP Server#TLS](/index.php/Apache_HTTP_Server#TLS "Apache HTTP Server"). 如果你不需要它, 移除它. 注意到SSL虚拟主机需要特定IP而不是通用IP. 同样如果你为Unicorn设置了自定义端口, 不要忘了在 `BalanceMember` 行也设置它.

### Gitlab-workhorse

Since 8.0 GitLab uses separate HTTP server [gitlab-workhorse](https://www.archlinux.org/packages/?name=gitlab-workhorse) for large HTTP requests like Git push/pull. If you want to use this instead of SSH, install the [gitlab-workhorse](https://www.archlinux.org/packages/?name=gitlab-workhorse) package, enable `gitlab-workhorse.service` and configure web server for this. [gitlab-workhorse](https://www.archlinux.org/packages/?name=gitlab-workhorse) should now be preferred over `gitlab-unicorn` according to the GitLab team: [https://gitlab.com/gitlab-org/gitlab-ce/issues/22528#note_16036216](https://gitlab.com/gitlab-org/gitlab-ce/issues/22528#note_16036216)

**Note:** Unicorn is still needed so don't disable or stop `gitlab-unicorn.service`.

By default [gitlab-workhorse](https://www.archlinux.org/packages/?name=gitlab-workhorse) listens on `/run/gitlab/gitlab-workhorse.socket`. You can [edit](/index.php/Edit "Edit") `gitlab-workhorse.service` and change the parameter `-listenAddr` to make it listen on an address, for example `-listenAddr 127.0.0.1:8181`. If listening on an address you also need to set the network type to `-listenNetwork tcp`

When using nginx remember to edit your nginx configuration file. To switch from gitlab-unicorn to gitlab-workhorse edit the two following settings accordingly

 `/etc/nginx/servers-available/gitlab` 
```
upstream gitlab {
   server unix:/run/gitlab/gitlab-workhorse.socket fail_timeout=0;
}

...

      proxy_pass [http://unix:/run/gitlab/gitlab-workhorse.socket](http://unix:/run/gitlab/gitlab-workhorse.socket);
  }  
}
```

## Useful Tips

### Hidden options

Go to Gitlab's home directory:

```
# cd /usr/share/webapps/gitlab

```

and run:

 `# rake -T | grep gitlab` 
```
rake gitlab:app:check                         # GITLAB | Check the configuration of the GitLab Rails app
rake gitlab:backup:create                     # GITLAB | Create a backup of the GitLab system
rake gitlab:backup:restore                    # GITLAB | Restore a previously created backup
rake gitlab:check                             # GITLAB | Check the configuration of GitLab and its environment
rake gitlab:cleanup:block_removed_ldap_users  # GITLAB | Cleanup | Block users that have been removed in LDAP
rake gitlab:cleanup:dirs                      # GITLAB | Cleanup | Clean namespaces
rake gitlab:cleanup:repos                     # GITLAB | Cleanup | Clean repositories
rake gitlab:env:check                         # GITLAB | Check the configuration of the environment
rake gitlab:env:info                          # GITLAB | Show information about GitLab and its environment
rake gitlab:generate_docs                     # GITLAB | Generate sdocs for project
rake gitlab:gitlab_shell:check                # GITLAB | Check the configuration of GitLab Shell
rake gitlab:import:all_users_to_all_groups    # GITLAB | Add all users to all groups (admin users are added as owners)
rake gitlab:import:all_users_to_all_projects  # GITLAB | Add all users to all projects (admin users are added as masters)
rake gitlab:import:repos                      # GITLAB | Import bare repositories from gitlab_shell -> repos_path into GitLab project instance
rake gitlab:import:user_to_groups[email]      # GITLAB | Add a specific user to all groups (as a developer)
rake gitlab:import:user_to_projects[email]    # GITLAB | Add a specific user to all projects (as a developer)
rake gitlab:satellites:create                 # GITLAB | Create satellite repos
rake gitlab:setup                             # GITLAB | Setup production application
rake gitlab:shell:build_missing_projects      # GITLAB | Build missing projects
rake gitlab:shell:install[tag,repo]           # GITLAB | Install or upgrade gitlab-shell
rake gitlab:shell:setup                       # GITLAB | Setup gitlab-shell
rake gitlab:sidekiq:check                     # GITLAB | Check the configuration of Sidekiq
rake gitlab:test                              # GITLAB | Run all tests
rake gitlab:web_hook:add                      # GITLAB | Adds a web hook to the projects
rake gitlab:web_hook:list                     # GITLAB | List web hooks
rake gitlab:web_hook:rm                       # GITLAB | Remove a web hook from the projects
rake setup                                    # GITLAB | Setup gitlab db

```

### Backup and restore

Create a backup of the gitlab system:

```
# sudo -u gitlab -H rake RAILS_ENV=production gitlab:backup:create

```

Restore the previously created backup file `/home/gitlab/gitlab/tmp/backups/20130125_11h35_1359131740_gitlab_backup.tar`:

```
# sudo -u gitlab -H rake RAILS_ENV=production gitlab:backup:restore BACKUP=/home/gitlab/gitlab/tmp/backups/20130125_11h35_1359131740

```

**Note:** Backup folder is set in `config/gitlab.yml`. GitLab backup and restore is documented [here](https://github.com/gitlabhq/gitlabhq/blob/master/doc/raketasks/backup_restore.md).

### Sending mails from Gitlab via SMTP

You might want to use a gmail (or other mail service) to send mails from your gitlab server. This avoids the need to install a mail daemon on the gitlab server.

Adjust `smtp_settings.rb` according to your mail server settings:

 `/usr/share/webapps/gitlab/config/initializers/smtp_settings.rb` 
```
if Rails.env.production?
  Gitlab::Application.config.action_mailer.delivery_method = :smtp

  ActionMailer::Base.delivery_method = :smtp
  ActionMailer::Base.smtp_settings = {
    address:              'smtp.gmail.com',
    port:                 587,
    domain:               'gmail.com',
    user_name:            'username@gmail.com',
    password:             'application password',
    authentication:       'plain',
    enable_starttls_auto: true
  }
end
```

Gmail will reject mails received this way (and send you a mail that it did). You will need to disable secure authentication (follow the link in the rejection mail) to work around this. The more secure approach is to enable two-factor authentication for username@gmail.com and to set up an application password for this configuration file.

## Troubleshooting

### HTTPS is not green (gravatar not using https)

Redis caches gravatar images, so if you have visited your GitLab with http, then enabled https, gravatar will load up the non-secure images. You can clear the cache by doing

```
cd /usr/share/webapps/gitlab
RAILS_ENV=production bundle-2.3 exec rake cache:clear

```

as the gitlab user.

### Errors after updating

After updating the package from the AUR, the database migrations and asset updates will sometimes fail. These steps may resolve the issue, if a simple reboot does not.

First, move to the gitlab installation directory.

```
# cd /usr/share/webapps/gitlab

```

If every gitlab page gives a 500 error, then the database migrations and the assets are probably stale. If not, skip this step.

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake db:migrate RAILS_ENV=production"

```

If gitlab is constantly waiting for the deployment to finish, then the assets have probably not been recompiled.

```
# su - gitlab -s /bin/sh -c "cd '/usr/share/webapps/gitlab'; bundle-2.3 exec rake gitlab:assets:clean gitlab:assets:compile cache:clear RAILS_ENV=production"

```

Finally, restart the gitlab services and test your site.

```
# systemctl restart gitlab-unicorn gitlab-sidekiq gitlab-workhorse

```

### Gitlab-Unicorn cannot access non-default repositories directory

If a custom repository storage directory is set in `/home`, disable the `ProtectHome=true` parameter in the `gitlab-unicorn.service` (see [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd") and the [relevant forum thread on gitlab.com](https://forum.gitlab.com/t/cannot-change-repositores-location/9634/2)).

### Failed to connect to Gitaly

Sometimes, the Gitaly service won't get started, leaving GitLab unable to connect to Gitaly. The solution is simple:

```
# systemctl start gitlab-gitaly

```

## See also

*   [Official installation documentation](https://docs.gitlab.com/ce/install/installation.html)
*   [GitLab recipes with further documentation on running it with several web servers](https://gitlab.com/gitlab-org/gitlab-recipes)
*   [GitLab source code](https://gitlab.com/gitlab-org/gitlab-ce)