# Clevo W840SU

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The W840SU is a device by the taiwanese OEM manufacturer Clevo. It is sold as Schenker S403, Tuxedo Book UC1402 and Nexoc B401\. A touch version exists as W840SU-T or UT1402\. The hardware is configurable and includes an Intel Haswell Core i3/i5/i7, Intel HD 4400 graphics, a 7 mm harddrive, a mSATA device (storage, 3g/LTE modem) and a HDMI output.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Airplane Mode](#Airplane_Mode)
    *   [1.2 Webcam](#Webcam)
    *   [1.3 Brightness Keys](#Brightness_Keys)
    *   [1.4 Sound](#Sound)
    *   [1.5 Touchpad](#Touchpad)
*   [2 Problems](#Problems)
    *   [2.1 Suspend/Hibernate/Resume](#Suspend.2FHibernate.2FResume)
    *   [2.2 Brightness Keys](#Brightness_Keys_2)

## Installation

Installing Archlinux is straightforward and most of the hardware works out of the box.

### Airplane Mode

To make use of the flightmode button, install _tuxedo-wmi_ from the AUR and load the tuxedo-wmi module. Use xbindkeys to map the key 255 (NoSymbol) to some script that disables wifi and bluetooth and enables the airplane mode LED.

```
$ cat ~/.xbindkeysrc
"sudo /home/user/bin/setAirplane.sh"
   m:0x0 + c:255
   NoSymbol

```

Enable the LED with:

```
echo 1 > /sys/class/leds/tuxedo::airplane/brightness

```

You can automate this by installing the AUR package _clevo-airplane-mode_.

### Webcam

The webcam needs to be activated by pressing FN+F10, otherwise you do not see the device.

```
$ lsusb
Bus 001 Device 002: ID 8087:8000 Intel Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 002 Device 003: ID 5986:0536 Acer, Inc
Bus 002 Device 002: ID 8087:07da Intel Corp.
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### Brightness Keys

Only the dimming key works properly by default. This can be resolved by adjusting the keybindings either manually or automatically by a [desktop environment](/index.php/Desktop_environment "Desktop environment") like [KDE](/index.php/KDE "KDE").

To do it manually, ensure that `<XF86MonBrightnessUp>` [is mapped](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg") to e. g. `xbacklight -inc 10` (from [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight)), resp. `<XF86MonBrightnessDown>` to `xbacklight -dec 10`.

### Sound

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [ALSA/Troubleshooting](/index.php/ALSA/Troubleshooting "ALSA/Troubleshooting").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Clevo W840SU#](https://wiki.archlinux.org/index.php/Talk:Clevo_W840SU))

Sound mostly works out of the box. Using _pulseaudio_ simplyfies configuration, switching outputs is possible. Unfortunately, the Haswell Intel HD Audio has a strange device list:

```
$ LANG=C aplay -l
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
card 1: PCH [HDA Intel PCH], device 0: ALC282 Analog [ALC282 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

The first three devices on the first card are HDMI devices, whereas **only** number 7 works for HDMI audio. The second card is the Analog output including the speakers and the output jack. PulseAudio, as described on [PulseAudio/Examples](/index.php/PulseAudio/Examples "PulseAudio/Examples") has a bug with more than 1 HDMI audio output, but the described workaround by editing _default.pa_ did not help for this device.

Instead, the following `~/.asoundrc` resp. `/etc/asound.conf` works by setting the default ALSA device to either HDMI or analog:

```
pcm.!default {
 type plug
 slave {
   pcm "hw:1,0" # 1,0 is analog
#    pcm "hw:0,7" # 1,0 is HDMI
#    pcm "dmix:1,0" # Use this for dmix
 }
}
ctl.!default {
 type hw
 card 1
}

```

Or alternatively:

```
defaults.pcm {
	card 1
	device 0
}
defaults.ctl {
	card 1
	device 0
}

```

You have to restart all ALSA devices for this to work. Including DMIX is necessary for multiple sound sources, as it is not loaded by default for digital devices. This may degrade sound quality. An asound.conf that uses DMIX and works for one owner of a W840SU is this:

```
pcm.!default {
	type plug
	slave.pcm "dmixer"
}
ctl.!default {
	type hw
	card 1
}
pcm.dmixer {
	type dmix
	ipc_key 1024
	ipc_key_add_uid off
	ipc_perm 0666 # so that other users can acces it, e.g. mpd
	slave {
		pcm "hw:1"
		period_time 4 # I had to add this to fix stutter in wine games
		period_size 2048
		buffer_size 4096
		rate 44100
	}
	bindings {
		0 0
		1 1
	}
}
ctl.dmixer {
	type hw
	card 1
}

```

**Microphone**

The volume control for the microphone is mislabeled and reads _Digital_.

### Touchpad

The touchpad works out of the box with the _synaptics_ driver. All current features are supported including two finger scroll, two- and three finger click and optional mouse buttons for the edges. Use _synclient_ for configuration. Four finger recognition and three finger swipe gestures do not seem to work, though.

## Problems

### Suspend/Hibernate/Resume

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** No bug reports linked (Discuss in [Talk:Clevo W840SU#](https://wiki.archlinux.org/index.php/Talk:Clevo_W840SU))

Resuming with an inserted SD stops after reading the image. This is most likely a problem with the cardreader driver and is still investigated.

Suspend to disk works best with kernel 3.14.43-2-lts. Newer kernels, including the new LTS 4.1.9 and 4.2 series lead to black screens or reboots immediately after resuming after the system has been in suspend to disk for several hours. Shorter times in suspend (to disk and ram) work in most cases, which makes the problem hard to debug.

### Brightness Keys

The brightness keys stop working after an external display was connected. This may be due to the fact, that the device exposes two brightness controls:

```
$ ls /sys/class/backlight/
acpi_video0  intel_backlight

```

Changing the brightness is still possible via the inte_backlight control but not via ACPI, which is used by KDE.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Clevo_W840SU&oldid=404070](https://wiki.archlinux.org/index.php?title=Clevo_W840SU&oldid=404070)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Clevo](/index.php/Category:Clevo "Category:Clevo")