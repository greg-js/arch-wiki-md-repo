**翻译状态：** 本文是英文页面 [Install_from_Existing_Linux](/index.php/Install_from_Existing_Linux "Install from Existing Linux") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-10-16，点击[这里](https://wiki.archlinux.org/index.php?title=Install_from_Existing_Linux&diff=0&oldid=407080)可以查看翻译后英文页面的改动。

本指南给出了从当前 Linux 发行版安装 Arch Linux 所需的准备步骤。 准备完成后的安装参考[Installation guide (简体中文)](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")。

从当前 Linux 发行版安装 Arch Linux 对以下情形有所帮助：

*   远程安装 Arch Linux，如一台（虚拟的）根服务器
*   无需 LiveCD 替换当前 Linux 发行版（参见[#无 LiveCD 替换当前系统](#.E6.97.A0_LiveCD_.E6.9B.BF.E6.8D.A2.E5.BD.93.E5.89.8D.E7.B3.BB.E7.BB.9F)）
*   创建基于 Arch Linux 的新 Linux 发行版或 LiveCD
*   创建 Arch Linux 的 chroot 环境，如可为 Docker 基础容器创建
*   [为无盘机器准备 rootfs-over-NFS](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")

这些准备步骤的目的在于为搭建一个 [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts)（如 `pacstrap` 和 `arch-root`）可运行的环境。 这个目的可通过在当前系统安装 [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) 或搭建基于 Arch Linux-based 的 chroot 环境达成。

若当前发行版为 Arch Linux，可直接安装 [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts)。

**注意:** 本指南要求当前系统能够运行目标 Arch Linux 构架的程序。x86_64 系统可通过 i686-pacman 搭建起32位的 chroot 环境。参见 [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")。但从32位系统搭建64位的环境并不容易。

## Contents

*   [1 从一个主机运行Arch Linux](#.E4.BB.8E.E4.B8.80.E4.B8.AA.E4.B8.BB.E6.9C.BA.E8.BF.90.E8.A1.8CArch_Linux)
    *   [1.1 安装和配置](#.E5.AE.89.E8.A3.85.E5.92.8C.E9.85.8D.E7.BD.AE)
*   [2 从一个主机运行另一个Linux发行版](#.E4.BB.8E.E4.B8.80.E4.B8.AA.E4.B8.BB.E6.9C.BA.E8.BF.90.E8.A1.8C.E5.8F.A6.E4.B8.80.E4.B8.AALinux.E5.8F.91.E8.A1.8C.E7.89.88)
    *   [2.1 创建 chroot](#.E5.88.9B.E5.BB.BA_chroot)
        *   [2.1.1 方法一：使用 Bootstrap 镜像（推荐）](#.E6.96.B9.E6.B3.95.E4.B8.80.EF.BC.9A.E4.BD.BF.E7.94.A8_Bootstrap_.E9.95.9C.E5.83.8F.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)
        *   [2.1.2 方法二：使用 LiveCD 镜像](#.E6.96.B9.E6.B3.95.E4.BA.8C.EF.BC.9A.E4.BD.BF.E7.94.A8_LiveCD_.E9.95.9C.E5.83.8F)
    *   [2.2 使用 chroot 环境](#.E4.BD.BF.E7.94.A8_chroot_.E7.8E.AF.E5.A2.83)
        *   [2.2.1 初始化 pacman 密匙环](#.E5.88.9D.E5.A7.8B.E5.8C.96_pacman_.E5.AF.86.E5.8C.99.E7.8E.AF)
        *   [2.2.2 选择镜像和下载基本工具](#.E9.80.89.E6.8B.A9.E9.95.9C.E5.83.8F.E5.92.8C.E4.B8.8B.E8.BD.BD.E5.9F.BA.E6.9C.AC.E5.B7.A5.E5.85.B7)
        *   [2.2.3 安装提示](#.E5.AE.89.E8.A3.85.E6.8F.90.E7.A4.BA)
            *   [2.2.3.1 基于 Debian 的当前系统](#.E5.9F.BA.E4.BA.8E_Debian_.E7.9A.84.E5.BD.93.E5.89.8D.E7.B3.BB.E7.BB.9F)
                *   [2.2.3.1.1 /dev/shm](#.2Fdev.2Fshm)
                *   [2.2.3.1.2 /dev/pts](#.2Fdev.2Fpts)
                *   [2.2.3.1.3 lvmetad](#lvmetad)
            *   [2.2.3.2 基于Fedora的当前系统](#.E5.9F.BA.E4.BA.8EFedora.E7.9A.84.E5.BD.93.E5.89.8D.E7.B3.BB.E7.BB.9F)
*   [3 无 LiveCD 替换当前系统](#.E6.97.A0_LiveCD_.E6.9B.BF.E6.8D.A2.E5.BD.93.E5.89.8D.E7.B3.BB.E7.BB.9F)
    *   [3.1 配置系统](#.E9.85.8D.E7.BD.AE.E7.B3.BB.E7.BB.9F)

## 从一个主机运行Arch Linux

安装 [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) 通过 [official repositories](/index.php/Official_repositories "Official repositories").

### 安装和配置

参考 [Installation guide#Mount the partitions](/index.php/Installation_guide#Mount_the_partitions "Installation guide")。如果 `/mnt`文件夹已经被占用 , 只要新建一个文件夹，比如 `/mnt/install`用来替代即可。

然后参考 [Installation guide#Installation](/index.php/Installation_guide#Installation "Installation guide")。你可以跳过 [Installation guide#Select the mirrors](/index.php/Installation_guide#Select_the_mirrors "Installation guide")，因为主机中应该已经有了合适的镜像列表。

**注意:** 如果你只想创建当前已经存在的Arch系统的备份, 可能只需要复制文件系统到新分区即可。但是你仍然需要做如下操作：

*   创建 [`/etc/fstab`](/index.php/Installation_guide#Fstab "Installation guide") 并编辑 `/etc/hostname`；
*   删除 `/etc/machine-id` ，这样在系统启动时将生成一个全新的、独一无二的matchine-id；
*   对安装媒介做其它相关更改；
*   安装 bootloader。

当复制文件系统根目录时, 使用比如`cp -ax` 或 `rsync -axX`来操作. 这可以避免复制挂载点的内容 (`-x`), 并且保护[capabilities](/index.php/Capabilities "Capabilities") 一些系统二进制文件的属性 (`rsync -X`).

## 从一个主机运行另一个Linux发行版

下列是多个可以自动处理大量步骤的工具。具体方法可以参考他们各自主页的相关说明。

*   [arch-bootstrap](https://github.com/tokland/arch-bootstrap) (Bash)
*   [image-bootstrap](https://github.com/hartwork/image-bootstrap) (Python)
*   [vps2arch](https://github.com/drizzt/vps2arch) (Bash)
*   [archcx](https://github.com/m4rienf/ArchCX) (Bash, from Hetzner CX Rescue System)

以下是介绍手动处理的办法。具体思路是在主机系统中运行Arch系统，并且是在Arch系统中进行的实际安装。这个嵌套系统是位于chroot中。

### 创建 chroot

以下是两个创建并进入chroot的方法，从最简单到最复杂。二者选其一，然后参考[#Using the chroot environment](#Using_the_chroot_environment).

#### 方法一：使用 Bootstrap 镜像（推荐）

从[镜像站](https://www.archlinux.org/download)下载 bootstrap 镜像：

```
 $ curl -O [http://mirror.bjtu.edu.cn/archlinux/iso/2015.10.01/archlinux-bootstrap-2015.10.01-x86_64.tar.gz](http://mirror.bjtu.edu.cn/archlinux/iso/2015.10.01/archlinux-bootstrap-2015.10.01-x86_64.tar.gz)

```

解压 tarball：

```
 # cd /tmp
 # tar xzf <path-to-bootstrap-image>/archlinux-bootstrap-2015.10.01-x86_64.tar.gz

```

选择软件仓库服务器：

```
 # nano /tmp/root.x86_64/etc/pacman.d/mirrorlist

```

**注意:** 从 x86_64 系统通过 bootstrap 引导 i686 镜像，须编辑 `/tmp/root.i686/etc/pacman.conf` 并设置 `Architecture = i686` 以便 pacman 获取 i686 的软件包。

进入 chroot

*   若安装了4或更高版本的 bash：

```
  # /tmp/root.x86_64/bin/arch-chroot /tmp/root.x86_64/

```

*   若无，执行：

```
  # cd /tmp/root.x86_64
  # cp /etc/resolv.conf etc
  # mount --rbind /proc proc
  # mount --rbind /sys sys
  # mount --rbind /dev dev
  # mount --rbind /run run
    （假设 /run 存在）
  # chroot /tmp/root.x86_64 /bin/bash

```

#### 方法二：使用 LiveCD 镜像

挂载最新的 Arch Linux 安装介质并 chroot 是可能的。这种方法为当前系统提供了可运作的 Arch Linux 安装程序而无需另外准备。

**注意:** 开始前，确保最近版本的 [squashfs](http://squashfs.sourceforge.net/) 已安装。否则会出现诸如 `FATAL ERROR aborting: uncompress_inode_table: failed to read block`的错误信息。

*   依据构架的不同，根镜像能在[镜像站](https://www.archlinux.org/download)的 arch/x86_64/ 或 arch/i686/ 目录下找到。squashfs 格式无法编辑，因此需要解压出根镜像并挂载。

*   解压，运行

 `# unsquashfs -d /squashfs-root root-image.fs.sfs` 

*   以 loop 挂载根镜像

```
# mkdir /arch
# mount -o loop /squashfs-root/root-image.fs /arch

```

*   [chroot](/index.php/Change_root "Change root") 前需设置些挂载点并为网络连接复制 resolv.conf。

```
# mount -t proc none /arch/proc
# mount -t sysfs none /arch/sys
# mount -o bind /dev /arch/dev
# mount -o bind /dev/pts /arch/dev/pts # pacman 所需（用于签名检查）
# cp -L /etc/resolv.conf /arch/etc # 网络连接所需

```

*   准备完毕，chroot 入新系统

 `# chroot /arch bash` 

### 使用 chroot 环境

#### 初始化 pacman 密匙环

开始安装前，需要设置 pacman 密匙。执行以下命令前请阅读[Pacman-key (简体中文)#初始化密钥环](/index.php/Pacman-key_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.9D.E5.A7.8B.E5.8C.96.E5.AF.86.E9.92.A5.E7.8E.AF "Pacman-key (简体中文)")以理解其对熵的要求：

```
# pacman-key --init
# pacman-key --populate archlinux

```

#### 选择镜像和下载基本工具

After [selecting a mirror](/index.php/Mirrors#Enabling_a_specific_mirror "Mirrors"), [refresh the package lists](/index.php/Mirrors#Force_pacman_to_refresh_the_package_lists "Mirrors") and [install](/index.php/Install "Install") what you need: [base](https://www.archlinux.org/groups/x86_64/base/), [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), [parted](https://www.archlinux.org/packages/?name=parted) etc.

#### 安装提示

请按照[Installation guide (简体中文)](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")中的[挂载分区](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Mount_the_partitions "Installation guide (简体中文)")和[安装基本系统](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Install_the_base_system "Installation guide (简体中文)")小节进行安装。

##### 基于 Debian 的当前系统

###### /dev/shm

在基于 Debian 的当前系统上，`pacstrap` 会发生以下错误：

```
# pacstrap /mnt base
# ==> Creating install root at /mnt
# mount: mount point /mnt/dev/shm is a symbolic link to nowhere
# ==> ERROR: failed to setup API filesystems in new root

```

Debian 中，/dev/shm 指向 /run/shm。而在基于 Arch 的 chroot 中，/run/shm 并不存在，因而链接失效。创建 /run/shm 目录可修复此错误：

```
# mkdir /run/shm

```

###### /dev/pts

While installing `archlinux-2015.07.01-x86_64` from a Debian 7 host, the following error prevented both [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) and [arch-chroot](/index.php/Change_root#Using_arch-chroot "Change root") from working:

 `# pacstrap -i /mnt` 
```
mount: mount point /mnt/dev/pts does not exist
==> ERROR: failed to setup chroot /mnt

```

Apparently, this is because these two scripts use a common function. `chroot_setup()`[[1]](https://projects.archlinux.org/arch-install-scripts.git/tree/common#n76) relies on newer features of [util-linux](https://www.archlinux.org/packages/?name=util-linux), which are incompatible with Debian 7 userland (see [FS#45737](https://bugs.archlinux.org/task/45737)).

The solution for *pacstrap* is to manually execute its [various tasks](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in#n77), but use the [regular procedure](/index.php/Change_root#Using_chroot "Change root") to mount the kernel filesystems on the target directory (`"$newroot"`):

```
# newroot=/mnt
# mkdir -m 0755 -p "$newroot"/var/{cache/pacman/pkg,lib/pacman,log} "$newroot"/{dev,run,etc}
# mkdir -m 1777 -p "$newroot"/tmp
# mkdir -m 0555 -p "$newroot"/{sys,proc}
# mount -t proc /proc "$newroot/proc"
# mount --rbind /sys "$newroot/sys"
# mount --rbind /run "$newroot/run"
# mount --rbind /dev "$newroot/dev"
# pacman -r "$newroot" --cachedir="$newroot/var/cache/pacman/pkg" -Sy base base-devel ... ## add the packages you want
# cp -a /etc/pacman.d/gnupg "$newroot/etc/pacman.d/"       ## copy keyring
# cp -a /etc/pacman.d/mirrorlist "$newroot/etc/pacman.d/"  ## copy mirrorlist
```

Instead of using `arch-chroot` for [Installation guide#Chroot](/index.php/Installation_guide#Chroot "Installation guide"), simply use `chroot "$newroot"`.

###### lvmetad

Trying to create [LVM](/index.php/LVM "LVM") [logical volumes](/index.php/LVM#Logical_volumes "LVM") from an `archlinux-bootstrap-2015.07.01-x86_64` environment on a Debian 7 host resulted in the following error:

 `# lvcreate -L 20G lvm -n root` 
```
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /dev/lvm/root: not found: device not cleared
  Aborting. Failed to wipe start of new LV.
```

(Physical volume and volume group creation worked despite `/run/lvm/lvmetad.socket: connect failed: No such file or directory` being displayed.)

This could be easily worked around by creating the logical volumes outside the chroot (from the Debian host). They are then available once chrooted again.

Also, if the system you are using has lvm, you might have the following output:

 `# grub-install --target=i386-pc --recheck /dev/mapper/main-archroot` 
```
Installing for i386-pc platform.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
```

This is because debian does not use lvmetad by default. You need to edit `/etc/lvm/lvm.conf` and set `use_lvmetad` to `0`:

```
use_lvmetad = 0

```

This will trigger later an error on boot in the initrd stage. Therefore, you have to change it back after the grub generation. In a software RAID + LVM, steps would be the following:

*   After installing all the system, when you have to do all the initramfs (mkinitcpio) and grub thing.
*   Change /etc/mdadm.conf to reflect your RAID config (if any)
*   Change HOOKS and MODULES according to lvm and raid requirements: `MODULES="dm_mod" HOOKS="base udev **mdadm_udev** ... block **lvm2** filesystems ..."`
*   Generate initrd images with mkinitcpio
*   Change /etc/lvm/lvm.conf to put use_lvmetad = 0
*   Generate grub config (grub-mkconfig)
*   Change /etc/lvm/lvm.conf to put use_lvmetad = 1

##### 基于Fedora的当前系统

On Fedora based hosts and live USBs you may encounter problems when using `genfstab` to generate your [fstab](/index.php/Fstab "Fstab"). Remove duplicate entries and the "seclabel" option where it appears, as this is Fedora-specific and will keep your system from booting normally.

## 无 LiveCD 替换当前系统

在硬盘上划分出 ~650MB 的空闲空间，如分割 swap 分区。若空闲空间小于 600 MB，则须筛选软件包，恰好使系统能在该分区上运行建立网络连接。这意味着需要为 pacstrap 通过选项 -c 指定软件包，以免占满了宝贵的空间。

一旦完成安装，重启进入该系统并[rsync 整个系统](/index.php?title=Full_system_backup_with_rsync_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Full system backup with rsync (简体中文) (page does not exist)")至主分区。 重启前须修改引导器配置。

#### 配置系统

请按照[Installation guide (简体中文)](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")中的[挂载分区](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Mount_the_partitions "Installation guide (简体中文)")及余下小节完成配置。