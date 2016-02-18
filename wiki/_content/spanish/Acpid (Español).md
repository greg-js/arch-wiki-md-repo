[acpid](http://acpid.sourceforge.net/) es un "demonio" flexible y extensible para entregar for delivering [eventos ACPI](/index.php?title=ACPI_modules_(Espa%C3%B1ol)&action=edit&redlink=1 "ACPI modules (Español) (page does not exist)"). Vigila `/proc/acpi/event` y cuando hay un evento, ejecuta programas para manejarlo. when an event occurs, executes programs to handle the event. Estos eventos se activan mediante ciertas acciones, como:

*   Apretar teclas especiales, incluyendo el boton de Encendido/Hibernar/Suspender.
*   Closing a notebook lid
*   (Des)conectar un adaptador de Corriente Alterna a un portátil.
*   (Des)conectar un jack de un teléfono, etc.

acpid puede ser usado asi mismo, o combinado con un sistema más robusto como [pm-utils](/index.php?title=Pm-utils_(Espa%C3%B1ol)&action=edit&redlink=1 "Pm-utils (Español) (page does not exist)") y [cpufrequtils](/index.php/CPU_Frequency_Scaling_(Espa%C3%B1ol) "CPU Frequency Scaling (Español)") para una mayor solución del control de energía.

**Nota:**

*   [Entornos de escritorio](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)"), como [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), gestor de inicio de sesión de [systemd](/index.php/Systemd_(Espa%C3%B1ol)#ACPI_administraci.C3.B3n_de_la_energ.C3.ADa "Systemd (Español)") y algunos demonios [manejadores de teclas extra](/index.php?title=Extra_Keyboard_Keys_(Espa%C3%B1ol)&action=edit&redlink=1 "Extra Keyboard Keys (Español) (page does not exist)") pueden implementar métodos propios de manejo de eventos, independientemente de acpid. Usar más de un sistema a la vez puede provocar un comportamiento inesperado, como suspenderse dos veces de una, tras apretar una vez el botón de hibernar. Ten esto en cuenta y activa solo manejadores deseados.
*   Ya que por defecto el script que provee acpid, **/etc/acpi/handler.sh**, sobreescribirá la funcionalidad del botón de encendido/apagado de tu entorno de escritorio, seguramente querrás cambiar la rutina de apagado de acpid para evitar apagar el ordenador cuando apretes de golpe cuando apretes el botón de encendido/apagado (ver instrucciones a continuación).

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Configuración alternativa](#Configuraci.C3.B3n_alternativa)
*   [3 Trucos y Sugerencias](#Trucos_y_Sugerencias)
    *   [3.1 Ampliando acpid con pm-utils](#Ampliando_acpid_con_pm-utils)
    *   [3.2 Eventos de Ejemplo](#Eventos_de_Ejemplo)
    *   [3.3 Activar el control del volumen](#Activar_el_control_del_volumen)
    *   [3.4 Activar el control del brillo](#Activar_el_control_del_brillo)
    *   [3.5 Habilitar el control del Wi-Fi](#Habilitar_el_control_del_Wi-Fi)
    *   [3.6 Apagar la pantalla del portátil](#Apagar_la_pantalla_del_port.C3.A1til)
    *   [3.7 Sacar el nombre de usuario del monitor actual](#Sacar_el_nombre_de_usuario_del_monitor_actual)
*   [4 Ver también](#Ver_tambi.C3.A9n)

## Instalación

[Instala](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [acpid](https://www.archlinux.org/packages/?name=acpid), disponible en los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)").

Para que inicie al arranque :

*   Si usas [systemd](/index.php/Systemd "Systemd") (seguramente), pon en un terminal `systemctl enable acpid` ;
*   Si usas [initscripts](/index.php/Rc.conf "Rc.conf"), edita `/etc/rc.conf` como superusuario y añade `acpid` a la[variable DAEMONS](/index.php/Rc.conf_(Espa%C3%B1ol)#Demonios "Rc.conf (Español)").

## Configuración

[acpid](https://www.archlinux.org/packages/?name=acpid) viene con un número de acciones predefinidas para eventos activos, como lo qué debería occurrir cuando apretas el botón de encendido/apagado en tu ordenador. Por defecto, esas acciones están definidas en `/etc/acpi/handler.sh`, que se ejecuta después de que se detecta un evento ACPI (según determine `/etc/acpi/events/anything`).

Lo siguiente es un ejemplo de una acción. En este caso, cuando se apreta el botón de Hibernar, acpid ejecuta el comando `echo -n mem >/sys/power/state`, que *debería* poner el ordenador en un estado de hibernación (suspendido):

```
button/sleep)
    case "$2" in
        SLPB) echo -n mem >/sys/power/state ;;
	 *)    logger "ACPI action undefined: $2" ;;
    esac
    ;;

```

Desafortunadamente, no todos los ordenadores etiquetan los eventos ACPI de la misma forma. Por ejemplo, el botón Hibernar puede identificarse en un PC como *SLPB* y en otra como *SBTN*.

Para determinar como son reconocidos tus botones o atajos de `teclado`, ejecuta el diguiente comando en un terminal como root:

```
# tail -f /var/log/messages.log

```

Ahora apreta el botón de Encendido y/o el botón de Hibernar (p. ej. `Ctrl+Alt+Supr`) de tu PC. El resultado debería ser algo asi:

```
logger: ACPI action undefined: PBTN
logger: ACPI action undefined: SBTN

```

Si no funciona, pon:

```
# acpi_listen

```

Entonces apreta el botón de Encendido/Apagado y verás algo así:

```
power/button PBTN 00000000 00000b31

```

La salida de `acpi_listen` se envía a `/etc/acpi/handler.sh` como parámetros $1, $2 , $3 & $4.. Ejemplo:

```
$1 power/button
$2 PBTN
$3 00000000
$4 00000b31

```

Como ya te habrás dado cuando, el botón de Hibernar en la salida de ejemplo es reconocido como *SBTN*, en lugar de la etiqueta *SLPB* especificada en archivo `/etc/acpi/handler.sh` por defecto. Para hacer que el botón de Hibernar funcione correctamente en este PC, necesitaremos reemplazar *SLPB)* con *SBTN)*.

Usando esto como base, puedes personalizar fácilmente el archivo `/etc/acpi/handler.sh` para ejecutar una variedad de comandos dependiendo de que evento es ejecutado. Mira la sección [#Trucos y Sugerencias](#Trucos_y_Sugerencias) a continuación para otros comandos usados comúnmente.

### Configuración alternativa

Por defecto, todos los eventos ACPI pasan por el script `/etc/acpi/handler.sh`. Esto se debe al conjunto de reglas escritas en `/etc/acpi/events/anything`:

```
# Pass all events to our one handler script
event=.*
action=/etc/acpi/handler.sh %e

```

Aunque esto funciona muy bien como está, algunos usuarios pueden preferir definir reglas de evento y acciones en sus propios scrpits independientes. Lo siguiente es un ejemplo de cómo usar un archivo de evento individual y su correspondiente script de acción:

Como superusuario, crea el archivo siguiente:

 `/etc/acpi/events/sleep-button` 
```
event=button sleep.*
action=/etc/acpi/actions/sleep-button.sh "%e"

```

Ahora crea el siguinte archivo:

 `/etc/acpi/actions/sleep-button.sh` 
```
#!/bin/sh
case "$2" in
    SLPB) echo -n mem >/sys/power/state ;;
    *)    logger "ACPI action undefined: $2" ;;
esac

```

Finalmente, haz el script ejecutable:

```
# chmod +x /etc/acpi/actions/sleep-button.sh

```

Usando este método, es fácil crear los scripts de eventos/acciones individuales que quieras.

## Trucos y Sugerencias

**Sugerencia:** Algunas acciones descritas aquí, como el control del Wi-Fi y del brillo, pueden ser controlados directamente por tus drivers. Deberías consultas la documentación de los módulos del kernel correspondientes cuando este sea el caso.

### Ampliando acpid con pm-utils

Aunque [acpid](https://www.archlinux.org/packages/?name=acpid) puede proveer una función de suspendido básica, podrías desear un sistema más robusto. [pm-utils](/index.php?title=Pm-utils_(Espa%C3%B1ol)&action=edit&redlink=1 "Pm-utils (Español) (page does not exist)") provee una estructura muy flexible suspender e hibernar, incluyendo soluciones para hardware y drivers tercos (p. ej. módulos fglrx). pm-utils provee dos scripts, `pm-suspend` y `pm-hibernate`, los cuales pueden ser insertados como eventos en acpid. Para más informacón lee el wiki [pm-utils](/index.php/Pm-utils "Pm-utils") wiki.

### Eventos de Ejemplo

Los siguientes son ejemplos de eventos que pueden ser usados en el script `/etc/acpi/handler.sh`. Estos ejemplos deberían ser modificados para que se ajusten a tu entorno específico, por ejemplo cambiando los nombres de las variables de evento tal y como las interprete `acpi_listen`.

Para bloquear la pantalla con `xscreensaver` cuando cierres la tapa del portátil pon:

```
button/lid)
    case $3 in
        close)
            # The lock command need to be run as the user who owns the xscreensaver process and not as root.
            # See: man xscreensaver-command. $xs will have the value of the user owning the process, if any.

            xs=$(ps -C xscreensaver -o user=)
            if test $xs; then su $xs -c "xscreensaver-command -lock"; fi
            ;;

```

Para suspender el sistema y bloquear la pantalla usando `slimlock` cuando la tapa está cerrada:

```
button/lid)
    case $3 in
        close)
            #echo "LID switched!">/dev/tty5
	     /usr/sbin/pm-suspend &
	     DISPLAY=:0.0 su -c - username /usr/bin/slimlock
            ;;

```

Execute `pm-suspend` when the sleep button is pressed:

```
button/sleep)
    case "$2" in
        SBTN) 
	     #echo -n mem >/sys/power/state
            /usr/sbin/pm-suspend
            ;;

```

Para ajustar el brillo del portátil según este conectado a la corriente o no (deberías ajustar los números, mira `/sys/class/backlight/acpi_video0/max_brightness`):

```
ac_adapter)
    case "$2" in
        AC*|AD*)
            case "$4" in
                00000000)
                    echo -n 50 > /sys/class/backlight/acpi_video0/brightness
                    ;;
                00000001)
                    echo -n 100 > /sys/class/backlight/acpi_video0/brightness
                    ;;
            esac

```

### Activar el control del volumen

Descubre la identificación de acpi de los botones del volunes (mira a continuación) y sustituye los eventos acpi en los archivos a continuación. Creamos un script para controlar el volumen (asumiendo que usas una tarjeta de sonido con [ALSA (Español)](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)")):

 `/etc/acpi/handlers/vol` 
```
#!/bin/sh
step=5

case $1 in
  -) amixer set Master $step-;;
  +) amixer set Master $step+;;
esac

```

Y conectalos a nuevos eventos acpi:

 `/etc/acpi/events/vol_d` 
```
event=button/volumedown
action=/etc/acpi/handlers/vol -

```
 `/etc/acpi/events/vol_u` 
```
event=button/volumeup
action=/etc/acpi/handlers/vol +

```

También otro evento para silenciar:

 `/etc/acpi/events/mute` 
```
event=button/mute
action=/usr/bin/amixer set Master toggle

```

### Activar el control del brillo

Parecido al control del volumen, acpid también te permite controlar el brillo de tu pantalla. Para conseguir esto escribe algún script, como este:

 `/etc/acpi/handlers/bl` 
```
#!/bin/sh
bl_dev=/sys/class/backlight/acpi_video0
step=1

case $1 in
  -) echo $((`cat $bl_dev/brightness` - $step)) >$bl_dev/brightness;;
  +) echo $((`cat $bl_dev/brightness` + $step)) >$bl_dev/brightness;;
esac

```

y otra vez, conecta las teclas a eventos ACPI:

 `/etc/acpi/events/bl_d` 
```
event=video/brightnessdown
action=/etc/acpi/handlers/bl -

```
 `/etc/acpi/events/bl_u` 
```
event=video/brightnessup
action=/etc/acpi/handlers/bl +

```

### Habilitar el control del Wi-Fi

También puedes crear un sencillo controlador wireless apretando los botones WLAN. Un ejemplo de evento:

 `/etc/acpi/events/wlan` 
```
event=button/wlan
action=/etc/acpi/handlers/wlan

```

y su script manejador:

 `/etc/acpi/handlers/wlan` 
```
#!/bin/sh
rf=/sys/class/rfkill/rfkill0

case `cat $rf/state` in
  0) echo 1 >$rf/state && systemctl start net-auto-wireless;;
  1) systemctl stop net-auto-wireless && echo 0 >$rf/state;;
esac

```

### Apagar la pantalla del portátil

Adaptado del [de Gentoo](http://en.gentoo-wiki.com/wiki/ACPI/Configuration%7CWiki), viene esta pequeña perla. Añade esto al final de `/etc/acpi/actions/lm_lid.sh` o a la sección *button/lid* `/etc/acpi/handler.sh`. Esto apagará la luz de la pantalla cuando la tapa esté cerrada, y la encenderá cuando la tapa se abra.

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) XAUTHORITY=$(ps -C xinit -f --no-header | sed -n 's/.*-auth //; s/ -[^ ].*//; p') xset -display :0 dpms force off ;;
    open)   XAUTHORITY=$(ps -C xinit -f --no-header | sed -n 's/.*-auth //; s/ -[^ ].*//; p') xset -display :0 dpms force on  ;;
esac

```

Si quieres incrementar/disminuir el brillo o algo que dependa de X, debes especificarel monitor con X y también el archivo MIT magic cookie (via XAUTHORITY). Lo último es una credencial de seguridad que provee acceso de escritura y lectura al servidor X, monitor, y dispositivos de entrada.

Aquí hay otro script que no usa XAUTHORITY sino sudo:

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) sudo -u `ps -o ruser= -C xinit` xset -display :0 dpms force off ;;
    open)   sudo -u `ps -o ruser= -C xinit` xset -display :0 dpms force on  ;;
esac

```

Con ciertas combinaciones de [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") y hardware problemático, `xset dpms force off` solo deja en blanco la pantalla dejando la luz encendida. Esto puede ser corregido usando [vbetool](https://www.archlinux.org/packages/?name=vbetool) de los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)"). Cambia la sección LCD a:

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) vbetool dpms off ;;
    open)   vbetool dpms on  ;;
esac

```

Si el monitor se apaga solo brevemente y después se enciende, seguramente sea el control de energía que viene con xscreensaver, que entra en conflicto con los ajustes manuales de *dpm'.*

### Sacar el nombre de usuario del monitor actual

Puedes usar la función `getuser` para descubrir el usuario del monitor actual:

```
getuser ()
    {
     export DISPLAY=`echo $DISPLAY | cut -c -2`
     user=`who | grep " $DISPLAY" | awk '{print $1}' | tail -n1`
     export XAUTHORITY=/home/$user/.Xauthority
     eval $1=$user
    }

```

Se puede usar esta función, por ejemplo, cuando apretas el botón de Encendido/Apagado, y quieres apagar [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)") correctamente:

```
button/power)
    case "$2" in
        PBTN)
            getuser "$user"
            echo $user > /dev/tty5
            su $user -c "dcop ksmserver ksmserver logout 0 2 0"
            ;;
          *) logger "ACPI action undefined $2" ;;
    esac
    ;;

```

En sistemas más nuevos usando systemd, los accesos a X11 no son necesariamente mostrados en `who`, de manera que la función `getuser` no funciona. Una alternativa es usar `loginctl` para obtener la información requerida (p.ej. usando [xuserrun](https://github.com/rephorm/xuserrun).

## Ver también

*   [http://acpid.sourceforge.net/](http://acpid.sourceforge.net/) - página de acpid
*   [http://www.gentoo-wiki.info/ACPI/Configuration](http://www.gentoo-wiki.info/ACPI/Configuration)
*   [ACPI hotkeys](/index.php?title=ACPI_hotkeys_(Espa%C3%B1ol)&action=edit&redlink=1 "ACPI hotkeys (Español) (page does not exist)")