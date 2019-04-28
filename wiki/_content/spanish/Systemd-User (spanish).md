Artículos relacionados

*   [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [Automatic login to virtual console (Español)](/index.php/Automatic_login_to_virtual_console_(Espa%C3%B1ol) "Automatic login to virtual console (Español)")
*   [Start X at Login (Español)](/index.php/Start_X_at_Login_(Espa%C3%B1ol) "Start X at Login (Español)")

[systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") ofrece a los usuarios la capacidad de ejecutar una instancia de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") para gestionar la sesión y los servicios. Esto permite a los usuarios iniciar, detener, habilitar y deshabilitar las unidades que se encuentren dentro de ciertas carpetas cuando systemd se ejecuta por el usuario. Esto es conveniente para los demonios y otros servicios que normalmente se ejecutan como un usuario diferente a root o un usuario especial, como por ejemplo [mpd](/index.php/Mpd "Mpd")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuración desde systemd 206](#Configuración_desde_systemd_206)
    *   [1.1 D-Bus](#D-Bus)
    *   [1.2 Inicio de sesión automático en Xorg sin gestor de pantallas](#Inicio_de_sesión_automático_en_Xorg_sin_gestor_de_pantallas)
    *   [1.3 Puesta en marcha automática de instancias de usuario de systemd](#Puesta_en_marcha_automática_de_instancias_de_usuario_de_systemd)
*   [2 Configuración](#Configuración)
    *   [2.1 Utilizar /usr/lib/systemd/systemd --user para gestionar la propia sesión](#Utilizar_/usr/lib/systemd/systemd_--user_para_gestionar_la_propia_sesión)
    *   [2.2 Inicio de sesión automático](#Inicio_de_sesión_automático)
    *   [2.3 Otros casos de uso](#Otros_casos_de_uso)
        *   [2.3.1 Multiplexor de terminal persistente](#Multiplexor_de_terminal_persistente)
            *   [2.3.1.1 Iniciar X](#Iniciar_X)
*   [3 Servicios de ususario](#Servicios_de_ususario)
    *   [3.1 Unidades instaladas por los paquetes](#Unidades_instaladas_por_los_paquetes)
    *   [3.2 Ejemplo](#Ejemplo)
    *   [3.3 Ejemplo con variables](#Ejemplo_con_variables)
    *   [3.4 Nota acerca de las aplicaciones X](#Nota_acerca_de_las_aplicaciones_X)
*   [4 Véase también](#Véase_también)

## Configuración desde systemd 206

**Nota:** Las sesiones de usuario están en desarrollo, por lo que faltan algunas características, que aún no están apoyadas por los desarrolladores. Véase [[1]](http://lists.freedesktop.org/archives/systemd-devel/2013-July/012392.html) y [[2]](http://lists.freedesktop.org/archives/systemd-devel/2013-August/012517.html) para obtener más detalles sobre el estado actual del asunto.

Desde la versión 206, el mecanismo para instancias de usuario de systemd ha cambiado. Ahora el módulo `pam_systemd.so` lanza una instancia de usuario, por defecto, en el primer inicio de sesión de un usuario, iniciando `user@.service`. En el estado actual, existen algunas diferencias con respecto a versiones anteriores de systemd, que hay que tener en cuenta:

*   La instancia `systemd --user` se ejecuta fuera de cualquier sesión de usuario. Esto está bien para correr, por ejemplo `mpd`, pero puede ser molesto si uno trata de iniciar un gestor de ventanas desde la instancia de usuario de systemd. Entonces polkit evita montar usb, reinicar, etc., como un usuario normal, porque el gestor de ventanas se ha ejecutado fuera de la sesión activa.
*   Las unidades en la instancia de usuario no heredan cualquier entorno, por lo que se debe fijar manualmente.
*   `user-session@.service` de [user-session-units](https://aur.archlinux.org/packages/user-session-units/) está ahora obsoleto.

Pasos para utilizar las unidades de instancia de usuario:

1\. Asegúrese de que la instancia de usuario de systemd se inicia correctamente. Puede comprobar esto con: `systemctl --user status` Desde systemd 206 debe haber una instancia de usuario ejecutando systemd por defecto, que se inicia en el módulo pam `pam_systemd.so` para la primera sesión de un usuario.
**Nota:** system-login necesita para comenzar de pam_systemd: este debe contener `-session optional pam_systemd.so`; compruebe si existe el archivo *.pacnew*.

2\. Agregue las variables de entorno que necesita, en un párrafo en el archivo de configuración para `user@.service`. Al menos, debe contener lo siguiente:

 `/etc/systemd/system/user@.service.d/environment.conf` 
```
[Service]
Environment=DISPLAY=:0

```

3\. Ponga todas sus unidades de usuario en `~/.config/systemd/user`. Cuando inicie la instancia de usuario, lance el target predeterminado `~/.config/systemd/user/default.target`. Después de eso, se pueden manejar las unidades de usuario con `systemctl --user`.

### D-Bus

Para utilizar [dbus](/index.php/D-Bus_(Espa%C3%B1ol) "D-Bus (Español)") en unidades de usuario, cree los siguientes archivos:

 `/etc/systemd/user/dbus.socket` 
```
[Unit]
Description=D-Bus Message Bus Socket
Before=sockets.target

[Socket]
ListenStream=/run/user/%U/dbus/user_bus_socket

[Install]
WantedBy=default.target

```
 `/etc/systemd/user/dbus.service` 
```
[Unit]
Description=D-Bus Message Bus
Requires=dbus.socket

[Service]
ExecStart=/usr/bin/dbus-daemon --session --address=systemd: --nofork --nopidfile --systemd-activation
ExecReload=/usr/bin/dbus-send --print-reply --session --type=method_call --dest=org.freedesktop.DBus / org.freedesktop.DBus.ReloadConfig

```

Active el socket ejecutando:

```
# systemctl --global enable dbus.socket

```

La unidad `user@.service` que lanza la instancia systemd del usuario, exporta, por defecto, la siguiente ruta de bus:

```
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/%I/dbus/user_bus_socket

```

que se propaga para los servicios que se ejecutan en esta instancia. Sin embargo, se ha sugerido que cada sesión de usuario debe tener su propia instancia de demonio dbus (lo que significa que debe usar, por ejemplo, el esqueleto [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)"), que inicia el demonio dbus para la sesión de Xorg ). Hay un debate en curso sobre este tema en la [lista de correo de systemd](http://lists.freedesktop.org/archives/systemd-devel/2013-March/009422.html). Como la decisión final no se ha tomado todavía, no existe una solución oficial.

### Inicio de sesión automático en Xorg sin gestor de pantallas

Se necesita tener [#D-Bus](#D-Bus) correctamente configurado y [xlogin-git](https://aur.archlinux.org/packages/xlogin-git/) instalado.

Configure [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") desde el esqueleto, para que le suministre los archivos en `/etc/X11/xinit/xinitrc.d/`. El funcionamiento de `~/.xinitrc` no debe retornar a sí mismo, por lo que o bien tiene `wait` como última orden, o añada `exec` a la última orden que es llamada y que no debe consistir en retornar (por ejemplo, llamar al gestor de ventanas).

La sesión utilizará su propio demonio dbus, pero varias utilidades systemd necesitarán la instancia `dbus.service`. Una posible solución a esto es crear alias para estas órdenes:

 `~/.bashrc` 
```
for sd_cmd in systemctl systemd-analyze systemd-run; do
    alias $sd_cmd='DBUS_SESSION_BUS_ADDRESS="unix:path=$XDG_RUNTIME_DIR/dbus/user_bus_socket" '$sd_cmd
done

```

Por último, active (**como root**) el servicio *xlogin* para iniciar automáticamente sesión al arrancar:

```
# systemctl enable xlogin@*nombredeusuario*

```

La sesión de usuario se desarrolla enteramente dentro de un espacio systemd y todo en la sesión de usuario debería funcionar bien.

### Puesta en marcha automática de instancias de usuario de systemd

La instancia de usuario de systemd es, por defecto, ejecutada después del primer inicio de sesión de un usuario, pero, a veces, puede ser útil empezar aquella después del arranque. Lingering se utiliza para generar la instancia de usuario systemd en el arranque y que siga funcionando después del cierre de sesión.

**Advertencia:** Los servicios de systemd **no** son sesiones, se ejecutan fuera de *logind*. No utilice lingering para permitir el inicio de sesión automática, ya que [rompe la sesión](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").

Utilice la siguiente orden para activar lingering para el usuario específico:

```
# loginctl enable-linger *nombredeusuario*

```

## Configuración

### Utilizar /usr/lib/systemd/systemd --user para gestionar la propia sesión

Systemd tiene muchas características sorprendentes, una de ellas es la capacidad de hacer un seguimiento de los programas utilizando cgroups (ejecutando `systemctl status`). Aunque esto es realmente útil para un sistema de init en cuyo proceso hay un **pid 1**, también es muy útil para los usuarios que quieran utilizar esta función para iniciar automáticamente los programas de los mismos, haciendo un seguimiento simultáneamente del contenido de cada cgrupo.

Todas las unidades de usuario de systemd residirán en `$HOME/.config/systemd/user`. Estas unidades tienen prioridad sobre otras unidades en residentes en otros directorios de unidades de systemd.

Necesitamos dos paquetes para conseguir este trabajo, por un lado, el disponible actualmente desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"): [systemd-xorg-launch-helper-git](https://aur.archlinux.org/packages/systemd-xorg-launch-helper-git/) y, opcionalmente, por otro lado, [systemd-user-session-units-git](https://aur.archlinux.org/packages/systemd-user-session-units-git/) si desea trabajar con autologin.

Lo siguiente será crear los targets (*«objetivos»*). Configuraremos dos: uno para el gestor de ventanas, y otro como un target por defecto. El target del gestor de ventanas debe ser similar a lo siguiente:

 `$HOME/.config/systemd/user/wm.target` 
```
[Unit]
Description=Window manager target
Wants=xorg.target
Wants=mystuff.target
Requires=dbus.socket
AllowIsolate=true

[Install]
Alias=default.target

```

Este será el target de su interfaz gráfica.

Crearemos un segundo target llamado `mystuff.target`. Valdrá para todos los servicios, pero debe contener el gestor de ventanas elegido en la línea `WantedBy`, bajo `[Install]`, señalando a esta unidad.

 `$HOME/.config/systemd/user/mystuff.target` 
```
[Unit]
Description=Xinitrc Stuff
Wants=wm.target

[Install]
Alias=default.target

```

Crearemos un enlace simbólico de nombre `default.target`. Cuando se inicie `/usr/lib/systemd/systemd --user`, dicho target vendrá iniciado también.

Por último, nececitamos escribir varios archivos de servicios correspondientes a los servicios que deben comenzar. Para ello, asociaremos un servicio al gestor de ventanas.

 `$HOME/.config/systemd/user/YOUR_WM.service` 
```
[Unit]
Description=your window manager service
Before=mystuff.target
After=xorg.target
Requires=xorg.target

[Service]
#Environment=PATH=uncomment:to:override:your:PATH
ExecStart=/full/path/to/wm/executable
Restart=always
RestartSec=10

[Install]
WantedBy=wm.target

```

**Nota:** La sección `[Install]` incluye el valor 'WantedBy'. Cuando usamos `systemctl --user enable` se asocia a este como `$HOME/.config/systemd/user/wm.target.wants/YOUR_WM.service`, lo que le permite arrancarlo al iniciar sesión. Se recomienda activar este servicio, en lugar de unirlo de forma manual.

Se puede poblar el directorio de unidades de usuario con una gran cantidad de servicios, incluyendo, a modo de ejemplo, algunos como **mpd**, **gpg-agent**, **offlineimap**, **parcellite**, **pulse**, **tmux**, **urxvtd**, **xbindkeys** y **xmodmap**.

Para salir de su sesión, utilice `systemctl --user exit`.

### Inicio de sesión automático

Si se quiere iniciar sesión automáticamente al arrancar con systemd, es posible utilizar la unidad correspondiente proporcionada por el paquete user-session-units. Considere la posibilidad de activar una pantalla locker para evitar que cualquier pueda valerse de la sesión recién iniciada. Añada esta línea a `/etc/pam.d/login` y a `/etc/pam.d/system-auth`:

 `session    required    pam_systemd.so` 

Debido a que `user-session@.service` viene iniciado en tty1, será necesario añadir `Conflicts=getty@tty1.service` al archivo de servicio en cuestión, si no existe ya. Como alternativa, puede hacer que se ejecute en tty7 en su lugar, modificando `TTYPath` en consecuencia, así como la línea `ExecStart` en `xorg.service` (`cp /usr/lib/systemd/user/xorg.service /etc/systemd/user/` y haciendo las modificaciones allí).

Una vez hecho esto, ejecute `systemctl --user enable` `YOUR_WM.service`

**Nota:** Hay que prestar atención a la tty de modo que la sesión de systemd esté marcada como activa. Systemd establece una sesión como inactiva cuando la tty activa es diferente de aquella en la cual se ha inicio sesión. Esto significa que el servidor X se debe ejecutar en la misma tty especificada en `user-session@.service`. Si la tty en `TTYPath` no coincide con el xorg lanzado, la sesión de systemd estará inactiva desde el punto de vista de las aplicaciones de X, y no será capaz de montar las unidades USB, por ejemplo.

Una de las cosas más importantes es añadir al propio archivo de servicio el uso de `Before=` y `After=` en la sección `[Unit]`. Esto permitirá determinar el orden de inicio de los servicios. Pongamos por caso que queremos disponer de una aplicación gráfica que se inicie al arranque, para ello será necesario añadir `After=xorg.target` a la propia sección unit. Otro caso, como por ejemplo iniciar **ncmpcpp**, el cual requiere **mpd** para funcionar, será necesario añadir `After=mpd.service` a la sección unit de ncmpcpp. El tiempo y la experiencia arrojarán luz sobre cómo gestionar el orden de inicio de las aplicaciones, o bien consultando la página de man de systemd. Comenzar con [systemd.unit(5)](http://www.freedesktop.org/software/systemd/man/systemd.unit.html) sería una buena idea.

### Otros casos de uso

#### Multiplexor de terminal persistente

Es posible que quiera utilizar la propia sesión de usuario para iniciar un multiplexor de terminal como [GNU Screen](/index.php/GNU_Screen "GNU Screen") o [Tmux](/index.php/Tmux "Tmux"), como fondo de pantalla para conectarse, en lugar de iniciar la sesión de un gestor de ventanas. Separar el login del login gráfico es probablemente útil para los usuarios que efectuan el arranque en una TTY, en lugar de utilizar un gestor de pantallas (en cuyo caso es posible insertar todos los programas de arranque en el target myStuff.target).

Para crear este tipo de sesión de usuario, proceda como se indica anteriormente, pero en lugar de crear wm.target, cree multiplexer.target:

```
[Unit]
Description=Terminal multiplexer
Documentation=info:screen man:screen(1) man:tmux(1)
After=cruft.target
Wants=cruft.target

[Install]
Alias=default.target
```

El target `cruft.target`, similar a myStuff.target, debería ocuparse de todos aquellos programas que consideremos que deberían empezar antes que tmux o screen (o que queremos iniciar al arranque independientemente del tiempo), como por ejemplo una sesión del demonio GnuPG.

Para todo esto, será necesario crear un servicio para la propia sesión del multiplexor. He aquí un servicio de muestra que utiliza tmux como ejemplo y provee una sesión gpg-agent que escribe la propia información en /tmp/gpg-agent-info. Esta sesión de muestra, al tiempo que inicia X, también es capaz de hacer correr programas gráficos, desde el momento en que la variable DISPLAY es ajustada.

```
[Unit]
Description=tmux: A terminal multiplixer Documentation=man:tmux(1)
After=gpg-agent.service
Wants=gpg-agent.service

[Service]
Type=forking
ExecStart=/usr/bin/tmux start
ExecStop=/usr/bin/tmux kill-server
Environment=DISPLAY=:0
EnvironmentFile=/tmp/gpg-agent-info

[Install]
WantedBy=multiplexer.target
```

Una vez hecho esto, `systemctl --user enable`, `tmux.service`, `multiplexer.target` y cualquier otro programa creado, serán ejecutados por `cruft.target`. Active `user-session@.service` como se describió antes, pero asegúrese de retirar el servicio `Conflicts=getty@tty1.service` de `user-session@.service`, puesto que la sesión de usuario no se hará cargo de una TTY. ¡Enhorabuena! ¡Ahora tiene un multiplexor de terminal en funcionamiento y otros programas útiles listos para iniciar en el arranque!

##### Iniciar X

Habrá podido advertir que, desde el multiplexor de terminal es ahora `default.target`. X no se iniciará automáticamente en el arranque. Para iniciar X, proceda como antes, pero no active o enlace manualmente `wm.target` a `default.target`. En su lugar, asumiendo que arranca desde un terminal, vamos a utilizar simplemente una solución temporal y enmascarar `/usr/bin/startx` con un alias de shell:

 `alias startx='systemctl --user start wm.target'` 

## Servicios de ususario

Ahora los usuarios pueden interactuar con las unidades ubicadas en los carpetas relacionadas más abajo, tal como lo harían con los servicios del sistema (carpetas ordenadas por prioridad ascendente):

*   `/usr/lib/systemd/user/`
*   `/etc/systemd/user/`
*   `~/.config/systemd/user/`

Para el control de la instancia de systemd, se debe utilizar la orden `systemctl --user`.

### Unidades instaladas por los paquetes

Una unidad proveída por un paquete está destinada a ser ejecutada por una instancia de usuario de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") que instalará la unidad en `/usr/lib/systemd/user/`. La administración del sistema puede modificar la unidad copiándola a `/etc/systemd/user/`. Un usuario puede modificar la unidad copiándola a `~/.config/systemd/user/`.

### Ejemplo

El siguiente es un ejemplo de una versión de `mpd.service` realizada por el usuario:

```
[Unit]
Description=Music Player Daemon

[Service]
ExecStart=/usr/bin/mpd --no-daemon

[Install]
WantedBy=default.target

```

### Ejemplo con variables

El siguiente es un ejemplo de una versión de usuario de `sickbeard.service`, que tiene en cuenta los directorios home como variable, donde SickBeard puede encontrar ciertos archivos:

```
[Unit]
Description=SickBeard Daemon

[Service]
ExecStart=/usr/bin/env python2 /opt/sickbeard/SickBeard.py --config %h/.sickbeard/config.ini --datadir %h/.sickbeard

[Install]
WantedBy=default.target

```

Como se detalla en [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5), la variable `%h` es reemplazada por la carpeta home del usuario que ejecuta el servicio. Hay otras variables en las manpages de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") que puede tenerlas en cuenta.

### Nota acerca de las aplicaciones X

La mayoría de las aplicaciones X necesita una variable `DISPLAY` para ser iniciada (si el propio servicio no se ha iniciado, con lo cual es la primera cosa a controlar), así que hay que asegurarse de incluir lo siguiente:

 `$HOME/.config/systemd/user/parcellite.service` 
```
[Unit]
Description=Parcellite clipboard manager

[Service]
ExecStart=/usr/bin/parcellite
Environment=DISPLAY=:0 # <= !

[Install]
WantedBy=mystuff.target

```

Una manera más simple, si se utiliza [user-session-units](https://aur.archlinux.org/packages/user-session-units/), es definirlo en `user-session@yourloginname.service` que lo heredará. Añada `Environment=DISPLAY=:0` a la sección `[Service]`. Otra variable de entorno útil para establecer aquí es `SHELL`.

Sin embargo, será preferible **no** insertar directamente el valor de la variable DISPLAY en el servicio (especialmente si se ejecuta más de una respecto a la pantalla):

 `$HOME/.config/systemd/user/x-app-template@.service` 
```
[Unit]
Description=Your amazing and original description

[Service]
ExecStart=/full/path/to/the/app
Environment=DISPLAY=%i # <= !

[Install]
WantedBy=mystuff.target

```

A continuación, se puede ejecutar con:

```
systemctl --user {start|enable} x-app@your-desired-display.service # <= :0 in most cases

```

Algunas aplicaciones X pueden no ponerse en marcha porque el socket de la pantalla aún no está disponible. Esto se puede solucionarlo mediante la adición de algo así:

 `$HOME/.config/systemd/user/x-app-template@.service` 
```
[Unit]
After=xorg.target
Requires=xorg.target

...

```

a sus unidades (el target `xorg.target` es parte del paquete [xorg-launch-helper](https://aur.archlinux.org/packages/xorg-launch-helper/)).

## Véase también

*   [KaiSforza's bitbucket wiki](https://bitbucket.org/KaiSforza/systemd-user-units/wiki/Home)
*   [Zoqaeski's units on Github](https://github.com/zoqaeski/systemd-user-units)
*   [Collection of useful systemd user units](https://github.com/grawity/systemd-user-units)
*   [More systemd user units](https://bitbucket.org/KaiSforza/systemd-user-units)
*   [Forum thread about changes in systemd 206 user instances](https://bbs.archlinux.org/viewtopic.php?id=167115)