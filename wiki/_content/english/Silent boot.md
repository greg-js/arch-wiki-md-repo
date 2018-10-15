This page is for those who prefer to limit the verbosity of their system to a strict minimum, either for aesthetics or other reasons. Following this guide will remove all text from the bootup process. [Video demonstration](http://www.youtube.com/watch?v=tuqhsqrhXk0)

## Contents

*   [1 Kernel parameters](#Kernel_parameters)
*   [2 Remove console cursor blinking](#Remove_console_cursor_blinking)
*   [3 sysctl](#sysctl)
*   [4 startx](#startx)
*   [5 fsck](#fsck)
*   [6 Make GRUB silent](#Make_GRUB_silent)
*   [7 Retaining the vendor logo from BIOS](#Retaining_the_vendor_logo_from_BIOS)

## Kernel parameters

Change the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") using the configuration options of your boot loader, to include the following parameters:

```
quiet vga=current

```

`vga=current` is the kernel argument that avoid weird behaviours like [FS#32309](https://bugs.archlinux.org/task/32309).

If you are still getting messages printed to the console, it may be dmesg sending you what it thinks are important messages. You can change the level at which these messages will be printed by using `quiet loglevel=<level>`, where `<level>` is any number between 0 and 7, where 0 is the most critical, and 7 is debug levels of printing.

```
quiet loglevel=3 vga=current

```

Note that this only seems to work if both `quiet` and `loglevel=<level>` are both used, and they must be in that order (quiet first). The loglevel parameter will only change that which is printed to the console, the levels of dmesg itself will not be affected and will still be available through the journal as well as the `dmesg` command. For more information, see the `Documentation/kernel-parameters.txt` file of the [linux-docs](https://www.archlinux.org/packages/?name=linux-docs) package.

If you also want to stop systemd from printing its version number when booting, you should also append `udev.log_priority=3` to your kernel commandline ([source](http://www.freedesktop.org/software/systemd/man/systemd-udevd.service.html#Kernel%20command%20line)). If systemd is used in an [initramfs](/index.php/Initramfs "Initramfs"), append `rd.udev.log_priority=3` instead.

If you are using the `systemd` hook in the [initramfs](/index.php/Initramfs "Initramfs"), you may get systemd messages during initramfs initialization. You can pass `rd.systemd.show_status=false` to disable them, or `rd.systemd.show_status=auto` to only suppress successful messages (so in case of errors you can still see them). Actually, `auto` is already passed to `systemd.show_status=auto` when `quiet` is used, however for some motive sometimes systemd inside initramfs does not get it. Below are the parameters that you need to pass to your kernel to get a completely clean boot with systemd in your [initramfs](/index.php/Initramfs "Initramfs"):

```
 quiet loglevel=3 rd.systemd.show_status=auto rd.udev.log_priority=3

```

Also `touch ~/.hushlogin` to remove the Last login message.

## Remove console cursor blinking

The console cursor at boot keeps blinking if you follow these instructions. This can be solved by passing `vt.global_cursor_default=0` to the kernel [[1]](http://www.friendlyarm.net/forum/topic/2998).

To recover the cursor in the TTY, run:

```
# setterm -cursor on >> /etc/issue

```

## sysctl

To hide any kernel messages from the console, add or modify the `kernel.printk` line according to [[2]](http://unix.stackexchange.com/a/45525/27433):

 `/etc/sysctl.d/20-quiet-printk.conf`  `kernel.printk = 3 3 3 3` 

## startx

To hide `startx` messages, you could redirect its output to `/dev/null`, in your [.bash_profile](https://github.com/kaihendry/Kai-s--HOME/blob/master/.bash_profile) like so:

**Note:** Redirection is broken with rootless login. See [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg").

```
$ [[ $(fgconsole 2>/dev/null) == 1 ]] && exec startx -- vt1 &> /dev/null

```

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

## Make GRUB silent

To hide GRUB welcome and boot messages, you may install unofficial [grub-silent](https://aur.archlinux.org/packages/grub-silent/) package.

After the installation, it is required to reinstall [GRUB](/index.php/GRUB "GRUB") to necessary partition first.

Then, take an example as `/etc/default/grub.silent`, and make necessary changes to `/etc/default/grub`.

Below three lines are necessary:

```
GRUB_DEFAULT=0
GRUB_TIMEOUT=0
GRUB_RECORDFAIL_TIMEOUT=$GRUB_TIMEOUT

```

**Note:** If you set `GRUB_TIMEOUT=0` and `GRUB_HIDDEN_TIMEOUT=1` (or any positive value), set `GRUB_RECORDFAIL_TIMEOUT=$GRUB_HIDDEN_TIMEOUT` instead of `GRUB_RECORDFAIL_TIMEOUT=$GRUB_TIMEOUT`. Otherwise pressing `Esc` on boot to show GRUB menu will not work.

Lastly, regenerate `grub.cfg` file.

## Retaining the vendor logo from BIOS

Modern UEFI systems display a vendor logo on boot until handing over control to the bootloader; e.g. Lenovo laptops display a bright red Lenovo logo. This vendor logo is typically blanked by the bootloader (if standard GRUB is used) or by the kernel.

To prevent the kernel from blanking the vendor logo, Linux 4.19 introduced a new configuration option `FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER` that retains the contents of the framebuffer until text needs to be printed on the framebuffer console. When combined with a low loglevel (to prevent text from being printed), the vendor logo can be retained while the system is initialized.

[Video demonstration](https://www.youtube.com/watch?v=5DW2JgJmsuY)

At the time of writing, Linux 4.19 has not been released yet, so you must [compile the 4.19.0-rc7 (or newer) kernel](/index.php/Kernel#Compilation "Kernel") with `CONFIG_FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER=y`.

The kernel command line should use `loglevel=3` or `rd.udev.log_priority=3` as mentioned above. Note that if you often receive `Core temperature above threshold, cpu clock throttled` messages in the kernel log, you need to use log level 2 to silence these at boot time. Alternatively, if you're compiling the kernel anyway, adjust the log level of the message in `arch/x86/kernel/cpu/mcheck/therm_throt.c`.

If you use [Intel graphics](/index.php/Intel_graphics "Intel graphics"), set `i915.fastboot=1` in the kernel command line to avoid unnecessary modesetting (and screen blanking) on boot.

*Further reading:*

*   [Phoronix: Linux 4.19 Adds Deferred Console Takeover Support For FBDEV - Cleaner Boot Process](https://www.phoronix.com/scan.php?page=news_item&px=Linux-4.19-FBDEV-Defer-Console)
*   [Hans de Goede: Adding deferred fbcon console takeover to the Fedora kernels](https://lists.fedoraproject.org/archives/list/kernel@lists.fedoraproject.org/thread/3MWCKJ2DVJPC4INXPKB4ECFZLA7X5RTI/)