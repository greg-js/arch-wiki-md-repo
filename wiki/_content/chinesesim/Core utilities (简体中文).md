**翻译状态：** 本文是英文页面 [Core_Utilities](/index.php/Core_Utilities "Core Utilities") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-07-26，点击[这里](https://wiki.archlinux.org/index.php?title=Core_Utilities&diff=0&oldid=326298)可以查看翻译后英文页面的改动。

本文涉及 GNU/Linux 系统的所谓的 "核心" 工具，就像 **less**, **ls**, 和 **grep**，包括了"但不限于"以上集成于GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) 中的工具。下文提供了颇为丰富的软件技巧和有帮助的其他信息。

## Contents

*   [1 cat](#cat)
*   [2 cron](#cron)
*   [3 dd](#dd)
    *   [3.1 检查 dd 运行时的进度](#.E6.A3.80.E6.9F.A5_dd_.E8.BF.90.E8.A1.8C.E6.97.B6.E7.9A.84.E8.BF.9B.E5.BA.A6)
    *   [3.2 dd 衍生](#dd_.E8.A1.8D.E7.94.9F)
*   [4 grep](#grep)
    *   [4.1 彩色化输出](#.E5.BD.A9.E8.89.B2.E5.8C.96.E8.BE.93.E5.87.BA)
*   [5 iconv](#iconv)
*   [6 ip](#ip)
*   [7 less](#less)
    *   [7.1 通过环境变量设置的彩色化输出](#.E9.80.9A.E8.BF.87.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F.E8.AE.BE.E7.BD.AE.E7.9A.84.E5.BD.A9.E8.89.B2.E5.8C.96.E8.BE.93.E5.87.BA)
    *   [7.2 直接通过包装来彩色化输出](#.E7.9B.B4.E6.8E.A5.E9.80.9A.E8.BF.87.E5.8C.85.E8.A3.85.E6.9D.A5.E5.BD.A9.E8.89.B2.E5.8C.96.E8.BE.93.E5.87.BA)
    *   [7.3 用Vim代替](#.E7.94.A8Vim.E4.BB.A3.E6.9B.BF)
    *   [7.4 读取标准输入时彩色化输出](#.E8.AF.BB.E5.8F.96.E6.A0.87.E5.87.86.E8.BE.93.E5.85.A5.E6.97.B6.E5.BD.A9.E8.89.B2.E5.8C.96.E8.BE.93.E5.87.BA)
*   [8 locate](#locate)
*   [9 ls](#ls)
*   [10 man](#man)
*   [11 mkdir](#mkdir)
*   [12 mv](#mv)
*   [13 rm](#rm)
*   [14 sed](#sed)
*   [15 seq](#seq)
*   [16 shred](#shred)
*   [17 sudo](#sudo)
*   [18 权限相关工具](#.E6.9D.83.E9.99.90.E7.9B.B8.E5.85.B3.E5.B7.A5.E5.85.B7)
*   [19 另请参阅](#.E5.8F.A6.E8.AF.B7.E5.8F.82.E9.98.85)

## cat

[cat](https://en.wikipedia.org/wiki/cat_(Unix) (*catenate*)是一件能够连接并显示多文件的标准Unix工具。

*   **cat** 并不内置于 shell ，不过若您追求高性能，您会发现在很多情况下改用[重定向](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)")就很方便得许多，例如编写脚本。事实上，`$ < *file*`的效果就如同`$ cat *file*`一样。

*   按照以下结构可直接在某文件添加多行文字：

```
$  cat << EOF >> *path/file*
 *first line*
 ...
 *last line*
 EOF

```

*   如果您希望能以倒读顺序显示文件内容，有个工具叫 [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* reversed).

## cron

[cron](https://en.wikipedia.org/wiki/cron "wikipedia:cron") 是在 Unix-like 操作系统中的一种计划任务。

参见 [cron](/index.php/Cron "Cron")。

**Note:** *systemd* 可以处理许多 *cron* 用例. 参阅 [related article](/index.php/Systemd/Timers "Systemd/Timers").

## dd

[dd](https://en.wikipedia.org/wiki/dd_(Unix) 是在 unix 和 类unix 系统中主要用于转换和拷贝文件的命令

**Note:** *cp* 等同于不带操作数的 *dd* ，但其并非被设计用于通用的磁盘擦除程序.

### 检查 dd 运行时的进度

默认情况下在任务完成前 dd 都没有输出，使用 *kill* 和 `USR1` 信号可以在不结束进程的情况下强制状态输出，打开第二个 root 终端并输入以下命令

```
# killall -USR1 dd

```

**Note:** 这也将影响到其他运行 *dd* 的进程.

或者:

```
# kill -USR1 *pid_of_dd_command*

```

例如:

```
# kill -USR1 $(pidof dd)

```

这将使 *dd* 立即输出进度到终端，例如:

```
605+0 records in
605+0 records out
634388480 bytes (634 MB) copied, 8.17097 s, 77.6 MB/s

```

### dd 衍生

其他类似 dd 带状态输出的程序, 例如一个简单的进度条.

	dcfldd 

	[dcfldd](https://www.archlinux.org/packages/?name=dcfldd) 一个用于鉴证和安全的dd增强版. 它接受多数 dd 的参数并且包括状态输出. 最后一个稳定版于2006年12月19日发布.

	ddrescue 

	GNU [ddrescue](https://www.archlinux.org/packages/?name=ddrescue) 是一个数据恢复工具. 它能忽略读取错误, 这在磁盘清理时几乎无用. 参见 [official manual](http://www.gnu.org/software/ddrescue/manual/ddrescue_manual.html) 获取跟多细节.

## grep

[grep](https://en.wikipedia.org/wiki/grep "wikipedia:grep") (来自 [ed](https://en.wikipedia.org/wiki/ed "wikipedia:ed")的 *g/re/p*，全局／正则 表达式／打印） 是最初给 Unix 写的命令行文字搜索工具，`grep`命令在文件或标准输入里搜索符合指定正则表达式模式的行，并把结果打印到标准输出。

*   记住，*grep* 能直接处理文件，所以用`$ grep *pattern* *file*`结构代替`$ cat *file* | grep *pattern*`即可。

*   若要 grep 集群服务器（VCS）的源代码，请使用专门的 Perl 工具[ack](https://www.archlinux.org/packages/?name=ack)。可访问[official web site](http://beyondgrep.com/)。

### 彩色化输出

除了美观用途以外，**grep**的彩色化输出也对学习[regexp](https://en.wikipedia.org/wiki/regexp "wikipedia:regexp")和**grep**功能很有用。

请在您的shell配置文件添加以下内容以启用默认的彩色化输出，适用于[Bash](/index.php/Bash "Bash")：

 `~/.bashrc`  `alias grep='grep --color=auto'` 

您还可以直接设置**GREP_OPTIONS** [环境变量](/index.php/Environment_variables "Environment variables") [[2]](http://www.gnu.org/software/grep/manual/html_node/Environment-Variables.html) ，不过这有可能会影响到那些用到**grep** [[3]](http://brainstorm.ubuntu.com/idea/24141/)的脚本：

```
export GREP_OPTIONS='--color=auto'

```

如果要显示行数，添加"*-n*"参数即可：

```
alias grep='grep -n --color=auto'

```

`GREP_COLORS`环境变量其实可以设定成默认之外的。

## iconv

`iconv` 将转换一个文本的字符编码.

下列命令转换文件`foo`从 ISO-8859-15 到 UTF-8 保存至 `foo.utf`:

```
$ iconv -f ISO-8859-15 -t UTF-8 foo >foo.utf

```

查阅 `man iconv` 获取更多细节.

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

[less](https://en.wikipedia.org/wiki/less_(Unix) 是一个对文本文件内容进行分页显示的终端程序，它和其他的分页显示程序如`more`和`pg`相似，但`less`提供了更高级的界面和更多的功能。[[4]](http://www.greenwoodsoftware.com/less/faq.html)

### 通过环境变量设置的彩色化输出

请在您的 shell 配置文件添加：

 `~/.bashrc` 
```
export LESS=-R
export LESS_TERMCAP_me=$(printf '\e[0m')
export LESS_TERMCAP_se=$(printf '\e[0m')
export LESS_TERMCAP_ue=$(printf '\e[0m')
export LESS_TERMCAP_mb=$(printf '\e[1;32m')
export LESS_TERMCAP_md=$(printf '\e[1;34m')
export LESS_TERMCAP_us=$(printf '\e[1;32m')
export LESS_TERMCAP_so=$(printf '\e[1;44;1m')
```

值随您所愿修改，请参照：[ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors "wikipedia:ANSI escape code")，

### 直接通过包装来彩色化输出

您可直接开启**less**内置的代码高亮。先安装好[source-highlight](https://www.archlinux.org/packages/?name=source-highlight)再在您的Shell配置文件里添加以下：

 `~/.bashrc` 
```
export LESSOPEN="| /usr/bin/source-highlight-esc.sh %s"
export LESS='-R '

```

经常使用命令行界面的用户可以安装[lesspipe](https://www.archlinux.org/packages/?name=lesspipe)：

```
# pacman -S lesspipe

```

用户可以使用以下 less 命令列出一个压缩包里的文件列表：

```
$ less compressed_file.tar.gz

```

```
==> use tar_file:contained_file to view a file in the archive
-rw------- username/group  695 2008-01-04 19:24 compressed_file/content1
-rw------- username/group   43 2007-11-07 11:17 compressed_file/content2
compressed_file.tar.gz (END)

```

`lesspipe`还被赋予`less`对文件而不仅是压缩包进行交互的能力，从而成为打开某一种文件的一个新工具（比如用来代替[html2text](https://www.archlinux.org/packages/?name=html2text)查看html文件。

安装完`lesspipe`后需重新登录以激活其功能，或者运行

```
source `/etc/profile.d/lesspipe.sh`

```

### 用Vim代替

[Vim](/index.php/Vim "Vim") (*visual editor improved*)有内置了某脚本，可直接查看文本文件、压缩包或目录的内容。在您的shell配置文件添加以下即可：

 `~/.bashrc`  `alias less='/usr/share/vim/vim73/macros/less.sh'` 

除了*less.sh*宏外还有另外一种用法, 依赖于 `PAGER`　环境变量. 安装 [vimpager](https://www.archlinux.org/packages/?name=vimpager) 并添加以下内容至shell配置文件:

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

所有使用 `PAGER` 环境变量的程序, 如 [git](/index.php/Git "Git"), 将使用 *vim* 作为分页程序.

### 读取标准输入时彩色化输出

**Note:** 建议将这些 [环境变量](#Colored_output_through_environment_variables) 添加到 `~/.bashrc` or `~/.zshrc`. 因为本节完全基于: `export LESS=R` 写成

当你运行一个命令和使用管道连接 [标准输出](https://en.wikipedia.org/wiki/Standard_output "wikipedia:Standard output") (*stdout*) 到 *less* 作为分页视图 (e.g. `yaourt -Qe --date | less`), 你也许会发现输出不再是彩色化的. 这通常是因为该程序试图检测如果其 *stdout* 是交互式终端, 在这种情况下将输出彩色化文本,否则输出未着色文本. 当你想重定向 *stdout* 到一个文件中，这是一个很好的行为, e.g. `yaourt -Qe --date > pkglst-backup.txt`. 但是，当你想在 `less` 浏览输出时这将不是很好的行为.

一些程序提供禁用交互式 tty 检测的选项:

```
# dmesg --color=always | less

```

如果程序不提供任何类似选项，可以欺骗程序相信*stdout* 是交互式终端，有几种可行方式:

1\. [stdoutisatty](https://github.com/lilydjwg/stdoutisatty) 是一个用c写成的小程序, 它可以调用 "fake interactive tty". 你可以通过 [AUR](/index.php/AUR "AUR"): [stdoutisatty](https://aur.archlinux.org/packages/stdoutisatty/)安装. 用法示例:

```
$ stdoutisatty yaourt -Qe --date | less

```

2\. [socat](http://www.dest-unreach.org/socat/) 是两个独立的数据通道之间的双向数据传输的中继. 基于 GNU [readline](https://www.archlinux.org/packages/?name=readline) 且可用的包位于 [official repositories](/index.php/Official_repositories "Official repositories"): [socat](https://www.archlinux.org/packages/?name=socat). 用法示例:

```
$ socat EXEC:"yaourt -Qe --date",pty STDIO | less

```

3\. [script](http://man7.org/linux/man-pages/man1/script.1.html) 是一个相当古老的实用工具， 可生成终端会话的typescript. 用法示例:

```
$ script -fqc 'yaourt -Qe --date' | less

```

**Tip:** Perhaps this helper function from [stackoverflow](http://stackoverflow.com/questions/1401002/trick-an-application-into-thinking-its-stdin-is-interactive-not-a-pipe/20401674#20401674) will be useful:
```
function faketty {script -qfc "$(printf "'%s' " "$@")"}

```

4\. [unbuffer](http://expect.sourceforge.net/example/unbuffer.man.html) 是一个基于 *sh* 和 [Tcl](http://tcl.tk/) 的很好的 (手册比程序本身还要长), 古老的脚本. *unbuffer* 附带 [expect](https://www.archlinux.org/packages/?name=expect). 我们只需要这样使用:

```
$ unbuffer yaourt -Qe --date | less

```

5\. [zpty](http://zsh.sourceforge.net/Doc/Release/Zsh-Modules.html#The-zsh_002fzpty-Module) 是 [zsh](/index.php/Zsh "Zsh") 的一个模块, 这里有一个来自 依云[[5]](http://lilydjwg.is-programmer.com/2011/6/29/using-zpty-module-of-zsh.27677.html) 的小函数, 将其放入 `~/.zshrc`:

```
ptyless() {
    zmodload zsh/zpty
    zpty ptyless ${1+"$@"}            # ptyless, name of pty
    zpty -r ptyless > /tmp/ptyless.$$ # Write to file, just dunno why pipeline doesn't work fine here
    less /tmp/ptyless.$$
    rm -f /tmp/ptyless.$$
    zpty -d ptyless                   # remove used pty
}

```

用法:

```
$ ptyless yaourt -Qe --date | less

```

## locate

[locate](https://en.wikipedia.org/wiki/locate_(Unix) 用于在文件系统中查找文件. 它通过由 *updatedb* 预生成的或者由守护进程和增量编码压缩过的文件数据库搜索. 它要快于 *find*, 但需要经常更新数据库.

参见 [main article](/index.php/Locate "Locate").

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls")是一个Unix和类Unix系统中列出目录里的文件的一个命令。

*   *ls* 可以列出 [file permissions](/index.php/File_permissions_and_attributes#Viewing_permissions "File permissions and attributes").

*   可以使用一个简单的命令别名启用彩色输出功能，`~/.bashrc`文件应该已经有一句从`/etc/skel/.bashrc`复制过来的指定别名命令：

	`alias ls='ls --color=auto'`

	以下步骤可以进一步改进`ls`的彩色输出功能，比如损坏的符号链接显示为红色，把以下内容添加到`~/.bashrc`，然后重新登录，或者把脚本source一下：

	`eval $(dircolors -b)`

## man

[man](https://en.wikipedia.org/wiki/Man_page "wikipedia:Man page") (*manual page*)是常见于Unix-like操作系统的一种在线软件文档的格式，内容涉及了计算机程序（包括库或系统调用），常见标准或惯例，甚至还有抽象概念。请阅读[Man Pages](/index.php/Man_Pages "Man Pages")。

## mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir_(Unix) (*make directory*)是一条创建目录的命令。

*   若需递归地创建一系列目录，就要用到 *-p*参数了。已经十分熟悉这原理的高级用户也可直接设为内置参数：

	 `alias mkdir='mkdir -p -v'` 

	`-v`参数可以使创建目录的消息更为详细。

*   不必使用 *chmod* 更改权限模式, 用 `-m`选项可直接定义新建目录的访问权限

**Note:** 如果您仅仅只是想建个临时目录，也许用**mktemp** (*make termporary*)更好: `$ mktemp -p`.

## mv

[mv](https://en.wikipedia.org/wiki/mv_(Unix) (*move*)是一条移动或重命名文件和目录的命令。使用这命令的风险可不小，请务必小心。

```
alias mv=' timeout 8 mv -iv'

```

这命令别名可以延迟**mv** 到8秒后才生效，或是当删除三个以上的文件就会进行确认。

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) (*remove*)是一条删除文件或目录的命令。

*   它同样十分危险，使用时请提高警觉：

	 `alias rm=' timeout 3 rm -Iv --one-file-system'` 

	这种命令别名可延迟**rm**到3秒后才生效， 或是当删除三个以上的文件就会进行确认，或是限于只在同一个文件系统生效。

	若您想在删除多文件时一一确认，用`-I`代替`-i`即可。

	Zsh 的使用者可在 `timeout` 前加上 `noglob`，避免隐式扩展。

*   若要移除空目錄，使用 *rmdir*,　若内含文件则命令失败。

## sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") (*stream editor*)是一条专门解析或替换文本的命令。

这里有一系列现成的[示范](http://sed.sourceforge.net/sed1line.txt)

**Note:** awk更为优秀，甚至Perl语言也可以。

## seq

**seq** (*sequence*)是一条专门排列数字的命令。可以按照[Wikipedia](https://en.wikipedia.org/wiki/seq "wikipedia:seq")上进行练习。

## shred

[shred](https://en.wikipedia.org/wiki/Shred_(Unix) "wikipedia:Shred (Unix)")是一条更安全的删除命令，尽管如此也要小心点。

```
alias shred=' timeout 3 shred -v'

```

这种命令别名可延迟**shred**到3秒后才生效， 或是当删除三个以上的文件就会进行确认。

## sudo

[Sudo](https://en.wikipedia.org/wiki/Sudo "wikipedia:Sudo") (*as superuser do*)是Unix-like操作系统上的一件允许用户以其他用户的权限（一般是超级用户或root）来运行用户的程序，请阅读[Sudo](/index.php/Sudo "Sudo")。

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