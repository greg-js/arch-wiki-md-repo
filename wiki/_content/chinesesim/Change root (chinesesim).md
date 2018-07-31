**翻译状态：** 本文是英文页面 [Change_Root](/index.php/Change_Root "Change Root") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-12-12，点击[这里](https://wiki.archlinux.org/index.php?title=Change_Root&diff=0&oldid=485038)可以查看翻译后英文页面的改动。

[Chroot](https://en.wikipedia.org/wiki/Chroot "wikipedia:Chroot") 就是变更当前进程及其子进程的可见根路径。变更后，程序无法访问可见根目录外文件和命令。这个目录叫作 *chroot jail*。

## Contents

*   [1 原因](#.E5.8E.9F.E5.9B.A0)
*   [2 必要条件](#.E5.BF.85.E8.A6.81.E6.9D.A1.E4.BB.B6)
*   [3 用法](#.E7.94.A8.E6.B3.95)
    *   [3.1 使用 arch-chroot](#.E4.BD.BF.E7.94.A8_arch-chroot)
        *   [3.1.1 运行一个命令并退出](#.E8.BF.90.E8.A1.8C.E4.B8.80.E4.B8.AA.E5.91.BD.E4.BB.A4.E5.B9.B6.E9.80.80.E5.87.BA)
    *   [3.2 使用 chroot](#.E4.BD.BF.E7.94.A8_chroot)
*   [4 在 chroot 中运行图形程序](#.E5.9C.A8_chroot_.E4.B8.AD.E8.BF.90.E8.A1.8C.E5.9B.BE.E5.BD.A2.E7.A8.8B.E5.BA.8F)
*   [5 不使用 root 权限](#.E4.B8.8D.E4.BD.BF.E7.94.A8_root_.E6.9D.83.E9.99.90)
    *   [5.1 PRoot](#PRoot)
    *   [5.2 Fakechroot](#Fakechroot)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 原因

切换根目录通常为了系统维护，例如重装引导程序或者重置遗忘的密码。

*   重新安装 [bootloader](/index.php/Bootloader "Bootloader").
*   重建 [initramfs 镜像](/index.php/Mkinitcpio "Mkinitcpio").
*   更新或 [降级软件包](/index.php/Downgrading_packages "Downgrading packages").
*   重置 [忘记的密码](/index.php/Password_recovery "Password recovery").
*   在干净的 chroot 中构建软件包：[DeveloperWiki:Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot").

参阅 [Wikipedia:Chroot#Limitations](https://en.wikipedia.org/wiki/Chroot#Limitations "wikipedia:Chroot").

## 必要条件

*   root 权限
*   另一个 linux 环境，例如 liveCD、USB 闪存介质或者一个已经安装的另一个 linux 发行版。
*   匹配的架构，chroot 前后的环境架构要一致(例如，都是 i686 或 x86_64)。可以用以下命令查看当前环境的架构 `uname -m` 
*   提前加载 chroot 环境需要的内核模块
*   如果需要 swap， chroot 前先启用 swap （`swapon /dev/sdxY`）
*   如果需要网络，chroot 之前先建立好网络连接。

## 用法

**Note:**

*   有些[systemd](/index.php/Systemd "Systemd") 工具无法在 chroot 中运行，例如 *localectl* 和 *timedatectl*，因为这些程序需要可用的 [dbus](/index.php/Dbus "Dbus") 连接. [[1]](https://github.com/systemd/systemd/issues/798#issuecomment-126568596)
*   新的 root (`/`) 所在的文件系统必须是可用访问的状态(提前解密、挂载).

有两种使用 chroot 的方式：

### 使用 arch-chroot

`arch-chroot` bash 脚本是软件包 [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) 的一部分，在运行 `/usr/bin/chroot` 前，这个脚本会挂载 `/proc` api 文件系统，建立可用的 `/etc/resolv.conf`。

进入 chroot

```
# arch-chroot */location/of/new/root*

```

例如在 [安装指南](/index.php/Installation_guide "Installation guide") 中，chroot 到 `/mnt`:

```
# arch-chroot /mnt

```

退出 chroot:

```
# exit

```

#### 运行一个命令并退出

用下面命令在 chroot 中运行一个命令并退出：

```
# arch-chroot */location/of/new/root* *mycommand*

```

例如要在 `/mnt/arch` 中运行 `mkinitcpio -p linux` 并退出:

```
# arch-chroot /mnt/arch mkinitcpio -p linux

```

### 使用 chroot

**警告:** 使用 `--rbind` 选项时，将无法卸载某些 `dev/` 和 `sys/` 的子目录，用 `umount -l` 卸载将会破坏会话并需要重启，所以请尽可能使用 `-o bind`。

作为 root 挂载 api 文件系统：

```
# cd */location/of/new/root*
# mount -t proc proc proc/
# mount --rbind /sys sys/
# mount --rbind /dev dev/

```

可选挂载:

```
# mount --rbind /run run/

```

如果已经建立了一个网络连接并且想在 chroot 环境中继续使用，将 DNS 服务器配置复制到新环境：

```
# cp -L /etc/resolv.conf etc/resolv.conf

```

chroot 到新环境中并启用指定 shell

```
# chroot /mnt/arch /usr/bin/bash

```

**Note:**

*   如果遇到错误 `chroot: cannot run command '/bin/bash': Exec format error`，很可能两个环境架构不匹配。
*   如果遇到错误 `chroot: '/usr/bin/bash': permission denied`,用执行权限重新挂载: `mount -o remount,exec /mnt/arch`。

（可选）加载 Bash 配置文件(`~/.bashrc` 和 `/etc/bash.bashrc`)，运行：

```
# source ~/.bashrc
# source /etc/profile

```

或创建一个独特的提示符来区别你的chroot环境：

```
# export PS1="(chroot) $PS1"

```

退出 chroot 环境：

```
# exit

```

然后卸载临时文件系统:

```
# cd /
# umount --recursive */location/of/new/root*

```

如果出现 `/mnt`(或其它任何分区) is busy, 这可能意味着：

*   chroot环境中残留了一个运行的程序或者还有分区没有被卸载，退出程序并用 `mount` 查找未卸载的分区。
*   如果你仍然不能卸载分区，使用`--force`选项： `# umount -f /mnt` ， 或使用 `umount --lazy` 直接释放挂载。这是，请立即重启系统以避免不一致的状态导致冲突。

## 在 chroot 中运行图形程序

如果系统上运行了[X](/index.php/X "X")，可以在 chroot 环境启动图形应用。

为了chroot环境能连接到你的X服务器，在X服务器中打开一个终端(例如，在用户当前登录的桌面中)，然后运行如下命令给任何人连接到用户X服务器的权限：

```
$ xhost +local

```

然后，从chroot环境中将应用指向你的X服务器，将chroot中的DISPLAY环境变量设定成和拥有X服务器的用户DISPLAY变量相匹配。例如，运行：

```
$ echo $DISPLAY

```

作为拥有X服务器的用户查看DISPLAY的值。如果是“:0”(例如是)，然后在chroot环境中运行

```
# export DISPLAY=:0

```

现在就可以从chroot命令行启动图形界面应用

## 不使用 root 权限

Chroot 需要 root 权限，有时用户并没有这个权限，下面工具可用实现类似的功能：

### PRoot

[PRoot](/index.php/PRoot "PRoot") 可用在没有 root 权限的情况下，用 `mount --bind` 设置可见根目录，这样可用为不同的 CPU 架构编译程序。这个程序的缺点是文件属于主机系统。可用用 `--root-id` 选项解决一部分问题。

### Fakechroot

[fakechroot](https://www.archlinux.org/packages/?name=fakechroot) 是一个拦截 chroot 调用并伪造结果的程序。用 [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) 可用为普通用户伪造一个 chroot 环境：

```
# fakechroot fakeroot chroot ~/my-chroot bash

```

## 参阅

*   [Chroot 基础](https://help.ubuntu.com/community/BasicChroot)