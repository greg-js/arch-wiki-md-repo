The Lenovo X240 is the latest version of the Lenovo Ultrabook Series and also is a complete redesign of the X Series. This can be observed especially with devices like the touchpad, which has been changed to be a one-click touchpad instead of having the classic 5 button touchpad. The X240 is a very light device, weighing in at just 2.84 lbs (1.36 kg) and measuring 12.02" x 8.19" x 0.79".

## Contents

*   [1 Tested Configuration](#Tested_Configuration)
*   [2 System Configuration](#System_Configuration)
    *   [2.1 Use analog sound card by default in ALSA](#Use_analog_sound_card_by_default_in_ALSA)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 TrackPoint](#TrackPoint)
    *   [2.4 Keyboard](#Keyboard)
    *   [2.5 Fingerprint Reader](#Fingerprint_Reader)
*   [3 Caveats](#Caveats)
    *   [3.1 Common hardware problems](#Common_hardware_problems)
    *   [3.2 Grey noise with analog audio when audio is not muted](#Grey_noise_with_analog_audio_when_audio_is_not_muted)
*   [4 More later (ToDo)](#More_later_.28ToDo.29)
*   [5 See also](#See_also)

#### Tested Configuration

**Tip:** Below were the tested configurations at the current time.

| Feature | X240 | X240 (20AMS4SM00) | X240 (20ALA0K-WIG) |
| CPU | Intel(R) Core(TM) i7-4600U CPU @ 2.10GHz | Intel(R) Core(TM) i5-4210U CPU @ 2.7GHz | Inter(R) Core(TM) i5-4200U CPU @ 1.6 GHz |
| Graphics | Intel HD 4400 - Haswell-ULT | Intel HD 4400 - Haswell-ULT | Intel HD 4400 - Haswell-ULT |
| Ram | 8 GB | 8 GB | 4 GB |
| Disk | Samsung 5120 SSD | Seagate ST500LM000-SSHD-8GB | WDC WD10JPVX-08JC3T5 |
| Display | 12.5" IPS FHD (1920x1080) | 12.5" IPS FHD (1920x1080) | 12.5" IPS 1366x768 |
| Wireless | Intel Corporation Wireless 7260 | Intel Corporation Wireless 7260 | Intel Corporation Wireless 7260 |
| Built-in Battery | 9 Cell | 9 Cell | Not Tested |
| Additional Plugable Battery | 6 Cell 19+ | 6 Cell 19+ | 6 Cell 19+ |
| Backlight Keyboard | Yes | Yes | Yes |
| ThinkLight | No | No | No |
| Fingerprint Scanner | Yes | Yes | Yes |
| Bluetooth | Yes | Yes | Yes |
| Camera | Yes | Yes | Yes |

### System Configuration

#### Use analog sound card by default in ALSA

You likely need to change the ALSA default sound card if you want to output sound via line-out by default.

Install the [alsa-utils](https://www.archlinux.org/packages/?sort=&q=alsa-utils&maintainer=&flagged=) package, run `aplay -l` and inspect its output:

```
**** List of PLAYBACK Hardware Devices ****
card 0: HDMI [HDA Intel HDMI], device 3: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: HDMI [HDA Intel HDMI], device 7: HDMI 1 [HDMI 1]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: HDMI [HDA Intel HDMI], device 8: HDMI 2 [HDMI 2]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: PCH [HDA Intel PCH], device 0: ALC3232 Analog [ALC3232 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

The card that drives the analog line-out is in this case card #1\. Create a global configuration file to make it the default:

 `$ cat /etc/asound.conf` 
```
defaults.ctl.card 1
defaults.pcm.card 1
defaults.timer.card 1

```

Alternatively, the same configuration may be set in `$HOME/.asoundrc`.

#### Touchpad

The touchpad works out of the box. You will need to install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

Some users may prefer to use the trackpoint over the touchpad. In that case, the touchpad can be disabled via `synclient TouchpadOff=1`(Will be gone after re-login). See [Synaptics](/index.php/Synaptics "Synaptics") for more information and options.

#### TrackPoint

The TrackPoint is usuable out of the box, but the default parameters for speed, sensitivity and inertia yield only insufficient navigation ability given the high-res display. The following udev configuration delivers a snappy experience:

 `$ cat /etc/udev/rules.d/10-trackpoint.rules` 
```

SUBSYSTEM=="serio", DRIVERS=="psmouse", ACTION=="change", ENV{SERIO_TYPE}=="05", ATTR{press_to_select}="1", ATTR{sensitivity}="196", ATTR{speed}="255", ATTR{inertia}="4"

```

Consult the [ThinkWiki](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint) for other configuration possibilities such as scrolling.

#### Keyboard

The keyboard works out of the box mostly, including the `Fn` key and XF86 aliases. For the LED of the `XF86AudioMute` button to work `acpi_osi="Linux"` needs to be appended to the kernel line in the bootloader. For [GRUB](/index.php/GRUB "GRUB") this would be:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="acpi_osi=\"Linux\""` 

Most WMs/DEs handle the special XF86 keys automatically, but you might need to add a configuration yourself. Tools like `amixer` ([alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils)), [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight), [arandr](https://www.archlinux.org/packages/?name=arandr) and [lxrandr](https://www.archlinux.org/packages/?name=lxrandr) help in this regard.

The button `XF86WLAN` automatically toggles the (soft) *rfkill* block state of the wireless device. Keep this in mind when you set it up to connect/disconnect to your wireless network. You can also unblock wlan without using this key: `rfkill unblock wlan`.

The keyboard doesn't have an LED for `Caps Lock`. If your WM/DE doesn't come with an indicator you can use [indicator-keylock](https://aur.archlinux.org/packages/indicator-keylock/) in the tray.

The indicator LED for `XF86AudioMicMute` seems to be broken in some way. According to [this commit](https://github.com/torvalds/linux/commit/420f9739a62cdb027f5580d25c813501ff93aa6f) it should work with `snd-hda-intel` but it doesn't. There is also an [older kernel patch](http://comments.gmane.org/gmane.linux.drivers.platform.x86.devel/1962) available that might or might not help, but probably doesn't work with a current kernel as is.

#### Fingerprint Reader

The fingerprint reader is a Validity Sensors model (138a:0017) also used on the Thinkpad X1 Carbon and T440\. ThinkFinger does NOT support this reader. This fingerprint reader requires libfprint to be build from the current git ([https://github.com/ars3niy/fprint_vfs5011.git](https://github.com/ars3niy/fprint_vfs5011.git) ). Alternatively, it can also be done going through [Fprint](/index.php/Fprint "Fprint"), for 20ALA0K-WIG.

### Caveats

#### Common hardware problems

[This page](https://github.com/leoluk/thinkpad-stuff/wiki/Haswell-ThinkPad-problems) provides a list and links regarding common issues with X240 hardware.

#### Grey noise with analog audio when audio is not muted

On some X240 and other TP 4xx models, persisting grey noise is hearable when the audio mixer has not been muted. The issue has been [reported to the ALSA developers](http://mailman.alsa-project.org/pipermail/alsa-devel/2014-December/085403.html), but as of now, the issue persists. Affected users are encouraged to report their situation in the linked thread.

### More later (ToDo)

```
- kernel
- powersave
- backlight
- keyboard

```

## See also

*   [A user's configuration walk through](http://www.function.fr/tag/x240/)
*   [Lenovo X240 Hardware Maintenance Manual](http://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles_pdf/x240_hmm_en_sp40a26001.pdf)
*   [Lenovo X240 User Guide](http://www.lenovo.com/shop/americas/content/user_guides/x240_ug_en.pdf)
*   [X240 on ThinkWiki.de (German)](http://thinkwiki.de/X240)
*   [X240 on ThinkWiki.org](http://www.thinkwiki.org/wiki/Category:X240)