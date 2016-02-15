El archivo `~/.xinitrc` es un script de shell leído por `xinit` y estos por el frontend `startx`. Se utiliza principalmente para ejecutar [entornos de escritorios](/index.php/Desktop_environment "Desktop environment"), [gestores de ventanas](/index.php/Window_manager "Window manager"), y otros programas al iniciar el servidor X (por ejemplo, como los daemons y las configuraciones de las variables de entorno). El programa `xinit` se utilizan para iniciar servidor [X Window System](/index.php/Xorg "Xorg") y funcionan como el primer programa cliente en sistemas que no utilizan un [gestor de inicio de sesión](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)").

Una de las principales funciones de `~/.xinitrc` es dictar al sistema X Window lo que se invoca desde el programa `startx` o `xinit` en función de lo especificado por cada usuario. Existe numerosas especificaciones adicionales y órdenes que se pueden añadir a `~/.xinitrc` con el fin de personalizar aún más su sistema.

La mayoría de los gestores de pantalla también suministran un archivo [xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)") similar antes de xinit.

## Contents

*   [1 Cómo empezar](#C.C3.B3mo_empezar)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Sobrescribir xinitrc desde la línea de órdenes](#Sobrescribir_xinitrc_desde_la_l.C3.ADnea_de_.C3.B3rdenes)
    *   [3.2 Realizar la elección de un DE/WM](#Realizar_la_elecci.C3.B3n_de_un_DE.2FWM)

## Cómo empezar

**Sugerencia:** `~/.xinitrc` es del llamado archivo 'dot' (.). Los archivos en un sistema de archivos *nix que están precedidos por un punto son 'ocultos' y no se mostrarán, por lo general, con la orden `ls`, en aras de mantener la integridad de los directorios. Los archivos ocultos se pueden ver mediante la ejecución de `ls -a`. La terminación 'rc' denota que estamos ante una orden «run» y simplemente indica que se trata de un archivo de configuración. Puesto que controla la forma en que un programa se inicia, se dice (aunque históricamente incorrecta) también que están para "Controlar su Ejecución".

Copie el archivo-modelo `/etc/X11/xinit/xinitrc` en su directorio personal (/home):

```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc

```

Ahora, edite `~/.xinitrc` y descomente la línea que corresponde a su DE/WM (entorno de escritorio/gestor de ventanas). Por ejemplo, si desea probar la configuración de X básico (ratón, teclado, resolución de los gráficos), puede simplemente usar [xterm](/index.php/Xterm "Xterm"):

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)

if [ -d /etc/X11/xinit/xinitrc.d ]; then
  for f in /etc/X11/xinit/xinitrc.d/*; do
    [ -x "$f" ] && . "$f"
  done
  unset f
fi

# exec gnome-session
# exec startkde
# exec startxfce4
# exec wmaker
# exec icewm
# exec blackbox
# exec fluxbox
# exec openbox-session
# ...or the Window Manager of your choice
exec xterm

```

**Nota:** Es importante que solo un `exec` esté descomentado, pues, de lo contrario, se ejecutará la primera línea no comentada. NO intente poner fondo a su WM añadiendo `&` a la línea.

Después de editar correctamente `~/.xinitrc`, es el momento de ejecutar X. Para ejecutar X como usuario no root, ejecute:

```
$ startx

```

o

```
$ xinit -- :1 -nolisten tcp vt$XDG_VTNR

```

**Nota:**

*   `xinit` no lee el archivo `/etc/X11/xinit/xserverrc` que afecta a todo el sistema, de modo que o bien tiene que copiarlo en el directorio home con el nombre `.xserverrc`, o especificar `vt$XDG_VTNR` como opción de la línea de órdenes a fin de [mantener los permisos de la sesión](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").
*   `xinit` no maneja múltiples sesiones si ya ha iniciado sesión en algún otro terminal virtual, para lo cual se tiene que especificar la sesión añadiendo `-- :<session_no>`. Si ya está ejecutando X, entonces debe comenzar con:1 o más.

El DE/WM de su elección debería haber comenzado. Puede probar el teclado y su distribución. Trate de mover el ratón para probarlo.

## Configuración

Cuando un gestor de ventanas no se utiliza, es importante tener en cuenta que la vida de la sesión X comienza y termina con el script de `~/.xinitrc`. Esto significa que una vez que el script se cierra, X se cierra, con independencia de que todavía se estén ejecutando programas (incluyendo su gestor de ventanas). Por lo tanto, es importante que el gestor de ventanas y X cierren al mismo tiempo. Esto se logra fácilmente mediante la ejecución del gestor de ventanas como el último programa en el guión del script.

Lo que sigue es un simple ejemplo de archivo `~/.xinitrc`, incluyendo algunos programas que se inician de forma automática:

```
~/.xinitrc

```

```
#!/bin/sh

if [ -d /etc/X11/xinit/xinitrc.d ]; then
  for f in /etc/X11/xinit/xinitrc.d/*; do
    [ -x "$f" ] && . "$f"
  done
  unset f
fi

xrdb -merge ~/.Xresources         # update x resources db

xscreensaver -no-splash &         # starts screensaver daemon 
xsetroot -cursor_name left_ptr &  # sets the cursor icon
sh ~/.fehbg &                     # sets the background image

exec openbox-session              # starts the window manager

```

Tenga en cuenta que en el primer ejemplo de arriba, los programas como `cairo-compmgr`, `xscreensaver`, `xsetroot` y `sh` se ejecutan en segundo plano (al añadirle el sufijo `&`). De lo contrario, el script detiene y hace esperar cada programa y daemons hasta que se ejecute `openbox-session`. También tenga en cuenta que `openbox-session` no está en segundo plano. Ésto asegura que el script no se cerrará hasta que openbox lo haga.

Preceder el gestor de ventanas `openbox-session` con `exec` es recomendable ya que sustituye el proceso en curso por ese otro, de modo que el script se detendrá pero X no se cerrará, incluso si hay subprocesos funcionando en segundo plano.

## Consejos y trucos

### Sobrescribir xinitrc desde la línea de órdenes

Si tiene diseñado `~/.xinitrc`, pero quiere probar otros WM/DE, es posible mediante el uso de `xinit`, seguido de la ruta de acceso al gestor de ventanas:

```
$ startx /full/path/to/window-manager

```

Tenga en cuenta que la ruta completa es **necesaria**. Opcionalmente, ambién puede sobrescribir el archivo `/etc/X11/xinit/xserverrc` (que almacena las opciones del servidor X por defecto) con opciones personalizadas añadiéndolas después de `--`, por ejemplo:

```
$ startx /usr/bin/enlightenment -- -nolisten tcp -br +bs -dpi 96 vt$XDG_VTNR

```

o

```
$ xinit /usr/bin/enlightenment -- -nolisten tcp -br +bs -dpi 96 vt$XDG_VTNR

```

### Realizar la elección de un DE/WM

Si no se usa un gestor de inicio gráfico o no se quiere usar uno, es posible que tenga que editar el archivo `~/.xinitrc` frecuentemente. Esto se puede resolver fácilmente con la simple adición de una línea para cada caso, que permitirá cargar el DE/WM deseado en base a los argumentos que le vengan proporcionados.

El ejemplo siguiente de `~/.xinitrc` muestra cómo iniciar un ED/WM concreto con un argumento:

 `~/.xinitrc` 

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)

if [ -d /etc/X11/xinit/xinitrc.d ]; then
        for f in /etc/X11/xinit/xinitrc.d/*; do
                [ -x "$f" ] && . "$f"
        done
        unset f
fi

# Here Xfce is kept as default
session=${1:-xfce}

case $session in
        enlightenment) exec enlightenment_start;;
        fluxbox) exec startfluxbox;;
        gnome) exec gnome-session;;
        lxde) exec startlxde;;
        kde) exec startkde;;
        openbox) exec openbox-session;;
        xfce) exec startxfce4;;
        # No known session, try to run it as command
        *) exec $1;;                
esac

```

Luego, copie el archivo `/etc/X11/xinit/xserverrc` en el directorio home:

```
$ cp /etc/X11/xinit/xserverrc ~/.xserverrc

```

Después de eso, se puede iniciar fácilmente un DE/WM concreto pasando un argumento, por ejemplo:

```
$ xinit
$ xinit gnome
$ xinit kde
$ xinit wmaker

```

o

```
$ startx
$ startx ~/.xinitrc gnome
$ startx ~/.xinitrc kde
$ startx ~/.xinitrc wmaker

```