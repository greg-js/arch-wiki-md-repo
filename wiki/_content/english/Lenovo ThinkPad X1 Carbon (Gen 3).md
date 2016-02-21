## Contents

*   [1 Model description](#Model_description)
    *   [1.1 Support](#Support)
*   [2 Configuration](#Configuration)
    *   [2.1 Trackpad](#Trackpad)
    *   [2.2 Audio](#Audio)
    *   [2.3 Display](#Display)
        *   [2.3.1 HDMI](#HDMI)
    *   [2.4 Fingerprint Reader](#Fingerprint_Reader)
*   [3 See also](#See_also)

## Model description

Lenovo ThinkPad X1 Carbon, Gen 3\.

*   No optical drive.
*   [UEFI](/index.php/UEFI "UEFI") with BIOS-legacy fallback mode.

To ensure you have this version, run *dmidecode*:

```
# dmidecode -t system | grep Version

Version: ThinkPad X1 Carbon 3rd

```

Options:

*   There is a version with a touch screen
*   The integrated mobile broadband can be upgraded to a LTE Sierra EM7345

### Support

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes |
| Mobile broadband |  ?? |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Touchscreen](/index.php/Touchscreen "Touchscreen") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| Camera | Yes |
| Fingerprint Reader | Yes |
| [Power management](/index.php/Power_management "Power management") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |

## Configuration

### Trackpad

Install [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) and see [libinput](/index.php/Libinput "Libinput") for configuration.

The correct driver is called **SynPS/2 Synaptics TouchPad**.

### Audio

Works with [PulseAudio](/index.php/PulseAudio "PulseAudio") and [ALSA](/index.php/ALSA "ALSA") installed. The built-in speakers, headphone, and mic all work.

### Display

There are three options for displays:

*   14" FHD TN (1920 x 1080): Works
*   14" WQHD+ (2560 x 1440): Works, see [HiDPI](/index.php/HiDPI "HiDPI") for configuration.
*   14" WQHD+ (2560 x 1440) Touch Screen: Works, see [HiDPI](/index.php/HiDPI "HiDPI") for configuration.

Install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) to drive the display.

[xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) works fine to adjust brightness levels.

#### HDMI

Works with [xrandr](/index.php/Xrandr "Xrandr"). Use [arandr](https://www.archlinux.org/packages/?name=arandr) or [lxrandr](https://www.archlinux.org/packages/?name=lxrandr) for a GUI.

### Fingerprint Reader

There are stable releases of [libfprint](https://www.archlinux.org/packages/?name=libfprint) that support this device. See [Fprint](/index.php/Fprint "Fprint") for more details about how to configure it.

To display the reader's model:

```
# lsusb | grep -i finger

Bus 001 Device 004: ID 138a:0017 Validity Sensors, Inc. Fingerprint Reader

```

Note that recent versions of fprint are broken for this model : One is able to enroll a finger but recognition always fails.

## See also

*   [Dual-Booting Arch Linux on Lenovo X1 Carbon 3rd gen](https://push.cx/2015/dual-booting-arch-linux-on-lenovo-x1-carbon-3rd-gen)
*   [X1C3 on Archlinux](http://natalian.org/archives/2015/02/18/Archlinux_on_a_Lenovo_X1C3/)
*   [ThinkWiki](http://www.thinkwiki.org/wiki/Category:X1_Carbon_(3rd_Gen))