**Estado de la traducción**
Este artículo es una traducción de [File systems](/index.php/File_systems "File systems"), revisada por última vez el **2019-03-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=File_systems&diff=0&oldid=566079) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)")
*   [Device file (Español)#lsblk](/index.php/Device_file_(Espa%C3%B1ol)#lsblk "Device file (Español)")
*   [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")
*   [fsck](/index.php/Fsck "Fsck")
*   [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)")
*   [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications")
*   [QEMU (Español)#Montaje de una partición dentro de una imagen de disco raw](/index.php/QEMU_(Espa%C3%B1ol)#Montaje_de_una_partición_dentro_de_una_imagen_de_disco_raw "QEMU (Español)")
*   [udev (Español)](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)")
*   [udisks](/index.php/Udisks "Udisks")
*   [umask (Español)](/index.php/Umask_(Espa%C3%B1ol) "Umask (Español)")
*   [USB storage devices (Español)](/index.php/USB_storage_devices_(Espa%C3%B1ol) "USB storage devices (Español)")

De [Wikipedia](https://en.wikipedia.org/wiki/es:Sistema_de_archivos "wikipedia:es:Sistema de archivos"):

	En informática, un sistema de archivos controla cómo se almacenan y recuperan los datos. Sin un sistema de archivos, la información colocada en un medio de almacenamiento sería una gran cantidad de datos sin una manera de decir dónde se detiene una información y comienza la siguiente. Al separar los datos en partes y darle a cada una un nombre, la información se aísla e identifica fácilmente. Tomando su nombre de la forma en que se nombran los sistemas de información en papel, cada grupo de datos se llama un «archivo». La estructura y las reglas lógicas utilizadas para administrar los grupos de información y sus nombres se denominan «sistema de archivos».

Las particiones individuales de la unidad se pueden configurar utilizando uno de los muchos y diferentes sistemas de archivos disponibles. Cada uno tiene sus propias ventajas, desventajas e idiosincrasias únicas. A continuación se ofrece una breve descripción de los sistemas de archivos compatibles; los enlaces son a páginas de Wikipedia que proporcionan mucha más información.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Tipos de sistemas de archivos](#Tipos_de_sistemas_de_archivos)
    *   [1.1 Journaling](#Journaling)
    *   [1.2 Sistemas de archivos basados ​​en FUSE](#Sistemas_de_archivos_basados_​​en_FUSE)
    *   [1.3 Sistemas de archivos apilables](#Sistemas_de_archivos_apilables)
    *   [1.4 Sistemas de archivos de solo lectura](#Sistemas_de_archivos_de_solo_lectura)
    *   [1.5 Sistemas de archivos agrupados (cluster)](#Sistemas_de_archivos_agrupados_(cluster))
*   [2 Identificar los sistemas de archivos existentes](#Identificar_los_sistemas_de_archivos_existentes)
*   [3 Crear un sistema de archivos](#Crear_un_sistema_de_archivos)
*   [4 Montar un sistema de archivos](#Montar_un_sistema_de_archivos)
    *   [4.1 Listar los sistemas de archivos montados](#Listar_los_sistemas_de_archivos_montados)
    *   [4.2 Desmontar un sistema de archivos](#Desmontar_un_sistema_de_archivos)
*   [5 Véase también](#Véase_también)

## Tipos de sistemas de archivos

Véase [filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5) para una visión general y [Wikipedia:es:Anexo:Comparación de sistemas de archivos](https://en.wikipedia.org/wiki/es:Anexo:Comparaci%C3%B3n_de_sistemas_de_archivos "wikipedia:es:Anexo:Comparación de sistemas de archivos") para una comparación detallada de características. Los sistemas de archivos soportados por el kernel están listados en `/proc/filesystems`.

| Sistema de archivos | Orden para crearlo | Utilidades de usuario | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) | Documentación del kernel [[2]](https://www.kernel.org/doc/Documentation/filesystems/) | Notas |
| [Btrfs](/index.php/Btrfs "Btrfs") | [mkfs.btrfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.btrfs.8) | [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | Sí | [btrfs.txt](https://www.kernel.org/doc/Documentation/filesystems/btrfs.txt) | [estado de su estabilidad](https://btrfs.wiki.kernel.org/index.php/Status) |
| [VFAT](/index.php/VFAT_(Espa%C3%B1ol) "VFAT (Español)") | [mkfs.fat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.fat.8) | [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | Sí | [vfat.txt](https://www.kernel.org/doc/Documentation/filesystems/vfat.txt) |
| [exFAT](https://en.wikipedia.org/wiki/es:exFAT "w:es:exFAT") | [mkexfatfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkexfatfs.8) | [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | Sí | N/D (basado en FUSE) |
| [F2FS](/index.php/F2FS "F2FS") | [mkfs.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.f2fs.8) | [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | Sí | [f2fs.txt](https://www.kernel.org/doc/Documentation/filesystems/f2fs.txt) | dispositivos basados ​​en flash |
| [ext3](/index.php/Ext3 "Ext3") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Sí ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext3.txt](https://www.kernel.org/doc/Documentation/filesystems/ext3.txt) |
| [ext4](/index.php/Ext4_(Espa%C3%B1ol) "Ext4 (Español)") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Sí ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext4.txt](https://www.kernel.org/doc/Documentation/filesystems/ext4.txt) |
| [HFS](https://en.wikipedia.org/wiki/es:Hierarchical_File_System "w:es:Hierarchical File System") | mkfs.hfsplus(8) | [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) | No | [hfs.txt](https://www.kernel.org/doc/Documentation/filesystems/hfs.txt) | sistema de archivos de [macOS](https://en.wikipedia.org/wiki/macOS "w:macOS") (8.x-10.12.x) |
| [JFS](/index.php/JFS "JFS") | [mkfs.jfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.jfs.8) | [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) | Sí ([base](https://www.archlinux.org/groups/x86_64/base/)) | [jfs.txt](https://www.kernel.org/doc/Documentation/filesystems/jfs.txt) |
| [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") | [mkfs.nilfs2(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.nilfs2.8) | [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils) | Sí | [nilfs2.txt](https://www.kernel.org/doc/Documentation/filesystems/nilfs2.txt) |
| [NTFS](/index.php/NTFS_(Espa%C3%B1ol) "NTFS (Español)") | [mkfs.ntfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.ntfs.8) | [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | Sí | N/D (basado en FUSE) | sistema de archivos de [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows "w:Microsoft Windows") |
| [Reiser4](/index.php/Reiser4 "Reiser4") | mkfs.reiser4(8) | [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) | No |
| [ReiserFS](https://en.wikipedia.org/wiki/es:ReiserFS "w:es:ReiserFS") | [mkfs.reiserfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.reiserfs.8) | [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) | Sí ([base](https://www.archlinux.org/groups/x86_64/base/)) |
| [UDF](https://en.wikipedia.org/wiki/es:Universal_Disk_Format "w:es:Universal Disk Format") | [mkfs.udf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.udf.8) | [udftools](https://www.archlinux.org/packages/?name=udftools) | Opcional | [udf.txt](https://www.kernel.org/doc/Documentation/filesystems/udf.txt) |
| [XFS](/index.php/XFS "XFS") | [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8) | [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) | Sí ([base](https://www.archlinux.org/groups/x86_64/base/)) | 

[xfs.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs.txt)
[xfs-delayed-logging-design.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-delayed-logging-design.txt)
[xfs-self-describing-metadata.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt)

 |
| [ZFS](/index.php/ZFS "ZFS") | [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/) | No | N/D ([OpenZFS](https://en.wikipedia.org/wiki/OpenZFS "w:OpenZFS") port) |

**Nota:** El kernel tiene su propio controlador NTFS (véase [ntfs.txt](https://www.kernel.org/doc/Documentation/filesystems/ntfs.txt)), pero tiene soporte limitado para escribir archivos.

### Journaling

Todos los sistemas de archivos anteriores con la excepción de ext2, FAT16/32, Btrfs and ZFS, utilizan [journaling](https://en.wikipedia.org/wiki/es:Journaling "wikipedia:es:Journaling"). Journaling proporciona tolerancia a fallos al registrar los cambios antes de que se confirmen en el sistema de archivos. En el caso de un fallo del sistema o de alimentación, estos sistemas de archivos son más rápidos para volver a estar en línea y es menos probable que se corrompan. El registro se realiza en un área dedicada del sistema de archivos.

No todas las técnicas Journaling son iguales. Ext3 y ext4 ofrecen data-mode journaling, que registra datos y metadatos, así como posibilidad de registrar solo los cambios de metadatos. Data-mode journaling viene con una penalización de velocidad y no está activada de forma predeterminada. Del mismo modo, [Reiser4](/index.php/Reiser4 "Reiser4") ofrece el llamado ["modelos de transacción"](https://reiser4.wiki.kernel.org/index.php/Reiser4_transaction_models), que incluye journaling puro (equivalente a data-mode journaling de ext4), aproximación a Copy-on-Write puro (equivalente al predeterminado de btrfs) y un enfoque combinado que alterna heurísticamente entre los dos anteriores.

**Nota:** Reiser4 no proporciona un equivalente al comportamiento de journaling predeterminado de ext4 (solo metadatos).

Los otros sistemas de archivos proporcionan ordered-mode journaling, que solo registra metadatos. Si bien todo journaling devolverá un sistema de archivos a un estado válido después de una caída, data-mode journaling ofrece la mayor protección contra la corrupción y la pérdida de datos. Sin embargo, existe un compromiso en el rendimiento del sistema, ya que data-mode journaling realiza dos operaciones de escritura: primero en el journal y luego en el disco. Al elegir el tipo de sistema de archivos, se debe considerar el equilibrio entre la velocidad del sistema y la seguridad de los datos.

Los sistemas de archivos basados ​​en copy-on-write, como Btrfs y ZFS, no tienen necesidad de usar el journal tradicional para proteger los metadatos, porque nunca se actualizan en el lugar. Aunque Btrfs todavía tiene un árbol de registro similar a journal, solo se utiliza para acelerar fdatasync/fsync.

### Sistemas de archivos basados ​​en FUSE

Véase [FUSE](/index.php/FUSE_(Espa%C3%B1ol) "FUSE (Español)").

### Sistemas de archivos apilables

*   **aufs** — Sistema de archivos de unificación multicapa avanzado, un sistema de archivos de unión basado en FUSE, una reescritura completa de Unionfs, fue rechazado de la línea principal de Linux y, en su lugar, OverlayFS se fusionó con el Kernel de Linux.

	[http://aufs.sourceforge.net](http://aufs.sourceforge.net) || [aufs](https://aur.archlinux.org/packages/aufs/)

*   **[eCryptfs](/index.php/ECryptfs "ECryptfs")** — El sistema de archivos de cifrado empresarial es un paquete de software de cifrado de disco para Linux. Se implementa como una capa de cifrado a nivel de sistema de archivos compatible con POSIX, con el objetivo de ofrecer una funcionalidad similar a la de GnuPG a nivel de sistema operativo.

	[http://ecryptfs.org](http://ecryptfs.org) || [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils)

*   **mergerfs** — Un sistema de archivos de unión basado en FUSE.

	[https://github.com/trapexit/mergerfs](https://github.com/trapexit/mergerfs) || [mergerfs](https://aur.archlinux.org/packages/mergerfs/)

*   **mhddfs** — Sistema de archivos FUSE Multi-HDD, un sistema de archivos de unión basado en FUSE.

	[http://mhddfs.uvw.ru](http://mhddfs.uvw.ru) || [mhddfs](https://aur.archlinux.org/packages/mhddfs/)

*   **[overlayfs](/index.php/Overlayfs "Overlayfs")** — OverlayFS es un servicio de sistema de archivos para Linux que implementa un montaje de unión para otros sistemas de archivos.

	[https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **Unionfs** — Unionfs es un servicio de sistema de archivos para Linux, FreeBSD y NetBSD que implementa un montaje de unión para otros sistemas de archivos.

	[http://unionfs.filesystems.org/](http://unionfs.filesystems.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **unionfs-fuse** — Una implementación de Unionfs en el espacio de usuario.

	[https://github.com/rpodgorny/unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) || [unionfs-fuse](https://www.archlinux.org/packages/?name=unionfs-fuse)

### Sistemas de archivos de solo lectura

*   **[SquashFS](https://en.wikipedia.org/wiki/es:SquashFS "wikipedia:es:SquashFS")** — SquashFS es un sistema de archivos comprimido de solo lectura. SquashFS comprime archivos, inodos y directorios, y admite tamaños de bloque de hasta 1 MB para una mayor compresión.

	[http://squashfs.sourceforge.net/](http://squashfs.sourceforge.net/) || [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools)

### Sistemas de archivos agrupados (cluster)

*   **[Ceph](/index.php/Ceph "Ceph")** — Unificado, sistema de almacenamiento distribuido diseñado para un excelente rendimiento, fiabilidad y escalabilidad.

	[https://ceph.com/](https://ceph.com/) || [ceph](https://www.archlinux.org/packages/?name=ceph)

*   **[Glusterfs](/index.php/Glusterfs "Glusterfs")** — Sistema de archivos agrupado capaz de escalar a varios peta-bytes.

	[https://www.gluster.org/](https://www.gluster.org/) || [glusterfs](https://www.archlinux.org/packages/?name=glusterfs)

*   **[IPFS](/index.php/IPFS "IPFS")** — Un protocolo de hipermedia de igual a igual *(peer-to-peer)* para que la web sea más rápida, segura y abierta. IPFS trata de reemplazar a HTTP y construir una mejor web para todos nosotros. Utiliza bloques para almacenar partes de un archivo, cada nodo de red almacena solo el contenido que le interesa, proporciona deduplicación, distribución, sistema escalable limitado solo por los usuarios. (actualmente en estado aplha)

	[https://ipfs.io/](https://ipfs.io/) || [go-ipfs](https://www.archlinux.org/packages/?name=go-ipfs)

*   **[MooseFS](https://en.wikipedia.org/wiki/MooseFS "wikipedia:MooseFS")** — MooseFS es un sistema de archivos distribuido en red de escalamiento horizontal tolerante a fallos, de alta disponibilidad y de alto rendimiento.

	[https://moosefs.com](https://moosefs.com) || [moosefs](https://www.archlinux.org/packages/?name=moosefs)

*   **[OpenAFS](/index.php/OpenAFS "OpenAFS")** — Implementación de código abierto del sistema de archivos distribuido AFS.

	[http://www.openafs.org](http://www.openafs.org) || [openafs](https://aur.archlinux.org/packages/openafs/)

*   **[OrangeFS](https://en.wikipedia.org/wiki/OrangeFS "wikipedia:OrangeFS")** — OrangeFS es un sistema de archivos de red de escalado horizontal diseñado para acceder de forma transparente al almacenamiento en disco multiservidor en paralelo. Ha optimizado el soporte de MPI-IO para aplicaciones paralelas y distribuidas. Simplifica el uso del almacenamiento paralelo no solo para clientes Linux, sino también para Windows, Hadoop y WebDAV. Compatible con POSIX. Parte del kernel de Linux desde la versión 4.6.

	[http://www.orangefs.org/](http://www.orangefs.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Sheepdog** — El sistema de almacenamiento de objetos distribuidos para servicios de volumen y contenedor. Gestiona los discos y nodos de forma inteligente.

	[https://sheepdog.github.io/sheepdog/](https://sheepdog.github.io/sheepdog/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — Tahoe Least-Authority Filesystem es un sistema de archivos libre y abierto, seguro, descentralizado, tolerante a fallos y distribuido de igual a igual.

	[https://tahoe-lafs.org/](https://tahoe-lafs.org/) || [tahoe-lafs](https://aur.archlinux.org/packages/tahoe-lafs/)

## Identificar los sistemas de archivos existentes

Para identificar los sistemas de archivos existentes, puede utilizar [lsblk](/index.php/Lsblk "Lsblk"):

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL     UUID                                 MOUNTPOINT
sdb                                                          
└─sdb1 vfat   Transcend 4A3C-A9E9
```

Un sistema de archivos existente, si está presente, se mostrará en la columna `FSTYPE`. Si está [montado](/index.php/Mount_(Espa%C3%B1ol) "Mount (Español)"), aparecerá en la columna `MOUNTPOINT`.

## Crear un sistema de archivos

Los sistemas de archivos generalmente se crean en una [partición](/index.php/Partition_(Espa%C3%B1ol) "Partition (Español)"), dentro de contenedores lógicos como [LVM](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)"), [RAID](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)") y [dm-crypt](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)"), o en un archivo normal (véase [Wikipedia:es:Loop device](https://en.wikipedia.org/wiki/es:Loop_device "wikipedia:es:Loop device")). Esta sección describe el caso de la partición.

**Nota:** Los sistemas de archivos se pueden escribir directamente en un disco, conocido como *superfloppy* o [particless disk](/index.php/Partitioning#Partitionless_disk "Partitioning"). Ciertas limitaciones están involucradas con este método, particularmente si [arranca](/index.php/Arch_boot_process "Arch boot process") desde tal unidad. Véase [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") para un ejemplo.

**Advertencia:**

*   Después de crear un nuevo sistema de archivos, es improbable que se recuperen los datos almacenados previamente en esta partición. **Haga una copia de seguridad de los datos que desee conservar**.
*   El propósito de una partición dada puede restringir la elección del sistema de archivos. Por ejemplo, una [partición del sistema EFI](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") debe contener un sistema de archivos [FAT32](/index.php/FAT32_(Espa%C3%B1ol) "FAT32 (Español)"), y el sistema de archivos que contiene el directorio `/boot` debe estar soportado por el [cargador de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)").

Antes de continuar, [identifique el dispositivo](/index.php/Lsblk_(Espa%C3%B1ol) "Lsblk (Español)") donde se creará el sistema de archivos y si está montado o no. Por ejemplo:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1                      C4DA-2C4D                            
├─sda2 ext4                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 /mnt
└─sda3                      56adc99b-a61e-46af-aab7-a6d07e504652 

```

Los sistemas de archivos montados **deben** ser [desmontados](#Desmontar_un_sistema_de_archivos) antes de continuar. En el ejemplo anterior, existe un sistema de archivos que está en `/dev/sda2` y se monta en `/mnt`. Se desmontaría con:

```
# umount /dev/sda2

```

Para encontrar los sistemas de archivos que estén montados, véase [#Listar los sistemas de archivos montados](#Listar_los_sistemas_de_archivos_montados).

Para crear un nuevo sistema de archivos, utilice [mkfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.8). Véase [#Tipos de sistemas de archivos](#Tipos_de_sistemas_de_archivos) para conocer el tipo exacto, así como las utilidades de espacio de usuario que desee instalar para un sistema de archivos en particular.

Por ejemplo, para crear un nuevo sistema de archivos de tipo [ext4](/index.php/Ext4_(Espa%C3%B1ol) "Ext4 (Español)") (común para particiones de datos de Linux) en `/dev/sda1`, ejecute:

```
# mkfs.ext4 /dev/sda1

```

**Sugerencia:**

*   Utilice la opción `-L` de *mkfs.ext4* para especificar una [etiqueta de sistema de archivos](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-label "Persistent block device naming (Español)"). *e2label* se puede utilizar para cambiar la etiqueta en un sistema de archivos existente.
*   Los sistemas de archivos pueden ser *redimensionados* tras su creación, con ciertas limitaciones. Por ejemplo, el tamaño del sistema de archivos [XFS](/index.php/XFS "XFS") se puede aumentar, pero no se puede reducir. Véase [Capacidades de redimensionar](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Resize_capabilities "w:Comparison of file systems") y la documentación del sistema de archivos correspondiente para obtener más información.

El nuevo sistema de archivos ahora se puede montar en el directorio de su elección.

## Montar un sistema de archivos

Para montar manualmente el sistema de archivos ubicado en un dispositivo (por ejemplo, una partición) en un directorio, utilice [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8). Este ejemplo monta `/dev/sda1` en `/mnt`.

```
# mount /dev/sda1 /mnt

```

Esto vincula el sistema de archivos en `/dev/sda1` en el directorio `/mnt`, haciendo visible el contenido del sistema de archivos. Todos los datos que existían en `/mnt` antes de esta acción se vuelven invisibles hasta que se desmonte el dispositivo.

[fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") contiene información sobre cómo se deben montar automáticamente los dispositivos, si están presentes. Véase el artículo [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") para obtener más información sobre cómo modificar este comportamiento.

Si se especifica un dispositivo en `/etc/fstab` y solo se proporciona el dispositivo o el punto de montaje en la línea de órdenes, esa información se utilizará en el montaje. Por ejemplo, si `/etc/fstab` contiene una línea que indica que `/dev/sda1` debe montarse en `/mnt`, entonces lo siguiente montará automáticamente el dispositivo en esa ubicación:

```
# mount /dev/sda1

```

o

```
# mount /mnt

```

*mount* contiene varias opciones, muchas de las cuales dependen del sistema de archivos especificado. Las opciones se pueden cambiar, ya sea:

*   utilizando opciones en la línea de órdenes con *mount*
*   editando [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)")
*   creando reglas [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)")
*   [compilando el kernel usted mismo](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")
*   o utilizando scripts de montaje específicos del sistema de archivos (situados en `/usr/bin/mount.*`).

Véase estos artículos relacionados y el artículo del sistema de archivos de interés para obtener más información.

### Listar los sistemas de archivos montados

Para listar todos los sistemas de archivos montados utilice [findmnt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/findmnt.8):

```
$ findmnt

```

*findmnt* toma una variedad de argumentos que pueden filtrar la salida y mostrar información adicional. Por ejemplo, puede tomar un dispositivo o punto de montaje como argumento para mostrar solo información sobre lo que se especifica:

```
$ findmnt /dev/sda1

```

*findmnt* reúne información de `/etc/fstab`, `/etc/mtab`, y `/proc/self/mounts`.

### Desmontar un sistema de archivos

Para desmontar un sistema de archivos utilice [umount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/umount.8). Se puede especificar el dispositivo que contiene el sistema de archivos (por ejemplo, `/dev/sda1`) o el punto de montaje (por ejemplo, `/mnt`):

```
# umount /dev/sda1

```

o

```
# umount /mnt

```

## Véase también

*   [filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5)
*   [Documentación de sistemas de archivos soportados por Linux](https://www.kernel.org/doc/Documentation/filesystems/)
*   [Wikipedia:es:Sistema de archivos](https://en.wikipedia.org/wiki/es:Sistema_de_archivos "wikipedia:es:Sistema de archivos")
*   [Wikipedia:es:Mount](https://en.wikipedia.org/wiki/es:Mount "wikipedia:es:Mount")