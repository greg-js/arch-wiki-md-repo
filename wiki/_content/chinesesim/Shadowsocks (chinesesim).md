[Shadowsocks](https://github.com/clowwindy/shadowsocks/)是一个轻量级[socks5](https://en.wikipedia.org/wiki/SOCKS_(protocol)#SOCKS5 "wikipedia:SOCKS (protocol)")代理，以python写成；

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [2.2 服务端](#.E6.9C.8D.E5.8A.A1.E7.AB.AF)
    *   [2.3 以守护进程形式运行客户端](#.E4.BB.A5.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E5.BD.A2.E5.BC.8F.E8.BF.90.E8.A1.8C.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [2.4 以守护进程形式运行服务端](#.E4.BB.A5.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E5.BD.A2.E5.BC.8F.E8.BF.90.E8.A1.8C.E6.9C.8D.E5.8A.A1.E7.AB.AF)
    *   [2.5 加密](#.E5.8A.A0.E5.AF.86)
    *   [2.6 Chrome/Chromium](#Chrome.2FChromium)
*   [3 参阅](#.E5.8F.82.E9.98.85)

## 安装

可自[community]中安装已打包好的shadowsocks。

| [shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks) | shadowsocks基本包； |
| [libsodium](https://www.archlinux.org/packages/?name=libsodium)
[python2-numpy](https://www.archlinux.org/packages/?name=python2-numpy)
[python2-salsa20](https://www.archlinux.org/packages/?name=python2-salsa20) | [Salsa20和Chacha20](https://github.com/shadowsocks/shadowsocks/wiki/Encryption)支持； |

## 配置

shadowsocks以[json](https://en.wikipedia.org/wiki/JSON "wikipedia:JSON")为配置文件格式，以下是一个样例：

 `/etc/shadowsocks/config.json` 
```
{
	"server":"remote-shadowsocks-server-ip-addr",
	"server_port":443,
	"local_address":"127.0.0.1",
	"local_port":1080,
	"password":"your-passwd",
	"timeout":300,
	"method":"aes-256-cfb",
	"fast_open":false,
	"workers":1
}

```

**提示:** 若需同时指定多个服务端ip，可参考`"server":["1.1.1.1","2.2.2.2"],`

| server | 服务端监听地址(IPv4或IPv6) |
| server_port | 服务端端口，一般为`443` |
| local_address | 本地监听地址，缺省为`127.0.0.1` |
| local_port | 本地监听端口，一般为`1080` |
| password | 用以加密的密匙 |
| timeout | 超时时间（秒） |
| method | 加密方法，默认的`table`是一种不安全的加密，此处首推`aes-256-cfb` |
| fast_open | 是否启用[TCP-Fast-Open](https://github.com/clowwindy/shadowsocks/wiki/TCP-Fast-Open) |
| wokers | worker数量，如果不理解含义请不要改 |

### 客户端

在`config.json`所在目录下运行`sslocal`即可；若需指定配置文件的位置：

 `# sslocal -c /etc/shadowsocks/config.json` 
**注意:** 有用户报告无法成功在运行时加载`config.json`
，或可尝试手动运行： `# sslocal -s *服务器地址* -p *服务器端口* -l *本地端端口* -k *密码* -m *加密方法*` 

配合nohup和&可以使之后台运行，关闭终端也不影响：

 `#nohup sslocal -s *服务器地址* -p *服务器端口* -l *本地端端口* -k *密码* -m *加密方法* &` 

* * *

**提示:** 当然也有图形化的使用[shadowsocks-gui@gitHub](https://github.com/shadowsocks/shadowsocks-gui),如果不希望自己编译的话，也可以到[shadowsocks-gui@sourceforge](http://sourceforge.net/projects/shadowsocksgui/files/dist/)下载。

* * *

由于作者被相关部门请去喝茶，出于某些原因，其项目已经从github移除,但仍然可以从aur中下载安装

对debian用户的友情提示，由于源中没有shadowsocks-qt5，可到unbuntu的源中下载，下载[shadowsocks-qt5以及libqtshadowsocks](https://launchpad.net/shadowsocks-qt5/+packages)，使用dpkg命令或者借助gdebi点击安装。

* * *

### 服务端

**提示:** 普通用户无需配置服务端；

在服务器上`cd`到`config.json`所在目录：

1.  运行`ssserver`；
2.  如果想在后台一直运行，可改执行：`nohup ssserver > log &`；

### 以守护进程形式运行客户端

Shadowsocks的[systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")服务可在`/etc/shadowsocks/`里调用不同的`*conf-file*.json`（以`*conf-file*`为区分标志），例： 在`/etc/shadowsocks/`中创建了`foo.json`配置文件，那么执行以下语句就可以调用该配置：

```
# systemctl start shadowsocks@foo

```

若需开机自启动：

```
# systemctl enable shadowsocks@foo

```

**提示:** 可用`journalctl -u shadowsocks@foo`来查询日志；

### 以守护进程形式运行服务端

以上只是启动了客户端的守护进程，如果架设的是服务器，则需要：

```
# systemctl start shadowsocks-server@foo
# systemctl enable shadowsocks-server@foo

```

**提示:** 如果使用的服务端端口号小于1024，需要修改`usr/lib/systemd/system/shadowsocks-server@.service`使得`user=root`，之后使用`systemctl daemon-reload`重新载入守护进程配置，即可开启监听。

### 加密

**注意:** 默认加密方法`table`速度很快，但很不安全。如果CPU支持AES硬件加速的话，推荐使用`aes-128-cfb`。如果是旧CPU（不支持AES硬件加速），ChaCha20是占用最小速度最快的一种方式。其实选择`aes-256-cfb`可能对速度几乎没有影响。请不要使用`rc4`，它不安全。

**提示:** 安装`M2Crypto`可略微提升加密速度，对于Python2来说，安装[python2-m2crypto](https://www.archlinux.org/packages/?name=python2-m2crypto)即可。

可选的加密方式：

*   aes-256-cfb: 默认加密方式
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
,

### Chrome/Chromium

至此，本地监听端口`127.0.0.1:1080`已配置完毕。现以[Chrome/Chromium](/index.php/Chromium_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Chromium (简体中文)")为例，示范使用代理服务器的方法。

方法一：

请安装 [Proxy SwitchyOmega插件](https://chrome.google.com/webstore/detail/padekgcemlokbadohgkifijomclgjgif)（SwitchySharp已停止开发），若商店打不开的话可以直接下载Github上面的[crx文件](https://github.com/FelisCatus/SwitchyOmega/releases)可参考[该扩展提供的图解流程](https://github.com/FelisCatus/SwitchyOmega)。

另外提供老版[Proxy SwitchySharp扩展](https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm)因为它诞生早，经过了更多用户的考验，且基本功能完备。

方法二：

1.直接指定Chromium走socks代理似乎不能远程dns解析，这未必是用户的期望，可使用privoxy等软件转化socks代理为http代理。

编辑privoxy配置文件（不要漏下1080后面的点)

 `/etc/privoxy/config` 
```
forward-socks5   /               127.0.0.1:1080 .
listen-address  127.0.0.1:8118
```

重启服务应用更改：

```
# /etc/init.d/privoxy restart

```

2.假设转化后的http代理为127.0.0.1:8118，则在终端中启动：

```
$ chromium %U --proxy-server=127.0.0.1:8118

```

## 参阅

*   [shadowsocks announcement](https://www.v2ex.com/t/32777)
*   [shadowsocks@gitHub](https://github.com/clowwindy/shadowsocks)
*   [shadowsocks使用说明](https://github.com/clowwindy/shadowsocks/wiki/Shadowsocks-%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E)
*   [About Shadowsocks](http://blog.robotshell.org/2014/about-shadowsocks/)
*   [shadowsocks最新配置](http://blog.pcwuyu.com/index.php/Arch/archlinux-shadowsocks-configuration.html)