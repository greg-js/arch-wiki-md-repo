**Estado de la traducción**
Este artículo es una traducción de [Device file](/index.php/Device_file "Device file"), revisada por última vez el **2019-01-23**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Device_file&diff=0&oldid=564483) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

De [Wikipedia](https://en.wikipedia.org/wiki/es:Archivo_de_dispositivo "wikipedia:es:Archivo de dispositivo"):

	En sistemas operativos similares a Unix, un archivo de dispositivo o un archivo especial es una interfaz a un controlador de dispositivo que aparece en un sistema de archivos como si fuera un archivo normal.

En Linux están en el directorio `/dev`, de acuerdo con el [Estándar de jerarquía del sistema de archivos](https://en.wikipedia.org/wiki/es:Filesystem_Hierarchy_Standard "wikipedia:es:Filesystem Hierarchy Standard").

En Arch Linux los nodos del dispositivo son gestionados por [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Dispositivos de bloque](#Dispositivos_de_bloque)
    *   [1.1 lsblk](#lsblk)
    *   [1.2 wipefs](#wipefs)
*   [2 Pseudo-dispositivos](#Pseudo-dispositivos)
*   [3 Véase también](#Véase_también)

## Dispositivos de bloque

Los [dispositivos de bloque](https://en.wikipedia.org/wiki/es:Archivo_de_dispositivo#Dispositivos_orientados_a_bloques "wikipedia:es:Archivo de dispositivo") proporcionan acceso en búfer a dispositivos de hardware y permite la lectura y escritura de bloques de cualquier tamaño y alineación.

El comienzo del nombre del dispositivo especifica el tipo de dispositivo de bloque. La mayoría de los dispositivos de almacenamiento modernos (por ejemplo, discos duros, [SSD](/index.php/SSD "SSD") y unidades flash USB) se reconocen como discos [SCSI](https://en.wikipedia.org/wiki/SCSI *existentes* en cada dispositivo se mostrarán con un número que comienza desde `1` para la primera partición (`sda1`), `2` para la segunda (`sda2`), y así sucesivamente. Otros tipos de dispositivos de bloque comunes incluyen, por ejemplo, `mmcblk` para tarjetas de memoria y `nvme` para dispositivos [NVMe](/index.php/NVMe "NVMe").

Véase también [Nombrado persistente de dispositivos de bloque](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)").

### lsblk

El paquete [util-linux](https://www.archlinux.org/packages/?name=util-linux) proporciona la utilidad [lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) que lista dispositivos de bloque, por ejemplo:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

En el ejemplo anterior, solo hay un dispositivo disponible (`sda`), y ese dispositivo tiene tres particiones (de `sda1` a `sda3`), cada uno con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") diferente.

### wipefs

*wipefs* puede listar o borrar las firmas de [sistemas de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)"), [RAID](/index.php/RAID "RAID") o la [tabla de particiones](/index.php/Partition_(Espa%C3%B1ol) "Partition (Español)") (cadenas mágicas) del dispositivo especificado para hacer las firmas invisibles para [libblkid(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libblkid.3). No borra los sistemas de archivos ni los datos del dispositivo.

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