## Contents

*   [1 Eee 700 Series and 900](#Eee_700_Series_and_900)
*   [2 Eee 900A](#Eee_900A)
*   [3 Eee 901, 904, and 1000(H)](#Eee_901.2C_904.2C_and_1000.28H.29)
*   [4 Eee 904HA](#Eee_904HA)
*   [5 Eee T101MT](#Eee_T101MT)
*   [6 Eee 1000HE](#Eee_1000HE)
*   [7 Eee 1001P](#Eee_1001P)
*   [8 Eee 1001PX](#Eee_1001PX)
*   [9 Eee 1005HA(B)](#Eee_1005HA.28B.29)
*   [10 Eee 1005P(E)](#Eee_1005P.28E.29)
*   [11 Eee 1011PX](#Eee_1011PX)
*   [12 Eee 1015B](#Eee_1015B)
*   [13 Eee 1015 BX](#Eee_1015_BX)
*   [14 Eee 1015 PE/PEM](#Eee_1015_PE.2FPEM)
    *   [14.1 Hardware](#Hardware)
    *   [14.2 Installation](#Installation)
*   [15 Eee 1015 PN](#Eee_1015_PN)
*   [16 Eee 1025C](#Eee_1025C)
*   [17 Eee 1201T](#Eee_1201T)
*   [18 Eee 1201N](#Eee_1201N)
*   [19 Eee 1215N](#Eee_1215N)
*   [20 Eee 1215B](#Eee_1215B)
    *   [20.1 Audio](#Audio)
    *   [20.2 Power Management](#Power_Management)
    *   [20.3 USB 3.0 on battery](#USB_3.0_on_battery)

# Eee 700 Series and 900

See [ASUS Eee PC 701](/index.php/ASUS_Eee_PC_701 "ASUS Eee PC 701").

# Eee 900A

See [Asus Eee PC 900A](/index.php/Asus_Eee_PC_900A "Asus Eee PC 900A").

# Eee 901, 904, and 1000(H)

The 901, 904, and 1000(H) all seem to share much-of, if not all the same hardware. See [ASUS Eee PC 901](/index.php/ASUS_Eee_PC_901 "ASUS Eee PC 901").

# Eee 904HA

[ASUS Eee PC 904HA](/index.php/ASUS_Eee_PC_904HA "ASUS Eee PC 904HA")

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

# Eee 1011PX

Some Fn keys might work out of the box but with recent kernels, you won't be able to turn wifi on or off unless you add `acpi_osi=Linux` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

# Eee 1015B

[ASUS Eee PC 1015b](/index.php/ASUS_Eee_PC_1015b "ASUS Eee PC 1015b")

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

# Eee 1015 PN

[ASUS Eee PC 1015pn](/index.php/ASUS_Eee_PC_1015pn "ASUS Eee PC 1015pn")

# Eee 1025C

[ASUS Eee PC 1025c](/index.php/ASUS_Eee_PC_1025c "ASUS Eee PC 1025c")

# Eee 1201T

[ASUS Eee PC 1201T](/index.php/ASUS_Eee_PC_1201T "ASUS Eee PC 1201T")

# Eee 1201N

[ASUS Eee PC 1201N](/index.php/ASUS_Eee_PC_1201N "ASUS Eee PC 1201N")

# Eee 1215N

[ASUS Eee PC 1215N](/index.php/ASUS_Eee_PC_1215N "ASUS Eee PC 1215N")

# Eee 1215B

Things that work out of the box: Wifi, Ethernet, Video (max resolution available with basic Xorg and xfce packages installed), Touchpad, Keyboard (Fn keys not working).

Things that need work: Audio, Fn keys, Power management.

## Audio

With the xfce4 desktop environment audio doesn't work by default (didn't test with other de). To fix this, add the following lines in your ~/.asoundrc:

```
defaults.pcm.card 1
defaults.ctl.card 1
```

(Credit to Touko Korpela from the Debian mailing list)

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