**Estado de la traducción:** este artículo es una versión traducida de [Acpid](/index.php/Acpid "Acpid"). Fecha de la última traducción/revisión: **2018-09-13**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Acpid&diff=0&oldid=515037).

Related articles

*   [Módulos ACPI](/index.php/ACPI_modules_(Espa%C3%B1ol) "ACPI modules (Español)")
*   [DSDT](/index.php/DSDT "DSDT")

[acpid2](http://acpid2.sourceforge.net/) es un demonio flexible y extensible para entregar [eventos ACPI](/index.php/ACPI_modules_(Espa%C3%B1ol) "ACPI modules (Español)"). Cuando ocurre un evento, ejecuta programas para manejarlo. Estos eventos son desencadenados por ciertas acciones, tales como:

*   Presionando teclas especiales, incluido el botón de Encendido/Suspensión/Hibernación
*   Cerrando la tapa de un portátil
*   (Des)Enchufando un adaptador de corriente de un portátil
*   (Des)Enchufando el conector del teléfono (módem), etc.

**Nota:** Los [entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)"), como [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), el administrador de inicio de sesión de [systemd](/index.php/Power_management_(Espa%C3%B1ol)#Eventos_de_ACPI "Power management (Español)") y algunos demonios que [manejan teclas extra](/index.php/Extra_keyboard_keys "Extra keyboard keys") pueden implementar esquemas propios de manejo de eventos, independientes de acpid. La ejecución de más de un sistema al mismo tiempo puede provocar un comportamiento inesperado, como suspender dos veces seguidas después de presionar un botón de suspensión. Tenga esto en cuenta y active solo los manejadores que necesite.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Configuración alternativa](#Configuraci.C3.B3n_alternativa)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Eventos de ejemplo](#Eventos_de_ejemplo)
    *   [3.2 Activar el control del volumen](#Activar_el_control_del_volumen)
    *   [3.3 Activar el control del brillo](#Activar_el_control_del_brillo)
    *   [3.4 Habilitar el control Wi-Fi](#Habilitar_el_control_Wi-Fi)
    *   [3.5 Obtener el nombre de usuario de la pantalla actual](#Obtener_el_nombre_de_usuario_de_la_pantalla_actual)
        *   [3.5.1 Conectar a un socket acpid](#Conectar_a_un_socket_acpid)
*   [4 Consulte también](#Consulte_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [acpid](https://www.archlinux.org/packages/?name=acpid). Entonces [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") y/o [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") `acpid.service`.

## Configuración

[acpid](https://www.archlinux.org/packages/?name=acpid) viene con una serie de acciones predefinidas para eventos activados, como lo que debería suceder cuando presionas el botón de encendido en tu máquina. De forma predeterminada, estas acciones se definen en `/etc/acpi/handler.sh`, que se ejecuta después de detectar cualquier evento ACPI (según lo determinado por `/etc/acpi/events/anything` )

Lo siguiente es un pequeño ejemplo de una acción de este tipo. En este caso, cuando se presiona el botón de Suspensión, acpid ejecuta el comando `echo -n mem >/sys/power/state` que *debería* colocar la computadora en un estado de suspensión (hibernación):

```
button/sleep)
    case "$2" in
        SLPB) echo -n mem >/sys/power/state ;;
	 *)    logger "ACPI action undefined: $2" ;;
    esac
    ;;

```

Desafortunadamente, no todas las computadoras etiquetan los eventos ACPI de la misma manera. Por ejemplo, el botón de suspensión puede identificarse en una máquina como *SLPB* y en otra como *SBTN*.

Para determinar cómo se reconocen sus botones o atajos `Fn`, ejecute el siguiente comando:

```
# journalctl -f

```

Ahora presione el botón de encendido y/o el botón de suspensión (por ejemplo, `Fn+Esc`) en su máquina. El resultado debería ser algo así:

```
logger: ACPI action undefined: PBTN
logger: ACPI action undefined: SBTN

```

Si eso no funciona, ejecute:

```
# acpi_listen

```

o con [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat):

```
$ netcat -U /var/run/acpid.socket

```

Luego presione el botón de encendido y verá algo como esto:

```
button/power PBTN 00000000 00000b31

```

El resultado de `acpi_listen` se envía a `/etc/acpi/handler.sh` como parámetros $1, $2, $3 y $4. Ejemplo:

```
$1 button/power
$2 PBTN
$3 00000000
$4 00000b31

```

Como habrá notado, el botón de suspensión en la salida del ejemplo se reconoce realmente como *SBTN*, en lugar de la etiqueta *SLPB* especificada en el archivo `/etc/acpi/handler.sh` predeterminado. Para que la función de suspensión funcione correctamente en esta máquina, debería reemplazar *SLPB)* por *SBTN)*.

Al utilizar esta información como base, puede personalizar fácilmente el archivo `/etc/acpi/handler.sh` para ejecutar una variedad de comandos según el evento que se active. Consulte la sección [#Consejos y trucos](#Consejos_y_trucos) a continuación para conocer otros comandos usados comúnmente.

### Configuración alternativa

De manera predeterminada, todos los eventos ACPI se pasan a través del script `/etc/acpi/handler.sh`. Esto se debe al conjunto de reglas descrito en `/etc/acpi/events/anything`:

```
# Pasar todos los eventos a nuestro script de un solo controlador
event=.*
action=/etc/acpi/handler.sh %e

```

Si bien esto funciona bien, algunos usuarios pueden preferir definir reglas y acciones de eventos en sus propios script independientes. El siguiente es un ejemplo de como usar un archivo de evento individual y el script de acción correspondiente:

Como superusuario, cree el siguiente archivo:

 `/etc/acpi/events/sleep-button` 
```
event=button sleep.*
action=/etc/acpi/actions/sleep-button.sh %e
```

Ahora cree el siguiente archivo:

 `/etc/acpi/actions/sleep-button.sh` 
```
#!/bin/sh
case "$3" in
    SLPB) echo -n mem >/sys/power/state ;;
    *)    logger "ACPI action undefined: $3" ;;
esac
```

Finalmente, haga el script ejecutable:

```
# chmod +x /etc/acpi/actions/sleep-button.sh

```

Al usar este método, es fácil crear cualquier cantidad de scripts de eventos/acciones individuales.

## Consejos y trucos

**Nota:** Algunas de las acciones descritas aquí, como el control de brillo de la pantalla y la (des)activación Wi-Fi, pueden ser ya administradas directamente por el controlador. Debe consultar la documentación de los módulos del kernel correspondientes, cuando este sea el caso.

### Eventos de ejemplo

Los siguientes son ejemplos de eventos que se pueden usar en el script `/etc/acpi/handler.sh`. Estos ejemplos se deben modificar para que se ajusten a su entorno específico, por ejemplo cambiando los nombres de las variables de evento interpretados por `acpi_listen`.

Para configurar el brillo de la pantalla del portátil cuando esté o no enchufado (es posible que sea necesario ajustar los números, consulte `/sys/class/backlight/acpi_video0/max_brightness`):

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

Averigüe la identidad acpi de los botones de volumen (consultar arriba) y sustitúyalos por los eventos acpi en los archivos a continuación.

 `/etc/acpi/events/vol-d` 
```
event=button/volumedown
action=amixer set Master 5-
```
 `/etc/acpi/events/vol-m` 
```
event=button/mute
action=amixer set Master toggle
```
 `/etc/acpi/events/vol-u` 
```
event=button/volumeup
action=amixer set Master 5+
```

**Nota:** Estos comandos pueden no funcionar como se espera con PulseAudio. [[1]](https://lists.freedesktop.org/archives/pulseaudio-discuss/2015-December/025062.html) Para una funcionalidad completa, ejecute comandos como el usuario actual mientras especifica la [variable de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `XDG_RUNTIME_DIR`, por ejemplo con `sudo -u *usuario* XDG_RUNTIME_DIR=/run/user/*1000* pactl`.

**Sugerencia:** Desactive o vincule los botones de volumen en Xorg para evitar conflictos con otras aplicaciones. Consulte [Xmodmap](/index.php/Xmodmap "Xmodmap") para más detalles.

Consulte también [[2]](http://web.archive.org/web/20150711044207/http://blog.lastlog.de/posts/fixing_volume_change_in_linux).

### Activar el control del brillo

De forma similar al control de volumen, acpid también le permite controlar el brillo de la pantalla. Para lograr esto, escriba algún controlador, como este:

 `/etc/acpi/handlers/bl` 
```
#!/bin/sh
bl_dev=/sys/class/backlight/acpi_video0
step=1

case $1 in
  -) echo $(($(< $bl_dev/brightness) - $step)) >$bl_dev/brightness;;
  +) echo $(($(< $bl_dev/brightness) + $step)) >$bl_dev/brightness;;
esac
```

y nuevamente, conecte las teclas a los eventos ACPI:

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

### Habilitar el control Wi-Fi

También puede crear un interruptor de alimentación de la red inalámbrica simple al presionar el botón WLAN. Un ejemplo de evento:

 `/etc/acpi/events/wlan` 
```
event=button/wlan
action=/etc/acpi/handlers/wlan
```

y su controlador:

 `/etc/acpi/handlers/wlan` 
```
#!/bin/sh
rf=/sys/class/rfkill/rfkill0

case $(< $rf/state) in
  0) echo 1 >$rf/state;;
  1) echo 0 >$rf/state;;
esac
```

### Obtener el nombre de usuario de la pantalla actual

Para ejecutar comandos que dependan de [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"), es necesario definir la visualización X así como el archivo MIT Magic Cookie (a través de XAUTHORITY). Después es tener una credencial de seguridad que proporciona acceso de lectura y escritura al servidor X, a la pantalla y a cualquier dispositivo de entrada (consulte [xauth(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xauth.1)).

Consulte [[3]](https://gist.githubusercontent.com/AladW/de1c5676d93d05a5a0e1/raw/16e010ecda9f2328e1e22d4e02ac814ed27717b4/gistfile1.txt) para una función de ejemplo cuando se usa [xinitrc](/index.php/Xinitrc "Xinitrc").

**Nota:**

*   Si la luz de fondo de la pantalla LCD no se apaga cuando la tapa está cerrada, puede hacerlo manualmente ejecutando `getXuser xset dpms force off` y `getXuser xset dpms force on` en los eventos de tapa cerrada y abierta respectivamente. Si la pantalla está en blanco pero la luz de fondo encendida, en su lugar utilice [vbetool](https://www.archlinux.org/packages/?name=vbetool) con `betool dpms off` y `vbetool dpms on`. Consulte también [Configuración de XScreenSaver](/index.php/XScreenSaver_(Espa%C3%B1ol)#Configuraci.C3.B3n "XScreenSaver (Español)").
*   Cuando utilice *who* o *w*, asegúrese de que se cree `/run/utmp` en el momento del arranque. Consulte [utmp(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/utmp.5) para más detalles.

#### Conectar a un socket acpid

Además de los archivos de reglas, acpid acepta conexiones en un socket de dominio UNIX, de forma predeterminada `/var/run/acpid.socket`. Las aplicaciones de usuario pueden conectarse a este socket.

```
#!/bin/bash
coproc acpi_listen
trap 'kill $COPROC_PID' EXIT

while read -u "${COPROC[0]}" -a event; do
    *handler.sh* "${event[@]}"
done

```

Donde *handler.sh* puede ser una script similar a `/etc/acpi/handler.sh`.

## Consulte también

*   [Página principal de acpid](http://acpid.sourceforge.net/)
*   [Wiki de Gentoo](https://wiki.gentoo.org/wiki/ACPI#Configuration)