<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Install](#Install)
    *   [1.1 Packages](#Packages)
*   [2 Suspend](#Suspend)
*   [3 Backlight](#Backlight)
    *   [3.1 Fingerprint reader](#Fingerprint_reader)
    *   [3.2 Thunderbolt 3](#Thunderbolt_3)
        *   [3.2.1 eGPU](#eGPU)
        *   [3.2.2 Dock Stations](#Dock_Stations)
    *   [3.3 Tablet mode](#Tablet_mode)
    *   [3.4 Pen](#Pen)
    *   [3.5 External display](#External_display)
*   [4 Issues](#Issues)
    *   [4.1 USB-C Charging](#USB-C_Charging)

## Install

### Packages

<caption>Packages to install</caption>
| Package | purpose |
| [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) | Auto brightness |
| [bolt](https://www.archlinux.org/packages/?name=bolt) | Thunderbolt 3 |
| [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) | Digitiser/Pen support |
| [nvidia](https://www.archlinux.org/packages/?name=nvidia) | For external GPU |
| [compute-runtime](https://aur.archlinux.org/packages/compute-runtime/) | For OpenCL CPU support |

## Suspend

If closing the lid doesn't suspend. In `/etc/systemd/logind.conf` uncomment the following:

 `/etc/systemd/logind.conf/etc/systemd/logind.conf` 
```
HandleSuspendKey=suspend
HandleLidSwitch=suspend
```

## Backlight

Works in gnome but can be reduced so far that it goes off, leaving the screen black.

One of these kernel parameters might fix this:

 `kernel parameters` 
```
acpi_backlight=video
acpi_backlight=vendor
acpi_backlight=native
```

Installing [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) does auto brightness.

### Fingerprint reader

The device is `Bus 001 Device 005: ID 06cb:0081 Synaptics, Inc.` Nether [fprint](https://www.archlinux.org/groups/x86_64/fprint/) nor [thinkfinger](https://www.archlinux.org/packages/?name=thinkfinger) work, but there is a prototype driver [here](https://github.com/nmikhailov/Validity90).

### Thunderbolt 3

Works once you install [bolt](https://www.archlinux.org/packages/?name=bolt).
**Note:** TODO: Add links to authoritative information on tb3
This can be temperamental, it may require unplugging and re-plugging the eGPU.

#### eGPU

This was tested with a Gigabyte Aorus 1070\. [Bumblebee](/index.php/Bumblebee "Bumblebee") might blacklist the nvidia module, comment out the nvidia modules in `/usr/lib/modprobe.d/bumblebee.conf` so that it looks like this:

 `/usr/lib/modprobe.d/bumblebee.conf` 
```
#blacklist nvidia
#blacklist nvidia-drm
#blacklist nvidia-modeset
#blacklist nvidia-uvm
blacklist nouveau
```

The following allows Xorg to use the GPU if it exists - you'll need to ether delay the Xorg startup or restart it once the device is fully active.

 `xorg.conf for both external and internal graphics` 
```
Section "ServerLayout"
    Identifier  "eGPU"
    # The two screens allow the server to start in one of two modes
    Screen 0 "eGPUScreen"
    Inactive "Intel"   
    Screen 1 "IntelScreen"
EndSection

Section "Device"
    Identifier  "eGPU"
    Driver      "nvidia"
    VendorName  "NVIDIA Corporation"
    Option "NoLogo" "true"
    Option "AllowEmptyInitialConfiguration"
    Option "AllowExternalGpus"
EndSection

Section "Device"
    Identifier   "Intel"
    Driver       "intel"
    VendorName   "Intel"
EndSection

Section "Screen"
    Identifier "eGPUScreen"
    Device     "eGPU"
EndSection

Section "Screen"
    Identifier "IntelScreen"
    Device     "Intel"
EndSection

```

You can use this script to delay the display manager until the device is fully configured.

 `/usr/local/bin/wait-for-egpu.sh` 
```
#!/bin/bash
DEVICE=/dev/dri/card1

# switch to our vt to see the messages
chvt 2
delay=30
wait=1

#while [ \( ! -c "$DEVICE" \) -a $delay -gt 1 -a `cat /sys/class/power_supply/AC*/online` != "1" ] ; do
while [ $wait -gt 0 -a $delay -gt 1 ]; do

        if [ \( -c "$DEVICE" \) -a `cat /sys/class/power_supply/AC*/online` == "1" ] ; then
                echo $'\e[32;1meGPU present, on AC power.\e[0m'
        elif [ -c "$DEVICE" ]; then
                echo $'\e[33;1meGPU present but no power.\e[0m'
        else
                echo $'\e[31;1mNo eGPU.\e[0m'
        fi

        echo "Press 'Y' to continue to Login. Press 'W' to wait forever. Any other key to rescan."

        if read -r -s -n 1 -t 5 key ; then

                if [ "$key" == "y" -o "$key" == "Y" ]; then
                        wait=0
                elif [ "$key" == "w" -o "$key" == "W" ]; then
                        wait=2
                fi
        elif [ $wait -eq 1 ]; then
                let "delay -= 5"
                echo "Waiting for ${delay} more seconds for eGPU."
        fi

done
```

Add the [systemd](/index.php/Systemd "Systemd") setup file below and activate it with `systemctl daemon-reload` and `systemctl enable wait-for-egpu`

 `/etc/systemd/system/wait-for-egpu.service` 
```
[Unit]
Description=Simple interactive dialog window
After=getty@tty2.service
Before=display-manager.service

[Service]
Type=oneshot
ExecStart=/usr/local/bin/wait-for-egpu.sh
StandardInput=tty
TTYPath=/dev/tty2
TTYReset=yes
TTYVHangup=yes

[Install]
WantedBy=multi-user.target
```

#### Dock Stations

<caption>Wavlink USB-C Ultra 5K Universal Docking Station</caption>
| Feature | Status |
| USB-C | Working |
| USB 3.0 | Working |
| Audio Jack | Working |
| Gigabit Ethernet | Working |
| HDMI 1 & 2 | Only X11, requires [DisplayLink](/index.php/DisplayLink "DisplayLink") |
| DisplayPort 1 & 2 | Untested |
| 5K Combo (Joined DisplayPorts) | Untested |

**Warning:** Some Windows Managers running in Wayland will freeze your system completely if there is a display connected to the dock station, requiring a reboot. This is the case of SwayWM.

**Note:** DisplayLink has stated [here](https://support.displaylink.com/forums/287786-displaylink-feature-suggestions/suggestions/16639654-linux-wayland-support) that they are working to bring eGPU/DisplayLink multimonitor support to Wayland through GNOME and a [patch was submitted for GNOME 3.32](https://gitlab.gnome.org/GNOME/mutter/commit/d4bea60e1aab8e58bd2925d24256ddfdd125dbdb)

### Tablet mode

Try gnome extension slide-for-keyboard, keyboard automatically disables under gnome.

### Pen

install [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom)

### External display

HDMI on USB-C adapter just works

## Issues

### USB-C Charging

With the Gigabyte Aorus 1070 Gaming box, the charging sometimes stops. Doesn't seem to happen in Windows.