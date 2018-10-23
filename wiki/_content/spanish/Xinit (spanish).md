**Estado de la traducción**
Este artículo es una traducción de [Xinit](/index.php/Xinit "Xinit"), revisada por última vez el **2018-10-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Xinit&diff=0&oldid=549210) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

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
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Sobrescribir xinitrc desde la línea de órdenes](#Sobrescribir_xinitrc_desde_la_l.C3.ADnea_de_.C3.B3rdenes)
    *   [5.2 Cambio entre entornos de escritorio/gestores de ventanas](#Cambio_entre_entornos_de_escritorio.2Fgestores_de_ventanas)
    *   [5.3 Inicio de aplicaciones sin un administrador de ventanas](#Inicio_de_aplicaciones_sin_un_administrador_de_ventanas)
    *   [5.4 Redirección de salida utilizando startx.](#Redirecci.C3.B3n_de_salida_utilizando_startx.)

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

## Consejos y trucos

### Sobrescribir xinitrc desde la línea de órdenes

Si tiene un `~/.xinitrc` en funcionamiento, pero solo desea probar otro administrador de ventanas o entorno de escritorio, puede ejecutarlo introduciendo *startx* seguido de la ruta al administrador de ventanas:

```
$ startx /full/path/to/window-manager

```

Si el administrador de ventanas tiene argumentos, deben citarse para ser reconocidos como parte del primer parámetro de *startx*:

```
$ startx "/full/path/to/window-manager --key value"

```

Tenga en cuenta que se **requiere** la ruta completa. Opcionalmente, también puede especificar opciones personalizadas para el script [#xserverrc](#xserverrc) añadiéndolas después de `--`, por ejemplo:

```
$ startx /usr/bin/enlightenment -- -br +bs -dpi 96

```

Véase también [startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1).

**Sugerencia:** Esto se puede utilizar incluso para iniciar un programa gráfico normal pero sin ninguna de las funciones del administrador de ventanas. Véase también [#Inicio de aplicaciones sin un administrador de ventanas](#Inicio_de_aplicaciones_sin_un_administrador_de_ventanas) y [Ejecutando programa en una pantalla X separada](/index.php/Running_program_in_separate_X_display "Running program in separate X display")

### Cambio entre entornos de escritorio/gestores de ventanas

Si está cambiando con frecuencia entre diferentes entornos de escritorio o administradores de ventanas, es conveniente utilizar un [administrador de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") o expandir `.xinitrc` para hacer posible el cambio.

El siguiente `~/.xinitrc` de ejemplo muestra como iniciar un entorno de escritorio o administrador de ventanas en particular con un argumento:

 `~/.xinitrc` 
```
...

# Aquí Xfce se mantiene por defecto
session=${1:-xfce}

case $session in
    i3|i3wm           ) exec i3;;
    kde               ) exec startkde;;
    xfce|xfce4        ) exec startxfce4;;
    # No hay sesión conocida, intento ejecutarlo como orden
    *                 ) exec $1;;
esac

```

Para pasar el argumento *session*:

```
$ xinit *session*

```

o

```
$ startx ~/.xinitrc *session*

```

### Inicio de aplicaciones sin un administrador de ventanas

Es posible iniciar solo aplicaciones específicas sin un administrador de ventanas, aunque lo más probable es que esto solo sea útil con una sola aplicación que se muestre en modo de pantalla completa. Por ejemplo:

 `~/.xinitrc` 
```
...

exec chromium

```

Con este método, debe establecer la geometría de cada ventana de la aplicación a través de sus propios archivos de configuración, si es posible.

**Sugerencia:** Este método puede ser útil para lanzar juegos gráficos, especialmente en sistemas donde excluir el uso de la memoria o la CPU de un administrador de ventanas o entorno de escritorio, y posibles aplicaciones accesorias, puede ayudar a mejorar el rendimiento del juego.

Véase también [Display manager#Starting applications without a window manager](/index.php/Display_manager#Starting_applications_without_a_window_manager "Display manager").

### Redirección de salida utilizando startx.

Véase [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg") para más detalles.