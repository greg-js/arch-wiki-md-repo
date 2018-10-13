**Estado de la traducción**
Este artículo es una traducción de [Xinit](/index.php/Xinit "Xinit"), revisada por última vez el **2018-10-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Xinit&diff=0&oldid=535133) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Administrador de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)")
*   [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)")
*   [xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)")
*   [Xresources](/index.php/Xresources "Xresources")

De [Wikipedia](https://en.wikipedia.org/wiki/es:xinit "wikipedia:es:xinit"):

	El programa **xinit** permite a un usuario iniciar manualmente un servidor de pantalla [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"). El script [startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1) es un front-end para [xinit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1).

*xinit* y *startx* toman un argumento opcional de la aplicación cliente. Si no proporciona uno, buscarán `~/.xinitrc` para ejecutarse como un script del intérprete de línea de órdenes para iniciar las aplicaciones cliente. Executar `xinit /usr/bin/foo` es por lo tanto equivalente a ejecutar `xinit` con `exec foo` en su `~/.xinitrc`.

*xinit* se utiliza normalmente para iniciar [administradores de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") o [entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)"). Aunque también puede utilizar *xinit* para ejecutar aplicaciones gráficas sin un administrador de ventanas, muchas aplicaciones gráficas esperan un administrador de ventanas compatible con [Wikipedia:Extended Window Manager Hints](https://en.wikipedia.org/wiki/Extended_Window_Manager_Hints inician [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") y, generalmente, [xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)").

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 xinitrc](#xinitrc)
    *   [2.2 xserverrc](#xserverrc)
*   [3 Utilización](#Utilizaci.C3.B3n)
*   [4 Inicio automático de X al inicio de sesión](#Inicio_autom.C3.A1tico_de_X_al_inicio_de_sesi.C3.B3n)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Override xinitrc from command line](#Override_xinitrc_from_command_line)
    *   [5.2 Switching between desktop environments/window managers](#Switching_between_desktop_environments.2Fwindow_managers)
    *   [5.3 Starting applications without a window manager](#Starting_applications_without_a_window_manager)
    *   [5.4 Output redirection using startx](#Output_redirection_using_startx)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit).

## Configuración

### xinitrc

Si `.xinitrc` está presente en el directorio personal del usuario, *startx* y *xinit* lo ejecutan. De lo contrario, *startx* ejecutará el `/etc/X11/xinit/xinitrc` predeterminado.

**Nota:** *Xinit* tiene su propio comportamiento predeterminado en lugar de ejecutar el archivo. Véase [xinit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1) para más detalles.

Este xinitrc predeterminado iniciará un entorno básico con [Twm](/index.php/Twm "Twm"), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) y [Xterm](/index.php/Xterm "Xterm") (asumiendo que los paquetes necesarios estén instalados). Por lo tanto, para iniciar un administrador de ventanas o un entorno de escritorio diferente, primero cree una copia del `xinitrc` predeterminado en su directorio personal:

```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc

```

Luego [edite](/index.php/Help:Reading_(Espa%C3%B1ol)#Adjuntar.2C_a.C3.B1adir.2C_crear_.2C_editar "Help:Reading (Español)") el archivo y reemplace los programas predeterminados con las órdenes deseadas. Recuerde que las líneas que siguen a una orden utilizando `exec` serían ignoradas. Por ejemplo, para iniciar `xscreensaver` en segundo plano y luego iniciar [openbox](/index.php/Openbox#Standalone "Openbox"), utilice lo siguiente:

 `~/.xinitrc` 
```
...
xscreensaver &
exec openbox-session
```

**Nota:** Por lo menos, asegúrese de que el último bloque if en `/etc/X11/xinit/xinitrc` esté presente en su archivo `.xinitrc` para asegurarse de que los scripts en `/etc/X11/xinit/xinitrc.d` son ejecutados.

Los programas de ejecución prolongada que se inician antes que el administrador de ventanas, como un salvapantallas y una aplicación de fondo de pantalla, deben bifurcarse (*fork*) o ejecutarse en segundo plano añadiendo un signo `&`. De lo contrario, el script se detendría y esperaría a que cada programa terminase antes de ejecutar el administrador de ventanas o el entorno de escritorio. Tenga en cuenta que algunos programas no deben ser bifurcados, para evitar errores de secuencia (*race bugs*), como es el caso de [xrdb](/index.php/Xrdb "Xrdb"). Antes de pasar `exec` se reemplazará el proceso del script con el proceso del administrador de ventanas, de modo que X no salga incluso si este proceso se bifurca en segundo plano.

### xserverrc

El archivo `xserverrc` es un script del intérprete de línea de órdenes responsable de iniciar el servidor X. Tanto *startx* como *xinit* ejecutan `~/.xserverrc` si existe, de lo contrario *startx* utilizará `/etc/X11/xinit/xserverrc`.

Para mantener un [sesión autenticada](/index.php/General_troubleshooting_(Espa%C3%B1ol)#Permisos_de_sesi.C3.B3n "General troubleshooting (Español)") con `logind` y para evitar eludir el bloqueo de pantalla al cambiar de terminal, [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") debe iniciarse en el mismo terminal virtual donde se produjo el inicio de sesión [[1]](http://blog.falconindy.com/articles/back-to-basics-with-x-and-systemd.html). Por lo tanto, se recomienda especificar `vt$XDG_VTNR` en el archivo `~/.xserverrc`:

 `~/.xserverrc` 
```
#!/bin/sh

exec /usr/bin/Xorg -nolisten tcp "$@" vt$XDG_VTNR

```

Véase [Xserver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xserver.1) para obtener un listado de todas las opciones de la línea de órdenes.

**Sugerencia:** `-nolisten local` puede añadirse después de `-nolisten tcp` para deshabilitar la abstracción de sockets de X11 para ayudar con el aislamiento. Hay un [breve resumen](https://tstarling.com/blog/2016/06/x11-security-isolation/) sobre cómo puede afectar esto a la seguridad de X11.

Alternativamente, si desea que X se muestre en una consola separada de la que se invoca al servidor, puede hacerlo utilizando el wrapper del servidor X proporcionado por `/usr/lib/systemd/systemd-multi-seat-x`. Para mayor comodidad, *xinit* y *startx* pueden configurarse para utilizar este contenedor modificando su `~/.xserverrc`.

**Nota:** Para volver a habilitar la redirección de la salida de la sesión X en el archivo de registro de Xorg, añada la opción `-keeptty`. Véase [Redirección rota](/index.php/Xorg#Broken_redirection "Xorg") para más detalles.

## Utilización

Para ejecutar Xorg como un usuario normal, introduzca:

```
$ startx

```

o

```
$ xinit -- :1

```

**Nota:** *xinit* no soporta múltiples pantallas cuando ya se ha iniciado otro servidor X. Para ello debe especificar la pantalla añadiendo `-- :*número_de_pantalla*`, donde `*número_de_pantalla*` es 1 o más.

Su administrador de ventanas (o entorno de escritorio) elegido debería comenzar ahora correctamente.

Para salir de X, ejecute la función de salida de su administrador de ventanas (asumiendo que tiene una). Si carece de dicha funcionalidad, ejecute:

```
$ pkill -15 Xorg

```

**Nota:** *pkill* eliminará todas las instancias de X en ejecución. Para terminar específicamente el administrador de ventanas en el terminal virtual actual, ejecute:
```
$ pkill -15 -t tty"$XDG_VTNR" Xorg

```

## Inicio automático de X al inicio de sesión

Asegúrese de que *startx* esté [configurado](#Configuraci.C3.B3n) correctamente.

Para [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)"), añada lo siguiente al final de `~/.bash_profile`. Si el archivo no existe, copie una versión de la estructura de `/etc/skel/.bash_profile`. Para [Zsh](/index.php/Zsh_(Espa%C3%B1ol) "Zsh (Español)"), añádalo a `~/.zprofile`.

```
if [[ ! $DISPLAY && $XDG_VTNR -eq 1 ]]; then
  exec startx
fi

```

Puede reemplazar la comparación `-eq` con una como `-le 3` (para vt1 a vt3) si desea usar inicios de sesión gráficos en más de un terminal virtual.

Las condiciones alternativas para detectar el terminal virtual incluyen `"$(tty)" = "/dev/tty1"`, que no permite la comparación con `-le`, y `"$(fgconsole 2>/dev/null || echo -1)" -eq 1`, que no funciona en [consolas en serie](/index.php/Serial_console "Serial console").

Si desea permanecer conectado cuando finalice la sesión X, elimine `exec`.

Véase también [Fish#Start X at login](/index.php/Fish#Start_X_at_login "Fish") e [inicio de sesión automático en Xorg sin gestor de pantallas](/index.php/Systemd/User_(Espa%C3%B1ol)#Inicio_de_sesi.C3.B3n_autom.C3.A1tico_en_Xorg_sin_gestor_de_pantallas "Systemd/User (Español)").

**Sugerencia:** Este método se puede combinar con el [inicio de sesión automático a la consola virtual](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console").

## Tips and tricks

### Override xinitrc from command line

If you have a working `~/.xinitrc`, but just want to try other window manager or desktop environment, you can run it by issuing *startx* followed by the path to the window manager:

```
$ startx /full/path/to/window-manager

```

If the window manager takes arguments, they need to be quoted to be recognized as part of the first parameter of *startx*:

```
$ startx "/full/path/to/window-manager --key value"

```

Note that the full path is **required**. Optionally, you can also specify custom options for [#xserverrc](#xserverrc) script by appending them after `--`, e.g.:

```
$ startx /usr/bin/enlightenment -- -br +bs -dpi 96

```

See also [startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1).

**Tip:** This can be used even to start a regular GUI programs but without any of the window manager features. See also [#Starting applications without a window manager](#Starting_applications_without_a_window_manager) and [Running program in separate X display](/index.php/Running_program_in_separate_X_display "Running program in separate X display").

### Switching between desktop environments/window managers

If you are frequently switching between different desktop environments or window managers, it is convenient to either use a [display manager](/index.php/Display_manager "Display manager") or expand `.xinitrc` to make the switching possible.

The following example `~/.xinitrc` shows how to start a particular desktop environment or window manager with an argument:

 `~/.xinitrc` 
```
...

# Here Xfce is kept as default
session=${1:-xfce}

case $session in
    i3|i3wm           ) exec i3;;
    kde               ) exec startkde;;
    xfce|xfce4        ) exec startxfce4;;
    # No known session, try to run it as command
    *                 ) exec $1;;
esac

```

To pass the argument *session*:

```
$ xinit *session*

```

or

```
$ startx ~/.xinitrc *session*

```

### Starting applications without a window manager

It is possible to start only specific applications without a window manager, although most likely this is only useful with a single application shown in full-screen mode. For example:

 `~/.xinitrc` 
```
...

exec chromium

```

With this method you need to set each application window's geometry through its own configuration files, if possible at all.

**Tip:** This method can be useful to launch graphical games, especially on systems where excluding the memory or CPU usage of a window manager or desktop environment, and possible accessory applications, can help improve the game's execution performance.

See also [Display manager#Starting applications without a window manager](/index.php/Display_manager#Starting_applications_without_a_window_manager "Display manager").

### Output redirection using startx

See [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg") for details.