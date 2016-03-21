来自 [QEMU 关于页面](http://wiki.qemu.org/Main_Page),

	"Qemu是一个广泛使用的开源计算机仿真器和虚拟机"

当作为仿真器时，可以在一种架构(如PC机)下运行另一种架构(如ARM)下的操作系统和程序。通过动态转化，可以获得很高的运行效率。

当 QEME 作为虚拟机时，可以使用 [xen](/index.php/Xen_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xen (简体中文)") 或 [kvm](/index.php/KVM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KVM (简体中文)") 访问 CPU 的扩展功能([HVM](https://en.wikipedia.org/wiki/Hardware-assisted_virtualization "wikipedia:Hardware-assisted virtualization"))，在主机 CPU 上直接执行虚拟客户端的代码，获得接近于真机的性能表现。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 QEMU 图形前端](#QEMU_.E5.9B.BE.E5.BD.A2.E5.89.8D.E7.AB.AF)
*   [3 创建新虚拟系统](#.E5.88.9B.E5.BB.BA.E6.96.B0.E8.99.9A.E6.8B.9F.E7.B3.BB.E7.BB.9F)
    *   [3.1 创建硬盘镜像](#.E5.88.9B.E5.BB.BA.E7.A1.AC.E7.9B.98.E9.95.9C.E5.83.8F)
        *   [3.1.1 Overlay storage images](#Overlay_storage_images)
        *   [3.1.2 调整镜像大小](#.E8.B0.83.E6.95.B4.E9.95.9C.E5.83.8F.E5.A4.A7.E5.B0.8F)
    *   [3.2 准备安装介质](#.E5.87.86.E5.A4.87.E5.AE.89.E8.A3.85.E4.BB.8B.E8.B4.A8)
*   [4 运行虚拟化的系统](#.E8.BF.90.E8.A1.8C.E8.99.9A.E6.8B.9F.E5.8C.96.E7.9A.84.E7.B3.BB.E7.BB.9F)
    *   [4.1 启用 KVM](#.E5.90.AF.E7.94.A8_KVM)
*   [5 宿主机和虚拟机数据交互](#.E5.AE.BF.E4.B8.BB.E6.9C.BA.E5.92.8C.E8.99.9A.E6.8B.9F.E6.9C.BA.E6.95.B0.E6.8D.AE.E4.BA.A4.E4.BA.92)
    *   [5.1 Samba](#Samba)
    *   [5.2 挂载虚拟硬盘镜像](#.E6.8C.82.E8.BD.BD.E8.99.9A.E6.8B.9F.E7.A1.AC.E7.9B.98.E9.95.9C.E5.83.8F)
    *   [5.3 挂载 qcow2 镜像](#.E6.8C.82.E8.BD.BD_qcow2_.E9.95.9C.E5.83.8F)
    *   [5.4 使用物理分区作为硬盘镜像中的唯一主分区](#.E4.BD.BF.E7.94.A8.E7.89.A9.E7.90.86.E5.88.86.E5.8C.BA.E4.BD.9C.E4.B8.BA.E7.A1.AC.E7.9B.98.E9.95.9C.E5.83.8F.E4.B8.AD.E7.9A.84.E5.94.AF.E4.B8.80.E4.B8.BB.E5.88.86.E5.8C.BA)
*   [6 使用基于内核的虚拟机(KVM)](#.E4.BD.BF.E7.94.A8.E5.9F.BA.E4.BA.8E.E5.86.85.E6.A0.B8.E7.9A.84.E8.99.9A.E6.8B.9F.E6.9C.BA.28KVM.29)
*   [7 网络](#.E7.BD.91.E7.BB.9C)
    *   [7.1 User-mode networking](#User-mode_networking)
    *   [7.2 虚拟拓扑网络](#.E8.99.9A.E6.8B.9F.E6.8B.93.E6.89.91.E7.BD.91.E7.BB.9C)
        *   [7.2.1 Basic idea](#Basic_idea)
        *   [7.2.2 Bridge virtual machines to external network](#Bridge_virtual_machines_to_external_network)
    *   [7.3 桥接网络](#.E6.A1.A5.E6.8E.A5.E7.BD.91.E7.BB.9C)
        *   [7.3.1 简介](#.E7.AE.80.E4.BB.8B)
        *   [7.3.2 准备](#.E5.87.86.E5.A4.87)
        *   [7.3.3 配置](#.E9.85.8D.E7.BD.AE)
        *   [7.3.4 启动](#.E5.90.AF.E5.8A.A8)
*   [8 图形](#.E5.9B.BE.E5.BD.A2)
    *   [8.1 std](#std)
    *   [8.2 vmware](#vmware)
    *   [8.3 Windows 客户机](#Windows_.E5.AE.A2.E6.88.B7.E6.9C.BA)
*   [9 Qemu的前端](#Qemu.E7.9A.84.E5.89.8D.E7.AB.AF)
*   [10 键盘不工作/方向键不工作](#.E9.94.AE.E7.9B.98.E4.B8.8D.E5.B7.A5.E4.BD.9C.2F.E6.96.B9.E5.90.91.E9.94.AE.E4.B8.8D.E5.B7.A5.E4.BD.9C)
*   [11 启动时运行 QEMU 虚拟机](#.E5.90.AF.E5.8A.A8.E6.97.B6.E8.BF.90.E8.A1.8C_QEMU_.E8.99.9A.E6.8B.9F.E6.9C.BA)
*   [12 External links](#External_links)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [qemu](https://www.archlinux.org/packages/?name=qemu)，并根据需要安装下面的可选软件包：

*   [qemu-arch-extra](https://www.archlinux.org/packages/?name=qemu-arch-extra) - 其它架构支持
*   [qemu-block-gluster](https://www.archlinux.org/packages/?name=qemu-block-gluster) - glusterfs block 支持
*   [qemu-block-iscsi](https://www.archlinux.org/packages/?name=qemu-block-iscsi) - iSCSI block 支持
*   [qemu-block-rbd](https://www.archlinux.org/packages/?name=qemu-block-rbd) - RBD block 支持
*   [samba](https://www.archlinux.org/packages/?name=samba) - SMB/CIFS 服务器支持

## QEMU 图形前端

与其他的虚拟方案如 [VirtualBox](/index.php/VirtualBox "VirtualBox") 和 [VMware](/index.php/VMware "VMware")不同, QEMU不提供用户图形界面来管理虚拟机 (除了运行虚拟机时出现的窗口), 也没有提供一种持久保存虚拟机设置方式. 必须每一次在命令行上指定所有运行虚拟机的参数,除非你已经创建了一个自定义的脚本来启动你的虚拟机. 然而，有几种用户图形界面前端的QEMU：

*   [qemu-launcher](https://www.archlinux.org/packages/?name=qemu-launcher)
*   [qtemu](https://www.archlinux.org/packages/?name=qtemu)
*   [aqemu](https://aur.archlinux.org/packages/aqemu/)

[libvirt](/index.php/Libvirt "Libvirt") 也有支持 QEME 的额外前端界面。

## 创建新虚拟系统

### 创建硬盘镜像

**提示:** 在[QEMU Wikibook](https://en.wikibooks.org/wiki/QEMU/Images) QEMU images参见更多信息

硬盘镜像是一个文件，存储虚拟机硬盘上的内容。除非直接从 CD-ROM 或网络引导并且不安装系统到本地，运行 QEMU 时都需要硬盘镜像。

一个硬盘镜像可能是 *raw*镜像, 和客户机器上看到的内容一模一样，主机上占用的空间客户机上的大小一样。这个方式 I/O 效率最高，但是因为客户机器上没使用的空间也被占用，所以有点浪费空间。另外一种方式是*qcow2* 格式，仅当客户系统实际写入内容的时候，才会分配镜像空间。对客户机器来说，硬盘大小是完整大小，但是在主机系统上实际仅占用和很小的空间。使用这种方式会影响效率.

QEMU 提供 `qemu-img`命令创建硬盘镜像.例如创建一个 4 GB *raw* 格式的镜像:

```
$ qemu-img create -f raw *image_file* 4G

```

您可以用 `-f qcow2` 改为创建一个 *qcow2* 磁盘

用 `dd` 或 `fallocate` 也可以创建一个 *raw* 镜像。

**Warning:** 如果硬盘镜像存储在 [Btrfs](/index.php/Btrfs "Btrfs") 系统上，在创建前请考虑禁用 [写时复制](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs")。

#### Overlay storage images

You can create a storage image once (the 'backing' image) and have QEMU keep mutations to this image in an overlay image. This allows you to revert to a previous state of this storage image. You could revert by creating a new overlay image at the time you wish to revert, based on the original backing image.

To create an overlay image, issue a command like:

```
$ qemu-img create -o backing_file=*img1.raw*,backing_fmt=*raw* -f *qcow2* *img1.cow*

```

After that you can run your QEMU VM as usual (see [#Running virtualized system](#Running_virtualized_system)):

```
$ qemu-system-i386 *img1.cow*

```

The backing image will then be left intact and mutations to this storage will be recorded in the overlay image file.

When the path to the backing image changes, repair is required.

**Warning:** The backing image's absolute filesystem path is stored in the (binary) overlay image file. Changing the backing image's path requires some effort.

Make sure that the original backing image's path still leads to this image. If necessary, make a symbolic link at the original path to the new path. Then issue a command like:

```
$ qemu-img rebase -b */new/img1.raw* */new/img1.cow*

```

At your discretion, you may alternatively perform an 'unsafe' rebase where the old path to the backing image is not checked:

```
$ qemu-img rebase -u -b */new/img1.raw* */new/img1.cow*

```

#### 调整镜像大小

**警告:** 调整包含NTFS引导文件系统的镜像将无法启动已安装的操作系统. 完整的解释和解决办法参见 [[1]](http://tjworld.net/wiki/Howto/ResizeQemuDiskImages).

执行 `qemu-img` 带 `resize` 选项调整硬盘驱动镜像的大小.它适用于 *raw* 和 *qcow2*. 例如, 增加镜像 10 GB 大小, 运行:

```
$ qemu-img resize *disk_image* +10G

```

After enlarging the disk image, you must use file system and partitioning tools inside the virtual machine to actually begin using the new space. When shrinking a disk image, you must **first reduce the allocated file systems and partition sizes** using the file system and partitioning tools inside the virtual machine and then shrink the disk image accordingly, otherwise shrinking the disk image will result in data loss!

### 准备安装介质

要将操作系统安装到您的磁盘镜像, 你需要操作系统的安装介质 (例如 光盘, USB设备, 或 ISO 镜像). 安装介质不能被挂载因为 QEMU 直接访问媒体

**Tip:** If using an optical disk, it is a good idea to first dump the media to a file because this both improves performance and does not require you to have direct access to the devices (that is, you can run QEMU as a regular user without having to change access permissions on the media's device file). For example, if the CD-ROM device node is named `/dev/cdrom`, you can dump it to a file with the command: `$ dd if=/dev/cdrom of=*cd_image.iso*` 

## 运行虚拟化的系统

`qemu-system-*` 程序 (例如 `qemu-system-i386` 或 `qemu-system-x86_64`, 取决于客户机架构)用来运行虚拟化的客户机. 用法是:

```
$ qemu-system-i386 *options* *disk_image*

```

所有 `qemu-system-*`的选项是相同的,参见 `qemu(1)` 查看文档和所有选项

默认 QEMU会在窗口中显示虚拟机的视频输出.有一点要记住:当您单击QEMU窗口,鼠标指针被捕获。要放开，按 `Ctrl+Alt`.

**警告:** QEMU 不应以 root 身份运行. If you must launch it in a script as root, you should use the `-runas` option to make QEMU drop root privileges.

### 启用 KVM

KVM 必须要您处理器和内核支持, 和必要的 [kernel modules](/index.php/Kernel_modules "Kernel modules")加载. 更多信息参见 [KVM](/index.php/KVM "KVM").

要在KVM模式中启动QEMU, 追加 `-enable-kvm`到启动选项. To check if KVM is enabled for a running VM, enter the QEMU [Monitor](https://en.wikibooks.org/wiki/QEMU/Monitor) using `Ctrl+Alt+Shift+2`, and type `info kvm`.

**Note:**

*   If you start your VM with a GUI tool and experience very bad performance, you should check for proper KVM support, as QEMU may be falling back to software emulation.
*   KVM needs to be enabled in order to start Windows 7 and Windows 8 properly without a *blue screen*.

## 宿主机和虚拟机数据交互

If you have servers on your host OS they will be accessible with the ip-address 10.0.2.2 without any further configuration. So you could just FTP or SSH, etc to 10.0.2.2 from windows to share data, or if you would like to use [Samba](/index.php/Samba_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Samba (简体中文)"):

### Samba

QEMU supports [Samba](/index.php/Samba "Samba") which allows you to mount host directories during the emulation. It seems that there is an incompatibility with Samba 3.x. and some versions of QEMU. But at least with a current snapshot of QEMU it should be working.

First, you need to have a working Samba installation. Then add the following section to your `smb.conf`:

```
[qemu]
   comment = Temporary file space
   path = /tmp
   read only = no
   public = yes

```

Now start QEMU with:

```
qemu [hd_image] -smb qemu

```

Then you should be able to access your host's Samba server with the IP address 10.0.2.2\. If you are running Win9x as a guest OS, you may need to add

```
10.0.2.2 smbserver

```

to `C:\Windows\lmhosts` (Win9x has Lmhosts.sam as a SAMple, rename it!).

### 挂载虚拟硬盘镜像

Fortunately there is a way to mount the hard disk image with a loopback device. Login as root, make a temporary directory and mount the image with the command:

```
mount -o loop,offset=32256 [[hd''image]] [[tmp''dir]]

```

Now you can copy data in both directions. When you are done, umount with:

```
umount [hd_image]

```

The drawback of this solution is that you cannot use it with qcow images (including overlay images). So you need to create you images without \"-f qcow\" option.

**小贴士:** Create a second, raw hard drive image. This way you will be able to transfer data easily and use qcow overlay images for the primary drive.

**警告:** 挂载时千万不要启动虚拟机!

### 挂载 qcow2 镜像

你可以使用 `qemu-nbd` 挂载 qcow2 镜像. 参见 [Wikipedia:Qcow#Mounting_qcow2_images](https://en.wikipedia.org/wiki/Qcow#Mounting_qcow2_images "wikipedia:Qcow").

### 使用物理分区作为硬盘镜像中的唯一主分区

Sometimes, you may wish to use one of your system partition from within QEMU (for instance, if you wish booting both your real machine or QEMU using a given partition as root). You can do this using software RAID in linear mode (you need the linear.ko kernel driver) and a loopback device: the trick is to dynamically prepend a master boot record (MBR) to the real partition you wish to embed in a QEMU raw disk image.

Suppose you have a plain, unmounted `/dev/hdaN` partition with some filesystem on it you wish to make part of a QEMU disk image. First, you create some small file to hold the MBR:

```
dd if=/dev/zero of=/path/to/mbr count=32

```

Here, a 16 KB (32 * 512 bytes) file is created. It is important not to make it too small (even if the MBR only needs a single 512 bytes block), since the smaller it will be, the smaller the chunk size of the software RAID device will have to be, which could have an impact on performance. Then, you setup a loopback device to the MBR file:

```
losetup -f /path/to/mbr

```

Let's assume the resulting device is `/dev/loop0`, because we would not already have been using other loopbacks. Next step is to create the "merged" MBR + `/dev/hdaN` disk image using software RAID:

```
 modprobe linear
 mdadm --build --verbose /dev/md0 --chunk=16 --level=linear --raid-devices=2 /dev/loop0 /dev/hdaN

```

The resulting `/dev/md0` is what you will use as a QEMU raw disk image (do not forget to set the permissions so that the emulator can access it). The last (and somewhat tricky) step is to set the disk configuration (disk geometry and partitions table) so that the primary partition start point in the MBR matches the one of `/dev/hdaN` inside `/dev/md0` (an offset of exactly 16 * 512 = 16384 bytes in this example). Do this using `fdisk` on the host machine, not in the emulator: the default raw disc detection routine from QEMU often results in non kilobyte-roundable offsets (such as 31.5 KB, as in the previous section) that cannot be managed by the software RAID code. Hence, from the the host:

```
 fdisk /dev/md0

```

Press `X` to enter the expert menu. Set number of 's'ectors per track so that the size of one cylinder matches the size of your MBR file. For two heads and a sector size of 512, the number of sectors per track should be 16, so we get cylinders of size 2x16x512=16k.

Now, press `R` to return to the main menu.

Press `P` and check that the cylinder size is now 16k.

Now, create a single primary partition corresponding to `/dev/hdaN`. It should start at cylinder 2 and end at the end of the disk (note that the number of cylinders now differs from what it was when you entered fdisk.

Finally, 'w'rite the result to the file: you are done. You know have a partition you can mount directly from your host, as well as part of a QEMU disk image:

```
 qemu -hdc /dev/md0 [...]

```

You can of course safely set any bootloader on this disk image using QEMU, provided the original `/dev/hdaN` partition contains the necessary tools.

## 使用基于内核的虚拟机(KVM)

[KVM](/index.php/KVM "KVM") is a full virtualization solution for Linux on x86 hardware containing virtualization extensions (Intel VT or AMD-V). It consists of a loadable kernel module, kvm.ko, that provides the core virtualization infrastructure and a processor specific module, kvm-intel.ko or kvm-amd.ko. Using KVM, one can run multiple virtual machines running unmodified Linux or Windows images. Each virtual machine has private virtualized hardware: a network card, disk, graphics adapter, etc.

This technology requires an x86 machine running a recent ( >= 2.6.22) Linux kernel on an Intel processor with VT-x (virtualization technology) extensions, or an AMD processor with SVM (Secure Virtual Machine) extensions. It is included in the mainline Linux kernel since 2.6.20 and is enabled by default in the Arch Linux kernel.

Please refer to the [KVM](/index.php/KVM "KVM") page itself, for more information on using QEMU with KVM on Arch Linux.

To take advantage of KVM, you simply need a compatible processor (the following command must return something on the screen):

```
grep -E "(vmx|svm)" --color=always /proc/cpuinfo

```

And load the appropriate module from your `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`.

*   For Intel® processors add `kvm-intel` to your `MODULES` array in `/etc/rc.conf`
*   for AMD® processors add `kvm-amd` to your `MODULES` array in `/etc/rc.conf`

Also, you will need to add yourself to the group `kvm`.

```
gpasswd -a <Your_User_Account> kvm

```

## 网络

### User-mode networking

By default, without any `-netdev` arguments, QEMU will use user-mode networking with a built-in DHCP server. Your virtual machines will be assigned an IP address when they run their DHCP client, and they will be able to access the physical host's network through IP masquerading done by QEMU. This only works with the TCP and UDP protocols, so ICMP, including `ping`, will not work.

This default configuration allows your virtual machines to easily access the Internet, provided that the host is connected to it, but the virtual machines will not be directly visible on the external network, nor will virtual machines be able to talk to each other if you start up more than one concurrently.

QEMU's user-mode networking can offer more capabilities such as built-in TFTP or SMB servers, or attaching guests to virtual LANs so that they can talk to each other. See the QEMU documentation on the `-net user` flag for more details.

However, user-mode networking has limitations in both utility and performance. More advanced network configurations require the use of tap devices or other methods.

### 虚拟拓扑网络

#### Basic idea

[Tap devices](https://en.wikipedia.org/wiki/TUN/TAP "wikipedia:TUN/TAP") are a Linux kernel feature that allows you to create virtual network interfaces that appear as real network interfaces. Packets sent to a "tap" interface are delivered to a userspace program, such as QEMU, that has bound itself to the interface.

QEMU can use tap networking for a virtual machine so that packets sent to the tap interface will be sent to the virtual machine and appear as coming from a network interface (usually an Ethernet interface) in the virtual machine. Conversely, everything that the virtual machine sends through its network interface will appear on the tap interface.

Tap devices are supported by the Linux bridge drivers, so it is possible to bridge together tap devices with each other and possibly with other host interfaces such as eth0\. This is desirable if you want your virtual machines to be able to talk to each other, or if you want other machines on your LAN to be able to talk to the virtual machines.

#### Bridge virtual machines to external network

The following describes how to bridge a virtual machine to a host interface such as eth0, which is probably the most common configuration. This configuration makes it appear that the virtual machine is located directly on the external network, on the same Ethernet segment as the physical host machine.

**Warning:** Beware that since your virtual machines will appear directly on the external network, this may expose them to attack. Depending on what resources your virtual machines have access to, you may need to take all the precautions you normally would take in securing a computer to secure your virtual machines.

We will replace the normal Ethernet adapter with a bridge adapter and bind the normal Ethernet adapter to it. See [http://en.gentoo-wiki.com/wiki/KVM#Networking_2](http://en.gentoo-wiki.com/wiki/KVM#Networking_2) .

*   Make sure that the following package is installed:
    *   [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils) (provides `brctl`, to manipulate bridges)

*   Enable IPv4 forwarding:

```
sysctl net.ipv4.ip_forward=1

```

To make the change permanent, add `net.ipv4.ip_forward = 1` to `/etc/sysctl.d/40-ip-forward.conf`.

*   Load the `tun` module and configure it to be loaded on boot. See [Kernel modules](/index.php/Kernel_modules "Kernel modules") for details.

*   Now create the bridge. See [Bridge with netcfg](/index.php/Bridge_with_netcfg "Bridge with netcfg") for details.

Remember to name your bridge as `br0`, or change the scripts below to your bridge's name.

*   Create the script that QEMU uses to bring up the tap adapter with root:kvm 750 permissions:

 `/etc/qemu-ifup` 
```
#!/bin/sh

echo "Executing /etc/qemu-ifup"
echo "Bringing up $1 for bridged mode..."
sudo /sbin/ip link set $1 up promisc on
echo "Adding $1 to br0..."
sudo /usr/sbin/brctl addif br0 $1
sleep 2

```

*   Create the script that QEMU uses to bring down the tap adapter in `/etc/qemu-ifdown` with root:kvm 750 permissions:

 `/etc/qemu-ifdown` 
```
#!/bin/sh

echo "Executing /etc/qemu-ifdown"
sudo /sbin/ip link set $1 down
sudo /usr/sbin/brctl delif br0 $1
sudo /sbin/ip link delete dev $1

```

*   Use `visudo` to add the following to your `sudoers` file:

```
Cmnd_Alias      QEMU=/sbin/ip,/sbin/modprobe,/usr/sbin/brctl,/usr/bin/tunctl
%kvm     ALL=NOPASSWD: QEMU

```

*   Make sure the user(s) wishing to use this new functionality are in the `kvm` group. Exit and log in again if necessary.

*   You launch QEMU using the following `run-qemu` script:

 `run-qemu` 
```
#!/bin/bash
USERID=`whoami`
IFACE=$(sudo tunctl -b -u $USERID)

# This line creates a random mac address. The downside is the dhcp server will assign a different ip each time
printf -v macaddr "52:54:%02x:%02x:%02x:%02x" $(( $RANDOM & 0xff)) $(( $RANDOM & 0xff )) $(( $RANDOM & 0xff)) $(( $RANDOM & 0xff ))
# Instead, uncomment and edit this line to set an static mac address. The benefit is that the dhcp server will assign the same ip.
# macaddr='52:54:be:36:42:a9'

qemu -net nic,macaddr=$macaddr -net tap,ifname="$IFACE" $*

sudo tunctl -d $IFACE &> /dev/null

```

Then to launch a VM, do something like this

```
$ run-qemu -hda myvm.img -m 512 -vga std

```

*   If you cannot get a DHCP address in the host, it might be because [iptables](/index.php/Iptables "Iptables") are up by default in the bridge. In that case (from [http://www.linux-kvm.org/page/Networking](http://www.linux-kvm.org/page/Networking) ):

```
# cd /proc/sys/net/bridge
# ls
bridge-nf-call-arptables  bridge-nf-call-iptables
bridge-nf-call-ip6tables  bridge-nf-filter-vlan-tagged
# for f in bridge-nf-*; do echo 0 > $f; done

```

And if you still cannot get networking to work, see: [Linux_Containers#Bridge_device_setup](/index.php/Linux_Containers#Bridge_device_setup "Linux Containers").

### 桥接网络

NOTE：这部分由[User:athurg](/index.php/User:Athurg "User:Athurg")根据实际体验过程翻译，和原文的流程有比较大的出入。如果有任何问题，请联系[User:athurg](/index.php/User:Athurg "User:Athurg")。

#### 简介

在QEMU中，桥接网络就是将虚拟机注册到主机的一个单独网络接口上，然后将这个接口和主机对外的网络接口一起桥接起来。如果你需要让虚拟机和外部网络完全互联互通时，就需要这么干了！不过需要提醒的是，这样的话客户机就完全暴露在网络中了。

#### 准备

首先，请确认下面的软件包已经安装了:

```
 bridge-utils (for brctl, to manipulate bridges)
 uml_utilities (for tunctl, to manipulate taps)
 sudo (for manipulating bridges and tunnels as root)

```

接下来加载桥接模块：

```
 # modprobe bridge

```

#### 配置

首先，修改你的网络配置。增加一个桥接网络接口`br0`，用它来取代原来主机上的本地链接。打开`/etc/rc.conf`，将网络配置部分修改如下：

```
 eth0="eth0 up"
 br0="dhcp"      #如果你原来的本地链接是DHCP方式获取配置的话
 #br0="br0 192.168.0.2 netmask 255.255.255.0 up"      #如果你原来的本地链接是静态设置的话
 INTERFACES=(eth0 br0)

```

然后，将原来的网络接口`eth0`绑定到桥接网络接口`br0`上，使得主机上的网络应用能够通过桥接网络接口，传递到外网中。编辑`/etc/conf.d/bridges`：

```
 bridge_br0="eth0"
 BRIDGE_INTERFACES=(br0)

```

加载tap模块

```
 # modprobe tun

```

创建一个`/etc/qemu-ifup`脚本，用于QEMU用来创建和加载虚拟机对外访问的网络接口。

```
 #!/bin/sh

 echo "Executing /etc/qemu-ifup"
 echo "Bringing up $1 for bridged mode..."
 sudo /sbin/ifconfig $1 0.0.0.0 promisc up
 echo "Adding $1 to br0..."
 sudo /usr/sbin/brctl addif br0 $1
 sleep 2

```

这个脚本的属主应该设置为root:kvm，权限为750，以使得kvm组的用户（可以启动虚拟机的用户）也能执行。这里也提醒大家一次，所有需要通过qemu使用KVM虚拟机的用户，都应当加入到kvm组中。

由于这个脚本里需要调用ifconfig等命令来给虚拟机动态增减网络接口，为了方便我们在脚本里通过sudo来执行。如果不想脚本执行过程中向用户索取密码，请编辑`sudo`或者`visudo`的配置文件，加入下面这一行：

```
 Cmnd_Alias      QEMU=/sbin/ifconfig,/sbin/modprobe,/usr/sbin/brctl,/usr/bin/tunctl
 %kvm     ALL=NOPASSWD: QEMU

```

最后，将`bridge`和`tun`加入到文件`/etc/rc.conf`的`MODULES`变量中，以便开机就能加载。

#### 启动

一切配置妥当，我们就可以开始体验了。 启动带桥接模式网络接口的QEMU大致有三个步骤

*   通过tunctl申请一个可用的虚拟网络接口——tap设备。
*   配置这个设备并桥接到桥接网络接口，然后启动qemu
*   退出qemu时，别网络删掉这个虚拟网络接口。

听上去很复杂吧？要是每次启动虚拟机都这么复杂不是很烦？我们可以创建一个脚本来实现：

```
USERID=`whoami`
IFACE=`sudo tunctl -b -u $USERID`

qemu -net nic -net tap,ifname="$IFACE" $*

sudo tunctl -d $IFACE &> /dev/null

```

需要注意一点，由于我们前面创建了`/etc/qemu-ifup`这个脚本，因此我们只需要把申请到的虚拟网络接口名通过-net tap,ifname="网络接口名"告诉qemu，他自己会用这个接口名为参数，调用/etc/qemu-ifup来完成桥接和配置这个网络接口的过程。

## 图形

QEMU 可以使用一下几个图形输出：std, cirrus, vmware, qxl, xenfs 和 vnc。

使用 `vnc` 选项，你可以单独运行客户机，并且通过 VNC 连接。其他选项是使用`std`, `vmware`, `cirrus`:

### std

使用 `-vga std` 你可以得到最高 2560 x 1600 像素的分辨率。

### vmware

尽管有一点怪怪的，但是这种方法确实比 std 和 cirrus 效果好。在客户机中，安装 VMware 驱动：

```
pacman -S xf86-video-vmware xf86-input-vmmouse

```

### Windows 客户机

如果你使用微软 Windows 客户机，你也许想使用远程桌面协议(RDP)连接到客户虚拟机。使用：(如果你使用 VLAN 或与客户机不在同一个网络之中)

```
qemu -nographic -net user,hostfwd=tcp::5555-:3389

```

然后用 rdesktop 或者 freerdp 连接到客户机，例如：

```
xfreerdp -g 2048x1152 localhost:5555 -z -x lan

```

## Qemu的前端

Qemu有几个图形前端，不习惯命令行的可以使用:

*   community/qemu-launcher
*   community/qemulator
*   community/qtemu

## 键盘不工作/方向键不工作

如果你发现一些键不工作或“按下”错误的键(尤其是方向键)，你也许需要在选项中指定你的键盘布局。键盘布局可以在 `/usr/share/qemu/keymaps` 找到。

```
qemu -k [keymap] [disk_image]

```

## 启动时运行 QEMU 虚拟机

想要在启动时运行 QEMU 虚拟机，你可以使用下面的 rc-script 和配置文件.

<caption>配置文件选项</caption>
| QEMU_MACHINES | 要启动的虚拟机列表 |
| qemu_${vm}_type | 调用的 QEMU 二进制文件。如果指定，会被加到 `/usr/bin/qemu-` 之后，这个程序会被使用来启动虚拟机。也就是说，如你可以启动比如 qemu-system-arm 镜像使用 qemu_my_arm_vm_type="system-arm"。如果不指定，`/usr/bin/qemu` 会被使用。 |
| qemu_${vm} | 启动的 QEMU 命令行。默认带有 `-name ${vm} -pidfile /var/run/qemu/${vm}.pid -daemonize -nographic`选项。 |
| qemu_${vm}_haltcmd | 安全关闭虚拟机的命令。我使用 `-monitor telnet:..` 以及通过发送`system_powerdown` 到 monitor，通过 ACPI 关闭我的虚拟机。你可以使用 ssh 或其他方法。 |
| qemu_${vm}_haltcmd_wait | 等待关闭虚拟机的时间。默认是30秒。rc-script 会在这个时间后 kill qemu 进程。 |

配置文件例子：

 `/etc/conf.d/qemu.conf` 
```
# VMs that should be started on boot
# use the ! prefix to disable starting/stopping a VM
QEMU_MACHINES=(vm1 vm2)

# NOTE: following options will be prepended to qemu_${vm}
# -name ${vm} -pidfile /var/run/qemu/${vm}.pid -daemonize -nographic

qemu_vm1_type="system-x86_64"

qemu_vm1="-enable-kvm -m 512 -hda /dev/mapper/vg0-vm1 -net nic,macaddr=DE:AD:BE:EF:E0:00 \
 -net tap,ifname=tap0 -serial telnet:localhost:7000,server,nowait,nodelay \
 -monitor telnet:localhost:7100,server,nowait,nodelay -vnc :0"

qemu_vm1_haltcmd="echo 'system_powerdown' | nc.openbsd localhost 7100" # or netcat/ncat

# You can use other ways to shutdown your VM correctly
#qemu_vm1_haltcmd="ssh powermanager@vm1 sudo poweroff"

# By default rc-script will wait 30 seconds before killing VM. Here you can change this timeout.
#qemu_vm1_haltcmd_wait="30"

qemu_vm2="-enable-kvm -m 512 -hda /srv/kvm/vm2.img -net nic,macaddr=DE:AD:BE:EF:E0:01 \
 -net tap,ifname=tap1 -serial telnet:localhost:7001,server,nowait,nodelay \
 -monitor telnet:localhost:7101,server,nowait,nodelay -vnc :1"

qemu_vm2_haltcmd="echo 'system_powerdown' | nc.openbsd localhost 7101"

```

rc-script:

 `/etc/rc.d/qemu` 
```
#!/bin/bash
. /etc/rc.conf
. /etc/rc.d/functions

[ -f /etc/conf.d/qemu.conf ] && source /etc/conf.d/qemu.conf

PIDDIR=/var/run/qemu
QEMU_DEFAULT_FLAGS='-name ${vm} -pidfile ${PIDDIR}/${vm}.pid -daemonize -nographic'
QEMU_HALTCMD_WAIT=30

case "$1" in
  start)
    [ -d "${PIDDIR}" ] || mkdir -p "${PIDDIR}"
    for vm in "${QEMU_MACHINES[@]}"; do
       if [ "${vm}" = "${vm#!}" ]; then
         stat_busy "Starting QEMU VM: ${vm}"
         eval vm_cmdline="\$qemu_${vm}"
         eval vm_type="\$qemu_${vm}_type"

         if [ -n "${vm_type}" ]; then
           vm_cmd="/usr/bin/qemu-${vm_type}"
         else
           vm_cmd='/usr/bin/qemu'
         fi

         eval "qemu_flags=\"${QEMU_DEFAULT_FLAGS}\""

         ${vm_cmd} ${qemu_flags} ${vm_cmdline} >/dev/null
         if [  $? -gt 0 ]; then
           stat_fail
         else
           stat_done
         fi
       fi
    done
    add_daemon qemu
    ;;

  stop)
    for vm in "${QEMU_MACHINES[@]}"; do
      if [ "${vm}" = "${vm#!}" ]; then
        # check pidfile presence and permissions
        if [ ! -r "${PIDDIR}/${vm}.pid" ]; then
          continue
        fi

        stat_busy "Stopping QEMU VM: ${vm}"

        eval vm_haltcmd="\$qemu_${vm}_haltcmd"
        eval vm_haltcmd_wait="\$qemu_${vm}_haltcmd_wait"
        vm_haltcmd_wait=${vm_haltcmd_wait:-${QEMU_HALTCMD_WAIT}}
        vm_pid=$(cat ${PIDDIR}/${vm}.pid)

        # check process existence
        if ! kill -0 ${vm_pid} 2>/dev/null; then
          stat_done
          rm -f "${PIDDIR}/${vm}.pid"
          continue
        fi

        # Try to shutdown VM safely
        _vm_running='yes'
        if [ -n "${vm_haltcmd}" ]; then
          eval ${vm_haltcmd} >/dev/null

          _w=0
          while [ "${_w}" -lt "${vm_haltcmd_wait}" ]; do
            sleep 1
            if ! kill -0 ${vm_pid} 2>/dev/null; then
              # no such process
              _vm_running=''
              break
            fi
            _w=$((_w + 1))
          done

        else
          # No haltcmd - kill VM unsafely
          _vm_running='yes'
        fi

        if [ -n "${_vm_running}" ]; then
            # kill VM unsafely
            kill ${vm_pid} 2>/dev/null
            sleep 1
        fi

        # report status
        if kill -0 ${vm_pid} 2>/dev/null; then
          # VM is still alive
          #kill -9 ${vm_pid}
          stat_fail
        else
          stat_done
        fi

        # remove pidfile
        rm -f "${PIDDIR}/${vm}.pid"
      fi
    done
    rm_daemon qemu
    ;;

  restart)
    $0 stop
    sleep 1
    $0 start
    ;;

  *)
    echo "usage: $0 {start|stop|restart}"

esac

```

## External links

*   [QEMUMenu for Windows](http://kidsquid.com/cgi-bin/moin.cgi/QEMUMenu).
*   [Network bridging setup for QEMU](http://mychael.gotdns.com/blog/2006/12/14/qemu-setup/)