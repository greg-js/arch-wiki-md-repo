**翻译状态：** 本文是英文页面 [Raspberry_Pi](/index.php/Raspberry_Pi "Raspberry Pi") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014_05_09，点击[这里](https://wiki.archlinux.org/index.php?title=Raspberry_Pi&diff=0&oldid=313536)可以查看翻译后英文页面的改动。

来自 [Wikipedia](https://en.wikipedia.org/wiki/Raspberry_Pi "wikipedia:Raspberry Pi"):

	"*树莓派是有英国树莓派基金会开发的一系列只有信用卡大小的单板计算机，目的是促进校园中基础性计算机教学的发展。*"

树莓派最初的版本于2012年发布，基于博通的BCM2835芯片（[ARM11 架构](https://en.wikipedia.org/wiki/ARM11 "wikipedia:ARM11")）。而最新的树莓派2于1015年发布，基于博通的BCM2836芯片（双核 [ARM Cortex-A7 架构](https://en.wikipedia.org/wiki/ARM_Cortex-A7 "wikipedia:ARM Cortex-A7")）。

## Contents

*   [1 前言](#.E5.89.8D.E8.A8.80)
*   [2 系统架构](#.E7.B3.BB.E7.BB.9F.E6.9E.B6.E6.9E.84)
*   [3 SD卡性能](#SD.E5.8D.A1.E6.80.A7.E8.83.BD)
*   [4 在树梅派上安装ArchLinux](#.E5.9C.A8.E6.A0.91.E6.A2.85.E6.B4.BE.E4.B8.8A.E5.AE.89.E8.A3.85ArchLinux)
*   [5 音频](#.E9.9F.B3.E9.A2.91)
    *   [5.1 HDMI音频说明](#HDMI.E9.9F.B3.E9.A2.91.E8.AF.B4.E6.98.8E)
*   [6 音频](#.E9.9F.B3.E9.A2.91_2)
    *   [6.1 HDMI / 模拟 TV-输出](#HDMI_.2F_.E6.A8.A1.E6.8B.9F_TV-.E8.BE.93.E5.87.BA)
    *   [6.2 X.org driver](#X.org_driver)
*   [7 Onboard Hardware Sensors](#Onboard_Hardware_Sensors)
    *   [7.1 Temperature](#Temperature)
    *   [7.2 Voltage](#Voltage)
    *   [7.3 Lightweight Monitoring Suite](#Lightweight_Monitoring_Suite)
*   [8 Overclocking/Underclocking](#Overclocking.2FUnderclocking)
*   [9 Tips for maximizing SD card performance](#Tips_for_maximizing_SD_card_performance)
    *   [9.1 Enable fsck on boot](#Enable_fsck_on_boot)
*   [10 Serial Console](#Serial_Console)
*   [11 Raspberry Pi Camera module](#Raspberry_Pi_Camera_module)
*   [12 Hardware Random Number Generator](#Hardware_Random_Number_Generator)
*   [13 GPIO](#GPIO)
    *   [13.1 Python](#Python)
*   [14 See also](#See_also)

## 前言

这篇文章并不是详尽的安装指南，我们假设读者已经成功在树梅派上部署了ArchLinux系统。建议初次使用ArchLinux的用户通过阅读[Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")来了解如何在Arch Linux上执行一些如创建用户、设置系统的一般性任务。

**Note:** ArchLinux的ARM架构支持由 [http://archlinuxarm.org](http://archlinuxarm.org) 社区提供，而非Arch Linux社区官方支持。任何关于ARM架构下特有问题的讨论将会被关闭，详见[Arch Linux distribution support ONLY](/index.php/Forum_etiquette#Arch_Linux_distribution_support_.2Aonly.2A "Forum etiquette") 政策

## 系统架构

树莓派是一个基于ARM的设备，因此它需要专门为此架构编译的二进制软件。这些二进制软件由[Arch Linux ARM project](http://archlinuxarm.org/about)提供，他们把Arch Linux移植到了ARM设备上。在他们的官方网站上也有一个松散的社区，而Arch Linux官方社区并不对ARM架构进行官方支持。

由于新版的树莓派2的推出，现在不同版本的树莓派基于不同的ARM架构，因此也需要选择支持不同ARM架构的软件包：

*   ARMv6 (BCM2835): 树莓派 Model A, A+, B, B+
*   ARMv7 (BCM2836): 树莓派 2 (基于 Model B+)

## SD卡性能

System responsiveness, particularly during operations involving disk I/O such as updating the system, can be adversely affected by poor quality/slow SD media. This is characterized by [frequent, often extended pauses](http://archlinuxarm.org/forum/viewtopic.php?f=64&t=9467) as pacman writes out files to the file system. The pauses are not due to saturation of the RPi or RPi2 bus, but are likely the bottle-neck due to a slow SD (or micro SD) card. See the [Benchmarking#Flash media](/index.php/Benchmarking#Flash_media "Benchmarking") for more.

## 在树梅派上安装ArchLinux

参看 [Arch Linux ARM Pi documentation](http://archlinuxarm.org/platforms/armv6/raspberry-pi) 或者 [Arch Linux ARM Pi2 documentation](http://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2)。

## 音频

**Note:** 所依赖的内核模块`snd-bcm2835`应当默认会被自动加载。

下载 **alsa-utils**, **alsa-firmware**, **alsa-lib** 和 **alsa-plugins** 包:

```
# pacman -S alsa-utils alsa-firmware alsa-lib alsa-plugins

```

可以使用`alsamixer`来调整音量，请确保"PCM"没有被设置为静音(测试：`MM`如果设置为静音，使用`M`关掉静音).

选择一个音频输出:

```
$ amixer cset numid=3 *x*

```

参数`*x*`应当为：

*   0 自动
*   1 模拟输出
*   3 HDMI

### HDMI音频说明

有些应用程序需要设置`/boot/config.txt`来强制开启HDMI模式：

```
hdmi_drive=2

```

## 音频

### HDMI / 模拟 TV-输出

开启或关闭[HDMI](https://en.wikipedia.org/wiki/HDMI "wikipedia:HDMI")或TV-输出：

```
/opt/vc/bin/tvservice

```

Use the *-s* parameter to check the status of your display, the *-o* parameter to turn your display off and *-p* parameter to power on HDMI with preferred settings.

Adjustments are likely required to correct proper overscan/underscan and are easily achieved in `boot/config.txt` in which many tweaks are set. To fix, simply uncomment the corresponding lines and setup per the commented instructions:

```
# uncomment the following to adjust overscan. Use positive numbers if console
# goes off screen, and negative if there is too much border
#overscan_left=16
overscan_right=8
overscan_top=-16
overscan_bottom=-16

```

Users wishing to use the analog video out should consult [this](https://raw.github.com/Evilpaul/RPi-config/master/config.txt) config file which contains options for non-NTSC outputs.

A reboot is needed for new settings to take effect.

### X.org driver

The X.org driver for Raspberry Pi can be installed with the **xf86-video-fbdev** package:

```
# pacman -S xf86-video-fbdev

```

## Onboard Hardware Sensors

### Temperature

Temperatures sensors can be queried with utils in the **raspberrypi-firmware-tools** package. The RPi offers a sensor on the BCM2835 SoC (CPU/GPU):

 `$ /opt/vc/bin/vcgencmd measure_temp`  `temp=49.8'C` 

Alternatively, simply read from the file system:

 `$ cat /sys/class/thermal/thermal_zone0/temp`  `49768` 

For human readable output:

 `awk '{printf "%3.1f°C
", $1/1000}' /sys/class/thermal/thermal_zone0/temp`  `54.1°C` 

### Voltage

Four different voltages can be monitored via `/opt/vc/bin/vcgencmd` as well:

```
$ /opt/vc/bin/vcgencmd measure_volts *<id>*

```

Where `*<id>*` is:

*   core for core voltage
*   sdram_c for sdram Core voltage
*   sdram_i for sdram I/O voltage
*   sdram_p for sdram PHY voltage

### Lightweight Monitoring Suite

[monitorix](https://aur.archlinux.org/packages/monitorix/) has specific support for the RPi since v3.2.0\. Screenshots available [here](http://www.monitorix.org/screenshots.html).

## Overclocking/Underclocking

The RPi can be overclocked by editing `/boot/config.txt`, for example:

```
arm_freq=800
arm_freq_min=100
core_freq=300
core_freq_min=75
sdram_freq=400
over_voltage=0

```

The optional xxx_min lines define the min usage of their respective settings. When the system is not under load, the values will drop down to those specified. Consult the [Overclocking](http://elinux.org/RPiconfig#Overclocking) article on elinux for additional options and examples.

A reboot is needed for new settings to take effect.

**Note:** The overclocked setting for CPU clock applies only when the governor throttles up the CPU, i.e. under load.

Users may query the current frequency of the CPU via this command:

```
$ cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq

```

## Tips for maximizing SD card performance

See [Maximizing performance](/index.php/Maximizing_performance "Maximizing performance") for the general performance improvements.

### Enable fsck on boot

To enable fsck on boot, the root filesystem should be mounted as readonly first, and then remounted as read-writable.

First, make root as read-only on boot. edit `/boot/cmdline.txt` to add "ro" after the option indicating root partition.

```
ipv6.disable=1 selinux=0 plymouth.enable=0 dwc_otg.lpm_enable=0 console=ttyAMA0,115200 kgdboc=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p5 **ro** rootfstype=ext4 elevator=noop rootwait

```

Next, add next line in `/etc/fstab` to remount the partition during boot.

```
/dev/mmcblk0p5  /       ext4    remount,rw        0       0

```

## Serial Console

Edit the default `/boot/cmdline.txt`, change `loglevel` to `5` to see boot messages:

```
loglevel=5

```

Change speed from 115200 to 38400:

```
console=ttyAMA0,38400 kgdboc=ttyAMA0,38400

```

Start getty service

```
# systemctl start getty@ttyAMA0

```

Enable on boot

```
# systemctl enable getty@ttyAMA0.service

```

Creating the proper service link:

```
# ln -s /usr/lib/systemd/system/serial-getty@.service /etc/systemd/system/getty.target.wants/serial-getty@ttyAMA0.service

```

Then connect :)

```
# screen /dev/ttyUSB0 38400

```

## Raspberry Pi Camera module

The commands for the camera module are including as part of the **raspberrypi-firmware-tools** package - which is installed by default. You can then use:

```
$ /opt/vc/bin/raspistill
$ /opt/vc/bin/raspivid

```

You need to append to `/boot/config.txt`:

```
start_file=start_x.elf
fixup_file=fixup_x.dat

```

Optionally

```
disable_camera_led=1

```

if you get the following error:

```
mmal: mmal_vc_component_enable: failed to enable component: ENOSPC
mmal: camera component couldn't be enabled
mmal: main: Failed to create camera component
mmal: Failed to run camera app. Please check for firmware updates

```

try setting these values in `/boot/config.txt`:

```
cma_lwm=
cma_hwm=
cma_offline_start=

```

## Hardware Random Number Generator

ArchLinux ARM for the Raspberry Pi is distributed with the **rng-tools** package installed and the **bcm2708-rng** module set to load at boot (see [this](http://archlinuxarm.org/forum/viewtopic.php?f=31&t=4993#p27708)), but we must also tell the Hardware RNG Entropy Gatherer Daemon (**rngd**) where to find the hardware random number generator.

This can be done by editing `/etc/conf.d/rngd`:

```
RNGD_OPTS="-o /dev/random -r /dev/hwrng"

```

and restarting the **rngd** daemon:

```
systemctl restart rngd

```

Once completed, this change ensures that data from the hardware random number generator is fed into the kernel's entropy pool at `/dev/random`.

## GPIO

### Python

To be able to use the GPIO pins from Python, you can use the [RPi.GPIO](https://pypi.python.org/pypi/RPi.GPIO) library. Install either [python-raspberry-gpio](https://aur.archlinux.org/packages/python-raspberry-gpio/) or [python2-raspberry-gpio](https://aur.archlinux.org/packages/python2-raspberry-gpio/) from the [AUR](/index.php/AUR "AUR").

## See also

*   [RPi Config](http://elinux.org/RPiconfig) - Excellent source of info relating to under-the-hood tweaks.
*   [RPi vcgencmd usage](http://elinux.org/RPI_vcgencmd_usage) - Overview of firmware command vcgencmd.
*   [Archlinux ARM on Raspberry PI](http://archpi.dabase.com/) - A FAQ style site with hints and tips for running Archlinux on the rpi