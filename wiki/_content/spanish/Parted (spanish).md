Artículos relacionados

*   [fdisk (Español)](/index.php/Fdisk_(Espa%C3%B1ol) "Fdisk (Español)")
*   [GPT fdisk (Español)](/index.php/GPT_fdisk_(Espa%C3%B1ol) "GPT fdisk (Español)")
*   [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Parted](/index.php/Parted "Parted"), revisada por última vez el **2019-11-04**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Parted&diff=0&oldid=587757) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[GNU Parted](https://www.gnu.org/software/parted/parted.html) es un programa para crear y manipular tablas de particiones. GParted es su versión de interfaz gráfica de usuario.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
    *   [2.1 Modalidad en línea de órdenes](#Modalidad_en_línea_de_órdenes)
    *   [2.2 Modalidad interactiva](#Modalidad_interactiva)
*   [3 Redondeo](#Redondeo)
*   [4 Particionar](#Particionar)
    *   [4.1 Crear nueva tabla de particiones](#Crear_nueva_tabla_de_particiones)
    *   [4.2 Esquemas de particiones](#Esquemas_de_particiones)
        *   [4.2.1 Ejemplos UEFI/GPT](#Ejemplos_UEFI/GPT)
        *   [4.2.2 Ejemplos BIOS/MBR](#Ejemplos_BIOS/MBR)
    *   [4.3 Redimensionar particiones](#Redimensionar_particiones)
        *   [4.3.1 Aumentar particiones](#Aumentar_particiones)
        *   [4.3.2 Reducir particiones](#Reducir_particiones)
*   [5 Advertencias](#Advertencias)
    *   [5.1 Alineamiento](#Alineamiento)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 Arranque dual con Windows XP](#Arranque_dual_con_Windows_XP)
    *   [6.2 Verificar alineación](#Verificar_alineación)
*   [7 Solución de problemas](#Solución_de_problemas)
    *   [7.1 Partición FAT32 redimensionada y luego no reconocida en Windows](#Partición_FAT32_redimensionada_y_luego_no_reconocida_en_Windows)
*   [8 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [parted](https://www.archlinux.org/packages/?name=parted). Para una interfaz gráfica, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gparted](https://www.archlinux.org/packages/?name=gparted), el [frontend](https://en.wikipedia.org/wiki/es:Front-end_y_back-end "wikipedia:es:Front-end y back-end") gráfico para *parted*.

## Utilización

Parted tiene dos modos: en línea de órdenes e interactivo. Parted siempre debe comenzar con:

```
# parted device

```

donde `*device*` es el dispositivo de disco duro para editar (por ejemplo, `/dev/sda`). Si omite el argumento `*device*`, *parted* intentará adivinar qué dispositivo desea.

### Modalidad en línea de órdenes

En el modo de línea de órdenes, lo anterior va seguido por una o más órdenes. Por ejemplo:

```
# parted /dev/sda mklabel gpt mkpart P1 ext3 1MiB 8MiB 

```

**Nota:** las opciones (como `--help`) solo se pueden especificar en la línea de órdenes.

### Modalidad interactiva

El modo interactivo simplifica el proceso de partición y reduce la repetición innecesaria de órdenes al aplicar automáticamente todas las órdenes de particionado al dispositivo especificado.

Para comenzar a operar sobre un dispositivo, ejecute:

```
# parted /dev/sd*x*

```

Notará que el indicador de la línea de órdenes cambia de un símbolo (`#`) a `(parted)`: esto también significa que el nuevo indicador no es una orden que deba ingresarse manualmente para ejecutar las órdenes dadas en los ejemplos.

Para ver una lista de las órdenes disponibles, escriba:

```
(parted) help

```

Cuando termine, o si desea implementar una tabla de particiones o esquema para otro dispositivo, salga de Parted con:

```
(parted) quit

```

Después de salir, el [prompt](https://en.wikipedia.org/wiki/es:Prompt "wikipedia:es:Prompt") de la línea de órdenes cambiará nuevamente a `#`.

Si no le proporciona un parámetro a una orden, Parted se lo solicitará. Por ejemplo:

```
(parted) mklabel
New disk label type? gpt

```

## Redondeo

Dado que muchos sistemas de particionamiento tienen restricciones complicadas, Parted generalmente hará algo ligeramente diferente a lo que le solicitó. (Por ejemplo, crear una partición comenzando en 10.352Mb, no en 10.4Mb). ​​Si los valores calculados difieren demasiado, Parted le pedirá confirmación. Si sabe exactamente lo que quiere o para ver exactamente qué está haciendo Parted, es útil especificar puntos finales de la partición en sectores (con el sufijo «s») y dar la orden «unit s» para que los puntos finales de la partición se muestren en los sectores.

A partir de parted 2.4, cuando se especifican valores iniciales y/o finales utilizando unidades binarias IEC como «MiB», «GiB», «TiB», etc., parted trata esos valores como exactos y equivalentes al mismo número especificado en bytes (es decir, con el sufijo «B»), ya que no proporciona un rango de desajuste «relevante». Compare eso con una solicitud de partición inicial de «4 GB», que en realidad puede resolverse en algún sector 500 MB antes o después de ese punto. Por lo tanto, al crear una partición, sería preferible especificar unidades en bytes («B»), sectores («s») o [unidades binarias](https://en.wikipedia.org/wiki/es:Prefijo_binario "wikipedia:es:Prefijo binario") fijadas por la [IEC](https://en.wikipedia.org/wiki/es:Comisi%C3%B3n_Electrot%C3%A9cnica_Internacional "wikipedia:es:Comisión Electrotécnica Internacional") como «MiB», pero no «MB», «GB», etc.

## Particionar

### Crear nueva tabla de particiones

Debe (re)crear la tabla de particiones de un dispositivo cuando nunca se ha particionado antes, o cuando desea cambiar el tipo de su tabla de particiones. La recreación de la tabla de particiones de un dispositivo también es útil cuando el esquema de partición necesita ser reestructurado desde cero.

Abra cada dispositivo cuya tabla de particiones quiere (re)crear con:

```
# parted /dev/sd*x*

```

Para crear una nueva [tabla de partición GUID](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)"), utilice la siguiente orden:

```
(parted) mklabel gpt

```

Para crear una nueva tabla de partición [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")/MS-DOS, utilice en su lugar:

```
(parted) mklabel msdos

```

### Esquemas de particiones

Puede decidir el número y el tamaño de las particiones en las que se deben dividir los dispositivos, y qué directorios se usarán para montar las particiones en el sistema instalado (también conocido como *puntos de montaje*). Vea [Partitioning (Español)#Esquemas de particiones](/index.php/Partitioning_(Espa%C3%B1ol)#Esquemas_de_particiones "Partitioning (Español)") para las particiones necesarias.

La siguiente orden se utilizará para crear las particiones:

```
(parted) mkpart *part-type* *fs-type* *start* *end*

```

*   `*part-type*` se refiere a uno de los tipos de partición `primary`, `extended` o `logical`, y es significativo solo para las tablas de partición MBR.
*   `*fs-type*` es un identificador elegido entre los enumerados al escribir `help mkpart` como la coincidencia más cercana al sistema de archivos que usará. La orden *mkpart* en realidad no crea el sistema de archivos: el parámetro `*fs-type*` simplemente será utilizado por *parted* para establecer un código de 1 byte que se usará por el cargador de arranque para «previsualizar» qué tipo de datos se encuentran en la partición y actuar en consecuencia si es necesario. Vea también [Wikipedia:Disk partitioning#PC partition types](https://en.wikipedia.org/wiki/Disk_partitioning#PC_partition_types "wikipedia:Disk partitioning").

**Sugerencia:** la mayoría de los [sistemas de archivos nativos de Linux](https://en.wikipedia.org/wiki/File_system#Linux "wikipedia:File system") mapean el mismo código de tipo de partición MBR ([0x83](https://en.wikipedia.org/wiki/Partition_type#PID_83h "wikipedia:Partition type")), por lo que es perfectamente seguro, por ejemplo, utilizar `ext2` para una partición formateada con *ext4*.

*   `*start*` es el comienzo de la partición desde el inicio del dispositivo. Consiste en un número seguido de una [unidad](http://www.gnu.org/software/parted/manual/parted.html#unit), por ejemplo, `1MiB` significa comenzar en 1 MiB.
*   `*end*` es el final de la partición desde el inicio del dispositivo (*no* desde el valor dado para `*start*`). Tiene la misma sintaxis que `*start*`, por ejemplo, `100%` significa el extremo final del dispositivo (esto es, utilizar todo el espacio restante).

**Sugerencia:** en un disco con una tabla de partición MBR, deje al menos 33 sectores de 512 bytes (16.5 KiB) de espacio libre sin particionar al final del disco para permitir [convertir MBR a GPT](/index.php/GPT_fdisk_(Espa%C3%B1ol)#Conversión_de_MBR_a_GPT_(y_viceversa) "GPT fdisk (Español)").

**Advertencia:** es importante que las particiones no se superpongan entre sí: si no desea dejar espacio sin utilizar en el dispositivo, asegúrese de que cada partición comience donde termina la anterior.

**Nota:** *parted* puede emitir una advertencia como:
```
Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel?

```
En este caso, lea [Partitioning (Español)#Alineamiento de las particiones](/index.php/Partitioning_(Espa%C3%B1ol)#Alineamiento_de_las_particiones "Partitioning (Español)") y siga [#Alineamiento](#Alineamiento) para arreglarlo.

La siguiente orden se utilizará para marcar la partición que contiene el directorio `/boot` como de arranque:

```
(parted) set *partition* boot on

```

*   `*partition*` es el número de la partición que se marcará (consulte el resultado con la orden `print`).

#### Ejemplos UEFI/GPT

En cualquier caso, se requiere una [EFI system partition](/index.php/EFI_system_partition "EFI system partition") especial de arranque.

Si crea una nueva EFI System Partition, utilice las siguientes órdenes (el tamaño recomendado es de, al menos, 260 MiB):

```
(parted) mkpart primary fat32 1MiB 261MiB
(parted) set 1 esp on

```

El esquema de particionado restante depende totalmente de sus necesidades. Para crear otra partición con el 100% del espacio restante:

```
(parted) mkpart primary ext4 261MiB 100%

```

Para particiones separadas `/` (20 GiB) y `/home` (todo el espacio restante):

```
(parted) mkpart primary ext4 261MiB 20.5GiB
(parted) mkpart primary ext4 20.5GiB 100%

```

Y para particiones separadas `/` (20 GiB), swap (4 GiB) y `/home` (todo el espacio restante):

```
(parted) mkpart primary ext4 261MiB 20.5GiB
(parted) mkpart primary linux-swap 20.5GiB 24.5GiB
(parted) mkpart primary ext4 24.5GiB 100%

```

#### Ejemplos BIOS/MBR

Para una partición primaria única (esto es, lo mínimo) que utilice todo el espacio disponible en disco, se usaría la siguiente orden:

```
(parted) mkpart primary ext4 1MiB 100%
(parted) set 1 boot on

```

En el siguiente ejemplo, se creará una partición de 20 GiB `/`, seguida de una partición `/home` utilizando todo el espacio restante:

```
(parted) mkpart primary ext4 1MiB 20GiB
(parted) set 1 boot on
(parted) mkpart primary ext4 20GiB 100%

```

En el ejemplo final siguiente, se crearán particiones separadas `/boot` (100 MiB), `/` (20 GiB), swap (4 GiB) y `/home` (todo el espacio restantes):

```
(parted) mkpart primary ext3 1MiB 100MiB
(parted) set 1 boot on
(parted) mkpart primary ext3 100MiB 20GiB
(parted) mkpart primary linux-swap 20GiB 24GiB
(parted) mkpart primary ext3 24GiB 100%

```

### Redimensionar particiones

**Advertencia:** las particiones ext2/3/4 que se estén redimensionando deben estar desmontadas y no estar en uso. Es difícil y peligroso intentar editar el sistema de archivos raíz desde un sistema operativo en ejecución; utilice un sistema de rescate o un soporte live en su lugar.

**Nota:**

*   Solo puede mover el final de la partición con `parted`.
*   A partir de la versión 4.2 de parted *resizepart* puede necesitar el uso de la [#Modalidad interactiva](#Modalidad_interactiva).[[1]](https://bugs.launchpad.net/ubuntu/+source/parted/+bug/1270203)
*   Estas instrucciones se aplican a particiones que tienen sistemas de archivos ext2, ext3, ext4 o btrfs.

Si está ampliando una partición, primero debe cambiar el tamaño de la partición y luego cambiar el tamaño del sistema de archivos presente en ella, mientras que para reducir el tamaño de la partición primero debe cambiar el tamaño del sistema de archivos antes de la partición para evitar la pérdida de datos.

#### Aumentar particiones

Para hacer crecer una partición (en modo interactivo de parted):

```
(parted) resizepart *number* *end*

```

Donde `*number*` es el número de la partición que está aumentando, y `*end*` es el nuevo final de la partición (que debe ser mayor que el final anterior).

Luego, para hacer aumentar el sistema de archivos (ext2/3/4) en la partición:

```
# resize2fs /dev/*sdaX* *[size]*

```

O, para hacer aumentar un sistema de archivos Btrfs:

```
# btrfs filesystem resize /dev/*sdaX* *[size]*

```

Donde `*sdaX*` representa la partición que está creciendo, y `*[size]*` es el nuevo tamaño de la partición. Tenga en cuenta que `*[size]*` es opcional, déjelo vacío para llenar el espacio restante en la partición.

#### Reducir particiones

Para reducir un sistema de archivos ext2/3/4 en la partición:

```
# resize2fs /dev/*sdaX* *size*

```

Para reducir un sistema de archivos Btrfs:

```
# btrfs filesystem resize /dev/*sdaX* *size*

```

Donde `*sdaX*` representa la partición que está reduciendo, y `*size*` es el nuevo tamaño de la partición.

Luego, reduzca la partición (en modo interactivo de parted):

```
(parted) resizepart *number* *end*

```

Donde `*number*` es el número de la partición que está reduciendo, y `*end*` es el nuevo final de la partición (que debe ser más pequeño que el final anterior).

Cuando termine, utilice la orden *resizepart* de [util-linux](https://www.archlinux.org/packages/?name=util-linux) para informar al kernel sobre el nuevo tamaño:

```
# resizepart *device* *number* *size*

```

Donde `*device*` es el dispositivo que contiene la partición, `*number*` es el número de la partición y `*size*` es el nuevo tamaño de la partición.

## Advertencias

Parted siempre le advertirá antes de hacer algo que sea potencialmente peligroso, a menos que la orden sea una de las que por sí sea inherentemente peligrosa (a saber, rm, mklabel y mkpart).

### Alineamiento

Al crear una partición, *parted* puede advertir sobre una alineación incorrecta de la partición, pero sin sugerir una alineación adecuada. Por ejemplo:

```
(parted) mkpart primary fat16 0 32M
Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel?                                                     

```

La advertencia significa que el inicio de la partición no está alineado. Introduzca «Ignore» para continuar de todos modos, imprima la tabla de particiones por sectores para ver dónde comienza y elimine/vuelva a crear la partición con el sector de inicio redondeado a potencias crecientes de 2 hasta que se detenga la advertencia. Como ejemplo, en una unidad flash con sectores de 512B, Parted requerirá que las particiones comiencen en sectores que sean un múltiplo de 2048, que es una alineación de 1 MiB.

Si desea que *parted* intente calcular por usted la alineación correcta, especifique la posición de inicio como 0% en lugar de algún valor concreto. Para crear una gran partición ext4, su orden se vería así:

```
(parted) mkpart primary ext4 0% 100%

```

## Consejos y trucos

### Arranque dual con Windows XP

Si tiene una partición de Windows XP que le gustaría mover de unidad a unidad que también resulta que es su partición de arranque, puede hacerlo fácilmente con GParted y mantener a Windows funcional simplemente eliminando la siguiente clave de registro ANTES de mover la partición:

```
HKEY_LOCAL_MACHINE\SYSTEM\MountedDevices

```

Referencia de esta pequeña joya [aquí](http://gparted-forum.surf4.info/viewtopic.php?pid=8347#p8347).

### Verificar alineación

En un disco ya particionado, puede usar *parted* para verificar la alineación de una partición en un dispositivo. Por ejemplo, para verificar la alineación de la partición 1 en `/dev/sda`:

```
# parted /dev/sda
(parted) align-check optimal 1
1 aligned

```

## Solución de problemas

### Partición FAT32 redimensionada y luego no reconocida en Windows

A fecha de diciembre de 2018, existía [un error antiguo](http://git.savannah.gnu.org/cgit/parted.git/commit/?id=c0d394abac4d6d2ce35c98585b6ecb33aea48583) en parted, que [se ha solucionado](http://git.savannah.gnu.org/cgit/parted.git/commit/?id=3447264ba9fedf236da92b2199a2b4823b773cf5) por los desarrolladores pero [nunca se ha publicado](https://bugzilla.gnome.org/show_bug.cgi?id=759916#c18) y, por lo tanto, todavía no está presente en ArchLinux.

Este error hace que se separen los primeros bytes de las particiones FAT32 redimensionadas, que luego no se reconocen en Windows (a pesar de que no se pierden los datos del usuario, y las particiones son totalmente montables en Linux).

Tales particiones corruptas se pueden reparar con la línea:

```
# echo -ne '\xeb\x58\x90' | dd conv=notrunc bs=1 count=3 of=*/dev/sdxy*

```

donde `/dev/sdxy` es la partición dañada (por ejemplo, `/dev/sdb1`).

## Véase también

*   [GNU parted - Manual de usuario de Parted](https://www.gnu.org/software/parted/manual/)
*   [Cómo alinear particiones para un mejor rendimiento utilizando parted](http://rainbow.chard.org/2013/01/30/how-to-align-partitions-for-best-performance-using-parted/)
*   [Cambiar el tamaño de una partición ext3/ext4](http://positon.org/resize-an-ext3-ext4-partition)
*   [Foros oficiales de GParted](http://gparted-forum.surf4.info/)