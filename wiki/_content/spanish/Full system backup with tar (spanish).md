**Estado de la traducción**
Este artículo es una traducción de [Full system backup with tar](/index.php/Full_system_backup_with_tar "Full system backup with tar"), revisada por última vez el **2019-11-15**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Full_system_backup_with_tar&diff=0&oldid=563848) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Full system backup with SquashFS (Español)](/index.php/Full_system_backup_with_SquashFS_(Espa%C3%B1ol) "Full system backup with SquashFS (Español)")

Este artículo le enseñará como hacer una copia de seguridad de todo el sistema con [tar](/index.php/Tar_(Espa%C3%B1ol) "Tar (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Descripción](#Descripción)
*   [2 Arrancar con LiveCD](#Arrancar_con_LiveCD)
*   [3 Cambiar a un entorno enjaulado](#Cambiar_a_un_entorno_enjaulado)
*   [4 Montar otras particiones](#Montar_otras_particiones)
*   [5 Excluir archivos](#Excluir_archivos)
*   [6 Script para realizar la copia de seguridad](#Script_para_realizar_la_copia_de_seguridad)
*   [7 Restaurar](#Restaurar)
*   [8 Realizar copia de seguridad con compresión parallel](#Realizar_copia_de_seguridad_con_compresión_parallel)

## Descripción

Crear una copia de seguridad con [tar](https://en.wikipedia.org/wiki/es:Tar "wikipedia:es:Tar") tiene la ventaja de usar compresión que puede ayudar a guardar espacio en disco, y aportar simplicidad. El proceso solo requiere varios pasos, que son:

1.  Arrancar desde un LiveCD.
2.  Pasar al entorno enjaulado de la instalación Linux.
3.  Montar (si hubiesen) otras particiones/discos.
4.  Añadir exclusiones.
5.  Utilizar el script de respaldo para hacer la copia de seguridad

Para reducir al mínimo la inactividad la copia de seguridad puede alternativamente realizarse en un sistema en ejecución usando [instantáneas LVM](/index.php/LVM_(Espa%C3%B1ol)#Instantáneas/Snapshots "LVM (Español)"), si todos los sistemas de archivos están montados en volúmenes LVM.

## Arrancar con LiveCD

Muchos LiveCD, USB... tienen la capacidad de dejarle cambiar al entorno enjaulado de su instalación. Aunque no es requisito montar una jaula para hacer la copia de seguridad, esto proporciona la capacidad para ejecutar el script sin tener que pasarlo a un dispositivo de almacenamiento temporal o tener que ubicarlo en el sistema de archivos. El medio vivo debe compartir con la instalación linux la misma arquitectura (es decir, i686 o x86_64).

## Cambiar a un entorno enjaulado

Lo primero que debería tener es un entorno de para ejecutar scripts («scripting») en su instalación Linux. Si no sabe lo que es, significa que puede ejecutar cualquier script que pueda tener como si fuera un programa normal. Si no pudiese, vea este [artículo](http://linuxtidbits.wordpress.com/2009/12/03/setting-up-a-scripting-environment/) para saber como hacerlo. Lo siguiente que necesita es pasar al entorno enjaulado, para aprender más sobre este proceso, lea [esto](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)"). Dentro de una jaula, no necesita ningún sistema de archivos temporal (`/proc`, `/sys` y `/dev`). Estos sistemas de archivos se inicializan durante el arranque y en verdad no debe hacer una copia de ellos, ya que pueden interferir con la correcta (y necesaria) inicialización del sistema, que puede cambiar con cualquier actualización. Para cambiar al entorno enjaulado, tiene que montar la partición raíz de su instalación Linux. Por ejemplo:

```
mkdir /mnt/arch
mount /dev/<su partición o disco>

```

Use `fdisk -l` para descubrir sus particiones y discos. Una vez lo sepa, ejecute `chroot`:

```
cd /mnt/arch
chroot . /bin/bash

```

Este ejemplo claramente usa bash pero puede utilizar otros intérpretes de órdenes si están disponibles. Ahora se encontrará en su entorno de scripting (esto es proporcionado si se haya cargado el archivo de configuración `~/.bashrc` al entrar en la jaula):

```
cat ~/.bash_profile
# Si usa bash, carga la configuración del archivo local .bashrc
source ~/.bashrc

```

## Montar otras particiones

Otras particiones que use tendrán que ser montadas en su ubicaciones correspondientes (por ejemplo, si tiene una partición `/home` separada).

## Excluir archivos

`tar` tiene la capacidad de ignorar ciertos archivos y carpetas. La sintaxis requiere colocar cada archivo o carpeta a ignorar en una línea distinta. `tar` también tiene la capacidad de entender expresiones regulares (regexps). Por ejemplo:

```
# No copias antiguas                                                               
/opt/backup/arch-full*                                                                   

# No archivos temporales                                                           
/tmp/*

# No a la caché de pacman
/var/cache/pacman/pkg/
...

```

## Script para realizar la copia de seguridad

Respaldar con tar es un proceso directo. Aquí tiene un script básico que puede hacerlo y que hace además unas cuantas comprobaciones. Tendrá que modificar este script definiendo la ubicación donde poner la copia, los archivos a excluir (si tiene alguno), y ejecutarlo una vez haya pasado al entorno `chroot` y montado todas las particiones.

```
#!/bin/bash
# Copia completa del sistema

# Destino de la copia
backdest=/opt/backup

# Etiquetas para la copia
#PC=${HOSTNAME}
pc=pavilion
distro=arch
type=full
date=$(date "+%F")
backupfile="$backdest/$distro-$type-$date.tar.gz"

# Exclusión de ubicación de archivo
prog=${0##*/} # Nombre de programa según el nombre del archivo
excdir="/home/<user>/.bin/root/backup"
exclude_file="$excdir/$prog-exc.txt"

# Comprobación de jaula
echo -n "Recuerde hacer chroot desde un LiveCD. ¿Ejecutar la copia de seguridad? (s/n): "
read executeback

# Comprobar si el archivo de exclusión existe
if [ ! -f $exclude_file ]; then
  echo -n "No existen ningún archivo excluido, ¿continuar? (s/n): "
  read continue
  if [ $continue == "n" ]; then exit; fi
fi

if [ $executeback = "s" ]; then
  # -p y --xattrs almacenan todos los permisos y atributos extendidos.
  # Sin ambos, muchos programas dejarán de funcionar.
  # Es seguro eliminar el indicador detallado (-v). Si estás usando un
  # terminal lenta, esto puede acelerar el proceso de copia de seguridad.
  tar --exclude-from=$exclude_file --xattrs -czpvf $backupfile /
fi

```

## Restaurar

Para restaurar desde una copia de seguridad anterior, monte todas las particiones relevantes, cambie el directorio de trabajo actual al directorio raíz y ejecute:

```
bsdtar --xattrs -xpf $backupfile

```

reemplazando $backupfile con el archivo de respaldo. La eliminación de todos los archivos que se agregaron desde que se realizó la copia de seguridad debe realizarse manualmente. Recreando los sistemas de archivos es una manera fácil de hacer esto.

## Realizar copia de seguridad con compresión parallel

Para realizar una copia de seguridad con compresión parallel ([SMP](https://en.wikipedia.org/wiki/es:Multiprocesamiento_sim%C3%A9trico "wikipedia:es:Multiprocesamiento simétrico")), utilice [pbzip2](https://www.archlinux.org/packages/?name=pbzip2) (Parallel bzip2).

Primero haga una copia de seguridad de los archivos en un archivo tarball simple sin compresión:

```
# tar -cvf /*ruta_de_destino*/etc-backup.tar /etc

```

Luego utilice pbzip2 para comprimirlo con parallel:

```
$ pbzip2 /ruta/a/directorio/elegid/etc-backup.tar.bz2

```

Almacene `etc-backup.tar.bz2` en uno o más medios sin conexión, como una memoria USB, disco duro externo o CD-R. Ocasionalmente verifique la integridad del proceso de copia de seguridad comparando los archivos y directorios originales con sus copias de seguridad. Posiblemente mantenga una lista de «hashes» de los archivos respaldados para hacer la comparación más rápida.

Restaure los archivos corruptos de `/etc` extrayendo el archivo `etc-backup.tar.bz2` en un directorio de trabajo temporal y copiando archivos y directorios individuales según sea necesario. Para restaurar todo el directorio `/etc` con todo su contenido, ejecute la siguiente orden como root:

```
tar -xvjf etc-backup.tar.bz2 -C /

```