[Kdump](https://www.kernel.org/doc/Documentation/kdump/kdump.txt) is a standard Linux mechanism to dump machine memory content on kernel crash. Kdump is based on [Kexec](/index.php/Kexec "Kexec"). Kdump utilizes two kernels: system kernel and dump capture kernel. System kernel is a normal kernel that is booted with special kdump-specific flags. We need to tell the system kernel to reserve some amount of physical memory where dump-capture kernel will be loaded. We need to load the dump capture kernel in advance because at the moment crash happens there is no way to read any data from disk because kernel is broken.

Once kernel crash happens the kernel crash handler uses [Kexec](/index.php/Kexec "Kexec") mechanism to boot dump capture kernel. Please note that memory with system kernel is untouched and accessible from dump capture kernel as seen at the moment of crash. Once dump capture kernel is booted, the user can use the file `/proc/vmcore` to get access to memory of crashed system kernel. The dump can be saved to disk or copied over network to some other machine for further investigation.

In real production environments system and dump capture kernel will be different - system kernel needs a lot of features and compiled with a many kernel flags/drivers. While dump capture kernel goal is to be minimalistic and take as small amount of memory as possible, e.g. dump capture kernel can be compiled without network support if we store memory dump to disk only. But in this article we will simplify things and use the same kernel both as system and dump capture one. It means we will load the same kernel code twice - one as normal system kernel, another one to reserved memory area.

## Contents

*   [1 Compiling kernel](#Compiling_kernel)
*   [2 Setup kdump kernel](#Setup_kdump_kernel)
*   [3 Testing crash](#Testing_crash)
*   [4 Dump crashed kernel](#Dump_crashed_kernel)
*   [5 Analyzing core dump](#Analyzing_core_dump)
*   [6 Additional information](#Additional_information)

## Compiling kernel

System/dump capture kernel requires some configuration flags that are not set by default. Please consult [Kernel Compilation](/index.php/Kernel_Compilation "Kernel Compilation") article for more information about compiling a custom kernel in Arch. Here we will emphasize on Kdump specific configuration.

To create a kernel you need to edit kernel config (or config.x86_64) file and enable following configuration options:

 `config{.x86_64} file` 
```
CONFIG_DEBUG_INFO=y
CONFIG_CRASH_DUMP=y
CONFIG_PROC_VMCORE=y

```

Also change package base name to something like **linux-kdump** to distinguish the kernel from the default Arch one. Compile kernel package and install it. Save *./src/linux-X.Y/vmlinux* uncompressed system kernel binary - it contains debug symbols and you will need them later when analyzing the crash.

In case if you have a separate kernel for the system and dump capture then it is recommended to consult [Kdump](https://www.kernel.org/doc/Documentation/kdump/kdump.txt) documentation. It has several recommendations how to make dump capture kernel smaller.

## Setup kdump kernel

First, you need to reserve memory for dump capture kernel. Edit you bootloader configuration and add `crashkernel=64M` boot option to the system kernel you just installed. For example [Syslinux](/index.php/Syslinux "Syslinux") boot entry would look like:

 `/boot/syslinux/syslinux.cfg` 
```
LABEL arch-kdump
        MENU LABEL Arch Linux Kdump
        LINUX ../vmlinuz-linux-kdump
        APPEND root=/dev/sda1 crashkernel=64M
        INITRD ../initramfs-linux-kdump.img

```

64M of memory should be enough to handle crash dumps on machines with up to 12G of RAM. Some systems require more reserved memory. In case if dump capture kernel unable not load try to increase the memory to *256M* or even to *512M*, but note that this memory is unavailable to system kernel.

Reboot into your system kernel. To make sure that the kernel is booted with correct options please check the `/proc/cmdline` file.

Next you need to tell [Kexec](/index.php/Kexec "Kexec") that you want to use your dump capture kernel. Specify your kernel, initramfs file, root device and other parameters if needed:

```
# kexec -p [/boot/vmlinuz-linux-kdump] --initrd=[/boot/initramfs-linux-kdump.img] --append="root=[root-device] single irqpoll maxcpus=1 reset_devices"

```

It loads the kernel into the reserved area. Without the `-p` flag *kexec* would boot the kernel right away, but in presence of the flag kernel will be loaded into reserved memory but boot postponed until a crash.

**Note:** For a loaded kernel `cat /sys/devices/system/cpu/online` shows the active CPU cores. The `maxcpus=1` kernel parameter should [limit](https://www.kernel.org/doc/Documentation/cpu-hotplug.txt) it to one. If it has no effect or your SMP-enabled kernel [does not boot](https://bbs.archlinux.org/viewtopic.php?pid=1424049#p1424049), try using `nr_cpus=1` instead.

Instead of running *kexec* manually you might want to setup [Systemd](/index.php/Systemd "Systemd") service that will run kexec on boot:

 `/etc/systemd/system/kdump.service` 
```
[Unit]
Description=Load dump capture kernel
After=local-fs.target

[Service]
ExecStart=/usr/bin/kexec -p [/boot/vmlinuz-linux-kdump] --initrd=[/boot/initramfs-linux-kdump.img] --append="root=[root-device] single irqpoll maxcpus=1 reset_devices"
Type=oneshot

[Install]
WantedBy=multi-user.target

```

Then enable the service :

```
# systemctl enable kdump

```

To check whether the crash kernel is already loaded please run following command:

```
$ cat /sys/kernel/kexec_crash_loaded

```

## Testing crash

If you want to test crash then you can use *sysrq* for this.
**Warning:** kernel crash may corrupt data on your disks, run it at your own risk!

```
# echo c > /proc/sysrq-trigger

```

Once crash happens kexec will load your dump capture kernel.

## Dump crashed kernel

Once booted into dump capture kernel you can read `/proc/vmcore` file. It is recommended to dump core to a file and analyze it later.

```
# cp /proc/vmcore /root/crash.dump

```

or optionally you can copy the crash to another machine. Once dump is saved you should reboot the machine into normal system kernel.

The crash dump can be quite big, [makedumpfile](https://aur.archlinux.org/packages/makedumpfile/) can be used to create smaller dumps by ignoring some memory regions and using compression:

```
# makedumpfile -c -d 31 /proc/vmcore /root/crash.dump

```

The following systemd service can be used to automatically save crash dumps and reboot into the main kernel:

 `/etc/systemd/system/kdump-save.service` 
```
[Unit]
Description=Create dump after kernel crash
DefaultDependencies=no
Wants=local-fs.target
After=local-fs.target

[Service]
Type=idle
ExecStart=/bin/sh -c 'mkdir -p /var/crash/ && /usr/bin/makedumpfile -c -d 31 /proc/vmcore "/var/crash/crashdump-$$(date +%F-%T)"'
ExecStopPost=/usr/bin/systemctl reboot
UMask=0077
StandardInput=tty-force
StandardOutput=inherit
StandardError=inherit

```

This can be invoked from the dump capture kernel command line:

 `/etc/systemd/system/kdump.service` 
```
[Unit]
Description=Load dump capture kernel
After=local-fs.target

[Service]
ExecStart=/usr/bin/kexec -p [/boot/vmlinuz-linux-kdump] --initrd=[/boot/initramfs-linux-kdump.img] --append="root=[root-device] **systemd.unit=kdump-save.service** irqpoll maxcpus=1 reset_devices"
Type=oneshot

[Install]
WantedBy=multi-user.target
```

## Analyzing core dump

You can use either *gdb* tool or special gdb extension called [crash](https://www.archlinux.org/packages/?name=crash). Run *crash* as

```
$ crash *vmlinux* *path*/crash.dump

```

Where *vmlinux* previously saved kernel binary with debug symbols.

Follow *man crash* or [http://people.redhat.com/~anderson/crash_whitepaper/](http://people.redhat.com/~anderson/crash_whitepaper/) for more information about debugging practices.

## Additional information

*   [https://www.kernel.org/doc/Documentation/kdump/kdump.txt](https://www.kernel.org/doc/Documentation/kdump/kdump.txt) - Official kdump documentation
*   [http://www.dedoimedo.com/computers/www.dedoimedo.com-crash-book.pdf](http://www.dedoimedo.com/computers/www.dedoimedo.com-crash-book.pdf) - The crash book