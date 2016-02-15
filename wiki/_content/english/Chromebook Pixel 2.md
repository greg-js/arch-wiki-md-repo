**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

The Chromebook Pixel 2 is a [Chromebook](/index.php/Chromebook "Chromebook") manufactured by Google in 2015\. This page details installing Arch Linux on the Pixel 2.

Also see the forum thread: [[1]](https://bbs.archlinux.org/viewtopic.php?id=194962)

## Contents

*   [1 Enabling developer mode](#Enabling_developer_mode)
*   [2 Installation](#Installation)
    *   [2.1 Grub](#Grub)
    *   [2.2 Dual Booting ChromeOS and Arch Linux](#Dual_Booting_ChromeOS_and_Arch_Linux)
*   [3 Touchpad, touchscreen and audio](#Touchpad.2C_touchscreen_and_audio)
    *   [3.1 Linux 4.1](#Linux_4.1)
    *   [3.2 Linux 3.19](#Linux_3.19)
*   [4 Backlight control](#Backlight_control)
*   [5 Keyboard rebindings](#Keyboard_rebindings)
*   [6 Disabling firmware write protect](#Disabling_firmware_write_protect)
*   [7 External Links](#External_Links)

## Enabling developer mode

Enable developer mode as you would on any Chrome OS Device, hold Esc and F3 (refresh icon) with the device powered off, then press the power button and use Ctrl-D to enable developer mode.

Enabling developer mode will wipe all of your data.

## Installation

**Note:** USB 3.0 may cause issues. Make sure that the installation media utilizes USB 2.0.

See [Chrome OS devices#Installation](/index.php/Chrome_OS_devices#Installation "Chrome OS devices").

##### Grub

It will not display the menu by default. GRUB_GFXMODE is set to auto. Grub does not detect the correct video mode. Using vbeinfo, on the grub command line, it's detected at 1280x850x16\. The options to display the menu are to either turn off GRUB_GFXMODE or set the correct display in `/etc/default/grub`

```
GRUB_TERMINAL_OUTPUT=console

```

or setting

```
GRUB_GFXMODE=1280x850x16

```

after making this change, run

```
grub-mkconfig -o /boot/grub/grub.cfg

```

### Dual Booting ChromeOS and Arch Linux

See [Chrome OS devices#Alternative installation, Install Arch Linux in addition to Chrome OS](/index.php/Chrome_OS_devices#Alternative_installation.2C_Install_Arch_Linux_in_addition_to_Chrome_OS "Chrome OS devices").

## Touchpad, touchscreen and audio

### Linux 4.1

[Install](/index.php/Install "Install") the [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/) package for Linux 4.1 support. You will need to regenerate your GRUB configuration after installing linux-samus4\. See [[2]](https://github.com/raphael/linux-4.1-samus) for information on how to enable audio and microphone support.

If the `linux-samus4` kernel hangs after `Loading initial ramdisk...` and you have an encrypted disk then try adding `i915` to `MODULES` in `/etc/mkinitcpio.conf` according to [Intel graphics](/index.php/Intel_graphics "Intel graphics") and then run `mkinitcpio -p linux-samus4` to regenerate the image.

### Linux 3.19

[Install](/index.php/Install "Install") the [linux-samus](https://aur.archlinux.org/packages/linux-samus/) package. You will need to import 2 kernel signing keys using gpg. Support for the Pixel 2 should be added in Linux 4.1\. You will need to regenerate your GRUB configuration after installing linux-samus.

To fix the touchpad, add the file `/etc/X11/xorg.conf.d/25-touchpad.conf` with the following contents. You will also need to install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

```
Section "InputClass"
    Identifier "touchpad"
    MatchIsTouchpad "on"
    MatchDevicePath "/dev/input/event*"
    Driver "synaptics"
EndSection

```

For audio, see [[3]](https://github.com/tsowell/linux-samus).

## Backlight control

The screen backlight can be controlled via <tt>/sys/class/backlight/intel_backlight/</tt>; see the [brightness](https://raw.githubusercontent.com/raphael/linux-samus/master/build/brightness) script from [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/).

The keyboard backlight can be controlled via <tt>/sys/class/leds/chromeos::kbd_backlight/</tt>; see the [keyboard-brightness.sh](https://gist.githubusercontent.com/strayArch/5c862648f261122d9e4e/raw/d0b800f13b8d792445f32e0317efd57e7f4439a1/keyboard-brightness.sh) script.

## Keyboard rebindings

[xkeyboard-config 2.16-1](https://www.archlinux.org/packages/extra/any/xkeyboard-config/) added a <tt>chromebook</tt> model that enables the Chrome OS style functions for the function keys. You can, for example, set this using <tt>localectl set-x11-keymap us chromebook</tt>. See the <tt>chromebook</tt> definition in <tt>/usr/share/X11/xkb/symbols/inet</tt> for the full mappings.

The search button acts as a `Super_L` key, which may be undesirable for keyboard layouts that make good use of this position. Using [xmodmap](/index.php/Xmodmap "Xmodmap"), you can rebind this to whatever you would like. Example using `Tab` for a keyboard layout with six layers:

```
$ xmodmap -e "keycode 133 = Tab Tab Tab Tab Tab Tab"

```

Add this to your .xinitrc to load at login.

## Disabling firmware write protect

Disabling the firmware write protect is only necessary if you wish to modify the firmware and is not necessary to install Linux.

Power off the Chromebook. Carefully peel off the two adhesive strips on the bottom. They will stretch very easily, so push up from the device while peeling, and don't pull from the end of the adhesive strip. Then remove all the screws under both adhesive strips. The lid should just fall off if you rotate it upside down.

Once the device is open, find the red-pink screw with a golden washer, located between the speaker and the USB Type-A port; remove the screw and washer. Reassemble your Chromebook and power it on.

## External Links

[Chromium OS device page](https://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/chromebook-pixel-2015)