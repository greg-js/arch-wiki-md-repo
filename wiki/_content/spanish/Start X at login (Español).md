En este artículo se explica cómo hacer que el [servidor X](/index.php/X_server "X server") se inicie automáticamente después de iniciar sesión en un terminal virtual. Esto se logra mediante la ejecución de la órden _startx_, cuyo comportamiento se puede personalizar como se describe en el artículo [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)"), por ejemplo para elegir qué [gestor de ventanas](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)") será lanzado. Alternativamente, se puede usar un [gestor de ventanas](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)") para iniciar automáticamente X y proporcionar una pantalla gráfica de acceso.

## Archivos de perfiles de la Shell

**Nota:** El siguiente procedimiento iniciará X en la misma tty que utiliza para iniciar sesión, condición necesaria para que se mantengan los permisos locales.

*   Para [Bash](/index.php/Bash "Bash"), añada lo siguiente al final de `~/.bash_profile`. Si el archivo no existe, utilice una copia de `/etc/skel/.bash_profile`.

*   Para [Zsh](/index.php/Zsh "Zsh"), añada lo siguiente a `~/.zprofile`, en su lugar.

```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx

```

**Nota:**

*   Se puede reemplazar la comparación `-eq 1` por otra como `-le 3` (de vt1 a vt3) si desea utilizar inicios de sesión gráfica en más de una terminal virtual.
*   X siempre se debe ejecutar en la misma tty donde se produjo el inicio de sesión, para conservar la sesión logind. Esto es manejado de forma predeterminada por `/etc/X11/xinit/xserverrc`.

*   Para [Fish](/index.php/Fish "Fish"), agregue lo que sigue al final de `~/.config/fish/config.fish`.

```
# start X at login
if status --is-login
    if test -z "$DISPLAY" -a $XDG_VTNR = 1
        exec startx
    end
end

```

## Consejos y trucos

*   Este método se puede combinar con [automatic login to virtual console (Español)](/index.php/Automatic_login_to_virtual_console_(Espa%C3%B1ol) "Automatic login to virtual console (Español)"). Al hacer esto tenemos que establecer dependencias correctas para el servicio autologin de systemd a fin de asegurar que dbus se inicia antes de que se lea ~/.xinitrc y, por lo tanto, comenzado pulseaudio (véase este [post](https://bbs.archlinux.org/viewtopic.php?id=155416)).
*   Si desea permanecer conectado cuando la sesión X termina, retire `exec`.
*   Para redirigir la salida de la sesión X a un archivo, cree un [alias](/index.php/Alias "Alias"):

	 `alias startx='startx &> ~/.xlog'`