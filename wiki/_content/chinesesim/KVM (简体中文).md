**KVM**（Kernel-based Virtual Machine的英文缩写是内核内建的虚拟机。有点类似于 [Xen](/index.php/Xen "Xen") ，但更追求更简便的运作，比如运行此虚拟机，仅需要加载相应的 `kvm` 模块即可后台待命。和 Xen 的完整模拟不同的是，KVM 需要芯片支持虚拟化技术（英特尔的 VT 扩展或者 AMD 的 AMD-V 扩展）。

在KVM中，可以运行各种未更改的GNU/Linux, Windows 或任何其他系统镜像。(请看[客户机支持状态](http://www.linux-kvm.org/page/Guest_Support_Status))，每个虚拟机都可提供独享的虚拟硬件：网卡，硬盘，显卡等。请看 [KVM Howto](http://www.linux-kvm.org/page/HOWTO)

KVM, Xen, VMware, 和 QEMU 的不同，请看这里[KVM FAQ](http://www.linux-kvm.org/page/FAQ#What_is_the_difference_between_kvm_and_Xen.3F).

## Contents

*   [1 检查是否支持KVM](#.E6.A3.80.E6.9F.A5.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81KVM)
    *   [1.1 硬件支持](#.E7.A1.AC.E4.BB.B6.E6.94.AF.E6.8C.81)
    *   [1.2 内核支持](#.E5.86.85.E6.A0.B8.E6.94.AF.E6.8C.81)
    *   [1.3 KVM模块](#KVM.E6.A8.A1.E5.9D.97)
*   [2 Para-virtualized devices](#Para-virtualized_devices)
    *   [2.1 VIRTIO modules](#VIRTIO_modules)
    *   [2.2 Loading kernel modules](#Loading_kernel_modules)
    *   [2.3 List of para-virtualized devices](#List_of_para-virtualized_devices)
*   [3 如何使用KVM](#.E5.A6.82.E4.BD.95.E4.BD.BF.E7.94.A8KVM)
*   [4 小贴士与小技巧](#.E5.B0.8F.E8.B4.B4.E5.A3.AB.E4.B8.8E.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [4.1 嵌套虚拟化](#.E5.B5.8C.E5.A5.97.E8.99.9A.E6.8B.9F.E5.8C.96)
    *   [4.2 Live snapshots](#Live_snapshots)
    *   [4.3 Poor Man's Networking](#Poor_Man.27s_Networking)
    *   [4.4 Enabling huge pages](#Enabling_huge_pages)
*   [5 See also](#See_also)

## 检查是否支持KVM

### 硬件支持

KVM需要虚拟机宿主（host）的处理器带有虚拟化支持（对于Intel处理器来说是VT-x，对于AMD处理器来说是AMD-V）。你可以通过以下命令来检查你的处理器是否支持虚拟化：

```
$ lscpu

```

如果你的处理器支持虚拟化，输出结果中会有一行Virtualization的信息。

你也可以运行：

```
$ grep -E "(vmx|svm)" --color=always /proc/cpuinfo

```

如果运行后没有显示，那么你的处理器**不**支持硬件虚拟化，你**不能**使用KVM。

**注意:** 您可能需要在BIOS中启用虚拟化支持

### 内核支持

Arch Linux的内核提供了相应的[内核模块](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)")来支持KVM和VIRTIO

### KVM模块

如果你的内核是用 CONFIG_IKCONFIG_PROC 这个选项编译的话，你可以通过以下命令来检查你的内核是否已经包含了支持虚拟化所必须的模块（`kvm`及`kvm_amd`与`kvm_intel`这两者中的任意一个）：

```
$ zgrep KVM /proc/config.gz

```

如果模块设置不等于 `y`或`m`,则该模块**不**可用

## Para-virtualized devices

Para-virtualization provides a fast and efficient means of communication for guests to use devices on the host machine. KVM provides para-virtualized devices to virtual machines using the Virtio API as a layer between the hypervisor and guest.

All virtio devices have two parts: the host device and the guest driver.

### VIRTIO modules

Use the following command to check if needed modules are available:

```
$ zgrep VIRTIO /proc/config.gz

```

### Loading kernel modules

First, check if the kernel modules are automatically loaded. This should be the case with recent versions of [udev](/index.php/Udev "Udev").

```
$ lsmod | grep kvm
$ lsmod | grep virtio

```

In case the above commands return nothing, you need to [load](/index.php/Kernel_modules#Loading "Kernel modules") kernel modules.

**Tip:** If modprobing `kvm_intel` or `kvm_amd` fails but modprobing `kvm` succeeds, (and `lscpu` claims that hardware acceleration is supported), check your BIOS settings. Some vendors (especially laptop vendors) disable these processor extensions by default. To determine whether there's no hardware support or there is but the extensions are disabled in BIOS, the output from `dmesg` after having failed to modprobe will tell.

### List of para-virtualized devices

*   network device (virtio-net)
*   block device (virtio-blk)
*   controller device (virtio-scsi)
*   serial device (virtio-serial)
*   balloon device (virtio-balloon)

## 如何使用KVM

请参考[QEMU](/index.php/QEMU "QEMU")条目。

## 小贴士与小技巧

**注意:** 请参考[QEMU#Tips and tricks](/index.php/QEMU#Tips_and_tricks "QEMU")和[QEMU#Troubleshooting](/index.php/QEMU#Troubleshooting "QEMU")词条。

### 嵌套虚拟化

在宿主机启用`kvm_intel`模块的嵌套虚拟化功能：

```
# modprobe -r kvm_intel
# modprobe kvm_intel nested=1

```

使嵌套虚拟化永久生效（请参考[Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules")）：

 `/etc/modprobe.d/modprobe.conf` 
```
options kvm_intel nested=1

```

检验嵌套虚拟化功能是否已被激活：

 `$ systool -m kvm_intel -v | grep nested` 
```
    nested              = "Y"

```

使用以下命令来运行guest虚拟机：

```
$ qemu-system-x86_64 -enable-kvm -cpu host

```

启动虚拟机并检查是否有vmx标志：

```
$ grep vmx /proc/cpuinfo

```

### Live snapshots

A feature called external snapshotting allows one to take a live snapshot of a virtual machine without turning it off. Currently it only works with qcow2 and raw file based images.

Once a snapshot is created, KVM attaches that new snapshotted image to virtual machine that is used as its new block device, storing any new data directly to it while the original disk image is taken offline which you can easily copy or backup. After that you can merge the snapshotted image to the original image, again without shutting down your virtual machine.

Here's how it works.

Current running vm

```
# virsh list --all
Id    Name                           State
----------------------------------------------------
3     archey                            running

```

List all its current images

```
# virsh domblklist archey 
Target     Source
------------------------------------------------
vda        /vms/archey.img

```

Notice the image file properties

```
# qemu-img info /vms/archey.img
image: /vms/archey.img
file format: qcow2
virtual size: 50G (53687091200 bytes)
disk size: 2.1G
cluster_size: 65536

```

Create a disk-only snapshot. The switch `--atomic` makes sure that the VM is not modified if snapshot creation fails.

```
# virsh snapshot-create-as archey snapshot1 --disk-only --atomic

```

List if you want to see the snapshots

```
# virsh snapshot-list archey
Name                 Creation Time             State
------------------------------------------------------------
snapshot1           2012-10-21 17:12:57 -0700 disk-snapshot

```

Notice the new snapshot image created by virsh and its image properties. It weighs just a few MiBs and is linked to its original "backing image/chain".

```
# qemu-img info /vms/archey.snapshot1
image: /vms/archey.snapshot1
file format: qcow2
virtual size: 50G (53687091200 bytes)
disk size: 18M
cluster_size: 65536
backing file: /vms/archey.img

```

At this point, you can go ahead and copy the original image with `cp -sparse=true` or `rsync -S`. Then you can merge the original image back into the snapshot.

```
# virsh blockpull --domain archey --path /vms/archey.snapshot1

```

Now that you have pulled the blocks out of original image, the file `/vms/archey.snapshot1` becomes the new disk image. Check its disk size to see what it means. After that is done, the original image `/vms/archey.img` and the snapshot metadata can be deleted safely. The `virsh blockcommit` would work opposite to `blockpull` but it seems to be currently under development in qemu-kvm 1.3 (including snapshot-revert feature), scheduled to be released sometime next year.

This new feature of KVM will certainly come handy to the people who like to take frequent live backups without risking corruption of the file system.

### Poor Man's Networking

Setting up bridged networking can be a bit of a hassle sometimes. If the sole purpose of the VM is experimentation, one strategy to connect the host and the guests is to use SSH tunneling.

The basic steps are as follows:

*   Setup an SSH server in the host OS
*   (optional) Create a designated user used for the tunneling (e.g. tunneluser)
*   Install SSH in the VM
*   Setup authentication

See: [SSH](/index.php/SSH "SSH") for the setup of SSH, especially [SSH#Forwarding other ports](/index.php/SSH#Forwarding_other_ports "SSH").

When using the default user network stack, the host is reachable at address 10.0.2.2.

If everything works and you can SSH into the host, simply add something like the following to your `/etc/rc.local`

```
# Local SSH Server
echo "Starting SSH tunnel"
sudo -u vmuser ssh tunneluser@10.0.2.2 -N -R 2213:127.0.0.1:22 -f
# Random remote port (e.g. from another VM)
echo "Starting random tunnel"
sudo -u vmuser ssh tunneluser@10.0.2.2 -N -L 2345:127.0.0.1:2345 -f

```

In this example a tunnel is created to the SSH server of the VM and an arbitrary port of the host is pulled into the VM.

This is a quite basic strategy to do networking with VMs. However, it is very robust and should be quite sufficient most of the time.

### Enabling huge pages

You may also want to enable hugepages to improve the performance of your virtual machine. With an up to date Arch Linux and a running KVM you probably already have everything you need. Check if you have the directory `/dev/hugepages`. If not create it. Now we need the right permissions to use this directory. Check if the group `kvm` exist and if you are member of this group. This should be the case if you already have a running virtual machine.

 `$ getent group kvm` 
```
kvm:x:78:USERNAMES

```

Add to your `/etc/fstab`:

```
hugetlbfs       /dev/hugepages  hugetlbfs       mode=1770,gid=78        0 0

```

Of course the gid must match that of the `kvm` group. The mode of `1770` allows anyone in the group to create files but not unlink or rename each other's files. Make sure `/dev/hugepages` is mounted properly:

```
# umount /dev/hugepages
# mount /dev/hugepages
$ mount | grep huge
```
 `hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,mode=1770,gid=78)` 

Now you can calculate how many hugepages you need. Check how large your hugepages are:

```
$ cat /proc/meminfo | grep Hugepagesize

```

Normally that should be 2048 kB ≙ 2 MB. Let's say you want to run your virtual machine with 1024 MB. 1024 / 2 = 512\. Add a few extra so we can round this up to 550\. Now tell your machine how many hugepages you want:

```
# echo 550 > /proc/sys/vm/nr_hugepages

```

If you had enough free memory you should see:

 `$ cat /proc/meminfo | grep HugePages_Total` 
```
HugesPages_Total:  550

```

If the number is smaller, close some applications or start your virtual machine with less memory (number_of_pages x 2):

```
$ qemu-system-x86_64 -enable-kvm -m 1024 -mem-path /dev/hugepages -hda <disk_image> [...]

```

Note the `-mem-path` parameter. This will make use of the hugepages.

Now you can check, while your virtual machine is running, how many pages are used:

 `$ cat /proc/meminfo | grep HugePages` 
```
HugePages_Total:     550
HugePages_Free:       48
HugePages_Rsvd:        6
HugePages_Surp:        0

```

Now that everything seems to work you can enable hugepages by default if you like. Add to your `/etc/sysctl.d/80-hugepages.conf`:

```
vm.nr_hugepages = 550

```

See also:

*   [https://www.kernel.org/doc/Documentation/vm/hugetlbpage.txt](https://www.kernel.org/doc/Documentation/vm/hugetlbpage.txt)
*   [http://wiki.debian.org/Hugepages](http://wiki.debian.org/Hugepages)
*   [http://www.linux-kvm.com/content/get-performance-boost-backing-your-kvm-guest-hugetlbfs](http://www.linux-kvm.com/content/get-performance-boost-backing-your-kvm-guest-hugetlbfs)

## See also

*   [KVM Howto](http://www.linux-kvm.org/page/HOWTO)
*   [KVM FAQ](http://www.linux-kvm.org/page/FAQ#General_KVM_information)