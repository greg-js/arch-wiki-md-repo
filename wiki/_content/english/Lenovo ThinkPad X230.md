Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [ThinkPad docks](/index.php/ThinkPad_docks "ThinkPad docks")
*   [HiDPI](/index.php/HiDPI "HiDPI")

Lenovo ThinkPad X230 [official page](https://pcsupport.lenovo.com/en/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x230), [datasheet](https://psref.lenovo.com/syspool/Sys/PDF/withdrawnbook/ThinkPad_X230.pdf), [hardware maintenance manual](https://us.download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles_pdf/x230_x230i_hmm_en_0b48666_01.pdf), [ThinkWiki](https://www.thinkwiki.org/wiki/Category:X230).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Screen](#Screen)
    *   [1.3 Brightness](#Brightness)
    *   [1.4 Suspend to ram](#Suspend_to_ram)
    *   [1.5 UMTS Modem](#UMTS_Modem)
*   [2 Input devices](#Input_devices)
    *   [2.1 TrackPoint](#TrackPoint)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Keyboard backlight control keys](#Keyboard_backlight_control_keys)
    *   [2.4 Sound control buttons](#Sound_control_buttons)
    *   [2.5 Fingerprint reader](#Fingerprint_reader)
    *   [2.6 X230T (tablet version)](#X230T_(tablet_version))
        *   [2.6.1 Wacom tablet input](#Wacom_tablet_input)
        *   [2.6.2 Multitouch screen for the X230t](#Multitouch_screen_for_the_X230t)
*   [3 OpenCL](#OpenCL)
*   [4 Power Saving](#Power_Saving)
    *   [4.1 TLP](#TLP)
    *   [4.2 Charge thresholds](#Charge_thresholds)
    *   [4.3 Fan control](#Fan_control)
*   [5 UEFI](#UEFI)
    *   [5.1 Boot configuration](#Boot_configuration)
    *   [5.2 USB UEFI update](#USB_UEFI_update)
    *   [5.3 Trusted Platform Module](#Trusted_Platform_Module)
*   [6 Known issues](#Known_issues)
*   [7 See also](#See_also)

## Configuration

### Kernel

Enable Intel [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") driver:

 `/etc/mkinitcpio.conf` 
```
MODULES="i915"

```

After saving the above files, make sure to regenerate your initram image by the command `mkinitcpio -p linux`, and follow the steps in [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### Screen

X230 has IPS or TN screen with 125.37 DPI. Refer to [HiDPI](/index.php/HiDPI "HiDPI") page for more information. It can be set with command `xrandr --dpi 125.37` using `[.xinitrc](/index.php/.xinitrc ".xinitrc")`, `[.xsession](/index.php/Xsession "Xsession")` or other autostarts.

### Brightness

If you experience that your brightness setting is not restored on resume from suspend, then create config:

 `/usr/share/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
Identifier "card0"
Driver "intel"
Option "Backlight" "intel_backlight"
BusID "PCI:0:2:0"
EndSection

```

### Suspend to ram

There is an issue with system shutdown with power saving tools that cannot distinguish sys devices. You will need to add to the systemd shutdown trigger on this machine or else you'll get a system reboot when you shutdown the machine. Put this in /etc/rc.local.shutdown and update and enable its service, if not already.

 `/etc/rc.local.shutdown` 
```
#!/bin/bash
# /etc/rc.local.shutdown: Local shutdown script.
# A script to act as a workaround for the bug in the runtime power management module, which causes thinkpad laptops to restart after shutting down. 
# Bus list for the runtime power management module.
buslist="pci i2c usb"
for bus in $buslist; do                                                             
  for i in /sys/bus/$bus/devices/*/power/control; do                              
    echo on > $i
  done
done

```
 `/usr/lib/systemd/system/rc-local-shutdown.service` 
```
[Unit]
Description=/etc/rc.local.shutdown Compatibility
ConditionFileIsExecutable=/etc/rc.local.shutdown
DefaultDependencies=no
After=rc-local.service basic.target
Before=shutdown.target

[Service]
Type=oneshot
ExecStart=/etc/rc.local.shutdown
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=shutdown.target

```

### UMTS Modem

	*Main article: [ThinkPad mobile Internet](/index.php/ThinkPad_mobile_Internet "ThinkPad mobile Internet")*

**Warning:** Official UEFI comes with whitelist of PCI boards (e.g. Wi-Fi and UMTS miniPCI cards). After installing unapproved PCI device boot will be interrupted with error: `1802: Unauthorized network card is plugged in - Power off and remove the miniPCI network card (0AF0/7201). System is halted.`

Some models come with an integrated USB UMTS modem.

 `$ lsusb -d 0bdb:1926`  `Bus 003 Device 004: ID 0bdb:1926 Ericsson Business Mobile Networks BV H5321 gw Mobile Broadband Driver` 

In order for it to work with [NetworkManager](/index.php/NetworkManager "NetworkManager"), you will need to install [ModemManager](https://www.archlinux.org/packages/?name=modemmanager) from the official repositories.

For it to be recognized by ModemManager, you also need to set the kernel module option to:

 `/etc/modprobe.d/umts-modem.conf`  `options cdc_ncm prefer_mbim=N` 

## Input devices

### TrackPoint

	*Main article: [TrackPoint](/index.php/TrackPoint "TrackPoint")*

Laptop equipped with combined pointing device called [UltraNav™](https://thinkwiki.org/wiki/UltraNav). It incorporates small touchpad, three hardware buttons and TrackPoint.

### Touchpad

**Note:** [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") superseded by [libinput](/index.php/Libinput "Libinput").

The original configuration renders the touchpad quite useless, as it behaves very jumpily. [Ubuntu Bugtracker](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-input-synaptics/+bug/1042069/comments/5) offers a solution for this issue. Add the following:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
Section "InputClass"
        Identifier "touchpad"
        MatchProduct "SynPS/2 Synaptics TouchPad"
        # MatchTag "lenovo_x230_all"
        Driver "synaptics"
        # fix touchpad resolution
        Option "VertResolution" "100"
        Option "HorizResolution" "65"
        # disable synaptics driver pointer acceleration
        Option "MinSpeed" "1"
        Option "MaxSpeed" "1"
        # tweak the X-server pointer acceleration
        Option "AccelerationProfile" "2"
        Option "AdaptiveDeceleration" "16"
        Option "ConstantDeceleration" "16"
        Option "VelocityScale" "20"
        Option "AccelerationNumerator" "30"
        Option "AccelerationDenominator" "10"
        Option "AccelerationThreshold" "10"
	# Disable two fingers right mouse click
	Option "TapButton2" "0"
        Option "HorizHysteresis" "100"
        Option "VertHysteresis" "100"
        # fix touchpad scroll speed
        Option "VertScrollDelta" "500"
        Option "HorizScrollDelta" "500"
EndSection

```

Setting e.g. the motion-acceleration value in *dconf* to 2.8 works nicely.

### Keyboard backlight control keys

**Note:** On most X230 models, backlight works by default without any issues. Use below only in case of any problems.

Due to an issue with the firmware of several ThinkPads the backlight control keys (`Fn` + `F8/F9` on the X230) sometimes don't work correctly. Setting the brightness via e.g. the GNOME power control panel or altering the brightness value in *sysfs* is possible. The issue can be temporarily and partially fixed in adding the `acpi_osi="!Windows 2012"` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). The fix is partial in that only 8 steps are accessible via the keys. See [[1]](https://bugzilla.kernel.org/show_bug.cgi?id=51231) for details.

Power saving [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") in addition to graphics card power saving, are shown below. `acpi_backlight=vendor` loads the vendor specific [Backlight#ACPI](/index.php/Backlight#ACPI "Backlight") driver (i.e. thinkpad_acpi) so the brightness keys (Fn + F8 and Fn + F9) work correctly.

Note that the `acpi_backlight=vendor` kernel option also works with the standard Arch kernel (currently 3.7.10-1) and has the additional bonus that (`Fn+Space`) controls the keyboard lighting.

### Sound control buttons

Red LED mute indicators light up automatically, if corresponding channel *muted* in `[alsamixer](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture")`. Easiest way to make buttons work is to install [PulseAudio](/index.php/PulseAudio "PulseAudio") and it's plugin for your [desktop environment](/index.php/Desktop_environment "Desktop environment").

*   [GNOME](/index.php/GNOME "GNOME") - works out of the box
*   [Xfce](/index.php/Xfce "Xfce") - install [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) [xfce4-pulseaudio-plugin](https://www.archlinux.org/packages/?name=xfce4-pulseaudio-plugin), add plugin to panel and reboot. Additionally [xfce4-pulseaudio-plugin](https://www.archlinux.org/packages/?name=xfce4-pulseaudio-plugin) uses [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) as mixer and [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd) for sound level popups
*   Handle ACPI events with [acpid](/index.php/Acpid "Acpid") the [hard way](https://makandracards.com/makandra/47162-how-to-enable-the-thinkpad-microphone-mute-key-on-ubuntu-16-04). Some functions like `thinkpad-mutemic` implemented in [thinkpad-scripts](https://aur.archlinux.org/packages/thinkpad-scripts/)
*   See also [ThinkPad: Mute button](/index.php/ThinkPad:_Mute_button "ThinkPad: Mute button")

### Fingerprint reader

Supported by [fprint](/index.php/Fprint "Fprint") out of the box. Used with [PAM](/index.php/PAM "PAM") for authentication, eliminating necessity of password input (logon, sudo). Though it's impossible to turn laptop on and boot Arch right into a [desktop environment](/index.php/Desktop_environment "Desktop environment") by just one finger swipe.

### X230T (tablet version)

#### Wacom tablet input

Works out of the box with [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom). See [Wacom tablet](/index.php/Wacom_tablet "Wacom tablet").

#### Multitouch screen for the X230t

Some X230t models have a multitouch screen in addition to the Wacom tablet. Works out of the box with [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput).

## OpenCL

Thinkpad X230 based on Intel [Ivy Bridge](https://en.wikipedia.org/wiki/Ivy_Bridge_(microarchitecture) (3rd generation) platform which meets [OpenCL](/index.php/OpenCL "OpenCL") 1.2 specification. Unfortunately GPU support in Linux is broken, so [beignet](https://www.archlinux.org/packages/?name=beignet) and [intel-opencl](https://aur.archlinux.org/packages/intel-opencl/) won't work. Use CPU-only [intel-opencl-runtime](https://aur.archlinux.org/packages/intel-opencl-runtime/) instead.

OpenCL computation performance differ between CPU and GPU, depending on task. In many cases GPU is preferable. For *Core(TM) i5-3210M* CPU, which incorporates *HD Graphics 4000* GPU:

*   GPU `[hashcat](/index.php/Hashcat "Hashcat") -m2500 -b -D 2 --force` reports 3095 H/s (checked in Windows)
*   CPU `[hashcat](/index.php/Hashcat "Hashcat") -m2500 -b -D 1` reports only 2660 H/s, which is the same as no-OpenCL `aircrack-ng -S`

In this example OpenCL don't give any advantage and better look for other options like [building native binary](/index.php/Makepkg#Building_optimized_binaries "Makepkg") for your system.

## Power Saving

	*Main article: [Power saving](/index.php/Power_saving "Power saving")*

### TLP

Users of [TLP](/index.php/TLP "TLP") need to pay attention to a hardware bug according to which it is recommended to only use either the upper or lower charging threshold. The following configuration is recommended by the developer of TLP.[[2]](http://thinkpad-forum.de/threads/184510-elementary-OS-Thinkpad-X230-einrichten?p=1865345&viewfull=1#post1865345)

 `/etc/default/tlp` 
```
START_CHARGE_THRESH_BAT0=67
STOP_CHARGE_THRESH_BAT0=100

```

### Charge thresholds

In order to prolong battery lifespan, especially if laptop always connected to AC power supply, it's possible to keep battery charge between 40-80 %. You can use [tpacpi-bat](https://www.archlinux.org/packages/?name=tpacpi-bat) (written in Perl) for [setting charge thresholds](/index.php/Tp_smapi#2nd_option,_tpacpi-bat "Tp smapi"). This tool was superseded by `[natacpi](https://linrunner.de/en/tlp/docs/tlp-faq.html)`, which included in kernel 4.17 and supported by [TLP](/index.php/TLP "TLP"). Though it's possible to change thresholds directly. Values will be stored in battery microcontroller and will survive reboot, but reset if you remove the battery.

```
# echo 40 > /sys/class/power_supply/BAT0/charge_start_threshold
# echo 80 > /sys/class/power_supply/BAT0/charge_stop_threshold

```

### Fan control

To optimize fan control, install and setup [thinkfan](/index.php/Fan_speed_control#ThinkPad_laptops "Fan speed control"). Then use the following configuration:

 `/etc/thinkfan.conf` 
```
tp_fan /proc/acpi/ibm/fan
hwmon /sys/class/thermal/thermal_zone0/temp

(0, 0,  60)
(1, 53, 65)
(2, 55, 66)
(3, 57, 68)
(4, 61, 70)
(5, 64, 71)
(7, 68, 32767)
```

## UEFI

Laptop incorporates InsydeH2O® UEFI BIOS with classic text interface. It supports [UEFI](/index.php/UEFI "UEFI") with [Secure Boot](/index.php/Secure_Boot "Secure Boot"), UEFI-CSM and Legacy BIOS modes.

### Boot configuration

UEFI boot options can be safely (no bricking) set with [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) or [UEFI Shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface") v2 (checked with *BIOS 2.77 (G2ETB7WW) EC 1.15*). Though you can delete *any* boot variable, so be careful!

X230 in UEFI-non-CSM mode installed with [EFISTUB](/index.php/EFISTUB "EFISTUB") on [SSD disk](/index.php/Solid_state_drive "Solid state drive") boots into [display manager](/index.php/Display_manager "Display manager") in less than 25 seconds. Small [ESP](/index.php/ESP "ESP") (100 MiB fat32) also supported.

### USB UEFI update

**Tip:** There are unofficial firmware available, such as [Coreboot](https://doc.coreboot.org/mainboard/lenovo/xx30_series.html) or Heads in order to remove hardware whitelists and provide trusted boot.

All official updates, including Windows utility, Bootable CD and documentation can be found [here](https://pcsupport.lenovo.com/gb/en/downloads/ds029187). You can use [geteltorito](https://aur.archlinux.org/packages/geteltorito/) to create bootable USB images from the Bootable CD:

```
$ geteltorito.pl g2uj24us.iso > update.img 
# dd bs=512K if=update.img of=/dev/sdX

```

Insert USB stick, reboot and press `F12`, choose your USB. Follow the instructions.

### Trusted Platform Module

Laptop has dedicated [TPM](/index.php/TPM "TPM") 1.2 chip onboard[[3]](https://www.st.com/en/secure-mcus/st33tpm12lpc.html)[[4]](https://trustedcomputinggroup.org/membership/certification/tpm-certified-products/). It doesn't looks like it can be upgraded to TPM 2.0\. Chip itself disabled by default sometimes, also owner clearing won't appear without *Supervisor password* set:

1.  Enter Thinkpad UEFI Setup by pressing `F1`
2.  Set *Security > Password* > *Supervisor password*
3.  Set *Security > Security Chip > Security Chip [Active]*
4.  Save settings by pressing F10 and reboot
5.  **Turn laptop off**, turn on and UEFI option *Security > Security Chip > Clear Security Chip* eventually will appear.

Process described in "ThinkPad X230 and X230i User Guide", *Chapter 4\. Security > Setting the security chip*.

## Known issues

*   There is a BIOS bug that gets in the way of the boot process with [LUKS](/index.php/LUKS "LUKS") and full-disk encryption. The user is stuck at the "Loading initial ramdisk" step, and does not see a password prompt to unlock the encrypted device. You can actually enter your password at this step, and boot-up will continue. However, updating the BIOS will resolve this completely.
*   UEFI option to clear [TPM](/index.php/TPM "TPM") not working. STM chip datasheet describes physical presence pin, which, probably, can be used as workaround.

## See also

*   [A Hacker's Ongoing Review for Lenovo ThinkPad X230](https://gist.github.com/bassu/8478346)
*   [Installing "Heads" and using TPM](http://osresearch.net/Installing-Heads.html)