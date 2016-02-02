# ASUS Eee PC 1005HA

| **Device** | **Status** | **Modules** |
| Intel 945GME | **Working** | xf86-video-intel |
| Ethernet | **Working** |
| Wireless | **Working** |
| Audio | **Working** | snd_hda_intel |
| Camera | **Working** | uvcvideo |
| Card Reader | **Working** |
| Function Keys | **Working** |

## Contents

*   [1 Installation](#Installation)
*   [2 Boot Booster](#Boot_Booster)
*   [3 Wireless/rfkill](#Wireless.2Frfkill)
*   [4 Display and input settings](#Display_and_input_settings)
*   [5 Powersaving and ACPI](#Powersaving_and_ACPI)
    *   [5.1 laptop-mode-tools](#laptop-mode-tools)
    *   [5.2 Gmabooster](#Gmabooster)
    *   [5.3 CPU frequency scaling](#CPU_frequency_scaling)
    *   [5.4 Hotkeys](#Hotkeys)
        *   [5.4.1 Wifi toggle](#Wifi_toggle)
        *   [5.4.2 Sound volume hotkeys](#Sound_volume_hotkeys)
        *   [5.4.3 Sleep](#Sleep)
    *   [5.5 Display settings](#Display_settings)
*   [6 Hardware](#Hardware)
    *   [6.1 Ethernet](#Ethernet)
    *   [6.2 WiFi](#WiFi)
    *   [6.3 Camera](#Camera)
    *   [6.4 Microphone](#Microphone)
*   [7 Hardware Info](#Hardware_Info)
    *   [7.1 lspci](#lspci)

# Installation

For an in-depth guide on the installation see the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

# Boot Booster

Boot Booster is a feature that caches the result of the POST check to the hard drive. It can save several seconds off your boot time once activated.

To continue using Boot Booster, create a [partition](/index.php/Partitioning "Partitioning") on the disk:

*   It must be a primary partition.
*   It must be 16MB minimum, pay attention to [partition alignments](/index.php/Partitioning#Partition_alignment "Partitioning").
*   It must be type <tt>0xEF</tt> (<tt>EFI (FAT-12/16/32)</tt> in [Fdisk](/index.php/Fdisk "Fdisk"), <tt>esp</tt> in [GNU_Parted](/index.php/GNU_Parted "GNU Parted")).

After install is complete, enable Boot Booster in the BIOS. On the second boot after enabling, Boot Booster will be fully activated. Boot Booster must be disabled in the BIOS to boot from other devices again.

# Wireless/rfkill

The wireless interface may become soft blocked shortly after booting after installation. Install [rfkill](https://www.archlinux.org/packages/?name=rfkill) as part of the installation and see the [rfkill caveat](/index.php/Wireless_network_configuration#Rfkill_caveat "Wireless network configuration").

# Display and input settings

See [Xorg](/index.php/Xorg "Xorg"), [Intel graphics](/index.php/Intel_graphics "Intel graphics"), [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") and [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

# Powersaving and ACPI

See the main page: [Power management](/index.php/Power_management "Power management").

Start off your powersaving adventures by installing [Powertop](/index.php/Powertop "Powertop"). This is basically a program to see how much power stuff is using, but it also gives you tips on what to change.

A good starting point is to disable the hardware you do not plan on using. Reboot and enter the BIOS by pressing F2\. Disable for example the card reader, camera, ethernet but only if you do not need them of course.

According to Powertop the 1005HA uses around 7-10 Watts on maximum powersave (using Laptop mode tools and cpufreq and the above hardware disabled, using Wifi and writing this). Idle around 5-6 W. Please report how to get it lower!

## laptop-mode-tools

[laptop-mode-tools](/index.php/Laptop-mode-tools "Laptop-mode-tools") is an easy way to setup most of the available power saving options on the 1005HA. These include spinning down the hard drive and adjusting the power saving modes of the harddrive and CPU, as well as autosuspending of the USB-ports and screen brightness etc. It provides a great centralized configuration file as well as separate configuration files for the various power saving modules managed by Laptop mode tools.

## Gmabooster

To further save power it is possible to use gmabooster to force a lower clock on the GPU when entering powersave and to overclock when on AC power.

Install [gmabooster](https://aur.archlinux.org/packages/gmabooster/) and then trigger the different clock levels with:

```
echo "foo" | gmabooster

```

Where **foo** can be in the range 1 to 4 which yields 166, 200, 250 or 400 MHz GPU Clock.

When using powerdown add the line to

```
/usr/bin/powerdown

```

and

```
/usr/bin/powerup 

```

and set **foo** appropriately.

## CPU frequency scaling

See [cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils").

## Hotkeys

To get the hotkeys working (fn+F1 etc, touchpad lock, powerbutton shutdown, Super hybrid engine toggle), install the [acpi-eeepc-generic](https://aur.archlinux.org/packages/acpi-eeepc-generic/) package from AUR. Configuration is done in the file /etc/conf.d/acpi-eeepc-generic.conf.

acpi-eeepc-generic needs the eeepc_wmi kernel module to be loaded to work. Check with:

```
lsmod | grep eeepc

```

If not found, use

```
acpi_osi=Linux

```

as mentioned under CPU Powersawing.

### Wifi toggle

To enable the toggling of the Wifi by pressing fn+f2, edit the acpi-eeepc-generic config file and change

```
COMMANDS_WIFI_TOGGLE=("/etc/acpi/eeepc/acpi-generic-toggle-wifi.sh")

```

to

```
COMMANDS_WIFI_TOGGLE=()

```

[Source](http://github.com/nbigaouette/acpi-eeepc-generic/wiki/Wireless).

### Sound volume hotkeys

In order to get the hotkeys for muting and raising and lowering of the sound volume, edit /etc/conf.d/acpi-eeepc-generic.conf and replace the lines:

```
COMMANDS_MUTE=("alsa_toggle_mute")
COMMANDS_VOLUME_DOWN=("alsa_set_volume 5%-")
COMMANDS_VOLUME_UP=("alsa_set_volume 5%+")

```

with

```
COMMANDS_MUTE=("@amixer set Master toggle")
COMMANDS_VOLUME_DOWN=("@amixer set Master 10%-")
COMMANDS_VOLUME_UP=("@amixer set Master 10%+")

```

Note that the value 10% can be any value you prefer, see the man page of amixer.

### Sleep

If you have problems with the script provided in acpi-eeepc-generic, try **pm-suspend** or native **systemd** instead.

To substitute the acpi sleep script, edit /etc/conf.d/acpi-eeepc-generic.conf and comment out the line that reads:

```
COMMANDS_SLEEP=("/etc/acpi/eeepc/acpi-eeepc-generic-suspend2ram.sh")

```

Replace it with:

```
COMMANDS_SLEEP=("/usr/sbin/pm-suspend")

```

or

```
COMMANDS_SLEEP=("systemctl suspend")

```

The relevance of the pm-suspend scripts are questioned since the switch to systemd. See [pm-utils](/index.php/Pm-utils "Pm-utils").

## Display settings

Create the /etc/X11/xorg.conf file and add the following to it to enable Intel's framebuffer compression, which according to [Lesswats.org](http://www.lesswatts.org/projects/display-and-graphics/faq.php) is supposed to save quite some power.

```
Section "Device"
 Identifier "Builtin Default intel Device 0"
 Driver	 "intel"
 Option	 "FramebufferCompression" "on"
 Option	 "AccelMethod" "EXA"
 Option	 "Tiling" "on"
EndSection

```

# Hardware

## Ethernet

Works with the stock 2.6.32 kernel.

## WiFi

WiFi works out of the box with the stock kernel (tested with 2.6.30 and 2.6.32).

## Camera

To enable/disable the camera:

```
 # enable
 echo 1 > /sys/devices/platform/eeepc/camera
 # disable
 echo 0 > /sys/devices/platform/eeepc/camera

```

If you really want camera to be disabled, take a look in devices section of BIOS.

Make sure that the module `uvcvideo` is loaded

To record video and take photos, you may use [cheese](https://www.archlinux.org/packages/?name=cheese) or [wxcam](https://www.archlinux.org/packages/?name=wxcam) package.

To simply test the camera, you may use `mplayer`:

```
 mplayer -fps 15 tv://

```

The webcam works with Skype.

## Microphone

The microphone works out of the box, it's just a matter of configuration. Run:

```
$ alsamixer

```

Press <F4> to go to the 'Capture' section. Navigate to the 'Capture' item using the right and left arrow keys and make sure 'LR Capture' appears. If it doesn't, press <Space>. The 'Capture' and 'Digital' levels are a trade-off between gain and static. I recommend setting to 70 and 75 (using the up and down arrow keys), respectivelly, but you can ajust this to your liking. Exit alsamixer pressing <ESC> and test it:

```
$ arecord /tmp/record.wav

```

Say something close enough to the microphone and hit <Ctrl+C> to stop recording. Play it with:

```
$ aplay /tmp/record.wav 

```

If everything went well, save your settings (as root):

```
# alsactl store

```

Source: [[1]](https://bbs.archlinux.org/viewtopic.php?pid=495168#p495168)

# Hardware Info

## lspci

Note that this is the 1005HA-M version.

 `$ lspci` 

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
00:1f.2 SATA controller: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA AHCI Controller (rev 02) 
01:00.0 Ethernet controller: Attansic Technology Corp. Atheros AR8132 / L1c Gigabit Ethernet Adapter (rev c0) 
02:00.0 Network controller: Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01)

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1005HA&oldid=418445](https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1005HA&oldid=418445)"