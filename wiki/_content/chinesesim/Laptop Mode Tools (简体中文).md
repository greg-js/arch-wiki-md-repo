**翻译状态：** 本文是英文页面 [Laptop_Mode_Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-12-25，点击[这里](https://wiki.archlinux.org/index.php?title=Laptop_Mode_Tools&diff=0&oldid=290267)可以查看翻译后英文页面的改动。

_[Laptop Mode Tools](http://samwel.tk/laptop_mode/) 是一个 Linux 系统下的笔记本电源管理软件。它是让内核开启笔记本电脑模式功能的主要方法，它会让硬盘降速。另外，它允许你通过一个简单的配置文件调整一些其他的节能相关的设置。_

与 [acpid](/index.php/Acpid "Acpid")、 [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")、 和 [pm-utils](/index.php/Pm-utils "Pm-utils") 结合，LMT 提供大多数用户一个完整的笔记本电脑电源管理方案。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 硬盘](#.E7.A1.AC.E7.9B.98)
        *   [2.1.1 固态硬盘](#.E5.9B.BA.E6.80.81.E7.A1.AC.E7.9B.98)
    *   [2.2 CPU 频率调节](#CPU_.E9.A2.91.E7.8E.87.E8.B0.83.E8.8A.82)
    *   [2.3 设备和总线](#.E8.AE.BE.E5.A4.87.E5.92.8C.E6.80.BB.E7.BA.BF)
        *   [2.3.1 Intel SATA](#Intel_SATA)
        *   [2.3.2 USB 自动休眠](#USB_.E8.87.AA.E5.8A.A8.E4.BC.91.E7.9C.A0)
    *   [2.4 显示和图形](#.E6.98.BE.E7.A4.BA.E5.92.8C.E5.9B.BE.E5.BD.A2)
        *   [2.4.1 LCD 显示器亮度](#LCD_.E6.98.BE.E7.A4.BA.E5.99.A8.E4.BA.AE.E5.BA.A6)
            *   [2.4.1.1 ThinkPad T40/T42](#ThinkPad_T40.2FT42)
            *   [2.4.1.2 ThinkPad T60](#ThinkPad_T60)
        *   [2.4.2 终端黑屏时间](#.E7.BB.88.E7.AB.AF.E9.BB.91.E5.B1.8F.E6.97.B6.E9.97.B4)
    *   [2.5 网络](#.E7.BD.91.E7.BB.9C)
        *   [2.5.1 以太网](#.E4.BB.A5.E5.A4.AA.E7.BD.91)
        *   [2.5.2 无线局域网](#.E6.97.A0.E7.BA.BF.E5.B1.80.E5.9F.9F.E7.BD.91)
    *   [2.6 音频设备](#.E9.9F.B3.E9.A2.91.E8.AE.BE.E5.A4.87)
        *   [2.6.1 AC97](#AC97)
        *   [2.6.2 Intel HDA](#Intel_HDA)
*   [3 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [3.1 Aliases](#Aliases)
    *   [3.2 lm-profiler](#lm-profiler)
    *   [3.3 Disabling](#Disabling)
*   [4 疑难问题](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98)
    *   [4.1 Laptop-mode-tools 不能收到事件](#Laptop-mode-tools_.E4.B8.8D.E8.83.BD.E6.94.B6.E5.88.B0.E4.BA.8B.E4.BB.B6)
    *   [4.2 连接电源后Laptop-mode-tools并没有停止](#.E8.BF.9E.E6.8E.A5.E7.94.B5.E6.BA.90.E5.90.8ELaptop-mode-tools.E5.B9.B6.E6.B2.A1.E6.9C.89.E5.81.9C.E6.AD.A2)
*   [5 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

## 安装

[laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/) 可以从 [AUR](/index.php/AUR "AUR") 中 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装")。

## 配置

配置是通过下列文件来控制的:

*   `/etc/laptop-mode/laptop-mode.conf` - 主要配置文件
*   `/etc/laptop-mode/conf.d/*` - 许多特定功能的模块.

每个模块都可以通过修改对应的`conf.d/*`文件中的`CONTROL_*`的值来启用或禁用。

如果在 `/etc/laptop-mode/laptop-mode.conf` 中设置了 `ENABLE_AUTO_MODULES`，LMT会自动启用那些`CONTROL_*`设为`auto`的模块。

下面的命令可以用来列出模块的启用配置（启用、禁用或自动）：

```
$ grep -r '^\(CONTROL\|ENABLE\)_' /etc/laptop-mode/conf.d

```

**注意:** `auto-hibernate.conf` 和 `battery-level-polling.conf` 例外地采用 `ENABLE_*` 变量而不是 `CONTROL_*`。

最后启用`laptop-mode`服务：

```
 # systemctl enable laptop-mode.service

```

### 硬盘

为了使用该功能您需要安装 hdparm 或者 sdparm。 查看 [Hdparm](/index.php/Hdparm "Hdparm").

通过 `hdparm -S` 命令来降低硬盘转速可以让计算机更省电同时更安静. 即是您正在使用电脑您依然可以使用磁盘预读功能让硬盘经常降低转速。LMT（笔记本电脑工具包）也可以使用`hdparm -B` 命令。硬盘省电级别最高（最省电）为1,最低是254,使用交流电源供电时默认为254,使用电池供电时默认为1。如果你觉得硬盘减速使得一些操作变慢的话，把它设置为一个高一点的值（比如128）是个好主意，这会让它不会太频繁的减速。 `hdparm -S` 和 `hdparm -B` 命令的一些参数设置在 `/etc/laptop-mode/laptop-mode.conf`文件中。

如果 `CONTROL_MOUNT_OPTIONS` 选项为 on (默认即为 on), laptop-mode-tools 会自动重新挂载你的分区, 并在挂载选项中增加了 'commit=600,noatime'。这会让磁盘日志程序jbd2每10分钟更新一次磁盘日志，而不是通常情况下的几秒钟更新一次 (注意：使用该设置你可能会丢掉前10分钟的工作成果（当系统意外关闭时）). 同时请确保不要使用 `atime` 的挂载参数, 使用 `noatime` 或 `relatime` 来替代。

**注意:** `CONTROL_MOUNT_OPTIONS` 的值不应该在nilfs2分区上被设置为 on (原因可查看 [https://bbs.archlinux.org/viewtopic.php?id=134656](https://bbs.archlinux.org/viewtopic.php?id=134656)) (也可以查看 [http://www.ibm.com/developerworks/cn/linux/l-cn-nilfs2/index.html](http://www.ibm.com/developerworks/cn/linux/l-cn-nilfs2/index.html) 对nilfs2文件系统的中文介绍)

#### 固态硬盘

来自 [官方上游 FAQ](http://samwel.tk/laptop_mode/faq):

**问题:**我电脑里装了一个固态硬盘，那么那些硬盘相关的配置还有效吗？

**回答:**它们有可能有效，原因有两个：1）laptop mode 会减少写次数，从而延长SSD的寿命；2）laptop mode 会让写操作变成突发形式，从而会使一些节电机制（例如ALPM）更好地介入。然而，效果可能会因硬件不同而有差别。有些硬件可能完全没效果，有些则效果显著。

### CPU 频率调节

使用该功能你需要安装调节CPU频率的驱动模块。 查看 [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

```
# cpufreq.conf
# ThinkPad T40/T42/T60 Example
#
CONTROL_CPU_FREQUENCY=1
BATT_CPU_MAXFREQ=fastest
BATT_CPU_MINFREQ=slowest
BATT_CPU_GOVERNOR=ondemand
BATT_CPU_IGNORE_NICE_LOAD=1
LM_AC_CPU_MAXFREQ=fastest
LM_AC_CPU_MINFREQ=slowest
LM_AC_CPU_GOVERNOR=ondemand
LM_AC_CPU_IGNORE_NICE_LOAD=1
NOLM_AC_CPU_MAXFREQ=fastest
NOLM_AC_CPU_MINFREQ=slowest
NOLM_AC_CPU_GOVERNOR=ondemand
NOLM_AC_CPU_IGNORE_NICE_LOAD=0
CONTROL_CPU_THROTTLING=0

```

### 设备和总线

#### Intel SATA

*   开启Intel SATA AHCI控制器的ALPM特性使磁盘空闲时让磁盘工作在非常低的功耗模式。

```
# intel-sata-powermgmt.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_INTEL_SATA_POWER=1
BATT_ACTIVATE_SATA_POWER=1
LM_AC_ACTIVATE_SATA_POWER=1
NOLM_AC_ACTIVATE_SATA_POWER=0

```

**Note:** 更多详细配置信息请参阅 `/etc/laptop-mode/conf.d/intel-sata-powermgmt.conf` 文件。

#### USB 自动休眠

```
# usb-autosuspend.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_USB_AUTOSUSPEND=1
BATT_SUSPEND_USB=1
LM_AC_SUSPEND_USB=1
NOLM_AC_SUSPEND_USB=0
AUTOSUSPEND_TIMEOUT=2

```

**注意:** 更多详细配置信息请参阅 `/etc/laptop-mode/conf.d/usb-autosuspend.conf` 文件。如果你有一个经常使用的USB设备（比如USB鼠标），把它们禁用可以防止它们自动休眠。

### 显示和图形

#### LCD 显示器亮度

*   可以通过以下命令来查看可用的笔记本电脑屏幕亮度数值:

```
$ cat /proc/acpi/video/VID/LCD/brightness

```

##### ThinkPad T40/T42

对于 [ThinkPad](http://en.wikipedia.org/wiki/ThinkPad) T40/T42 笔记本，最小和最大亮度的查看要通过以下命令:

```
$ cat /sys/class/backlight/acpi_video0/brightness
$ cat /sys/class/backlight/acpi_video0/max_brightness

```

```
# lcd-brightness.conf
# ThinkPad T40/T42 Example
#
DEBUG=0
CONTROL_BRIGHTNESS=1
BATT_BRIGHTNESS_COMMAND="echo 0"
LM_AC_BRIGHTNESS_COMMAND="echo 7"
NOLM_AC_BRIGHTNESS_COMMAND="echo 7"
BRIGHTNESS_OUTPUT="/sys/class/backlight/thinkpad_screen/brightness"

```

##### ThinkPad T60

*   对于 [ThinkPad](http://en.wikipedia.org/wiki/ThinkPad) T60 笔记本，最小和最大亮度的查看要通过以下命令:

```
$ cat /sys/class/backlight/thinkpad_screen/max_brightness
$ cat /sys/class/backlight/thinkpad_screen/brightness

```

```
# lcd-brightness.conf
# ThinkPad T60 Example
#
DEBUG=0
CONTROL_BRIGHTNESS=1
BATT_BRIGHTNESS_COMMAND="echo 0"
LM_AC_BRIGHTNESS_COMMAND="echo 7"
NOLM_AC_BRIGHTNESS_COMMAND="echo 7"
BRIGHTNESS_OUTPUT="/sys/class/backlight/acpi_video0/brightness"

```

**注意:** 更多配置细节请阅读 `/etc/laptop-mode/conf.d/lcd-brightness.conf` 文件。

#### 终端黑屏时间

```
# terminal-blanking.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_TERMINAL=1
TERMINALS="/dev/tty1"
BATT_TERMINAL_BLANK_MINUTES=1
BATT_TERMINAL_POWERDOWN_MINUTES=2
LM_AC_TERMINAL_BLANK_MINUTES=10
LM_AC_TERMINAL_POWERDOWN_MINUTES=10
NOLM_AC_TERMINAL_BLANK_MINUTES=10
NOLM_AC_TERMINAL_POWERDOWN_MINUTES=10

```

**注意:** 更多配置细节请参阅 `/etc/laptop-mode/conf.d/terminal-blanking.conf` 文件。

### 网络

#### 以太网

```
# ethernet.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_ETHERNET=1
LM_AC_THROTTLE_ETHERNET=0
NOLM_AC_THROTTLE_ETHERNET=0
DISABLE_WAKEUP_ON_LAN=1
DISABLE_ETHERNET_ON_BATTERY=1
ETHERNET_DEVICES="eth0"

```

#### 无线局域网

无线网络设备的电源管理是设备相关的，因此配置时更需要一些技巧。依赖于无线芯片，设置通过下面三个文件中的一个来管理：

1.  `/etc/laptop-mode/conf.d/wireless-power.conf` 用于的电源管理的通用方法 (通过 "iwconfig wlan0 power on/off"). 这个适用于大多数芯片（除了Intel芯片集之外）。
2.  `/etc/laptop-mode/conf.d/wireless-ipw-power.conf` 通过老的ipw驱动来管理 Intel 芯片集。这适用于 IPW3945、IPW2200 和 IPW2100\. 现在（到LMT 1.55-1为止）它用 iwpriv 来管理 IPW3945，以及用 iwconfig 结合 iwpriv来管理 IPW2100 和 IPW220。详细信息请参见 `/usr/share/laptop-mode-tools/modules/wireless-ipw-power` 文件。（注意，ipw3945模块已经废弃了，见下面）
3.  `/etc/laptop-mode/conf.d/wireless-iwl-power.conf` 用于管理 iwl4965、iwl3945 和 iwlagn 驱动的Intel芯片集（iwlagn 支持 4965, 5100, 5300, 5350, 5150, 1000, 和 6000 芯片集）

**注意:** 三个模块全开通常不会带来问题，因为LMT会自动检测设备对应的模块。

每个配置文件所支持的模块是直接源自LMT的。但是有些已经过时了，因为从Linux内核版本2.6.34开始就不再提供ipw3945和iwl4965模块（3945采用iwl3945，4965采用通用模块iwlagn）。这并不影响LMT的正常工作。

对于iwlagn驱动的一些芯片集（包括5300或其它），有一个已知的问题。在这些芯片集上，文件 `/etc/laptop-mode/conf.d/wireless-iwl-power.conf`中的下列配置：

```
IWL_AC_POWER
IWL_BATT_POWER

```

会被忽略，因为文件 `/sys/class/net/wlan*/device/power_level` 不存在。于是通用方法（通过 "iwconfig wlan0 power on/off" ）会被自动启用。

### 音频设备

#### AC97

```
# ac97-powersave.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_AC97_POWER=1

```

#### Intel HDA

```
# intel-hda-powersave.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_INTEL_HDA_POWER=1
BATT_INTEL_HDA_POWERSAVE=1
LM_AC_INTEL_HDA_POWERSAVE=1
NOLM_AC_INTEL_HDA_POWERSAVE=0
INTEL_HDA_DEVICE_TIMEOUT=10
INTEL_HDA_DEVICE_CONTROLLER=0

```

## 提示和技巧

### Aliases

### lm-profiler

### Disabling

## 疑难问题

### Laptop-mode-tools 不能收到事件

对于使用 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 的系统，开启并使其开机自动加载[acpid](/index.php/Acpid_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Acpid (简体中文)") 请运行以下命令:

```
# systemctl enable acpid
# systemctl start acpid

```

如果这样不管用的话，请仔细检查一边 laptop-mode 的配置文件并确定需要开启的服务被设置成 1 了。许多服务，包括cpu频率控制服务 (cpufreq control) 默认设置都是'自动'("auto")，所以可能没有开启。

### 连接电源后Laptop-mode-tools并没有停止

这可能是因为同时安装有laptop-mode-tools和pm-utils两个软件包，它们互相会冲突，从而导致laptop-mode-tools不能准确的设定自己的状态。

这可以通过禁用pm-utils中带有重复功能的脚本来解决。问题的主要原因是位于`/usr/lib/pm-utils/power.d`中的laptop-mode脚本。可以通过在 `/etc/pm/power.d`中添加一个同名的空文件来禁用这个脚本，例如，如果想禁用laptop-mode：

```
# touch /etc/pm/power.d/laptop-mode

```

**注意:** 不要在这个文件上设置可执行标记。

建议浏览一下`/usr/lib/pm-utils/power.d`中的所有脚本并把其中提供了与laptop-mode-tools同样功能的脚本全都禁用掉。

## 相关链接

*   [Laptop Mode Tools](http://samwel.tk/laptop_mode/)
*   [Mailing List Archives](http://mailman.samwel.tk/pipermail/laptop-mode/)