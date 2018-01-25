Related articles

*   [fprint](/index.php/Fprint "Fprint")
*   [TrackPoint](/index.php/TrackPoint "TrackPoint")
*   [HiDPI](/index.php/HiDPI "HiDPI")

[Lenovo ThinkPad X230](http://www.lenovo.com/hk/en/productcatalog/pdf/X230-datasheet.pdf)

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Screen](#Screen)
    *   [1.3 Brightness](#Brightness)
    *   [1.4 Touchpad](#Touchpad)
    *   [1.5 Backlight control keys](#Backlight_control_keys)
    *   [1.6 Suspend to ram](#Suspend_to_ram)
    *   [1.7 UMTS Modem](#UMTS_Modem)
    *   [1.8 Fan control](#Fan_control)
*   [2 USB BIOS update](#USB_BIOS_update)
*   [3 Power Saving](#Power_Saving)
    *   [3.1 TLP](#TLP)
*   [4 x230T (tablet version)](#x230T_.28tablet_version.29)
    *   [4.1 Multitouch screen for the x230t (tablet version)](#Multitouch_screen_for_the_x230t_.28tablet_version.29)
    *   [4.2 Wacom tablet input](#Wacom_tablet_input)
*   [5 Not Working](#Not_Working)
*   [6 See also](#See_also)

## Configuration

### Kernel

 `/etc/mkinitcpio.conf` 
```
MODULES="i915"

```

After saving the above files, make sure to regenerate your init ram image by the command `mkinitcpio -p linux`, and follow the steps in [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### Screen

X230 has IPS or TN screen with 125.37 DPI. Refer to [HiDPI](/index.php/HiDPI "HiDPI") page for more information. It can be set with command `xrandr --dpi 125.37` using .xinitrc or other autostarts.

See [Intel](/index.php/Intel "Intel") for driver choice.

### Brightness

If you experience that your brightness setting is not restored on resume from suspend, then create `/usr/share/X11/xorg.conf.d/20-intel.conf` with the following content.

 `/usr/share/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
Identifier "card0"
Driver "intel"
Option "Backlight" "intel_backlight"
BusID "PCI:0:2:0"
EndSection

```

### Touchpad

The original configuration renders the touchpad quite useless, as it behaves very jumpily. [Ubuntu Bugtracker](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-input-synaptics/+bug/1042069/comments/5) offers a solution for this issue. Add the following

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

Setting e.g. the motion-acceleration value in dconf to 2.8 works nicely.

### Backlight control keys

**Note:** On most X230 models, backlight works by default without any issues. Use below only in case of any problems.

Due to an issue with the firmware of several ThinkPads the backlight control keys (fn + F8/F9 on the X230) don't work correctly. Setting the brightness via e.g. the GNOME power control panel or altering the brightness value in sysfs is possible.

The issue can be temporarily and partially fixed in adding the acpi_osi="!Windows 2012" [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). The fix is partial in that only 8 steps are accessible via the keys. See [[1]](https://bugzilla.kernel.org/show_bug.cgi?id=51231) for details.

### Suspend to ram

There is an issue with system shutdown with power saving tools that cannot distinguish sys devices. You will need to add to the systemd shutdown trigger on this machine or else you'll get a system reboot when you shutdown the machine. Put this in /etc/rc.local.shutdown and update and enable its service, if not already.

 `/etc/rc.local.shutdown` 
```
#!/bin/bash
# /etc/rc.local.shutdown: Local shutdown script.
# A script to act as a workaround for the bug in the runtime power management module, which causes thinkpad laptops to restart after shutting down. 
# Bus list for the runtime power management module.
buslist="pci i2c"
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

```

### UMTS Modem

Some models come with an integrated USB UMTS modem.

 `$ lsusb -d 0bdb:1926`  `Bus 003 Device 004: ID 0bdb:1926 Ericsson Business Mobile Networks BV H5321 gw Mobile Broadband Driver` 

In order for it to work with [NetworkManager](/index.php/NetworkManager "NetworkManager"), you will need to install [ModemManager](https://www.archlinux.org/packages/?name=modemmanager) from the official repositories.

For it to be recognized by ModemManager, you also need to set the kernel module option to:

 `/etc/modprobe.d/umts-modem.conf`  `options cdc_ncm prefer_mbim=N` 

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

## USB BIOS update

You can use [geteltorito](https://aur.archlinux.org/packages/geteltorito/) to create bootable USB images from the BIOS update ISO. It is as easy as:

```
$ geteltorito.pl g2uj24us.iso > update.img 
# dd bs=512K if=update.img of=/dev/sdX

```

## Power Saving

Follow the main article: [Power saving](/index.php/Power_saving "Power saving")

Power saving [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") in addition to graphics card power saving, are shown below. `acpi_backlight=vendor` loads the vendor specific [Backlight#ACPI](/index.php/Backlight#ACPI "Backlight") driver (i.e. thinkpad_acpi) so the brightness keys (Fn + F8 and Fn + F9) work correctly.

Note that the `acpi_backlight=vendor` kernel option also works with the standard Arch kernel (currently 3.7.10-1) and has the additional bonus that (Fn + spacebar) controls the keyboard lighting.

### TLP

Users of [TLP](/index.php/TLP "TLP") need to pay attention to a hardware bug according to which it is recommended to only use either the upper or lower charging threshold. The following configuration is recommended by the developer of TLP.[[1](http://thinkpad-forum.de/threads/184510-elementary-OS-Thinkpad-X230-einrichten?p=1865345&viewfull=1#post1865345)]

 `/etc/default/tlp` 
```
START_CHARGE_THRESH_BAT0=67
STOP_CHARGE_THRESH_BAT0=100

```

## x230T (tablet version)

### Multitouch screen for the x230t (tablet version)

**Note:** Some x230t models have a multitouch screen in addition to the wacom tablet.

Works out of the box with [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput).

### Wacom tablet input

Works out of the box with [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom). See [Wacom tablet](/index.php/Wacom_tablet "Wacom tablet")

## Not Working

*   Microphone on-off key does not work out of the box

**Note:** It works out of the box with GNOME.

## See also

*   [A Hacker's Ongoing Review for Lenovo ThinkPad X230](https://gist.github.com/bassu/8478346)