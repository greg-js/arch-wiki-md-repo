Artículos relacionados

*   [Display manager (Español)](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)")

[SLiM](http://slim.berlios.de/) es un acronimo de Simple Login Manager. Slim es simple, ligero y fácilmente configurable. Slim es usado por algunos, ya que no requiere dependencias de [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") o [KDE](/index.php/KDE "KDE") y puede ayudar a hacer un sistema más claro para los usuarios que les gusta usar escritorios ligeros como [Xfce](/index.php/Xfce "Xfce"), [Openbox](/index.php/Openbox "Openbox") o [Fluxbox](/index.php/Fluxbox "Fluxbox").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Habilitando SLiM](#Habilitando_SLiM)
    *   [2.2 Un solo manejador de ventanas](#Un_solo_manejador_de_ventanas)
    *   [2.3 Logueo Automático](#Logueo_Automático)
    *   [2.4 Múltiples gestores de ventanas](#Múltiples_gestores_de_ventanas)
    *   [2.5 Temas](#Temas)
        *   [2.5.1 Utilizar imagen personalizada como fondo de login](#Utilizar_imagen_personalizada_como_fondo_de_login)
        *   [2.5.2 Configuración de pantalla dual](#Configuración_de_pantalla_dual)
*   [3 Otras opciones](#Otras_opciones)
    *   [3.1 Cambiando el cursor](#Cambiando_el_cursor)
    *   [3.2 Igualar fondos de SLiM y de fondo de pantalla](#Igualar_fondos_de_SLiM_y_de_fondo_de_pantalla)
    *   [3.3 Apagar, reiniciar, suspender, ejecutar, ejecutar terminal desde SLiM](#Apagar,_reiniciar,_suspender,_ejecutar,_ejecutar_terminal_desde_SLiM)
    *   [3.4 SLiM da error con el demonio en rc.d](#SLiM_da_error_con_el_demonio_en_rc.d)
    *   [3.5 Error de apagado con Splashy](#Error_de_apagado_con_Splashy)
    *   [3.6 Usar un tema aleatorio](#Usar_un_tema_aleatorio)
*   [4 Todas las opciones de SLiM](#Todas_las_opciones_de_SLiM)
*   [5 Fuentes](#Fuentes)

## Instalación

Instalando SLiM de los repositorios **extra**:

```
# pacman -S slim

```

## Configuración

### Habilitando SLiM

SLiM puede ser cargado en el arranque añadiéndolo a la lista de Demonios en `rc.conf` o modificando `inittab`. Mire [Display manager](/index.php/Display_manager "Display manager") para instrucciones mas detalladas.

### Un solo manejador de ventanas

Para configurar SLim para cargar un solo entorno, edite su archivo [~/.xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") :

```
#!/bin/sh

#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

exec [session-command]

```

Reemplace `[session-command]` Con su correspondiente comando de sesión. Algunos ejemplos para los diferentes diferentes escritorios:

```
exec awesome
exec dwm
exec fluxbox
exec fvwm2
exec gnome-session
exec openbox-session
exec startkde
exec startlxde
exec startxfce4

```

Si su gestor de ventanas no esta en esta lista, consulte su a su correspondiente pagina wiki.

### Logueo Automático

Para hacer SLiM inicie sesión con un usuario especifico (para evitar tipear una contraseña) las siguientes lineas en /etc/slim.conf deben ser cambiadas:

```
# default_user        simone

```

Descomente esta linea, y cambie "simone" por el usuario que se va a loguear automáticamente.

```
# auto_login          no

```

Descomente esta linea y cambie el "no" por "yes". Esto habilita el auto logueo.

### Múltiples gestores de ventanas

Para poder elegir entre varios entornos de escritorio, SLIM se puede configurar para inicie con lo que usted elija.

Ponga una declaración como esta en su archivo `~/.xinitrc` y edite la variable de sesiones en `/etc/slim.conf` para que coincida con los nombres que desencadenan la declaración del caso. Puede elegir el gestor de ventanas en el momento de entrada pulsando la tecla F1\. Tenga en cuenta que esta característica es experimental.

```
# The following variable defines the session which is started if the user doesn't explicitly select a session
# Source: http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample

DEFAULT_SESSION=twm

case $1 in
kde)
	exec startkde
	;;
xfce4)
	exec startxfce4
	;;
icewm)
	icewmbg &
	icewmtray &
	exec icewm
	;;
wmaker)
	exec wmaker
	;;
blackbox)
	exec blackbox
	;;
*)
	exec $DEFAULT_SESSION
	;;
esac

```

### Temas

Instale el paquete [slim-themes](https://www.archlinux.org/packages/?name=slim-themes):

```
# pacman -S slim-themes archlinux-themes-slim

```

El paquete [slim-themes](https://www.archlinux.org/packages/?name=slim-themes) contiene varios temas diferentes. Mire en el directorio `/usr/share/slim/themes` para ver los temas disponibles. Reemplace 'current_theme'por el nombre del tema elegido en `/etc/slim.conf`:

```
#current_theme       default
current_theme       archlinux-simplyblack

```

Para una vista previa de los temas, ejecute el siguiente comando mientras esta activa una instancia de Xorg:

```
$ slim -p /usr/share/slim/themes/<theme name>

```

Para cerrar, escriba "exit" en la linea de logueo y pulse Enter.

Temas adicionales se encuentran disponibles en [AUR](/index.php/AUR "AUR").

#### Utilizar imagen personalizada como fondo de login

Puede usar cualquier tema instalado o el tema por defecto de SLiM para utilizar la imagen de su elección.

Primero se debe asegurar que el tema que se desea personalizar está configurado como tema actual en el archivo de configuración de SLiM

```
# current_theme       <nombre_tema> (por ejemplo: default, archlinux-simplyblack)

```

Después se debe reemplazar el archivo background.jpg del tema actual con la imagen deseada

```
# mv /usr/share/slim/themes/<nombre_tema>/background.jpg{,.bck}
# cp /path/to/image.jpg /usr/share/slim/themes/<nombre_tema>/background.jpg

```

Se puede previsualizar la nueva imagen de login con el comando

```
# slim -p /usr/share/slim/themes/<nombre_tema>

```

#### Configuración de pantalla dual

Puede personalizar el tema de SLiM en /usr/share/slim/themes/<your-theme>/slim.theme para cambiar estos porcentajes. La caja en si misma es de 450 pixeles por 250 pixeles:

```
input_panel_x           50%
input_panel_y           50%

```

en valores de pixeles:

```
# Esta configuración en el tema "archlinux-simplyblack" pone el panel en el centro, en una pantalla de 1440x900
input_panel_x           495
input_panel_y           325

```

```
# Esta configuración en el tema "archlinux-retro" pone el panel en el centro, en una pantalla de 1680x1050
input_panel_x           615
input_panel_y           400

```

Si su tema tiene un imagen de fondo, debería usar la configuración background_style ('stretch', 'tile', 'center' o 'color') para que se vea correctamente. Observe la documentación oficial en [very simple and clear official documentation about slim themes](http://slim.berlios.de/themes_howto.php) para mas detalles.

## Otras opciones

Algunas cosas que puede probar;

### Cambiando el cursor

Si quiere cambiar el cursor por defecto, hay mas disponibles en este paquete [slim-cursor](https://aur.archlinux.org/packages/slim-cursor/)

Después de instalarlo, edite el archivo `/etc/slim.conf` y descomente la linea;

```
cursor   left_ptr

```

Esto pondrá un cursor normal en su lugar. Esta configuración afecta a `xsetroot -cursor_name`. Puede ver los nombres de posibles cursores en [here](http://cvsweb.xfree86.org/cvsweb/*checkout*/xc/lib/X11/cursorfont.h?rev=HEAD&content-type=text/plain) o en `/usr/share/icons/<your-cursor-theme>/cursors/`.

Para cambiar el modelo del cursor en la pantalla de logueo, cree un archivo llamado `/usr/share/icons/default/index.theme` con este contenido:

```
[Icon Theme]
Inherits=<your-cursor-theme>

```

Reemplace <your-cursor-theme> con el nombre del tema que se desea usar (por ejemplo whiteglass).

### Igualar fondos de SLiM y de fondo de pantalla

Para compartir el fondo de pantalla entre SLiM y su escritorio, renombre la imagen de fondo, luego cree un enlace desde la imagen de escritorio hacia el tema por defecto de SliM:

```
# mv /usr/share/slim/themes/default/background.jpg{,.bck}
# ln -s /path/to/mywallpaper.jpg /usr/share/slim/themes/default/background.jpg

```

### Apagar, reiniciar, suspender, ejecutar, ejecutar terminal desde SLiM

Se puede Apagar, reiniciar, suspender, ejecutar, ejecutar terminal desde la pantalla de logueo de SLiM. Para esto, use la caja donde tipea el usuario, y la contraseña de root en la caja donde se tipea la contraseña:

*   Para iniciar una terminal, ingrese **console** como el usuario (por defecto usa xterm que debe ser instalado por separado... edite `/etc/slim.conf` para cambiar las preferencias de terminal)
*   Para apagar, ingrese **halt** como usuario
*   Para reiniciar, ingrese **reboot** como usuario
*   Para salir al bash, ingrese **exit** como usuario
*   Para suspender, ingrese **suspend** como usuario (suspender esta desabilitado por defecto, edite el archivo `/etc/slim.conf` como root para descomentar esta linea `suspend_cmd`)

### SLiM da error con el demonio en rc.d

Si inicializa SLiM agregando el demonio en `/etc/rc.conf` y esto falla al iniciar es probable que sea cuestion de un archivo bloqueado. SLiM crea un archivo de bloqueo en `/var/lock`, sin embargo en cada inicializacion la mayoria de las veces la carpeta en /var no existe, causando que SLiM no inicie. Verifique que la carpeta `/var/lock` existe y en caso contrario creela con este comando:

```
# mkdir /var/lock/

```

### Error de apagado con Splashy

Si usa Splashy y SLiM, aveces no podra apagar o reiniciar desde el menu en GNOME,Xfce, LXDE o otros. Verifique el archivo `/etc/slim.conf` y setee DEFAULT_TTY=7 como xserver_arguments vt07.

### Usar un tema aleatorio

En la variable current_theme ponga todos los temas a elegir aleatoriamente separados por comas.

## Todas las opciones de SLiM

Aqui hay una lista de todas las opciones para configurar SLiM:

**Note:** welcome_msg allows 2 variables **%host** and **%domain**
sessionstart_cmd allows **%user** *(execd right before login_cmd)* and it is also allowed in sessionstop_cmd
login_cmd allows **%session** and **%theme**

| Option Name | Default Value |
| default_path | <tt>/bin:/usr/bin:/usr/local/bin</tt> |
| default_xserver | <tt>/usr/bin/X</tt> |
| xserver_arguments | <tt>vt07 -auth /var/run/slim.auth</tt> |
| numlock |
| daemon | <tt>yes</tt> |
| xauth_path | <tt>/usr/bin/xauth</tt> |
| login_cmd | <tt>exec /bin/bash -login ~/.xinitrc %session</tt> |
| halt_cmd | <tt>/sbin/shutdown -h now</tt> |
| reboot_cmd | <tt>/sbin/shutdown -r now</tt> |
| suspend_cmd |
| sessionstart_cmd |
| sessionstop_cmd |
| console_cmd | <tt>/usr/bin/xterm -C -fg white -bg black +sb -g %dx%d+%d+%d -fn %dx%d -T</tt> |
| screenshot_cmd | <tt>import -window root /slim.png</tt> |
| welcome_msg | <tt>Welcome to %host</tt> |
| session_msg | <tt>Session:</tt> |
| default_user |
| focus_password | <tt>no</tt> |
| auto_login | <tt>no</tt> |
| current_theme | <tt>default</tt> |
| lockfile | <tt>/var/run/slim.lock</tt> |
| logfile | <tt>/var/log/slim.log</tt> |
| authfile | <tt>/var/run/slim.auth</tt> |
| shutdown_msg | <tt>The system is halting...</tt> |
| reboot_msg | <tt>The system is rebooting...</tt> |
| sessions | <tt>wmaker,blackbox,icewm</tt> |
| sessiondir |
| hidecursor | <tt>false</tt> |
| input_panel_x | <tt>50%</tt> |
| input_panel_y | <tt>40%</tt> |
| input_name_x | <tt>200</tt> |
| input_name_y | <tt>154</tt> |
| input_pass_x | <tt>-1</tt> |
| input_pass_y | <tt>-1</tt> |
| input_font | <tt>Verdana:size=11</tt> |
| input_color | <tt>#000000</tt> |
| input_cursor_height | <tt>20</tt> |
| input_maxlength_name | <tt>20</tt> |
| input_maxlength_passwd | <tt>20</tt> |
| input_shadow_xoffset | <tt>0</tt> |
| input_shadow_yoffset | <tt>0</tt> |
| input_shadow_color | <tt>#FFFFFF</tt> |
| welcome_font | <tt>Verdana:size=14</tt> |
| welcome_color | <tt>#FFFFFF</tt> |
| welcome_x | <tt>-1</tt> |
| welcome_y | <tt>-1</tt> |
| welcome_shadow_xoffset | <tt>0</tt> |
| welcome_shadow_yoffset | <tt>0</tt> |
| welcome_shadow_color | <tt>#FFFFFF</tt> |
| intro_msg |
| intro_font | <tt>Verdana:size=14</tt> |
| intro_color | <tt>#FFFFFF</tt> |
| intro_x | <tt>-1</tt> |
| intro_y | <tt>-1</tt> |
| background_style | <tt>stretch</tt> |
| background_color | <tt>#CCCCCC</tt> |
| username_font | <tt>Verdana:size=12</tt> |
| username_color | <tt>#FFFFFF</tt> |
| username_x | <tt>-1</tt> |
| username_y | <tt>-1</tt> |
| username_msg | <tt>Please enter your username</tt> |
| username_shadow_xoffset | <tt>0</tt> |
| username_shadow_yoffset | <tt>0</tt> |
| username_shadow_color | <tt>#FFFFFF</tt> |
| password_x | <tt>-1</tt> |
| password_y | <tt>-1</tt> |
| password_msg | <tt>Please enter your password</tt> |
| msg_color | <tt>#FFFFFF</tt> |
| msg_font | <tt>Verdana:size=16:bold</tt> |
| msg_x | <tt>40</tt> |
| msg_y | <tt>40</tt> |
| msg_shadow_xoffset | <tt>0</tt> |
| msg_shadow_yoffset | <tt>0</tt> |
| msg_shadow_color | <tt>#FFFFFF</tt> |
| session_color | <tt>#FFFFFF</tt> |
| session_font | <tt>Verdana:size=16:bold</tt> |
| session_x | <tt>50%</tt> |
| session_y | <tt>90%</tt> |
| session_shadow_xoffset | <tt>0</tt> |
| session_shadow_yoffset | <tt>0</tt> |
| session_shadow_color | <tt>#FFFFFF</tt> |

## Fuentes

*   [SLiM homepage](http://slim.berlios.de/)
*   [SLiM documentation](http://slim.berlios.de/manual.php)