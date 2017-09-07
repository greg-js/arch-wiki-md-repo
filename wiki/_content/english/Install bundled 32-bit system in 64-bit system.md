This article presents one way of running 32-bit applications, which may be of use to those who do not wish to install the lib32-* libraries from the multilib repository and instead prefer to isolate 32bit applications. The approach involves creating a "chroot jail" to handle 32-bit apps.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Settings](#Settings)
*   [2 Configuration](#Configuration)
*   [3 Schroot](#Schroot)
    *   [3.1 Using Schroot to run a 32-bit application](#Using_Schroot_to_run_a_32-bit_application)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Video problems](#Video_problems)
    *   [4.2 Sound in Flash](#Sound_in_Flash)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Java in a chroot](#Java_in_a_chroot)
    *   [5.2 Allow 32-bit applications access to 64-bit PulseAudio](#Allow_32-bit_applications_access_to_64-bit_PulseAudio)
    *   [5.3 Sound in Firefox](#Sound_in_Firefox)
    *   [5.4 Printing](#Printing)

## Installation

[Install](/index.php/Install "Install") the [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) package and create the chroot. Make sure to use a [pacman](/index.php/Pacman "Pacman") configuration that does not use the `[multilib]` repository.

```
# mkdir /opt/arch32
# linux32 pacstrap -C *path/to/pacman.conf* -di /opt/arch32 base base-devel

```

### Settings

Key configuration files should be copied over:

```
# cd /etc
# for i in passwd* shadow* group* sudoers resolv.conf localtime locale.gen vimrc inputrc profile.d/locale.sh; do cp -p /etc/"$i" /opt/arch32/etc/; done

```

Remember to define the correct the number of MAKEFLAGS and other vars in `/opt/arch32/etc/makepkg.conf` before attempting to build.

## Configuration

```
# linux32 arch-chroot /opt/arch32

```

**Note:** If access to the [Xorg](/index.php/Xorg "Xorg") server of the host is required, allow it for a given user with `xhost +si:localuser:*chroot_user*`. See [Xsecurity(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/Xsecurity.7) for details.

It is recommended to use a custom bash prompt inside the 32-bit chroot installation in order to differentiate from the regular system. You can, for example, add a `ARCH32` string to the `PS1` variable defined in `~/.bashrc`.

## Schroot

[Install](/index.php/Install "Install") [schroot](https://www.archlinux.org/packages/?name=schroot) to the native **64-bit** installation:

Edit `/etc/schroot/schroot.conf`, and create an *[Arch32]* section.

```
[Arch32]
type=directory
profile=arch32
description=Arch32
directory=/opt/arch32
users=user1,user2,user3
groups=users
root-groups=root
personality=linux32
aliases=32,default

```

### Using Schroot to run a 32-bit application

The general syntax for calling an application *inside* the chroot is:

```
# schroot -p -- htop

```

In this example, htop is called from within the 32-bit environment.

## Troubleshooting

### Video problems

If you get:

```
X Error of failed request: BadLength (poly request too large or internal Xlib length error)

```

while trying to run an application that requires video acceleration, make sure you have installed appropriate [video drivers](/index.php/Video_drivers "Video drivers") in your chroot.

### Sound in Flash

[Install](/index.php/Install "Install") the [alsa-oss](https://www.archlinux.org/packages/?name=alsa-oss) package inside the chroot, and export the `FIREFOX_DSP` [environment variable](/index.php/Environment_variable "Environment variable") before launching [Firefox](/index.php/Firefox "Firefox"):

```
$ export FIREFOX_DSP="aoss"

```

Every chroot into the 32-bit system requires this environment variable.

For [Wine](/index.php/Wine "Wine") this works the same way. The alsa-oss package will also install the alsa libraries required by [Wine](/index.php/Wine "Wine") to output sound.

## Tips and tricks

### Java in a chroot

See [Java](/index.php/Java "Java"). After installation, adjust the path:

```
$ export PATH="/opt/java/bin/:$PATH"

```

### Allow 32-bit applications access to 64-bit PulseAudio

Additional paths have to be bind-mounted to the chroot environment:

```
# mount --bind /var/run /opt/arch32/var/run
# mount --bind /var/lib/dbus /opt/arch32/var/lib/dbus

```

Unmount them when leaving the environment:

```
# umount /opt/arch32/var/run
# umount /opt/arch32/var/lib/dbus

```

Optionally add the commands to the `/usr/local/bin/arch32` script after the other bind-mount/umount commands. See [PulseAudio from within a chroot](/index.php/PulseAudio/Examples#PulseAudio_from_within_a_chroot_.28e.g._32-bit_chroot_in_64-bit_install.29 "PulseAudio/Examples") for details

### Sound in Firefox

Create `/usr/bin/firefox32` as root:

```
#!/bin/sh
schroot -p firefox $1;export FIREFOX_DSP="aoss"

```

Make it executable:

```
# chmod +x /usr/bin/firefox32

```

### Printing

To access installed CUPS printers from the chroot environment, one needs to bind the `/var/run/cups` directory to the same (relative) location in the chroot environment.

Simply make sure the `/var/run/cups` directory exists in the chroot environment and bind-mount the host `/var/run/cups` to the chroot environment:

```
# mkdir /opt/arch32/var/run/cups
# mount --bind /var/run/cups /opt/arch32/var/run/cups

```

and printers should be available from 32-bit chroot applications immediately.