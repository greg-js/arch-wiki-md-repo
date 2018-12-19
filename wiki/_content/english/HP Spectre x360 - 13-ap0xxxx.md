| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | bluetooth |
| Audio | Partially Working | snd_hda_intel |
| Touchpad | Working | ? |
| Touchscreen | Working | hid_multitouch |
| Pen input | Working with quirks | ? |
| Webcam | working | uvcvideo |
| Card Reader | Working | rtsx_pci |
| Wireless Switch | Untested | ? |
| Function/Multimedia Keys | Working | ? |
| Suspend/Resume | Working | ? |
| Fingerprint sensor | Not working | ? synaptic 06cb:00bb |

This article covers specific configuration of this laptop. Currently based on experience with Xfce4, running on X.org.

## Contents

*   [1 Hardware Info](#Hardware_Info)
    *   [1.1 Hardware Options](#Hardware_Options)
    *   [1.2 lspci for 13-ap0xxxx](#lspci_for_13-ap0xxxx)
    *   [1.3 lsusb for 13-ap0xxxx](#lsusb_for_13-ap0xxxx)
*   [2 Installation](#Installation)
*   [3 Issues / Notes](#Issues_/_Notes)
    *   [3.1 Audio](#Audio)
    *   [3.2 Camera](#Camera)
    *   [3.3 Mute Button](#Mute_Button)
    *   [3.4 Auto Rotation](#Auto_Rotation)
    *   [3.5 Dual boot](#Dual_boot)
    *   [3.6 Hp "sureview" privacy screen](#Hp_"sureview"_privacy_screen)
    *   [3.7 USB-C HDMI-out / dualscreen](#USB-C_HDMI-out_/_dualscreen)
    *   [3.8 Bluetooth](#Bluetooth)
    *   [3.9 ACPI Errors](#ACPI_Errors)
    *   [3.10 Pen input](#Pen_input)
    *   [3.11 Battery optimizations](#Battery_optimizations)
    *   [3.12 Sensors](#Sensors)

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

Installation needs a bit of workarounds ( as of 2018.12 arch iso ).

First you will need to disable secureboot in BIOS (ESC to bring up menu, then F10 for BIOS and/or F9 for Boot options).

Using bios F.08 I somehow had to enable legacy boot support to be able to boot even if using UEFI ( this may be a side effect of testing many things, needs to be clarified ).

Upon boot, you need to edit the kernel cmdline ( press e in UEFI mode when presented with the list of boot options on the arch USB key ) and remove the first initrd lines mentionning intel and amd.

Then follow the [installation guide](/index.php/Installation_guide "Installation guide") as usual.

## Issues / Notes

### Audio

The laptop has a Realtek ALC285 Codec with a 4 speaker system built in. Internal microphone do not work ( or I have not yet found the correct parameters ). External mic with headphones works.

### Camera

The camera is detected as a standard UVC device. The hardware switch works without issue to enable/disable it.

### Mute Button

All the media keys works. The mute button does not light up though.

### Auto Rotation

Installing screen-rotator and iio-sensor-proxy: works out of the box.

### Dual boot

Works without issues. You can resize the windows partition if you want to keep the stock windows 10 setup from HP ( do not forget to bcdedit the device and osdevice if you follow a linux guide to repartitionning the ntfs drive. You will need to disabled bitlocker also to be able to use the drive ).

### Hp "sureview" privacy screen

Works out of the box. May seem a bit too bright/white for me ? Never had a sureview before so no comparison points available. Windows test after testing linux seems to exhibit same behavior.

### USB-C HDMI-out / dualscreen

Works out of the box with a generic USB-C to HDMI adapter

### Bluetooth

Seems to work out of the box. May need further testing. Some random disconnects are experienced with an apple magic mouse. Unable to pair an apple magic touchpad that was paired without issues to my previous computer.

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

### Pen input

Working, but seems like using the pen disable the touchscreen. more testing needed.

### Battery optimizations

tlp installed

Powertop display a constant mW consumption of 570 mW ( probably wrong ). There is a setting in the BIOS to allow reporting via ACPI of the battery remaining time. It is disabled by default => to investigate.

### Sensors

coretemp-isa-0000 Adapter: ISA adapter Package id 0: +51.0°C (high = +100.0°C, crit = +100.0°C) Core 0: +49.0°C (high = +100.0°C, crit = +100.0°C) Core 1: +51.0°C (high = +100.0°C, crit = +100.0°C) Core 2: +48.0°C (high = +100.0°C, crit = +100.0°C) Core 3: +48.0°C (high = +100.0°C, crit = +100.0°C)

acpitz-acpi-0 Adapter: ACPI interface temp1: +49.0°C

iwlwifi-virtual-0 Adapter: Virtual device temp1: +52.0°C

pch_cannonlake-virtual-0 Adapter: Virtual device temp1: +45.0°C