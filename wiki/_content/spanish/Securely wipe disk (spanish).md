Artículos relacionados

*   [Securely wipe disk/Tips and tricks](/index.php/Securely_wipe_disk/Tips_and_tricks "Securely wipe disk/Tips and tricks")
*   [File recovery](/index.php/File_recovery "File recovery")
*   [Benchmarking](/index.php/Benchmarking "Benchmarking")
*   [Frandom](/index.php/Frandom "Frandom")
*   [Disk encryption (Español)#Preparar el disco](/index.php/Disk_encryption_(Espa%C3%B1ol)#Preparar_el_disco "Disk encryption (Español)")
*   [dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk"), revisada por última vez el **2019-11-01**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Securely_wipe_disk&diff=0&oldid=587546) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

La limpieza de un disco se realiza escribiendo nuevos datos sobre cada bit.

**Nota:** las referencias a «discos» en este artículo también se aplican a los dispositivos [loopback](https://en.wikipedia.org/wiki/es:Loopback "wikipedia:es:Loopback").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Casos de uso comunes](#Casos_de_uso_comunes)
    *   [1.1 Borrar todos los datos que quedan en el dispositivo](#Borrar_todos_los_datos_que_quedan_en_el_dispositivo)
    *   [1.2 Preparativos para el cifrado de dispositivos de bloque](#Preparativos_para_el_cifrado_de_dispositivos_de_bloque)
*   [2 Remanencia de datos](#Remanencia_de_datos)
    *   [2.1 Sistema operativo, programas y sistema de archivos](#Sistema_operativo,_programas_y_sistema_de_archivos)
    *   [2.2 Problemas específicos de hardware](#Problemas_específicos_de_hardware)
        *   [2.2.1 Memoria flash](#Memoria_flash)
        *   [2.2.2 Sectores defectuosos marcados](#Sectores_defectuosos_marcados)
        *   [2.2.3 Magnetismo residual](#Magnetismo_residual)
*   [3 Seleccionar un objetivo](#Seleccionar_un_objetivo)
*   [4 Seleccionar un tamaño de bloque](#Seleccionar_un_tamaño_de_bloque)
    *   [4.1 Calcular bloques para borrar manualmente](#Calcular_bloques_para_borrar_manualmente)
*   [5 Seleccionar una fuente de datos](#Seleccionar_una_fuente_de_datos)
    *   [5.1 Datos no aleatorios](#Datos_no_aleatorios)
        *   [5.1.1 Prueba de escritura de patrón](#Prueba_de_escritura_de_patrón)
    *   [5.2 Datos aleatorios](#Datos_aleatorios)
    *   [5.3 Datos cifrados](#Datos_cifrados)
*   [6 Sobrescribir el objetivo](#Sobrescribir_el_objetivo)
    *   [6.1 Redirigir la salida](#Redirigir_la_salida)
    *   [6.2 dd](#dd)
    *   [6.3 wipe](#wipe)
    *   [6.4 shred](#shred)
    *   [6.5 Badblocks](#Badblocks)
    *   [6.6 hdparm](#hdparm)
*   [7 Véase también](#Véase_también)

## Casos de uso comunes

### Borrar todos los datos que quedan en el dispositivo

El caso de uso más común para limpiar un dispositivo de forma completa e irrevocable será cuando el dispositivo se va a regalar o vender. Es posible que queden datos (sin cifrar) en el dispositivo y que desee protegerlos contra una investigación forense simple que puede ser un juego de niños con, por ejemplo, el software [recuperación de archivos](/index.php/File_recovery "File recovery").

Si desea borrar rápidamente todo del disco, utilidades como `/dev/zero` o patrones simples, permiten un rendimiento aceptable, en tanto que una aleatoriedad adecuada puede ser ventajosa en algunos casos que deberían tratarse para [#Remanencia de datos](#Remanencia_de_datos).

Cada bit sobrescrito significa proporcionar un nivel de borrado de datos que no permite la recuperación con funciones normales del sistema (como las órdenes estándar ATA/SCSI) e interfaces de hardware. Cualquier software de recuperación de archivos mencionado anteriormente debería estar especializado con funcionalidades propietarias de hardware de almacenamiento.

En el caso de un disco HDD, la recreación de datos no será posible sin, al menos, órdenes de disco no documentadas o alterando el controlador o el firmware del dispositivo para que se lean, por ejemplo, sectores reasignados (bloques defectuosos que [S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") retiró de su uso).

Existen diferentes problemas de borrado relacionados con ciertas tecnologías de almacenamiento físico, en particular todos los dispositivos basados ​​en memoria flash y almacenamiento magnético más antiguo (discos duros antiguos, disquetes, cintas).

### Preparativos para el cifrado de dispositivos de bloque

Si desea preparar su unidad para configurar de forma segura el [cifrado de dispositivo de bloque](/index.php/Disk_encryption#Block_device_encryption "Disk encryption") dentro del área borrada, debe usar [#Datos aleatorios](#Datos_aleatorios) generados por una cadena de números aleatorios criptográficamente segura (denominado RNG en este artículo en adelante).

Véase también [Wikipedia:Random number generation](https://en.wikipedia.org/wiki/Random_number_generation "wikipedia:Random number generation").

**Advertencia:** si el cifrado del dispositivo de bloque se usa en una partición que contiene algo distinto que datos aleatorios/cifrados, será posible revelar los patrones de uso en la unidad cifrada, lo cual debilita el cifrado al ser comparable con el cifrado a nivel del sistema de archivos. No utilice nunca `/dev/zero`, patrones simples (badblocks, por ejemplo) u otros datos no aleatorios antes de configurar el cifrado de un dispositivo de bloque, si quiere hacerlo bien.

## Remanencia de datos

Véase también [Wikipedia:es:Persistencia de datos](https://en.wikipedia.org/wiki/es:Persistencia_de_datos "wikipedia:es:Persistencia de datos").

La representación residual de los datos puede permanecer incluso después de que se hayan hecho intentos para eliminar o borrar los datos.

Los datos residuales pueden borrarse escribiendo datos (aleatorios) en el disco con una o más [iteraciones](https://en.wikipedia.org/wiki/es:Iteraci%C3%B3n "wikipedia:es:Iteración"). Sin embargo, más de una iteración puede no disminuir significativamente la posibilidad de reconstruir los datos de las unidades de disco duro. Vea [#Magnetismo residual](#Magnetismo_residual).

### Sistema operativo, programas y sistema de archivos

El sistema operativo, los programas ejecutados o los [sistemas de archivos journaling](https://en.wikipedia.org/wiki/es:Journaling "wikipedia:es:Journaling") pueden copiar sus datos no cifrados en todo el dispositivo de bloque. Al escribir en discos planos, esto solo debería ser relevante en conjunción con uno de los anteriores.

Si los datos pueden ubicarse exactamente en el disco y nunca se copiaron en ningún otro lugar, el borrado con datos aleatorios puede ser exhaustivo e impresionantemente rápido siempre que haya suficiente entropía en el agrupamiento.

Un buen ejemplo es cryptsetup utilizando `/dev/urandom` para [limpiar los espacios de keyslots de LUKS](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol)#Gestión_de_claves "Dm-crypt (Español)/Device encryption (Español)").

### Problemas específicos de hardware

#### Memoria flash

La [amplificación de la escritura](https://en.wikipedia.org/wiki/Write_amplification "wikipedia:Write amplification") y otras características hacen de la memoria flash (donde se incluye explícitamente SSD) un objetivo obstinado para un borrado confiable. Como hay mucha abstracción transparente entre los datos tal y como se ven en el chip de la controladora del dispositivo y los datos expuestos en el sistema operativo, nunca se sobrescribe la posición y borrar bloques o archivos particulares no es fiable.

Otras «características» como la compresión transparente (todos los SSD SandForce) pueden comprimir su /dev/zero o patrón de flujo, por lo que si el borrado es rápido más allá de lo razonable, este podría ser el caso.

Desensamblar dispositivos de memoria flash, desoldar los chips y analizar el contenido de datos sin la controladora de por medio es posible sin dificultad utilizando [hardware simple](http://www.flash-extractor.com/manual/reader_models/). Las empresas de recuperación de datos lo hacen por poco dinero.

Para más información, vea:

*   [Solid state drive/Memory cell clearing](/index.php/Solid_state_drive/Memory_cell_clearing "Solid state drive/Memory cell clearing")
*   [Borrado fiable de datos de unidades de estado sólido basadas en flash](http://www.usenix.org/events/fast11/tech/full_papers/Wei.pdf).
*   [#Seleccionar un objetivo](#Seleccionar_un_objetivo)

#### Sectores defectuosos marcados

Si un disco duro marca un sector como defectuoso, lo acordona y la sección se vuelve imposible de escribir a través del software. Por lo tanto, una sobrescritura completa no lo alcanzaría. Sin embargo, debido al tamaño de los bloques, estas secciones solo equivaldrían a unos pocos KB teóricamente recuperables.

#### Magnetismo residual

Una sola sobrescritura completa con ceros o datos aleatorios no genera datos recuperables en un dispositivo de almacenamiento moderno de alta densidad.[[1]](http://www.howtogeek.com/115573/htg-explains-why-you-only-have-to-wipe-a-disk-once-to-erase-it/) No obstante, las indicaciones se refieren a bits residuales únicos; la reconstrucción de los patrones de bytes generalmente no es factible.[[2]](https://web.archive.org/web/20120102004746/http://www.h-online.com/newsticker/news/item/Secure-deletion-a-single-overwrite-will-do-it-739699.html) Consulte también [[3]](https://www.google.com/search?tbs=bks:1&q=isbn:9783540898610), [[4]](http://security.stackexchange.com/questions/26132/is-data-remanence-a-myth/26134#26134) y [[5]](http://www.nber.org/sys-admin/overwritten-data-guttman.html).

## Seleccionar un objetivo

Utilice [fdisk (Español)](/index.php/Fdisk_(Espa%C3%B1ol) "Fdisk (Español)") para localizar todos los dispositivos de lectura/escritura a los que el usuario tiene acceso de lectura.

Verifique en la salida las líneas que comienzan con dispositivos como `/dev/sd"X"`.

Este es un ejemplo para un disco HDD formateado para arrancar un sistema Linux:

 `# fdisk -l` 
```
Disk /dev/sda: 250.1 GB, 250059350016 bytes, 488397168 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00ff784a

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048      206847      102400   83  Linux
/dev/sda2          206848   488397167   244095160   83  Linux

```

O la imagen de instalación de Arch escrita en una memoria USB de 4GB:

 `# fdisk -l` 
```
Disk /dev/sdb: 4075 MB, 4075290624 bytes, 7959552 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x526e236e

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1   *           0      802815      401408   17  Hidden HPFS/NTFS

```

Si le preocupa causar un daño involuntario a datos importantes del equipo principal, considere usar un entorno aislado como un entorno virtual (VirtualBox, VMWare, QEMU, etc...) con unidades de disco conectadas directamente a él o un único equipo con un solo disco de almacenamiento que necesita limpiar arrancado desde un [soporte Live](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)") (USB, CD, PXE, etc.) o utilice un script para [evitar limpiar particiones montadas por un error tipográfico](/index.php/Securely_wipe_disk/Tips_and_tricks#Prevent_wiping_mounted_partitions "Securely wipe disk/Tips and tricks").

## Seleccionar un tamaño de bloque

Vea también [Wikipedia:Dd (Unix)#Block size](https://en.wikipedia.org/wiki/Dd_(Unix)#Block_size "wikipedia:Dd (Unix)"), [blocksize io-limits](http://people.redhat.com/msnitzer/docs/io-limits.txt).

Si tiene un disco duro de [formato avanzado](/index.php/Advanced_Format_(Espa%C3%B1ol) "Advanced Format (Español)"), se recomienda que especifique un tamaño de bloque mayor que los 512 bytes predeterminados. Para acelerar el proceso de sobrescritura, elija un tamaño de bloque que coincida con la geometría física de su unidad, agregando la opción de tamaño de bloque a la orden *dd* (es decir, `bs=4096` para 4KB).

*fdisk* muestra el tamaño del sector físico y lógico para cada disco. Alternativamente, sysfs expone información:

```
/sys/block/sdX/size
/sys/block/sdX/queue/physical_block_size
/sys/block/sdX/queue/logical_block_size
/sys/block/sdX/sdXY/alignment_offset
/sys/block/sdX/sdXY/start
/sys/block/sdX/sdXY/size

```

**Advertencia:** estos métodos muestran el tamaño de bloque que la unidad informa al kernel. Sin embargo, muchas unidades de formato avanzado subestiman incorrectamente el tamaño del bloque físico dándolo como 512.

**Sugerencia:** este script, [genwipe.sh](https://aur.archlinux.org/packages/genwipe.sh/), ayuda a calcular los parámetros para borrar un dispositivo/partición con dd, por ejemplo `genwipe.sh /dev/sd"XY"`.

### Calcular bloques para borrar manualmente

A continuación, la determinación del área de datos a borrar se realiza en un ejemplo.

Un dispositivo de almacenamiento de bloque contiene sectores y un tamaño único para cada sector que puede usarse para calcular el tamaño completo del dispositivo en bytes. Puede hacerlo multiplicando el número de sectores con el tamaño del sector.

Como ejemplo, vamos a usar los parámetros con la orden *dd* para borrar una partición:

```
# dd if=*fuente_datos* of=/dev/sd"X" bs=*tamaño_sector* count=*número_sector* seek=*sector_inicio_partición* status=progress

```

Aquí verá solo una parte de la salida de la orden `fdisk -l /dev/sdX` ejecutada con root, que muestra la información de la partición de ejemplo:

```
Device     Boot      Start        End         Sectors     Size  Id Type
/dev/sd"XA"            2048         3839711231  3839709184  1,8T  83 Linux
/dev/sd"XB"            3839711232   3907029167  67317936    32,1G  5 Extended

```

La primera línea de la salida de *fdisk* muestra el tamaño del disco en bytes y los sectores lógicos:

```
Disk /dev/sd"X": 1,8 TiB, 2000398934016 bytes, 3907029168 sectors

```

Para calcular el tamaño de un solo sector lógico, utilice `echo $((2000398934016 / 3907029168))` o utilice los datos de la segunda línea de salida de *fdisk*:

```
Units: sectors of 1 * 512 = 512 bytes

```

Para calcular los sectores físicos que harán que funcione más rápido, podemos usar la tercera línea:

```
Sector size (logical/physical): 512 bytes / 4096 bytes

```

Para obtener el tamaño del disco en sectores físicos, necesitará el tamaño del disco conocido en bytes dividido por el tamaño de un solo sector físico `echo $((2000398934016 / 4096))`, puede obtener el tamaño del dispositivo de almacenamiento o partición del mismo con la orden `blockdev --getsize64 /dev/sd"XY"`.

**Nota:**

*   En los ejemplos siguientes utilizaremos el tamaño del sector lógico.
*   Puede incluso borrar el espacio en disco no asignado con una orden `dd` calculando la diferencia entre el final de uno y el inicio de la siguiente partición.

Para borrar la partición `/dev/sd"XA"`, los parámetros de ejemplo con sectores lógicos se usarían así:

```
Start=2048
End=3839711231
BytesInSector=512
```

Para utilizar la dirección de inicio de la partición en el dispositivo para establecerla en la opción `seek=`:

```
# dd if=*data_source* of=/dev/sd"X" bs=${BytesInSector} count=${End - Start} seek=${Start} status=progress

```

Para utilizar el tamaño de las particiones (en sectores lógicos):

```
LogicalSectors=3839709184

```

```
# dd if=*data_source* of=/dev/sd"XA" bs=${BytesInSector} count=${LogicalSectors} status=progress

```

O, para borrar todo el disco utilizando los sectores físicos:

```
AllDiskPhysicalSectors=488378646
PhysicalSectorSizeBytes=4096
```

```
# dd if=*data_source* of=/dev/sd"X" bs=${PhysicalSectorSizeBytes} count=${AllDiskPhysicalSectors} seek=0 status=progress

```

**Nota:** la opción `count=` no es necesaria al limpiar el área física limitada, por ejemplo `sd"XY"` o `sd"X"`, desde el principio hasta el final, pero mostrará un error de falta de espacio libre cuando intente escribir fuera de los límites.

## Seleccionar una fuente de datos

Como se acaba de decir si desea borrar datos confidenciales, puede usar cualquier opción que se ajuste a sus necesidades.

Si desea configurar el cifrado de dispositivos de bloque después, siempre debe borrar, al menos, con un algoritmo de cifrado como fuente o, incluso, con datos pseudoaleatorios.

Para datos que no son verdaderamente aleatorios, la velocidad de escritura de su disco debería ser el único factor limitante. Si necesita datos aleatorios, el rendimiento del sistema requerido para generarlos puede depender en gran medida de lo que elija como fuente de entropía.

### Datos no aleatorios

La sobrescritura con `/dev/zero` o patrones simples se considera segura en la mayoría de los recursos. En el caso de los discos duros actuales, debería ser suficiente para limpiar rápidamente los discos.

**Advertencia:** una unidad que es anormalmente rápida en la escritura de patrones o puesta a cero podría estar haciendo una compresión transparente. Es obviamente presumible que no todos los bloques se limpiarán de esta manera. Algunos dispositivos de [#Memoria flash](#Memoria_flash) tienen dicha «característica».

#### Prueba de escritura de patrón

[#Badblocks](#Badblocks) puede escribir patrones simples en cada bloque de un dispositivo y luego leerlos y verificarlos buscando áreas dañadas (al igual que memtest86* hace con la memoria).

Como el patrón se escribe en cada bloque accesible, esto efectivamente borra el dispositivo.

### Datos aleatorios

Para conocer las diferencias entre los datos aleatorios y pseudoaleatorios como fuente, consulte [Random number generation](/index.php/Random_number_generation "Random number generation").

**Nota:** los datos que son difíciles de comprimir (datos aleatorios) se escribirán más lentamente, si la lógica de la unidad mencionada en la advertencia de [#Datos no aleatorios](#Datos_no_aleatorios) intenta comprimirlos. Sin embargo, esto no debería conducir a [#Remanencia de datos](#Remanencia_de_datos). Como la velocidad máxima de escritura no es el cuello de botella en el rendimiento, puede obviarse completamente mientras se limpian discos con datos aleatorios.

### Datos cifrados

Al preparar una unidad para el cifrado de disco completo, generalmente no es necesario obtener una entropía de alta calidad. La alternativa es usar un flujo de datos cifrado. Por ejemplo, si va a utilizar AES para su partición encriptada, debe limpiarla con un cifrado de encriptación equivalente antes de crear el sistema de archivos para hacer que el espacio vacío no se distinga del espacio utilizado.

## Sobrescribir el objetivo

La unidad elegida se puede sobrescribir con varias utilidades, haga su elección. Si solo desea borrar un solo archivo, [Securely wipe disk/Tips and tricks#Wipe a single file](/index.php/Securely_wipe_disk/Tips_and_tricks#Wipe_a_single_file "Securely wipe disk/Tips and tricks") tiene consideraciones adicionales además de las utilidades mencionadas a continuación.

### Redirigir la salida

La salida redirigida se puede usar tanto para la creación de los archivos como para reescribir el espacio libre en la partición, borrar todo el dispositivo o una sola partición.

A continuación se presentan ejemplos que se pueden usar para reescribir la partición o un dispositivo de bloque al redirigir [stdout (salida estándar)](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-3.html) desde otras utilidades:

 `$ cat /dev/urandom > /dev/sd"XY"` 
```
cat: write error: No space left on device

```
 `$ xz -z0 /dev/urandom -c > /dev/sd"XY"` 
```
xz: (stdout): Write error: No space left on device

```
 `$ dd if=/dev/urandom > /dev/sd"XY"` 
```
dd: writing to ‘standard output’: No space left on device
20481+0 records in
20480+0 records out
10485760 bytes (10 MB, 10 MiB) copied, 2.29914 s, 4.6 MB/s
```

La orden de copia de archivos `cp` también se puede utilizar para reescribir el dispositivo, ya que ignora el tipo de destino:

 `$ cp /dev/urandom /dev/sd"XY"` 
```
 cp: error writing ‘/dev/sd"XY"’: No space left on device
 cp: failed to extend ‘/dev/sd"XY"’: No space left on device

```

Para mostrar la velocidad y el tiempo, puede usar [pv](https://www.archlinux.org/packages/?name=pv):

```
# pv --timer --rate --stop-at-size -s "$(blockdev --getsize64 /dev/sd"XY" )" /dev/zero > /dev/sd"XY"

```

### dd

Consulte también [Core utilities (Español)#Esenciales](/index.php/Core_utilities_(Espa%C3%B1ol)#Esenciales "Core utilities (Español)").

**Advertencia:** no hay confirmación con respecto a la ejecución de esta orden, así que **verifique repetidamente** que la unidad o partición correcta ha sido seleccionada. Asegúrese de que la opción `of=...` apunta a la unidad de destino y no a un disco del sistema.

Rellene con ceros el disco escribiendo un byte de cero en cada ubicación dirigida al disco utilizando la secuencia [/dev/zero](https://en.wikipedia.org/wiki/es:/dev/zero "wikipedia:es:/dev/zero").

```
# dd if=/dev/zero of=/dev/sdX bs=4096 status=progress

```

O la secuencia [/dev/urandom](https://en.wikipedia.org/wiki/es:/dev/random "wikipedia:es:/dev/random"):

```
# dd if=/dev/urandom of=/dev/sdX bs=4096 status=progress

```

El proceso finaliza cuando dd informa `No space left on device` y devuelve el control:

```
dd: writing to ‘/dev/sdb’: No space left on device
7959553+0 records in
7959552+0 records out
4075290624 bytes (4.1 GB, 3.8 GiB) copied, 1247.7 s, 3.3 MB/s

```

Para acelerar la limpieza de una unidad grande, consulte también:

*   [Securely wipe disk/Tips and tricks#dd - advanced example](/index.php/Securely_wipe_disk/Tips_and_tricks#dd_-_advanced_example "Securely wipe disk/Tips and tricks") que utiliza OpenSSL;
*   [Securely wipe disk/Tips and tricks#Using a template file](/index.php/Securely_wipe_disk/Tips_and_tricks#Using_a_template_file "Securely wipe disk/Tips and tricks") que borra datos preestablecidos no aleatorios (por ejemplo, sobrescribe un disco completo con un solo archivo) pero es muy rápido;
*   [Dm-crypt/Drive preparation#dm-crypt specific methods](/index.php/Dm-crypt/Drive_preparation#dm-crypt_specific_methods "Dm-crypt/Drive preparation") que utiliza dm-crypt.

### wipe

Especializado en borrar archivos, está disponible como el paquete [wipe](https://www.archlinux.org/packages/?name=wipe). Para borrar rápidamente un destino, puede usar algo como:

```
$ wipe -r /path/to/wipe

```

Vea también [wipe(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipe.1). La herramienta se actualizó por última vez en 2009\. Su [página SourceForge](http://wipe.sourceforge.net/) sugiere que está **actualmente sin mantenimiento**.

### shred

[*shred*](https://www.gnu.org/software/coreutils/manual/html_node/shred-invocation.html) (del paquete [coreutils](https://www.archlinux.org/packages/?name=coreutils)) es una orden de Unix que se puede usar para eliminar de forma segura archivos individuales o dispositivos completos de modo que puedan recuperarse solo con hardware especializado no sin gran dificultad, si es que lo hacen. Por defecto, *shred* usa tres pasadas, escribiendo [datos pseudoaleatorios](/index.php/Random_number_generation "Random number generation") en el dispositivo durante cada pasada. Esto se puede reducir o aumentar.

La siguiente orden invoca shred con su configuración predeterminada y muestra el progreso.

```
# shred -v /dev/sd*X*

```

Alternativamente, se le puede indicar a shred que haga solo una pasada, con entropía de, por ejemplo, `/dev/urandom`.

```
# shred --verbose --random-source=/dev/urandom -n1 /dev/sd*X*

```

### Badblocks

Para permitir que [badblocks](/index.php/Badblocks "Badblocks") (del paquete [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)) realice una limpieza de disco, se debe realizar una [prueba de lectura-escritura](/index.php/Badblocks#Read-write_test_(warning:destructive) "Badblocks") destructiva:

```
# badblocks -c <NUMBER_BLOCKS> -wsv /dev/<drive>

```

### hdparm

**Advertencia:** no intente emitir una orden Secure Erase ATA en un dispositivo conectado a través de USB; vea [https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase](https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase) y [http://www.tomshardware.co.uk/answers/id-1984547/secure-erase-external-usb-hard-drive.html](http://www.tomshardware.co.uk/answers/id-1984547/secure-erase-external-usb-hard-drive.html) para detalles.

[hdparm](/index.php/Hdparm "Hdparm") admite [ATA Secure Erase](http://tinyapps.org/docs/wipe_drives_hdparm.html), que es funcionalmente equivalente a llenar un disco con ceros. Sin embargo, es manejado por el firmware del disco duro e incluye «áreas de datos ocultos». Como tal, puede verse como una orden moderna de «formato de bajo nivel». Según los informes, las unidades [SSD](/index.php/SSD "SSD") alcanzan el rendimiento de fábrica después de emitir esta orden, pero es posible que no se borren lo suficiente (consulte [#Memoria flash](#Memoria_flash)).

Algunas unidades admiten **Enhanced Secure Erase**, que utiliza distintos patrones definidos por el fabricante. Si la salida de `hdparm -I` para el dispositivo indica una ventaja de tiempo múltiple para el borrado **Enhanced**, el dispositivo probablemente tenga una función de cifrado por hardware y el borrado se realizará con las claves de dicho cifrado solamente.

Para obtener instrucciones detalladas sobre el uso de ATA Secure Erase, consulte [Solid state drive/Memory cell clearing](/index.php/Solid_state_drive/Memory_cell_clearing "Solid state drive/Memory cell clearing") y la [Linux ATA wiki](https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase).

## Véase también

*   [Limpiar el espacio libre en Linux](http://superuser.com/questions/19326/how-to-wipe-free-disk-space-in-linux)