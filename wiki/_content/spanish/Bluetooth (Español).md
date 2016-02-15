## Instalación

Para utilizar el Bluetooth, el paquete [bluez](http://www.bluez.org) se debe instalar:

```
# pacman -S bluez

```

Una vez que se ha instalado bluez, tanto el demonio "dbus" y el demonio "bluetooth" debe iniciarse:

```
# /etc/rc.d/dbus start
# /etc/rc.d/bluetooth start

```

El demonio de dbus se usa para leer la configuración y el emparejamiento de pines, mientras que el demonio de bluetooth es necesario para el protocolo Bluetooth. Es importante que se inicia dbus**antes** bluetooth. Si dbus no se estaba ejecutando cuando se inició bluetooth, a continuación, intenta (después de haberse iniciado dbus):

```
# /etc/rc.d/bluetooth restart

```

Para empezar bluetooth de forma automática en el arranque, ay que añadir Bluetooth a su gama demonios en [rc.conf](/index.php/Rc.conf "Rc.conf") (después de dbus):

```
 DEMONIOS =(... dbus ... bluetooth)

```

**Advertencia:** Si usted tiene dbus y bluetooth en segundo plano, puede suceder que bluetooth se desactiva al arrancar gnome.

Para solucionar esto, dbus no tiene que estar en segundo plano.

Si desea permitir la transmisión de audio desde el dispositivo a su ordenador, deberá modificar `/etc/bluetooth/audio.conf` y añadir esto a la sección [General]:

```
Enable=Source

```

## Interfaces gráficas

Los siguientes paquetes permiten una interfaz gráfica para personalizar el Bluetooth.

### Blueman

[Blueman](http://blueman-project.org) es un gestor completo de Bluetooth esta escrito en GTK y, como tal, se recomienda para [GNOME](/index.php/GNOME "GNOME") o [Xfce](/index.php/Xfce "Xfce"). Para instalar Blueman utilizando la herramienta de pacman:

```
 # Pacman-S blueman

```

Asegúrese de que el demonio _bluetooth_ se está ejecutando según lo descrito anteriormente y despues ejecute_blueman-applet_. Para hacer que el applet se ejecute en el inicio de sesión ay que añadir _blueman-applet_ a el menú_,_ Xfce Menu -> Settings -> Session and Startup _en(Xfce)._

Nota: si está ejecutando blueman fuera de Gnome/GDM, por ejemplo, en Xfce usando el comando "startx" debe agregar ". /etc/X11/xinit/xinitrc.d/*" en la parte superior de su archivo ~/.xinitrc para que nautilus sea capaz de navegar por los dispositivos.

Nota: si usted no está usando nautilus (por ejemplo thunar) (esto es útil para usuarios de OpenBox, etc), puede resultar útil:

```
 #! / bin / bash
 fusermount-u ~ / bluetooth
 obexfs-b $ 1 ~ / bluetooth
 thunar ~ / bluetooth

```

sin fusermount-u /mountpoint es posible obtener un error causado por desmontar unclean de fuse fs.

Ahora tendrá que mover el script (lo llamé obex_thunar.sh) a /usr/bin, y después darle permisos de ejecucion

```
 chmod +x /usr/bin/obex_thunar.sh

```

El último paso sería cambiar la línea de Local Services > Transfer > Advanced para obex_thunar.sh% d