**Estado de la traducción**
Este artículo es una traducción de [FAT](/index.php/FAT "FAT"), revisada por última vez el **2018-10-31**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=FAT&diff=0&oldid=552197) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [File systems](/index.php/File_systems "File systems")

De [Wikipedia:Tabla de asignación de archivos](https://en.wikipedia.org/wiki/es:Tabla_de_asignaci%C3%B3n_de_archivos "wikipedia:es:Tabla de asignación de archivos"):

	Tabla de asignación de archivos, comúnmente conocido como FAT (del inglés file allocation table), es un sistema de archivos desarrollado para MS-DOS, así como el sistema de archivos principal de las ediciones no empresariales de Microsoft Windows hasta Windows Me.

	FAT es relativamente sencillo. A causa de ello, es un formato popular para disquetes admitido prácticamente por todos los sistemas operativos existentes para computadora personal. Se utiliza como mecanismo de intercambio de datos entre sistemas operativos distintos que coexisten en la misma computadora, lo que se conoce como entorno multiarranque. También se utiliza en tarjetas de memoria y dispositivos similares.

## Contents

*   [1 Creación del sistema de archivos](#Creaci.C3.B3n_del_sistema_de_archivos)
*   [2 Configuración del kernel](#Configuraci.C3.B3n_del_kernel)
*   [3 Escribir en FAT32 como usuario normal](#Escribir_en_FAT32_como_usuario_normal)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Creación del sistema de archivos

Para crear un sistema de archivos FAT, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [dosfstools](https://www.archlinux.org/packages/?name=dosfstools).

`mkfs.fat` admite la creación de FAT12, FAT16 y FAT32, consulte [Wikipedia:es:Tabla de asignación de archivos#Historia y versiones](https://en.wikipedia.org/wiki/es:Tabla_de_asignaci%C3%B3n_de_archivos#Historia_y_versiones "wikipedia:es:Tabla de asignación de archivos") para obtener una explicación de sus diferencias. `mkfs.fat` seleccionará el tipo de FAT según el tamaño de la partición, para crear explícitamente un cierto tipo de sistema de archivos FAT use la opción `-F`. Vea [mkfs.fat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.fat.8) para más información.

**Sugerencia:** Para la mayoría de las situaciones, querrá usar FAT32.

Formatear una partición a FAT32:

```
# mkfs.fat -F 32 /dev/*partición*

```

## Configuración del kernel

He aquí un ejemplo de la configuración predeterminada de *montaje* en el kernel:

 `$ zgrep -e FAT -e DOS /proc/config.gz | sort -r` 
```
# DOS/FAT/NT Filesystems
CONFIG_FAT_FS=m
CONFIG_MSDOS_PARTITION=y
CONFIG_FAT_FS=m
CONFIG_MSDOS_FS=m
CONFIG_VFAT_FS=m
CONFIG_FAT_DEFAULT_CODEPAGE=437
CONFIG_FAT_DEFAULT_IOCHARSET="iso8859-1"
CONFIG_NCPFS_SMALLDOS=y
```

Una breve descripción de las opciones:

*   Configuración de idioma: `CONFIG_FAT_DEFAULT_CODEPAGE`, `CONFIG_FAT_DEFAULT_IOCHARSET`
*   Todos los nombres de archivo a minúscula en una partición FAT, si están habilitados: `CONFIG_NCPFS_SMALLDOS`
*   Habilita la compatibilidad con los sistemas de archivos FAT: `CONFIG_FAT_FS`, `CONFIG_MSDOS_FS`, `CONFIG_VFAT_FS`
*   Habilita el soporte de un disco duro particionado en formato FAT en un ordenador con arquitectura x86: `CONFIG_MSDOS_PARTITION`

Si el tipo de partición detectado por el montaje es VFAT, se ejecutará el script `/usr/bin/mount.vfat`.

 `/usr/bin/mount.vfat` 
```
#!/bin/bash
#montar VFAT con permisos rw (lectura-escritura) completos para todos los usuarios
#/usr/bin/mount -i -t vfat -oumask=0000,iocharset=utf8 "$@"
#Lo anterior es lo mismo que
mount -i -t vfat -oiocharset=utf8,fmask=0000,dmask=0000 "$@"
```

## Escribir en FAT32 como usuario normal

Para escribir en una partición FAT32, debe realizar algunos cambios en el archivo [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)").

 `/etc/fstab`  `/dev/sd*xY*    /mnt/algún_directorio  vfat   **user**,rw,umask=000              0  0` 

La marca `user` significa que cualquier usuario (incluso no root) puede montar y desmontar la partición `/dev/sd*X* `. `rw` otorga acceso de lectura-escritura; la opción `umask` elimina los permisos seleccionados, por ejemplo, `umask=111` elimina los permisos de ejecución. El problema es que esta entrada también elimina los permisos de ejecución de los directorios, por lo que debemos corregirlo con `dmask=000`. Véase también [Umask](/index.php/Umask_(Espa%C3%B1ol) "Umask (Español)").

Sin estas opciones, todos los archivos serán ejecutables. Puede usar la opción `showexec` en lugar de las opciones umask y dmask, que muestra todos los ejecutables de Windows (com, exe, bat) en colores ejecutables.

Por ejemplo, si su partición FAT32 está en `/dev/sda9`, y desea montarla en `/mnt/fat32`, entonces usaría:

 `/etc/fstab`  `/dev/sda9    /mnt/fat32        vfat   **user**,rw,umask=111,dmask=000    0  0` 

Ahora, cualquier usuario puede montarlo con:

```
$ mount /mnt/fat32

```

Y desmontarlo con:

```
$ umount /mnt/fat32

```

## Véase también

*   [Montar sistema de archivos FAT](http://www.nslu2-linux.org/wiki/HowTo/MountFATFileSystems)