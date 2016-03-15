## Contents

*   [1 什么是 user-mode-linux?](#.E4.BB.80.E4.B9.88.E6.98.AF_user-mode-linux.3F)
*   [2 为什么使用 UML?](#.E4.B8.BA.E4.BB.80.E4.B9.88.E4.BD.BF.E7.94.A8_UML.3F)
*   [3 HOWTO](#HOWTO)
*   [4 运行所需:](#.E8.BF.90.E8.A1.8C.E6.89.80.E9.9C.80:)
*   [5 现在开始](#.E7.8E.B0.E5.9C.A8.E5.BC.80.E5.A7.8B)

#### 什么是 user-mode-linux?

User-mode-linux (UML) 是让一个linux作为一个独立进程运行在另一个linux上。 请在[[1]](http://user-mode-linux.sourceforge.net/) 查找 uml 的详细安装使用指南。
这篇 wiki 文章是 [这帖](https://bbs.archlinux.org/viewtopic.php?t=12553) 概要。 如果你有任何意见和建议可以在这回帖。

#### 为什么使用 UML?

UML 是一种在同一时间运行多 (arch-)linux 的安全方式。 每个进程都是独立去其它的， 这非常安全，例如在同一机器上进行多种测试和开发而不互相干扰。如果一些测试进程损坏并不会影响宿主系统或者开发用进程。

#### HOWTO

#### 运行所需:

*   User-mode-linux 内核(pacman -S user-mode-linux 就可以)
*   uml_工具, 特别使 tunctl 程序 (会在安装 uml 内核后有)
*   [archbootstrap 脚本](http://painkiller.one.pl/~lucke/archbootstrap). 在 [这个主题](https://bbs.archlinux.org/viewtopic.php?t=4020) 进行讨论.

#### 现在开始

1.) 首先要创建一个独立、大的文件用来安装 arch。 如下命令会创建一个独立的空的 1GB 文件 - 应该足够安装一个基 arch 系统。

```
dd if=/dev/zero of=archRootFs bs=1MB count=1000

```

2.) 当创建完成后格式化。 如下命令将会提示 archRootFs 不是一个 block 设备。 你可以完全忽略或者加入 *-F* 来使 mke2fs 可以屏蔽提示信息。

```
mke2fs archRootFS

```

3.) 格式化后加载它。 以root用户执行如下命令:

```
mount -o loop archRootFs /mnt

```

4.) 现在开始基本系统安装。您可以用 archbootstrap 脚本， 这会象光盘安装一样，不同的是这个安装从指定目录开始。这是一个真实的基本系统安装 - 因而会花费一点时间！

```
sh archbootstrap /mnt/ ftp://archlinux-mirror

```

5.) 在系统以 user-mode-linux 模式启动之前, 一些 arch 基本系统文件要求定制。 在 */mnt/etc/fstab* 加入:

```
/dev/ubd0 / ext2 defaults 0 0

```

可以通过禁用 hotplugin 来加快启动时间，在 */mnt/etc/rc.conf* 加入:

```
DAEMONS=(syslog-ng !hotplug !pcmcia network netfs crond)

```

6.) 卸载文件系统。 **注意:** 如果你在加载的系统中改变了 *任何东西* (例如 /mnt) 而它正在 *运行*，则很有可能 *毁了* 它 !

```
umount /mnt

```
7.) 下一步是配置网络。 因此您要创建 tun 设备 (请阅读 [[uml howto](http://user-mode-linux.sourceforge.net/UserModeLinux-HOWTO-6.html)] 得到具体的 tun/tap 信息)， 分配一个 IP 地址。 如下命令将会创建 tun/tap 设备并让普通用户能够使用，然后分配 ip 地址。为了安全起见您最好建立一个 uml 用户组并赋予使用网络设备的权限。
```
modprobe tun
tunctl -u users
chown root.users /dev/net/tun
ip addr add 192.168.0.100/24 dev tap0

```

8.) 现在可以启动镜像。为了使用网络，您要在 uml 内核中声明正确的设备值。 (确保普通用户通过运行 uml 命令有足够的权限使用网络！)

```
linux ubd0=archRootFs eth0=tuntap,,,192.168.0.100

```

",,," 意思是:

```
eth0=transport,tuntap device,MAC adress,ip

```

例如:

```
eth0=tuntap,tap0,3f:2a:bb:00:00:00,192.168.3.23

```

祝您开心使用 uml。