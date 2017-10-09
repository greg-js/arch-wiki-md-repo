A *kernel panic* occurs when the Linux kernel enters an unrecoverable failure state. The state typically originates from buggy hardware drivers resulting in the machine being deadlocked, non-responsive, and requiring a reboot. Just prior to deadlock, a diagnostic message is generated, consisting of: the *machine state* when the failure ocurred, a *call trace* leading to the kernel function that recognized the failure, and a listing of currently loaded modules. Thankfully, kernel panics don't happen very often using *mainline* versions of the kernel--such as those supplied by the official repositories--but when they do happen, you need to know how to deal with them.

**Note:** Kernel panics are sometimes referred to as *oops* or *kernel oops*. While both panics and oops occur as the result of a failure state, an *oops* is more general in that it does not *necessarily* result in a deadlocked machine--sometimes the kernel can recover from an oops by killing the offending task and carrying on.

**Tip:** Pass the kernel parameter `oops=panic` at boot or write `1` to `/proc/sys/kernel/panic_on_oops` to force a recoverable oops to issue a panic instead. This is advisable is you are concerned about the small chance of system instability resulting from an oops recovery which may make future errors difficult to diagnose.

## Examine panic message

If a kernel panic occurs very early in the boot process, you may see a message on the console containing "Kernel panic - not syncing:", but once [Systemd](/index.php/Systemd "Systemd") is running, kernel messages will typically be captured and written to the system log. However, when a panic occurs, the diagnostic message output by the kernel is *almost never* written to the log file on disk because the machine deadlocks before `system-journald` gets the chance. Therefore, the only way to examine the panic message is to view it on the console as it happens (without resorting to setting up a *kdump crashkernel*). You can do this by booting with the following kernel parameters and attempting to reproduce the panic on tty1:

 `systemd.journald.forward_to_console=1 console=tty1` 
**Tip:** In the event that the panic message scrolls away too quickly to examine, try passing the kernel parameter `pause_on_oops=*seconds*` at boot.

### Example scenario: bad module

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

## Reboot into root shell and fix problem

You'll need a root shell to make changes to the system so the panic no longer occurs. If the panic occurs on boot, there are several strategies to obtain a root shell before the machine deadlocks:

*   Reboot with the kernel parameter `emergency`, `rd.emergency`, or `-b` to receive a prompt to login just after the root filesystem is mounted and `systemd` is started.

**Note:** At this point, the root filesystem will be mounted **read-only**. Execute `# mount -o remount,rw /` to make changes.

*   Reboot with the kernel parameter `rescue`, `rd.rescue`, `single`, `s`, `S`, or `1` to receive a prompt to login just after local filesystems are mounted.
*   Reboot with the kernel parameter `systemd.debug-shell=1` to obtain a very early root shell on tty9\. Switch to it with by pressing `Ctrl-Alt-F9`.
*   Experiment by rebooting with different sets of kernel parameters to possibly disable the kernel feature that is causing the panic. Try the "old standbys" `acpi=off` and `nolapic`.

**Tip:** See `Documentation/admin-guide/kernel-parameters.txt` in the Linux kernel source tree for all options.

*   As a last resort, boot with the **Arch Linux Installation CD** and mount the root filesystem on `/mnt` then execute `# arch-chroot /mnt`.

Disable the service or program that is causing the panic, roll-back a faulty update, or fix a configuration problem.