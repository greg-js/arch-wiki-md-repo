# Squid (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

来自 Squid [官方网站](http://www.squid-cache.org)：

_**Squid** 是一个 Web 缓存代理，支持 HTTP, HTTPS, FTP, 以及更多。它通过缓存与重用经常请求的web页面，减少带宽使用同时提升了响应时间。Squid 具有可扩展的访问控制功能，同时可以使服务器加速。它运行在 Unix 和 Windows 中，采用 GNU GPL 协议发布。_

尽管 squid 在大型公司和学校中工作的很好，它也可以为个人家庭用户使用。然而如果你在寻找一个更轻量级的单用户代理，你可以尝试使用 [Polipo](/index.php/Polipo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Polipo (简体中文)")。

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的 [squid](https://www.archlinux.org/packages/?name=squid)。

## 配置

默认设置下，缓存目录会创建于 `/var/cache/squid`,同时正确的权限会被同时设置好。然而，为了更好的控制，我们需要深入 `/etc/squid/squid.conf`.

所有的配置项都有注释，但是如果你想去掉注释的话，你可以运行：

```
sed -i "/^#/d;/^ *$/d" /etc/squid/squid.conf

```

下面的选项会对你有用。如果你没有这些选项，你可以添加进去。

*   `http_port` - 设置 Squid 绑定的代理端口。你可以将 Squid 绑定到多个端口，使用多个 http_port 行。默认情况下，Squid 绑定到 3128 端口。

```
http_port 3128
http_port 3129

```

*   `http_access` - 这是访问控制列表，即谁被允许使用这个代理。默认只有 localhost 被允许访问这个代理。作为测试目的，你可以改变这个选项 `http_access deny all` 为 `http_access allow all`，这会允许所有人链接到你的代理。如果你想仅仅允许子网内访问，你可以使用：

```
acl ip_acl src 192.168.1.0/24
http_access allow ip_acl
http_access deny all

```

*   `cache_mgr` - 这是缓存管理员的 email 地址。

```
cache_mgr squid.admin@example.com

```

*   `shutdown_lifetime` - 指定当 squid 的 rc.d 脚本请求停止的时候等待的时间。如果你在你的桌面电脑上运行 squid，你也许需要设成短一点的时间值。

```
shutdown_lifetime 10 seconds

```

*   `cache_mem` - 这是你想让 squid 使用内存而不写入硬盘的内存量。Squid 的总内存使用量会超过这个值！默认这个值是 8MB，所以如果你有很多内存的话，你也许想增加这个值。

```
cache_mem 64 MB

```

*   `visible_hostname` - 可以在状态/错误信息中看到的 hostname。

```
visible_hostname cerberus

```

*   `cache_peer` - 如果你想让 Squid 穿过另一个代理服务器，而不是直接连到 Internet，你需要在这里指定。
*   `login` - 如果上层代理需要认证的话使用这个选项。
*   `never_direct` - 如果你设定了上面的选项的话，可以告诉缓存不要直接连接到 Internet 请求页面。

```
cache_peer 10.1.1.100 parent 8080 0 no-query default login=user:password
never_direct allow all

```

*   `maximum_object_size` - 这是缓存部件的最大大小。默认这个值很小 (我认为是 256KB)，所以如果你有很多磁盘空间，你需要将这个值增大到一个合理的值。

```
maximum_object_size 10 MB

```

*   `cache_dir` - 这是你的缓存文件夹，存储缓存文件的位置。有很多个选项，但是格式大概是这样子：

```
cache_dir diskd <directory> <size in MB> 16 256

```

所以，在一个学校的代理服务器中：

```
cache_dir diskd /cache0 200000 16 256

```

如果你改变了默认的缓存文件夹，你需要在启动 squid 前为文件夹设置合适的权限。否则会无法创建缓存文件夹并且停止运行。

## 启动

配置完成之后，你需要检查一下配置文件是否正确：

```
# squid -k check

```

然后创建缓存目录：

```
# squid -z

```

最后你可以启动 Squid:

```
# systemctl start squid

```

开机启动：

```
# systemctl enable squid

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Squid_(简体中文)&oldid=413929](https://wiki.archlinux.org/index.php?title=Squid_(简体中文)&oldid=413929)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Networking (简体中文)](/index.php/Category:Networking_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Networking (简体中文)")
*   [Security (简体中文)](/index.php/Category:Security_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Security (简体中文)")
*   [Proxy servers (简体中文)](/index.php/Category:Proxy_servers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Proxy servers (简体中文)")
*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")