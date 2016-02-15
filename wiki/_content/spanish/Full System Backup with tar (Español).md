Este artículo le enseñará como hacer una copia de seguridad de todo el sistema con [tar (Español)](/index.php?title=Tar_(Espa%C3%B1ol)&action=edit&redlink=1 "Tar (Español) (page does not exist)").

## Contents

*   [1 Descripción](#Descripci.C3.B3n)
*   [2 Arrancar con LiveCD](#Arrancar_con_LiveCD)
*   [3 Cambiar a un entorno enjaulado](#Cambiar_a_un_entorno_enjaulado)
*   [4 Montar otras particiones](#Montar_otras_particiones)
*   [5 Excluir ficheros](#Excluir_ficheros)
*   [6 Script para la copia de seguridad](#Script_para_la_copia_de_seguridad)

## Descripción

Respaldar con tar tiene la ventaja de usar compresión que puede ayudar a guardar espacio en disco, y aportar simplicidad. El proceso solo requiere varios pasos, que son:

1.  Arrancar desde un LiveCD
2.  Pasar al entorno enjaulado de la instalación Linux.
3.  Montar (si hubiesen) otras particiones/discos
4.  Añadir exclusiones
5.  Use el script de respaldo para hacer la copia de seguridad

Para reducir al mínimo la inactividad la copia de seguridad puede alternativamente realizarse en un sistema en ejecución usando [instantáneas LVM](/index.php/LVM_(Espa%C3%B1ol)#Instant.C3.A1neas.2FSnapshots "LVM (Español)"), si todos los sistemas de archivos están montados en volúmenes LVM.

## Arrancar con LiveCD

Muchos LiveCD, USBs... tienen la capacidad de dejarle cambiar al entorno enjaulado de su instalación. Aunque no es requisito montar una jaula para hacer la copia de seguridad, esto proporciona la capacidad para ejecutar el script sin tener que pasarlo a un dispositivo de almacenamiento temporal o tener que ubicarlo en el sistema de archivos. El medio vivo debe compartir con la instalación linux la misma arquitectura (por. ej: i686 o x86_64).

## Cambiar a un entorno enjaulado

Lo primero que debería tener es un entorno de scripting en su instalación Linux. Si no sabe lo que es, significa que puede ejecutar cualquier script que pueda tener como si fuera un programa normal. Si no pudiese, vea este [artículo](http://linuxtidbits.wordpress.com/2009/12/03/setting-up-a-scripting-environment/) para saber como hacerlo. Lo siguiente que necesita es pasar al entorno enjaulado, para aprender más sobre este proceso, lea [esto](/index.php/Change_root_(Espa%C3%B1ol) "Change root (Español)"). Dentro de una jaula, no necesita ningún sistema de archivos temporal (<tt>/proc</tt>, <tt>/sys</tt>, and <tt>/dev</tt>). Estos sistemas de archivos se inicializan durante el arranque y en verdad no debe hacer una copia de ellos, ya que pueden interferir con la correcta (y necesaria) inicialización del sistema, que puede cambiar con cualquier actualización. Para cambiar al entorno enjaulado, tiene que montar la partición raíz de su instalación Linux. Por ejemplo:

```
mkdir /mnt/arch
mount /dev/<su partición o disco>

```

Use `fdisk -l` para descubrir sus particiones y discos. Una vez lo sepa, ejecute `chroot`:

```
cd /mnt/arch
chroot . /bin/bash

```

Este ejemplo claramente usa bash pero puede utilizar otros intérpretes si están disponibles. Ahora se encontrará en su entorno de scripting (esto es dado que se haya cargado el archivo de configuración `~/.bashrc` al entrar en la jaula):

```
cat ~/.bash_profile
# Si usa bash, carga la configuración del archivo local .bashrc
source ~/.bashrc

```

## Montar otras particiones

Otras particiones que use tendrán que ser montadas en su ubicaciones correspondientes (p. ej: si tiene una partición <tt>/home</tt> separada).

## Excluir ficheros

`tar` tiene la capacidad de ignorar ciertos ficheros y carpetas. La sintaxis requiere colocar cada archivo o carpeta a ignorar en una línea distinta. `tar` también tiene la capacidad de entender expresiones regulares (regexps). Por ejemplo:

```
# No copias antiguas                                                               
/opt/backup/arch-full*                                                                   

# No archivos temporales                                                           
/tmp/*

# No la cache del pacman
/var/cache/pacman/pkg/
...

```

## Script para la copia de seguridad

Respaldar con tar es un proceso directo. Aquí tiene un script básico que puede hacerlo y que hace además unas cuantas comprobaciones. Tendrá que modificar este script definiendo la ubicación donde poner la copia, los ficheros a excluir (si tiene alguno), y ejecutarlo una vez haya pasado al entorno `chroot` y montado todas las particiones.

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

# Exclusión de ubicación de fichero
prog=${0##*/} # Nombre de programa del nombre del archivo
excdir="/home/<user>/.bin/root/backup"
exclude_file="$excdir/$prog-exc.txt"

# Comprobación de jaula
echo -n "Recuerde hacer chroot desde un LiveCD.  ¿Ejecutar la copia de seguridad? (S/n): "
read executeback

# Comprobar si el fichero de exclusión existe
if [ ! -f $exclude_file ]; then
  echo -n "No existen ningún fichero excluido, ¿continuar? (S/n): "
  read continue
  if [ $continue == "n" ]; then exit; fi
fi

if [ $executeback = "y" ]; then
  tar --exclude-from=$exclude_file -czpvf $backupfile /
fi

```