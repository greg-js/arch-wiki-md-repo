Notes to get Arch Linux on the [GPD Pocket](https://www.indiegogo.com/projects/gpd-pocket-7-0-umpc-laptop-ubuntu-or-win-10-os-laptop--2#/).

## Contents

*   [1 Specs](#Specs)
*   [2 Installation](#Installation)
    *   [2.1 Power and Fan](#Power_and_Fan)
    *   [2.2 WiFi](#WiFi)
    *   [2.3 Bluetooth](#Bluetooth)
    *   [2.4 Xorg](#Xorg)
    *   [2.5 Sound](#Sound)
    *   [2.6 SDDM](#SDDM)
    *   [2.7 Touchscreen Gestures](#Touchscreen_Gestures)
    *   [2.8 KDE Display](#KDE_Display)
    *   [2.9 Mouse Scroll Emulation](#Mouse_Scroll_Emulation)
*   [3 Known Issues](#Known_Issues)
*   [4 Acknowledgements:](#Acknowledgements:)

## Specs

Display: 7inch IPS 1920x1200
CPU: Intel Atom X7-Z8750
RAM: 8GB LPDDR3-1600
Storage: 128GB eMMC SSD (non-replacable)
Battery: 7000mAH
WiFi: Broadcom 4356 802.11ac
Bluetooth: Broadcom 2045
Audio: Realtek ALC5645
Ports: 1 x USB 3 type A, 1 x MicroHDMI, 1 x USB 3 type C 1 x 3.5mm Headphone Jack

## Installation

During Boot add **"fbcon=rotate:1"** to the kernel line to rotate the console. Install using USB Ethernet following the wiki. During install append to /etc/pacman.conf.

 `/etc/pacman.conf` 
```
[gpd-pocket] 
SigLevel = Optional TrustAll 
Server = https://github.com/njkli/$repo/raw/master/repo 

```

Install fan control and custom kernel using `# pacman -S gpd-fan linux-jwrdegoede linux-jwrdegoede-docs linux-jwrdegoede-headers`.

### Power and Fan

Install [tlp](https://www.archlinux.org/packages/?name=tlp) `# pacman -S tlp`
Edit the following lines in /etc/default/tlp

 `/etc/default/tlp` 
```
...
DISK_DEVICES="mmcblk0"
DISK_IOSCHED="deadline" 
...

```

Copy fan config `# cp /etc/default/gpd-fan.example /etc/default/gpd-fan` and uncomment settings.

### WiFi

Copy brcmfmac4356-pcie.txt from [here](https://github.com/cawilliamson/ansible-gpdpocket/tree/master/roles/common/files) to /lib/firmware/brcm/ then run
`# modprobe -r brcmfmac`
`# modprobe brcmfmac`

**Note:** This did not work for me right away. I would get this error on boot

> brcmfmac: brcmf_chip_recognition: chip backplane type 15 is not supported
> brcmfmac: brcmf_pcie_probe: failed 14e4:43ec

To fix this, I installed broadcom-wl-dkms and tested and then removed it now the wifi works just fine.

### Bluetooth

To load bluetooth, enable btusb module.

 `/etc/modules-load.d/btusb.conf` 
```
btusb

```

### Xorg

Create /etc/X11/xorg.conf.d/20-intel.conf to configure graphics.

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device" 
	Identifier  "Intel Graphics" 
	Driver      "intel" 
	Option      "AccelMethod"     "sna" 
	Option      "TearFree"        "true" 
	Option      "DRI"             "3" 
EndSection

```

/etc/X11/xorg.conf.d/40-monior.conf to rotate the monitor.

 `/etc/X11/xorg.conf.d/40-monior.conf` 
```
Section "Monitor" 
	Identifier "DSI1" 
	Option "Rotate" "right" 
EndSection 

```

/etc/X11/xorg.conf.d/99-touchscreen.conf to rotate the touchscreen.

 `/etc/X11/xorg.conf.d/99-touchscreen.conf` 
```
Section "InputClass" 
	Identifier	"calibration" 
	MatchProduct	"Goodix Capacitive TouchScreen" 
	Option  "TransformationMatrix" "0 1 0 -1 0 1 0 0 1" 
EndSection 

```

Alternatively you can copy the files from [here](https://github.com/nexus511/gpd-ubuntu-packages/tree/master/packages/gpdpocket-xorg/files/config).

### Sound

Copy chtrt5645.conf and HiFi.conf from [here](https://github.com/nexus511/gpd-ubuntu-packages/tree/master/packages/gpdpocket-audio/files) to /usr/share/alsa/ucm/chtrt5645/. Append the following lines into /etc/pulse/default.pa.

 `/etc/pulse/default.pa` 
```
set-card-profile alsa_card.platform-cht-bsw-rt5645 HiFi
set-default-sink alsa_output.platform-cht-bsw-rt5645.HiFi__hw_chtrt5645__sink  
set-sink-port alsa_output.platform-cht-bsw-rt5645.HiFi__hw_chtrt5645__sink [Out] Speaker  

```

Turn off realtime_scheduleing by editing /etc/pulse/daemon.conf.
`realtime-scheduling = no`

### SDDM

Change DPI to be readable, append the following lines to /usr/share/sddm/scripts/Xsetup.

 `/usr/share/sddm/scripts/Xsetup` 
```
# Set DPI  
xrandr --dpi 168"  

```

### Touchscreen Gestures

Install [touchegg](https://aur.archlinux.org/packages/touchegg/) then copy config files from [here](https://github.com/nexus511/gpd-ubuntu-packages/tree/master/packages/gpdpocket-touchegg-config/files) and set permissions.

```
# cp touchegg.conf /usr/share/touchegg/
# chmod 0644 /usr/share/touchegg/touchegg/touchegg.conf
# cp 01_touchegg /etc/X11/xinit/xinitrc.d/
# chmod 0755 /etc/X11/xinit/xinitrc.d/01_touchegg

```

### KDE Display

In System Settings > Display and Monitor change Orientation to 90° Clockwise, and Scale Display to a comfortable size.

### Mouse Scroll Emulation

Create /home/$HOME/bin/mousescroll.sh to scroll while holding right click.

 `/home/$HOME/bin/mousescroll.sh` 
```
#!/bin/bash  
# Emulate scroll wheel in built in nub while holding the right click button  
xinput --set-prop pointer:"SINO WEALTH Gaming Keyboard" "libinput Middle Emulation Enabled" 1  
# Trigger wheel emulation with button 3 (right click)  
xinput --set-prop pointer:"SINO WEALTH Gaming Keyboard" "libinput Button Scrolling Button" 3  

```

Add script to SDDM Autostart in System Settings > Startup and Shutdown > Autostart.

## Known Issues

Battery status, Wifi, and Bluetooth do not work on Arch Kernel 4.12.10-1 use Hans Kernel.

## Acknowledgements:

[https://github.com/njkli/gpd-pocket/](https://github.com/njkli/gpd-pocket/)
[https://github.com/cawilliamson/ansible-gpdpocket/](https://github.com/cawilliamson/ansible-gpdpocket/)
[https://github.com/nexus511/gpd-ubuntu-packages](https://github.com/nexus511/gpd-ubuntu-packages)
[https://www.reddit.com/r/GPDPocket/comments/6rszbo/project_linux_installer_for_gpd_pocket](https://www.reddit.com/r/GPDPocket/comments/6rszbo/project_linux_installer_for_gpd_pocket)
[http://hansdegoede.livejournal.com/](http://hansdegoede.livejournal.com/)