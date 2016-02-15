`sudo` («substitute user do») permite que un administrador del sistema delegue autoridad para dar a ciertos usuarios (o grupos de usuarios) la capacidad de ejecutar algunas órdenes (o la totalidad) como root u otro usuario, al tiempo que permite auditar el rastro de las órdenes dadas y sus argumentos.

## Contents

*   [1 Justificación](#Justificaci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Utilización](#Utilizaci.C3.B3n)
*   [4 Configuración](#Configuraci.C3.B3n)
    *   [4.1 Ver la configuración actual](#Ver_la_configuraci.C3.B3n_actual)
    *   [4.2 Usar visudo](#Usar_visudo)
    *   [4.3 Ejemplos de entradas](#Ejemplos_de_entradas)
    *   [4.4 Permisos de archivos predeterminados por sudoers](#Permisos_de_archivos_predeterminados_por_sudoers)
    *   [4.5 Expiración de la contraseña](#Expiraci.C3.B3n_de_la_contrase.C3.B1a)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Archivo de ejemplo](#Archivo_de_ejemplo)
    *   [5.2 Activar la función autocompletar con Tab en Bash](#Activar_la_funci.C3.B3n_autocompletar_con_Tab_en_Bash)
    *   [5.3 Ejecutar aplicaciones X11 utilizando sudo](#Ejecutar_aplicaciones_X11_utilizando_sudo)
    *   [5.4 Desactivar sudo para cada terminal](#Desactivar_sudo_para_cada_terminal)
    *   [5.5 Variables de entornos](#Variables_de_entornos)
    *   [5.6 Activar alias](#Activar_alias)
    *   [5.7 Avisos](#Avisos)
    *   [5.8 Contraseña root](#Contrase.C3.B1a_root)
    *   [5.9 Desactivar el acceso de root](#Desactivar_el_acceso_de_root)
        *   [5.9.1 kdesu](#kdesu)
        *   [5.9.2 PolicyKit](#PolicyKit)
        *   [5.9.3 NetworkManager](#NetworkManager)
    *   [5.10 Ejemplo para proteger con sudo](#Ejemplo_para_proteger_con_sudo)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [6.1 Problemas de SSH con TTY](#Problemas_de_SSH_con_TTY)
    *   [6.2 Mostrar privilegios del usuario](#Mostrar_privilegios_del_usuario)
    *   [6.3 Umask permisiva](#Umask_permisiva)
    *   [6.4 Estrutura de Defaults](#Estrutura_de_Defaults)

## Justificación

Sudo es una alternativa a [su](/index.php/Su "Su") para ejecutar órdenes como root. A diferencia de [su](/index.php/Su "Su"), el cual lanza una shell de root que permite además el acceso a todas las órdenes, sudo, por el contrario, realiza una dosificada entrega de privilegios temporales para una sola orden. El uso de sudo otorga los privilegios de root solo cuando es necesario y reduce el riesgo que un error tipográfico o un error en la invocación de una orden puede causar en el sistema. Sudo también se puede utilizar para ejecutar órdenes como otro u otros usuarios, y además, sudo registra todas las órdenes emitidas y los intentos fallidos.

## Instalación

Instale el paquete [sudo](https://www.archlinux.org/packages/?name=sudo), disponible en los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)"):

```
# pacman -S sudo

```

Para empezar a usar `sudo` por un usuario sin privilegios, debe estar correctamente configurado. Así que lea la sección de configuración.

## Utilización

Con sudo, los usuarios normales pueden emitir órdenes con el prefijo `sudo` para ejecutárlas con privilegios de superusuario (o de otros grupos de usuarios).

Por ejemplo, para usar pacman:

```
$ sudo pacman -Syu

```

Véase el [manual de sudo](http://www.gratisoft.us/sudo/man/sudo.html) para obtener más información.

## Configuración

### Ver la configuración actual

Ejecute `sudo -ll` para visualizar la configuración actual de sudo.

### Usar visudo

El archivo de configuración de sudo es `/etc/sudoers`. Sería conveniente que dicho archivo **siempre** se editase con la orden `visudo`. `visudo` bloquea el archivo `sudoers`, guarda las modificaciones en un archivo temporal y comprueba la gramática de ese archivo antes de copiarlo a `/etc/sudoers`.

**Advertencia:** ¡Es imperativo que el archivo `sudoers` no tenga errores de sintaxis! Cualquier error hará sudo inutilizable. Modifíquelo **siempre** con `visudo` para evitar errores.

El editor por defecto para visudo es `vi`. Será utilizado si no se especifica otro editor, configurado o bien con VISUAL o bien con EDITOR como variables de entorno (utilizado en ese orden) para el editor que desee, por ejemplo, `nano`. La orden se ejecuta como root:

```
# EDITOR=nano visudo

```

Se puede cambiar permanentemente la configuración de todo el sistema para, por ejemplo, `vim`, añadiendo:

```
export EDITOR=nano

```

en el archivo `~/.bashrc` . Tenga en cuenta que este no entrará en vigor para las shells ya en ejecución.

Para usar permanentemente el editor elegido cuando se ejecuta la orden `visudo`, agregue la línea siguiente a `/etc/sudoers` (donde `nano` es el editor elegido):

```
# Restablece el entorno por defecto
Defaults      env_reset
# Establece el editor por defecto para vim, y no permite a visudo utilizar EDITOR/VISUAL.
Defaults      editor=/usr/bin/nano, !env_editor

```

### Ejemplos de entradas

Para permitir a un usuario normal obtener privilegios de superusuario cuando antepone `sudo` a una orden, agregue la siguiente línea:

```
NOMBRE_DE_USUARIO   ALL=(ALL) ALL

```

Para permitir a un usuario ejecutar todas las órdenes de cualquier usuario, pero únicamente en la máquina con el hostname NOMBRE_DEL_EQUIPO:

```
NOMBRE_DE_USUARIO   NOMBRE_DE_EQUIPO=(ALL) ALL

```

Para permitir que los miembros del grupo `wheel` tengan acceso a sudo:

```
%wheel      ALL=(ALL) ALL

```

Para desactivar solicitar una contraseña para el usuario NOMBRE_DE_USUARIO:

```
Defaults:NOMBRE_DE_USUARIO      !authenticate

```

Para activar las órdenes definidas explícitamente solo para el usuario NOMBRE_DE_USUARIO en el equipo NOMBRE_DEL_EQUIPO:

```
USER_NAME NOMBRE_DEL_EQUIPO=/sbin/halt,/sbin/poweroff,/sbin/reboot,/usr/bin/pacman -Syu

```

**Nota:** La opción personalizada añadida debe ir al final del archivo, ya que las líneas posteriores anulan las anteriores. En particular, esta línea debe ser posterior a la línea `%wheel` si el usuario se encuentra en este grupo.

Para activar, sin necesidad de contraseña, las órdenes definidas explícitamente únicamente para el usuario NOMBRE_DE_USUARIO en el equipo NOMBRE_DEL_EQUIPO:

```
NOMBRE_DE_USUARIO NOMBRE_DEL_EQUIPO= NOPASSWD: /sbin/halt,/sbin/poweroff,/sbin/reboot,/usr/bin/pacman -Syu

```

Un ejemplo detallado de archivo sudoers se puede encontrar [aquí](http://www.gratisoft.us/sudo/sample.sudoers). Por otro lado, véase el [manual de sudoers](http://www.gratisoft.us/sudo/man/sudoers.html) para obtener más información.

### Permisos de archivos predeterminados por sudoers

El propietario y el grupo para el archivo sudoers deben ser ambos 0\. Los permisos de los archivos se deben establecer en 0440\. Estos permisos se establecen de forma predeterminada, pero si accidentalmente los cambia, debe modificarlos de inmediato o sudo fallará.

```
# chown -c root:root /etc/sudoers
# chmod -c 0440 /etc/sudoers

```

### Expiración de la contraseña

Los usuarios pueden estar interesados en cambiar el tiempo de espera predeterminado antes de que la contraseña almacenada en la caché caduque. Esto se logra con la opción timestamp_timeout en `/etc/sudoers` que se cuenta en minutos. Para configurar el tiempo de espera en 20 minutos:

```
Defaults:USER_NAME timestamp_timeout=20

```

**Sugerencia:** Para asegurar que sudo siempre pedirá una contraseña, establezca el tiempo de espera en 0\. Para garantizar que la contraseña nunca expire, establezca timeout en menos de 0.

## Consejos y trucos

### Archivo de ejemplo

Este ejemplo es especialmente útil para aquellos que utilizan multiplexores de terminales como screen, tmux o ratpoison, y los que usan sudo desde scripts/cronjobs:

 `/etc/sudoers` 

```
Cmnd_Alias WHEELER = /usr/sbin/lsof, /bin/nice, /bin/ps, /usr/bin/top, /usr/local/bin/nano, /usr/sbin/ss, /usr/bin/locate, /usr/bin/find, /usr/bin/rsync
Cmnd_Alias PROCESSES = /bin/nice, /bin/kill, /usr/bin/nice, /usr/bin/ionice, /usr/bin/top, /usr/bin/kill, /usr/bin/killall, /usr/bin/ps, /usr/bin/pkill
Cmnd_Alias EDITS = /usr/bin/vim, /usr/bin/nano, /usr/bin/cat, /usr/bin/vi
Cmnd_Alias ARCHLINUX = /usr/sbin/gparted, /usr/bin/pacman

root ALL = (ALL) ALL
USER_NAME ALL = (ALL) ALL, NOPASSWD: WHEELER, NOPASSWD: PROCESSES, NOPASSWD: ARCHLINUX, NOPASSWD: EDITS

Defaults !requiretty, !tty_tickets, !umask
Defaults visiblepw, path_info, insults, lecture=always
Defaults loglinelen = 0, logfile =/var/log/sudo.log, log_year, log_host, syslog=auth
Defaults mailto=webmaster@foobar.com, mail_badpass, mail_no_user, mail_no_perms
Defaults passwd_tries = 8, passwd_timeout = 1
Defaults env_reset, always_set_home, set_home, set_logname
Defaults !env_editor, editor="/usr/bin/vim:/usr/bin/vi:/usr/bin/nano"
Defaults timestamp_timeout=360
Defaults passprompt="Sudo invoked by [%u] on [%H] - Cmd run as %U - Password for user %p:"

```

### Activar la función autocompletar con Tab en Bash

`Tab`-completion, por defecto, no funciona cuando un usuario se añade inicialmente al archivo sudoers. Por ejemplo, Juan normalmente necesita escribir solo:

```
$ fire<`Tab`>

```

y la shell completará el mandato para él como:

```
$ firefox

```

Sin embargo, si Juan es agregado al archivo sudoers y escribe:

```
$ sudo fire<`Tab`>

```

la shell no hará nada.

Para activar `Tab`-completion con sudo, [instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) desde los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)"). Véase [bash#Auto-completion](/index.php/Bash#Auto-completion "Bash") para obtener más información

Como alternativa, añada lo siguiente al archivo `~/.bashrc`:

```
complete -cf sudo

```

### Ejecutar aplicaciones X11 utilizando sudo

Para permitir que sudo inicie una aplicación gráfica en X11, es necesario agregar:

```
Defaults env_keep += "HOME"

```

a visudo.

### Desactivar sudo para cada terminal

**Advertencia:** Esto permitirá usar cualquier proceso desde la sesión de sudo.

Si le molesta que sudo, de forma predeterminada, le obligue a introducir la contraseña cada vez que se abre una nueva terminal, desactive **tty_tickets**:

```
Defaults !tty_tickets

```

### Variables de entornos

Si se tienen muchas variables de entorno, o exporta la configuración del proxy a través de `export http_proxy="..."`, al usar sudo estas variables no se pasan a la cuenta de root, a menos que ejecute sudo con la opción `-E`.

```
$ sudo -E pacman -Syu

```

La forma recomendada de preservar las variables de entorno es añadiendo a `env_keep`:

 `/etc/sudoers` 

```
Defaults env_keep += "ftp_proxy http_proxy https_proxy no_proxy"

```

### Activar alias

Si utiliza muchos alias, habrá advertido que no se transfieren a la cuenta de root cuando usa sudo. No obstante, hay una manera fácil de hacer que funcionen. Solo tiene que añadir lo siguiente a `~/.bashrc` o a `/etc/bash.bashrc`:

```
alias sudo='sudo '

```

### Avisos

Los usuarios pueden configurar sudo para mostrar _«avisos ingeniosos»»_ cuando se introduce una contraseña incorrecta, en lugar de mostrar el mensaje predeterminado «contraseña incorrecta» (_wrong password_) . Busque la línea Defaults en `/etc/sudoers` y añada el parámetro «insults», separándolo con una coma de las opciones existentes. El resultado final podría verse así:

```
#Defaults specification
Defaults insults

```

Para probar, escriba `sudo -K` para finalizar la sesión actual y dejar que sudo pida la contraseña de nuevo.

### Contraseña root

Los usuarios pueden configurar sudo para pedir la contraseña de root, en lugar de la contraseña de usuario, añadiendo "rootpw" a la línea Defaults en `/etc/sudoers`:

```
Defaults timestamp_timeout=0,rootpw

```

### Desactivar el acceso de root

**Advertencia:** Arch Linux no viene ajustado para funcionar con una cuenta de root desactivada. Los usuarios pueden encontrar problemas con este método.

Con sudo instalado y configurado, el usuario puede deshabilitar el inicio de sesión de root. Sin root, los _«attackers»_, primero, deben adivinar un nombre de usuario configurado como un sudoer y, luego, la contraseña de usuario.

**Advertencia:** Asegúrese de que un usuario está correctamente configurado como un sudoer _antes_ de desactivar la cuenta de root.

La cuenta puede ser bloqueada mediante `passwd`:

```
# passwd -l root

```

Una orden similar desbloquea root.

```
$ sudo passwd -u root

```

De forma alternativa, edite `/etc/shadow` y vuelva a colocar la contraseña cifrada de root con «!»:

```
root:!:12345::::::

```

Para activar el acceso de root de nuevo:

```
$ sudo passwd root

```

#### kdesu

kdesu puede ser utilizado bajo KDE para lanzar aplicaciones gráficas con privilegios de root. Es posible que, por defecto, kdesu trate de usar _«su»_, incluso si la cuenta de root está desactivada. Afortunadamente se puede invocar kdesu para usar «sudo» en lugar de «su». Cree/modifique el archivo `~/.kde4/share/config/kdesurc`:

```
[super-user-command]
super-user-command=sudo

```

#### PolicyKit

Al desactivar la cuenta de root, es necesario cambiar la configuración de [PolicyKit](/index.php/PolicyKit "PolicyKit") para hacer que la autorización local actúe en consecuencia. El valor predeterminado es solicitar la contraseña de root, por lo que debe ser cambiado. Con polkit-1, esto se puede lograr mediante la edición de `/etc/polkit-1/localauthority.conf.d/50-localauthority.conf` de manera que `AdminIdentities=unix-user:0` se modifique añadiéndole algo más, dependiendo de la configuración del sistema. Puede ser con una lista de usuarios y grupos, por ejemplo:

```
AdminIdentities=unix-group:wheel

```

o

```
AdminIdentities=unix-user:me;unixuser:mom;unix-group:wheel

```

Para obtener más información, véase `man pklocalauthority`.

#### NetworkManager

Incluso con la configuración anterior de PolicyKit todavía necesita configurar una política para NetworkManager. Esto está documentado en la página [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") de esta wiki

### Ejemplo para proteger con sudo

Pongamos por caso que se crean 3 usuarios: admin, devel y Joe.

*   admin es utilizado para journalctl, systemctl, mount, kill, e iptables.

*   devel es utilizado para instalar paquetes y editar archivos de configuración.

*   Joe es el usuario con el que se inicia sesión. Podrá reiniciar, apagar y usar netctl.

Edite `/etc/pam.d/su and /etc/pam.d/su-1`

Demande que el usuario esté en el grupo `wheel`, pero no ponga a nadie en él.

```
#%PAM-1.0
auth            sufficient      pam_rootok.so
# Uncomment the following line to implicitly trust users in the "wheel" group.
#auth           sufficient      pam_wheel.so trust use_uid
# Uncomment the following line to require a user to be in the "wheel" group.
auth            required        pam_wheel.so use_uid
auth            required        pam_unix.so
account         required        pam_unix.so
session         required        pam_unix.so

```

Limite el inicio de sesión de SSH al grupo `ssh`, y ponga únicamente a Joe en él.

```
groupadd -r ssh
gpasswd -a Joe ssh
echo 'AllowGroups ssh' >> /etc/ssh/sshd_config
systemctl restart sshd.service

```

Permita agregar usuarios a otros grupos.

```
for g in power network ;do ;gpasswd -a Joe $g ;done
for g in network power storage ;do ;gpasswd -a admin $g ;done

```

Ajuste los permisos sobre las configuraciones para que pueda editarlas.

```
chown -R devel:root /etc/{http,openvpn,cups,zsh,vim,screenrc}

```

```
Cmnd_Alias  POWER       =   /usr/bin/shutdown -h now, /usr/bin/halt, /usr/bin/poweroff, /usr/bin/reboot
Cmnd_Alias  STORAGE     =   /usr/bin/mount, /usr/bin/umount
Cmnd_Alias  SYSTEMD     =   /usr/bin/journalctl, /usr/bin/systemctl
Cmnd_Alias  KILL        =   /usr/bin/kill, /usr/bin/killall
Cmnd_Alias  PKGMAN      =   /usr/bin/pacman
Cmnd_Alias  NETWORK     =   /usr/bin/netctl
Cmnd_Alias  FIREWALL    =   /usr/bin/iptables, /usr/bin/ip6tables
Cmnd_Alias  SHELL       =   /usr/bin/zsh, /usr/bin/bash
%power      ALL         =   (root)  NOPASSWD: POWER
%network    ALL         =   (root)  NETWORK
%storage    ALL         =   (root)  STORAGE
root        ALL         =   (ALL)   ALL
admin       ALL         =   (root)  SYSTEMD, KILL, FIREWALL
devel	    ALL         =   (root)  PKGMAN
Joe	    ALL         =   (devel) SHELL, (admin) SHELL 

```

Con esta configuración casi nunca se tendrá que iniciar sesión como usuario Root.

Joe se puede conectar a una red WiFi doméstica:

```
sudo netctl start home
sudo poweroff

```

Joe no puede utilizar netctl como cualquier otro usuario como administrador...

```
sudo -u admin -- netctl start home

```

Cuando Joe tiene que utilizar journalctl o terminar la ejecución de un proceso puede cambiar al usuario habilitado:

```
sudo -i -u devel
sudo -i -u admin

```

Pero no es Root:

```
sudo -i -u root

```

Si Joe quiere iniciar una sesión GNU Screen como administrador puede hacerlo de esta manera:

```
sudo -i -u admin
admin% chown admin:tty `echo $TTY`
admin% screen

```

## Solución de problemas

### Problemas de SSH con TTY

SSH no asigna una tty de forma predeterminada cuando se ejecuta un comando remoto. Sin una tty, sudo no puede desactivar _«echo»_ cuando pida la contraseña. Puede utilizar la opción `-tt` para obligar a SSH a asignar una tty (utilice `-tt` dos veces).

La opción `requiretty` de `Defaults` solo permite al usuario ejecutar sudo si tiene una tty.

```
# Desactive "ssh hostname sudo <cmd>", ya que mostrará la contraseña en texto claro. Se tiene que ejecutar "ssh -t hostname sudo <cmd>".
#
#Defaults    requiretty

```

### Mostrar privilegios del usuario

Se puede averiguar cuáles son los privilegios que un usuario en particular tiene con la siguiente orden:

```
$ sudo -lU sunombredeusuario

```

O vea su cuenta con:

 `$ sudo -l` 

```
Matching Defaults entries for yourusename on this host:
(''«Juego de entradas Defaults para sunombredeusuario en este host:»'')
    loglinelen=0, logfile=/var/log/sudo.log, log_year, syslog=auth, mailto=sqpt.webmaster@gmail.com, mail_badpass, mail_no_user, mail_no_perms, env_reset, always_set_home, tty_tickets, lecture=always, pwfeedback, rootpw, set_home

User yourusename may run the following commands on this host:
(''«El usuario sunombredeusuario puede ejecutar las siguientes órdenes en este host:»'')

    (ALL) ALL
    (ALL) NOPASSWD: /usr/sbin/lsof, /bin/nice, /usr/sbin/ss, /usr/bin/su, /usr/bin/locate, /usr/bin/find, /usr/bin/rsync, /usr/bin/strace,
    (ALL) /bin/nice, /bin/kill, /usr/bin/nice, /usr/bin/ionice, /usr/bin/top, /usr/bin/kill, /usr/bin/killall, /usr/bin/ps, /usr/bin/pkill
    (ALL) /usr/sbin/gparted, /usr/bin/pacman
    (ALL) /usr/local/bin/synergyc, /usr/local/bin/synergys
    (ALL) /usr/bin/vim, /usr/bin/nano, /usr/bin/cat
    (root) NOPASSWD: /usr/local/bin/synergyc
```

### Umask permisiva

Sudo reunifica el valor [umask](/index.php/Umask_(Espa%C3%B1ol) "Umask (Español)") del usuario con el del propio umask (que por defecto es 0022). Esto evita que sudo cree archivos con permisos más abiertos que el umask del usuario permite. Si bien esto es un valor predefinido aceptable si el umask personalizado no está en uso, esto puede llevar a situaciones en las que un programa dirigido por sudo puede crear archivos con permisos diferentes que si los ejecutara root directamente. Si se incurre en este tipo de errores, sudo proporciona un medio para fijar la umask del usuario, incluso en el caso de que la umask sea más permisiva respecto de la umask especificada por el usuario. La adición de las líneas de abajo (usando `visudo`) modificará tal comportamiento por defecto de sudo:

```
Defaults umask = 0022
Defaults umask_override

```

Esto establece la umask de sudo para la umask por defecto de root (0022) y sobrescribe el comportamiento predefinido, utilizando siempre la umask indicada, independientemente de cómo la umask del usuario esté configurada.

### Estrutura de Defaults

En [este enlace](http://www.gratisoft.us/sudo/sudoers.man.html#sudoers_options) se puede encontrar una lista de todas las opciones disponibles para su uso con la orden `Defaults` en el archivo `/etc/sudoers`.

La lista completa de opciones _(analizada a partir del código fuente de la versión 1.8.7)_ se reproduce justo debajo en un formato optimizado para copiar y pegar en los archivos sudoers y luego hacer los cambios.

```
#Defaults always_set_home
#  If enabled, sudo will set the HOME environment variable to the home directory of the target user
#  (which is root unless the -u option is used).  This effectively means that the -H option
#  always_set_home is only effective for configurations where either env_reset is disabled or HOME is present
#  in the env_keep list.  Default: OFF

#Defaults authenticate
#  If set, users must authenticate themselves via a password (or other means of authentication)
#  before they may run commands.  This default may be overridden via the PASSWD and NOPASSWD

#Defaults closefrom_override
#  If set, the user may use sudo's -C option which overrides the default starting
#  point at which sudo begins closing open file descriptors.  Default: OFF

#Defaults compress_io
#  If set, and sudo is configured to log a command's input or output, the I/O logs will be
#  compressed using zlib.  This flag is on by default when sudo is compiled with zlib support.

#Defaults env_editor
#  If set, visudo will use the value of the EDITOR or VISUAL environment variables before falling back on the default
#  editor list.  Note that this may create a security hole as it allows th separated list of editors in the editor
#  variable.  visudo will then only use the EDITOR or VISUAL if they match a value specified in editor.  On by default.

#Defaults env_reset
#  If set, sudo will run the command in a minimal environment containing the TERM, PATH, HOME, MAIL, SHELL, LOGNAME,
#  USER, USERNAME and SUDO_* variables.  Any variables in the caller's env in the file specified by the env_file
#  option (if any).  The default contents of the env_keep and env_check lists are displayed when sudo is run by
#  root with the -V option.

#Defaults fast_glob
#  Normally, sudo uses the glob(3) function to do shell-style globbing when matching path names.
#  However, since it accesses the file system, glob(3) can take a long time to complete for som (automounted).
#  The fast_glob option causes sudo to use the fnmatch(3) function, which does not access the file system to do
#  its matching.  The disadvantage of fast_glob is that it is unable to ma names that include globbing characters
#  are used with the negation operator, '!', as such rules can be trivially bypassed.  As such, this option should
#  not be used when sudoers contains rules that

#Defaults fqdn
#  Set this flag if you want to put fully qualified host names in the sudoers file.  I.e., instead of myhost you
#  would use myhost.mydomain.edu.  You may still use the short form if you wish (and sudo unusable if DNS stops
#  working (for example if the machine is not plugged into the network).  Also note that you must use the
#  host's official name as DNS knows it.  That is, you may not use a all aliases from DNS.  If your machine's
#  host name (as returned by the hostname command) is already fully qualified you shouldn't need to set fqdn.
#  Default: OFF

#Defaults ignore_dot
#  If set, sudo will ignore '.' or '' (current dir) in the PATH environment variable; the PATH
#  itself is not modified.  Default: OFF

#Defaults ignore_local_sudoers
#  If set via LDAP, parsing of /etc/sudoers will be skipped.  This is intended for Enterprises that wish to prevent
#  the usage of local sudoers files so that only LDAP is used.  /etc/sudoers does not even need to exist.
#  Since this option tells sudo how to behave when no specific LDAP entries have been matched, this sudo
#  Option is only meaningful for the cn=default

#Defaults insults
#  If set, sudo will insult users when they enter an incorrect password.  Default: OFF

#Defaults log_host
#  If set, the host name will be logged in the (non-syslog) sudo log file.  Default: OFF

#Defaults log_input
#  If set, sudo will run the command in a pseudo tty and log all user input.  If the standard
#  input is not connected to the user's tty, due to I/O redirection or because the command is part Input is logged
#  to the directory specified by the iolog_dir option (/var/log/sudo-io by default) using a unique session ID that
#  is included in the normal sudo log line, prefixed with TSID=.  Note that user input may contain sensitive
#  information such as passwords (even if they are not echoed to the screen), which will be stored in the log file
#  unencrypted.

#Defaults log_output
#  If set, sudo will run the command in a pseudo tty and log all output that is sent to the
#  screen, similar to the script(1) command.  If the standard output or standard error is not connec is also captured and
#  stored in separate log files. Output is logged to the directory specified by the iolog_dir option (/var/log/sudo-io
#  by default) using a unique session ID that is included in the normal sudo log line, prefixed with TSID=.  The Output
#  logs may be viewed with the sudoreplay(8) utility, which can also be used to list or search the available logs.

#Defaults log_year
#  If set, the four-digit year will be logged in the (non-syslog) sudo log file.  Default: OFF

#Defaults long_otp_prompt
#  When validating with a One Time Password (OTP) scheme such as S/Key or OPIE, a two-line
#  prompt is used to make it easier to cut and paste the challenge to a local window

#Defaults mail_always
#  Send mail to the mailto user every time a users runs sudo.  Default: OFF

#Defaults mail_badpass
#  Send mail to the mailto user if the user running sudo does not enter the correct password.
#  Default: OFF

#Defaults mail_no_host
#  If set, mail will be sent to the mailto user if the invoking user exists in the sudoers
#  file, but is not allowed to run commands on the current host.  Default: OFF

#Defaults mail_no_perms
#  If set, mail will be sent to the mailto user if the invoking user is allowed to use sudo
#  but the command they are trying is not listed in their sudoers file entry or is explicitly denied

#Defaults mail_no_user
#  If set, mail will be sent to the mailto user if the invoking user is not in the sudoers file.
#  Default: ON

#Defaults noexec
#  If set, all commands run via sudo will behave as if the NOEXEC tag has been set, unless overridden
#  by a EXEC tag.  See the description of NOEXEC and EXEC below as well as the "PREVENTING SHE

#Defaults path_info
#  Normally, sudo will tell the user when a command could not be found in their PATH environment
#  variable.  Some sites may wish to disable this as it could be used to gather information on t the executable is
#  simply not in the user's PATH, sudo will tell the user that they are not allowed to run it, which can be confusing.
#  Default: ON

#Defaults passprompt_override
#  The password prompt specified by passprompt will normally only be used if the password prompt provided by
#  systems such as PAM matches the string "Password:"

#Defaults preserve_groups
#  By default, sudo will initialize the group vector to the list of groups the target
#  user is in.  When preserve_groups is set, the user's existing group vector is left unaltered.

#Defaults pwfeedback
#  By default, sudo reads the password like most other Unix programs, by turning off echo
#  until the user hits the return (or enter) key.  Some users become confused by this as it appears to the user
#  presses a key.  Note that this does have a security impact as an onlooker may be able to determine the length of
#  the password being entered.  Default: OFF

#Defaults requiretty
#  If set, sudo will only run when the user is logged in to a real tty.  When this flag is set,
#  sudo can only be run from a login session and not via other means such as cron(8) or cgi-bin

#Defaults root_sudo
#  If set, root is allowed to run sudo too.  Disabling this prevents users from "chaining" sudo
#  commands to get a root shell by doing something like "sudo sudo /bin/sh".  Note, however, that real additional
#  security; it exists purely for historical reasons.  Default: ON

#Defaults rootpw
#  If set, sudo will prompt for the root password instead of the password of the invoking user.
#  Default: OFF

#Defaults runaspw
#  If set, sudo will prompt for the password of the user defined by the runas_default option
#  (defaults to root) instead of the password of the invoking user.  Default: OFF

#Defaults set_home
#  If enabled and sudo is invoked with the -s option the HOME environment variable will be set
#  to the home directory of the target user (which is root unless the -u option is used).  So set_home is only
#  effective for configs where either env_reset is disabled or HOME is present in the env_keep list.  Default: OFF

#Defaults set_logname
#  Normally, sudo will set the LOGNAME, USER and USERNAME environment variables to the name
#  of the target user (usually root unless the -u option is given).  However, since some programs ( may be desirable
#  to change this behavior.  This can be done by negating the set_logname option.  Note that if the env_reset option
#  has not been disabled, entries in the env_keep list will override

#Defaults set_utmp
#  When enabled, sudo will create an entry in the utmp (or utmpx) file when a pseudo-tty is
#  allocated.  A pseudo-tty is allocated by sudo when the log_input, log_output or use_pty flags are e the tty, time,
#  type and pid fields updated.  Default: ON

#Defaults setenv
#  Allow the user to disable the env_reset option from the command line via the -E option.
#  Additionally, environment variables set via the command line are not subject to the restrictions impo variables
#  in this manner.  Default: OFF

#Defaults shell_noargs
#  If set and sudo is invoked with no arguments it acts as if the -s option had been given.
#  That is, it runs a shell as root (the shell is determined by the SHELL environment variable if is off by default.

#Defaults stay_setuid
#  Normally, when sudo executes a command the real and effective UIDs are set to the target
#  user (root by default).  This option changes that behaviour such that the real UID is left as the systems that
#  disable some potentially dangerous functionality when a program is run setuid.  This option is only effective on
#  systems with either the setreuid() or setresuid() function.  This flag

#Defaults targetpw
#  If set, sudo will prompt for the password of the user specified by the -u option (defaults to root) instead
#  of the password of the invoking user.  In addition, the timestamp file name will passwd database as an argument
#  to the -u option.  Default: OFF

#Defaults tty_tickets
#  If set, users must authenticate on a per-tty basis.  With this flag enabled, sudo will
#  use a file named for the tty the user is logged in on in the user's time stamp directory.

#Defaults umask_override
#  If set, sudo will set the umask as specified by sudoers without modification.  This makes
#  it possible to specify a more permissive umask in sudoers than the user's own umask and match user's umask and what
#  is specified in sudoers.  Default: OFF

#Defaults use_pty
#  If set, sudo will run the command in a pseudo-pty even if no I/O logging is being gone.
#  A malicious program run under sudo could conceivably fork a background process that retains to the u that impossible.
#  Default: OFF

#Defaults utmp_runas
#  If set, sudo will store the name of the runas user when updating the utmp (or utmpx) file.
#  By default, sudo stores the name of the invoking user.  Default: OFF

#Defaults visiblepw
#  By default, sudo will refuse to run if the user must enter a password but it is not possible to disable echo on the 
#  terminal. If the visiblepw flag is set, sudo will prompt for a password even when it would be visible on the screen. 
#  This makes it possible to run things like "rsh somehost sudo ls" since rsh(1) does not allocate a tty. Default: OFF

#Defaults closefrom
#  Before it executes a command, sudo will close all open file descriptors other than standard
#  input, standard output and standard error (ie: file descriptors 0-2).

#Defaults passwd_tries
#  The number of tries a user gets to enter his/her password before sudo logs the failure
#  and exits.  The default is 3.

#Defaults loglinelen
#  Number of characters per line for the file log.  This value is used to decide when to wrap
#  lines for nicer log files.  This has no effect on the syslog log file, only the file log.

#Defaults passwd_timeout
#  Number of minutes before the sudo password prompt times out, or 0 for no timeout.
#  The timeout may include a fractional component if minute granularity is insufficient, for example 2

#Defaults timestamp_timeout
#  Number of minutes that can elapse before sudo will ask for a passwd again.  The timeout
#  may include a fractional component if minute granularity is insufficient, for example 2.5\. timestamp will never expire.
#  This can be used to allow users to create or delete their own timestamps via sudo -v and sudo -k respectively.

#Defaults umask
#  Umask to use when running the command.  Negate this option or set it to 0777 to preserve
#  the user's umask.  The actual umask that is used will be the union of the user's umask and the value o running
#  a command.  Note on systems that use PAM, the default PAM configuration may specify its own umask which will
#  override the value set in sudoers.

#Defaults badpass_message
#  Message that is displayed if a user enters an incorrect password.  The default is Sorry,
#  try again. unless insults are enabled.

#Defaults editor
#  A colon (':') separated list of editors allowed to be used with visudo.  visudo will choose
#  the editor that matches the user's EDITOR environment variable if possible, or the first editor in

#Defaults iolog_dir
#  The top-level directory to use when constructing the path name for the input/output log
#  directory.  Only used if the log_input or log_output options are enabled or when the LOG_INPUT or L directory.
#  The default is "/var/log/sudo-io". The following percent (%) escape sequences are supported:
#    %{seq}         - expanded to base-36 sequence number, such as 0100A5, to form a new directory, e.g. 01/00/A5
#    %{user}        - expanded to the invoking user's login name
#    %{group}       - expanded to the name of the invoking user's real group ID
#    %{runas_user}  - expanded to the login name of the user the command will be run as (e.g. root)
#    %{runas_group} - expanded to the group name of the user the command will be run as (e.g. wheel)
#    %{hostname}    - expanded to the local host name without the domain name
#    %{command}     - expanded to the base name of the command being run In addition, any escape sequences supported by
#                     strftime() function will be expanded. To include a literal % character, the string %% should be used.

#Defaults iolog_file
#  The path name, relative to iolog_dir, in which to store input/output logs when the log_input or log_output options are
#  enabled or when the LOG_INPUT or LOG_OUTPUT tags are present for a See the iolog_dir option above for a list of
#  supported percent (%) escape sequences. In addition to the escape sequences, path names that end in six or more Xs will
#  have the Xs replaced with a unique combination of digits and letters, similar to the mktemp() function.

#Defaults mailsub
#  Subject of the mail sent to the mailto user. The escape %h will expand to the host name of
#  the machine.  Default is *** SECURITY information for %h ***.

#Defaults noexec_file
#  This option is no longer supported.  The path to the noexec file should now be set in the /etc/sudo.conf file.

#Defaults passprompt
#  The default prompt to use when asking for a password; can be overridden via the -p option or the SUDO_PROMPT
#  environment variable.  The following percent (%) escape sequences are supported:
#    %H - expanded to the local host name including the domain (only if the host name is fqdn or fqdn option is set)
#    %h - expanded to the local host name without the domain name
#    %p - expanded to the user whose password is being asked for (respects the rootpw, targetpw and runaspw flags)
#    %U - expanded to the login name of the user the command will be run as (defaults to root)
#    %u - expanded to the invoking user's login name
#    %% - two consecutive % characters are collapsed into a single % character
#  The default value is Password:.

#Defaults runas_default
#  The default user to run commands as if the -u option is not specified on the command line. This defaults to root.

#Defaults syslog_badpri
#  Syslog priority to use when user authenticates unsuccessfully.  Defaults to alert.
#  alert, crit, debug, emerg, err, info, notice, and warning.

#Defaults syslog_goodpri
#  Syslog priority to use when user authenticates successfully.  Defaults to notice. See syslog_badpri for the priorities.

#Defaults sudoers_locale
#  Locale to use when parsing the sudoers file, logging commands, and sending email.
#  Note that changing the locale may affect how sudoers is interpreted.  Defaults to "C".

#Defaults timestampdir
#  The directory in which sudo stores its timestamp files.  The default is /var/db/sudo.

#Defaults timestampowner
#  The owner of the timestamp directory and the timestamps stored therein.  The default is root.

#Defaults env_file
#  The env_file option specifies the fully qualified path to a file containing variables to
#  be set in the environment of the program being run.  Entries in this file should either be of the f quotes.
#  Variables in this file are subject to other sudo environment settings such as env_keep and env_check.

#Defaults exempt_group
#  Users in this group are exempt from password and PATH requirements.  The group name specified should not include
#  a % prefix.  This is not set by default.

#Defaults group_plugin
#  A string containing a sudoers group plugin with optional arguments.  This can be used to implement support for the
#  nonunix_group syntax described earlier.  The string should consist of configuration arguments the plugin requires.
#  These arguments (if any) will be passed to the plugin's initialization function. If arguments are present, the
#  string must be enclosed in double quote For example, given /etc/sudo-group, a group file in Unix group format,
#  the sample group plugin can be used: Defaults group_plugin="sample_group.so /etc/sudo-group"
#  For more information see sudo_plugin(5).

#Defaults lecture
#  This option controls when a short lecture will be printed along with the password prompt.  The default value is once.
#  It has the following possible values:
#    always - Always lecture the user.
#    never  - Never lecture the user.
#    once   - Only lecture the user the first time they run sudo.
#  If no value is specified, a value of once is implied.  Negating the option results in a value of never being used.

#Defaults lecture_file
#  Path to a file containing an alternate sudo lecture that will be used in place of the standard lecture if the named
#  file exists.  By default, sudo uses a built-in lecture.

#Defaults listpw
#  This option controls when a password will be required when a user runs sudo with the -l option.
#  It has the following possible values:
#    all    - All the user's sudoers entries for the current host must have the NOPASSWD set to avoid entering a pass.
#    always - The user must always enter a password to use the -l option.
#    any    - At least one of the user's sudoers entries for the current host must have the NOPASSWD set to avoid pass.
#    never  - The user need never enter a password to use the -l option.
#  If no value is specified, a value of any is implied.  The default value is any.

#Defaults logfile
#  Path to the sudo log file (not the syslog log file).  Setting a path turns on logging to a file;
#  negating this option turns it off.  By default, sudo logs via syslog.

#Defaults mailerflags
#  Flags to use when invoking mailer. Defaults to -t.

#Defaults mailerpath
#  Path to mail program used to send warning mail.  Defaults to the path to sendmail found at configure time.

#Defaults mailfrom
#  Address to use for the "from" address when sending warning and error mail.  The address should
#  be enclosed in double quotes (") to protect against sudo interpreting the @ sign.

#Defaults mailto
#  Address to send warning and error mail to.  The address should be enclosed in double quotes
#  (") to protect against sudo interpreting the @ sign.  Defaults to root.

#Defaults secure_path
#  Path used for every command run from sudo.  If you don't trust the people running sudo to have a sane PATH environment
#  variable you may want to use this.  Another use is if you want to option are not affected by secure_path.
#  This option is not set by default.

#Defaults syslog
#  Syslog facility if syslog is being used for logging (negate to disable syslog logging). Defaults to auth.
#  authpriv (if OS supports it), auth, daemon, user, local0, local1, local2, local3, local4, local5, local6, and local7.

#Defaults verifypw
#  This option controls when a password will be required when a user runs sudo with the -v option.
#  It has the following possible values:
#    all    - All the user's sudoers entries for the current host must have the NOPASSWD flag to avoid pw.
#    always - The user must always enter a password to use the -v option.
#    any    - At least one of the user's sudoers entries for the current host must have NOPASSWD to avoid pw.
#    never  - The user need never enter a password to use the -v option
#  If no value is specified, a value of all is implied.  Negating the option results in a value of never being used.
#  The default value is all.

#Defaults env_check
#  Environment variables to be removed from the user's environment if the variable's value contains % or / characters.
#  This can be used to guard against printf-style format vulnerabilities value without double-quotes.  The list can be
#  replaced, added to, deleted from, or disabled by using the =, +=, -=, and ! operators respectively.  Regardless of
#  whether the env_reset option is ena they pass the aforementioned check. The default list of environment variables
#  to check is displayed when sudo is run by root with the -V option.

#Defaults env_delete
#  Environment variables to be removed from the user's environment when the env_reset option is not in effect.  The
#  argument may be a double-quoted, space-separated list or a single value w +=, -=, and ! operators respectively.
#  The default list of environment variables to remove is displayed when sudo is run by root with the -V option.

#Defaults env_keep
#  Environment variables to be preserved in the user's environment when the env_reset option is in effect.  This
#  allows fine-grained control over the environment sudo-spawned processes will r quotes.  The list can be replaced,
#  added to, deleted from, or disabled by using the =, +=, -=, and ! operators respectively.
```