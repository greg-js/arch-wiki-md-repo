[Splashy](http://splashy.alioth.debian.org) es una implementación en el espacio de usuario de una pantalla de bienvenida para los sistemas Linux. Proporciona un entorno gráfico durante el arranque del sistema utilizando la capa framebuffer de Linux vía [directfb](http://www.directfb.org).

Vea por favor [este hilo](https://bbs.archlinux.org/viewtopic.php?id=48978) en el foro de ArchLinux para añadir un repositorio con paquetes modificados o más actualizados de Splashy.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 /boot/grub/menu.lst](#.2Fboot.2Fgrub.2Fmenu.lst)
    *   [2.2 /etc/rc.conf](#.2Fetc.2Frc.conf)
    *   [2.3 /etc/mkinitcpio.conf](#.2Fetc.2Fmkinitcpio.conf)
    *   [2.4 Actualizando](#Actualizando)
*   [3 Temas de splashy](#Temas_de_splashy)
*   [4 Problemas conocidos](#Problemas_conocidos)
*   [5 Enlaces](#Enlaces)

# Instalación

1.  Conseguir el [paquete](https://aur.archlinux.org/packages.php?do_Details=1&ID=10211) en AUR y construirlo mediante makepkg (o el programa que involucre a makepkg que prefiera) e instalarlo vía Pacman o desde yaourt
2.  Lo mejor es que hagamos una copia sobre todo de nuestro rc.conf que posteriormente restauraremos ahora hacemos:

```
   cp /etc/rc.conf ~/

```

```
   yaourt -S splashy

```

```
   sudo cp ~/rc.conf /etc/rc.conf

```

1.  El paquete splashy viene sin temas por defecto así que debemos instalar splashy-themes y configurar el que mas nos guste como defecto:

```
   yaourt -S splashy-themes

```

**¡Atencíon!** "initscripts-splash" ahora es una dependencia de splashy. Reemplaza a "initscripts", así que algunos archivos en /etc serán respaldados como *.pacsave.

# Configuración

#### /boot/grub/menu.lst

Añadir **quiet vga=791 splash** en la línea correspondiente del kernel en */boot/grub/menu.lst*. p.ej.:

```
kernel (hd0,6)/vmlinuz-linux root=/dev/sda6 ro quiet vga=791 splash

```

#### /etc/rc.conf

Añadir SPLASH="splashy" en */etc/rc.conf* al final del archivo. p.ej.:

```
SPLASH="splashy"

```

#### /etc/mkinitcpio.conf

*   **Debe recordar reconstruir la imagen initramfs cada vez que se cambie la configuración de Splashy.** (p.ej. si cambió el tema de Splashy)

1.  Añadir **splashy** al **final** de la línea HOOKS en */etc/mkinitcpio.conf*. p.ej.: `HOOKS="base udev autodetect ide sata filesystems splashy"` 
2.  Reconstruir la imagen del kernel `# mkinitcpio -p <nombre del kernel>` p.ej. `# mkinitcpio -p linux` 

### Actualizando

*   No olvidar reconstruir la imagen initramfs después de actualizar Splashy.

# Temas de splashy

Puedes ver la lista de temas de splashy tecleando en terminal lo siguiente:

```
ls /usr/share/splashy/themes

```

Los nombres de las carpetas son los nombres de los temas. Es importante destacar que los temas que finalizan con "43" son temas en 4:3, mientras que los otros son panorámicos. Prueba "simplyback", que es un buen tema para iniciarse.

Para cambiar el tema hay dos formas, aunque la primera seguramente es la recomendada:

*   Usando splasy_config

```
splashy_config --set-theme <nombre_del_tema_que_estés_interesado>

```

*   Modo manual: edita el archivo /etc/splashy/config.xml y cambia el nombre del tema por el que quieras en la siguiente linea:

```
<current_theme>**archlinux-simplyblack-43**</current_theme>

```

*   Lo que esta en negrita es el tema que se va a usar, en este caso seria: **archlinux-simplyblack-43**

Después de cambiar el tema o hacer cambios en splashy de cualquier clase hemos de rehacer el kernel escribiendo en consola:

```
# mkinitcpio -p kernel26

```

# Problemas conocidos

1.  Cuando un guión de inicio falla o cuando un error se produce, Splashy no finaliza o bien cambia automáticamente a modo *verbose*.
2.  Algo va "terribelemente mal" cuando estando Splashy en ejecución, comienza una comprobación forzada de un sistema de archivos. Por alguna razón desconocida (aún), después del fsck el sistema se reinicia por sí sólo.
3.  X puede mostrar iregularidades en la parte superior de la pantalla, si Splashy es activado durante el arranque.
4.  Añadir `<autoverboseonerror>no</autoverboseonerror>` en `/etc/splashy/config.xml` podría solucionar algunos problemas en portátiles durante el arranque.

# Enlaces

*   [http://splashy.alioth.debian.org](http://splashy.alioth.debian.org)
*   [http://www.directfb.org](http://www.directfb.org)