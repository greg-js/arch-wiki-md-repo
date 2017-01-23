This page is for those who prefer to limit the verbosity of their system to a strict minimum, either for aesthetics or other reasons. Following this guide will remove all text from the bootup process. [Video demonstration](http://www.youtube.com/watch?v=tuqhsqrhXk0)

## Contents

*   [1 Kernel parameters](#Kernel_parameters)
*   [2 sysctl](#sysctl)
*   [3 startx](#startx)
*   [4 fsck](#fsck)
*   [5 Remove console cursor blinking](#Remove_console_cursor_blinking)

## Kernel parameters

Change the kernel parameters using the configuration options of your boot loader, to include the following parameters:

```
quiet vga=current

```

`vga=current` is the kernel argument that avoid weird behaviours like [FS#32309](https://bugs.archlinux.org/task/32309).

If you are still getting messages printed to the console, it may be dmesg sending you what it thinks are important messages. You can change the level at which these messages will be printed by using `quiet loglevel=<level>`, where `<level>` is any number between 0 and 7, where 0 is the most critical, and 7 is debug levels of printing.

```
quiet loglevel=3 vga=current

```

Note that this only seems to work if both `quiet` and `loglevel=<level>` are both used, and they must be in that order (quiet first). The loglevel parameter will only change that which is printed to the console, the levels of dmesg itself will not be affected and will still be available through the journal as well as the `dmesg` command. For more information, see the `Documentation/kernel-parameters.txt` file of the [linux-docs](https://www.archlinux.org/packages/?name=linux-docs) package.

If you also want to stop systemd from printing its version number when booting, you should also append `udev.log-priority=3` to your kernel commandline ([source](http://www.freedesktop.org/software/systemd/man/systemd-udevd.service.html#Kernel%20command%20line)). If systemd is used in an [initramfs](/index.php/Initramfs "Initramfs"), append `rd.udev.log-priority=3` instead.

If you are using the `systemd` hook in the [initramfs](/index.php/Initramfs "Initramfs"), you may get systemd messages during initramfs initialization. You can pass `rd.systemd.show_status=false` to disable them, or `rd.systemd.show_status=auto` to only suppress successful messages (so in case of errors you can still see them). Actually, `auto` is already passed to `systemd.show_status=auto` when `quiet` is used, however for some motive sometimes systemd inside initramfs does not get it. Below are the parameters that you need to pass to your kernel to get a completely clean boot with systemd in your [initramfs](/index.php/Initramfs "Initramfs"):

```
 quiet loglevel=3 rd.systemd.show_status=auto rd.udev.log-priority=3

```

Also `touch ~/.hushlogin` to remove the Last login message.

## sysctl

To hide any kernel messages from the console, add or modify the `kernel.printk` line according to [[1]](http://unix.stackexchange.com/a/45525/27433):

 `/etc/sysctl.d/20-quiet-printk.conf`  `kernel.printk = 3 3 3 3` 

## startx

To hide `startx` messages, you could redirect its output to `/dev/null`, in your [.bash_profile](https://github.com/kaihendry/Kai-s--HOME/blob/master/.bash_profile) like so:

**Warning:** As of Xorg 1.16 with rootless login, see [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg").

```
$ [[ $(fgconsole 2>/dev/null) == 1 ]] && exec startx -- vt1 &> /dev/null

```

Outstanding Issues:

*   [Systemd shutdowns are not quiet](https://bugs.freedesktop.org/show_bug.cgi?id=57216) - As of systemd v206, the `quiet` kernel command line parameter is now respected on shutdown, though it seems that if you use the `shutdown` hook of [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio), this function has not been set up to support that parameter.

## fsck

To hide fsck messages during boot, let systemd check the root filesystem. For this, remove *fsck* from:

```
HOOKS=(...) 

```

in `/etc/mkinitcpio.conf` and then run:

```
mkinitcpio -p linux

```

Now copy the files `systemd-fsck-root.service` and `systemd-fsck@.service` located at `/usr/lib/systemd/system/` to `/etc/systemd/system/` and edit them, configuring *StandardOutput* and *StandardError* like this:

```
(...)

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/lib/systemd/systemd-fsck
StandardOutput=null
StandardError=journal+console
TimeoutSec=0

```

See [this](http://www.freedesktop.org/software/systemd/man/systemd-fsck@.service.html) for more info on the options you can pass to `systemd-fsck` - you can change how often the service will check (or not) your filesystems.

## Remove console cursor blinking

The console cursor at boot keeps blinking if you follow these intstructions. This can be solved by passing vt.global_cursor_default=0 to the kernel ([source](http://www.friendlyarm.net/forum/topic/2998)).

To recover the cursor in ttys run:

```
# setterm -cursor on >> /etc/issue

```