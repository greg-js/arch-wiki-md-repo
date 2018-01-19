Notes to get Arch Linux on the [GPD Pocket](https://www.indiegogo.com/projects/gpd-pocket-7-0-umpc-laptop-ubuntu-or-win-10-os-laptop--2#/).

## Contents

*   [1 Specs](#Specs)
*   [2 Installation](#Installation)
    *   [2.1 Automatic](#Automatic)
    *   [2.2 Manual](#Manual)
*   [3 Configuration](#Configuration)
    *   [3.1 Automatic](#Automatic_2)
    *   [3.2 Manual](#Manual_2)
        *   [3.2.1 Bluetooth](#Bluetooth)
        *   [3.2.2 WiFi](#WiFi)
        *   [3.2.3 Backlight and KMS](#Backlight_and_KMS)
        *   [3.2.4 Wayland](#Wayland)
            *   [3.2.4.1 Basic Configuration](#Basic_Configuration)
            *   [3.2.4.2 Right Click Emulation](#Right_Click_Emulation)
        *   [3.2.5 Xorg](#Xorg)
            *   [3.2.5.1 Basic Configuration](#Basic_Configuration_2)
            *   [3.2.5.2 Gnome and GDM](#Gnome_and_GDM)
            *   [3.2.5.3 KDE](#KDE)
            *   [3.2.5.4 Right Click Emulation](#Right_Click_Emulation_2)
            *   [3.2.5.5 SDDM](#SDDM)
            *   [3.2.5.6 Touchscreen Gestures](#Touchscreen_Gestures)
        *   [3.2.6 Fan](#Fan)
        *   [3.2.7 Power Saving](#Power_Saving)
        *   [3.2.8 PulseAudio](#PulseAudio)
*   [4 Known Issues](#Known_Issues)
*   [5 Acknowledgements](#Acknowledgements)

## Specs

*   Display: 7inch IPS 1920x1200
*   CPU: Intel Atom X7-Z8750
*   RAM: 8GB LPDDR3-1600
*   Storage: 128GB eMMC SSD (non-replacable)
*   Battery: 7000mAh
*   WiFi: Broadcom 4356 802.11ac
*   Bluetooth: Broadcom 2045
*   Audio: Realtek ALC5645
*   Ports: 1 x USB 3 type A, 1 x MicroHDMI, 1 x USB 3 type C, 1 x 3.5mm Headphone Jack

## Installation

### Automatic

You can download a pre-patched ISO from [here](https://github.com/sigboe/GPD-ArchISO/releases).

### Manual

During boot add `fbcon=rotate:1` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to rotate the console.

Install using a USB Ethernet dongle by following the [installation guide](/index.php/Installation_guide "Installation guide").

## Configuration

### Automatic

During install append the following to /etc/pacman.conf:

 `/etc/pacman.conf` 
```
...
[gpd-pocket] 
SigLevel = Optional TrustAll 
Server = https://github.com/njkli/$repo/releases/download/$arch
...

```

Install the changes necessary for the GPD Pocket to run Arch properly by running:

`# pacman -Syu --noconfirm gpd-pocket-support`

### Manual

#### Bluetooth

To load bluetooth create the following file:

 `/etc/modules-load.d/btusb.conf` 
```
btusb

```

#### WiFi

Copy `brcmfmac4356-pcie.txt` and `brcmfmac4356-pcie.bin` from [here](https://raw.githubusercontent.com/njkli/gpd-pocket/master/gpd-pocket-support/brcmfmac4356-pcie.txt) to `/usr/lib/firmware/brcm/` then run:

```
# modprobe -r brcmfmac
# modprobe brcmfmac

```

**Note:** This did not work for me right away. I would get this error on boot:
```
brcmfmac: brcmf_chip_recognition: chip backplane type 15 is not supported
brcmfmac: brcmf_pcie_probe: failed 14e4:43ec

```
To fix this, I installed [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms) and tested and then removed it now the wifi works just fine.

#### Backlight and KMS

In order to enable backlight control with early KMS change `/etc/mkinitcpio.conf` to match the following:

 `/etc/mkinitcpio.conf` 
```
...
MODULES=(pwm_lpss pwm_lpss_platform i915)
...

```

#### Wayland

##### Basic Configuration

Create `/etc/udev/rules.d/99-goodix-touch.rules` to rotate the touchscreen:

 `/etc/udev/rules.d/99-goodix-touch.rules` 
```
ACTION=="add|change", KERNEL=="event[0-9]*", ATTRS{name}=="Goodix Capacitive TouchScreen", ENV{LIBINPUT_CALIBRATION_MATRIX}="0 1 0 -1 0 1"

```

##### Right Click Emulation

The above configuration for mouse scroll emulation only works for Xorg. Under Wayland, such configuration is supposed to be exposed by the compositor, and unfortunately, some compositors (e.g. GNOME Wayland) does not expose these configurations properly. However, the regarding functionality is still available in `libinput`. Since these compositors normally loads `/etc/profile.d`, `LD_PRELOAD` can be used to hook into `libinput` and force apply these configurations.

A sample implementation of this approach is available [here](https://github.com/PeterCxy/scroll-emulation).

#### Xorg

##### Basic Configuration

Create `/etc/X11/xorg.conf.d/20-intel.conf` to configure graphics:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
  Identifier    "Intel Graphics"
  Driver        "intel"
  Option        "TearFree" "true"
EndSection

```

Create `/etc/X11/xorg.conf.d/30-monitor.conf` to rotate the monitor:

 `/etc/X11/xorg.conf.d/30-monitor.conf` 
```
Section "Monitor"
  Identifier "DSI1"
  Option     "Rotate" "right"
EndSection

```

Create `/etc/X11/xorg.conf.d/40-touchscreen.conf` to rotate the touchscreen:

 `/etc/X11/xorg.conf.d/40-touchscreen.conf` 
```
Section "InputClass"
  Identifier    "GoodixTS"
  MatchProduct  "Goodix Capacitive TouchScreen"
  Option        "TransformationMatrix" "0 1 0 -1 0 1 0 0 1"
EndSection

```

##### Gnome and GDM

Edit `~/.config/monitors.xml` (this file might not be present by default):

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

For [GDM](/index.php/GDM "GDM"), copy the above `~/.config/monitors.xml` to `/var/lib/gdm/.config/monitors.xml` to set the correct rotation.

##### KDE

In *System Settings > Display and Monitor* change *Orientation* to *90° Clockwise*, and *Scale Display* to a comfortable size.

##### Right Click Emulation

Create `/etc/X11/xorg.conf.d/50-trackpoint.conf` to scroll while holding right click:

 `/etc/X11/xorg.conf.d/50-trackpoint.conf` 
```
Section "InputClass"
  Identifier      "GPD trackpoint"
  MatchProduct    "SINO WEALTH Gaming Keyboard"
  MatchIsPointer  "on"
  Driver          "libinput"
EndSection

```

##### SDDM

Change DPI to be readable, append the following lines to `/usr/share/sddm/scripts/Xsetup`:

 `/usr/share/sddm/scripts/Xsetup` 
```
# Set DPI  
xrandr --dpi 168"  

```

##### Touchscreen Gestures

Install [touchegg](https://aur.archlinux.org/packages/touchegg/) then copy config files from [here](https://github.com/nexus511/gpd-ubuntu-packages/tree/master/packages/gpdpocket-touchegg-config/files) and set permissions:

```
# cp touchegg.conf /usr/share/touchegg/
# chmod 0644 /usr/share/touchegg/touchegg.conf
# cp 01_touchegg /etc/X11/xinit/xinitrc.d/
# chmod 0755 /etc/X11/xinit/xinitrc.d/01_touchegg

```

#### Fan

With the latest kernel your fan should work out of the box.

**Note:** If you are having issues with your fan not functioning as intended - try the following:
```
# modprobe -r gpd-pocket-fan
# modprobe gpd-pocket-fan temp_limits=40000,40001,40002

```

Once this has been completed - you should hear your fan start up at 40c - if you hear a clicking sound - power off the device, remove the back panel and very gently push the fan around a few times. Then re-attach the panel and power on the device - running the above commands again once logged in. It seems to be an issue with some devices that the fan cannot start properly when it has not been powered on in a while. This resolved the issue for me.

Once you have completed these steps and the fan is working properly - you should then either reboot or run the following in order to return the temperature limits to default:

```
# modprobe -r gpd-pocket-fan
# modprobe gpd-pocket-fan

```

#### Power Saving

Install [tlp](https://www.archlinux.org/packages/?name=tlp) and then edit following lines in `/etc/default/tlp`:

 `/etc/default/tlp` 
```
...
# improve disk IO
DISK_DEVICES="mmcblk0"
DISK_IOSCHED="deadline"
...
# disable wifi power saving mode (wifi speed drops MASSIVELY!)
WIFI_PWN_ON_AC=off
WIFI_PWR_ON_BAT=off
...

```

#### PulseAudio

Append the following lines into `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa` 
```
set-card-profile alsa_card.platform-cht-bsw-rt5645 HiFi
set-default-sink alsa_output.platform-cht-bsw-rt5645.HiFi__hw_chtrt5645_0__sink  
set-sink-port alsa_output.platform-cht-bsw-rt5645.HiFi__hw_chtrt5645_0__sink [Out] Speaker  

```

Turn off realtime scheduling by editing `/etc/pulse/daemon.conf`:

`realtime-scheduling = no`

**Note:** You might need to manually select the correct output (Speaker) sometimes through pactl or your desktop's settings page.

## Known Issues

*   USB-C power source status, screen brightness control do not work on Arch Kernel 4.14-2\. Use Hans kernel.

## Acknowledgements

*   [https://github.com/njkli/gpd-pocket/](https://github.com/njkli/gpd-pocket/)
*   [https://github.com/cawilliamson/ansible-gpdpocket/](https://github.com/cawilliamson/ansible-gpdpocket/)
*   [https://github.com/nexus511/gpd-ubuntu-packages](https://github.com/nexus511/gpd-ubuntu-packages)
*   [https://www.reddit.com/r/GPDPocket/comments/6rszbo/project_linux_installer_for_gpd_pocket](https://www.reddit.com/r/GPDPocket/comments/6rszbo/project_linux_installer_for_gpd_pocket)
*   [http://hansdegoede.livejournal.com/](http://hansdegoede.livejournal.com/)