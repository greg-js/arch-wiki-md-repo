**KVM**（Kernel-based Virtual Machine的英文缩写）是内核内建的虚拟机。有点类似于 [Xen](/index.php/Xen "Xen") ，但更追求更简便的运作，比如运行此虚拟机，仅需要加载相应的 `kvm` 模块即可后台待命。和 Xen 的完整模拟不同的是，KVM 需要芯片支持虚拟化技术（英特尔的 VT 扩展或者 AMD 的 AMD-V 扩展）。

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

首先检查内核模块是否已经自动加载，This should be the case with recent versions of [udev](/index.php/Udev "Udev").

```
$ lsmod | grep kvm
$ lsmod | grep virtio

```

上面的命令如果没有返回内容，那么你需要[Kernel_modules_(简体中文) #手动加载卸载](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.89.8B.E5.8A.A8.E5.8A.A0.E8.BD.BD.E5.8D.B8.E8.BD.BD "Kernel modules (简体中文)") 内核模块。

**Tip:** 如果 `kvm_intel` 或 `kvm_amd` 加载失败但是`kvm` 加载成功， (`lscpu`可检查硬件支持情况)检查你的BIOS设置。一些品牌机 (尤其时笔记本电脑) 默认关闭了这个功能，请确保是否是硬件支持该功能，但在BIOS中它被关闭了，在`dmesg`的提示信息中会展示出相关的警告信息。

### List of para-virtualized devices

*   network device (virtio-net)
*   block device (virtio-blk)
*   controller device (virtio-scsi)
*   serial device (virtio-serial)
*   balloon device (virtio-balloon)

## 如何使用KVM

请参考[QEMU](/index.php/QEMU_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "QEMU (简体中文)")条目。

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