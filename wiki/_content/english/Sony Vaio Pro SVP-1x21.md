This document will guide you through the process of installing [Arch Linux](/index.php/Arch_Linux "Arch Linux") on the 2013 Sony Vaio Pro [Haswell](https://en.wikipedia.org/wiki/Haswell_(microarchitecture) based [Ultrabook](https://en.wikipedia.org/wiki/Ultrabook "wikipedia:Ultrabook"). 1.1kg for the 13" model

## Contents

*   [1 Pre-installation](#Pre-installation)
    *   [1.1 BIOS Configuration](#BIOS_Configuration)
    *   [1.2 Install media](#Install_media)
    *   [1.3 Internet connection](#Internet_connection)
*   [2 Installation](#Installation)
    *   [2.1 Picking a bootloader](#Picking_a_bootloader)
        *   [2.1.1 UEFI](#UEFI)
            *   [2.1.1.1 GRUB](#GRUB)
            *   [2.1.1.2 Dual-boot Windows 8](#Dual-boot_Windows_8)
*   [3 Post-installation](#Post-installation)
*   [4 Hardware support](#Hardware_support)
    *   [4.1 Sound](#Sound)
    *   [4.2 Touch screen](#Touch_screen)
    *   [4.3 Keyboard backlight](#Keyboard_backlight)
    *   [4.4 Monitor backlight control](#Monitor_backlight_control)
    *   [4.5 Trackpad](#Trackpad)
        *   [4.5.1 Toggle TouchPad via Fn+F1](#Toggle_TouchPad_via_Fn.2BF1)
    *   [4.6 Fan control](#Fan_control)
    *   [4.7 Charging](#Charging)
    *   [4.8 USB ports](#USB_ports)

## Pre-installation

### BIOS Configuration

Get into the BIOS by pushing the assist button when the system is shut off and then hitting *Start BIOS Setup*. **Do not** try to boot from your usb key using *recovery mode*, instead change the boot order in the BIOS. Make the following changes:

```
Intel(R) AT Support System	[Disabled]
Secure Boot			[Disabled]
External Device Boot		[Enabled]
Select 1st Boot Priority	[External Device]

```

If you want to use the legacy boot (non-EFI), change:

```
Boot Mode			[Legacy]

```

### Install media

*   When installing via UEFI from USB [create an UEFI bootable USB from ISO](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface")
*   When booting from USB you might need to append `libata.force=noncq` to the kernel parameters to avoid problems with the SSD. You may even need to make this a persistent kernel parameter when booting from the SSD after installation.
*   Some users were not able to boot when using the rear USB port labelled with a lightning bolt. so use the other one in that case.

### Internet connection

Works as expected as of kernel version 3.11

## Installation

### Picking a bootloader

#### UEFI

Inside the chroot [UEFI variables](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Variables "Unified Extensible Firmware Interface") might not be available. To make them available for installing the bootloader, run

```
   mount -t efivarfs efivarfs /sys/firmware/efi/efivars

```

##### GRUB

Some users are unable to run the install.

**Note:** Grub should install fine if UEFI boot mode is turned on in the BIOS.

##### Dual-boot Windows 8

Windows 8 fast boot mode overwrites your EFI variables. To keep your bootloader in working order, fast boot needs to be disabled. In cmd.exe as Administrator:

```
   powercfg /h off

```

The laptop firmware seems to have a preference to boot Windows even when other bootmanagers are present.

A solution is to move your bootloader to a recognised location such as `/EFI/Boot/bootx64.efi` [[1]](http://www.slideshare.net/slideshow/embed_code/27418512)

It is important to add the efi entry with the label "Windows Boot Manager" and EFI/Boot/Bootx64.efi as path, else Sony firmware does not load it. Add the efi entry for your bootmanager with: `efibootmgr -c -g -d /dev/sda -p 1 -w -L "Windows Boot Manager" -l '\EFI\Boot\Bootx64.efi'` Verify that your bootloader is in the first position of the boot order with: `efibootmgr -v` Reboot and see if your bootloader is loaded. If it does not work you can try to delete the windows boot entries with: `efibootmgr -B -b 000X` where X is the number of the windows efi entry. If you can't boot anymore to windows with this error message: `The boot configuration data for your PC is missing or contains errors. File :\EFI\Microsoft\Boot\BCD Error code: 0xc000000f` then follow these repair steps: [http://woshub.com/how-to-repair-uefi-bootloader-in-windows-8/#!prettyPhoto](http://woshub.com/how-to-repair-uefi-bootloader-in-windows-8/#!prettyPhoto)

## Post-installation

*   For a faster boot, don't forget to undo these BIOS settings:

```
External Device Boot		[Disabled]
Select 1st Boot Priority	[Internal Drive]

```

*   If you want all the power from the Haswell CPU, don't use a kernel version before 3.12.

## Hardware support

### Sound

As the [Installation guide](/index.php/Installation_guide "Installation guide") suggests, install [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) and follow [this](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture") guide to get started. Works out of the box, although main sound card may have index 1, making it non-default (index 0 is taken by Intel HDMI). To fix this, edit **/usr/share/alsa/alsa.conf** (near line 68):

 `/usr/share/alsa/alsa.conf` 
```
defaults.ctl.card 1
defaults.pcm.card 1

```

### Touch screen

Tapping works out of the box. Multitouch gestures work after installing the driver [Multitouch Displays#eGalax](/index.php/Multitouch_Displays#eGalax "Multitouch Displays") and using touchegg [Multitouch Displays#Gestures](/index.php/Multitouch_Displays#Gestures "Multitouch Displays").

Note: touchegg is no longer required in Gnome 3.14 for multitouch gestures.

### Keyboard backlight

Works out of the box. Enables in low amblient light and a key press, turns off after about 20s. Can be customized by modifying `kbd_backlight` and `kbd_backlight_timeout` found in:

```
/sys/devices/platform/sony-laptop/

```

A simple shell script for toggling the backlight, bind to a keyboard shortcut for easy use:

```
#!/bin/sh
path="/sys/devices/platform/sony-laptop/kbd_backlight"
if [ $(<$path) -eq 1 ]
then
	newval=0
else
	newval=1
fi
echo "$newval" > $path

```

Make sure that you can write to this file without root privileges:

```
# chmod 777 /sys/devices/platform/sony-laptop/kbd_backlight

```

### Monitor backlight control

Works out of the box with [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight). By default the backlight is only adjusted by 1% per button press. This can easily be fixed by binding those keys to a [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) command. DM:s like [Xfce](/index.php/Xfce "Xfce") does take larger steps by default.

With KDE 1% adjustment can be fixed by kernel module parameter video.brightness_switch_enabled=0\. This will disable kernel driver 1% adjustment, then KDE PowerDevil correctly adjust brightness by 10% and shows gauge window. There is no need to bind keys.

### Trackpad

Works great with the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) driver. A good base config can be found [here](/index.php/Synaptics#Buttonless_touchpads_.28aka_ClickPads.29 "Synaptics").

#### Toggle TouchPad via Fn+F1

The hotkey that toggles the TouchPad can be configured using [acpid](/index.php/Acpid "Acpid"). Create the following two files to do so:

 `/etc/acpi/events/toggle-touchpad` 
```
event=button.fnf1 FNF1
action=/etc/acpi/actions/toggle-touchpad.sh "%e"
```

**Note:** This file must be marked as executable.
 `/etc/acpi/actions/toggle-touchpad.sh` 
```
#! /bin/sh
PATH="/bin:/usr/bin:/sbin:/usr/sbin"

# Modern method, for Linux 3.11 or later.
sys_enable_file=/sys/devices/platform/sony-laptop/touchpad
if [ -r "$sys_enable_file" ]; then
  read -r is_currently_enabled < "$sys_enable_file"
  echo > "$sys_enable_file" $((1 - $is_currently_enabled))
else

# Older method: have the X11 driver do it
  export DISPLAY=:0
  USER=`who | grep ':0' | grep -o '^\w*' | head -n1`

  if [ "$(su "$USER" -c "synclient -l" | grep TouchpadOff | awk '{print $3}')" == "0" ]; then
      su "$USER" -c "synclient TouchpadOff=1"
  else
      su "$USER" -c "synclient TouchpadOff=0"
  fi
fi
```

**Note:** Restart acpid using systemctl after adding the files.

### Fan control

Works well out of the box. It stays quiet during normal load. Change profile by editing `thermal_control` found in:

```
/sys/devices/platform/sony-laptop/

```

Available profiles can be found in `thermal_profiles` in the same directory.

### Charging

Set the maximum charge to 50/80/100% by modifying `battery_care_limiter` found in:

```
/sys/devices/platform/sony-laptop/

```

In order for changes to take effect, it may be necessary to execute:

```
echo 0 | sudo tee /sys/devices/platform/sony-laptop/battery_care_limiter

```

### USB ports

Some users are having issues with the usb port labeled with a lightning bolt not working for anything but charging. This is a known issue for many Sony laptops.