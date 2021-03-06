锐捷是国内众多大学采用的拨号客户端，但其 Linux 版久无更新，很多使用它的用户无法通过认证，少数能通过但容易掉线。虽然网上第三方 Linux 版锐捷客户端不少，但都大同小异，难以通过锐捷的客户端校验。

本条目旨在提供一个在 Linux 下能与锐捷兼容性很好的认证客户端 MentoHUST 使用教程，方便 Arch Linux 用户实现锐捷拨号并上网。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置与运行](#.E9.85.8D.E7.BD.AE.E4.B8.8E.E8.BF.90.E8.A1.8C)
    *   [2.1 网络参数配置](#.E7.BD.91.E7.BB.9C.E5.8F.82.E6.95.B0.E9.85.8D.E7.BD.AE)
        *   [2.1.1 静态 IP 用户](#.E9.9D.99.E6.80.81_IP_.E7.94.A8.E6.88.B7)
        *   [2.1.2 动态 IP 用户](#.E5.8A.A8.E6.80.81_IP_.E7.94.A8.E6.88.B7)
    *   [2.2 MentoHUST 配置](#MentoHUST_.E9.85.8D.E7.BD.AE)
        *   [2.2.1 参数说明](#.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E)
        *   [2.2.2 示范](#.E7.A4.BA.E8.8C.83)
    *   [2.3 运行](#.E8.BF.90.E8.A1.8C)
*   [3 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [3.1 提示“在网卡 eth0 上获取 IP 失败”](#.E6.8F.90.E7.A4.BA.E2.80.9C.E5.9C.A8.E7.BD.91.E5.8D.A1_eth0_.E4.B8.8A.E8.8E.B7.E5.8F.96_IP_.E5.A4.B1.E8.B4.A5.E2.80.9D)
    *   [3.2 提示“IP 地址类型错误”](#.E6.8F.90.E7.A4.BA.E2.80.9CIP_.E5.9C.B0.E5.9D.80.E7.B1.BB.E5.9E.8B.E9.94.99.E8.AF.AF.E2.80.9D)
    *   [3.3 提示“IP 端口绑定错误"](#.E6.8F.90.E7.A4.BA.E2.80.9CIP_.E7.AB.AF.E5.8F.A3.E7.BB.91.E5.AE.9A.E9.94.99.E8.AF.AF.22)
    *   [3.4 提示“找不到服务器”](#.E6.8F.90.E7.A4.BA.E2.80.9C.E6.89.BE.E4.B8.8D.E5.88.B0.E6.9C.8D.E5.8A.A1.E5.99.A8.E2.80.9D)
    *   [3.5 提示“不允许使用的客户端类型”](#.E6.8F.90.E7.A4.BA.E2.80.9C.E4.B8.8D.E5.85.81.E8.AE.B8.E4.BD.BF.E7.94.A8.E7.9A.84.E5.AE.A2.E6.88.B7.E7.AB.AF.E7.B1.BB.E5.9E.8B.E2.80.9D)
    *   [3.6 提示“客户端版本过低”](#.E6.8F.90.E7.A4.BA.E2.80.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E7.89.88.E6.9C.AC.E8.BF.87.E4.BD.8E.E2.80.9D)
    *   [3.7 提示“客户端完整性被破坏”](#.E6.8F.90.E7.A4.BA.E2.80.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.AE.8C.E6.95.B4.E6.80.A7.E8.A2.AB.E7.A0.B4.E5.9D.8F.E2.80.9D)
    *   [3.8 认证成功但仍无法上网](#.E8.AE.A4.E8.AF.81.E6.88.90.E5.8A.9F.E4.BD.86.E4.BB.8D.E6.97.A0.E6.B3.95.E4.B8.8A.E7.BD.91)
*   [4 二次拨号](#.E4.BA.8C.E6.AC.A1.E6.8B.A8.E5.8F.B7)
*   [5 参见](#.E5.8F.82.E8.A7.81)

## 安装

安装 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 中的 [mentohust-git](https://aur.archlinux.org/packages/mentohust-git/) 即可。

**注意:** [mentohust-git](https://aur.archlinux.org/packages/mentohust-git/) 目前还在开发中，主要针对锐捷v4算法，暂不兼容旧版本的mentohust，若使用出现问题，可尝试旧版本的[mentohust](https://code.google.com/archive/p/mentohust/downloads),亦可安裝[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")中的旧版本[mentohust](https://aur.archlinux.org/packages/mentohust/) 。

## 配置与运行

### 网络参数配置

MentoHUST 直接依赖 Arch Linux 内置的相关网络参数，例如 IP、网关、DNS 等等，需要事先进行此方面的配置。

**注意:** 以下包含的 `eth0` 为一种网卡，且每种 PC 所拥有的网卡名称却不一定是这个，请自行执行 `ip link` 以查询本机上正确的网卡名称即可。

不论获取 IP 方式如何，用户需事先从校方相关部门索取用户名和密码。

#### 静态 IP 用户

首先一般需要事先从校方相关部门索取 IP、子网掩码、网关、DNS 信息等，不妨假设分别为 `10.10.45.49`，`24`，`10.10.173.1`，`210.32.24.21`，以及主机所用网络接口为`eth0`。执行以下命令设置即可：

启动网络接口

```
$ ip link set eth0 up

```

在其网络接口上设置 IP（后缀紧跟了子网掩码）

```
$ ip addr add 10.10.45.49/24 dev eth0

```

在路由表上添加网关记录

```
$ ip route add default via 10.10.45.1

```

在 `/etc/resolv.conf` 上添加 DNS 地址

```
$ echo "nameserver 210.32.24.21 > /etc/resolv.conf

```

#### 动态 IP 用户

首先同样地要启动网络接口

```
$ ip link set eth0 up

```

但无须设置其它网络参数，直接启动 dhpcd 即可：

```
$ systemctl start dhcpcd@eth0.service

```

### MentoHUST 配置

MentoHUST 参数丰富，以最大程度适应不同学校的不同锐捷认证环境。本程序使用配置文件 `/etc/mentohust.conf` 保存参数，虽然该配置文件是还算标准的 ini 格式文件，并不复杂。但还是有人因多加空格或；导致配置出现问题，所以不提倡手工修改配置文件来设置参数，而是直接靠命令参数配置。

#### 参数说明

`-h` 显示帮助信息。

`-k` MentoHUST 支持 daemon 运行，也就是认证成功后可以关闭终端而认证不会中断。当进入 daemon 运行方式后，是不能像没有进入这一模式时一样通过Ctrl+C退出的，这时如果需要退出，可以使用以下命令：

```
$ mentohust -k

```

或者

```
$ pkill mentohust

```

`-w` 在命令行参数中指定的参数默认不会保存到配置文件，如果需要保存，请加上该参数，例如下面这个命令将会把用户名更新为hust，密码更新为123456。

```
$ mentohust -u hust -p 123456 -w

```

`-u，-p，-n` 分别指定用户名、密码、网卡。如果均不指定，就会自动判断是否需要输入。

`-i，-m，-g，-s` 静态 IP 用户可通过这些参数分别指定学校分配的 IP、子网掩码、网关、DNS。但由于已经在[#网络参数配置](#.E7.BD.91.E7.BB.9C.E5.8F.82.E6.95.B0.E9.85.8D.E7.BD.AE)事先设定好，一般不用再考虑。

`-o` 指定智能重连时用来 ping 的目标 IP，例如未认证时，1.2.3.4 无法 ping 通，认证成功后可以 ping 通，就可以加上参数 `-o 1.2.3.4`，当掉线且未收到服务器下线通知时会在掉线1分钟之内重连。除非网络不好，一般不会掉线，掉线且收到服务器下线通知时会在掉线后立即重连。

`-t` 指定认证时多少秒后仍未收到服务器回应则重启认证，一般保持默认即可。

`-e` 指定认证成功后每隔多少秒向服务器发送一次数据以表明自己仍然在线，一般保持默认即可。

`-r` 由于有些学校会规定认证失败后一定时间内不允许再次认证，所以在这期间不论发多少数据服务器都不会响应，为了减少这种垃圾数据，MentoHUST 会在认证失败后等待一段时间或者服务器向客户端请求数据时再认证，这个时间就由此参数指定，一般保持默认即可。 `-r15` 并不是说在认证失败后15秒才会再次认证，如果在15秒内服务器发来一个数据包要求开始认证，MentoHUST会放弃等待，立即开始再次认证。

`-a` 指定组播地址或客户端类型，`-a0` 为标准 `-a1` 为锐捷私有，这两个分别对应于锐捷中的标准和私有，有些学校只能用标准，有些学校只能用私有，所以如果提示“找不到服务器”而网卡并没有选错，就检查是不是这里设置错了。`-a2` 表示将MentoHUST用于赛尔认证（赛尔用 `-a0` 标准也行）。

`-d` 指定 DHCP 方式，使用动态 IP 的同学应该在这里正确设置，一般不是 `1` 就是 `2`，如果用 `3` 认证成功却无法上网，请改成 `1` 试试。使用静态 IP 的同学应该将这里设为 `0`。

`-b` 指定后台（daemon）运行方式，`-b0` 不后台运行，认证成功后，不能关闭终端；`-b1`、`-b2` 均为后台运行，但前者无输出，后者则保留输出；`-b3` 后台运行并将输出保存到 `/tmp/mentohust.log`，可以随时打开该文件查看输出。

`-y` 指定是否显示通知（notify），`-y0` 不显示，`1~20` 显示，其中数字指定通知持续时间。

`-c` 指定动态 IP 用户 DHCP 时运行的脚本，一般保持默认即可。如果觉得这个输出太多影响用户，可以改为 `-cdhclient>/dev/null`。

`-q` 很多锐捷用户不清楚他们的 DHCP 方式是什么，本参数用于显示解密后的锐捷 `SuConfig.dat` 文件内容。假如锐捷所在目录为/path/to，则执行以下命令即可：

```
# mentohust -q '/path/to/SuConfig.dat'

```

#### 示范

某用户获取 IP 的方式是静态 IP，用户名为`hust`，密码为`123456`，ping 地址为`192.168.1.254`，同时以 deamon 方式保存输出到文件。

首先按[#网络参数配置](#.E7.BD.91.E7.BB.9C.E5.8F.82.E6.95.B0.E9.85.8D.E7.BD.AE)配置好 IP、网关、子网掩码、DNS 等，然后执行：

```
# mentohust -u hust -p 123456 -o 192.168.1.254 -b 3 -w

```

### 运行

```
$ systemctl start mentohust.service

```

若要开机自启动，执行以下一次即可：

```
$ systemctl enable mentohust.service

```

## 故障排除

### 提示“在网卡 eth0 上获取 IP 失败”

如果获取 IP 方式是是动态 IP 的话，无须理会；否则按[#网络参数配置](#.E7.BD.91.E7.BB.9C.E5.8F.82.E6.95.B0.E9.85.8D.E7.BD.AE)进行排错。

### 提示“IP 地址类型错误”

DHCP 方式设置错误。使用 `-q` 参数查看正确的 DHCP 方式并按需修改。

### 提示“IP 端口绑定错误"

若是静态 IP，原因是在 MentoHUST 中将绑定 IP 设置错误，可以通过 `-i` 参数修改。

### 提示“找不到服务器”

一般是选错了组播模式，在“标准”与“锐捷”中切换试试。

如果 ping 任何 IP 均出现 `Destination Host Unreacheable` 错误，请检查下网线。

### 提示“不允许使用的客户端类型”

学校禁用了 xrgsu ，使用 `-v` 参数指定版本号，或者复制相关文件（`8021x.exe` 和 `W32N55.dll`，可能还需要 `SuConfig.dat`）到 `/etc/mentohust/`。

### 提示“客户端版本过低”

和[#提示“不允许使用的客户端类型”](#.E6.8F.90.E7.A4.BA.E2.80.9C.E4.B8.8D.E5.85.81.E8.AE.B8.E4.BD.BF.E7.94.A8.E7.9A.84.E5.AE.A2.E6.88.B7.E7.AB.AF.E7.B1.BB.E5.9E.8B.E2.80.9D)的解决方法相同。

### 提示“客户端完整性被破坏”

说明校方开启了客户端校验，复制相关文件（`8021x.exe` 和 `W32N55.dll`，可能还需要 `SuConfig.dat`）到 `/etc/mentohust/`。

### 认证成功但仍无法上网

静态 IP 用户未正确设置 IP 及 DNS，或动态 IP 用户未能正确地获取到 IP 及 DNS。

## 二次拨号

可参见 [MentoHUST 及『二次撥號』的臨時解決方案](http://arch.acgtyrant.com/2014/02/23/mentohust-and-l2tp/)

## 参见

MentoHUST 在 [Google Code 的主页](https://code.google.com/p/mentohust/)

Ubuntu Wiki 条目[『锐捷、赛尔认证MentoHUST』](http://wiki.ubuntu.org.cn/%E9%94%90%E6%8D%B7%E3%80%81%E8%B5%9B%E5%B0%94%E8%AE%A4%E8%AF%81MentoHUST)

[acgtyrant 在浙江理工大学进行锐捷拨号的自动化脚本](https://github.com/acgtyrant/bin/blob/master/mentohust.sh)