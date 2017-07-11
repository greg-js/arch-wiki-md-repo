| **Device** | **Working** |
| Intel graphics | Yes |
| HDMI | Not tested |
| VGA | Not tested |
| Audio | Yes |
| USB 3.0 | Yes |
| Ethernet | Not tested |
| WLAN | Yes |
| Bluetooth | Yes |
| Touchpad | Yes |
| Backlight control | Yes - only software control |
| Function keys | Yes |
| Hardware switches | Yes |
| Card reader | Yes |
| Webcam | Not tested |
| USB 3.0 Type-C™ port | Yes |
| Fingerprint Reader | No |

## Contents

*   [1 Device information](#Device_information)
*   [2 Backlight](#Backlight)
*   [3 ACPI errors](#ACPI_errors)
*   [4 Graphic card setup](#Graphic_card_setup)
*   [5 Keyboard mapping](#Keyboard_mapping)
*   [6 PCIe error in dmesg](#PCIe_error_in_dmesg)

## Device information

This is a work in progress with information about the HP ProBook 430 G4\. There are many configurations for these models of HP Probooks. The information below are given from a model HP ProBook 430 G4/822C, BIOS P85 Ver. 01.03 12/05/2016, shipped with a Core i5-7200U, 8GB, 256GB SSD. The notebook supports exchanging two memory modules and support one 2,5" disc drive and one M.2-SSD. The UEFI bios allows legacy boot.

A review in German is available here: [HP ProBook 430 G4 review](http://www.notebookcheck.com/Test-HP-ProBook-430-G4-Core-i7-Full-HD-Laptop.185256.0.html). Basic hardware works out of the box. No configuration was needed. Information for the "Not tested" units will be posted additionally.

```
lspci
00:00.0 Host bridge: Intel Corporation Device 5904 (rev 02)
00:02.0 VGA compatible controller: Intel Corporation Device 5916 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1c.5 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #6 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d58 (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Device 9d71 (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 15)
02:00.0 Network controller: Intel Corporation Wireless 7265 (rev 59)
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)

```

## Backlight

I have not found a solution so far to control the backlight via kernel hardware control keys via kernel. So backlight control works only via software. It works out of the box under Xfce and under i3wm using a custom command "xbacklight -inc/-dec 10".

## ACPI errors

There are lots of acpi related error messages with kernel 4.9.x:

```
Feb 21 16:08:57 localhost kernel: ACPI Error: Field [CAP1] at 96 exceeds Buffer [NULL] size 64 (bits) (20160831/dsopcode-236)
Feb 21 16:08:57 localhost kernel: ACPI Error: Method parse/execution failed [\_SB._OSC] (Node ffff88041f8ef348), AE_AML_BUFFER_LIMIT (20
...
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff88041b43f750 (20160831/exresop-594)
Feb 21 16:09:01 laptop64 kernel: ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20160831/ds
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff88041f89bcd0), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff88041f89b780), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff88041ce2e318 (20160831/exresop-594)
Feb 21 16:09:01 laptop64 kernel: ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20160831/ds
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff88041f89bcd0), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff88041f89b780), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff88041b43f900 (20160831/exresop-594)
Feb 21 16:09:01 laptop64 kernel: ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20160831/ds
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff88041f89bcd0), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff88041f89b780), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: input: HP WMI hotkeys as /devices/virtual/input/input18
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Attempt to CreateField of length zero (20160831/dsopcode-168)
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPI] (Node ffff88041f89b280), AE_AML_OPERAND_VALU
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff88041f89b780), AE_AML_OPERAND_VALU
```

Upstream report: [https://bugzilla.kernel.org/show_bug.cgi?id=194833](https://bugzilla.kernel.org/show_bug.cgi?id=194833) - this seems to be a BIOS implementation bug.

## Graphic card setup

Either modesetting driver or Intel driver seem to work well. Using the Intel driver with DRI3 works well.

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
      Identifier  "Intel Graphics"

     #Driver      "modesetting"
     #Option      "AccelMethod"     "glamor"

      Driver      "intel"
      Option      "AccelMethod"     "sna"

     #Option      "DRI"             "2"

     Option      "Backlight"       "intel_backlight" # use your backlight that works here

EndSection
```

## Keyboard mapping

To avoid error messages appearing in dmesg add

 `/etc/udev/hwdb.d/99-hp_g430_g4.hwdb` 
```
# HP ProBook 430 G4
evdev:atkbd:dmi:bvn*:bvr*:bd*:svnHP:pnHPProBook430G4:pvr*
 KEYBOARD_KEY_f8=wlan                                   # Wireless HW switch button
```

## PCIe error in dmesg

```
Feb 21 16:08:58 localhost systemd-udevd[75]: Assertion '!d->current' failed at src/libsystemd/sd-event/sd-event.c:733, function event_un
...
Feb 21 16:09:01 laptop64 kernel: pcieport 0000:00:1d.0: PCIe Bus Error: severity=Corrected, type=Physical Layer, id=00e8(Receiver ID)
Feb 21 16:09:01 laptop64 kernel: pcieport 0000:00:1d.0:   device [8086:9d18] error status/mask=00000001/00002000
Feb 21 16:09:01 laptop64 kernel: pcieport 0000:00:1d.0:    [ 0] Receiver Error         (First)
```

This one can be fixed with appending pci=noaer to the kernel boot line.