**翻译状态：** 本文是英文页面 [Local_Mirror](/index.php/Local_Mirror "Local Mirror") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-05-26，点击[这里](https://wiki.archlinux.org/index.php?title=Local_Mirror&diff=0&oldid=258420)可以查看翻译后英文页面的改动。

**警告:** 如果你想创建一个官方镜像，参考 [这个页面](https://wiki.archlinux.org/index.php/DeveloperWiki:NewMirrors)。

## Contents

*   [1 稍等](#.E7.A8.8D.E7.AD.89)
    *   [1.1 替代方法](#.E6.9B.BF.E4.BB.A3.E6.96.B9.E6.B3.95)
*   [2 本地镜像](#.E6.9C.AC.E5.9C.B0.E9.95.9C.E5.83.8F)
    *   [2.1 需要牢记的事实](#.E9.9C.80.E8.A6.81.E7.89.A2.E8.AE.B0.E7.9A.84.E4.BA.8B.E5.AE.9E)
    *   [2.2 服务器设置](#.E6.9C.8D.E5.8A.A1.E5.99.A8.E8.AE.BE.E7.BD.AE)
        *   [2.2.1 编写 Rsync 命令](#.E7.BC.96.E5.86.99_Rsync_.E5.91.BD.E4.BB.A4)
        *   [2.2.2 示例脚本](#.E7.A4.BA.E4.BE.8B.E8.84.9A.E6.9C.AC)
        *   [2.2.3 另外一个使用 lftp 的脚本](#.E5.8F.A6.E5.A4.96.E4.B8.80.E4.B8.AA.E4.BD.BF.E7.94.A8_lftp_.E7.9A.84.E8.84.9A.E6.9C.AC)
        *   [2.2.4 部分镜像](#.E9.83.A8.E5.88.86.E9.95.9C.E5.83.8F)
        *   [2.2.5 服务](#.E6.9C.8D.E5.8A.A1)
    *   [2.3 客户端配置](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.85.8D.E7.BD.AE)

## 稍等

**警告:** 通常不赞成创建一个本地镜像，因为需要很大的带宽。其中一个替代的方法也许会满足你的要求。请查看下面的替代方法。

#### 替代方法

*   [在网络上共享 pacman 缓存](/index.php/Pacman_tips_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.9C.A8.E7.BD.91.E7.BB.9C.E4.B8.8A.E5.85.B1.E4.BA.ABpacman.E7.BC.93.E5.AD.98 "Pacman tips (简体中文)")

## 本地镜像

### 需要牢记的事实

*   镜像的带宽不是免费的，镜像必须为提供给你的数据付费
    *   尽管你已经为你的 ISP 付费，这也是成立的。
*   有很多你可能下载了却永远用不到的包
*   镜像的管理员会更喜欢让你仅下载需要的包
*   再次请求仔细查看上面的替代方案

**如果你完全确定本地镜像是唯一合适的解决方案，那么按照下面的指引操作。**

### 服务器设置

#### 编写 Rsync 命令

*   参照 [DeveloperWiki:NewMirrors](https://wiki.archlinux.org/index.php/DeveloperWiki:NewMirrors) 使用 rsync 参数
*   从上文中选择一个服务器
*   在 rsync 参数中包含 `--exclude-from="/path/to/exclude.txt"` 以排除那些你不想包含的目录或文件。示例内容可能包括：

```
iso

#Exclude i686 Packages
*/os/i686
pool/*/*-i686.pkg.tar.xz
pool/*/*-i686.pkg.tar.gz

#Exclude x86_64 Packages
*/os/x86_64
pool/*/*-x86_64.pkg.tar.xz
pool/*/*-x86_64.pkg.tar.gz

```

*   所有软件包都位于 pool 目录。然后从 pool 创建符号到 to core/extra/testing/etc。
    *   截至 9/21/2010 此迁移仍没有完成。
        *   在 ${repo}/os/${arch} 中应该有确切的软件包，而不是符号链接
*   排除那些你不需要的顶极目录

例如： `rsync *$rsync_arguments* --exclude="/path/to/exclude.txt" *rsync://example.com/* /path/to/destination`

#### 示例脚本

**警告:** 除非你阅读了本文开头的警告，否则不要使用本脚本

**警告:** 仅使用本脚本同步 Core/Extra/Community！ 如果你需要 Testing，gnome-unstable 或是任何其他软件库，另外使用 rsync --exclude！

是的，为了避免人们以复制粘贴的形式搭建他们自己的镜像，本脚本 **故意** 缺失了部分内容。如果你确实想要搭建一个镜像，错误是很容易修补的。

```
#!/bin/bash

#################################################################################################
### It is generally frowned upon to create a local mirror due the bandwidth that is required.
### One of the alternatives will likely fulfill your needs.
### REMEMBER:
###   * Bandwidth is not free for the mirrors. They must pay for all the data they serve you
###       => This still applies although you pay your ISP 
###       => There are many packages that will be downloaded that you will likely never use
###       => Mirror operators will much prefer you to download only the packages you need
###   * Really please look at the alternatives on this page:
###       [https://wiki.archlinux.org/index.php?title=Local_Mirror](https://wiki.archlinux.org/index.php?title=Local_Mirror)
### If you are ABSOLUTELY CERTAIN that a local mirror is the only sensible solution, then this
### script will get you on your way to creating it. 
#################################################################################################

# Configuration
SOURCE='rsync://mirror.example.com/archlinux'
DEST='/srv/mirrors/archlinux'
BW_LIMIT='500'
REPOS='core extra'
RSYNC_OPTS="-rtlHq --delete-after --delay-updates --copy-links --safe-links --max-delete=1000 --bwlimit=${BW_LIMIT} --delete-excluded --exclude=.*"
LCK_FLE='/var/run/repo-sync.lck'

# Make sure only 1 instance runs
if [ -e "$LCK_FLE" ] ; then
	OTHER_PID=`/bin/cat $LCK_FLE`
	echo "Another instance already running: $OTHER_PID"
	exit 1
fi
echo $$ > "$LCK_FLE"

for REPO in $REPOS ; do
	echo "Syncing $REPO"
	echo /usr/bin/rsync $RSYNC_OPTS ${SOURCE}/${REPO} ${DEST}
done

# Cleanup
/bin/rm -f "$LCK_FLE"

exit 0

```

#### 另外一个使用 lftp 的脚本

lftp 可以通过许多不同的协议来做镜像，如： ftp，http。它会在出错时重启，而且可以在后台运行。把如下代码放置到你的 $PATH 可以方便地使你在登出后镜像仍正常工作。

```
#!/usr/bin/lftp -f
lcd /local/path/to/your/mirror
open ftp.archlinux.org (or whatever your favorite mirror is)
# Use 'cd' to change into the proper directory on the mirror, if necessary.
mirror -cve -x '.*i686.*' core &
mirror -cve -x '.*i686.*' extra &
mirror -cve -x '.*i686.*' community &
mirror -cve -x '.*i686.*' multilib &
lcd pool
cd pool
mirror -cve -x '.*i686.*' community &
mirror -cve -x '.*i686.*' packages &

```

如果你想要查看当前镜像的状态，在终端打开 lftp ，输入 'attach <PID>'

#### 部分镜像

由于大多数软件包集中在 `pool/`，仅镜像部分软件库显然不容易。 [这篇博文](http://blog.invokk.net/2012/01/mirroring-only-some-repositories-of-archlinux/) 提供了一个脚本用于完成此任务。

#### 服务

*   HTTP (LAN)
    *   [LAMP](/index.php/LAMP "LAMP")
    *   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   FTP (LAN)
    *   [vsftpd](/index.php/Vsftpd "Vsftpd")
*   物理媒介
    *   闪存
    *   移动硬盘

### 客户端配置

*   在 /etc/pacman.d/mirrorlist 添加合适的 Server = variable
*   对于物理媒介 (例如闪存)，可以输入如下内容： Server = file:///mnt/media/repo/$repo/os/$arch (*/mnt/media/repo 是本地镜像位于的目录*)