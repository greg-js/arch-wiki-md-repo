Artículos relacionados

*   [fstab (Español)](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)")
*   [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)")
*   [Swap (Español)](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)")
*   [File Systems (Español)](/index.php/File_Systems_(Espa%C3%B1ol) "File Systems (Español)")

*Particionar* un disco duro significa dividir lógicamente el espacio disponible en secciones a las que se puede acceder de forma independiente una de otra.

Un disco duro completo se puede o bien asignar a una sola partición, o bien se puede dividir el espacio de almacenamiento disponible en varias particiones. La existencia de una variedad de escenarios requieren la creación de múltiples particiones: dual o multi-arranque, por ejemplo, o el mantenimiento de un partición [swap](/index.php/Swap "Swap"). En otros casos, la partición se utiliza como un medio para guardar datos separados lógicamente, como crear particiones para guardar los archivos de audio y vídeo. Los esquemas de particionado más comunes se tratan con más detalle a continuación.

Cada partición debe ser formateada con un [tipo de sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") antes de ser utilizada.

## Contents

*   [1 Tabla de particiones](#Tabla_de_particiones)
    *   [1.1 Master Boot Record](#Master_Boot_Record)
    *   [1.2 GUID Partition Table](#GUID_Partition_Table)
    *   [1.3 Particionado con Btrfs](#Particionado_con_Btrfs)
    *   [1.4 Elegir entre GPT y MBR](#Elegir_entre_GPT_y_MBR)
*   [2 Esquemas de particionado](#Esquemas_de_particionado)
    *   [2.1 Partición única root](#Partición_única_root)
    *   [2.2 Particiones dedicadas](#Particiones_dedicadas)
    *   [2.3 Puntos de montaje](#Puntos_de_montaje)
        *   [2.3.1 Partición raíz](#Partición_raíz)
        *   [2.3.2 /boot](#/boot)
        *   [2.3.3 /home](#/home)
        *   [2.3.4 /var](#/var)
        *   [2.3.5 /tmp](#/tmp)
        *   [2.3.6 Swap](#Swap)
        *   [2.3.7 ¿Qué tamaño deben tener las particiones?](#¿Qué_tamaño_deben_tener_las_particiones?)
*   [3 Herramientas de particionado](#Herramientas_de_particionado)
*   [4 Alineamiento de las particiones](#Alineamiento_de_las_particiones)
    *   [4.1 Unidades de disco duro](#Unidades_de_disco_duro)
    *   [4.2 Unidades de estado sólido](#Unidades_de_estado_sólido)
    *   [4.3 Herramientas de particionado](#Herramientas_de_particionado_2)
*   [5 Usar GPT - método moderno](#Usar_GPT_-_método_moderno)
    *   [5.1 Resumen del uso de gdisk](#Resumen_del_uso_de_gdisk)
*   [6 Usar MBR - método tradicional](#Usar_MBR_-_método_tradicional)
    *   [6.1 Resumen del uso de fdisk](#Resumen_del_uso_de_fdisk)
*   [7 Véase también](#Véase_también)

## Tabla de particiones

La información de las particiones se almacena en la tabla de particiones, para lo cual hay 2 formatos en uso hoy en día. El clásico [Master Boot Record](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)") y la moderna [GUID Partition Table](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)"), que es una versión mejorada que elimina varias limitaciones.

### Master Boot Record

MBR originalmente solo admitía hasta 4 particiones. Más tarde, se ampliaron al introducir particiones lógicas para superar esta limitación.

Existen tres tipos de particiones de disco:

*   Primaria
*   Extendida
    *   Lógica

La particiones **primarias** pueden ser todas configuradas como booteables (de arranque) y están limitadas a cuatro por disco o volumen RAID. Si un esquema de particionado necesita más de cuatro particiones, se utilizará una partición **extendida** para contener particiones **lógicas**. Las particiones extendidas están pensadas para contener particiones lógicas. Un disco duro no puede contener más de una partición extendida. La partición extendida también se cuenta como una partición primaria, por lo que si el disco tiene una partición extendida, solo son posibles tres particiones primarias adicionales (es decir, tres particiones primarias y una partición extendida). El número de particiones lógicas que pueden residir en una partición extendida es ilimitado. Un sistema de arranque dual con Windows requiere que Windows resida en una partición primaria.

El esquema de numeración habitual es crear particiones primarias *sda1* a *sda3*, seguido de una partición extendida *sda4*. Las particiones lógicas en *sda4* son numeradas como *sda5*, *sda6*, etc.

Véase también [Wikipedia:es:Master boot record](https://en.wikipedia.org/wiki/es:Master_boot_record "wikipedia:es:Master boot record").

### GUID Partition Table

Existe un solo tipo de partición, **primaria**. La cantidad de particiones por disco o volumen RAID es ilimitado.

Véase también [Wikipedia:es:GUID Partition Table](https://en.wikipedia.org/wiki/es:GUID_Partition_Table "wikipedia:es:GUID Partition Table").

### Particionado con Btrfs

Btrfs pueden ocupar todo un dispositivo de almacenamiento de datos y reemplazar los esquemas de particionado [MBR](/index.php/MBR "MBR") o [GPT](/index.php/GPT "GPT"). Véanse las instrucciones de [Btrfs Partitioning](/index.php/Btrfs#Partitioning "Btrfs") para conocer más detalles.

Véase también [Wikipedia:es:Btrfs](https://en.wikipedia.org/wiki/es:Btrfs "wikipedia:es:Btrfs").

### Elegir entre GPT y MBR

[GUID Partition Table (Español)](/index.php/GUID_Partition_Table_(Espa%C3%B1ol) "GUID Partition Table (Español)") (GPT) es una alternativa, el estilo de partición actual. Tiene la intención de sustituir el viejo sistema [Master Boot Record (Español)](/index.php/Master_Boot_Record_(Espa%C3%B1ol) "Master Boot Record (Español)") (MBR). GPT tiene varias ventajas sobre el MBR, que tiene peculiaridades que datan de tiempos de MS-DOS. Con los desarrollos recientes en el formato de las herramientas *fdisk* (MBR) y *gdisk* (GPT), es igual de fácil usar GPT o MBR y obtener el máximo rendimiento.

La elección básicamente se reduce a esto:

*   Si se utiliza GRUB Legacy como el gestor de arranque, es necesario utilizar MBR.
*   Para un arranque dual con Windows (32 bits y 64 bits) utilizando Legacy BIOS, se debe usar MBR.
*   Para un arranque dual con Windows de 64 bits que utiliza UEFI en lugar del BIOS, se debe usar GPT.
*   Si no se dan ninguna de las circunstancias anteriores, elija libremente entre GPT y MBR; dado que GPT es más moderno, se recomienda en este caso.
*   Se recomienda siempre usar GPT con el arranque UEFI dado que algunos firmwares UEFI no permiten arrancar UEFI desde MBR.

**Nota:** Para arrancar GRUB en un esquema de particionado GPT en un sistema BIOS, es necesario crear una [BIOS boot partition](/index.php/GRUB_(Espa%C3%B1ol)#Instrucciones_espec.C3.ADficas_para_GUID_Partition_Table_.28GPT.29 "GRUB (Español)").

## Esquemas de particionado

No hay reglas estrictas para crear particiones en un disco duro, aunque se puede seguir la orientación general que se da a continuación. El esquema de una partición de disco está determinado por diversos temas como la flexibilidad deseada, la velocidad, la seguridad, así como las limitaciones impuestas por el espacio disponible en el disco. Se trata esencialmente de una cuestión de preferencia personal. Si se desea un arranque dual de Arch Linux con un sistema operativo Windows, por favor vea [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot").

### Partición única root

Este esquema es el más simple y debería ser suficiente para la mayoría de los casos al uso. El [archivo swap](/index.php/Swapfile "Swapfile") se puede crear fácilmente y cambiarlo de tamaño según convenga. Por lo general, tiene sentido empezar por considerar una sola partición `/` y luego otras separadas a partir de esta última en función del uso específico que se les vaya a dar como raid, cifrado, una partición compartida de archivos multimedia, etc.

### Particiones dedicadas

Crear una ruta de acceso como una partición separada permite elegir entre diferentes sistema de archivos y opciones de montaje. En algunos casos como una partición para los archivos multimedia, de modo que los mismos también puedan ser compartidos entre distintos sistemas operativos.

### Puntos de montaje

Los puntos de montaje siguientes son opciones posibles para particiones separadas, tome la decisión sobre la base de sus necesidades reales.

#### Partición raíz

El directorio raíz está en la parte superior de la jerarquía, el punto en el que está montado el sistema de archivos principal y de la que se derivan todos los demás sistemas de archivos. Todos los archivos y directorios aparecen debajo del directorio raíz *`/`*, incluso si están almacenados en diferentes dispositivos físicos. El contenido del sistema de archivos raíz debe ser adecuado para arrancar, restaurar, recuperar y/o reparar el sistema. Por lo tanto, ciertos directorios de *`/`* no son candidatos para particiones separadas.

La partición `/` o la partición raíz es necesaria y es la más importante. Las otras particiones pueden ser reemplazadas por ella.

**Advertencia:** Los directorios esenciales para el arranque **deben** estar en la misma partición que **`/`** o montados en el primer espacio de usuario por [initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"). Estos directorios esenciales son: `/etc` y `/usr`[[1]](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken).

#### /boot

El directorio `/boot` contiene las imágenes del kernel y del ramdisk, así como el archivo de configuración del gestor de arranque y las etapas del mismo. También almacena datos que se utilizan por el kernel antes de que se ejecuten los programas en el espacio de usuario. `/boot` no es necesario para el funcionamiento normal del sistema, tan solo durante las actualizaciones del arranque y del kernel (al regenerar la imagen del disco RAM inicial).

Si se instala un sistema de RAID0 software (stripe) es necesaria una partición `/boot` separada.

#### /home

La directorio `/home` contiene los archivos de configuración específicos del usuario, la memoria caché de los datos de las aplicaciones y los archivos multimedia.

Mantener `/home` en una partición separada de `/` permite redimensionarlas por separado, lo cual puede ser útil para el caso de que vuelva a reinstalar el sistema, pero tenga en cuenta que todavía puede volver a instalar Arch dejando el directorio `/home` intacto, incluso si no está en una partición separada (basta con eliminar los directorios de nivel superior y, entonces, ejecutar pacstrap).

No es buena práctica compartir directorios entre usuarios de diferentes distribuciones, ya que utilizan versiones incompatibles de software y parches. En su lugar, considere la posibilidad de compartir una partición de archivos multimedia o, al menos, utilizar diferentes directorios personales en la misma partición `/home`.

#### /var

El directorio `/var` guarda datos de variables como archivos y directorios spool, datos administrativos y de registro, caché de [pacman](/index.php/Pacman "Pacman"), el árbol [ABS](/index.php/Arch_Build_System "Arch Build System"), etc. Es utilizada, por ejemplo, para el almacenamiento de la caché y del registro, y, por lo tanto, leído o escrito con frecuencia. El que todo quede en una partición separada evita quedarse sin espacio en el disco debido a los registros flunky, etc.

Si existe, es posible montar *`/usr`* como solo lectura. Todo lo que históricamente fue a *`/usr`* escrito durante las operaciones del sistema (en oposición a la instalación y mantenimiento del software) deben residir en *`/var`*.

**Nota:** `/var` contiene muchos archivos pequeños. La elección del tipo de sistema de archivos (véase más abajo) debe tener esto en cuenta si se crea como partición separada.

#### /tmp

De hecho es una partición separada por defecto, en virtud de ser montado como *tmpfs* por systemd.

#### Swap

El partición [swap](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)") proporciona una memoria que se puede utilizar como RAM virtual. También puede ser considerado el uso de un [archivo swap](/index.php/Swapfile "Swapfile") ya que no tienen casi ninguna diferencia de rendimiento en comparación con una partición, pero son mucho más fáciles de redimensionar según sea necesario. Una partición swap puede ser *potencialmente* compartida entre distintos sistemas operativos, pero no si se utiliza la hibernación.

#### ¿Qué tamaño deben tener las particiones?

**Nota:**

*   Lo que sigue son simples recomendaciones; no hay una regla que dictamine el tamaño óptimo de una partición.
*   Si tiene espacio disponible, un margen adicional del 25% para cada sistema de archivos proporciona seguridad para su posible expansión futura y ayuda a protegerlos contra la fragmentación.

El tamaño de las particiones es una cuestión de preferencia personal, pero la información siguiente puede servir de orientación:

	`/boot` — 200 MB 

	Una partición `/boot` requiere solo unos 100 MB, pero si es propenso a utilizar varias imágenes del kernel/boot, 200 o 300 MB es una mejor elección.

	`/` — 15-20 GB 

	Esta partición contiene tradicionalmente el directorio `/usr`, que puede crecer significativamente dependiendo de cuánto software se instale. 15-20 GB debería ser suficiente para la mayoría de los usuarios con los discos duros modernos.

	`/var` — 8-12 GB 

	El sistema de archivos `/var` contiene, entre otros datos, el árbol [ABS](/index.php/Arch_Build_System "Arch Build System") y la caché de [pacman](/index.php/Pacman "Pacman"). Mantener los paquetes almacenados en la memoria caché es útil y versátil, ya que proporciona la capacidad de realizar downgrade. Como resultado, `/var` tiende a crecer en tamaño. La caché de pacman, en particular, crecerá a medida que el sistema se amplíe y se actualice. Puede, sin embargo, de forma segura, borrar si la falta de el espacio se convierte en un problema. Para un sistema de escritorio, 8-12 GB debe ser suficiente para `/var`, dependiendo de cuánto software se tenga previsto instalar.

	`/home` — [variable] 

	El sistema de archivos `/home` es normalmente donde residen los datos del usuario, las descargas y los archivos multimedia. En un sistema de escritorio, el sistema de archivos `/home` es, generalmente, el de mayor tamaño del disco.

	`swap` — [variable] 

	Históricamente, la regla general para determinar el tamaño de la partición de intercambio consistía en asignarle el doble de la cantidad de RAM física. A medida que los ordenadores han ido ganando cada vez mayores capacidades de memoria, esta regla ha devenido obsoleta. En las máquinas con hasta 512 MB de RAM, la regla 2x es normalmente suficiente. Si está disponible una cantidad suficiente de RAM (más de 1024), es posible tener una partición de intercambio más pequeña o incluso omitirla. Con más de 2 GB de memoria RAM física, generalmente se puede esperar un buen rendimiento sin la existencia de una partición de intercambio.

**Nota:** Si va a utilizar una partición/archivo swap para hibernar, debe echar un vistazo a [Suspend and hibernate#About swap partition/file size](/index.php/Suspend_and_hibernate#About_swap_partition/file_size "Suspend and hibernate").

	`/datos` — [variable] 

	Se puede considerar el montaje de una partición para «datos» para contener archivos para ser compartidos por todos los usuarios. La utilización de la partición `/home` para este fin también es válido.

## Herramientas de particionado

*   **fdisk** — Herramienta de particionado de terminal incluida en Linux.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **cfdisk** — Herramienta de particionado de terminal escrito con las bibliotecas ncurses.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

**Advertencia:** La primera partición creada por *cfdisk* comienza en el sector 63, en lugar de los habituales 2048\. Esto puede conducir a una reducción del rendimiento en el SSD y en las unidades (sector 4k) de formato avanzado. También causará problemas con [GRUB](/index.php/GRUB_(Espa%C3%B1ol)#Mensaje_de_error_msdos-style "GRUB (Español)"). En cambio, grub-legacy y syslinux deberían funcionar bien.

*   **gdisk** — Versión de fdisk para [GPT](/index.php/GPT "GPT").

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **cgdisk** — Versión de cfdisk para [GPT](/index.php/GPT "GPT").

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **sgdisk** — Versión de script de gdisk.

	[http://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html](http://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **[GNU Parted](/index.php/GNU_Parted "GNU Parted")** — Herramienta de particionado de terminal.

	[http://www.gnu.org/software/parted/parted.html](http://www.gnu.org/software/parted/parted.html) || [parted](https://www.archlinux.org/packages/?name=parted)

*   **[GParted](/index.php/GParted "GParted")** — Herramienta gráfica escrita en GTK.

	[http://gparted.sourceforge.net/](http://gparted.sourceforge.net/) || [gparted](https://www.archlinux.org/packages/?name=gparted)

*   **Partitionmanager** — Herramienta gráfica escrita en QT.

	[http://sourceforge.net/projects/partitionman/](http://sourceforge.net/projects/partitionman/) || [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)

*   **QtParted** — Similar a Partitionmanager, disponible en [AUR](/index.php/AUR "AUR").

	[http://qtparted.sourceforge.net/](http://qtparted.sourceforge.net/) || [qtparted](https://aur.archlinux.org/packages/qtparted/)

## Alineamiento de las particiones

La alineación adecuada de la partición es esencial para obtener un rendimiento óptimo y duradero. Esta es definida por la naturaleza del [bloque](https://en.wikipedia.org/wiki/Block_(data_storage) de cada operación de E/S a nivel del hardware en combinación con el sistema de archivos. La clave para el alineamiento es particionar según (al menos) el *tamaño del bloque* dado, que va a depender del hardware utilizado. Si las particiones no están alineadas para comenzar con múltiplos del *tamaño del bloque*, el alineamiento del sistema de archivos será un ejercicio estéril, porque todo estará sesgado por el desplazamiento inicial de la partición.

### Unidades de disco duro

Tradicionalmente, los discos duros se trataron mediante la indicación del *cilindro*, el *cabezal* y el *sector* en el que los datos se iban a leer o escribir (también conocido como [CHS addressing](https://en.wikipedia.org/wiki/es:Cylinder-head-sector "wikipedia:es:Cylinder-head-sector")). Estos representaban la posición radial, la cabeza de la unidad (disco y laterales) y la posición axial de los datos, respectivamente. Hoy en día, con el [direccionamiento de bloque lógico](https://en.wikipedia.org/wiki/es:Logical_block_addressing "wikipedia:es:Logical block addressing"), todo el disco duro es tratado como un flujo continuo de datos y el término [sector](https://en.wikipedia.org/wiki/Disk_sector "wikipedia:Disk sector") designa la unidad más pequeña identificable.

### Unidades de estado sólido

Las unidades de estado sólido se basan en [memorias flash](https://en.wikipedia.org/wiki/es:Flash_memory "wikipedia:es:Flash memory"), y, por lo tanto, difieren significativamente de los discos duros. Mientras que la lectura sigue siendo posible en forma de acceso aleatorio, el borrado (de ahí la reescritura y la escritura aleatoria) es solo posible por [bloques enteros](https://en.wikipedia.org/wiki/Flash_memory#Block_erasure "wikipedia:Flash memory"). Además, el *tamaño del bloque de borrado* (EBS) es significativamente mayor que el *tamaño del bloque* tradicional, por ejemplo 128KiB vs. 4KiB, por lo que la alineación ha de hacerse a múltiplos de EBS.

### Herramientas de particionado

En el pasado, la alineación adecuada requería la intervención y el calculo manual durante el particionado. Ahora hay muchas herramientas de particionado común que gestionan la alineación de las particiones de forma automática:

*   fdisk
*   gdisk
*   gparted
*   parted

Para verificar que una partición está alineada, se puede consultar con `/usr/bin/blockdev` como se muestra a continuación. Si la salida devuelve un '0', la partición está alineada:

```
# blockdev --getalignoff /dev/<partición>
0

```

## Usar GPT - método moderno

### Resumen del uso de gdisk

Usando GPT, la utilidad para editar la tabla de particiones se llama `fdisk`. Esta realiza la alineación de la partición de forma automática al sector 2048 (o 1024KiB), base del tamaño del bloque, que tendría que ser compatible con la gran mayoría de los SSD, si no todos. GNU Parted también soporta GPT, pero es [menos fácil de usar](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=601813) para alinear las particiones. El entorno proporcionado por la ISO de instalación de Arch Linux incluye la orden *gdisk*. Si la necesita más adelante, una vez instalado el sistema, puede obtener *gdisk* a través del paquete [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk).

He aquí un resumen del uso típico de `gdisk`:

*   Inicie `gdisk` sobre la unidad en cuestión como root (el *dispositivo-disco* puede ser, por ejemplo, `/dev/sda`).

	 `# gdisk *dispositivo-disco*` 

*   Si el disco es nuevo o si quiere volver a empezar, cree una nueva tabla de particiones GUID vacía (esto es, GPT) con la orden `o`.
*   Cree una nueva partición con la orden `n` (primary type/1st partition).
*   Suponiendo que la partición es nueva, *gdisk* elegirá la alineación más alta posible. De lo contrario, tomará la mayor posible después de obtener la media compensando todas las particiones.
*   Si elige iniciar en un sector antes del 2048, gdisk cambiará automáticamente el inicio de la partición para el sector 2048 del disco. Esto es para asegurar una alineación de 2048 sectores (como un sector es de 512B, esto supone una alineación a 1024KiB, que debería ajustarse a cualquier bloque de borrado NAND de SSD).
*   Use el formato `+x{M,G}` para extender la partición `x` megabytes o gigabytes. Si la elección del tamaño no es un múltiplo de 1024 (tamaño de la alineación -1024kiB-), gdisk reducirá la partición al múltiplo más cercano inferior. Por ejemplo, si desea crear una partición de 15GiB, debe escribir `+15G`.
*   Seleccione el identificador del tipo de la partición, el valor predeterminado, `Linux/Windows data` (código `0700`), debería estar bien para la mayoría de los casos. Pulse `L` para mostrar la lista de códigos. Si planea utilizar LVM, seleccione `Linux LVM` (`8e00`).
*   Asigne otras particiones siguiendo el método descrito.
*   Escriba la tabla en el disco y salga con la orden `w`.
*   Formatee las particiones nuevas con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)").

## Usar MBR - método tradicional

Usando MBR, la utilidad para la edición de la tabla de particiones se llama `fdisk`. Las versiones recientes de fdisk han abandonado el sistema obsoleto del uso de cilindros como unidad de referencia por defecto, así como la compatibilidad con MS-DOS de forma predeterminada. La última versión de fdisk alinea automáticamente todas las particiones al sector 2048, o 1024 Kb, que debe funcionar para todos los tamaños de EBS conocidos, por ser los utilizados por los fabricantes de SSD. Esto significa que la configuración por defecto le dará una alineación correcta.

Tenga en cuenta que antes, *fdisk* utilizaba los cilindros como la unidad de referencia por defecto, y mantuvo sin sentido la compatibilidad con MS-DOS que introdujo para la alineación de SSD. Por lo tanto, encontrará muchas guías en Internet de 2008-2009, que siguen esta tendencia haciendole entender que todo está correcto. Con la última versión de fdisk, las cosas son mucho más simples, como se refleja en esta guía.

### Resumen del uso de fdisk

*   Inicie `fdisk` sobre la unidad como root (el *dispositivo-disco* puede ser, por ejemplo, `/dev/sda`):

	 `# fdisk *dispositivo-disco*` 

*   Si el disco es nuevo o desea empezar de cero, cree una nueva tabla de partición DOS vacía con la orden `o`.
*   Cree una nueva partición con la orden `n` (primary type/1st partition).
*   Utilice el formato `+xG` para extender la partición `x` gigabytes. Por ejemplo, si desea crear una partición de 15GiB, debe escribir `+15G`.
*   Cambie el identificador del sistema de particiones desde el tipo predeterminado de Linux (`tipo 83`) para el tipo deseado con la orden `t`. Este es un paso opcional para el caso de que el usuario desea crear otro tipo de partición, por ejemplo, swap, NTFS, LVM, etc. Puede ver una lista completa de todos los tipos de particiones válidos con la orden `l`.
*   Asigne otras particiones siguiendo el método descrito.
*   Escriba la tabla en el disco y salga con la orden `w`.
*   Formatee las particiones nuevas con un [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)").

## Véase también

*   [Wikipedia:Disk partitioning](https://en.wikipedia.org/wiki/Disk_partitioning "wikipedia:Disk partitioning")
*   [Manually Partitioning Your Hard Drive with fdisk](http://www.novell.com/coolsolutions/feature/19350.html)
*   [Partition Alignment](http://www.thomas-krenn.com/en/wiki/Partition_Alignment) (with examples)