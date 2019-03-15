**Estado de la traducción**
Este artículo es una traducción de [Device file](/index.php/Device_file "Device file"), revisada por última vez el **2019-03-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Device_file&diff=0&oldid=568683) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Nombrado de dispositivo de bloque persistente](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)")

De [Wikipedia](https://en.wikipedia.org/wiki/es:Archivo_de_dispositivo "wikipedia:es:Archivo de dispositivo"):

	En sistemas operativos similares a Unix, un archivo de dispositivo o un archivo especial es una interfaz a un controlador de dispositivo que aparece en un sistema de archivos como si fuera un archivo normal.

En Linux están en el directorio `/dev`, de acuerdo con el [Estándar de jerarquía del sistema de archivos](https://en.wikipedia.org/wiki/es:Filesystem_Hierarchy_Standard "wikipedia:es:Filesystem Hierarchy Standard").

En Arch Linux los nodos del dispositivo son gestionados por [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Dispositivos de bloque](#Dispositivos_de_bloque)
    *   [1.1 Nombres de dispositivos de bloque](#Nombres_de_dispositivos_de_bloque)
        *   [1.1.1 SCSI](#SCSI)
        *   [1.1.2 NVME](#NVME)
        *   [1.1.3 MMC](#MMC)
        *   [1.1.4 Unidad de disco óptico SCSI](#Unidad_de_disco_óptico_SCSI)
    *   [1.2 Utilidades](#Utilidades)
        *   [1.2.1 lsblk](#lsblk)
        *   [1.2.2 wipefs](#wipefs)
*   [2 Pseudo-dispositivos](#Pseudo-dispositivos)
*   [3 Véase también](#Véase_también)

## Dispositivos de bloque

Los [dispositivos de bloque](https://en.wikipedia.org/wiki/es:Archivo_de_dispositivo#Dispositivos_orientados_a_bloques "wikipedia:es:Archivo de dispositivo") proporciona acceso en búfer a dispositivos de hardware y permite la lectura y escritura de bloques de cualquier tamaño y alineación.

### Nombres de dispositivos de bloque

El comienzo del nombre del dispositivo especifica el subsistema del controlador utilizado por el kernel para operar el dispositivo de bloque.

**Advertencia:** Los descriptores de nombre del kernel para dispositivos de bloque no son [persistentes](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)") y pueden cambiar en cada arranque, por lo que no deben utilizarse en archivos de configuración.

#### SCSI

Los dispositivos de almacenamiento, como discos duros, [SSD](/index.php/SSD "SSD") y unidades USB, que soporten las [órdenes SCSI](https://en.wikipedia.org/wiki/es:SCSI_Command "wikipedia:es:SCSI Command") ([SCSI](https://en.wikipedia.org/wiki/es:SCSI "wikipedia:es:SCSI"), [SAS](https://en.wikipedia.org/wiki/es:Serial_Attached_SCSI "wikipedia:es:Serial Attached SCSI"), [UASP](https://en.wikipedia.org/wiki/USB_Attached_SCSI "wikipedia:USB Attached SCSI")), ATA ([PATA](https://en.wikipedia.org/wiki/es:Parallel_ATA "wikipedia:es:Parallel ATA"), [SATA](https://en.wikipedia.org/wiki/es:Serial_ATA "wikipedia:es:Serial ATA")) o [USB de almacenamiento masivo](https://en.wikipedia.org/wiki/es:Clase_de_dispositivo_de_almacenamiento_masivo_USB "wikipedia:es:Clase de dispositivo de almacenamiento masivo USB") son gestionados por el subsistema SCSI del kernel. Todos ellos comparten el mismo esquema de nombres.

El nombre de estos dispositivos comienza con `sd`. Luego le sigue una letra minúscula que comienza en `a` para el primer dispositivo descubierto (`sda`), `b` para el segundo dispositivo descubierto (`sdb` ), y así sucesivamente. Las [particiones](/index.php/Partition_(Espa%C3%B1ol) "Partition (Español)") existentes en cada dispositivo se mostrarán con el número que le es asignado en la tabla de particiones, por ejemplo `sda1` para la partición (`1`), `sda2` para la partición (`2`), y así sucesivamente.

Resumen:

*   `/dev/sda` - dispositivo `a`, el primer dispositivo descubierto.
*   `/dev/sda1` - partición `1` en el dispositivo `a`.
*   `/dev/sde` - dispositivo `e`, el quinto dispositivo descubierto.
*   `/dev/sde7` - partición `7` en el dispositivo `e`.

#### NVME

El nombre de los dispositivos de almacenamiento, como los [SSDs](/index.php/SSD "SSD"), que son conectados través de [NVM Express](/index.php/NVM_Express "NVM Express") (NVMe) comienza con `nvme`. Luego le sigue un número que comienza desde `0` para el controlador del dispositivo, `nvme0` para el primer controlador NVMe descubierto, `nvme1` para el segundo y así sucesivamente. Lo siguiente es la letra "n" y un número que comienza desde `1` que expresa el dispositivo en un controlador, es decir, `nvme0n1` para el primer dispositivo descubierto en el primer controlador descubierto, `nvme0n2` para el segundo dispositivo descubierto en el primer controlador descubierto, y así sucesivamente. Las [particiones](/index.php/Partition_(Espa%C3%B1ol) "Partition (Español)") existentes en cada dispositivo se mostrarán con la letra "p" y el número que le es asignado en la tabla de particiones. Por ejemplo, `nvme0n1p` para la partición con el número `1` en el primer dispositivo descubierto en el primer controlador descubierto, `nvme0n1p2` para la partición `2`, y así sucesivamente.

Resumen:

*   `/dev/nvme0n1` - dispositivo `1` en el controlador `0`, el primer dispositivo descubierto en el primer controlador descubierto.
*   `/dev/nvme0n1p1` - partición `1` en el dispositivo `1` en el controlador `0`.
*   `/dev/nvme2n5` - dispositivo `5` en el controlador `2`, el quinto dispositivo descubierto en el tercer controlador descubierto.
*   `/dev/nvme2n5p7` - partición `7` en el dispositivo `5` en el controlador `2`.

#### MMC

Las [tarjetas SD](https://en.wikipedia.org/wiki/es:Secure_Digital existentes en cada dispositivo se mostrarán con la letra "p" y el número que le es asignado en la tabla de particiones. La partición con el número `1` en la tabla de particiones sería `mmcblk0p1`, la partición con el número `2` sería `mmcblk0p2`, y así sucesivamente.

Resumen:

*   `/dev/mmcblk0` - dispositivo `0`, el primer dispositivo descubierto.
*   `/dev/mmcblk0p1` - partición `1` en el dispositivo `0`.
*   `/dev/mmcblk4` - dispositivo `4`, el quinto dispositivo descubierto.
*   `/dev/mmcblk4p7` - partición `7` en el dispositivo `4`.

#### Unidad de disco óptico SCSI

El nombre de [unidades de disco óptico](/index.php/Optical_disc_drive_(Espa%C3%B1ol) "Optical disc drive (Español)") (ODDs), que se conecta utilizando una de las interfaces compatibles con el subsistema del controlador [SCSI](#SCSI), comienza con `sr`. El nombre va seguido de un número que comienza desde `0` para el dispositivo, es decir. `sr0` para el primer dispositivo descubierto, `sr1` para el segundo dispositivo descubierto, y así sucesivamente.

[Udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") también proporciona `/dev/cdrom` que es un enlace simbólico a `/dev/sr0`. El nombre siempre será `cdrom` independientemente de los tipos de disco admitidos en la unidad o del medio insertado.

Resumen:

*   `/dev/sr0` - unidad de disco óptico `0`, la primera unidad de disco óptico descubierta.
*   `/dev/sr4` - unidad de disco óptico `4`, la quinta unidad de disco óptico descubierta.
*   `/dev/cdrom` - un enlace simbólico a `/dev/sr0`.

### Utilidades

#### lsblk

El paquete [util-linux](https://www.archlinux.org/packages/?name=util-linux) proporciona la utilidad [lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) que lista los dispositivos de bloque, por ejemplo:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

En el ejemplo anterior, solo hay un dispositivo disponible (`sda`), y ese dispositivo tiene tres particiones (de `sda1` a `sda3`), cada uno con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") diferente.

#### wipefs

*wipefs* puede listar o borrar las firmas de [sistemas de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)"), [RAID](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)") o la [tabla de particiones](/index.php/Partition_(Espa%C3%B1ol) "Partition (Español)") (cadenas mágicas) del dispositivo especificado para hacer las firmas invisibles para [libblkid(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libblkid.3). No borra los sistemas de archivos ni los datos del dispositivo.

Véase [wipefs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipefs.8) para más información.

Por ejemplo, para borrar todas las firmas del dispositivo `/dev/sdb` y crear un archivo con la copia de seguridad de la firma `~/wipefs-sdb-*offset*.bak` por cada firma:

```
# wipefs --all --backup /dev/sdb

```

## Pseudo-dispositivos

Son nodos de dispositivo que no tienen dispositivo físico.

*   [/dev/random](/index.php//dev/random "/dev/random"), véase [random(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/random.4)
*   [/dev/shm](/index.php//dev/shm_(Espa%C3%B1ol) "/dev/shm (Español)")
*   [/dev/null](https://en.wikipedia.org/wiki/es:/dev/null "wikipedia:es:/dev/null"), [/dev/zero](https://en.wikipedia.org/wiki/es:/dev/zero "wikipedia:es:/dev/zero"), véase [null(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/null.4)
*   [/dev/full](https://en.wikipedia.org/wiki/es:/dev/full "wikipedia:es:/dev/full"), véase [full(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/full.4)
*   [/dev/ttyX](/index.php//dev/ttyX "/dev/ttyX"), donde X es un número

## Véase también

*   [Dispositivos asignados de Linux — La documentación del kernel de Linux](https://www.kernel.org/doc/html/latest/admin-guide/devices.html)
*   [Gentoo:Device file](https://wiki.gentoo.org/wiki/Device_file "gentoo:Device file")