**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

This page details installing Arch Linux on the Google Chromebook Pixel (2015). It is commonly referred to as the Chromebook Pixel 2, sometimes referred to by its codename Samus, and sometimes called the Chromebook Pixel LS (which stands for "Ludicrous Speed") when referring to the upgraded version with a Intel Core i7.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 GRUB](#GRUB)
*   [2 Linux](#Linux)
    *   [2.1 Suspend](#Suspend)
*   [3 Audio, Brightness, and Touch](#Audio,_Brightness,_and_Touch)
    *   [3.1 Audio scripts fail](#Audio_scripts_fail)
    *   [3.2 Kernel 5.5 Audio Issues](#Kernel_5.5_Audio_Issues)
    *   [3.3 Enable pulseaudio-alsa without scripts](#Enable_pulseaudio-alsa_without_scripts)
*   [4 Keyboard Bindings](#Keyboard_Bindings)
*   [5 Unresolved Issues](#Unresolved_Issues)
*   [6 See Also](#See_Also)

## Installation

1.  [Enable developer mode](/index.php/Chrome_OS_devices#Enabling_developer_mode "Chrome OS devices").
2.  [Use the superuser shell](/index.php/Chrome_OS_devices#Accessing_the_superuser_shell "Chrome OS devices") in order to [enable SeaBIOS](/index.php/Chrome_OS_devices#Enabling_SeaBIOS "Chrome OS devices").
3.  You have the option to [Boot to SeaBIOS by default](/index.php/Chrome_OS_devices#Boot_to_SeaBIOS_by_default "Chrome OS devices") so you can boot without any keyboard shortcuts.
4.  [Install Arch Linux](/index.php/Chrome_OS_devices#Installing_Arch_Linux "Chrome OS devices").
5.  Continue reading below to correctly configure GRUB before rebooting.

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

## Linux

Touchpad, touchscreen, and audio have been working in the vanilla Linux kernel since v4.9, but [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/) comes with a config that is somewhat optimized for the Chromebook Pixel (2015).

### Suspend

Since kernel 5.x suspend seems to not work out-of-the-box anymore and instead shuts down when lid is closed. Install [acpi](https://www.archlinux.org/packages/?name=acpi) and [tpm2-tools](https://www.archlinux.org/packages/?name=tpm2-tools), then create `/etc/modprobe.d/suspend.conf` with

```
options tpm_tis force=1 interrupts=0

```

This should make suspend work on lid close.

## Audio, Brightness, and Touch

The source for [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/) contains some helpful scripts[[1]](https://github.com/raphael/linux-samus/tree/master/scripts/setup) that aren't distributed in the package, but can instead be installed in a derivative package called [samus-scripts](https://aur.archlinux.org/packages/samus-scripts/). These are helpful for managing audio (e.g. switching between speaker and headphone output), setting screen backlight and keyboard LED brightness, and fixing the Atmel maXTouch bug (see [#Unresolved Issues](#Unresolved_Issues)).

### Audio scripts fail

If audio scripts from above don't work, create `/etc/modprobe.d/audio.conf` with

```
options snd_soc_sst_bdw_rt5677_mach index=0 
options snd-hda-intel index=1

```

and make sure to install [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa)

### Kernel 5.5 Audio Issues

After Linux Kernel 5.5, there is an extra kernel options to enable SST audio driver for bdw-rt5677 (Which is initially disabled after 5.5). Add the following switches in the kernel boot parameters to enable audio

```
snd_intel_dspcfg.dsp_driver=2

```

### Enable pulseaudio-alsa without scripts

The hardware and driver mismatch the left and right channel, and it is defaultly muted. Just open alsamixer, and turn on the following switches will make audio works

```
Stereo DAC MIXL DAC1 R
Stereo DAC MIXR DAC1 L

```

This switches will make all audio works, and enable the autoswitch to headphone when connected. (If no other scripts make the audio works, linux-samus's sripts will make the autoswitch failed)

## Keyboard Bindings

[xkeyboard-config 2.16-1](https://www.archlinux.org/packages/extra/any/xkeyboard-config/) added a <tt>chromebook</tt> model that enables the Chrome OS style functions for the function keys. You can, for example, set this using <tt>localectl set-x11-keymap us chromebook</tt>. See the <tt>chromebook</tt> definition in <tt>/usr/share/X11/xkb/symbols/inet</tt> for the full mappings.

The search button acts as a `Super_L` key, which may be undesirable for keyboard layouts that make good use of this position. Using [xmodmap](/index.php/Xmodmap "Xmodmap"), you can rebind this to whatever you would like. Example using `Tab` for a keyboard layout with six layers:

```
$ xmodmap -e "keycode 133 = Tab Tab Tab Tab Tab Tab"

```

Add this to your .xinitrc to load at login.

## Unresolved Issues

*   [xkeyboard-config](https://www.archlinux.org/packages/?name=xkeyboard-config) provides a <tt>chromebook</tt> model which can be specified, for example, with <tt>localectl set-x11-keymap us chromebook</tt> but when using [GNOME](/index.php/GNOME "GNOME") on [Wayland](/index.php/Wayland "Wayland") the model is not recognized. The media keys still behave as function keys and <tt>setxkbmap -print -verbose 10</tt> doesn't show the <tt>chromebook</tt> model being used.
*   Touchpad occasionally doesn't work after waking from sleep using linux 4.9-1+. If this happens, reloading the touchpad driver via <tt>sudo modprobe -r atmel_mxt_ts && sudo modprobe atmel_mxt_ts</tt> usually restores touchpad functionality. This fix is also available as <tt>enable-touch</tt> from [samus-scripts](https://aur.archlinux.org/packages/samus-scripts/).

## See Also

*   [Laptop Issues » Google Chromebook Pixel 2](https://bbs.archlinux.org/viewtopic.php?id=194962)
*   [Chromium OS Developer Information for Chromebook Pixel (2015)](https://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/chromebook-pixel-2015)
*   [Install Arch Linux in addition to Chrome OS](/index.php/Chrome_OS_devices#Alternative_installation,_Install_Arch_Linux_in_addition_to_Chrome_OS "Chrome OS devices")
*   [tpm bug: systemctl suspend turns off computer](https://bbs.archlinux.org/viewtopic.php?id=246716)