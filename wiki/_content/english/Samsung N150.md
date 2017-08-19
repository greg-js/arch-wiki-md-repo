This article describes the installation and configuration of 64-bit Arch Linux on the Samsung N150 netbook. Based on the output from *dmidecode*, this material might also be useful for the N210, N220 and NB30 models.

## Contents

*   [1 Hardware overview](#Hardware_overview)
*   [2 Installation](#Installation)
*   [3 Device configuration](#Device_configuration)
    *   [3.1 Graphics](#Graphics)
        *   [3.1.1 Backlight](#Backlight)
    *   [3.2 Audio](#Audio)
    *   [3.3 Suspend to RAM (S3 sleep)](#Suspend_to_RAM_.28S3_sleep.29)
    *   [3.4 Suspend to disk (hibernate)](#Suspend_to_disk_.28hibernate.29)
    *   [3.5 Touchpad](#Touchpad)
*   [4 Fn keys](#Fn_keys)

## Hardware overview

The Samsung N150 netbook is equipped with the [Intel Atom](https://en.wikipedia.org/wiki/Intel_Atom "wikipedia:Intel Atom") N450 ("Pineview") CPU with integrated [Intel GMA 3100 GPU](/index.php/Intel "Intel") and "Pine Trail" chipset. Unlike the prior single-core Intel Atom N2xx and Z series processors, the N450 supports the x86_64 instruction set. Although DMI information suggests the motherboard will accept up to 8 GiB RAM, the integrated memory controller in the Atom N450 can address a maximum of 2 GiB. Since the hardware is limited to a 32-bit address space, the primary benefit to running the 64-bit version of Arch on this system is to take advantage of AUR packages built on more powerful 64-bit systems belonging to the same owner.

Shipping versions of the N150 (as of early March 2010) include the "starter" edition of a proprietary operating system and therefore include only 1 GiB RAM in the form of a single DDR2 667 MhZ SODIMM, which is user-replaceable. Per the DMI information, the unit contains two mini PCI express slots, one of which is populated by the included Atheros AR9285 wireless card. Other versions of this model are apparently available with an integrated 3G WAN adapter installed in the other slot.

External connectivity provided on the system includes 3 USB 2.0 ports, a single VGA port, 10/100 Ethernet (Marvell 88E8040 PCI-E), headphone/microphone jacks, and an integrated card reader (SD/SDHC/MMC). An integrated VGA-resolution webcam is connected to the internal USB controller.

## Installation

Since netbooks lack optical drives, the preferred installation mechanism is via a USB flash drive. Upon first boot into the 2009.08 installation media, the system will reboot after CPU initialization. Subsequent reboots using the same kernel will not exhibit this behavior, although booting into a later installed kernel may reboot the first time.

This article assumes the entire hard disk will be used for Arch, eliminating the manufacturer-supplied software (including the recovery partitions). It is not entirely clear which partitions are required for the recovery software to function properly: retention of the only first partition, of unknown type, is **not** sufficient. If a recovery mechanism for the factory-supplied software is desired, a set of recovery DVDs should be created using an external DVD burner prior to installing Arch.

Upon the first installation, *cfdisk* will exit with an error due to the existing partition layout extending beyond the end of the disk (using Linux default geometries). The solution is to run fdisk and create a new, empty partition table.

**Warning:** This operation will destroy the current hard disk partitions, effectively causing all data on the hard disk to be lost.

```
fdisk /dev/sda << EOF
o
w
EOF

```

After initializing the drive with an empty partition table, cfdisk will work properly in the Arch installer.

## Device configuration

### Graphics

The [Intel GMA 3100 GPU](/index.php/Intel "Intel"), embedded in the Atom 450 CPU package, works out of the box with [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Early KMS initialization seems to improve boot speed slightly and can be enabled by adding the following to the `MODULES` line in `/etc/mkinitcpio.conf`:

```
MODULES="**intel_agp i915**"

```

Run `mkinitcpio -p linux` to make the configuration effective.

Unlike the prior [Samsung N140](/index.php/Samsung_N140 "Samsung N140") model, the N150 does not seem to suffer from display powersaving problems.

Once `Fn` keys are enabled (see below), `Fn+F4` will toggle between LCD only, extended, and cloned modes automatically whenever an external screen is connected to the VGA port.

#### Backlight

Like other Samsung laptops and netbooks, direct ACPI control of the backlight is not possible on the N150\. You can fix brightness control issue by adding the following in `/etc/X11/xorg.conf.d/20-intel.conf`:

```
Section "Device"
        Driver      "intel"
        Option      "Backlight"  "intel_backlight"
        Identifier "card0"
EndSection

```

### Audio

Intel HD Audio works out of the box on this model, although the volume for the "speaker" mixer channel needs to be increased from zero. Install the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package to acquire an init script for restoring the volume at boot time.

For N210 owners the internal microphone might not work out of the box. You have to run the following:

```
# echo 0x19 0x90A70011 > /sys/class/sound/hwC0D0/user_pin_configs
# echo 1 > /sys/class/sound/hwC0D0/reconfig

```

### Suspend to RAM (S3 sleep)

With Gnome 2.28 and the [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager) package installed, suspend-to-RAM works out of the box whenever the netbook lid is closed. The suspend process requires up to 30 seconds or so to take effect. Waking from S3 requires activating the power button under the default configuration. Waking upon opening the lid, or pressing a key, can be enabled in the BIOS.

With the realtek wireless card, wireless doesn't always come up again on suspend. Unloading and reloading the *r8192e_pci* module brings it back. This can also be configured automatically with [Pm-utils](/index.php/Pm-utils "Pm-utils").

From kernel 2.6.35 there is a regression that may prevent the system to comming back (experienced on N210 with 2.6.39) from suspend. The solution is, to create a file `/etc/pm/sleep.d/10cpu-disable` with the following content

```
#!/bin/sh
#
# 10cpu-disable: turn of the second CPU before suspend. 
# fixes resume problem on 2.6.35-2.6.39... on Samsung Nxxx laptops.
# bug: https://bugzilla.kernel.org/show_bug.cgi?id=21952

case "$1" in
        hibernate|suspend)
                echo 0 > /sys/devices/system/cpu/cpu1/online
        ;;
        thaw|resume)
                echo 1 > /sys/devices/system/cpu/cpu1/online
        ;;
        *) exit $NA
        ;;
esac

```

### Suspend to disk (hibernate)

Hibernate support with [pm-utils](/index.php/Pm-utils "Pm-utils") does not work reliably. Upon resuming from hibernation, there are ELF header errors related to glibc, effectively preventing any new applications (including `shutdown`) from starting. Moreover, even if this problem can be resolved, the process of resuming from the swap partition (before the errors are observed) is slightly longer than a cold boot.

With the kernel 2.6.36 series, some samsung N series machines requires to add the parameter `intel_idle.max_cstate=0` to the kernel line for the hibernation/suspension to work correctly.

### Touchpad

The Synaptics touchpad works for single-finger operation with scrolling along the right edge out of the box. When `Fn+F10` is pressed, the BIOS automatically enables or disables the touchpad hardware. To receive notification of this event, it is useful to install the [xosd](https://www.archlinux.org/packages/?name=xosd) package and configure a script to print a message whenever `Fn+F10` is pressed (see below for Fn key configuration). This script should be saved in `/usr/local/bin/report_touchpad`:

```
#!/bin/bash

FONT='-adobe-helvetica-bold-*-*-*-34-*-*-*-*-*-*-*'
DELAY=1
state=Unknown

case "$1" in
        on)
                state=Enabled
        ;;
        off)
                state=Disabled
        ;;
        *)
                echo "usage: $0 {on|off}"
                exit 2
        ;;
esac

osd_cat -A center -p middle -f $FONT -d $DELAY << EOF
Touchpad $state
EOF

exit 0

```

To enable tapping, the easiest solution is to install [gpointing-device-settings](https://www.archlinux.org/packages/?name=gpointing-device-settings). Although the literature shipping with the netbook claims multitouch support (for two-finger tap, two-finger scroll, etc.), it does not appear to work properly.

For n220 owners (these parameters haven't been tested on n150 but it migth work), these touchpad rules enable multitouch (/etc/hal/fdi/policy/11-x11-synaptics.fdi)

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<deviceinfo version="0.2">
        <device>
                <match key="info.capabilities" contains="input.touchpad">
                        <merge key="input.x11_driver" type="string">synaptics</merge>
                        <merge key="input.x11_options.TapButton1" type="string">1</merge>
                        <merge key="input.x11_options.TapButton2" type="string">2</merge>
                        <merge key="input.x11_options.TapButton3" type="string">3</merge>

                        <merge key="input.x11_options.SHMConfig" type="string">true</merge>

                        <merge key="input.x11_options.VertEdgeScroll" type="string">false</merge>
                        <merge key="input.x11_options.PalmDetect" type="string">false</merge>

                        <merge key="input.x11_options.VerteScrollDelta" type="string">100</merge>

                        <merge key="input.x11_options.VertTwoFingerScroll" type="string">true</merge>
                        <merge key="input.x11_options.HorizTwoFingerScroll" type="string">true</merge>
                        <merge key="input.x11_options.EmulateTwoFingerMinZ" type="string">40</merge>
                        <merge key="input.x11_options.EmulateTwoFingerMinW" type="string">5</merge>

                </match>
        </device>
</deviceinfo>

```

## Fn keys

[Samsung Tools](https://launchpad.net/samsung-tools) can be installed to quickly get the `Fn` key combinations work. It is available in AUR ([samsung-tools](https://aur.archlinux.org/packages/samsung-tools/)).

Several of the special `Fn` key combinations work out of the box with the N150, but most do not. Unusual scancodes are reported to the kernel, which does not know how to convert these codes to keycodes natively. Worse, many of the scancodes produce a key press event without a corresponding key release event. Appending the following lines to /etc/rc.local will enable all `Fn` keys and map them properly:

```
setkeycodes e002 227   # Fn+F4 maps to switchvidmode
setkeycodes e003 236   # Fn+F2 maps to battery
setkeycodes e004 148   # Fn+F5 maps to prog1
setkeycodes e006 238   # Fn+F9 maps to wlan
setkeycodes e008 225   # Fn+Up maps to brightnessup
setkeycodes e009 224   # Fn+Dn maps to brightnessdown
setkeycodes e031 149   # Fn+F7 maps to prog2
setkeycodes e033 202   # Fn+F8 maps to prog3
setkeycodes e077 191   # Fn+F10 maps to F21 whenever the touchpad is enabled
setkeycodes e079 192   # Fn+F10 maps to F22 whenever the touchpad is disabled

# Ensure key release events occur for all except Fn+F7, which properly reports a key release for some reason
echo 130,131,132,134,136,137,179,247,249 > /sys/devices/platform/i8042/serio0/force_release

```

To enable hotkeys to change backlight, wireless, and system performance settings, it is necessary to give regular users certain permissions via the [sudo](/index.php/Sudo "Sudo") command. Run `# visudo` and add the following to the Cmnd alias specifications:

```
Cmnd_Alias NETBOOK_CMDS = /usr/local/bin/backlight, /usr/local/bin/rftoggle, /usr/local/bin/cpufreq_toggle

```

Then add the following to the bottom of the file:

```
%users ALL=(ALL) NOPASSWD: NETBOOK_CMDS

```

Now custom keyboard shortcuts can be added to Gnome by means of the "Keyboard Shortcuts" preferences.

| Name | Command | Key |
| Touchpad disabled | /usr/local/bin/report_touchpad off | Press Fn+F10 while touchpad enabled |
| Touchpad enabled | /usr/local/bin/report_touchpad on | Press Fn+F10 while touchpad disabled |
| Toggle CPU frequency scaling | /usr/local/bin/cpufreq_toggle_osd | Fn+F8 |
| Raise backlight | sudo /usr/local/bin/backlight up | Fn+Up arrow |
| Lower backlight | sudo /usr/local/bin/backlight down | Fn+Down arrow |
| Toggle wireless | sudo /usr/local/bin/rftoggle | Fn+F9 |
| Toggle backlight | sudo /usr/local/bin/backlight toggle | Fn+F5 |