**Estado de la traducción**
Este artículo es una traducción de [Fdisk](/index.php/Fdisk "Fdisk"), revisada por última vez el **2018-12-17**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Fdisk&diff=0&oldid=559268) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Sistemas de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)")
*   [gdisk](/index.php/Gdisk "Gdisk")
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted")
*   [Particionar](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)")
*   [dd](/index.php/Dd "Dd")

[util-linux fdisk](https://git.kernel.org/cgit/utils/util-linux/util-linux.git/)es una utilidad de línea de órdenes dirigida por diálogos que crea y manipula las tablas de particiones y las particiones en un disco duro. Los discos duros se dividen en particiones y esta división se describe en la tabla de particiones.

Este artículo cubre [fdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fdisk.8) y su utilidad relacionada [sfdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sfdisk.8).

**Sugerencia:** Para la funcionalidad de partición básica con una interfaz de usuario de texto, se puede utilizar [cfdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cfdisk.8).

## Contents

*   [1 Instalación](#Instalación)
*   [2 Listar las particiones](#Listar_las_particiones)
*   [3 Copia de seguridad y restauración de la tabla de particiones](#Copia_de_seguridad_y_restauración_de_la_tabla_de_particiones)
*   [4 Crear una tabla de particiones y las particiones](#Crear_una_tabla_de_particiones_y_las_particiones)
    *   [4.1 Crear nueva tabla](#Crear_nueva_tabla)
    *   [4.2 Crear particiones](#Crear_particiones)
    *   [4.3 Escribir cambios en el disco](#Escribir_cambios_en_el_disco)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Ordenar particiones](#Ordenar_particiones)
*   [6 Véase también](#Véase_también)

## Instalación

Para utilizar *fdisk* y sus utilidades asociadas, se requiere el paquete [util-linux](https://www.archlinux.org/packages/?name=util-linux), que es parte del grupo [base](https://www.archlinux.org/groups/x86_64/base/).

## Listar las particiones

Para listar las tablas de particiones y las particiones en un dispositivo (por ejemplo `/dev/sda`), puede ejecutar lo siguiente:

```
# fdisk -l /dev/sda

```

**Nota:** Si no se especifica el dispositivo, *fdisk* listará todas las particiones en `/proc/partitions`.

## Copia de seguridad y restauración de la tabla de particiones

Antes de realizar cambios en un disco duro, es posible que quiera realizar una copia de seguridad de la tabla de particiones y el esquema de partición de la unidad. También puede utilizar una copia de seguridad para copiar el mismo diseño de partición en múltiples unidades.

Tanto para GPT como para MBR puede utilizar *sfdisk* para guardar el diseño de partición de su dispositivo en un archivo con la opción `-d`/`--dump`. Ejecute la siguiente orden para el dispositivo `/dev/sda`:

```
# sfdisk -d /dev/sda > sda.dump

```

El archivo debería tener este aspecto para una única partición ext4 con un tamaño de 1 GiB:

 `sda.dump` 
```
label: gpt
label-id: AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE
device: /dev/sda
unit: sectors
first-lba: 34
last-lba: 1048576

/dev/sda1 : start=2048, size=1048576, type=0FC63DAF-8483-4772-8E79-3D69D8477DE4, uuid=BBF1CD36-9262-463E-A4FB-81E32C12BDE7
```

Para restaurar posteriormente este diseño puede ejecutar:

```
# sfdisk /dev/sda < sda.dump

```

## Crear una tabla de particiones y las particiones

El primer paso para [particionar](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") un disco es crear una tabla de particiones. Después de eso, las particiones reales se crean de acuerdo con el [esquema de partición](/index.php/Partition_scheme_(Espa%C3%B1ol) "Partition scheme (Español)") deseado. Véase el artículo [tabla de particiones](/index.php/Partition_table_(Espa%C3%B1ol) "Partition table (Español)") para ayudarle a decidir si utilizar [MBR](/index.php/MBR_(Espa%C3%B1ol) "MBR (Español)") o [GPT](/index.php/GPT_(Espa%C3%B1ol) "GPT (Español)").

Antes de comenzar, es posible que desee realizar una [copia de seguridad](#Copia_de_seguridad_y_restauración_de_la_tabla_de_particiones) de su actual tabla de particiones y esquema.

Las versiones recientes de *fdisk* han abandonado el obsoleto sistema de utilizar cilindros como unidad de visualización predeterminada, así como la compatibilidad con MS-DOS de forma predeterminada. *fdisk* alinea automáticamente todas las particiones a 2048 sectores, o 1 MiB, que debería funcionar para todos los tamaños de EBS que se sabe que son utilizados por los fabricantes de SSD. Esto significa que la configuración predeterminada le dará una alineación adecuada.

Inicie *fdisk* contra su disco como superusuario. En este ejemplo estamos utilizando `/dev/sda`:

```
# fdisk /dev/sda

```

Esto abre el diálogo de *fdisk* donde puede escribir las órdenes.

### Crear nueva tabla

**Advertencia:** Si crea una nueva tabla de particiones en un disco con datos, borrará todos los datos del disco. Asegúrese antes de que esto es lo que quiere hacer.

Para crear una nueva tabla de particiones y borrar todos los datos de la partición actual escriba `o` en el indicador de una tabla de particiones MBR o `g` para una Tabla de particiones GUID (GPT). Omita este paso si la tabla que necesita ya se ha creado.

### Crear particiones

Cree una nueva partición con la orden `n`. Introduzca un tipo de partición, un número de partición, un sector inicial y un sector final.

Cuando se le solicite, especifique el tipo de partición, escriba `p` para crear una partición primaria o `e` para crear una extendida. Puede haber hasta cuatro particiones primarias.

El primer sector debe especificarse en términos absolutos utilizando números de sector. El último sector se puede especificar utilizando la posición absoluta en sectores o mediante el símbolo `+` para especificar una posición relativa al sector de inicio medido en sectores, kibibytes (`K`), mebibytes (`M`), gibibytes (`G`), tebibytes (`T`), o pebibytes (`P`); por ejemplo, si define `+2G` como el último sector, especificará un punto 2GiB después del sector de inicio. Al presionar la tecla `Intro` sin entrada, se especifica el valor predeterminado, que es el inicio del bloque más grande disponible para el sector de inicio y el final del mismo bloque para el sector de final.

Seleccione el tipo de identificación de la partición. El valor predeterminado, `Linux filesystem`, debería estar bien para la mayoría de los casos. Presione `l` para mostrar la lista de códigos. Puede hacer que la partición se pueda iniciar escribiendo `a`.

**Sugerencia:**

*   Cuando se particiona, siempre es una buena idea seguir los valores predeterminados para los sectores de inicio y final de la partición. Además, especifique los tamaños de partición con la notación *+<tamaño>{M,G,...}*. Dichas particiones siempre se alinean de acuerdo con las propiedades del dispositivo.
*   En un disco con particionado MBR, deje al menos 16.5 KiB de espacio libre al final del disco para simplificar la [conversión entre MBR y GPT](/index.php/Gdisk#Convert_between_MBR_and_GPT "Gdisk") si alguna vez surge la necesidad.
*   La [partición del sistema EFI](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") requiere el tipo `EFI System`.
*   [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") requiere una [partición de arranque BIOS](/index.php/BIOS_boot_partition_(Espa%C3%B1ol) "BIOS boot partition (Español)") con el tipo `BIOS boot` al instalar GRUB en un disco.
*   Se recomienda utilizar `Linux swap` para cualquier partición [swap](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)"), ya que systemd lo montará automáticamente.

Véase los artículos respectivos para conocer las consideraciones sobre el tamaño y la ubicación de estas particiones.

Repita este procedimiento hasta que tenga las particiones que desee.

### Escribir cambios en el disco

Escriba la tabla en el disco y salga mediante la orden `w`.

## Consejos y trucos

### Ordenar particiones

Esto se aplica cuando se crea una nueva partición en el espacio entre dos particiones o se elimina una partición. Se utiliza `/dev/sda` en este ejemplo.

```
# sfdisk -r /dev/sda

```

Después de ordenar las particiones si no está utilizando la [nomenclatura de dispositivo de bloque persistente](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)"), es posible que deba ajustar los archivos de configuración `/etc/fstab` y/o `/etc/crypttab`.

**Nota:** El kernel debe leer la nueva tabla de particiones para que las particiones (por ejemplo, `/dev/sda1`) sean utilizables. Reinicie el sistema o diga al núcleo que [vuelva a leer la tabla de particiones](https://serverfault.com/questions/36038/reread-partition-table-without-rebooting).

## Véase también

*   [Particionando manual su disco duro con fdisk](http://www.novell.com/coolsolutions/feature/19350.html)