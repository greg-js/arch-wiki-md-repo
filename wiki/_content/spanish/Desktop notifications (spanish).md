Libnotify es una fácil manera de mostrar notificaciones de escritorio e información en pequeños cuadros de dialogo. Es usado en muchas aplicaciones de código abierto tales como evolution, pidgin, etc. Tiene soporte para aplicaciones Gtk+ y Qt.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Gnome](#Gnome)
    *   [2.2 XFCE](#XFCE)
*   [3 Trucos y Consejos](#Trucos_y_Consejos)
*   [4 Mas recursos](#Mas_recursos)

## Instalación

El paquete libnotify esta disponible en el repositorio Extra. Instale libnotify desde la terminal con el siguiente comando.

```
pacman -S libnotify

```

## Configuración

### Gnome

Para configurar libnotify en Gnome instale los paquetes notification-daemon y gconf-editor disponible en el repositorio Extra. Para instalar los paquetes desde la terminal:

```
pacman -S notification-daemon gconf-editor

```

Abra gconf-editor desde la terminal con el siguiente comando:

```
gconf-editor

```

Desde gconf-editor, selecciona "/apps/notification-daemon/". Allí puedes configurar libnotify

### XFCE

Para configurar libnotify en XFCE, necesita los paquetes xfce4-notifyd and xfconf disponible en el repositorio Extra. Para instalar los paquetes desde la terminal:

```
pacman -S xfce4-notifyd
pacman -S xfconf 

```

Para la configuración de libnotify ejecuta

```
xfce4-notifyd-config

```

## Trucos y Consejos

Tu puedes escribir tus propio mensajes de notificación fácilmente en Python u otros lenguajes. Aquí hay un ejemplo simple en Python.

Note que necesitara los enlaces de Python para libnotify

```
pacman -S python-notify  #(communitiy)

```

Ejemplo "hola mundo"

```
#!/usr/bin/env python
import subprocess
info = "Hola mundo "
subprocess.call(('notify-send',info))

```

```
#!/usr/bin/python
import subprocess
import commands    
#KERNEL VERSION
uname = commands.getoutput('uname -r')
head = "Toda la informacion de su sistema:"
msg = "Su version del kernel (núcleo): "+ uname +"
"       
# print message
subprocess.call(['notify-send', head, msg])

```

O puedes usar bash

```
# enviar una notificación que diga hola mundo
notify-send "hola mundo"

```

## Mas recursos

[Libnotify python example](http://www.florijan.net/2009/05/22/howto-using-python-to-display-notifications-using-libnotify/) [another libnotify example](http://roscidus.com/desktop/node/336)