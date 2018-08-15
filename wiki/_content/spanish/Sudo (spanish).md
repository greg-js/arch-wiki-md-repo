**Estado de la traducción:** este artículo es una versión traducida de [sudo](/index.php/Sudo "Sudo"). Fecha de la última traducción/revisión: **2018-08-13**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Sudo&diff=0&oldid=534686).

Related articles

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
    *   [3.2 Utilizando visudo](#Utilizando_visudo)
    *   [3.3 Ejemplos de entradas](#Ejemplos_de_entradas)
    *   [3.4 Permisos de archivo predeterminados de sudoers](#Permisos_de_archivo_predeterminados_de_sudoers)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Deshabilitar sudo por cada terminal](#Deshabilitar_sudo_por_cada_terminal)
    *   [4.2 Variables de entorno](#Variables_de_entorno)
    *   [4.3 Transferir alias](#Transferir_alias)
    *   [4.4 Contraseña de superusuario](#Contrase.C3.B1a_de_superusuario)
    *   [4.5 Desactivar el acceso de superusuario](#Desactivar_el_acceso_de_superusuario)
        *   [4.5.1 kdesu](#kdesu)
    *   [4.6 Ejemplo de protección con sudo](#Ejemplo_de_protecci.C3.B3n_con_sudo)
    *   [4.7 Configurar sudo mediante archivos complementarios en /etc/sudoers.d](#Configurar_sudo_mediante_archivos_complementarios_en_.2Fetc.2Fsudoers.d)
    *   [4.8 Edición de archivos](#Edici.C3.B3n_de_archivos)
*   [5 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [5.1 Problemas de TTY con SSH](#Problemas_de_TTY_con_SSH)
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

### Utilizando visudo

El archivo de configuración de sudo es `/etc/sudoers`. **Siempre** debe editarse con el comando [visudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/visudo.8). `visudo` bloquea el archivo `sudoers`, guarda los cambios en un archivo temporal y verifica la gramática de dicho archivo antes de copiarlo en `/etc/sudoers`.

**Advertencia:** ¡Es imperativo que el archivo `sudoers` no tenga errores de sintaxis! Cualquier error hará sudo inutilizable. Modifíquelo **siempre** con `visudo` para evitar errores.

El editor predeterminado para visudo es `vi`. sudo del repositorio central *(core)* se compila con `--with-env-editor` de forma predeterminada y respeta el uso de las variables `VISUAL` y `EDITOR`. `EDITOR` no se usa cuando se establece `VISUAL`.

Para establecer nano como el editor de **visudo** durante la sesión actual de shell exporte `EDITOR=nano`; para usar un editor diferente una vez, simplemente configure la variable antes de llamar a **visudo**:

```
# EDITOR=nano visudo

```

Alternativamente, puede editar una copia del archivo `/etc/sudoers` y verificarlo utilizando `visudo -c -f */copy/of/sudoers*`. Esto podría ser útil en caso de que quiera eludir el bloqueo del archivo con visudo.

Para cambiar el editor permanentemente, consulte la sección sobre [variables de entorno por usuario](/index.php/Environment_variables_(Espa%C3%B1ol)#Por_usuario "Environment variables (Español)"). Para cambiar el editor elegido solo para `visudo` de forma permanente en todo el sistema, añada lo siguiente a `/etc/sudoers` (suponiendo que `nano` es su editor preferido):

```
# Restablece el entorno predeterminado
Defaults      env_reset
# Establece el EDITOR predeterminado a nano, y no permite a visudo usar EDITOR/VISUAL.
Defaults      editor=/usr/bin/nano, !env_editor

```

### Ejemplos de entradas

Para permitir a un usuario normal obtener privilegios de superusuario *(root)* cuando antepone `sudo` a una orden, añada la siguiente línea:

```
NOMBRE_DE_USUARIO   ALL=(ALL) ALL

```

Para permitir a un usuario ejecutar todas los comandos como cualquier usuario, pero únicamente en la máquina con el nombre `NOMBRE_DEL_EQUIPO`:

```
NOMBRE_DE_USUARIO   NOMBRE_DE_EQUIPO=(ALL) ALL

```

Para permitir que los miembros del grupo `wheel` tengan acceso a sudo:

```
%wheel      ALL=(ALL) ALL

```

Para dehabilitar la solicitud de contraseña para el usuario `NOMBRE_DE_USUARIO`:

**Advertencia:** Esto permitirá que cualquier proceso que se ejecute con su nombre de usuario use sudo sin solicitar permiso.

```
Defaults:NOMBRE_DE_USUARIO      !authenticate

```

Para habilitar las órdenes definidas explícitamente solo para el usuario `NOMBRE_DE_USUARIO` en el equipo `NOMBRE_DEL_EQUIPO`:

```
NOMBRE_DE_USUARIO NOMBRE_DEL_EQUIPO=/usr/bin/halt,/usr/bin/poweroff,/usr/bin/reboot,/usr/bin/pacman -Syu

```

**Nota:** La opción más personalizada debe ir al final del archivo, ya que las líneas posteriores anulan las anteriores. En particular, una línea de este tipo debe estar después de la línea `%wheel` si su usuario está en este grupo.

Para activar, sin necesidad de contraseña, los comandos definidos explícitamente solo para el usuario `NOMBRE_DE_USUARIO` en el equipo `NOMBRE_DEL_EQUIPO`:

```
NOMBRE_DE_USUARIO NOMBRE_DEL_EQUIPO= NOPASSWD: /usr/bin/halt,/usr/bin/poweroff,/usr/bin/reboot,/usr/bin/pacman -Syu

```

Un ejemplo detallado de `sudoers` está disponible en `/usr/share/doc/sudo/examples/sudoers`. Por otro lado, consulte [sudoers(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudoers.5) para obtener información detallada.

### Permisos de archivo predeterminados de sudoers

El propietario y el grupo para el archivo `sudoers` deben ser ambos 0\. Los permisos de los archivos deben establecerse en 0440\. Estos permisos se establecen de forma predeterminada, pero si los cambia accidentalmente, deberían ser cambiados de nuevo inmediatamente o sudo fallará.

```
# chown -c root:root /etc/sudoers
# chmod -c 0440 /etc/sudoers

```

## Consejos y trucos

### Deshabilitar sudo por cada terminal

**Advertencia:** Esto permitirá que cualquier proceso use su sesión sudo.

Si le molesta que sudo, de forma predeterminada, requiera introducir la contraseña cada vez que abra un nuevo terminal, deshabilite **tty_tickets**:

```
Defaults !tty_tickets

```

### Variables de entorno

Si se tienen muchas variables de entorno, o exporta la configuración del proxy a través de `export http_proxy="..."`, al usar sudo estas variables no se pasan a la cuenta de root, a menos que ejecute sudo con la opción `-E`.

```
$ sudo -E pacman -Syu

```

La forma recomendada de preservar las variables de entorno es añadiendo a `env_keep`:

 `/etc/sudoers` 
```
Defaults env_keep += "ftp_proxy http_proxy https_proxy no_proxy"

```

### Transferir alias

Si utiliza muchos alias, es posible que haya notado que no se transfieren a la cuenta de superusuario al usar sudo. Sin embargo, hay una manera fácil de hacer que funcionen. Simplemente añada lo siguiente a su `~/.bashrc` o `/etc/bash.bashrc`:

```
alias sudo='sudo '

```

### Contraseña de superusuario

Los usuarios pueden configurar sudo para solicitar la contraseña del superusuario en lugar de la contraseña de usuario añadiendo `targetpw` (usuario de destino, predeterminado a superusuario) o `rootpw` a la línea Defaults en `/etc/sudoers`:

```
Defaults targetpw

```

Para evitar exponer su contraseña de superusuario a los usuarios, puede restringirla a un grupo específico:

```
Defaults:%wheel targetpw
%wheel ALL=(ALL) ALL

```

### Desactivar el acceso de superusuario

Los usuarios pueden querer deshabilitar el inicio de sesión del superusuario. Sin este, los atacantes deben primero adivinar un nombre de usuario configurado como sudoer, así como su contraseña. Consulte por ejemplo [Denegar](/index.php/Secure_Shell_(Espa%C3%B1ol)#Denegar "Secure Shell (Español)").

**Advertencia:**

*   Tenga cuidado, puede bloquearse al deshabilitar el inicio de sesión del superusuario. Sudo no se instala automáticamente y su configuración predeterminada no permite el acceso al superusuario sin contraseña ni con su propia contraseña. Asegúrese de que el usuario esté configurado correctamente como un sudoer *antes* de deshabilitar la cuenta de superusuario.
*   Si ha cambiado su archivo sudoers para usar rootpw como predeterminado, entonces no desactive el inicio de sesión del superusuario con ninguno de los siguientes comandos.
*   Si ya está bloqueado, consulte como [reiniciar la contraseña del superusuario](/index.php/Reset_root_password "Reset root password") para obtener ayuda.

La cuenta puede ser bloqueada mediante `passwd`:

```
# passwd -l root

```

Una orden similar desbloquea al superusuario.

```
$ sudo passwd -u root

```

Alternativamente, edite `/etc/shadow` y reemplace la contraseña cifrada del superusuario *(root)* con «!»:

```
root:!:12345::::::

```

Para activar de nuevo el acceso del superusuario:

```
$ sudo passwd root

```

**Sugerencia:** Para acceder a un shell de superusuario, incluso después de deshabilitar la cuenta *root*, utilice `sudo -i`.

#### kdesu

kdesu puede ser utilizado bajo KDE para lanzar aplicaciones gráficas con privilegios de superusuario. Es posible que, por defecto, kdesu trate de usar su incluso si la cuenta de superusuario está desactivada. Afortunadamente se puede invocar kdesu para usar sudo en lugar de su. Cree/modifique el archivo `~/.config/kdesurc`:

```
[super-user-command]
super-user-command=sudo

```

o use el siguiente comando:

```
$ kwriteconfig5 --file kdesurc --group super-user-command --key super-user-command sudo

```

Alternativamente, instale [kdesudo](https://aur.archlinux.org/packages/kdesudo/), que tiene la ventaja adicional de autocompletar con tabulador el comando siguiente.

### Ejemplo de protección con sudo

Digamos que crea 3 usuarios: admin, devel y joe. El usuario «admin» se usa para journalctl, systemctl, mount, kill e iptables; «devel» se usa para instalar paquetes y editar archivos de configuración; y «joe» es el usuario con el que inicia sesión. Para permitir a «joe» reiniciar, apagar y usar netctl, haríamos lo siguiente:

Edite `/etc/pam.d/su` y `/etc/pam.d/su-1` Requiere que el usuario esté en el grupo wheel, pero no ponga a nadie en él.

```
#%PAM-1.0
auth            sufficient      pam_rootok.so
# Descomente la siguiente línea para confiar implícitamente en los usuarios del grupo "wheel".
#auth           sufficient      pam_wheel.so trust use_uid
# Descomente la siguiente línea para requerir que un usuario esté en el grupo "wheel".
auth            required        pam_wheel.so use_uid
auth            required        pam_unix.so
account         required        pam_unix.so
session         required        pam_unix.so

```

Limite el inicio de sesión de SSH al grupo 'ssh'. Solo «joe» será parte de este grupo.

```
groupadd -r ssh
gpasswd -a joe ssh
echo 'AllowGroups ssh' >> /etc/ssh/sshd_config

```

[Reinicie](/index.php/Restart "Restart") `sshd.service`.

Añada usuarios a otros grupos.

```
for g in power network ;do ;gpasswd -a joe $g ;done
for g in network power storage ;do ;gpasswd -a admin $g ;done

```

Ajuste los permisos en las configuraciones para que «devel» pueda editarlos.

```
chown -R devel:root /etc/{http,openvpn,cups,zsh,vim,screenrc}

```

```
Cmnd_Alias  POWER       =   /usr/bin/shutdown -h now, /usr/bin/halt, /usr/bin/poweroff, /usr/bin/reboot
Cmnd_Alias  STORAGE     =   /usr/bin/mount -o nosuid\,nodev\,noexec, /usr/bin/umount
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
devel       ALL         =   (root)  PKGMAN
joe         ALL         =   (devel) SHELL, (admin) SHELL 

```

Con esta configuración, casi nunca necesitará iniciar sesión como superusuario.

«joe» se puede conectar a una red inalámbrica doméstica:

```
sudo netctl start home
sudo poweroff

```

«joe» no puede utilizar netctl como cualquier otro usuario.

```
sudo -u admin -- netctl start home

```

Cuando «joe» necesite utilizar journalctl o terminar la ejecución de un proceso puede cambiar a dicho usuario:

```
sudo -i -u devel
sudo -i -u admin

```

Pero «joe» no puede cambiar a superusuario:

```
sudo -i -u root

```

Si «joe» quiere iniciar una sesión gnu-screen como «admin» puede hacerlo así:

```
sudo -i -u admin
admin% chown admin:tty `echo $TTY`
admin% screen

```

### Configurar sudo mediante archivos complementarios en /etc/sudoers.d

*sudo* analiza los archivos contenidos en el directorio `/etc/sudoers.d/`. Esto significa que en lugar de editar `/etc/sudoers`, puede cambiar la configuración mediante archivos independientes y soltarlos en ese directorio. Esto tiene dos ventajas:

*   No hay necesidad de editar un archivo `sudoers.pacnew`;
*   Si hay un problema con una nueva entrada, puede eliminar el archivo afectado en lugar de editar `/etc/sudoers` (pero consulte la advertencia a continuación).

El formato para las entradas en estos archivos complementarios es el mismo que para `/etc/sudoers`. Para editarlos directamente, utilice `visudo -f /etc/sudoers.d/*nombre_archivo*`. Consulte la sección "Incluir otros archivos desde sudoers" de [sudoers(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudoers.5) para obtener más información.

Los archivos en el directorio `/etc/sudoers.d/` se analizan en orden lexicográfico, los nombres de archivo que contienen `.` o `~` se omiten. Para evitar problemas de clasificación, los nombres de los archivos deben comenzar con dos dígitos, por ejemplo `01_foo`.

**Nota:** El orden de las entradas en los archivos complementarios es importante: asegúrese de que las declaraciones no se anulan a sí mismas.

**Advertencia:** Los archivos en `/etc/sudoers.d/` son tan frágiles como el mismo `/etc/sudoers`: cualquier archivo incorrectamente formateado evitará el funcionamiento de `sudo`. Por lo tanto, por esta misma razón, se recomienda encarecidamente usar `visudo`

### Edición de archivos

`sudo -e` o `sudoedit` le permite editar un archivo como otro usuario mientras ejecuta el editor de texto como su usuario.

Esto es especialmente útil para editar archivos como superusuario sin elevar el privilegio de su editor de texto. Consulte [sudo(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sudo.8#e) para más detalles.

Tenga en cuenta que puede configurar el editor para cualquier programa, por lo que, por ejemplo, uno puede usar [meld](https://www.archlinux.org/packages/?name=meld) para administrar archivos [pacnew](/index.php/Pacman/Pacnew_and_Pacsave_(Espa%C3%B1ol) "Pacman/Pacnew and Pacsave (Español)"):

```
$ SUDO_EDITOR=meld sudo -e /etc/*file*{,.pacnew*}*

```

## Solución de problemas

### Problemas de TTY con SSH

SSH no asigna una tty de forma predeterminada cuando ejecuta un comando remoto. Sin una tty, sudo no puede desactivar *«echo»* cuando se solicita una contraseña. Puede utilizar la opción de ssh `-t` para forzar la asignación de una tty.

La opción `requiretty` de `Defaults` permite al usuario ejecutar sudo solo si tiene una tty.

```
# Desactive "ssh hostname sudo <cmd>", ya que mostrará la contraseña en texto claro. Se tiene que ejecutar "ssh -t hostname sudo <cmd>".
#
#Defaults    requiretty

```

### Umask permisiva

Sudo unirá el valor [umask](/index.php/Umask_(Espa%C3%B1ol) "Umask (Español)") del usuario con su propia umask (que por defecto es 0022). Esto evita que sudo cree archivos con permisos más abiertos que los que permite el umask del usuario. Si bien este es un valor predeterminado cuando no se usa umask personalizada, esto puede llevar a situaciones en las que una utilidad ejecutada por sudo puede crear archivos con permisos diferentes que si se ejecutara directamente desde el superusuario *(root)*. Si surgen errores a partir de esto, sudo proporciona un medio para reparar la umask, incluso si la umask deseada es más permisiva que la umask que el usuario ha especificado. Añadir esto (usando `visudo`) anulará el comportamiento predeterminado de sudo:

```
Defaults umask = 0022
Defaults umask_override

```

Esto establece el umask de sudo en umask predeterminado del superusuario (0022) y anula el comportamiento predefinido, utilizando siempre la umask indicada, independientemente de la umask definida del usuario.

### Estructura por defecto

La página de los autores tiene una [lista de todas las opciones](http://www.sudo.ws/sudo/sudoers.man.html#x5355444f455253204f5054494f4e53) que se puede usar con el comando `Defaults` en el archivo `/etc/sudoers`.

Consulte [[1]](https://gist.github.com/AladW/7eca9799b9ea624eca31) para obtener una lista de opciones (analizadas desde el código fuente de la versión 1.8.7) en un formato optimizado para `sudoers`.