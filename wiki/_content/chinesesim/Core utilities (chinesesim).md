**翻译状态：** 本文是英文页面 [Core_Utilities](/index.php/Core_Utilities "Core Utilities") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-03-29，点击[这里](https://wiki.archlinux.org/index.php?title=Core_Utilities&diff=0&oldid=513811)可以查看翻译后英文页面的改动。

相关文章

*   [Bash (简体中文)](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)")
*   [Zsh (简体中文)](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)")
*   [常用建议](/index.php/General_Recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General Recommendations (简体中文)")
*   [GNU Project](/index.php/GNU_Project "GNU Project")
*   [sudo (简体中文)](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)")
*   [cron (简体中文)](/index.php/Cron_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cron (简体中文)")
*   [man page (简体中文)](/index.php/Man_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Man page (简体中文)")
*   [Securely wipe disk#shred](/index.php/Securely_wipe_disk#shred "Securely wipe disk")
*   [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")
*   [Color output in console (简体中文)](/index.php/Color_output_in_console_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Color output in console (简体中文)")

本文涉及 GNU/Linux 系统的所谓的 "核心" 工具，比如 **less**, **ls**, 和 **grep**，包括但不限于以上集成于 GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) 中的工具。下文提供了关于这些实用工具颇为丰富的技巧和有帮助的其他信息。

## Contents

*   [1 基本命令](#.E5.9F.BA.E6.9C.AC.E5.91.BD.E4.BB.A4)
*   [2 cat](#cat)
*   [3 dd](#dd)
*   [4 grep](#grep)
*   [5 find](#find)
*   [6 iconv](#iconv)
    *   [6.1 在原文件上转换](#.E5.9C.A8.E5.8E.9F.E6.96.87.E4.BB.B6.E4.B8.8A.E8.BD.AC.E6.8D.A2)
*   [7 ip](#ip)
*   [8 locate](#locate)
*   [9 less](#less)
    *   [9.1 用 Vim 代替 less 来分页](#.E7.94.A8_Vim_.E4.BB.A3.E6.9B.BF_less_.E6.9D.A5.E5.88.86.E9.A1.B5)
*   [10 ls](#ls)
    *   [10.1 “长格式”输出](#.E2.80.9C.E9.95.BF.E6.A0.BC.E5.BC.8F.E2.80.9D.E8.BE.93.E5.87.BA)
    *   [10.2 带空格的文件名被引号引起](#.E5.B8.A6.E7.A9.BA.E6.A0.BC.E7.9A.84.E6.96.87.E4.BB.B6.E5.90.8D.E8.A2.AB.E5.BC.95.E5.8F.B7.E5.BC.95.E8.B5.B7)
*   [11 lsblk](#lsblk)
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
*   [23 参阅](#.E5.8F.82.E9.98.85)

## 基本命令

下面表格列出了每个 Linux 用户都应该熟悉的命令，黑体命令是 shell 的一部分，其它的是 shell 调用的程序。命令的细节请阅读接下来的几节和*相关文章*。

| 命令 | 描述 | 手册页名称 | 示例 |
| man | 显示命令的手册页 | [man(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man.7) | man ed |
| **cd** | 变更目录 | [cd(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cd.1p) | cd /etc/pacman.d |
| mkdir | 创建目录 | [mkdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1) | mkdir ~/newfolder |
| rmdir | 删除空目录 | [rmdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rmdir.1) | rmdir ~/emptyfolder |
| rm | 删除文件 | [rm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rm.1) | rm ~/file.txt |
| rm -r | 删除目录和内容 | rm -r ~/.cache |
| ls | 显示文件 | [ls(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ls.1) | ls *.mkv |
| ls -a | 显示隐藏文件 | ls -a /home/archie |
| ls -al | 显示隐藏文件和文件属性 |
| mv | 移动文件 | [mv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mv.1) | mv ~/compressed.zip ~/archive/compressed2.zip |
| cp | 复制文件 | [cp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cp.1) | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | 设置文件为可执行文件 | [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1) | chmod +x ~/.local/bin/myscript.sh |
| cat | 显示文件内容 | [cat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cat.1) | cat /etc/hostname |
| strings | 显示文件中可打印的内容 | [strings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strings.1) | strings /usr/bin/free |
| find | 查找文件 | [find(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find.1) | find ~ -name myfile |
| mount | 挂载分区 | [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) | mount /dev/sdc1 /media/usb |
| df -h | 显示分区上的剩余空间 | [df(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/df.1) |
| ps -A | 显示所有正在运行的进程 | [ps(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ps.1) |
| killall | 杀死所有运行中的进程 | [killall(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/killall.1) |
| ss -at | 显示开放的 TCP 连接列表 | [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8) |

## cat

[cat](https://en.wikipedia.org/wiki/cat_(Unix) 是一个能够连接并显示多文件的标准 Unix 工具。

*   **cat** 并不内置于 shell ，不过若追求高性能，你会发现在很多情况下改用[重定向](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)")就很方便得许多，例如编写脚本。事实上，`$ < *file*` 的效果就如同 `$ cat *file*` 一样。

*   按照以下结构可直接在某文件添加多行文字：

```
$ cat << EOF >> *path/file*
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

*   如果您希望能以倒读顺序显示文件内容，有个工具叫 [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* 倒着写).

## dd

[dd](https://en.wikipedia.org/wiki/dd_(Unix) 是在 unix 和 类 unix 系统中主要用于转换和拷贝文件的命令。

与 *cp* 类似，默认情况下 *dd* 以块为单位拷贝文件，具有较低级别的 I/O流 控制功能。

**提示：** 默认情况下在任务完成前 dd 都没有输出，要监控操作的进度，可以添加 `status=progress` 选项。

更多信息参考 [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) 或 [完整文档](https://www.gnu.org/software/coreutils/dd)。

## grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") (来自 [ed](https://en.wikipedia.org/wiki/ed "wikipedia:ed") 的 *g/re/p*，*global/regular expression/print*）是最初给 Unix 写的命令行文字搜索工具，`grep` 命令在文件或标准输入里搜索符合指定正则表达式模式的行，并把结果打印到标准输出。

*   记住，*grep* 能直接处理文件，所以用 `grep *pattern* *file*` 代替 `cat *file* | grep *pattern*` 即可。
*   若要 grep 版本控制系统（VCS）的源代码，请使用专门的工具 [ripgrep](https://www.archlinux.org/packages/?name=ripgrep)、[the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher) 和 [ack](https://www.archlinux.org/packages/?name=ack)。
*   要在输出结果中显示行数，加上 `-n` 选项。

**注意:** 一些命令把错误输出到 [stderr(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stderr.3)，grep 就无法处理。这时，用 `*command* 2>&1 | grep *args*` 或 (对于 Bash 4) `*command* |& grep *args*` 将 *stderr* 重定向到 *stdout*。参阅 [I/O 重定向](http://www.tldp.org/LDP/abs/html/io-redirection.html)。

参阅 [Color output in console#grep](/index.php/Color_output_in_console#grep "Color output in console") 来启用彩色输出支持。

## find

*find* 是 [findutils](https://www.archlinux.org/packages/?name=findutils) 软件包的一部分, 它属于 [base](https://www.archlinux.org/groups/x86_64/base/) 软件包组。

**提示：** [fd](https://www.archlinux.org/packages/?name=fd) 是 `find` 的一个更加简单、快速、友好的替代方案，它有着更合理的默认值（比如忽略隐藏文件、文件夹和 `.gitignore` 等文件，可用 `fd PATTERN` 代替 `find -iname '*PATTERN*'`）。它具有彩色输出（类似 `ls`），unicode 支持，正则表达式等等。

你可能希望 *find* 命令将一个文件名称作为参数，并在文件系统中搜索与该名称匹配的文件。下面的 [#locate](#locate) 程序可以专门做这件事。

相反，find 需要一组目录，并将它们下面的每个文件与一组表达式进行匹配。这种设计为实现一些“能干的单行小程序”提供了强大的支持，而这是上述“直观”设计无法实现的。参阅 [UsingFind](http://mywiki.wooledge.org/UsingFind) 来获取使用说明。

## iconv

*iconv* 将转换一个文本的字符编码。

下列命令将文件 `*foo*` 从 ISO-8859-15 转换至 UTF-8，然后保存到 `*foo*.utf`：

```
$ iconv -f ISO-8859-15 -t UTF-8 *foo* > *foo*.utf

```

查阅 [iconv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iconv.1) 获取更多细节。

### 在原文件上转换

**提示：** 如果你不想改变文件的修改时间，可以用 [recode](https://www.archlinux.org/packages/?name=recode) 代替 iconv。

与 [sed](#sed) 不同，*iconv* 没有提供直接转换文件的选项，但是 [moreutils](https://www.archlinux.org/packages/?name=moreutils) 包里面的 `sponge` 可以帮忙：

```
$ iconv -f WINDOWS-1251 -t UTF-8 *foobar*.txt | sponge *foobar*.txt

```

更多细节请参阅 [sponge(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1)。

## ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") 显示关于网络设备，IP 地址，路由表和其他 Linux [IP](https://en.wikipedia.org/wiki/Internet_Protocol "wikipedia:Internet Protocol") 软件栈的对象信息。通过附加各种命令，你可以操纵或配置大多数对象。

**注意:** *ip* 命令在 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 包中提供，这个包已经包含在 [base](https://www.archlinux.org/groups/x86_64/base/) 组。

| 对象 | 作用 | 手册页名称 |
| ip addr | 协议地址管理 | [ip-address(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8) |
| ip addrlabel | 协议地址标签管理 | [ip-addrlabel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-addrlabel.8) |
| ip l2tp | tunnel Ethernet over IP (L2TPv3) | [ip-l2tp(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-l2tp.8) |
| ip link | 网络设备配置 | [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8) |
| ip maddr | 多播地址管理 | [ip-maddress(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-maddress.8) |
| ip monitor | 监测 netlink 信息 | [ip-monitor(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-monitor.8) |
| ip mroute | 多播路由缓存管理 | [ip-mroute(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-mroute.8) |
| ip mrule | 多播路由策略数据库的规则 |
| ip neigh | 邻居/ARP 表管理 | [ip-neighbour(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-neighbour.8) |
| ip netns | process network namespace management | [ip-netns(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-netns.8) |
| ip ntable | 邻居表配置 | [ip-ntable(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-ntable.8) |
| ip route | 路由表管理 | [ip-route(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8) |
| ip rule | 路由策略数据库管理 | [ip-rule(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-rule.8) |
| ip tcp_metrics | 管理 TCP Metrics | [ip-tcp_metrics(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tcp_metrics.8) |
| ip tunnel | 隧道配置 | [ip-tunnel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tunnel.8) |
| ip tuntap | 管理 TUN/TAP 设备 |
| ip xfrm | 管理 IPsec 策略 | [ip-xfrm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-xfrm.8) |

`help` 帮助命令可用于所有对象。例如，输入 `ip addr help` 将显示地址的命令语法。高级用法参见 [iproute2 documentation](http://www.policyrouting.org/iproute2.doc.html)。

[Network configuration](/index.php/Network_configuration "Network configuration") 显示 *ip* 命令的多种常见任务中的使用方式。

**注意:** 你也许很熟悉 [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") 命令，它用于旧版linux的接口配置。在 Arch Linux 中现已不赞成使用；应当用 *ip* 替代之。

## locate

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [mlocate](https://www.archlinux.org/packages/?name=mlocate)。包里包括了一个 `updatedb.timer` 单元，用于每天更新数据库。这个 systemd 定时器在安装后就会 enable，如果不想重启系统，请手动 [start](/index.php/Start "Start")。以 root 手动运行 *updatedb* 也可以更新数据库。默认会忽略 `/media` 和 `/mnt` 等路径，所以 *locate* 不会查找外置设备里的文件。详情请参考 [updatedb(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.8)。

*locate* 命令是一个快速查找文件系统的常用 Unix 工具。因为是从数据库查找而不是直接访问文件系统，所以速度比 [find](https://en.wikipedia.org/wiki/Find "wikipedia:Find") 快很多。而缺点是在数据库更新后创建的新文件不会被搜索到。

使用 *locate* 前需建立数据库，请先以 root 权限执行 `updatedb`。

详情参考 [How locate works and rewrite it in one minute](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/)。

## less

[less](https://en.wikipedia.org/wiki/less_(Unix) 是一个对文本文件内容进行分页显示的终端程序，它和其他的分页显示程序如 [more](https://en.wikipedia.org/wiki/more_(command) 和 [pg](https://en.wikipedia.org/wiki/pg_(Unix) 相似，但 *less* 提供了更高级的界面和更多的 [功能](http://www.greenwoodsoftware.com/less/faq.html)。

参阅 [List of applications#Terminal pagers](/index.php/List_of_applications#Terminal_pagers "List of applications") 查找更多替代方案。

### 用 Vim 代替 less 来分页

[Vim](/index.php/Vim "Vim") 内置了脚本，可直接查看文本文件、压缩包或目录的内容。在你的 shell 配置文件添加以下内容：

 `~/.bashrc`  `alias less='/usr/share/vim/vim80/macros/less.sh'` 

除了 *less.sh* 宏外还有另外一种用法，依赖于 `PAGER`　环境变量。安装 [vimpager](https://www.archlinux.org/packages/?name=vimpager) 并添加以下内容至shell配置文件:

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

这样，所有使用 `PAGER` 环境变量的程序, 如 [git](/index.php/Git "Git"), 将使用 *vim* 作为分页程序。

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") 是一个Unix和类Unix系统中列出目录里的文件的一个命令。

请参考 `info ls` 或 [在线文档](http://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html#ls-invocation)。

[exa](https://the.exa.website) 相较于 `ls` 和 `tree` 是一个更加现代的、人性化的选择。它有更多的特性，例如将 [Git](/index.php/Git "Git") 修改和文件名一同显示，在 `--long` 模式中对每列进行不同的着色，或者在 `tree` 视图中显示 `--long` 模式元数据。 [exa](https://www.archlinux.org/packages/?name=exa)

### “长格式”输出

`-l` 选项显示一些元数据，例如：

 `$ ls -l */path/to/directory*` 
```
total 128
drwxr-xr-x 2 archie users  4096 Jul  5 21:03 Desktop
drwxr-xr-x 6 archie users  4096 Jul  5 17:37 Documents
drwxr-xr-x 2 archie users  4096 Jul  5 13:45 Downloads
-rw-rw-r-- 1 archie users  5120 Jun 27 08:28 customers.ods
-rw-r--r-- 1 archie users  3339 Jun 27 08:28 todo
-rwxr-xr-x 1 archie users  2048 Jul  6 12:56 myscript.sh

```

`total` 值表示目录中文件的总磁盘分配，默认情况下为块的数量。

每个文件和子目录由一行表示，每行划分为 7 个字段，按以下顺序表示：

*   类型与权限：
    *   首字母表示内部类型，参阅 `info ls -n "What information is listed"` 来查看所有可能类型的介绍；例如：
        *   `-` 表示一个普通文件；
        *   `d` 表示一个目录，比如一个包括了其他文件和文件夹的文件夹；
        *   `p` 表示一个命名的管道（又名 FIFO）；
        *   `l` 表示这是一个软链接；
    *   其他字母表示这个条目的 [权限](/index.php/Permissions "Permissions");
*   这个条目 [硬链接](https://en.wikipedia.org/wiki/Hard_link "wikipedia:Hard link") 的数量；对文件而言这个数字至少是 1，即当前显示的文件引用本身；对文件夹而言这个数字至少是 2，当前显示的引用、对自己的引用（`.` 条目）以及这个文件夹中的子文件夹对父文件夹的引用（`..` 条目）；
*   [用户](/index.php/User "User") 名；
*   [组](/index.php/Group "Group") 名；
*   大小；
*   修改时间；
*   名称。

### 带空格的文件名被引号引起

默认情况下，包含空格的文件名和目录名会被单引号引起。要改变这一特性，请使用 `-N` 或 `--quoting-style=literal` 选项。另外，将 `QUOTING_STYLE` [环境变量](/index.php/Environment_variable "Environment variable") 设置为 `literal` 也可以。[[1]](https://unix.stackexchange.com/questions/258679/why-is-ls-suddenly-surrounding-items-with-spaces-in-single-quotes)

## lsblk

[lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) 命令会显示所有连接到系统的 [块设备](https://en.wikipedia.org/wiki/Device_file#Block_devices "w:Device file") 和分区状况：

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

设备名开头定义块设备的类型，大部分现代的硬盘、[SSD](/index.php/SSD "SSD") 和 USB 闪存设备都被识别为 SCSI disks (`sd`)。类型后面跟着给设备编号的小写字母，第一个设备从 `a` 开始 (`sda`)，第二个设备就是 `b` (`sdb`)，以此类推。每个设备上的 *现有* 分区将用数字编号，从 `1` 开始 (`sda1`)，第二个分区就是 `2` (`sda2`)，以此类推。在上面的示例中，只有一个设备可用 (`sda`)，该设备有三个分区 （`sda1` 到 `sda3`），每个分区具有不同的 [文件系统](/index.php/File_system "File system")。

其它块设备比如 `mmcblk`（内存卡）或 `nvme`（[NVMe](/index.php/NVMe "NVMe") 设备）。不清楚的设备类型可以在这里搜索到：[kernel documentation](https://www.kernel.org/doc/Documentation/devices.txt)。

## mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir "wikipedia:mkdir") (*make directory*) 可以创建目录。

若需递归地创建一系列目录，就要用到 `-p` 参数了，否则会出错。已经十分熟悉这原理的高级用户也可直接设为内置参数：

```
alias mkdir='mkdir -p -v'

```

`-v` 参数可以使创建目录过程中的信息更为详细。

不必使用 *chmod* 更改权限模式, 用 `-m` 选项可直接定义新建目录的访问权限。

**提示：** 如果您仅仅只是想建个临时目录，也许用 [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file"): `mktemp -d` 更好。

## mv

[mv](https://en.wikipedia.org/wiki/mv "wikipedia:mv") (*move*) 可以移动或重命名文件和目录。

为了降低使用这个命令带来的风险，请添加一个 alias：

```
alias mv='timeout 8 mv -iv'

```

这个别名可以延迟 *mv* 到 8 秒后才生效，在覆盖已存在的文件时要求确认，列出正在进行的操作并且在 shell 被配置为忽略空格开头的命令的情况下，不将自身记入 shell 的命令历史记录。

## od

[od](https://en.wikipedia.org/wiki/od_(Unix) (*o*ctal *d*ump) 命令在显示非人类可读格式时非常有用，比如程序的可执行文件，或者未格式化的设备的内容。参阅[manual](https://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html#od-invocation) 了解详情。

## pv

可以用 [pv](https://www.archlinux.org/packages/?name=pv) (*pipe viewer*) 来监视管道中传递的数据，例如：

```
# dd if=*/source/filestream* | pv -*monitor_options* -s *size_of_file* | dd of=*/destination/filestream*

```

大多数情况下 `pv` 可直接替代 `cat`。

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) (*remove*) 用于删除文件或目录。

为了降低使用这个命令带来的风险，请添加一个 alias：

```
alias rm='timeout 3 rm -Iv --one-file-system'

```

这个别名可延迟 *rm* 到 3 秒后才生效，在删除三个以上的文件时要求确认，列出正在进行的操作，限于只在同一个文件系统生效并且在 shell 被配置为忽略空格开头的命令的情况下，不将自身记入 shell 的命令历史记录。若你想在删除多文件时一一确认，用 `-I` 代替 `-i` 即可。

Zsh 的使用者可在 `timeout` 前加上 `noglob`，避免隐式扩展。

若要移除空目录，使用 *rmdir*，若内含文件则命令失败。

## sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") (*stream editor*) 是一条专门解析或替换文本的命令。

这里有一系列现成的 *sed* [示范](http://sed.sourceforge.net/sed1line.txt)。

**提示：** [AWK](https://en.wikipedia.org/wiki/AWK "wikipedia:AWK") 和 [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") 语言在这方面更为强大。

## seq

*seq* (*sequence*) 是一条专门排列数字的命令。Shell 内置了该命令的其他替代方案，可以按照 [Wikipedia](https://en.wikipedia.org/wiki/Seq_(Unix) 的说明进行练习。

## ss

*ss* 是一个检查网络端口的实用程序，并且是 [base](https://www.archlinux.org/groups/x86_64/base/) 组中的 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 包的一部分。它具有与 [弃用的](https://www.archlinux.org/news/deprecation-of-net-tools/) netstat 实用程序类似的功能。

常用用法包括：

显示所有 TCP Sockets，连同 service 名称：

```
$ ss -at

```

显示所有 TCP Sockets，连同端口号：

```
$ ss -atn

```

显示所有 UDP Sockets：

```
$ ss -au

```

更多信息请参考 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 包里的 [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8) 或 `ss.html`。

## tar

作为早期的 Unix 存档格式，.tar 文件（称为“tarballs”）广泛用于类 Unix 操作系统中的打包操作。[pacman](/index.php/Pacman "Pacman") 和 [AUR](/index.php/AUR "AUR") 软件包都是压缩的 tarball，Arch 默认使用 [GNU 的](/index.php/GNU_Project "GNU Project") *tar* 程序。

对于 *.tar* 文件，*tar* 默认根据扩展名来解压文件：

```
$ tar xvf *file.EXTENSION*

```

强制给定格式：

| 文件类型 | 解压命令 |
| `*file*.tar` | `tar xvf *file*.tar` |
| `*file*.tgz` | `tar xvzf *file*.tgz` |
| `*file*.tar.gz` | `tar xvzf *file*.tar.gz` |
| `*file*.tar.bz` | `bzip -cd *file*.bz | tar xvf -` |
| `*file*.tar.bz2` | `tar xvjf *file*.tar.bz2`
`bzip2 -cd *file*.bz2 | tar xvf -` |
| `*file*.tar.xz` | `tar xvJf *file*.tar.xz`
`xz -cd *file*.xz | tar xvf -` |
| `*file*.tar.zst` | `tar -I zstd xvf *file*.tar.zst` |

这其中有部分 *tar* 的参数可以认为是历史遗留问题，但在执行某些特定的操作时仍然有用。更多细节请参阅 [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1)。

## which

[which](https://en.wikipedia.org/wiki/Which_(Unix) 显示 shell 命令的完整路径。在下面的例子中 `ssh` 的完整路径作为一个参数传递给了 `journalctl`：

```
# journalctl $(which sshd)

```

## wipefs

*wipefs* 可以列出或擦除指定设备的 [文件系统](/index.php/File_system "File system")、[RAID](/index.php/RAID "RAID") 或 [分区表](/index.php/Partition "Partition") 标志 (magic strings)。它不会擦除文件系统本身，也不会擦除设备中的任何其他数据。

更多信息请参阅 [wipefs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipefs.8)。

例如，擦除 `/dev/sdb` 设备中的所有标志并为每个标志在 `~/wipefs-sdb-*offset*.bak` 创建一个备份文件：

```
# wipefs --all --backup /dev/sdb

```

## 参阅

*   [A sampling of coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Overview of commands in coreutils
*   [GNU Coreutils online documentation](https://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [Learn the DD command](https://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)