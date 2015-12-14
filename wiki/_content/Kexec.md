# Kexec

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Systemd](/index.php/Systemd "Systemd")

**Kexec** is a system call that enables you to load and boot into another kernel from the currently running kernel. This is useful for kernel developers or other people who need to reboot very quickly without waiting for the whole BIOS boot process to finish. Note that kexec may not work correctly for you due to devices _not_ fully re-initializing when using this method, however this is rarely the case.

## Contents

*   [1 Installation](#Installation)
*   [2 Rebooting using kexec](#Rebooting_using_kexec)
    *   [2.1 Systemd](#Systemd)
        *   [2.1.1 Separate /boot partition](#Separate_.2Fboot_partition)
    *   [2.2 Manually](#Manually)
*   [3 See also](#See_also)

## Installation

To install kexec, [install](/index.php/Install "Install") the [kexec-tools](https://www.archlinux.org/packages/?name=kexec-tools) package which is available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Rebooting using kexec

### Systemd

You will need to create a new unit file, `kexec-load@.service`, that will load the specified kernel to be kexec'ed:

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
RequiresMountsFor=/boot/vmlinuz-%i
Conflicts=kexec.target

[Service]
Type=oneshot
ExecStart=-/usr/bin/true
RemainAfterExit=yes
ExecStop=/usr/bin/kexec -l /boot/vmlinuz-%i --initrd=/boot/initramfs-%i.img --reuse-cmdline

[Install]
WantedBy=basic.target
```

Unfortunately, while the above file works reliably on some machines, the ExecStop command seems to fail to run on others. Hence, at present there does not appear to be a known reliable way to make "systemctl kexec" do the right thing on all machines. Until then, it may be best to call kexec manually before invoking "systemctl kexec" (or even "reboot", which will do the right thing when a kernel is loaded).

### Manually

It is also perfectly legal to invoke kexec manually:

```
# kexec -l /boot/vmlinuz-linux --initrd=/boot/initramfs-linux.img --reuse-cmdline
# kexec -e

```

**Warning:** Running `kexec -e` directly will not unmount active filesystemd or terminate any running services gracefully.

It is also possible to load kernel manually and then let systemd handle service shutdown and kexec for you:

```
# kexec -l /boot/vmlinuz-linux --initrd=/boot/initramfs-linux.img --reuse-cmdline
# systemctl kexec

```

## See also

*   [[systemd-devel] Right way to do kexec](http://lists.freedesktop.org/archives/systemd-devel/2012-March/004760.html)
*   [kdump: a kexec based crash dumping mechansim for Linux](http://lse.sourceforge.net/kdump/)
*   [Reboot Linux faster using kexec](https://web.archive.org/web/20090505132901/http://www.ibm.com/developerworks/linux/library/l-kexec.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kexec&oldid=412115](https://wiki.archlinux.org/index.php?title=Kexec&oldid=412115)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Boot process](/index.php/Category:Boot_process "Category:Boot process")
*   [Kernel](/index.php/Category:Kernel "Category:Kernel")