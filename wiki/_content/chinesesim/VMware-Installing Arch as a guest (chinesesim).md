相关文章

*   [VMware](/index.php/VMware "VMware")
*   [Installing VMWare vCLI](/index.php/Installing_VMWare_vCLI "Installing VMWare vCLI")
*   [Installing Arch Linux in VMware (systemd)](/index.php/Installing_Arch_Linux_in_VMware_(systemd) "Installing Arch Linux in VMware (systemd)")

**翻译状态：** 本文是英文页面 [VMware/Installing Arch as a guest](/index.php/VMware/Installing_Arch_as_a_guest "VMware/Installing Arch as a guest") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-05，点击[这里](https://wiki.archlinux.org/index.php?title=VMware%2FInstalling+Arch+as+a+guest&diff=0&oldid=390024)可以查看翻译后英文页面的改动。

这篇文章是关于如何在[VMware](/index.php/VMware "VMware")产品，比如[Player (Plus)](http://www.vmware.com/products/player/)，[Fusion](http://www.vmware.com/products/fusion/)或[Workstation](http://www.vmware.com/products/workstation/)中安装ArchLinux。

## Contents

*   [1 编译进内核的驱动程序（模块）](#.E7.BC.96.E8.AF.91.E8.BF.9B.E5.86.85.E6.A0.B8.E7.9A.84.E9.A9.B1.E5.8A.A8.E7.A8.8B.E5.BA.8F.EF.BC.88.E6.A8.A1.E5.9D.97.EF.BC.89)
*   [2 VMware Tools 与 Open-VM-Tools 方案对比](#VMware_Tools_.E4.B8.8E_Open-VM-Tools_.E6.96.B9.E6.A1.88.E5.AF.B9.E6.AF.94)
*   [3 Open-VM-Tools](#Open-VM-Tools)
    *   [3.1 实用工具](#.E5.AE.9E.E7.94.A8.E5.B7.A5.E5.85.B7)
    *   [3.2 内核模块](#.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [3.3 安装](#.E5.AE.89.E8.A3.85)
        *   [3.3.1 多用户目标](#.E5.A4.9A.E7.94.A8.E6.88.B7.E7.9B.AE.E6.A0.87)
        *   [3.3.2 图形界面目标](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E7.9B.AE.E6.A0.87)
    *   [3.4 在窗口大小变动后自动重设分辨率](#.E5.9C.A8.E7.AA.97.E5.8F.A3.E5.A4.A7.E5.B0.8F.E5.8F.98.E5.8A.A8.E5.90.8E.E8.87.AA.E5.8A.A8.E9.87.8D.E8.AE.BE.E5.88.86.E8.BE.A8.E7.8E.87)
*   [4 VMware Tools](#VMware_Tools)
    *   [4.1 模块](#.E6.A8.A1.E5.9D.97)
    *   [4.2 安装（从客户机）](#.E5.AE.89.E8.A3.85.EF.BC.88.E4.BB.8E.E5.AE.A2.E6.88.B7.E6.9C.BA.EF.BC.89)
*   [5 Xorg 配置](#Xorg_.E9.85.8D.E7.BD.AE)
*   [6 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [6.1 通过 vmhgfs-fuse 共享目录](#.E9.80.9A.E8.BF.87_vmhgfs-fuse_.E5.85.B1.E4.BA.AB.E7.9B.AE.E5.BD.95)
        *   [6.1.1 fstab](#fstab)
        *   [6.1.2 Systemd](#Systemd)
    *   [6.2 3D加速](#3D.E5.8A.A0.E9.80.9F)
        *   [6.2.1 OpenGL 与 GLSL 支持](#OpenGL_.E4.B8.8E_GLSL_.E6.94.AF.E6.8C.81)
    *   [6.3 时间同步](#.E6.97.B6.E9.97.B4.E5.90.8C.E6.AD.A5)
        *   [6.3.1 与宿主机同步时间](#.E4.B8.8E.E5.AE.BF.E4.B8.BB.E6.9C.BA.E5.90.8C.E6.AD.A5.E6.97.B6.E9.97.B4)
        *   [6.3.2 与外部服务器同步时间](#.E4.B8.8E.E5.A4.96.E9.83.A8.E6.9C.8D.E5.8A.A1.E5.99.A8.E5.90.8C.E6.AD.A5.E6.97.B6.E9.97.B4)
    *   [6.4 Performance Tips](#Performance_Tips)
        *   [6.4.1 平行虚拟化 SCSI 驱动](#.E5.B9.B3.E8.A1.8C.E8.99.9A.E6.8B.9F.E5.8C.96_SCSI_.E9.A9.B1.E5.8A.A8)
        *   [6.4.2 平行虚拟化网络驱动](#.E5.B9.B3.E8.A1.8C.E8.99.9A.E6.8B.9F.E5.8C.96.E7.BD.91.E7.BB.9C.E9.A9.B1.E5.8A.A8)
        *   [6.4.3 虚拟机设置](#.E8.99.9A.E6.8B.9F.E6.9C.BA.E8.AE.BE.E7.BD.AE)
*   [7 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [7.1 鼠标问题](#.E9.BC.A0.E6.A0.87.E9.97.AE.E9.A2.98)
        *   [7.1.1 按钮丢失](#.E6.8C.89.E9.92.AE.E4.B8.A2.E5.A4.B1)
    *   [7.2 Boot problems](#Boot_problems)
        *   [7.2.1 Slow boot time](#Slow_boot_time)
        *   [7.2.2 Shutdown/Reboot hangs](#Shutdown.2FReboot_hangs)
    *   [7.3 Autofit problems](#Autofit_problems)
    *   [7.4 拖拽，复制/粘贴](#.E6.8B.96.E6.8B.BD.EF.BC.8C.E5.A4.8D.E5.88.B6.2F.E7.B2.98.E8.B4.B4)
    *   [7.5 Problems when running as a shared VM on Workstation 11](#Problems_when_running_as_a_shared_VM_on_Workstation_11)
    *   [7.6 Shared folder not mounted after system upgrade](#Shared_folder_not_mounted_after_system_upgrade)

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

以往，VMware Tools 方案所提供的网络与储存驱动是最好的，而且还带有时间同步等功能。然而网络与 SCSI 驱动这部分代码已经早就合入 Linux 内核了。VMware Tools 的优势只剩下 Unity mode 等附加功能。

VMware Tools 与 Open-VM-Tools 两个方案都需要额外安装软件包 [xf86-video-vmware](https://www.archlinux.org/packages/?name=xf86-video-vmware)。

## Open-VM-Tools

### 实用工具

[open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) 软件包里包括如下工具：

*   `vmtoolsd` - 负责汇报虚拟机状态的服务。
*   `vmware-checkvm` - 用于检测虚拟机中是否在运行着某程序的工具。
*   `vmware-toolbox-cmd` - 用于收集宿主系统信息的工具。
*   `vmware-user-suid-wrapper` - 用于实现宿主 / 客机系统间共享剪贴板。
*   `vmware-vmblock-fuse` - 文件系统。基于 [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (Filesystem in Userspace) 实现了宿主 / 客机之间拖拽文件。
*   `vmware-xferlogs` - 向虚拟机的日志文件输出日志与调试信息。
*   `vmhgfs-fuse` - 挂载 HGFS 共享目录的工具。

### 内核模块

[open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) 软件包里包含了如下内核模块：

*   `vmhgfs` - 旧有的 HGFS 驱动。这是传统的宿主机-客机间共享目录的方案。
*   `vmxnet` - 旧有的 VMXNET 网卡驱动。

### 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools) 软件包。

Open-VM-Tools 会从文件 `/etc/arch-release` 读取系统版本信息，但这个文件是空的。需要做如下的操作来满足它:

```
# cat /proc/version > /etc/arch-release

```

#### 多用户目标

**注意:** 对“目标”术语的解释见：[Systemd_(简体中文)#目标（target）](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.9B.AE.E6.A0.87.EF.BC.88target.EF.BC.89 "Systemd (简体中文)")

本小节的操作步骤可以帮你将系统启动至 `multi-user.target`。如果你想要启动至 `graphical.target` 那么请跳过本小节。

[启动服务](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") `vmtoolsd.service`。如果需要的话，也可以设置成开机自动启动。

#### 图形界面目标

如果你希望启动至 `graphical.target`，那么按照如下步骤配置：

```
# 将 vmware-vmblock-fuse.service 设置成开机自启动
systemctl enable vmware-vmblock-fuse.service

```

如果你还安装了 [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/)，那么你还需要将 `dkms.service` 这个 Systemd 服务也设置成开机自启动。这个服务会在每次内核更新之后自动重新编译内核模块。

如果 [gtkmm](https://www.archlinux.org/packages/?name=gtkmm) 不能正常工作，可以试试手动安装它。

### 在窗口大小变动后自动重设分辨率

按照这里：[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1081629#p1081629) 的步骤，在登录到 X 会话之后，启动 `/usr/bin/vmware-user-suid-wrapper`。

## VMware Tools

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

安装依赖项：[base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)（用于编译模块），[net-tools](https://www.archlinux.org/packages/?name=net-tools)（提供 `ifconfig` 供安装程序调用）和 [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) (提供内核头文件)。

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

从 [opem-vm-tools](https://www.archlinux.org/packages/?name=opem-vm-tools) 中拷贝并启用 `vmware-vmblock-fuse` 服务：

```
 # pacman -S asp
 # asp checkout open-vm-tools
 # cp open-vm-tools/trunk/vmware-* /usr/lib/systemd/system
 # systemctl enable vmware-vmblock-fuse.service

```

重新启动虚拟机：

```
# systemctl reboot

```

登录并启动 VMware Tools:

```
# /etc/init.d/rc6.d/K99vmware-tools start

```

**Tip:** 在 GitHub 上有个项目 [[2]](https://github.com/rasa/vmware-tools-patches) 尝试将这些步骤全自动处理。

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

然后[激活](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") `<shared folders root directory>-<shared_folder>.service` 这个挂载服务。

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

### Performance Tips

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

## 疑难解答

### 鼠标问题

鼠标可能会发生这些问题：

*   The automatic grab/ungrab feature will not automatically grab input when cursor enters the window
*   输入延迟
*   Clicks are not registered in some applications
*   当光标进入/离开虚拟机时跳动
*   光标跳转到它离开VM客户机的地方

您可以尝试卸载[xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse)。[xf86-input-vmmouse](https://www.archlinux.org/packages/?name=xf86-input-vmmouse)和[xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)足以处理鼠标与键盘输入。

您可以尝试添加这些设置到`.vmx`配置文件([光标跳转到它离开VM客户机的地方](https://forums.mageia.org/en/viewtopic.php?f=7&t=7977)):

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx` 
```
mouse.vusb.enable = "TRUE"
mouse.vusb.useBasicMouse = "FALSE"
usb.generic.allowHID = "TRUE"

VMware attempts to automatically optimize mouse for gaming. If experiencing problems, disabling it is recommended: *Edit > Preferences > Input > Optimize mouse for games: Never*
```

Alternatively, attempting to [disable](http://www.spinics.net/lists/xorg/msg53932.html) the `catchall` event in `10-evdev.conf` may be needed:

 `/etc/X11/xorg.conf.d/10-evdev.conf` 
```
#Section "InputClass"
#        Identifier "evdev pointer catchall"
#        MatchIsPointer "on"
#        MatchDevicePath "/dev/input/event*"
#        Driver "evdev"
#EndSection

```

#### 按钮丢失

If not by default, all mouse buttons should be working after adding `[mouse.vusb.useBasicMouse = "FALSE"](https://communities.vmware.com/thread/457313?start=15&tstart=0)` to the `.vmx`.

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx`  `mouse.vusb.useBasicMouse = "FALSE"` 

### Boot problems

#### Slow boot time

You may see the following errors if VMWare's memory hot-add feature is enabled.

*   add_memory failed
*   acpi_memory_enable_device() error

Disable the memory hot-add feature by setting `mem.hotadd = "FALSE"` to the `.vmx`.

 `~/vmware/*<Virtual Machine name>*/*<Virtual Machine name>*.vmx`  `mem.hotadd = "FALSE"` 

#### Shutdown/Reboot hangs

Adjust the timeout for the vmtoolsd service (defaults to 90 seconds).

 `/etc/systemd/system/vmtoolsd.service.d/timeout.conf` 
```
[Service]
TimeoutStopSec=1
```

### Autofit problems

If VMWare is stretching instead of changing the resolution even with the system service enabled, you may need to add the modules to mkinitcpio.conf.

 `/etc/mkinitcpio.conf`  `MODULES="vsock vmw_vsock_vmci_transport vmw_balloon vmw_vmci vmwgfx"` 

Do not forget to run:

 `# mkinitcpio -p linux` 

### 拖拽，复制/粘贴

`/etc/xdg/autostart/vmware-user.desktop` may try to start *vmware-user-suid-wrapper* properly when you log in, but there is an unspecified relationship between it and *gtkmm* that causes it to silently fail. This is documented in [FS#43159](https://bugs.archlinux.org/task/43159).

### Problems when running as a shared VM on Workstation 11

Workstation 11 has a bug where vmware-hostd crashes if an Arch guest is running as a shared VM and vmtoolsd is running in the guest. A patch to open-vm-tools to work around the bug is [here](https://github.com/vmware/open-vm-tools/issues/31).

### Shared folder not mounted after system upgrade

This is probably only happens to [open-vm-tools](https://www.archlinux.org/packages/?name=open-vm-tools). Since the vmhgfs module belongs to [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) which belongs to AUR repositiory, therefore would not get's updated automatically by the `pacman -Syu` command. Always update the [open-vm-tools-dkms](https://aur.archlinux.org/packages/open-vm-tools-dkms/) manually before the system upgrade.

If you happened to get in to this situation, you need to remove the automount for shared file system, upgrade and do a `mkinitcpio -p linux`.