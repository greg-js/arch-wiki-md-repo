Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")

来自[项目主页](http://linrunner.de/en/tlp/tlp.html):

	TLP在不需要您了解所有技术细节的情况下给您带来优秀的Linux高级电源管理方案。TLP默认带有对电池使用时间最优化的配置，所以你只需要安装即可享受延长的使用时间。不过，TLP也是高度可配置的以满足您的特定需求。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 只对Thinkpad有用的功能](#.E5.8F.AA.E5.AF.B9Thinkpad.E6.9C.89.E7.94.A8.E7.9A.84.E5.8A.9F.E8.83.BD)
*   [2 = 图形界面](#.3D_.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 Btrfs](#Btrfs)
    *   [3.2 Bumblebee及NVIDIA驱动](#Bumblebee.E5.8F.8ANVIDIA.E9.A9.B1.E5.8A.A8)
    *   [3.3 无线设备设置向导](#.E6.97.A0.E7.BA.BF.E8.AE.BE.E5.A4.87.E8.AE.BE.E7.BD.AE.E5.90.91.E5.AF.BC)
    *   [3.4 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C)
*   [4 调试](#.E8.B0.83.E8.AF.95)
*   [5 未包含的特性](#.E6.9C.AA.E5.8C.85.E5.90.AB.E7.9A.84.E7.89.B9.E6.80.A7)
*   [6 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

## 安装

从[官方源](/index.php/%E5%AE%98%E6%96%B9%E6%BA%90 "官方源")[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")[tlp](https://www.archlinux.org/packages/?name=tlp) - 注意它可能可以用于提供更佳的省电性能的可选依赖。

为了完成TLP的安装，您必须[启用systemd](/index.php/%E5%90%AF%E7%94%A8 "启用")服务`tl.service`以及`tlp-sleep.service`。您也应该[标记掉systemd](/index.php?title=%E6%A0%87%E8%AE%B0%E6%8E%89&action=edit&redlink=1 "标记掉 (page does not exist)")服务`systemd-rfkill.service`以及套接字`systemd-rfkill.socket`来防止冲突并保证TLP无线设备的开关选项的正确运行。

**注意:** 如果`NetworkManager.service`可用的话，`tlp.service` 将启动 `NetworkManager.service`；[FS#43733](https://bugs.archlinux.org/task/43733)。如果您使用不同的[网络管理器](/index.php/List_of_applications#Network_managers "List of applications")，编辑`tlp.service`来去除服务(line`Wants`)或[标记掉](/index.php?title=%E6%A0%87%E8%AE%B0%E6%8E%89&action=edit&redlink=1 "标记掉 (page does not exist)")它。

### 只对Thinkpad有用的功能

如果需要更优化的电池管理功能，比如充电阈值控制以及电池校准，安装下列软件包：

*   [tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) - 电池充电阈值控制，电池校准和特殊的tlp-stat输出需要tp-smapi。
*   [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) - 在Sandy Bridge及更新型号（X220/T420,X230/T430等）的电池充电阈值控制和电池校准需要acpi-call。

访问TLP问答板块 ["Which kernel module?"](http://linrunner.de/en/tlp/docs/tlp-faq.html#kernmod)以获取详情。

使用[threshy](https://aur.archlinux.org/packages/threshy/)及其Qt图形界面[threshy-gui](https://aur.archlinux.org/packages/threshy-gui/)可在不使用Root权限的情况下用D-Bus控制电池充电阈值。

## = 图形界面

[tlpui-git](https://aur.archlinux.org/packages/tlpui-git/)是用Python和GTK编写的TLP的图形界面。该软件还处于测试阶段。

## 配置

配置文件位于 `/etc/default/tlp` 并默认提供高度优化的省电方案。对选项的全部解释请访问:[TLP configuration](http://linrunner.de/en/tlp/docs/tlp-configuration.html)。

### Btrfs

为了防止Btrfs格式文件系统损坏，设置:

```
SATA_LINKPWR_ON_BAT=max_performance

```

这些链接与本主题的讨论有关： [Github bug report](https://github.com/linrunner/TLP/issues/128), [Reddit follow-up discussion](https://www.reddit.com/r/archlinux/comments/4f5xvh/saving_power_is_the_btrfs_dataloss_warning_still/)。

### Bumblebee及NVIDIA驱动

如果您与NVIDIA驱动一同运行[Bumblebee](/index.php/Bumblebee "Bumblebee")，您需要关闭TLP对GPU的电源管理以使Bumblebee控制GPU的电源。

运行`lspci`确定GPU的地址（以01:00.0为例），然后设置值：

```
RUNTIME_PM_BLACKLIST="01:00.0"

```

### 无线设备设置向导

无线设备设置向导可根据网络连接/断开事件进行更复杂的管理。它需要[[NetworkManager,{Pkg|tlp-rdw}}并需要启用`NetworkManager-dispatcher.service`。

详情请访问[TLP configuration](http://linrunner.de/en/tlp/docs/tlp-configuration.html#rdw)

### 命令行

TLP提供多个命令行工具。详情访问[TLP commands](http://linrunner.de/en/tlp/docs/tlp-linux-advanced-power-management.html#commands).

## 调试

下列命令可以显示目前使用模式（交流电/电池）以及应用的配置：

1.  tlp-stat

## 未包含的特性

*   风扇控制。访问[Fan speed control (简体中文)](/index.php/Fan_speed_control_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fan speed control (简体中文)")
*   亮度控制。访问[Backlight(简体中文)](/index.php?title=Backlight(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Backlight(简体中文) (page does not exist)")

## 相关链接

*   [TLP - Linux Advanced Power Management](http://linrunner.de/tlp) - 项目主页及文档。