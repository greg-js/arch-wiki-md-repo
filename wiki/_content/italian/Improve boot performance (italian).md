Incrementare la velocità di boot di un sistema riduce i tempi di attesa e significa conoscere meglio come certi files di sistema e scripts interagiscono gli uni con gli altri. Questo articolo prova ad aggregare vari metodi per migliorare i tempi di boot di un sistema Arch Linux.

## Contents

*   [1 Analizzare il processo di boot](#Analizzare_il_processo_di_boot)
    *   [1.1 systemd-analyze](#systemd-analyze)
    *   [1.2 Usare systemd-bootchart](#Usare_systemd-bootchart)
    *   [1.3 Usare bootchart2](#Usare_bootchart2)
*   [2 Compiling a custom kernel](#Compiling_a_custom_kernel)
*   [3 Early start for services](#Early_start_for_services)
*   [4 Staggered spin-up](#Staggered_spin-up)
*   [5 Filesystem mounts](#Filesystem_mounts)
*   [6 Initramfs](#Initramfs)
*   [7 Less output during boot](#Less_output_during_boot)
*   [8 See also](#See_also)

### Analizzare il processo di boot

#### systemd-analyze

Systemd fornisce una utilità chiamata `systemd-analyze` che permette di analizzare il proprio processo d'avvio al fine di evidenziare quali unità stanno causando rallentamenti nel processo di avvio stesso. E' possibile quindi ottimizzare il sistema tenendo conto di ciò.

Per vedere quanto tempo ha impiegato il boot del kernelspace e dello userspace, semplicemente si usi:

```
$ systemd-analyze

```

**Tip:**

*   Se si aggiunge l'hook `timestamp` al proprio `HOOKS` array in `/etc/[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").conf` e si ricostruisce l'initramfs con `mkinitcpio -p linux`, systemd-analyze è in grado di mostrare anche quanto tempo è passato nell'initramfs.
*   Se si fa il boot tramite[UEFI](/index.php/UEFI "UEFI") e si usa un boot loader che implementi systemds' [Boot Loader Interface](http://www.freedesktop.org/wiki/Software/systemd/BootLoaderInterface) (attualmente solo [Gummiboot](/index.php/Gummiboot "Gummiboot")), systemd-analyze può mostrare in aggiunta quanto tempo è trascorso nel firmware EFI firmware e nel boot loader stesso.

Per elencare le unità avviate, ordinate a seconda del tempo che impiegano ad avviarsi:

```
$ systemd-analyze blame

```

Si può inoltre creare un file SVG che descriva il processo di boot graficamente, similmente a [Bootchart](/index.php/Bootchart "Bootchart"):

```
$ systemd-analyze plot > plot.svg

```

#### Usare systemd-bootchart

Bootchart è stato implementato in systemd dal 17 Ottobre 2012, e si può utilizzarlo per il boot proprio come si farebbe con il bootchart originale. Aggiongere alla linea del kernel:

```
 initcall_debug printk.time=y init=/usr/lib/systemd/systemd-bootchart

```

#### Usare bootchart2

E' possibile usare una versione di bootchart per visualizzare la sequenza di boot. Da quando non è più possibile inserire un secondo "init" nel comando del kernel non c'è più la possibilità di usare alcuna configurazione standard di bootchart. Tuttavia il pacchetto [bootchart2](https://aur.archlinux.org/packages/bootchart2/) di [AUR](/index.php/AUR "AUR") nasce con un non documentato service di systemd. Dopo aver installato bootchart2 fare:

```
# systemctl enable bootchart

```

Leggere la [documentazione di bootchart](https://github.com/mmeeks/bootchart) per ulteriori dettagli sull'uso di questa versione di bootchart.

## Compiling a custom kernel

Compiling a custom kernel can reduce boot time and memory usage. Though with the standardization of the 64 bit architecture and the modular nature of the Linux kernel, these benefits may not be as great as expected. [Read more about compiling a kernel](/index.php/Kernel_Compilation "Kernel Compilation").

## Early start for services

One central feature of systemd is [D-Bus](/index.php/D-Bus "D-Bus") and socket activation. This causes services to be started when they are first accessed and is generally a good thing. However, if you know that a service (like [UPower](/index.php/UPower "UPower")) will always be started during boot, then the overall boot time might be reduced by starting it as early as possible. This can be achieved (if the service file is set up for it, which in most cases it is) by issuing:

```
# systemctl enable upower

```

This will cause systemd to start UPower as soon as possible, without causing races with the socket or D-Bus activation.

## Staggered spin-up

Some hardware implements [staggered spin-up](https://en.wikipedia.org/wiki/Spin-up#Staggered_spin-up "wikipedia:Spin-up"), which causes the OS to probe ATA interfaces serially, which can spin up the drives one-by-one and reduce the peak power usage. This slows down the boot speed, and on most consumer hardware provides no benefits at all since the drives will already spin-up immediately when the power is turned on. To check if SSS is being used:

```
$ dmesg | grep SSS

```

If it wasn't used during boot, there will be no output.

To disable it, add `libahci.ignore_sss=1` to the [kernel line](/index.php/Kernel_line "Kernel line").

## Filesystem mounts

Thanks to [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")'s `fsck` hook, you can avoid a possibly costly remount of the root partition by changing `ro` to `rw` on the kernel line and removing it from `/etc/fstab`. Options can be set with `rootflags=mount options...` on the kernel line. Remember to remove the entry from your /etc/fstab file, else the systemd-remount-fs.service will continue to try to apply those settings. Alternatively, one could try to mask that unit.

If btrfs is in use for the root filesystem, there is no need for a fsck on every boot like other filesystems. If this is the case, [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")'s `fsck` hook can be removed. You may also want to mask the `systemd-fsck-root.service`, or tell it not to fsck the root filesystem from the kernel command line using `fsck.mode=skip`. Without [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")'s `fsck` hook, systemd will still fsck any relevant filesystems with the `systemd-fsck@.service`

You can also remove API filesystems from `/etc/fstab`, as systemd will mount them itself (see `pacman -Ql systemd | grep '\.mount$'` for a list). It is not uncommon for users to have a /tmp entry carried over from sysvinit, but you may have noticed from the command above that systemd already takes care of this. Ergo, it may be safely removed.

Other filesystems like `/home` can be mounted with custom mount units. Adding `noauto,x-systemd.automount` will buffer all access to that partition, and will fsck and mount it on first access, reducing the number of filesystems it must fsck/mount during the boot process.

**Note:** this will make your `/home` filesystem type `autofs`, which is ignored by [mlocate](/index.php/Mlocate "Mlocate") by default. The speedup of automounting `/home` may not be more than a second or two, depending on your system, so this trick may not be worth it.

## Initramfs

As mentioned above, boot time can be decreased by slimming the kernel, thereby reducing the amount of data that must be loaded. This is also true for your initramfs (result of mkinitcpio), as this is loaded immediately after the kernel, and takes care of recognizing your root filesystem and mounting it. To boot, very little is actually needed and includes the storage bus, block device, and filesystem. Falconindy (Dave Reisner) has begrudgingly created a [short tutorial](http://blog.falconindy.com/articles/optmizing-bootup-with-mkinitcpio.html) on how to achieve this on his blog.

**Note:** If you are using anything that requires udev to be included in the initramfs (for example, lvm2, mdadm_udev, or even just specifying the filesystem label with `/dev/disk/by-label`), trying to strip down your initramfs will not be a worthwhile endeavor.

## Less output during boot

Change `verbose` to `quiet` on the bootloader's kernel line. For some systems, particularly those with an SSD, the slow performance of the TTY is actually a bottleneck, and so less output means faster booting.

## See also

*   [systemd](/index.php/Systemd "Systemd")
*   [e4rat](/index.php/E4rat "E4rat")
*   [udev](/index.php/Udev "Udev")
*   [Daemon](/index.php/Daemon "Daemon")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [Maximizing performance](/index.php/Maximizing_performance "Maximizing performance")
*   [Bootchart](/index.php/Bootchart "Bootchart") - Tool to assist in profiling the boot process
*   [Kexec](/index.php/Kexec "Kexec") - Tool to reboot very quickly without waiting for the whole BIOS boot process to finish.