**[dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")**

* * *

<a class="mw-selflink selflink">Preparar dispositivo</a> – [Cifrar dispositivo](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol) "Dm-crypt/Device encryption (Español)") – [Cifrar sistema de archivos no root](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting a non-root file system (Español)") – [Cifrar un sistema completo](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)") – [Cifrar espacio de intercambio](/index.php/Dm-crypt/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt/Swap encryption (Español)") – [Montar y acceder a /home cifrado](/index.php/Dm-crypt/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt/Mounting at login (Español)") – [Configurar el sistema](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol) "Dm-crypt/System configuration (Español)") – [Especialidades](/index.php/Dm-crypt/Specialties_(Espa%C3%B1ol) "Dm-crypt/Specialties (Español)")

**Estado de la traducción**
Este artículo es una traducción de [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"), revisada por última vez el **2018-10-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt/Drive_preparation&diff=0&oldid=519186) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Disk encryption (Español)#Preparar el disco](/index.php/Disk_encryption_(Espa%C3%B1ol)#Preparar_el_disco "Disk encryption (Español)")
*   [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk")

Antes de cifrar una unidad, es recomendable realizar un borrado seguro del disco, sobrescribiendo toda la unidad con datos aleatorios. Para evitar ataques criptográficos o [recuperación de archivos](/index.php/File_recovery "File recovery") no deseados, lo ideal es que estos datos sean indistinguibles de los datos escritos posteriormente por dm-crypt. Para comprender mejor el tema vea [Disk encryption (Español)#Preparar el disco](/index.php/Disk_encryption_(Espa%C3%B1ol)#Preparar_el_disco "Disk encryption (Español)").

## Contents

*   [1 Borrar de forma segura la unidad de disco duro](#Borrar_de_forma_segura_la_unidad_de_disco_duro)
    *   [1.1 Métodos genéricos](#Métodos_genéricos)
    *   [1.2 Métodos específicos de dm-crypt](#Métodos_específicos_de_dm-crypt)
        *   [1.2.1 Limpiar un disco o partición vacíos con dm-crypt](#Limpiar_un_disco_o_partición_vacíos_con_dm-crypt)
        *   [1.2.2 Limpiar espacio libre con dm-crypt después de la instalación](#Limpiar_espacio_libre_con_dm-crypt_después_de_la_instalación)
        *   [1.2.3 Limpiar el encabezado LUKS](#Limpiar_el_encabezado_LUKS)
*   [2 Particionar](#Particionar)
    *   [2.1 Particiones físicas](#Particiones_físicas)
    *   [2.2 Dispositivos de bloques apilados](#Dispositivos_de_bloques_apilados)
    *   [2.3 Subvolúmenes Btrfs](#Subvolúmenes_Btrfs)
    *   [2.4 Partición de arranque (GRUB)](#Partición_de_arranque_(GRUB))

## Borrar de forma segura la unidad de disco duro

Al decidir qué método utilizar para el borrado seguro de una unidad de disco duro, recuerde que esto solo se debe realizar una vez antes de que la unidad sea utilizada como una unidad cifrada.

**Advertencia:** haga copias de seguridad apropiadas de aquellos datos importantes antes de comenzar.

**Nota:** cuando se trate de limpiar gran cantidad de datos, el proceso tardará varias horas o varios días en completarse.

**Sugerencia:**

*   El proceso de llenado de una unidad cifrada puede tomar más de un día para completarse en un disco de varios terabytes. Para no dejar la máquina inutilizable durante la operación, puede valer la pena hacerlo desde un sistema ya instalado en otra unidad, en lugar de hacerlo desde el sistema de instalación *live* de Arch.
*   Para discos [SSD](/index.php/SSD "SSD"), a fin de rentabilizar la operación y minimizar los residuos de caché de la [memoria flash](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk"), considere realizar [un borrado de las celdas de la memoria SSD](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") *antes* de seguir las instrucciones siguientes.

### Métodos genéricos

Para obtener instrucciones detalladas sobre cómo borrar y preparar una unidad, consulte [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk").

### Métodos específicos de dm-crypt

Los dos métodos siguientes son específicos para dm-crypt y se mencionan porque son muy rápidos y se pueden realizar después de configurar la partición también.

Las [FAQ de cryptsetup](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) (elemento 2.19 «*¿Cómo puedo limpiar un dispositivo con aleatoriedad criptográfica?*») mencionan un procedimiento muy sencillo para usar en un volumen existente de dm-crypt para limpiar todo el espacio libre accesible en el bloque subyacente del dispositivo con datos aleatorios al actuar como un simple generador de números pseudoaleatorios. También se afirma que protege contra la divulgación de patrones de uso. Esto se debe a que los datos cifrados son prácticamente indistinguibles de los aleatorios.

#### Limpiar un disco o partición vacíos con dm-crypt

En primer lugar, cree un contenedor temporal cifrado en la partición (`sdXY`) o en el disco completo (`sdX`), que va a ser cifrado:

```
# cryptsetup open --type plain -d /dev/urandom /dev/<dispositivo_de_bloque> para_ser_borrado

```

En segundo lugar, compruebe que existe:

 `# lsblk` 
```
NAME                 MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
sda                    8:0    0  1.8T  0 disk
└─para_ser_borrado   252:0    0  1.8T  0 crypt

```

Limpie el contenedor con ceros. Un uso de `if=/dev/urandom` no es necesario ya que el cifrado de encriptación se utiliza para enfarruyar.

 `# dd if=/dev/zero of=/dev/mapper/para_ser_borrado status=progress`  `dd: writing to ‘/dev/mapper/para_ser_borrado’: No space left on device` 
**Sugerencia:**

*   La utilización de *dd* con la opción `bs=`, por ejemplo `bs=1M`, se utiliza con frecuencia para aumentar el rendimiento del disco de la operación.
*   Para realizar una comprobación de la operación, llene de ceros la partición antes de crear el contenedor de limpieza. Después se puede usar la orden de borrado `blockdev --getsize64 */dev/mapper/container*` para obtener el tamaño exacto del contenedor como root. Ahora se puede usar 'od' para ver como el borrado sobrescribe los sectores puestos a cero, por ejemplo `od -j *containersize - blocksize*` para ver el borrado completo hasta el final.

Finalmente, cierre el contenedor temporal:

```
# cryptsetup close para_ser_borrado

```

Al cifrar un sistema completo, el siguiente paso es [#Particionar](#Particionar). Si acaba de cifrar una partición, continúe en [Dm-crypt/Encrypting a non-root file system (Español)#Partición](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol)#Partición "Dm-crypt/Encrypting a non-root file system (Español)").

#### Limpiar espacio libre con dm-crypt después de la instalación

Los usuarios que no tuvieron tiempo para realizar el borrado antes de la [instalación](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)"), pueden lograr un efecto similar una vez que se arranque el sistema cifrado y se monten los sistemas de archivos. Sin embargo, considere la posibilidad de que el sistema de archivos afectado haya establecido un espacio reservado, por ejemplo para el usuario root u otro mecanismo de [cuota de disco](/index.php/Disk_quota "Disk quota"), que puede limitar el borrado, incluso cuando se realiza por el usuario root: en esos casos, es posible que algunas partes del dispositivo de bloque subyacente no se escriban en absoluto.

Para ejecutar el borrado, llene temporalmente el espacio libre restante de la partición escribiendo en un archivo presente en el contenedor cifrado:

 `# dd if=/dev/zero of=/archivo/en/contenedor status=progress`  `dd: writing to ‘/archivo/en/contenedor’: No space left on device` 

Sincronice el caché del disco y luego elimine el archivo para reclamar el espacio libre.

```
# sync
# rm /archivo/en/contenedor

```

El proceso anterior debe repetirse para cada partición creada y su sistema de archivos de cada dispositivo de bloque. Por ejemplo, la instalación de [LVM sobre LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#LVM_sobre_LUKS "Dm-crypt/Encrypting an entire system (Español)"), el proceso debe realizarse para cada volumen lógico.

#### Limpiar el encabezado LUKS

Las particiones formateadas con dm-crypt/LUKS contienen un encabezado con las opciones de cifrado y claves utilizadas, al que se remite `dm-mod` al abrir el dispositivo de bloque. Después del encabezado comienza la aleatoriedad real de los datos de la partición. Por lo tanto, al reinstalar en una unidad ya cifrada, o desarmar una (por ejemplo, la venta de PC, el cambio de unidades, etc.) «puede» ser suficiente limpiar el encabezado de la partición, en lugar de sobrescribir la unidad entera, que puede ser un proceso largo.

Al borrar el encabezado LUKS se borrará la clave maestra cifrada PBKDF2 (AES), las [sal](https://en.wikipedia.org/wiki/es:Sal "wikipedia:es:Sal"), y así sucesivamente.

**Nota:** es importante escribir en la partición cifrada con LUKS (`/dev/sda**1**` en este ejemplo) y no directamente a los nodos de las particiones del disco. Configuraciones con cifrado como una capa de asignación de dispositivos encima de otras, por ejemplo LVM sobre LUKS sobre RAID debería escribir en RAID, respectivamente.

En un encabezado con un único valor predeterminado de 256 bits, el tamaño de la clave ocupa 1024 KB. Se aconseja también sobrescribir los primeros 4KB escritos por dm-crypt, de modo que se deben borrar los primeros 1028KB. Esto es `1052672` bytes.

Para poner a cero el encabezado, utilice:

```
# head -c 1052672 /dev/urandom > */dev/sdX1*; sync

```

Para una longitud de clave de 512 bits (por ejemplo, para aes-xts-plain con clave de 512 bits) el encabezado le dedica 2 MiB. El encabezado de LUKS2 es de 4MiB.

En caso de duda, basta con ser generoso y sobrescribir los primeros 10 MB o menos.

```
# dd if=/dev/urandom of=*/dev/sdX1* bs=512 count=20480

```

**Nota:** con una copia de seguridad de los datos de cabecera se puede rescatar el sistema, pero el sistema de archivos estará probablemente dañado, dado que los primeros sectores cifrados habrán sido sobrescritos. Vea otras secciones sobre cómo hacer una copia de seguridad de los bloques de cabecera cruciales.

Al limpiar el encabezado con datos aleatorios, todo lo que queda en el dispositivo son datos cifrados. Una excepción a esto puede ocurrir con un disco SSD, debido a los bloques de caché utilizados por los SSD. En teoría, puede suceder que el encabezado se haya almacenado en caché durante un tiempo y que, por consiguiente, la copia puede estar disponible después de limpiar el encabezado original. Para evitar problemas de seguridad serios, debe realizarse un borrado ATA seguro del SSD (proceda consultando la página de cryptsetup [FAQ 5.19](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)).

## Particionar

Esta sección solo se aplica cuando se cifra un sistema completo. Después de que se haya sobrescrito de forma segura la unidad o los discos, se tendrá que elegir adecuadamente un esquema de particionado, teniendo en cuenta los requisitos de dm-crypt y los efectos que tendrán las diversas opciones en la gestión del sistema resultante.

Es importante tener en cuenta que en [casi](#Partición_de_arranque_(GRUB)) todos los casos debe haber una partición separada para `/boot` que debe permanecer sin cifrar, ya que el gestor de arranque necesita acceder al directorio `/boot` donde se cargarán los módulos de encriptación y de initramfs necesarios para iniciar el resto del sistema (vea [mkinitcpio (Español)](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") para más detalles). Si esto plantea problemas de seguridad, vea [dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties").

Otro factor importante a tener en cuenta es cómo se manejarán el espacio de swap y la suspensión del sistema, vea [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

### Particiones físicas

En el caso más simple, las capas cifradas pueden hacerse directamente sobre las particiones físicas; vea [Partitioning (Español)](/index.php/Partitioning_(Espa%C3%B1ol) "Partitioning (Español)") para ver los métodos para crearlas. Al igual que en un sistema sin cifrar, será suficiente con una partición raíz, además de otra para `/boot`, como se indicó anteriormente. Este método permite decidir qué particiones cifrar y cuáles dejar sin cifrar, y funciona igual, independientemente del número de discos implicados. También será posible añadir o eliminar particiones en el futuro, pero el tamaño de una partición estará limitado por el tamaño del disco que lo aloja. Por último, tenga en cuenta que para abrir cada partición encriptada se necesitarán claves o frases de acceso separadas, aunque esto se puede automatizar durante el arranque usando el archivo `crypttab`, vea [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration").

### Dispositivos de bloques apilados

Sin embargo, si se necesita más flexibilidad, dm-crypt puede coexistir con otros dispositivos de bloque apilados como [LVM (Español)](/index.php/LVM_(Espa%C3%B1ol) "LVM (Español)") y [RAID (Español)](/index.php/RAID_(Espa%C3%B1ol) "RAID (Español)"). Los contenedores cifrados pueden residir por debajo o por encima de otros dispositivos de bloque apilados:

*   Si los dispositivos LVM/RAID se crean encima de la capa cifrada, será posible agregar, quitar y cambiar el tamaño de los sistemas de archivos de la misma partición cifrada libremente, y solo se necesitará una clave o frase de acceso para todos ellos. Dado que la capa cifrada reside en una partición física, no será posible, sin embargo, explotar la capacidad de LVM y RAID para abarcar varios discos.
*   Si la capa cifrada se crea en la parte superior de los dispositivos LVM/RAID, todavía será posible reorganizar los sistemas de archivos en el futuro, pero con mayor complejidad, ya que las capas de cifrado tendrán que ser ajustadas en consecuencia. Además, se requerirán frases secretas o claves separadas para abrir cada dispositivo encriptado. Esta, sin embargo, es la única opción para sistemas que necesitan sistemas de archivos cifrados que abarquen múltiples discos.

### Subvolúmenes Btrfs

Las [características de subvolumes](/index.php/Btrfs#Subvolumes "Btrfs") integradas en el sistema de archivos [Btrfs](/index.php/Btrfs "Btrfs") se pueden usar con dm-crypt, reemplazando completamente la necesidad de LVM si no se requieren otros sistemas de archivos. Sin embargo, tenga en cuenta que los archivos de intercambio [no son soportados](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F) por brtrfs, por lo que es necesaria una partición [de intercambio](/index.php/Encrypted_swap "Encrypted swap") cifrada si se desea un espacio de [intercambio](/index.php/Swap_(Espa%C3%B1ol) "Swap (Español)"). Vea también [Dm-crypt/Encrypting an entire system (Español)#Subvolúmenes btrfs con espacio de intercambio](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Subvolúmenes_btrfs_con_espacio_de_intercambio "Dm-crypt/Encrypting an entire system (Español)").

### Partición de arranque (GRUB)

Véase [dm-crypt/Encrypting an entire system (Español)#Cifrar partición de arranque (GRUB)](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol)#Cifrar_partición_de_arranque_(GRUB) "Dm-crypt/Encrypting an entire system (Español)").