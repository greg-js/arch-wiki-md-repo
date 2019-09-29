**Estado de la traducción**
Este artículo es una traducción de [dd](/index.php/Dd "Dd"), revisada por última vez el **2019-09-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dd&diff=0&oldid=583613) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Disk cloning (Español)](/index.php/Disk_cloning_(Espa%C3%B1ol) "Disk cloning (Español)")
*   [USB flash installation media (Español)#Utilizar dd](/index.php/USB_flash_installation_media_(Espa%C3%B1ol)#Utilizar_dd "USB flash installation media (Español)")
*   [Benchmarking#dd](/index.php/Benchmarking#dd "Benchmarking")

[dd](https://en.wikipedia.org/wiki/dd_(Unix) es una de las [Core utilities (Español)](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)") cuyo objetivo principal es convertir y copiar un archivo.

De manera similar a *cp*, por defecto *dd* hace una copia bit a bit del archivo, pero con funciones de control de flujo de E/S de nivel inferior.

Para obtener más información, consulte [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) o la [documentación completa](https://www.gnu.org/software/coreutils/dd).

**Sugerencia:** por defecto, *dd* no muestra nada hasta que la tarea haya finalizado. Para monitorear el progreso de la operación, agregue la opción `status=progress` a la orden.

**Advertencia:** se debe ser extremadamente cauteloso utilizando *dd*, ya que con cualquier orden de este tipo se pueden destruir datos de forma irreversible.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Clonación y restauración de discos](#Clonación_y_restauración_de_discos)
    *   [2.1 Clonar una partición](#Clonar_una_partición)
    *   [2.2 Clonar un disco duro completo](#Clonar_un_disco_duro_completo)
    *   [2.3 Crear copia de seguridad de la tabla de particiones](#Crear_copia_de_seguridad_de_la_tabla_de_particiones)
    *   [2.4 Crear imagen de disco](#Crear_imagen_de_disco)
    *   [2.5 Restaurar el sistema](#Restaurar_el_sistema)
*   [3 Parchear archivos binarios](#Parchear_archivos_binarios)
*   [4 Copiar y restaurar el MBR](#Copiar_y_restaurar_el_MBR)
    *   [4.1 Eliminar el gestor de arranque](#Eliminar_el_gestor_de_arranque)

## Instalación

*dd* es parte de GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils). Para otras utilidades del paquete, consulte [Core utilities (Español)](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)").

## Clonación y restauración de discos

La orden *dd* es una herramienta simple, pero versátil y potente. Se puede utilizar para copiar de origen a destino, bloque por bloque, independientemente de los tipos de sistemas de archivos o sistemas operativos. Un método conveniente es usar *dd* desde un entorno live, como en un CD Live.

**Advertencia:** al igual que con cualquier orden de este tipo, debe ser muy cauteloso al usarlo; puede destruir datos. ¡Recuerde el orden del archivo de entrada (`if=`) y del archivo de salida (`of=`) y no los invierta! Asegúrese siempre de que la unidad o partición de destino (`of=`) sea de igual o mayor tamaño que la fuente (`if=`).

### Clonar una partición

Desde el disco físico `/dev/sda`, partición 1, al disco físico `/dev/sdb`, partición 1:

```
# dd if=/dev/sda1 of=/dev/sdb1 bs=64K conv=noerror,sync status=progress

```

**Nota:** tenga en cuenta que si la partición de salida `of=` (`sdb1` en el ejemplo) no existe, *dd* creará un archivo con este nombre y comenzará a llenar su sistema de archivos raíz.

### Clonar un disco duro completo

Desde el disco físico `/dev/sda` al disco físico `/dev/sdb`:

```
# dd if=/dev/sda of=/dev/sdb bs=64K conv=noerror,sync status=progress

```

Esta orden clonará toda la unidad, incluido el MBR (y, por lo tanto, el cargador de arranque), todas las particiones, UUID y datos.

*   `bs=` establece el tamaño del bloque. El valor predeterminado es 512 bytes, que es el tamaño de bloque «clásico» para discos duros desde principios de la década de 1980, pero no es el más conveniente. Utilice un valor mayor, 64K o 128K. Además, lea la advertencia siguiente, porque no solo hay que tener encuenta los «tamaños de bloques» en sí, también influyen estos en cómo se propagan los errores de lectura. Consulte [[1]](http://www.mail-archive.com/eug-lug@efn.org/msg12073.html) y [[2]](http://blog.tdg5.com/tuning-dd-block-size/) para obtener más información y para determinar el mejor valor de bs para su caso particular.
*   `noerror` indica a *dd* que continúe la operación, ignorando todos los errores de lectura. El comportamiento predeterminado para *dd* es detenerse ante cualquier error.
*   `sync` rellena los bloques de entrada con ceros si hubo errores de lectura, por lo que las compensaciones de datos permanecerán sincronizadas.
*   `status=progress` muestra estadísticas de transferencia periódicas que se utilizan para estimar cuándo puede completarse la operación.

**Nota:** el tamaño de bloque que especifique influye en cómo se manejarán los errores de lectura. Lee abajo. Para la recuperación de datos, utilice [ddrescue](/index.php/Disk_cloning_(Espa%C3%B1ol)#Utilizar_ddrescue "Disk cloning (Español)").

La utilidad *dd* técnicamente tiene un «tamaño de bloque de entrada» (IBS) y un «tamaño de bloque de salida» (OBS). Cuando configura `bs`, configura de manera efectiva tanto IBS como OBS. Normalmente, si el tamaño de su bloque es, digamos, 1 MiB, *dd* leerá 1024×1024 bytes y escribirá bytes iguales. Pero si ocurre un error de lectura, las cosas saldrán mal. Mucha gente parece pensar que *dd* «llenará los errores de lectura con ceros si usa las opciones `noerror, sync`, pero esto no es lo que sucede. *dd*, según la documentación, llenará el OBS al tamaño del IBS *después de completar su lectura*, lo que significa agregar ceros al *final* del bloque. Esto significa, para un disco, que efectivamente todo 1 MiB se estropearía debido a un solo error de lectura de 512 bytes al comienzo de la lectura: 12ERROR89 se convertiría en 128900000 en lugar de 120000089.

Si está seguro de que su disco no contiene ningún error, puede continuar usando un tamaño de bloque más grande, lo que aumentará la velocidad de su copia varias veces. Por ejemplo, cambiar bs de 512 a 64K cambiará la velocidad de copia de 35 MB/s a 120 MB/s en un sistema Celeron de 2.7 GHz. Pero tenga en cuenta que los errores de lectura en el disco de origen terminarán como «errores de bloque» en el disco de destino, es decir, un solo error de lectura de 512 bytes dañará todo el bloque de salida de 64 KiB.

**Sugerencia:** si desea ver el progreso de *dd*, utilice la opción `status=progress`. Vea [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) para más detalles.

**Nota:**

*   Para recuperar UUID únicos de un sistema de archivos *ext2/3/4*, utilice `tune2fs /dev/sd*XY* -U random` en cada partición. Para particiones de intercambio, utilice `mkswap /dev/sd*XY*` en su lugar.
*   El kernel no registra los cambios de la tabla de particiones realizadas por *dd* . Para notificar los cambios sin reiniciar, utilice una utilidad como *partprobe* (parte de [GNU Parted](/index.php/Parted "Parted")).

### Crear copia de seguridad de la tabla de particiones

Consulte [fdisk (Español)#Copia de seguridad y restauración de la tabla de particiones](/index.php/Fdisk_(Espa%C3%B1ol)#Copia_de_seguridad_y_restauración_de_la_tabla_de_particiones "Fdisk (Español)") o [GPT fdisk#Backup and restore partition table](/index.php/GPT_fdisk#Backup_and_restore_partition_table "GPT fdisk").

### Crear imagen de disco

Arranque desde un medio live y asegúrese de que no se monten particiones desde el disco duro de origen.

Luego monte el disco duro externo y haga una copia de seguridad del disco (de origen):

```
# dd if=/dev/sda conv=sync,noerror bs=64K | gzip -c  > */ruta/a/backup.img.gz*

```

Si es necesario (por ejemplo, cuando los archivos resultantes están almacenados en un sistema de archivos [FAT32](/index.php/FAT_(Espa%C3%B1ol) "FAT (Español)")) divida la imagen del disco en varias partes (consulte también [split(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/split.1)):

```
# dd if=/dev/sda conv=sync,noerror bs=64K | gzip -c | split -a3 -b2G - */ruta/a/backup.img.gz*

```

Si no hay suficiente espacio en el disco local, puede enviar la imagen a través de *ssh*:

```
# dd if=/dev/sda conv=sync,noerror bs=64K | gzip -c | ssh user@local dd of=backup.img.gz

```

Finalmente, guarde información adicional sobre la geometría de la unidad necesaria para interpretar la tabla de particiones almacenada dentro de la imagen. La más importante de las cuales es el tamaño del cilindro.

```
# fdisk -l /dev/sda > */path/to/list_fdisk.info*

```

**Nota:** es posible que desee utilizar un tamaño de bloque (`bs=`) que sea igual a la cantidad de caché en el disco duro que está respaldando. Por ejemplo, `bs=8192K` funciona para un caché de 8 MiB. El 64 KiB mencionado en este artículo es mejor que los `bs=512` bytes predeterminados, pero se ejecutará más rápido con un `bs=` más largo.

**Sugerencia:** *gzip* solo puede comprimir datos usando un solo núcleo de CPU, lo que conduce a un rendimiento de datos considerablemente menor que las velocidades de escritura en el almacenamiento moderno. Para aprovechar la compresión multinúcleo y crear una imagen de disco más rápidamente, se podría, por ejemplo, instalar el paquete [pigz](https://www.archlinux.org/packages/?name=pigz), y simplemente reemplazar la orden `gzip -c` anterior, con `pigz -c`. Para discos grandes, esto potencialmente puede ahorrar horas.

### Restaurar el sistema

Para restaurar su sistema:

```
# gunzip -c */ruta/a/backup.img.gz* | dd of=/dev/sda

```

Cuando la imagen se haya dividido, use lo siguiente:

```
# cat */ruta/a/backup.img.gz** | gunzip -c | dd of=/dev/sda

```

## Parchear archivos binarios

Si se quiere reemplazar el desplazamiento `0x123AB` de un archivo con la secuencia hexadecimal `FF C0 14`, esto se puede hacer con la línea de órdenes:

 `# printf '\xff\xc0\x14' | dd seek=$((0x123AB)) conv=notrunc bs=1 of=*/ruta/al/archivo*` 

## Copiar y restaurar el MBR

Antes de realizar cambios en un disco, es posible que desee hacer una copia de seguridad de la tabla de particioines y del esquema de particionado de la unidad. También puede usar una copia de seguridad para replicar el mismo esquema de particionado en varias unidades.

El MBR se almacena en los primeros 512 bytes del disco. Consta de 4 partes:

1.  Los primeros 440 bytes contienen el código de arranque (cargador de arranque).
2.  Los siguientes 6 bytes contienen la firma del disco.
3.  Los siguientes 64 bytes contienen la tabla de particiones (4 entradas de 16 bytes cada una, una entrada para cada partición primaria).
4.  Los últimos 2 bytes contienen una firma de arranque.

Para guardar el MBR como `mbr_file.img`:

```
# dd if=/dev/sd*X* of=*/path/to/mbr_file.img* bs=512 count=1

```

También puede extraer el MBR desde una imagen completa de disco con dd :

```
# dd if=*/ruta/al/disco.img* of=*/ruta/al/mbr_file.img* bs=512 count=1

```

Para restaurar (tenga cuidado, esto destruye la tabla de particiones existente y con ella el acceso a todos los datos en el disco):

```
# dd if=/*/ruta/al/mbr_file.img* of=/dev/sd*X* bs=512 count=1

```

**Advertencia:** restaurar el MBR con una tabla de particiones que no coincida hará que sus datos sean ilegibles y casi imposibles de recuperar. Si simplemente necesita reinstalar el gestor de arranque, consulte sus respectivas páginas, ya que también emplean la [región de compatibilidad de DOS](http://www.pixelbeat.org/docs/disk/): [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") o [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)").

Si solo desea restaurar el cargador de arranque, pero no las entradas de la tabla de partición primaria, simplemente restaure los primeros 440 bytes del MBR:

```
# dd if=*/ruta/al/mbr_file.img* of=/dev/sd*X* bs=440 count=1

```

Para restaurar solo la tabla de particiones, se debe usar:

```
# dd if=*/ruta/al/mbr_file.img* of=/dev/sd*X* bs=1 skip=446 count=64

```

### Eliminar el gestor de arranque

Para borrar el código de arranque MBR (puede ser útil si tiene que reinstalar completamente otro sistema operativo), solo es necesario poner a cero los primeros 440 bytes:

```
# dd if=/dev/zero of=/dev/sd*X* bs=440 count=1

```