## Contents

*   [1 Note](#Note)
*   [2 GPT / MBR Partition Table](#GPT_.2F_MBR_Partition_Table)
*   [3 Wifi issues](#Wifi_issues)
*   [4 Nvidia Optimus Setup](#Nvidia_Optimus_Setup)
    *   [4.1 Bumblebee](#Bumblebee)
    *   [4.2 Multimonitor](#Multimonitor)
*   [5 Ultranav - Trackpoint and Touchpad](#Ultranav_-_Trackpoint_and_Touchpad)
*   [6 Other](#Other)

## Note

I am also maintaining this content at [GitHub](https://github.com/kportertx/ArchTPw520) and it may be more up to date.

## GPT / MBR Partition Table

I was unable to get the most recent version of the BIOS to boot from a GPT partition table. Everything worked fine once I tried an MBR ("msdos" in gparted) partition table.

## Wifi issues

*   Random Disconnection
    *   check "dmesg | grep wlan0" will probably be complaining about "wlan0: deauthenticating from MAC by local choice (reason=3)"
    *   Arch wiki hints at solution: [Wicd#Random disconnecting](/index.php/Wicd#Random_disconnecting "Wicd")
    *   My Solution:
        *   Disable power management of pci-express in BIOS
*   Wicd cannot obtain IP address
    *   [Wicd#Failed to get IP address](/index.php/Wicd#Failed_to_get_IP_address "Wicd")
    *   Use dhclient instead of dhcpcd:
        *   pacman -S dhclient
        *   Set wicd to use dhclient:
        *   in wicd-curse press 'P', select external sources, and then select dhclient

## Nvidia Optimus Setup

### Bumblebee

nVidia Optimus works nicely with a standard [bumblebee](/index.php/Bumblebee "Bumblebee") setup, using the proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") drivers. For further information refer to the [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") article.

### Multimonitor

The digital and analog video outputs are hardwired to the nVidia chip and are thus unvailable in a standard bumblebee setup, since the X Server is run by the Intel GPU. Unlike earlier Thinkpad W Models, the VGA-Output is not connected to the integrated chip. There are several workarounds available.

Using `intel-virtual-output` works really well with little tweaking necessary

```
$ intel-virtual-output -f

```

**Note:** -f prevents it from becoming a daemon (thus easier to stop)

**Note:** Starting with nvidia-360 the nvidia-modeset module will prevent bumblebee from unloading properly and has to be removed first.

For the nvidia card to recognize external monitors, some lines have to be commented out of the default config file at `/etc/bumblebee/xorg.conf.nvidia`.

 `xorg.conf.nvidia` 
```
...
 #   Option "UseEDID" "false"
 #   Option "UseDisplayDevice" "none"
...

```

see also: [Phoronix](http://www.phoronix.com/scan.php?page=news_item&px=OTQxNg) [Nvidia Forums](http://forums.nvidia.com/index.php?showtopic=203600)

## Ultranav - Trackpoint and Touchpad

Trackpoint and Touchpad will work out of the box, but some tweaking is required for further configuration.

*   Set up trackpoint scrolling by adding a new config in `xorg.conf.d`.

 `20-trackpoint.conf` 
```
Section "InputClass"
         Identifier      "Trackpoint Wheel Emulation"
         MatchProduct    "TPPS/2 IBM TrackPoint|DualPoint Stick|Synaptics Inc. Composite TouchPad /
         MatchDevicePath "/dev/input/event*"
         Option          "EmulateWheel"                "true"
         Option          "EmulateWheelButton"  "2"
         Option          "Emulate3Buttons"     "false"
         Option          "XAxisMapping"                "6 7"
         Option          "YAxisMapping"                "4 5"
EndSection
```

*   Trackpoint sensitivity and speed can be set up using an udev rule in `/etc/udev/rules.d/` (the add-rule will work around the configuration not being applied when the trackpoint hasnt been loaded, alternatively a wait-for can be used, which comes with the added drawback of added unresponsiveness of the trackpoint some time after boot)

 `82-trackpoint.rules` 
```
# Set the trackpoint speed and sensitivity
ACTION=="add",SUBSYSTEM=="input",ATTR{name}=="TPPS/2 IBM TrackPoint",ATTR{device/sensitivity}="240"
```

*   Touchpad can be used after [installing](/index.php/Installing "Installing") [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)
    *   other Xorg Drivers can conflict with the synaptics driver causing an synclient error and unresponsiveness to Gnome Settings, this should be resolved by [removing](/index.php/Pacman "Pacman") [xf86-input-mouse](https://www.archlinux.org/packages/?name=xf86-input-mouse)

## Other

*   Boot up issue with UDEV timeout
    *   cat /var/log/boot | grep -i pci reveals udevd[169]: seq 1352 '/devices/pci0000:00/0000:00:1c.1/0000:03:00.0' killed
        *   Found similar issue here [Arch Bugs Report](https://bugs.archlinux.org/task/27938)
*   Disable annoying system beep
    *   Insert "blacklist pcspkr" into /etc/modprobe.d/pcspkr_blacklist.confor
    *   Reboot or rmmod pcspkr
*   Screen brightness setting doesnt work after linux 3.16
    *   since 3.16 video.use_native_backlight has been enabled by default, unfortunately this setting does not work well for the W520, disabling it should solve the issue

```
video.use_native_backlight=0

```