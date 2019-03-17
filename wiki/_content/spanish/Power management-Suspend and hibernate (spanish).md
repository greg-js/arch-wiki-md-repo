Artículos relacionados

*   [Uswsusp](/index.php/Uswsusp "Uswsusp")
*   [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [Power management](/index.php/Power_management "Power management")

Actualmente hay tres métodos de suspensión disponibles: **suspender en RAM** (llamado solo **suspender**), **suspender en disco** (conocido como **hibernar**) y **suspensión híbrida** (a veces llamado **suspender a ambos**):

*   **Suspender en RAM**: Este método corta la corriente en muchas partes del sistema excepto de la RAM, que es necesaria para restaurar el estado de la máquina, de ahí el gran ahorro energético. Es recomendable para los portátiles que entre en este modo automáticamente cuando el ordenador esta consumiendo baterías y la pantalla está cerrada (o el usuario está inactivo por un periodo de tiempo).

*   **Suspender en disco**: Este método guarda el estado de la máquina en [espacio swap](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)") y apaga completamente la máquina. Cuando la máquina se enciende el estado se restaura. Hasta entonces no hay consumo de energía.

*   **Suspensión híbrida**: Este método guarda el estado en el espacio swap, pero no apaga la máquina. En su lugar, invoca un suspender en RAM. De esta forma si la batería no se agota, el sistema puede continuar desde RAM. Si se agota, el sistema puede continuar desde el disco, que es más lento que continuar desde RAM, pero el estado de la máquina no se pierde.

Hay varias interfaces de bajo nivel (backends) que proporcionan una funcionalidad básica y varias interfaces de alto nivel que proporcionan retoques para encargarse de los controladores de hardware problemáticos/módulos kernel (p.ej. reinicialización de la tarjeta de vídeo).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Interfaces de bajo nivel](#Interfaces_de_bajo_nivel)
    *   [1.1 Núcleo (swsusp)](#Núcleo_(swsusp))
    *   [1.2 Uswsusp](#Uswsusp)
*   [2 Interfaces de alto nivel](#Interfaces_de_alto_nivel)
    *   [2.1 Systemd](#Systemd)
*   [3 Hibernation](#Hibernation)
    *   [3.1 About swap partition/file size](#About_swap_partition/file_size)
    *   [3.2 Required kernel parameters](#Required_kernel_parameters)
        *   [3.2.1 Hibernation into swap file](#Hibernation_into_swap_file)
    *   [3.3 Configure the initramfs](#Configure_the_initramfs)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 ACPI_OS_NAME](#ACPI_OS_NAME)
    *   [4.2 VAIO users](#VAIO_users)
    *   [4.3 Suspend/hibernate doesn't work, or not consistently](#Suspend/hibernate_doesn't_work,_or_not_consistently)
    *   [4.4 Wake-on-LAN](#Wake-on-LAN)
    *   [4.5 Instantaneous wakeups from suspend](#Instantaneous_wakeups_from_suspend)
    *   [4.6 System does not power off when hibernating](#System_does_not_power_off_when_hibernating)

## Interfaces de bajo nivel

Aunque estas interfaces se pueden usar directamente es aconsejable que se utilice alguna [interfaz de alto nivel](#Interfaces_de_alto_nivel) para suspender/hibernar. Utilizar interfaces de bajo nivel es significativamente más rápido que utilizar las interfaces de alto nivel, ya que ejecutar los pre y post hooks lleva tiempo, pero estos hooks pueden establecer apropiadamente el reloj hardware, restaurar las redes inalámbricas, etc.

### Núcleo (swsusp)

Lo más directo es informar directamente al núcleo (kernel) el código de suspensión del software para cambiar a un estado de suspensión (swsusp); el método exacto y el estado depende del nivel que soporta el hardware. En los núcleos modernos, el principal mecanismo para lanzar esta suspensión es escribir las apropiadas instrucciones en `/sys/power/state`.

vea la [documentación del kernel (en inglés)](https://www.kernel.org/doc/Documentation/power/states.txt) para más detalles.

### Uswsusp

La suspensión de software de espacio de usuario ('uswsusp') es un envoltorio del mecanismo de suspensión a RAM del núcleo que realiza algunas manipulaciones del adaptador gráfico desde el espacio de usuario antes de suspender y después de reanudar. Vea el articulo del manual [Uswsusp](/index.php/Uswsusp "Uswsusp").

## Interfaces de alto nivel

El objetivo de estos paquetes es proporcionar script/binarios que puedan invocar y realizar la suspensión/hibernación. En realidad los enlaces a los botones de encendido o a los clic en un menú o a los eventos de la tapa de un portátil se les deja a otras herramientas. Para suspender/hibernar automáticamente en ciertos eventos de energía, como el cierre de la tapa del ordenador o bajo porcentaje de batería puede que estés buscando ejecutar [Acpid (Español)](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)").

### Systemd

[Systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") proporciona de forma nativa comandos para suspender, hibernar y suspender de forma híbrida, vea [administración de energía con systemd (en inglés)](/index.php/Power_management#Power_management_with_systemd "Power management") para más detalles. Esta es la interfaz por defecto usada en Arch Linux.

Vea [sleep hooks](/index.php/Power_management_(Espa%C3%B1ol)#Sleep_hooks "Power management (Español)") como información adicional para configurar los hook de suspensión/hibernación. Vea también [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1), [systemd-sleep(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.8), y [systemd.special(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.special.7).

## Hibernation

In order to use hibernation, you need to create a [swap](/index.php/Swap "Swap") partition or file. You will need to point the kernel to your swap using the `resume=` kernel parameter, which is configured via the boot loader. You will also need to [configure the initramfs](#Configure_the_initramfs). This tells the kernel to attempt resuming from the specified swap in early userspace. These three steps are described in detail below.

**Note:** See [Dm-crypt/Swap encryption#With suspend-to-disk support](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption") when using [encryption](/index.php/Encryption "Encryption").

### About swap partition/file size

Even if your swap partition is smaller than RAM, you still have a big chance of hibernating successfully. According to [kernel documentation](https://www.kernel.org/doc/Documentation/power/interface.txt):

	*`/sys/power/image_size` controls the size of the image created by the suspend-to-disk mechanism. It can be written a string representing a non-negative integer that will be used as an upper limit of the image size, in bytes. The suspend-to-disk mechanism will do its best to ensure the image size will not exceed that number. However, if this turns out to be impossible, it will try to suspend anyway using the smallest image possible. In particular, if "0" is written to this file, the suspend image will be as small as possible. Reading from this file will display the current image size limit, which is set to 2/5 of available RAM by default.*

You may either decrease the value of `/sys/power/image_size` to make the suspend image as small as possible (for small swap partitions), or increase it to possibly speed up the hibernation process.

See [Systemd#Temporary files](/index.php/Systemd#Temporary_files "Systemd") to make this change persistent.

### Required kernel parameters

The kernel parameter `resume=*swap_partition*` has to be used. Either the name the kernel assigns to the partition or its [UUID](/index.php/UUID "UUID") can be used as `*swap_partition*`. For example:

*   `resume=/dev/sda1`
*   `resume=UUID=4209c845-f495-4c43-8a03-5363dd433153`
*   `resume=/dev/archVolumeGroup/archLogicVolume` -- example if using LVM

Generally, the naming method used for the `resume` parameter should be the same as used for the `root` parameter.

The configuration depends on the used [boot loader](/index.php/Boot_loader "Boot loader"), refer to [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for details.

#### Hibernation into swap file

**Warning:** [Btrfs](/index.php/Btrfs#Swap_file "Btrfs") on Linux kernel before version 5.0 does not support swap files. Failure to heed this warning may result in file system corruption. While a swap file may be used on Btrfs when mounted through a loop device, this will result in severely degraded swap performance.

Using a swap file instead of a swap partition requires an additional kernel parameter `resume_offset=*swap_file_offset*`.

The value of `*swap_file_offset*` can be obtained by running `filefrag -v *swap_file*`, the output is in a table format and the required value is located in the first row of the `physical_offset` column. For example:

 `# filefrag -v /swapfile` 
```
Filesystem type is: ef53
File size of /swapfile is 4294967296 (1048576 blocks of 4096 bytes)
 ext:     logical_offset:        physical_offset: length:   expected: flags:
   0:        0..       0:      38912..     38912:      1:            
   1:        1..   22527:      38913..     61439:  22527:             unwritten
   2:    22528..   53247:     899072..    929791:  30720:      61440: unwritten
...

```

In the example the value of `*swap_file_offset*` is the first `38912` with the two periods.

**Tip:** The following command may be used to identify `*swap_file_offset*`: `filefrag -v /swapfile | awk '{ if($1=="0:"){print $4} }'`.

**Note:**

*   Before the first hibernation, a reboot is required to activate the feature.
*   The value of `*swap_file_offset*` can also be obtained by running `swap-offset *swap_file*`. The *swap-offset* binary is provided within the set of tools [uswsusp](/index.php/Uswsusp "Uswsusp"). If using this method, then these two parameters have to be provided in `/etc/suspend.conf` via the keys `resume device` and `resume offset`. No reboot is required in this case.

**Tip:** You might want to decrease the [Swap#Swappiness](/index.php/Swap#Swappiness "Swap") for your swapfile if the only purpose is to be able to hibernate and not expand RAM.

### Configure the initramfs

*   When an [initramfs](/index.php/Initramfs "Initramfs") with the `base` hook is used, which is the default, the `resume` hook is required in `/etc/mkinitcpio.conf`. Whether by label or by UUID, the swap partition is referred to with a udev device node, so the `resume` hook must go *after* the `udev` hook. This example was made starting from the default hook configuration:

	 `HOOKS=(base udev autodetect keyboard modconf block filesystems **resume** fsck)` 

	Remember to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") for these changes to take effect.

**Note:** [LVM](/index.php/LVM "LVM") users should add the `resume` hook after `lvm2`.

*   When an initramfs with the `systemd` hook is used, a resume mechanism is already provided, and no further hooks need to be added.

## Troubleshooting

### ACPI_OS_NAME

You might want to tweak your **DSDT table** to make it work. See [DSDT](/index.php/DSDT "DSDT") article

### VAIO users

Add the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `acpi_sleep=nonvs` to your bootloader.

### Suspend/hibernate doesn't work, or not consistently

There have been many reports about the screen going black without easily viewable errors or the ability to do anything when going into and coming back from suspend and/or hibernate. These problems have been seen on both laptops and desktops. This is not an official solution, but switching to an older kernel, especially the LTS-kernel, will probably fix this.

Also problem may arise when using hardware watchdog timer (disabled by default, see `RuntimeWatchdogSec=` in [systemd-system.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-system.conf.5#OPTIONS)). Bugged watchdog timer may reset the computer before the system finished creating the hibernation image.

Sometimes the screen goes black due to device initialization from within the initramfs. Removing any modules you might have in [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") and rebuilding the initramfs, can possibly solve this issue, specially graphics drivers for [early KMS](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"). Initializing such devices before resuming can cause inconsistencies that prevents the system resuming from hibernation. This does not affect resuming from RAM. Also, check the blog article [best practices to debug suspend issues](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues).

For Intel graphics drivers, enabling early KMS may help to solve the blank screen issue. Refer to [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for details.

After upgrading to kernel 4.15.3, resume may fail with a static (non-blinking) cursor on a black screen. [Blacklisting](/index.php/Blacklisting "Blacklisting") the module `nvidiafb` might help. [[1]](https://bbs.archlinux.org/viewtopic.php?id=234646)

### Wake-on-LAN

If [Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") is active, the network interface card will consume power even if the computer is hibernated.

### Instantaneous wakeups from suspend

For some Intel Haswell systems with the LynxPoint and LynxPoint-LP chipset, instantaneous wakeups after suspend are reported. They are linked to erroneous BIOS ACPI implementations and how the `xhci_hcd` module interprets it during boot. As a work-around reported affected systems are added to a blacklist (named `XHCI_SPURIOUS_WAKEUP`) by the kernel case-by-case.[[2]](https://bugzilla.kernel.org/show_bug.cgi?id=66171#c6)

Instantaneous resume may happen, for example, if a USB device is plugged during suspend and ACPI wakeup triggers are enabled. A viable work-around for such a system, if it is not on the blacklist yet, is to disable the wakeup triggers. An example to disable wakeup through USB is described as follows.[[3]](https://bbs.archlinux.org/viewtopic.php?pid=1575617)

To view the current configuration:

 `$ cat /proc/acpi/wakeup` 
```
Device  S-state   Status   Sysfs node
...
EHC1      S3    *enabled  pci:0000:00:1d.0
EHC2      S3    *enabled  pci:0000:00:1a.0
XHC       S3    *enabled  pci:0000:00:14.0
...

```

The relevant devices are `EHC1`, `EHC2` and `XHC` (for USB 3.0). To toggle their state you have to echo the device name to the file as root.

```
# echo EHC1 > /proc/acpi/wakeup
# echo EHC2 > /proc/acpi/wakeup
# echo XHC > /proc/acpi/wakeup

```

This should result in suspension working again. However, this settings are only temporary and would have to be set at every reboot. To automate this take a look at [systemd#Writing unit files](/index.php/Systemd#Writing_unit_files "Systemd"). See [BBS thread](https://bbs.archlinux.org/viewtopic.php?pid=1575617#p1575617) for a possible solution and more information.

If you use `nouveau` driver, the reason of instantaneous wakeup may be a bug in that driver, which sometimes prevents graphics card from suspension. One possible workaround is unloading `nouveau` kernel module right before going to sleep and loading it back after wakeup. To do this, create the following script:

 `/usr/lib/systemd/system-sleep/10-nouveau.sh` 
```
#!/bin/bash

case $1/$2 in
  pre/*)
    # echo "Going to $2..."
    /usr/bin/echo "0" > /sys/class/vtconsole/vtcon1/bind
    /usr/bin/rmmod nouveau
    ;;
  post/*)
    # echo "Waking up from $2..."
    /usr/bin/modprobe nouveau
    /usr/bin/echo "1" > /sys/class/vtconsole/vtcon1/bind
    ;;
esac
```

The first echo line unbinds nouveaufb from the framebuffer console driver (fbcon). Usually it is `vtcon1` as in this example, but it may also be another `vtcon*`. See `/sys/class/vtconsole/vtcon*/name` which one of them is a "frame buffer device" [[4]](https://nouveau.freedesktop.org/wiki/KernelModeSetting/).

### System does not power off when hibernating

When you hibernate your system, the system should power off (after saving the state on the disk). Sometimes, you might see the power LED is still glowing. If that happens, it might be instructive to set the `HibernateMode` to `shutdown` in [sleep.conf.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sleep.conf.d.5):

 `/etc/systemd/sleep.conf.d/hibernatemode.conf` 
```
[Sleep]
HibernateMode=shutdown
```

With the above configuration, if every thing else is setup correctly, on invocation of a `systemctl hibernate` the machine will shutdown saving state to disk as it does so.