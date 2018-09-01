**翻译状态：** 本文是英文页面 [Core_Utilities](/index.php/Core_Utilities "Core Utilities") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-31，点击[这里](https://wiki.archlinux.org/index.php?title=Core_Utilities&diff=0&oldid=538932)可以查看翻译后英文页面的改动。

相关文章

*   [Command-line shell](/index.php/Command-line_shell "Command-line shell")
*   [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")
*   [GNU](/index.php/GNU "GNU")
*   [sudo (简体中文)](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)")
*   [cron (简体中文)](/index.php/Cron_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cron (简体中文)")
*   [man page (简体中文)](/index.php/Man_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Man page (简体中文)")
*   [Securely wipe disk#shred](/index.php/Securely_wipe_disk#shred "Securely wipe disk")
*   [File permissions and attributes (简体中文)](/index.php/File_permissions_and_attributes_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File permissions and attributes (简体中文)")
*   [Color output in console (简体中文)](/index.php/Color_output_in_console_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Color output in console (简体中文)")
*   [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression")
*   [chmod](/index.php/Chmod "Chmod")
*   [chown](/index.php/Chown "Chown")

本文涉及 GNU/Linux 系统的所谓的 "核心" 工具，比如 **less**, **ls**, 和 **grep**，包括但不限于以上集成于 GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) 中的工具。下文提供了关于这些实用工具颇为丰富的技巧和有帮助的其他信息。

大多数命令行工具的文档都存放在 [man page](/index.php/Man_page "Man page") 里面，来自 [GNU Project](/index.php/GNU_Project "GNU Project") 的工具放在 [Info manual](/index.php/Info_manual "Info manual") 里面，一些 [shell](/index.php/Shell "Shell") 为它的内置命令提供了 `help` 命令。另外，大多数命令加上 `--help` 参数时会显示自身的使用说明。

## Contents

*   [1 文件管理](#.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86)
    *   [1.1 ls](#ls)
    *   [1.2 cat](#cat)
    *   [1.3 less](#less)
    *   [1.4 mkdir](#mkdir)
    *   [1.5 mv](#mv)
    *   [1.6 rm](#rm)
    *   [1.7 find](#find)
    *   [1.8 locate](#locate)
    *   [1.9 diff](#diff)
*   [2 文本流处理](#.E6.96.87.E6.9C.AC.E6.B5.81.E5.A4.84.E7.90.86)
    *   [2.1 grep](#grep)
    *   [2.2 sed](#sed)
    *   [2.3 awk](#awk)
*   [3 系统管理](#.E7.B3.BB.E7.BB.9F.E7.AE.A1.E7.90.86)
    *   [3.1 sudo](#sudo)
    *   [3.2 which](#which)
    *   [3.3 lsblk](#lsblk)
    *   [3.4 ip](#ip)
    *   [3.5 ss](#ss)
*   [4 杂项](#.E6.9D.82.E9.A1.B9)
    *   [4.1 dd](#dd)
    *   [4.2 iconv](#iconv)
    *   [4.3 od](#od)
    *   [4.4 seq](#seq)
    *   [4.5 tar](#tar)
    *   [4.6 wipefs](#wipefs)
*   [5 参考资料](#.E5.8F.82.E8.80.83.E8.B5.84.E6.96.99)

## 文件管理

| 命令 | 描述 | 手册页名称 | 示例 |
| cd | 变更目录（shell 内置命令） | [cd(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cd.1p) | cd /etc/pacman.d |
| mkdir | 创建目录 | [mkdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1) | mkdir ~/newfolder |
| rmdir | 删除空目录 | [rmdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rmdir.1) | rmdir ~/emptyfolder |
| rm | 删除文件 | [rm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rm.1) | rm ~/file.txt |
| rm -r | 删除目录和目录内文件 | rm -r ~/.cache |
| ls | 列出文件名称 | [ls(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ls.1) | ls *.mkv |
| ls -a | 列出隐藏文件 | ls -a /home/archie |
| ls -al | 显示隐藏文件和文件属性 |
| mv | 移动文件 | [mv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mv.1) | mv ~/compressed.zip ~/archive/compressed2.zip |
| cp | 复制文件 | [cp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cp.1) | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | 设置文件为[可执行文件](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.B7.BB.E5.8A.A0.E5.8F.AF.E6.89.A7.E8.A1.8C.E6.9D.83.E9.99.90 "Help:Reading (简体中文)") | [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1) | chmod +x ~/.local/bin/myscript.sh |
| cat | 显示文件内容 | [cat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cat.1) | cat /etc/hostname |
| find | 查找文件 | [find(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find.1) | find ~ -name myfile |

### ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") 可以列出目录中的文件名称。

请参考 `ls` [Info manual](/index.php/Info_manual "Info manual")（[在线版本](https://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html#ls-invocation)）获取更多信息。

[exa](https://the.exa.website) 相较于 `ls` 和 `tree` 是一个更加现代的、人性化的选择。它有更多的特性，例如将 [Git](/index.php/Git "Git") 修改和文件名一同显示，在 `--long` 模式中对每列进行不同的着色，或者在 `tree` 视图中显示 `--long` 模式元数据。*exa* 可以在软件包 [exa](https://www.archlinux.org/packages/?name=exa) 中找到。

`-l` 选项（“长格式”）用于显示文件类型、[权限](/index.php/File_permissions_and_attributes_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File permissions and attributes (简体中文)")、所有者的[用户名](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)")和[用户组](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.94.A8.E6.88.B7.E7.BB.84.E7.AE.A1.E7.90.86 "Users and groups (简体中文)")、大小、修改时间等等，具体参阅 [info document](https://www.gnu.org/software/coreutils/manual/html_node/What-information-is-listed.html#index-long-ls-format)。

默认情况下，包含空格的文件名和目录名会被单引号引起。要改变这一特性，请使用 `-N` 或 `--quoting-style=literal` 选项。另外，将 `QUOTING_STYLE` [环境变量](/index.php/Environment_variables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Environment variables (简体中文)") 设置为 `literal` 也可以。[[1]](https://unix.stackexchange.com/questions/258679/why-is-ls-suddenly-surrounding-items-with-spaces-in-single-quotes)

### cat

[cat](https://en.wikipedia.org/wiki/cat_(Unix) 是一个将文件内容发送到标准输出的标准 Unix 工具。

如果您希望能以倒读顺序显示文件内容，有个位于 coreutils 包中的工具叫 [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* 倒着写)。

### less

[less](https://en.wikipedia.org/wiki/less_(Unix) 是一个对文本文件内容进行分页显示的终端程序，它与其他的分页显示程序如 [more](https://en.wikipedia.org/wiki/more_(command) 和 [已废弃](https://git.kernel.org/cgit/utils/util-linux/util-linux.git/tree/Documentation/deprecated.txt) 的 [pg](https://en.wikipedia.org/wiki/pg_(Unix) 相似，但 *less* 提供了更高级的界面和更复杂的 [功能](http://www.greenwoodsoftware.com/less/faq.html)。

参阅 [List of applications#Terminal pagers](/index.php/List_of_applications#Terminal_pagers "List of applications") 查找更多可选方案。

### mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir "wikipedia:mkdir") (*make directory*) 可以创建目录。

若需递归地创建一系列目录，就要用到 `-p` 参数，否则会出错。

用 `-m` 选项可直接指定新建目录的访问权限，因此不必使用 *chmod* 更改权限。

**提示：** 如果您仅仅只是想建个临时目录，也许用 [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file"): `mktemp -d` 更好。

### mv

[mv](https://en.wikipedia.org/wiki/mv "wikipedia:mv") (*move*) 可以移动或重命名文件和目录。

**注意:** 一旦你习惯了“安全别名”，那它就是危险的，因为当你使用另一个没有这些别名的系统或用户时，可能会导致数据丢失。

为了降低使用这个命令带来的风险，请为它添加一个别名：

```
alias mv='mv -iv'

```

这个别名可以在覆盖已存在的文件前要求确认，并会显示出正在进行的操作。

### rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) (*remove*) 用于删除文件或目录。

**注意:** 一旦你习惯了“安全别名”，那它就是危险的，因为当你使用另一个没有这些别名的系统或用户时，可能会导致数据丢失。

为了降低使用这个命令带来的风险，请为它添加一个别名：

```
alias rm='rm -Iv --one-file-system'

```

这个别名可以在删除三个以上的文件时要求确认、显示出正在进行的操作、不跨越多个文件系统。如果想在删除一个文件时也获得确认，用 `-i` 代替 `-I` 即可。

Zsh 用户可在命令前加上 `noglob`，避免隐式扩展。

若要移除空目录，使用 *rmdir*，若内含文件则命令失败。

### find

*find* 是 [findutils](https://www.archlinux.org/packages/?name=findutils) 软件包的一部分, 它属于 [base](https://www.archlinux.org/groups/x86_64/base/) 软件包组。

**提示：** [fd](https://www.archlinux.org/packages/?name=fd) 是 `find` 的一个更加简单、快速、友好的替代方案，它有着更合理的默认值（比如忽略隐藏文件、文件夹和 `.gitignore` 等文件，可用 `fd PATTERN` 代替 `find -iname '*PATTERN*'`）。它具有彩色输出（类似 `ls`），unicode 支持，正则表达式支持等等。

你可能希望 *find* 命令将一个文件名称作为参数，并在文件系统中搜索与该名称匹配的文件。下面的 [#locate](#locate) 程序可以专门做这件事。

相反，find 需要一组目录，并将它们下面的每个文件与一组表达式进行匹配。这种设计为实现一些强大的“单行小程序” ("one-liners") 提供了支持，而这是上述“直观”设计无法实现的。参阅 [GregsWiki:UsingFind](https://mywiki.wooledge.org/UsingFind "gregswiki:UsingFind") 来获取使用说明。

### locate

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [mlocate](https://www.archlinux.org/packages/?name=mlocate)。包里包括了一个 `updatedb.timer` 单元，用于每天更新数据库。这个 systemd 定时器在安装后就会 enable，如果不想重启系统就开始使用它，请手动 [start](/index.php/Start "Start")。以 root 身份手动运行 *updatedb* 也可以更新数据库。默认会忽略 `/media` 和 `/mnt` 等路径，所以 *locate* 无法找到外置设备里的文件。详情请参考 [updatedb(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.8)。

*locate* 命令是一个靠文件名快速查找文件的常用 Unix 工具。因为是从数据库查找而不是直接访问文件系统，所以速度比 [find](https://en.wikipedia.org/wiki/Find "wikipedia:Find") 快很多。而缺点是在数据库更新后创建的新文件不会被搜索到。

使用 *locate* 前需建立数据库，请先以 root 权限执行 `updatedb`。

详情参考 [How locate works and rewrite it in one minute](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/)。

### diff

*diff* 用于逐行比较文件，它的输出内容可以放到一种被称为 patch 的文件里，而这种文件可以被 [patch(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/patch.1) 工具所使用。Arch Linux 默认的 *diff* 来自 GNU [diffutils](https://www.archlinux.org/packages/?name=diffutils)，而这个软件包也包含了 *cmp*，可以逐字节比较文件。

另一个可以逐行比对两份已排序的文件的命令叫 *comm*，参阅 [comm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/comm.1)。

比较文本文件时，逐个单词地比对通常更加合理：

*   [git](/index.php/Git "Git") 内置的 `git diff` 可以使用 `--color-words` 参数来实现逐词比较，使用 `--no-index` 参数来比较 Git 工作树外的文件。
*   **dwdiff** — 一个用于 diff 程序的逐词 diff 前端，支持彩色输出。

	[https://os.ghalkes.nl/dwdiff.html](https://os.ghalkes.nl/dwdiff.html) || [dwdiff](https://www.archlinux.org/packages/?name=dwdiff)

*   **GNU wdiff** — GNU 实现的逐词比较的 diff，不支持彩色输出。

	[https://www.gnu.org/software/wdiff/](https://www.gnu.org/software/wdiff/) || [wdiff](https://www.archlinux.org/packages/?name=wdiff)

*   **cwdiff** — 对 GNU wdiff 的包装，使它支持彩色输出。

	[https://github.com/junghans/cwdiff](https://github.com/junghans/cwdiff) || [cwdiff](https://aur.archlinux.org/packages/cwdiff/), [cwdiff-git](https://aur.archlinux.org/packages/cwdiff-git/)

## 文本流处理

### grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") (*global/regular expression/print*) 是最初给 Unix 写的命令行文字搜索工具，"grep" 命令在文件或标准输入里搜索符合指定正则表达式的行，并把结果打印到标准输出。

*   要在输出结果中显示行数，加上 `-n` 选项。
*   *grep* 可以在二进制文件中查找十六进制数值，例如要查找文件中的 `A1 F2`，应该这样写命令： `$ LANG=C grep --text --perl-regexp "\xA1\xF2" */path/to/file*` 

参阅 [Color output in console#grep](/index.php/Color_output_in_console#grep "Color output in console") 来启用彩色输出支持。

更多信息请参阅 [grep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grep.1)。

**提示：** 有专门用于检索版本控制系统（VCS）源代码的 *grep* 工具，例如 [ripgrep](https://www.archlinux.org/packages/?name=ripgrep)、[the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher) 和 [ack](https://www.archlinux.org/packages/?name=ack)，再加上 [mgrep](https://aur.archlinux.org/packages/mgrep/)（一个多行查找工具）。

### sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") (*stream editor*) 是一条专门过滤或替换文本的命令。

[这个列表](http://sed.sourceforge.net/sed1line.txt)里有一系列现成的 *sed* 单行命令示范。

**提示：** [awk](#awk) 和 [Perl](/index.php/Perl "Perl") 语言在这方面更为强大。

### awk

[AWK](https://en.wikipedia.org/wiki/AWK "wikipedia:AWK") 是一种模式扫描和处理语言，存在多个实现：

*   **gawk** — GNU 版本的 awk, 参考 [gawk(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gawk.1).

	[https://www.gnu.org/software/gawk/](https://www.gnu.org/software/gawk/) || [gawk](https://www.archlinux.org/packages/?name=gawk) （已经包含在[base](https://www.archlinux.org/groups/x86_64/base/)中）

*   **nawk** — 真正的 AWK 实现，参考 [nawk(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nawk.1).

	[https://www.cs.princeton.edu/~bwk/btl.mirror/](https://www.cs.princeton.edu/~bwk/btl.mirror/) || [nawk](https://www.archlinux.org/packages/?name=nawk)

*   **mawk** — 一个非常快速的 AWK 实现。

	[http://invisible-island.net/mawk/](http://invisible-island.net/mawk/) || [mawk](https://aur.archlinux.org/packages/mawk/)

*   [BusyBox](/index.php/BusyBox "BusyBox") 也包含了一个 AWK 实现。

## 系统管理

| 命令 | 描述 | 手册页名称 | 示例 |
| mount | 挂载分区 | [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) | mount /dev/sdc1 /media/usb |
| df -h | 显示各个分区上的剩余空间 | [df(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/df.1) |
| ps -A | 列出所有正在运行的进程 | [ps(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ps.1) |
| killall | 杀死所有运行中的进程实例 | [killall(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/killall.1) |
| ss -at | 列出所有已打开的 TCP 套接字 | [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8) |

### sudo

参阅 [Sudo](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)")。

### which

[which](https://en.wikipedia.org/wiki/Which_(Unix) 显示 shell 命令的完整路径。在下面的例子中 `ssh` 的完整路径作为一个参数传递给了 `journalctl`：

```
# journalctl $(which sshd)

```

### lsblk

[lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) 命令会显示所有连接到系统的 [块设备](https://en.wikipedia.org/wiki/Device_file#Block_devices "wikipedia:Device file") 和分区状况，例如：

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

设备名称的开头定义块设备的类型，大部分现代存储设备（如硬盘、[SSD](/index.php/SSD "SSD") 和 USB 闪存设备）都被识别为 SCSI disks (`sd`)。类型后面跟着给设备编号的小写字母，第一个设备从 `a` 开始 (`sda`)，第二个设备就是 `b` (`sdb`)，以此类推。每个设备上的 *现有* 分区将用数字编号，从 `1` 开始 (`sda1`)，第二个分区就是 `2` (`sda2`)，以此类推。在上面的示例中，只有一个设备可用 (`sda`)，该设备有三个分区 （`sda1` 到 `sda3`），每个分区具有不同的 [文件系统](/index.php/File_system "File system")。

其它常见的块设备有 `mmcblk`（内存卡）或 `nvme`（[NVMe](/index.php/NVMe "NVMe") 设备）。不清楚的设备类型可以在这里搜索到：[kernel documentation](https://www.kernel.org/doc/html/latest/admin-guide/devices.html)。

### ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") 显示关于网络设备，IP 地址，路由表和其他 Linux [IP](https://en.wikipedia.org/wiki/Internet_Protocol "wikipedia:Internet Protocol") 软件栈的对象信息。通过附加各种命令，你可以操纵或配置大多数对象。
**注意:** *ip* 命令在 [iproute2](https://www.archlinux.org/packages/?name=iproute2) 包中提供，这个包已经包含在 [base](https://www.archlinux.org/groups/x86_64/base/) 组。

| 子命令 | 作用 | 手册页名称 |
| ip addr | 协议地址管理 | [ip-address(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8) |
| ip addrlabel | 协议地址标签管理 | [ip-addrlabel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-addrlabel.8) |
| ip l2tp | tunnel Ethernet over IP (L2TPv3) | [ip-l2tp(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-l2tp.8) |
| ip link | 网络设备配置 | [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8) |
| ip maddr | 多播地址管理 | [ip-maddress(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-maddress.8) |
| ip monitor | 监测 netlink 信息 | [ip-monitor(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-monitor.8) |
| ip mroute | 多播路由缓存管理 | [ip-mroute(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-mroute.8) |
| ip mrule | 多播路由策略数据库的规则 |
| ip neigh | 邻居表/ARP 表管理 | [ip-neighbour(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-neighbour.8) |
| ip netns | process network namespace management | [ip-netns(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-netns.8) |
| ip ntable | 邻居表配置 | [ip-ntable(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-ntable.8) |
| ip route | 路由表管理 | [ip-route(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8) |
| ip rule | 路由策略数据库管理 | [ip-rule(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-rule.8) |
| ip tcp_metrics | 管理 TCP Metrics | [ip-tcp_metrics(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tcp_metrics.8) |
| ip tunnel | 隧道配置 | [ip-tunnel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tunnel.8) |
| ip tuntap | 管理 TUN/TAP 设备 |
| ip xfrm | 管理 IPsec 策略 | [ip-xfrm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-xfrm.8) |

`help` 帮助命令可用于所有子命令。例如，输入 `ip addr help` 将显示地址对象相关的命令语法。高级用法参见 [iproute2 documentation](http://www.policyrouting.org/iproute2.doc.html)。

[Network configuration (简体中文)](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)") 中提到了 *ip* 命令在多种实际任务中的使用方法。

**注意:** 你也许很熟悉旧版 Linux 中的 [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") 命令。在 Arch Linux 中现已不再使用；应当用 *ip* 替代之。

### ss

参阅 [Network configuration#Investigate sockets](/index.php/Network_configuration#Investigate_sockets "Network configuration")。

## 杂项

| 命令 | 描述 | 手册页名称 | 示例 |
| strings | 显示二进制文件中可打印的字符 | [strings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strings.1) | strings /usr/bin/free |

### dd

[dd](/index.php/Dd "Dd") 是在 unix 和 类 unix 系统中主要用于转换和拷贝文件的命令。

### iconv

*iconv* 可以转换文本的字符编码。

下列命令将文件 `*foo*` 从 ISO-8859-15 转换至 UTF-8，然后保存到 `*foo*.utf`：

```
$ iconv -f ISO-8859-15 -t UTF-8 *foo* > *foo*.utf

```

查阅 [iconv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iconv.1) 获取更多细节。

**提示：** 如果你不想改变文件的修改时间，可以用 [recode](https://www.archlinux.org/packages/?name=recode) 代替 iconv。

### od

[od](https://en.wikipedia.org/wiki/od_(Unix) (*o*ctal *d*ump) 命令在显示非人类可读格式时非常有用，比如程序的可执行文件，或者未格式化的设备的内容。参阅 [manual](https://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html#od-invocation) 了解详情。

### seq

*seq* (*sequence*) 可以打印一列数字。Shell 内置了该命令的其他替代方案，可以按照 [Wikipedia](https://en.wikipedia.org/wiki/Seq_(Unix) 的说明进行练习。

### tar

作为早期的 Unix 存档格式，.tar 文件（称为“tarballs”）广泛用于类 Unix 操作系统中的打包操作。[pacman](/index.php/Pacman "Pacman") 和 [AUR](/index.php/AUR "AUR") 软件包都是压缩的 tarball，Arch 默认使用 [GNU 的](/index.php/GNU_Project "GNU Project") *tar* 程序。

对于 *.tar* 文件，*tar* 默认根据扩展名来解压文件：

```
$ tar xvf *file.EXTENSION*

```

强制指定格式：

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

**注意:** 虽然 GNU 的 *tar* 是默认的 *tar* 程序，但是官方 Arch Linux 项目（如 [pacman](/index.php/Pacman "Pacman") 和 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")）使用的是 [libarchive](https://www.archlinux.org/packages/?name=libarchive) 包中的 *bsdtar*。

另请参考 [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression")。

### wipefs

*wipefs* 可以列出或擦除指定设备的 [文件系统](/index.php/File_systems_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File systems (简体中文)")、[RAID](/index.php/RAID_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "RAID (简体中文)") 或 [分区表](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)") 标志 (magic strings)。它不会擦除文件系统本身，也不会擦除设备中的任何其他数据。

更多信息请参阅 [wipefs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipefs.8)。

例如，擦除 `/dev/sdb` 设备中的所有标志并为每个标志在 `~/wipefs-sdb-*offset*.bak` 创建一个备份文件：

```
# wipefs --all --backup /dev/sdb

```

## 参考资料

*   [POSIX Utilities](http://pubs.opengroup.org/onlinepubs/9699919799/idx/utilities.html)
*   [GNU Coreutils online documentation](https://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [A sampling of coreutils on Reddit](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Overview of commands in coreutils
*   [Learn the DD command](https://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)