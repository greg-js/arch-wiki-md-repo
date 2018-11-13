*Un pequeño tutorial para la instalación de paquetes sin conexión a internet. Esta basado en la publicación del usuario [Byte](/index.php/User:Byte "User:Byte") de [este](https://bbs.archlinux.org/viewtopic.php?id=30431) hilo del foro, y usa KDE como ejemplo.*

## Contents

*   [1 Método](#Método)
*   [2 A slightly contrived example](#A_slightly_contrived_example)
    *   [2.1 Generar una lista de los paquetes a descargar](#Generar_una_lista_de_los_paquetes_a_descargar)
    *   [2.2 Descarga de los paquetes y sus dependencias](#Descarga_de_los_paquetes_y_sus_dependencias)
    *   [2.3 Crear una base de datos de repositorios solo para esos paquetes](#Crear_una_base_de_datos_de_repositorios_solo_para_esos_paquetes)
    *   [2.4 Transferir los paquetes](#Transferir_los_paquetes)
    *   [2.5 Instalar los paquetes](#Instalar_los_paquetes)
    *   [2.6 Enlaces y fuentes](#Enlaces_y_fuentes)

## Método

Descargar los paquetes de las bases de datos en una computadora con conexión a internet y transferirlos a la máquina a instalar:

Para i686:

*   [ftp://ftp.archlinux.org/core/os/i686/core.db.tar.gz](ftp://ftp.archlinux.org/core/os/i686/core.db.tar.gz)
*   [ftp://ftp.archlinux.org/extra/os/i686/extra.db.tar.gz](ftp://ftp.archlinux.org/extra/os/i686/extra.db.tar.gz)
*   [ftp://ftp.archlinux.org/community/os/i686/community.db.tar.gz](ftp://ftp.archlinux.org/community/os/i686/community.db.tar.gz)

Para x86_64:

*   [ftp://ftp.archlinux.org/core/os/x86_64/core.db.tar.gz](ftp://ftp.archlinux.org/core/os/x86_64/core.db.tar.gz)
*   [ftp://ftp.archlinux.org/extra/os/x86_64/extra.db.tar.gz](ftp://ftp.archlinux.org/extra/os/x86_64/extra.db.tar.gz)
*   [ftp://ftp.archlinux.org/community/os/x86_64/community.db.tar.gz](ftp://ftp.archlinux.org/community/os/x86_64/community.db.tar.gz)

Los siguientes pasos aseguran que se está trabajando con una lista de paquetes al día, como si se ejecutara (online) `pacman -Sy`.

En el equipo PC, hacer lo siguiente como superusuario (root):

```
cd /var/lib/pacman/
mkdir -p sync
cd sync

mkdir -p core
rm -r core/*
cd core
tar -xzf {path-to-download}/core.db.tar.gz

cd ..
mkdir -p extra
rm -r extra/*
cd extra
tar -xzf {path-to-download}/extra.db.tar.gz

cd ..
mkdir -p community
rm -r community/*
cd community
tar -xzf {path-to-download}/community.db.tar.gz

```

```
pacman -Sp --noconfirm {package-name} > pkglist

```

**Sugerencia:** Asegurarse de tener habilitado al menos uno de los servidores definidos en el archivo /etc/pacman.d/mirrorlist. Si no es así, el sistema devolverá el siguiente error: error: no database for package: {package-name}

Para actualizar un nuevo sistema base de Arch Linux después de una instalación, se ejecuta la siguiente orden:

pacman -Sup --noconfirm > pkglist

Después, se abre el archivo con un editor, y se borran las líneas que no son direcciones URL.

Posteriormente, se lleva esa lista a un equipo con conexión a internet, y se realiza la descarga de cada URL de forma manual, o ejecutando:

`wget -nv -i ../pkglist`

en un directorio vacío. Por último, se lleva los paquetes (archivos .pkg.tar.gz/xz) al directorio del equipo a instalar /var/cache/pacman/pkg, y para instalarlos se ejectuta:

```
pacman -S {package-name}

```

## A slightly contrived example

Ejemplo: teniendo dos máquinas con Archlinux, 'Al' (con conexión a internet) y 'Bob' (sin conexión a internet), y se necesita instalar los paquetes de Nvidia y sus dependencias en 'Bob'. Digamos que los paquetes de los que hablamos son nvidia, nvidia-utils y xf86-video-nouveau, y se desea usar un directorio dedicado en lugar de /var/cache/pacman/pkg/, creando un repositorio llamado 'nvidia' (en lugar de los usuales core, extra, etc).

### Generar una lista de los paquetes a descargar

Esto puede ser hecho por cualquier máquina que tenga instalado Archlinux y la base de datos de los repositorios actualizados (véase más arriba enlaces para los archivos de base de datos); para crear la lista de los enlaces de los paquetes requeridos usa:

```
pacman -Sp nvidia nvidia-utils xf86-video-nouveau > /path/to/nvidia.list

```

el archivo nvidia.list contendrá enlaces de los paquetes listados y de otros que son sus dependencias.

### Descarga de los paquetes y sus dependencias

Obviamente esto requiere una conexión a internet, entonces en 'Al' crea una carpeta llamada /path/to/nvidia para los archivos y ejecuta:

```
wget -P /path/to/nvidia/ -i /path/to/nvidia.list

```

### Crear una base de datos de repositorios solo para esos paquetes

Esto puede ser hecho en 'Al' o 'Bob' usando el comando repo-add que viene con pacman; primero, anda al directorio /path/to/nvidia donde habían sido descargados los paquetes, luego crea el paquete de base de datos llamado nvidia.db.tar.gz:

```
cd /path/to/nvidia
repo-add nvidia.db.tar.gz *.pkg.tar.gz

```

### Transferir los paquetes

Ahora que todos los paquetes han sido descargados, 'Al' deja de ser necesario. Se copia el contenido de /path/to/nvidia a una carpeta cache de paquetes de nvidia temporal en 'Bob', por ejemplo '/home/me/nvidia':

```
cp /path/to/nvidia/* /home/me/nvidia

```

Posterior a este paso, se debe informar a Pacman de la existencia de este nuevo repositorio; se realiza mediante la adición de las siguientes líneas en cualquier lugar del archivo **pacman.conf** (ubicado en /etc):

```
[nvidia]
Server = file:///home/me/nvidia

```

Ahora, se sincroniza Pacman para recibir la información del nuevo repositorio:

```
pacman -Sy 

```

Esta orden encuentra el archivo nvidia.db.tar.gz en /home/me/nvidia y lo expande a /var/lib/pacman/sync/nvidia, para crear una base de datos de paquetes contenidos en el repositorio nvidia.

### Instalar los paquetes

Finalmente se instalan los paquetes:

```
pacman -S nvidia nvidia-utils xf86-video nouveau

```

### Enlaces y fuentes

Esto es un compilado de los foros, gracias a [Heller_Barbe](https://bbs.archlinux.org/viewtopic.php?id=60856)) y [byte](https://bbs.archlinux.org/viewtopic.php?id=30431)