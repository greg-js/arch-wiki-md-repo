**Estado de la traducción**
Este artículo es una traducción de [Allow users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown"), revisada por última vez el **2018-11-08**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Allow_users_to_shutdown&diff=0&oldid=549069) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Contents

*   [1 Eventos de botones y de tapa](#Eventos_de_botones_y_de_tapa)
*   [2 Utilizar systemd-logind](#Utilizar_systemd-logind)
*   [3 Utilizar sudo](#Utilizar_sudo)
    *   [3.1 Usuarios sin privilegios sudo](#Usuarios_sin_privilegios_sudo)
*   [4 Crear alias](#Crear_alias)

## Eventos de botones y de tapa

El presionado de los botones de suspensión, apagado e hibernación y los eventos de cierre de la tapa se controlan mediante *logind* como se describe en la página [Gestión de energía#Eventos de ACPI](/index.php/Power_management_(Espa%C3%B1ol)#Eventos_de_ACPI "Power management (Español)").

## Utilizar systemd-logind

Si está utilizando [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") (el cual está implementado de manera predeterminada en Arch Linux) e [instala](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [polkit](https://www.archlinux.org/packages/?name=polkit), los usuarios con sesión no remota pueden emitir comandos relacionados con la alimentación eléctrica siempre que [la sesión no esté rota](/index.php/General_troubleshooting_(Espa%C3%B1ol)#Permisos_de_sesi.C3.B3n "General troubleshooting (Español)").

Para comprobar si su sesión está activa

```
$ loginctl show-session $XDG_SESSION_ID --property=Active

```

El usuario puede usar entonces los comandos *systemctl* en la línea de comandos, o añadirlos a los menús:

```
$ systemctl poweroff
$ systemctl reboot

```

También se pueden usar otros comandos, incluyendo `systemctl suspend` y `systemctl hibernate`. Veáse la sección *System Commands* en [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1).

## Utilizar sudo

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [sudo](https://www.archlinux.org/packages/?name=sudo), y otorgue al usuario [privilegios sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)"). El usuario podrá usar entonces los comandos `sudo systemctl` (por ejemplo, `sudo systemctl poweroff`, `sudo systemctl reboot`, `sudo systemctl suspend` y `sudo systemctl hibernate`). Véase la sección *System Commands* en [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1)

### Usuarios sin privilegios sudo

Si a los usuarios solo se les permite usar comandos de apagado, pero no tienen otros privilegios sudo, entonces, como root, agregue lo siguiente al final de `/etc/sudoers` usando el comando `visudo` . Sustituya *usuario* por su nombre de usuario y *nombre_del_host* por el nombre de host de la máquina.

```
*usuario* *nombre_del_host* =NOPASSWD: /usr/bin/systemctl poweroff,/usr/bin/systemctl halt,/usr/bin/systemctl reboot

```

Ahora su usuario puede apagar con `sudo systemctl poweroff`, y reiniciar con `sudo systemctl reboot`. Los usuarios que deseen apagar un sistema también pueden usar `sudo systemctl halt`. Use la etiqueta `NOPASSWD:` solo si no desea que se le solicite su contraseña.

## Crear alias

Para su comodidad, puede agregar estos [alias](/index.php/Bash_(Espa%C3%B1ol)#Alias "Bash (Español)") a su `~/.bashrc` de su usuario si lo tiene habilitado (o a `/etc/bash.bashrc` para una configuración global de todo el sistema):

```
alias reboot="sudo systemctl reboot"
alias poweroff="sudo systemctl poweroff"
alias halt="sudo systemctl halt"

```

Esto también se puede hacer instalando [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat). Este paquete crea enlaces simbólicos del respectivo nombre a systemctl.