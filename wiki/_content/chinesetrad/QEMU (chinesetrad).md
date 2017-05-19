來自 [QEMU 的關於頁面](http://wiki.qemu.org/Main_Page),

	"Qemu是一個廣泛使用的開源電腦仿真器和虛擬機"

當作為仿真器时，可以在一种架構(如x86 PC機器)下執行另一種架構(如ARM)下的作業系統和程式。通过動態轉化，可以获得很高的運作效率。

當 QEMU 作為虛擬機器時，可以使用 [KVM](/index.php/KVM_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "KVM (正體中文)") 或 [Xen](/index.php/Xen "Xen") 存取 CPU 的擴充功能([HVM](https://en.wikipedia.org/wiki/Hardware-assisted_virtualization "wikipedia:Hardware-assisted virtualization"))，在主機 CPU 上直接執行虛擬客户端的代碼，获得接近於真實機的性能表現。

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
*   [2 QEMU GUI前端](#QEMU_GUI.E5.89.8D.E7.AB.AF)
*   [3 創建新虛擬系統](#.E5.89.B5.E5.BB.BA.E6.96.B0.E8.99.9B.E6.93.AC.E7.B3.BB.E7.B5.B1)
    *   [3.1 創建硬碟鏡像](#.E5.89.B5.E5.BB.BA.E7.A1.AC.E7.A2.9F.E9.8F.A1.E5.83.8F)
        *   [3.1.1 Overlay storage images](#Overlay_storage_images)
        *   [3.1.2 調整鏡像大小](#.E8.AA.BF.E6.95.B4.E9.8F.A1.E5.83.8F.E5.A4.A7.E5.B0.8F)
    *   [3.2 準備安裝介質](#.E6.BA.96.E5.82.99.E5.AE.89.E8.A3.9D.E4.BB.8B.E8.B3.AA)
*   [4 運行虛擬機](#.E9.81.8B.E8.A1.8C.E8.99.9B.E6.93.AC.E6.A9.9F)
    *   [4.1 啟用 KVM](#.E5.95.9F.E7.94.A8_KVM)
*   [5 宿主機和虛擬機的資料交互](#.E5.AE.BF.E4.B8.BB.E6.A9.9F.E5.92.8C.E8.99.9B.E6.93.AC.E6.A9.9F.E7.9A.84.E8.B3.87.E6.96.99.E4.BA.A4.E4.BA.92)
    *   [5.1 Samba](#Samba)
    *   [5.2 掛載虛擬硬碟鏡像](#.E6.8E.9B.E8.BC.89.E8.99.9B.E6.93.AC.E7.A1.AC.E7.A2.9F.E9.8F.A1.E5.83.8F)
    *   [5.3 掛載 qcow2 鏡像](#.E6.8E.9B.E8.BC.89_qcow2_.E9.8F.A1.E5.83.8F)
    *   [5.4 使用物理分割區作為硬碟鏡像中的唯一主分割區](#.E4.BD.BF.E7.94.A8.E7.89.A9.E7.90.86.E5.88.86.E5.89.B2.E5.8D.80.E4.BD.9C.E7.82.BA.E7.A1.AC.E7.A2.9F.E9.8F.A1.E5.83.8F.E4.B8.AD.E7.9A.84.E5.94.AF.E4.B8.80.E4.B8.BB.E5.88.86.E5.89.B2.E5.8D.80)
*   [6 使用KVM](#.E4.BD.BF.E7.94.A8KVM)
*   [7 網路](#.E7.B6.B2.E8.B7.AF)
    *   [7.1 User-mode networking](#User-mode_networking)
    *   [7.2 虛擬拓補網路](#.E8.99.9B.E6.93.AC.E6.8B.93.E8.A3.9C.E7.B6.B2.E8.B7.AF)
        *   [7.2.1 Basic idea](#Basic_idea)
        *   [7.2.2 Bridge virtual machines to external network](#Bridge_virtual_machines_to_external_network)
    *   [7.3 橋接網路](#.E6.A9.8B.E6.8E.A5.E7.B6.B2.E8.B7.AF)
        *   [7.3.1 簡介](#.E7.B0.A1.E4.BB.8B)
        *   [7.3.2 準備](#.E6.BA.96.E5.82.99)
        *   [7.3.3 配置](#.E9.85.8D.E7.BD.AE)
        *   [7.3.4 啟動](#.E5.95.9F.E5.8B.95)
*   [8 圖形](#.E5.9C.96.E5.BD.A2)
    *   [8.1 std](#std)
    *   [8.2 vmware](#vmware)
    *   [8.3 Windows 客戶機](#Windows_.E5.AE.A2.E6.88.B6.E6.A9.9F)
*   [9 Qemu的前端](#Qemu.E7.9A.84.E5.89.8D.E7.AB.AF)
*   [10 鍵盤不工作/方向鍵不工作](#.E9.8D.B5.E7.9B.A4.E4.B8.8D.E5.B7.A5.E4.BD.9C.2F.E6.96.B9.E5.90.91.E9.8D.B5.E4.B8.8D.E5.B7.A5.E4.BD.9C)
*   [11 開機時執行 QEMU 虛擬機](#.E9.96.8B.E6.A9.9F.E6.99.82.E5.9F.B7.E8.A1.8C_QEMU_.E8.99.9B.E6.93.AC.E6.A9.9F)
*   [12 External links](#External_links)

## 安裝

[安裝](/index.php?title=%E5%AE%89%E8%A3%9D&action=edit&redlink=1 "安裝 (page does not exist)") [qemu](https://www.archlinux.org/packages/?name=qemu)，並根據需要安裝下面的可選軟體包：

*   [qemu-arch-extra](https://www.archlinux.org/packages/?name=qemu-arch-extra) - 其它架構支援
*   [qemu-block-gluster](https://www.archlinux.org/packages/?name=qemu-block-gluster) - glusterfs block 支援
*   [qemu-block-iscsi](https://www.archlinux.org/packages/?name=qemu-block-iscsi) - iSCSI block 支援
*   [qemu-block-rbd](https://www.archlinux.org/packages/?name=qemu-block-rbd) - RBD block 支援
*   [samba](https://www.archlinux.org/packages/?name=samba) - SMB/CIFS 伺服器支援

## QEMU GUI前端

與 [VirtualBox](/index.php/VirtualBox "VirtualBox") 和 [VMware](/index.php/VMware "VMware")等虛擬化方案不同, QEMU不提供GUI界面来管理虛擬機器 (除了執行虛擬機時出現的視窗), 也沒有提供一种持久保存虛擬機設定方式. 必須每一次在命令列上指定所有執行虛擬機器的參數,除非你已經創建了一個Script來啟動你的虛擬機. 然而，有幾種使用者圖形界面前端的QEMU：

*   [qemu-launcher](https://www.archlinux.org/packages/?name=qemu-launcher)
*   [qtemu](https://www.archlinux.org/packages/?name=qtemu)
*   [aqemu](https://aur.archlinux.org/packages/aqemu/)

[libvirt (正體中文)](/index.php/Libvirt_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Libvirt (正體中文)") 也有援 QEMU 的額外前端界面。

## 創建新虛擬系統

### 創建硬碟鏡像

**提示：** 在[QEMU Wikibook](https://en.wikibooks.org/wiki/QEMU/Images) QEMU images常見更多資訊

硬碟鏡像是一個檔案，存儲虛擬機的虛擬硬碟上的內容。除非直接從 CD-ROM 或網路開機並且不安裝系統到硬碟，否則執行 QEMU 時都需要硬碟鏡像。

一個硬碟鏡像可能是 *raw*鏡像, 和客戶機器上看到的內容一模一样，主機上佔用的空間和客戶機上的大小一樣。這個方式 I/O 效率最高，但是因為客户機器上沒使用的空間也被佔用，所以有點浪費空間。另外一種常見的方式是*qcow2* 格式，僅當客戶系統實際寫入內容的時候，才會分配鏡像空間。對客戶機器來說，硬碟大小是完整大小，但是在主機系統上實際僅佔用較小的空間。使用這種方式會影响效率，不過影響非常小.

QEMU 提供 `qemu-img`命令創建硬碟鏡像.例如創建一個 4 GB *raw* 格式的鏡像:

```
$ qemu-img create -f raw *image_file* 4G

```

您可以用 `-f qcow2` 改為創建一個 *qcow2* 磁碟

用 `dd` 或 `fallocate` 也可以創建一個 *raw* 鏡像。

**Warning:** 如果硬碟鏡像存儲在 [Btrfs](/index.php/Btrfs "Btrfs") 系統上，在創建前請考慮禁用 [寫時複製](/index.php/Btrfs#Copy-on-Write_.28CoW.29 "Btrfs")。

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

#### 調整鏡像大小

**警告:** 調整包含NTFS開機檔案系統的鏡像將無法啟動已安裝的作業系統. 完整的解釋和解決辦法參見 [[1]](http://tjworld.net/wiki/Howto/ResizeQemuDiskImages).

執行 `qemu-img` 帶 `resize` 選項調整硬碟鏡像的大小.它適用於 *raw* 和 *qcow2*. 例如, 增加 10 GB 大小, 執行:

```
$ qemu-img resize *disk_image* +10G

```

After enlarging the disk image, you must use file system and partitioning tools inside the virtual machine to actually begin using the new space. When shrinking a disk image, you must **first reduce the allocated file systems and partition sizes** using the file system and partitioning tools inside the virtual machine and then shrink the disk image accordingly, otherwise shrinking the disk image will result in data loss!

### 準備安裝介質

要將作業系統安裝到虛擬機器中, 你需要作業系統的安裝介質 (例如 光碟, USB裝置, 或 ISO 鏡像). 安裝介質不能被掛載因為 QEMU 會直接存取這些媒體。

**Tip:** If using an optical disk, it is a good idea to first dump the media to a file because this both improves performance and does not require you to have direct access to the devices (that is, you can run QEMU as a regular user without having to change access permissions on the media's device file). For example, if the CD-ROM device node is named `/dev/cdrom`, you can dump it to a file with the command: `$ dd if=/dev/cdrom of=*cd_image.iso*` 

## 運行虛擬機

`qemu-system-*` 程式 (例如 `qemu-system-i386` 或 `qemu-system-x86_64`, 取决于客戶機的架構)用來執行QEMU虛擬機. 用法是:

```
$ qemu-system-i386 *options* *disk_image*

```

所有 `qemu-system-*`的選項是大致相同的,參見 `qemu(1)` 查看文件和所有選項

預設 QEMU會在視窗中顯示虛擬機的視訊輸出.有一點要記住:當您按一下QEMU視窗,滑鼠將被捕获。要放開，按 `Ctrl+Alt`.

**警告:** QEMU 最好不要以 root 身分執行. If you must launch it in a script as root, you should use the `-runas` option to make QEMU drop root privileges.

### 啟用 KVM

更多資訊參見 [KVM](/index.php/KVM "KVM").

要在KVM模式中啟動QEMU, 追加 `-enable-kvm`到QEMU選項中. To check if KVM is enabled for a running VM, enter the QEMU [Monitor](https://en.wikibooks.org/wiki/QEMU/Monitor) using `Ctrl+Alt+Shift+2`, and type `info kvm`.

**Note:**

*   If you start your VM with a GUI tool and experience very bad performance, you should check for proper KVM support, as QEMU may be falling back to software emulation.
*   KVM needs to be enabled in order to start Windows 7 and Windows 8 properly without a *blue screen*.

## 宿主機和虛擬機的資料交互

If you have servers on your host OS they will be accessible with the ip-address 10.0.2.2 without any further configuration. So you could just FTP or SSH, etc to 10.0.2.2 from windows to share data, or if you would like to use [Samba](/index.php/Samba "Samba"):

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

### 掛載虛擬硬碟鏡像

Fortunately there is a way to mount the hard disk image with a loopback device. Login as root, make a temporary directory and mount the image with the command:

```
mount -o loop,offset=32256 [[hd''image]] [[tmp''dir]]

```

Now you can copy data in both directions. When you are done, umount with:

```
umount [hd_image]

```

The drawback of this solution is that you cannot use it with qcow images (including overlay images). So you need to create you images without \"-f qcow\" option.

**提示：** Create a second, raw hard drive image. This way you will be able to transfer data easily and use qcow overlay images for the primary drive.

**警告:** 掛載時千萬不要啟動虛擬機!

### 掛載 qcow2 鏡像

你可以使用 `qemu-nbd` 掛載 qcow2 鏡像. 參見 [Wikipedia:Qcow#Mounting_qcow2_images](https://en.wikipedia.org/wiki/Qcow#Mounting_qcow2_images "wikipedia:Qcow").

### 使用物理分割區作為硬碟鏡像中的唯一主分割區

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

## 使用KVM

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

## 網路

### User-mode networking

By default, without any `-netdev` arguments, QEMU will use user-mode networking with a built-in DHCP server. Your virtual machines will be assigned an IP address when they run their DHCP client, and they will be able to access the physical host's network through IP masquerading done by QEMU. This only works with the TCP and UDP protocols, so ICMP, including `ping`, will not work.

This default configuration allows your virtual machines to easily access the Internet, provided that the host is connected to it, but the virtual machines will not be directly visible on the external network, nor will virtual machines be able to talk to each other if you start up more than one concurrently.

QEMU's user-mode networking can offer more capabilities such as built-in TFTP or SMB servers, or attaching guests to virtual LANs so that they can talk to each other. See the QEMU documentation on the `-net user` flag for more details.

However, user-mode networking has limitations in both utility and performance. More advanced network configurations require the use of tap devices or other methods.

### 虛擬拓補網路

#### Basic idea

[Tap devices](https://en.wikipedia.org/wiki/TUN/TAP "wikipedia:TUN/TAP") are a Linux kernel feature that allows you to create virtual network interfaces that appear as real network interfaces. Packets sent to a "tap" interface are delivered to a userspace program, such as QEMU, that has bound itself to the interface.

QEMU can use tap networking for a virtual machine so that packets sent to the tap interface will be sent to the virtual machine and appear as coming from a network interface (usually an Ethernet interface) in the virtual machine. Conversely, everything that the virtual machine sends through its network interface will appear on the tap interface.

Tap devices are supported by the Linux bridge drivers, so it is possible to bridge together tap devices with each other and possibly with other host interfaces such as eth0\. This is desirable if you want your virtual machines to be able to talk to each other, or if you want other machines on your LAN to be able to talk to the virtual machines.

#### Bridge virtual machines to external network

The following describes how to bridge a virtual machine to a host interface such as eth0, which is probably the most common configuration. This configuration makes it appear that the virtual machine is located directly on the external network, on the same Ethernet segment as the physical host machine.

**Warning:** Beware that since your virtual machines will appear directly on the external network, this may expose them to attack. Depending on what resources your virtual machines have access to, you may need to take all the precautions you normally would take in securing a computer to secure your virtual machines.

We will replace the normal Ethernet adapter with a bridge adapter and bind the normal Ethernet adapter to it.

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

And if you still cannot get networking to work, see: [Linux Containers#Bridge_device_setup](/index.php/Linux_Containers#Bridge_device_setup "Linux Containers").

### 橋接網路

NOTE：這部分由[User:Athurg](/index.php/User:Athurg "User:Athurg")根據實際體驗過程翻譯，和原文的流程有比較大的出入。如果有任何問題，請聯繫[User:Athurg](/index.php/User:Athurg "User:Athurg")。

#### 簡介

在QEMU中，橋接網路就是將虛擬機注冊到主機的一個單獨網路介面上，然後將這個介面和主機對外的網路介面一起橋接起來。如果你需要讓虛擬機和外部網路完全互聯互通時，就需要這麼做了！不過需要提醒的是，這樣的話客戶機就完全暴露在網路中了。

#### 準備

首先，請確認下面的軟體包已經安裝上了:

```
 bridge-utils (for brctl, to manipulate bridges)
 uml_utilities (for tunctl, to manipulate taps)
 sudo (for manipulating bridges and tunnels as root)

```

接下來載入橋接模組：

```
 # modprobe bridge

```

#### 配置

首先，修改你的網路配置。增加一个橋接網路介面`br0`，用它来取代原來主機上的本機連線。打開`/etc/rc.conf`，將網路配置的部分修改如下：

```
 eth0="eth0 up"
 br0="dhcp"      #如果你原來的本機連線是DHCP方式獲取配置的話
 #br0="br0 192.168.0.2 netmask 255.255.255.0 up"      #如果你原來的本機連線是靜態設定的話
 INTERFACES=(eth0 br0)

```

然後，將原來的網路卡`eth0`綁定到橋接網路卡`br0`上，使得主機上的網路應用能够通過橋接網路介面，傳遞到外網中。編輯`/etc/conf.d/bridges`：

```
 bridge_br0="eth0"
 BRIDGE_INTERFACES=(br0)

```

載入tap模組

```
 # modprobe tun

```

創建一個`/etc/qemu-ifup`腳本，用於QEMU用來創建和載入虛擬機器對外存取的網路介面。

```
 #!/bin/sh

 echo "Executing /etc/qemu-ifup"
 echo "Bringing up $1 for bridged mode..."
 sudo /sbin/ifconfig $1 0.0.0.0 promisc up
 echo "Adding $1 to br0..."
 sudo /usr/sbin/brctl addif br0 $1
 sleep 2

```

這個腳本的屬主應該設定為root:kvm，權限為750，以使得kvm組的使用者（可以啟動虛擬機的使用者）也能执執行。這裡也提醒大家一次，所有需要通過qemu使用KVM虛擬機的使用者，都應該加入到kvm組中。

由於這個Script里需要調用ifconfig等命令來給虛擬機動態增減網路介面，为了方便我們在腳本里通過sudo來執行。如果不想腳本執行過程中向使用者索取密碼，請編輯`sudo`或者`visudo`的設定檔，加入下面這一行：

```
 Cmnd_Alias      QEMU=/sbin/ifconfig,/sbin/modprobe,/usr/sbin/brctl,/usr/bin/tunctl
 %kvm     ALL=NOPASSWD: QEMU

```

最後，將`bridge`和`tun`加入到檔案`/etc/rc.conf`的`MODULES`變數中，以便開機就能載入。

#### 啟動

一切配置妥當，我們就可以開始體驗了。 啟動帯橋接模式網路界面的QEMU大致有三個步驟

*   通過tunctl申請一個可用的虛擬網路介面——tap设备。
*   配置這個裝置並橋接到橋接網路介面，然後啟動qemu
*   要是每次啟動虛擬機都這麼複雜不是很煩？我們可以創建一個腳本來實現：

```
USERID=`whoami`
IFACE=`sudo tunctl -b -u $USERID`

qemu -net nic -net tap,ifname="$IFACE" $*

sudo tunctl -d $IFACE &> /dev/null

```

需要注意一点，由於我們前面創建了`/etc/qemu-ifup`這個Script，因此我們只需要把申請到的虛擬網路介面名通過-net tap,ifname="網路介面名"告訴qemu，他自己会用這個介面名為參數，調用/etc/qemu-ifup來完成橋接和配置這個網路介面的過程。

## 圖形

QEMU 可以使用以下幾個圖形輸出：std, cirrus, vmware, qxl, xenfs 和 vnc。

使用 `vnc` 選項，你可以單獨執行客戶機，並且通過 VNC 連接。其他選項是使用`std`, `vmware`, `cirrus`:

### std

使用 `-vga std` 你可以得到最高 2560 x 1600 像素的解析度。

### vmware

儘管有一點怪怪的，但是這種方法確實比 std 和 cirrus 效果好。在客戶機中，安裝 VMware 驅動程式：

```
pacman -S xf86-video-vmware xf86-input-vmmouse

```

### Windows 客戶機

如果你使用 Windows 客戶機，你也許想使用遠端桌面協定(RDP)連線到客戶虛擬機。使用：(如果你使用 VLAN 或與客戶機不在同一个網路之中)

```
qemu -nographic -net user,hostfwd=tcp::5555-:3389

```

然后用 rdesktop 或者 freerdp 连接到客户机，例如：

```
xfreerdp -g 2048x1152 localhost:5555 -z -x lan

```

## Qemu的前端

Qemu有幾個圖像前端，不喜歡命令行的可以使用:

*   community/qemu-launcher
*   community/qemulator
*   community/qtemu

## 鍵盤不工作/方向鍵不工作

如果你發現一些按鍵不工作或“按下”錯誤的鍵(尤其是方向鍵)，你也許需要在選項中指定你的鍵盤佈局。鍵盤佈局可以在 `/usr/share/qemu/keymaps` 找到。

```
qemu -k [keymap] [disk_image]

```

## 開機時執行 QEMU 虛擬機

想要在開機時執行 QEMU 虛擬機，你可以使用下面的 rc-script 和設定檔.

<caption>設定檔選項</caption>
| QEMU_MACHINES | 要啟動的虛擬機清單 |
| qemu_${vm}_type | 調用的 QEMU 二進制檔案。如果指定，会被加到 `/usr/bin/qemu-` 之後，這個程式会被使用來啟動虛擬機。也就是說，如你可以啟動比如 qemu-system-arm 鏡像使用 qemu_my_arm_vm_type="system-arm"。如果不指定，`/usr/bin/qemu` 會被使用。 |
| qemu_${vm} | 啟動的 QEMU 命令行。預設帯有 `-name ${vm} -pidfile /var/run/qemu/${vm}.pid -daemonize -nographic`選項。 |
| qemu_${vm}_haltcmd | 安全關閉虛擬機的命令。我使用 `-monitor telnet:..` 以及通過發送`system_powerdown` 到 monitor，通過 ACPI 關閉我的虛擬機。你可以使用 ssh 或其他方法。 |
| qemu_${vm}_haltcmd_wait | 等待關閉虛擬機的時間。預設是30秒。rc-script 會在這個時間後 kill qemu 處理程序。 |

設定檔例子：

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