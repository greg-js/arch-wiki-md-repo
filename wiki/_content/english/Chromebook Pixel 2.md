**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

This page details installing Arch Linux on the Google Chromebook Pixel (2015). It is commonly referred to as the Chromebook Pixel 2, sometimes referred to by its codename Samus, and sometimes referred to, somewhat erroneously, as the Chromebook Pixel LS.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 GRUB](#GRUB)
*   [2 Touchpad, touchscreen and audio](#Touchpad.2C_touchscreen_and_audio)
    *   [2.1 (Vanilla) Linux](#.28Vanilla.29_Linux)
    *   [2.2 (Samus) Linux (AUR)](#.28Samus.29_Linux_.28AUR.29)
*   [3 Backlight](#Backlight)
*   [4 Keyboard Bindings](#Keyboard_Bindings)
*   [5 Unresolved Issues](#Unresolved_Issues)
*   [6 See Also](#See_Also)

## Installation

**Note:** USB 3.0 may cause issues. Make sure that the installation media utilizes USB 2.0.

1.  [Enable developer mode](/index.php/Chrome_OS_devices#Enabling_developer_mode "Chrome OS devices").
2.  [Use the superuser shell](/index.php/Chrome_OS_devices#Accessing_the_superuser_shell "Chrome OS devices") in order to [enable SeaBIOS](/index.php/Chrome_OS_devices#Enabling_SeaBIOS "Chrome OS devices"). Don't worry about the **Boot to SeaBIOS by default** section since the Chromebook Pixel (2015) isn't believed to have that issue.\
3.  [Install Arch Linux](/index.php/Chrome_OS_devices#Installing_Arch_Linux "Chrome OS devices") but be aware of additional notes below, e.g. on Grub.

### GRUB

GRUB does not detect the correct video mode and does not display the menu by default. <tt>GRUB_GFXMODE</tt> is set to auto. Using <tt>vbeinfo</tt>, on the grub command line, it's detected at <tt>1280x850x16</tt>. The options to display the menu are to either turn off <tt>GRUB_GFXMODE</tt> or set the correct display. In `/etc/default/grub` either,

```
GRUB_TERMINAL_OUTPUT=console

```

or,

```
GRUB_GFXMODE=1280x850x16

```

and then run

```
grub-mkconfig -o /boot/grub/grub.cfg

```

to update the config.

If you forget to do this you can boot off the installation media again mount your disks and <tt>arch-chroot</tt> in.

## Touchpad, touchscreen and audio

### (Vanilla) Linux

Touchpad, touchscreen, and audio have been working in the vanilla Linux kernel since v4.9.

### (Samus) Linux (AUR)

The [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/) no longer contains a patched kernel, but it comes with a config that is somewhat optimized for the Chromebook Pixel 2015\. [[1]](https://github.com/raphael/linux-samus#linux-for-chromebook-pixel-2015) [Install](/index.php/Install "Install") the package. The installed [boot loader](/index.php/Boot_loader "Boot loader") needs to be configured so that it is possible to boot the [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/) image. See [[2]](https://github.com/raphael/linux-samus) for more information (i.e. audio and microphone configuration).

According to [Intel graphics](/index.php/Intel_graphics "Intel graphics") if the `linux-samus4` kernel has a blank screen during boot, then try adding `i915` to `MODULES` in `/etc/mkinitcpio.conf`. Finally, run `mkinitcpio -p linux-samus4` to regenerate the image.

**Note:**

*   Make sure that `/boot` is mounted when `mkinitcpio -p linux-samus4` is executed, otherwise on reboot the boot partition will be mounted over the new image.

## Backlight

The screen backlight can be controlled via <tt>/sys/class/backlight/intel_backlight/</tt>; see the [brightness](https://raw.githubusercontent.com/raphael/linux-samus/master/build/brightness) script from [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/).

The keyboard backlight can be controlled via <tt>/sys/class/leds/chromeos::kbd_backlight/</tt>; see the [keyboard](https://raw.githubusercontent.com/raphael/linux-samus/master/scripts/setup/brightness/keyboard_led) script from [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/).

## Keyboard Bindings

[xkeyboard-config 2.16-1](https://www.archlinux.org/packages/extra/any/xkeyboard-config/) added a <tt>chromebook</tt> model that enables the Chrome OS style functions for the function keys. You can, for example, set this using <tt>localectl set-x11-keymap us chromebook</tt>. See the <tt>chromebook</tt> definition in <tt>/usr/share/X11/xkb/symbols/inet</tt> for the full mappings.

The search button acts as a `Super_L` key, which may be undesirable for keyboard layouts that make good use of this position. Using [xmodmap](/index.php/Xmodmap "Xmodmap"), you can rebind this to whatever you would like. Example using `Tab` for a keyboard layout with six layers:

```
$ xmodmap -e "keycode 133 = Tab Tab Tab Tab Tab Tab"

```

Add this to your .xinitrc to load at login.

## Unresolved Issues

*   [xkeyboard-config](https://www.archlinux.org/packages/?name=xkeyboard-config) provides a <tt>chromebook</tt> model which can be specified, for example, with <tt>localectl set-x11-keymap us chromebook</tt> but when using [GNOME](/index.php/GNOME "GNOME") on [Wayland](/index.php/Wayland "Wayland") the model is not recognized. The media keys still behave as function keys and <tt>setxkbmap -print -verbose 10</tt> doesn't show the <tt>chromebook</tt> model being used.
*   Occasional lockup on booting into GDM using Wayland 1.12.0-1, GDM 3.22.1-1, and linux 4.9-1.
*   It would be nice if touchscreen behaved more like the touchpad so that the touchscreen could be used for scrolling.
*   Touchpad occasionally doesn't work after waking from sleep using linux 4.9-1+. If this happens, reloading the touchpad driver via <tt>sudo modprobe -r atmel_mxt_ts && sudo modprobe atmel_mxt_ts</tt> usually restores touchpad functionality.

## See Also

*   [Laptop Issues » Google Chromebook Pixel 2](https://bbs.archlinux.org/viewtopic.php?id=194962)
*   [Chromium OS Developer Information for Chromebook Pixel (2015)](https://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/chromebook-pixel-2015)
*   [Install Arch Linux in addition to Chrome OS](/index.php/Chrome_OS_devices#Alternative_installation.2C_Install_Arch_Linux_in_addition_to_Chrome_OS "Chrome OS devices")