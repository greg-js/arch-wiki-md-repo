**KVM**（英文Kernel-based Virtual Machine的缩写）是内核内建的虚拟机。有点类似于 [Xen](/index.php/Xen "Xen") ，但更追求更简便的运作，比如运行此虚拟机，仅需要加载相应的 `kvm` 模块即可后台待命。和 Xen 的完整模拟不同的是，KVM 需要芯片支持虚拟化技术（英特尔的 VT 扩展或者 AMD 的 AMD-V 扩展）。

在KVM中，可以运行各种未更改的GNU/Linux, Windows 或任何其他系统镜像。(请看[客户机支持状态](http://www.linux-kvm.org/page/Guest_Support_Status))，每个虚拟机都可提供独享的虚拟硬件：网卡，硬盘，显卡等。请看 [KVM Howto](http://www.linux-kvm.org/page/HOWTO)

KVM, Xen, VMware, 和 QEMU 的不同，请看这里[KVM FAQ](http://www.linux-kvm.org/page/FAQ#What_is_the_difference_between_kvm_and_Xen.3F).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 检查是否支持KVM](#检查是否支持KVM)
    *   [1.1 硬件支持](#硬件支持)
    *   [1.2 内核支持](#内核支持)
*   [2 准虚拟化(使用VIRTIO)](#准虚拟化(使用VIRTIO))
    *   [2.1 内核支持](#内核支持_2)
    *   [2.2 准虚拟化设备列表](#准虚拟化设备列表)
*   [3 如何使用KVM](#如何使用KVM)
*   [4 小贴士与小技巧](#小贴士与小技巧)
    *   [4.1 嵌套虚拟化](#嵌套虚拟化)

## 检查是否支持KVM

### 硬件支持

KVM需要虚拟机宿主（host）的处理器带有虚拟化支持（对于Intel处理器来说是VT-x，对于AMD处理器来说是AMD-V）。你可以通过以下命令来检查你的处理器是否支持虚拟化：

```
$ LC_ALL=C lscpu | grep Virtualization

```

或者： $ grep -E --color=auto 'vmx|svm|0xc0f' /proc/cpuinfo 如果运行后没有显示，那么你的处理器**不**支持硬件虚拟化，你**不能**使用KVM。

**注意:** 您可能需要在BIOS中启用虚拟化支持

### 内核支持

Arch Linux的内核提供了相应的[内核模块](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)")来支持KVM。

*   你可以通过以下命令来检查你的内核是否已经包含了支持虚拟化所必须的模块（`kvm`及`kvm_amd`与`kvm_intel`这两者中的任意一个）：

```
$ zgrep CONFIG_KVM /proc/config.gz

```

如果模块设置不为 `y`或`m`,则该模块**不**可用

*   然后确认这些内核模块是否已自动加载：

```
$ lsmod | grep kvm

```

如果运行后没有显示，那么需要[手动加载](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#手动加载卸载 "Kernel modules (简体中文)")这些模块。

## 准虚拟化(使用VIRTIO)

准虚拟化为客户机提供了一种使用主机上设备的快速有效的通信方式。KVM使用Virtio API作为虚拟机管理程序和客户机之间的连接层，为虚拟机提供准虚拟化设备（亦称Virtio设备）。 所有Virtio设备都包括两部分：主机设备和客户机驱动程序。

### 内核支持

*   用以下命令检查VIRTIO模块是否可用:

```
$ zgrep VIRTIO /proc/config.gz

```

*   检查VIRTIO模块是否已经自动加载:

```
$ lsmod | grep virtio

```

如果运行后没有显示，那么需要[手动加载](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#手动加载卸载 "Kernel modules (简体中文)")这些模块。

**Tip:** 如果 `kvm_intel` 或 `kvm_amd` 加载失败但是`kvm` 加载成功， (`lscpu`可检查硬件支持情况)检查你的BIOS设置。一些品牌机 (尤其时笔记本电脑) 默认关闭了这个功能，请确保是否是硬件支持该功能，但在BIOS中它被关闭了，在`dmesg`的提示信息中会展示出相关的警告信息。

### 准虚拟化设备列表

*   网络设备 (virtio-net)
*   硬盘设备 (virtio-blk)
*   控制器设备 (virtio-scsi)
*   串口设备 (virtio-serial)
*   气球设备 (virtio-balloon)

## 如何使用KVM

请参考[QEMU](/index.php/QEMU_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "QEMU (简体中文)")条目。

## 小贴士与小技巧

**注意:** 请参考[QEMU#Tips and tricks](/index.php/QEMU#Tips_and_tricks "QEMU")和[QEMU#Troubleshooting](/index.php/QEMU#Troubleshooting "QEMU")词条获取更多相关技巧。

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