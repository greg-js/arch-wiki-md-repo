Este documento le guía en la configuración del acceso a particiones NTFS con derechos de lectura y escritura utilizando ntfs-3g.

## Contents

*   [1 Instalar ntfs-3g](#Instalar_ntfs-3g)
*   [2 Montaje manual](#Montaje_manual)
    *   [2.1 Configuración básica](#Configuración_básica)
        *   [2.1.1 Editar fstab](#Editar_fstab)
    *   [2.2 Configuración avanzada](#Configuración_avanzada)
        *   [2.2.1 Editar fstab](#Editar_fstab_2)
        *   [2.2.2 Opciones habituales y muy útiles de ntfs-3g](#Opciones_habituales_y_muy_útiles_de_ntfs-3g)
        *   [2.2.3 Valores de máscara (Bitmask)](#Valores_de_máscara_(Bitmask))
    *   [2.3 Daños en sistemas de archivo NTFS](#Daños_en_sistemas_de_archivo_NTFS)
    *   [2.4 Montar la partición](#Montar_la_partición)
    *   [2.5 Fallo de montaje](#Fallo_de_montaje)

### Instalar ntfs-3g

Asegúrese de tener habilitado el repositorio [extra]: [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

## Montaje manual

Existen dos opciones para montar particiones NTFS. La tradicional:

```
# mount -t ntfs /dev/<tu-partición-NTFS> /{mnt,...}/<folder>

```

La segunda opción es llamar a `ntfs-3g` directamente:

```
# ntfs-3g /dev/<tu-partición-NTFS> /<mount-location>

```

**Note:** No es necesario especificar el tipo de montaje ntfs-3g. El comando de montaje por defecto usará `/sbin/mount.ntfs`, que es un enlace simbólico a `/bin/ntfs-3g` una vez instalado el paquete ntfs-3g.

### Configuración básica

#### Editar fstab

Edite su archivo `/etc/fstab` de acuerdo con:

```
<partition>  <mount point>  ntfs  defaults  0 0

```

Por ejemplo:

```
/dev/sda1  /mnt/windows  ntfs  defaults  0 0

```

**Note:** Para las versiones de ntfs-3g iguales o mayores a la 2009.1.1, no es necesario agregar la opción `locale=<locale>`, por ej: `defaults,locale=es_ES.utf8`, para que los nombres de los archivos se muestren corréctamente.

### Configuración avanzada

Basicamente, no queremos poner aquí la opción `defaults` porque queremos tener mayor control sobre cómo se montan nuestras particiones NTFS.

#### Editar fstab

Edite su archivo `/etc/fstab` de acuerdo con:

```
<partition>  <mount point>  ntfs-3g  <options>  0 0

```

Ejemplos:

```
/dev/sda1  /mnt/windows  ntfs-3g  users,noauto,gid=users,umask=0022  0 0
/dev/sda5  /mnt/backup   ntfs-3g  users,uid=1000,gid=users,umask=0022        0 0

```

*   **Los ejemplos anteriores son útiles si quiere:**

1.  que sus particiones NTFS sean montables y desmontables por parte de cualquier usuario perteneciente al grupo (`gid=users`).
2.  que el usuario (`uid=1000`) y el grupo (`gid=users`) sean los "propietarios" de todo lo que hay en la partición y que los permisos sean -rw-rw-r-- (0664) para los ficheros y drwxrwxr-x (1775) para los directorios.
3.  que `/dev/sda5` sea montado automáticamente en el arranque pero `/dev/sda1` no

#### Opciones habituales y muy útiles de ntfs-3g

	users

	permite a todo el mundo mountar y desmontar las particiones NTFS siempre y cuando el binario ntfs-3g tenga establecido el permiso SUID para root *(Orden: `chmod u+s /bin/ntfs-3g`)*. Dese cuenta de que tiene que utilizar `users` en vez de `user`.

	noauto

	no montar automáticamente la partición en el arranque

	uid

	el valor en notación decimal del propietario de los archivos y directorios de una partición NTFS en particular

	gid

	el valor en notación decimal del grupo al que pertenecen los archivos y directorios de una partición NTFS en particular.

	umask

	el valor en notación octal para la máscara de archivos y carpetas. Más información sobre umask [aquí](http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html)

	fmask y dmask

	como umask, pero para establecer los permisos por separado para archivos y carpetas.

#### Valores de máscara (Bitmask)

Para saber fácilmente el valor de máscara de un conjunto de permisos en particular sin tener que hacer cálculos, todo lo que tiene que hacer es:

1.  Inicie una nueva sesión de shell. Utilice el emulador de terminal que prefiera.
2.  Use la orden **umask** para obtener la representación en notación octal de un conjunto de permisos en particular.
    1.  "Establezca" utilizando umask la máscara del modo para la creación de archivos. p.ej.: `$ umask ug=rw,o=r` Tenga en cuenta que ug=rw,o=r es equivalente a -rw-rw-r-- ó 0664.
    2.  Obtenga el equivalente octal simplemente ejecutando umask sin ningún argumento. `$ umask` Debería obtener esto: `0113` 

*   Consulte la sección **EXTENDED DESCRIPTION** de la página de manual de chmod para obtener más información acerca del operando **mode** (formato de cadena de la nueva máscara de modo de creación de archivos).

### Daños en sistemas de archivo NTFS

Si un sistema de archivos NTFS tiene errores, ntfs-3g lo montará solo con permisos de lectura. Para arreglar el problema deberá ejecutar Windows y el programa para corregir errores en disco.

Para corregir el sistema de archivos, debemos desmontar el dispositivo. Por ejemplo, si la partición NTFS con errores está en `/dev/sda2`:

```
# umount /dev/sda2
# ntfsfix /dev/sda2
Mounting volume... OK
Processing of $MFT and $MFTMirr completed successfully.
NTFS volume version is 3.1.
NTFS partition /dev/sda2 was processed successfully.
# mount /dev/sda2

```

Si todo a ido bien, el volumen tendrá permisos de escritura.

### Montar la partición

Esta sección puede ser usada para montar sus particiones NTFS y probar si todo a salido bien. Si has añadido todo en `/etc/fstab`, será montado automáticamente cada vez que el sistema arranque.

```
# mount <partition>

```

o bien

```
# mount <mount point>

```

Ejemplos:

```
# mount /dev/sda1
# mount /mnt/backup

```

*   Usted puede montar y desmontar particiones NTFS como un usuario normal si sigue la sección **Configuración avanzada** de este documento.

### Fallo de montaje

Si no puede montar la partición NFTS con los pasos seguidos en esta guía, pruebe a añadir la sección UUID en `fstab` para las particiones NTFS.

Ejemplo:

```
UUID=El_UUID_Correspondiente  /mnt/windows  ntfs-3g  noauto,gid=users,umask=0022  0 0

```