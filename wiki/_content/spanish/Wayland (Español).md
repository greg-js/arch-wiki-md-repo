**Wayland** es un nuevo protocolo para gestionar ventanas para Linux. La utilización de Wayland requiere cambios y reinstalación de partes del software del sistema. Para obtener más información sobre Wayland vea esta [página](http://wayland.freedesktop.org/).

**Advertencia:** Wayland está en fuerte desarrollo. La ayuda técnica no se puede garantizar y puede que no funcione como se esperaba.

## Contents

*   [1 Requisitos](#Requisitos)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Utilización](#Utilizaci.C3.B3n)
*   [4 Weston](#Weston)
    *   [4.1 Instalación](#Instalaci.C3.B3n_2)
    *   [4.2 Utilización](#Utilizaci.C3.B3n_2)
    *   [4.3 Configuración](#Configuraci.C3.B3n)
        *   [4.3.1 XWayland](#XWayland)
*   [5 Bibliotecas GUI](#Bibliotecas_GUI)
    *   [5.1 GTK+](#GTK.2B)
    *   [5.2 Qt5](#Qt5)
    *   [5.3 Clutter](#Clutter)
    *   [5.4 SDL](#SDL)
    *   [5.5 EFL](#EFL)
*   [6 Gestores de ventanas y shells de escritorios](#Gestores_de_ventanas_y_shells_de_escritorios)
    *   [6.1 KDE](#KDE)
    *   [6.2 GNOME](#GNOME)
    *   [6.3 i3](#i3)
    *   [6.4 Wayland puro](#Wayland_puro)
        *   [6.4.1 Wayland, DRM, Pixman, libxkbcommon](#Wayland.2C_DRM.2C_Pixman.2C_libxkbcommon)
        *   [6.4.2 Mesa](#Mesa)
        *   [6.4.3 cairo](#cairo)
        *   [6.4.4 weston](#weston_2)
*   [7 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [7.1 LLVM assertion failure](#LLVM_assertion_failure)
*   [8 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Requisitos

Actualmente Wayland solo funciona en sistemas que utilizan [KMS](/index.php/Kernel_Mode_Setting_(Espa%C3%B1ol) "Kernel Mode Setting (Español)").

## Instalación

Wayland es muy posible que ya se encuentre instalado en su sistema dado que es una dependencia indirecta de [gtk2](https://www.archlinux.org/packages/?name=gtk2) y [gtk3](https://www.archlinux.org/packages/?name=gtk3). Si no está instalado, busque el paquete [wayland](https://www.archlinux.org/packages/?name=wayland) en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Utilización

Como Wayland es solo una biblioteca, es inoperativo por sí mismo. Para usarlo, necesita un compositor (como Weston), aplicaciones demo de Weston, QT5 con complementos de Wayland y/o GTK+ con soporte para Wayland.

## Weston

### Instalación

Necesita instalar [weston](https://www.archlinux.org/packages/?name=weston) disponible en los repositorios oficiales.

### Utilización

<caption>_**Atajos del teclado**_
**Nota:**<small>

*   super = tecla windows - se puede cambiar, ver weston.ini `Ctrl-b`
*   LMB (left mouse buton)=botón secundario ratón; MMB (mid mouse buton)=botón central ratón; RMB (right mouse buton)=botón principal ratón

</small>

</caption>
| Combinación | Acción |
| Ctrl + Alt + Retroceso | Salir de Weston |
| Super + Bloq Despl (o RePág/AvPág ) | Zoom del escritorio |
| Super + Tab | Cambiar entre ventanas |
| Super + LMB | Mover la ventana |
| Super + MMB | Redimensionar la ventana |
| Super + RMB | ¡Girar la ventana! |
| Super + Tab | Cambiar entre ventanas |
| Super + K | Forzar el cierre de la ventana activa |
| Super + KeyUp/KeyDown | Cambiar entre el anterior/siguiente espacio de trabajo |
| Super + Mayús + KeyUp/KeyDown | Grab Current Window and Switch Workspace |
| Super + F_**n**_ | Cambiar entre espacios de trabajo _**n**_ |

Ahora que Wayland se ha instalado con sus requisitos, se está listo para probarlo.

**Nota:**

El usuario necesita estar en el grupo de vídeo para iniciar Weston; esta orden se supone que no se ejecuta como root y ¡si lo hace puede congelar su VT!

Es posible ejecutar Weston dentro de una sesión X en ejecución:

```
$ weston

```

Por otra parte, para poner en marcha de forma nativa Weston, pruebe cambiando de terminal y ejecutar:

```
$ weston-launch

```

Luego, en una TTY dentro de Weston, puede ejecutar las demos.

Para ejecutar un emulador de terminal :

```
$ weston-terminal

```

Para mover flores alrededor de la pantalla :

```
$ weston-flower 

```

Para poner a prueba el protocolo frame (se ejecuta `glxgears`):

```
$ weston-gears

```

Para visualizar imágenes:

```
$ weston-image image1.jpg image2.jpg...

```

Para visualizar archivos PDF :

```
$ weston-view doc1.pdf doc2.pdf...

```

### Configuración

He aquí un archivo de configuración de ejemplo para la distribución del teclado, la selección de módulos y modificaciones de la interfaz de usuario. Vea `man weston.ini` para obtener los detalles completos:

 `~/.config/weston.ini` 

```
[core]
### Descomentar esta línea para dar soporte a «xwayland» ###
#modules=desktop-shell.so,xwayland.so

[shell]
background-image=/usr/share/backgrounds/gnome/Aqua.jpg
background-color=0xff002244
panel-color=0x90ff0000
locking=true
animation=zoom
#binding-modifier=ctrl
#num-workspaces=6
### Para los temas del cursor instale el paquete «xcursor-themes» desde Extra ###
#cursor-theme=whiteglass
#cursor-size=24

### Opciones de tablet ###
#lockscreen-icon=/usr/share/icons/gnome/256x256/actions/lock.png
#lockscreen=/usr/share/backgrounds/gnome/Garden.jpg
#homescreen=/usr/share/backgrounds/gnome/Blinds.jpg
#animation=fade

[keyboard]
keymap_rules=evdev
#keymap_layout=es
#keymap_options=caps:ctrl_modifier,shift:both_capslock_cancel
### keymap_options obtenidas desde /usr/share/X11/xkb/rules/base.lst ###

[terminal]
#font=DroidSansMono
#font-size=14

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/gnome-terminal

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/hicolor/24x24/apps/firefox.png
path=/usr/bin/firefox

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/arts.png
path=./clients/flower

[screensaver]
# Descomentar path para desactivar el salvapantallas
path=/usr/libexec/weston-screensaver
duration=600

[input-method]
path=/usr/libexec/weston-keyboard

###  Para pantallas de portátiles  ###
#[output]
#name=LVDS1
#mode=1680x1050
#transform=90

#[output]
#name=VGA1
# Lo siguiente establece la modalidad con un modeline, puede obtener modeline para sus resoluciones preferidas mediante la utilidad cvt
#mode=173.00 1920 2048 2248 2576 1080 1083 1088 1120 -hsync +vsync
#transform=flipped

#[output]
#name=X1
#mode=1024x768
#transform=flipped-270

```

Configuración mínima de `weston.ini` :

 `~/.config/weston.ini` 

```
[core]
modules=desktop-shell.so,xwayland.so

[keyboard]
keymap_layout=es

[launcher]
icon=/usr/share/icons/gnome/24x24/apps/utilities-terminal.png
path=/usr/bin/weston-terminal

[launcher]
icon=/usr/share/icons/hicolor/24x24/apps/firefox.png
path=/usr/bin/firefox

[output]
name=LVDS1
mode=1680x1050
transform=90

```

#### XWayland

XWayland _es_ un servidor XOrg y se compila igual que al que sustituye. La única diferencia es que se obtiene de la rama Wayland del repositorio xorg-server y como tal tiene las extensiones de Wayland. Estas extensiones permiten que se ejecute como un cliente de Weston.

Cuando se quiere ejecutar una aplicación X desde Weston, se gira hacia el servidor X modificado para atender la solicitud.

**Advertencia:** Los pasos de esta sección se dirigen _a reemplazar su entramado de gráficos_. Una instalación incompleta puede dar lugar a un entorno gráfico roto.

Si piensa ejecutar aplicaciones nativas de X dentro de Wayland, entonce tiene que instalar [xorg-server-dev](https://aur.archlinux.org/packages/xorg-server-dev/). Después de eso, cree o modifique el siguiente archivo de configuración:

 `~/.config/weston.ini` 

```
[core]
modules=xwayland.so,desktop-shell.so

```

A partir de ahora se podrían también ejecutar aplicaciones X en una especie de «modo de compatibilidad». El apoyo definitivo a XWayland debería estar disponible con la liberación de la versión 1.16 del servidor X, que no verá la luz hasta [mediados de 2014](http://www.phoronix.com/scan.php?page=news_item&px=MTQ1NzM).

Los paquetes de AUR pueden requerir algunas modificaciones con el fin de compilar correctamente, para lo cual ([mire este hilo](https://bbs.archlinux.org/viewtopic.php?pid=1328812#p1328812)).

## Bibliotecas GUI

(Veánse los detalles en la [página oficial](http://wayland.freedesktop.org/toolkits.html))

### GTK+

Se necesita instalar [gtk3](https://www.archlinux.org/packages/?name=gtk3) disponible en los repositorios oficiales, que ahora tiene el backend Wayland activado.

Con GTK+ 3.0, GTK+ proporciona apoyo para multiples backends ejecutables en tiempo real que pueden cambiar entre sí, de la misma manera que Qt puede hacerlo con lighthouse.

Cuando ambos backends, Wayland y X, están activados, GTK+ de forma predeterminada utiliza el backend X11, pero esto puede ser anulado por la modificación de una variable de entorno: `GDK_BACKEND=wayland`.

### Qt5

Tiene que hacerse o bien ~~recompilando [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) con _-opengl es2_~~ (actualmente no funciona, véase [http://lists.qt-project.org/pipermail/development/2013-December/014789.html](http://lists.qt-project.org/pipermail/development/2013-December/014789.html) ) o bien utilizando [qtbase-git](https://aur.archlinux.org/packages/qtbase-git/). Después compile el complemento [qtwayland-git](https://aur.archlinux.org/packages/qtwayland-git/) de wayland.

Para ejecutar una aplicación Qt5 con el complemento de Wayland, establezca `QT_QPA_PLATFORM=wayland-egl`.

### Clutter

El conjunto de herramientas de Clutter tiene un backend Wayland que permite que se ejecute como cliente de Wayland. El backend está activado en el paquete oficial disponible en Extra.

Para ejecutar una aplicación de Clutter en Wayland, establezca `CLUTTER_BACKEND=wayland`.

### SDL

El apoyo experimental a Wayland se encuentra ahora en SDL 2.0.2 y está activado por defecto en Arch Linux.

Para ejecutar una aplicación de SDL en Wayland, establezca `SDL_VIDEODRIVER=wayland`.

### EFL

EFL tiene soporte completo para Wayland.

Para ejecutar una aplicación de EFL en Wayland, vea la [página del proyecto](http://wayland.freedesktop.org/efl.html) de Wayland.

## Gestores de ventanas y shells de escritorios

### KDE

KDE 4.11 beta permite iniciar [KWin bajo el compositor del sistema Wayland](http://blog.martin-graesslin.com/blog/2013/06/starting-a-full-kde-plasma-session-in-wayland/). Actualmente no existe soporte para el uso de KWin como compositor de sesión.

### GNOME

Desde la versión 3.10, Gnome tiene soporte experimental Wayland, pero se debe instalar [xwayland-git](https://aur.archlinux.org/packages/xwayland-git/) y el parche equivalente del controlador de la tarjeta gráfica, por ejemplo [xf86-video-intel-xwayland-git](https://aur.archlinux.org/packages/xf86-video-intel-xwayland-git/) para hacer que _Mutter_ funcione. Para más detalles mire en [GNOME wiki](https://live.gnome.org/Initiatives/Wayland) .

 `gnome-session --session=gnome-wayland` 

### i3

Algunos desarrolladores de i3 han [esbozado un proyecto completamente nuevo](http://www.i3way.org/) para implementar un complemento de shell para Weston a fin de conservar las mismas características y estilo de i3.

### Wayland puro

**Advertencia:** He aquí algunas notas breves sobre cómo instalar Wayland puro (sin X11) en un sistema Arch Linux. Este es obtenido desde su fuente e instalado en `/usr/local`. Puede romper el sistema. Considérese advertido.

Primero instale un sistema base de Arch Linux con base y base-devel. No instale xorg o cualquiera de sus bibliotecas.

#### Wayland, DRM, Pixman, libxkbcommon

```
$ pacman -S wayland libdrm pixman libxkbcommon

```

#### Mesa

```
$ sudo pacman -S python2 libxml2 llvm
$ git clone [git://anongit.freedesktop.org/mesa/mesa](git://anongit.freedesktop.org/mesa/mesa)
$ cd mesa
$ CFLAGS=-DMESA_EGL_NO_X11_HEADERS ./autogen.sh --prefix=/usr/local --enable-gles2 --disable-gallium-egl --with-egl-platforms=wayland,drm --enable-gbm --enable-shared-glapi --with-gallium-drivers=r300,r600,swrast,nouveau --disable-glx --disable-xlib
$ make
$ sudo make install

```

#### cairo

**Nota:** Sin glx/gl o xcb. Únicamente EGL.

```
$ pacman -S libpng
$ git clone [git://anongit.freedesktop.org/cairo](git://anongit.freedesktop.org/cairo)
$ cd cairo
$ CFLAGS=-DMESA_EGL_NO_X11_HEADERS ./autogen.sh --prefix=/usr/local/  --disable-xcb  --enable-glesv2 
$ make
$ sudo make install

```

#### weston

```
$ sudo pacman -S gegl mtdev
_(selecciones mesa-gl en options para libgl)_
$ git clone [git://anongit.freedesktop.org/wayland/weston](git://anongit.freedesktop.org/wayland/weston)
$ cd weston/
$ CFLAGS="-DMESA_EGL_NO_X11_HEADERS" ./autogen.sh --prefix=/usr/local/ --with-cairo-glesv2 --disable-xwayland --disable-x11-compositor --disable-xwayland-test
$ make
$ sudo make install

```

## Solución de problemas

### LLVM assertion failure

Si obtiene un error de «LLVM assertion failure», necesita recompilar [mesa](https://www.archlinux.org/packages/?name=mesa) sin Gallium LLVM hasta que se solucione este problema.

Esto puede implicar la desactivación de algunos controladores que requiere LLVM. También puede tratar de exportar lo siguiente, si tiene problemas con los controladores del hardware:

```
$ export EGL_DRIVER=/usr/lib/egl/egl_gallium.so

```

## Véase también

*   [Cursor Themes](/index.php/Cursor_Themes "Cursor Themes")
*   [Arch Linux forum discussion](https://bbs.archlinux.org/viewtopic.php?id=107499)
*   [Wayland documentation online](http://wayland.freedesktop.org/docs/html/)
*   [Wayland usability wiki](http://www.chaosreigns.com/wiki/Wayland_State)