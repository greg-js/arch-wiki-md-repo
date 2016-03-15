Este articulo tiene el propósito de guiar a través de los pasos llevados acabo para reinstalar el cargador de arranque si este deja de trabajar correctamente. Para los propósitos de este articulo, se asume que `/dev/sda3` es la partición raíz del sistema Arch Linux y que `/dev/sda1` es la partición de arranque. Este articulo mostrara los pasos utilizados para los cargadores de arranque GRUB y LILO. Se debe leer el las páginas wiki de GRUB y LILO para asegurarse que se sabe lo que se está haciendo. Recuerda que la recuperación del cargador de arranque no es más que reinstalar el programa en el MBR (Master Boot Record) en el disco duro.

## Contents

*   [1 Sencillo](#Sencillo)
    *   [1.1 Obtener el CD de inicio de Arch Linux](#Obtener_el_CD_de_inicio_de_Arch_Linux)
    *   [1.2 Iniciar con el CD de Arch Linux](#Iniciar_con_el_CD_de_Arch_Linux)
    *   [1.3 Corrigiendo el grub/lilo](#Corrigiendo_el_grub.2Flilo)
*   [2 Complicado](#Complicado)

## Sencillo

### Obtener el CD de inicio de Arch Linux

Descargar o utilizar el CD base de Arch Linux ([obtener Arch Linux](https://www.archlinux.org/download/))

### Iniciar con el CD de Arch Linux

Iniciar normalmente el sistema con el cd de Arch Linux

en el momento de las opciones de arranque indicar:

```
arch root=/dev/sda3  

```

Esto significa que el cd de instalación/rescate cargara su propio kernel, pero utilizara **/dev/sda3** como el directorio raíz. Esencialmente, se esta ejecutando el sistema que esta en tu disco duro.

### Corrigiendo el grub/lilo

Ahora hacerlo como usuario root:

para corregir el grub:

```
grub-install /dev/sda

```

para corregir el lilo:

```
/sbin/lilo -v

```

## Complicado

Algunas veces, recuperar el MBR no podría ser una simple cuestión de reinstalar el cargador de arranque. Es posible que existiera algo mal con la forma en que el sistema fue configurado y esto llevo a que el cargador de arranque fallara. En este caso, es probable que ni siquiera pueda utilizarse el disco de instalación/rescate para arrancar en la partición raíz del disco duro. En este caso solo se puede iniciar el cd de instalación/rescate normalmente (sin proporcionar la opción `root=`) y entonces manualmente montar la partición raíz.

```
arch

```

Y entonces, montar las particiones de disco manualmente.

```
mount /dev/sda3 /mnt
mount /dev/sda1 /mnt/boot

```

Incluso se pueden montar los directorios *especiales*. Esto sera necesario si se requiere reinstalar el kernel, por ejemplo.

```
mount --bind /dev/ /mnt/dev
mount --bind /proc /mnt/proc
mount --bind /sys /mnt/sys

```

Tambien se puede considerar copiar el archivo **/etc/mtab**, para haver un chroot en la nueva partición raíz montada.

```
cp /etc/mtab /mnt/etc
chroot /mnt

```

Y finalmente, ejecutar el comando **install-grub**, **grub-install**, o **lilo** para instalar el cargador de arranque en el MBR.