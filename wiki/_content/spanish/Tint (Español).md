## Contents

*   [1 Introducción](#Introducci.C3.B3n)
    *   [1.1 Características](#Caracter.C3.ADsticas)
    *   [1.2 Requerimientos](#Requerimientos)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 PKGBUILD de AUR](#PKGBUILD_de_AUR)
    *   [2.2 Compilando desde el código fuente](#Compilando_desde_el_c.C3.B3digo_fuente)
    *   [2.3 Otros metodos de instalacion](#Otros_metodos_de_instalacion)
*   [3 Ejecutando Tint](#Ejecutando_Tint)
*   [4 Otros Recursos](#Otros_Recursos)

## Introducción

Desde [homepage](http://code.google.com/p/ttm/):

_ttm es un panel_ _ttm is a simple panel/barra de tareas creado para openbox3, pero también funciona con otros manejadores de ventanas. Esta bajo desarrollo así que por favor informar errores:)_

### Características

*   background button-border effect (see screenshot)
*   font shadow
*   option to center tasks
*   option to change panel width/height
*   tasks do now squeeze (more or less) when they hit panel edge
*   middle-click closes window
*   left-click toggles shade

### Requerimientos

Con el fin de tomar la última (SVN) instantánea de código fuente de tinte, tendrá que instalar el paquete subversion (un sistema de control de versiones):

```
# pacman -S subversion

```

## Instalación

### PKGBUILD de AUR

El paquete de Tint2 [PKGBUILD](https://aur.archlinux.org/packages.php?ID=40739) esta disponible en [AUR](/index.php/AUR "AUR"). Creelo con [Makepkg](/index.php/Makepkg "Makepkg") e instalelo con pacman.

El archivo de configuración sera creado con la primera ejecución de tint2 en .config/tint/tintrc

### Compilando desde el código fuente

Abra su terminal favorita e ingrese:

```
$ svn checkout [http://ttm.googlecode.com/svn/trunk/](http://ttm.googlecode.com/svn/trunk/) ttm
$ cd ./ttm/src
$ make
$ sudo make install

```

Ahora copie la configuración de ejemplo:

```
$ cd ..
$ mkdir -p ~/.config/tint/
$ cp config_sample ~/.config/tint/tintrc

```

### Otros metodos de instalacion

Edite su archivo /etc/pacman.conf y agregue:

```
[rfad]
# Repository made by haxit | Contact: requiem [at] archlinux.us for package suggestions!
Server = [http://web.ncf.ca/ey723/archlinux/repo/](http://web.ncf.ca/ey723/archlinux/repo/)

```

Y luego ejecute el siguiente comando:

```
pacman -S tint

```

## Ejecutando Tint

Ahora puede iniciar Tint como cualquier otra aplicación (Por ejempo: Alt+F2 -> tint). Para ejecutarlo al inicio, puede agregarlo en el archivo ~/.xinitrc, o en ~/.config/openbox/autostart.sh, por ejemplo:

```
xscreensaver -no-splash &
eval `cat $HOME/.fehbg` &
conky &
visibility &
_**tint &**_
exec openbox-session

```

## Otros Recursos

[Tint 0.6 Documentation (PDF)](http://tint2.googlecode.com/files/tint-0.6.pdf)

[Tint2 0.7 Documentation (PDF)](http://tint2.googlecode.com/files/tint2-0.7.pdf)