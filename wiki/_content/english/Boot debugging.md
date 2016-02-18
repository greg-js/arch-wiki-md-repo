A lot happens during the boot process, so it is a common time for errors to manifest. There are many methods for diagnosing and fixing boot problems, but most involve changing the kernel parameters and rebooting the system. Ensure that you are familiar with how to change your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). For common issues, see [General troubleshooting#Boot problems](/index.php/General_troubleshooting#Boot_problems "General troubleshooting").

## Contents

*   [1 Console clearing](#Console_clearing)
*   [2 Debug output](#Debug_output)
*   [3 Recovery shells](#Recovery_shells)
*   [4 See also](#See_also)

## Console clearing

If all you want is to be able to see error messages that are already being displayed, you should [disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages").

## Debug output

Most kernel messages are hidden during boot. You can see more of these messages by adding different kernel parameters. The simplest ones are:

*   `debug` enables debug messages for both the kernel and [systemd](/index.php/Systemd "Systemd")
*   `ignore_loglevel` forces *all* kernel messages to be printed

Other parameters you can add that might be useful in certain situations are:

*   `earlyprintk=vga,keep` prints kernel messages very early in the boot process, in case the kernel would crash before output is shown. You must change `vga` to `efi` for [EFI](/index.php/EFI "EFI") systems
*   `log_buf_len=16M` allocates a larger (16MB) kernel message buffer, to ensure that debug output is not overwritten

There are also a number of separate debug parameters for enabling debugging in specific subsystems e.g. `bootmem_debug`, `sched_debug`. Check the [kernel parameter documentation](https://www.kernel.org/doc/Documentation/kernel-parameters.txt) for specific information.

**Note:** If you cannot scroll back far enough to view the desired boot output, you should increase the size of the [scrollback buffer](/index.php/Scrollback_buffer "Scrollback buffer").

## Recovery shells

Getting an interactive shell at some stage in the boot process can help you pinpoint exactly where and why something is failing. There are several kernel parameters for doing so, but they all launch a normal shell which you can `exit` to let the kernel resume what it was doing:

*   `rescue` launches a shell shortly after the root filesystem is remounted read/write
*   `emergency` launches a shell even earlier, before most filesystems are mounted
*   `init=/bin/sh` (as a last resort) changes the init program to a root shell. `rescue` and `emergency` both rely on [systemd](/index.php/Systemd "Systemd"), but this should work even if *systemd* is broken

Another option is to [enable](/index.php/Enable "Enable") `debug-shell.service`, which adds a root shell on `tty9` (accessible with Ctrl+Alt+F9). Take care to disable the service when done to avoid the security risk of leaving a root shell open on every boot.

## See also

*   [Memtest86+](http://www.memtest.org/)
*   [List of Tools for UBCD](http://wiki.ultimatebootcd.com/index.php?title=Tools) - Can be added to custom menu.lst like memtest
*   Wikipedia's page on [BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [QA/Sysrq](https://fedoraproject.org/wiki/QA/Sysrq) - Using sysrq
*   systemd documentation: [Debug Logging to a Serial Console](http://freedesktop.org/wiki/Software/systemd/Debugging#Debug_Logging_to_a_Serial_Console)
*   [How to Isolate Linux ACPI Issues](https://web.archive.org/web/20120217124742/http://www.lesswatts.org/projects/acpi/debug.php)