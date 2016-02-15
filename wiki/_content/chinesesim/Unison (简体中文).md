**翻译状态：** 本文是英文页面 [Unison](/index.php/Unison "Unison") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-07-26，点击[这里](https://wiki.archlinux.org/index.php?title=Unison&diff=0&oldid=317386)可以查看翻译后英文页面的改动。

**Unison**是一款可以在类UNIX操作系统(包括 Linux, Mac OS X, 和Solaris) 和Windows 环境下运行的双向文件同步工具。他可以把一个文件或目录的两个备份分别储存在两个不同的主机(或同一个主机的不同的磁盘上)，分别修改，并且通过把双方的改变传递到对方来完成同步。同时，他也不限制哪一方做主机。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 GUI](#GUI)
    *   [2.2 手动操作](#.E6.89.8B.E5.8A.A8.E6.93.8D.E4.BD.9C)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
*   [4 版本不兼容性](#.E7.89.88.E6.9C.AC.E4.B8.8D.E5.85.BC.E5.AE.B9.E6.80.A7)
*   [5 提醒与小技巧](#.E6.8F.90.E9.86.92.E4.B8.8E.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [5.1 人生苦短，少敲键盘](#.E4.BA.BA.E7.94.9F.E8.8B.A6.E7.9F.AD.EF.BC.8C.E5.B0.91.E6.95.B2.E9.94.AE.E7.9B.98)
    *   [5.2 常规配置文件同步](#.E5.B8.B8.E8.A7.84.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E5.90.8C.E6.AD.A5)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 安装

请从[official repositories](/index.php/Official_repositories "Official repositories") [安装](/index.php/Pacman "Pacman") [unison](https://www.archlinux.org/packages/?name=unison), 那里有提供 CLI, GTK+ 和 GTK+ 2.0 接口. 如果有线下文档需求的话，请从 [AUR](/index.php/AUR "AUR") 安装 [unison-doc](https://aur.archlinux.org/packages/unison-doc/).

## 配置

为了使用Unison，你需要创建一份配置文件.

### GUI

如果想在GUI环境下配置的话 请运行:

```
$ unison-gtk2

```

### 手动操作

或者，在`~/.unison`里手动创建配置文件，并且将接下来的几行加入到默认配置文件`~/.unison/_profilename_.prf`里。

为被同步文件定义根目录

```
root=/home/user/

```

定义一个远程目录，文件将被同步到那里

```
root=[ssh://example.com//path/to/server/storags](ssh://example.com//path/to/server/storags)

```

为[SSH](/index.php/SSH "SSH")提供参数(可选)

```
sshargs=-p 4000

```

定义同步哪些文件和目录:

```
# dirs
path=Documents
path=Photos
path=Study
# files
path=.bashrc
path=.vimrc

```

你还可以定义无视哪些文件:

```
ignore=Name temp.*
ignore=Name .*~
ignore=Name *.tmp

```

**Note:** 如若需要更多咨询请看 [User Manual and Reference Guide](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html)中的 [Sample profiles](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#profileegs)。

## 使用

设定好配置文件以后就可以开始同步了:

```
$ unison _profilename_

```

如果你选择使用GUI工具的话就这么干:

```
$ unison-gtk2

```

然后选择配置文件。Unison的界面很赞，你可以看到变动和进度。

## 版本不兼容性

如果你希望Unison能正常工作的话，请**确保**每一个客户端上安装的版本都是一样的。举个例子，如果一套电脑上安装了2.40版本而另外一台上安装的是2.32，那他们就没法互相同步了。这对于**所有全部一切**你希望进行同步作业的计算机都适用。

由于Linux发行版数目众多，Unison的release错综复杂，所以你很有可能会陷入老版本的泥潭。Arch Linux在上游的Extra repository里提供有最新版本的Unison。同时在 [AUR](/index.php/AUR "AUR") 有非官方的 2.32版本 ([unison-232](https://aur.archlinux.org/packages/unison-232/))和 2.27版本([unison-227](https://aur.archlinux.org/packages/unison-227/)) 的 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")，这样各种发行版的用户们都可以在他们的系统上愉快的使用Unison啦

## 提醒与小技巧

### 人生苦短，少敲键盘

如果哪位在一个有能力维持一个合适的scrollback buffer的VDT环境下运行Unison的话，他就没有确认每一个无冲突改变的必要了；设定 `auto` 为 true 来避开这些提示。

### 常规配置文件同步

在同步那些在不同的系统(比如服务器，工作站，笔记本，智能手机)但却含有通用构造(比如键盘映射，基本shell同义名)的配置文件(比如针对本地程序，对安全性敏感的配置)时，最好把这些内容放到分散的配置文件中(比如`.bashrc_common`)并且只对他们进行同步。

**Warning:** 通过让被同步方(甚至也许还包括其他与被同步方同步的机器)的配置文件接受恶意的篡改，配置文件的双向同步可能会打开一条入侵的光明大道。这对于对手来说很有吸引力，尤其是在比如公共shell服务器vs个人工作站这样双方"实力悬殊"的情况下，因为要瓦解一个安全等级更低的系统看起来真不是什么难事。你并不需要在两台特定的机器间进行双向同步时一直使用`noupdate`；如果真的有这个必要，请在同步时确认每一处变动。在对待自动的双向同步行为的时候,当心点。

## 参阅

*   [Unison (file synchronizer)](/index.php?title=Wikipedia&action=edit&redlink=1 "Wikipedia (page does not exist)")
*   [Official website](http://www.cis.upenn.edu/~bcpierce/unison/)
*   [Yahoo! user group](http://tech.groups.yahoo.com/group/unison-users)
*   _[Liberation through data replication](http://www.pgbovine.net/unison_guide.htm)_ by Philip Guo
*   _[Setting up Unison for your mom](http://www.pgbovine.net/unison-for-your-mom.htm)_ by Philip Guo
*   _[Replication using Unison](http://twiki.org/cgi-bin/view/Codev/ReplicationUsingUnison)_ on TWiki