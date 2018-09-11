**Estado de la traducción:** este artículo es una versión traducida de [Acpid](/index.php/Acpid "Acpid"). Fecha de la última traducción/revisión: **2018-09**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Acpid&diff=0&oldid=515037).

Related articles

*   [Módulos ACPI](/index.php/ACPI_modules "ACPI modules")
*   [DSDT](/index.php/DSDT "DSDT")

[acpid2](http://acpid2.sourceforge.net/) es un demonio flexible y extensible para entregar [eventos ACPI](/index.php/ACPI_modules "ACPI modules"). Cuando ocurre un evento, ejecuta programas para manejarlo. Estos eventos son desencadenados por ciertas acciones, tales como:

*   Presionando teclas especiales, incluido el botón de Encendido/Suspensión/Hibernación
*   Cerrando la tapa de un portátil
*   (Des)Enchufando un adaptador de corriente de un portátil
*   (Des)Enchufando el conector del teléfono (módem), etc.

**Nota:** Los [entornos de escritorio](/index.php?title=Desktop_environments_(Espa%C3%B1ol)&action=edit&redlink=1 "Desktop environments (Español) (page does not exist)"), como [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), el administrador de inicio de sesión de [systemd](/index.php/Power_Management_(Espa%C3%B1ol)#Eventos_de_ACPI "Power Management (Español)") y algunos demonios que [manejan teclas extra](/index.php/Extra_keyboard_keys "Extra keyboard keys") pueden implementar esquemas propios de manejo de eventos, independientes de acpid. La ejecución de más de un sistema al mismo tiempo puede provocar un comportamiento inesperado, como suspender dos veces seguidas después de presionar un botón de suspensión. Tenga esto en cuenta y active solo los manejadores que necesite.

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

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [acpid](https://www.archlinux.org/packages/?name=acpid). Entonces [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") y/o [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") `acpid.service`.

## Configuración

[acpid](https://www.archlinux.org/packages/?name=acpid) viene con un número de acciones predefinidas para eventos activos, como lo qué debería occurrir cuando se presiona el botón de encendido/apagado en el ordenador. Por defecto, esas acciones están definidas en `/etc/acpi/handler.sh`, que se ejecuta después de que se detecta un evento ACPI (según determine `/etc/acpi/events/anything`).

Lo siguiente es un ejemplo de una acción. En este caso, cuando se presiona el botón de Hibernar, acpid ejecuta el comando `echo -n mem >/sys/power/state`, que *debería* poner el ordenador en un estado de hibernación (suspendido):

```
button/sleep)
    case "$2" in
        SLPB) echo -n mem >/sys/power/state ;;
	 *)    logger "ACPI action undefined: $2" ;;
    esac
    ;;

```

Desafortunadamente, no todos los ordenadores etiquetan los eventos ACPI de la misma forma. Por ejemplo, el botón Hibernar puede identificarse en un PC como *SLPB* y en otra como *SBTN*.

Para determinar como son reconocidos tus botones o atajos de `teclado`, ejecuta el siguiente comando en un terminal como root:

```
# tail -f /var/log/messages.log

```

Ahora presione el botón de Encendido y/o el botón de Hibernar (p. ej. `Ctrl+Alt+Supr`) de la PC. El resultado debería ser algo asi:

```
logger: ACPI action undefined: PBTN
logger: ACPI action undefined: SBTN

```

Si no funciona, intenta:

```
# acpi_listen

```

Entonces presione el botón de Encendido/Apagado y se verá algo así:

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

Como se puede observar, el botón de Hibernar en la salida de ejemplo es reconocido como *SBTN*, en lugar de la etiqueta *SLPB* especificada en archivo `/etc/acpi/handler.sh` por defecto. Para hacer que el botón de Hibernar funcione correctamente en el PC, necesitaremos reemplazar *SLPB)* con *SBTN)*.

Usando esto como base, se puede personalizar fácilmente el archivo `/etc/acpi/handler.sh` para ejecutar una variedad de comandos dependiendo de que evento es ejecutado. Mira la sección [#Trucos y Sugerencias](#Trucos_y_Sugerencias) a continuación para otros comandos usados comúnmente.

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

**Sugerencia:** Algunas acciones descritas aquí, como el control del Wi-Fi y del brillo, pueden ser controlados directamente por los drivers. Deberías consultar la documentación de los módulos del kernel correspondientes cuando este sea el caso.

### Ampliando acpid con pm-utils

Aunque [acpid](https://www.archlinux.org/packages/?name=acpid) puede proveer una función de suspendido básica, se podría desear un sistema más robusto. [pm-utils](/index.php?title=Pm-utils_(Espa%C3%B1ol)&action=edit&redlink=1 "Pm-utils (Español) (page does not exist)") provee una estructura muy flexible suspender e hibernar, incluyendo soluciones para hardware y drivers tercos (p. ej. módulos fglrx). pm-utils provee dos scripts, `pm-suspend` y `pm-hibernate`, los cuales pueden ser insertados como eventos en acpid. Para más información lee el wiki [pm-utils](/index.php/Pm-utils "Pm-utils") wiki.

### Eventos de Ejemplo

Los siguientes son ejemplos de eventos que pueden ser usados en el script `/etc/acpi/handler.sh`. Estos ejemplos deberían ser modificados para que se ajusten a el entorno específico, por ejemplo cambiando los nombres de las variables de evento tal y como las interprete `acpi_listen`.

Para bloquear la pantalla con `xscreensaver` cuando se cierra la tapa del portátil intenta:

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

Ejecuta `pm-suspend` cuando se presiona el botón de suspensión.

```
button/sleep)
    case "$2" in
        SBTN) 
	     #echo -n mem >/sys/power/state
            /usr/sbin/pm-suspend
            ;;

```

Para ajustar el brillo del portátil según este conectado a la corriente o no (se debería ajustar los números, mira `/sys/class/backlight/acpi_video0/max_brightness`):

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

Descubre la identificación de acpi de los botones de volumen (mira a continuación) y sustituye los eventos acpi en los archivos a continuación. Creamos un script para controlar el volumen (asumiendo que se usa una tarjeta de sonido con [ALSA (Español)](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)")):

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

Parecido al control del volumen, acpid también permite controlar el brillo de la pantalla. Para conseguir esto escribe un script como el siguiente:

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

También se puede crear un sencillo controlador wireless presionando los botones WLAN. Un ejemplo de evento:

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

Adaptado del [de Gentoo](http://www.gentoo-wiki.info/ACPI/Configuration%7CWiki), viene esta pequeña perla. Añade esto al final de `/etc/acpi/actions/lm_lid.sh` o a la sección *button/lid* `/etc/acpi/handler.sh`. Esto apagará la luz de la pantalla cuando la tapa esté cerrada, y la encenderá cuando la tapa se abra.

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) XAUTHORITY=$(ps -C xinit -f --no-header | sed -n 's/.*-auth //; s/ -[^ ].*//; p') xset -display :0 dpms force off ;;
    open)   XAUTHORITY=$(ps -C xinit -f --no-header | sed -n 's/.*-auth //; s/ -[^ ].*//; p') xset -display :0 dpms force on  ;;
esac

```

Si se quiere incrementar/disminuir el brillo o algo que dependa de X, se debe especificar el monitor con X y también el archivo MIT magic cookie (via XAUTHORITY). Lo último es una credencial de seguridad que provee acceso de escritura y lectura al servidor X, monitor, y dispositivos de entrada.

Aquí hay otro script que no usa XAUTHORITY sino sudo:

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) sudo -u `ps -o ruser= -C xinit` xset -display :0 dpms force off ;;
    open)   sudo -u `ps -o ruser= -C xinit` xset -display :0 dpms force on  ;;
esac

```

Con ciertas combinaciones de [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") y hardware problemático, `xset dpms force off` solo deja en blanco la pantalla dejando la luz encendida. Esto puede ser corregido usando [vbetool](https://www.archlinux.org/packages/?name=vbetool) de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Cambia la sección LCD a:

```
case $(cat /proc/acpi/button/lid/LID0/state | awk '{print $2}') in
    closed) vbetool dpms off ;;
    open)   vbetool dpms on  ;;
esac

```

Si el monitor se apaga solo brevemente y después se enciende, seguramente sea el control de energía que viene con xscreensaver, que entra en conflicto con los ajustes manuales de *dpm'.*

### Sacar el nombre de usuario del monitor actual

Se puede usar la función `getuser` para descubrir el usuario del monitor actual:

```
getuser ()
    {
     export DISPLAY=`echo $DISPLAY | cut -c -2`
     user=`who | grep " $DISPLAY" | awk '{print $1}' | tail -n1`
     export XAUTHORITY=/home/$user/.Xauthority
     eval $1=$user
    }

```

Se puede usar esta función, por ejemplo, cuando se presiona el botón de Encendido/Apagado, y se requiere apagar [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)") correctamente:

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

En sistemas más nuevos usando systemd, los accesos a X11 no son necesariamente mostrados en `who`, de manera que la función `getuser` no sirve. Una alternativa es usar `loginctl` para obtener la información requerida (p.ej. usando [xuserrun](https://github.com/rephorm/xuserrun).

## Ver también

*   [http://acpid.sourceforge.net/](http://acpid.sourceforge.net/) - página de acpid
*   [Gentoo wiki](http://www.gentoo-wiki.info/ACPI/Configuration)
*   [ACPI hotkeys](/index.php?title=ACPI_hotkeys_(Espa%C3%B1ol)&action=edit&redlink=1 "ACPI hotkeys (Español) (page does not exist)")