## Contents

*   [1 AutoFS](#AutoFS)
    *   [1.1 ¿Qué es?](#.C2.BFQu.C3.A9_es.3F)
    *   [1.2 Instalación](#Instalaci.C3.B3n)
    *   [1.3 Notas](#Notas)
*   [2 Gestor de medios de XFCE](#Gestor_de_medios_de_XFCE)
    *   [2.1 ¿Qué es?](#.C2.BFQu.C3.A9_es.3F_2)
    *   [2.2 Requisitos e instalación](#Requisitos_e_instalaci.C3.B3n)
    *   [2.3 Notas](#Notas_2)

## AutoFS

Basado en información encontrada en este hilo: [https://bbs.archlinux.org/viewtopic.php?t=7630](https://bbs.archlinux.org/viewtopic.php?t=7630)
e información encontrada en esta página: [http://libranet.com/support/2.8/0381](http://libranet.com/support/2.8/0381)

### ¿Qué es?

Este documento esboza el procedimiento necesario para configurar AutoFS, un paquete utilizado por automount. Proporciona la capacidad de que los CD, los disquetes, y otros medios removibles se monten automáticamente según son insertados.

### Instalación

*   Instale el paquete autofs:

```
pacman -S autofs

```

*   Edite el archivo `/etc/autofs/auto.master`. Borre su contenido y añada después la siguiente línea:

```
/media /etc/autofs/auto.media

```

Cree ahora una línea adicional al final del archivo (pulse ENTER justo después de la última palabra). Si no hay una línea EOF correcta, el demonio AUTOFS no funcionará correctamente.

Si Autofs no desmonta automáticamente sus dispositivos (justo después de realizar los pasos que aquí se detallan), reemplace la última línea por:

```
/media /etc/autofs/auto.media --timeout 3

```

*   Cree el archivo /etc/autofs/auto.media con el siguiente contenido:

```
 cdrom -fstype=iso9660,ro,nodev,nosuid :/dev/cdrom
 floppy -fstype=auto,async,nodev,nosuid,umask=000 :/dev/fl
 usbstick -fstype=auto,async,nodev,nosuid,umask=000 :/dev/sda1

```

Puede que tenga que cambiar los dispositivos. Puede añadir también dispositivos similares adicionales. Si tiene un DVD-ROM y necesita el sistema de archivos UDF cambie la línea del cdrom anterior añadiendo "-fstype=auto".

*   Cree el archivo `/etc/default/autofs` y añádale la siguiente línea:

```
TIMEOUT=1

```

*   Abra el archivo `/etc/conf.d/autofs` y edite la línea de las daemonoptions:

```
daemonoptions='-g'

```

*   Cree el directorio `/media`:

```
mkdir /media

```

*   Puede que tenga que cargar el módulo autofs4:

```
modprobe autofs4

```

*   Arranque el demonio autofs usando:

```
/etc/rc.d/autofs start

```

*   Inicie este demonio en cada arranque añadiendo `autofs` al array DAEMONS en /etc/rc.conf. (Puede que también necesite añadir `autofs4` al array de módulos.)

Los dispositivos se montan ahora automáticamente cuando se accede a ellos. Visite los directorios /media/cdrom y /media/floppy para acceder a ellos. Se mantendrán montados tanto tiempo como se esté accediendo a ellos.

Si navega al directorio /media directory en un administrador de archivos, no verá entradas de directorio ni para el cdrom ni para la disquetera. Estas entradas estarán presentes con ningún medio en el dispositivo. Esto significa que en el navegador de archivos podrá ver qué dispositivos son susceptibles de ser montados, pero los directorios estarán vacios si no hay un medio presente. Aparentemente no todos los gestores de archivos pueden manejar el caso en que no exista un directorio.

### Notas

Si utiliza varios dispositivos usb y quiere diferenciarlos fácilemente, puede usar Autofs para configurar los puntos de montaje y a udev para crear distintos nombres para cada uno de sus dispositivos usb. [Map Custom Device Entries with udev (Inglés)](/index.php/Map_Custom_Device_Entries_with_udev "Map Custom Device Entries with udev") tiene instrucciones sobre cómo configurar reglas para udev.

Si autofs no le funciona, asegúrese de que son correctos los permisos de los archivos de autofs, de otro modo autofs no se iniciará. Esto puede suceder si usted hizo una copia de respaldo de sus archivos de configuración de manera que no se conservaran los modos de los archivos. A continuación puede ver como deberían ser los modos de los archivos de configuración:

0644 - /etc/autofs/auto.master

0644 - /etc/autofs/auto.media

0644 - /etc/autofs/auto.misc

0755 - /etc/autofs/auto.net

0644 - /etc/conf.d/autofs

## Gestor de medios de XFCE

Aquellos usuarios del entorno de escritorio XFCE, podrían considerar la utilización del gestor de medios propio del entorno en vez de Automount. Sin tan siquiera tener instalado automount, xfce puede automáticamente, detectar, montar y abrir medios, tales como dispositivos usb o CDs.

### ¿Qué es?

El gestor de medios es manejado por Thunar, de manera que tendrá que utilizar éste, en contraste con XFFM (a menos que configure ambos para correr juntos, no cubierto aquí). El plugin se llama 'Thunar Volume Manager', se puede obtener más información en [http://foo-projects.org/~benny/projects/thunar-volman/](http://foo-projects.org/~benny/projects/thunar-volman/).

### Requisitos e instalación

```
- XFCE, con Thunar
- Thunar Volume Manager plugin (obtenido de [http://foo-projects.org/~benny/projects/thunar-volman/](http://foo-projects.org/~benny/projects/thunar-volman/))
- Dbus
- Hal

```

El plugin puede ser instalado manualmente, o a través de pacman con:

```
sudo pacman -S thunar-volman

```

Después de instalar el plugin, abra el gestor de configuración de XFCE, y en él, las preferencias del gestor de archivos. Bajo la columna 'Avanzadas', compruebe 'Habilitar gestión de medios'. Haga click en "configurar". La configuración es sencilla. Aquí tiene un ejemplo que hace que Amarok reproduzca un CD de audio.

Multimedia - Audio CDs: amarok --cdplay %d

### Notas

Es esencial tener corriendo los demonios Hal y Dbus, de otro modo el gestor de medios no detectará nada. Esto puede parecer obvio, pero ha habido gente quejándose y preguntando por qué no funcionaba y todo el asunto residía en que no estaban corriendo estos dos demonios. Asegúrese también de que pertenece usted a los grupos storage y optical.

Para poner a funcionar Hal y Dbus en el arranque simplementee edita /etc/rc.conf y añade 'hal' y 'dbus' a los [daemons](/index.php/Daemons "Daemons"): DAEMONS=( ... hal dbus ... ). Obtenga más información sobre [Daemons (Inglés)](/index.php/Daemons "Daemons").