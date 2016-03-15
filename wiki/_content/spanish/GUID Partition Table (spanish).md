GUID Partition Table (GPT) es un nuevo formato de particionado integrante de la especificación [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"), que usa un [identificador único global](https://en.wikipedia.org/wiki/Globally_unique_identifier "wikipedia:Globally unique identifier") para los dispositivos. Es diferente del [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") (el estilo más comúnmente utilizado de partición) en muchos aspectos y tiene muchas ventajas.

**Advertencia:** Si quiere un arranque dual con Windows en la misma unidad, recuerde que Windows no puede arrancar desde un disco con tabla GPT en modalidad BIOS. Si ya tiene instalado Windows en la unidad con tabla de particiones MBR para arrancar a través de la BIOS, no convierta la unidad a una tabla de particionado GPT, dado que Windows no podrá arrancar, independientemente del gestor de arranque que utilice para cargar Windows. Necesita instalar Windows en modo UEFI y utilizar uno de los [gestores de arranque de UEFI](/index.php/UEFI_Bootloaders "UEFI Bootloaders") para cargar en cadena Windows, si se está arrancando desde una unidad con tabla GPT. Esta es una limitación de Windows.

Para entender GPT, es importante entender lo que es MBR y cuáles son sus desventajas.

## Contents

*   [1 Master Boot Record](#Master_Boot_Record)
    *   [1.1 Problemas con MBR](#Problemas_con_MBR)
*   [2 GUID Partition Table](#GUID_Partition_Table)
    *   [2.1 Ventajas de GPT](#Ventajas_de_GPT)
    *   [2.2 Soporte para el Kernel](#Soporte_para_el_Kernel)
*   [3 Soporte para el gestor de arranque](#Soporte_para_el_gestor_de_arranque)
    *   [3.1 Sistemas UEFI](#Sistemas_UEFI)
    *   [3.2 Sistemas BIOS](#Sistemas_BIOS)
*   [4 Utilidades de particionado](#Utilidades_de_particionado)
    *   [4.1 GPT fdisk](#GPT_fdisk)
        *   [4.1.1 Conversión de MBR a GPT](#Conversi.C3.B3n_de_MBR_a_GPT)
    *   [4.2 Fdisk de util-linux](#Fdisk_de_util-linux)
    *   [4.3 GNU Parted](#GNU_Parted)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Master Boot Record

La tabla de particiones MBR almacena la información de las particiones en el primer sector de un disco duro de la siguiente manera:

| Ubicación en el disco duro | Propósito del Código |
| Primeros 440 bytes | Código de arranque de MBR que es lanzado por la BIOS. |
| 441-446 bytes | Firma de disco MBR. |
| 447-510 bytes | Tabla de particiones vigente con información acerca de las particiones primarias y extendidas. (Tenga en cuenta que las particiones lógicas no están listadas aquí) |
| 511-512 bytes | Firma de arranque MBR 0xAA55. |

La información completa acerca de las particiones primarias se limita a los 64 bytes asignados. Para ampliar ésto, fueron utilizadas particiones extendidas. Una partición extendida es simplemente una partición primaria en el MBR, que actúa como un contenedor para otras particiones llamadas particiones lógicas. Así que un disco duro queda limitado a 4 particiones primarias, o 3 primarias y 1 partición extendida con un número variable de particiones lógicas en su interior.

### Problemas con MBR

1.  Sólo pueden ser definidas 4 particiones primarias o 3 primarias + 1 partición extendida (con un número arbitrario de particiones lógicas dentro de la partición extendida). Si tiene 3 particiones primarias + 1 partición extendida, y tiene algo de espacio libre fuera del área de la partición extendida, no se puede crear una nueva partición en ese espacio libre.
2.  Dentro de la partición extendida, los metadatos de las particiones lógicas se almacenan en una estructura de lista enlazada. Si un enlace se pierde, todas las particiones lógicas existentes, después de los metadatos, se pierden.
3.  MBR sólo admite 1 byte para códigos de tipo de partición, lo que conlleva muchas colisiones.
4.  MBR almacena la información del sector de la partición con valores LBA de 32 bits. Esta longitud de LBA junto con los 512 byte del tamaño del sector (más comúnmente utilizados) limita el tamaño máximo manejable del disco hasta 2 [TiB](https://en.wikipedia.org/wiki/es:TiB "wikipedia:es:TiB"). Cualquier espacio superior a 2 TiB supone que no puede ser definido como una partición si se utiliza MBR para particionarlo.

## GUID Partition Table

GUID Partition Table (GPT) utiliza GUID (o UUID en el mundo linux) para definir particiones y sus tipos, de ahí el nombre. La GPT se compone de:

| Ubicación en el disco duro | Propósito |
| Primer sector lógico del disco o Primeros 512 bytes | Protective MBR - Igual que un MBR normal, pero el área de 64 bytes contiene una sola Partición Primaria del tipo 0xEE entrada definida sobre el tamaño total del disco o en caso de >2 [TiB](https://en.wikipedia.org/wiki/es:TiB "wikipedia:es:TiB"), hasta un tamaño de partición de 2 TiB. |
| Segundo sector lógico del disco o Siguientes 512 bytes | Cabecera GPT Principal - Contiene el Unique Disk GUID (GUID Único del Disco), Ubicación de la Tabla de la Partición Primaria, Número de posibles entradas en la tabla de particiones, las sumas de comprobación CRC32 de sí mismo y de la Tabla de Partición Primaria, Localización de la Segunda Cabecera (o Backup) GPT |
| 16 KiB (por defecto), tras el segundo sector lógico del disco | Tabla GPT Principal - 128 entradas de partición (por defecto, aunque puede ser más alto), cada una con una entrada de 128 bytes de tamaño (de ahí el total de 16 Kb para 128 entradas de partición). Los números del sector se almacenan en 64-bit LBA y cada partición tiene un tipo GUID de partición y un único GUID por partición . |
| 16 KiB (por defecto) antes del último sector lógico del disco | Tabla GPT Secundaria - Es byte por byte idéntica a la tabla Principal. Se utiliza principalmente para la recuperación en caso de que la tabla de partición principal esté dañada. |
| Último sector lógico del disco o Últimos 512 bytes | Cabecera GPT Secundaria - Contiene la GUID Única del Disco, lugar de la tabla de la partición secundaria, el número de entradas posibles en la tabla de particiones, las sumas de comprobación CRC32 de sí mismo y la Tabla de Partición Secundaria, Localización de la Principal Cabecera GPT. Esta cabecera se puede utilizar para recuperar información de la GPT en caso de que la cabecera principal esté dañada. |

### Ventajas de GPT

1.  Utiliza GUID (UUID) para identificar los tipos de particiones - Sin colisiones.
2.  Proporciona un GUID único de disco y un GUID único de partición para cada partición - Un buen sistema de archivos independiente referenciando a las particiones y discos.
3.  Número arbitrarios de particiones -depende del espacio asignado por la tabla de particiones-. No hay necesidad de particiones extendidas y lógicas. Por defecto, la tabla GPT contiene espacio para la definición de 128 particiones. Sin embargo, si el usuario desea definir más particiones, se puede asignar más espacio (actualmente se sabe que solo gdisk soporta esta característica).
4.  Utiliza 64-bit LBA para almacenar números del Sector - tamaño máximo del disco manejable es de 2 [ZiB](https://en.wikipedia.org/wiki/es:ZiB "wikipedia:es:ZiB").
5.  Almacena una copia de seguridad del encabezado y de la tabla de particiones al final del disco que ayuda en la recuperación en el caso de que los primeros están dañados.
6.  Checksum CRC32 para detectar errores y daños de la cabecera y en la tabla de particiones.

### Soporte para el Kernel

La opción `CONFIG_EFI_PARTITION` en la configuración del kernel permite el soporte GPT en el kernel (a pesar del nombre PARTICIÓN EFI). Esta opción debe ser incorporada en el kernel y no compilada como un módulo cargable. La misma es necesaria incluso si los discos GPT solo se utilizan para el almacenamiento de datos y no para el arranque. Esta opción está activada por defecto en el kernel de Arch [linux](https://www.archlinux.org/packages/?name=linux) y [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) contenido en el repositorio [core]. Para el caso de un kernel personalizado, esta opción se habilita estableciendo `CONFIG_EFI_PARTITION=y`.

## Soporte para el gestor de arranque

### Sistemas UEFI

Todos los gestores de arranque UEFI admiten discos GPT desde el momento en que GPT es una parte de la especificación UEFI y, por lo tanto, obligatorio para el arranque UEFI. Consulte [Boot loaders](/index.php/Boot_loaders "Boot loaders") para más información.

### Sistemas BIOS

**Nota:** En algunos sistemas BIOS con placas base Intel solo se iniciará un disco GPT si la partición protective MBR tiene establecida la etiqueta Boot. En tales sistemas BIOS, usando [MBR](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)") (también conocido como particiones msdos) se recomienda usar GPT para permitir su compatibilidad. Véase [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) y [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) para obtener más información y posibles soluciones.

*   [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") requiere una [BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") (de 2 [MiB](https://en.wikipedia.org/wiki/es:MiB "wikipedia:es:MiB"), sin sistema de archivos, código tipo `EF02` con gdisk o el indicador bios_grub con GNU Parted) en los sistemas BIOS para incrustar su archivo `core.img` debido a la falta de espacio post-MBR para poder insertar discos GPT. Entre tanto, la compatibilidad GPT en GRUB es proporcionada por el módulo `part_gpt` que no está relacionado con el requisito de la **BIOS Boot Partition**.

*   [Syslinux](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)") requiere la partición que contiene `/boot/syslinux/ldlinux.sys` (independientemente de si `/boot` es una partición separada o no) que esté marcada con el atributo GPT «Legacy BIOS Bootable» (indicador *legacy_boot* en GNU Parted) para identificar la partición que contiene los archivos de arranque de Syslinux para el código de arranque del MBR en los 440 byte, `gptmbr.bin`. Consulte [Syslinux:GPT](/index.php/Syslinux#GUID_Partition_Table_aka_GPT "Syslinux") para más información.

*   [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") y [LILO](/index.php/LILO "LILO") no soportan GPT.

## Utilidades de particionado

### GPT fdisk

GPT fdisk es un conjunto de utilidades en modo texto para la edición de los discos GPT. Éstas consisten en gdisk, sgdisk y cgdisk que son equivalentes a las herramientas respectivas de fdisk desde util-linux (utilizadas para discos MBR). [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) está disponible en el repositorio [extra].

#### Conversión de MBR a GPT

Una de las mejores características de gdisk (y sgdisk y cgdisk también) es su capacidad para convertir MBR y etiquetas de disco BSD a GPT sin pérdida de datos. Tras la conversión, todas las particiones MBR primarias y las particiones lógicas quedarán convertidas en particiones GPT con los tipos GUID de partición correctos y GUID únicos de partición creados para cada partición.

Sólo tiene que abrir el disco MBR usando gdisk y salir con «w» para escribir los cambios en el disco (similar a fdisk) para convertir el disco MBR a GPT. **¡Cuidado con los errores y de corregirlos antes de escribir cualquier cambio en el disco!**, ya que corre el riesgo de perder datos. Consulte [http://www.rodsbooks.com/gdisk/mbr2gpt.html](http://www.rodsbooks.com/gdisk/mbr2gpt.html) para más información. Después de la conversión, el gestor de arranque tendrá que ser reinstalado para configurarlo a fin de que arranque desde GPT.

**Nota:**

*   Recuerde que GPT almacena una tabla secundaria al final del disco. Esta estructura de datos consume 33 sectores de 512 bytes por defecto. MBR no tiene una estructura de datos similar al final del disco, lo que significa que la última partición en un disco MBR a veces se extiende hasta el final del disco y evita la conversión completa. Si esto le sucede, debe abandonar la conversión, redimensionar el tamaño de la partición final, o convertir todo salvo la partición final.
*   Tenga en cuenta que si su gestor de arranque es GRUB, necesita una [BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB"). Si el diseño del particionado MBR hay probabilidades de que la primera partición comience en el sector 2048 por razones de alineación. Eso significa que al principio tendá 1.007 [KiB](https://en.wikipedia.org/wiki/es:KiB "wikipedia:es:KiB") de espacio vacío donde poder crear la partición bios de arranque. Para ello, en primer lugar, realice la conversión de mbr -> gpt con gdisk como se ha descrito anteriormente. A continuación, cree una nueva partición con gdisk, especifique su posición entre los sectores 34 a 2047, y establezca el tipo de partición como `EF02`.

### Fdisk de util-linux

La utilidad fdisk de util-linux (basado en libfdisk) apoya parcialmente GPT, pero todavía está en fase beta (con fecha 7 de octubre de 2013). Las utilidades relacionadas, cfdisk y sfdisk, todavía no admiten GPT, y pueden dañar el encabezado GPT y la tabla de particiones, si se utiliza en un disco GPT.

### GNU Parted

En GNU Parted >=3,0, la utilidad de línea de órdenes `parted` no es compatible con cualquier operación relacionada con sistema de archivos, y la mayor parte del código relacionado con FS ha sido eliminado de libparted, dejando sólo el código mínimo requerido por las aplicaciones externas como gparted. Upstream recomienda el uso de las herramientas específicas del sistema de archivos o una de las utilidades que contienen GUI como gparted (que llama a estas herramientas externas) para las operaciones relacionadas con el sistema de archivos.

## Véase también

1.  Página de Wikipedia sobre [GPT](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table") y [MBR](https://en.wikipedia.org/wiki/Master_boot_record "wikipedia:Master boot record")
2.  Página de Rod Smith sobre [la herramienta fdisk GPT](http://rodsbooks.com/gdisk/) y página del proyecto [Sourceforge.net - gptfdisk](http://sourceforge.net/projects/gptfdisk/)
3.  Página Rod Smith's sobre [conversión de MBR a GPT](http://rodsbooks.com/gdisk/mbr2gpt.html) y arranque de sistemas operativos [desde GPT](http://rodsbooks.com/gdisk/booting.html~~HEAD=NNS)
4.  Página Rod Smith's sobre la [Nueva Partición Tipo GUID](http://www.rodsbooks.com/linux-fs-code/index.html) para datos de particiones Linux
5.  Presentación página [CD's de Recuperación del Sistema en GPT](http://sysresccd.org/Sysresccd-Partitioning-The-new-GPT-disk-layout)
6.  Página de Wikipedia sobre [BIOS Boot Partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
7.  Aproveche al máximo de unidades de gran tamaño con [GPT y Linux - IBM Developer Works](http://www.ibm.com/developerworks/linux/library/l-gpt/index.html?ca=dgr-lnxw07GPT-Storagedth-lx&S_TACT=105AGY83&S_CMP=grlnxw07)
8.  [FAQ de Microsoft Windows y GPT](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)