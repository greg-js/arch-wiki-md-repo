This should be the page to gather all information on installing and running arch on the Asus Eee. Why? Because the 'old' page is a bit confusing/outdated, wrongly named (makes finding it in a search hard) and the title limits it to just the install precedure.

The 'old' page should be cleaned up and merged into this page, and any future information should also go on this page. If no one that actualy owns an Eee want to do it, then I (Mr.Elendig) can do it, but it will take some time.

## Contents

*   [1 Eee 700 Series and 900](#Eee_700_Series_and_900)
    *   [1.1 Installation](#Installation)
    *   [1.2 Xorg](#Xorg)
    *   [1.3 Sound](#Sound)
*   [2 Eee 900A](#Eee_900A)
*   [3 Eee 901, 904, and 1000(H)](#Eee_901.2C_904.2C_and_1000.28H.29)
*   [4 Eee 904HA](#Eee_904HA)
*   [5 Eee T91MT](#Eee_T91MT)
*   [6 Eee T101MT](#Eee_T101MT)
*   [7 Eee 1000HE](#Eee_1000HE)
*   [8 Eee 1001P](#Eee_1001P)
*   [9 Eee 1001PX](#Eee_1001PX)
*   [10 Eee 1005HA(B)](#Eee_1005HA.28B.29)
*   [11 Eee 1005P(E)](#Eee_1005P.28E.29)
*   [12 Eee 1011CX](#Eee_1011CX)
*   [13 Eee 1011PX](#Eee_1011PX)
*   [14 Eee 1015B](#Eee_1015B)
    *   [14.1 Audio](#Audio)
    *   [14.2 Powersaving](#Powersaving)
*   [15 Eee 1015 BX](#Eee_1015_BX)
*   [16 Eee 1015 PE/PEM](#Eee_1015_PE.2FPEM)
    *   [16.1 Hardware](#Hardware)
    *   [16.2 Installation](#Installation_2)
        *   [16.2.1 ACPI](#ACPI)
        *   [16.2.2 Modules](#Modules)
*   [17 Eee 1015 PN](#Eee_1015_PN)
*   [18 Eee 1025C](#Eee_1025C)
*   [19 Eee 1201T](#Eee_1201T)
*   [20 Eee 1201NL](#Eee_1201NL)
*   [21 Eee 1215n](#Eee_1215n)
*   [22 Eee 1215P](#Eee_1215P)
*   [23 Eee 1215B](#Eee_1215B)
    *   [23.1 Installation](#Installation_3)
    *   [23.2 Audio](#Audio_2)
    *   [23.3 Video](#Video)
    *   [23.4 Power Management](#Power_Management)
    *   [23.5 USB 3.0 on battery](#USB_3.0_on_battery)

# Eee 700 Series and 900

This should be filled with the majority of the content from [ASUS Eee PC 701](/index.php/ASUS_Eee_PC_701 "ASUS Eee PC 701").

### Installation

Installation can be achieved from an external cdrom drive, or from a usb stick configured as described in [Install from USB stick](/index.php/Install_from_USB_stick "Install from USB stick")

The wireless module (ath5k) is now part of the stock kernel. The stock kernel performs very well on the eeepc. You do not need to install any extra packages from AUR for wireless or install any special kernel.

During installation make sure you add the following packages in addition to the base packages for wireless to work.

```
wireless_tools
netcfg

```

Thats all you now need for a working eee.

### Xorg

Xorg works without an xorg.conf on the eeepc fine with the new hotplugging system. See [Xorg](/index.php/Xorg "Xorg").

### Sound

If sound does not work in a new installation add the following line to `/etc/modprobe.d/modprobe.conf`

```
options snd-hda-intel model=3stack-dig

```

# Eee 900A

The 900A is a 900 with a Intel Atom CPU and new hardware (the most is like in 901), you can get help in [Asus Eee PC 900A](/index.php/Asus_Eee_PC_900A "Asus Eee PC 900A").

# Eee 901, 904, and 1000(H)

The 901, 904, and 1000(H) all seem to share much-of, if not all the same hardware. The steps for setting up Arch Linux are as follows. NB. There is a separate wiki page as well dedicated to the [ASUS Eee PC 901](/index.php/ASUS_Eee_PC_901 "ASUS Eee PC 901").

# Eee 904HA

[ASUS Eee PC 904HA](/index.php/ASUS_Eee_PC_904HA "ASUS Eee PC 904HA")

# Eee T91MT

[ASUS Eee PC T91MT](/index.php/ASUS_Eee_PC_T91MT "ASUS Eee PC T91MT")

# Eee T101MT

[ASUS Eee PC T101MT](/index.php/ASUS_Eee_PC_T101MT "ASUS Eee PC T101MT")

# Eee 1000HE

[ASUS Eee PC 1000HE](/index.php/ASUS_Eee_PC_1000HE "ASUS Eee PC 1000HE")

# Eee 1001P

[ASUS Eee PC 1001p](/index.php/ASUS_Eee_PC_1001p "ASUS Eee PC 1001p")

# Eee 1001PX

[ASUS Eee PC 1001px](/index.php/ASUS_Eee_PC_1001px "ASUS Eee PC 1001px")

# Eee 1005HA(B)

[ASUS Eee PC 1005HA](/index.php/ASUS_Eee_PC_1005HA "ASUS Eee PC 1005HA")

# Eee 1005P(E)

[ASUS Eee PC 1005P](/index.php/ASUS_Eee_PC_1005P "ASUS Eee PC 1005P")

# Eee 1011CX

[ASUS Eee PC 1011cx](/index.php/ASUS_Eee_PC_1011cx "ASUS Eee PC 1011cx")

# Eee 1011PX

Some Fn keys might work out of the box but with recent kernels, you won't be able to turn wifi on or off unless you add `acpi_osi=Linux` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

# Eee 1015B

Things that "just work":

*   Wlan (ath9k is part of the kernel; some use brcmsmac)
*   Ethernet
*   Graphics (with kms and dri2, using the xf86-video-ati driver)
*   Webcam (using v4l)
*   Suspend-to-RAM (after installing acpid)
*   Cardreader (but keucr is in staging, thus **taints the kernel**. PyroPeter experienced **crashes** while he inserted or removed sd cards)
*   Bluetooth (after installing bluez)
*   CPU Frequency Scaling (Use acpi_cpufreq since linux 3.7)
*   TouchPad (support multi-touch after installing xf86-input-synaptics)
*   Video Acceleration (either [open source driver](/index.php/ATI#Enabling_video_acceleration "ATI") ([xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)) or [ATI/AMD's propretary driver(catalyst)](/index.php/ATI_Catalyst#Video_acceleration "ATI Catalyst") work)

*/etc/modprobe.d/eeepc1015b.conf:*

```
# supposed to help against following msg in dmesg:
# SP5100 TCO timer: mmio address 0xbafe00 already in use
blacklist sp5100_tco

# if you don't need the sd-card reader you may want to blacklist
# keucr. it is in staging, thus taints the kernel
blacklist keucr

# if you find "*ACPI: resource piix4_smbus [io 0x0b00-0x0b07]*
# *conflicts with ACPI region SMRG [io 0xb00-0xb0f]*" 
# in /var/log/messages.log ,try to uncomment the following line
#blacklist i2c_piix4

```

lspci:

```
00:00.0 Host bridge: Advanced Micro Devices [AMD] Family 14h Processor Root Complex
00:01.0 VGA compatible controller: Advanced Micro Devices [AMD] nee ATI Device 9805
00:01.1 Audio device: Advanced Micro Devices [AMD] nee ATI Wrestler HDMI Audio [Radeon HD 6250/6310]
00:04.0 PCI bridge: Advanced Micro Devices [AMD] Family 14h Processor Root Port
00:05.0 PCI bridge: Advanced Micro Devices [AMD] Family 14h Processor Root Port
00:11.0 SATA controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 SATA Controller [AHCI mode]
00:12.0 USB controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 USB OHCI0 Controller
00:12.2 USB controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 USB EHCI Controller
00:13.0 USB controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 USB OHCI0 Controller
00:13.2 USB controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 USB EHCI Controller
00:14.0 SMBus: Advanced Micro Devices [AMD] nee ATI SBx00 SMBus Controller (rev 42)
00:14.2 Audio device: Advanced Micro Devices [AMD] nee ATI SBx00 Azalia (Intel HDA) (rev 40)
00:14.3 ISA bridge: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 LPC host controller (rev 40)
00:14.4 PCI bridge: Advanced Micro Devices [AMD] nee ATI SBx00 PCI to PCI Bridge (rev 40)
00:15.0 PCI bridge: Advanced Micro Devices [AMD] nee ATI SB700/SB800/SB900 PCI to PCI bridge (PCIE port 0)
00:18.0 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 0 (rev 43)
00:18.1 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 1
00:18.2 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 2
00:18.3 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 3
00:18.4 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 4
00:18.5 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 6
00:18.6 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 5
00:18.7 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 7
01:00.0 Network controller: Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01)
02:00.0 Ethernet controller: Atheros Communications Inc. AR8152 v2.0 Fast Ethernet (rev c1)

```

On models with ASMedia USB 3.0 chip, replace last 2 line with:

```
01:00.0 Network controller: Broadcom Corporation BCM4313 802.11b/g/n Wireless LAN Controller (rev 01)
02:00.0 Ethernet controller: Atheros Communications Inc. AR8152 v2.0 Fast Ethernet (rev c1)
03:00.0 USB controller: ASMedia Technology Inc. Device 1040

```

lsusb:

```
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 002: ID 13d3:5702 IMC Networks UVC VGA Webcam

```

## Audio

After running alsaconf the graphics card was the default audio output, so I had to create `/etc/asound.conf` with the following contents:

```
defaults.ctl.card 1
defaults.pcm.card 1
defaults.timer.card 1

```

Volume function key for alsa:

 `/etc/acpi/handler.sh` 
```
......
        open)
            #echo "LID opend!">/dev/tty5
            ;;
    esac
    ;;
## volume control key ##
button/mute)
  case "$2" in
    MUTE) amixer set Master toggle ;;
  esac
  ;;
button/volumedown)
  case "$2" in
    VOLDN) amixer set Master 2%- ;;
  esac
  ;;
button/volumeup)
  case "$2" in
    VOLUP) amixer set Master 2%+ ;;
  esac
  ;;
## volume control key end ##
*)
  logger "ACPI group/action underfined: $1 /$2"
  ;;
esac
```

## Powersaving

When system is idle, [ATI/AMD's propretary driver(catalyst)](/index.php/ATI_Catalyst "ATI Catalyst") saves 2.5W than xf86-video-ati.

# Eee 1015 BX

Most seems to work 'out-of-the-box':

*   Wlan
*   Ethernet
*   Graphics (using the xf86-video-ati driver)
*   Webcam
*   Suspend-to-RAM (with acpi & acpid)
*   Cardreader
*   CPU Frequency Scaling (add 'eeepc-wmi ac battery button fan video' to MODULES array in '/etc/rc.conf')
*   TouchPad (using the xf86-input-synaptics driver)

My blacklist:

```
# /etc/modprobe.d/blacklist.conf
blacklist sp5100_tco

```

For sound at DE add this file to your HOME-directory:

```
#
# ~/.asoundrc
#

defaults.ctl.card 1
defaults.pcm.card 1
defaults.timer.card 1

```

For volume-control-buttons I use shortcuts with:

```
amixer -q -c 1 set Master 5+
amixer -q -c 1 set Master 5-
amixer -q -c 1 set Master toggle

```

# Eee 1015 PE/PEM

## Hardware

The Eee 1015 series laptops come with a 1024x600 LED display and a Dual Core Intel Atom processor (N550). They also have a [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") card and an Atheros Ethernet port.

Here is the output of `lspci`:

```
00:00.0 Host bridge: Intel Corporation N10 Family DMI Bridge (rev 02)
00:02.0 VGA compatible controller: Intel Corporation N10 Family Integrated Graphics Controller (rev 02)
00:02.1 Display controller: Intel Corporation N10 Family Integrated Graphics Controller (rev 02)
00:1b.0 Audio device: Intel Corporation N10/ICH 7 Family High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 2 (rev 02)
00:1c.3 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 4 (rev 02)
00:1d.0 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #1 (rev 02)
00:1d.1 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #2 (rev 02)
00:1d.2 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #3 (rev 02)
00:1d.3 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #4 (rev 02)
00:1d.7 USB controller: Intel Corporation N10/ICH 7 Family USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation NM10 Family LPC Controller (rev 02)
00:1f.2 SATA controller: Intel Corporation N10/ICH7 Family SATA Controller [AHCI mode] (rev 02)
01:00.0 Ethernet controller: Atheros Communications Inc. AR8132 Fast Ethernet (rev c0)
02:00.0 Network controller: Broadcom Corporation BCM4313 802.11b/g/n Wireless LAN Controller (rev 01)
```

**Note:** The wireless card uses the **brcmsmac** driver. Since linux 3.3.1 the brcmsmac driver depends on the bcma module and blacklisting is no longer required. See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless")

Here is the output of `lscpu`:

```
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                4
On-line CPU(s) list:   0-3
Thread(s) per core:    2
Core(s) per socket:    2
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 28
Stepping:              10
CPU MHz:               1499.813
BogoMIPS:              3000.61
L1d cache:             24K
L1i cache:             32K
L2 cache:              512K
NUMA node0 CPU(s):     0-3

```

## Installation

To install Arch on the Asus Eee 1015 series you need to use an external cd-rom drive or [USB Installation Media](/index.php/USB_Installation_Media "USB Installation Media").

The partition created by Asus on my 1015 PEM is as follows:

```
Number Start    End    Size   Type      File System   Flags
1      1049kb   107Gb  107Gb  primary   NTFS           
2      107Gb    123Gb  16.1Gb primary   fat32         hidden
3      123Gb    250Gb  127Gb  primary   NTFS          
4      250Gb    250Gb  21.2Gb primary   

```

Results may vary. The first partition was the Windows 7 installation. The second is the recovery partition with splashtop. Removing this second partition will cause the fast-start Linux to stop working. The third is Windows D:\ drive and the last one is the boot partition for Windows 7.

Due to the limitations of having 4 partitions per drive I installed arch on the first 107Gb partition and created a swap file instead of a partition as per [Swap](/index.php/Swap "Swap").

### ACPI

ACPI works fine following the [acpid](/index.php/Acpid "Acpid") guide. The following is for older versions of the kernel.

To enable acpi you need to edit menu.lst and add acpi_osi=Linux to the kernel line like so:

```
 kernel /boot/vmlinuz-linux root=/dev/sda1 ro acpi_osi=Linux

```

This enabled you to trigger devices in /sys/devices/platform/eeepc/.

**Note:** As far as I can tell, this is no longer required. If you do add it, the module eeepc-wmi will fail to load - kernel 2.6.39.2-1

### Modules

As of [kernel](http://kernel.org) 3.3.7-1, no extra modules are **required** in order for full usage of Arch Linux on this laptop.

# Eee 1015 PN

[ASUS Eee PC 1015pn](/index.php/ASUS_Eee_PC_1015pn "ASUS Eee PC 1015pn")

# Eee 1025C

[ASUS Eee PC 1025c](/index.php/ASUS_Eee_PC_1025c "ASUS Eee PC 1025c")

# Eee 1201T

[ASUS Eee PC 1201T](/index.php/ASUS_Eee_PC_1201T "ASUS Eee PC 1201T")

# Eee 1201NL

[ASUS Eee PC 1201NL](/index.php/ASUS_Eee_PC_1201NL "ASUS Eee PC 1201NL")

# Eee 1215n

[ASUS Eee PC 1215n](/index.php/ASUS_Eee_PC_1215n "ASUS Eee PC 1215n")

# Eee 1215P

[ASUS Eee PC 1215p](/index.php/ASUS_Eee_PC_1215p "ASUS Eee PC 1215p")

# Eee 1215B

Things that work out of the box: Wifi, Ethernet, Video (max resolution available with basic Xorg and xfce packages installed), Touchpad, Keyboard (Fn keys not working).

Things that need work: Audio, Fn keys, Power management.

## Installation

Arch setup encountered no problems, GRUB installed successfully with no damages to Windows (need to uncomment the windows lines in in /boot/grub/menu.lst) and Express Gate.

## Audio

With the xfce4 desktop environment audio doesn't work by default (didn't test with other de). To fix this, add the following lines in your ~/.asoundrc:

```
defaults.pcm.card 1
defaults.ctl.card 1
```

(Credit to Touko Korpela from the Debian mailing list)

## Video

YouTube videos with the default ATI driver work flawlessly with a resolution of 720p, while with 1080p playback isn't smooth anymore. Didn't test with the catalyst drivers, maybe a better playback could be achieved.

## Power Management

ACPI executes correctly and returns remaining battery life. Cpufreq doesn't seem to work, hence making it impossible for Jupiter ([[1]](http://sourceforge.net/projects/jupiter/)) to manage the Super Hybrid Engine. However, from the Jupiter tray icon, screen orientation, resolution and touchpad can be toggled and modified.

By suggestion from the Debian mailing list, I tried loading "powernow-k8" with modprobe to get cpufreq working. This is apparently a bug in the driver detection mechanism of cpufreq, and should be reported upstream, I guess. After loading that module, cpufreq-info seems to work. Have not tried getting Jupiter to manage SHE yet after that.

**Suspend** and **hibernate** work **OK**, with one tiny bug: I can't seem to get the SD-card reader working after resuming from hibernate. After a reboot, it works fine.

## USB 3.0 on battery

On battery devices plugged in to the usb 3.0 port were not recognized before the usb autosuspend power save feature was turned off. The problem is reported as a reset or a loss of power:

```
$ dmesg | tail
[ 3039.634343] usb usb1: root hub lost power or was reset
[ 3039.634397] usb usb3: root hub lost power or was reset
[ 3040.634459] usb usb1: root hub lost power or was reset
[ 3040.634514] usb usb3: root hub lost power or was reset
```

[Autosuspend](https://www.kernel.org/doc/Documentation/usb/power-management.txt) can be disabled globally by using the `usbcore.autosuspend=-1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

Disabling autosuspend only for the usb 3.0 port is possible by creating a specific [udev](/index.php/Udev "Udev") rule. See [udev#Writing udev rules](/index.php/Udev#Writing_udev_rules "Udev") for more information.

Information about the usb 3.0 device can be obtained with `lsusb` and `udevadmn info`. Below is a simple udev rule which disables autosuspend for all version 3.0 usb devices:

 `/etc/udev/rules.d/usb-power.rules` 
```
# Disable autosuspend for USB 3.0 port
SUBSYSTEM=="usb", ATTR{version}==" 3.00", ATTR{power/control}="on"
```