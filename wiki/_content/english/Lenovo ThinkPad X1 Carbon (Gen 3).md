Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")
*   [Lenovo ThinkPad X1 Carbon (Gen 6)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6) "Lenovo ThinkPad X1 Carbon (Gen 6)")

**Tip:** A great resource for thinkpads is [https://www.thinkwiki.org/wiki/ThinkWiki](https://www.thinkwiki.org/wiki/ThinkWiki)

## Contents

*   [1 Model description](#Model_description)
    *   [1.1 Support](#Support)
*   [2 Configuration](#Configuration)
    *   [2.1 Touchpad](#Touchpad)
    *   [2.2 Audio](#Audio)
    *   [2.3 Display](#Display)
        *   [2.3.1 HDMI](#HDMI)
    *   [2.4 Fingerprint Reader](#Fingerprint_Reader)
    *   [2.5 WiFi](#WiFi)
        *   [2.5.1 Bluetooth](#Bluetooth)
    *   [2.6 WWAN](#WWAN)
        *   [2.6.1 GPS](#GPS)
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
| [Fingerprint Reader](/index.php?title=Fingerprint_Reader&action=edit&redlink=1 "Fingerprint Reader (page does not exist)") | Yes |
| [Power management](/index.php/Power_management "Power management") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |

## Configuration

### Touchpad

Install [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) and see [libinput](/index.php/Libinput "Libinput") for configuration.

The correct driver is called **SynPS/2 Synaptics TouchPad**.

Enable Natural scrolling: First get the current settings:

```
xinput list-props "SynPS/2 Synaptics TouchPad" | grep "Synaptics Scrolling Distance"

```

It shows on my laptop:

```
Synaptics Scrolling Distance (301):	114, 114

```

Set these two values to negative to reverse the scrolling orientation:

```
xinput set-prop "SynPS/2 Synaptics TouchPad" "Synaptics Scrolling Distance" -114 -114

```

Similarly, to set tap actions with 1/2/3 fingers:

```
xinput set-prop "SynPS/2 Synaptics TouchPad" "Synaptics Tap Action" 0 0 0 0 1 3 2

```

and enable two-finger scrolling in all directions:

```
xinput set-prop "SynPS/2 Synaptics TouchPad" "Synaptics Two-Finger Scrolling" 1 1

```

To enable the above settings on login, put all those "set-prop" commands into your **~/.xprofile**.

### Audio

Works with [PulseAudio](/index.php/PulseAudio "PulseAudio") and [ALSA](/index.php/ALSA "ALSA") installed. The built-in speakers, headphone, and mic all work.

Some users have experienced problems with white noise and popping/cracking sounds when audio is first played and when the computer is turned off.

To fix this, blacklist snd_hda_codec_realtek.

```
# echo "blacklist snd_hda_codec_realtek" >> /etc/modprobe.d/blacklist.conf

```

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

There are stable releases of [fprintd](https://www.archlinux.org/packages/?name=fprintd) that support this device. See [Fprint](/index.php/Fprint "Fprint") for more details about how to configure it.

To display the reader's model:

```
# lsusb | grep -i finger

Bus 001 Device 004: ID 138a:0017 Validity Sensors, Inc. Fingerprint Reader

```

Note that recent versions of [fprintd](https://www.archlinux.org/packages/?name=fprintd) have been broken for this model : One was able to enroll a finger but recognition always failed. With version 0.7.0-1 everything works.

### WiFi

There are several cards used - all should be covered by iwlwifi:

*   Intel Wireless-N 7265, 2x2, 802.11b/g/n
*   Intel Dual Band Wireless-N 7265, 2x2 802.11a/b/g/n
*   Intel Dual Band Wireless-AC 7265, 2x2, 802.11a/b/g/n/ac

#### Bluetooth

All cards feature BT4.0 connectivity and should work out of the box when starting the bluetooth service

### WWAN

There are several cards used

*   Ericsson N5321 (3.5G)
*   Sierra Wireless EM7345 (4G)

EM7345: SIM-Problems, TBD

#### GPS

N5321 is unknown EM7345 can output GPS using AT-Commands. You can use [[1]](https://github.com/tuxmaster/gpsd-tcp%7Cgpsd-tcp) to interface to gpsd.

## See also

*   [Dual-Booting Arch Linux on Lenovo X1 Carbon 3rd gen](https://push.cx/2015/dual-booting-arch-linux-on-lenovo-x1-carbon-3rd-gen)
*   [X1C3 on Archlinux](http://natalian.org/archives/2015/02/18/Archlinux_on_a_Lenovo_X1C3/)
*   [ThinkWiki](https://www.thinkwiki.org/wiki/Category:X1_Carbon_(3rd_Gen))