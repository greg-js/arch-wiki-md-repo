## Usando sudo

Primero Instala sudo:

```
# pacman -S sudo

```

Luego, como root, añade las siguientes lineas en el archivo `/etc/sudoers` usando el comando `visudo`, o si prefieres usar nano utiliza `EDITOR=nano visudo`. Substituye `**user**` por tu nombre de usuario y `**hostname**` por el nombre del Host.

```
**user** **hostname** =NOPASSWD: /sbin/shutdown -h now,/sbin/halt,/sbin/poweroff,/sbin/reboot

```

Ahora puedes aparar el equipo con `sudo shutdown -h now`, y reiniciar con `sudo reboot`, si deseas tambien puedes hacer uso de `poweroff` o `halt` para apagar el equipo.

El uso de la etiqueta `NOPASSWD:` se utiliza si no desea que se pida contraseña.

Por conveniencia, puedes agregar los alias a tu `~/.bashrc` (o `/etc/bash.bashrc` para todo el sistema):

```
alias reboot="sudo reboot"
alias poweroff="sudo poweroff"
alias halt="sudo halt"

```

## Usando acpid

[acpid](/index.php/Acpid "Acpid") puede ser usado para permitir apagar el equipo por cualquiera con acceso fisico al botón de encendido del equipo.