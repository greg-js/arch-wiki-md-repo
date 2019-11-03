Artículos relacionados

*   [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)")
*   [fdisk (Español)](/index.php/Fdisk_(Espa%C3%B1ol) "Fdisk (Español)")
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted")
*   [dd (Español)](/index.php/Dd_(Espa%C3%B1ol) "Dd (Español)")

**Estado de la traducción**
Este artículo es una traducción de [GPT fdisk](/index.php/GPT_fdisk "GPT fdisk"), revisada por última vez el **2019-11-01**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GPT_fdisk&diff=0&oldid=587511) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[GPT fdisk](https://www.rodsbooks.com/gdisk/) —que consta de los programas *gdisk*, *cgdisk*, *sgdisk* y *fixparts*— es un conjunto de herramientas de particionado en modo texto creadas por Rod Smith. Funcionan en discos de tabla de particiones (GPT) con identificador único global (GUID), en lugar de en las tablas de particionado de registro de arranque maestro (MBR) más antiguas (y también smás comunes).

*gdisk*, *cgdisk* y *sgdisk* tienen la misma funcionalidad, pero proporcionan diferentes interfaces de usuario. *gdisk* es interactivo en modo texto, *sgdisk* funciona en línea de órdenes y *cgdisk* tiene una interfaz basada en [curses](https://en.wikipedia.org/wiki/es:Curses "wikipedia:es:Curses"). Este artículo cubre las utilidades [gdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gdisk.8) y [sgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sgdisk.8).

**Sugerencia:**

*   Para usar la funcionalidad básica de particionado con una interfaz de usuario en modo texto, se puede utilizar [cgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgdisk.8).
*   El sitio web de GPT fdisk dispone de tutoriales detallados para [gdisk](https://www.rodsbooks.com/gdisk/walkthrough.html), [cgdisk](https://www.rodsbooks.com/gdisk/cgdisk-walkthrough.html), [sgdisk](https://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html) y [FixParts](https://www.rodsbooks.com/fixparts/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Listar particiones](#Listar_particiones)
*   [3 Realizar copia de seguridad y restaurar la tabla de particiones](#Realizar_copia_de_seguridad_y_restaurar_la_tabla_de_particiones)
*   [4 Crear una tabla de particionado y las particiones](#Crear_una_tabla_de_particionado_y_las_particiones)
    *   [4.1 Crear nueva tabla](#Crear_nueva_tabla)
    *   [4.2 Crear particiones](#Crear_particiones)
        *   [4.2.1 Número de la partición](#Número_de_la_partición)
        *   [4.2.2 Primer y último sector](#Primer_y_último_sector)
        *   [4.2.3 Tipo de partición](#Tipo_de_partición)
    *   [4.3 Escribir los cambios en el disco](#Escribir_los_cambios_en_el_disco)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Conversión de MBR a GPT (y viceversa)](#Conversión_de_MBR_a_GPT_(y_viceversa))
    *   [5.2 Ordenar particiones](#Ordenar_particiones)
    *   [5.3 Recuperar encabezado GPT](#Recuperar_encabezado_GPT)
    *   [5.4 Expandir un disco GPT](#Expandir_un_disco_GPT)
    *   [5.5 Prevenir el montaje automático de la partición GPT](#Prevenir_el_montaje_automático_de_la_partición_GPT)
    *   [5.6 Apliación gdisk para EFI](#Apliación_gdisk_para_EFI)
*   [6 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk).

## Listar particiones

Para enumerar las tablas de particionado y las particiones presentes en un [dispositivo de bloque](/index.php/Device_file_(Espa%C3%B1ol)#Dispositivos_de_bloque "Device file (Español)"), puede ejecutar lo siguiente, donde el dispositivo puede llevar por nombre `/dev/sda`, `/dev/nvme0n1`, `/dev/mmcblk0`, etc.:

```
# gdisk -l /dev/sda

```

o, alternativamente, realizar la misma acción utilizando *sgdisk*:

```
# sgdisk -p /dev/sda

```

## Realizar copia de seguridad y restaurar la tabla de particiones

Antes de realizar cambios en un disco, es posible que desee hacer una copia de seguridad de la tabla de particionado y del esquema de particiones de la unidad. También puede usar una copia de seguridad para copiar el mismo esquema de particiones en otras unidades.

Utilizando *sgdisk* puede crear una copia de seguridad binaria que contendrá el MBR protector, el encabezado GPT principal, el encabezado GPT de respaldo y una copia de la tabla de particiones. El siguiente ejemplo guardará la tabla de particiones de `/dev/sda` en un archivo `sgdisk-sda.bin`:

```
# sgdisk -b=sgdisk-sda.bin /dev/sda

```

Luego, puede restaurar la copia de seguridad ejecutando:

```
# sgdisk -l=sgdisk-sda.bin /dev/sda

```

Si desea clonar el esquema de particiones de su dispositivo actual (`/dev/sda` en este caso) en otra unidad (`/dev/sdc`) ejecute:

```
# sgdisk -R=/dev/sdc /dev/sda

```

Si ambas unidades están en el mismo ordenador, debe [aleatorizar](https://en.wikipedia.org/wiki/es:Aleatorizaci%C3%B3n "wikipedia:es:Aleatorización") el disco y los GUID de las particiones:

```
# sgdisk -G /dev/sdc

```

## Crear una tabla de particionado y las particiones

El primer paso para [particionar](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") un disco es crear una tabla de particiones. Después de eso, las particiones reales se crean de acuerdo con el [esquema de particionado](/index.php/Partition_scheme "Partition scheme") deseado.

Antes de comenzar, es posible que desee [realizar una copia de seguridad](#Realizar_copia_de_seguridad_y_restaurar_la_tabla_de_particiones) de su actual tabla y esquema de particionado.

A continuación se muestra cómo usar *gdisk* para realizar la creación de una tabla de particiones y la creación de las particiones reales. Alternativamente, puede usar la versión basada en curses llamada *cgdisk*; sin embargo, las siguientes instrucciones no se aplican a él. Vea [cgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgdisk.8) para su uso.

*gdisk* realiza la alineación de la partición automáticamente sobre una base de tamaño de bloque de 2048 con sectores de 512 bytes (1 MiB) que debería ser compatible con todos los [formatos avanzados](/index.php/Advanced_Format_(Espa%C3%B1ol) "Advanced Format (Español)") de discos HDD y la gran mayoría de [SSD](/index.php/SSD "SSD"), si no todos .

Para utilizar *gdisk* , ejecute el programa seguido del nombre del [dispositivo de bloque](/index.php/Device_file_(Espa%C3%B1ol)#Dispositivos_de_bloque "Device file (Español)") que desea cambiar/editar. En este ejemplo usamos `/dev/sda`:

```
# gdisk /dev/sda

```

### Crear nueva tabla

**Advertencia:** si crea una nueva tabla de particionado en un disco con datos, borrará todos los datos del disco. Asegúrese de que esto es lo que quiere hacer.

Para crear una nueva [GUID Partition Table (Español)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)") y borrar todos los datos de las particiones actuales, escriba `o` en el [prompt](https://en.wikipedia.org/wiki/es:Prompt "wikipedia:es:Prompt"). Omita este paso si la tabla que necesita ya se ha creado.

### Crear particiones

Cree una nueva partición con la orden `n`. Debe ingresar el número de partición, el primer sector y el último, y el tipo de partición.

**Nota:** consulte [Partitioning (Español)#Esquemas de particionado](/index.php/Partitioning_(Espa%C3%B1ol)#Esquemas_de_particionado "Partitioning (Español)") para obtener información sobre el tamaño y la ubicación de las particiones.

#### Número de la partición

Un número de partición es el número asignado a una partición, por ejemplo, una partición con el número `1` en un disco `/dev/sda` sería `/dev/sda1`. Los números de las particiones pueden no coincidir siempre con el orden de las particiones en el disco, en cuyo caso pueden ser [ordenadas](#Ordenar_particiones).

Se recomienda elegir el número predeterminado sugerido por *gdisk*.

#### Primer y último sector

El primer y el último sector de la partición se pueden especificar en números de sector o como posiciones medidas en [kibibytes](https://en.wikipedia.org/wiki/es:Kibibyte "wikipedia:es:Kibibyte") (`K`), [mebibytes](https://en.wikipedia.org/wiki/es:Mebibyte "wikipedia:es:Mebibyte") (`M`), [gibibytes](https://en.wikipedia.org/wiki/es:Gibibyte "wikipedia:es:Gibibyte") (`G`), [tebibytes](https://en.wikipedia.org/wiki/es:Tebibyte "wikipedia:es:Tebibyte") (`T`), o [pebibytes](https://en.wikipedia.org/wiki/es:Pebibyte "wikipedia:es:Pebibyte") (`P`);

La posición se puede especificar:

*   en términos absolutos, desde el inicio del disco. Por ejemplo, `40M` como primer sector, especifica una posición de 40 MiB contados desde el inicio del disco;
*   en términos relativos, precediendo el tamaño con el signo `**+***tamaño*` o `**-***tamaño*`. Por ejemplo, `+2G` para especificar un punto de 2 GiB contados después del sector de inicio predeterminado, o `-200M` para especificar un punto 200 MiB descontados antes del último sector disponible.

Al presionar la tecla `Intro` sin ninguna entrada, se está especificando el valor predeterminado, que es el inicio del bloque más grande disponible para el primer sector y el final del mismo bloque para el último sector.

**Sugerencia:**

*   Al particionar, siempre es una buena idea especificar tamaños de partición usando términos relativos con la notación `+*tamaño{M,G,T,P}*` y no usar tamaños menores de 1 MiB. Tales particiones siempre estarán alineadas de acuerdo con las propiedades del dispositivo.
*   Deje un espacio libre de 1 MiB en algún lugar de los primeros 2 TiB del disco (por ejemplo, utilizando `+1M` como primer sector de una partición) en caso de que necesite crear una [BIOS boot partition (Español)](/index.php/BIOS_boot_partition_(Espa%C3%B1ol) "BIOS boot partition (Español)").

#### Tipo de partición

Seleccione el tipo de partición ingresando el código de tipo interno de gdisk o especificando el [GUID del tipo de partición](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") manualmente. El valor predeterminado, `Linux filesystem` (GUID: `0FC63DAF-8483-4772-8E79-3D69D8477DE4`; código interno de gdisk: `8300`), debería ser aceptable para la mayoría de los casos de uso.

<caption>Tipos de partición comunes</caption>
| Tipo de partición | Punto de montaje | Código
de gdisk | [GUID del tipo de partición](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") |
| Linux filesystem | Cualquiera | `8300` | `0FC63DAF-8483-4772-8E79-3D69D8477DE4` |
| [EFI system partition](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") | Cualquiera | `ef00` | `C12A7328-F81F-11D2-BA4B-00A0C93EC93B` |
| [BIOS boot partition](/index.php/BIOS_boot_partition_(Espa%C3%B1ol) "BIOS boot partition (Español)") | Ninguno | `ef02` | `21686148-6449-6E6F-744E-656564454649` |
| [Linux x86-64 root (/)](/index.php/Partitioning#/ "Partitioning") | `/` | `8304` | `4F68BCE3-E8CD-4DB1-96E7-FBCAF984B709` |
| [Linux swap](/index.php/Partitioning#Swap "Partitioning") | `[SWAP]` | `8200` | `0657FD6D-A4AB-43C4-84E5-0933C84B4F4F` |
| [Linux /home](/index.php/Partitioning_(Espa%C3%B1ol)#/home "Partitioning (Español)") | `/home` | `8302` | `933AC7E1-2EB4-4F13-B844-0E14E2AEF915` |
| [Linux /srv](/index.php/Partitioning_(Espa%C3%B1ol)#Particiones_dedicadas "Partitioning (Español)") | `/srv` | `8306` | `3B8F8425-20E0-4F3B-907F-1A25A76F98E8` |
| [Linux LVM](/index.php/LVM#_(Español)#Crear_particiones "LVM") | Cualquiera | `8e00` | `E6D6D379-F507-44C2-A23C-238F2A3DF928` |
| [Linux RAID](/index.php/RAID_(Espa%C3%B1ol)#GUID_Partition_Table "RAID (Español)") | Cualquiera | `fd00` | `A19D880F-05FC-4D3B-A006-743F0F84911E` |
| [Linux LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol)/Drive_preparation_(Espa%C3%B1ol)#Particiones_físicas "Dm-crypt (Español)/Drive preparation (Español)") | Cualquiera | `8309` | `CA7D7CCB-63ED-4C53-861C-1742536059CC` |
| [Linux dm-crypt](/index.php/Dm-crypt_(Espa%C3%B1ol)/Drive_preparation_(Espa%C3%B1ol)#Particiones_físicas "Dm-crypt (Español)/Drive preparation (Español)") | Cualquiera | `8308` | `7FFEC5C9-2D00-49B7-8941-3EA10A5586B7` |

**Sugerencia:**

*   Presione `L` para mostrar la lista de códigos internos de gdisk.
*   Se recomienda seguir la [Especificación de particiones detectables](https://www.freedesktop.org/wiki/Specifications/DiscoverablePartitionsSpec/) ya que [systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8) las montará automáticamente. Consulte [#Prevenir el montaje automático de la partición GPT](#Prevenir_el_montaje_automático_de_la_partición_GPT) si desea desactivar el montaje automático para una partición.

Repita este procedimiento hasta que tenga las particiones que desea.

### Escribir los cambios en el disco

**Sugerencia:** utilice la orden `c` para cambiar el nombre de una partición ([PARTLABEL](/index.php/PARTLABEL "PARTLABEL")) para distinguirla fácilmente.

Escriba la tabla en el disco y salga mediante la orden `w`.

## Consejos y trucos

### Conversión de MBR a GPT (y viceversa)

**Sugerencia:** lea [Convertir a/de GPT](https://www.rodsbooks.com/gdisk/mbr2gpt.html) de Rod Smith para obtener información más detallada y guía.

*gdisk*, *sgdisk* y *cgdisk* tienen la capacidad de convertir MBR y [BSD disklabels](https://en.wikipedia.org/wiki/BSD_disklabel "wikipedia:BSD disklabel") a GPT sin pérdida de datos. Tras la conversión, todas las particiones primarias MBR y las particiones lógicas se convierten en particiones GPT con los GUID de tipo de partición correctos y los GUID de partición únicos creados para cada partición.

Después de la conversión, será necesario reinstalar el [gestor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)") para configurarlo para que arranque desde GPT.

**Advertencia:**

*   GPT almacena una tabla secundaria al final del disco. Esta estructura de datos consume 33 sectores de 512 bytes (16,5 KiB) por defecto. MBR no tiene una estructura de datos similar en su extremo final del disco, lo que significa que la última partición en un disco MBR, a veces, se extiende hasta el final del disco, evitando así la conversión completa. Si este es el caso, debe abortar la conversión y cambiar el tamaño de la partición final (antes de volver a continuar).

*   Existen problemas de corrupción conocidos con el GPT de respaldo en portátiles que están basados en el chipset Intel y se ejecutan en modo RAID. La solución es usar AHCI en lugar de RAID, si es posible.

Para convertir una tabla de partición MBR a GPT usando *sgdisk*, utilice la opción `-g`/`--mbrtogpt`:

```
# sgdisk -g /dev/sda

```

Para convertir GPT a MBR, utilice la opción `-m`/`--gpttombr`. Tenga en cuenta que no es posible convertir más de cuatro particiones de GPT a MBR.

```
# sgdisk -m /dev/sda

```

### Ordenar particiones

Esto es aplicable cuando se crea una nueva partición en el espacio entre dos particiones o se elimina una partición. `/dev/sda` se utiliza en este ejemplo.

```
# sgdisk -s /dev/sda

```

Después de ordenar las particiones si no está utilizando [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)"), puede ser necesario ajustar la configuración de `/etc/fstab` y/o la configuración del archivo `/etc/crypttab`.

**Nota:** el kernel debe leer la nueva tabla de particiones para que las particiones (por ejemplo, `/dev/sda1`) puedan utilizarse. Reinicie el sistema o dígale al kernel que [vuelva a leer la tabla de particiones](https://serverfault.com/questions/36038/reread-partition-table-without-rebooting).

### Recuperar encabezado GPT

En caso de que el encabezado GPT principal o el encabezado GPT de respaldo se dañen, puede recuperar uno desde el otro con *gdisk*. `/dev/sda` se utiliza en este ejemplo.

```
# gdisk /dev/sda

```

elija `r` para las opciones de recuperación y transformación (solo expertos). A partir de ahí, elija entre:

*   `b`: utiliza el encabezado GPT de respaldo (reconstrucción principal)
*   `d`: utiliza el encabezado GPT principal (reconstrucción de la copia de seguridad)

Cuando termine, escriba la tabla en el disco y salga con la orden `w`.

### Expandir un disco GPT

Después de agrandar un disco (por ejemplo, en hardware [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)") o un disco de [máquina virtual](/index.php/Virtual_machine "Virtual machine")) el espacio libre recién agregado no se podrá utilizar de inmediato ya que GPT mantiene los datos al final del disco. Debe reubicar el encabezado GPT de respaldo al nuevo extremo del disco.

Ejecute *sgdisk* con la opción `-e`/`--move-second-header`, por ejemplo:

```
# sgdisk -e /dev/sda

```

Luego [imprima la tabla de particiones](#Listar_particiones); el espacio libre total ahora debería haberse incrementado.

### Prevenir el montaje automático de la partición GPT

[systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8) montará automáticamente las particiones siguiendo la [Especificación de particiones detectables](https://www.freedesktop.org/wiki/Specifications/DiscoverablePartitionsSpec/). A veces eso puede no ser lo deseable.

El montaje automático puede desactivarlo configurando el [atributo de partición](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries_.28LBA_2-33.29 "wikipedia:GUID Partition Table") `63` "do not automount" en la partición.

Inicie *gdisk*, por ejemplo:

```
# gdisk /dev/sda

```

Presione `p` para imprimir la tabla de particiones y tome nota de los números de partición para los que desea desactivar el montaje automático.

Presione `x` *extra functionality (experts only)*.

Presione `a` *set attributes*. Ingrese el número de partición y establezca el atributo `63`. En `Set fields are:` ahora debería mostrar `63 (do not automount)`. Presione `Intro` para finalizar el cambio de atributo. Repita este proceso para todas las particiones que desee evitar que se monten automáticamente.

Cuando termine, escriba la tabla en el disco y salga con la orden `w`.

Alternativamente, utilizando *sgdisk*, el atributo se puede establecer usando la opción `-A`/`--attributes=`; vea [sgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sgdisk.8) para su utilización. Por ejemplo, para establecer el atributo de partición `63` "do not automount" en `/dev/sda2` ejecute:

```
# sgdisk -A 2:set:63 /dev/sda

```

### Apliación gdisk para EFI

No hay un paquete gdisk para la versión EFI, pero Rod Smith proporciona un binario gdisk precompilado para EFI en [SourceForge](https://sourceforge.net/projects/gptfdisk/files/gptfdisk/). Descargue `gdisk-efi-*.zip` y extraiga el archivo. Para usarlo, copie `gdisk_x64.efi` en la [EFI system partition](/index.php/EFI_system_partition_(Espa%C3%B1ol) "EFI system partition (Español)") y láncelo desde su [gestor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)") o [Shell de UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol)#Shell_de_UEFI "Unified Extensible Firmware Interface (Español)").

*gdisk_x64.efi* le permite editar la tabla de particiones incluso antes de que se inicie el sistema operativo. Se usa de la misma manera que el binario *gdisk* en Linux.

**Nota:** *gdisk_x64.efi* no puede acceder al sistema de archivos, por lo tanto, no puede hacer una copia de seguridad de la tabla de particiones ni restaurarla desde la copia de seguridad.

Consulte [README-efi.txt](https://sourceforge.net/p/gptfdisk/code/ci/master/tree/README-efi.txt) para obtener más información.

## Véase también

*   [GPT fdisk Tutorial](https://www.rodsbooks.com/gdisk/index.html) — página web oficial de GPT fdisk con tutoriales detallados.
*   [página SourceForge de GPT fdisk](https://sourceforge.net/projects/gptfdisk/)