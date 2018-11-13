Artículos relacionados

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [Installing with Fake RAID](/index.php/Installing_with_Fake_RAID "Installing with Fake RAID")
*   [Convert a single drive system to RAID](/index.php/Convert_a_single_drive_system_to_RAID "Convert a single drive system to RAID")
*   [ZFS](/index.php/ZFS "ZFS")
*   [Experimenting with ZFS](/index.php/Experimenting_with_ZFS "Experimenting with ZFS")

En este artículo se explica qué es RAID y cómo crear/administrar una matriz RAID por software utilizando mdadm.

## Contents

*   [1 Introducción](#Introducción)
    *   [1.1 Niveles RAID estándar](#Niveles_RAID_estándar)
    *   [1.2 Niveles RAID anidados](#Niveles_RAID_anidados)
    *   [1.3 Comparación de niveles RAID](#Comparación_de_niveles_RAID)
*   [2 Implementación](#Implementación)
    *   [2.1 ¿Qué tipo de RAID tengo?](#¿Qué_tipo_de_RAID_tengo?)
*   [3 Instalación](#Instalación)
    *   [3.1 Preparar los dispositivos](#Preparar_los_dispositivos)
    *   [3.2 Crear la tabla de particiones](#Crear_la_tabla_de_particiones)
    *   [3.3 Compilar la matriz](#Compilar_la_matriz)
    *   [3.4 Actualizar archivo de configuración](#Actualizar_archivo_de_configuración)
    *   [3.5 Ensamblar la matriz](#Ensamblar_la_matriz)
    *   [3.6 Formatear RAID con un sistema de archivos](#Formatear_RAID_con_un_sistema_de_archivos)
        *   [3.6.1 Calcular el stride y stripe-width](#Calcular_el_stride_y_stripe-width)
            *   [3.6.1.1 Ejemplo 1\. RAID0](#Ejemplo_1._RAID0)
            *   [3.6.1.2 Ejemplo 2\. RAID5](#Ejemplo_2._RAID5)
*   [4 Montar desde un CD live](#Montar_desde_un_CD_live)
*   [5 Instalar Arch Linux en RAID](#Instalar_Arch_Linux_en_RAID)
    *   [5.1 Actualizar archivo de configuración](#Actualizar_archivo_de_configuración_2)
    *   [5.2 Añadir el hook mdadm a mkinitcpio.conf](#Añadir_el_hook_mdadm_a_mkinitcpio.conf)
    *   [5.3 Configurar syslinux](#Configurar_syslinux)
*   [6 Mantenimiento de RAID](#Mantenimiento_de_RAID)
    *   [6.1 Depuración](#Depuración)
        *   [6.1.1 Notas generales sobre la depuración](#Notas_generales_sobre_la_depuración)
        *   [6.1.2 Notas sobre la depuración de RAID1 y RAID10](#Notas_sobre_la_depuración_de_RAID1_y_RAID10)
    *   [6.2 Extracción de dispositivos de una matriz](#Extracción_de_dispositivos_de_una_matriz)
    *   [6.3 Adición de un nuevo dispositivo a una matriz](#Adición_de_un_nuevo_dispositivo_a_una_matriz)
        *   [6.3.1 Para matrices RAID0](#Para_matrices_RAID0)
*   [7 Monitorización](#Monitorización)
    *   [7.1 Observar estado con mdstat](#Observar_estado_con_mdstat)
    *   [7.2 Seguimiento E/S con iotop](#Seguimiento_E/S_con_iotop)
    *   [7.3 Seguimiento E/S con iostat](#Seguimiento_E/S_con_iostat)
    *   [7.4 Correos sobre eventos](#Correos_sobre_eventos)
        *   [7.4.1 Método alternativo](#Método_alternativo)
*   [8 Solución de problemas](#Solución_de_problemas)
    *   [8.1 Error: «invalid raid superblock magic»](#Error:_«invalid_raid_superblock_magic»)
    *   [8.2 Error: «kernel: ataX.00: revalidation failed»](#Error:_«kernel:_ataX.00:_revalidation_failed»)
    *   [8.3 Iniciar matrices en solo lectura](#Iniciar_matrices_en_solo_lectura)
    *   [8.4 Recuperación de una unidad rota o ausente en el raid](#Recuperación_de_una_unidad_rota_o_ausente_en_el_raid)
*   [9 Benchmarking](#Benchmarking)
*   [10 Véase también](#Véase_también)

## Introducción

Véase también [Wikipedia:RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID").

*Redundant Array of Independent Disks* (Matriz Redundante de Discos Independientes, siglas en inglés RAID) es una tecnología de almacenamiento que combina varios componentes de unidades de disco —normalmente unidades de disco o particiones de los mismos— en una unidad lógica. Dependiendo de la implementación de RAID, la unidad lógica puede ser un sistema de archivos o una capa transparente adicional que puede contener varias particiones. Los datos se distribuyen a través de las unidades de una las muchas maneras que hay, llamadas «niveles de RAID», dependiendo del nivel de redundancia y del rendimiento requeridos. El nivel RAID elegido, por lo tanto, va a depender de si lo que se quiere es prevenir la pérdida de datos en caso de un fallo del disco duro, aumentar el rendimiento o una combinación de ambos.

A pesar de la redundancia implícita en la mayoría de los niveles de RAID, RAID no garantiza que los datos estén asegurados. Un RAID no protege los datos si se produce un incendio, el equipo es robado o varios discos duros fallan a la vez. Por otra parte, la instalación de un sistema con RAID es un proceso complejo que puede destruir los datos.
**Advertencia:** Por tanto, asegúrese de [hacer copia de respaldo](/index.php/Backup_programs "Backup programs") de todos los datos antes de proceder.

**Nota:** Los usuarios que estén considerando usar una matriz RAID para almacenamiento/redundancia de datos, también deben considerar RAIDZ que se implementa a través de [ZFS](/index.php/ZFS "ZFS"), una alternativa más moderna y potente de RAID por software.

### Niveles RAID estándar

Hay muchos [niveles de RAID](https://en.wikipedia.org/wiki/Standard_RAID_levels "wikipedia:Standard RAID levels"), sírvase encontrar a continuación los más comúnmente usados.

	[RAID 0](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_0 "wikipedia:Standard RAID levels")

	Utiliza [striping](https://en.wikipedia.org/wiki/es:Striping "wikipedia:es:Striping") para combinar discos. A pesar de que *no proporciona redundancia* (es decir, la posibilidad de recuperar o reconstruir los datos almacenados), todavía se considera RAID. Lo que si hace, sin embargo, es *proporcionar un gran beneficio velocidad* . Si el aumento de la velocidad vale la pena ante la posibilidad de pérdida de datos (para la partición [swap](/index.php/Swap "Swap"), por ejemplo), elija este nivel de RAID. En un servidor, las matrices RAID 1 y RAID 5 son las más apropiadas. El tamaño de un dispositivo de bloques de una matriz RAID 0 equivale al tamaño de la partición más pequeña que la compone de entre el número de particiones integrantes.

	[RAID 1](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_1 "wikipedia:Standard RAID levels")

	Es el nivel RAID más simple: replicación pura. Al igual que con otros niveles de RAID, solo tiene sentido si las particiones están en diferentes unidades de discos físicos. Si una de esas unidades falla, el dispositivo de bloque proporcionado por la matriz RAID va a seguir funcionando con normalidad. El ejemplo que se utiliza es RAID 1 para todo, excepto [swap](/index.php/Swap "Swap") y los datos temporales. Tenga en cuenta que con una implementación de software, el nivel de RAID 1 es la única opción para la partición de arranque, porque los gestores de arranque, que leen la partición de arranque, no entienden RAID, pero una partición integrante de RAID 1 puede ser leída como una partición normal. El tamaño de un sistema RAID 1 equivale a la dimensión de la partición más pequeña que lo compone.

	[RAID 5](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_5 "wikipedia:Standard RAID levels")

	Requiere 3 o más unidades físicas, y proporciona la redundancia de RAID 1 en combinación con la velocidad y los beneficios del tamaño de RAID 0\. RAID 5 utiliza *striping*, como RAID 0, pero también bloques de paridad de almacenaje *distribuidos entre cada disco miembro*. En el caso de que un disco falle, esta bloques de paridad se utilizan para reconstruir los datos en un disco de reemplazo. RAID 5 puede soportar la pérdida de uno de los discos miembros.

**Nota:** RAID 5 es una opción común debido a su combinación de velocidad y redundancia de datos. La advertencia es que si una unidad falla y, antes de que fuera reemplazada, la otra unidad fallara, se perderían todos los datos.

### Niveles RAID anidados

	[RAID 1+0](https://en.wikipedia.org/wiki/Nested_RAID_levels#RAID_1_.2B_0 "wikipedia:Nested RAID levels")

	Comúnmente conocido como *RAID 10* , es un RAID anidado que combina dos de los niveles estándar de RAID para obtener un rendimiento y redundancia adicional. Es la mejor alternativa a RAID 5 cuando la redundancia es crucial.

### Comparación de niveles RAID

| Nivel RAID | Redundancia de datos | Utilización de la unidad física | Rendimiento de lectura | Rendimiento de escritura | Unidades mínimas |
| **0** | **No** | 100% | nX

**Máxima**

 | nX

**Máxima**

 | 2 |
| **1** | Sí | 50% | nX (teóricamente)

1X (en la práctica)

 | 1X | 2 |
| **5** | Sí | 67% - 94% | (n−1)X

**Superior**

 | (n−1)X

**Superior**

 | 3 |
| **6** | Sí | 50% - 88% | (n−2)X | (n−2)X | 4 |
| **10** | Sí | 50% | nX (teóricamente) | (n/2)X | 4 |

* Donde *n* es el *standing* multiplicado por el número de discos dedicados.

## Implementación

Los dispositivos RAID pueden gestionarse de diferentes maneras:

	RAID por software

	Esta es la implementación más fácil, ya que no se basa en firmware y software propietarios para ser utilizado. La matriz es administrada por el sistema operativo, ya sea:

*   por una capa de abstracción (por ejemplo, [mdadm](#Instalar_Arch_Linux_en_RAID));
    **Nota:** Este es el método que utilizaremos más adelante en esta guía.

*   por un gestor de volúmenes lógicos (por ejemplo, [LVM](/index.php/LVM "LVM"));
*   por un componente de un sistema de archivos (por ejemplo, [ZFS](/index.php/ZFS "ZFS")).

	RAID por hardware

	La matriz está gestionada directamente por una tarjeta de hardware dedicada instalada en el PC al que los discos se conectan directamente. La lógica RAID se ejecuta en un procesador de la placa base independientemente del [procesador del equipo (CPU)](https://en.wikipedia.org/wiki/es:Unidad_central_de_procesamiento "wikipedia:es:Unidad central de procesamiento"). Aunque esta solución es independiente de cualquier sistema operativo, este último requiere un controlador para poder funcionar correctamente con la controladora de RAID hardware. La matriz RAID, o bien se puede configurar a través de una opción de la interfaz rom o, según el fabricante, con una aplicación dedicada, cuando se ha instalado el sistema operativo. La configuración es transparente para el kernel de Linux: no ve los discos por separado.

	[FakeRAID](/index.php/Fakeraid "Fakeraid")

	Este tipo de RAID es llamado propiamente BIOS o RAID integrado en la placa base, pero es falsamente anunciado como RAID por hardware. La matriz está gestionada por controladoras pseudoRAID donde la lógica RAID se implementa en una opción de rom o en el propio firmware [con un EFI SataDriver](http://www.win-raid.com/t19f13-Intel-EFI-RAID-quot-SataDriver-quot-BIOS-Modules.html) (en el caso de [UEFI](/index.php/UEFI "UEFI")), pero no son completas controladoras de RAID hardware con *todas* las funciones RAID implementadas. Por lo tanto, este tipo de RAID a veces se llama fakeRAID. [dmraid](https://www.archlinux.org/packages/?name=dmraid) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"), se utilizará para suplir a estas controladoras. Algunos ejemplos de controladoras FakeRAID son: [Intel Rapid Storage](https://en.wikipedia.org/wiki/Intel_Rapid_Storage_Technology "wikipedia:Intel Rapid Storage Technology"), JMicron JMB36x RAID ROM, AMD RAID, ASMedia 106x,...

### ¿Qué tipo de RAID tengo?

Dado que el RAID por software se implementa por el usuario, este tipo de RAID es fácilmente conocido por el usuario.

Sin embargo, discernir entre fakeRAID y RAID de hardware verdadero puede ser más difícil. Como se dijo, los fabricantes no suelen distinguir correctamente estos dos tipos de RAID y siempre es posible falsear la publicidad. La mejor solución, en estos casos, es ejecutar la orden `lspci` y mirar la salida para encontrar la conntroladora RAID. A continuación, realice una búsqueda para ver qué información puede definir la controladora RAID.

## Instalación

Instale [mdadm](https://www.archlinux.org/packages/?name=mdadm) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). *mdadm* se utiliza para la administración de RAID por software puro usando dispositivos de bloque plano: el hardware subyacente no ofrece ninguna lógica RAID, solo un suministro de discos. *mdadm* funcionará con cualquier colección de dispositivos de bloques. Incluso si son inusuales. Por ejemplo, se puede, pues, hacer un matriz RAID de una colección de memorias USB.

### Preparar los dispositivos

**Advertencia:** Estos pasos borran todo el contenido de un dispositivo, por lo que escriba con cuidado

Para evitar posibles problemas de los dispositivos en el RAID, debe hacerse una [limpieza segura](/index.php/Securely_wipe_disk "Securely wipe disk") de cada uno. Si el dispositivo está siendo reutilizado o repuesto de una matriz existente, borre cualquier información de configuración RAID antigua:

```
# mdadm --zero-superblock /dev/<unidad>

```

o, si se va a eliminar una partición particular de una unidad:

```
# mdadm --zero-superblock /dev/<partición>

```

**Nota:** Hacer limpieza de un superbloque de partición no debe afectar a las otras particiones en el disco.

### Crear la tabla de particiones

Es recomendable particionar los discos que se utilizarán en la matriz. Como la mayoría de los usuarios RAID seleccionan discos duros de >2 TB, es preferible y recomendable utilizar tablas de particionado GPT. Los discos se dividen fácilmente usando [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk).

*   Después de creada, al tipo de partición se le debe asignar un código hexadecimal FD00.
*   Es preferible crear particiones del mismo tamaño en cada uno de los dispositivos.
*   Un buen consejo es dejar aproximadamente 100 MB en el extremo del dispositivo al particionar. Véase más abajo la justificación.

**Nota:** También es posible crear un RAID directamente en los discos crudos (sin particiones), pero no se recomienda, ya que puede causar problemas cuando se cambia un disco averiado.

Al reemplazar un disco averiado de un RAID, el nuevo disco tiene que ser exactamente del mismo tamaño que el disco que ha fallado o más grande, de lo contrario el proceso de reconstrucción de la matriz no va a funcionar. Incluso las unidades de disco duro del mismo fabricante y modelo pueden tener pequeñas diferencias de tamaño. Al dejar un poco de espacio sin asignar en la parte final del disco se pueden compensar las diferencias de tamaño entre las unidades, por lo que es más fácil elegir un modelo de unidad para el reemplazo. Por lo tanto, **es una buena práctica dejar unos 100 MB de espacio no asignado al final del disco**

### Compilar la matriz

Utilice `mdadm` para compilar la matriz. Varios ejemplos se dan a continuación.

**Advertencia:** No basta con copiar/pegar los ejemplos siguientes; sustituir las opciones/letras correctas de la unidad

**Nota:** Si se trata de una matriz RAID 1 que se pretende arrancar desde [Syslinux](/index.php/Syslinux "Syslinux") una limitación en la v4.07 de syslinux requiere que el valor de los metadatos se ajuste a 1.0 en lugar de la opción predeterminada de 1.2.

El siguiente ejemplo muestra la compilación de una matriz RAID 1 en el dispositivo 2:

```
# mdadm --create --verbose --level=1 --metadata=1.2 --chunk=64 --raid-devices=2 /dev/md0 /dev/sdb1 /dev/sdc1

```

**Nota:** En un RAID1 en realidad no se necesita el conmutador *chunk*.

El siguiente ejemplo muestra la compilación de una matriz RAID 5 en dispositivo 4:

```
# mdadm --create --verbose --level=5 --metadata=1.2 --chunk=256 --raid-devices=4 /dev/md0 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1 --spare-devices=1 /dev/sdf1

```

La matriz se crea en el dispositivo virtual `/dev/mdX`, montado y listo para su uso (en modo degradado). Se puede comenzar directamente utilizándolo mientras mdadm resincroniza la matriz en segundo plano. Puede tomar mucho tiempo hasta restablecer la paridad.

 `$ cat /proc/mdstat` 

### Actualizar archivo de configuración

Después de compilar cualquier matriz RAID nueva, el archivo de configuración por defecto, `mdadm.conf`, debe ser actualizado, así:

```
# mdadm --detail --scan >> /etc/mdadm.conf

```

Verifique siempre el contenido de `/etc/mdadm.conf` después de ejecutar esta orden.

Valores de nombres o metadatos incorrectos en `mdadm.conf` pueden causar que la matriz RAID no coincida con ninguna entrada en `mdadm.conf`. Los nombres y los parámetros de los metadatos se pueden quitar y serán detectados automáticamente.

### Ensamblar la matriz

Una vez que el archivo de configuración se ha actualizado, la matriz puede ser ensamblada usando mdadm:

```
# mdadm --assemble --scan

```

### Formatear RAID con un sistema de archivos

La matriz ahora se puede formatear con un sistema de archivos como cualquier otro disco, basta tener en cuenta que:

*   debido al gran tamaño del volumen, no todos los sistemas de archivos son adecuados (ver: [limitaciones de los sistema de archivos](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Limits "wikipedia:Comparison of file systems")).
*   el sistema de archivos debe apoyar su aumento y reducción mientras se está en línea (ver: [características de los sistemas de archivos](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Features "wikipedia:Comparison of file systems")).
*   se debe calcular el stride y stripe-width correctos para un rendimiento óptimo.

#### Calcular el stride y stripe-width

Stride = (tamaño chunk/tamaño bloque).

Stripe-width = (# discos de **datos** físicos * stride).

##### Ejemplo 1\. RAID0

Ejemplo formateando con sistema de archivos ext4 con stride y stripe-width correctas:

*   Hipotética matriz RAID0 que se compone de 2 discos físicos.
*   El tamaño de Chunk es 64k.
*   El tamaño del bloque es 4k.

Stride = (tamaño chunk/tamaño bloque). En este ejemplo, la matemática es (64/4) por lo que stride = 16.

Stripe-width = (# discos de **datos** físicos * stride). En este ejemplo, la matemática es (2*16) por lo que stripe-width = 32.

```
# mkfs.ext4 -v -L myarray -m 0.5 -b 4096 -E stride=16,stripe-width=32 /dev/md0

```

##### Ejemplo 2\. RAID5

Ejemplo formateando con sistema de archivos ext4 con stride y stripe-width correctas:

*   Hipotética matriz RAID5 que se compone de 4 discos físicos; 3 discos de datos y 1 disco de paridad.
*   El tamaño chunk es 256k.
*   El tamaño de bloque es 4k.

Stride = (tamaño chunk/tamaño de bloque). En este ejemplo, la matemática es (256/4) por lo que stride = 64.

Stripe-width = (# discos de **datos** físicos * stride). En este ejemplo, la matemática es (3*64) de modo que stripe-width = 192.

```
# mkfs.ext4 -v -L myarray -m 0.5 -b 4096 -E stride=64,stripe-width=192 /dev/md0

```

Para más información sobre stride y stripe-width, ver: [Matemáticas RAID](http://wiki.centos.org/HowTos/Disk_Optimization).

**Nota:** del traductor:

*   Stride: es el número de posicionamiento en la memoria entre los comienzos de uno y otro de los sucesivos elementos de la matriz, se puede traducir por «zancada», «banda» o «tira».
*   Stride-width: es el tamaño o ancho de la zancada.
*   Chunk: es la masa «atómica» más pequeña de datos que puede ser escrita en los dispositivos, lo podríamos traducir por «porción».

## Montar desde un CD live

Los usuarios que quieran montar la partición RAID desde un CD live, escriban:

```
# mdadm --assemble /dev/<disk1> /dev/<disk2> /dev/<disk3> /dev/<disk4>

```

## Instalar Arch Linux en RAID

**Nota:** La siguiente sección se aplica solo si el sistema de archivos raíz reside en la matriz. Los usuarios pueden saltarse esta sección si la matriz contiene una partición(s) de datos.

Se debe crear la matriz RAID entre los pasos de [particionar](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") y [formatear](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)") del proceso de instalación. En lugar de formatear directamente una partición para que sea su sistema de archivos raíz, ello se hará sobre la matriz RAID. Siga la sección [#Instalación](#Instalación) para crear la matriz RAID. Luego, continúe con el procedimiento de instalación hasta que se complete el paso pacstrap. Al usar [arranque UEFI](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"), consulte también [ESP en RAID](/index.php/EFI_system_partition#ESP_on_RAID "EFI system partition").

### Actualizar archivo de configuración

**Nota:** Esto debe hacerse fuera de chroot, de ahí el prefijo /mnt en la ruta de archivo.

Después de que el sistema base se haya instalado, el archivo de configuración por defecto, `mdadm.conf`, debe ser actualizado, así:

```
# mdadm --detail --scan >> /mnt/etc/mdadm.conf

```

Compruebe siempre el archivo de configuración mdadm.conf con un editor de texto después de ejecutar esta orden, para asegurarse de que su contenido parece razonable.

Continuar con el proceso de instalación hasta que llegue al paso «Crear un entorno inicial ramdisk» y, a continuación, siga en sección siguiente.

### Añadir el hook mdadm a mkinitcpio.conf

**Nota:** Esto debe hacerse en entorno chroot.

Agregue `mdadm_udev` a la sección [HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") de [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") para añadir soporte para mdadm directamente en la imagen ram inicial:

 `HOOKS="base udev autodetect block **mdadm_udev** filesystems usbinput fsck"` 

Regenere la imagen initramfs (ver [creación y activación de imagen](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")) después de hacer la modificación de la matriz HOOKS:

```
# mkinitcpio -p linux

```

### Configurar syslinux

Cuando se utiliza el gestor de arranque syslinux, hay que ajustar la línea de órdenes del kernel mediante la configuración de `/boot/syslinux/syslinux.cfg`. Cambie la línea `APPEND` para adaptarse a sus matrices RAID. Como ejemplo, el siguiente tiene capacidad para tres matrices RAID 1 y establece la apropiada como root:

```
APPEND root=/dev/md1 rw md=0,/dev/sda2,/dev/sdb2 md=1,/dev/sda3,/dev/sdb3 md=2,/dev/sda4,/dev/sdb4

```

Si el arranque desde una partición de RAID por sotfware falla al utilizar el método de nodos de dispositivos del kernel descrito, como método alternativo, más confiable, se pueden usar las etiquetas de las particiones:

```
APPEND root=LABEL=THEROOTPARTITIONLABEL rw

```

## Mantenimiento de RAID

### Depuración

Es una buena práctica para que los datos funcionen con normalidad [hacer una depuración](https://en.wikipedia.org/wiki/Data_scrubbing "wikipedia:Data scrubbing") para comprobar y corregir los errores. Dependiendo del tamaño/configuración de la matriz, una depuración puede durar varias horas en completarse.

Para iniciar una depuración de datos:

```
# echo check > /sys/block/md0/md/sync_action

```

La operación de verificación escanea las unidades para los sectores defectuosos y los repara automáticamente. Si encuentra sectores no defectuosos que contienen datos erróneos (los datos de un sector no concuerdan con los datos que otro disco nos indica que debería tener, por ejemplo, el bloque de paridad + los demás bloques de datos, nos haría pensar que este bloque de datos es incorrecto), entonces no se toma ninguna acción, pero el evento se registra (ver más abajo). Este «no hacer nada», permite a los administradores inspeccionar los datos en el sector y los datos que se producirían mediante la reconstrucción de los sectores con la información redundante, y escoger los datos correctos a mantener.

Como con muchas tareas/artículos relativos a mdadm, el estado de la limpieza se puede consultar mediante la lectura de`/proc/mdstat`.

Ejemplo:

 `$ cat /proc/mdstat` 
```
Personalities : [raid6] [raid5] [raid4] [raid1] 
md0 : active raid1 sdb1[0] sdc1[1]
      3906778112 blocks super 1.2 [2/2] [UU]
      [>....................]  check =  4.0% (158288320/3906778112) finish=386.5min speed=161604K/sec
      bitmap: 0/30 pages [0KB], 65536KB chunk

```

Para detener con seguridad una depuración de datos cuya ejecución está en curso:

```
# echo idle > /sys/block/md0/md/sync_action

```

**Nota:** Si se reinicia el sistema después que una depuración parcial haya sido suspendida, la depuración comenzará de nuevo.

Cuando la depuración se ha completado, los administradores pueden comprobar cuántos bloques (si los hay) se han marcado como erróneos:

```
# cat /sys/block/md0/md/mismatch_cnt

```

#### Notas generales sobre la depuración

**Nota:** Los usuarios pueden alternativamente aplicar echo **repair** a /sys/block/md0/md/sync_action, pero esto es poco aconsejable, ya que si se encuentra una falta de coincidencia en los datos, se actualizará automáticamente para mantener la coherencia. El peligro es que realmente no sabemos si se trata de una falta de paridad o el bloque de datos es correcto (o cuál bloque de datos en caso de RAID 1). Es una cuestión de azar si la operación recibe los datos correctos en lugar de los datos erróneos.

Es una buena idea establecer un trabajo cron como root para programar una limpieza periódica. Ver [raid-check](https://aur.archlinux.org/packages/raid-check/) que puede ayudar con esto.

#### Notas sobre la depuración de RAID1 y RAID10

Debido al hecho de que RAID 1 y RAID 10 escriben en el kernel sin búfer, una matriz puede tener cuentas desajustadas sin 0 incluso cuando la matriz es saludable. Estos recuentos sin 0 solo existirán en áreas de datos transitorios en los que no suponen un problema. Sin embargo, no podemos discernir la diferencia entre una cuenta sin 0 respecto de datos transitorios, con un recuento sin 0 que signifique un verdadero problema. Este hecho es una fuente de falsos positivos en matrices RAID 1 y RAID 10\. Sin embargo, a pesar de ello se recomienda realizar depuraciones regularmente con el fin de detectar y corregir los sectores erróneos que pueden estar presentes en los dispositivos.

### Extracción de dispositivos de una matriz

Se puede eliminar un dispositivo de la matriz después de marcarlo como defectuoso:

```
# mdadm --fail /dev/md0 /dev/sdxx

```

Ahora quítelo de la matriz:

```
# mdadm -r /dev/md0 /dev/sdxx

```

Retire el dispositivo de forma permanente (por ejemplo, para utilizarlo de forma individual a partir de ahora): emita las dos órdenes descritas anteriormente, y luego:

```
# mdadm --zero-superblock /dev/sdxx

```

**Advertencia:** La reutilización del disco eliminado sin reducción a cero del superbloque **CAUSARÁ LA PÉRDIDA DE TODOS LOS DATOS** en el siguiente arranque (dado que mdadm puede tratar de utilizarlo como parte de la matriz RAID). **NO** ejecute esta orden en matrices RAID0 o lineales, o **PERDERÁ** los datos

Para dejar de usar una matriz:

1.  desmontar la matriz de destino;
2.  detener la matriz con: `mdadm --stop /dev/md0`;
3.  repetir las tres órdenes descritas al principio de esta sección en cada dispositivo;
4.  quitar la línea correspondiente de /etc/mdadm.conf.

### Adición de un nuevo dispositivo a una matriz

La adición de nuevos dispositivos con mdadm se puede hacer en un sistema en funcionamiento con los dispositivos montados. Particione el nuevo dispositivo usando el mismo diseño de uno de los que ya están en la matriz, como se mencionó anteriormente.

Monte la matriz RAID si no está ya montada:

```
# mdadm --assemble /dev/md0 /dev/sda1 /dev/sdb1

```

Agregue el nuevo dispositivo de la matriz:

```
# mdadm --add /dev/md0 /dev/sdc1

```

Esto no debe llevarle mucho tiempo a mdadm. Una vez más, comprobar el progreso con:

```
# cat /proc/mdstat

```

Compruebe que el dispositivo se ha añadido, con la orden:

```
# mdadm --misc --detail /dev/md0

```

#### Para matrices RAID0

Si obtiene un error como:

```
mdadm: add new device failed for /dev/sdc1 as 2: Invalid argument

```

Puede ser porque está utilizando RAID 0\. La orden anterior sumará el nuevo disco como un «repuesto», pero RAID0 no tiene repuestos. Si desea agregar un dispositivo a una matriz RAID 0, tiene que realizar el «aumento» y la «adición» en la misma orden:

```
# mdadm --grow /dev/md0 --raid-devices=3 --add /dev/sdc1

```

## Monitorización

Una simple orden de una sola línea imprime el estado de los dispositivos RAID:

```
awk '/^md/ {printf "%s: ", $1}; /blocks/ {print $NF}' </proc/mdstat

```

```
md1: [UU]
md0: [UU]

```

### Observar estado con mdstat

 `watch -t 'cat /proc/mdstat'` 

O preferiblemente usando [tmux](https://www.archlinux.org/packages/?name=tmux)

 `tmux split-window -l 12 "watch -t 'cat /proc/mdstat'"` 

### Seguimiento E/S con iotop

El paquete [iotop](https://www.archlinux.org/packages/?name=iotop) muestra las estadísticas de entrada/salida para los procesos. Utilice esta orden para ver la E/S para los hilos de raid.

 `iotop -a -p $(sed 's, , -p ,g' <<<`pgrep "_raid|_resync|jbd2"`)` 

### Seguimiento E/S con iostat

La utilidad *iostat* del paquete [sysstat](https://www.archlinux.org/packages/?name=sysstat) muestra las estadísticas de entrada/salida para los dispositivos y las particiones.

```
 iostat -dmy 1 /dev/md0
 iostat -dmy 1 # todo

```

### Correos sobre eventos

Un servidor de correo SMTP (sendmail) o al menos un agente de correo electrónico (ssmtp/msmtp) es necesario para lograr esto. Tal vez la solución más simple es utilizar [dma](https://aur.archlinux.org/packages/dma/) que es muy pequeño (instala 0,08 MiB) y no requiere instalación.

Editar `/etc/mdadm.conf` para definir la dirección de correo electrónico en la que se recibirán notificaciones.

**Nota:** Si utiliza dma como se mencionó anteriormente, los usuarios pueden simplemente enviar correos directamente al nombre de usuario en el equipo local, en lugar de a una dirección de correo electrónico externo.

Para probar la configuración:

```
# mdadm --monitor --scan -1 --test

```

[mdadm](/index.php/Mdadm "Mdadm") incluye un servicio de systemd (mdmonitor.service) para llevar a cabo la tarea de control, por lo que en este punto, no tiene nada más que hacer. Si no configura un correo electrónico en `/etc/mdadm.conf`, dicho servicio fallará. Si no desea recibir correos sobre eventos mdadm, el fallo puede ser ignorado; si no desea recibir las notificaciones ni los mensajes acerca del error, puede enmascarar la unidad.

#### Método alternativo

Para evitar la instalación de un servidor de correo SMTP o un expedidor de correo electrónico, puede utilizar la herramienta [S-nail](/index.php/S-nail "S-nail") (no se olvide de configurarla) ya presente en el sistema.

Cree un archivo llamado `/etc/mdadm_warning.sh` con:

```
#!/bin/bash
event=$1
device=$2

echo " " | /usr/bin/mailx -s "$event on $device" **destination@email.com**

```

Y dele permisos de ejecución: `chmod +x /etc/mdadm_warning.sh`

A continuación, agregue esto a mdadm.conf

```
PROGRAM /etc/mdadm_warning.sh

```

Puede probar y activar el uso de la misma como en el método anterior.

## Solución de problemas

### Error: «invalid raid superblock magic»

Si está obteniendo el error «invalid raid superblock magic» al reiniciar y tiene otros discos duros adicionales que sean los componentes de la matriz, verifique que el orden de los discos duros es el correcto. Durante la instalación, los dispositivos RAID pueden ser HDD, HDE y HDF, pero durante el arranque pueden ser hda, hdb y hdc. Ajuste su línea del kernel en consecuencia.

### Error: «kernel: ataX.00: revalidation failed»

Si de repente (después del reinicio, al cambiar la configuración del BIOS) experimenta mensajes de error como:

```
Feb  9 08:15:46 hostserver kernel: ata8.00: revalidation failed (errno=-5)

```

no significa necesariamente que una unidad esté rota. A menudo se encuentran enlaces de pánico en la web que indican lo peor. En una palabra, *No Panic* (que no cunda el pánico). Tal vez acaba de cambiar la configuración de APIC o ACPI en la BIOS o los parámetros del kernel de algún modo. Cámbielos de nuevo y debería funcionar bien. Generalmente, cambiar ACPI y/o apagar ACPI debe ayudar.

### Iniciar matrices en solo lectura

Cuando se inicia una matriz md, el superbloque será escrito, y puede iniciarse la resincronización. Para comenzar en solo lectura, establecer el módulo del kernel `md_mod` con el parámetro `start_ro`. Cuando se establece, las nuevas matrices vendrán activadas un modo «auto-ro», que desactiva todas las e/s internas (actualizaciones de superbloque, resincronización, recuperación) y se pone automáticamente en «rw» cuando llega la primera solicitud de escritura.

**Nota:** La matriz se puede establecer en modo «ro» usando `mdadm --readonly` antes que venga la primera solicitud de escritura, o se puede iniciar la resincronización sin una solicitud de escritura mediante `mdadm --readwrite`.

Para establecer el parámetro en el arranque, añadir `md_mod.start_ro=1` a la línea del kernel.

O establezca el parámetro al tiempo de cargar el módulo desde el archivo `/etc/modprobe.d/` o directamente desde `/sys/`.

 `echo 1 > /sys/module/md_mod/parameters/start_ro` 

### Recuperación de una unidad rota o ausente en el raid

Se puede obtener el error mencionado anteriormente también cuando una de las unidades se rompe por cualquier razón. En ese caso, tendrá que forzar a raid a encender con un disco más corto. Escriba esta orden (modificar cuando sea necesario):

```
# mdadm --manage /dev/md0 --run

```

Ahora debería ser capaz de montarla de nuevo con algo como esto (si es que lo tenía en fstab):

```
# mount /dev/md0

```

Ahora el raid debería estar funcionando de nuevo y disponible para su uso, sin embargo, con un disco corto. Después, debe particionar el disco de la manera como se ha descrito anteriormente en la sección para [preparar los dispositivos](#Preparar_los_dispositivos). Una vez hecho esto puede agregar el nuevo disco a la matriz escribiendo:

```
# mdadm --manage --add /dev/md0 /dev/sdd1

```

Si escribe:

```
# cat /proc/mdstat

```

es probable que vea que el raid ya está activo y en reconstrucción.

También puede actualizar su configuración (ver: [#Actualizar archivo de configuración](#Actualizar_archivo_de_configuración)).

## Benchmarking

Vea [Wikipedia:es:Benchmark (informática)](https://en.wikipedia.org/wiki/es:Benchmark_(inform%C3%A1tica) "wikipedia:es:Benchmark (informática)").

Hay varias herramientas para la evaluación comparativa de un RAID. La mejora más notable es el aumento de la velocidad cuando varios subprocesos están leyendo desde el mismo volumen RAID.

[Tiobench](http://sourceforge.net/projects/tiobench/) es un programa que mide las mejoras de rendimiento mediante la medición completa de E/S de los hilos del disco.

[Bonnie++](http://www.coker.com.au/bonnie++/) analiza el tipo de acceso a la base de datos para uno o más archivos, y la creación, lectura y borrado de archivos pequeños que puede simular el uso de programas como Squid, INN, o el formato de e-mail Maildir. El programa [ZCAV](http://www.coker.com.au/bonnie++/zcav/) pone a prueba el rendimiento de diferentes zonas de un disco duro sin necesidad de escribir ningún dato en el disco.

`hdparm` **NO** debería ser utilizado para comparar un RAID, ya que proporciona resultados muy inconsistentes.

## Véase también

*   [Software RAID in the new Linux 2.4 kernel, Part 1](http://www.gentoo.org/doc/en/articles/software-raid-p1.xml) and [Part 2](http://www.gentoo.org/doc/en/articles/software-raid-p2.xml) in the Gentoo Linux Docs
*   [Linux RAID wiki entry](http://raid.wiki.kernel.org/index.php/Linux_Raid) on The Linux Kernel Archives
*   [How Bitmaps Work](https://raid.wiki.kernel.org/index.php/Write-intent_bitmap)
*   [Arch Linux software RAID installation guide](http://linux-101.org/howto/arch-linux-software-raid-installation-guide) on Linux 101
*   [Chapter 15: Redundant Array of Independent Disks (RAID)](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-raid.html) of Red Hat Enterprise Linux 6 Documentation
*   [Linux-RAID FAQ](http://tldp.org/FAQ/Linux-RAID-FAQ/x37.html) on the Linux Documentation Project
*   [Dell.com Raid Tutorial](http://support.dell.com/support/topics/global.aspx/support/entvideos/raid?c=us&l=en&s=gen) - Interactive Walkthrough of Raid
*   [BAARF](http://www.miracleas.com/BAARF/) including *[Why should I not use RAID 5?](http://www.miracleas.com/BAARF/RAID5_versus_RAID10.txt)* by Art S. Kagel
*   [Introduction to RAID](http://www.linux-mag.com/id/7924/), [Nested-RAID: RAID-5 and RAID-6 Based Configurations](http://www.linux-mag.com/id/7931/), [Intro to Nested-RAID: RAID-01 and RAID-10](http://www.linux-mag.com/id/7928/), and [Nested-RAID: The Triple Lindy](http://www.linux-mag.com/id/7932/) in Linux Magazine
*   [HowTo: Speed Up Linux Software Raid Building And Re-syncing](http://www.cyberciti.biz/tips/linux-raid-increase-resync-rebuild-speed.html)
*   [RAID5-Server to hold all your data](http://fomori.org/blog/?p=94)

**mdadm**

*   [Debian mdadm FAQ](http://anonscm.debian.org/gitweb/?p=pkg-mdadm/mdadm.git;a=blob_plain;f=debian/FAQ;hb=HEAD)
*   [mdadm source code](http://www.kernel.org/pub/linux/utils/raid/mdadm/)
*   [Software RAID on Linux with mdadm](http://www.linux-mag.com/id/7939/) in Linux Magazine

**Hilos del foro**

*   [Raid Performance Improvements with bitmaps](http://forums.overclockers.com.au/showthread.php?t=865333)
*   [GRUB and GRUB2](https://bbs.archlinux.org/viewtopic.php?id=125445)
*   [Can't install grub2 on software RAID](https://bbs.archlinux.org/viewtopic.php?id=123698)
*   [Use RAID metadata 1.2 in boot and root partition](http://forums.gentoo.org/viewtopic-t-888624-start-0.html)

**RAID con encryption**

*   [Linux/Fedora: Encrypt /home and swap over RAID with dm-crypt](http://www.shimari.com/dm-crypt-on-raid/) by Justin Wells