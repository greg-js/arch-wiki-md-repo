## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Iniciar desde el CD de instalación](#Iniciar_desde_el_CD_de_instalaci.C3.B3n)
*   [3 Chroot a tu partición raíz](#Chroot_a_tu_partici.C3.B3n_ra.C3.ADz)
*   [4 Volver a la versión anterior del Kernel](#Volver_a_la_versi.C3.B3n_anterior_del_Kernel)
*   [5 Reiniciando](#Reiniciando)

## Introducción

Esta página describe como volver a una versión del kernel anterior si la actual falla.

## Iniciar desde el CD de instalación

Bootea desde el CD de instalación. Cuando haya cargado, escribe arch, como harías cuando instalas arch.

```
# arch

```

## Chroot a tu partición raíz

Cuando ya hayas booteado, tendrás un pequeño pero funcional mini-entorno de trabajo. Ahora, debes montar tu partición raíz en /mnt:

```
# mount /dev/hdXY /mnt

```

Si usas una partición de booteo no olvides montarla:

```
# mount /dev/hdaXY /mnt/boot

```

Kernels nuevos usan un ramdisk inicial para acelerar su entorno. Cuando reinstalas un kernel, ese ramdisk inicial se regenerará con mkinitcpio. Una de las características de mkinitcpio es que hace una auto-detección para encontrar cuales son los módulos que cargan al inicio del sistema. Para que esta auto-detección funcione, /dev, /sys y /proc deben estar montados en tu chroot:

```
# mount -t proc none /mnt/proc
# mount -t sysfs none /mnt/sys
# mount --bind /dev /mnt/dev

```

Ahora haremos un chroot a este disco, así puedes usarlo como si tu PC hubiera booteado normalmente. Claro, muchas cosas no funcionarán.

```
# chroot /mnt

```

## Volver a la versión anterior del Kernel

Si dejas tus ficheros descargados del pacman, puedes volver fácilmente. Si no, deberás buscar una versión anterior del kernel de tu sistema ahora.

Supongamos que dejaste guardado el paquete. Lo instalaremos:

```
# pacman -U /var/cache/pacman/pkg/kernel26-<tt>VERSIÓN-ANTERIOR-DEL-KERNEL-ACTUAL</tt>.pkg.tar.gz

```

## Reiniciando

Ahora el kernel funcional esta instalado. Sal de chroot, desmonta las particiones y reinicia:

```
# cd /
# umount -a
# exit
# cd /
# umount -a
# reboot

```

No olvides visitar [el sitio oficial de Arch](https://www.archlinux.org/), y dirigirte a la parte de noticias, para ver que salió mal con esa versión del Kernel.