**Estado de la traducción:** este artículo es una versión traducida de [sudo](/index.php/Sudo "Sudo"). Fecha de la última traducción/revisión: **2018-08-10**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Sudo&diff=0&oldid=529530).

Artículos relacionados

*   [Usuarios y grupos](/index.php/Users_and_Groups_(Espa%C3%B1ol) "Users and Groups (Español)")
*   [su](/index.php/Su_(Espa%C3%B1ol) "Su (Español)")

[Sudo](https://www.sudo.ws/sudo/) permite al administrador del sistema delegar autoridad para otorgar a ciertos usuarios (o grupos de usuarios) la capacidad de ejecutar comandos como superusuario *(root)* u otro mientras proporciona un registro de auditoría de los comandos y sus argumentos.

Sudo es una alternativa a [su](/index.php/Su_(Espa%C3%B1ol) "Su (Español)") para ejecutar comandos como superusuario. A diferencia de **su**, que lanza un shell de superusuario que permite que todos los demás comandos tengan acceso de superusuario, sudo ofrece una escalada temporal de privilegios a un solo comando. Al habilitar los privilegios de superusuario solo cuando es necesario, el uso de sudo reduce la probabilidad de que un error tipográfico o en un comando invocado arruine el sistema.

Sudo también se puede usar para ejecutar comandos como otros usuarios; además, sudo registra todos los comandos y los intentos de acceso fallidos para la auditoría de seguridad.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Utilización](#Utilizaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Ver la configuración actual](#Ver_la_configuraci.C3.B3n_actual)
    *   [3.2 Usando visudo](#Usando_visudo)
    *   [3.3 Ejemplos de entradas](#Ejemplos_de_entradas)
    *   [3.4 Permisos de archivos predeterminados por sudoers](#Permisos_de_archivos_predeterminados_por_sudoers)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Desactivar sudo para cada terminal](#Desactivar_sudo_para_cada_terminal)
    *   [4.2 Variables de entornos](#Variables_de_entornos)
    *   [4.3 Activar alias](#Activar_alias)
    *   [4.4 Avisos](#Avisos)
    *   [4.5 Contraseña root](#Contrase.C3.B1a_root)
    *   [4.6 Desactivar el acceso de root](#Desactivar_el_acceso_de_root)
        *   [4.6.1 kdesu](#kdesu)
    *   [4.7 Ejemplo para proteger con sudo](#Ejemplo_para_proteger_con_sudo)
*   [5 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [5.1 Problemas de SSH con TTY](#Problemas_de_SSH_con_TTY)
    *   [5.2 Umask permisiva](#Umask_permisiva)
    *   [5.3 Estructura por defecto](#Estructura_por_defecto)

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [sudo](https://www.archlinux.org/packages/?name=sudo).

## Utilización

Para comenzar a usar `sudo` como un usuario sin privilegios, debe estar configurado correctamente. Consulte la sección de [configuración](#Configuraci.C3.B3n).

Para usar *sudo*, simplemente anteponga `sudo` y un espacio al comando y sus argumentos:

```
$ sudo *comando*

```

Por ejemplo, para usar pacman:

```
$ sudo pacman -Syu

```

Consulte [sudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudo.8) para más información.

## Configuración

Consulte [sudoers(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudoers.5) para más información, como configurar el tiempo de espera de la contraseña.

### Ver la configuración actual

Ejecute `sudo -ll` para visualizar la configuración actual de sudo, o `sudo -lU *usuario*` para un usuario específico.

### Usando visudo

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

## Consejos y trucos

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

Los usuarios pueden configurar sudo para mostrar *«avisos ingeniosos»»* cuando se introduce una contraseña incorrecta, en lugar de mostrar el mensaje predeterminado «contraseña incorrecta» (*wrong password*) . Busque la línea Defaults en `/etc/sudoers` y añada el parámetro «insults», separándolo con una coma de las opciones existentes. El resultado final podría verse así:

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

Con sudo instalado y configurado, el usuario puede deshabilitar el inicio de sesión de root. Sin root, los *«attackers»*, primero, deben adivinar un nombre de usuario configurado como un sudoer y, luego, la contraseña de usuario.

**Advertencia:** Asegúrese de que un usuario está correctamente configurado como un sudoer *antes* de desactivar la cuenta de root.

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

kdesu puede ser utilizado bajo KDE para lanzar aplicaciones gráficas con privilegios de root. Es posible que, por defecto, kdesu trate de usar *«su»*, incluso si la cuenta de root está desactivada. Afortunadamente se puede invocar kdesu para usar «sudo» en lugar de «su». Cree/modifique el archivo `~/.kde4/share/config/kdesurc`:

```
[super-user-command]
super-user-command=sudo

```

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

SSH no asigna una tty de forma predeterminada cuando se ejecuta un comando remoto. Sin una tty, sudo no puede desactivar *«echo»* cuando pida la contraseña. Puede utilizar la opción `-tt` para obligar a SSH a asignar una tty (utilice `-tt` dos veces).

La opción `requiretty` de `Defaults` solo permite al usuario ejecutar sudo si tiene una tty.

```
# Desactive "ssh hostname sudo <cmd>", ya que mostrará la contraseña en texto claro. Se tiene que ejecutar "ssh -t hostname sudo <cmd>".
#
#Defaults    requiretty

```

### Umask permisiva

Sudo reunifica el valor [umask](/index.php/Umask_(Espa%C3%B1ol) "Umask (Español)") del usuario con el del propio umask (que por defecto es 0022). Esto evita que sudo cree archivos con permisos más abiertos que el umask del usuario permite. Si bien esto es un valor predefinido aceptable si el umask personalizado no está en uso, esto puede llevar a situaciones en las que un programa dirigido por sudo puede crear archivos con permisos diferentes que si los ejecutara root directamente. Si se incurre en este tipo de errores, sudo proporciona un medio para fijar la umask del usuario, incluso en el caso de que la umask sea más permisiva respecto de la umask especificada por el usuario. La adición de las líneas de abajo (usando `visudo`) modificará tal comportamiento por defecto de sudo:

```
Defaults umask = 0022
Defaults umask_override

```

Esto establece la umask de sudo para la umask por defecto de root (0022) y sobrescribe el comportamiento predefinido, utilizando siempre la umask indicada, independientemente de cómo la umask del usuario esté configurada.

### Estructura por defecto

La página de los autores tiene una [lista de todas las opciones](http://www.sudo.ws/sudo/sudoers.man.html#x5355444f455253204f5054494f4e53) que se puede usar con el comando `Defaults` en el archivo `/etc/sudoers`.

Consulte [[1]](https://gist.github.com/AladW/7eca9799b9ea624eca31) para obtener una lista de opciones (analizadas desde el código fuente de la versión 1.8.7) en un formato optimizado para `sudoers`.