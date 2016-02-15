Desde [Wikipedia](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	_Un sistema de archivos (o_ «filesystem»_) es un medio para organizar los datos que se espera se mantengan después que un programa haya terminado, al proporcionar procedimientos para almacenar, recuperar y actualizar dichos datos, así como gestionar el espacio disponible en el dispositivo(s) que lo contiene. Un sistema de archivos organiza los datos de una manera eficiente y está sintonizado con las características específicas del dispositivo._

Cada partición individual se puede configurar mediante uno de los muchos sistemas de archivos disponibles. Cada uno tiene sus propias ventajas, desventajas e idiosincrasias únicas. A continuación se hace una breve descripción de los sistemas de archivos compatibles; se hacen, también, enlaces a páginas de Wikipedia que proporcionan mucha más información.

Antes de ser formateado, el disco debe ser [particionado](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)").

## Contents

*   [1 Tipos de sistemas de archivos](#Tipos_de_sistemas_de_archivos)
    *   [1.1 Journaling](#Journaling)
    *   [1.2 Soporte técnico de Arch Linux](#Soporte_t.C3.A9cnico_de_Arch_Linux)
    *   [1.3 Sistemas de archivos basados en FUSE](#Sistemas_de_archivos_basados_en_FUSE)
*   [2 Crear un sistema de archivos](#Crear_un_sistema_de_archivos)
*   [3 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Tipos de sistemas de archivos

*   [Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") - También conocido como «Better FS», es un **nuevo sistema de archivos con potentes funciones, similares al excelente ZFS de Sun/Oracle**. Estas incluyen la creación de instantáneas, striping y mirroring multi-disco (RAID software sin mdadm), sumas de comprobación, copias de seguridad incrementales, y compresión sobre la marcha integrada, que pueden dar un significativo aumento de las prestaciones, así como ahorrar espacio. A partir de enero de 2011, Btrfs es considerado inestable a pesar de que se ha estado insertando en el kernel principal con un estado experimental. Btrfs parece ser el futuro de los sistemas de archivos de GNU/Linux y se ofrece como una opción para el sistema de archivos de root en todos las instalaciones de las distribuciones más importantes.
*   [exFAT](https://en.wikipedia.org/wiki/exFAT "wikipedia:exFAT") - **Sistema de archivos de Microsoft optimizado para unidades flash**. A diferencia de NTFS, exFAT no puede preasignar espacio en disco para un archivo con solo marcar el espacio arbitrariamente en el disco como «asignado». Al igual que en FAT, cuando se crea un archivo de longitud conocida, exFAT debe llevar a cabo una completa escritura física del mismo tamaño del archivo.
*   [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2") - **Second Extended Filesystem** es un consolidado y maduro sistema de archivos para GNU/Linux muy estable. Uno de sus inconvenientes es que no tiene apoyo para el registro (journaling) (véase más abajo) o las barreras. La falta de _registro por diario_ («journaling») puede traducirse en la pérdida de datos en caso de un corte de corriente o fallo del sistema. También puede **no** ser conveniente para las particiones root (`/`) y `/home`, porque las comprobaciones del sistema de archivos pueden tomar mucho tiempo. Un sistema de archivos ext2 puede ser [convertido a ext3](/index.php/Convert_ext2_to_ext3 "Convert ext2 to ext3").
*   [ext3](https://en.wikipedia.org/wiki/ext3 "wikipedia:ext3") - **Third Extended Filesystem** es, esencialmente, el sistema de archivos ext2 pero con el apoyo de journaling y la escritura de barreras. Es compatible con ext2, bien probado, y extremadamente estable.
*   [ext4](https://en.wikipedia.org/wiki/ext4 "wikipedia:ext4") - **Fourth Extended Filesystem** es un sistema de archivos nuevo que también es compatible con ext2 y ext3\. Proporciona apoyo para volúmenes con tamaños de hasta 1 exabyte (es decir, 1.048.576 terabytes) y archivos con tamaños de hasta 16 terabytes. Aumenta el límite de los 32.000 subdirectorios de ext3 a 64.000\. También ofrece la capacidad de desfragmentación en línea.
*   [F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") - **Flash-Friendly File System** es un sistema de archivos flash creado por Kim Jaegeuk (Hangul: 김재극) de Samsung para el kernel del sistema operativo Linux. La motivación para F2FS era construir un sistema de archivos que desde el principio tuviese en cuenta las características de los dispositivos de almacenamiento basados ​​en memoria flash NAND (como los discos de estado sólido, eMMC, y tarjetas SD), que han sido ampliamente utilizados en el en sistemas informáticos que van desde dispositivos móviles a servidores.
*   [JFS](https://en.wikipedia.org/wiki/JFS_(file_system) "wikipedia:JFS (file system)") - El **Journaled File System** de IBM fue el primer sistema de archivos en ofrecer journaling, y ha sido empleado durante muchos años en el sistema operativo IBM AIX® antes de ser portado a GNU/Linux. JFS demanda menos recursos de la CPU que cualquier otro disponible para los sistemas GNU/Linux. Es muy rápido en el formato, montaje y comprobación del sistema de archivos (fsck). JFS ofrece óptimas prestaciones en general, especialmente en conjunción con el planificador de I/O. No es tan ampliamente soportado como los sistemas de archivos ext o ReiserFS, pero, sin embargo, muy maduro y estable.
*   [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") - **New Implementation of a Log-structured File System** fue desarrollado por NTT. Registra todos los datos en un formato continuo, a modo de un archivo de registro, que experimenta solo añadidos y nunca se sobrescribe. Está diseñado para reducir los tiempos de búsqueda y minimizar el tipo de pérdida de datos que se produce después de un accidente con los convencionales sistemas de archivos de Linux.
*   [NTFS](https://en.wikipedia.org/wiki/NTFS "wikipedia:NTFS") - **Sistema de archivos utilizado por Windows**. NTFS contiene algunas mejoras técnicas respecto a FAT y HPFS (High Performance File System), como el soporte mejorado para los metadatos y el uso de estructuras de datos avanzadas para mejorar el rendimiento, la confiabilidad y la utilización del espacio en disco, además de extensiones adicionales, como las listas de control de acceso de seguridad (ACL) y journaling del sistema de archivos.
*   [Reiser4](https://en.wikipedia.org/wiki/Reiser4 "wikipedia:Reiser4") - **Sucesor del sistema de archivos ReiserFS**, desarrollado desde cero por Namesys y patrocinado por DARPA y Linspire, utiliza B*-trees junto con el enfoque del equilibrado del árbol de directorios, en el que los nodos poco poblados no se fusionarán hasta que no se efectúe un nivelado del disco, o cuando la memoria esté baja o se completa una operación. Este sistema también permite a Reiser4 crear archivos y directorios sin tener que perder el tiempo y el espacio a través de bloques fijos.
*   [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") - **Sistema de archivos con journaling y altas prestaciones de Hans Reiser (V3)** que utiliza un método muy interesante de transferencia de datos basado en un algoritmo creativo e innovador. ReiserFS es anunciado como muy rápido, especialmente cuando se trata de muchos archivos pequeños. ReiserFS es rápido en dar formato, sin embargo, comparativamente lento en el montaje. Muy maduro y estable. ReiserFS (V3) no está siendo activamente desarrollado en este momento. Generalmente considerado como una buena opción para `/var`.
*   [Swap](https://en.wikipedia.org/wiki/Paging "wikipedia:Paging") - es el sistema de archivos utilizado para particiones de intercambio.
*   [VFAT](https://en.wikipedia.org/wiki/File_Allocation_Table#VFAT "wikipedia:File Allocation Table") - **Virtual File Allocation Table** es técnicamente sencillo y con el apoyo de prácticamente todos los sistemas operativos existentes. Esto hace que sea un formato útil para las tarjetas de memoria de estado sólido y una manera práctica para compartir datos entre sistemas operativos. VFAT soporta nombres largos de archivos.
*   [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") - **Primeros sistemas de archivos con journaling desarrollado originalmente por Silicon Graphics** para el sistema operativo IRIX y portado después a GNU/Linux. Proporciona un rendimiento muy rápido en los archivos y sistemas de archivos grandes y es muy rápido en el formato y montaje. Pruebas de benchmark comparativa han demostrado que es más lento cuando trata con muchos archivos pequeños. XFS es muy maduro y ofrece capacidad de desfragmentación en línea.
*   [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS") - **Combinación de sistema de archivos y gestor de volumen lógicos diseñado por Sun Microsystems**. Las características de ZFS incluyen la protección contra la corrupción de datos, soporte para grandes capacidades de almacenamiento, la integración de los conceptos de sistema de archivos y la gestión de volúmenes, instantáneas y clones copy-on-write, la comprobación continua de la integridad y reparación automática de los archivos, RAID-Z y NFSv4 ACL nativos.

### Journaling

Todos los sistemas de archivos antes vistos, con la excepción de ext2, FAT16/32, usan [journaling](https://en.wikipedia.org/wiki/es:Journaling "wikipedia:es:Journaling"). Journaling proporciona la rehabilitación de los fallos al registrar los cambios antes de que comprometan al sistema de archivos. En caso de un fallo del sistema o un corte de energía, este procedimiento es más rápido para informar en línea al sistema y es menos probable de que se dañe. El registro se lleva a cabo en un área específica del sistema de archivos.

No todas las técnicas de journaling son iguales. Solo ext3 y ext4 proporcionan la función _data-mode_ («modalidad de datos») de journaling, que registra los datos y los meta-datos. La «modalidad de datos» de journaling conlleva una pérdida de velocidad y no está habilitada de forma predeterminada. Los otros sistemas de archivos ofrecen una «modalidad de clasificación» (_ordered-mode_) de journaling, que solo registra los meta-datos. Mientras el resto de los journaling restaurarán un sistema de archivos a un estado válido después de un accidente, la «modalidad de datos» de journaling ofrece la mayor protección contra la corrupción y pérdida de datos. Sin embaro, este último compromete el rendimiento del sistema, porque la modalidad de datos journaling hace dos operaciones de escritura: primero al registro y luego al disco. El equilibrio entre la velocidad del sistema y la seguridad de los datos debe tenerse presente a la hora de elegir entre uno u otro tipo de sistemas de archivos.

### Soporte técnico de Arch Linux

*   **btrfs-progs** — soporte técnico para [Btrfs](/index.php/Btrfs "Btrfs").

	[http://btrfs.wiki.kernel.org/](http://btrfs.wiki.kernel.org/) || [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

*   **dosfstools** — soporte técnico para VFAT.

	[http://www.daniel-baumann.ch/software/dosfstools/](http://www.daniel-baumann.ch/software/dosfstools/) || [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

*   **exfat-utils** — soporte técnico para exFAT.

	[http://code.google.com/e/exfat/](http://code.google.com/e/exfat/) || [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

*   **f2fs-tools** — Soporte técnico para [F2FS](/index.php/F2fs "F2fs").

	[https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git](https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git) || [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools)

*   **e2fsprogs** — soporte técnico para ext2, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4").

	[http://e2fsprogs.sourceforge.net](http://e2fsprogs.sourceforge.net) || [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

*   **jfsutils** — soporte técnico para [JFS](/index.php/JFS "JFS").

	[http://jfs.sourceforge.net](http://jfs.sourceforge.net) || [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

*   **nilfs-utils** — soporte técnico para NILFS.

	[http://www.nilfs.org/](http://www.nilfs.org/) || [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils)

*   **ntfs-3g** — soporte técnico para [NTFS](/index.php/NTFS "NTFS").

	[http://www.tuxera.com/community/ntfs-3g-download/](http://www.tuxera.com/community/ntfs-3g-download/) || [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

*   **reiser4progs** — soporte técnico para [ReiserFSv4](/index.php/Reiser4 "Reiser4").

	[http://sourceforge.net/projects/reiser4/](http://sourceforge.net/projects/reiser4/) || [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/)

*   **reiserfsprogs** — soporte técnico para ReiserFSv3.

	[https://www.kernel.org/](https://www.kernel.org/) || [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

*   **xfsprogs** — soporte técnico para [XFS](/index.php/XFS "XFS").

	[http://oss.sgi.com/projects/xfs/](http://oss.sgi.com/projects/xfs/) || [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

*   **zfs** — soporte técnico para [ZFS](/index.php/ZFS "ZFS").

	[http://zfsonlinux.org/](http://zfsonlinux.org/) || [zfs-git](https://aur.archlinux.org/packages/zfs-git/)

### Sistemas de archivos basados en FUSE

El [sistema de archivos en el espacio de usuario](https://en.wikipedia.org/wiki/es:Sistema_de_archivos_en_el_espacio_de_usuario "wikipedia:es:Sistema de archivos en el espacio de usuario") (FUSE) es un mecanismo para sistemas operativos tipo Unix que permite a los usuarios sin privilegios de root crear sus propios sistemas de archivos sin necesidad de editar el código del núcleo. Esto se logra mediante la ejecución del código del sistema de archivos en _el espacio de usuario_, al tiempo que el módulo del kernel FUSE solo proporciona un «puente» a las interfaces del kernel que se está ejecutando.

## Crear un sistema de archivos

**Nota:**

*   Si desea cambiar el diseño de las particiones, vea [Partitioning](/index.php/Partitioning "Partitioning").
*   Si desea crear una partición de intercambio, vea [Swap](/index.php/Swap "Swap").

Antes de comenzar, se necesita saber qué nombre dio Linux al dispositivo. Los discos duros y memorias USB aparecen como `/dev/sd_x_`, donde «x» es una letra minúscula, mientras que las particiones aparecen como `/dev/sd_xY_`, donde «Y» es un número.

Por lo general, los sistemas de archivos se crean en una partición, pero también se pueden crear en el interior de contenedores lógicos como [LVM](/index.php/LVM "LVM"), [RAID](/index.php/RAID "RAID") o [dm-crypt](/index.php/Dm-crypt "Dm-crypt").

Para crear un nuevo sistema de archivos en una partición, el sistema de archivos existente ubicado en la partición no debe estar montado.

Si el dispositivo que desea formatear está montado, se mostrará en la columna _MOUNTPOINT_ al ejecutar:

```
$ lsblk

```

Para desmontarlo, puede usar _umount_ sobre el directorio donde se ha montado el disco:

```
# umount /punto_de_montaje

```

Para crear un nuevo sistema de archivos de tipo ext4, por ejemplo, en una partición haga:

**Advertencia:** Al formatear un dispositivo se eliminan todos los datos que contenga, asegúrese de hacer copias de seguridad de todo aquello que desee conservar.

```
# mkfs.ext4 /dev/_partición_

```

La orden `mkfs` es solo un sistema front-end unificado para las diferentes herramientas de `mkfs._fstype_`, por lo que alternativamente se puede usar también así:

```
# mkfs -t ext4 /dev/_partición_

```

## Véase también

*   [wikipedia:Comparison of file systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "wikipedia:Comparison of file systems")