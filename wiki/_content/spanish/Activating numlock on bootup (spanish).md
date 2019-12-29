**Estado de la traducción**
Este artículo es una traducción de [Activating Numlock on Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup"), revisada por última vez el **2019-10-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Activating_Numlock_on_Bootup&diff=0&oldid=582086) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Consola](#Consola)
    *   [1.1 Usando un servicio separado](#Usando_un_servicio_separado)
    *   [1.2 Extendiendo getty@.service](#Extendiendo_getty@.service)
    *   [1.3 Alternativa en Bash](#Alternativa_en_Bash)
*   [2 X.org](#X.org)
    *   [2.1 startx](#startx)
    *   [2.2 MATE](#MATE)
    *   [2.3 KDE Plasma](#KDE_Plasma)
    *   [2.4 GDM](#GDM)
    *   [2.5 GNOME](#GNOME)
    *   [2.6 Xfce](#Xfce)
    *   [2.7 SDDM](#SDDM)
    *   [2.8 SLiM](#SLiM)
    *   [2.9 OpenBox](#OpenBox)
    *   [2.10 LightDM](#LightDM)
    *   [2.11 LXDM](#LXDM)
    *   [2.12 LXQt](#LXQt)

## Consola

### Usando un servicio separado

**Sugerencia:** Estos pasos pueden ser automatizados al [instalar](/index.php/Install "Install") el paquete [systemd-numlockontty](https://aur.archlinux.org/packages/systemd-numlockontty/) y [activando](/index.php/Enabling "Enabling") el servicio `numLockOnTty`.

Primero cree una secuencia de comandos *(script)* para establecer el bloqueo numérico en los TTYs relevantes:

 `/usr/local/bin/numlock` 
```
#!/bin/bash

for tty in /dev/tty{1..6}
do
    /usr/bin/setleds -D +num < "$tty";
done

```

Entonces cree y [active](/index.php/Enable "Enable") un servicio systemd:

 `/etc/systemd/system/numlock.service` 
```
[Unit]
Description=numlock

[Service]
ExecStart=/usr/local/bin/numlock
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

### Extendiendo getty@.service

Esto es más simple que usar un servicio separado y no codifica el número de VTs en una secuencia de comandos. Cree un [drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") para `getty@.service` que se aplique sobre el original:

 `/etc/systemd/system/getty@.service.d/activate-numlock.conf` 
```
[Service]
ExecStartPre=/bin/sh -c 'setleds -D +num < /dev/%I'
```

**Nota:** Si tiene algún problema, intente reemplazar `ExecStartPre` con `ExecStartPost`, y/o desactive la sugerencia como se describe a continuación.

Para desactivas la sugerencia de activación del bloqueo numérico que se muestra en la pantalla de inicio de sesión, [edite](/index.php/Edit "Edit") `getty@tty1.service` y añada `--nohints` a las opciones de *agetty*:

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty '-p -- \\u' --nohints --noclear %I $TERM

```

### Alternativa en Bash

Añada `setleds -D +num` a `~/.bash_profile`. Tenga en cuenta que, a diferencia de los otros métodos, esto no tendrá efecto hasta después de iniciar sesión.

## X.org

Están disponibles varios métodos.

### startx

Instale el paquete [numlockx](https://www.archlinux.org/packages/?name=numlockx) e inclúyalo en el archivo `~/.xinitrc` antes de `exec`:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

numlockx &

exec window_manager

```

### MATE

De forma predeterminada, MATE guarda el último estado al cerrar sesión y lo restaura durante el siguiente inicio de sesión. Para activar el bloqueo numérico en cada inicio de sesión, debe cambiar los siguientes valores DCONF:

```
dconf write org.mate.peripherals-keyboard remember-numlock-state false
dconf write org.mate.peripherals-keyboard numlock-state 'on'

```

### KDE Plasma

Vaya a *Configuración del sistema > Dispositivos de entrada > Teclado* y elija el comportamiento del bloqueo numérico en la sección *Bloqueo numérico en el inicio de Plasma*.

### GDM

**Note:** GDM ya no ejecuta secuencia de comandos en `/etc/gdm/Init`.

Asegúrese de que tiene [numlockx](https://www.archlinux.org/packages/?name=numlockx) instalado y luego añada el siguiente código a [~/.xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)"):

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```

### GNOME

Cuando no se usa el administrador de inicio de sesión de GDM, se puede añadir numlockx a las aplicaciones de inicio de GNOME.

[Instale](/index.php/Install "Install") el paquete [numlockx](https://www.archlinux.org/packages/?name=numlockx). Entonces, añada un comando de inicio para lanzar `numlockx`.

```
$ gnome-session-properties

```

El comando anterior abre el applet **Preferencias de aplicaciones de inicio**. Pulse en ***Añadir*** e introduzca lo siguiente:

| Name: | *Numlockx* |
| Command: | */usr/bin/numlockx on* |
| Comment: | *Activa el bloqueo numérico.* |

**Nota:** Esto no es un cambio para todo el sistema, repita estos pasos para cada usuario que desee activar el bloqueo numérico después de iniciar sesión.

### Xfce

En el archivo `~/.config/xfce4/xfconf/xfce-perchannel-xml/keyboards.xml`, asegúrese de que los siguientes valores estén establecidos como verdadero *(true)*:

```
<property name="Numlock" type="bool" value="true"/>
<property name="RestoreNumlock" type="bool" value="true"/>

```

**Nota:** Si el archivo no existe, abra Configuración > Teclado, luego marque y desmarque `Restaurar estado del bloqueo numérico al inicio`. Esto creará el archivo `keyboards.xml`.

### SDDM

En el archivo `/etc/sddm.conf`, bajo la sección `[General]`, configure el valor del bloqueo numérico *(Numlock)* como activo *(on)*:

```
[General]
...
Numlock=on

```

### SLiM

En el archivo `/etc/slim.conf` busque la línea y descomentela (elimine el `#`):

```
#numlock             on

```

### OpenBox

En el archivo `~/.config/openbox/autostart` añada la línea:

```
numlockx &

```

Y luego guarde el archivo.

### LightDM

Véase [LightDM#NumLock on by default](/index.php/LightDM#NumLock_on_by_default "LightDM").

### LXDM

Establezca la opción en `/etc/lxdm/lxdm.conf`:

```
numlock=1

```

### LXQt

Establezca la opción en `~/.config/lxqt/session.conf`:

```
[Keyboard]
numlock=true

```