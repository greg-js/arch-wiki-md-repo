## Contents

*   [1 简单介绍](#.E7.AE.80.E5.8D.95.E4.BB.8B.E7.BB.8D)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 测试](#.E6.B5.8B.E8.AF.95)

# 简单介绍

telnet是一种基于TCP的传统命令行远程控制协议。telnet使用非加密的通道，因此不太安全。现在主要用于链接一些旧设备。

下面这些介绍主要适用于在Arch Linux系统中配置一个telnet服务器。

# 安装

如果只使用telnet联接到别的机器，只需要安装netkit-telnet即可：

```
# pacman -S inetutils

```

如果需要安装和配置telnet服务器，还需要安装xinetd：

```
# pacman -S xinetd

```

*   重要提示, "Telnetd是传统脚本，代码不佳并且不可信赖 - 除非不得已，否则不要运行他。" 引用自netkit-telnet的README文件。

如果你非得要telnet服务器，有一个更好的选择。安装AUR里面的telnet-bsd软件包取代netkit-telnet（同样也支持IPv6）。

# 配置

1\. 要允许通过xinetd联接telnet，需要编辑/etc/xinetd.d/telnet文件：

```
# vi /etc/xinetd.d/telnet

```

将'disable'的值从'yes'修改为'no'。

2\. 要允许telnet从其他机子联接到本机，需要添加允许规则。打开文件/etc/hosts.allow，添加如下行：

```
in.telnetd: ALL

```

3\. 如果需要开机自动开启该服务，将xinetd加入到/etc/rc.conf的"DAEMONS"中：

```
DAEMONS=(syslog-ng network netfs crond ............ xinetd)

```

4\. 重新启动电脑。或者重新启动xinetd（如下）：

```
# /etc/rc.d/xinetd restart

```

### 测试

先试试看在本地用telnet联接自己：

```
$ telnet localhost

```

提示：你不能通过telnet登录为根用户｛包括使用bsd telnet）。