**Estado de la traducción**
Este artículo es una traducción de [FuseISO](/index.php/FuseISO "FuseISO"), revisada por última vez el **2018-11-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=FuseISO&diff=0&oldid=554486) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[FuseISO](https://sourceforge.net/projects/fuseiso/) es un módulo [FUSE (Español)](/index.php/FUSE_(Espa%C3%B1ol) "FUSE (Español)") para permitir a los usuarios sin privilegios de root montar imágenes del sistema de archivos [ISO](https://en.wikipedia.org/wiki/es:ISO_9660 "wikipedia:es:ISO 9660") (*.iso*, *.nrg*, *.bin*, *.mdf* y *.img*).

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Utilización](#Utilizaci.C3.B3n)
    *   [2.1 Montaje](#Montaje)
    *   [2.2 Desmontaje](#Desmontaje)
*   [3 Desmontaje](#Desmontaje_2)
    *   [3.1 Archivos de GNOME](#Archivos_de_GNOME)
    *   [3.2 Nemo](#Nemo)

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [fuseiso](https://www.archlinux.org/packages/?name=fuseiso).

## Utilización

### Montaje

Para montar una imagen:

```
$ fuseiso *image* *directory*

```

El punto de montaje de destino debe poder escribirse y no debe tener otros archivos o dispositivos montados.

Ejecute `fuseiso -h` para conocer todas las opciones disponibles.

### Desmontaje

Para desmontar la imagen:

```
$ fusermount -u *directory*

```

La orden se puede utilizar para desconectar otros dispositivos de almacenamiento montados por otras herramientas de montaje.

## Desmontaje

### Archivos de GNOME

Para los usuarios de GNOME, hay una forma fácil de usar fuseiso desde el menú contextual de nautilus.

Primero necesitará el paquet [filemanager-actions](https://www.archlinux.org/packages/?name=filemanager-actions), luego deberá guardar los siguientes scripts en una carpeta de su elección (por ejemplo, `~/.local/bin/`):

 `filemanager-actions-iso-mount.sh` 
```
 #!/bin/bash

 FILE=$(basename "$1")
 MOUNTPOINT="$HOME/Desktop/$FILE"

 fuseiso -p "$1" "$MOUNTPOINT"

```
 `filemanager-actions-iso-umount.sh` 
```
 #!/bin/bash

 FILE=$(basename "$1")
 MOUNTPOINT="$HOME/Desktop/$FILE"

 fusermount -u "$MOUNTPOINT"

```

Hága ejecutables los scripts:

```
$ chmod +x /*ruta_a_los_scripts*/filemanager-actions-iso-*

```

Ahora, inicie *fma-config-tool* (*Sistema> Preferencias> Configuración de acciones de Nautilus*).

Añada una nueva acción con la siguiente configuración:

*   Etiqueta: *Mount ISO*
*   Icono: un símbolo de su elección (por ejemplo: *gtk-cdrom*)
*   Ruta: `/'ruta_a_los_scripts*/filemanager-actions-iso-mount.sh*`
*   Parámetros: *%F*
*   Directorio de trabajo: *%d*
*   Basenames: **.iso ; *.nrg ; *.bin ; *.img ; *.mdf (para cada uno agregue una entrada separada)*
*   Caso de coincidencia: *"must match one of"*
*   Mimetypes: **/**

Con esta acción puede montar imágenes ISO en su escritorio. Creará una carpeta en ~/Escritorio con el nombre de la imagen iso. fuseiso montará la iso a dicha carpeta.

Añada una segunda acción:

*   Etiqueta: *Unmount ISO*
*   Icono: un símbolo de su elección (por ejemplo *gtk-cdrom*)
*   Ruta: `/*path_to_scripts*/filemanager-actions-iso-umount.sh`
*   Parámetros: *%F*
*   Directorio de trabajo directory: *%d*
*   Basenames: **.iso ; *.nrg ; *.bin ; *.img ; *.mdf (para cada uno agregue una entrada separada)*
*   Caso de coincidencia: *"must match one of"*
*   Mimetypes: **/**

Esta segunda acción desmontará la iso montada y eliminará la carpeta del escritorio.

A veces, debe cerrar la sesión para poder montar cualquier imagen de los tipos dados, simplemente haciendo clic con el botón secundario sobre Archivos y seleccionando *Montar ISO*. Para volver a desmontarlo, haga clic con el botón secundario sobre la carpeta correspondiente de su escritorio y seleccione *Desmontar ISO*.

### Nemo

[Nemo](/index.php/Nemo "Nemo") como explorador de archivos tiene una función empaquetada al hacer clic con el botón secundario para montar una iso. El desmontaje se realiza haciendo clic en el icono respectivo de la ISO montada, tal como lo haría con las unidades USB.