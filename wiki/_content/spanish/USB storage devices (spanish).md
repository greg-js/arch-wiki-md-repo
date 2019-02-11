Artículos relacionados

*   [Mount](/index.php/Mount "Mount")

Este documento describe cómo usar las populares memorias USB con Linux. No obstante, también es válido para otros dispositivos, como las cámaras digitales que actúan como si fueran meros dispositivos USB de almacenamiento.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Cargar el módulo "usb_storage" en el kernel](#Cargar_el_módulo_"usb_storage"_en_el_kernel)
*   [2 Montar la memoria USB](#Montar_la_memoria_USB)
*   [3 Reparticionar la memoria USB](#Reparticionar_la_memoria_USB)
*   [4 Montar el dispositivo USB como un usuario normal](#Montar_el_dispositivo_USB_como_un_usuario_normal)

## Cargar el módulo "usb_storage" en el kernel

Si no utiliza un kernel personalizado, ya puede comenzar, pues todos los kernel empaquetados para Arch están adecuadamente configurados. Si utiliza un kernel personalizado, asegúrese de que está compilado con "SCSI-Support", "SCSI-Disk-Support" y "usb_storage". Si utiliza el [][udev]] más reciente, puede simplemente insertar su dispositivo que el sistema se encargará de cargar automáticamente todos los módulos del kernel que sean necesarios. Algunas versiones más antiguas de udev necesitarían tener instalado también [hotplug](/index.php?title=HotPlug&action=edit&redlink=1 "HotPlug (page does not exist)"). Por otro lado, puede hacer lo mismo manualmente:

```
# modprobe usb-storage
# modprobe sd_mod      (sólo para los kernel sin SCSI)

```

## Montar la memoria USB

Después de insertar el dispositivo puede montarlo como root con

```
# mount -t vfat /dev/sda1 /mnt/usbstick

```

Nota: /dev/sda1 es variable. Si su disco duro está asignado a /dev/sda1, tendrá probablemente que utilizar /dev/sdb1\. Para comprobar dónde está su dispositivo USB, busque /dev/sd* en la salida de dmesg. Utilice lsusb para verificar que su dispositivo USB es efectivamente reconocido por el sistema, si se produce un error.

La opción -t especifica el tipo de sistema de archivos. Si el dispositivo está formateado como fat32 utilice entonces el parámetro vfat. Se supone por defecto que los dispositivos <tt>sdx</tt> están formateados como fat32, así que esta opción puede omitirse.

Nota: the directory you mount the stick into must exist before you issue the mount command.

If you use [KDE](/index.php/KDE "KDE") or [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), they should show you the inserted device right on your desktop so you don't need to mount it manually.

**Nota:** Si obtiene un mensaje de error como "Error org.freedesktop.DBus.Error.AccessDenied.", pruebe a añadir su usuario al grupo 'storage'.

## Reparticionar la memoria USB

A veces el dispositivo está dividido hasta un máximo de cuatro particiones, y Linux no puede leer nada. Para solucionar esto tiene que reparticionar el dispositivo con `fdisk`. Asegúrese de que no queda ningún archivo en el dispositivo (si lo utilizaba antes en Windows, Mac OS o lo que sea). Teclee:

```
# modprobe usb_storage
# fdisk /dev/sda

```

Elimine todas las particiones que aparezcan (*d* y número de la partición), cree una nueva partición con *n* (le sugiero que utilice una única partición), pulse *w* para escribir los cambios y salga.

Cree un sistema de ficheros en el dispositivo:

```
# mkfs.vfat /dev/sda1

```

Si no dispone de mkfs.vfat en su sistema use pacman para instalar dosfstools:

```
# pacman -S dosfstools

```

Ahora puede monrtarlo y desmontarlo como se mencionó anteriormente.

## Montar el dispositivo USB como un usuario normal

Si quiere que los usuarios sin privilegios de administrador sean capaces de montar dispositivos USB, añada la siguiente línea a su /etc/fstab file:

```
/dev/sda1 /mnt/usbstick vfat rw,noauto,async,user 0 0

```

Ahora, cualquier usuario puede montarlo con:

```
mount /mnt/usbstick

```

Y desmontarlo con:

```
umount /mnt/usbstick

```