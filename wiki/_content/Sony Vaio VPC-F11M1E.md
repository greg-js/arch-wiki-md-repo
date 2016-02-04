# Sony Vaio VPC-F11M1E

-

## Contents

*   [1 Xorg](#Xorg)
*   [2 Display backlight regulation](#Display_backlight_regulation)
*   [3 Automatic Backlight Regulation](#Automatic_Backlight_Regulation)
*   [4 Special Keys](#Special_Keys)
    *   [4.1 Using udev](#Using_udev)
    *   [4.2 Using the kernel tool setkeycodes](#Using_the_kernel_tool_setkeycodes)
*   [5 Hardware Controls](#Hardware_Controls)
*   [6 Suspend to RAM](#Suspend_to_RAM)
*   [7 DTS/AC3 Over HDMI with ALSA](#DTS.2FAC3_Over_HDMI_with_ALSA)
*   [8 DTS/AC3 Over HDMI with PULSE](#DTS.2FAC3_Over_HDMI_with_PULSE)
*   [9 Sources](#Sources)

## Xorg

X server works with the standard [nvidia](https://www.archlinux.org/packages/?name=nvidia) package but shows a blank screen when exiting the X server or just switching terminals using Ctrl+Alt+Fx.

To resolve the blank screen issue you need to use [vesafb](https://wiki.archlinux.org/index.php/Uvesafb).

Install [v86d](https://aur.archlinux.org/packages/v86d/) and remove any vga=<foo> kernel boot parameters.

Next ensure that `/etc/modprobe.d/uvesafb.conf` contains:

```
options uvesafb mode_option=1280x800-32 scroll=ywrap

```

This isn't the largest resolution available (1280x1024-32 is) but it best fits the aspect ratio of the screen.

Finally add the v86d hook to HOOKS in mkinitcpio.conf:

```
HOOKS="base udev v86d ..."

```

and regenerate your initramfs with mkinitcpio (adjust the following command to your setup):

```
mkinitcpio -p linux

```

## Display backlight regulation

I found this solution - [http://code.google.com/p/vaio-f11-linux/wiki/NVIDIASetup](http://code.google.com/p/vaio-f11-linux/wiki/NVIDIASetup). It's for Vaio F11, but it works for my F13 too.

I've added this line in section "Device" in /etc/X11/xorg.conf :

```
Option    "RegistryDwords"    "EnableBrightnessControl=1;PowerMizerEnable=0x1;PerfLevelSrc=0x3333;PowerMizerLevel=0x3;PowerMizerDefault=0x3;PowerMizerDefaultAC=0x3"

```

Plus I use module **sony_laptop** .. MODULES=(sony_laptop) in /etc/rc.conf

The patched kernel is available in the AUR: [linux-sony](https://aur.archlinux.org/packages/linux-sony/)

The sony-acpid daemon is also available in the AUR: [sony-acpid-git](https://aur.archlinux.org/packages/sony-acpid-git/)

Keep in mind that you will need a custom **nvidia** package for each custom kernel. Alternatively, you can install [nvidia-all](https://aur.archlinux.org/packages/nvidia-all/)

## Automatic Backlight Regulation

This requires the [linux-sony](https://aur.archlinux.org/packages/linux-sony/) and [sony-acpid-git](https://aur.archlinux.org/packages/sony-acpid-git/) packages.

Once those two packages are installed, add sony-acpid to the DAEMONS array in rc.conf:

```
DAEMONS=(hwclock syslog-ng !network !netfs crond @net-profiles alsa sony-acpid)

```

## Special Keys

The 'Display Off' and media keys work out of the box.

The 'ASSIST', 'S1' and 'VAIO' keys require configuring the appropriate keymap.

### Using udev

Firstly run:

```
$ /lib/udev/findkeyboards

```

Then do:

```
# /lib/udev/keymap -i input/eventX

```

BUT switch `input/eventX` for the keyboard outputted in the first command. I got 'AT keyboard' and 'module' from the first command. 'AT keyboard' is the normal keyboard for mapping 'Fn+X' and 'module' is the hotkey keyboard.

After doing the second command you need to press the buttons that you want to map, then Control-C to exit `keymap`.

Then edit /lib/udev/keymaps/module-sony, adding the relevant scan code from the second command and then the event you want. All valid events are listed in [http://hal.freedesktop.org/quirk/quirk-keymap-list.txt](http://hal.freedesktop.org/quirk/quirk-keymap-list.txt)

Here is an example module-sony keymap file for the VPC-F11M1E:

```
0xA0 mute # Fn+F2
0xAE volumedown # Fn+F3
0xB0 volumeup # Fn+F4
0x10 brightnessdown # Fn+F5
0x11 brightnessup # Fn+F6
0x12 switchvideomode # Fn+F7
0x14 zoomout # Fn+F9
0x15 zoomin # Fn+F10
0x17 suspend # Fn+F12
0x28 help #Assist
0x20 prog1 #S1
0x49 vendor #VAIO Hotkey

```

### Using the kernel tool `setkeycodes`

_See the detailed article: [setkeycodes](/index.php/Setkeycodes "Setkeycodes")._

## Hardware Controls

Many VAIO specific hardware controls can be adjusted using the VAIO control centre, which is in the [vaio-control-center-git](https://aur.archlinux.org/packages/vaio-control-center-git/) package.

## Suspend to RAM

Out of the box, a "sudo pm-suspend" will result in a proper suspending but a failure to resume, resulting in a new reboot. The solution is to add the following parameter to your kernel (into the line )

 `acpi_sleep=nonvs` 

Your grub kernel entry should look like this

 `linux /boot/vmlinuz-linux-sony root=/dev/dm-1 acpi_sleep=nonvs` 

## DTS/AC3 Over HDMI with ALSA

Make sure you installed ALSA.

 `$ aplay -l` 

```
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: ALC275 Analog [ALC275 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: ALC275 Digital [ALC275 Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: NVidia [HDA NVidia], device 3: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: NVidia [HDA NVidia], device 7: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: NVidia [HDA NVidia], device 8: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: NVidia [HDA NVidia], device 9: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

The right ALSA device to use to get a working sound over HDMI is the device **7**.

To get mplayer to use it,

 `mplayer -ao alsa:device=hw=1.7 -channels 8 -ac hwdts,hwac3, <file>` 

The comma after hwac3 is not a typo.

## DTS/AC3 Over HDMI with PULSE

After installing **pulseaudio**, you will need to edit

```
/etc/pulse/default.pa

```

and add the following line

 `load-module module-alsa-sink device=hw:1,7 channels=8` 

Put channels to the highest number of **channels** supported by the combination of your hardware (computer + receiver/TV).

## Sources

[http://code.google.com/p/vaio-f11-linux/w/list?q=label:State-Solution](http://code.google.com/p/vaio-f11-linux/w/list?q=label:State-Solution)

[https://wiki.archlinux.org/index.php/Map_scancodes_to_keycodes](https://wiki.archlinux.org/index.php/Map_scancodes_to_keycodes)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sony_Vaio_VPC-F11M1E&oldid=392672](https://wiki.archlinux.org/index.php?title=Sony_Vaio_VPC-F11M1E&oldid=392672)"