**翻译状态：** 本文是英文页面 [Pacman_tips](/index.php/Pacman_tips "Pacman tips") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-05-17，点击[这里](https://wiki.archlinux.org/index.php?title=Pacman_tips&diff=0&oldid=201509)可以查看翻译后英文页面的改动。

## Contents

*   [1 修饰和便利](#.E4.BF.AE.E9.A5.B0.E5.92.8C.E4.BE.BF.E5.88.A9)
    *   [1.1 彩色输出](#.E5.BD.A9.E8.89.B2.E8.BE.93.E5.87.BA)
    *   [1.2 快捷方式](#.E5.BF.AB.E6.8D.B7.E6.96.B9.E5.BC.8F)
        *   [1.2.1 配置 shell](#.E9.85.8D.E7.BD.AE_shell)
        *   [1.2.2 用法](#.E7.94.A8.E6.B3.95)
        *   [1.2.3 注解](#.E6.B3.A8.E8.A7.A3)
    *   [1.3 巧用 Bash 语法](#.E5.B7.A7.E7.94.A8_Bash_.E8.AF.AD.E6.B3.95)
*   [2 维护](#.E7.BB.B4.E6.8A.A4)
    *   [2.1 显示所有软件包及其大小](#.E6.98.BE.E7.A4.BA.E6.89.80.E6.9C.89.E8.BD.AF.E4.BB.B6.E5.8C.85.E5.8F.8A.E5.85.B6.E5.A4.A7.E5.B0.8F)
        *   [2.1.1 查找不属于任何软件包的文件](#.E6.9F.A5.E6.89.BE.E4.B8.8D.E5.B1.9E.E4.BA.8E.E4.BB.BB.E4.BD.95.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.9A.84.E6.96.87.E4.BB.B6)
    *   [2.2 删除孤立软件包](#.E5.88.A0.E9.99.A4.E5.AD.A4.E7.AB.8B.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [2.3 删除base软件包组以外的所有软件包](#.E5.88.A0.E9.99.A4base.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.BB.84.E4.BB.A5.E5.A4.96.E7.9A.84.E6.89.80.E6.9C.89.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [2.4 仅显示正式安装的软件包](#.E4.BB.85.E6.98.BE.E7.A4.BA.E6.AD.A3.E5.BC.8F.E5.AE.89.E8.A3.85.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [3 安装和修复](#.E5.AE.89.E8.A3.85.E5.92.8C.E4.BF.AE.E5.A4.8D)
    *   [3.1 从 CD/DVD/ISO 安装软件包](#.E4.BB.8E_CD.2FDVD.2FISO_.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [3.1.1 从 Arch 的 core 镜像安装软件包](#.E4.BB.8E_Arch_.E7.9A.84_core_.E9.95.9C.E5.83.8F.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.2 自建本地仓库](#.E8.87.AA.E5.BB.BA.E6.9C.AC.E5.9C.B0.E4.BB.93.E5.BA.93)
    *   [3.3 在网络上共享pacman缓存](#.E5.9C.A8.E7.BD.91.E7.BB.9C.E4.B8.8A.E5.85.B1.E4.BA.ABpacman.E7.BC.93.E5.AD.98)
        *   [3.3.1 避免过度清理缓存](#.E9.81.BF.E5.85.8D.E8.BF.87.E5.BA.A6.E6.B8.85.E7.90.86.E7.BC.93.E5.AD.98)
    *   [3.4 备份和恢复已安装软件包](#.E5.A4.87.E4.BB.BD.E5.92.8C.E6.81.A2.E5.A4.8D.E5.B7.B2.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.5 列出所有不属于base或base-devel的已安装软件包](#.E5.88.97.E5.87.BA.E6.89.80.E6.9C.89.E4.B8.8D.E5.B1.9E.E4.BA.8Ebase.E6.88.96base-devel.E7.9A.84.E5.B7.B2.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.6 重新安装所有软件包](#.E9.87.8D.E6.96.B0.E5.AE.89.E8.A3.85.E6.89.80.E6.9C.89.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.7 恢复pacman本地数据库](#.E6.81.A2.E5.A4.8Dpacman.E6.9C.AC.E5.9C.B0.E6.95.B0.E6.8D.AE.E5.BA.93)
        *   [3.7.1 日志过滤脚本](#.E6.97.A5.E5.BF.97.E8.BF.87.E6.BB.A4.E8.84.9A.E6.9C.AC)
        *   [3.7.2 生成软件包列表](#.E7.94.9F.E6.88.90.E8.BD.AF.E4.BB.B6.E5.8C.85.E5.88.97.E8.A1.A8)
        *   [3.7.3 恢复数据库](#.E6.81.A2.E5.A4.8D.E6.95.B0.E6.8D.AE.E5.BA.93)
    *   [3.8 从已有安装修复 USB 系统](#.E4.BB.8E.E5.B7.B2.E6.9C.89.E5.AE.89.E8.A3.85.E4.BF.AE.E5.A4.8D_USB_.E7.B3.BB.E7.BB.9F)
    *   [3.9 解压缩软件包](#.E8.A7.A3.E5.8E.8B.E7.BC.A9.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [4 性能](#.E6.80.A7.E8.83.BD)
    *   [4.1 提高数据库访问速度](#.E6.8F.90.E9.AB.98.E6.95.B0.E6.8D.AE.E5.BA.93.E8.AE.BF.E9.97.AE.E9.80.9F.E5.BA.A6)
    *   [4.2 加快下载速度](#.E5.8A.A0.E5.BF.AB.E4.B8.8B.E8.BD.BD.E9.80.9F.E5.BA.A6)
        *   [4.2.1 使用 Powerpill](#.E4.BD.BF.E7.94.A8_Powerpill)
        *   [4.2.2 使用wget](#.E4.BD.BF.E7.94.A8wget)
    *   [4.3 使用aria2](#.E4.BD.BF.E7.94.A8aria2)
        *   [4.3.1 安装](#.E5.AE.89.E8.A3.85)
        *   [4.3.2 配置](#.E9.85.8D.E7.BD.AE)
        *   [4.3.3 参数细节 =](#.E5.8F.82.E6.95.B0.E7.BB.86.E8.8A.82_.3D)
            *   [4.3.3.1 其他解释](#.E5.85.B6.E4.BB.96.E8.A7.A3.E9.87.8A)
        *   [4.3.4 使用其它程序](#.E4.BD.BF.E7.94.A8.E5.85.B6.E5.AE.83.E7.A8.8B.E5.BA.8F)

## 修饰和便利

### 彩色输出

pacman 4.1.0 开始支持彩色输出，只需要在`/etc/pacman.conf`中取消 Color 行前面的注释即可使用。

### 快捷方式

使用命令别名简化常用pacman命令，方便使用和记忆。

#### 配置 shell

下面是个范例，将其加入shell配置文件即，同时适用于[Bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)")和[Zsh](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)")：

```
# Pacman 别名示例
alias pacupg='sudo pacman -Syu'        # 同步软件仓库信息然后升级系统
alias pacin='sudo pacman -S'           # 从软件仓库安装软件包
alias pacins='sudo pacman -U'          # 从本地文件安装软件包
alias pacre='sudo pacman -R'           # 删除软件包，保留配置和依赖
alias pacrem='sudo pacman -Rns'        # 彻底删除软件包，清除配置，删除无用依赖
alias pacrep='pacman -Si'              # 显示软件仓库中某软件包的信息
alias pacreps='pacman -Ss'             # 在软件仓库搜索软件包
alias pacloc='pacman -Qi'              # 显示本地数据库中某软件包的信息
alias paclocs='pacman -Qs'             # 在本地数据库搜索软件包

```

```
# 更多示例
alias pacupd='sudo pacman -Sy && sudo abs'     # 同步软件仓库信息并更新abs
alias pacinsd='sudo pacman -S --asdeps'        # 将某软件包作为其它软件包的依赖安装
alias pacmir='sudo pacman -Syy'                # 强制刷新软件仓库信息

```

#### 用法

就像使用普通命令一样使用这些别名即可。例如，要同步软件仓库信息然后升级系统：

```
$ pacupg

```

从软件仓库安装软件包：

```
$ pacin <软件包1> <软件包2> <软件包3>

```

安装软件包文件：

```
$ pacins /path/to/<软件包路径>

```

彻底删除软件包：

```
$ pacrem <软件包>

```

在软件仓库搜索软件包：

```
$ pacreps <关键字>

```

显示软件仓库中某软件包的信息（比如：占用空间，依赖关系）：

```
$ pacrep <keywords>

```

#### 注解

上面提供的只是一个例子。按照上面的格式，可以自己编写命令别名，比如：

```
alias pacrem='sudo pacman -Rns'
alias pacout='sudo pacman -Rns'

```

上面的例子中，`pacrem`和`pacout`代表同样的命令：`sudo pacman -Rns`。你可以使用自己喜欢的名称代替这些命令。

### 巧用 Bash 语法

下面应用[Bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)")技巧，实现复杂的pacman功能。

*   安装多个名称部分相同的软件包（而非安装整个软件包组），以[kde](https://www.archlinux.org/groups/x86_64/kde/)为例：

```
 pacman -S kde-{applets,theme,tools}

```

*   也可以嵌套使用：

```
 pacman -S kde-{ui-kde,kdeartwork}

```

*   使用`-s`搜索时会匹配软件包描述，从而导致很多不需要的结果。限制只匹配软件包名称：

```
 pacman -Ss '^vim-'

```

*   pacman的`-q`操作会输出所有本地软件包名称。利用该输出、以及简单的shell技巧，重新安装所有名称包含“compiz”的软件包：

```
 pacman -S $(pacman -Qq | grep compiz)

```

## 维护

保持系统干净，遵循 [Arch 之道](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")。

### 显示所有软件包及其大小

将所有软件包按占用空间大小排序输出：

*   安装 [expac](https://www.archlinux.org/packages/?name=expac) 并运行 `expac -s "%-30n %m"`
*   用 [community] 中的 [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) 加 -c 选项可以生成所有安装的软件包及其大小.

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

下面命令可以插入 `$HOME/.bashrc` 并在找到孤立软件包时进行删除：

```
orphans() {
  if [[ ! -n $(pacman -Qdt) ]]; then
    echo no orphans to remove
  else
    sudo pacman -Rs $(pacman -Qdtq)
  fi
}
```

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

**小贴士:** 另外一个方案：[pacserve](http://xyne.archlinux.ca/projects/pacserve/)。

要在多机间共享软件包，使用任何网络协议共享`/var/cache/pacman/`目录即可。本节介绍如何使用shfs或sshfs，在局域网内的多机间分享软件包及相关库文件目录。注意，网络间共享可能速度缓慢，取决于所选文件系统等因素。

首先，在服务器安装任意网络文件系统：[sshfs](/index.php/Sshfs "Sshfs")，[shfs](/index.php/Shfs "Shfs")，[ftpfs](/index.php?title=Ftpfs&action=edit&redlink=1 "Ftpfs (page does not exist)")，[smbfs](/index.php/Smbfs "Smbfs")或[nfs](/index.php/Nfs "Nfs")。

**小贴士:** 使用sshfs或shfs前，先阅读[Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys")。

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

### 恢复pacman本地数据库

如果遇到下面的问题，很可能需要恢复pacman本地数据库：

*   `pacman -Q`什么都不输出，`pacman -Syu`错误地报告系统已为最新。
*   使用`pacman -S`安装软件包时，很多已经安装过的依赖提示未安装。

pacman储存本地软件包的数据库`/var/lib/pacman/local`很可能已经损坏甚至丢失。这是很严重的问题，请按照如下步骤修复。

首先，确认pacman的日志文件还在：

```
$ ls /var/log/pacman.log

```

如果日志丢失了，那就*不能*使用本方法修复，可以尝试使用[Xyne的软件包检测脚本](https://bbs.archlinux.org/viewtopic.php?pid=670876)重建数据库。要是还行不通，很遗憾，最后的路就是重装系统。

#### 日志过滤脚本

创建一个awk脚本文件，内容如下 ：

 `log2pkglist.awk` 
```
#!/bin/awk -f

$3 ~ /^(installed|upgraded)$/ {
  pkg[$4] = 1
  next
} 

$3 == "removed" {
  pkg[$4] = 0
} 

END {
  for (i in pkg) if (pkg[i]) print i
}

```

打上可执行标志：

```
$ chmod +x log2pkglist.awk

```

#### 生成软件包列表

运行该脚本，输出到一个文本文件中：

```
$ ./log2pkglist.awk /var/log/pacman.log > pkglist.orig

```

（可选）手动检查`pkglist.orig`，删除所有不需要重新安装的软件包，例如：自己从ABS安装的软件包。

过滤掉无法从软件仓库中安装的软件包：

```
$ { cat pkglist.orig; pacman -Slq; } | sort | uniq -d > pkglist

```

检查**base**软件包组中的软件包是否缺失，并加入列表：

```
$ comm -23 <(pacman -Sgq base) pkglist.orig >> pkglist

```

当`pkglist`列表内容完备后，继续下一步，利用这个列表恢复数据库。

#### 恢复数据库

建立临时的缓存、数据库以及根目录：

```
tmp=~/tmp
mkdir -p "${tmp}"

pushd "${tmp}"
dbpath=$(readlink -f ./dbpath)
root=$(readlink -f ./root)
cache=$(readlink -f ./cache)
log=/dev/null
mkdir -p "${dbpath}" "${cache}" "${root}"
popd

recovery-pacman() {
  fakeroot pacman "$@"   \
    --dbpath "${dbpath}" \
    --root   "${root}"   \
    --cache  "${cache}"  \
    --log    "${log}"    \
    --noscriptlet        \
    #
}
```

同步临时目录中的数据库：

```
$ recovery-pacman -Sy

```

或者复制系统的数据库：

```
$ cp -r /var/lib/pacman/sync "${dbpath}"

```

（可选）要避免下载和处理当前系统本地数据库中存在的软件包，复制本地数据库到临时目录：

```
$ cp -r /var/lib/pacman/local "${dbpath}"

```

从上一步获取的`pkglist`生成临时本地数据库：

```
$ recovery-pacman -S --nodeps --needed $(< pkglist)

```

**注意:** 由于`--noscriptlet`选项，fakeroot生成的文件不会被真正安装到系统中。

生成数据库后，复制到真正的系统中：

```
# cp -r "${dbpath}"/local /var/lib/pacman

```

最后，更新本地数据库，将不受其他软件包依赖的软件包标记为手动安装，剩下的标记为依赖安装：

```
# pacman -D --asdeps $(pacman -Qq)
# pacman -D --asexplicit $(pacman -Qtq)

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

Powerpill 是 Pacman 的完整包裹程序，增加了平行下载和分段下载功能，加速下载过程。Pacman 一次只下载一个软件包，完成后才开始下一个下载。 Powerpill 同时下载多个软件包。 [Powerpill wiki 页面](/index.php/Powerpill "Powerpill")提供了基本的配置和使用方法。

#### 使用wget

对于需要更强大代理支持的用户来说，用wget比用Pacman自己的下载方式更加方便。

要使用 `wget`，首先使用`pacman -S wget`安装它，然后修改`/etc/pacman.conf`并在其中的`[options]`区段将下面内容去掉注释：

```
XferCommand = /usr/bin/wget -c --passive-ftp -c %u

```

除了将`wget`参数放在`/etc/pacman.conf`里，你也可以直接修改`wget`配置文件（全局文件是`/etc/wgetrc`，各个用户的文件是`$HOME/.wgetrc`）。

### 使用aria2

[aria2](/index.php/Aria2 "Aria2")是一个具有断点续传和分块下载功能的轻量级下载软件，支持HTTP/HTTPS/FTP协议。[aria2](http://aria2.sourceforge.net/)可以多线程通过HTTP/HTTPS和FTP协议连接镜像服务器，显著提高下载速度。

**注意:** 在Pacman的XferCommand使用 aria2c **不会**导致并行下载多个包。因为Pacman调用XferCommand时是一次一个包调用的，等待下载完成才会启动下一个。想要并行下载多个包，参见下面的 [powerpill-light](#.E4.BD.BF.E7.94.A8_powerpill-light) 部分。

##### 安装

通过`pacman -S aria2`安装[aria2](https://www.archlinux.org/packages/?name=aria2)。

##### 配置

修改`/etc/pacman.conf`，在`[option]`段添加下列一行（如果已存在则修改之）：

 `XferCommand = /usr/bin/aria2c --allow-overwrite=true -c --file-allocation=none --log-level=error -m2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 -t5 -d / -o %o %u` 

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

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`