**翻译状态：** 本文是英文页面 [Laptop](/index.php/Laptop "Laptop") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-13，点击[这里](https://wiki.archlinux.org/index.php?title=Laptop&diff=0&oldid=491765)可以查看翻译后英文页面的改动。

本文是笔记本索引页面，包括很多到其它页面的链接，以帮助用户将笔记本电脑配置为最佳体验。配置笔记本电脑大体上和配置台式机相同，但仍然存在一些关键的区别。Arch Linux 提供了完成这些配置所需的软件工具。下文重点讲述这些软件，并附以适当的提示和教程。

下面的厂商专页包含具体笔记本型号需要注意的地方。

| [Laptop main page](/index.php/Laptop "Laptop") |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") (discontinued) - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other") |

如果某个笔记本需要特殊的操作，会在厂商页面提供链接，如果找不到您的型号，可以参考 [Category:Laptops](/index.php/Category:Laptops "Category:Laptops") 中的相似型号。

## Contents

*   [1 电源管理](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
    *   [1.1 电池状态](#.E7.94.B5.E6.B1.A0.E7.8A.B6.E6.80.81)
        *   [1.1.1 ACPI](#ACPI)
        *   [1.1.2 低电量时自动休眠](#.E4.BD.8E.E7.94.B5.E9.87.8F.E6.97.B6.E8.87.AA.E5.8A.A8.E4.BC.91.E7.9C.A0)
            *   [1.1.2.1 Testing events](#Testing_events)
    *   [1.2 挂起和休眠](#.E6.8C.82.E8.B5.B7.E5.92.8C.E4.BC.91.E7.9C.A0)
    *   [1.3 硬盘停转问题](#.E7.A1.AC.E7.9B.98.E5.81.9C.E8.BD.AC.E9.97.AE.E9.A2.98)
    *   [1.4 Modify wake events](#Modify_wake_events)
    *   [1.5 Cpufrequtils](#Cpufrequtils)
*   [2 硬件支持](#.E7.A1.AC.E4.BB.B6.E6.94.AF.E6.8C.81)
    *   [2.1 屏幕亮度](#.E5.B1.8F.E5.B9.95.E4.BA.AE.E5.BA.A6)
    *   [2.2 触摸板](#.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [2.3 Fingerprint Reader](#Fingerprint_Reader)
    *   [2.4 Webcam](#Webcam)
    *   [2.5 硬盘冲击保护](#.E7.A1.AC.E7.9B.98.E5.86.B2.E5.87.BB.E4.BF.9D.E6.8A.A4)
    *   [2.6 Hybrid graphics](#Hybrid_graphics)
*   [3 Network time syncing](#Network_time_syncing)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 电源管理

**注意:** 请先阅读[Power management](/index.php/Power_management "Power management")，本文介绍的是笔记本特有的功能设置。

如果想充分利用电池容量，电源管理是非常重要的。下列工具能帮助延长电池寿命，并保持你笔记本电脑的低温和静音。

### 电池状态

有多种方式可以读取电池状态，传统方法是用 ACPI 接口周期查询。在某些系统中，电池会在每消耗 1% 电量的时候发送 [udev](/index.php/Udev "Udev") 事件，可以用 udev 规则执行需要的操作。

安装Acpi用这条命令

```
# pacman -S acpi

```

有一个简单的能驻留在系统托盘的电池监控程序：[batterymon](https://aur.archlinux.org/packages.php?ID=24694)，可以在[AUR](/index.php/AUR "AUR")中找到。

#### ACPI

电池状态当然可以从终端用 acpi 读取。[acpi](https://www.archlinux.org/packages/?name=acpi) 软件包提供了 ACPI 命令行工具，详情请参考 [ACPI modules](/index.php/ACPI_modules "ACPI modules")。

*   [cbatticon](https://www.archlinux.org/packages/?name=cbatticon) 是常驻系统托盘的电池图标。
*   [batterymon-clone](https://aur.archlinux.org/packages/batterymon-clone/) 是常驻系统托盘的电池监控程序。
*   [batify](https://aur.archlinux.org/packages/batify/) 是一个通过充放电和电量变化 udev 规则文件触发的通知程序，支持 multi-x 会话。

#### 低电量时自动休眠

If your battery sends events to [udev](/index.php/Udev "Udev") whenever it (dis)charges by 1%, you can use this udev rule to automatically hibernate the system when battery level is critical, and thus prevent all unsaved work from being lost.

**Note:** Not all batteries report discharge events. Test by running `udevadm monitor --property` while on battery and see if any events are reported. You should wait at least 1% drop. If no events are reported and `/sys/class/power_supply/BAT0/alarm` is non-zero then the battery will likely trigger an event when `BAT0/energy_now` drops below the alarm value, and the udev rule will work as long as the percentage math works out. Some laptops have an option for this disabled in BIOS by default.
 `/etc/udev/rules.d/99-lowbat.rules` 
```
# Suspend the system when battery level drops to 5% or lower
SUBSYSTEM=="power_supply", ATTR{status}=="Discharging", ATTR{capacity}=="[0-5]", RUN+="/usr/bin/systemctl hibernate"

```

This rule will be repeated whenever the condition is set. As such, when resuming from hibernate when the battery is critical, the computer will hibernate directly. Some laptops do not boot beyond a certain battery level, so the rule could be adjusted accordingly.

Batteries can jump to a lower value instead of discharging continuously, therefore a udev string matching pattern for all capacities 0 through 5 is used.

Other rules can be added to perform different actions depending on power supply status and/or capacity.

If your system has no or missing ACPI events, use [cron](/index.php/Cron "Cron") with the following script:

```
#!/bin/sh
acpi -b | awk -F'[,:%]' '{print $2, $3}' | {
	read -r status capacity

	if [ "$status" = Discharging -a "$capacity" -lt 5 ]; then
		logger "Critical battery threshold"
		systemctl hibernate
	fi
}

```

##### Testing events

One way to test udev rules is to have them create a file when they are run. For example:

 `/etc/udev/rules.d/98-discharging.rules` 
```
SUBSYSTEM=="power_supply", ATTR{status}=="Discharging", RUN+="/usr/bin/touch /home/example/discharging"

```

This creates a file at `/home/example/discharging` when the laptop charger is unplugged. You can test whether the rule worked by unplugging your laptop and looking for this file. For more advanced udev rule testing, see [Udev#Testing rules before loading](/index.php/Udev#Testing_rules_before_loading "Udev").

### 挂起和休眠

根据笔记本的使用模式，手动将系统挂起到内存或磁盘是提高电池使用时间的最有效方法。请参阅 [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate")。

### 硬盘停转问题

Documented [here](https://bugs.launchpad.net/ubuntu/+source/acpi-support/+bug/59695).

To prevent your laptop hard drive from spinning down too often, set less aggressive power management as described in [hdparm#Power management configuration](/index.php/Hdparm#Power_management_configuration "Hdparm"). Even the default values may be too aggressive.

### Modify wake events

Events which cause the system to resume from [power states](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface#Power_states "w:Advanced Configuration and Power Interface") can be regulated in `/proc/acpi/wakeup`. Writing an entry from the *Device* column toggles the status from `enabled` to `disabled`, or vice-versa.

For example, to disable waking from suspend (S3) on opening the lid, run:

```
# echo LID > /proc/acpi/wakeup

```

This change can be made permanent with [tmpfiles.d(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5):

 `/etc/tmpfiles.d/disable-lid-wakeup.conf`  `w /proc/acpi/wakeup - - - - LID` 

### Cpufrequtils

[CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")依据当前系统载荷及电源方案，使CPU加速或降速。快速简易的安装。

## 硬件支持

### 屏幕亮度

参阅 [Backlight](/index.php/Backlight "Backlight").

### 触摸板

To get your touchpad working properly, see the [libinput](/index.php/Libinput "Libinput") page. [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") is the older input driver, which is currently in maintenance mode and is no longer updated.

### Fingerprint Reader

See [Fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui"), [fprint](/index.php/Fprint "Fprint") and [ThinkFinger](/index.php/ThinkFinger "ThinkFinger") (for ThinkPads).

### Webcam

See [Webcam setup](/index.php/Webcam_setup "Webcam setup").

### 硬盘冲击保护

There are several laptops from different vendors featuring shock protection capabilities. As manufacturers have refused to support open source development of the required software components so far, Linux support for shock protection varies considerably between different hardware implementations.

Currently, two projects, named [HDAPS](/index.php/HDAPS "HDAPS") and [Hpfall](/index.php/Hpfall "Hpfall") (available in the [AUR](/index.php/AUR "AUR")), support this kind of protection. HDAPS is for IBM/Lenovo Thinkpads and hpfall for HP/Compaq laptops.

### Hybrid graphics

The laptop manufacturers developed new technologies involving two graphic cards in an single computer, enabling both high performance and power saving usages. These laptops usually use an Intel chip for display by default, so an [Intel graphics](/index.php/Intel_graphics "Intel graphics") driver is needed first. Then you can [choose methods](/index.php/Hybrid_graphics "Hybrid graphics") to utilize the second graphics chip.

## Network time syncing

For a laptop, it may be a good idea to use [Chrony](/index.php/Chrony "Chrony") as an alternative to [NTPd](/index.php/NTPd "NTPd"), [OpenNTPD](/index.php/OpenNTPD "OpenNTPD") or [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") to sync your clock over the network. Chrony is designed to work well even on systems with no permanent network connection (such as laptops), and is capable of much faster time synchronisation than standard ntp. Chrony has several advantages when used in systems running on virtual machines, such as a larger range for frequency correction to help correct quickly drifting clocks, and better response to rapid changes in the clock frequency. It also has a smaller memory footprint and no unnecessary process wakeups, improving power efficiency.

## 参阅

	通用页面

*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") is a technology used primarily by notebooks which enables the OS to scale the CPU frequency up or down, depending on the current system load and/or power scheme.
*   [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling") describes how to automatically turn off the laptop screen after a specified interval of inactivity (not just blanked with a screensaver but completely shut off).
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") provides information about setting up wireless connection.
*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") describes configuration of Media keys.
*   [acpid](/index.php/Acpid "Acpid") which is a flexible and extensible daemon for delivering ACPI events.

	型号相关页面

*   See [Category:Laptops](/index.php/Category:Laptops "Category:Laptops") and its subcategories for pages dedicated to specific models/vendors.
*   Battery tweaks for ThinkPads can be found in [TLP](/index.php/TLP "TLP") and the [tp_smapi](/index.php/Tp_smapi "Tp smapi") article.
*   [acerhdf](/index.php/Acer_Aspire_One#acerhdf "Acer Aspire One") is a kernel module for controlling fan speed on Acer Aspire One and some Packard Bell Notebooks.

	外部资源

*   [http://www.linux-on-laptops.com/](http://www.linux-on-laptops.com/)
*   [http://www.linlap.com/](http://www.linlap.com/)