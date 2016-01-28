# ASUS Eee PC 1000HE

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Intel 945GM</td>

<td style="color:green">**Working**</td>

<td>xf86-video-intel</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="color:green">**Working**</td>

<td>atl1e</td>

</tr>

<tr>

<td>Wireless</td>

<td style="color:green">**Working**</td>

<td>ath9k or rt2860sta</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="color:green">**Working**</td>

<td>btusb</td>

</tr>

<tr>

<td>Audio</td>

<td style="color:green">**Working**</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Camera</td>

<td style="color:green">**Working**</td>

<td>uvcvideo</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="color:green">**Working**</td>

</tr>

<tr>

<td>Function Keys</td>

<td style="color:green">**Working**</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Installation](#Installation)
*   [2 Xorg](#Xorg)
    *   [2.1 DPI Settings](#DPI_Settings)
    *   [2.2 Graphic Performance](#Graphic_Performance)
    *   [2.3 Touchpad](#Touchpad)
    *   [2.4 xrandr](#xrandr)
*   [3 Powersaving](#Powersaving)
    *   [3.1 laptop-mode-tools](#laptop-mode-tools)
        *   [3.1.1 Super Hybrid Engine](#Super_Hybrid_Engine)
    *   [3.2 Wireless](#Wireless)
    *   [3.3 acpi-eeepc-generic](#acpi-eeepc-generic)
        *   [3.3.1 Sleep](#Sleep)
    *   [3.4 cpufrequtils](#cpufrequtils)
*   [4 Hardware](#Hardware)
    *   [4.1 lspci](#lspci)
    *   [4.2 WiFi](#WiFi)
    *   [4.3 Bluetooth](#Bluetooth)
    *   [4.4 Camera](#Camera)

## Installation

See [Install from USB stick](/index.php/Install_from_USB_stick "Install from USB stick"). There is out-of-the-box support for the wired and wireless NICs. There are no special instructions for installation. For an in-depth guide on the installation see the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

## Xorg

### DPI Settings

In general the autodetected DPI does not fit the smaller resolution very well at all. A good comfortable setting would be 96dpi or 75dpi if you like your fonts really small. An easy way to set your DPI would be to add this to the end of your xserverrc (located in `/etc/X11/xinit/`).

```
exec /usr/bin/X -nolisten tcp **-dpi 96**

```

See also [Xorg#Display size and DPI](/index.php/Xorg#Display_size_and_DPI "Xorg").

### Graphic Performance

See [Intel](/index.php/Intel "Intel") for more information.

According to the Intel driver documentation, X-Video Motion Compensation or "XvMC" is not enabled by default. Enabling this option can greatly reduce CPU utilization when playing back MPEG-2 video. To enable this option, two things need to be done; first, add this to the device section of your `xorg.conf`:

```
Option "XvMC" "true"

```

Lastly, create a configuration file to tell the X server where the XvMC library is:

```
echo /usr/lib/libIntelXvMC.so > /etc/X11/XvMCConfig

```

### Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")

### xrandr

For a nice GUI tool, try [lxrandr](https://www.archlinux.org/packages/?name=lxrandr); it is very simple to use!

Switch to External Monitor:

```
xrandr --output LVDS --off --output VGA --auto

```

Switch back to eeepc's LCD:

```
xrandr --output LVDS --auto --output VGA --off

```

## Powersaving

### laptop-mode-tools

I got the best powersaving from a combination of [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools").

Use laptop-mode to control all power saving features. Enable bluetooth.conf, cpufreq.conf, hal-polling.conf, intel-hda-powersave.conf, usb-autosuspend.conf, and lcd-brightness.conf.

*   For lcd-brightness, use the following options. Adjust your max/min brightness as suits you. The maximums are located in the same directory as the control file.

```
BATT_BRIGHTNESS_COMMAND="echo 3"
LM_AC_BRIGHTNESS_COMMAND="echo 15"
NOLM_AC_BRIGHTNESS_COMMAND="echo 15"
BRIGHTNESS_OUTPUT="/sys/devices/virtual/backlight/eeepc/brightness"

```

*   The intel-hda-powersave has a side-effect. Short sounds such as IM notifications may not come through, or will be messed up as it starts playing the sound before the sound card wakes up.

#### Super Hybrid Engine

The eeepc "Super Hybrid Engine" as it is known under Windows has a significant effect on powersaving. This underclocks the FSB for powersave/overclocks for performance and can be controlled via `/sys/devices/platform/eeepc/cpufv` which is provided by the `eeepc_laptop` module. The following is a laptop-mode configuration for it that controls it automatically.

```
#! /bin/sh

if [ x$SUPERHE_CONTROL_FILE = x ]; then
    SUPERHE_CONTROL_FILE=/sys/devices/platform/eeepc/cpufv
fi

if [ x$CONTROL_SUPERHE = x1 ]; then
    if [ $ON_AC -eq 1 ]; then
        if [ $ACTIVATE -eq 1 ]; then
            SUPERHE_VALUE="$LM_AC_SUPERHE"
        else
            SUPERHE_VALUE="$NOLM_AC_SUPERHE"
        fi
    else
        SUPERHE_VALUE="$BATT_SUPERHE"
    fi
    echo $SUPERHE_VALUE > $SUPERHE_CONTROL_FILE
fi

```

```
#
# Configuration file for Laptop Mode Tools module eee-superhe
#
# For more information, consult the laptop-mode.conf(8) manual page.
#

# Control FSB speed. Requires eeepc_laptop kernel module loaded.
CONTROL_SUPERHE=1

# 2 is powersave
# 1 is normal
# 0 is performance

BATT_SUPERHE=2
LM_AC_SUPERHE=0
NOLM_AC_SUPERHE=0

# If your system has the control file located at another point
# configure it here
# SUPERHE_CONTROL_FILE=

```

### Wireless

The rt2860sta wireless has pretty good powersaving, but it is a tradeoff between throughput<->power usage. Minimum power usage gives a pretty low throughput of ~11KB/s when I would normally get >1MB/s.

```
iwpriv ra0 set PSMode=MAX_PSP

```

*   MAX_PSP - maximum power saving
*   CAM - seems to be normal
*   FAST_PSP - ? untested, probably a medium value.

### acpi-eeepc-generic

Install the [acpi-eeepc-generic](https://aur.archlinux.org/packages/acpi-eeepc-generic/)<sup><small>AUR</small></sup> package from [AUR](/index.php/AUR "AUR"). You must install version 0.9 or greater, as previous versions do not have support for the 1000HE.

#### Sleep

If you want to use **pm-suspend** from [pm-utils](/index.php/Pm-utils "Pm-utils") with acpi-eeepc-generic, edit `/etc/conf.d/acpi-eeepc-generic.conf` to comment out the line

```
#SUSPEND2RAM_COMMANDS=("echo -n \"mem\" > /sys/power/state") # Simple suspend

```

and uncomment the line

```
SUSPEND2RAM_COMMANDS=("pm-suspend") # Use pm-utils

```

### cpufrequtils

To scale the CPU and possibly save a bit of power, you will want to set up [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling"). For this you will be using the `acpi-cpufreq` kernel module. Note that if you have already configured [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") to set governors, frequencies, etc then you do not need to bother with loading the cpufreq daemon.

## Hardware

### lspci

```
00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller (rev 03)
00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller (rev 03)
00:1b.0 Audio device: Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 2 (rev 02)
00:1c.3 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 4 (rev 02)
00:1d.0 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #1 (rev 02)
00:1d.1 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #2 (rev 02)
00:1d.2 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #3 (rev 02)
00:1d.3 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #4 (rev 02)
00:1d.7 USB Controller: Intel Corporation 82801G (ICH7 Family) USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
00:1f.2 IDE interface: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA IDE Controller (rev 02)
01:00.0 Network controller: Atheros Communications Inc. AR928X Wireless Network Adapter (PCI-Express) (rev 01)
03:00.0 Ethernet controller: Attansic Technology Corp. L1e Gigabit Ethernet Adapter (rev b0)

```

Note: lspci for another user produced "Network controller: RaLink RT2860" rather than the Atheros chipset in the output above

### WiFi

WiFi should work out of the box with the stock kernel. However, if you do have trouble, you can try switching to the rt2860sta module provided by the [rt2860](https://aur.archlinux.org/packages/rt2860/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/rt2860)]</sup> package. If you use the AUR package, you may need to [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") the rt2800lib and rt2800pci modules.

### Bluetooth

To turn the bluetooth radio on/off:

```
 # enable
 $ echo 1 > /sys/class/rfkill/rfkill1/state
 # disable
 $ echo 0 > /sys/class/rfkill/rfkill1/state

```

Install the [bluez](https://www.archlinux.org/packages/?name=bluez) package and then `modprobe btusb`.

See the Arch Linux [Bluetooth](/index.php/Bluetooth "Bluetooth") and [Bluetooth mouse](/index.php/Bluetooth_mouse "Bluetooth mouse") wiki pages for more information about configuring and using Bluetooth devices.

### Camera

Make sure that the `uvcvideo` module is loaded.

To enable/disable the camera:

```
 # enable
 echo 1 > /sys/devices/platform/eeepc/camera
 # disable
 echo 0 > /sys/devices/platform/eeepc/camera

```

To record video and take photos, you may use [cheese](https://www.archlinux.org/packages/?name=cheese) or the wxcam package.

To simply test the camera, you may use [MPlayer](/index.php/MPlayer "MPlayer"):

```
 mplayer -fps 15 tv://

```

The webcam is reported to work with [Skype](/index.php/Skype "Skype").

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1000HE&oldid=408671](https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1000HE&oldid=408671)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")