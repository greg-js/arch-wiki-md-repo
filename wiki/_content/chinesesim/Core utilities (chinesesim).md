**翻译状态：** 本文是英文页面 [Core_Utilities](/index.php/Core_Utilities "Core Utilities") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-01，点击[这里](https://wiki.archlinux.org/index.php?title=Core_Utilities&diff=0&oldid=448817)可以查看翻译后英文页面的改动。

本文涉及 GNU/Linux 系统的所谓的 "核心" 工具，就像 **less**, **ls**, 和 **grep**，包括了"但不限于"以上集成于GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) 中的工具。下文提供了颇为丰富的软件技巧和有帮助的其他信息。

## Contents

*   [1 基本问题](#.E5.9F.BA.E6.9C.AC.E9.97.AE.E9.A2.98)
*   [2 cat](#cat)
*   [3 dd](#dd)
*   [4 grep](#grep)
    *   [4.1 标准错误](#.E6.A0.87.E5.87.86.E9.94.99.E8.AF.AF)
*   [5 find](#find)
*   [6 locate](#locate)
*   [7 lsblk](#lsblk)
*   [8 iconv](#iconv)
    *   [8.1 Convert a file in place](#Convert_a_file_in_place)
*   [9 ip](#ip)
*   [10 less](#less)
    *   [10.1 用Vim代替](#.E7.94.A8Vim.E4.BB.A3.E6.9B.BF)
*   [11 ls](#ls)
    *   [11.1 File names containing spaces enclosed in quotes](#File_names_containing_spaces_enclosed_in_quotes)
*   [12 mkdir](#mkdir)
*   [13 mv](#mv)
*   [14 od](#od)
*   [15 pv](#pv)
*   [16 rm](#rm)
*   [17 sed](#sed)
*   [18 seq](#seq)
*   [19 ss](#ss)
*   [20 tar](#tar)
*   [21 which](#which)
*   [22 wipefs](#wipefs)
*   [23 权限相关工具](#.E6.9D.83.E9.99.90.E7.9B.B8.E5.85.B3.E5.B7.A5.E5.85.B7)
*   [24 另请参阅](#.E5.8F.A6.E8.AF.B7.E5.8F.82.E9.98.85)

## 基本问题

下面表格列出了每个 Linux 用户都应该熟悉的命令，黑体命令是 shell 的一部分，其它的是 shell 调用的程序。

| 命令 | 描述 | 示例 |
| man | 显示命令的手册页 | man ed |
| **cd** | 变更目录 | cd /etc/pacman.d |
| mkdir | 创建目录 | mkdir ~/newfolder |
| rmdir | 删除空目录 | rmdir ~/emptyfolder |
| rm | 删除文件 | rm ~/file.txt |
| rm -r | 删除目录和内容 | rm -r ~/.cache |
| ls | 显示文件 | ls *.mkv |
| ls -a | 显示隐藏文件 | ls -a /home/archie |
| ls -al | 显示隐藏文件和文件属性 |
| mv | 移到文件 | mv ~/compressed.zip ~/archive/compressed2.zip |
| cp | 复制文件 | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | 设置文件为可执行文件 | chmod +x ~/.local/bin/myscript.sh |
| cat | 显示文件内容 | cat /etc/hostname |
| strings | 显示文件中可打印的内容 | strings /usr/bin/free |
| find | 查找文件 | find ~ -name myfile |
| mount | 挂载分区 | mount /dev/sdc1 /media/usb |
| df -h | 显示分区上的剩余空间 |
| ps -A | 显示所有正在运行的程序 |
| killall | 杀死所有运行中的进程 |
| ss -at | 显示开放的 TCP 连接列表 |

## cat

[cat](https://en.wikipedia.org/wiki/cat_(Unix) 是一件能够连接并显示多文件的标准Unix工具。

*   **cat** 并不内置于 shell ，不过若您追求高性能，您会发现在很多情况下改用[重定向](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)")就很方便得许多，例如编写脚本。事实上，`$ < *file*`的效果就如同`$ cat *file*`一样。

*   按照以下结构可直接在某文件添加多行文字：

```
$  cat << EOF >> *path/file*
 *first line*
 ...
 *last line*
 EOF

```

或者使用 `printf`:

```
$ printf '%s
' 'first line' ... 'last line'

```

*   如果您希望能以倒读顺序显示文件内容，有个工具叫 [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* reversed).

## dd

[dd](https://en.wikipedia.org/wiki/dd_(Unix) 是在 unix 和 类unix 系统中主要用于转换和拷贝文件的命令。

默认情况下在任务完成前 dd 都没有输出，要监控操作的进度，可以添加 `status=progress` 选项，详情参考 [manual](http://www.gnu.org/software/coreutils/manual/html_node/dd-invocation.html#dd-invocation)。

**Note:** *cp* 等同于不带操作数的 *dd* ，但其并非被设计用于通用的磁盘擦除程序.

## grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") (来自 [ed](https://en.wikipedia.org/wiki/ed "wikipedia:ed")的 *g/re/p*，*global/regular expression/print*）是最初给 Unix 写的命令行文字搜索工具，`grep`命令在文件或标准输入里搜索符合指定正则表达式模式的行，并把结果打印到标准输出。

*   记住，*grep* 能直接处理文件，所以用`$ grep *pattern* *file*` 代替 `$ cat *file* | grep *pattern*`即可。

*   若要 grep 集群服务器（VCS）的源代码，请使用专门的 Perl 工具[ack](https://www.archlinux.org/packages/?name=ack)。

### 标准错误

如果命令将错误输出到 std error，grep 就无法处理，这时，将它们重定向到 stdout：

```
$ *command* 2>&1 | grep *args*

```

对 Bash 4 还能使用：

```
$ *command* |& grep *args*

```

参考 [I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html).

## find

*find* is part of the [findutils](https://www.archlinux.org/packages/?name=findutils) package, which belongs to the [base](https://www.archlinux.org/groups/x86_64/base/) package group.

One would probably expect a *find* command to take as argument a file name and search the filesystem for files matching that name. For a program that does exactly that see [#locate](#locate) below.

Instead, find takes a set of directories and matches each file under them against a set of expressions. This design allows for some very powerful "one-liners" that would not be possible using the "intuitive" design described above. See [UsingFind](http://mywiki.wooledge.org/UsingFind) for usage details.

## locate

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [mlocate](https://www.archlinux.org/packages/?name=mlocate)，安装后，一个脚本会每天更新数据库。以 root 手动运行 *updatedb* 也可以更新数据库。 也预生成的或者由守护进程和增量编码压缩过的文件数据库搜索. 它要快于 *find*, 但需要经常更新数据库.默认会忽略 `/media` 和 `/mnt` 等路径，所以 *locate* 不会查找外置设备。详情请参考 [updatedb(1)](http://man7.org/linux/man-pages/man1/updatedb.1.html)。

*locate* 命令是一个快速查找文件系统的常用 Unix 工具。因为是从数据库查找而不是直接访问文件系统，所以速度比 [find](https://en.wikipedia.org/wiki/Find "wikipedia:Find") 快很多。而缺点是数据库更新后的新文件不会被搜索到。使用 *locate* 前，请先以 root 权限执行 `updatedb`.

详情参考 [这篇文章](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/).

## lsblk

[lsblk(8)](http://man7.org/linux/man-pages/man8/lsblk.8.html) 命令会显示所有连接到系统的设备和分区状况：

 `$ lsblk` 
```
NAME            MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda               8:0    0    80G  0 disk
└─sda1            8:1    0    80G  0 part

```

设备名开头定义块设备的类型，大部分现代的硬盘/[SSD](/index.php/SSD "SSD") 都是 SCSI (**s**) storage **d**evices, 使用 `/dev/sd*x*` 这样的名字，其中 *x* 是一个或多个小写字母。文件系统被命名为 `/dev/sd*xY*`，其中 *Y* 是一个数字。

其它块设备比如 flash 可能使用 `mmcblk`(内存卡) 或 `nvme` ([NVMe](/index.php/Solid_State_Drives/NVMe "Solid State Drives/NVMe")). 可以从[内核文档](https://www.kernel.org/doc/Documentation/devices.txt)查看不清楚的设备类型.

[安装](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")时，结果中会包含 Arch 安装设备(例如 USB 安装盘)，不是所有设备都适合安装。`rom`, `loop` 或 `airoot` 格式的分区可以忽略。

## iconv

`iconv` 将转换一个文本的字符编码.

下列命令转换文件`foo`从 ISO-8859-15 到 UTF-8 保存至 `foo.utf`:

```
$ iconv -f ISO-8859-15 -t UTF-8 foo >foo.utf

```

查阅 `man iconv` 获取更多细节.

+

### Convert a file in place

**Tip:** You can use [recode](https://www.archlinux.org/packages/?name=recode) instead of iconv if you do not want to touch the mtime.

Unlike [sed](#sed), *iconv* does not provide an option to convert a file in place. However, `sponge` can be used to handle it, it comes with [moreutils](https://www.archlinux.org/packages/?name=moreutils).

```
$ iconv -f WINDOWS-1251 -t UTF-8 foobar.txt | sponge foobar.txt

```

See `man sponge` for details.

## ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") 显示关于网络设备, IP 地址, 路由表, 和其他Linux [IP](https://en.wikipedia.org/wiki/Internet_Protocol "wikipedia:Internet Protocol") 软件栈的对象信息.通过附加各种命令, 你可以操纵或配置大多数对象.

**Note:** *ip* 命令在[iproute2](https://www.archlinux.org/packages/?name=iproute2)包中提供, 包含在[base](https://www.archlinux.org/groups/x86_64/base/)组.

| 对象 | 作用 | 手册页名称 |
| ip addr | 协议地址管理 | ip-address |
| ip addrlabel | 协议地址标签管理 | ip-addrlabel |
| ip l2tp | tunnel Ethernet over IP (L2TPv3) | ip-l2tp |
| ip link | 网络设备配置 | ip-link |
| ip maddr | 多播地址管理 | ip-maddress |
| ip monitor | 监测 netlink 信息 | ip-monitor |
| ip mroute | 多播路由缓存管理 | ip-mroute |
| ip mrule | 多播路由策略数据库的规则 |
| ip neigh | 邻居/ARP 表管理 | ip-neighbour |
| ip netns | process network namespace management | ip-netns |
| ip ntable | 邻居表配置 | ip-ntable |
| ip route | 路由表管理 | ip-route |
| ip rule | 路由策略数据库管理 | ip-rule |
| ip tcp_metrics | 管理 TCP Metrics | ip-tcp_metrics |
| ip tunnel | 隧道配置 | ip-tunnel |
| ip tuntap | 管理 TUN/TAP 设备 |
| ip xfrm | 管理 IPsec 策略 | ip-xfrm |

`help` 帮助命令可用于所有对象. 例如, 输入 `ip addr help` 将显示地址的命令语法. 高级用法参见 [iproute2 documentation](http://www.policyrouting.org/iproute2.doc.html).

The [Network configuration](/index.php/Network_configuration "Network configuration") 显示 *ip* 命令的多种常见任务中的使用方式.

**Note:** 您也许很熟悉 [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") 命令, 它用于旧版linux的接口配置. 在 archlinx 中现已不赞成使用; 您应当用 *ip* 替代之.

## less

[less](https://en.wikipedia.org/wiki/less_(Unix) 是一个对文本文件内容进行分页显示的终端程序，它和其他的分页显示程序如`more`和`pg`相似，但`less`提供了更高级的界面和更多的功能。[[1]](http://www.greenwoodsoftware.com/less/faq.html)

### 用Vim代替

[Vim](/index.php/Vim "Vim") 内置了脚本，可直接查看文本文件、压缩包或目录的内容。在您的shell配置文件添加以下即可：

 `~/.bashrc`  `alias less='/usr/share/vim/vim73/macros/less.sh'` 

除了*less.sh*宏外还有另外一种用法, 依赖于 `PAGER`　环境变量. 安装 [vimpager](https://www.archlinux.org/packages/?name=vimpager) 并添加以下内容至shell配置文件:

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

所有使用 `PAGER` 环境变量的程序, 如 [git](/index.php/Git "Git"), 将使用 *vim* 作为分页程序.

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls")是一个Unix和类Unix系统中列出目录里的文件的一个命令。

*   *ls* 可以列出 [file permissions](/index.php/File_permissions_and_attributes#Viewing_permissions "File permissions and attributes").

请参考 `info ls` 或 [在线文档](http://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html#ls-invocation)。

### File names containing spaces enclosed in quotes

By default, file and directory names that contain spaces are displayed surrounded by single quotes. To change this behavior use the `-N` or `--quoting-style=literal` options. Alternatively, set the `QUOTING_STYLE` [environment variable](/index.php/Environment_variable "Environment variable") to `literal`. [[2]](https://unix.stackexchange.com/questions/258679/why-is-ls-suddenly-surrounding-items-with-spaces-in-single-quotes)

## mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir_(Unix) (*make directory*)是一条创建目录的命令。

若需递归地创建一系列目录，就要用到 *-p*参数了。已经十分熟悉这原理的高级用户也可直接设为内置参数：

```
alias mkdir='mkdir -p -v'

```

`-v`参数可以使创建目录的消息更为详细。

不必使用 *chmod* 更改权限模式, 用 `-m`选项可直接定义新建目录的访问权限

**Note:** 如果您仅仅只是想建个临时目录，也许用**mktemp** (*make termporary*)更好: `$ mktemp -p`.

## mv

[mv](https://en.wikipedia.org/wiki/mv_(Unix) (*move*)是一条移动或重命名文件和目录的命令。使用这命令的风险可不小，请务必小心。

```
alias mv=' timeout 8 mv -iv'

```

这命令别名可以延迟**mv** 到8秒后才生效，或是当删除三个以上的文件就会进行确认。

## od

The [od](https://en.wikipedia.org/wiki/od_(Unix) (*o*ctal *d*ump) command is useful for visualizing data that is not in a human-readable format, like the executable code of a program, or the contents of an unformatted device. See the [manual](http://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html#od-invocation) for more information.

## pv

You can use [pv](https://www.archlinux.org/packages/?name=pv) (*pipe viewer*) to monitor the progress of data through a pipeline, for example:

```
# dd if=*/source/filestream* | pv -*monitor_options* -s *size_of_file* | dd of=*/destination/filestream*

```

In most cases `pv` functions as a drop-in replacement for `cat`.

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) (*remove*)是一条删除文件或目录的命令。

它同样十分危险，使用时请提高警觉：

```
alias rm=' timeout 3 rm -Iv --one-file-system'

```

	这种命令别名可延迟**rm**到3秒后才生效， 或是当删除三个以上的文件就会进行确认，或是限于只在同一个文件系统生效。

	若您想在删除多文件时一一确认，用`-I`代替`-i`即可。

	Zsh 的使用者可在 `timeout` 前加上 `noglob`，避免隐式扩展。

若要移除空目錄，使用 *rmdir*,　若内含文件则命令失败。

## sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") (*stream editor*)是一条专门解析或替换文本的命令。

这里有一系列现成的[示范](http://sed.sourceforge.net/sed1line.txt)

**Note:** awk更为优秀，甚至Perl语言也可以。

## seq

**seq** (*sequence*)是一条专门排列数字的命令。可以按照[Wikipedia](https://en.wikipedia.org/wiki/seq "wikipedia:seq")上进行练习。

## ss

*ss* is a utility to investigate network ports and is part of the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package in the [base](https://www.archlinux.org/groups/x86_64/base/) group. It has a similar functionality to the [deprecated](https://www.archlinux.org/news/deprecation-of-net-tools/) netstat utility.

Common usage includes:

Display all TCP Sockets with service names:

```
$ ss -at

```

Display all TCP Sockets with port numbers:

```
$ ss -atn

```

Display all UDP Sockets:

```
$ ss -au

```

For more information see [ss(8)](http://man7.org/linux/man-pages/man8/ss.8.html) or [introductory examples](http://www.cyberciti.biz/files/ss.html).

## tar

As an early Unix archiving format, .tar files—known as "tarballs"—are widely used for packaging in Unix-like operating systems. Both [pacman](/index.php/Pacman "Pacman") and [AUR](/index.php/AUR "AUR") packages are compressed tarballs, and Arch uses [GNU's](/index.php/GNU_Project "GNU Project") *tar* program by default.

For .tar archives, *tar* by default will extract the file according to its extension:

```
$ tar xvf *file.EXTENSION*

```

Forcing a given format:

| File Type | Extraction Command |
| `*file*.tar` | `tar xvf *file*.tar` |
| `*file*.tgz` | `tar xvzf *file*.tgz` |
| `*file*.tar.gz` | `tar xvzf *file*.tar.gz` |
| `*file*.tar.bz` | `bzip -cd *file*.bz | tar xvf -` |
| `*file*.tar.bz2` | `tar xvjf *file*.tar.bz2`
`bzip2 -cd *file*.bz2 | tar xvf -` |
| `*file*.tar.xz` | `tar xvJf *file*.tar.xz`
`xz -cd *file*.xz | tar xvf -` |

The construction of some of these *tar* arguments may be considered legacy, but they are still useful when performing specific operations. See its [man page](/index.php/Man_page "Man page") with `man tar` for details.

## which

[which](https://en.wikipedia.org/wiki/Which_(Unix) shows the full path of shell commands. In the following example the full path of `ssh` is used as an argument for `journalctl`:

```
# journalctl $(which sshd)

```

## wipefs

*wipefs* can list or erase [file system](/index.php/File_system "File system"), [RAID](/index.php/RAID "RAID") or [partition-table](/index.php/Partition "Partition") signatures (magic strings) from the specified device. It does not erase the file systems themselves nor any other data from the device.

See [wipefs(8)](http://man7.org/linux/man-pages/man8/wipefs.8.html) for more information.

For example, to erase all signatures from the device `/dev/sdb` and create a signature backup `~/wipefs-sdb-*offset*.bak` file for each signature:

```
# wipefs --all --backup /dev/sdb

```

## 权限相关工具

*   [chmod](https://en.wikipedia.org/wiki/chmod "wikipedia:chmod") (*change mode*) 是一个 Unix shell 命令和系统调用名称, 用于修改文件系统对象的访问权限（包括文件和目录）, 也用于指定特殊flags.

*   [chown](https://en.wikipedia.org/wiki/chown "wikipedia:chown") (*change owner*) 用于 Unix-like 系统改变文件拥有者.

*   [chattr](https://en.wikipedia.org/wiki/chattr "wikipedia:chattr") (*change attributes*) 允许用户设置 linux 系统中文件的某些属性.

*   [lsattr](https://en.wikipedia.org/wiki/lsattr "wikipedia:lsattr") (*list attributes*) 列出 linux 扩展文件系统上的属性.

*   `ls -l` 列出文件属性.

这些工具在 [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes") 中说明. 更多高级权限用例请参考 [capabilities](/index.php/Using_File_Capabilities_Instead_Of_Setuid "Using File Capabilities Instead Of Setuid") 和 [ACL](/index.php/ACL "ACL").

## 另请参阅

*   [A sampling of coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - coreutils 命令概述

*   [GNU Coreutils Manpage](http://www.gnu.org/software/coreutils/manual/coreutils.html)

*   [Learn the DD command](http://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)