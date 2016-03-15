pptpclient是一个实现Microsoft PPTP协议的程序。因此它能够被用来接入另一个Microsoft VPN网络，比如学校和单位。

## Contents

*   [1 安装PPTPClient](#.E5.AE.89.E8.A3.85PPTPClient)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 编辑配置文件](#.E7.BC.96.E8.BE.91.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [2.2 编辑密码文件](#.E7.BC.96.E8.BE.91.E5.AF.86.E7.A0.81.E6.96.87.E4.BB.B6)
    *   [2.3 命名你的VPN隧道](#.E5.91.BD.E5.90.8D.E4.BD.A0.E7.9A.84VPN.E9.9A.A7.E9.81.93)
*   [3 创建你的连接](#.E5.88.9B.E5.BB.BA.E4.BD.A0.E7.9A.84.E8.BF.9E.E6.8E.A5)
    *   [3.1 配置路由](#.E9.85.8D.E7.BD.AE.E8.B7.AF.E7.94.B1)
        *   [3.1.1 选择路由](#.E9.80.89.E6.8B.A9.E8.B7.AF.E7.94.B1)
        *   [3.1.2 配置为默认路由](#.E9.85.8D.E7.BD.AE.E4.B8.BA.E9.BB.98.E8.AE.A4.E8.B7.AF.E7.94.B1)
        *   [3.1.3 使用ip-up.d设置默认路由](#.E4.BD.BF.E7.94.A8ip-up.d.E8.AE.BE.E7.BD.AE.E9.BB.98.E8.AE.A4.E8.B7.AF.E7.94.B1)
*   [4 断开连接](#.E6.96.AD.E5.BC.80.E8.BF.9E.E6.8E.A5)
*   [5 把一个VPN连接配为默认启动](#.E6.8A.8A.E4.B8.80.E4.B8.AAVPN.E8.BF.9E.E6.8E.A5.E9.85.8D.E4.B8.BA.E9.BB.98.E8.AE.A4.E5.90.AF.E5.8A.A8)
*   [6 注意](#.E6.B3.A8.E6.84.8F)

## 安装PPTPClient

pptpclient由安装包pptpclient提供，运行下列命令可以安装：

```
# pacman -S pptpclient

```

## 配置

你需要从网络管理员获取以下信息来配置pptpclient:

*   VPN服务器的ip或者域名
*   VPN隧道名称
*   Windows域（不是所有网络都需要）
*   VPN用户名
*   VPN密码

### 编辑配置文件

用你称手的编辑器打开/etc/ppp/options.pptp。这个文件为你的VPN连接启用了一系列默认安全设置。如果你连接时候出现问题，你可以自定义配置。你的options.pptp文件最少需要包含以下内容：

```
lock
noauth
nobsdcomp
nodeflate

```

### 编辑密码文件

下一步，打开或者创建/etc/ppp/chap-secrets。我们将在这个文件里面存储你的密码，记得修改权限让除root之外所有用户不能访问它。这个文件的格式如下：

```
<DOMAIN>\\<USERNAME> PPTP <PASSWORD> *

```

如果你的服务器不要求域，则配置如下：

```
<USERNAME> PPTP <PASSWORD> *

```

替换掉上文中范例中的占位符。注意，如果你的密码包含特殊字符，比如“$”，你需要用双引号把它们包起来。

### 命名你的VPN隧道

用你称手的编辑器创建类似/etc/ppp/peers/<TUNNEL>的文件，把<TUNNEL>这里替换成你的VPN连接名。这个文件设置之后看起来如下：

```
pty "pptp <SERVER> --nolaunchpppd"
name <DOMAIN>\\<USERNAME>
remotename PPTP
require-mppe-128
file /etc/ppp/options.pptp
ipparam <TUNNEL>

```

**注意:** 跟刚才一样，如果你的连接不要求域，忽略范例中的"<DOMAIN>\\"

**注意:** PPTP远程主机使用Chap-Secrets文件中的<PASSWORD>

<SERVER>是VPN服务器的地址，<DOMAIN>是你所属的域，<USERNAME>是你将要用来连接服务器的用户名，<TUNNEL>是连接的名称。

**注意:** 如果你不需要使用MPPE，你应当从/etc/ppp/options.pptp中移除require-mppe-128这个选项

## 创建你的连接

用root执行以下命令来确保配置是正确的：

```
# pon $TUNNEL debug dump logfd 2 nodetach

```

如果一切都配置好了，pon命令应当不会自动结束。一旦你感觉差不多OK了，就可以终止这个命令。

**注意:** 另一个用来确保配置正确的命令是ifconfig -a，看看里面时候有一个名叫ppp0的新驱动，并且还是可用的

执行以下命令来连接VPN隧道：

```
# pon <TUNNEL>

```

<TUNNEL>是你之前命名过的VPN隧道名称。注意使用root命令执行。

### 配置路由

一旦你成功连接上VPN，你就可以和VPN服务器交互了。当然在此之前，咱们需要添加一个新的路由到你的路由表，从而可以接入远程网络。

**注意:** 根据你的环境配置，你可能需要每次都重复添加路由信息

你可以阅读[PPTP Routing Howto](http://pptpclient.sourceforge.net/routing.phtml)来获得更多如何添加路由的信息，里面还有很多范例。

#### 选择路由

对我来说，只有传输到VPN网络的数据包才应该走VPN连接，所以我添加如下路由条目：

```
# ip route add 192.168.10.0/24 dev ppp0

```

这将路由所有目的地址为191.168.10.xxx的数据到VPN连接。

#### 配置为默认路由

如果你想要所有数据从VPN连接走，下面这条命令包你爽：

```
# ip route add default dev ppp0

```

**注意:** 所有数据从VPN连接走的话会比正常连接慢一些

#### 使用ip-up.d设置默认路由

**注意:** /etc/ppp/ip-up.d/下所有脚本将在VPN连接建立的时候自动执行

```
#!/bin/bash

# This script is called with the following arguments:
# Arg Name
# $1 接口名字
# $2 The tty
# $3 连接速度
# $4 本地ip地址
# $5 Peer IP number
# $6 可选``ipparam'' 的参数

route add default gw $4

```

把这个脚本命名为01-routes.sh,然后放在/etc/ppp/ip-up.d/下面。

## 断开连接

下面这条命令用来断开VPN连接：

```
# poff <TUNNEL>

```

<TUNNEL>是你VPN连接的名称。

## 把一个VPN连接配为默认启动

你可以在rc.d创建一个快捷命令来实现自动在后台连接VPN网络。

**注意:** 和平常一样，<TUNNEL>是你隧道的名字，<ROUTING COMMAND>是你加入路由表的命令。

```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

DAEMON=<TUNNEL>-vpn
ARGS=

[ -r /etc/conf.d/$DAEMON ] && . /etc/conf.d/$DAEMON

case "$1" in
 start)
   stat_busy "Starting $DAEMON"
   pon <TUNNEL> updetach persist &> /dev/null && <ROUTING COMMAND> &>/dev/null
   if [ $? = 0 ]; then
     add_daemon $DAEMON
     stat_done
   else
     stat_fail
     exit 1
   fi
   ;;
 stop)
   stat_busy "Stopping $DAEMON"
   poff MST &>/dev/null
   if [ $? = 0 ]; then
     rm_daemon $DAEMON
     stat_done
   else
     stat_fail
     exit 1
   fi
   ;;
 restart)
   $0 stop
   sleep 1
   $0 start
   ;;
 *)
   echo "usage: $0 {start|stop|restart}"  
esac

```

注意，我们可以使用updetach和persist这两个附加命令在pon上。updetach保证pon阻塞知道连接被建立。另外一个命令persist保证网络自动重练。如果需要开机自动启动，则添加@<TUNNEL>-vpn到rc.conf的DAEMONS中去。

## 注意

你可以在[pptpclient website](http://pptpclient.sourceforge.net/)查到更多关于pptpclient的配置信息。Ubuntu的帮助手册也有一些帮助你配置的信息。这些范例能够很轻松的稍加变换从而添加到daemons中去，从而帮助你自动化运行。