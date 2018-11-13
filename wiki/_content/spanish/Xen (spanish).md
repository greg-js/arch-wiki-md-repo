Esta página explica como instalar Xen en Arch Linux.

## Contents

*   [1 Que es Xen?](#Que_es_Xen?)
*   [2 Instalando Xen](#Instalando_Xen)
    *   [2.1 Consiguiendo los paquetes necesarios](#Consiguiendo_los_paquetes_necesarios)
    *   [2.2 Configurando GRUB](#Configurando_GRUB)
    *   [2.3 Configurando GRUB2](#Configurando_GRUB2)
    *   [2.4 Agregando un domU](#Agregando_un_domU)
    *   [2.5 Virtualización por Hardware](#Virtualización_por_Hardware)
*   [3 Arch como huésped de Xen (modo PV)](#Arch_como_huésped_de_Xen_(modo_PV))
    *   [3.1 xe-guest-utilities](#xe-guest-utilities)
    *   [3.2 Notas](#Notas)
*   [4 Administrando Xen](#Administrando_Xen)
*   [5 Paquetes Útiles](#Paquetes_Útiles)
*   [6 Enlaces Externos](#Enlaces_Externos)

## Que es Xen?

Según el equipo de desarrollo de Xen: "Xen Hypervisor, la solución para virtualización open source estándar del mercado, ofrece un poderoso, eficiente, y seguro conjunto de características para la virtualización de x86, x86_64, IA64, PowerPC, y otras arquitecturas. Soporta una amplia gama de sistemas operativos huéspedes, incluyendo Windows®, Linux®, Solaris®, y sistemas basados en BSD."

Xen es una capa delgada de software que emula una arquitectura de computadora. Comienza a funcionar desde el cargador de arranque y permite correr simultáneamente varios sistemas operativos sobre el. Una vez cargado el hipervisor Xen, éste arranca el "dom0" (dominio 0), o dominio privilegiado, que en nuestro caso corre un kernel modificado de Linux (otros sistemas como NetBSD y OpenSolaris tambien son capaces de alojar el dom0). El [kernel dom0](https://aur.archlinux.org/packages.php?ID=29023) que está disponible en AUR, está basado en una version reciente del kernel 2.6 de linux. Hay [una version -dev más inestable](https://aur.archlinux.org/packages.php?ID=38175) tambien; para el que el hardware debe, obviamente, estar soportado por este kernel para correr Xen. Después de que el dom0 halla arrancado, uno o más dominios "domU" (sin privilegios) pueden ser ejecutados y administrados desde dom0.

## Instalando Xen

### Consiguiendo los paquetes necesarios

Antes de trabajar con el paquete xen, debemos estar seguros de que tenemos gcc, make, patch, y python2 instalados.

 `pacman -S gcc make patch python2` 

El nuevo paquete xen, contiene Xen 4 y resuelve la mayoría de sus dependencias automáticamente. Pero debido a que la versión 3 de Python ahora es la oficial de Arch Linux, algunos scripts antiguos de Xen producen errores al ser ejecutados. Para solucionar este problema, descargamos python2.5 desde AUR:

 `yaourt -S xen python25` 

Al momento de editar el PKGBUILD de Xen (preferentemente con nano), no debemos olvidar reemplazar las lineas:

```
make PYTHON=python2 DESTDIR=$pkgdir  install-xen
make PYTHON=python2 DESTDIR=$pkgdir  install-tools
make PYTHON=python2 DESTDIR=$pkgdir  install-docs
```

por:

```
make PYTHON=python2.5 DESTDIR=$pkgdir  install-xen
make PYTHON=python2.5 DESTDIR=$pkgdir  install-tools
make PYTHON=python2.5 DESTDIR=$pkgdir  install-docs

sed -i -e "s|#![ ]*/usr/bin/python$|#!/usr/bin/python2.5|" \
-e "s|#![ ]*/usr/bin/env python$|#!/usr/bin/env python2.5|" \
$(find $pkgdir -name '*.py')
```

Xen-tools es una colección de simples scripts de perl que permiten crear facilmente nuevos dominios huéspedes de Xen. Si es que lo necesitas, tambien está disponible en AUR.

 `yaourt -S xen-tools` 

El siguiente paso es compilar e instalar el kernel dom0\. Para hacer eso, vamos a construir el paquete kernel26-xen-dom0 desde AUR.

 `yaourt -S kernel26-xen-dom0` 

**Importante:** Actualmente, la versión de kernel26-xen-dom0 es 2.6.32.15, y hasta entonces no ha sido puesto al día con los nuevos kernels. Lo más recomendable, es pasar por alto los parámetros correspondientes a las nuevas versiones y usar los valores por defecto del paquete - A partir de ahi, apretamos enter cada vez que se nos pida.

La etapa de instalación termina aquí. Ahora vamos a configurar Grub para arrancar en el kernel que acabamos de compilar.

### Configurando GRUB

Grub debe ser configurado de tal manera que el hipervisor Xen arranque seguido por el kernel dom0\. Agregaremos la siguiente entrada al archivo /boot/grub/menu.lst:

```
title Xen con Arch Linux
root (hd0,X)
kernel /xen.gz dom0_mem=524288
module /vmlinuz26-xen-dom0 root=/dev/sdaY ro console=tty0
module /kernel26-xen-dom0.img

```

En donde X e Y son los números correspondientes a nuestra configuración de disco; y dom0_mem, console, y vga son parámetros opcionales y personalizables. Pequeño Detalle: podemos usar volúmenes LVM también. Entonces, en vez de /dev/sdaY podriamos poner /dev/mapper/númerodelvm.

El kernel estándar de arch puede ser usado para arrancar domU's. Para lograr esto, debemos agregar 'xen-blkfront' a los modules de /etc/mkinitcpio.conf:

```
MODULES="... xen-blkfront ..."

```

Una vez que reiniciamos, y arrancamos en el kernel xen, tenemos que iniciar xend:

```
# /etc/rc.d/xend start

```

Asignar una cantidad de fija de memoria es la mejor opción a la hora de usar xen. Además, si estamos corriendo huéspedes con una actividad de E/S intensiva, es una buena idea dedicar (pin) un núcleo del CPU únicamente para uso de dom0\. Para mas información, visitar la sección "Can I dedicate a cpu core (or cores) only for dom0?" de [XenCommonProblems](http://wiki.xensource.com/xenwiki/XenCommonProblems).

### Configurando GRUB2

Se hace de la misma manera que en Grub, pero en este caso, necesitamos usar el comando 'multiboot' en vez de usar 'kernel'. Un ejemplo podría ser:

```
# (2) Arch Linux(XEN)
menuentry "Arch Linux(XEN)" {
    set root=(hd0,X)
    multiboot /boot/xen.gz dom0_mem=2048M
    module /boot/vmlinuz26-xen-dom0 root=/dev/sdaY ro
    module /boot/kernel26-xen-dom0.gz
}

```

Si ya pudimos arrancar en el kernel dom0, podemos continuar.

### Agregando un domU

La idea básica detrás de agregar un domU es la siguiente. Necesitamos conseguir los kernels domU, asignar espacio para el disco virtual, crear un archivo de configuración para el domU, y finalmente arrancarlo con xm.

```
$ mkfs.ext4 /dev/sdb1    ## format partition
$ mkdir /tmp/install
$ mount /dev/sdb1 /tmp/install
$ mkdir -p /tmp/install/dev /tmp/install/proc /tmp/install/sys /tmp/install/var/lib/pacman /tmp/install/var/cache/pacman/pkg /tmp/install/var/lib/pacman
$ mount -o bind /dev /tmp/install/dev
$ mount -t proc none /tmp/install/proc
$ mount -o bind /sys /tmp/install/sys
$ pacman -Sy -r /tmp/install --cachedir /tmp/install/var/cache/pacman/pkg -b /tmp/install/var/lib/pacman base
$ cp -r /etc/pacman* /tmp/install/etc
$ chroot /tmp/install /bin/bash
$ vi /etc/resolv.conf
$ vi /etc/fstab
    /dev/xvda               /           ext4    defaults                0       1

$ vi /etc/inittab
    c1:2345:respawn:/sbin/agetty -8 38400 hvc0 linux
    #c1:2345:respawn:/sbin/agetty -8 38400 tty1 linux
    #c2:2345:respawn:/sbin/agetty -8 38400 tty2 linux
    #c3:2345:respawn:/sbin/agetty -8 38400 tty3 linux
    #c4:2345:respawn:/sbin/agetty -8 38400 tty4 linux
    #c5:2345:respawn:/sbin/agetty -8 38400 tty5 linux
    #c6:2345:respawn:/sbin/agetty -8 38400 tty6 linux

$ exit  ## exit chroot
$ umount /tmp/install/dev
$ umount /tmp/install/proc
$ umount /tmp/install/sys
$ umount /tmp/install

```

Si no estamos arrancado desde una instalación fresca y queremos usar rsync con un sistema operativo preexistente:

```
$ mkfs.ext4 /dev/sdb1    ## format lv partition
$ mkdir /tmp/install
$ mount /dev/sdb1 /tmp/install
$ mkdir /tmp/install/{proc,sys}
$ chmod 555 /tmp/install/proc
$ rsync -avzH --delete --exclude=proc/ --exclude=sys/ old_ooga:/ /tmp/install/

$ vi /etc/xen/dom01     ## create config file
    #  -*- mode: python; -*-
    kernel = "/boot/vmlinuz26"
    ramdisk = "/boot/kernel26.img"
    memory = 1024
    name = "dom01"
    vif = [ 'mac=00:16:3e:00:01:01' ]
    disk = [ 'phy:/dev/sdb1,xvda,w' ]
    dhcp="dhcp"
    hostname = "ooga"
    root = "/dev/xvda ro"

$ xm create -c dom01

```

### Virtualización por Hardware

Si queremos tener virtualización por hardware en nuestros dominios huéspedes, el hardware del sistema anfitrión debe soportar la tecnología de virtualización Intel-VT o AMD-V (si el procesador es Intel o Amd, respectivamente). Para comprobar esto, ejecutamos el siguiente comando en un terminal del sistema anfitrión:

Para procesadores Intel:

 `grep vmx /proc/cpuinfo` 

Para procesadores AMD:

 `grep svm /proc/cpuinfo` 

Si ninguno de los comandos mencionados devuelven una respuesta, quiere decir que el hardware del sistema anfitrión no dispone de esa tecnología y por lo tanto seremos incapaces de correr huéspedes Xen con virtualización por hardware. Tambien es posible que el procesador soporte una de esas tecnologías, pero que ha sido deshabilitada desde el BIOS. En ese caso, accedemos al menú de configuración del BIOS del sistema anfitrión y buscamos una opción que esté relacionada con soporte para virtualización. Si encontramos esa opción y esta deshabilitada, la habilitamos, luego reiniciamos y volvemos a ejecutar los comandos en un terminal para saber si ya tenemos soporte para virtualización por hardware.

## Arch como huésped de Xen (modo PV)

Para llevar a cabo la paravirtualización tenemos que instalar:

*   [kernel26-xen](https://aur.archlinux.org/packages.php?ID=16087)
*   (opcional) [xe-guest-utilities](https://aur.archlinux.org/packages/xe-guest-utilities/)

Cambiamos al modo PV por comandos (en dom0):

```
 xe vm-param-set uuid=<vm uuid> HVM-boot-policy=""
 xe vm-param-set uuid=<vm uuid> PV-bootloader=pygrub

```

Editamos /boot/grub/menu.lst y agregamos kernel26-xen:

```
 # (1) Arch Linux (domU)
 title  Arch Linux (domU)
 root   (hd0,0)
 kernel /boot/vmlinuz26-xen root=/dev/xvda1 ro console=hvc0
 initrd /boot/kernel26-xen.img

```

Agregamos los siguientes módulos de Xen a nuestro initcpio, añadiendo los siguientes módulos a MODULES en /etc/mkinitcpio.conf: "xen-blkfront xen-fbfront xenfs xen-netfront xen-kbdfront" y reconstruimos nuestro initcpio:

```
 mkinitcpio -p kernel26-xen

```

Descomentamos la siguiente línea en /etc/inittab para habilitar el login por console:

```
 h0:2345:respawn:/sbin/agetty -8 38400 hvc0 linux

```

### xe-guest-utilities

Para usar xe-guest-utilities, agregamos el punto de montaje xenfs al archivo /etc/fstab:

```
 xenfs                  /proc/xen     xenfs     defaults            0      0

```

y añadimos 'xe-linux-distribution' a la sección DAEMONS de /etc/rc.conf.

### Notas

*   pygrub no tiene un menú de arranque.
*   Para evitar mensajes de error de hwclock, debemos establecer HARDWARECLOCK="xen" en /etc/rc.conf (actualmente, alcanza con usar cualquier valor que no sea "UTC" o "localtime")
*   Si necesitamos volver a la HVM, establecemos HVM-boot-policy="BIOS order".
*   Si se presenta un mensaje 'kernel panic' en el arranque de Xen y éste sugiere 'use apic="debug" and send an error report', podemos intentar agregar 'noapic' a la línea del kernel en menu.lst

## Administrando Xen

"Virtual Machine Manager" es una interfaz gráfica que permite al usuario manejar maquinas virtuales, que presenta una vista resumida de los dominios que están en marcha, su rendimiento en vivo y estadísticas sobre su utilización de recursos. La vista detallada muestra el rendimiento y la utilización a lo largo del tiempo. Posee un asistente que permite la creación de nuevos dominios, y configurar la asignación de recursos y el hardware virtual de los mismos. Tambien, cuenta con un cliente VNC integrado que presenta una completa consola gráfica del dominio huésped.

 `yaourt -S virt-manager-light` 

## Paquetes Útiles

En AUR, hay una pequeña cantidad de paquetes que pueden sernos útiles si se tienen en cuenta, en la siguiente lista se encuentran algunos de los más interesantes (Actualizado: 23/05/2010)

*   Clón multiplataforma de código abierto de la interfaz de XenCenter: [openxencenter](https://aur.archlinux.org/packages.php?ID=34398)
*   Clón multiplataforma de código abierto de la interfaz de XenCenter (versión svn): [openxencenter-svn](https://aur.archlinux.org/packages.php?ID=36074)
*   Interfaz de la plataforma Xen Cloud: [xvp](https://aur.archlinux.org/packages/xvp/)

## Enlaces Externos

*   Web Oficial de Xen: [[1]](http://www.xen.org/)
*   La Wiki Xen: [[2]](http://wiki.xensource.com/xenwiki/)
*   Parches Xen para el kernel: [[3]](http://code.google.com/p/gentoo-xen-kernel/)
*   Virtuatopia - Virtualizando Windows Server 2008 con Xen: [[4]](http://www.virtuatopia.com/index.php/Virtualizing_Windows_Server_2008_with_Xen)