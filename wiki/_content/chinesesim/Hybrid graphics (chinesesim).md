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

### 完全关闭独立显卡

你可能为了节约电量而希望关闭高性能图形处理器，你可以通过安装 [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) 包来实现。

**Tip:** 对于内核不是[Official repositories (简体中文)](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的用户, [acpi_call-dkms](https://www.archlinux.org/packages/?name=acpi_call-dkms) 是代替方案. 参见 [DKMS](/index.php/DKMS "DKMS")。

安装后加载内核模块：

```
# modprobe acpi_call

```

加载内核模块后执行以下命令：

```
# /usr/share/acpi_call/examples/turn_off_gpu.sh

```

此脚本将遍历所有已知数据总线并尝试将其关闭。您将获得类似于以下内容的输出：

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

看到“works!”了么？这意味着脚本找到了一个GPU所在的总线，现在它已经关闭了芯片。要确认这一点，您的电池剩余时间应该会增加。目前，芯片将在下次重启时重新启动，要解决此问题我们需要执行以下操作：

**Note:** 只需要重启就可以重新启用GPU。

将内核模块添加到模块列表以在引导时加载:

 `/etc/modules-load.d/acpi_call.conf` 
```
#Load 'acpi_call.ko' at boot.

acpi_call
```

要在启动时关闭GPU，我们可以运行上面的脚本，但老实说这不是很优雅，所以我们可以使用systemd的tmpfiles。

 `/etc/tmpfiles.d/acpi_call.conf` 
```

w /proc/acpi/call - - - - \\_SB.PCI0.PEG0.PEGP._OFF
```

上面的配置将由systemd在启动时加载。它的作用是将特定的OFF信号写入 `/proc/acpi/call` 文件。显然，需要将 `\_SB.PCI0.PEG0.PEGP._OFF` 替换为适用于您系统的那个（请注意您需要转义反斜杠）。

**Tip:** 如果您在禁用GPU后遇到休眠或暂停系统的问题，请尝试通过发送相应的acpi_call再次启用它。参加：[使用服务文件](/index.php/Power_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E6.9C.8D.E5.8A.A1.E6.96.87.E4.BB.B6 "Power management (简体中文)").