This article explains some methods for general troubleshooting. For application specific issues, please reference the particular wiki page for that program.

## Contents

*   [1 General procedures](#General_procedures)
    *   [1.1 Attention to detail](#Attention_to_detail)
    *   [1.2 Questions/checklist](#Questions.2Fchecklist)
    *   [1.3 Be more specific](#Be_more_specific)
    *   [1.4 Additional support](#Additional_support)
*   [2 Boot problems](#Boot_problems)
    *   [2.1 Console messages](#Console_messages)
        *   [2.1.1 Flow control](#Flow_control)
        *   [2.1.2 Scrollback](#Scrollback)
        *   [2.1.3 Debug output](#Debug_output)
    *   [2.2 Recovery shells](#Recovery_shells)
    *   [2.3 Blank screen with Intel video](#Blank_screen_with_Intel_video)
    *   [2.4 Stuck while loading the kernel](#Stuck_while_loading_the_kernel)
    *   [2.5 Debugging kernel modules](#Debugging_kernel_modules)
    *   [2.6 Debugging hardware](#Debugging_hardware)
    *   [2.7 See also](#See_also)
*   [3 Package management](#Package_management)
*   [4 fuser](#fuser)
*   [5 Session permissions](#Session_permissions)
*   [6 error while loading shared libraries](#error_while_loading_shared_libraries)
*   [7 file: could not find any magic files!](#file:_could_not_find_any_magic_files.21)
*   [8 See also](#See_also_2)

## General procedures

### Attention to detail

In order to resolve an issue that you are having, it is *absolutely crucial* to have a firm basic understanding of how that specific subsystem functions. How does it work, and what does it need to run without error? If you cannot comfortably answer these question then you would best review the [Archwiki](/index.php/Table_of_contents "Table of contents") article for the subsystem that you are having trouble with. Once you feel like you've understood it, it will be easier for you to pinpoint the cause of the problem.

### Questions/checklist

The following gives a number of questions for you whenever dealing with a malfunctioning system. Under each question there are notes explaining how you should be answering each question, followed by some light examples on how to easily gather data output and what tools can be used to review logs and the journal.

1.  What is the issue(s)?

    	Be *as precise as possible*. This will help you not get confused and/or side-tracked when looking up specific information.

2.  Are there error messages? (if any)

    	Copy and paste *full outputs* that contain **error messages** related to your issue into a separate file, such as `$HOME/issue.log`. For example, to forward the output of the following [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") command to `$HOME/issue.log`:

    	 `$ mkinitcpio -p linux >> $HOME/issue.log` 

3.  Can you reproduce the issue?

    	If so, give *exact* **step-by-step** instructions/commands needed to do so.

4.  When did you first encounter these issues and what was changed between then and when the system was operating without error?

    	If it occurred right after an update then, list **all packages that were updated**. Include *version numbers*, also, paste the entire update from [pacman](/index.php/Pacman "Pacman").log (`/var/log/pacman.log`). Also take note of the statuses of *any* service(s) needed to support the malfunctioning application(s) using [systemd](/index.php/Systemd "Systemd")'s systemctl tools. For example, to forward the output of the following [systemd](/index.php/Systemd#Basic_systemctl_usage "Systemd") command to `$HOME/issue.log`:

    	 `$ systemctl status dhcpcd@eth0.service >> $HOME/issue.log` 

    **Note:** Using `**>>**` will ensure any previous text in `$HOME/issue.log` will not be overwritten.

### Be more specific

When attempting to resolve an issue, **never** approach it as:

*Application X does not work.*

Instead, look at it in its entirety:

*Application X produces Y error(s) when performing Z tasks under conditions A and B.*

### Additional support

With all the information in front of you you should have a good idea as to what is going on with the system and you can now start working on a proper fix.

If you require any additional support, it can be found on [the forums](https://bbs.archlinux.org) or IRC at irc.freenode.net #archlinux See [IRC channels](/index.php/IRC_channels "IRC channels") for other options.

When asking for support post the **complete** output/logs, not just what you think are the significant sections. Sources of information include:

*   Full output of any command involved - don't just select what you think is relevant.
*   Output from systemd's `journalctl`. For more extensive output, use the `systemd.log_level=debug` boot parameter.
*   Log files (have a look in `/var/log`)
*   Relevant configuration files
*   Drivers involved
*   Versions of packages involved
*   Kernel: `dmesg`. For a boot problem, at least the last 10 lines displayed, preferably more
*   Networking: Exact output of commands involved, and any configuration files
*   Xorg: `/var/log/Xorg.0.log`, and prior logs if you have overwritten the problematic one
*   Pacman: If a recent upgrade broke something, look in `/var/log/pacman.log`

One of the better ways to post this information is to use an online pastebin. You can [install](/index.php/Install "Install") the [pbpst](https://www.archlinux.org/packages/?name=pbpst) or [gist](https://www.archlinux.org/packages/?name=gist) package to automatically upload information. For example, to upload the content of your systemd journal from this boot you would do:

```
# journalctl -xb | pbpst -S

```

A link will then be output that you can paste to the forum or IRC.

Additionally, before posting your question, you may wish to review [how to ask smart questions](http://www.catb.org/esr/faqs/smart-questions.html). See also [Code of conduct](/index.php/Code_of_conduct "Code of conduct").

## Boot problems

Diagnosing errors during the [boot process](/index.php/Boot_process "Boot process") involves changing the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), and rebooting the system.

If booting the system is not possible, boot from a [live image](https://www.archlinux.org/download/) and [change root](/index.php/Change_root "Change root") to the existing system.

### Console messages

After the boot process, the screen is cleared and the login prompt appears, leaving users unable to read init output and error messages. This default behavior may be modified using methods outlined in the sections below.

Note that regardless of the chosen option, kernel messages can be displayed for inspection after booting by using `dmesg` or all logs from the current boot with `journalctl -b`.

#### Flow control

This is basic management that applies to most terminal emulators, including virtual consoles (vc):

*   Press `Ctrl+S` to pause the output
*   And `Ctrl+Q` to resume it

This pauses not only the output, but also programs which try to print to the terminal, as they will block on the `write()` calls for as long as the output is paused. If your *init* appears frozen, make sure the system console is not paused.

To see error messages which are already displayed, see [Getty#Have boot messages stay on tty1](/index.php/Getty#Have_boot_messages_stay_on_tty1 "Getty").

#### Scrollback

Scrollback allows the user to go back and view text which has scrolled off the screen of a text console. This is made possible by a buffer created between the video adapter and the display device called the scrollback buffer. By default, the key combinations of `Shift+PageUp` and `Shift+PageDown` scroll the buffer up and down.

If scrolling up all the way does not show you enough information, you need to expand your scrollback buffer to hold more output. This is done by tweaking the kernel's framebuffer console (fbcon) with the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `fbcon=scrollback:Nk` where `N` is the desired buffer size is kilobytes. The default size is 32k.

If this does not work, your framebuffer console may not be properly enabled. Check the [Framebuffer Console documentation](https://www.kernel.org/doc/Documentation/fb/fbcon.txt) for other parameters, e.g. for changing the framebuffer driver.

#### Debug output

Most kernel messages are hidden during boot. You can see more of these messages by adding different kernel parameters. The simplest ones are:

*   `debug` enables debug messages for both the kernel and [systemd](/index.php/Systemd "Systemd")
*   `ignore_loglevel` forces *all* kernel messages to be printed

Other parameters you can add that might be useful in certain situations are:

*   `earlyprintk=vga,keep` prints kernel messages very early in the boot process, in case the kernel would crash before output is shown. You must change `vga` to `efi` for [EFI](/index.php/EFI "EFI") systems
*   `log_buf_len=16M` allocates a larger (16MB) kernel message buffer, to ensure that debug output is not overwritten

There are also a number of separate debug parameters for enabling debugging in specific subsystems e.g. `bootmem_debug`, `sched_debug`. Check the [kernel parameter documentation](https://www.kernel.org/doc/Documentation/kernel-parameters.txt) for specific information.

**Note:** If you cannot scroll back far enough to view the desired boot output, you should increase the size of the [scrollback buffer](#Scrollback).

### Recovery shells

Getting an interactive shell at some stage in the boot process can help you pinpoint exactly where and why something is failing. There are several kernel parameters for doing so, but they all launch a normal shell which you can `exit` to let the kernel resume what it was doing:

*   `rescue` launches a shell shortly after the root filesystem is remounted read/write
*   `emergency` launches a shell even earlier, before most filesystems are mounted
*   `init=/bin/sh` (as a last resort) changes the init program to a root shell. `rescue` and `emergency` both rely on [systemd](/index.php/Systemd "Systemd"), but this should work even if *systemd* is broken

Another option is systemd's debug-shell which adds a root shell on `tty9` (accessible with Ctrl+Alt+F9). It can be enabled by either adding `systemd.debug-shell` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), or by [enabling](/index.php/Enabling "Enabling") `debug-shell.service`. Take care to disable the service when done to avoid the security risk of leaving a root shell open on every boot.

### Blank screen with Intel video

This is most likely due to a problem with [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Try [disabling modesetting](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting") or changing the [video port](/index.php/Intel#KMS_Issue:_console_is_limited_to_small_area "Intel").

### Stuck while loading the kernel

Try disabling ACPI by adding the `acpi=off` kernel parameter.

### Debugging kernel modules

See [Kernel modules#Obtaining information](/index.php/Kernel_modules#Obtaining_information "Kernel modules").

### Debugging hardware

See [udev#Debug output](/index.php/Udev#Debug_output "Udev").

### See also

*   [Memtest86+](http://www.memtest.org/)
*   [List of Tools for UBCD](http://wiki.ultimatebootcd.com/index.php?title=Tools) - Can be added to custom menu.lst like memtest
*   Wikipedia's page on [BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [QA/Sysrq](https://fedoraproject.org/wiki/QA/Sysrq) - Using sysrq
*   systemd documentation: [Debug Logging to a Serial Console](http://freedesktop.org/wiki/Software/systemd/Debugging#Debug_Logging_to_a_Serial_Console)
*   [How to Isolate Linux ACPI Issues](https://web.archive.org/web/20120217124742/http://www.lesswatts.org/projects/acpi/debug.php)

## Package management

See [Pacman#Troubleshooting](/index.php/Pacman#Troubleshooting "Pacman") for general topics, and [pacman/Package signing#Troubleshooting](/index.php/Pacman/Package_signing#Troubleshooting "Pacman/Package signing") for issues with PGP keys.

## fuser

*fuser* is a command-line utility for identifying processes using resources such as files, filesystems and TCP/UDP ports.

*fuser* is provided by the [psmisc](https://www.archlinux.org/packages/?name=psmisc) package, which should be already installed as part of the [base](https://www.archlinux.org/groups/x86_64/base/) group.

## Session permissions

**Note:** You must be using [systemd](/index.php/Systemd "Systemd") as your init system for local sessions to work.[[1]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) It is required for polkit permissions and ACLs for various devices (see `/usr/lib/udev/rules.d/70-uaccess.rules` and [[2]](http://enotty.pipebreaker.pl/2012/05/23/linux-automatic-user-acl-management/))

First, make sure you have a valid local session within X:

```
$ loginctl show-session $XDG_SESSION_ID

```

This should contain `Remote=no` and `Active=yes` in the output. If it does not, make sure that X runs on the same tty where the login occurred. This is required in order to preserve the logind session.

A D-Bus session should also be started along with X. See [D-Bus#Starting the user session](/index.php/D-Bus#Starting_the_user_session "D-Bus") for more information on this.

Basic [polkit](/index.php/Polkit "Polkit") actions do not require further set-up. Some polkit actions require further authentication, even with a local session. A polkit authentication agent needs to be running for this to work. See [polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit") for more information on this.

## error while loading shared libraries

If, while using a program, you get an error similar to:

```
error while loading shared libraries: libusb-0.1.so.4: cannot open shared object file: No such file or directory

```

Use [pacman](/index.php/Pacman "Pacman") or [pkgfile](/index.php/Pkgfile "Pkgfile") to search for the package that owns the missing library:

 `$ pacman -Fs libusb-0.1.so.4` 
```
extra/libusb-compat 0.1.5-1
    usr/lib/libusb-0.1.so.4

```

In this case, the [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat) package needs to be [installed](/index.php/Installed "Installed").

The error could also mean that the package that you used to install your program does not list the library as a dependency in its [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"): if it is an official package, [report a bug](/index.php/Report_a_bug "Report a bug"); if it is an [AUR](/index.php/AUR "AUR") package, report it to the maintainer using its page in the AUR website.

## file: could not find any magic files!

*Example:* After an every-day routine update or following the installation of a package you are given the following error:

```
# file: could not find any magic files!

```

This will most likely leave your system crippled. And, any attempts made to recompile/reinstall the package(s) responsible for the breakage will fail. Also, any attempts made to try to rebuild the [initramfs](/index.php/Initramfs "Initramfs") will result in the following:

```
# mkinitcpio -p linux
==> Building image from preset: 'default'
 -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux.img
file: could not find any magic files!
==> ERROR: invalid kernel specifier: `/boot/vmlinuz-linux'
==> Building image from preset: 'fallback'
 -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux-fallback.img -S autodetect
file: could not find any magic files!
@==> ERROR: invalid kernel specifier: `/boot/vmlinuz-linux'

```

Typically a previously installed application had placed a configuration file within `/etc/ld.so.conf.d/` or it had made changes to `/etc/ld.so.conf` which are now invalid.

1.  Boot into the Arch Linux Live CD / Installation Media.
2.  Mount your root (`**/**`) partition to `/mnt` and using [arch-chroot](/index.php/Change_root#Change_root "Change root"), [chroot](/index.php/Chroot "Chroot") into your system.

**Note:** [arch-chroot](/index.php/Change_root#Change_root "Change root") leaves mounting the `/boot` partition up to the user.

1.  Examine `/etc/ld.so.conf` and remove any invalid lines found.
2.  Examine the files located inside the directory `/etc/ld.so.conf.d/` and remove all invalid files.
3.  Rebuild the [initramfs](/index.php/Initramfs "Initramfs").

```
# mkinitcpio -p linux

```

1.  Reboot back to your installed system.
2.  Once booted, reinstall the package that was responsible for leaving your system inoperable using:

```
# pacman -S <package>

```

## See also

*   [Fix the Most Common Problems](http://www.tuxradar.com/content/how-fix-most-common-linux-problems)
*   [A how-to in troubleshooting for newcomers](https://www.reddit.com/r/archlinux/comments/tjjwr/archlinux_a_howto_in_troubleshooting_for_newcomers/)