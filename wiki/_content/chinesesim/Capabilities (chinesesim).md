**翻译状态：** 本文是英文页面 [Capabilities](/index.php/Capabilities "Capabilities") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-05-09，点击[这里](https://wiki.archlinux.org/index.php?title=Capabilities&diff=0&oldid=422752)可以查看翻译后英文页面的改动。

**能力(capability)** (POSIX 1003.1e, capabilities(7))用更小的粒度控制超级管理员权限,可以避免使用 root 权限。软件开发者应该为二进制文件赋予最小权限，而不是使用强大的[setuid](https://en.wikipedia.org/wiki/Setuid "wikipedia:Setuid")。很多软件包用了能力, 比如 [iputils](https://www.archlinux.org/packages/?name=iputils)提供的`ping` 使用的CAP_NET_RAW(能力的一种) 。例如`ping`可以被普通用户执行(和**setuid**模式一样),同时减少了`ping`的潜在安全隐患。

## Contents

*   [1 设置方法](#.E8.AE.BE.E7.BD.AE.E6.96.B9.E6.B3.95)
*   [2 管理和维护](#.E7.AE.A1.E7.90.86.E5.92.8C.E7.BB.B4.E6.8A.A4)
*   [3 从capabilities受益的其他程序](#.E4.BB.8Ecapabilities.E5.8F.97.E7.9B.8A.E7.9A.84.E5.85.B6.E4.BB.96.E7.A8.8B.E5.BA.8F)
    *   [3.1 beep](#beep)
    *   [3.2 chvt](#chvt)
    *   [3.3 iftop](#iftop)
    *   [3.4 mii-tool](#mii-tool)
*   [4 有用的命令](#.E6.9C.89.E7.94.A8.E7.9A.84.E5.91.BD.E4.BB.A4)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 设置方法

在linux中，能力是通过命名空间*security*下的[extended attributes](/index.php/Extended_attributes "Extended attributes") ([xattr(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/xattr.7))实现。主流linux都支持扩展属性，包括Ext2，Ext3，Ext4，Btrfs，JFS，XFS，和Reiserfs。 下面的例子展示了用`getcap`显示ping命令的能力，然后通过使用`getfattr`显示相同的编码后的数据。

```
$ getcap /bin/ping
/bin/ping = cap_net_raw+ep
$ getfattr -d -m "^security\\." /bin/ping
# file: bin/ping
security.capability=0sAQAAAgAgAAAAAAAAAAAAAAAAAAA=

```

扩展属性可以通过`cp -a`自动复制, 但是其他的命令需要一个特别的参数,比如: `rsync -X`。

在Arch中, 能力可以通过包安装脚本`iputils.install`设置。

## 管理和维护

如果一个包有过度宽松的能力设置将会被认为是一个错误(bug), 所以这种情况应该被报告出来, 而不是在这里指出.等同于root访问权限的能力(CAP_SYS_ADMIN)或者仅仅等同于root访问(CAP_DAC_OVERRIDE)的能力, 因为Arch不支持任何MAC/RBAC系统,所以不当错误(bug).

**Warning:** 太多能力能让小的特权升级. 查看例子和解释需要看Brad Spengler的帖子 [False Boundaries and Arbitrary Code Execution](http://forums.grsecurity.net/viewtopic.php?f=7&t=2522&sid=c6fbcf62fd5d3472562540a7e608ce4e#p10271).

## 从capabilities受益的其他程序

下面软件包不包含 setuid 属性的文件，但是需要 root 权限才能执行。通过启用一些能力，一般用户就可以使用软件。

### beep

```
# setcap cap_dac_override,cap_sys_tty_config+ep /usr/bin/beep

```

### chvt

```
# setcap cap_dac_read_search,cap_sys_tty_config+ep /usr/bin/chvt

```

### iftop

```
# setcap cap_net_raw+ep /usr/bin/iftop

```

### mii-tool

```
# setcap cap_net_admin+ep /usr/bin/mii-tool

```

## 有用的命令

找到 setuid-root 文件:

```
$ find /usr/bin /usr/lib -perm /4000 -user root

```

找到 setgid-root 文件:

```
$ find /usr/bin /usr/lib -perm /2000 -group root

```

## 参阅

*   Man Page capabilities(7) setcap(8) getcap(8)
*   [DeveloperWiki:Security#Replacing setuid with capabilities](/index.php/DeveloperWiki:Security#Replacing_setuid_with_capabilities "DeveloperWiki:Security")