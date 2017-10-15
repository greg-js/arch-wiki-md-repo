**翻译状态：** 本文是英文页面 [Shadowsocks](/index.php/Shadowsocks "Shadowsocks") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-9-26，点击[这里](https://wiki.archlinux.org/index.php?title=Shadowsocks&diff=0&oldid=472909)可以查看翻译后英文页面的改动。

[Shadowsocks](https://github.com/clowwindy/shadowsocks/)是一个轻量级[socks5](https://en.wikipedia.org/wiki/SOCKS_(protocol)#SOCKS5 "wikipedia:SOCKS (protocol)")代理，最初用 Python 编写。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [2.1.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C)
        *   [2.1.2 以守护进程形式运行客户端](#.E4.BB.A5.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E5.BD.A2.E5.BC.8F.E8.BF.90.E8.A1.8C.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [2.1.3 图形界面客户端](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [2.1.4 配置代理](#.E9.85.8D.E7.BD.AE.E4.BB.A3.E7.90.86)
            *   [2.1.4.1 浏览器配置](#.E6.B5.8F.E8.A7.88.E5.99.A8.E9.85.8D.E7.BD.AE)
    *   [2.2 服务端](#.E6.9C.8D.E5.8A.A1.E7.AB.AF)
        *   [2.2.1 以命令行启动进程](#.E4.BB.A5.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.90.AF.E5.8A.A8.E8.BF.9B.E7.A8.8B)
        *   [2.2.2 以守护进程形式运行](#.E4.BB.A5.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E5.BD.A2.E5.BC.8F.E8.BF.90.E8.A1.8C)
        *   [2.2.3 多端口运行](#.E5.A4.9A.E7.AB.AF.E5.8F.A3.E8.BF.90.E8.A1.8C)
        *   [2.2.4 加密方法](#.E5.8A.A0.E5.AF.86.E6.96.B9.E6.B3.95)
        *   [2.2.5 性能优化](#.E6.80.A7.E8.83.BD.E4.BC.98.E5.8C.96)
*   [3 参阅](#.E5.8F.82.E9.98.85)

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

要更改日志等级，应添加 `"verbose": *value*` 选项并赋予下列某一个值：

*   2: full logging
*   1: debug
*   0: default
*   -1: warnings
*   -2: errors

### 客户端

#### 命令行

运行 `ss-local` 启动客户端；若需指定配置文件的位置：

 `# sslocal -c /etc/shadowsocks/config.json` 
**注意:** 有用户报告无法成功在运行时加载`config.json`
，或可尝试手动运行： `# sslocal -s *服务器地址* -p *服务器端口* -l *本地端端口* -k *密码* -m *加密方法*` 

配合nohup和&可以使之后台运行，关闭终端也不影响：

 `#nohup sslocal -s *服务器地址* -p *服务器端口* -l *本地端端口* -k *密码* -m *加密方法* &` 

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

使用[Iptables_(简体中文)](/index.php/Iptables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Iptables (简体中文)")等工具，桌面环境用户可使用桌面设置中网络设置里的代理功能。

**注意:** 使用全局代理会使所有的连接通过shadowsocks服务器中转，一般不建议使用全局代理。

*   程序设置自身代理

不少程序都能在其设置中添加代理，只需要在其设置中找到网络相关配置，添加socks v5代理，参照本地配置文件中的ip和port填写即可。例如浏览器的配置可参考下文[Shadowsocks_(简体中文)#浏览器配置](/index.php/Shadowsocks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.B5.8F.E8.A7.88.E5.99.A8.E9.85.8D.E7.BD.AE "Shadowsocks (简体中文)")）。

*   使用工具进行临时代理

例如[proxychains](https://www.archlinux.org/packages/?name=proxychains)（参看[Proxy_settings#Using_a_SOCKS_proxy](/index.php/Proxy_settings#Using_a_SOCKS_proxy "Proxy settings")）和[redsocks-git](https://aur.archlinux.org/packages/redsocks-git/)。

*   转换为http代理

直接指走socks代理似乎不能远程dns解析，这未必是用户的期望（尤其是在浏览器上使用时），可使用privoxy等软件转化socks代理为http代理。可使用[privoxy](https://www.archlinux.org/packages/?name=privoxy)和[squid](https://www.archlinux.org/packages/?name=squid)。 以[Privoxy](/index.php/Privoxy "Privoxy")为例，编辑privoxy配置文件，添加socks5转发（不要漏下1080后面的点)：

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

**提示：** 浏览器直接使用[SOCKS](https://en.wikipedia.org/wiki/SOCKS "wikipedia:SOCKS")代理时，你可能需要使用[privoxy](/index.php/Privoxy "Privoxy")等辅助程序，因为一般浏览器会泄漏你的DNS请求，从而减少你的匿名，参看前文[Shadowsocks_(简体中文)#配置代理](/index.php/Shadowsocks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E9.85.8D.E7.BD.AE.E4.BB.A3.E7.90.86 "Shadowsocks (简体中文)")中转化为http代理一节。

*   firefox

可使用firefox的连接设置，打开设置-高级-连接，在其中选用socks v5进行配置。 或者使用扩展，以foxyproxy为例： 安装[foxyproxy](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/?src=userprofile)：打开浏览器右上角菜单，进入扩展管理，在搜索框中输入foxyproxy，安装foxyproxy，添加socks v5代理。

订阅白名单规则，以gfwlist为例，可从[gfwlist](https://github.com/gfwlist/gfwlist)]获取被屏蔽的网址规则列表，点击该项目的gfwlist.txt文件，进入后点击"raw"查看源码，可从浏览器地址栏获取[该文件URL](https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt)。然后打开foxyproxy,在规则订阅（pattern subscrib)选项卡中添加一个新的订阅规则，规则订阅URL栏填写刚才用"raw"查看的[gfwlist.txt地址](https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt)，代理项选择使先前添加的socks v5代理，设置一个自动更新规则的间隔时间（Refresh Rate），格式（Format)选择FoxyProxy，混淆（obfuscation）选择Base64，保存后使其生效。

其余扩展使用方法类似，例如switchyomega可参照下文chromium中的switchyomega设置。

*   Chrome/Chromium

[Chrome/Chromium](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)")使用使用插件switchomega配置示例例：

安装 [Proxy SwitchyOmega插件](https://chrome.google.com/webstore/detail/padekgcemlokbadohgkifijomclgjgif)（[Proxy SwitchySharp](https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm)已停止维护），若商店打不开的话可以直接下载Github上面的[crx文件](https://github.com/FelisCatus/SwitchyOmega/releases)可参考[该扩展提供的图解流程](https://github.com/FelisCatus/SwitchyOmega)。

添加gfwlist规则：参阅[Google Chrome + SwitchyOmega + GFWList](https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList)

### 服务端

**提示：** 普通用户无需配置服务端；

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
 # ssserver -c /etc/shadowsocks/foo.json -d start  #停止
 # ssserver -c /etc/shadowsocks/foo.json -d start  #重启

```

*   使用systemd

```
# systemctl start shadowsocks-server@foo  #立即启动
# systemctl enable shadowsocks-server@foo  #开机自启动

```

**注意:** 如果使用[shadowsocks-libev](https://www.archlinux.org/packages/?name=shadowsocks-libev)，则使用`shadowsocks-libev-server`替代`shadowsocks-server`。

**提示：** 如果使用的服务端端口号小于1024，需要修改`usr/lib/systemd/system/shadowsocks-server@.service`使得`user=root`，之后使用`systemctl daemon-reload`重新载入守护进程配置，即可开启监听。当然也可以用**root**权限运行shadowsocks，来开启端口号小于1024的监听。

#### 多端口运行

**注意:** [shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks)和[shadowsocks-go-server](https://aur.archlinux.org/packages/shadowsocks-go-server/)等支持多端口，而[shadowsocks-libev](https://www.archlinux.org/packages/?name=shadowsocks-libev)不支持，可到[Configure-Multiple-Users](https://github.com/shadowsocks/shadowsocks/wiki/Configure-Multiple-Users)查看哪些版本支持多端口。

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

**提示：** 有反映多端口配置后使用systemd进行守护进程运行会失败，可使用`-d`参数方法[#以守护进程形式运行](#.E4.BB.A5.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E5.BD.A2.E5.BC.8F.E8.BF.90.E8.A1.8C)。

#### 加密方法

**注意:** 默认加密方法`table`速度很快，但很不安全。请不要使用`rc4`，它不安全。

**提示：** 安装`M2Crypto`可略微提升加密速度，对于Python2来说，安装[python2-m2crypto](https://www.archlinux.org/packages/?name=python2-m2crypto)即可。

可选的加密方式：

*   aes-256-cfb（Shadowsocks经典、传统的加密算法，也是Shadowsocks的作者推荐过的加密算法，移动平台可能开销稍高）
*   aes-128-cfb
*   aes-192-cfb
*   aes-256-ofb
*   aes-128-ofb
*   aes-192-ofb
*   aes-128-ctr
*   aes-192-ctr
*   aes-256-ctr
*   aes-128-cfb8
*   aes-192-cfb8
*   aes-256-cfb8
*   aes-128-cfb1
*   aes-192-cfb1
*   aes-256-cfb1
*   aes-256-gcm
*   aes-128-gcm
*   aes-192-gcm
*   bf-cfb
*   camellia-128-cfb
*   camellia-192-cfb
*   camellia-256-cfb
*   cast5-cfb
*   chacha20
*   idea-cfb
*   rc2-cfb
*   rc4-md5
*   salsa20
*   seed-cfb

**注意:** 官方软件源的[shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks)不支持全部加密方式，官方软件源Chacha20以及salsa20的支持可以安装libsodium（For salsa20 and chacha20 support） 。若对非主流加密方式有需求，可尝试[aur](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")中的[shadowsocks-nodejs](https://aur.archlinux.org/packages/shadowsocks-nodejs/)

加密类别列表参见[[1]](https://github.com/shadowsocks/shadowsocks/wiki/Encryption)。 并且可以使用[[2]](https://github.com/shadowsocks/shadowsocks-libev/blob/0437e05aa8ec7f36f1eeb8c366dfd2b2b3b0288b/scripts/iperf.sh)脚本来比较和找出在你机器上运行最快的加密方法。

#### 性能优化

*   多用户使用的情况下，简易使用[#多端口运行]，尽量避免一个端口有过多用户连接。
*   使用[常用端口](https://www.google.com/search?newwindow=1&q=%E5%B8%B8%E7%94%A8%E7%AB%AF%E5%8F%A3%E5%8F%B7&oq=%E5%B8%B8%E7%94%A8%E7%AB%AF%E5%8F%A3%E5%8F%B7&gs_l=psy-ab.3...30218.34357.0.34596.9.8.1.0.0.0.552.2392.4-4j1.5.0....0...1.1.64.psy-ab..4.3.1400...35i39k1j0i5i30k1.0.tTk_3WbYY-g)（如25、443、21等等），[GFW](https://zh.wikipedia.org/wiki/%E9%98%B2%E7%81%AB%E9%95%BF%E5%9F%8E)为减轻压力，对常用端口检查相对较少。
*   使用[python-gevent](https://www.archlinux.org/packages/?name=python-gevent)提升python的[shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks)运行的速度。
*   使用[python-pip](https://www.archlinux.org/packages/?name=python-pip)安装`M2Crypto`可略微提升加密速度；使用较弱的加密方式CR4-MD5提升加密速度（请根据实际使用情况考虑加密强度的选择）。
*   优化内核参数，参看[Optimizing-Shadowsocks](https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks)进行设置。
*   开启fast open降低延迟

```
 # echo 'net.ipv4.tcp_fastopen = 3' >> /etc/sysctl.conf

```

*   开启TCP[BBR](https://github.com/google/bbr)拥塞控制算法

**注意:** 需要内核4.9及以上版本，可使用`uname -r`查看。

**警告:** 该算法增加发包率从何提升流量消耗;可能消耗更多的系统资源；如果使用openvz的服务器，不建议使用bbr，据反映容易导致判定为滥用而被服务商禁用。

```
 modprobe tcp_bbr
 echo "tcp_bbr" >> /etc/modules-load.d/modules.conf
 echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
 echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
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