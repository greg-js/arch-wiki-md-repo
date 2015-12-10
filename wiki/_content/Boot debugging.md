# Boot debugging

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot loaders](/index.php/Boot_loaders "Boot loaders")
*   [Netconsole](/index.php/Netconsole "Netconsole")
*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [Kernel Mode Setting](/index.php/Kernel_Mode_Setting "Kernel Mode Setting")
*   [systemd](/index.php/Systemd "Systemd")

A lot happens during the boot process, so it is a common time for errors to manifest. There are many methods for diagnosing and fixing boot problems but most of them involve changing the kernel parameters and rebooting the system. Ensure that you are familiar with how to change your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## Contents

*   [1 Console Clearing](#Console_Clearing)
*   [2 Debug output](#Debug_output)
*   [3 Recovery shells](#Recovery_shells)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Blank screen with Intel video](#Blank_screen_with_Intel_video)
    *   [4.2 Stuck while loading the kernel](#Stuck_while_loading_the_kernel)
    *   [4.3 Unbootable system](#Unbootable_system)
    *   [4.4 Debugging kernel modules](#Debugging_kernel_modules)
    *   [4.5 Debugging hardware](#Debugging_hardware)
*   [5 Advanced methods](#Advanced_methods)
    *   [5.1 netconsole](#netconsole)
    *   [5.2 Hijacking cmdline](#Hijacking_cmdline)
*   [6 See also](#See_also)

## Console Clearing

If all you want is to be able to see error messages that are already being displayed, you should [disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages").

## Debug output

Most kernel messages are hidden during boot. You can see more of these messages by adding different kernel parameters. The simplest ones are:

*   `debug` enables debug messages for both the kernel and [systemd](/index.php/Systemd "Systemd")
*   `ignore_loglevel` forces _all_ kernel messages to be printed

Other parameters you can add that might be useful in certain situations are:

*   `earlyprintk=vga,keep` prints kernel messages very early in the boot process, in case the kernel would crash before output is shown. You must change `vga` to `efi` for [EFI](/index.php/EFI "EFI") systems
*   `log_buf_len=16M` allocates a larger (16MB) kernel message buffer, to ensure that debug output is not overwritten

There are also a number of separate debug parameters for enabling debugging in specific subsystems e.g. `bootmem_debug`, `sched_debug`. Check the [kernel parameter documentation](https://www.kernel.org/doc/Documentation/kernel-parameters.txt) for specific information.

**Note:** If you cannot scroll back far enough to view the desired boot output, you should increase the size of the [scrollback buffer](/index.php/Scrollback_buffer "Scrollback buffer").

## Recovery shells

Getting an interactive shell at some stage in the boot process can help you pinpoint exactly where and why something is failing. There are several kernel parameters for doing so, but they all launch a normal shell which you can `exit` to let the kernel resume what it was doing:

*   `rescue` launches a shell shortly after the root filesystem is remounted read/write
*   `emergency` launches a shell even earlier, before most filesystems are mounted
*   `init=/bin/sh` (as a last resort) changes the init program to a root shell. `rescue` and `emergency` both rely on [systemd](/index.php/Systemd "Systemd"), but this should work even if _systemd_ is broken

Another option is to [enable](/index.php/Enable "Enable") `debug-shell.service`, which adds a root shell on `tty9` (accessible with Ctrl+Alt+F9). Take care to disable the service when done to avoid the security risk of leaving a root shell open on every boot.

## Troubleshooting

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

## Advanced methods

### netconsole

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [netconsole](/index.php/Netconsole "Netconsole").**

**Notes:** The main article should have complete information for doing this, and it shouldn't be duplicated here. (Discuss in [Talk:Boot debugging#](https://wiki.archlinux.org/index.php/Talk:Boot_debugging))

[netconsole](/index.php/Netconsole "Netconsole") is a kernel module which sends kernel logs over the network, which is useful for debugging slower computers. The setup process is:

1.  Set up another computer (running Arch) to accept syslog requests on a remote port using `syslog.conf`
2.  View the logs using your `/var/log/everything.log` file
3.  On the computer you are debugging, add a kernel paramter like `netconsole=514@10.0.0.2/12:34:56:78:9a:bc` (along with whatever debugging parameters you want)
4.  Restart the computer and view the logs

Netconsole can view even more output than the `earlyprintk=vga` parameter allows, due to its extensive integration in the kernel. See also the [netconsole documentation](https://www.kernel.org/doc/Documentation/networking/netconsole.txt).

### Hijacking cmdline

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").**

**Notes:** This is really just a different way of changing kernel parameters. (Discuss in [Talk:Boot debugging#](https://wiki.archlinux.org/index.php/Talk:Boot_debugging))

Even without access to your bootloader it is possible to change your kernel parameters to enable debugging (if you have root access). This can be accomplished by overwriting `/proc/cmdline` which stores the kernel parameters. However `/proc/cmdline` is not writable even as root, so this hack is accomplished by using a bind mount to mask the path.

First create a file containing the desired kernel parameters

 `/root/cmdline`  `root=/dev/disk/by-label/ROOT ro console=tty1 logo.nologo debug` 

Then use a bind mount to overwrite the parameters

```
# mount -n --bind -o ro /root/cmdline /proc/cmdline

```

The `-n` option skips adding the mount to `/etc/mtab`, so it will work even if root is mounted read-only. You can `cat /proc/cmdline` to confirm that your change was successful.

## See also

*   [Kernel Parameters Documentation](https://www.kernel.org/doc/Documentation/kernel-parameters.txt)
*   [Memtest86+](http://www.memtest.org/)
*   [List of Tools for UBCD](http://wiki.ultimatebootcd.com/index.php?title=Tools) - Can be added to custom menu.lst like memtest
*   Official GRUB2 Manual - [https://www.gnu.org/software/grub/manual/grub.html](https://www.gnu.org/software/grub/manual/grub.html)
*   Ubuntu wiki page for GRUB2 - [https://help.ubuntu.com/community/Grub2](https://help.ubuntu.com/community/Grub2)
*   GRUB2 wiki page describing steps to compile for UEFI systems - [https://help.ubuntu.com/community/UEFIBooting](https://help.ubuntu.com/community/UEFIBooting)
*   Wikipedia's page on [BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [QA/Sysrq](https://fedoraproject.org/wiki/QA/Sysrq) - Using sysrq
*   systemd documentation: [Debug Logging to a Serial Console](http://freedesktop.org/wiki/Software/systemd/Debugging#Debug_Logging_to_a_Serial_Console)
*   [How to Isolate Linux ACPI Issues](https://lesswatts.org/projects/acpi/debug.php)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Boot_debugging&oldid=410488](https://wiki.archlinux.org/index.php?title=Boot_debugging&oldid=410488)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Boot process](/index.php/Category:Boot_process "Category:Boot process")
*   [System recovery](/index.php/Category:System_recovery "Category:System recovery")