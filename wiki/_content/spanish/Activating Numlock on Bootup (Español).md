## Contents

*   [1 Consolas virtuales 1-6](#Consolas_virtuales_1-6)
*   [2 X window](#X_window)
*   [3 KDM](#KDM)
*   [4 Usuarios de KDE](#Usuarios_de_KDE)
*   [5 GDM](#GDM)

### Consolas virtuales 1-6

Para activar la tecla numlock durante el arranque normal en las consolas 1-6 (vc/n), añada la siguiente línea a `/etc/rc.local`:

```
for i in $(seq 6); do /usr/bin/setleds -D +num < /dev/vc/${i} >/dev/null; done

```

### X window

Si utiliza la orden startx para iniciar una sesión de X window, sólo tiene que instalar el paquete numlockx y añadirlo a su archivo `~/.xinitrc`.

Install `numlockx`:

```
pacman -S numlockx

```

Añada esto a `~/.xinitrc` antes de `exec`:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Ejecutado por startx (lance su gestor de ventanas desde aquí)
#

numlockx &

exec your_window_manager

```

### KDM

Si utiliza KDM como gestor de ingreso, añada :

```
numlockx on

```

a su archivo `/usr/share/config/kdm/Xsetup`.

### Usuarios de KDE

Como alternativa también puede añadir un guión a su directorio ~/.kde4/Autostart :

```
nano ~/.kde4/Autostart/numlockx

```

Añada lo siguiente:

```
#!/bin/sh
numlockx on

```

Y hágalo ejecutable:

```
chmod +x ~/.kde4/Autostart/numlockx

```

### GDM

Los usuarios de GDM pueden añadir el siguiente código al archivo /etc/gdm/Init/Default :

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```