Related articles

*   [Tor](/index.php/Tor "Tor")
*   [Polipo](/index.php/Polipo "Polipo")

[Privoxy](http://www.privoxy.org/) 是一个HTTP协议过滤代理，常结合Tor使用。privoxy是有着先进的过滤能力和保护隐私的代理工具，它可以过滤网页内容，管理cookies，控制访问，除广告、横幅、弹出窗口等等，它同时支持单系统和多用户网络。

Using Privoxy is necessary when they use a [SOCKS](https://en.wikipedia.org/wiki/SOCKS "wikipedia:SOCKS") proxy directly because browsers leak your DNS requests, which reduces your anonymity.

当使用[SOCKS](https://en.wikipedia.org/wiki/SOCKS "wikipedia:SOCKS")代理直接访问时使用Privoxy是有必要的，因为直接使用socks5访问时，浏览器可能会泄漏泄漏DNS请求，从降低匿名性。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 监听地址](#.E7.9B.91.E5.90.AC.E5.9C.B0.E5.9D.80)
    *   [2.2 转发协议](#.E8.BD.AC.E5.8F.91.E5.8D.8F.E8.AE.AE)
    *   [2.3 广告屏蔽](#.E5.B9.BF.E5.91.8A.E5.B1.8F.E8.94.BD)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
*   [4 See also](#See_also)

## 安装

安装[privoxy](https://www.archlinux.org/packages/?name=privoxy)。

## 配置

使用Privoxy必须指定转发规则，Privoxy的主配置文件在`/etc/privoxy/config`。

### 监听地址

Privoxy默认只提供给本机使用（即localhost或者127.0.0.1），如果需要将Privoxy提供给网络中的其他计算机使用，需要`/etc/privoxy/config`在添加监听信息，格式：

```
listen-address [SERVER-IP]:[PORT]

```

例如提供给192.168.1.1的8118端口使用:

```
listen-address 192.168.1.1:8118

```

### 转发协议

编辑 `/etc/privoxy/config`文件添加相关转发规则：

*   转发socks5

示例（注意9050后面有一个空格和点号）：

```
 forward-socks5 / localhost:9050 .

```

*   转发.i2p

通过[I2P](/index.php/I2P "I2P")路由转发.i2p，示例：

```
 forward .i2p localhost:4444

```

*   转发onion

示例（注意9050后面有一个空格和点号）：

```
forward-socks4a .onion localhost:9050 .

```

### 广告屏蔽

**Warning:** Blocking advertisements can reduce anonymity, since it creates a unique browser signature. This should not be done when using tor or another proxy for anonymity.

Using an ad blocking extension in a web browser can increase page load time. Additionally, extensions like AdBlock Plus are not supported by all browsers. A useful alternative is to install system-wide ad blocking by setting a proxy address in your preferred browser.

You can use adblock plus filters. The [privoxy blocklist](https://github.com/Andrwe/privoxy-blocklist) script automatically downloads adblock plus filters, converts them to a privoxy friendly format, and edits privoxy's config file to include those filters:

1.  Run the script once to create `/etc/conf.d/privoxy-blacklist`
2.  Edit `/etc/conf.d/privoxy-blacklist` to uncomment the line `PRIVOXY_USER=` and the two lines below it.
3.  Run the script again to download and install the blocklists.
4.  Restart privoxy.

To block tracking via embedded Facebook "Like" button, Twitter "follow", and Google Plus "+1", edit `/etc/privoxy/user.action` and add these lines to the end:

```
{+block-as-image{Facebook "like" and similar tracking URLs.}}
www.facebook.com/(extern|plugins)/(login_status|like(box)?|activity|fan)\.php
platform.twitter.com/widgets/follow_button?
plusone.google.com

```

## 使用

使用[Systemd_(简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 启用privoxy服务。

对程序进行代理设置，默认的地址是:

```
localhost:8118

```

Firefox浏览器:进入 首选项 > 高级 > 网络 > 设置，添加http代理。

Chromium

```
$ chromium --proxy-server="localhost:8118"

```

你也可以添加`http_proxy`环境变量，例如添加到`~/.bashrc`中:

```
http_proxy="http://localhost:8118"

```

参看[Proxy_settings](/index.php/Proxy_settings "Proxy settings")

## See also

*   [Privoxy Official Website](http://www.privoxy.org/)
*   [Tor Official Website](https://www.torproject.org/index.html.en)