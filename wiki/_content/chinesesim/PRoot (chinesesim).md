[PRoot](https://proot-me.github.io)是一个能在用户空间内运行的程序, 功能类似于[chroot](/index.php/Chroot "Chroot"), `mount --bind`和 binfmt_misc , 能让root用户使用备用根目录运行程序, 就像chroot "jail"一样。 PRoot在由于缺少root权限而无法使用chroot的情况下尤其有用。

## 安装

PRoot可以从[proot](https://aur.archlinux.org/packages/proot/)包安装。 *pacstrap*可以在运行*proot*之前用Arch环境初始化目录。

## 用法

安装完成之后, PRoot不需要root权限。 和chroot一样, 你必须为PRoot提供一个新目录作为新的根目录。 如果没有指定程序，PRoot默认将启动`/bin/sh`。 虚拟文件系统不需要手动挂载，因为PRoot会自动处理这个问题。

```
proot -r ~/mychroot/

```

此时，将启动一个shell， `/` 对应于主机上的 `~/chroot/` 文件夹。

可以使用 `-b` 选项明确地绑定变量：

```
proot -b /bin/bash:/bin/sh

```

这使得主机的/bin/bash在来宾的/bin/sh处可用

PRoot在内部使用qemu用户模式模拟器来允许程序在PRoot内运行，即使程序是为主机系统以外的体系结构编译的。

## Security

Like chroot, PRoot provides only filesystem level isolation. Programs inside the PRoot "jail" share the same kernel, hardware, process space, and networking subsystem. chroot and PRoot are not designed to be substitutes for real [virtualization](/index.php/Virtualization "Virtualization") applications, such as hypervisors and paravirtualizers.