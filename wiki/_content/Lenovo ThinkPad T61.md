# Lenovo ThinkPad T61

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 System Specifications](#System_Specifications)
    *   [1.1 What works/What doesn't](#What_works.2FWhat_doesn.27t)
*   [2 Pre-installation notes](#Pre-installation_notes)
*   [3 Accessing the recovery partition with GRUB](#Accessing_the_recovery_partition_with_GRUB)
*   [4 Configuration](#Configuration)
    *   [4.1 Video Driver](#Video_Driver)
        *   [4.1.1 Intel](#Intel)
        *   [4.1.2 Nvidia](#Nvidia)
    *   [4.2 Audio](#Audio)
    *   [4.3 Network](#Network)
        *   [4.3.1 Wired](#Wired)
        *   [4.3.2 Wireless](#Wireless)
        *   [4.3.3 Modem](#Modem)
    *   [4.4 USB](#USB)
    *   [4.5 Bluetooth](#Bluetooth)
    *   [4.6 TrackPoint scrolling (wheel emulation)](#TrackPoint_scrolling_.28wheel_emulation.29)
    *   [4.7 Touchpad](#Touchpad)
    *   [4.8 ThinkFinger](#ThinkFinger)
    *   [4.9 ACPI](#ACPI)
    *   [4.10 Hotswap UltraBay devices](#Hotswap_UltraBay_devices)
    *   [4.11 Multimedia Keys](#Multimedia_Keys)
    *   [4.12 HDAPS](#HDAPS)
    *   [4.13 Card Readers](#Card_Readers)
        *   [4.13.1 PCMCIA](#PCMCIA)
        *   [4.13.2 Compact Flash](#Compact_Flash)
        *   [4.13.3 Secure Digital](#Secure_Digital)
*   [5 Other Tweaks](#Other_Tweaks)
    *   [5.1 HDD clicks](#HDD_clicks)
*   [6 See also](#See_also)

## System Specifications

Lenovo ThinkPad T61 - Intel Centrino Pro

*   Intel(R) Core(TM)2 Duo CPU T7300 (2.00GHz, 4MB, 800MHz)
*   Mobile Intel 965GM Express Chipset
*   2GB PC2-5300/677MHz
*   80-GB 5400 rpm SATA Harddrive
*   14.1-inch color TFT WXGA+ (1440 x 900, 200 nit)
*   Intel® Graphics Media Accelerator GM965 (128MB)
*   82801H ICH8 Family HD Audio Controller
*   DVD-ROM, CD-RW/DVD Combo, Multi-Burner Plus
*   Modem; Gigabit Ethernet
*   Intel® Wireless Wi-Fi Link 4965AG
*   1 Type II PC Card slot
*   1 ExpressCard 34/54
*   Dual pointing devices (both Pointstick and Touchpad)

Output of lshwd

```
00:00.0 Class 0600: Intel Corporation|Mobile Memory Controller Hub (unknown)
00:02.0 Class 0300: Intel Corporation|Mobile Integrated Graphics Controller (vesa)
00:02.1 Class 0380: Intel Corporation|Mobile Integrated Graphics Controller (vesa)
00:19.0 Class 0200: Intel Corporation|Mobile Integrated Graphics Controller (unknown)
00:1a.0 Class 0c03: Intel Corporation|USB UHCI Controller #4 (unknown)
00:1a.1 Class 0c03: Intel Corporation|USB UHCI Controller #5 (unknown)
00:1a.7 Class 0c03: Intel Corporation|USB2 EHCI Controller #2 (unknown)
00:1b.0 Class 0403: Intel Corp.|ICH8 HD Audio DID (snd-hda-intel)
00:1c.0 Class 0604: Intel Corporation|PCI Express Port 1 (unknown)
00:1c.1 Class 0604: Intel Corporation|PCI Express Port 2 (unknown)
00:1c.2 Class 0604: Intel Corporation|PCI Express Port 3 (unknown)
00:1c.3 Class 0604: Intel Corporation|PCI Express Port 4 (unknown)
00:1c.4 Class 0604: Intel Corporation|PCI Express Port 5 (unknown)
00:1d.0 Class 0c03: Intel Corporation|USB UHCI Controller #1 (unknown)
00:1d.1 Class 0c03: Intel Corporation|USB UHCI Controller #2 (unknown)
00:1d.2 Class 0c03: Intel Corporation|USB UHCI Controller #3 (unknown)
00:1d.7 Class 0c03: Intel Corporation|USB2 EHCI Controller #1 (unknown)
00:1e.0 Class 0604: Intel Corp.|82801 Hub Interface to PCI Bridge (hw_random)
00:1f.0 Class 0601: Intel Corporation|Mobile LPC Interface Controller (unknown)
00:1f.2 Class 0101: Intel Corporation|Mobile SATA Controller cc=IDE (ata_piix)
00:1f.3 Class 0c05: Intel Corporation|SMBus Controller (i2c-i801)
03:00.0 Class 0280: Intel Corporation|SMBus Controller (unknown)
15:00.0 Class 0607: Ricoh Co Ltd.|RL5c476 II (yenta_socket)
15:00.1 Class 0c00: Ricoh Co Ltd.|RL5c476 II (unknown)
15:00.2 Class 0805: Ricoh Co Ltd.|SD Card reader (unknown)
15:00.3 Class ffff: Ricoh Co Ltd.|SD Card reader (unknown)
15:00.4 Class 0880: Ricoh Co Ltd.|R5C592 Memory Stick Bus Host Adapter (unknown)
15:00.5 Class 0880: Ricoh Co Ltd.|xD-Picture Card Controller (unknown)

```

### What works/What doesn't

Pretty much everything works on this laptop. The modem is untested.

## Pre-installation notes

Remember to back up the restore partition if you plan to restore it, or leave it.

Follow the [official Arch Linux install guide](/index.php/Installation_guide "Installation guide")

## Accessing the recovery partition with GRUB

Edit your **/boot/grub/menu.lst** file and add the following:

```
# booting "Rescue and Recovery" partition from Lenovo
title Thinkpad Maintenance
unhide (hd0,0)
rootnoverify (hd0,0)
chainloader +1

```

## Configuration

### Video Driver

#### Intel

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Intel graphics](/index.php/Intel_graphics "Intel graphics").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Lenovo ThinkPad T61#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_T61))

The Intel® Graphics Media Accelerator GM965 uses the xf86-video-intel driver.

```
#pacman -S xf86-video-intel

```

The relevent kernel drivers include:

*   DRM_I915

For framebuffer graphics one of the kernel drivers:

*   intelfb
*   fb_uvesa
*   fb_vesa

Should work. It is up to you which one you wish to use. Intelfb is known to have a few problems with hardware acceleration and requires grub2 patched with 915resolution to properly set the correct resolution.

The package grub2-915resolution in the AUR has the necessary patch to make intelfb work with laptops that use the 965GM card.

Here is a sample file:

 `/etc/X11/xorg.conf` 

```

    Section "Module"
        Load        "dbe"   # Double buffer extension
        SubSection  "extmod"
          Option    "omit xfree86-dga"
        EndSubSection
        Load        "freetype"
        Load        "GLcore"
        Load        "glx"
        Load        "bitmap"
        Load        "dri"
 #        Load        "int10"
 #        Load        "ddc"
 #        Load        "vbe"
 #        Load        "xtrap"
    EndSection

    Section "Files"
        ModulePath "/usr/lib/xorg/modules"
        FontPath   "/usr/share/fonts/local/"
        FontPath   "/usr/share/fonts/misc/:unscaled"
        FontPath   "/usr/share/fonts/75dpi/:unscaled"
        FontPath   "/usr/share/fonts/100dpi/:unscaled"
        FontPath   "/usr/share/fonts/misc/"
        FontPath   "/usr/share/fonts/75dpi/"
        FontPath   "/usr/share/fonts/100dpi/"
        FontPath   "/usr/share/fonts/TTF/"
        FontPath   "/usr/share/fonts/Type1/"
        FontPath   "/usr/share/fonts/local/"
    EndSection

    Section "ServerFlags"
        Option      "blank time"    "3"
        Option      "standby time"  "5"
        Option      "suspend time"  "10"
        Option      "off time"      "15"
        Option      "RandR"
        Option      "AutoAddDevices" "False"
    EndSection

    Section "InputDevice"
        Identifier  "Keyboard0"
        Driver      "kbd"
        Option      "CoreKeyboard"
        Option      "XkbRules" "xorg"
        Option      "XkbModel" "thinkpad60"
        Option      "XkbLayout" "us"
    EndSection

    Section "InputDevice"
        Identifier  "UltraNav Trackpoint"
        Driver      "mouse"
        Option      "CorePointer"
        Option      "Device"              "/dev/input/mice"
        Option      "Protocol"            "ImPS/2"
        Option      "Emulate3Buttons"     "off"
        Option      "EmulateWheel"        "on"
        Option      "EmulateWheelTimeOut" "250"
        Option      "EmulateWheelButton"  "2"
        Option      "YAxisMapping"        "4 5"
        Option      "XAxisMapping"        "6 7"
        Option      "ZAxisMapping"        "4 5"
    EndSection

 #    Section "InputDevice"
 #           Identifier  "Synaptics"
 #           Driver      "synaptics"
 #           Option      "Device" "/dev/input/mice"
 #           Option      "Protocol" "auto-dev"
 #           Option      "Emulate3Buttons" "yes"
 #           Option      "SHMConfig" "on"
 #    EndSection

    Section "Monitor"
        Identifier  "Thinkpad Monitor"
        Option      "DPMS"
 #        HorizSync   31.5-50.0
 #        VertRefresh 59.9-60.1
     EndSection

    Section "Device"
        Identifier  "Intel GMA X3100"
        Driver      "intel"
        BusID       "PCI:0:2:0"
        Option      "AccelMethod"  "exa"
        Option      "MigrationHeuristic"     "greedy"
    EndSection

    Section "Screen"
        Identifier          "Thinkpad Screen"
        Device              "Intel GMA X3100"
        Monitor             "Thinkpad Monitor"
        DefaultDepth        24
        SubSection "Display"
             Depth 24
             Modes "1280x800" "1024x768"  "832x624" "800x600" "640x480" "720x400" "640x400" "640x350"
             Virtual     2048 2048
        EndSubSection
    EndSection

    Section "DRI"
        Mode        0666
    EndSection

    Section "Extensions"
        Option      "Composite"     "Enable"
        Option      "RENDER"        "Enable"
    EndSection

    Section "ServerLayout"
        Identifier  "Default Layout"
        Screen "Thinkpad Screen"
        InputDevice "UltraNav Trackpoint" "CorePointer"
 #        InputDevice "Synaptics" "CorePointer"
        InputDevice "Keyboard0" "CoreKeyboard"
    EndSection

```

Please note that this has the touchpad and xorg input hotplugging disabled.

#### Nvidia

Follow the instructions in [NVIDIA](/index.php/NVIDIA "NVIDIA").

**Note:** If you're following the [Beginners Guide](/index.php/Beginners_Guide "Beginners Guide") and you're not seeing the cursor after the NVIDIA logo, you should try the simple baseline X test.

### Audio

Sound works out of the box. The relevant module for sound is:

*   SND_HDA_INTEL

Refer to following guides to set it up:

[OSS](/index.php/OSS "OSS")

[ALSA](/index.php/ALSA "ALSA")

[PulseAudio](/index.php/PulseAudio "PulseAudio")

Use whichever you wish.

### Network

#### Wired

The wired connection works out of the box and uses the following module:

*   e1000e

#### Wireless

Uses either module, varies with different setups:

*   iwl3945
*   iwl4965

Requires firmware be installed to work.

Refer to [Wireless network configuration#Intel](/index.php/Wireless_network_configuration#Intel "Wireless network configuration")

#### Modem

Untested.

### USB

Works out of the box.

Following modules are used:

*   uhci_hcd
*   ehci_hcd
*   usbhid

### Bluetooth

Works out of the box.

Following modules are used:

*   bluetooth
*   btusb
*   l2cap
*   rfcomm
*   hci_usb
*   ehci-hcd
*   uhci-hcd

### TrackPoint scrolling (wheel emulation)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [TrackPoint](/index.php/TrackPoint "TrackPoint").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Lenovo ThinkPad T61#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_T61))

To enable scrolling with the TrackPoint while holding down the middle mouse button, create a new file /etc/X11/xorg.conf.d/20-thinkpad.conf with the following content:

```
Section "InputClass"
    Identifier	"Trackpoint Wheel Emulation"
    MatchProduct	"TPPS/2 IBM TrackPoint|DualPoint Stick|Synaptics Inc. Composite TouchPad / TrackPoint|ThinkPad USB Keyboard with TrackPoint|USB Trackpoint pointing device"
    MatchDevicePath	"/dev/input/event*"
    Option		"EmulateWheel"		"true"
    Option		"EmulateWheelButton"	"2"
    Option		"Emulate3Buttons"	"false"
    Option		"XAxisMapping"		"6 7"
    Option		"YAxisMapping"		"4 5"
EndSection

```

### Touchpad

There is a synaptic touchpad on this laptop. If you follow [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"), you should have no problems getting this to work.

The relevant kernel driver is:

*   mouse_ps2_synaptics

### ThinkFinger

Works, read [ThinkFinger](/index.php/ThinkFinger "ThinkFinger") for reference and examples.

### ACPI

To get all the special keys working requires the module:

*   THINKPAD_ACPI

It is necessary to edit the default /etc/acpi/handler.sh included with the acpid package to get these keys working.

```
#!/bin/sh
# Default acpi script that takes an entry for all actions, modified to include thinkpad special keys.

# NOTE: This is a 2.6-centric script.  If you use 2.4.x, you'll have to
#       modify it to not use /sys

minspeed=`cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_min_freq`
maxspeed=`cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_max_freq`
setspeed="/sys/devices/system/cpu/cpu0/cpufreq/scaling_setspeed"

set $*

case "$1" in
   ibm/hotkey)
   case "$2" in
       HKEY)
           case "$4" in
               00001002) # Lock screen
               #Enter your xlock or xscreensaver command here
                   ;;
               00001003) # switching display off
                   xset dpms force off
                   ;;
               00001004) # Suspend to RAM
                   /usr/sbin/pm-suspend
                   ;;
               00001005) # Switch Bluetooth
                   ;;
               00001007) # Toggle external display
                   if [ "$(xrandr -q | grep "VGA connected")" ]; then
                       if [ "$(xrandr -q | grep "VGA connected [0-9]")" ]; then
                           xrandr --output VGA --off
                       else
                           xrandr --output VGA --auto
                       fi
                   else
                       xrandr --output VGA --off
                   fi
                   ;;
               #00001008) # Toggle Trackpoint/Touchpad
               #    ;;
               #00001009) # Eject from dock
               #    ;;
               0000100c) # Hibernate
                   /usr/sbin/pm-hibernate
                   ;;
               00001011) #Brightness down
                   CUR="xbacklight -get"
                   CUR="echo $CUR | awk '{print $1-5}'"
                   xbacklight -set $CUR
                   ;;
               00001012) #Brightness up
                   CUR=`xbacklight -get`
                   CUR="echo $CUR | awk '{print $1+5}'"
                   xbacklight -set $CUR
                   ;;
               #00001014) # Toggle zoom
               #    ;;
               00001018) # ThinkVantage button
                   ;;
           esac
           ;;
   esac
   ;;
   button/power)
       #echo "PowerButton pressed!">/dev/tty5
       case "$2" in
           PWRF)   
              logger "PowerButton pressed: $2"
              /sbin/init 0
              ;;
           *)      logger "ACPI action undefined: $2" ;;
       esac
       ;;
   button/sleep)
       case "$2" in
           SLPB)   /usr/sbin/pm-suspend ;;
           *)      logger "ACPI action undefined: $2" ;;
       esac
       ;;
   ac_adapter)
       case "$2" in
           AC)
               case "$4" in
                   00000000)
                       #/etc/laptop-mode/laptop-mode start
                   ;;
                   00000001)
                       #/etc/laptop-mode/laptop-mode stop
                   ;;
               esac
               ;;
           *)  logger "ACPI action undefined: $2" ;;
       esac
       ;;
   battery)
       case "$2" in
           BAT0)
               case "$4" in
                   00000000)   #echo "offline" >/dev/tty5
                   #Enter whatever power scripts you have here.
                   ;;
                   00000001)   #echo "online"  >/dev/tty5
                   #Enter whatever power scripts you may have here.
                   ;;
               esac
               ;;
           CPU0)	
               ;;
           *)  logger "ACPI action undefined: $2" ;;
       esac
       ;;
   button/lid)
       #echo "LID switched!">/dev/tty5
       /usr/sbin/pm-suspend
       ;;
   *)
       logger "ACPI group/action undefined: $1 / $2"
       ;;
esac

```

### Hotswap UltraBay devices

If you want to be able to eject devices from the Thinkpad's UltraBay using Fn+F9 create a script named for example "tp_ultrabay_eject.sh" with the content from [[1]](http://www.thinkwiki.org/wiki/How_to_hotswap_Ultrabay_devices#Script_for_Ultrabay_eject).

As stated at the top of the script, the variable "DEVPATH" (near the top of the script) has to be changed to match your system. Insert the UltraBay optical drive and run:

```
udevadm info --query=path --name=/dev/sr0 | perl -pe 's!/block/...$!!'

```

Replace the value of "DEVPATH" with the output of that command.

Now change ownership and permissions of the script:

```
chown root:root tp_ultrabay_eject.sh
chmod 555 tp_ultrabay_eject.sh

```

Move it somewhere save and add it to your /etc/acpi/handler.sh (under section "ibm/hotkey)"):

```
              00001009) # Eject from dock
                  DISPLAY=:0.0 /path/to/tp_ultrabay_eject.sh
                  ;;

```

"DISPLAY=:0.0" is necessary to tell X where to send notifications to.

Now, pressing Fn+F9 unmounts the relevant filesystems, powers off the UltraBay and notifies you (using notify-send) about what's happening. If a filesystem can't be unmounted you get a warning message.

It is also possible to achieve the above by just releasing the UltraBay eject lever (without pressing Fn+F9 before). Consult [http://www.thinkwiki.org/wiki/How_to_hotswap_Ultrabay_devices](http://www.thinkwiki.org/wiki/How_to_hotswap_Ultrabay_devices) for detailed instructions on how to get it working.

### Multimedia Keys

See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

### HDAPS

See [HDAPS](/index.php/HDAPS "HDAPS").

### Card Readers

#### PCMCIA

Works as expected. Uses the module:

*   yenta

#### Compact Flash

The same goes for the Compact Flash. It's supposed to work as it uses the same interfaces as the PCMCIA does, but I can't confirm anything since I do not have a CF-card.

#### Secure Digital

The SD-card reader works out of the box with SD cards.

## Other Tweaks

### HDD clicks

Install [hdparm](/index.php/Hdparm "Hdparm") and run the following command on system startup:

```
# hdparm -B 244 /dev/sda

```

Details: [http://www.thinkwiki.org/wiki/Problem_with_hard_drive_clicking](http://www.thinkwiki.org/wiki/Problem_with_hard_drive_clicking)

## See also

*   [http://www.thinkwiki.org/wiki/ThinkWiki](http://www.thinkwiki.org/wiki/ThinkWiki)
*   This report is listed at the [TuxMobil: Linux Laptop and Notebook Installation Guides Survey: Fujitsu-Siemens - FSC](http://tuxmobil.org/fujitsu.html).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T61&oldid=376876](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T61&oldid=376876)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")