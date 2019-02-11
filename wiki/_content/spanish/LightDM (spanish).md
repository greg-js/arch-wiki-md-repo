Artículos relacionados

*   [Display Manager](/index.php/Display_Manager "Display Manager")

[Lightdm](http://www.freedesktop.org/wiki/Software/LightDM) LighDM es un gestor de sesión inter-escritorio que aspira a ser el estándar para el sistema de ventanas X11 y para [Wayland](/index.php/Wayland "Wayland").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Greeter](#Greeter)
    *   [1.2 Habilitar Lightdm](#Habilitar_Lightdm)
*   [2 Configuración](#Configuración)
    *   [2.1 Command line tool](#Command_line_tool)
        *   [2.1.1 Cambiando la imagen o color de fondo](#Cambiando_la_imagen_o_color_de_fondo)
            *   [2.1.1.1 GTK+ Greeter](#GTK+_Greeter)
            *   [2.1.1.2 Unity Greeter](#Unity_Greeter)
            *   [2.1.1.3 KDE Greeter](#KDE_Greeter)
    *   [2.2 Cambiando íconos](#Cambiando_íconos)
    *   [2.3 Habilitando el autologin](#Habilitando_el_autologin)

# Instalación

Se puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [lightdm](https://www.archlinux.org/packages/?name=lightdm) desde los repositorios oficiales-

**Sugerencia:** Lanzamientos estables tienen números pares (1.8, 1.10), lanzamientos en desarrollo tienen números impares (1.9, 1.11). Estos lanzamientos en desarrollo están disponibles con el paquete [lightdm-devel](https://aur.archlinux.org/packages/lightdm-devel/).

### Greeter

Después de instalar Ligthdm necesitarás instalar un Greeter (una interfaz de usuario para LightDM). Es posible usar LightDM sin un Greeter al configurar login automático.

Los repositorios oficiales contienes los siguientes Greeters:

*   [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter): el Greeter **recomendado** que LightDM intenta usar por defecto al no modificar ninguna configuracion.
*   [lightdm-kde-greeter](https://www.archlinux.org/packages/?name=lightdm-kde-greeter): Greeter usado en KDE4.
*   [deepin-session-ui](https://www.archlinux.org/packages/?name=deepin-session-ui) Lightdm-deepin-greeter: Un Greeter del proyecto [Deepin](/index.php/Deepin "Deepin").

Otros greeters que se pueden instalar mediante [AUR](/index.php/AUR "AUR") son:

*   [lightdm-webkit-greeter](https://aur.archlinux.org/packages/lightdm-webkit-greeter/): Un greeter que usa webkit.
*   [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/): El greeter usado por [Unity](/index.php/Unity "Unity") en Ubuntu.
*   [lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/): Un greeter para el proyecyo ElementaryOS.

Puedes cambiar el greeter por defecto cambiando la configuración del archivo:

 `/etc/lightdm/lightdm.conf` 
```
greeter-session=lightdm-yourgreeter-greeter

```

## Habilitar Lightdm

se habilita usando systemd, asegúrate de tener activado `lightdm.service` [using systemctl](/index.php/Systemd#Using_units "Systemd") para que se cargue automáticamente al inicio.

# Configuración

En caso de necesitarla, existe el archivo que está bien documentado y que contiene las opciones del LightDM, este está ubicado en:

```
/etc/lightdm.conf

```

## Command line tool

LightDM ofrece una herramienta para el shell, `dm-tool`, que puede ser usada para bloquear la sesión actual, intercambiar sesiones, etc, que es util con gestores de de escritorio 'minimalistas' y para testing. Para ver una lista completa de las opciones de esta herramienta:

```
$ dm-tool --help

```

### Cambiando la imagen o color de fondo

Los Usuarios que deseen tener un solo color plano (sin imagen) pueden solo ajustar la variable **background** a un color en formato Hexadecimal.

Por ejemplo:

```
background=#000000

```

Si por el contrario se desea usar una imagen, leer a continuación

#### GTK+ Greeter

Los Usuarios que deseen personalizar el wallpaper en la pantalla de este greeter, solo tienen que editar `/etc/lightdm/lightdm-gtk-greeter.conf` definiendo la variable **background**

Por ejemplo:

```
background=/usr/share/pixmaps/black_and_white_photography-wallpaper-1920x1080.jpg

```

#### Unity Greeter

Aquellos que usan [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/) tienen que editar el archivo `/usr/share/glib-2.0/schemas/com.canonical.unity-greeter.gschema.xml` y luego ejecutar:

```
# glib-compile-schemas /usr/share/glib-2.0/schemas/

```

De acuerdo con [this](https://bbs.archlinux.org/viewtopic.php?id=149945).

**Note:** Es recomendable colocar el archivo PNG or JPG en `/usr/share/pixmaps` puesto que el usuario LightDM necesita acceso de lectura al archivo de wallpaper.

#### KDE Greeter

Solo es necesario entrar a *System Settings > Login Screen (LightDM)* y cambiar la imagen de fondo para tu theme.

## Cambiando íconos

Usuarios que deseen cambiar el icono de Computador en el login deben seguir 3 pasos:

Copia la imagen a /usr/share/icons/hicolor/64x64/devices , se obvia que debe ser de 64x64. Ejecute gtk-update-icon-cache /usr/share/icons/hicolor Edite /usr/share/lightdm-gtk-greeter/greeter.ui Busque 'image1' y edite la 'propiedad' xml del archivo para apuntar a la imagen deseada (sin la extensión, lightdm la obvia), por defecto 'computer'.

Un buen lugar para encontrar iconos así es el paquete [archlinux-artwork] en extra, éste posee iconos varios en formato 64x64. Para copiarlos siga estas instrucciones:

1.  find /usr/share/archlinux/icons -name "*64*" -exec cp {} /usr/share/icons/hicolor/64x64/devices \;

Una vez copiados los iconos puede, si así lo desea, eliminar el paquete.

## Habilitando el autologin

Edite /etc/lightdm/lightdm.conf y cámbielo por algo como esto:

[Seat:*] autologin-user=su_usuario autologin-user-timeout=0 pam-service=lightdm-autologin NumLock ON instale numlockx y modifique /etc/lightdm/lightdm.conf para agregar lo siguiente:

greeter-setup-script=/usr/bin/numlockx on