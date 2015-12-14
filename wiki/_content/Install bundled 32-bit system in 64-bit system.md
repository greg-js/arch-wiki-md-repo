# Install bundled 32-bit system in 64-bit system

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article presents one way of running 32-bit applications, which may be of use to those who do not wish to install the lib32-* libraries from the multilib repository and instead prefer to isolate 32bit applications. The approach involves creating a "chroot jail" to handle 32-bit apps.

**Tip:** Xyne has created a package that installs a minimalist 32-bit chroot as described below. See [[1]](https://bbs.archlinux.org/viewtopic.php?id=97629) and [[2]](http://xyne.archlinux.ca/projects/arch32-light) for details.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Settings](#Settings)
    *   [1.2 Daemon and systemd service](#Daemon_and_systemd_service)
*   [2 Configuration](#Configuration)
    *   [2.1 First-time Setup](#First-time_Setup)
*   [3 Schroot](#Schroot)
    *   [3.1 Using Schroot to run a 32-bit application](#Using_Schroot_to_run_a_32-bit_application)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Compilation and installing](#Compilation_and_installing)
    *   [4.2 Video problems](#Video_problems)
    *   [4.3 Sound in Flash](#Sound_in_Flash)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Java in a chroot](#Java_in_a_chroot)
    *   [5.2 Allow 32-bit applications access to 64-bit PulseAudio](#Allow_32-bit_applications_access_to_64-bit_PulseAudio)
    *   [5.3 Sound in Firefox](#Sound_in_Firefox)
    *   [5.4 3D acceleration](#3D_acceleration)
    *   [5.5 WINE](#WINE)
    *   [5.6 Printing](#Printing)

## Installation

1\. Create the directory:

```
# mkdir /opt/arch32

```

2\. Generate temporary [pacman](/index.php/Pacman "Pacman") configuration files for chroot:

```
# sed -e 's/\$arch/i686/g' /etc/pacman.d/mirrorlist > /opt/arch32/mirrorlist
# sed -e 's@/etc/pacman.d/mirrorlist@/opt/arch32/mirrorlist@g' -e '/Architecture/ s,auto,i686,'  /etc/pacman.conf > /opt/arch32/pacman.conf

```

*   These files would conflict with the normal pacman files, which will be installed in the later steps.
*   For this reason they must be put _into_ a temporary location (`/opt/arch32` is used here).
*   Remember to delete/comment the multilib repo, if you have enabled it, in the `/opt/arch32/pacman.conf` file

3\. Create the directory:

```
# mkdir -p /opt/arch32/var/{cache/pacman/pkg,lib/pacman}

```

4\. Sync pacman:

```
# pacman --root /opt/arch32 --cachedir /opt/arch32/var/cache/pacman/pkg --config /opt/arch32/pacman.conf -Sy

```

5\. Install the base and optionally base-devel groups:

```
# pacman --root /opt/arch32 --cachedir /opt/arch32/var/cache/pacman/pkg --config /opt/arch32/pacman.conf -S base base-devel

```

Optionally add your favorite text editor and distcc if you plan to compile within the chroot with other machines:

```
# pacman --root /opt/arch32 --cachedir /opt/arch32/var/cache/pacman/pkg --config /opt/arch32/pacman.conf -S base base-devel sudo vim distcc

```

Optionally move the pacman mirror list into place:

```
# mv /opt/arch32/mirrorlist /opt/arch32/etc/pacman.d

```

### Settings

Key configuration files should be copied over:

```
# for i in passwd* shadow* group* sudoers resolv.conf localtime locale.gen vimrc mtab inputrc profile.d/locale.sh; do cp -p /etc/"$i" /opt/arch32/etc/; done

```

Remember to define the correct the number of MAKEFLAGS and other vars in `/opt/arch32/etc/makepkg.conf` before attempting to build.

### Daemon and systemd service

 `/etc/systemd/system/arch32.service` 

```
[Unit]
Description=32-bit chroot

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/local/bin/arch32 start
ExecStop=/usr/local/bin/arch32 stop

[Install]
WantedBy=multi-user.target

```

 `/usr/local/bin/arch32` 

```
#!/bin/bash

## User variables.
MOUNTPOINT=/opt/arch32

## Set MANAGEPARTITION to any value if /opt/arch32 resides on a separate
## partition and not mounted by /etc/fstab or some other means.
## If /opt/arch32 is part of your rootfs, leave this empty.
MANAGEPARTITION=

## Leave USEDISTCC empty unless you wish to use distccd from within the chroot.
USEDISTCC=
DISTCC_SUBNET='10.9.8.0/24'

## PIDFILE shouldn't need to ba changed from this default.
PIDFILE=/run/arch32

start_distccd() {
	[[ ! -L "$MOUNTPOINT"/usr/bin/distccd-chroot ]] &&
		ln -s /usr/bin/distccd "$MOUNTPOINT"/usr/bin/distccd-chroot 
	DISTCC_ARGS="--user nobody --allow $DISTCC_SUBNET --port 3692 --log-level warning --log-file /tmp/distccd-i686.log"

	[[ -z "$(pgrep distccd-chroot)" ]] &&
		linux32 chroot "$MOUNTPOINT" /bin/bash -c "/usr/bin/distccd-chroot --daemon $DISTCC_ARGS"
}

stop_distccd() {
	[[ -n "$(pgrep distccd-chroot)" ]] &&
		linux32 chroot "$MOUNTPOINT" /bin/bash -c "pkill -SIGTERM distccd-chroot"
}

case $1 in
	start)
		[[ -f "$PIDFILE" ]] && exit 1

		if [[ -n "$MANAGEPARTITION" ]]; then
			mountpoint -q $MOUNTPOINT || mount LABEL="arch32" $MOUNTPOINT
		fi

		dirs=(/tmp /dev /dev/pts /home)
		for d in "${dirs[@]}"; do
			mount -o bind $d "$MOUNTPOINT"$d
		done

		mount -t proc none "$MOUNTPOINT/proc"
		mount -t sysfs none "$MOUNTPOINT/sys"
		touch "$PIDFILE"
		[[ -n "$USEDISTCC" ]] && start_distccd
		;;

	stop)
		[[ ! -f "$PIDFILE" ]] && exit 1
		[[ -n "$USEDISTCC" ]] && stop_distccd

		if [[ -n "$MANAGEPARTITION" ]]; then
			umount -R -A -l "$MOUNTPOINT"
		else
			dirs=(/home /dev/pts /dev /tmp)
			[[ -n "$USEDISTCC" ]] && stop_distccd
			umount "$MOUNTPOINT"/{sys,proc}
			for d in "${dirs[@]}"; do
				umount -l "$MOUNTPOINT$d"
			done
		fi

		rm -f "$PIDFILE"
		;;
	*)
		echo "usage: $0 (start|stop)"
		exit 1
esac

```

Be sure to make the init script executable:

```
# chmod +x /usr/local/bin/arch32

```

[Start](/index.php/Start "Start") and optionally [enable](/index.php/Enable "Enable") `arch32.service`.

## Configuration

Chroot into the new system:

```
# /usr/local/bin/arch32 start
$ xhost +SI:localuser:username_to_give_access_to
# chroot /opt/arch32

```

It is recommended to use a custom bash prompt inside the 32-bit chroot installation in order to differentiate from the regular system. You can, for example, add a _ARCH32_ string to the _PS1_ variable defined in `~/.bashrc`. In fact, the default Debian .bashrc prompt string contains appropriate logic to report whether the working directory is within a chroot.

### First-time Setup

Fix possible locale problems:

```
# /usr/bin/locale-gen

```

Initialize pacman:

```
# sed -i 's/CheckSpace/#CheckSpace/' /etc/pacman.conf
# pacman-key --init && pacman-key --populate archlinux

```

## Schroot

[Install](/index.php/Install "Install") [schroot](https://www.archlinux.org/packages/?name=schroot) to the native **64-bit** installation:

Edit `/etc/schroot/schroot.conf`, and create an _[Arch32]_ section.

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

Optionally edit `/etc/schroot/arch32/mount` to match the mounts created within `/usr/local/bin/arch32`.

### Using Schroot to run a 32-bit application

The general syntax for calling an application _inside_ the chroot is:

```
# schroot -p -- htop

```

In this example, htop is called from within the 32-bit environment.

## Troubleshooting

### Compilation and installing

Ensure the desired options are set in the local `/etc/makepkg.conf`.

Some packages may require a `--host` flag be added to the ./configure script in the PKBUILD:

```
$ ./configure --host="i686-pc-linux" ...

```

This is the case when the build makes use of values (for example, the output of the `uname` command) inherited from your base system.

### Video problems

If you get:

```
X Error of failed request: BadLength (poly request too large or internal Xlib length error)

```

while trying to run an application that requires video acceleration, make sure you have installed appropriate [video drivers](/index.php/Video_drivers "Video drivers") in your chroot.

### Sound in Flash

To get sound from the flash player in Firefox, open a terminal and chroot inside the 32-bit system:

```
# chroot /opt/arch32

```

From there, install [alsa-oss](https://www.archlinux.org/packages/?name=alsa-oss) as usual with [pacman](/index.php/Pacman "Pacman").

Then type:

```
$ export FIREFOX_DSP="aoss"

```

Every chroot into the 32-bit system will require this export command to be entered so it may be best to incorporate it into a script.

Finally, launch Firefox.

For [Wine](/index.php/Wine "Wine") this works the same way. The package alsa-oss will also install the alsa libs required by [Wine](/index.php/Wine "Wine") to output sound.

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

Now you can make an alias for Firefox, if desired:

```
alias firefox="firefox32"

```

Add this to `~/.bashrc` and source it to enable it. Or you can just change all your desktop environment's launchers to firefox32 if you still want 64-bit Firefox to be available.

### 3D acceleration

You need to install the corresponding package under your "native" arch for 3D support.

For information on how to set up your graphic adapter refer to:

*   [ATI](/index.php/ATI "ATI")
*   [Intel](/index.php/Intel "Intel")
*   [NVIDIA](/index.php/NVIDIA "NVIDIA")

### WINE

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** The _wine-hacks_ package does not exist anymore. (Discuss in [Talk:Install bundled 32-bit system in 64-bit system#](https://wiki.archlinux.org/index.php/Talk:Install_bundled_32-bit_system_in_64-bit_system))

In order to compile wine, you need a 32-bit system installed. Compiling wine is needed for applying patches in order to get [PulseAudio](http://art.ified.ca/?page_id=40) working. See also [wine-hacks](https://aur.archlinux.org/packages.php?ID=19675) from AUR.

Add the following alias to `~/.bashrc`:

```
alias wine='schroot -pqd "$(pwd)" -- wine'

```

The `-q` switch makes schroot operate in quiet mode, so it works like "regular" wine does. Also note that If you still use dchroot instead of schroot, you should use switch `-d` instead of `-s`.

### Printing

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** The note below contains a link to this very page, making it very unclear. (Discuss in [Talk:Install bundled 32-bit system in 64-bit system#](https://wiki.archlinux.org/index.php/Talk:Install_bundled_32-bit_system_in_64-bit_system))

**Note:** If you have a 64-bit base installation with a [32-bit chroot environment](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64"), explicit installation of CUPS is not necessary in the 32-bit environment.

To access installed CUPS printers from the chroot environment, one needs to bind the `/var/run/cups` directory to the same (relative) location in the chroot environment.

Simply make sure the `/var/run/cups` directory exists in the chroot environment and bind-mount the host `/var/run/cups` to the chroot environment:

```
# mkdir _chroot32-dir/var/run/cups_
# mount --bind /var/run/cups _chroot32-dir/var/run/cups_

```

and printers should be available from 32-bit chroot applications immediately.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Install_bundled_32-bit_system_in_64-bit_system&oldid=412104](https://wiki.archlinux.org/index.php?title=Install_bundled_32-bit_system_in_64-bit_system&oldid=412104)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")