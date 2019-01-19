| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| Fingerprint Reader | Yes |

This article covers the installation and configuration of Arch Linux on a Lenovo T470 laptop.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Firmware (e.g. bios and peripherals)](#Firmware_(e.g._bios_and_peripherals))
*   [2 Kernel and hardware support](#Kernel_and_hardware_support)
    *   [2.1 Fingerprint reader](#Fingerprint_reader)
    *   [2.2 Screen backlight](#Screen_backlight)
    *   [2.3 Thunderbolt 3](#Thunderbolt_3)
    *   [2.4 UEFI boot](#UEFI_boot)
    *   [2.5 BIOS GPT boot](#BIOS_GPT_boot)
    *   [2.6 Special buttons](#Special_buttons)
*   [3 PCI and USB devices](#PCI_and_USB_devices)
    *   [3.1 T470 model 20HD](#T470_model_20HD)
        *   [3.1.1 lspci](#lspci)
        *   [3.1.2 lsusb](#lsusb)
    *   [3.2 T470 model 20JN](#T470_model_20JN)
        *   [3.2.1 lspci](#lspci_2)
        *   [3.2.2 lsusb](#lsusb_2)
    *   [3.3 T470 model 20HD,20HE(Campus model)](#T470_model_20HD,20HE(Campus_model))
        *   [3.3.1 lspci](#lspci_3)
        *   [3.3.2 lsusb](#lsusb_3)
*   [4 See also](#See_also)

## Firmware (e.g. bios and peripherals)

As of writing, the current BIOS version is 1.54. The T470 is one of the models supported officially by Lenovo through the [fwupd](/index.php/Fwupd "Fwupd") firmware update program. If you are using a UEFI boot scheme, this is probably the easiest and most officially supported way to keep all the firmware programs updated.

If it does not work for you or if you prefer these methods, it is still possible to do the BIOS update by booting on a specially crafted disk or USB stick. By visiting the downloads section (T470) an ISO can be downloaded and burned to disk which will perform the update [from Lenovo](http://pcsupport.lenovo.com/gb/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t470/downloads). Or [extracted and copied on a USB Stick](http://www.thinkwiki.org/wiki/BIOS_Upgrade#Booting_from_a_USB_Flash_drive).

Another option that works if you got a CD-ISO from Lenovo is to follow [this guide](https://rikkonsecurity.wordpress.com/2017/06/16/how-to-update-thinkpad-t470-bios-from-linux-using-usb/) and convert the ISO to an IMG prior to dd-ing it to a USB stick.

## Kernel and hardware support

[Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") with Kaby Lake seems to work fine via va-api.

As noted in [Intel graphics](/index.php/Intel_graphics "Intel graphics"), the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver seems to cause more issue than the builtin `modesetting` Xorg driver. Works fine without the intel driver (on a Skylake configuration).

suspend-resume results in the fan holding at 100% without ever spinning down. This is being tracked on the [kernel bugtracker](https://bugzilla.kernel.org/show_bug.cgi?id=196975). The issue [seems to be resolved](https://bugzilla.kernel.org/show_bug.cgi?id=196975#c54) by BIOS 1.43.

### Fingerprint reader

As of writing this, the fingerprint reader is still under [prototype development](https://github.com/nmikhailov/Validity90), but looks like working fine on the T470.

To get the sensor working, it first must be initialized with data. This currently only works with Windows. So if you had used the reader before installing Arch, this should work fine. Otherwise install a Windows version in a virtualbox, connect the Validity Sensor over USB(USB 2.0), install the drivers and use it a few times.

As soon as this step is completed, the sensor can be used under Linux. Check out [Validity90 prototype](https://github.com/nmikhailov/Validity90/tree/master/prototype), build it and check if the sensor is working. Install [fprintd](https://www.archlinux.org/packages/?name=fprintd), [libfprint-vfs0097-git](https://aur.archlinux.org/packages/libfprint-vfs0097-git/) and for testing [fprint_demo](https://aur.archlinux.org/packages/fprint_demo/). You can now enroll your fingers. fprintd and fprint_demo might have be started with superuser privileges.

After setting up the fingerprint sensor is complete, one can use it to login or authenticate for `sudo` or `su`(To use this, launch fprintd_enroll prior as root).

For login edit `/etc/pam.d/login`

Add the following and comment out the other entrys

```
 auth required pam_env.so
 auth sufficient pam_fprintd.so
 auth sufficient pam_unix.so try_first_pass likeauth nullok
 auth required pam_deny.so

```

Do the same for sudo with `/etc/pam.d/sudo` or su with `/etc/pam.d/su`

For more information visit [libfprint](https://github.com/3v1n0/libfprint) and adapt for the vfs0097 package.

### Screen backlight

Without the `intel` driver ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)), neither `xbacklight` or `xrandr` brightness control are working. It is possible that, with the good `acpi_*` kernel parameters, the backlight related keys do their job.

Other workaround exists, such as described [on this post](https://bbs.archlinux.org/viewtopic.php?pid=1449243#p1449243) or in the wiki [acpid#Enabling backlight control](/index.php/Acpid#Enabling_backlight_control "Acpid"). Using the [acpilight](https://www.archlinux.org/packages/?name=acpilight) package as a `xbacklight` replacement works well. You can also check [this repository](https://lab.knightsofnii.com/kristaba/tpacpi-backlight)] as a base to add the ACPI rules to call `xbacklight` when backlight keys are pressed.

**Note:** The [acpilight](https://www.archlinux.org/packages/?name=acpilight) package is known to allow controlling the ThinkPad keyboard backlight. Similar ACPI rules should allow to toggle it when the keyboard backlight key is pressed.

### Thunderbolt 3

With the latest kernel (4.12.12 as of writing), the *Alpine Ridge* thunderbolt 3 controller is recognized without any additional configuration. Using a generic thunderbolt 3 to HDMI + USB3 hub works out of the box (the HDMI output is recognized by xrandr as DP-1 output).

### UEFI boot

After configuring the BIOS setup to allow UEFI boot (either *UEFI only* or *both*), it works flawlessly.

### BIOS GPT boot

**Note:** I was unable to boot with a GPT + BIOS configuration, and therefore switch to GPT + EFI. However, until another confirmation, it is quite probable that was caused by some bad configuration from my side.

I can confirm that issue. Even with a recent bios (1.52), it doesn't work.

I had to trick my ThinkPad into UEFI (because my bios is locked, found that method by pure luck). It works by installing the [syslinux](/index.php/Syslinux "Syslinux") bootloader on your freshly installed arch (be sure to follow the GPT specific instructions at [Syslinux#GUID partition table](/index.php/Syslinux#GUID_partition_table "Syslinux")) and the boot that syslinux with the arch install iso ('Boot existing OS' -> press `TAB` -> replace `hd0 0` with `hd1 0`). Syslinux should show you an option to boot the ArchLinux installation in UEFI mode. Mount you Arch installation, `arch-chroot` into it and install [GRUB](/index.php/GRUB "GRUB") (or your favorite bootloader) for UEFI. That did the trick for me.

You have to create a proper UEFI partition. Have a look at [partitioning](/index.php/Partitioning "Partitioning").

### Special buttons

Some special buttons are not supported by X server due to keycode number limit.

| Key combination | Scancode | Keycode |
| `Fn+F11` | `0x49` | `374` `KEY_KEYBOARD` |
| `Fn+F12` | `0x45` | `364` `KEY_FAVORITES` |

You can remap unsupported keys using [udev hwdb](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes"):

 `/etc/udev/hwdb.d/90-thinkpad-keyboard.hwdb` 
```
evdev:name:ThinkPad Extra Buttons:dmi:bvn*:bvr*:bd*:svnLENOVO*:pn*
 KEYBOARD_KEY_45=prog1
 KEYBOARD_KEY_49=prog2

```

Update hwdb after editing the rule.

```
# udevadm hwdb --update
# udevadm trigger --sysname-match="event*"

```

## PCI and USB devices

### T470 model 20HD

Kernel '4.10.13-1-ARCH'

#### lspci

```
00:00.0 Host bridge: Intel Corporation Device 5904 (rev 02)
00:02.0 VGA compatible controller: Intel Corporation Device 5916 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1d.2 PCI bridge: Intel Corporation Device 9d1a (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d58 (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Device 9d71 (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-V (rev 21)
04:00.0 Network controller: Intel Corporation Device 24fd (rev 78)
3e:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a804

```

#### lsusb

```
Bus 002 Device 007: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 008: ID 138a:0097 Validity Sensors, Inc. 
Bus 001 Device 005: ID 5986:111c Acer, Inc 
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### T470 model 20JN

Quite specific model, comes with a 6th generation Intel processor (Skylake) instead of a Kaby Lake like most T470 models. Output of lspci and lsusb with kernel 4.12.12-1.

#### lspci

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 520 (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1d.2 PCI bridge: Intel Corporation Device 9d1a (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection I219-LM (rev 21)
04:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
05:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
06:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
06:01.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
06:02.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
3d:00.0 USB controller: Intel Corporation Device 15c1 (rev 01)

```

#### lsusb

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 002: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### T470 model 20HD,20HE(Campus model)

#### lspci

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 02)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 620 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.6 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #7 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1d.2 PCI bridge: Intel Corporation Device 9d1a (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-V (rev 21)
04:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
3e:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM961/PM961

```

#### lsusb

```
Bus 002 Device 003: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 138a:0097 Validity Sensors, Inc. 
Bus 001 Device 003: ID 5986:111c Acer, Inc 
Bus 001 Device 002: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## See also

*   [Lenovo Support Page](http://support.lenovo.com/us/en/products/Laptops-and-netbooks/ThinkPad-T-Series-laptops/ThinkPad-T470?beta=false)