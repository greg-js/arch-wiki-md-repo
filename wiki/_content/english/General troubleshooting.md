Related articles

*   [Reporting bug guidelines](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Debug - Getting Traces](/index.php/Debug_-_Getting_Traces "Debug - Getting Traces")
*   [IRC Collaborative Debugging](/index.php/IRC_Collaborative_Debugging "IRC Collaborative Debugging")

This article explains some methods for general troubleshooting. For application specific issues, please reference the particular wiki page for that program.

## Contents

*   [1 General procedures](#General_procedures)
    *   [1.1 Attention to detail](#Attention_to_detail)
    *   [1.2 Questions/checklist](#Questions/checklist)
    *   [1.3 Approach](#Approach)
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
*   [3 Kernel panics](#Kernel_panics)
    *   [3.1 Examine panic message](#Examine_panic_message)
        *   [3.1.1 Example scenario: bad module](#Example_scenario:_bad_module)
    *   [3.2 Reboot into root shell and fix problem](#Reboot_into_root_shell_and_fix_problem)
*   [4 Package management](#Package_management)
*   [5 fuser](#fuser)
*   [6 Session permissions](#Session_permissions)
*   [7 Message: "error while loading shared libraries"](#Message:_"error_while_loading_shared_libraries")
*   [8 Message: "file: could not find any magic files!"](#Message:_"file:_could_not_find_any_magic_files!")
    *   [8.1 Problem](#Problem)
    *   [8.2 Solution](#Solution)
*   [9 See also](#See_also)

## General procedures

### Attention to detail

In order to resolve an issue that you are having, it is *absolutely crucial* to have a firm basic understanding of how that specific subsystem functions. How does it work, and what does it need to run without error? If you cannot comfortably answer these question then you would best review the [Archwiki](/index.php/Table_of_contents "Table of contents") article for the subsystem that you are having trouble with. Once you feel like you have understood it, it will be easier for you to pinpoint the cause of the problem.

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

### Approach

Rather than approaching an issue by stating,

*Application X does not work.*

you will find it more helpful to formulate your issue in the context of the system as a whole, as:

*Application X produces Y error(s) when performing Z tasks under conditions A and B.*

### Additional support

With all the information in front of you you should have a good idea as to what is going on with the system and you can now start working on a proper fix.

If you require any additional support, it can be found on [the forums](https://bbs.archlinux.org) or IRC at irc.freenode.net #archlinux. See [IRC channels](/index.php/IRC_channels "IRC channels") for other options.

**Note:** [Support is provided for Arch Linux *only*](/index.php/Code_of_conduct#Arch_Linux_distribution_support_.2Aonly.2A "Code of conduct") and not [Arch-based distributions](/index.php/Arch-based_distributions "Arch-based distributions").

When asking for support post the **complete** output/logs, not just what you think are the significant sections. Sources of information include:

*   Full output of any command involved - do not just select what you think is relevant.
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

If scrolling up all the way does not show you enough information, you need to expand your scrollback buffer to hold more output. This is done by tweaking the kernel's framebuffer console (fbcon) with the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `fbcon=scrollback:Nk` where `N` is the desired buffer size in kilobytes. The default size is 32k.

If this does not work, your framebuffer console may not be properly enabled. Check the [Framebuffer Console documentation](https://www.kernel.org/doc/Documentation/fb/fbcon.txt) for other parameters, e.g. for changing the framebuffer driver.

#### Debug output

Most kernel messages are hidden during boot. You can see more of these messages by adding different kernel parameters. The simplest ones are:

*   `debug` enables debug messages for both the kernel and [systemd](/index.php/Systemd "Systemd")
*   `ignore_loglevel` forces *all* kernel messages to be printed

Other parameters you can add that might be useful in certain situations are:

*   `earlyprintk=vga,keep` prints kernel messages very early in the boot process, in case the kernel would crash before output is shown. You must change `vga` to `efi` for [EFI](/index.php/EFI "EFI") systems
*   `log_buf_len=16M` allocates a larger (16MB) kernel message buffer, to ensure that debug output is not overwritten

There are also a number of separate debug parameters for enabling debugging in specific subsystems e.g. `bootmem_debug`, `sched_debug`. Check the [kernel parameter documentation](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt) for specific information.

**Note:** If you cannot scroll back far enough to view the desired boot output, you should increase the size of the [scrollback buffer](/index.php/Scrollback_buffer "Scrollback buffer").

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

*   You can display extra debugging information about your hardware by following [udev#Debug output](/index.php/Udev#Debug_output "Udev").
*   Ensure that [Microcode](/index.php/Microcode "Microcode") updates are applied on your system.
*   Test your device's RAM with [memtest86+](https://www.archlinux.org/packages/?name=memtest86%2B). Unstable RAM may lead to some extremely odd issues, ranging from random crashes to data corruption. [memtester](https://www.archlinux.org/packages/?name=memtester) performs similar tests, but it can't test the whole RAM.

## Kernel panics

A *kernel panic* occurs when the Linux kernel enters an unrecoverable failure state. The state typically originates from buggy hardware drivers resulting in the machine being deadlocked, non-responsive, and requiring a reboot. Just prior to deadlock, a diagnostic message is generated, consisting of: the *machine state* when the failure occurred, a *call trace* leading to the kernel function that recognized the failure, and a listing of currently loaded modules. Thankfully, kernel panics do not happen very often using *mainline* versions of the kernel--such as those supplied by the official repositories--but when they do happen, you need to know how to deal with them.

**Note:** Kernel panics are sometimes referred to as *oops* or *kernel oops*. While both panics and oops occur as the result of a failure state, an *oops* is more general in that it does not *necessarily* result in a deadlocked machine--sometimes the kernel can recover from an oops by killing the offending task and carrying on.

**Tip:** Pass the kernel parameter `oops=panic` at boot or write `1` to `/proc/sys/kernel/panic_on_oops` to force a recoverable oops to issue a panic instead. This is advisable if you are concerned about the small chance of system instability resulting from an oops recovery which may make future errors difficult to diagnose.

### Examine panic message

If a kernel panic occurs very early in the boot process, you may see a message on the console containing "Kernel panic - not syncing:", but once [Systemd](/index.php/Systemd "Systemd") is running, kernel messages will typically be captured and written to the system log. However, when a panic occurs, the diagnostic message output by the kernel is *almost never* written to the log file on disk because the machine deadlocks before `system-journald` gets the chance. Therefore, the only way to examine the panic message is to view it on the console as it happens (without resorting to setting up a *kdump crashkernel*). You can do this by booting with the following kernel parameters and attempting to reproduce the panic on tty1:

 `systemd.journald.forward_to_console=1 console=tty1` 
**Tip:** In the event that the panic message scrolls away too quickly to examine, try passing the kernel parameter `pause_on_oops=*seconds*` at boot.

#### Example scenario: bad module

It is possible to make a best guess as to what subsystem or module is causing the panic using the information in the diagnostic message. In this scenario, we have a panic on some imaginary machine during boot. Pay attention to the lines highlighted in **bold**:

```
**kernel: BUG: unable to handle kernel NULL pointer dereference at (null)** [1]
**kernel: IP: fw_core_init+0x18/0x1000 [firewire_core]** [2]
kernel: PGD 718d00067 
kernel: P4D 718d00067 
kernel: PUD 7b3611067 
kernel: PMD 0 
kernel: 
kernel: Oops: 0002 [#1] PREEMPT SMP
**kernel: Modules linked in: firewire_core(+) crc_itu_t cfg80211 rfkill ipt_REJECT nf_reject_ipv4 nf_log_ipv4 nf_log_common xt_LOG nf_conntrack_ipv4 ...** [3] 
kernel: CPU: 6 PID: 1438 Comm: modprobe Tainted: P           O    4.13.3-1-ARCH #1
kernel: Hardware name: Gigabyte Technology Co., Ltd. H97-D3H/H97-D3H-CF, BIOS F5 06/26/2014
kernel: task: ffff9c667abd9e00 task.stack: ffffb53b8db34000
kernel: RIP: 0010:fw_core_init+0x18/0x1000 [firewire_core]
kernel: RSP: 0018:ffffb53b8db37c68 EFLAGS: 00010246
kernel: RAX: 0000000000000000 RBX: 0000000000000000 RCX: 0000000000000000
kernel: RDX: 0000000000000000 RSI: 0000000000000008 RDI: ffffffffc16d3af4
kernel: RBP: ffffb53b8db37c70 R08: 0000000000000000 R09: ffffffffae113e95
kernel: R10: ffffe93edfdb9680 R11: 0000000000000000 R12: ffffffffc16d9000
kernel: R13: ffff9c6729bf8f60 R14: ffffffffc16d5710 R15: ffff9c6736e55840
kernel: FS:  00007f301fc80b80(0000) GS:ffff9c675dd80000(0000) knlGS:0000000000000000
kernel: CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
kernel: CR2: 0000000000000000 CR3: 00000007c6456000 CR4: 00000000001406e0
kernel: Call Trace:
**kernel:  do_one_initcall+0x50/0x190** [4]
kernel:  ? do_init_module+0x27/0x1f2
kernel:  do_init_module+0x5f/0x1f2
kernel:  load_module+0x23f3/0x2be0
kernel:  SYSC_init_module+0x16b/0x1a0
kernel:  ? SYSC_init_module+0x16b/0x1a0
kernel:  SyS_init_module+0xe/0x10
kernel:  entry_SYSCALL_64_fastpath+0x1a/0xa5
kernel: RIP: 0033:0x7f301f3a2a0a
kernel: RSP: 002b:00007ffcabbd1998 EFLAGS: 00000246 ORIG_RAX: 00000000000000af
kernel: RAX: ffffffffffffffda RBX: 0000000000c85a48 RCX: 00007f301f3a2a0a
kernel: RDX: 000000000041aada RSI: 000000000001a738 RDI: 00007f301e7eb010
kernel: RBP: 0000000000c8a520 R08: 0000000000000001 R09: 0000000000000085
kernel: R10: 0000000000000000 R11: 0000000000000246 R12: 0000000000c79208
kernel: R13: 0000000000c8b4d8 R14: 00007f301e7fffff R15: 0000000000000030
kernel: Code: <c7> 04 25 00 00 00 00 01 00 00 00 bb f4 ff ff ff e8 73 43 9c ec 48 
kernel: RIP: fw_core_init+0x18/0x1000 [firewire_core] RSP: ffffb53b8db37c68
kernel: CR2: 0000000000000000
kernel: ---[ end trace 71f4306ea1238f17 ]---
**kernel: Kernel panic - not syncing: Fatal exception** [5]
kernel: Kernel Offset: 0x80000000 from 0xffffffff810000000 (relocation range: 0xffffffff800000000-0xfffffffffbffffffff
kernel: ---[ end Kernel panic - not syncing: Fatal exception
```

*   [1] Indicates the type of error that caused the panic. In this case it was a programmer bug.
*   [2] Indicates that the panic happened in a function called *fw_core_init* in module *firewire_core*.
*   [3] Indicates that *firewire_core* was the latest module to be loaded.
*   [4] Indicates that the function that called function *fw_core_init* was *do_one_initcall*.
*   [5] Indicates that this *oops* message is, in fact, a kernel panic and the system is now deadlocked.

We can surmise then, that the panic occurred during the initialization routine of module *firewire_core* as it was loaded. (We might assume then, that the machine's firewire hardware is incompatible with this version of the firewire driver module due to a programmer error, and will have to wait for a new release.) In the meantime, the easiest way to get the machine running again is to prevent the module from being loaded. We can do this in one of two ways:

*   If the module is being loaded during the execution of the *initramfs*, reboot with the kernel parameter `rd.blacklist=firewire_core`.
*   Otherwise reboot with the kernel parameter `module_blacklist=firewire_core`.

### Reboot into root shell and fix problem

You will need a root shell to make changes to the system so the panic no longer occurs. If the panic occurs on boot, there are several strategies to obtain a root shell before the machine deadlocks:

*   Reboot with the kernel parameter `emergency`, `rd.emergency`, or `-b` to receive a prompt to login just after the root filesystem is mounted and `systemd` is started.

**Note:** At this point, the root filesystem will be mounted **read-only**. Execute `# mount -o remount,rw /` to make changes.

*   Reboot with the kernel parameter `rescue`, `rd.rescue`, `single`, `s`, `S`, or `1` to receive a prompt to login just after local filesystems are mounted.
*   Reboot with the kernel parameter `systemd.debug-shell=1` to obtain a very early root shell on tty9\. Switch to it with by pressing `Ctrl-Alt-F9`.
*   Experiment by rebooting with different sets of kernel parameters to possibly disable the kernel feature that is causing the panic. Try the "old standbys" `acpi=off` and `nolapic`.

**Tip:** See `Documentation/admin-guide/kernel-parameters.txt` in the Linux kernel source tree for all parameters.

*   As a last resort, boot with the **Arch Linux Installation CD** and mount the root filesystem on `/mnt` then execute `# arch-chroot /mnt`.

Disable the service or program that is causing the panic, roll-back a faulty update, or fix a configuration problem.

## Package management

See [Pacman#Troubleshooting](/index.php/Pacman#Troubleshooting "Pacman") for general topics, and [pacman/Package signing#Troubleshooting](/index.php/Pacman/Package_signing#Troubleshooting "Pacman/Package signing") for issues with PGP keys.

## fuser

*fuser* is a command-line utility for identifying processes using resources such as files, filesystems and TCP/UDP ports.

*fuser* is provided by the [psmisc](https://www.archlinux.org/packages/?name=psmisc) package, which should be already installed as part of the [base](https://www.archlinux.org/groups/x86_64/base/) group. See [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1) for detail.

## Session permissions

**Note:** You must be using [systemd](/index.php/Systemd "Systemd") as your init system for local sessions to work.[[1]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) It is required for polkit permissions and ACLs for various devices (see `/usr/lib/udev/rules.d/70-uaccess.rules` and [[2]](http://enotty.pipebreaker.pl/2012/05/23/linux-automatic-user-acl-management/))

First, make sure you have a valid local session within X:

```
$ loginctl show-session $XDG_SESSION_ID

```

This should contain `Remote=no` and `Active=yes` in the output. If it does not, make sure that X runs on the same tty where the login occurred. This is required in order to preserve the logind session.

Basic [polkit](/index.php/Polkit "Polkit") actions do not require further set-up. Some polkit actions require further authentication, even with a local session. A polkit authentication agent needs to be running for this to work. See [polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit") for more information on this.

## Message: "error while loading shared libraries"

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

In this case, the [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat) package needs to be [installed](/index.php/Install "Install").

The error could also mean that the package that you used to install your program does not list the library as a dependency in its [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"): if it is an official package, [report a bug](/index.php/Report_a_bug "Report a bug"); if it is an [AUR](/index.php/AUR "AUR") package, report it to the maintainer using its page in the AUR website.

## Message: "file: could not find any magic files!"

If you see this message, it likely indicates that a package update has corrupted the dynamic linker run-time bindings file and your system is now essentially crippled. You will not be able to recompile or reinstall the package responsible or rebuild the [initramfs](/index.php/Initramfs "Initramfs") until you fix it.

### Problem

A package update likely added an invalid `*filename*.conf` to the directory `/etc/ld.so.conf.d` or edited `/etc/ld.so.conf` incorrectly. The result is that the dynamic linker run-time bindings file `/etc/ld.so.cache` is being re-generated with invalid data. This can potentially cause all programs on the system that depend on shared libraries to fail (ie. almost all of them).

### Solution

1.  Boot with the ***Arch Linux Installation CD***.
2.  Mount your root `/` filesystem on `/mnt` and your `/boot` filesystem on `/mnt/boot` and chroot into the broken system by executing `# arch-chroot /mnt`.
3.  Examine the file `/etc/ld.so.conf` and remove any invalid lines found.
4.  Examine the files located in the directory `/etc/ld.so.conf.d/` and remove any invalid files.
5.  Rebuild the dynamic linker run-time bindings file `/etc/ld.so.cache` by executing `# ldconfig`.
6.  Rebuild the [Initramfs](/index.php/Initramfs "Initramfs") by executing `# mkinitcpio -p linux`.
7.  Exit the chroot, unmount filesystems, and reboot back into your installed system.

## See also

*   [Fix the Most Common Problems](http://www.tuxradar.com/content/how-fix-most-common-linux-problems)
*   [A how-to in troubleshooting for newcomers](https://www.reddit.com/r/archlinux/comments/tjjwr/archlinux_a_howto_in_troubleshooting_for_newcomers/)
*   [List of Tools for UBCD](http://wiki.ultimatebootcd.com/index.php?title=Tools) - Memtest-like tools to add to grub.cfg on UltimateBootCD.com
*   [Wikipedia:BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [REISUB](/index.php/REISUB "REISUB")
*   [Debug Logging to a Serial Console](https://freedesktop.org/wiki/Software/systemd/Debugging/#Debug_Logging_to_a_Serial_Console) on Freedesktop.org
*   [How to Isolate Linux ACPI Issues](https://web.archive.org/web/20120217124742/http://www.lesswatts.org/projects/acpi/debug.php) on Archive.org