相关文章

*   [VMware](/index.php/VMware "VMware")
*   [Installing VMWare vCLI](/index.php/Installing_VMWare_vCLI "Installing VMWare vCLI")

**翻译状态：** 本文是英文页面 [VMware/Installing Arch as a guest](/index.php/VMware/Installing_Arch_as_a_guest "VMware/Installing Arch as a guest") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-9-30，点击[这里](https://wiki.archlinux.org/index.php?title=VMware%2FInstalling+Arch+as+a+guest&diff=0&oldid=545127)可以查看翻译后英文页面的改动。

这篇文章是关于如何在[VMware](/index.php/VMware "VMware")产品，比如[Player (Plus)](http://www.vmware.com/products/player/)，[Fusion](http://www.vmware.com/products/fusion/)或[Workstation](http://www.vmware.com/products/workstation/)中安装ArchLinux。

## Contents

*   [1 编译进内核的驱动程序（模块）](#编译进内核的驱动程序（模块）)
*   [2 VMware Tools 与 Open-VM-Tools 方案对比](#VMware_Tools_与_Open-VM-Tools_方案对比)
*   [3 Open-VM-Tools](#Open-VM-Tools)
    *   [3.1 实用工具](#实用工具)
    *   [3.2 内核模块](#内核模块)
    *   [3.3 安装](#安装)
*   [4 官方的 VMware Tools](#官方的_VMware_Tools)
    *   [4.1 模块](#模块)
    *   [4.2 安装（从客户机）](#安装（从客户机）)
*   [5 Xorg 配置](#Xorg_配置)
*   [6 提示与技巧](#提示与技巧)
    *   [6.1 通过 vmhgfs-fuse 共享目录](#通过_vmhgfs-fuse_共享目录)
        *   [6.1.1 fstab](#fstab)
        *   [6.1.2 Systemd](#Systemd)
    *   [6.2 3D加速](#3D加速)
        *   [6.2.1 OpenGL 与 GLSL 支持](#OpenGL_与_GLSL_支持)
    *   [6.3 时间同步](#时间同步)
        *   [6.3.1 与宿主机同步时间](#与宿主机同步时间)
        *   [6.3.2 与外部服务器同步时间](#与外部服务器同步时间)
    *   [6.4 性能优化](#性能优化)
        *   [6.4.1 平行虚拟化 SCSI 驱动](#平行虚拟化_SCSI_驱动)
        *   [6.4.2 平行虚拟化网络驱动](#平行虚拟化网络驱动)
        *   [6.4.3 虚拟机设置](#虚拟机设置)
*   [7 故障排除](#故障排除)
    *   [7.1 客户机网络速度减慢](#客户机网络速度减慢)
    *   [7.2 较新的内核下的文件共享问题](#较新的内核下的文件共享问题)
    *   [7.3 声音问题](#声音问题)
    *   [7.4 鼠标问题](#鼠标问题)
    *   [7.5 启动故障](#启动故障)
        *   [7.5.1 启动速度慢](#启动速度慢)
        *   [7.5.2 关机/重启时卡住不动](#关机/重启时卡住不动)
    *   [7.6 窗口分辨率自动适配](#窗口分辨率自动适配)
        *   [7.6.1 方案 1](#方案_1)
        *   [7.6.2 方案 2](#方案_2)
        *   [7.6.3 方案 3](#方案_3)
        *   [7.6.4 方案 4](#方案_4)
    *   [7.7 拖拽与复制粘贴](#拖拽与复制粘贴)
    *   [7.8 在 VMware Workstation 11 版上运行共享 VM](#在_VMware_Workstation_11_版上运行共享_VM)
    *   [7.9 系统更新后共享文件夹没有被挂载](#系统更新后共享文件夹没有被挂载)

## 编译进内核的驱动程序（模块）

*   `vmw_balloon` - 物理内存管理驱动。它可以像一个气球一样被“吹大”，从监视器处夺走物理内存的使用权；也可以“放气”，允许物理内存被虚拟机使用。还支持将反分配状态（deallocated）的虚拟机原本所占的内存释放回主机，而无需彻底停用虚拟机。
*   `vmw_pvscsi` - VMware 平行虚拟化 SCSI（PVSCSI）的主机总线适配器（HBA）。
*   `vmw_vmci` - 虚拟机通信接口（VMCI）。VMCI 虚拟设备的作用是使虚拟环境间的主机-客机高速通信。
*   `vmwgfx` - 这是 VMware SVGA2 虚拟显卡的 DRM 驱动，作用是 3D 加速。支持 [|KMS](/index.php/Kernel_mode_setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel mode setting (简体中文)")。
*   `vmxnet3` - VMware 的 vmxnet3 虚拟网卡所需模块。
*   从 Linux 内核 4.0 起，[open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) 包含了一个基于 [FUSE](/index.php/Fuse "Fuse") 实现的 HGFS 文件系统。用于主机-客机间共享目录。

如果你在某种监视器（比如 [VMware vSphere Hypervisor](http://www.vmware.com/products/vsphere-hypervisor)）上运行 Arch Linux，那么下面这些模块也是需要的：

*   `vsock` - 虚拟套接字协议。其作用是允许虚拟机，主机或监视器间像 TCP/IP 协议一样通信。
*   `vmw_vsock_vmci_transport` - 基于 VMCI 实现的虚拟套接字。

**注意:** 以上模块只有少量会被 Arch 的 [Udev](/index.php/Udev "Udev") 自动检测并启用。某些附加模块，比如`vmw_balloon`，可能需要添加到[Mkinitcpio](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")的 `MODULES` 列表，来实现尽早加载。例如: ` # cat /etc/mkinitcpio.conf` 
```
...
MODULES="... vmw_balloon vmw_pvscsi vmware_vmhgfs vsock vmw_vsock_vmci_transport ..."
```

修改 mkinitcpio.conf 后记得运行:

```
 # mkinitcpio -p linux

```

某些模块，例如旧方案中实现共享目录的 `vmhgfs`，还需要额外地手工编译，并手工从 systemd 启用服务，才能正常运转。

## VMware Tools 与 Open-VM-Tools 方案对比

2007 年，VMware 将 [VMware Tools](http://kb.vmware.com/kb/340) 中的大部分代码以 LGPL 协议发布，这就是 [Open-VM-Tools](http://sourceforge.net/projects/open-vm-tools/)。官方的 VMware Tools 不再[单独](http://packages.vmware.com/tools/esx/latest/repos/index.html)向 Arch Linux 提供。

以往，VMware Tools 方案所提供的网络与储存驱动是最好的，而且还带有时间同步等功能。然而网络与 SCSI 驱动这部分代码已经早就合入 Linux 内核了。

VMware Tools 曾经有使用 Unity mode 功能的优势，但由于使用的人不多且维护困难，于是从 VMWare Workstation 12 开始移除了 Linux 客户机的 Unity mode 支持。详情请阅 [此跟帖](https://communities.vmware.com/thread/518735) 的答案。

## Open-VM-Tools

### 实用工具

[open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) 软件包里包括如下工具：

*   `vmtoolsd` - 负责汇报虚拟机状态的服务。
*   `vmware-checkvm` - 用于检测虚拟机中是否在运行着某程序的工具。
*   `vmware-toolbox-cmd` - 用于收集宿主系统信息的工具。
*   `vmware-user` - Tool to enable clipboard sharing (copy/paste) between host and guest.
*   `vmware-vmblock-fuse` - 文件系统。基于 [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (Filesystem in Userspace) 实现了宿主 / 客机之间拖拽文件。
*   `vmware-xferlogs` - 向虚拟机的日志文件输出日志与调试信息。
*   `vmhgfs-fuse` - 挂载 HGFS 共享目录的工具。

### 内核模块

*   `vmhgfs` - 旧有的 HGFS 驱动。这是传统的宿主机-客机间共享目录的方案。
*   `vmxnet` - 旧有的 VMXNET 网卡驱动。

### 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) 。 如果你想使用共享文件夹，你还需要安装 [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) 包。 然后 [启动](/index.php?title=%E5%90%AF%E5%8A%A8&action=edit&redlink=1 "启动 (page does not exist)") 并 [启用](/index.php/%E5%90%AF%E7%94%A8 "启用") `vmtoolsd.service` 和 `vmware-vmblock-fuse.service`。

如果该功能无法正常工作，请尝试手动安装 [gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3) 。如要启用客户机的拖拽与复制粘贴功能，则需要安装 [gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3) 。

## 官方的 VMware Tools

### 模块

*   `vmblock` - 文件系统驱动。支持在主机-客机间拖拽文件。已被 `vmware-vmblock-fuse`（[取代](https://www.mail-archive.com/open-vm-tools-devel@lists.sourceforge.net/msg00213.html)）。
*   `vmci` - 主机-客机间的高性能通信接口。
*   `vmmon` - 虚拟机监视器。
*   `vmnet` - 网络驱动。
*   `vsock` - VMCI 套接字。

**注意:** `vmware-vmblock-fuse` 这一组件不是以内核模块的形式实现的，而是需要手动启动 Systemd 服务。具体操作步骤见下文。 {ic
模块已经从内核移除（除非你禁用了 `fuse`）。

}}

### 安装（从客户机）

安装依赖项：[base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)（用于编译模块），[net-tools](https://www.archlinux.org/packages/?name=net-tools)（提供 `ifconfig` 供安装程序调用）和 [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) (提供内核头文件)。为签出 `open-vm-tools` 的生成依赖项是 [asp](https://www.archlinux.org/packages/?name=asp)。

然后创建 init 目录，满足安装程序：

```
# for x in {0..6}; do mkdir -p /etc/init.d/rc$x.d; done

```

挂载安装程序：

```
# mount /dev/cdrom /mnt

```

解压（以 `/root` 为例）：

```
# tar xf /mnt/VMwareTools*.tar.gz -C /root

```

开始安装

```
# perl /root/vmware-tools-distrib/vmware-install.pl

```

若安装时出现如下的错误，都可以安全忽略：

*   VMNEXT 3 虚拟网卡
*   “Warning: This script could not find mkinitrd or update-initramfs and cannot remake the initrd file!”
*   在系统中找不到 Fuse 组件

启用 `vmware-vmblock-fuse` systemd 服务（请确保你手动安装了依赖或使用 `-s` 参数）：

```
 $ asp checkout open-vm-tools
 $ cd open-vm-tools/repos/community-x86_64/
 $ makepkg -s --asdeps
 # cp vm* /usr/lib/systemd/system
 # systemctl enable vmware-vmblock-fuse
 # systemctl enable vmtoolsd

```

重新启动虚拟机：

```
# systemctl reboot

```

登录并启动 VMware Tools:

```
# /etc/init.d/rc6.d/K99vmware-tools start

```

**Tip:** 在 GitHub 上有个项目 [[1]](https://github.com/rasa/vmware-tools-patches) 尝试将这些步骤全自动处理。

## Xorg 配置

**注意:** 要在虚拟机中使用 Xorg，至少需要为其分配 32MB 的显存。

需要安装以下依赖：[xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse)，[xf86-video-vmware](https://www.archlinux.org/packages/?name=xf86-video-vmware)，以及 [mesa](https://www.archlinux.org/packages/?name=mesa)。

如果能启动至 `graphical.target` 那么已经接近成功了。接下来 `/etc/xdg/autostart/vmware-user.desktop` 会自动启动，并负责完成在虚拟机里运行 X 的必要配置。

然而如果你先启动至了 `multi-user.target`，或者你的环境不太常规（比如用了多个显示器），那么你需要手动启动 `vmtoolsd.service` 服务。并且为了让 X server 拥有 root 权限来加载驱动，还需要编辑下面的配置：

 `/etc/X11/Xwrapper.config`  `needs_root_rights=yes` 

## 提示与技巧

### 通过 `vmhgfs-fuse` 共享目录

**注意:** 这一功能需要的最低软件版本是 `open-vm-tools` v.10.x 与 Linux 内核 4.x。或者 VMware Workstation / Fusion。

在菜单中选择 *Edit virtual machine settings > Options > Shared Folders > Always enabled*，即可建立共享目录。

在客机里运行如下命令可以列出共享目录：

```
$ vmware-hgfsclient

```

然后以如下方式挂载：

```
# mkdir <shared folders root directory>
# vmhgfs-fuse -o allow_other -o auto_unmount .host:/*<shared_folder>* *<shared folders root directory>*

```

欲了解 `vmhgfs-fuse` 的其他挂载参数，可以用 `-h` 参数调用：

```
# vmhgfs-fuse -h

```

##### fstab

每个共享目录的挂载都需要写如下的一行配置：

 `/etc/fstab` 
```
.host:/*<shared_folder>* */home/user1/shares* fuse.vmhgfs-fuse defaults 0 0

```

然后创建并挂载目录：

```
# mkdir /home/user1/shares
# mount /home/user1/shares

```

##### Systemd

可以把挂载目录的命令写成 Systemd `.service`：

 `/etc/systemd/system/*<shared folders root directory>*-*<shared_folder>*.service` 
```
[Unit]
Description=Load VMware shared folders
Requires=vmware-vmblock-fuse.service
After=vmware-vmblock-fuse.service
ConditionPathExists=.host:/*<shared_folder>*
ConditionVirtualization=vmware

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=
ExecStart=/usr/bin/vmhgfs-fuse -o allow_other -o auto_unmount .host:/*<shared_folder>* *<shared folders root directory>*

[Install]
WantedBy=multi-user.target
```

如果客机里的 `*<shared folders root directory>*` 目录还不存在，你需要手动提前创建：

```
# mkdir -p *<shared folders root directory>*

```

然后[激活](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)") `<shared folders root directory>-<shared_folder>.service` 这个挂载服务。

删掉 *<shared_folder>* 的部分可以一次性挂载所有共享目录。

### 3D加速

3D加速功能如果在创建客户机时没有选择, 可以勾选: *编辑虚拟机设置 > 硬件 > 显示器 > 加速3D图形*.

**注意:** 启用 3D 加速之后，Xorg 的性能可能会很差。有些时候通过 llvmpipe 来实现软件渲染的性能可能更好。

#### OpenGL 与 GLSL 支持

用户可以自行更新实现 OpenGL 的 GLSL 内核模块，覆盖 Arch 自带的版本。

本文成文时，OpenGL 3.3 和 GLSL 3.30 都得到了支持。参阅 [https://bbs.archlinux.org/viewtopic.php?id=202713](https://bbs.archlinux.org/viewtopic.php?id=202713) 可以了解更多细节。

### 时间同步

为虚拟机配置时间同步很重要，因为虚拟机比物理机更容易出现时间波动现象。主要原因就在于 CPU 是被共用的。

有两种方案可以实现实现同步：同步到宿主机，或是外部服务器。

#### 与宿主机同步时间

保证 `vmtoolsd.service` 服务处于运行状态，然后用如下的命令启用时间同步功能：

```
# vmware-toolbox-cmd timesync enable

```

宿主系统休眠后，用如下的命令来使客机间同步时间：

```
# hwclock --hctosys --localtime

```

#### 与外部服务器同步时间

参阅 [NTP](/index.php/NTP "NTP")。

### 性能优化

下面这些技巧可以帮你改善虚拟机性能。

#### 平行虚拟化 SCSI 驱动

[VMware 平行虚拟化 SCSI (PVSCSI) 驱动](http://kb.vmware.com/kb/1010398) 是为 VMware ESXi 设计的 SCSI 驱动。可以明显提升吞吐量，降低 CPU 消耗。

在虚拟机设置的 SCSI 适配器类型里可以找到 `VMware 平行虚拟化`选项。

如果你在虚拟机设置里找不到这些选项，可以用这个办法：首先确保将 PVSCSI 模块添加进内核的内存盘镜像。具体的做法是修改`mkinitcpio.conf` 文件：

 ` cat /etc/mkinitcpio.conf` 
```
...
MODULES="... vmw_pvscsi"
...
```

然后重建内存盘镜像：

```
# mkinitcpio -p linux

```

将虚拟机关机，在虚拟机的 `.vmx` 配置文件里用如下的方法指定 SCSI 驱动：

```
scsi0.virtualDev = "pvscsi"

```

#### 平行虚拟化网络驱动

VMware 虚拟机提供了 [多种网络适配方案](http://kb.vmware.com/kb/1001805)。默认的网卡适配器一般是`e1000`，它能模拟 Intel 82545EM 千兆以太网卡。该网卡可以被常见的操作系统（含 Arch）直接支持。

若要 [提升性能，并引入更多高级功能](http://rickardnobel.se/vmxnet3-vs-e1000e-and-e1000-part-1/)（比如多队列支持），可以考虑使用 VMware 原生的 `vmxnet3` 网络适配器。

正常安装的 Arch 就包含有 `vmxnet3` 内核模块。该模块可以通过 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") 来启用（或者被自动加载。可以用 `lsmod | grep vmxnet3` 命令来验证加载成功），然后关闭虚拟机，并如下修改 *.vmx* 文件：

```
ethernet0.virtualDev = "vmxnet3"

```

指定更换网卡驱动之后，你还要更新网络与 [dhcpcd](/index.php/Dhcpcd "Dhcpcd") 的设置来真正使用新网卡：

```
# dhcpcd *new_interface_name*
# systemctl enable dhcpcd@*new_interface_name*.service

```

运行 `ip link` 命令可以找到新网卡的名字。

#### 虚拟机设置

按照 [Vmware KB1008885](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1008885) 给出的如下优化方法，可以减少硬盘 I/O 操作数量，但代价是提升宿主机内存占用：

```
mainMem.useNamedFile = "FALSE"
MemTrimRate = "0"
prefvmx.useRecommendedLockedMemSize = "TRUE"
MemAllowAutoScaleDown = "FALSE"
sched.mem.pshare.enable = "FALSE"

```

*   **mainMem.useNamedFile**: 把这个参数的值设为 *"FALSE"* 可以让 VMware 不再创建 *.vmem* 文件。这样有助于减少虚拟机关机时的硬盘操作，但这么做只对 Windows 宿主系统有效。如果你的宿主系统是 Linux，建议用这个配置：*mainmem.backing = "swap"*。
*   **MemTrimRate**: 这项优化会使客机释放的内存在宿主机得不到释放。
*   **prefvmx.useRecommendedLockedMemSize**: 很遗憾，这项优化没给出什么解释。貌似会阻止宿主系统把客机系统的部分内存进行内存换页。
*   **MemAllowAutoScaleDown**: 阻止 VMware 在申请不到内存的时候自动调整虚拟机的内存大小。
*   **sched.mem.pshare.enable**: 如果同时有多台虚拟机运行，VMware 会尝试找到它们之间相同的内存页，并且在共享这些页。但这是个 I/O 消耗很大的操作。

下面这些配置可以在 VMware Workstation 的配置对话框里调整 (*Edit -> Preferences... -> Memory/Priority*)。

```
prefvmx.minVmMemPct = "100"
mainMem.partialLazySave = "FALSE"
mainMem.partialLazyRestore = "FALSE"

```

*   **prefvmx.minVmMemPct**: 指定虚拟机的内存应该有多大的部分来自物理内存，单位是百分比。如果这个值设得较低，那么虚拟机可见的内存总量是可以超过物理机的物理内存的。但这就会带来大量的硬盘读写。如果你的物理内存够大的话，这个值应该维持在 100。

*   **mainMem.partialLazySave** and **mainMem.partialLazyRestore**: 这两项参数的优化是为了阻止虚拟机出于休眠的目的来创建不完整内存快照。如此优化之后，虚拟机的休眠操作耗时会稍长些，但相应地也会减少硬盘读写。

## 故障排除

### 客户机网络速度减慢

Arch Linux，和其他 Linux 客户机一样，当使用 NAT 模式的时候也许会碰到网络速度减慢的问题。为了解决这个问题，请在宿主机下把对应的客户机的网络模式切换为 **桥接模式** ，在必要时修改客户机网络的配置文件。有关配置的详细信息请参阅 [Network configuration (简体中文)](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)") 。如果在 Windows 宿主机下，使用正确的客户机网络配置忍让无法正确连接网络, 可使用 **管理员** 运行 **虚拟网络编辑器** 并点击左下方的 **还原默认设置** 按钮。

### 较新的内核下的文件共享问题

由于 [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) 包已经不再更新，较新的内核无法正确地使用它的做出兼容宿主机和客户机之间文件共享的修补。该[Github 仓库](https://github.com/davispuh/open-vm-tools-dkms) 有一些修补文件可以手动应用它们并解决问题。

你还被推荐查看该包的 AUR comment 部分。

### 声音问题

如果虚拟机发出了恼人的巨响，那有可能是 [PC 扬声器](/index.php/PC_speaker "PC speaker")的原因。在客户机系统里禁用 PC 扬声器即可解决：

```
# echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf

```

### 鼠标问题

虚拟机可能会出现下列鼠标问题：

*   自动获取/失去焦点的功能可能会在鼠标箭头移入窗口时失效
*   按键无响应
*   卡顿、延迟
*   在个别软件中点击无响应
*   箭头在移入/移出虚拟机时跳跃
*   箭头会跳跃到从虚拟机移出的位置

可以先卸载软件包 [xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse) 试试看。

为解决[鼠标箭头跳跃到从虚拟机移出的位置](https://forums.mageia.org/en/viewtopic.php?f=7&t=7977)的问题，可以试试在 `.vmx` 配置文件里写入这些：

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx` 
```
mouse.vusb.enable = "TRUE"
mouse.vusb.useBasicMouse = "FALSE"
```

VMware 还会为游戏做自动的鼠标优化。如果这一优化产生了问题，可以在这里将其禁用：*Edit > Preferences > Input > Optimize mouse for games: Never*

再者，尝试在 `60-libinput.conf` 里[禁用](http://www.spinics.net/lists/xorg/msg53932.html) `catchall` 事件也可能有用:

 `/usr/share/X11/xorg.conf.d/60-libinput.conf` 
```
#Section "InputClass"
#        Identifier "libinput pointer catchall"
#        MatchIsPointer "on"
#        MatchDevicePath "/dev/input/event*"
#        Driver "libinput"
#EndSection

```

### 启动故障

#### 启动速度慢

如果 VMware 开启了内存热扩容功能，那么有可能会出现如下错误：

*   add_memory failed
*   acpi_memory_enable_device() error

若要禁用内存热扩容功能，可以在 `.vmx` 配置文件里写入 `mem.hotadd = "FALSE"`。

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx`  `mem.hotadd = "FALSE"` 

#### 关机/重启时卡住不动

试着降低 vmtoolsd 服务的超时阈值（默认是 90 秒）：

 `/etc/systemd/system/vmtoolsd.service.d/timeout.conf` 
```
[Service]
TimeoutStopSec=1
```

### 窗口分辨率自动适配

自动适配的意思是，当你在宿主机里缩放 VMware 窗口之后，Arch 作为客户机系统，应该自动根据主系统窗口的新尺寸来调整分辨率。

#### 方案 1

确保在设置里开启了自动适配。

VMware Worksation 的这一设置位于：*View -> Autosize -> Autofit Guest*

#### 方案 2

分辨率自动适配的功能依赖 [gtkmm](https://www.archlinux.org/packages/?name=gtkmm) 和 [gtk2](https://www.archlinux.org/packages/?name=gtk2) 软件包。确保客户机里装上这两个包。如果你没安装 X，或者你使用的桌面环境不依赖 GTK（比如 KDE），那么你需要手动安装这两个包。

#### 方案 3

通过 mkinitcpio.conf 加载以下模块：

 `/etc/mkinitcpio.conf`  `MODULES="vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx"` 

然后运行：

 `# mkinitcpio -p linux` 

再重启试试看。

#### 方案 4

[启用](/index.php/%E5%90%AF%E7%94%A8 "启用") `vmtoolsd.service`.

### 拖拽与复制粘贴

**Tip:** 由于与 *gtkmm3* 的依赖关系没有明确声明导致该功能无法正常使用。此问题在 [FS#43159](https://bugs.archlinux.org/task/43159)有详述。

为了确保拖拽与复制粘贴功能正常工作，需要安装 [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) 和 [gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3) 这两个包。

使 `vmware-user` 在 [X11](/index.php/X11 "X11") 之后运行：

*   确保 `etc/xdg/autostart/vmware-user.desktop` 存在，如果文件不存在，请运行：

```
# cp /etc/vmware-tools/vmware-user.desktop /etc/xdg/autostart/vmware-user.desktop

```

或

*   添加 `vmware-user` 到 [Xinitrc](/index.php/Xinitrc "Xinitrc")

### 在 VMware Workstation 11 版上运行共享 VM

Workstation 11 有个 bug：当 Arch 客户机以共享 VM 模式运行，且启动了 vmtoolsd 服务时，vmware-hostd 会崩溃。open-vm-tools 有个补丁来[绕过](https://github.com/vmware/open-vm-tools/issues/31)这一问题。

### 系统更新后共享文件夹没有被挂载

这个问题基本上只会在 [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) 出现。 自从 `vmhgfs` 模块属于 [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) 以后，使用 `pacman -Syu` 命令并不会升级传统的文件系统驱动。 因此在升级官方仓库之前应该手动升级 [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) 。

如果在系统升级之后共享文件夹没有被挂载，则删除共享文件系统自动挂载，升级 [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) 后执行 `pacman -Syu` ，最后执行 `mkinitcpio -p linux`。不要忘记恢复文件系统自动挂载。