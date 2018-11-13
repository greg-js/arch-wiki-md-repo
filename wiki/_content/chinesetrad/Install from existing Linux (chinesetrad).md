這份指南試圖結合這個Wiki上已存在且相似的三篇不同安裝指南。 也寫給對想在其它運作中的Linux平台(LiveCD或是已安裝的不同發行版)上安裝Arch Linux的任何使用者。

## Contents

*   [1 總覽](#總覽)
*   [2 設定 host 系統](#設定_host_系統)
    *   [2.1 取得必要的軟體包](#取得必要的軟體包)
    *   [2.2 安裝必要檔案到 host 系統](#安裝必要檔案到_host_系統)
    *   [2.3 設罝 host 系統組態](#設罝_host_系統組態)
*   [3 設定 target 系統](#設定_target_系統)
    *   [3.1 準備分割給 Arch 使用](#準備分割給_Arch_使用)
    *   [3.2 安裝 core](#安裝_core)
    *   [3.3 準備 /dev nodes](#準備_/dev_nodes)
    *   [3.4 Chroot](#Chroot)
    *   [3.5 安裝剩餘部分](#安裝剩餘部分)
    *   [3.6 設罝 target 系統組態](#設罝_target_系統組態)
    *   [3.7 設定 Grub](#設定_Grub)
    *   [3.8 Finishing touches](#Finishing_touches)
*   [4 疑難排除](#疑難排除)
    *   [4.1 Kernel Panic](#Kernel_Panic)
    *   [4.2 Root device '/dev/sd??' 不存在](#Root_device_'/dev/sd??'_不存在)
*   [5 另一個方法: 用 Arch 映像檔從已有的 Linux 安裝](#另一個方法:_用_Arch_映像檔從已有的_Linux_安裝)
    *   [5.1 Preparing the Installation Environment](#Preparing_the_Installation_Environment)
    *   [5.2 Install from New Environment](#Install_from_New_Environment)
    *   [5.3 Update and Install packages from host system via chroot](#Update_and_Install_packages_from_host_system_via_chroot)

## 總覽

Arch Linux 的 [pacman](/index.php/Pacman "Pacman") 可指定(-r)任何你想要的目錄作為"根目錄(root)"完成安裝操作。 這對在另一個發行版的LiveCD或已有的系統上從頭開始建罝一個新的Arch Linux系統很有幫助。 It's also useful for creating new chroot environments on a "host" system, maintaining a "golden-master" for development & distribution, or other fun topics like rootfs-over-NFS for diskless machines.

以x86_64 host來說，它甚至有可能用i686-pacman建罝出32-bit的chroot環境。請參閱 [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")。

Throughout this guide, we will refer to partitions as /dev/sdxx. This refers to whatever dev entry you have on your system for the partition in question. The convention is: Drive 1, Partition 1: /dev/sda1 Drive 1, Partition 2: /dev/sda2 Drive 2, Partition 1: /dev/sdb1 etc...

We will refer to it as /dev/sdxx whenever possible.

如果你在安裝過程中有寬頻連線可用，而且只想作basic install，[UNetBootin](http://unetbootin.sourceforge.net/) 可能會是值得一看的容易解答。 (還有 [discussed here](/index.php/Putting_installation_media_on_a_USB_key#UNetBootin "Putting installation media on a USB key").)

In this article, "host" refers to the computer which is used to perform the installation, and "target" refers to the computer where you want to install Arch. These may be one and the same computer. The host does not need to be an Arch system -- it can be a Debian or Redhat system. The section entitled "Setup the host system" explains how to install pacman on the host. The following section entitle "Setup the target system" explains how to use pacman from the host system to install Arch on the target system. Therefore if the host system is already running Arch, you can skip to "Setup the target system".

## 設定 host 系統

你需要安裝archlinux軟體包管理程式[pacman](/index.php/Pacman "Pacman")到你的 host linux 環境。 另外你也會需要一份pacman映像站台清單，用來下載軟體包和它們自己的資料。

### 取得必要的軟體包

You need to get the required packages for your host linux environment. The examples given here assume you are using a i686 environment. **If you are running on an 64bit linux instead you should replace each occurance of "i686" with "x86_64".**

All version numbers given here may change. Please check the version numbers the packages are at first and note them down. The version numbers can be found [here for pacman](https://www.archlinux.org/packages/core/i686/pacman/) and [here for pacman-mirrorlist](https://www.archlinux.org/packages/core/i686/pacman-mirrorlist/). Once you are sure of the version numbers download the required packages:

```
mkdir /tmp/archlinux
cd /tmp/archlinux
wget [ftp://ftp.archlinux.org/core/os/i686/pacman-\*.pkg.tar.gz](ftp://ftp.archlinux.org/core/os/i686/pacman-\*.pkg.tar.gz)
tar xzvf pacman-*.pkg.tar.gz

```

### 安裝必要檔案到 host 系統

If you do not mind littering your install host, you can extract all the downloaded tar balls into your root directory by running as root:

```
cd /
for f in /tmp/archlinux/pacman-*pkg.tar.gz
  tar xzf $f
done

```

1.  If installing from Ubuntu 9.10's LiveCD (perhaps other versions), you will need more than just the pacman files (shared libs) to use pacman at all. Use Lucky's script described in [this thread](https://bbs.archlinux.org/viewtopic.php?pid=759166) to get/install them for you!

2.  Alternatively, you can instead turn these tarballs into packages for your distribution with the [alien](http://kitenet.net/~joey/code/alien/) tool. See the man page of the tool for instructions. The packages created that way may be installed into your host distribution using the usual package management tools available there. This approach offers the best integration into the host linux environment. For a debian package based system this is done with the following commands:
    ```
    cd /tmp/archlinux
    alien -d pacman-3.3.3-1-i686.pkg.tar.gz
    alien -d pacman-mirrorlist-20101223-1-any.pkg.tar.gz

    ```

    RPM based systems will need to replace the parameter "-d" with "-r".

    These distribution packages can then get installed using the normal package management tools of the host linux environment.

3.  Under Fedora 12, I wasn't able to install pacman with any of the other methods, but with the nice script at [https://bbs.archlinux.org/viewtopic.php?pid=734336#p734336](https://bbs.archlinux.org/viewtopic.php?pid=734336#p734336) it will download and install it for you. Worked wonderfully for me.

4.  On [Gentoo](http://gentoo.org/): First Install the [sunrise overlay](http://overlays.gentoo.org/proj/sunrise/). Then unmask pacman by adding <tt>sys-apps/pacman</tt> to <tt>/etc/portage/package.keywords</tt>. Now just run <tt>emerge -av pacman</tt>.

    There is also a [more detailed tutorial](http://ohnopub.net/~ohnobinki/gentoo/arch/).

5.  An older method is [discussed here](/index.php?title=Quick_Custom_Installation&action=edit&redlink=1 "Quick Custom Installation (page does not exist)").

### 設罝 host 系統組態

Configure your /etc/pacman.conf to your liking, and remove unnecessary mirrors from /etc/pacman.d/mirrorlist. Also, enabling at least a few mirrors might become necessary, as you may experience errors during syncing if you have no mirror set. You may want to manually resolve DNS in the /etc/pacman.d/mirrorlist, because pacman for i686 may not be able to get address information on x86_64 systems.

If you're installing from a LiveCD, and you have a system with a low amount of combined RAM and swap (< 1 GB), be sure to set the cachedir in /etc/pacman.conf to be in the new Arch partition (e.g. `/newarch/var/cache/pacman/pkg`). Otherwise you could exhaust memory between the overhead of the existing distro and downloading necessary packages to install.

## 設定 target 系統

### 準備分割給 Arch 使用

You don't *have to* install Arch on a separate partition. You could instead build up a root filesystem in a normal directory, and then create a master tarball from it, or transfer it across the network.

However, most users will want to be installing Arch onto its own partition.

Prepare any partitions and filesystems you need for your installation. If your host system has any gui tools for this, such as gparted, cfdisk, or mandrakes diskdrake, feel free to use them.

To format a partition as ext3, you run (where /dev/sdxx is the partition you want to setup):

```
# mkfs.ext3 /dev/sdxx 

```

To format it as ext3 with journaling and dir_index:

```
# mkfs.ext3 -j -O dir_index /dev/sdxx 

```

To format it as reiserfs:

```
# mkreiserfs /dev/sdxx 

```

To format a partition as swap, and to start using it:

```
# mkswap /dev/sdxx 
# swapon /dev/sdxx

```

Most other filesystems can be setup with their own mkfs variant, take a look with tab completion. Available filesystems depend entirely on your host system.

Once you have your filesystems setup, mount them. Throughout this guide, we will refer to the new Arch root directory as /newarch, however you can put it wherever you like.

```
# mkdir /newarch 
# mount /dev/sdxx /newarch

```

### 安裝 core

Update pacman. You may have to create the `/newarch/var/lib/pacman` folder for it to work (see "Setup the host system" above):

```
# mkdir -p /newarch/var/lib/pacman 
# pacman -Sy -r /newarch

```

Install the 'base' group of packages:

```
# pacman -S base -r /newarch

```

**NOTE:** The -r parameter doesn't change the location of Pacman's cache directory. If you don't want Pacman's cache to be created in your host distro, supply another location with --cachedir, or modify pacman.conf as described [above](#Configure_the_host_system).

### 準備 /dev nodes

First, ensure the correct /dev nodes have been made for udev:

```
ls -alF /newarch/dev

```

This result in a list containing lines similar to the following (the dates will differ for you):

```
crw-------  1 root root 5, 1 2008-12-27 21:40 console
crw-rw-rw-  1 root root 1, 3 2008-12-27 21:42 null
crw-rw-rw-  1 root root 1, 5 2008-12-27 21:40 zero

```

Delete and recreate any device which has a different set of permissions (the crw-... stuff plus the two root entries) and major/minor numbers (the two before the date).

```
cd /newarch/dev 
rm console ; mknod -m 600 console c 5 1 
rm null ; mknod -m 666 null c 1 3 
rm zero ; mknod -m 666 zero c 1 5

```

All device nodes should have been created for you already with the right permissions and you should not need to recreate any of them.

### Chroot

Now we will [chroot into the new Arch system](/index.php/Change_root "Change root").

In order for DNS to work properly you need to edit `/newarch/etc/resolv.conf` or replace it with the resolv.conf from your running distribution

```
cp /etc/resolv.conf /newarch/etc/ 

```

Also, you need to copy a correctly setup mirrorlist into the new system:

```
cp /etc/pacman.d/mirrorlist /newarch/etc/pacman.d

```

Mount various filesystems into the new Arch system:

```
mount -t proc proc /newarch/proc
mount -t sysfs sys /newarch/sys
mount -o bind /dev /newarch/dev

```

If you have a separate `/boot` partition, you'll probably need to mount that too. See [Change root](/index.php/Change_root "Change root") for more details.

When everything is prepared, chroot into the new filesystem:

```
chroot /newarch /bin/bash

```

### 安裝剩餘部分

Install your preferred kernel, and any other packages you may wish to install. For the default kernel (which is already installed!):

```
pacman -S linux

```

If you wish to install extra packages now, you may do so with:

```
pacman -S packagename

```

### 設罝 target 系統組態

Edit your `/etc/fstab`, remembering to add /, swap and any other partitions you may wish to use.

Edit your `/etc/rc.conf`, `/etc/hosts` and `/etc/mkinitcpio.conf` to your needs. Then rebuild your initcpio image:

```
mkinitcpio -p linux

```

Edit `/etc/locale.gen`, uncommenting any locales you wish to have available, and build the locales:

```
locale-gen

```

### 設定 Grub

To use [GRUB](/index.php/GRUB "GRUB") when chrooted, you need to ensure that `/etc/mtab` is up-to-date:

```
grep -v rootfs /proc/mounts > /etc/mtab  

```

You can now run:

```
grub-install /dev/sdx

```

If grub-install fails, you can manually install:

```
grub 
grub> find /boot/grub/stage1     (You should see some results here if you have done everything right so far.   If not, back up and retrace your steps.)
grub> root (hd0,X) 
grub> setup (hd0) 
grub> quit 

```

Double-check your `/boot/grub/menu.lst`. Depending on the host, it could need correcting from hda to sda, and a prefix of /boot as well in the paths.

Detailed instructions for [GRUB](/index.php/GRUB "GRUB") and [LILO](/index.php/LILO "LILO") are available elsewhere on this wiki.

### Finishing touches

[Exit your chroot](/index.php/Change_root#Cleaning_up "Change root"):

```
  exit
  umount /newarch/boot   # if you mounted this or any other separate partitions
  umount /newarch/{proc,sys,dev}
  umount /newarch

```

Reboot to your new Arch system!

## 疑難排除

### Kernel Panic

如果在重開機到你的新系統時遇到 kernel panic 說 console 打不開：

```
kinit: couldn't open console, no such file... 

```

這表示你沒有跟著前面的步驟做。在開頭準備的地方照著步驟來產生basic device nodes。

### Root device '/dev/sd??' 不存在

If when you reboot into your new system you get a error messages like this:

```
Root device '/dev/sda1' doesn't exist, attempting to create it... etc. 

```

This means the drives are showing up as "hda1" instead of "sda1" In which case change your GRUB or LILO settings to use "hd??" or try the following.

Edit /etc/mkinitcpio.conf and change "ide" to "pata" in the "HOOKS=" line. Then regenerate your initrd. (Make sure you have chroot'ed into the new system first.)

```
mkinitcpio -p linux

```

If you are using LVM make sure you add "lvm2" in the HOOKS line. Regenerate your initrd as above.

If you're installing to a device that needs PATA hook make sure it's located before autodetect hook in mkinitcpio.conf.

# 另一個方法: 用 Arch 映像檔從已有的 Linux 安裝

### Preparing the Installation Environment

You can grab whatever image from Arch's Download Page and get the content of image by mount loopback:

CD Image:

```
$ mount -o loop archlinux-2009.08-core-i686.iso /mnt/loop

```

with USB Image:

```
$ losetup -f archlinux-2009.08-core-i686.img
$ losetup -fo 32256 /dev/loop0
$ mount /dev/loop0 /mnt/loop

```

and the content of image:

```
$ ls /mnt/loop 
boot  core-pkgs.sqfs  isomounts  lost+found  overlay.sqfs  root-image.sqfs

```

extract the root image:

```
$ cd /mnt
$ unsquashfs loop/root-image.sqfs

```

after this step, you will have a new squashfs-root directory which contain new Arch system.

### Install from New Environment

If you have Core Arch installation media, and want to install the core packages from it, just copy core-pkgs.sqfs to new squashfs-root directory:

```
$ cp loop/core-pkgs.sqfs squashfs-root

```

Now [chroot into the new Arch system](/index.php/Change_root "Change root"):

```
$ mount -t proc proc /mnt/squashfs-root/proc
$ mount -t sysfs sys /mnt/squashfs-root/sys
$ mount -o bind /dev /mnt/squashfs-root/dev 
$ chroot /mnt/squashfs-root /bin/bash

```

Now you're inside the new installation's filesystem. If you're going to use core-pkgs.sqfs, mount it now:

```
$ mkdir -p /src/core/pkg
$ mount -o loop -t squashfs core-pkgs.sqfs /src/core/pkg 

```

At this point, go ahead and launch Arch's aif installer!

```
$ aif -p interactive

```

and you can install Arch as normal (from CD or Internet) with the notice:

*   Your target partition must not using by host system

After installing Arch from chroot's environment, you can remove any squashfs-root directory and exit the chroot:

```
$ umount /src/core/pkg
$ exit
$ umount /mnt/squashfs-root/dev 
$ umount /mnt/squashfs-root/sys 
$ umount /mnt/squashfs-root/proc
$ rm -rf /mnt/squashfs-root

```

### Update and Install packages from host system via chroot

Add an entry to your existing Grub bootloader's menu.lst, or if you installed a new Grub during the Arch installation process, add it to the /boot/grub/menu.lst on your Arch filesystem.

Now either reboot or [chroot](/index.php/Change_root "Change root") into the new Arch's partition to install further packages:

```
$ mkdir /mnt/arch
$ mount /dev/sdxx /mnt/arch
$ mount -t proc proc /mnt/arch/proc
$ mount -t sysfs sys /mnt/arch/sys
$ mount -o bind /dev /mnt/arch/dev 
$ chroot /mnt/arch /bin/bash

```

Update and install new packages:

```
# pacman -Syu

```