## Contents

*   [1 Introduction](#Introduction)
*   [2 Globally](#Globally)
*   [3 Locally](#Locally)
    *   [3.1 Console](#Console)
    *   [3.2 ALSA](#ALSA)
    *   [3.3 Xorg](#Xorg)
    *   [3.4 GNOME](#GNOME)
    *   [3.5 Cinnamon](#Cinnamon)
    *   [3.6 GTK+](#GTK.2B)
*   [4 Beep](#Beep)
    *   [4.1 Installation](#Installation)
    *   [4.2 Access for non-root users](#Access_for_non-root_users)
    *   [4.3 Tips and Tricks](#Tips_and_Tricks)
*   [5 See also](#See_also)

## Introduction

The computer often seems to make beep noises or other sounds at various times, whether we want them or not. They come from various sources, and as such, you may be able to configure if or when they occur. In situations where no sound card or speakers are available and simple audio notification is desired, use [beep](https://www.archlinux.org/packages/?name=beep). The [beep](https://www.archlinux.org/packages/?name=beep) package provides an advanced PC speaker beeping program.

Sounds from the computer can be heard from the built-in case speaker, the speakers, or headphones which are plugged into the sound card (in which case the noise may be unexpectedly loud). Turning off a particular instance of a sound, while leaving the others operational, is possible if and only if one can identify which portion of the environment generates the particular sound. This allows for a customized selection of attention-getting sounds possible. Please feel free to add any configurations and settings to this wiki page that may be useful for other users.

**Note:** The sounds are caused by the BIOS (Basic Input/Output System), the OS (Operating System), the DE (Desktop Environment), or various software programs. The BIOS is a particularly troublesome problem because it is kept inside an EPROM chip on the motherboard, and the only direct control the user has is by turning the power on or off. Unless the BIOS setup has a setting you can adjust or you wish to attempt to reprogram that chip with the proper light source, it is not likely you will be able to change it at all. BIOS-generated beep sounds are not addressed here, except to say that unplugging your computer case speaker will stop all such sounds from being heard. (Do so at your own risk.)

## Globally

The PC speaker can be disabled by [unloading](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") the `pcspkr` module, which is provided by the [linux](https://www.archlinux.org/packages/?name=linux) kernel:

```
# rmmod pcspkr

```

[Blacklisting](/index.php/Blacklisting "Blacklisting") the `pcspkr` module will prevent [udev](/index.php/Udev "Udev") from loading it at boot:

```
# echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf

```

[Blacklisting it on the kernel command line](/index.php/Kernel_modules#Using_kernel_command_line_2 "Kernel modules") is yet another way. Simply add `modprobe.blacklist=pcspkr` to your bootloader's kernel line.

## Locally

### Console

You can add this command in `/etc/profile` or a dedicated file like `/etc/profile.d/disable-beep.sh` (must be executable):

```
setterm -blength 0

```

Another way is to add or uncomment this line in `/etc/inputrc` or `~/.inputrc`:

```
set bell-style none

```

### ALSA

**Tip:** For most Intel's cards, if you do not see a channel named PC Speaker or Beep in alsamixer's default device, then try selecting the correct card by pressing F6 (e.g. "HDA Intel PCH"). It is listed as "Beep" there. This is because PulseAudio proxy controls may not list all PC Speakers.

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

The channel can also be unmuted by using the `↑` key to increase the volume of the channel.

Press `Esc` to close alsamixer.

To persist the current ALSA Mixer state, save the settings:

```
# alsactl -f /var/lib/alsa/asound.state store

```

**Note:** Not every sound card creates a PC Speaker or PC Beep slider control in alsamixer.

### Xorg

```
$ xset -b

```

You can add this command to a startup file, such as [xprofile](/index.php/Xprofile "Xprofile") to make it permanent.

### GNOME

Using GSettings:

```
$ gsettings set org.gnome.desktop.wm.preferences audible-bell false

```

### Cinnamon

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

## Beep

### Installation

[Install](/index.php/Install "Install") the [beep](https://www.archlinux.org/packages/?name=beep) package.

### Access for non-root users

By default `beep` will fail if not run by the root. Other users may call it using [sudo](/index.php/Sudo "Sudo"). To let group `users` call `sudo beep` without a password (for example to use it in scripts), `/etc/sudoers` [should be edited](/index.php/Sudo#Using_visudo "Sudo"):

```
%users ALL=(ALL) NOPASSWD: /usr/bin/beep

```

or, to let only a single user do that:

```
username ALL=(ALL) NOPASSWD: /usr/bin/beep

```

Another way is setting the sticky bit on `/usr/bin/beep`:

```
# chmod 4755 /usr/bin/beep

```

Note however that this way **anyone** can execute `/usr/bin/beep` with root permissions. The change also creates a difference between local copy and the package, which will be reported by `pacman -Qkk`.

### Tips and Tricks

While many people are happy with the traditional beep sound, some may like to change its properties a bit. The following example plays slighly higher and shorter sound and repeats it two times.

```
# beep -f 5000 -l 50 -r 2

```

## See also

*   Have a look at these `man` pages for further information: `xset(1)`, `setterm(1)`, `readline(3)`.
*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture")