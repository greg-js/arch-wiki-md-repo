Proporciona un mecanismo de permisos adicionales más flexibles para los sistemas de archivos. Está diseñado para ayudar con los permiso de archivos en UNIX. ACL permite dar permisos para cualquier usuario o grupo a cualquier recurso del disco.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Habilitando ACL](#Habilitando_ACL)
    *   [2.2 Establecer ACL](#Establecer_ACL)
    *   [2.3 Mostrar ACL](#Mostrar_ACL)
*   [3 Ejemplos](#Ejemplos)
    *   [3.1 Salida del comando ls](#Salida_del_comando_ls)
    *   [3.2 Conceder permisos de ejecución para archivos privados a un servidor Web](#Conceder_permisos_de_ejecuci.C3.B3n_para_archivos_privados_a_un_servidor_Web)
*   [4 También puede ver](#Tambi.C3.A9n_puede_ver)

## Instalación

El paquete [acl](https://www.archlinux.org/packages/?name=acl) es una dependencia de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") que debería estar instalado.

## Configuración

### Habilitando ACL

Para habilitar ACL los sistema de archivos se deben haber montado con la opción `acl`, puede usar [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)") para hacer el montaje con acl permanente en su sistema.

Es posible que la opción `acl` estés activada por defecto como opción de montaje en el sistema de archivos; en Btrfs y ext* también. Use el siguiente comando para verificar las particiones formateadas con ext* con la opción:

 `# tune2fs -l /dev/sd*XY* | grep "Default mount options:"` 
```
Default mount options:    user_xattr acl

```

También puede verificar que el punto de montaje por defecto no está anulado, en tal caso vería `noacl` en `/proc/mounts`.

Puede configurar las opciones de montajes predeterminadas de un sistema de archivos utilizando el comando `tune2fs -o *opción* *partición*` por ejemplo:

```
# tune2fs -o acl /dev/sdXY

```

Utilizar las opciones de montaje por defecto en lugar de las entradas en `/etc/fstab` es muy útil para unidades externa, tales particiones serán montadas con la opción `acl` en otras máquinas GNU/Linux; sin necesidad de editar /etc/fstab en cada máquina.

**Note:**

*   `acl` se especifica por defecto cuando se crean sistemas de archivos ext2/3/4 y se configura en `/etc/mke2fs.conf`.
*   Por defecto las opciones de montaje no están en la lista de `/proc/mounts`.

### Establecer ACL

ACL puede ser modificado usando el comando ‘’’setfacl’’’

Para agregar permiso a un usuario (`*user*` es el nombre del usuario o el ID):

```
# setfacl -m "u:*user:permissions*" <file/dir>

```

Agregar permisos para un grupo (`*group*` es el nombre del grupo o el ID del grupo):

```
# setfacl -m "g:*group:permissions*" <file/dir>

```

Para permitir que todos los archivos o directorios hereden las entradas de ACL desde el directorio con:

```
# setfacl -dm "*entry*" <dir>

```

Para eliminar un entrada específica:

```
# setfacl -x "*entry*" <file/dir>

```

Para remover todas las entradas:

```
 # setfacl -b <file/dir>

```

### Mostrar ACL

Para mostrar los permisos use:

```
# getfacl <nombre archivo>

```

## Ejemplos

Establecer todos lo permisos para el usuario Jhonny en el archivo con nombre “abc”:

```
# setfacl -m "u:johny:rwx" abc

```

Check permissions

 `# getfacl abc` 
```
# file: abc
# owner: someone
# group: someone
user::rw-
user:johny:rwx
group::r--
mask::rwx
other::r--

```

Listar los permisos

```
# setfacl -m "u:johny:r-x" abc

```

Check permissions

 `# getfacl abc` 
```
# file: abc
# owner: someone
# group: someone
user::rw-
user:johny:r-x
group::r--
mask::r-x
other::r--

```

Eliminar todas las entradas ACL extendidas:

```
# setfacl -b abc

```

Check permissions

 `# getfacl abc` 
```
# file: abc
# owner: someone
# group: someone
user::rw-
group::r--
other::r--

```

### Salida del comando ls

Notará que hay un ACL para un archivo dado porque se mostrará un `**+**` (signo más) después del permiso Unix en la salida de `ls -l`.

 `$ ls -l /dev/audio` 
```
crw-rw----+ 1 root audio 14, 4 nov.   9 12:49 /dev/audio

```
 `$ getfacl /dev/audio` 
```
getfacl: Removing leading '/' from absolute path names
# file: dev/audio
# owner: root
# group: audio
user::rw-
user:solstice:rw-
group::rw-
mask::rw-
other::---

```

### Conceder permisos de ejecución para archivos privados a un servidor Web

La siguiente técnica describe de cómo un proceso de un servidor web puede tener acceso a los archivos que residen en el directorio personal de un usuario sin comprometer la seguridad dando acceso a todo el mundo.

Supongamos que el servidor web se ejecuta como `webserver` del usuario y le concede acceso al directorio personal del usuario geoffrey que es `/home/geoffrey`

El primer paso es otorgar permiso de ejecución a `webserver` para que pueda acceder a directorio personal de `geoffrey`:

```
# setfacl -m "u:webserver:--x" /home/geoffrey

```

*Recuerda*: Los permisos de ejecución en un directorio son necesarios para que un proceso enumere el contenido del directorio.

Ahora `webserver` puede acceder a los archivos en `/home/geoffrey` y otros no necesitan acceso por lo tanto se puede remover de forma segura.

```
# chmod o-rx /home/geoffrey

```

El comando `getfacl` puede ser usado para verificar los cambios.

```
$ getfacl /home/geoffrey
getfacl: Removing leading '/' from absolute path names
# file: home/geoffrey
# owner: geoffrey
# group: geoffrey
user::rwx
user:webserver:--x
group::r-x
mask::r-x
otros::---

```

Como se muestra en la salida anterior ya no tiene permisos pero `webserver` todavía puede acceder a los archivos, por lo tanto la seguridad se ha incrementado.

## También puede ver

*   [getfacl(1)](http://man7.org/linux/man-pages/man1/getfacl.1.html)
*   [setfacl(1)](http://man7.org/linux/man-pages/man1/setfacl.1.html)
*   Un antiguo, exhaustivo y relevante recurso [guia](http://vanemery.net/Linux/ACL/linux-acl.html) de ACL
*   [How to set default file permissions for all folders/files in a directory?](http://unix.stackexchange.com/questions/1314/how-to-set-default-file-permissions-for-all-folders-files-in-a-directory)