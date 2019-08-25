| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | bluetooth |
| Mobile broadband | Not working | ? Intel XMM 7560 |
| Audio | Partially Working | snd_hda_intel or snd_sof |
| Touchpad | Working | ? |
| Touchscreen | Working | hid_multitouch |
| Pen input | Working | ? |
| Webcam | working | uvcvideo |
| Card Reader | Working | rtsx_pci |
| Wireless Switch | Working | ? |
| Function/Multimedia Keys | Working | ? |
| Suspend/Resume | Partially Working (patched kernel needed) | ? |
| Fingerprint sensor | Not working | ? synaptic 06cb:00bb WIP |

This article covers specific configuration of this laptop. Currently based on experience with Xfce4 and with Awesome, running on X.org.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware Info](#Hardware_Info)
    *   [1.1 Hardware Options](#Hardware_Options)
    *   [1.2 lspci for 13-ap0xxxx](#lspci_for_13-ap0xxxx)
    *   [1.3 lsusb for 13-ap0xxxx](#lsusb_for_13-ap0xxxx)
*   [2 Installation](#Installation)
    *   [2.1 Basics](#Basics)
    *   [2.2 Advanced / Kernel update](#Advanced_/_Kernel_update)
*   [3 Issues / Notes](#Issues_/_Notes)
    *   [3.1 Audio](#Audio)
    *   [3.2 Camera](#Camera)
    *   [3.3 Mute Button](#Mute_Button)
    *   [3.4 Auto Rotation](#Auto_Rotation)
    *   [3.5 Dual boot](#Dual_boot)
    *   [3.6 Hp "sureview" privacy screen](#Hp_"sureview"_privacy_screen)
    *   [3.7 USB-C HDMI-out / dualscreen](#USB-C_HDMI-out_/_dualscreen)
    *   [3.8 Bluetooth](#Bluetooth)
    *   [3.9 Mobile Broadband](#Mobile_Broadband)
    *   [3.10 Fingerprint Reader](#Fingerprint_Reader)
    *   [3.11 Tablet mode](#Tablet_mode)
    *   [3.12 IR Camera Login](#IR_Camera_Login)
    *   [3.13 Battery optimizations](#Battery_optimizations)
    *   [3.14 Suspend issues](#Suspend_issues)
    *   [3.15 Sensors](#Sensors)
    *   [3.16 ACPI Errors](#ACPI_Errors)

## Hardware Info

### Hardware Options

This is the late 2018 edition of the Spectre x360 from HP codename Gem cut ( 13-ap0xxx/851 )

*   Intel i7-8565U Whiskey Lake Refresh
*   16GB Ram
*   512 GB NvMe SSD
*   FHD Touchscreen "Sureview" with Elantech pen
*   4 Speaker Sound
*   2 USB-C, Thunderbolt 3 Ports
*   1 USB 3
*   TPM 2
*   Synaptics Fingerprint Sensor

### lspci for 13-ap0xxxx

```
00:00.0 Host bridge: Intel Corporation Device 3e34 (rev 0b)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (Whiskey Lake)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0b)
00:12.0 Signal processing controller: Intel Corporation Device 9df9 (rev 30)
00:13.0 Serial controller: Intel Corporation Device 9dfc (rev 30)
00:14.0 USB controller: Intel Corporation Device 9ded (rev 30)
00:14.2 RAM memory: Intel Corporation Device 9def (rev 30)
00:14.3 Network controller: Intel Corporation Device 9df0 (rev 30)
00:15.0 Serial bus controller [0c80]: Intel Corporation Device 9de8 (rev 30)
00:15.1 Serial bus controller [0c80]: Intel Corporation Device 9de9 (rev 30)
00:16.0 Communication controller: Intel Corporation Device 9de0 (rev 30)
00:1c.0 PCI bridge: Intel Corporation Device 9dba (rev f0)
00:1c.4 PCI bridge: Intel Corporation Device 9dbc (rev f0)
00:1d.0 PCI bridge: Intel Corporation Device 9db4 (rev f0)
00:1f.0 ISA bridge: Intel Corporation Device 9d84 (rev 30)
00:1f.3 Multimedia audio controller: Intel Corporation Device 9dc8 (rev 30)
00:1f.4 SMBus: Intel Corporation Device 9da3 (rev 30)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Device 9da4 (rev 30)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
02:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
03:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
03:01.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
03:02.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
03:04.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
04:00.0 System peripheral: Intel Corporation JHL6540 Thunderbolt 3 NHI (C step) [Alpine Ridge 4C 2016] (rev 02)
38:00.0 USB controller: Intel Corporation JHL6540 Thunderbolt 3 USB Controller (C step) [Alpine Ridge 4C 2016] (rev 02)
6d:00.0 Non-Volatile memory controller: Toshiba America Info Systems Device 0116

```

### lsusb for 13-ap0xxxx

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 06cb:00bb Synaptics, Inc. 
Bus 001 Device 002: ID 0408:5251 Quanta Computer, Inc. 
Bus 001 Device 004: ID 8087:0aaa Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Installation

### Basics

Installation needs a bit of workarounds ( as of 2018.12 arch iso ).

First you will need to disable secureboot in BIOS (ESC to bring up menu, then F10 for BIOS and/or F9 for Boot options).

Using bios F.08 I somehow had to enable legacy boot support to be able to boot even if using UEFI ( this may be a side effect of testing many things, needs to be clarified ).

Upon boot, you need to edit the kernel cmdline ( press e in UEFI mode when presented with the list of boot options on the arch USB key ) and remove the first initrd lines mentionning intel and amd.

Then follow the [installation guide](/index.php/Installation_guide "Installation guide") as usual.

### Advanced / Kernel update

If you want to have support for the digital mic, sleep mode s2idle and working rotation, you can also try compiling the kernel at [[1]](https://github.com/gled-rs/linux-hp_ap0xxx)

## Issues / Notes

### Audio

The laptop has a Realtek ALC285 Codec with a 4 speaker system built in. External mic with headphones works and legacy driver plays only on two speakers.

For the internal dual digital mic, it currently does not work with the legacy driver ( snd-hda-intel ) but works using snd-sof as described in the kernel bug [https://bugzilla.kernel.org/show_bug.cgi?id=201251#c73](https://bugzilla.kernel.org/show_bug.cgi?id=201251#c73) . Hopefully will be merged fully by kernel 5.3-5.4 and will allow using the microphone.

There is still work needed to support the 4 speakers.

### Camera

The camera is detected as a standard UVC device. The hardware switch works without issue to enable/disable it.

### Mute Button

All the media keys works. The mute button does not light up though.

### Auto Rotation

Installing [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) and [screenrotator-git](https://aur.archlinux.org/packages/screenrotator-git/) autorotation works out of the box.

You can also use this script [[2]](https://gist.github.com/Migacz85/3f544933ce5add438555ba7cd33f0413) but you have to change the line TOUCHPAD="ELAN Touchscreen" by PEN="ELAN2514:00 04F3:280E Pen (0)" and change everywhere the word TOUCHPAD by the word PEN. Indeed, the touchpad do not need to be remaped, since it is deactivated when the screen is rotated, however the PEN is.

WARNING sensor support is broken in 5.0+ kernels because of a kernel bug floating around that cause issues and error messages to be spammed. A simple fix is [https://lkml.org/lkml/2019/3/8/2](https://lkml.org/lkml/2019/3/8/2) ( that patch got reverted in the current 5.2+ kernels, but can be reapplied safely ).

### Dual boot

Works without issues. You can resize the windows partition if you want to keep the stock windows 10 setup from HP ( do not forget to bcdedit the device and osdevice if you follow a linux guide to repartitionning the ntfs drive. You will need to disabled bitlocker also to be able to use the drive ).

### Hp "sureview" privacy screen

Works out of the box. May seem a bit too bright/white for me ? Never had a sureview before so no comparison points available. Windows test after testing linux seems to exhibit same behavior.

### USB-C HDMI-out / dualscreen

Works out of the box with a generic USB-C to HDMI adapter

### Bluetooth

Works out of the box.

### Mobile Broadband

Some configurations include the [Intel XMM 7560](https://www.intel.com/content/www/us/en/wireless-products/mobile-communications/xmm-7560-brief.html) 4G LTE modem, an updated version of [the 7360 with no Linux kernel driver](https://superuser.com/a/1337418).

`lspci` lists the module as:

```
01:00.0 Wireless controller [0d40]: Intel Corporation Device [8086:7560] (rev 01)
	Subsystem: Hewlett-Packard Company Device [103c:8507]

```

### Fingerprint Reader

Not supported at the moment in libfprint, there seems to be a beginning of work to support those types of fingerprint readers here: [https://gitlab.freedesktop.org/vincenth/libfprint.git](https://gitlab.freedesktop.org/vincenth/libfprint.git) The branch synaptics-driver-20190617 contains code that seems to be able to open the fingerprint reader ( if you add the correct device id in drivers/synaptics/synaptics.c ) .

Generates an error after opening though so this is not complete yet.

### Tablet mode

Keyboard is automatically deactivated when screen is rotated to tent or tablet mode. Screen-rotator works great. Using Onboard for onscreen keyboard works also, but xfce4 does not allow Onboard to come automatically when editing text ( Onboard uses the Gnome accessibility, so if you are a Gnome user, you should be fine ).

### IR Camera Login

Works with [Howdy](/index.php/Howdy "Howdy") configured to use /dev/video2 and the patch referenced in [https://github.com/boltgolt/howdy/issues/70#issuecomment-439123621](https://github.com/boltgolt/howdy/issues/70#issuecomment-439123621)

### Battery optimizations

tlp installed, no customisations: around 8-12h of browsing / sysadmin work, depending on the tasks. (Please, see next section, since tlp messes up with suspend).

Powertop display a constant mW consumption of 570 mW ( probably wrong ). There is a setting in the BIOS to allow reporting via ACPI of the battery remaining time. It is disabled by default => to investigate.

### Suspend issues

This model only supports the S0ix, and so only S0 (s2idle) sleep mode is activated. Since this device use a Hynix SSD, it is affected by a bug [[3]](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1801875), resulting in 4-5% battery drain per hour during suspend. A patch set is available, but will not be merged [[4]](https://lore.kernel.org/patchwork/patch/1007283/). In any case, you can install the patched kernel from AUR [linux-hynix](https://aur.archlinux.org/packages/linux-hynix/). The battery drain during suspend should drop to 1-2% per hour.

As it is mentioned by Intel [[5]](https://01.org/blogs/qwang59/2018/how-achieve-s0ix-states-linux), TLP may not work, and so it should not be used with S0ix.

### Sensors

coretemp-isa-0000 Adapter: ISA adapter Package id 0: +51.0°C (high = +100.0°C, crit = +100.0°C) Core 0: +49.0°C (high = +100.0°C, crit = +100.0°C) Core 1: +51.0°C (high = +100.0°C, crit = +100.0°C) Core 2: +48.0°C (high = +100.0°C, crit = +100.0°C) Core 3: +48.0°C (high = +100.0°C, crit = +100.0°C)

acpitz-acpi-0 Adapter: ACPI interface temp1: +49.0°C

iwlwifi-virtual-0 Adapter: Virtual device temp1: +52.0°C

pch_cannonlake-virtual-0 Adapter: Virtual device temp1: +45.0°C

### ACPI Errors

Many ACPI errors are logged on boot:

```
[    0.596152] ACPI BIOS Error (bug): Could not resolve [\_SB.PCI0.XDCI], AE_NOT_FOUND (20180810/dswload2-160)
[    0.596156] ACPI Error: AE_NOT_FOUND, During name lookup/catalog (20180810/psobject-221)
[    0.596158] ACPI Error: Ignore error and continue table load (20180810/psobject-604)
[    0.596159] ACPI Error: Skip parsing opcode Scope (20180810/psloop-543)
[    0.596616] ACPI BIOS Error (bug): Could not resolve [\_SB.PCI0.I2C1.TPL1], AE_NOT_FOUND (20180810/dswload2-160)
[    0.596619] ACPI Error: AE_NOT_FOUND, During name lookup/catalog (20180810/psobject-221)
[    0.596620] ACPI Error: Ignore error and continue table load (20180810/psobject-604)
[    0.596621] ACPI Error: Skip parsing opcode Scope (20180810/psloop-543)
[    0.597096] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.GPLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.597098] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.597100] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.597101] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.TPLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.597103] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.597104] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.597106] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.GUPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.597107] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.597108] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.597110] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.TUPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.597111] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.597112] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.597135] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS01._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.597137] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.597138] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.597140] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS01._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.597141] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.597142] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.598594] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS02._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.598596] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.598597] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.598598] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS02._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.598600] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.598601] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.599963] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS03._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.599965] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.599966] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.599968] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS03._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.599969] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.599970] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.601334] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS04._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.601337] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.601338] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.601339] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS04._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.601341] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.601342] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.602704] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS05._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.602706] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.602707] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.602708] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS05._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.602710] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.602711] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.604077] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS06._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.604079] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.604080] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.604081] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS06._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.604083] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.604084] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.605444] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS07._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.605446] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.605448] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.605449] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS07._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.605451] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.605452] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.606815] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS08._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.606817] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.606818] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.606819] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS08._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.606821] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.606822] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.608067] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS09._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.608069] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.608070] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.608072] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS09._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.608073] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.608074] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.609433] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS10._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.609435] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.609436] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.609437] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.HS10._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.609439] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.609440] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610852] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.USR1._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610854] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610855] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610856] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.USR1._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610858] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610859] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610862] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.USR2._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610863] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610864] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610866] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.USR2._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610868] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610869] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610893] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS01._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610895] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610896] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610897] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS01._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610899] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610900] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610923] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS02._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610925] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610926] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610927] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS02._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610929] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610930] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610953] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS03._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610955] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610956] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610958] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS03._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610959] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610960] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610984] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS04._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610986] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610987] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.610988] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS04._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.610990] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.610991] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.611014] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS05._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.611016] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.611017] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.611018] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS05._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.611020] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.611021] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.611044] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS06._UPC], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.611046] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.611047] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.611048] ACPI BIOS Error (bug): Failure creating [\_SB.PCI0.XHC.RHUB.SS06._PLD], AE_ALREADY_EXISTS (20180810/dswload2-316)
[    0.611050] ACPI Error: AE_ALREADY_EXISTS, During name lookup/catalog (20180810/psobject-221)
[    0.611051] ACPI Error: Skip parsing opcode Method (20180810/psloop-543)
[    0.611121] ACPI BIOS Error (bug): Could not resolve [\_SB.PCI0.XDCI], AE_NOT_FOUND (20180810/dswload2-160)
[    0.611123] ACPI Error: AE_NOT_FOUND, During name lookup/catalog (20180810/psobject-221)
[    0.611124] ACPI Error: Ignore error and continue table load (20180810/psobject-604)
[    0.611125] ACPI Error: Skip parsing opcode Scope (20180810/psloop-543)
[    0.688571] ACPI BIOS Error (bug): Could not resolve [\_SB.PCI0.I2C1.TPL1.TDX], AE_NOT_FOUND (20180810/psargs-330)
[    0.688580] ACPI Error: Method parse/execution failed \_SB.PCI0.I2C1.INC1, AE_NOT_FOUND (20180810/psparse-516)
[    0.688586] ACPI Error: Method parse/execution failed \_SB.PCI0.I2C1._INI, AE_NOT_FOUND (20180810/psparse-516)
[   17.339606] ACPI Error: Field [D128] at bit offset/length 128/1024 exceeds size of target Buffer (160 bits) (20180810/dsopcode-201)
[   17.339616] ACPI Error: Method parse/execution failed \HWMC, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.339628] ACPI Error: Method parse/execution failed \_SB.WMID.WMAA, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.339715] ACPI Error: Field [D128] at bit offset/length 128/1024 exceeds size of target Buffer (160 bits) (20180810/dsopcode-201)
[   17.339721] ACPI Error: Method parse/execution failed \HWMC, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.339731] ACPI Error: Method parse/execution failed \_SB.WMID.WMAA, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.339813] ACPI Error: Field [D128] at bit offset/length 128/1024 exceeds size of target Buffer (160 bits) (20180810/dsopcode-201)
[   17.339819] ACPI Error: Method parse/execution failed \HWMC, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.339829] ACPI Error: Method parse/execution failed \_SB.WMID.WMAA, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.341014] ACPI Error: Field [D128] at bit offset/length 128/1024 exceeds size of target Buffer (160 bits) (20180810/dsopcode-201)
[   17.341022] ACPI Error: Method parse/execution failed \HWMC, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.341033] ACPI Error: Method parse/execution failed \_SB.WMID.WMAA, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.341119] ACPI Error: Field [D128] at bit offset/length 128/1024 exceeds size of target Buffer (160 bits) (20180810/dsopcode-201)
[   17.341125] ACPI Error: Method parse/execution failed \HWMC, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.341136] ACPI Error: Method parse/execution failed \_SB.WMID.WMAA, AE_AML_BUFFER_LIMIT (20180810/psparse-516)
[   17.820943] ACPI: Video Device [GFX0] (multi-head: yes  rom: no  post: no)

```