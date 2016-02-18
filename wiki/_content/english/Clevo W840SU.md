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

## Installation

Installing Archlinux is straightforward and most of the hardware works out of the box.

### Airplane Mode

To make use of the flightmode button, install *tuxedo-wmi* from the AUR and load the tuxedo-wmi module. Use xbindkeys to map the key 255 (NoSymbol) to some script that disables wifi and bluetooth and enables the airplane mode LED.

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

You can automate this by installing the AUR package *clevo-airplane-mode*.

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

Sound mostly works out of the box. Using *pulseaudio* simplyfies configuration, switching outputs is possible.

**Microphone**

The volume control for the microphone is mislabeled and reads *Digital* in ALSA.

### Touchpad

The touchpad works out of the box with the *synaptics* driver. All current features are supported including two finger scroll, two- and three finger click and optional mouse buttons for the edges. Use *synclient* for configuration. Four finger recognition and three finger swipe gestures do not seem to work, though.

## Problems

### Suspend/Hibernate/Resume

Suspend to disk works best with kernel 3.14.43-2-lts. Newer kernels, including the new LTS 4.1.9 and 4.2 series lead to black screens or reboots immediately after resuming. Further information may be found in [https://bugs.archlinux.org/task/44807](https://bugs.archlinux.org/task/44807) .