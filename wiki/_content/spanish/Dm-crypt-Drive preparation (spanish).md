< Volver a [Dm-crypt (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol) "Dm-crypt (Español)")

**Estado de la traducción:** este artículo es una versión traducida de [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"). Fecha de la última traducción/revisión: **2017-09-29**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Dm-crypt/Drive_preparation&diff=0&oldid=450405).

Antes de cifrar una unidad, es recomendable realizar un borrado seguro del disco, sobrescribiendo toda la unidad con datos aleatorios. Para evitar ataques criptográficos o [recuperación de archivos](/index.php/File_recovery "File recovery") no deseados, lo ideal es que estos datos sean indistinguibles de los datos escritos posteriormente por dm-crypt. Para comprender mejor el tema vea [Disk encryption#Preparing the disk](/index.php/Disk_encryption#Preparing_the_disk "Disk encryption").

## Contents

*   [1 Borrar de forma segura la unidad de disco duro](#Borrar_de_forma_segura_la_unidad_de_disco_duro)
    *   [1.1 Métodos genéricos](#M.C3.A9todos_gen.C3.A9ricos)
    *   [1.2 Métodos específicos de dm-crypt](#M.C3.A9todos_espec.C3.ADficos_de_dm-crypt)
        *   [1.2.1 Limpiar un disco o partición vacíos con dm-crypt](#Limpiar_un_disco_o_partici.C3.B3n_vac.C3.ADos_con_dm-crypt)
        *   [1.2.2 Limpiar espacio libre con dm-crypt después de la instalación](#Limpiar_espacio_libre_con_dm-crypt_despu.C3.A9s_de_la_instalaci.C3.B3n)
        *   [1.2.3 Limpiar el encabezado LUKS](#Limpiar_el_encabezado_LUKS)
*   [2 Particionar](#Particionar)
    *   [2.1 Particiones físicas](#Particiones_f.C3.ADsicas)
    *   [2.2 Dispositivos de bloques apilados](#Dispositivos_de_bloques_apilados)
    *   [2.3 Subvolúmenes Btrfs](#Subvol.C3.BAmenes_Btrfs)
    *   [2.4 Partición de arranque (GRUB)](#Partici.C3.B3n_de_arranque_.28GRUB.29)

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

Las [FAQ de cryptsetup](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) mencionan un procedimiento muy sencillo para usar en un volumen existente de dm-crypt para limpiar todo el espacio libre accesible en el bloque subyacente del dispositivo con datos aleatorios al actuar como un simple generador de números pseudoaleatorios. También se afirma que protege contra la divulgación de patrones de uso. Esto se debe a que los datos cifrados son prácticamente indistinguibles de los aleatorios.

#### Limpiar un disco o partición vacíos con dm-crypt

En primer lugar, cree un contenedor temporal cifrado en la partición (`sdXY`) o en el disco completo (`sdX`), que va a ser cifrado, por ejemplo usando parámetros de cifrado predeterminados y una clave aleatoria a través de la opción `--key-file /dev/{u}random` (véase también [Random number generation](/index.php/Random_number_generation "Random number generation")):

```
# cryptsetup open --type plain /dev/sdXY container --key-file /dev/random

```

En segundo lugar, compruebe que existe:

 `# fdisk -l` 
```
Disk /dev/mapper/container: 1000 MB, 1000277504 bytes
...
Disk /dev/mapper/container does not contain a valid partition table
```

Limpie el contenedor con ceros. Un uso de `if=/dev/urandom` no es necesario ya que el cifrado de encriptación se utiliza para enfarruyar.

 `# dd if=/dev/zero of=/dev/mapper/container status=progress`  `dd: writing to ‘/dev/mapper/container’: No space left on device` 
**Sugerencia:**

*   La utilización de *dd* con la opción `bs=`, por ejemplo `bs=1M`, se utiliza con frecuencia para aumentar el rendimiento del disco de la operación.
*   Para realizar una comprobación de la operación, llene de ceros la partición antes de crear el contenedor de limpieza. Después se puede usar la orden de borrado `blockdev --getsize64 */dev/mapper/container*` para obtener el tamaño exacto del contenedor como root. Ahora se puede usar 'od' para ver como el borrado sobrescribe los sectores puestos a cero, por ejemplo `od -j *containersize - blocksize*` para ver el borrado completo hasta el final.

Finalmente, cierre el contenedor temporal:

```
# cryptsetup close container

```

Al cifrar un sistema completo, el siguiente paso es [particionar](#Partitioning). Si acaba de cifrar una partición, continúe en [dm-crypt/Encrypting a non-root file system#Partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system").

#### Limpiar espacio libre con dm-crypt después de la instalación

Los usuarios que no tuvieron tiempo para realizar el borrado antes de la [instalación](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"), pueden lograr un efecto similar una vez que se arranque el sistema cifrado y se monten los sistemas de archivos. Sin embargo, considere la posibilidad de que el sistema de archivos afectado haya establecido un espacio reservado, por ejemplo para el usuario root u otro mecanismo de [cuota de disco](/index.php/Disk_quota "Disk quota"), que puede limitar el borrado, incluso cuando se realiza por el usuario root: en esos casos, es posible que algunas partes del dispositivo de bloque subyacente no se escriban en absoluto.

Para ejecutar el borrado, llene temporalmente el espacio libre restante de la partición escribiendo en un archivo presente en el contenedor cifrado:

 `# dd if=/dev/zero of=/file/in/container status=progress`  `dd: writing to ‘/file/in/container’: No space left on device` 

Sincronice la caché del disco y, luego, elimine el archivo para recuperar el espacio libre.

```
# sync
# rm /file/in/container

```

El proceso anterior debe repetirse para cada dispositivo de bloqueo de partición creado y del sistema de archivos en él. Por ejemplo, la instalación de [LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system"), el proceso debe realizarse para cada volumen lógico.

#### Limpiar el encabezado LUKS

Las particiones formateadas con dm-crypt/LUKS contienen un encabezado con las opciones de cifrado y claves utilizadas, al que se remite `dm-mod` al abrir el dispositivo de bloque. Después del encabezado comienza la aleatoriedad real de los datos de la partición. Por lo tanto, al reinstalar en una unidad ya cifrada, o desarmar una (por ejemplo, la venta de PC, el cambio de unidades, etc.) «puede» ser suficiente limpiar el encabezado de la partición, en lugar de sobrescribir la unidad entera, que puede ser un proceso largo.

Al borrar el encabezado LUKS se borrará la clave maestra cifrada PBKDF2 (AES), las [sal](https://en.wikipedia.org/wiki/es:Sal "wikipedia:es:Sal"), y así sucesivamente.

**Nota:** es importante escribir en la partición cifrada con LUKS (`/dev/sda**1**` en este ejemplo) y no directamente a los nodos de las particiones del disco. Configuraciones con cifrado como una capa de asignación de dispositivos encima de otras, por ejemplo LVM sobre LUKS sobre RAID debería escribir en RAID, respectivamente.

En un encabezado con un único valor predeterminado de 256 bits, el tamaño de la clave ocupa 1024 KB. Se aconseja también sobrescribir los primeros 4KB escritos por dm-crypt, de modo que se deben borrar los primeros 1028KB. Esto es `1052672` bytes.

Para poner a cero el encabezado, utilice:

```
# head -c 1052672 /dev/urandom > /dev/sda1; sync

```

Para una longitud de clave de 512 bits (por ejemplo, para aes-xts-plain con clave de 512 bits) el encabezado le dedica 2 MB.

En caso de duda, basta con ser generoso y sobrescribir los primeros 10 MB o menos.

```
# dd if=/dev/urandom of=/dev/sda1 bs=512 count=20480

```

**Nota:** con una copia de seguridad de los datos de cabecera se puede rescatar el sistema, pero el sistema de archivos estará probablemente dañado, dado que los primeros sectores cifrados habrán sido sobrescritos. Vea otras secciones sobre cómo hacer una copia de seguridad de los bloques de cabecera cruciales.

Al limpiar el encabezado con datos aleatorios, todo lo que queda en el dispositivo son datos cifrados. Una excepción a esto puede ocurrir con un disco SSD, debido a los bloques de caché utilizados por los SSD. En teoría, puede suceder que el encabezado se haya almacenado en caché durante un tiempo y que, por consiguiente, la copia puede estar disponible después de limpiar el encabezado original. Para evitar problemas de seguridad serios, debe realizarse un borrado ATA seguro del SSD (proceda consultando la página de cryptsetup [FAQ 5.19](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)).

## Particionar

Esta sección solo se aplica cuando se cifra un sistema completo. Después de que se haya sobrescrito de forma segura la unidad o los discos, se tendrá que elegir adecuadamente un esquema de particionado, teniendo en cuenta los requisitos de dm-crypt y los efectos que tendrán las diversas opciones en la gestión del sistema resultante.

Es importante tener en cuenta que en [casi](#Boot_partition_.28GRUB.29) todos los casos debe haber una partición separada para `/boot` que debe permanecer sin cifrar, ya que el gestor de arranque necesita acceder al directorio `/boot` donde se cargarán los módulos de encriptación y de initramfs necesarios para iniciar el resto del sistema (vea [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") para más detalles). Si esto plantea problemas de seguridad, vea [dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties").

Otro factor importante a tener en cuenta es cómo se manejarán el espacio de swap y la suspensión del sistema, vea [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

### Particiones físicas

En el caso más simple, las capas cifradas pueden hacerse directamente sobre las particiones físicas; vea [Partitioning](/index.php/Partitioning "Partitioning") para ver los métodos para crearlas. Al igual que en un sistema sin cifrar, será suficiente con una partición raíz, además de otra para `/boot`, como se indicó anteriormente. Este método permite decidir qué particiones cifrar y cuáles dejar sin cifrar, y funciona igual, independientemente del número de discos implicados. También será posible añadir o eliminar particiones en el futuro, pero el tamaño de una partición estará limitado por el tamaño del disco que lo aloja. Por último, tenga en cuenta que para abrir cada partición encriptada se necesitarán claves o frases de acceso separadas, aunque esto se puede automatizar durante el arranque usando el archivo `crypttab`, vea [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration").

### Dispositivos de bloques apilados

Sin embargo, si se necesita más flexibilidad, dm-crypt puede coexistir con otros dispositivos de bloque apilados como [LVM](/index.php/LVM "LVM") y [RAID](/index.php/RAID "RAID"). Los contenedores cifrados pueden residir por debajo o por encima de otros dispositivos de bloque apilados:

*   Si los dispositivos LVM/RAID se crean encima de la capa cifrada, será posible agregar, quitar y cambiar el tamaño de los sistemas de archivos de la misma partición cifrada libremente, y solo se necesitará una clave o frase de acceso para todos ellos. Dado que la capa cifrada reside en una partición física, no será posible, sin embargo, explotar la capacidad de LVM y RAID para abarcar varios discos.
*   Si la capa cifrada se crea en la parte superior de los dispositivos LVM/RAID, todavía será posible reorganizar los sistemas de archivos en el futuro, pero con mayor complejidad, ya que las capas de cifrado tendrán que ser ajustadas en consecuencia. Además, se requerirán frases secretas o claves separadas para abrir cada dispositivo encriptado. Esta, sin embargo, es la única opción para sistemas que necesitan sistemas de archivos cifrados que abarquen múltiples discos.

### Subvolúmenes Btrfs

Las [características de subvolumes](/index.php/Btrfs#Subvolumes "Btrfs") integradas en el sistema de archivos [Btrfs](/index.php/Btrfs "Btrfs") se pueden usar con dm-crypt, reemplazando completamente la necesidad de LVM si no se requieren otros sistemas de archivos. Sin embargo, tenga en cuenta que los archivos de intercambio [no son soportados](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F) por brtrfs, por lo que es necesaria una partición [swap](/index.php/Encrypted_swap "Encrypted swap") cifrada si se desea un espacio de [intercambio](/index.php/Swap "Swap") . Vea también [Dm-crypt/Encrypting an entire system#Btrfs subvolumes with swap](/index.php/Dm-crypt/Encrypting_an_entire_system#Btrfs_subvolumes_with_swap "Dm-crypt/Encrypting an entire system").

### Partición de arranque (GRUB)