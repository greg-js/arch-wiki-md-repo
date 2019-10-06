**Estado de la traducción**
Este artículo es una traducción de [RAID](/index.php/RAID "RAID"), revisada por última vez el **2019-09-30**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=RAID&diff=0&oldid=580689) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [LVM (Español)#RAID](/index.php/LVM_(Espa%C3%B1ol)#RAID "LVM (Español)")
*   [Installing with Fake RAID](/index.php/Installing_with_Fake_RAID "Installing with Fake RAID")
*   [Convert a single drive system to RAID](/index.php/Convert_a_single_drive_system_to_RAID "Convert a single drive system to RAID")
*   [ZFS](/index.php/ZFS "ZFS")
*   [ZFS/Virtual disks](/index.php/ZFS/Virtual_disks "ZFS/Virtual disks")
*   [Swap (Español)#Striping](/index.php/Swap_(Espa%C3%B1ol)#Striping "Swap (Español)")
*   [Btrfs#RAID](/index.php/Btrfs#RAID "Btrfs")

*Redundant Array of Independent Disks* (Matriz Redundante de Discos Independientes, siglas en inglés [RAID](https://en.wikipedia.org/wiki/es:RAID "wikipedia:es:RAID")) es una tecnología de almacenamiento que combina varios componentes de unidades de disco —normalmente unidades de disco o particiones de los mismos— en una unidad lógica. Dependiendo de la implementación de RAID, la unidad lógica puede ser un sistema de archivos o una capa transparente adicional que puede contener varias particiones. Los datos se distribuyen a través de las unidades de una las muchas maneras que hay, llamadas [#Niveles RAID](#Niveles_RAID), dependiendo del nivel de redundancia y del rendimiento requeridos. El nivel RAID elegido, por lo tanto, va a depender de si lo que se quiere es prevenir la pérdida de datos en caso de un fallo del disco duro, aumentar el rendimiento o una combinación de ambos.

En este artículo se explica qué es RAID y cómo crear/administrar una matriz RAID por software utilizando mdadm.

**Advertencia:** asegúrese de [hacer una copia de seguridad](/index.php/Backup_programs "Backup programs") de todos los datos antes de continuar.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Niveles RAID](#Niveles_RAID)
    *   [1.1 Niveles RAID estándar](#Niveles_RAID_estándar)
    *   [1.2 Niveles RAID anidados](#Niveles_RAID_anidados)
    *   [1.3 Comparación de niveles RAID](#Comparación_de_niveles_RAID)
*   [2 Implementación](#Implementación)
    *   [2.1 ¿Qué tipo de RAID tengo?](#¿Qué_tipo_de_RAID_tengo?)
*   [3 Instalación](#Instalación)
    *   [3.1 Preparar los dispositivos](#Preparar_los_dispositivos)
    *   [3.2 Particionar los dispositivos](#Particionar_los_dispositivos)
        *   [3.2.1 Tabla de particiones GUID](#Tabla_de_particiones_GUID)
        *   [3.2.2 Master Boot Record](#Master_Boot_Record)
    *   [3.3 Compilar la matriz](#Compilar_la_matriz)
    *   [3.4 Actualizar archivo de configuración](#Actualizar_archivo_de_configuración)
    *   [3.5 Ensamblar la matriz](#Ensamblar_la_matriz)
    *   [3.6 Formatear RAID con un sistema de archivos](#Formatear_RAID_con_un_sistema_de_archivos)
        *   [3.6.1 Calcular el stride y stripe-width](#Calcular_el_stride_y_stripe-width)
            *   [3.6.1.1 Ejemplo 1\. RAID0](#Ejemplo_1._RAID0)
            *   [3.6.1.2 Ejemplo 2\. RAID5](#Ejemplo_2._RAID5)
            *   [3.6.1.3 Example 3\. RAID10,far2](#Example_3._RAID10,far2)
*   [4 Montar desde un CD live](#Montar_desde_un_CD_live)
*   [5 Instalar Arch Linux en RAID](#Instalar_Arch_Linux_en_RAID)
    *   [5.1 Actualizar archivo de configuración](#Actualizar_archivo_de_configuración_2)
    *   [5.2 Configurar mkinitcpio](#Configurar_mkinitcpio)
    *   [5.3 Configurar el gestor de arranque](#Configurar_el_gestor_de_arranque)
*   [6 Mantenimiento de RAID](#Mantenimiento_de_RAID)
    *   [6.1 Depuración](#Depuración)
        *   [6.1.1 Notas generales sobre la depuración](#Notas_generales_sobre_la_depuración)
        *   [6.1.2 Notas sobre la depuración de RAID1 y RAID10](#Notas_sobre_la_depuración_de_RAID1_y_RAID10)
    *   [6.2 Extracción de dispositivos de una matriz](#Extracción_de_dispositivos_de_una_matriz)
    *   [6.3 Adición de un nuevo dispositivo a una matriz](#Adición_de_un_nuevo_dispositivo_a_una_matriz)
    *   [6.4 Incrementar tamaño de un volumen RAID](#Incrementar_tamaño_de_un_volumen_RAID)
    *   [6.5 Cambiar los límites de velocidad de sincronización](#Cambiar_los_límites_de_velocidad_de_sincronización)
*   [7 Monitorización](#Monitorización)
    *   [7.1 Observar estado con mdstat](#Observar_estado_con_mdstat)
    *   [7.2 Seguimiento Entrada/Salida con iotop](#Seguimiento_Entrada/Salida_con_iotop)
    *   [7.3 Seguimiento Entrada/Salida con iostat](#Seguimiento_Entrada/Salida_con_iostat)
    *   [7.4 Correos sobre eventos](#Correos_sobre_eventos)
        *   [7.4.1 Método alternativo](#Método_alternativo)
*   [8 Solución de problemas](#Solución_de_problemas)
    *   [8.1 Error: «invalid raid superblock magic»](#Error:_«invalid_raid_superblock_magic»)
    *   [8.2 Error: «kernel: ataX.00: revalidation failed»](#Error:_«kernel:_ataX.00:_revalidation_failed»)
    *   [8.3 Iniciar matrices en solo lectura](#Iniciar_matrices_en_solo_lectura)
    *   [8.4 Recuperación de una unidad rota o ausente en el raid](#Recuperación_de_una_unidad_rota_o_ausente_en_el_raid)
*   [9 Benchmarking](#Benchmarking)
*   [10 Véase también](#Véase_también)

## Niveles RAID

A pesar de la redundancia implícita en la mayoría de los niveles de RAID, RAID no garantiza que los datos estén seguros. Un RAID no protegerá los datos si el equipo se quema, es robado o fallan varios discos duros a la vez. Además, instalar un sistema con RAID es un proceso complejo que puede destruir datos.

### Niveles RAID estándar

Hay muchos [niveles de RAID](https://en.wikipedia.org/wiki/Standard_RAID_levels "wikipedia:Standard RAID levels"), sírvase encontrar a continuación los más comúnmente usados.

	[RAID 0](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_0 "wikipedia:Standard RAID levels")

	Utiliza [striping](https://en.wikipedia.org/wiki/es:Striping "wikipedia:es:Striping") para combinar discos. A pesar de que *no proporciona redundancia* (es decir, la posibilidad de recuperar o reconstruir los datos almacenados), todavía se considera RAID. Lo que si hace, sin embargo, es *proporcionar un gran beneficio de velocidad*. Si el aumento de la velocidad vale la pena ante la posibilidad de pérdida de datos (para la partición [swap (Español)](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)"), por ejemplo), elija este nivel de RAID. En un servidor, las matrices RAID 1 y RAID 5 son las más apropiadas. El tamaño de un dispositivo de bloques de una matriz RAID 0 equivale al tamaño de la partición más pequeña que la compone de entre el número de particiones integrantes.

	[RAID 1](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_1 "wikipedia:Standard RAID levels")

	Es el nivel RAID más simple: replicación pura. Al igual que con otros niveles de RAID, solo tiene sentido si las particiones están en diferentes unidades de discos físicos. Si una de esas unidades falla, el dispositivo de bloque proporcionado por la matriz RAID va a seguir funcionando con normalidad. El ejemplo que se utiliza es RAID 1 para todo, excepto [swap](/index.php/Swap "Swap") y los datos temporales. Tenga en cuenta que con una implementación por software, el nivel de RAID 1 es la única opción para la partición de arranque, porque los gestores de arranque, que leen la partición de arranque, no entienden de RAID, pero una partición integrante de RAID 1 puede ser leída como una partición normal. El tamaño de un sistema RAID 1 equivale a la dimensión de la partición más pequeña que lo compone.

	[RAID 5](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_5 "wikipedia:Standard RAID levels")

	Requiere 3 o más unidades físicas, y proporciona la redundancia de RAID 1 en combinación con la velocidad y los beneficios del tamaño de RAID 0\. RAID 5 utiliza *striping*, como RAID 0, pero también bloques de paridad de almacenaje *distribuidos entre cada disco miembro*. En el caso de que un disco falle, estos bloques de paridad se utilizan para reconstruir los datos en un disco de reemplazo. RAID 5 puede soportar la pérdida de uno de los discos miembros.

**Nota:** RAID 5 es una opción común debido a su combinación de velocidad y redundancia de datos. La advertencia es que si una unidad falla y, antes de que fuera reemplazada, la otra unidad fallara, se perderían todos los datos. Además, con los tamaños de los disco modernos y las tasas de error de lectura (URE) irrecuperables esperadas en los discos de consumo, **se espera** que la reconstrucción de una matriz de 4TiB (es decir, una probabilidad superior al 50%) tenga al menos una URE. Debido a esto, RAID 5 ya no es aconsejado por la industria del almacenamiento.

	[RAID 6](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_6 "wikipedia:Standard RAID levels")

	Requiere 4 o más unidades físicas, y proporciona los beneficios de RAID 5 pero con seguridad contra el fallo de dos unidades. RAID 6 también usa striping, como RAID 5, pero almacena dos bloques de paridad distintos *distribuidos en cada disco miembro*. En el caso de que falle un disco, estos bloques de paridad se utilizan para reconstruir los datos en un disco de reemplazo. RAID 6 puede soportar la pérdida de dos discos miembros. La robustez frente a errores de lectura irrecuperables es algo mejor, porque la matriz todavía tiene bloques de paridad cuando se reconstruye desde una sola unidad fallida. Sin embargo, dada la sobrecarga, RAID 6 es costoso y en la mayoría de las configuraciones RAID 10 en el diseño far2 (ver más abajo) proporciona mejores beneficios de velocidad y robustez, y por lo tanto es preferible.

### Niveles RAID anidados

	[RAID 1+0](https://en.wikipedia.org/wiki/Nested_RAID_levels#RAID_10_.28RAID_1.2B0.29 "wikipedia:Nested RAID levels")

	RAID1+0 es un RAID anidado que combina dos de los niveles estándar de RAID para obtener rendimiento y redundancia adicional. Se le conoce comúnmente como *RAID10* , sin embargo, Linux MD RAID10 es ligeramente diferente de las capas RAID simples, ver más abajo.

	[RAID 10](https://en.wikipedia.org/wiki/Non-standard_RAID_levels#Linux_MD_RAID_10 "wikipedia:Non-standard RAID levels")

	RAID10 bajo Linux se basa en los conceptos de RAID1+0, sin embargo, implementa esto como una sola capa, con múltiples diseños posibles.

	El diseño *near X* en los discos Y repite cada trozo X veces en franjas Y/2, pero no necesita X para dividir Y de manera uniforme. Los fragmentos se colocan en casi la misma ubicación en cada disco en el que se replican, de ahí el nombre. Puede funcionar con cualquier cantidad de discos, comenzando con 2\. Near de 2 en 2 discos es equivalente a RAID1, near de 2 en 4 discos a RAID1+0.

	El diseño *far X* en los discos Y está diseñado para ofrecer un rendimiento de lectura striped en una matriz replicada. Esto se logra dividiendo cada disco en dos secciones, por ejemplo, adelante y atrás, y lo que está escrito al principio del disco 1 se refleja al final del disco 2, y viceversa. Esto tiene el efecto de poder dividir las lecturas secuenciales, que es de donde RAID0 y RAID5 obtienen su rendimiento. El inconveniente es que la escritura secuencial tiene una penalización de rendimiento muy leve debido a la distancia que el disco necesita alcanzar hasta la otra sección del disco para almacenar la réplica. Sin embargo, RAID10 en el diseño de far 2 es preferible a RAID1+0 **y** RAID5 en capas siempre que las velocidades de lectura sean preocupantes y la disponibilidad/redundancia sea crucial. Sin embargo, todavía no es un sustituto de las copias de seguridad. Vea la página de wikipedia para más información.

**Advertencia:** mdadm no puede cambiar la forma de las matrices en diseños de *far X*, lo que significa que una vez que se haya creado la matriz, no podrá realizar `mdadm --grow`. Por ejemplo, si tiene una matriz RAID10 de 4x1 TB y desea cambiar a discos de 2 TB, su capacidad utilizable seguirá siendo de 2 TB. Para tales casos de uso, adhiérase al diseño *near X*.

### Comparación de niveles RAID

| Nivel RAID | Redundancia de datos | Utilización de la unidad física | Rendimiento de lectura | Rendimiento de escritura | Unidades mínimas |
| **0** | No | 100% | nX

**Máxima**

 | nX

**Máxima**

 | 2 |
| **1** | Sí | 50% | Hasta nX si se leen múltiples procesos, de lo contrario 1X | 1X | 2 |
| **5** | Sí | 67% - 94% | (n−1)X

**Superior**

 | (n−1)X

**Superior**

 | 3 |
| **6** | Sí | 50% - 88% | (n−2)X | (n−2)X | 4 |
| **10,far2** | Sí | 50% | nX

**Superior;** a la par con RAID0 pero redundante

 | (n/2)X | 2 |
| **10,near2** | Sí | 50% | Hasta nX si se leen múltiples procesos, de lo contrario 1X | (n/2)X | 2 |

* Donde *n* es el *standing* multiplicado por el número de discos dedicados.

## Implementación

Los dispositivos RAID pueden gestionarse de diferentes maneras:

	RAID por software

	Esta es la implementación más fácil, ya que no se basa en firmware y software propietarios para ser utilizado. La matriz es administrada por el sistema operativo, ya sea:

*   por una capa de abstracción (por ejemplo, [mdadm](#Instalación));
    **Nota:** este es el método que utilizaremos más adelante en esta guía.

*   por un gestor de volúmenes lógicos (por ejemplo, [LVM](/index.php/LVM_(Espa%C3%B1ol)#RAID "LVM (Español)"));
*   por un componente de un sistema de archivos (por ejemplo, [ZFS](/index.php/ZFS "ZFS"), [Btrfs](/index.php/Btrfs#RAID "Btrfs")).

	RAID por hardware

	La matriz está gestionada directamente por una tarjeta de hardware dedicada instalada en el PC al que los discos se conectan directamente. La lógica RAID se ejecuta en un procesador de la placa base independientemente del [procesador del equipo (CPU)](https://en.wikipedia.org/wiki/es:Unidad_central_de_procesamiento "wikipedia:es:Unidad central de procesamiento"). Aunque esta solución es independiente de cualquier sistema operativo, este último requiere un controlador para poder funcionar correctamente con la controladora de RAID por hardware. La matriz RAID, o bien se puede configurar a través de una opción de la interfaz rom o, según el fabricante, con una aplicación dedicada, cuando se ha instalado el sistema operativo. La configuración es transparente para el kernel de Linux: no ve los discos por separado.

	[FakeRAID](/index.php/Fakeraid "Fakeraid")

	Este tipo de RAID es llamado propiamente BIOS o RAID integrado en la placa base, pero es falsamente anunciado como RAID por hardware. La matriz está gestionada por controladoras pseudoRAID donde la lógica RAID se implementa en una opción de rom o en el propio firmware [con un EFI SataDriver](http://www.win-raid.com/t19f13-Intel-EFI-RAID-quot-SataDriver-quot-BIOS-Modules.html) (en el caso de [Unified Extensible Firmware Interface (Español)](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)")), pero no son completas controladoras de RAID por hardware con *todas* las funciones RAID implementadas. Por lo tanto, este tipo de RAID a veces se llama fakeRAID. [dmraid](https://www.archlinux.org/packages/?name=dmraid) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"), se utilizará para suplir a estas controladoras. Algunos ejemplos de controladoras FakeRAID son: [Intel Rapid Storage](https://en.wikipedia.org/wiki/Intel_Rapid_Storage_Technology "wikipedia:Intel Rapid Storage Technology"), JMicron JMB36x RAID ROM, AMD RAID, ASMedia 106x y NVIDIA MediaShield.

### ¿Qué tipo de RAID tengo?

Dado que el RAID por software se implementa por el usuario, este tipo de RAID es fácilmente conocido por el usuario.

Sin embargo, discernir entre fakeRAID y RAID por hardware verdadero puede ser más difícil. Los fabricantes no suelen distinguir correctamente estos dos tipos de RAID y siempre es posible falsear la publicidad. La mejor solución, en estos casos, es ejecutar la orden `lspci` y mirar la salida para encontrar la controladora RAID. A continuación, realice una búsqueda para ver qué información puede definir dicha controladora RAID. Los controladores RAID por hardware aparecen en esta lista, pero las implementaciones de FakeRAID no. Además, los verdaderos controladores de RAID por hardware a menudo son bastante caros, por lo que si alguien personaliza el sistema, es muy probable que al elegir una configuración RAID por hardware haya un cambio muy notable en el precio del equipo.

## Instalación

Instale [mdadm](https://www.archlinux.org/packages/?name=mdadm) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). *mdadm* se utiliza para la administración de RAID por software puro usando dispositivos de bloque plano: el hardware subyacente no ofrece ninguna lógica RAID, solo un suministro de discos. *mdadm* funcionará con cualquier colección de dispositivos de bloques. Incluso si son inusuales. Por ejemplo, se puede, pues, hacer un matriz RAID de una colección de memorias USB.

### Preparar los dispositivos

**Advertencia:** estos pasos borran todo el contenido de un dispositivo, por lo que escriba con cuidado.

Si el dispositivo está siendo reutilizado o repuesto de una matriz existente, borre cualquier información de configuración RAID antigua:

```
# mdadm --misc --zero-superblock /dev/<unidad>

```

o, si se va a eliminar una partición particular de una unidad:

```
# mdadm --misc --zero-superblock /dev/<partición>

```

**Nota:**

*   Hacer limpieza de un superbloque de partición no debe afectar a las otras particiones en el disco.
*   Debido a la naturaleza de la funcionalidad RAID, es muy difícil realizar un [borrado con seguridad del disco](/index.php/Securely_wipe_disk "Securely wipe disk") completo en una matriz en funcionamiento. Considere si es útil hacerlo antes de crearla.

### Particionar los dispositivos

Es recomendable particionar los discos que se utilizarán en la matriz. Como la mayoría de los usuarios RAID seleccionan discos duros de >2 TB, es preferible y recomendable utilizar tablas de particionado GPT. Consulte [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") para obtener más información sobre la partición y las [[[Partitioning (Español)#Herramientas de particionado]] disposibles.

**Nota:** también es posible crear un RAID directamente en los discos sin formato (sin particiones), pero no se recomienda porque puede causar problemas al intercambiar un disco fallido.

**Sugerencia:** al reemplazar un disco fallido de un RAID, el nuevo disco debe ser exactamente del mismo tamaño que el disco fallido o más grande; de lo contrario, el proceso de recreación de matriz no funcionará. Incluso los discos duros del mismo fabricante y modelo pueden tener pequeñas diferencias de tamaño. Al dejar un poco de espacio sin asignar al final del disco, se pueden compensar las diferencias de tamaño entre las unidades, lo que facilita la elección de un modelo de unidad de reemplazo. Por lo tanto, es una buena práctica dejar aproximadamente 100 MiB de espacio no asignado al final del disco.

#### Tabla de particiones GUID

*   Después de crear las particiones, su [GUID de tipo de partición](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") debe ser `A19D880F-05FC-4D3B-A006-743F0F84911E` (puede asignarse seleccionando el tipo de partición `Linux RAID` en *fdisk* o `FD00` en *gdisk*).
*   Si se emplea una matriz de discos más grande, considere asignar [etiquetas de sistemas de archivos](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-label "Persistent block device naming (Español)") o [etiquetas de particiones](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol)#by-partlabel "Persistent block device naming (Español)") para que sea más fácil identificar un disco individual más tarde.
*   Se recomienda crear particiones que sean del mismo tamaño en cada uno de los dispositivos.

#### Master Boot Record

Para aquellos que creen particiones en discos duros con una tabla de particiones MBR, los [ID de tipos de particiones](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") disponibles para su uso son:

*   `0xFD` para matrices raid autodetectadas (`Linux raid autodetect` en *fdisk*)
*   `0xDA` para datos sin sistema de archivos (`Non-FS data` en *fdisk*)

Consulte [Linux Raid Wiki:Partition Types](https://raid.wiki.kernel.org/index.php/Partition_Types) para obtener más información.

### Compilar la matriz

Utilice `mdadm` para compilar la matriz. Varios ejemplos se dan a continuación.

**Advertencia:** no basta con copiar/pegar los ejemplos siguientes; sustituya las opciones/letras correctas de la unidad.

**Nota:**

*   Si se trata de una matriz RAID 1 que se pretende arrancar desde [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)") una limitación en la v4.07 de syslinux requiere que el valor de los metadatos se ajuste a 1.0 en lugar de la opción predeterminada de 1.2.
*   Al crear una matriz desde un [medio de instalación de Arch](/index.php/Archiso_(Espa%C3%B1ol) "Archiso (Español)") utilice la opción `--homehost=*myhostname*` (o `--homehost=any` para tener siempre el mismo nombre independientemente del equipo) para establecer el [nombre del equipo](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)"), de lo contrario, el nombre del host `archiso` se escribirá en los metadatos de la matriz.

**Sugerencia:** puede especificar un nombre de dispositivo de raid personalizado utilizando la opción `--name=*MyRAIDName*` o configurando la ruta del dispositivo de raid en `/dev/md/*MyRAIDName*`. Udev creará enlaces simbólicos a las matrices de raid en `/dev/md/` usando ese nombre. Si `homehost` coincide con el [nombre del equipo](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)") actual (o si homehost está configurado como `any`) el enlace será `/dev/md/*name*`, si el nombre de host no coincide con él, el enlace será `/dev/md/*homehost*:*name*`.

El siguiente ejemplo muestra la compilación de una matriz RAID 1 en el dispositivo 2:

```
# mdadm --create --verbose --level=1 --metadata=1.2 --raid-devices=2 /dev/md/MyRAID1Array /dev/sdb1 /dev/sdc1

```

El siguiente ejemplo muestra la compilación de una matriz RAID 5 con 4 dispositivos activos y 1 dispositivo de repuesto:

```
# mdadm --create --verbose --level=5 --metadata=1.2 --chunk=256 --raid-devices=4 /dev/md/MyRAID5Array /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1 --spare-devices=1 /dev/sdf1

```

**Sugerencia:** `--chunk` se usa para cambiar el valor predeterminado del tamaño del fragmento. Consulte [Chunks: la clave oculta para el rendimiento RAID](http://www.zdnet.com/article/chunks-the-hidden-key-to-raid-performance/) para obtener más información sobre la optimización del tamaño del fragmento.

El siguiente ejemplo muestra la construcción de una matriz RAID10,far2 con 2 dispositivos:

```
# mdadm --create --verbose --level=10 --metadata=1.2 --chunk=512 --raid-devices=2 --layout=f2 /dev/md/MyRAID10Array /dev/sdb1 /dev/sdc1

```

La matriz se crea en el dispositivo virtual `/dev/mdX`, ensamblada y lista para usar (en modo degradado). Se puede comenzar a usarla directamente al tiempo que mdadm resincroniza la matriz en segundo plano. Restaurar la paridad puede llevar mucho tiempo. Verifique el progreso con:

```
$ cat /proc/mdstat

```

### Actualizar archivo de configuración

Por defecto, la mayoría de `mdadm.conf` está comentada y contiene solo lo siguiente:

 `/etc/mdadm.conf` 
```
...
DEVICE partitions
...

```

Esta directiva le dice a mdadm que examine los dispositivos a los que hace referencia `/proc/partitions` y que ensamble tantas matrices como sea posible. Esto está bien si realmente desea iniciar todos las matrices disponibles y está seguro de que no se encontrarán superbloques inesperados (como después de instalar un nuevo dispositivo de almacenamiento). Un enfoque más preciso es agregar explícitamente las matrices a `/etc/mdadm.conf`:

```
# mdadm --detail --scan >> /etc/mdadm.conf

```

Esto resulta en algo como lo siguiente:

 `/etc/mdadm.conf` 
```
...
DEVICE partitions
...
ARRAY /dev/md/MyRAID1Array metadata=1.2 name=pine:MyRAID1Array UUID=27664f0d:111e493d:4d810213:9f291abe
```

Esto también hace que mdadm examine los dispositivos a los que hace referencia `/proc/partitions`. Sin embargo, solo los dispositivos que tienen superbloques con un UUID de `27664…` se ensamblan en matrices activas.

Consulte [mdadm.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mdadm.conf.5) para obtener más información.

### Ensamblar la matriz

Una vez que el archivo de configuración se ha actualizado, la matriz puede ser ensamblada usando mdadm:

```
# mdadm --assemble --scan

```

### Formatear RAID con un sistema de archivos

La matriz ahora se puede formatear con un sistema de archivos como cualquier otro disco, basta tener en cuenta que:

*   debido al gran tamaño del volumen, no todos los sistemas de archivos son adecuados (ver: [limitaciones de los sistema de archivos](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Limits "wikipedia:Comparison of file systems"));
*   el sistema de archivos debe apoyar su aumento y reducción mientras se está en línea (ver: [características de los sistemas de archivos](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Features "wikipedia:Comparison of file systems"));
*   se debe calcular el «stride» y «stripe-width» correctos para un rendimiento óptimo.

#### Calcular el stride y stripe-width

Se requieren dos parámetros para optimizar la estructura del sistema de archivos para que se ajuste de manera óptima dentro de la estructura RAID subyacente: el *«stride»* y *«stripe-width»*. Estos se derivan del *tamaño del fragmento* («*chunk*») de RAID , el *tamaño del bloque* del sistema de archivos, y el *número de «discos de datos»*.

El tamaño del fragmento (chunk) es una propiedad de la matriz RAID, decidida en el momento de su creación. El valor predeterminado actual de `mdadm` es 512 KiB. Se puede encontrar con `mdadm`:

```
# mdadm --detail /dev/mdX | grep 'tamaño del fragmento (chunk)'

```

El tamaño del bloque es una propiedad del sistema de archivos, decidido en *su* creación. El valor predeterminado para muchos sistemas de archivos, incluido ext4, es 4 KiB. Consulte `/etc/mke2fs.conf` para obtener detalles sobre ext4.

El número de «discos de datos» es el número mínimo de dispositivos necesarios en la matriz para reconstruirlo completamente sin pérdida de datos. Por ejemplo, este es N para una matriz raid0 de N dispositivos y N-1 para raid5.

Una vez que tenga estas tres cantidades, el «stride» y el «stripe-width» se pueden calcular utilizando las siguientes fórmulas:

```
stride = tamaño del fragmento / tamaño del bloque
stripe width = número de discos físicos de datos * stride

```

##### Ejemplo 1\. RAID0

Ejemplo formateando con sistema de archivos ext4 con «stride» y «stripe-width» correctas:

*   Hipotética matriz RAID0 que se compone de 2 discos físicos.
*   El tamaño del fragmento es 64 KiB.
*   El tamaño del bloque es 4 KiB.

Stride = (tamaño fragmento (chunk)/tamaño bloque). En este ejemplo, la matemática es (64/4) por lo que stride = 16.

Stripe-width = (número de discos físicos de **datos** * stride). En este ejemplo, la matemática es (2*16) por lo que stripe-width = 32.

```
# mkfs.ext4 -v -L myarray -m 0.5 -b 4096 -E stride=16,stripe-width=32 /dev/md0

```

##### Ejemplo 2\. RAID5

Ejemplo formateando con sistema de archivos ext4 con «stride» y «stripe-width» correctas:

*   Hipotética matriz RAID5 que se compone de 4 discos físicos; 3 discos de datos y 1 disco de paridad.
*   El tamaño fragmento (chunk) es 512 KiB.
*   El tamaño de bloque es 4 KiB.

Stride = (tamaño fragmento (chunk)/tamaño de bloque). En este ejemplo, la matemática es (256/4) por lo que stride = 64.

Stripe-width = (número de discos físicos de **datos** * stride). En este ejemplo, la matemática es (3*128) de modo que stripe-width = 384.

```
# mkfs.ext4 -v -L myarray -m 0.01 -b 4096 -E stride=128,stripe-width=384 /dev/md0

```

Para más información sobre «stride» y stripe-width, ver: [Matemáticas RAID](http://wiki.centos.org/HowTos/Disk_Optimization).

**Nota:** **[del traductor]**

*   `Stride`: es el número de posicionamiento en la memoria entre los comienzos de uno y otro de los sucesivos elementos de la matriz, se puede traducir por «banda», «tira» o «zancada».
*   `Stride-width`: es el tamaño o ancho de la zancada.
*   `[Chunk](https://en.wikipedia.org/wiki/es:Chunk "wikipedia:es:Chunk")`: es la masa «atómica» más pequeña de datos que puede ser escrita en los dispositivos, lo podríamos traducir por «porción», «trozo» o «fragmento».

##### Example 3\. RAID10,far2

Ejemplo de formato a ext4 con el «stripe-width» y «stride» correctos:

*   La matriz hipotética RAID10 se compone de 2 discos físicos. Debido a las propiedades de RAID10 con el diseño far2, ambos cuentan como discos de datos.
*   El tamaño del fragmento es de 512 KiB.

 `# mdadm --detail /dev/md0 | grep 'Chunk Size'` 
```
    Chunk Size : 512K

```

*   El tamaño del bloque es de 4 KiB.

stride = tamaño de fragmento / tamaño de bloque. En este ejemplo, la matemática es 512/4, por lo que stride = 128.

stripe width = número de discos físicos de **datos** * stride. En este ejemplo, la matemática es 2*128, por lo que el «stripe-width» = 256.

```
# mkfs.ext4 -v -L myarray -m 0.01 -b 4096 -E stride=128,stripe-width=256 /dev/md0

```

## Montar desde un CD live

Los usuarios que quieran montar la partición RAID desde un CD live, escriban:

```
# mdadm --assemble /dev/md<number> /dev/<disk1> /dev/<disk2> /dev/<disk3> /dev/<disk4>

```

Si su RAID 1, al que le falta una matriz de discos, se autodetectó erróneamente como RAID 1 (según `mdadm --detail /dev/md<number>`) y se informó como inactivo (según `cat /proc/mdstat`), detenga primero la matriz:

```
# mdadm --stop /dev/md<number>

```

## Instalar Arch Linux en RAID

**Nota:** la siguiente sección se aplica solo si el sistema de archivos raíz reside en la matriz. Los usuarios pueden saltarse esta sección si la matriz contiene una partición(s) de datos.

Se debe crear la matriz RAID entre los pasos de [particionar](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") y [formatear](/index.php/File_systems_(Espa%C3%B1ol)#Crear_un_sistema_de_archivos "File systems (Español)") del proceso de instalación. En lugar de formatear directamente una partición para que sea su sistema de archivos raíz, ello se hará sobre la matriz RAID. Siga la sección [#Instalación](#Instalación) para crear la matriz RAID. Luego, continúe con el procedimiento de instalación hasta que se complete el paso pacstrap. Al usar [arranque UEFI](/index.php/Unified_Extensible_Firmware_Interface_(Espa%C3%B1ol) "Unified Extensible Firmware Interface (Español)"), consulte también [EFI system partition (Español)#Partición ESP sobre RAID](/index.php/EFI_system_partition_(Espa%C3%B1ol)#Partición_ESP_sobre_RAID "EFI system partition (Español)").

### Actualizar archivo de configuración

**Nota:** esto debe hacerse fuera de chroot, de ahí el prefijo /mnt en la ruta de archivo.

Después de que el sistema base se haya instalado, el archivo de configuración por defecto, `mdadm.conf`, debe ser actualizado, así:

```
# mdadm --detail --scan >> /mnt/etc/mdadm.conf

```

**Nota:** para evitar el fallo de `mdmonitor.service` en el arranque (activado de forma predeterminada), deberá descomentar `MAILADDR` y proporcionar una dirección de correo electrónico y/o aplicación para manejar notificación de problemas con su matriz en en la parte de abajo del archivo `mdadm.conf`. Vea [#Mailing on events](#Mailing_on_events).

Continuar con el proceso de instalación hasta que llegue al paso [crear un entorno inicial ramdisk](/index.php/Installation_guide_(Espa%C3%B1ol)#Initramfs "Installation guide (Español)") y, a continuación, siga en sección siguiente.

### Configurar mkinitcpio

**Nota:** esto debe hacerse en entorno chroot.

Añada `mdadm_udev` a la sección [HOOKS](/index.php/Mkinitcpio_(Espa%C3%B1ol)#HOOKS "Mkinitcpio (Español)") de `mkinitcpio.conf` para añadir soporte para mdadm directamente en la imagen initramfs inicial:

 `/etc/mkinitcpio.conf` 
```
...
 HOOKS=(base udev autodetect keyboard modconf block **mdadm_udev** filesystems fsck)
...
```

Si usa el hook `mdadm_udev` con una matriz FakeRAID, se recomienda incluir *mdmon* en la matriz [BINARIES](/index.php/Mkinitcpio_(Espa%C3%B1ol)#BINARIOS_y_ARCHIVOS "Mkinitcpio (Español)"):

 `/etc/mkinitcpio.conf` 
```
...
BINARIES=(**mdmon**)
...
```

Después [regenere la imagen initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)").

Véase también [mkinitcpio (Español)#Utilizar RAID](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Utilizar_RAID "Mkinitcpio (Español)").

### Configurar el gestor de arranque

Apunte el parámetro `root` al dispositivo asignado. Por ejemplo:

```
root=/dev/md/*MyRAIDArray*

```

Si el arranque desde una partición RAID por software falla usando el método anterior de nodo de dispositivo del kernel, una forma alternativa es usar uno de los métodos de [Persistent block device naming (Español)](/index.php/Persistent_block_device_naming_(Espa%C3%B1ol) "Persistent block device naming (Español)"), por ejemplo:

```
root=LABEL=Root_Label

```

Véase también [GRUB (Español)#RAID](/index.php/GRUB_(Espa%C3%B1ol)#RAID "GRUB (Español)").

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

**Nota:** si se reinicia el sistema después que una depuración parcial haya sido suspendida, la depuración comenzará de nuevo.

Cuando la depuración se ha completado, los administradores pueden comprobar cuántos bloques (si los hay) se han marcado como erróneos:

```
# cat /sys/block/md0/md/mismatch_cnt

```

#### Notas generales sobre la depuración

**Nota:** los usuarios pueden alternativamente aplicar echo **repair** a `/sys/block/md0/md/sync_action`, pero esto es poco aconsejable, ya que si se encuentra una falta de coincidencia en los datos, se actualizará automáticamente para mantener la coherencia. El peligro es que realmente no sabemos si se trata de una falta de paridad o el bloque de datos es correcto (o cuál bloque de datos en caso de RAID1). Es una cuestión de azar si la operación recibe los datos correctos en lugar de los datos erróneos.

Es una buena idea configurar un trabajo cron como root para programar una limpieza periódica. Vea [raid-check](https://aur.archlinux.org/packages/raid-check/) que puede ayudar con esto. Para realizar una limpieza periódica utilizando temporizadores systemd en lugar de cron. Consulte [raid-check-systemd](https://aur.archlinux.org/packages/raid-check-systemd/) que contiene el mismo script junto con los archivos de unidad de temporizador systemd asociados.

**Nota:** para las unidades de disco típicas, la limpieza puede tomar aproximadamente **seis segundos por gigabyte** (es decir, una hora cuarenta y cinco minutos por terabyte), así que planifique el inicio de su trabajo cron o temporizador adecuadamente.

#### Notas sobre la depuración de RAID1 y RAID10

Debido al hecho de que RAID1 y RAID10 escriben en el kernel sin búfer, una matriz puede tener cuentas desajustadas sin 0 incluso cuando la matriz es saludable. Estos recuentos sin 0 solo existirán en áreas de datos transitorios en los que no suponen un problema. Sin embargo, no podemos discernir la diferencia entre una cuenta sin 0 respecto de datos transitorios, con un recuento sin 0 que signifique un verdadero problema. Este hecho es una fuente de falsos positivos en matrices RAID1 y RAID10\. Sin embargo, a pesar de ello se recomienda realizar depuraciones regularmente con el fin de detectar y corregir los sectores erróneos que pueden estar presentes en los dispositivos.

### Extracción de dispositivos de una matriz

Se puede eliminar un dispositivo de la matriz después de marcarlo como defectuoso:

```
# mdadm --fail /dev/md0 /dev/sdxx

```

Ahora quítelo de la matriz:

```
# mdadm -r /dev/md0 /dev/sdxx

```

Retire el dispositivo de forma permanente (por ejemplo, para utilizarlo de forma individual a partir de ahora). Emita las dos órdenes descritas anteriormente, y luego:

```
# mdadm --zero-superblock /dev/sdxx

```

**Advertencia:**

*   ¡No emita esta orden en matrices lineales o RAID0 o se producirán pérdidas de datos!
*   La reutilización del disco eliminado sin poner a cero el superbloque provocará la pérdida de todos los datos en el próximo arranque. (Después de que mdadm intentará usarlo como parte de la matriz de raid).

Para dejar de usar una matriz:

1.  desmontar la matriz de destino;
2.  detener la matriz con: `mdadm --stop /dev/md0`;
3.  repetir las tres órdenes descritas al principio de esta sección en cada dispositivo;
4.  quitar la línea correspondiente de `/etc/mdadm.conf`.

### Adición de un nuevo dispositivo a una matriz

La adición de nuevos dispositivos con mdadm se puede hacer en un sistema en funcionamiento con los dispositivos montados. Particione el nuevo dispositivo usando el mismo diseño de uno de los que ya están en la matriz, como se mencionó anteriormente.

Ensamble la matriz RAID si no está ya ensamblada:

```
# mdadm --assemble /dev/md0 /dev/sda1 /dev/sdb1

```

Añada el nuevo dispositivo de la matriz:

```
# mdadm --add /dev/md0 /dev/sdc1

```

Esto no debería tomar mucho tiempo para que mdadm lo haga.

Dependiendo del tipo de RAID (por ejemplo, con RAID1), mdadm puede agregar el dispositivo como repuesto sin sincronizar los datos. Puede aumentar la cantidad de discos que utiliza RAID utilizando `--grow` con la opción `--raid-devices`. Por ejemplo, para aumentar una matriz a cuatro discos:

```
# mdadm --grow /dev/md0 --raid-devices=4

```

Esto no debe llevarle mucho tiempo a mdadm. Una vez más, compruebe el progreso con:

```
# cat /proc/mdstat

```

Compruebe que el dispositivo se ha añadido, con la orden:

```
# mdadm --misc --detail /dev/md0

```

**Note:** For RAID0 arrays you may get the following error message:
```
mdadm: add new device failed for /dev/sdc1 as 2: Invalid argument

```

Esto se debe a que los comandos anteriores agregarán el nuevo disco como «repuesto» pero RAID0 no tiene repuestos. Si desea agregar un dispositivo a una matriz RAID0, debe «agrandar» y «añadirß en la misma orden, como se muestra a continuación:

```
# mdadm --grow /dev/md0 --raid-devices=3 --add /dev/sdc1

```

### Incrementar tamaño de un volumen RAID

Si se instalan discos más grandes en una matriz RAID o se ha aumentado el tamaño de la partición, puede ser conveniente aumentar el tamaño del volumen RAID para llenar el espacio más grande disponible. Este proceso puede comenzar siguiendo primero las secciones anteriores relacionadas con el reemplazo de discos. Una vez que el volumen RAID se ha reconstruido en los discos más grandes, debe «agrandar» para llenar el espacio.

```
# mdadm --grow /dev/md0 --size=max

```

A continuación, las particiones presentes en el volumen RAID `/dev/md0` puede que necesiten ser redimensionadas. Consulte [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") para más detalles. Finalmente, será necesario cambiar el tamaño del sistema de archivos en la partición mencionada anteriormente. Si la partición se realizó con `gparted`, esto se hará automáticamente. Si se utilizaron otras herramientas, desmonte y cambie el tamaño del sistema de archivos manualmente.

```
# umount /storage
# fsck.ext4 -f /dev/md0p1
# resize2fs /dev/md0p1

```

### Cambiar los límites de velocidad de sincronización

La sincronización puede llevar un tiempo. Si la máquina no es necesaria para otras tareas, se puede aumentar el límite de velocidad.

 `# cat /proc/mdstat` 
```
 Personalities : [raid1]
 md0 : active raid1 sda3[2] sdb3[1]
       155042219 blocks super 1.2 [2/1] [_U]
       [>....................]  recovery =  0.0% (77696/155042219) finish=265.8min speed=9712K/sec

 unused devices: <none>

```

Verifique el límite de velocidad actual.

 `# cat /proc/sys/dev/raid/speed_limit_min` 
```
1000

```
 `# cat /proc/sys/dev/raid/speed_limit_max` 
```
200000

```

Aumente los límites.

```
# echo 400000 >/proc/sys/dev/raid/speed_limit_min
# echo 400000 >/proc/sys/dev/raid/speed_limit_max

```

Luego revise la velocidad de sincronización y el tiempo estimado de finalización.

 `# cat /proc/mdstat` 
```
 Personalities : [raid1]
 md0 : active raid1 sda3[2] sdb3[1]
       155042219 blocks super 1.2 [2/1] [_U]
       [>....................]  recovery =  1.3% (2136640/155042219) finish=158.2min speed=16102K/sec

 unused devices: <none>

```

Véase también [sysctl#MDADM](/index.php/Sysctl#MDADM "Sysctl").

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

```
# watch -t 'cat /proc/mdstat'

```

O preferiblemente usando [tmux](https://www.archlinux.org/packages/?name=tmux)

```
# tmux split-window -l 12 "watch -t 'cat /proc/mdstat'"

```

### Seguimiento Entrada/Salida con iotop

El paquete [iotop](https://www.archlinux.org/packages/?name=iotop) muestra las estadísticas de entrada/salida para los procesos. Utilice esta orden para ver la Entrada/Salida para los hilos de raid.

```
# iotop -a -p $(sed 's, , -p ,g' <<<`pgrep "_raid|_resync|jbd2"`)

```

### Seguimiento Entrada/Salida con iostat

La utilidad *iostat* del paquete [sysstat](https://www.archlinux.org/packages/?name=sysstat) muestra las estadísticas de entrada/salida para los dispositivos y las particiones.

```
 iostat -dmy 1 /dev/md0
 iostat -dmy 1 # todo

```

### Correos sobre eventos

Un servidor de correo SMTP (sendmail) o al menos un agente de correo electrónico (ssmtp/msmtp) es necesario para lograr esto. Tal vez la solución más simple es utilizar [dma](https://aur.archlinux.org/packages/dma/) que es muy pequeño (instala 0,08 MiB) y no requiere instalación.

Editar `/etc/mdadm.conf` para definir la dirección de correo electrónico en la que se recibirán notificaciones.

**Nota:** si utiliza dma como se mencionó anteriormente, los usuarios pueden simplemente enviar correos directamente al nombre de usuario en el equipo local, en lugar de a una dirección de correo electrónico externo.

Para probar la configuración:

```
# mdadm --monitor --scan --oneshot --test

```

mdadm incluye un servicio de systemd `mdmonitor.service` para llevar a cabo la tarea de control, por lo que en este punto, no tiene nada más que hacer. Si no configura un correo electrónico en `/etc/mdadm.conf`, dicho servicio fallará. Si no desea recibir correos sobre eventos mdadm, el fallo puede ser ignorado; si no desea recibir las notificaciones ni los mensajes acerca del error, puede [enmascarar](/index.php/Mask "Mask") la unidad.

#### Método alternativo

Para evitar la instalación de un servidor de correo SMTP o un expedidor de correo electrónico, puede utilizar la herramienta [S-nail](/index.php/S-nail "S-nail") (no se olvide de configurarla) ya presente en el sistema.

Cree un archivo llamado `/etc/mdadm_warning.sh` con:

 `/etc/mdadm_warning.sh` 
```
#!/bin/bash
event=$1
device=$2

echo " " | /usr/bin/mailx -s "$event on $device" '''destination@email.com'''

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

Cuando se inicia una matriz md, el superbloque será escrito, y puede iniciarse la resincronización. Para comenzar en solo lectura, establecer el módulo del kernel `md_mod` con el parámetro `start_ro`. Cuando se establece, las nuevas matrices vendrán activadas un modo «auto-ro», que desactiva todas las entradas/salidas internas (actualizaciones de superbloque, resincronización, recuperación) y se pone automáticamente en «rw» cuando llega la primera solicitud de escritura.

**Nota:** la matriz se puede establecer en modo «ro» usando `mdadm --readonly` antes que venga la primera solicitud de escritura, o se puede iniciar la resincronización sin una solicitud de escritura mediante `mdadm --readwrite`.

Para establecer el parámetro en el arranque, añadir `md_mod.start_ro=1` a la línea del kernel.

O establezca el parámetro al tiempo de cargar el módulo desde el archivo `/etc/modprobe.d/` o directamente desde `/sys/`:

```
# echo 1 > /sys/module/md_mod/parameters/start_ro

```

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

[Tiobench](http://sourceforge.net/projects/tiobench/) es un programa que mide las mejoras de rendimiento mediante la medición completa de Entrada/Salida de los hilos del disco.

[bonnie++](https://www.archlinux.org/packages/?name=bonnie%2B%2B) analiza el tipo de acceso a la base de datos para uno o más archivos, y la creación, lectura y borrado de archivos pequeños que puede simular el uso de programas como Squid, INN, o el formato de e-mail Maildir. El programa [ZCAV](http://www.coker.com.au/bonnie++/zcav/) pone a prueba el rendimiento de diferentes zonas de un disco duro sin necesidad de escribir ningún dato en el disco.

`hdparm` **NO** debería ser utilizado para comparar un RAID, ya que proporciona resultados muy inconsistentes.

## Véase también

*   [Linux Software RAID](https://www.thomas-krenn.com/en/wiki/Linux_Software_RAID) (thomas-krenn.com)
*   [Linux RAID wiki entry](http://raid.wiki.kernel.org/index.php/Linux_Raid) on The Linux Kernel Archives
*   [How Bitmaps Work](https://raid.wiki.kernel.org/index.php/Write-intent_bitmap)
*   [Chapter 15: Redundant Array of Independent Disks (RAID)](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-raid.html) of Red Hat Enterprise Linux 6 Documentation
*   [Linux-RAID FAQ](http://tldp.org/FAQ/Linux-RAID-FAQ/x37.html) on the Linux Documentation Project
*   [Introduction to RAID](http://www.linux-mag.com/id/7924/), [Nested-RAID: RAID-5 and RAID-6 Based Configurations](http://www.linux-mag.com/id/7931/), [Intro to Nested-RAID: RAID-01 and RAID-10](http://www.linux-mag.com/id/7928/), and [Nested-RAID: The Triple Lindy](http://www.linux-mag.com/id/7932/) in Linux Magazine
*   [HowTo: Speed Up Linux Software Raid Building And Re-syncing](http://www.cyberciti.biz/tips/linux-raid-increase-resync-rebuild-speed.html)
*   [RAID5-Server to hold all your data](http://fomori.org/blog/?p=94)
*   [Wikipedia:Non-RAID drive architectures](https://en.wikipedia.org/wiki/Non-RAID_drive_architectures "wikipedia:Non-RAID drive architectures")

**mdadm**

*   [mdadm source code](http://www.kernel.org/pub/linux/utils/raid/mdadm/)
*   [Software RAID on Linux with mdadm](http://www.linux-mag.com/id/7939/) in Linux Magazine
*   [Wikipedia - mdadm](https://en.wikipedia.org/wiki/mdadm "wikipedia:mdadm")

**Hilos del foro**

*   [Raid Performance Improvements with bitmaps](http://forums.overclockers.com.au/showthread.php?t=865333)
*   [GRUB and GRUB2](https://bbs.archlinux.org/viewtopic.php?id=125445)
*   [Can't install grub2 on software RAID](https://bbs.archlinux.org/viewtopic.php?id=123698)
*   [Use RAID metadata 1.2 in boot and root partition](http://forums.gentoo.org/viewtopic-t-888624-start-0.html)

**RAID con encriptación**

*   [Linux/Fedora: Encrypt /home and swap over RAID with dm-crypt](http://www.shimari.com/dm-crypt-on-raid/) by Justin Wells