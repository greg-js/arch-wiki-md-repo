Esta página es para aquellos que prefieren limitar el nivel de detalle de mensajes de su sistema a lo estrictamente necesario, ya sea por estética o por otros motivos. Siguiendo esta guía elimina todo el texto lanzado desde el proceso de arranque. [Vídeo demostración](http://www.youtube.com/watch?v=tuqhsqrhXk0)

## Syslinux y Systemd

La sección del kernel en `/boot/syslinux/syslinux.cfg` debería mostrar algo como esto:

```
APPEND root=/dev/sda1 rw 5 init=/usr/lib/systemd/systemd quiet vga=current

```

vga=current es el argumento del kernel que evita comportamientos extraños como [grey flash](https://bugs.archlinux.org/task/32309).

Si todavía está recibiendo mensajes en la consola, se puede indicar a dmesg que limite los mensajes a los que considere importantes. Puede cambiar el nivel en el que estos mensajes serán mostrados usando `quiet loglevel=<level>`, donde `<level>` es cualquier número entre 0 y 7, 0 es el más crítico y 7 el nivel de depuración de la impresión. Tenga en cuenta que esto solo parece funcionar si tanto `quiet` como `loglevel=<level>` son utilizados, y deben estar en ese orden («quiet» primero). El parámetro loglevel solo va a cambiar lo que sale impreso en la consola, los niveles propios de dmesg no se verán afectados y seguirán estando disponibles a través de journal, así como con la orden `dmesg`. Para más información, véase el archivo _Documentation/kernel-parameters.txt_ y el paquete [linux-docs](https://www.archlinux.org/packages/?name=linux-docs).

Configure el servicio getty como se describe en [Automatic login to virtual console (Español)](/index.php/Automatic_login_to_virtual_console_(Espa%C3%B1ol) "Automatic login to virtual console (Español)").

 `$ grep Exec /etc/systemd/system/autologin\@.service` 

```
...
ExecStart=-/sbin/agetty -n -i -a YOUR_USERNAME %I
...

```

Para eliminar el mensaje lastlog necesita comentar _lastlog_ en `/etc/pam.d/login`:

```
#session                optional        pam_lastlog.so

```

También `touch ~/.hushlogin` para eliminar el mensaje Last login.

Para ocultar los mensajes del kernel de la consola o modificar la línea _kernel.printk_ proceda como [sigue](http://unix.stackexchange.com/a/45525/27433):

 ` /etc/sysctl.d/20-quiet-printk.conf`  ` kernel.printk = 3 3 3 3` 

Para ocultar los mensajes de `startx`, puede redirigir su salida a `/dev/null`, en el archivo [.bash_profile](https://github.com/kaihendry/Kai-s--HOME/blob/master/.bash_profile), como sigue:

```
$ [[ $(fgconsole 2>/dev/null) == 1 ]] && exec startx -- vt1 &> /dev/null

```

Cuestiones pendientes:

*   [Los apagados de systemd no usan «quiet»](https://bugs.freedesktop.org/show_bug.cgi?id=57216) - Desde systemd v206, el parámetro del kernel `quiet` es ahora respectado en el apagado, aunque parece que si se utiliza el hook `shutdown` de [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio), función esta que no se ha creado para apoyar aquel parámetro.

## GRUB y systemd

Para un arranque sin mensajes utilizando grub, deje que systemd comprobe el sistema de archivos root. Para ello, quite _fsck_ de:

```
HOOKS=(...) 

```

en `/etc/mkinitcpio`, y, después, ejecute:

```
# mkinitcpio -p linux

```

Luego, edite `/etc/default/grub` y establezca:

```
GRUB_CMDLINE_LINUX_DEFAULT="ro quiet"

```

Por último, ejecute:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Ahora edite los archivos `systemd-fsck-root.service` y `systemd-fsck@.service` ubicados en `/usr/lib/systemd/system/` para configurar _StandardOutput_ y _StandardError_ de este modo:

```
(...)

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/lib/systemd/systemd-fsck
StandardOutput=null
StandardError=journal+console
FsckPassNo=1
TimeoutSec=0

```

Véase [esto](http://www.freedesktop.org/software/systemd/man/systemd-fsck@.service.html) para obtener más información sobre las opciones que se pueden pasar a `systemd-fsck` - puede cambiar la frecuencia con que el servicio comprobará (o no) los sistemas de archivos.