## Contents

*   [1 配置笔记本电脑](#.E9.85.8D.E7.BD.AE.E7.AC.94.E8.AE.B0.E6.9C.AC.E7.94.B5.E8.84.91)
*   [2 电源管理](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
    *   [2.1 Power saving](#Power_saving)
    *   [2.2 电池状态监控程序](#.E7.94.B5.E6.B1.A0.E7.8A.B6.E6.80.81.E7.9B.91.E6.8E.A7.E7.A8.8B.E5.BA.8F)
    *   [2.3 Thinkpad电池管理](#Thinkpad.E7.94.B5.E6.B1.A0.E7.AE.A1.E7.90.86)
    *   [2.4 Cpufrequtils](#Cpufrequtils)
    *   [2.5 Pm-utils](#Pm-utils)
    *   [2.6 Lapsus](#Lapsus)
    *   [2.7 Install PowerTOP](#Install_PowerTOP)
    *   [2.8 Laptop mode tools](#Laptop_mode_tools)
    *   [2.9 PCIe ASPM](#PCIe_ASPM)
    *   [2.10 Suggestions for saving power](#Suggestions_for_saving_power)
        *   [2.10.1 Disk-related tweaks](#Disk-related_tweaks)
        *   [2.10.2 硬盘停转问题](#.E7.A1.AC.E7.9B.98.E5.81.9C.E8.BD.AC.E9.97.AE.E9.A2.98)
*   [3 触摸板](#.E8.A7.A6.E6.91.B8.E6.9D.BF)
*   [4 Special Buttons](#Special_Buttons)
*   [5 硬盘冲击保护](#.E7.A1.AC.E7.9B.98.E5.86.B2.E5.87.BB.E4.BF.9D.E6.8A.A4)

## 配置笔记本电脑

本文链接到很多其它页面，它们包含把笔记本电脑配置为最佳体验所需的配置。配置笔记本电脑大体上和配置台式机相同，然而，还是会有一些差别。当在笔记本电脑上安装Arch Linux时，下面几项是需要注意的：

*   [#电源管理](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)。电量消耗（怎么尽量延长电池续航时间）？
    *   [#待机休眠](#.E5.BE.85.E6.9C.BA.E4.BC.91.E7.9C.A0)。如何使笔记本电脑进入待机和休眠状态？
    *   [#硬盘停转](#.E7.A1.AC.E7.9B.98.E5.81.9C.E8.BD.AC.E9.97.AE.E9.A2.98)。在计算机不活动多长时间以后，使硬盘停转？
    *   关闭屏幕。在计算机不活动多长时间以后，关闭屏幕？（不只是启动屏保，而是完全关闭屏幕）

*   屏幕亮度。如何调节屏幕亮度？
*   无线网络。如何配置和连接无线网络？无线网络问题参见[Wireless Setup (简体中文)](/index.php/Wireless_Setup_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless Setup (简体中文)").
*   多功能键。配置详见[Extra keyboard keys (简体中文)](/index.php/Extra_keyboard_keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Extra keyboard keys (简体中文)").
*   [#触摸板](#.E8.A7.A6.E6.91.B8.E6.9D.BF)。如何配置触摸板（Synaptics或Alps）的灵敏度、加速、键位功能、滚动条？
*   [#硬盘冲击保护](#.E7.A1.AC.E7.9B.98.E5.86.B2.E5.87.BB.E4.BF.9D.E6.8A.A4)

在你配置笔记本电脑时，这几项内容都是很关键的。幸运的是，Arch Linux提供了所需的软件工具。下文重点讲述这些软件，并附以适当的提示和教程。

注意：下面的链接可能对你有用：

*   [http://www.linux-on-laptops.com/](http://www.linux-on-laptops.com/)
*   [http://www.linlap.com/](http://www.linlap.com/)

## 电源管理

如果想充分利用电池容量，电源管理是非常重要的。下列工具能帮助延长电池寿命，并保持你笔记本电脑的低温和静音。

### Power saving

请阅读 [power saving](/index.php/Power_saving "Power saving").

### 电池状态监控程序

电池状态当然可以从终端用 acpi 读取。安装Acpi用这条命令

```
# pacman -S acpi

```

有一个简单的能驻留在系统托盘的电池监控程序：[batterymon](https://aur.archlinux.org/packages.php?ID=24694)，可以在[AUR](/index.php/AUR "AUR")中找到。

### Thinkpad电池管理

参见这篇文章 [tp_smapi](/index.php/Tp_smapi "Tp smapi").

### Cpufrequtils

[CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")依据当前系统载荷及电源方案，使CPU加速或降速。快速简易的安装。

### Pm-utils

[Pm-utils](/index.php/Pm-utils "Pm-utils") 提供系统挂起和电量状态的配置框架，Pm-utils 可以配合 cpufrequtils 以提供完整的电源管理解决方案。

### Lapsus

[Lapsus](/index.php/ASUS_G1#The_Lapsus_daemon_.26_KDE_applet "ASUS G1") 是一组程序，它们便于对多种笔记本电脑的功能进行控制。目前它支持华硕笔记本电脑内核模块（由ACPIAsus项目提供）的大部分功能，比如额外的LED屏、快捷键、背光控制等。它也通过IBM ThinkPad ACPI Extras Driver 和 NVRAM设备 支持一些IBM笔记本电脑的特性。

### Install PowerTOP

[PowerTOP](http://www.lesswatts.org/projects/powertop/) is a handy utility from Intel that displays which hardware/processes are using the most power on your system, and provides instructions on how to stop or remove power-wasting services. Works great for mobile Intel CPUs; provides the current CPU state and suggestions for power saving. Also works on AMD systems, but does not provide as much information about the CPU state. Install with:

```
# pacman -S powertop

```

### Laptop mode tools

从aur中安装[laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/) ，使用参看 [Laptop Mode Tools](/index.php/Laptop_Mode_Tools_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Laptop Mode Tools (简体中文)") 。

### PCIe ASPM

On some laptops, powertop suggests enabling the CONFIG_PCIEASPM kernel option. It can be found unter "Bus options (PCI etc.)"->"PCI Express ASPM support". This option is marked as experimental in the current kernel (2.6.35) and allows the PCIe links to enter a power saving state.

According to [[1]](http://www.lesswatts.org/projects/devices-power-management/pcie.php), this option might degrade performance a bit, but on an Acer 3820TG laptop, it can reduce power consumption by about one third or even more.

More experience with this setting would be appreciated, so please share them [here](https://bbs.archlinux.org/viewtopic.php?id=107173)!

It seems like the option is going to be enabled by default in kernel 2.6.36; if so, the information here will be obsolete soon.

### Suggestions for saving power

*Note:* Not only are these not needed if using laptop-mode-tools, but using laptopmode also gives you the benefit of applying them only when desired (ie, while the AC cable is unplugged).

#### Disk-related tweaks

Disable file access time: every time you access (read) a file the filesystem writes an access time to the file metadata. You can disable this on individual files by using the chattr command, or you can enable it on an entire disk by setting the *noatime* option in your fstab, as follows:

```
/dev/sda1          /          ext3          defaults,noatime          1  2

```

[Source](http://www.faqs.org/docs/securing/chap6sec73.html)

	*Note*: disabling atime causes troubles with [mutt](/index.php/Mutt "Mutt") and other applications that make use of file timestamps. Consider compromising between performance and compatibility by using mount option relatime instead, or look into [mutt work-around for noatime](http://wiki.mutt.org/?MaildirFormat).

To allow the CD/DVD rom to spin down after a while, run the following:

```
/usr/bin/hal-disable-polling --device /dev/scd0

```

#### 硬盘停转问题

Documented [here](https://bugs.launchpad.net/ubuntu/+source/acpi-support/+bug/59695)

To prevent your laptop hard drive from spinning down too often (result of too aggressive APM defaults) do the following:

Add the following to */etc/rc.local*

```
hdparm -B 254 /dev/sdX *where X is your hard drive device*

```

You can also set it to 255 to completely disable spinning down. You may wish to set a lower value if you move your laptop around as lower values park the heads more often and reduce the chance of damage to your hard disk while it is being moved. If you don't move your laptop at all when you are using it, then 255 or 254 is probably best. If you do, then you might want to try a lower value. A value like 128 might be a good middle-ground.

Add the following to */etc/pm/sleep.d/50-hdparm_pm*

```
#!/bin/sh

if [ -n "$1" ] && ([ "$1" = "resume" ] || [ "$1" = "thaw" ]); then
	hdparm -B 254 /dev/your-hard-drive > /dev/null
fi

```

and run "chmod +x /etc/pm/sleep.d/50-hdparm_pm" to make sure it resets after suspend. Again, you can change the value 254 as you see fit.

Now the APM level should be set for your hard drive.

For some laptops, the option -S to hdparm can also be relevant (sets the spindown time for the drive). Note that all these options can also be configured using the [laptop-mode tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools"). This will allow you to set a high value when on AC and a lower value when you are running on battery power.

## 触摸板

To get your touchpad working properly, see the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") page. Note that your laptop may have an ALPS touchpad (such as the DELL Inspiron 6000), and not a Synaptics touchpad. In either case, see the link above.

## Special Buttons

To configure any special keys or buttons on your laptop, please refer to the [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") page.

## 硬盘冲击保护

There are several laptops from different vendors featuring shock protection capabilities. As manufacturers have refused to support open source development of the required software components so far, Linux support for shock protection varies considerably between different hardware implementations.

Currently, only one project, named HDAPS, support this kind of protection, which is prepared for IBM/Lenovo Thinkpads.

Just Check [Hard Disk Active Protection System](/index.php/HDAPS "HDAPS").