相关文章

*   [Mirrors (简体中文)](/index.php/Mirrors_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mirrors (简体中文)")
*   [创建软件包](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)")

**翻译状态：** 本文是英文页面 [Pacman_tips](/index.php/Pacman_tips "Pacman tips") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-08-29，点击[这里](https://wiki.archlinux.org/index.php?title=Pacman_tips&diff=0&oldid=487415)可以查看翻译后英文页面的改动。

Pacman 本身也是 bash 程序，所以有些通用优化请参考 [Core utilities](/index.php/Core_utilities "Core utilities") 和 [Bash](/index.php/Bash "Bash").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 维护](#维护)
    *   [1.1 查询软件包](#查询软件包)
    *   [1.2 显示所有软件包及其大小](#显示所有软件包及其大小)
        *   [1.2.1 获取大小](#获取大小)
        *   [1.2.2 按日期查询](#按日期查询)
        *   [1.2.3 查找不属于任何软件包的文件](#查找不属于任何软件包的文件)
    *   [1.3 删除孤立软件包](#删除孤立软件包)
    *   [1.4 删除base软件包组以外的所有软件包](#删除base软件包组以外的所有软件包)
    *   [1.5 仅显示正式安装的软件包](#仅显示正式安装的软件包)
*   [2 安装和修复](#安装和修复)
    *   [2.1 从 CD/DVD/ISO 安装软件包](#从_CD/DVD/ISO_安装软件包)
        *   [2.1.1 从 Arch 的 core 镜像安装软件包](#从_Arch_的_core_镜像安装软件包)
    *   [2.2 自建本地仓库](#自建本地仓库)
    *   [2.3 在网络上共享pacman缓存](#在网络上共享pacman缓存)
        *   [2.3.1 避免过度清理缓存](#避免过度清理缓存)
    *   [2.4 备份和恢复已安装软件包](#备份和恢复已安装软件包)
    *   [2.5 列出所有不属于base或base-devel的已安装软件包](#列出所有不属于base或base-devel的已安装软件包)
    *   [2.6 重新安装所有软件包](#重新安装所有软件包)
    *   [2.7 从已有安装修复 USB 系统](#从已有安装修复_USB_系统)
    *   [2.8 解压缩软件包](#解压缩软件包)
*   [3 性能](#性能)
    *   [3.1 提高数据库访问速度](#提高数据库访问速度)
    *   [3.2 加快下载速度](#加快下载速度)
        *   [3.2.1 使用 Powerpill](#使用_Powerpill)
        *   [3.2.2 使用wget](#使用wget)
    *   [3.3 使用aria2](#使用aria2)
        *   [3.3.1 安装](#安装)
        *   [3.3.2 配置](#配置)
        *   [3.3.3 参数细节 =](#参数细节_=)
            *   [3.3.3.1 其他解释](#其他解释)
        *   [3.3.4 使用其它程序](#使用其它程序)
*   [4 工具](#工具)
    *   [4.1 图形前端](#图形前端)

## 维护

保持系统干净，遵循 [Arch 之道](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")。参考 [System maintenance](/index.php/System_maintenance "System maintenance").

### 查询软件包

要获取已经的软件包以及它们的版本：

*   所有明确安装的软件包: `pacman -Qe`.
*   所有明确安装的，存在于数据库而且不是直接或可选依赖的软件包: `pacman -Qent`.
*   所有外部软件包 (通常是手动下载安装，或者已经从数据库中删除): `pacman -Qm`.
*   所有从数据库中安装的软件包: `pacman -Qn`.
*   按正则表达式查询软件包: `pacman -Qs *regex*`.
*   按正则表达式查询软件包，自定义输出格式：`expac -s "%-30n %v" *regex*` (需要安装 [expac](https://www.archlinux.org/packages/?name=expac)).

### 显示所有软件包及其大小

将所有软件包按占用空间大小排序输出：

*   安装 [expac](https://www.archlinux.org/packages/?name=expac) 并运行 `expac -s "%-30n %m"`
*   用 [community] 中的 [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) 加 -c 选项可以生成所有安装的软件包及其大小.

#### 获取大小

要按大小排序安装的软件包：

*   安装 [expac](https://www.archlinux.org/packages/?name=expac) 并运行 `expac -H M '%m\t%n' | sort -h`.
*   以 `-c` 参数执行 [pacgraph](https://www.archlinux.org/packages/?name=pacgraph).

查询软件包的下载大小(不加 `*packages*` 将查询所有软件包):

```
$ expac -S -H M '%k\t%n' *packages*

```

查询不属于 [base](https://www.archlinux.org/groups/x86_64/base/) 或 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 的软件包，带大小和描述：

```
$ expac -H M "%011m\t%-20n\t%10d" $(comm -23 <(pacman -Qqen | sort) <(pacman -Qqg base base-devel | sort)) | sort -n

```

#### 按日期查询

用 [expac](https://www.archlinux.org/packages/?name=expac) 查询最近安装的 20 个软件包：

```
$ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20

```

用从 epoch(1970-01-01 UTC) 开始的秒数：

```
$ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20

```

#### 查找不属于任何软件包的文件

建议定期检查 pacman 数据库之外的文件。通常这些文件是第三方程序使用一般方式安装 (例如 **./configure; make; make install**)。下面脚本可以找出它们：

 `pacman-disowned` 
```
#!/bin/sh

tmp=${TMPDIR-/tmp}/pacman-disowned-$UID-$$
db=$tmp/db
fs=$tmp/fs

mkdir "$tmp"
trap  'rm -rf "$tmp"' EXIT

pacman -Qlq | sort -u > "$db"

find /bin /etc /lib /sbin /usr \
  ! -name lost+found \
  \( -type d -printf '%p/
' -o -print \) | sort > "$fs"

comm -23 "$fs" "$db"

```

要生成列表：

```
$ pacman-disowned > non-db.txt

```

注意删除 `non-db.txt` 中的文件时先仔细确认。有写是配置文件、日志等，不要删除它们。

### 删除孤立软件包

递归删除孤立软件包：

```
# pacman -Rs $(pacman -Qtdq)

```

如果没有孤立软件包，将显示错误 `error: no targets specified`. 这个是正常的，因为 `pacman -Rns` 没有收到任何参数.

**Note:** `-Qt` 仅显示真的孤立包，要包含可选依赖，请使用 `-Qtt` .

### 删除base软件包组以外的所有软件包

以下命令会保留base软件包组、删除其他所有软件包：

 `# pacman -Rs $(comm -23 <(pacman -Qeq|sort) <((for i in $(pacman -Qqg base); do pactree -ul $i; done)|sort -u|cut -d ' ' -f 1))` 

来源：[这个帖子](https://bbs.archlinux.org/viewtopic.php?id=130176)

注记：

1.  `comm`命令需要已排序的输入，否则会得到诸如“comm: file 1 is not in sorted order”之类的错误信息。
2.  `pactree`是生成软件包依赖树的工具，输出如下：

 `$ pactree -lu logrotate` 
```
logrotate
popt
glibc
linux-api-headers
tzdata
dcron cron
bash
readline
ncurses
gzip
```

为了避免“dcron cron”（前者是软件包名，后者是该软件包提供的软件包名）这样的内容导致错误，用到了`cut -d ' ' -f 1`——只保留软件包名称。

### 仅显示正式安装的软件包

```
pacman -Qq |grep -Fv -f <(pacman -Qqm)

```

## 安装和修复

几种获取和修复软件包的方法。

### 从 CD/DVD/ISO 安装软件包

*   先挂载 CD （如果需要，替换*cdrom*为*dvd*或其他介质)：

```
# mount /mnt/cdrom

```

	如果使用的是ISO映像，先在 /mnt 建立一个目录：

```
# mkdir /mnt/iso

```

	然后挂载镜像：

```
# mount -t iso9660 -o ro,loop /path/to/iso /mnt/iso

```

*   配置pacman：

```
# nano -w /etc/pacman.conf

```

*   将如下仓库信息添加到其他软件仓库（如 extra、core）之前，确保优先使用介质中的软件包：

```
# 使用 cdrom 作为仓库
[custom]
Server = file:///mnt/cdrom/arch/pkg

```

	如果使用其他介质，记得替换 *cdrom* 。

修改`pacman.conf`后，更新软件仓库即可。

#### 从 Arch 的 core 镜像安装软件包

如果暂时无法链接网络（比如要配置无线网络），可以通过Arch的core仓库镜像获取软件包。先挂载之：

```
# mount -o loop /path/to/arch_core_image/i686/repo-core-i686.sfs /mnt/iso

```

然后修改`pacman.conf`的`[core]`段，（临时）替换为镜像挂载的位置：

```
[core]
#Include = /etc/pacman.d/mirrorlist
Server = file:///mnt/iso

```

然后同步：

```
# pacman -Syu

```

### 自建本地仓库

pacman 3 引入了一个名为`repo-add`脚本，用于帮助个人用户生成软件仓库。使用 `repo-add --help` 查看详细用法。

将所有要加入仓库的软件包放入一个目录，运行如下命令（*repo*是自建仓库的名称）：

```
$ repo-add /path/to/repo.db.tar.gz /path/to/*.pkg.tar.xz

```

注意，`repo-add`生成的数据库文件不一定和软件包放在同一目录，但使用pacman同步时，两者必须放在一起。

向仓库添加新软件包（并移除旧的）：

```
$ repo-add /path/to/repo.db.tar.gz /path/to/packagetoadd-1.0-1-i686.pkg.tar.xz

```

**注意:** 使用`repo-remove`删除软件包。

本地仓库建立后，添加仓库到`pacman.conf`。`db.tar.gz`文件的名字就是仓库的名字，路径格式是*file://...*或FTP地址*[ftp://localhost/path/to/directory](ftp://localhost/path/to/directory)*。

欢迎到[非官方用户软件仓库](/index.php/Unofficial_user_repositories "Unofficial user repositories")，分享你的仓库。

### 在网络上共享pacman缓存

**提示：** 另外一个方案：[pacserve](http://xyne.archlinux.ca/projects/pacserve/)。

要在多机间共享软件包，使用任何网络协议共享`/var/cache/pacman/`目录即可。本节介绍如何使用shfs或sshfs，在局域网内的多机间分享软件包及相关库文件目录。注意，网络间共享可能速度缓慢，取决于所选文件系统等因素。

首先，在服务器安装任意网络文件系统：[SSHFS](/index.php/SSHFS "SSHFS")，[shfs](/index.php/Shfs "Shfs")，[ftpfs](/index.php?title=Ftpfs&action=edit&redlink=1 "Ftpfs (page does not exist)")，[smbfs](/index.php/Smbfs "Smbfs")或[NFS](/index.php/NFS "NFS")。

**提示：** 使用sshfs或shfs前，先阅读[Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys")。

然后，挂载服务器的`/var/cache/pacman/pkg`到客户端机器上的`/var/cache/pacman/pkg`目录即可。

要分享软件包数据，使用同样方法共享`/var/lib/pacman/sync/{core,extra,testing,community}`即可。修改`/etc/fstab`以开机自动挂载。

#### 避免过度清理缓存

执行`pacman -Sc`清理软件包缓存时，会删除所有当前机器上为安装的软件包。由于pacman无法判断软件包是否在其他机器上安装，这会导致移除某些还需要的软件包。

避免的方法是修改清理方式为：删除所有已有新版本的过期软件包。添加以下内容到`/etc/pacman.conf`的`[options]`段：

```
CleanMethod = KeepCurrent

```

### 备份和恢复已安装软件包

定期备份软件包是个好习惯。万一系统出了大问题，需要重装，就可以利用备份的软件包恢复到原先的系统。

*   第一步，生成系统上安装的非本地（即从官方仓库获取的）软件包列表：

```
 $ comm -23 <(pacman -Qeq|sort) <(pacman -Qmq|sort) > pkglist

```

*   把生成的pkglist存储在一个安全的地方，比如U盘，或者gist.github.com、evernote、dropbox之类的文本储存网站。

*   今后重装系统时，把pkglist复制到新系统。

*   使用如下命令安装所有软件包：

```
 # pacman -S $(< pkglist)

```

要是备份的软件包列表包含非官方软件包（从AUR或其他什么地方下载的），就得使用下面这个吓人的命令了，不然pacman会出错：

```
# pacman -S --needed $(diff <(cat badpkglist|sort) <(diff <(cat badpkglist|sort) <(pacman -Slq|sort)|grep \<|cut -f2 -d' ')|grep \<|cut -f2 -d' ')

```

解释：

*   *pacman -Slq*列出所有可以安装的软件包。由于输出是按照来源仓库排序的，需要再调用*sort*排序。
*   排序是为*diff*命令比对列表做准备。
*   第一个*diff*返回所有无法安装的软件包；第二个返回所有可以安装的软件包。
*   *--needed*表示跳过已安装软件包。

可以接着用*yaourt*恢复从AUR获取的软件包（不推荐）：

```
$ yaourt -S --noconfirm $(diff <(cat badpkglist|sort) <(pacman -Slq|sort) |grep \<|cut -f2 -d' ')

```

最后，还可以卸载掉新系统上安装的、但之前系统并未安装的软件包。 警告：务必小心使用，仔细查看pacman输出，避免悲剧。

```
# pacman -Rsu $(diff <(cat badpkglist|sort) <(pacman -Qq|sort) | grep \>|cut -f2 -d' ')

```

### 列出所有不属于base或base-devel的已安装软件包

下列命令输出所有不属于base或base-devel软件包组的已安装软件包。这些软件包一般都是用户自己安装的：

```
comm -23 <(pacman -Qeq|sort) <(pacman -Qgq base base-devel|sort)

```

### 重新安装所有软件包

要是你的系统遭到了大规模破坏（比如`rm -rf`什么的），可以通过pacman重新安装所有软件包来挽救。

如果没有安装外来软件包（比如来自AUR的），使用如下命令即可：

```
# pacman -Qeq | pacman -S -
# pacman -Qdq | pacman -S --asdeps -

```

如果安装了外来软件包，使用上面的命令会出错。下面的命令先生成所有软件包列表，再用`pacman -Qmq`剔除外来软件包，即重新安装所有仓库中可以找到的软件包，同时保留依赖安装、手动安装标志：

```
# comm -23 <(pacman -Qeq) <(pacman -Qmq) | pacman -S -
# comm -23 <(pacman -Qdq) <(pacman -Qmq) | pacman -S --asdeps -

```

### 从已有安装修复 USB 系统

如果你有一个Arch安装在U盘上，不小心搞坏了（比如，写入U盘时断电了），可以使用主机上的Arch修复U盘上的Arch（假设U盘挂载在/newarch）：

```
# pacman -S $(pacman -Qq --dbpath /newarch/var/lib/pacman) --root /newarch --dbpath /newarch/var/lib/pacman

```

### 解压缩软件包

Arch软件包其实就是普通的xz压缩包，解压方法没啥特别的：

```
$ tar -Jxvf package.tar.xz

```

## 性能

### 提高数据库访问速度

Pacman将所有软件包的信息放在一一对应的许多小文件中。通过改善数据库访问速度，可以减少花在数据库相关任务上的时间，比如：寻找软件包、检索软件包依赖性。

最安全最简单的方法是以root身份运行

```
# pacman-optimize

```

上述命令试图将所有小文件放在磁盘上同一个物理区域，以减少磁头移动。这种方法很安全，但不一定有效。其效果取决于你的文件系统、磁盘使用率、和磁盘碎片程度。另一种更激进的方式是在优化数据库之前首先删除 cache 中所有未安装以及不使用的仓库中的包：

```
# pacman -Sc && pacman-optimize

```

### 加快下载速度

**注意:** 如果你的包下载速度变得极慢，首先确定你用的是那些([镜像](/index.php/Mirrors_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mirrors (简体中文)"))网站而不是ftp.archlinux.org，因为后者[从2007年3月开始限速](https://www.archlinux.org/news/302/)。

可以通过各种下载工具而不是Pacman内置的下载方式，来改善Pacman的下载速度。

不论怎样，在做任何修改前，你必须确定拥有了最新版的Pacman：

```
# pacman -Syu

```

#### 使用 Powerpill

Powerpill 是 Pacman 的完整包裹程序，增加了平行下载和分段下载功能，加速下载过程。Pacman 一次只下载一个软件包，完成后才开始下一个下载。 Powerpill 同时下载多个软件包。[Powerpill wiki 页面](/index.php/Powerpill "Powerpill")提供了基本的配置和使用方法。

#### 使用wget

对于需要更强大代理支持的用户来说，用wget比用Pacman自己的下载方式更加方便。

要使用 `wget`，首先使用`pacman -S wget`安装它，然后修改`/etc/pacman.conf`并在其中的`[options]`区段将下面内容去掉注释：

 `XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u` 

除了将`wget`参数放在`/etc/pacman.conf`里，你也可以直接修改`wget`配置文件（全局文件是`/etc/wgetrc`，各个用户的文件是`$HOME/.wgetrc`）。

### 使用aria2

[aria2](/index.php/Aria2 "Aria2")是一个具有断点续传和分块下载功能的轻量级下载软件，支持HTTP/HTTPS/FTP协议。[aria2](http://aria2.sourceforge.net/)可以多线程通过HTTP/HTTPS和FTP协议连接镜像服务器，显著提高下载速度。

**注意:** 在Pacman的XferCommand使用 aria2c **不会**导致并行下载多个包。因为Pacman调用XferCommand时是一次一个包调用的，等待下载完成才会启动下一个。想要并行下载多个包，参见下面的 [powerpill-light](#使用_Powerpill) 部分。

##### 安装

通过`pacman -S aria2`安装[aria2](https://www.archlinux.org/packages/?name=aria2)。

##### 配置

修改`/etc/pacman.conf`，在`[option]`段添加下列一行（如果已存在则修改之）：

 `XferCommand = /usr/bin/aria2c --allow-overwrite=true -c --file-allocation=none --log-level=error -m2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 -t5 -d / -o %o %u` 

#### 参数细节 =

	`/usr/bin/aria2c`

	aria2主程序的完整路径。

	`--allow-overwrite=true`

	如果相应的控制文件不存在则重新下载。(默认值：false)

	`-c, --continue`

	如果相应的控制文件存在则继续未完成的下载。

	`--file-allocation=none`

	下载开始前预设空间。(默认值: prealloc) 

	`--log-level=error`

	设置错误输出级别。 (默认值: debug)

	`-m2, --max-tries=2`

	从每个镜像源下载特定文件的最大尝试次数设为2。 (默认值: 5)

	`--max-connection-per-server=2`

	下载每个文件时到每个镜像源的最大连接数设为2。(默认值: 1)

	`--max-file-not-found=5`

	如果5次尝试后仍未下载完成1字节则强制停止。(默认值: 0)

	`--min-split-size=5M`

	只有当文件大于5MB时才分割下载。 (默认值: 20M)

	`--no-conf`

	不加载 `aria2.conf` 。 (默认值: `~/.aria2/aria2.conf`)

	`--remote-time=true`

	对远程文件应用时间戳并应用到本地文件。 (默认值: false)

	`--summary-interval=60`

	每60s显式一次下载总进度。 (默认值: 60) 

	`-t5, --timeout=5`

	对镜像源的连接建立后5s超时。 (默认值: 60)

	`-d, --dir`

	由 [pacman](/index.php/Pacman "Pacman") 设定的文件下载目录。

	`-o, --output`

	输出的下载文件的文件名

	`%o`

	代表 pacman 指定的文件名的变量

	`%u`

	代表 pacman 指定的 URL 的变量

##### 其他解释

	 `--file-allocation=falloc`

	对较新的文件系统建议使用，如 ext4(支持extents)、 btrfs 和 xfs 因为它们存储大文件(GB级别)时速度很快。 较老的文件系统如ext3则不要使用falloc，因为prealloc消耗的时间几乎和标准分配相同，同时会锁定aria2进程而停止下载。

	 `--summary-interval=0`

	减少下载总进度的输出并有可能改善性能。日志会按照 `log-level` 选项的设置继续输出。

#### 使用其它程序

这里还有一些可以和Pacman协同工作的下载软件。下面列举了它们对应的XferCommand命令写法：

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`

## 工具

*   **Lostfiles** — Script that identifies files not owned by any package.

	[https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [lostfiles](https://www.archlinux.org/packages/?name=lostfiles)

*   **Pacmatic** — Pacman wrapper to check Arch News before upgrading, avoid partial upgrades, and warn about configuration file changes.

	[http://kmkeen.com/pacmatic](http://kmkeen.com/pacmatic) || [pacmatic](https://www.archlinux.org/packages/?name=pacmatic)

*   **pacutils** — Helper library for libalpm based programs.

	[https://github.com/andrewgregory/pacutils](https://github.com/andrewgregory/pacutils) || [pacutils](https://www.archlinux.org/packages/?name=pacutils)

*   **[pkgfile](/index.php/Pkgfile "Pkgfile")** — Tool that finds what package owns a file.

	[http://github.com/falconindy/pkgfile](http://github.com/falconindy/pkgfile) || [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)

*   **pkgtools** — Collection of scripts for Arch Linux packages.

	[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)

*   **repoctl** — Tool to help manage local repositories.

	[https://github.com/cassava/repoctl](https://github.com/cassava/repoctl) || [repoctl](https://aur.archlinux.org/packages/repoctl/)

*   **repose** — An Arch Linux repository building tool.

	[https://github.com/vodik/repose](https://github.com/vodik/repose) || [repose](https://www.archlinux.org/packages/?name=repose)

*   **[snap-pac](/index.php/Snapper#Wrapping_pacman_transactions_in_snapshots "Snapper")** — Make pacman automatically use snapper to create pre/post snapshots like openSUSE's YaST.

	[https://github.com/wesbarnett/snap-pac](https://github.com/wesbarnett/snap-pac) || [snap-pac](https://www.archlinux.org/packages/?name=snap-pac)

### 图形前端

**Warning:** Some front-ends such as [octopi](https://aur.archlinux.org/packages/octopi/) [[1]](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) perform [partial upgrades](/index.php/Partial_upgrade "Partial upgrade") periodically.

*   **Arch-Update** — Update indicator for Gnome-Shell.

	[https://github.com/RaphaelRochet/arch-update](https://github.com/RaphaelRochet/arch-update) || [gnome-shell-extension-arch-update](https://aur.archlinux.org/packages/gnome-shell-extension-arch-update/)

*   **Arch-Update-Notifier** — Update indicator for KDE.

	[https://github.com/I-Dream-in-Code/kde-arch-update-plasmoid](https://github.com/I-Dream-in-Code/kde-arch-update-plasmoid) || [plasma5-applets-kde-arch-update-notifier-git](https://aur.archlinux.org/packages/plasma5-applets-kde-arch-update-notifier-git/)

*   **Discover** — A collection of package management tools for KDE, using PackageKit.

	[https://projects.kde.org/projects/kde/workspace/discover](https://projects.kde.org/projects/kde/workspace/discover) || [discover](https://www.archlinux.org/packages/?name=discover)

*   **GNOME packagekit** — GTK based package management tool

	[http://www.freedesktop.org/software/PackageKit/](http://www.freedesktop.org/software/PackageKit/) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **GNOME Software** — Gnome Software App. (Curated selection for GNOME)

	[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **kalu** — A small application that will add an icon to your systray and sit there, regularly checking if there's anything new for you to upgrade.

	[https://jjacky.com/kalu/](https://jjacky.com/kalu/) || [kalu](https://aur.archlinux.org/packages/kalu/)

*   **pamac** — A DBus daemon and Gtk3 frontend for libalpm written in Vala.

	[https://github.com/manjaro/pamac/](https://github.com/manjaro/pamac/) || [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/)

*   **pcurses** — Package management in a curses frontend

	[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **tkPacman** — Depends only on Tcl/Tk and X11, and interacts with the package database via the CLI of *pacman*.

	[http://sourceforge.net/projects/tkpacman](http://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)