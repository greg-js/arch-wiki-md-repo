# General troubleshooting

This article explains some methods for general troubleshooting. For application specific issues, please reference the particular wiki page for that program.

## Contents

*   [1 General procedures](#General_procedures)
    *   [1.1 Attention to detail](#Attention_to_detail)
    *   [1.2 Questions / checklist](#Questions_.2F_checklist)
    *   [1.3 Be more specific](#Be_more_specific)
    *   [1.4 Additional support](#Additional_support)
*   [2 Boot problems](#Boot_problems)
    *   [2.1 Blank screen with Intel video](#Blank_screen_with_Intel_video)
    *   [2.2 Stuck while loading the kernel](#Stuck_while_loading_the_kernel)
    *   [2.3 Unbootable system](#Unbootable_system)
    *   [2.4 Debugging kernel modules](#Debugging_kernel_modules)
    *   [2.5 Debugging hardware](#Debugging_hardware)
*   [3 Package management](#Package_management)
*   [4 fuser](#fuser)
*   [5 Session permissions](#Session_permissions)
*   [6 error while loading shared libraries](#error_while_loading_shared_libraries)
*   [7 file: could not find any magic files!](#file:_could_not_find_any_magic_files.21)
*   [8 Why I can't write on NTFS partitions?](#Why_I_can.27t_write_on_NTFS_partitions.3F)
*   [9 Spellcheck is marking all of my text as incorrect!](#Spellcheck_is_marking_all_of_my_text_as_incorrect.21)
*   [10 See also](#See_also)

## General procedures

### Attention to detail

In order to resolve an issue that you are having, it is _absolutely crucial_ to have a firm understanding of how that specific system functions. How it works, and what does it need to run without error? If you cannot comfortably answer these question then it is strongly advised that you review the [Archwiki](/index.php/Table_of_contents "Table of contents") article for the function that you are having troubles with. Once you feel like you've understood the specific system, it will be easier for you to pin-point the problem.

### Questions / checklist

The following gives a number of questions for you whenever dealing with a malfunctioning system. Under each question there are notes explaining how you should be answering each question, followed by some light examples on how to easily gather data output and what tools can be used to review logs and the journal.

1.  What is the issue(s)?

    	Be _as precise as possible_. This will help you not get confused and/or side-tracked when looking up specific information.

2.  Are there error messages? (if any)

    	Copy and paste _full outputs_ that contain **error messages** related to your issue into a separate file, such as `$HOME/issue.log`. For example, to forward the output of the following [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") command to `$HOME/issue.log`:

    	 `$ mkinitcpio -p linux >> $HOME/issue.log` 

3.  Can you reproduce the issue?

    	If so, give _exact_ **step-by-step** instructions/commands needed to do so.

4.  When did you first encounter these issues and what was changed between then and when the system was operating without error?

    	If it occurred right after an update then, list **all packages that were updated**. Include _version numbers_, also, paste the entire update from [pacman](/index.php/Pacman "Pacman").log (`/var/log/pacman.log`). Also take note of the statuses of _any_ service(s) needed to support the malfunctioning application(s) using [systemd](/index.php/Systemd "Systemd")'s systemctl tools. For example, to forward the output of the following [systemd](/index.php/Systemd#Basic_systemctl_usage "Systemd") command to `$HOME/issue.log`:

    	 `$ systemctl status dhcpcd@eth0.service >> $HOME/issue.log` 

    **Note:** Using `**>>**` will ensure any previous text in `$HOME/issue.log` will not be overwritten.

### Be more specific

When attempting to resolve an issue, **never** approach it as:

_Application X does not work._

Instead, look at it in its entirety:

_Application X produces Y error(s) when performing Z tasks under conditions A and B._

### Additional support

With all the information in front of you. You should have a good idea as to what is going on with the system. And you can now start working on a proper fix.

If you require any additional support, it can be found on [the forums](https://bbs.archlinux.org) or IRC at irc.freenode.net #archlinux

## Boot problems

See [Boot debugging](/index.php/Boot_debugging "Boot debugging") to retrieve additional information.

### Blank screen with Intel video

This is most likely due to a problem with [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Try [disabling modesetting](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting") or changing the [video port](/index.php/Intel#KMS_Issue:_console_is_limited_to_small_area "Intel").

### Stuck while loading the kernel

Try disabling ACPI by adding the `acpi=off` kernel parameter.

### Unbootable system

If your system will not boot at all, simply boot from a [live image](https://www.archlinux.org/download/) and [change root](/index.php/Change_root "Change root") to log into the system and fix the issue.

### Debugging kernel modules

See [Kernel modules#Obtaining information](/index.php/Kernel_modules#Obtaining_information "Kernel modules").

### Debugging hardware

See [udev#Debug output](/index.php/Udev#Debug_output "Udev").

## Package management

See [Pacman#Troubleshooting](/index.php/Pacman#Troubleshooting "Pacman") for general topics, and [pacman/Package signing#Troubleshooting](/index.php/Pacman/Package_signing#Troubleshooting "Pacman/Package signing") for issues with PGP keys.

## fuser

_fuser_ is a command-line utility for identifying processes using resources such as files, filesystems and TCP/UDP ports.

_fuser_ is provided by the [psmisc](https://www.archlinux.org/packages/?name=psmisc) package, which should be already installed as part of the [base](https://www.archlinux.org/groups/x86_64/base/) group.

## Session permissions

**Note:** You must be using [systemd](/index.php/Systemd "Systemd") as your init system for local sessions to work.[[1]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) It is required for polkit permissions and ACLs for various devices (see `/usr/lib/udev/rules.d/70-uaccess.rules` and [[2]](http://enotty.pipebreaker.pl/2012/05/23/linux-automatic-user-acl-management/))

First, make sure you have a valid local session within X:

```
$ loginctl show-session $XDG_SESSION_ID

```

This should contain `Remote=no` and `Active=yes` in the output. If it does not, make sure that X runs on the same tty where the login occurred. This is required in order to preserve the logind session. This is handled by the default `/etc/X11/xinit/xserverrc`.

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

_Example:_ After an every-day routine update or following the installation of a package you are given the following error:

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

## Why I can't write on NTFS partitions?

In clear system you can only read from NTFS file system. If you want to write, install [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) package.

## Spellcheck is marking all of my text as incorrect!

Have you installed an [aspell](https://www.archlinux.org/packages/?name=aspell) dictionary? Use `pacman -Ss aspell` to see available dictionaries for downloading.

If installing the dictionary files did not resolve the problem, it is most likely a problem with `enchant`. Check for known dictionary files:

 `$ aspell dicts` 

```
en
en_GB
...etc
```

If your respective language dictionary is listed, add it to `/usr/share/enchant/enchant.ordering`. From the above example, it would be:

```
en_GB:aspell

```

## See also

*   [Fix the Most Common Problems](http://www.maximumpc.com/article/features/linux_troubleshooting_guide_fix_most_common_problems)
*   [A how-to in troubleshooting for newcomers](https://www.reddit.com/r/archlinux/comments/tjjwr/archlinux_a_howto_in_troubleshooting_for_newcomers/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=General_troubleshooting&oldid=419498](https://wiki.archlinux.org/index.php?title=General_troubleshooting&oldid=419498)"