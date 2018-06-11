The Lenovo ThinkPad X250 is the successor to the [Lenovo ThinkPad X240](/index.php/Lenovo_ThinkPad_X240 "Lenovo ThinkPad X240"). Major differences include the physical TrackPoint buttons above the touchpad mouse as well as the Broadwell line of Intel CPUs.

## Contents

*   [1 Tested Configuration](#Tested_Configuration)
*   [2 System Configuration](#System_Configuration)
    *   [2.1 Mouse](#Mouse)
    *   [2.2 Fingerprint](#Fingerprint)
    *   [2.3 Backlight and Keyboard](#Backlight_and_Keyboard)
    *   [2.4 Sound and Volume Control](#Sound_and_Volume_Control)
    *   [2.5 Bluetooth](#Bluetooth)
*   [3 BIOS updates](#BIOS_updates)
*   [4 See also](#See_also)

#### Tested Configuration

**Tip:** Below are the tested configurations at the current time.

| Feature | Configuration 1 | Configuration 2 |
| CPU | Intel i5-5200U | Intel i7-5600U |
| Graphics | Intel HD 5400 | Intel HD 5500 |
| RAM | 8 GB | 8GB |
| Disk | unknown 180 GB SSD | SanDisk X300 256GB |
| Display | 12.5" IPS FHD (1920x1080) non-touch | 12.5" IPS FHD (1920x1080) non-touch |
| Wireless | Intel Wireless 7265 AC | Intel Wireless 7265 AC |
| Built-in Battery | 9 Cell | 9 Cell |
| Additional Pluggable Battery | 6 Cell 19+ | 6 Cell 19+ |
| Backlight Keyboard | Yes | Yes |
| ThinkLight | No | No |
| Fingerprint Scanner | Yes | Yes |
| Bluetooth | Yes | Yes |
| Camera | Yes | Yes |
| WWAN | ? | Sierra EM7345 |
| Smartcard reader |  ? | Yes |

### System Configuration

#### Mouse

With kernels > 4.0.5 TrackPoint and touchpad work out of the box.

#### Fingerprint

The fingerprint reader works out of the box with [fprintd](https://www.archlinux.org/packages/?name=fprintd).

#### Backlight and Keyboard

In order to get the backlight to work, I added `options thinkpad_acpi force-load=1` to `/etc/modprobe.d/x250.conf`. This forces the thinkpad_acpi module to load, which is needed for controlling the backlight via [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) as well as enable some of the extra media keys.

**Note:** Not all X250 keyboards have backlight

Although a dedicated Pause-key is missing, it can be input using the key combination `Fn` + `P`

#### Sound and Volume Control

In order to get control of the audio from Intel hdmi, you have to disable it and force alsa to use Intel PCH. See [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA") to set the default sound card to Intel PCH (speakers and headphones).

 ` /etc/modprobe.d/thinkpad-x250.conf `  `options snd_hda_intel index=1,0` 

With [acpid](https://www.archlinux.org/packages/?name=acpid) and [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) installed, you can map the volume buttons to change the volume. Here are some samples:

`/etc/acpi/events/volumemute`:

```
event=button/mute
action=amixer -c 1 sset Master toggle -q

```

`/etc/acpi/events/volumedown`:

```
event=button/volumedown
action=amixer -c 1 sset -M Master 5%%- unmute -q

```

`/etc/acpi/events/volumeup`:

```
event=button/volumeup
action=amixer -c 1 sset -M Master 5%%+ unmute -q

```

`/etc/acpi/events/mutemic`:

```
event=button/f20
action=amixer -c 1 sset Mic toggle -q

```

[PulseAudio](/index.php/PulseAudio "PulseAudio") and [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) are also great tools for fixing volume issues.

#### Bluetooth

Bluetooth works out of the box with [bluez](https://www.archlinux.org/packages/?name=bluez) and [gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth).

### BIOS updates

**Warning:** This may brick your device! Be careful!

In order to get a working and bootable usb dongle to flash a current BIOS it may be necessary to follow these steps:

1\. Download newest BIOS update tool (ISO) from Lenovos x250 downloads section[[1]](https://pcsupport.lenovo.com/de/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x250/downloads/)

2\. Install [geteltorito](https://aur.archlinux.org/packages/geteltorito/) or find another way to extract the hidden image. With geteltorito you just do `geteltorito -o thinkpadbios.img xyz.iso`

3\. Copy the extracted image to a usb dongle with dd: `sudo dd if᐀thinkpadbios.img of᐀/dev/sdX bs᐀1M`

4\. Just in case run `sync` once.

5\. Reboot

6\. Press enter at the Lenovo screen, chose your usb dongle

7\. Flash the BIOS update following the description on your screen. You need to have a charged battery and a connected ac adapter in order to run this tool successfully.

## See also

[Thinkwiki on BIOS updates (German)](http://thinkwiki.de/BIOS-Update_ohne_optisches_Laufwerk_unter_Linux)