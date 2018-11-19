Related articles

*   [Systemd](/index.php/Systemd "Systemd")

[Kexec](https://en.wikipedia.org/wiki/Kexec "wikipedia:Kexec") is a system call that enables you to load and boot into another kernel from the currently running kernel. This is useful for kernel developers or other people who need to reboot very quickly without waiting for the whole BIOS boot process to finish. Note that kexec may not work correctly for you due to devices *not* fully re-initializing when using this method, however this is rarely the case.

## Contents

*   [1 Installation](#Installation)
*   [2 Rebooting using kexec](#Rebooting_using_kexec)
    *   [2.1 Manually](#Manually)
    *   [2.2 Systemd](#Systemd)
        *   [2.2.1 Custom unit file](#Custom_unit_file)
        *   [2.2.2 Separate /boot partition](#Separate_/boot_partition)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 System hangs or reboots after "kexec_core: Starting new kernel"](#System_hangs_or_reboots_after_"kexec_core:_Starting_new_kernel")
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [kexec-tools](https://www.archlinux.org/packages/?name=kexec-tools) package.

## Rebooting using kexec

### Manually

You can manually invoke kexec using:

```
# kexec -l /boot/vmlinuz-linux --initrd=/boot/initramfs-linux.img --reuse-cmdline
# kexec -e

```

**Warning:** Running `kexec -e` directly will not unmount active filesystems or terminate any running services gracefully.

It is also possible to load kernel manually and then let systemd handle service shutdown and kexec for you. This, however, requires the bootloader to be [Systemd-boot](/index.php/Systemd-boot "Systemd-boot").

```
# kexec -l /boot/vmlinuz-linux --initrd=/boot/initramfs-linux.img --reuse-cmdline
# systemctl kexec

```

### Systemd

By default, if [systemd-boot](/index.php/Systemd-boot "Systemd-boot") is used and no kernel was loaded manually using `kexec -l` before, systemd will load the kernel specified in the default boot loader entry. For example, to reboot into the newer kernel after a system update, you may simply run:

```
# systemctl kexec

```

The command will refuse to execute if you have several initrd entries (e.g. for [Microcode](/index.php/Microcode "Microcode") updates) which are currently not supported.

#### Custom unit file

If the default behavior does not work for you or you desire to conveniently load custom kernels, you may wrap the kernel loading into a service unit. Create a new unit file, `kexec-load@.service`, that will load the specified kernel to be kexec'ed:

 `/etc/systemd/system/kexec-load@.service` 
```
[Unit]
Description=load %i kernel into the current kernel
Documentation=man:kexec(8)
DefaultDependencies=no
Before=shutdown.target umount.target final.target

[Service]
Type=oneshot
ExecStart=/usr/bin/kexec -l /boot/vmlinuz-%i --initrd=/boot/initramfs-%i.img --reuse-cmdline

[Install]
WantedBy=kexec.target
```

Then enable the service file for the kernel you want to load, for example simply the default kernel `linux`:

 `# systemctl enable kexec-load@linux`  `ln -s '/etc/systemd/system/kexec-load@.service' '/etc/systemd/system/kexec.target.wants/kexec-load@linux.service'` 

Ensure that the shutdown hook is not part of your initramfs image by removing it from the `HOOKS` array in `/etc/mkinitcpio.conf`. If it is, remove it and rebuild your initrd image with `mkinitcpio -p linux`.

Then to kexec

```
# systemctl kexec

```

If you wish to load a different kernel for the next kexec, for example `linux-lts`, disable the service for the current kernel and enable the one for the new kernel:

```
# systemctl disable kexec-load@linux
# systemctl enable kexec-load@linux-lts

```

#### Separate /boot partition

The above systemd unit file will fail if /boot is not on the root file system, as systemd will likely unmount /boot before it runs the kexec-load unit file. An alternative approach is to load a "hook" unit file that does nothing on startup and invokes kexec upon termination. By making this unit file conflict with kexec.target and only kexec.target, you can ensure the new kernel gets loaded early enough and only after a "systemctl kexec" command. Here is an alternate `/etc/systemd/system/kexec-load@.service` file that follows this strategy:

```
[Unit]
Description=hook to load vmlinuz-%i kernel upon kexec
Documentation=man:kexec(8)
DefaultDependencies=no
Requires=sysinit.target
After=sysinit.target

[Service]
Type=oneshot
ExecStart=-/usr/bin/true
RemainAfterExit=yes
ExecStop=/usr/bin/kexec -l /boot/vmlinuz-%i --initrd=/boot/initramfs-%i.img --reuse-cmdline

[Install]
WantedBy=basic.target
```

Note that Conflicts=shutdown.target is not really needed, as it's implicitly guaranteed by strict ordering on systinit.target which itself Conflicts= with shutdown.target.

## Troubleshooting

### System hangs or reboots after "kexec_core: Starting new kernel"

In this case, the troubleshooting information on [General troubleshooting#Boot problems](/index.php/General_troubleshooting#Boot_problems "General troubleshooting") may be helpful for diagnosing the problem.

In particular, if adding the `acpi=off` kernel parameter makes kexec work correctly, adding the `acpi_rsdp` kernel parameter on the kexec command line as explained in [[1]](https://github.com/coreos/bugs/issues/167) may solve the issue [in some cases](https://bbs.archlinux.org/viewtopic.php?id=219878) without the need to completely disable ACPI.

## See also

*   [[systemd-devel] Right way to do kexec](http://lists.freedesktop.org/archives/systemd-devel/2012-March/004760.html)
*   [kdump: a kexec based crash dumping mechansim for Linux](http://lse.sourceforge.net/kdump/)
*   [Reboot Linux faster using kexec](https://web.archive.org/web/20090505132901/http://www.ibm.com/developerworks/linux/library/l-kexec.html)