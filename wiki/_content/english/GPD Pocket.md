Notes to get Arch Linux on the [GPD Pocket](https://www.indiegogo.com/projects/gpd-pocket-7-0-umpc-laptop-ubuntu-or-win-10-os-laptop--2#/).

## Contents

*   [1 Specs](#Specs)
*   [2 Installation](#Installation)
    *   [2.1 Backlight and Early KMS](#Backlight_and_Early_KMS)
    *   [2.2 Power and Fan](#Power_and_Fan)
    *   [2.3 WiFi](#WiFi)
    *   [2.4 Bluetooth](#Bluetooth)
    *   [2.5 Xorg](#Xorg)
    *   [2.6 Mouse Scroll Emulation (Xorg)](#Mouse_Scroll_Emulation_.28Xorg.29)
    *   [2.7 Mouse Scroll Emulation (Wayland)](#Mouse_Scroll_Emulation_.28Wayland.29)
    *   [2.8 Sound](#Sound)
    *   [2.9 SDDM](#SDDM)
    *   [2.10 Touchscreen Gestures](#Touchscreen_Gestures)
    *   [2.11 KDE Display](#KDE_Display)
    *   [2.12 GNOME Wayland / GDM](#GNOME_Wayland_.2F_GDM)
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
Server = https://github.com/njkli/$repo/releases/download/$arch

```

Install fan control and custom kernel and more using `# pacman -S --force gpd-pocket-support`.

### Backlight and Early KMS

Backlight control requires **pwm_lpss** and **pwm_lpss_platform** kernel modules, which is included in the **linux-jwrdegoede** (AKA. Hans) kernel, but not in the vanilla kernel up to 4.14-2\. Hans kernel is a dependency of gpd-pocket-support.

If you wish to setup [KMS in early userspace](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"), remember to include the above 2 modules together with **i915**, otherwise these modules would not load afterwards.

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

**Note:** this step is already included in the [gpd-pocket-support](https://github.com/njkli/gpd-pocket/tree/master/gpd-pocket-support) package.

Copy brcmfmac4356-pcie.txt and brcmfmac4356-pcie.bin from [here](https://github.com/cawilliamson/ansible-gpdpocket/tree/master/roles/common/files) to /lib/firmware/brcm/ then run
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

### Mouse Scroll Emulation (Xorg)

/etc/X11/xorg.conf.d/80-trackpoint.conf to scroll while holding right click.

 `/etc/X11/xorg.conf.d/80-trackpoint.conf` 
```
Section "InputClass"
        Identifier "GPD trackpoint"
        MatchProduct "SINO WEALTH Gaming Keyboard"
        MatchIsPointer "on"
        Driver "libinput"
        Option "MiddleEmulation" "1"
        Option "ScrollButton" "3"
        Option "ScrollMethod" "button"
EndSection

```

### Mouse Scroll Emulation (Wayland)

The above configuration for mouse scroll emulation only works for Xorg. Under Wayland, such configuration is supposed to be exposed by the compistor, and unfortunaly, some compositors (e.g. GNOME Wayland) does not expose these configurations properly. However, the regarding functionality is still available in `libinput`. Since these compositors normally loads `/etc/profile.d`, `LD_PRELOAD` can be used to hook into `libinput` and force apply these configurations.

A sample implementation of this approach is available [here](https://github.com/PeterCxy/scroll-emulation).

### Sound

Copy chtrt5645.conf and HiFi.conf from [here](https://fedorapeople.org/%7Ejwrdegoede/chtrt5645/) to /usr/share/alsa/ucm/chtrt5645/. Append the following lines into /etc/pulse/default.pa.

 `/etc/pulse/default.pa` 
```
set-card-profile alsa_card.platform-cht-bsw-rt5645 HiFi
set-default-sink alsa_output.platform-cht-bsw-rt5645.HiFi__hw_chtrt5645_0__sink  
set-sink-port alsa_output.platform-cht-bsw-rt5645.HiFi__hw_chtrt5645_0__sink [Out] Speaker  

```

Turn off realtime_scheduleing by editing /etc/pulse/daemon.conf.
`realtime-scheduling = no`

**Note:** You might need to manually select the correct output (Speaker) sometimes through pactl or your desktop's settings page.

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

### GNOME Wayland / GDM

Edit ~/.config/monitors.xml (this file might not be present by default)

 `~/.config/monitors.xml` 
```
<monitors version="2">
  <configuration>
    <logicalmonitor>
      <x>0</x>
      <y>0</y>
      <scale>2</scale>
      <primary>yes</primary>
      <transform>
        <rotation>right</rotation>
        <flipped>no</flipped>
      </transform>
      <monitor>
        <monitorspec>
          <connector>DSI-1</connector>
          <vendor>unknown</vendor>
          <product>unknown</product>
          <serial>unknown</serial>
        </monitorspec>
        <mode>
          <width>1200</width>
          <height>1920</height>
          <rate>60.384620666503906</rate>
        </mode>
      </monitor>
    </logicalmonitor>
  </configuration>
</monitors>

```

This sets the correct rotation (`<rotation>right</rotation>`) and a scale factor of 2 (`<scale>2</scale>`). For fractional scaling, see [HiDPI#GNOME](/index.php/HiDPI#GNOME "HiDPI").

For [GDM](/index.php/GDM "GDM"), copy the above ~/.config/monitors.xml to /var/lib/gdm/.config/monitors.xml to set the correct rotation.

## Known Issues

Battery/usb-c power source status, screen brightness control, Wifi, and Bluetooth do not work on Arch Kernel 4.12.10-1\. Use Hans kernel.

Battery/usb-c power source status, screen brightness control, and Bluetooth do not work on Arch Kernel 4.13.12-1\. Use Hans kernel.

Usb-c power source status, screen brightness control do not work on Arch Kernel 4.14-2\. Use Hans kernel.

## Acknowledgements:

[https://github.com/njkli/gpd-pocket/](https://github.com/njkli/gpd-pocket/)
[https://github.com/cawilliamson/ansible-gpdpocket/](https://github.com/cawilliamson/ansible-gpdpocket/)
[https://github.com/nexus511/gpd-ubuntu-packages](https://github.com/nexus511/gpd-ubuntu-packages)
[https://www.reddit.com/r/GPDPocket/comments/6rszbo/project_linux_installer_for_gpd_pocket](https://www.reddit.com/r/GPDPocket/comments/6rszbo/project_linux_installer_for_gpd_pocket)
[http://hansdegoede.livejournal.com/](http://hansdegoede.livejournal.com/)