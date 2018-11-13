**提示：** 由于shadowsocks多为中文用户使用，该中文页面大量内容领先于英文页面。

[Shadowsocks](https://github.com/clowwindy/shadowsocks/)是一个轻量级[socks5](https://en.wikipedia.org/wiki/SOCKS_(protocol)#SOCKS5 "wikipedia:SOCKS (protocol)")代理，最初用 Python 编写。

## Contents

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 客户端](#客户端)
        *   [2.1.1 命令行](#命令行)
        *   [2.1.2 以守护进程形式运行客户端](#以守护进程形式运行客户端)
        *   [2.1.3 图形界面客户端](#图形界面客户端)
        *   [2.1.4 配置代理](#配置代理)
            *   [2.1.4.1 浏览器配置](#浏览器配置)
    *   [2.2 服务端](#服务端)
        *   [2.2.1 以命令行启动进程](#以命令行启动进程)
        *   [2.2.2 以守护进程形式运行](#以守护进程形式运行)
        *   [2.2.3 多端口运行](#多端口运行)
        *   [2.2.4 加密方法](#加密方法)
        *   [2.2.5 性能优化](#性能优化)
*   [3 参阅](#参阅)

## 安装

可[安装](/index.php/Install "Install") [shadowsocks-libev](https://www.archlinux.org/packages/?name=shadowsocks-libev) 或者 [shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks)。

## 配置

shadowsocks以[json](https://en.wikipedia.org/wiki/JSON "wikipedia:JSON")为配置文件格式，以下是安装包中的样例：

 `/etc/shadowsocks/config.json` 
```
{
	"server":"remote-shadowsocks-server-ip-addr",
	"server_port":443,
	"local_address":"127.0.0.1",
	"local_port":1080,
	"password":"your-passwd",
	"timeout":300,
	"method":"chacha20-ietf",
	"fast_open":false,
	"workers":1
}

```

**提示：** shadowsocks: 若需同时指定多个服务端ip，使用如下例的语法`"server":["1.1.1.1","2.2.2.2"],`

**提示：** 要找出在你的机器上运行最快的方式，可以运行[这个脚本](https://github.com/shadowsocks/shadowsocks-libev/blob/0437e05aa8ec7f36f1eeb8c366dfd2b2b3b0288b/scripts/iperf.sh)

| Name | Explanation |
| server | 服务端监听地址(IPv4或IPv6) |
| server_port | 服务端端口，一般为`443` |
| local_address | 本地监听地址，缺省为`127.0.0.1` 可用-b参数设置 |
| local_port | 本地监听端口，一般为`1080` |
| password | 用以加密的密匙 |
| timeout | 超时时间（秒） |
| method | 参阅 [加密](https://github.com/shadowsocks/shadowsocks/wiki/Encryption) |
| fast_open | 是否启用[TCP-Fast-Open](https://github.com/clowwindy/shadowsocks/wiki/TCP-Fast-Open) |
| wokers | worker数量，如果不理解含义请不要改 |

### 客户端

#### 命令行

运行 `ss-local` 启动客户端；若需指定配置文件的位置：

 `# ss-local -c /etc/shadowsocks/config.json` 
**注意:** 有用户报告无法成功在运行时加载`config.json`
，或可尝试手动运行： `# ss-local -s *服务器地址* -p *服务器端口* -l *本地端端口* -k *密码* -m *加密方法*` 

配合nohup和&可以使之后台运行，关闭终端也不影响：

 `#nohup ss-local -s *服务器地址* -p *服务器端口* -l *本地端端口* -k *密码* -m *加密方法* &` 

增加 `-v` 参数获取详细log信息

* * *

#### 以守护进程形式运行客户端

**注意:** shadowsocks和shadowsocks-libev的systemd 系统单元使用相同的配置文件路径 （`/etc/shadowsocks`）

Shadowsocks的[systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")服务可在`/etc/shadowsocks/`里调用不同的`*conf-file*.json`（以`*conf-file*`为区分标志），例： 在`/etc/shadowsocks/`中创建了`foo.json`配置文件，那么执行以下语句就可以调用该配置：

```
# systemctl start shadowsocks@foo

```

若需开机自启动：

```
# systemctl enable shadowsocks@foo

```

**提示：** 可用`journalctl -u shadowsocks@foo`来查询日志；

#### 图形界面客户端

安装 [shadowsocks-qt5](https://www.archlinux.org/packages/?name=shadowsocks-qt5)。

#### 配置代理

shadowsocks客户端启动后，其他程序并不会直接应用socks5连接，可使用以下方法对其进行配置。

*   全局代理

使用[Iptables (简体中文)](/index.php/Iptables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Iptables (简体中文)")等工具，桌面环境用户可使用桌面设置中网络设置里的代理功能。

**注意:** 使用全局代理会使所有的连接通过shadowsocks服务器中转，一般不建议使用全局代理。另外，gnome桌面的代理设置无法正常使用。

*   程序设置自身代理

不少程序都能在其设置中添加代理，只需要在其设置中找到网络相关配置，添加socks v5代理，参照本地配置文件中的ip和port填写即可（例如浏览器的配置可参考下文[#浏览器配置](#浏览器配置)）。

*   使用工具进行临时代理

例如[proxychains-ng](https://www.archlinux.org/packages/?name=proxychains-ng)（参看[Proxy settings#Using a SOCKS proxy](/index.php/Proxy_settings#Using_a_SOCKS_proxy "Proxy settings")）和[redsocks-git](https://aur.archlinux.org/packages/redsocks-git/)。 例如使用[proxychanis](/index.php?title=Proxychanis&action=edit&redlink=1 "Proxychanis (page does not exist)")代理的例子(假设你已经在`/etc/proxychains.conf`中配置好socks5）：

```
 proxychains firefox

```

*   转换为http代理

直接走socks代理有时未必是用户的期望，可使用privoxy等软件转化socks代理为http代理。可使用[privoxy](https://www.archlinux.org/packages/?name=privoxy)和[squid](https://www.archlinux.org/packages/?name=squid)等工具。 以[Privoxy](/index.php/Privoxy "Privoxy")为例，编辑privoxy配置文件，添加socks5转发（不要漏下1080后面的点)：

```
 forward-socks5 / 127.0.0.1:1080 .

```

默认监听的是本机的8188端口，即`localhost:8188`，可更改为监听其他端口，如

```
 listen-address  127.0.0.1:8010

```

**提示：** 如果希望网络上其他主机也能使用该privoxy配置，可以更改127.0.0.1为0.0.0.0或直接删除127.0.0.1。

使用[systemd](/index.php/Systemd "Systemd")启动或重启`privoxy.service`服务，就可以使用了。假设转化后的http代理为127.0.0.1:8010，则在终端中启动（以启动chromium为例）：

```
 $ chromium %U --proxy-server=127.0.0.1:8010

```

##### 浏览器配置

**提示：** 浏览器直接使用[SOCKS](https://en.wikipedia.org/wiki/SOCKS "wikipedia:SOCKS")代理时，你可能需要使用[privoxy](/index.php/Privoxy "Privoxy")等辅助程序，因为一般浏览器会泄漏你的DNS请求，从而减少你的匿名，参看前文[#配置代理](#配置代理)中转化为http代理一节。

*   firefox
    *   使用扩展如[foxyproxy](https://getfoxyproxy.org/)或[switchyomega](https://github.com/FelisCatus/SwitchyOmega)等。
    *   直接在首选项-常规-网络代理中设置“手动代理配置”或者“自动代理配置的URL（PAC）”。

使用“手动代理配置”，在”socks主机“栏填上shadowsocks设置的本地ip（默认127.0.0.1）和端口（默认1080），点选”SOCKS v5“，然后保存即可。 使用“自动代理配置的URL（PAC）”，可使用[genpac](https://github.com/JinnLynn/genpac)工具生成，或者使用现成的pac如[gfwlist to pac](https://github.com/search?utf8=%E2%9C%93&q=gfwlist+pac&type=)，将该页面url填入并保存即可。

*   Chrome/Chromium

使用插件如[SwitchyOmega](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif)(使用方法参看[SwitchyOmega-wiki](https://github.com/FelisCatus/SwitchyOmega/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)

### 服务端

**提示：** 普通用户无需配置服务端。

#### 以命令行启动进程

可使用以下方法运行：

**注意:** 如果安装的是[shadowsocks-libev](https://www.archlinux.org/packages/?name=shadowsocks-libev)则使用`ss-server`替代`ssserver`。

*   在配置文件目录内运行

1.  在服务器上`cd`到`config.json`所在目录：
2.  运行`ssserver`

如果想在后台一直运行，可改执行：`nohup ssserver > log &`；

*   手动指定配置参数

 `# ssserver -s *监听地址(通常为0.0.0.0)* -p *监听端口* -k *密码* -m *加密方法* -t *超时时间（秒）*` 

配合nohup和&可使之后台运行，关闭终端也不影响，例如：

```
# nohup ssserver -s 0.0.0.0 -p 443 -k a29rw4pacnj2ahmf -m aes-192-cfb -t 600 &

```

#### 以守护进程形式运行

首先在`/etc/shadowsocks/foo.json`（foo是文件名，可随意更改）配置文件内填写好相关参数，然后可以使用以下方法使其以守护进程形式在后台运行：

*   使用`-d`参数

```
 # ssserver -c /etc/shadowsocks/foo.json -d start  #启动
 # ssserver -c /etc/shadowsocks/foo.json -d stop  #停止
 # ssserver -c /etc/shadowsocks/foo.json -d restart  #重启

```

*   使用systemd

```
# systemctl start shadowsocks-server@foo  #立即启动
# systemctl enable shadowsocks-server@foo  #开机自启动

```

**注意:** 如果使用[shadowsocks-libev](https://www.archlinux.org/packages/?name=shadowsocks-libev)，则使用`shadowsocks-libev-server`替代`shadowsocks-server`。

**提示：** 如果使用的服务端端口号小于1024，需要修改`usr/lib/systemd/system/shadowsocks-server@.service`使得`user=root`，之后使用`systemctl daemon-reload`重新载入守护进程配置，即可开启监听。当然也可以用**root**权限运行shadowsocks，来开启端口号小于1024的监听。

#### 多端口运行

**注意:** [shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks), [shadowsocks-libev](https://www.archlinux.org/packages/?name=shadowsocks-libev)和[shadowsocks-go-server](https://aur.archlinux.org/packages/shadowsocks-go-server/)等均支持多端口，可到[Configure-Multiple-Users](https://github.com/shadowsocks/shadowsocks/wiki/Configure-Multiple-Users)查看哪些版本支持多端口。

将配置文件中的`server_port`和`password`配置删去，添加上`"port_password"`字段配置端口及其密码，示例：

 `/etc/shadowsocks/foo.json` 
```
{
  "server": yourip,
  "_comment": {
    "25":"me",
    "9999": "girl",
    "520": "godness"
  },
  "port_password": {
    "25": "kexuedeshangwang",
    "520": "loveyoumygodness",,
    "9999": "forever",
  },
  "local_address": "127.0.0.1",
  "local_port": 1080,
  "timeout": 300,
  "method": "aes-256-cfb",
  "fast_open": false,
  "workers": 1,
  "prefer_ipv6": false
}

```

**提示：** 有反映多端口配置后使用systemd进行守护进程运行会失败，该情况下可使用上文`-d`参数的方法。

#### 加密方法

**注意:** 默认加密方法`table`速度很快，但很不安全。请不要使用`rc4`，它不安全。推荐使用AEAD加密

**提示：** 安装`M2Crypto`可略微提升加密速度，对于Python2来说，安装[python2-m2crypto](https://www.archlinux.org/packages/?name=python2-m2crypto)即可。

AEAD加密:

| Name | Alias | Key Size | Salt Size | Nonce Size | Tag Size |
| AEAD_CHACHA20_POLY1305 | chacha20-ietf-poly1305 | 32 | 32 | 12 | 16 |
| AEAD_AES_256_GCM | aes-256-gcm | 32 | 32 | 12 | 16 |
| AEAD_AES_192_GCM | aes-192-gcm | 24 | 24 | 12 | 16 |
| AEAD_AES_128_GCM | aes-128-gcm | 16 | 16 | 12 | 16 |

可选的加密方式：

| Name | Key Size | IV Length |
| aes-128-ctr | 16 | 16 |
| aes-192-ctr | 24 | 16 |
| aes-256-ctr | 32 | 16 |
| aes-128-cfb | 16 | 16 |
| aes-192-cfb | 24 | 16 |
| aes-256-cfb | 32 | 16 |
| camellia-128-cfb | 16 | 16 |
| camellia-192-cfb | 24 | 16 |
| camellia-256-cfb | 32 | 16 |
| chacha20-ietf | 32 | 12 |

不推荐加密方式：

| Name | Key Size | IV Length |
| bf-cfb | 16 | 8 |
| chacha20 | 32 | 8 |
| salsa20 | 32 | 8 |
| rc4-md5 | 16 | 16 |

**注意:** 官方软件源的[shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks)不支持全部加密方式，官方软件源Chacha20以及salsa20的支持可以安装libsodium（For salsa20 and chacha20 support） 。若对非主流加密方式有需求，可尝试[aur](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")中的[shadowsocks-nodejs](https://aur.archlinux.org/packages/shadowsocks-nodejs/)

加密类别列表参见[[1]](https://github.com/shadowsocks/shadowsocks/wiki/Encryption)。 并且可以使用[[2]](https://github.com/shadowsocks/shadowsocks-libev/blob/0437e05aa8ec7f36f1eeb8c366dfd2b2b3b0288b/scripts/iperf.sh)脚本来比较和找出在你机器上运行最快的加密方法。

#### 性能优化

*   多用户使用的情况下，建议使用[#多端口运行](#多端口运行)，尽量避免一个端口有过多用户连接。
*   使用[常用端口](https://www.google.com/search?newwindow=1&q=%E5%B8%B8%E7%94%A8%E7%AB%AF%E5%8F%A3%E5%8F%B7&oq=%E5%B8%B8%E7%94%A8%E7%AB%AF%E5%8F%A3%E5%8F%B7&gs_l=psy-ab.3...30218.34357.0.34596.9.8.1.0.0.0.552.2392.4-4j1.5.0....0...1.1.64.psy-ab..4.3.1400...35i39k1j0i5i30k1.0.tTk_3WbYY-g)如25、443、21等等，[GFW](https://zh.wikipedia.org/wiki/%E9%98%B2%E7%81%AB%E9%95%BF%E5%9F%8E)为减轻压力，对常用端口检查相对较少。
*   使用[python-gevent](https://www.archlinux.org/packages/?name=python-gevent)提升python的[shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks)运行的速度。
*   使用[python-pip](https://www.archlinux.org/packages/?name=python-pip)安装`M2Crypto`可略微提升加密速度；使用较弱的加密方式CR4-MD5提升加密速度（但是会降低安全程度，请根据实际使用情况考虑加密强度的选择）。
*   优化内核参数，参看[Optimizing-Shadowsocks](https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks)进行设置。
*   开启fast open降低延迟

```
 # echo 'net.ipv4.tcp_fastopen = 3' >> /etc/sysctl.d/tcp-fastopen.conf

```

*   开启TCP[BBR](https://github.com/google/bbr)拥塞控制算法

**注意:** 需要内核4.9及以上版本，可使用`uname -r`查看。

**警告:** 该算法增加发包率从而提升流量消耗;可能消耗更多的系统资源；如果使用openvz的服务器，不建议使用bbr，据反映容易导致判定为滥用而被服务商禁用。

```
 modprobe tcp_bbr
 echo "tcp_bbr" > /etc/modules-load.d/bbr.conf
 echo '
   net.core.default_qdisc=fq
   net.ipv4.tcp_congestion_control=bbr
 ' > /etc/sysctl.d/bbr.conf
 sysctl -p

```

检查:

```
 sysctl net.ipv4.tcp_available_congestion_control
 sysctl net.ipv4.tcp_congestion_control

```

如果结果都有 bbr字样, 则证明你的内核已开启 bbr。 执行`lsmod` ，看到有`tcp_bbr`模块即说明 bbr 已启动。

## 参阅

*   [shadowsocks announcement](https://www.v2ex.com/t/32777)
*   [shadowsocks@gitHub](https://github.com/clowwindy/shadowsocks)
*   [shadowsocks使用说明](https://github.com/clowwindy/shadowsocks/wiki/Shadowsocks-%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E)
*   [About Shadowsocks](http://blog.robotshell.org/2014/about-shadowsocks/)
*   [shadowsocks最新配置](http://blog.pcwuyu.com/index.php/Arch/archlinux-shadowsocks-configuration.html)
*   [Linux Kernel 4.9 中的 BBR 算法与之前的 TCP 拥塞控制相比有什么优势？](https://www.zhihu.com/question/53559433)