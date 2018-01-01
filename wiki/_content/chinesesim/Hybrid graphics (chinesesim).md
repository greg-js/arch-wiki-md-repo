**翻译状态：** 本文是英文页面 [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-10-21，点击[这里](https://wiki.archlinux.org/index.php?title=Hybrid+graphics&diff=0&oldid=454661)可以查看翻译后英文页面的改动。

混合图形技术是指在同一个计算机上使用多个显卡. 笔记本生产商在同一个计算机上使用两个显卡，具有不同的性能和电源消耗，混合图形技术通过控制两个显卡的使用情况实现高性能和低功耗两个目标。

不同的厂商有不同的混合显示解决方案，这个功能在 Windows 上支持的很好，但是在 Linux 上还只是实验性质。我们会简单的介绍各种方式和社区的支持情况。

## 第一代混合显示模式 (基本切换)

除非笔记本是十年前的产品，否则应该是使用的是动态切换模式。

第一代使用混合显示技术的笔记本用硬件多路复用 ([MUX](https://en.wikipedia.org/wiki/Multiplexer "wikipedia:Multiplexer"))的方式. 机器可以在低功耗和低性能的集成显卡和高功耗高性能的独立显卡之间进行切换。用户可以在启动或登陆时选择要使用哪个显卡，后面使用的时候就一直不变。基本的切换步骤:

*   关闭显示器
*   打开独立显卡
*   切换多路复用电路
*   关闭集成显卡
*   重新打开显示器

这种切换并不平滑，会出现屏幕闪烁或黑屏。后面的切换方式更加用户友好。

## 动态切换模式

2016 年生产的笔记本应该都是这个模式。新的混合显示技术也需要在不同的显卡之间切换，但是现在不再使用硬件多路复用的方式，而是通过一个帧缓存进行协调。集成显卡一直工作，独立显卡会根据显示的需要动态的开关。大部分情况下都无法只使用独立显卡，而且切换是由软件控制。

*   NV 的闭源驱动请参考 [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") 和 [Bumblebee](/index.php/Bumblebee "Bumblebee")
*   其它驱动，包括 NV Nouveau 开源驱动和 AMD Radeon 请参考 [PRIME](/index.php/PRIME "PRIME")

### Fully Power Down Discrete GPU

You may want to turn off the high-performance graphics processor to save battery power, this can be done by installing the [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) package.

**Tip:** For kernels not in the [Official repositories](/index.php/Official_repositories "Official repositories"), the [acpi_call-dkms](https://aur.archlinux.org/packages/acpi_call-dkms/) is an alternative. See also [DKMS](/index.php/DKMS "DKMS").

Once installed load the kernel module:

```
# modprobe acpi_call

```

With the kernel module loaded run the following:

```
# /usr/share/acpi_call/examples/turn_off_gpu.sh

```

This script will go through all the known data buses and attempt to turn them off. You will get an output similar to the following:

```
Trying \_SB.PCI0.P0P1.VGA._OFF: failed
Trying \_SB.PCI0.P0P2.VGA._OFF: failed
Trying \_SB_.PCI0.OVGA.ATPX: failed
Trying \_SB_.PCI0.OVGA.XTPX: failed
Trying \_SB.PCI0.P0P3.PEGP._OFF: failed
Trying \_SB.PCI0.P0P2.PEGP._OFF: failed
Trying \_SB.PCI0.P0P1.PEGP._OFF: failed
Trying \_SB.PCI0.MXR0.MXM0._OFF: failed
Trying \_SB.PCI0.PEG1.GFX0._OFF: failed
Trying \_SB.PCI0.PEG0.GFX0.DOFF: failed
Trying \_SB.PCI0.PEG1.GFX0.DOFF: failed
**Trying \_SB.PCI0.PEG0.PEGP._OFF: works!**
Trying \_SB.PCI0.XVR0.Z01I.DGOF: failed
Trying \_SB.PCI0.PEGR.GFX0._OFF: failed
Trying \_SB.PCI0.PEG.VID._OFF: failed
Trying \_SB.PCI0.PEG0.VID._OFF: failed
Trying \_SB.PCI0.P0P2.DGPU._OFF: failed
Trying \_SB.PCI0.P0P4.DGPU.DOFF: failed
Trying \_SB.PCI0.IXVE.IGPU.DGOF: failed
Trying \_SB.PCI0.RP00.VGA._PS3: failed
Trying \_SB.PCI0.RP00.VGA.P3MO: failed
Trying \_SB.PCI0.GFX0.DSM._T_0: failed
Trying \_SB.PCI0.LPC.EC.PUBS._OFF: failed
Trying \_SB.PCI0.P0P2.NVID._OFF: failed
Trying \_SB.PCI0.P0P2.VGA.PX02: failed
Trying \_SB_.PCI0.PEGP.DGFX._OFF: failed
Trying \_SB_.PCI0.VGA.PX02: failed

```

See the "works"? This means the script found a bus which your GPU sits on and it has now turned off the chip. To confirm this, your battery time remaining should have increased. Currently, the chip will turn back on with the next reboot to get around this we do the following:

**Note:** To turn the GPU back on just reboot.

Add the kernel module to the array of modules to load at boot:

 `/etc/modules-load.d/acpi_call.conf` 
```
#Load 'acpi_call.ko' at boot.

acpi_call
```

To turn off the GPU at boot we could just run the above script but honestly that is not very elegant so instead lets make use of systemd's tmpfiles.

 `/etc/tmpfiles.d/acpi_call.conf` 
```

w /proc/acpi/call - - - - \\_SB.PCI0.PEG0.PEGP._OFF
```

The above config will be loaded at boot by systemd. What it does is write the specific OFF signal to the `/proc/acpi/call` file. Obviously, replace the `\_SB.PCI0.PEG0.PEGP._OFF` with the one which works on your system (please note that you need to escape the backslash).

**Tip:** If you are experiencing trouble hibernating or suspending the system after disabling the GPU, try to enable it again by sending the corresponding acpi_call. See also [Suspend/resume service files](/index.php/Power_management#Suspend.2Fresume_service_files "Power management").