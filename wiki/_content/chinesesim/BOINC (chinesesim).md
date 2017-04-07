[BOINC 官方网站](http://boinc.berkeley.edu/)：“利用您的计算机（Windows、Mac 以及 Linux）的空闲的时间，帮助寻找治疗疾病的方法、研究全球变暖、发现脉冲星…… 进行各种各样的科学研究。这一切简单且安全！”

[维基百科](https://en.wikipedia.org/wiki/BOINC "wikipedia:BOINC")：“伯克利开放式网络计算平台（Berkeley Open Infrastructure for Network Computing，BOINC）是一个用于志愿计算和网格计算的非商业的中间件系统。开发 BOINC 的最初目的是支援 SETI@home 项目，而后来它发展成为一个支持多种项目的强大的分布式计算平台，这些项目的研究领域涵盖了数学、医学、分子生物学、气候学以及天体物理学等等。BOINC 力图让研究人员享用到全世界数以亿计的个人电脑的强大计算能力。”

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
    *   [2.1 密码文件配置](#.E5.AF.86.E7.A0.81.E6.96.87.E4.BB.B6.E9.85.8D.E7.BD.AE)
    *   [2.2 图形界面](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2)
        *   [2.2.1 使用 GPU 的项目](#.E4.BD.BF.E7.94.A8_GPU_.E7.9A.84.E9.A1.B9.E7.9B.AE)
    *   [2.3 命令行界面](#.E5.91.BD.E4.BB.A4.E8.A1.8C.E7.95.8C.E9.9D.A2)
*   [3 日志文件](#.E6.97.A5.E5.BF.97.E6.96.87.E4.BB.B6)
*   [4 选择项目时需要考虑的因素](#.E9.80.89.E6.8B.A9.E9.A1.B9.E7.9B.AE.E6.97.B6.E9.9C.80.E8.A6.81.E8.80.83.E8.99.91.E7.9A.84.E5.9B.A0.E7.B4.A0)
    *   [4.1 64 位系统](#64_.E4.BD.8D.E7.B3.BB.E7.BB.9F)
*   [5 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [5.1 GPU missing](#GPU_missing)
    *   [5.2 笔记本过热，续航时间缩短](#.E7.AC.94.E8.AE.B0.E6.9C.AC.E8.BF.87.E7.83.AD.EF.BC.8C.E7.BB.AD.E8.88.AA.E6.97.B6.E9.97.B4.E7.BC.A9.E7.9F.AD)
    *   [5.3 无法下载 World Community Grid 任务](#.E6.97.A0.E6.B3.95.E4.B8.8B.E8.BD.BD_World_Community_Grid_.E4.BB.BB.E5.8A.A1)
    *   [5.4 cc_config.xml 相关配置](#cc_config.xml_.E7.9B.B8.E5.85.B3.E9.85.8D.E7.BD.AE)
*   [6 相关资源](#.E7.9B.B8.E5.85.B3.E8.B5.84.E6.BA.90)

## 安装

[官方仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 提供了 [boinc](https://www.archlinux.org/packages/?name=boinc) 和 [boinc-nox](https://www.archlinux.org/packages/?name=boinc-nox) 软件包，使用 [安装](/index.php/Pacman "Pacman") 其一即可。后者不依赖 [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")，适用于没有物理控制台的服务器。

两个软件包都提供了系统服务 `boinc.service`，可以使用 `systemctl` 管理。详情参见 [Systemd (简体中文)#使用单元](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)")。

## 使用

**注意:** 以下内容仅仅适用于：1、Arch 官方软件包提供的 BOINC；2、从 systemd 服务正确启动。如要通过 boinc 命令启动管理，请自行查阅相关文档。

### 密码文件配置

BOINC 服务会在首次启动后自动创建密码文件 `/var/lib/boinc/gui_rpc_auth.cfg`，任何管理器都需要使用该密码来链接 BOINC 服务。如果从菜单图标启动 BOINC Manager，它会自动读取该文件。但该文件默认只有用户 boinc 可读，为了连接 BOINC 服务，你需要先将当前用户加入 boinc 组，并修改密码文件的访问权限：

```
$ gpasswd -a <用户名> boinc
$ sudo chmod g+r /var/lib/boinc/gui_rpc_auth.cfg

```

重新登录即可生效。

如果你经常使用命令行操作，或需要从终端启动 BOINC Manager，则可将密码文件连接至用户目录，这样 BOINC Manager 或 boinccmd 就能自动连接 BOINC 服务：

```
$ cd ~/
$ ln -s /var/lib/boinc/gui_rpc_auth.cfg gui_rpc_auth.cfg

```

若要手动设置该密码（甚至清空），只需修改 `/var/lib/boinc/gui_rpc_auth.cfg` 文件，并重启 BOINC 服务即可。

### 图形界面

运行 `boincmgr` 命令启动图形界面的 BOINC Manager：

```
$ boincmgr

```

首次启动时，BOINC Manager 会指引你加入项目。注意，有些项目可以通过 BOINC Manager 直接创建项目，而有些则需要先在其网页上注册。如果存储空间、计算能力和时间等条件允许，可以通过菜单项 *工具 / 增加项目* 加入多个项目。

如果 BOINC Manager 没有像上面那样指引你加入项目，那么可能是连接 BOINC 服务失败了。点击菜单项 *高级 / 选择计算机*，输入计算机名（本机使用 `localhost` 即可），然后输入 `/var/lib/boinc/gui_rpc_auth.cfg` 中的密码即可。（如果不想每次都这样做，请确保按照上面的步骤正确配置 gui_rpc_auth.cfg 。）

#### 使用 GPU 的项目

要使用 GPU 计算，需要安装闭源的 [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)") 和 [AMD](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)") 驱动。对于 ATI/AMD 显卡，还需要安装 [AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 软件包 [libopencl](https://aur.archlinux.org/packages/libopencl/)。NVIDIA 用户只需安装 [extra] 中的 [opencl-nvidia](https://www.archlinux.org/packages/?name=opencl-nvidia) 即可。

此外还需要将 boinc 用户加入 video 组：

```
# gpasswd -a boinc video

```

boinc 用户还需要有访问你的 X session 的权限：

```
xhost local:boinc

```

若要避免每次都输入，可将上述命令加入启动脚本。

**注意:** 对于使用双显卡笔记本电脑的用户，如果使用某些软件（如 bumblebee/bbswitch）禁用了高性能显卡的驱动，在使用 GPU 计算时，可能遇到一些麻烦（找不到显卡、计算错误等等）。如果要使用 GPU 计算，原则上你必须在 BOINC 运行时确保显卡开启，以及加载正确的驱动模块。当前似乎还没有什么好的解决方案。 —— 译者注

### 命令行界面

对于命令行操作，可参照 `boinccmd` 和 `boinc` 命令的帮助及 man 手册。`boinccmd` 是 BOINC 自带的命令行界面工具。

## 日志文件

BOINC 的日志文件存放在 `/var/lib/boinc/` 中：

```
/var/lib/boinc/stderrdae.txt
/var/lib/boinc/stdoutdae.txt

```

## 选择项目时需要考虑的因素

不同项目的硬件要求（CPU、磁盘空间等）有所差异，每个任务的计算时间也不尽相同。如果不能在上报期限前完成任务，服务器会判定任务过期，并把他交给其他计算机。请根据硬件条件选择合适的项目，避免这样的问题发生。

此外，项目的研究方向和公开度也是需要考虑的因素。

### 64 位系统

某些项目只提供32位计算程序和图形显示程序，因此你需要从 [multilib] 安装一些基本的库。

	运行计算程序需要通常需要（以 Climateprediction 项目为例）：

	[lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc), [lib32-glib2](https://www.archlinux.org/packages/?name=lib32-glib2)

	显示图形需要（如 WCG 的几个子项目、Climateprediction）：

	[lib32-pango](https://www.archlinux.org/packages/?name=lib32-pango), [lib32-libxdamage](https://www.archlinux.org/packages/?name=lib32-libxdamage), [lib32-libxi](https://www.archlinux.org/packages/?name=lib32-libxi), [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl), [lib32-libjpeg6](https://aur.archlinux.org/packages/lib32-libjpeg6/) (AUR), [lib32-libxmu](https://www.archlinux.org/packages/?name=lib32-libxmu)

## 疑难解答

### GPU missing

如果出现这样的错误：

 `GPU Missing` 

且 GPU 计算任务无法启动，则应尝试 [重启](/index.php/Daemons_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E9.87.8D.E5.90.AF.E6.9C.8D.E5.8A.A1 "Daemons (简体中文)") `boinc.service` 服务。

这样的错误通常是因为 BOINC 服务先于 X 启动。

### 笔记本过热，续航时间缩短

如果在笔记本上运行 BOINC，且 CPU 频率管理策略为 ondemand（默认即是），CPU 频率会始终保持在最大值，导致 CPU 过热、续航时间缩短。解决方法是要求内核调整 CPU 频率时忽略 BOINC 任务的影响：

 `# echo 1 >/sys/devices/system/cpu/cpufreq/ondemand/ignore_nice_load` 

创建以下 tmpfiles.d 配置，可实现开机自动设置：

 `/etc/tmpfiles.d/ondemand-ignore-nice.conf`  `w /sys/devices/system/cpu/cpufreq/ondemand/ignore_nice_load - - - - 1` 

### 无法下载 World Community Grid 任务

由于 openssl 的问题，一些用户无法下载 World Community Grid 项目的任务。要解决这一问题，需要对该软件包进行一些修改，然后重新编译。

首先，获取 openssl 的 PKGBUILD，以及打包其他所需文件：

```
$ git clone [git://projects.archlinux.org/svntogit/packages.git](git://projects.archlinux.org/svntogit/packages.git) --single-branch --branch packages/openssl

```

如果你安装了 yaourt，也可以使用如下命令：

```
$ yaourt -G openssl

```

执行完第一个命令后，你会看到一个 ./packages/trunk/ 目录，其中有包括 PKGBUILD 在内的若干文件。该 PKGBUILD 需要修改，正确的可以从[这里](http://pastebin.com/pYcYf4dr)下载。

然后，创建软件软件包：

```
$ makepkg 

```

完成后，会出现一个扩展名为 .pkg.tar.xz 的软件包，安装并重启 BOINC 服务即可：

```
# pacman -U openssl-*.pkg.tar.xz
# systemctl restart boinc

```

大功告成。如果还有问题，请参见[原讨论贴](https://bbs.archlinux.org/viewtopic.php?pid=1160393#p1160393)，发帖请求帮助。

### cc_config.xml 相关配置

cc_config.xml 为BOINC管理器的一个高级配置脚本。通过增加不同的参数，可以达到许多意想不到的效果。

将编辑好的文件复制到 /var/lib/boinc 后，还需更改文件为640权限。

## 相关资源

*   [中国分布式计算总站](http://www.equn.com/)
*   [BOINC 官方网站](http://boinc.berkeley.edu/)
*   [BOINC 项目列表](http://boinc.berkeley.edu/projects.php)
*   [维基百科的介绍](https://en.wikipedia.org/wiki/BOINC "wikipedia:BOINC")