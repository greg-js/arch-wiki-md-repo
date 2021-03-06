<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 GPT / MBR Partition Table](#GPT_/_MBR_Partition_Table)
*   [2 Wifi issues](#Wifi_issues)
*   [3 Nvidia Optimus Setup](#Nvidia_Optimus_Setup)
    *   [3.1 Bumblebee](#Bumblebee)
    *   [3.2 Multimonitor](#Multimonitor)
*   [4 Ultranav - Trackpoint and Touchpad](#Ultranav_-_Trackpoint_and_Touchpad)
*   [5 Other](#Other)
*   [6 FAN Settings with Thinkfan](#FAN_Settings_with_Thinkfan)

## GPT / MBR Partition Table

I was unable to get the most recent version of the BIOS to boot from a GPT partition table. Everything worked fine once I tried an MBR ("msdos" in gparted) partition table.

## Wifi issues

*   Random Disconnection
    *   check "dmesg | grep wlan0" will probably be complaining about "wlan0: deauthenticating from MAC by local choice (reason=3)"
    *   Disable power management of pci-express in BIOS

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

It is needed to enable virtual outputs for intel graphic card `xorg.conf.d`.

 `20-intel.conf` 
```
Section "Device"
    Identifier "intelgpu0"
    Driver "intel"
    Option "VirtualHeads" "2"
EndSection
```

see also [Stackexchange](https://unix.stackexchange.com/questions/321151/do-not-manage-to-activate-hdmi-on-a-laptop-that-has-optimus-bumblebee) for troubleshooting with virtual outputs

 `multiscreen_enable.sh` 
```
#!/bin/bash
# Initializes Bumblebee for multi-screen functionality.

#modprobe bbswitch # probably not needed 
optirun true
intel-virtual-output
#following line needs to be adapted to the according sceanrio
xrandr --output LVDS1 --auto --pos 0x0 --output VIRTUAL8 --mode VIRTUAL8.740-1920x1200 --pos 1920x-60 

```
 `multiscreen_term.sh` 
```
#!/bin/bash
# Initializes Bumblebee for multi-screen functionality.
xrandr --output VIRTUAL8 --off  
xorg_process=$(ps aux | grep 'Xorg :8' | awk '{print $2}')
kill -15 $xorg_process
sleep 1
rmmod nvidia_modeset
sleep 1
rmmod nvidia

```
 `multiscreen_reinit.sh` 
```
#!/bin/bash
# Restarts Bumblebee for multi-screen functionality.

tee /proc/acpi/bbswitch <<<ON
modprobe bbswitch
modprobe nvidia-modeset
optirun true
intel-virtual-output
xrandr --output LVDS1 --auto --pos 0x0 --output VIRTUAL8 --mode VIRTUAL8.740-1920x1200 --pos 1920x-60 

```

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

*   Touchpad can be used after [installing](/index.php/Install "Install") [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)
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

## FAN Settings with Thinkfan

Default temperature management allows only a limited fan speed. This inherently leads to overheating since the laptop is designed to run with unregulated fan speed under full load.

Thinkfan.conf:

 `thinkfan.conf` 
```
Section
hwmon /sys/devices/virtual/thermal/thermal_zone0/temp
# Fan   Temp1   Temp2
(0,     0,      35)
(1,     30,     40)
(2,     35,     45)
(3,     40,     50)
(4,     45,     55)
(5,     50,     60)
(6,     55,     65)
(7,     60,     70)
(127,   65,     32767)
# last line is unregulated/max speed.  Like this the Laptop will be ~ at 60
EndSection
```