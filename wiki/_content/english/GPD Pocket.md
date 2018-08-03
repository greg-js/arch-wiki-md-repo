Notes for the [GPD Pocket](https://www.indiegogo.com/projects/gpd-pocket-7-0-umpc-laptop-ubuntu-or-win-10-os-laptop--2#/).

## Contents

*   [1 Specs](#Specs)
*   [2 Installation](#Installation)
    *   [2.1 Automatic](#Automatic)
    *   [2.2 Manual](#Manual)
*   [3 Configuration](#Configuration)
    *   [3.1 Automatic](#Automatic_2)
    *   [3.2 Manual](#Manual_2)
        *   [3.2.1 WiFi](#WiFi)
        *   [3.2.2 Backlight and KMS](#Backlight_and_KMS)
        *   [3.2.3 Wayland](#Wayland)
            *   [3.2.3.1 Basic Configuration](#Basic_Configuration)
            *   [3.2.3.2 Right Click Emulation](#Right_Click_Emulation)
        *   [3.2.4 Xorg](#Xorg)
            *   [3.2.4.1 Basic Configuration](#Basic_Configuration_2)
            *   [3.2.4.2 Gnome and GDM](#Gnome_and_GDM)
            *   [3.2.4.3 KDE](#KDE)
            *   [3.2.4.4 Right Click Emulation](#Right_Click_Emulation_2)
            *   [3.2.4.5 SDDM](#SDDM)
            *   [3.2.4.6 Touchscreen Gestures](#Touchscreen_Gestures)
        *   [3.2.5 Fan](#Fan)
        *   [3.2.6 Power Saving](#Power_Saving)
        *   [3.2.7 PulseAudio](#PulseAudio)
*   [4 Known Issues](#Known_Issues)
    *   [4.1 USB-C Power source status](#USB-C_Power_source_status)
    *   [4.2 systemd-gpt-auto-generator failed to dissect](#systemd-gpt-auto-generator_failed_to_dissect)
*   [5 See also](#See_also)

## Specs

*   Display: 7inch IPS 1920x1200
*   CPU: Intel Atom X7-Z8750
*   RAM: 8GB LPDDR3-1600
*   Storage: 128GB eMMC SSD (non-replaceable)
*   Battery: 7000mAh
*   WiFi: Broadcom 4356 802.11ac
*   Bluetooth: Broadcom 2045
*   Audio: Realtek ALC5645
*   Ports: 1 x USB 3 type A, 1 x MicroHDMI, 1 x USB 3 type C, 1 x 3.5mm Headphone Jack

## Installation

### Automatic

You can download a pre-patched ISO from [here](https://github.com/sigboe/GPD-ArchISO/releases).

### Manual

Because WiFi is not working with the default configuration, you have to fix WiFi first, or use a supported USB Ethernet/WiFi dongle.

## Configuration

### Automatic

During install append the following to /etc/pacman.conf:

 `/etc/pacman.conf` 
```
...
[gpd-pocket-arch]
SigLevel = Never
Server = https://github.com/joshskidmore/gpd-pocket-arch/raw/master
...

```

Install the changes necessary for the GPD Pocket to run Arch properly by running:

`# pacman -Syu gpd-pocket-support`

Because the patch for alsa-lib is an optional dependency, it must be installed manually to get audio to work:

`# pacman -S gpd-pocket-alsa-lib`

### Manual

#### WiFi

Install the package [gpd-pocket-support-bcm4356-git](https://aur.archlinux.org/packages/gpd-pocket-support-bcm4356-git/) and reload the WiFi kernel module:

```
# modprobe -r brcmfmac
# modprobe brcmfmac

```

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

Create `/etc/udev/rules.d/99-goodix-touch.rules` to rotate the touchscreen, and fill it with:

```
ACTION=="add|change", KERNEL=="event[0-9]*", ATTRS{name}=="Goodix Capacitive TouchScreen", ENV{LIBINPUT_CALIBRATION_MATRIX}="0 1 0 -1 0 1"

```

##### Right Click Emulation

The above configuration for mouse scroll emulation only works for Xorg. Under Wayland, such configuration is supposed to be exposed by the compositor, and unfortunately, some compositors (e.g. GNOME Wayland) does not expose these configurations properly. However, the regarding functionality is still available in `libinput`. Since these compositors normally loads `/etc/profile.d`, `LD_PRELOAD` can be used to hook into `libinput` and force apply these configurations.

A sample implementation of this approach is available [here](https://github.com/PeterCxy/scroll-emulation).

#### Xorg

##### Basic Configuration

Create `/etc/X11/xorg.conf.d/30-monitor.conf` to rotate the monitor:

**Note:** The Identifier may be different depending on your display driver of choice (either `DSI-1`  or `DSI1` )
 `/etc/X11/xorg.conf.d/30-monitor.conf` 
```
Section "Monitor"
  Identifier "DSI-1"
  Option     "Rotate" "right"
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
  Option          "MiddleEmulation" "1"
  Option          "ScrollButton" "3"
  Option          "ScrollMethod" "button"
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

Install [touchegg](https://aur.archlinux.org/packages/touchegg/), then edit the following line in `/usr/share/touchegg/touchegg.conf`:

 `/usr/share/touchegg/touchegg.conf` 
```
...
<action type="SCROLL">SPEED=7:INVERTED=true</action>
...
```

Create `/etc/X11/xinit/xinitrc.d/01_touchegg`

 `/etc/X11/xinit/xinitrc.d/01_touchegg` 

Set the permissions on `/etc/X11/xinit/xinitrc.d/01_touchegg`

```
# chmod 0755 /etc/X11/xinit/xinitrc.d/01_touchegg

```

#### Fan

With the latest kernel your fan should work out of the box.

**Note:** If you are having issues with your fan not functioning as intended - try the following:

```
# modprobe -r gpd-pocket-fan
# modprobe gpd-pocket-fan temp_limits=40000,40001,40002

```

Once this has been completed - you should hear your fan start up at 40c - if you hear a clicking sound - power off the device, remove the back panel and very gently push the fan around a few times. Then re-attach the panel and power on the device - running the above commands again once logged in. It seems to be an issue with some devices that the fan cannot start properly when it has not been powered on in a while.

Once you have completed these steps and the fan is working properly - you should then either reboot or reload the fan kernel module in order to return the temperature limits to default:

```
# modprobe -r gpd-pocket-fan
# modprobe gpd-pocket-fan

```

**Note:** By default fan is always spinning when on AC [[1]](https://github.com/stockmind/gpd-pocket-ubuntu-respin#gpd-fan-always-spinning-on-ac). To override this behavior add `gpd-pocket-fan.speed_on_ac=0` to the [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

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
WIFI_PWR_ON_AC=off
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

 `/etc/pulse/daemon.conf`  `realtime-scheduling = no` 

## Known Issues

#### USB-C Power source status

USB-C power source status does not work on Kernel 4.14-15\. Hans' kernel has a patch fixing this.

#### systemd-gpt-auto-generator failed to dissect

Due to [this issue](https://github.com/systemd/systemd/issues/5806), an error message appears at boot:

`systemd-gpt-auto-generator[199]: Failed to dissect: Input/output error`.

To avoid the error message, add this boot parameter to your boot loader.

```
systemd.gpt_auto=0

```

## See also

*   [https://github.com/njkli/gpd-pocket/](https://github.com/njkli/gpd-pocket/)
*   [http://hansdegoede.livejournal.com/](http://hansdegoede.livejournal.com/)