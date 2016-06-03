## Contents

*   [1 Introduction](#Introduction)
*   [2 Globally](#Globally)
*   [3 Locally](#Locally)
    *   [3.1 In X](#In_X)
    *   [3.2 In console](#In_console)
    *   [3.3 Using ALSA](#Using_ALSA)
    *   [3.4 In GNOME](#In_GNOME)
    *   [3.5 In Cinnamon](#In_Cinnamon)
    *   [3.6 GTK+](#GTK.2B)
*   [4 See also](#See_also)

## Introduction

The computer often seems to make beep noises or other sounds at various times, whether we want them or not. They come from various sources, and as such, you may be able to configure if or when they occur.

Further, the sounds from the computer can be heard from the built-in case speaker, or the speakers or headphones which are plugged into the sound card (in which case the noise may be unexpectedly loud). This article deals primarily with the former.

The sounds are caused by the BIOS (Basic Input/Output System), the OS (Operating System), the DE (Desktop Environment), or various software programs. The BIOS is a particularly troublesome problem because it is kept inside an EPROM chip on the motherboard, and the only direct control the user has is by turning the power on or off. Unless the BIOS setup has a setting you can adjust or you wish to attempt to reprogram that chip with the proper light source, it is not likely you will be able to change it at all. BIOS-generated beep sounds are not addressed here, except to say that unplugging your computer case speaker will stop all such sounds from being heard. (Do so at your own risk.)

However, everything else which can cause a sound to come out of the computer case speaker can be handled with the suggestions listed below.

One should also note that the option of turning off a particular instance of a sound, while leaving the others operational, is possible if one can identify which portion of the environment is the source of the particular sound generation. This can make a very customized selection of attention-getting sounds possible. Please feel free to add your findings to this wiki page when you find particular examples of settings combinations which may be useful for other users.

## Globally

The PC speaker can be disabled by [unloading](/index.php/Kernel_modules#Removal "Kernel modules") the `pcspkr` module:

```
# rmmod pcspkr

```

[Blacklisting](/index.php/Blacklisting "Blacklisting") the `pcspkr` module will prevent [udev](/index.php/Udev "Udev") from loading it at boot:

```
# echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf

```

[Blacklisting it on the kernel command line](/index.php/Kernel_modules#Using_kernel_command_line_2 "Kernel modules") is yet another way. Simply add `modprobe.blacklist=pcspkr` to your bootloader's kernel line.

## Locally

### In X

```
$ xset -b

```

You can add this command to a startup file, such as [xprofile](/index.php/Xprofile "Xprofile") to make it permanent.

### In console

You can add this command in `/etc/profile` or a dedicated file like `/etc/profile.d/disable-beep.sh` (must be executable):

```
setterm -blength 0

```

Another way is to add or uncomment this line in `/etc/inputrc` or `~/.inputrc`:

```
set bell-style none

```

### Using ALSA

**Tip:** For most Intel's cards, if you do not see PC Speaker in alsamixer's default device, then try selecting "HDA Intel PCH" device by pressing F6\. It is listed as "Beep" there. This is because PulseAudio proxy controls may not list all PC Speakers.

Try muting the PC Speaker:

```
$ amixer set 'PC Speaker' 0% mute

```

For certain sound cards, it is the PC Beep:

```
$ amixer set 'PC Beep' 0% mute

```

Or merely Beep:

```
$ amixer set 'Beep' 0% mute

```

You can also use alsamixer for a console GUI

```
$ alsamixer

```

Scroll to PC beep and press 'M' to mute. Save your alsa settings:

```
# alsactl store

```

**Note:** Not every sound card creates a PC Speaker or PC Beep slider control in alsamixer.

### In GNOME

Using GSettings:

```
$ gsettings set org.gnome.desktop.wm.preferences audible-bell false

```

### In Cinnamon

Cinnamon seems to play a "water drop" sound. To disable it, set in dconf:

```
$ dconf write /org/cinnamon/desktop/wm/preferences/audible-bell false

```

### GTK+

Append this line to `~/.gtkrc-2.0`:

```
gtk-error-bell = 0

```

Add the same line to the [Settings] section of `$XDG_CONFIG_HOME/gtk-3.0/settings.ini`:

```
[Settings]
gtk-error-bell = 0

```

This is documented in the [Gnome Developer Handbook](https://developer.gnome.org/gtk3/stable/GtkSettings.html).

## See also

*   Have a look at these `man` pages for further information: `xset(1)`, `setterm(1)`, `readline(3)`.
*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")