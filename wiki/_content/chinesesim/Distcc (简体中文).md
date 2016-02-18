Distcc 是一个将 C、C++、Objective C 或 Objective C++ 等程序的编译任务分发到网络中多个主机的程序。distcc 的结果和本地编译一模一样，安装后使用方便，通常比本地编译快很多。

## Contents

*   [1 名词定义](#.E5.90.8D.E8.AF.8D.E5.AE.9A.E4.B9.89)
*   [2 开始](#.E5.BC.80.E5.A7.8B)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 Daemon 和 Server 配置](#Daemon_.E5.92.8C_Server_.E9.85.8D.E7.BD.AE)
    *   [3.2 Daemon 配置](#Daemon_.E9.85.8D.E7.BD.AE)
*   [4 添加Daemon](#.E6.B7.BB.E5.8A.A0Daemon)
*   [5 编译](#.E7.BC.96.E8.AF.91)
*   [6 监视进度](#.E7.9B.91.E8.A7.86.E8.BF.9B.E5.BA.A6)
*   [7 为每个编译任务使用distcc](#.E4.B8.BA.E6.AF.8F.E4.B8.AA.E7.BC.96.E8.AF.91.E4.BB.BB.E5.8A.A1.E4.BD.BF.E7.94.A8distcc)
*   [8 技巧](#.E6.8A.80.E5.B7.A7)
    *   [8.1 限制硬盘使用](#.E9.99.90.E5.88.B6.E7.A1.AC.E7.9B.98.E4.BD.BF.E7.94.A8)
        *   [8.1.1 修改 $HOME/.distcc 位置](#.E4.BF.AE.E6.94.B9_.24HOME.2F.distcc_.E4.BD.8D.E7.BD.AE)
        *   [8.1.2 修改日志级别](#.E4.BF.AE.E6.94.B9.E6.97.A5.E5.BF.97.E7.BA.A7.E5.88.AB)
*   [9 在使用CMake等工具时出现无法编译的错误](#.E5.9C.A8.E4.BD.BF.E7.94.A8CMake.E7.AD.89.E5.B7.A5.E5.85.B7.E6.97.B6.E5.87.BA.E7.8E.B0.E6.97.A0.E6.B3.95.E7.BC.96.E8.AF.91.E7.9A.84.E9.94.99.E8.AF.AF)

## 名词定义

	distcc daemon

	运行着distcc的计算机与服务器分布式的编译代码. daemon编译一部分代源代码并发送另一部分源代码给*DISTCC_HOSTS*中定义的主机。

	distcc server

	计算机与服务器编译从daemon中获取的代码，编译完成后，把编译后的目标代码发送回daemon，然后再接收下一部分代码（如果编译还没完成的话）。

## 开始

将所有用到的计算机都装上[community] 中的 distcc

```
# pacman -S distcc

```

如果是其他的发行版甚至使用 Cygwin 的 Windows 操作系统,请阅读 [distcc 文档](http://distcc.samba.org/doc.html)。

## 配置

### Daemon 和 Server 配置

编辑 `/etc/conf.d/distccd`，修改唯一没有被注释掉的那一行，设置正确的 IP 地址或整个子网。

```
DISTCC_ARGS="--user nobody --allow 192.168.0.0/24"

```

### Daemon 配置

在daemon上, 编辑`/etc/makepkg.conf`

1.  确保 BUILDENV 中的distcc没有被禁用(前面没有感叹号)
2.  编辑*DISTCC_HOSTS* ，加入可以使用的编译服务器的 IP 地址 + 反斜杠 + 线程数，不同 IP 地址用空格隔开，按照处理器性能排列
3.  修改 MAKEFLAGS 中的 N 为所有使用线程的和。在下面的示例为 5+3+3=11\. 如果超过这个值，超出的线程将会被 distcc阻塞。

**Note:** 在单机编译时一般定义为 CPU 数加一，仅在单机编译时才是对的，这里不应该使用这个方法。

相关行的示例:

```
BUILDENV=(distcc fakeroot color !ccache !check)
MAKEFLAGS="-j11"
DISTCC_HOSTS="192.168.0.2/5 192.168.0.3/3 192.168.0.4/3"

```

如果通过 SSH 使用 distcc，在 IP 地址前加 "@" 符号。如果未设置基于密钥的认证，将设置 DISTCC_SSH="ssh -i" 以忽略认证。

## 添加Daemon

要使得Server能找到所有的集群Daemon,还需要把所有Daemon的IP地址加入到/etc/distcc/hosts里面:

```
127.0.0.1
192.168.1.2
192.168.1.3
#...

```

## 编译

在每台参与编译的机器上开启 distcc daemon

```
# systemctl start distccd

```

要启动自动运行 distcc：

```
# systemctl enable distccd

```

然后正常运行 makepkg 即可。

## 监视进度

有多种方式可以监视进度。

1.  distccmon-text
2.  tailing log file

执行 distccmon-text 检查编译状况:

```
$ distccmon-text
29291 Preprocess  probe_64.c                                 192.168.0.2[0]
30954 Compile     apic_noop.c                                192.168.0.2[0]
30932 Preprocess  kfifo.c                                    192.168.0.2[0]
30919 Compile     blk-core.c                                 192.168.0.2[1]
30969 Compile     i915_gem_debug.c                           192.168.0.2[3]
30444 Compile     block_dev.c                                192.168.0.3[1]
30904 Compile     compat.c                                   192.168.0.3[2]
30891 Compile     hugetlb.c                                  192.168.0.3[3]
30458 Compile     catalog.c                                  192.168.0.4[0]
30496 Compile     ulpqueue.c                                 192.168.0.4[2]
30506 Compile     alloc.c                                    192.168.0.4[0]

```

通过 watch 加程序名可以循环执行程序，程序名后面加数字也可以实现重复查询:

```
$ watch distccmon-text

```

or

```
$ distccmon-text 2

```

在 daemon 上 tail `/var/log/messages.log` 也行:

```
# tail -f /var/log/messages.log

```

## 为每个编译任务使用distcc

如果你在pacman之外使用distcc，那么你需要做的就是把你加进*/etc/makepkg.conf* 文件中的"export ..."加到"/etc/profile"里：*/etc/makepkg.conf* 里的"export"只在"makepkg"或"makeworld"执行的时间读取，而*/etc/profile* 会在登录的时候执行。

## 技巧

### 限制硬盘使用

#### 修改 $HOME/.distcc 位置

distcc 默认会在 `$HOME/.distcc` 保存中间结果。在内存 /tmp 中创建 *.distcc* 并链接到 $HOME 可以避免磁盘读写。

```
$ mv $HOME/.distcc /tmp
$ ln -s /tmp/.distcc $HOME/.distcc

```

只需要在重启时让 Systemd 重新创建目录即可，创建文件：

 ` /etc/tmpfiles.d/tmpfs-create.conf ` 
```
d /tmp/.distcc 0666 nobody nobody -

```

#### 修改日志级别

默认日志放在 `/var/log/messages.log`，也可以放到一个单独的文件，例如通过 /tmp 放到 RAM 中。同时降低日志级别也可以只显示错误信息。LEVEL 可以是任意 syslog 级别，例如 critical, error, warning, notice, info, 或 debug.

把它们**附加**到 `/etc/conf.d/distccd` 的 DISTCC_ARGS 中。

```
DISTCC_ARGS="--user nobody --allow 192.168.0.0/24 --log-level error --log-file /tmp/distccd.log"

```

## 在使用CMake等工具时出现无法编译的错误

因为CMake使用了gcc的[Response File](http://gcc.gnu.org/wiki/Response_Files)特性，但distcc当前版本（3.2）还无法支持这个特性。 如果出现这个错误，可以选择打这个[补丁](http://code.google.com/p/distcc/issues/detail?id=85&q=response)， 或者使用aur上的[distcc-rsp](https://aur.archlinux.org/packages/distcc-rsp/)版本。