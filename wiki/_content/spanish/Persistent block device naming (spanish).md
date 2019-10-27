**Estado de la traducción**
Este artículo es una traducción de [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"), revisada por última vez el **2019-10-23**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Persistent_block_device_naming&diff=0&oldid=586928) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)")
*   [udev (Español)](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)")
*   [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)")

Este artículo describe cómo utilizar nombres permanentes para sus [dispositivos de bloques](/index.php/Block_device_(Espa%C3%B1ol) "Block device (Español)"). Esto ha sido posible gracias a la introducción de udev y tiene algunas ventajas sobre los nombres basados en el bus de conexión. Si el equipo tiene más de una controladora de disco SATA, SCSI o IDE, el orden en que se añaden sus correspondientes nodos de dispositivos es arbitraria. Esto puede dar lugar a nombres de dispositivos como `/dev/**sda**` y `/dev/**sdb**` alternando aleatoriamente en cada arranque, que puede terminar en una nominación de los dispositivos que impida el arranque del sistema, en pánico del kernel o en una desaparición del dispositivo de bloque. La nomenclatura permanente resuelve estos problemas.

**Nota:**

*   La nomenclatura persistente tiene límites que están fuera del alcance de este artículo. Por ejemplo, si bien [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") tiene soporte para cierto método, systemd puede imponer sus propios límites (por ejemplo, [FS#42884](https://bugs.archlinux.org/task/42884)) para nombrarlo, puediendo implementarlo durante el arranque.
*   Si está usando [LVM](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), este artículo no es relevante, dado que los volúmenes lógicos como `/dev/*NombredelGrupodeVolúmenes*/*NombredelVolumenLógico*`, las rutas del dispositivo son persistentes.

[https://wiki.archlinux.org/index.php](https://wiki.archlinux.org/index.php)?

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Métodos para nombrar los dispositivos de forma permanente](#Métodos_para_nombrar_los_dispositivos_de_forma_permanente)
    *   [1.1 by-label](#by-label)
    *   [1.2 by-uuid](#by-uuid)
    *   [1.3 by-id y by-path](#by-id_y_by-path)
    *   [1.4 by-partlabel](#by-partlabel)
    *   [1.5 by-partuuid](#by-partuuid)
    *   [1.6 Nombres estáticos de los dispositivos con udev](#Nombres_estáticos_de_los_dispositivos_con_udev)
*   [2 Utilizar nomenclatura permanente](#Utilizar_nomenclatura_permanente)
    *   [2.1 fstab](#fstab)
    *   [2.2 Parámetros del kernel](#Parámetros_del_kernel)

## Métodos para nombrar los dispositivos de forma permanente

Hay cuatro esquemas diferentes para nombrar de forma permanente los dispositivos: [by-label](#by-label), [by-uuid](#by-uuid), [by-id y by-path](#by-id_y_by-path). Para aquellos que utilizan discos con [tabla de particiones GUID (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table"), pueden usar dos esquemas adicionales [by-partlabel](#by-partlabel) y [by-partuuid](#by-partuuid). También puede utilizar [#Nombres estáticos de dispositivos con udev](#Nombres_estáticos_de_dispositivos_con_udev).

Los directorios en `/dev/disk/` se crean y destruyen dinámicamente, dependiendo de si hay dispositivos en ellos.

**Nota:** tenga en cuenta que la [clonación de discos](/index.php/Disk_cloning_(Espa%C3%B1ol) "Disk cloning (Español)") crea dos discos diferentes con el mismo nombre.

Las siguientes secciones describen lo que son y cómo se utilizan los diferentes métodos de asignación de nombres permanentes.

La orden [lsblk](/index.php/Lsblk_(Espa%C3%B1ol) "Lsblk (Español)") se puede utilizar para la visualización gráfica de los primeros esquemas de nombres persistentes:

 `$ lsblk -f` 
```
NAME        FSTYPE LABEL      UUID                                 MOUNTPOINT
sda                                                       
├─sda1      vfat              CBB6-24F2                            /boot
├─sda2      ext4   Arch Linux 0a3407de-014b-458b-b5c1-848e92a327a3 /
├─sda3      ext4   Data       b411dc99-f0a0-4c87-9e05-184977be8539 /home
└─sda4      swap              f9fe0b69-a280-415d-a03a-a32752370dee [SWAP]
mmcblk0
└─mmcblk0p1 vfat              F4CA-5D75

```

Para aquellos que utilizan [GPT](/index.php/GPT_(Espa%C3%B1ol) "GPT (Español)"), puede acudir a la orden `blkid`. Esta última es más eficiente para los scripts, pero más difícil de leer.

 `# blkid` 
```
/dev/sda1: UUID="CBB6-24F2" TYPE="vfat" PARTLABEL="EFI system partition" PARTUUID="d0d0d110-0a71-4ed6-936a-304969ea36af" 
/dev/sda2: LABEL="Arch Linux" UUID="0a3407de-014b-458b-b5c1-848e92a327a3" TYPE="ext4" PARTLABEL="GNU/Linux" PARTUUID="98a81274-10f7-40db-872a-03df048df366" 
/dev/sda3: LABEL="Data" UUID="b411dc99-f0a0-4c87-9e05-184977be8539" TYPE="ext4" PARTLABEL="Home" PARTUUID="7280201c-fc5d-40f2-a9b2-466611d3d49e" 
/dev/sda4: UUID="f9fe0b69-a280-415d-a03a-a32752370dee" TYPE="swap" PARTLABEL="Swap" PARTUUID="039b6c1c-7553-4455-9537-1befbc9fbc5b"
/dev/mmcblk0: PTUUID="0003e1e5" PTTYPE="dos"
/dev/mmcblk0p1: UUID="F4CA-5D75" TYPE="vfat" PARTUUID="0003e1e5-01"
```

### by-label

Casi todos los tipos de [sistemas de archivos](/index.php/File_systems_(Espa%C3%B1ol)#Tipos_de_sistemas_de_archivos "File systems (Español)") pueden tener una etiqueta. Todos los volúmenes que tienen una se enumeran en el directorio `/dev/disk/by-label`.

 `$ ls -l /dev/disk/by-label` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 Data -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 Arch\x20Linux -> ../../sda2

```

La mayoría de los sistemas de archivos admiten la configuración de etiquetas al crear el sistema de archivos, consulte la [página de manual](/index.php/Man_page_(Espa%C3%B1ol) "Man page (Español)") de la utilidad `mkfs.*`. Para algunos sistemas de archivos también es posible cambiar las etiquetas. Los siguientes son algunos métodos para cambiar etiquetas en sistemas de archivos comunes:

	swap 

	`swaplabel -L "*etiqueta nueva*" /dev/*XXX*` utilizando [util-linux](https://www.archlinux.org/packages/?name=util-linux)

	ext2/3/4 

	`e2label /dev/*XXX* "*etiqueta nueva*"` utilizando [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

	btrfs 

	`btrfs filesystem label /dev/*XXX* "*etiqueta nueva*"` utilizando [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

	reiserfs 

	`reiserfstune -l "*etiqueta nueva*" /dev/*XXX*` utilizando [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

	jfs 

	`jfs_tune -L "*etiqueta nueva*" /dev/*XXX*` utilizando [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

	xfs 

	`xfs_admin -L "*etiqueta nueva*" /dev/*XXX*` utilizando [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

	fat/vfat 

	`fatlabel /dev/*XXX* "*etiqueta nueva*"` utilizando [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

	`mlabel -i /dev/*XXX* ::"*etiqueta nueva*"` utilizando [mtools](https://www.archlinux.org/packages/?name=mtools)

	exfat 

	`exfatlabel /dev/*XXX* "*etiqueta nueva*"` utilizando [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

	ntfs 

	`ntfslabel /dev/*XXX* "*etiqueta nueva*"` utilizando [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

	udf 

	`udflabel /dev/*XXX* "*etiqueta nueva*"` utilizando [udftools](https://www.archlinux.org/packages/?name=udftools)

	crypto_LUKS (LUKS2 only) 

	`cryptsetup config --label="*etiqueta nueva*" /dev/*XXX*` utilizando [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup)

La etiqueta de un dispositivo se puede obtener con *lsblk*:

 `$ lsblk -dno LABEL /dev/sda2` 
```
Arch Linux

```

O con *blkid*:

 `# blkid -s LABEL -o value /dev/sda2` 
```
Arch Linux

```

**Nota:**

*   El sistema de archivos no debe estar montado para poder cambiar su etiqueta. Para el sistema de archivos raíz, esto se puede lograr arrancando desde otro volumen.
*   Las etiquetas tienen que ser inequívocas (sin ambigüedades) para evitar posibles conflictos.
*   Las etiquetas pueden tener una longitud de hasta 16 caracteres.
*   Dado que la etiqueta es una propiedad del sistema de archivos, no es adecuada para direccionar hacia un único dispositivo RAID de forma persistente.
*   Cuando se usan contenedores cifrados con [dm-crypt](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)"), las etiquetas de los sistemas de archivos dentro de los contenedores no estarán disponibles mientras el contenedor esté bloqueado/cifrado.

### by-uuid

[UUID](https://en.wikipedia.org/wiki/es:Universally_unique_identifier de un identificador único. Estos identificadores son generados por las utilidades del sistema de archivos (por ejemplo, `mkfs.*`) cuando la partición se formatea y se ha diseñado de manera que evite conflictos. Todos los sistemas de archivos de GNU/Linux (incluyendo swap y las cabeceras LUKS de dispositivos cifrados en bruto) soportan UUID. Los sistemas de archivos FAT, exFAT y NTFS no son compatibles con UUID, pero todavía se enumeran en `/dev/disk/by-uuid` con un UID más corto (identificador único):

 `$ ls -l /dev/disk/by-uuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 0a3407de-014b-458b-b5c1-848e92a327a3 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 b411dc99-f0a0-4c87-9e05-184977be8539 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 CBB6-24F2 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 f9fe0b69-a280-415d-a03a-a32752370dee -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 F4CA-5D75 -> ../../mmcblk0p1

```

El UUID de un dispositivo se puede obtener con *lsblk*:

 `$ lsblk -dno UUID /dev/sda1` 
```
CBB6-24F2

```

O con *blkid*:

 `# blkid -s UUID -o value /dev/sda1` 
```
CBB6-24F2

```

La ventaja de usar el método UUID es que es mucho menos probable que se produzcan colisiones de nombres que con las etiquetas. Además, se genera automáticamente en la creación del sistema de archivos. Será, por ejemplo, el único indicador, incluso si el dispositivo está conectado a otro sistema (el cual, tal vez, puede tener un dispositivo con la misma etiqueta).

La desventaja es que UUID hace largas líneas de código difícil de leer y rompe el formato en muchos archivos de configuración (por ejemplo [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") o [crypttab](/index.php/Dm-crypt_(Espa%C3%B1ol)/System_configuration_(Espa%C3%B1ol)#crypttab_(Español) "Dm-crypt (Español)/System configuration (Español)")). También, cada vez que un volumen se redimensiona o reformatea, se genera un nuevo UUID y los archivos de configuración tienen que volver a ajustarse manualmente.

**Sugerencia:** en caso de que su partición de intercambio no tenga un UUID asignado, tendrá que restablecer la partición de swap usando la utilidad [mkswap](/index.php/Swap_(Espa%C3%B1ol)#Partición_swap "Swap (Español)").

### by-id y by-path

`by-id` crea un nombre único en función del número de serie del hardware, `by-path` crea un nombre único en función de la ruta física más corta (de acuerdo con sysfs). Ambos contienen cadenas para indicar el subsistema al que pertenecen (es decir, `pci-` para `by-path`, y `ata-` para `by-id`) de modo que están vinculados al hardware que controla el dispositivo. Esto implica diferentes niveles de persistencia: `by-path` cambiará cuando el dispositivo se conecte a un puerto diferente del controlador; `by-id` cambiará cuando se conecte el dispositivo en un puerto de un controlador de hardware sujeto a otro subsistema. [[1]](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/persistent_naming.html) Por lo tanto, ninguno de los dos son adecuados para lograr nombres persistentes tolerantes a los cambios de hardware.

Sin embargo, ambos proporcionan información importante para encontrar un dispositivo en particular en una gran infraestructura de hardware. Por ejemplo, si no se asignan manualmente etiquetas persistentes (`by-label` o `by-partlabel`) y se mantiene un directorio con utilización de puerto de hardware, `by-id` y `by-path` pueden ser utilizados para encontrar un dispositivo en particular. [[2]](http://linuxshellaccount.blogspot.in/2008/09/how-to-easily-find-wwns-of-qlogic-hba.html) [[3]](http://www.linuxquestions.org/questions/linux-server-73/how-to-find-wwn-for-dev-sdc-917269/)

`by-id` también crea enlaces a [nombres a nivel mundial](https://en.wikipedia.org/wiki/es:World_Wide_Name "wikipedia:es:World Wide Name") (siglas en inglés World Wide Name) de los dispositivos de almacenamiento que lo admitan. A diferencia de otros enlaces `by-id`, WWNs son completamente persistentes y no cambiarán al margen del subsistema utilizado.

 `$ ls -l /dev/disk/by-id/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470 -> ../../sda
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part1 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part2 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part3 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part4 -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 mmc-SD32G_0x0040006d -> ../../mmcblk0
lrwxrwxrwx 1 root root 10 May 27 23:31 mmc-SD32G_0x0040006d-part1 -> ../../mmcblk0p1
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f -> ../../sda
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part1 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part2 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part3 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part4 -> ../../sda4

```
 `$ ls -l /dev/disk/by-path/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1 -> ../../sda
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part1 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part2 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part3 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part4 -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:07:00.0-platform-rtsx_pci_sdmmc.0 -> ../../mmcblk0
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:07:00.0-platform-rtsx_pci_sdmmc.0-part1 -> ../../mmcblk0p1

```

### by-partlabel

**Nota:** este método solo se refiere a los discos con [tabla de particiones GUID (GPT)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)").

Las etiquetas de partición GPT se pueden definir en el encabezado de la [entrada de la partición](https://en.wikipedia.org/wiki/es:Tabla_de_particiones_GUID#Entradas_de_partici.C3.B3n_.28LBAs_2_al_33.29 "wikipedia:es:Tabla de particiones GUID") en discos GPT.

Este método es muy similar al de las [etiquetas de los sistemas de archivos](#by-label), excepto que las etiquetas de la partición no se ven afectadas si se cambia el sistema de archivos en la partición.

Todas las particiones que tienen etiquetas de partición se enumeran en el directorio `/dev/disk/by-partlabel`.

 `ls -l /dev/disk/by-partlabel/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 EFI\x20system\x20partition -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 GNU\x2fLinux -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 Home -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 Swap -> ../../sda4

```

La etiqueta de partición de un dispositivo se puede obtener con *lsblk*:

 `$ lsblk -dno PARTLABEL /dev/sda1` 
```
EFI system partition

```

O con *blkid*:

 `# blkid -s PARTLABEL -o value /dev/sda1` 
```
EFI system partition

```

**Nota:**

*   Las etiquetas de las particiones GPT también tienen que ser diferentes para evitar conflictos. Para cambiar la etiqueta de una partición, puede utilizar [gdisk](/index.php/Gdisk "Gdisk") o la versión basada en ncurse [cgdisk](/index.php/Cgdisk "Cgdisk"). Ambas utilidades están disponibles en el paquete [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk). Vea [Partitioning (Español)#Herramientas de particionado](/index.php/Partitioning_(Espa%C3%B1ol)#Herramientas_de_particionado "Partitioning (Español)").
*   De acuerdo con la especificación, las etiquetas de las particiones GPT pueden tener hasta 72 caracteres de longitud.

### by-partuuid

Al igual que con las [etiquetas de particiones GPT](#by-partlabel), el UUID de la partición se define en la [entrada de la partición](https://en.wikipedia.org/wiki/es:Tabla_de_particiones_GUID#Entradas_de_partici.C3.B3n_.28LBAs_2_al_33.29 "wikipedia:es:Tabla de particiones GUID") en discos GPT.

MBR no admite UUID de las particiones, pero Linux[[4]](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=d33b98fc82b0908e91fb05ae081acaed7323f9d2) y el software que utiliza libblkid[[5]](https://git.kernel.org/pub/scm/utils/util-linux/util-linux.git/commit/?id=d67cc2889a0527b26d7bb8c76f2acac46751d673) (por ejemplo, udev[[6]](https://github.com/systemd/systemd/pull/3293)) son capaces de generar pseudo PARTUUID para particiones MBR. El formato es `*SSSSSSSS*-*PP*`, donde `*SSSSSSSS*` es una [firma de disco MBR](https://en.wikipedia.org/wiki/es:Registro_de_arranque_principal#MBR_e_identificaci.C3.B3n_de_los_discos "wikipedia:es:Registro de arranque principal") de 32 bits llena de ceros, y `*PP*` es un número de partición lleno de ceros en formato hexadecimal. A diferencia de un PARTUUID normal de una partición GPT, el pseudo PARTUUID de MBR puede cambiar si cambia el número de la partición.

El directorio dinámico es similar al de los otros métodos y, al igual que con el [UUID de los sistemas de archivos](#by-uuid), el uso del UUID de las particiones es preferido sobre el de las etiquetas.

 `ls -l /dev/disk/by-partuuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 0003e1e5-01 -> ../../mmcblk0p1
lrwxrwxrwx 1 root root 10 May 27 23:31 039b6c1c-7553-4455-9537-1befbc9fbc5b -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 7280201c-fc5d-40f2-a9b2-466611d3d49e -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 98a81274-10f7-40db-872a-03df048df366 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 d0d0d110-0a71-4ed6-936a-304969ea36af -> ../../sda1

```

La partición UUID de un dispositivo se puede obtener con *lsblk*:

 `$ lsblk -dno PARTUUID /dev/sda1` 
```
d0d0d110-0a71-4ed6-936a-304969ea36af

```

O con*blkid*:

 `# blkid -s PARTUUID -o value /dev/sda1` 
```
d0d0d110-0a71-4ed6-936a-304969ea36af

```

### Nombres estáticos de los dispositivos con udev

Véase [Udev (Español)#Configurar nombres estáticos para los dispositivos](/index.php/Udev_(Espa%C3%B1ol)#Configurar_nombres_estáticos_para_los_dispositivos "Udev (Español)").

## Utilizar nomenclatura permanente

Existen varias aplicaciones que se pueden configurar mediante el uso la nomenclatura permanente. Los siguientes son algunos ejemplos de cómo configurarlos.

### fstab

Ver el artículo principal: [fstab (Español)#Identificación de los sistemas de archivos](/index.php/Fstab_(Espa%C3%B1ol)#Identificación_de_los_sistemas_de_archivos "Fstab (Español)").

### Parámetros del kernel

Para usar nombres persistentes en los [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"), se deben cumplir los siguientes requisitos previos. En una instalación estándar, que sigue la guía de instalación, se cumplen los dos requisitos previos:

*   Está utilizando una imagen de disco RAM inicial de [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Configuración "Mkinitcpio (Español)")
*   Tiene activado el hook de udev o de systemd en `/etc/mkinitcpio.conf`

La ubicación del sistema de archivos raíz viene dada por el parámetro `root` en la línea de órdenes del kernel. La línea de órdenes del kernel se configura desde el [gestor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)"), consulte [Kernel parameters (Español)#Configuración](/index.php/Kernel_parameters_(Espa%C3%B1ol)#Configuración "Kernel parameters (Español)"). Para cambiar a nombres de dispositivo persistentes, basta con cambiar los parámetros que identifican los dispositivos de bloque, por ejemplo, `root` y `resume`, dejando otros parámetros tal como están. Se admiten varios esquemas de nomenclatura:

El nombre persistente del dispositivo [utilizando etiquetas](#by-label) y el formato `LABEL=`, en este ejemplo `Arch Linux` es la ETIQUETA del sistema de archivos raíz.

```
root="LABEL=Arch Linux"

```

El nombre persistente del dispositivo [utilizando UUID](#by-uuid) y el formato `UUID=`, en este ejemplo `0a3407de-014b-458b-b5c1-848e92a327a3`, es el UUID del sistema de archivos raíz.

```
root=UUID=0a3407de-014b-458b-b5c1-848e92a327a3

```

El nombre persistente del dispositivo [utilizando el id del disco](#by-id_y_by-path) y el formato de ruta `/dev`, en este ejemplo `wwn-0x60015ee0000b237f-part2`, es el identificador de la partición raíz.

```
root=/dev/disk/by-id/wwn-0x60015ee0000b237f-part2

```

El nombre persistente del dispositivo [utilizando el UUID de la partición GPT](#by-partuuid) y el formato `PARTUUID=`, en este ejemplo `98a81274-10f7-40db-872a-03df048df366`, es el PARTLABEL de la partición raíz.

```
root=PARTUUID=98a81274-10f7-40db-872a-03df048df366

```

El nombre persistente del dispositivo [utilizando la etiqueta de la partición GPT](#by-partlabel) y el formato `PARTLABEL=`, en este ejemplo `GNU/Linux`, es el PARTLABEL de la partición raíz.

```
root="PARTLABEL=GNU/Linux"

```