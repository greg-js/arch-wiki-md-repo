**Estado de la traducción**
Este artículo es una traducción de [SSHFS](/index.php/SSHFS "SSHFS"), revisada por última vez el **2019-03-01**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=SSHFS&diff=0&oldid=566372) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [SCP and SFTP](/index.php/SCP_and_SFTP "SCP and SFTP")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")
*   [Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")
*   [sftpman](/index.php/Sftpman "Sftpman")

[SSHFS](https://github.com/libfuse/sshfs) es un cliente de sistema de archivos basado en FUSE para montar directorios remotos a través de una conexión [Secure Shell](/index.php/Secure_Shell "Secure Shell").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Montaje](#Montaje)
    *   [1.2 Desmontaje](#Desmontaje)
*   [2 Opciones](#Opciones)
*   [3 Haciendo Chroot](#Haciendo_Chroot)
*   [4 Montaje automático](#Montaje_automático)
    *   [4.1 Bajo demanda](#Bajo_demanda)
    *   [4.2 En el arranque](#En_el_arranque)
    *   [4.3 Acceso de usuario seguro](#Acceso_de_usuario_seguro)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 Lista de comprobación](#Lista_de_comprobación)
    *   [5.2 Connection reset by peer](#Connection_reset_by_peer)
    *   [5.3 El host remoto se ha desconectado](#El_host_remoto_se_ha_desconectado)
    *   [5.4 Problemas de montaje fstab](#Problemas_de_montaje_fstab)
*   [6 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [sshfs](https://www.archlinux.org/packages/?name=sshfs).

**Sugerencia:**

*   Si a menudo necesita montar sistemas de archivos sshfs, puede estar interesado en utilizar un ayudante sshfs, como [qsshfs](https://aur.archlinux.org/packages/qsshfs/), [sftpman](/index.php/Sftpman "Sftpman"), [sshmnt](https://aur.archlinux.org/packages/sshmnt/) o [fmount.py](https://github.com/lahwaacz/Scripts/blob/master/fmount.py).
*   Es posible que desee utilizar [Google Authenticator](/index.php/Google_Authenticator_(Espa%C3%B1ol) "Google Authenticator (Español)") para proporcionar seguridad adicional como es la autenticación de dos pasos.
*   [SSH keys](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)") puede ser utilizado sobre la autenticación tradicional de contraseña.

### Montaje

Para poder montar un directorio, el usuario de SSH necesita poder acceder a él. Invoque *sshfs* para montar un directorio remoto:

```
$ sshfs *[usuario@]host:[dir] puntodemontaje [opciones]*

```

Por ejemplo:

```
$ sshfs miusuario@micomputadora:/ruta/remota /ruta/local -C -p 9876

```

Aquí `-p 9876` especifica el número de puerto y `-C` activa la compresión. Para más opciones véase la sección [#Opciones](#Opciones).

Cuando no se especifica, la ruta remota se establece de manera predeterminada en el directorio de inicio del usuario remoto. Los nombres de usuario y las opciones predeterminadas se pueden predefinir para cada computadora en `~/.ssh/config` para simplificar el uso de *sshfs*. Para obtener más información, véase [OpenSSH#Client usage](/index.php/OpenSSH#Client_usage "OpenSSH").

SSH le pedirá la contraseña, si es necesario. Si no desea escribir la contraseña varias veces al día, véase [SSH keys](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)").

### Desmontaje

Para desmontar el sistema remoto:

```
$ fusermount3 -u *puntodemontaje*

```

Por ejemplo:

```
$ fusermount3 -u /ruta/local

```

## Opciones

*sshfs' puede convertir automáticamente entre ID de usuarios locales y remotos. Utilice la opción `idmap=user` para traducir el UID del usuario que se conecta al usuario remoto `miusuario` (GID permanece sin cambios):*

```
$ sshfs miusuario@micomputadora:/ruta/remota /ruta/local -o idmap=user

```

Si necesita más control sobre la traducción de UID y GID, mire las opciones `idmap=file`, `uidfile` y `gidfile`.

Se puede encontrar una lista completa de opciones en [sshfs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshfs.1).

## Haciendo Chroot

Es posible que desee restringir un usuario específico a un directorio específico en el sistema remoto. Esto se puede hacer editando `/etc/ssh/sshd_config`:

 `/etc/ssh/sshd_config` 
```
.....
Match User *algúnusuario* 
       ChrootDirectory */chroot/%u*
       ForceCommand internal-sftp
       AllowTcpForwarding no
       X11Forwarding no
.....

```

**Nota:** El directorio chroot **debe** ser propiedad del superusuario *(root)*, de lo contrario no podrá conectarse.

Véase también [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot"). Para más información revise la página del manual [sshd_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshd_config.5) para `Match`, `ChrootDirectory` y `ForceCommand`.

## Montaje automático

El montaje automático puede ocurrir en el arranque o bajo demanda (al acceder al directorio). Para ambos, la configuración ocurre en [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)").

**Nota:** Tenga en cuenta que el montaje automático se realiza a través del superusuario, por lo tanto, no puede utilizar anfitriones *(hosts)* configurados en `.ssh/config` de su usuario normal.

Para permitir que el superusuario utilice una clave SSH de un usuario normal, especifique su ruta completa en la opción `IdentityFile`.

**Y más importante**, utilice manualmente cada montaje sshfs al menos una vez **cuando sea superusuario** para que la firma del anfitrión se añada al archivo `/root/.ssh/known_hosts`.

### Bajo demanda

Con systemd es posible el montaje bajo demanda utilizando entradas `/etc/fstab`.

Por ejemplo:

```
usuario@host:/carpeta/remota /punto/montaje  fuse.sshfs noauto,x-systemd.automount,_netdev,users,idmap=user,IdentityFile=/home/usuario/.ssh/id_rsa,allow_other,reconnect 0 0

```

Las opciones de montaje importantes aquí son *noauto,x-systemd.automount,_netdev*.

*   *noauto* le dice que no se monte en el arranque
*   *x-systemd.automount* hace la magia bajo demanda
*   *_netdev* le dice que es un dispositivo de red, no un dispositivo de bloque (sin él pueden ocurrir errores del tipo "No existe dicho dispositivo")

**Nota:** Despues de editar `/etc/fstab`, (re)inicie el servicio requerido: `systemctl daemon-reload && systemctl restart <objetivo>` donde `<objetivo>` se puede encontrar ejecutando `systemctl list-unit-files --type automount`

**Sugerencia:** [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) no requiere editar `/etc/fstab` para añadir un nuevo punto de montaje. En cambio, los usuarios normales pueden crear uno simplemente intentando acceder a él (por ejemplo, con algo como `ls ~/mnt/ssh/[usuario@]yourremotehost[:puerto]`). [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) utiliza AutoFS. Los usuarios deben estar activados para utilizarlo con `autosshfs-user`.

### En el arranque

Un ejemplo de cómo utilizar sshfs para montar un sistema de archivos remoto a través de `/etc/fstab`

```
USUARIO@NOMBREHOST_O_IP:/DIRECTORIO/REMOTO  /PUNTOMONTAJE/LOCAL  fuse.sshfs  defaults,_netdev  0  0

```

Tomemos, por ejemplo, la línea *fstab*

```
llib@192.168.1.200:/home/llib/FAH  /media/FAH2  fuse.sshfs  defaults,_netdev  0  0

```

Lo anterior funcionará automáticamente si está utilizando una clave SSH para el usuario. Véase [Uso de claves SSH](/index.php/Using_SSH_Keys "Using SSH Keys").

Si quiere utilizar sshfs con múltiples usuarios:

```
usuario@dominio.org:/home/usuario  /media/usuario   fuse.sshfs    defaults,allow_other,_netdev    0  0

```

Una vez más, es importante configurar la opción de montaje *_netdev* para asegurarse de que la red esté disponible antes de intentar montar.

### Acceso de usuario seguro

Al realizar el montaje automático a través de [fstab](/index.php/Fstab_(Espa%C3%B1ol) "Fstab (Español)"), el sistema de archivos generalmente será montado por el superusuario. De forma predeterminada, esto produce resultados indeseables si desea acceder como un usuario normal y limitar el acceso a otros usuarios.

Un ejemplo de configuración del punto de montaje:

```
USUARIO@NOMBREHOST_O_IP:/DIRECTORIO/REMOTO  /PUNTOMONTAJE/LOCAL  fuse.sshfs noauto,x-systemd.automount,_netdev,user,idmap=user,follow_symlinks,identityfile=/home/USUARIO/.ssh/id_rsa,allow_other,default_permissions,uid=N_ID_USUARIO,gid=N_GID_USUARIO 0 0

```

Resumen de las opciones relevantes:

*   *allow_other* - Permite que otros usuarios que no sean el montador (es decir, el superusuario) accedan al recurso compartido.
*   *default_permissions* - Permite que el kernel verifique los permisos, es decir, utilice los permisos reales en el sistema de archivos remoto. Esto permite prohibir el acceso a todas las personas que de otra forma concede *allow_other*.
*   *uid*, *gid* - establece la propiedad de archivos reportada a unos valores determinados; *uid* es el ID numérico de su usuario, *gid* es el ID numérico del grupo de su usuario.

## Solución de problemas

### Lista de comprobación

Lea primero [OpenSSH (Español)#Lista de comprobación](/index.php/OpenSSH_(Espa%C3%B1ol)#Lista_de_comprobación "OpenSSH (Español)"). Otros temas para verificar son:

1\. ¿Su inicio de sesión SSH está enviando información adicional desde, por ejemplo, el archivo `/etc/issue` del servidor? Esto podría confundir SSHFS. Debería desactivar temporalmente el archivo `/etc/issue` del servidor:

```
$ mv /etc/issue /etc/issue.orig

```

2\. Tenga en cuenta que la mayoría de los artículos de solución de problemas relacionados con SSH que encontrará en la web no están relacionados con Systemd. A menudo las definiciones en `/etc/fstab` comienzan erroneamente con `*sshfs#*user@host:/mnt/servidores/carpeta ... fuse ...` en lugar de utilizar la sintaxis `user@host:/mnt/servidores/carpeta ... fuse.*sshfs* ... *x-systemd*, ...`.

3\. Compruebe que el propietario de la carpeta de origen y el contenido del servidor es propiedad del usuario del servidor.

```
$ chown -R USER_S: /mnt/servidores/carpeta

```

4\. El ID de usuario del servidor puede ser diferente del cliente. Obviamente ambos nombres de usuario tienen que ser los mismos. Solo tiene que cuidar los ID de usuario del cliente. SSHFS traducirá el UID con las siguientes opciones de montaje:

```
uid=*ID_USUARIO_C*,gid=*ID_GRUPO_C*

```

5\. Compruebe que el punto de montaje de destino del cliente (carpeta) es propiedad del usuario cliente. Esta carpeta debe tener el mismo ID de usuario definido en las opciones de montaje de SSHFS.

```
$ chown -R USUARIO_C: /mnt/cliente/carpeta

```

6\. Compruebe que el punto de montaje (carpeta) del cliente esté vacío. De forma predeterminada no puede montar carpetas SSHFS en carpetas no vacías.

### Connection reset by peer

*   Si está intentando acceder al sistema remoto con un nombre de host, intente utilizar su dirección IP, ya que puede ser un problema de resolución de nombres de dominio. Asegúrese de editar `/etc/hosts` con los detalles del servidor.
*   Si está utilizando nombres de clave no predeterminados y los está pasando como `-i .ssh/my_key`, no funcionará. Tiene que utilizar `-o IdentityFile=/home/user/.ssh/my_key`, con la ruta completa a la clave.
*   Si su `/root/.ssh/config` es un enlace simbólico, recibirá este error también. Véase [este tema en serverfault](http://serverfault.com/questions/507748/bad-owner-or-permissions-on-root-ssh-config)
*   Añadiendo la opción '`sshfs_debug`' (como en '`sshfs -o sshfs_debug user@server ...`') puede ayudar a resolver el problema.
*   Si eso no revela nada útil, también puede intentar añadir la opción '`debug`'
*   Si está intentando hacer sshfs a través de un enrutador que utiliza DD-WRT o similar, hay una solución [aquí](http://www.dd-wrt.com/wiki/index.php/SFTP_with_DD-WRT). (tenga en cuenta que la opción -osftp_server=/opt/libexec/sftp-server se puede utilizar para la orden sshfs en lugar de parchear dropbear)
*   Si ve esto solo durante el arranque, puede ser que systemd esté intentando montar antes de que haya una conexión de red disponible. Habilite el servicio de 'espera-en-línea' apropiado para su conexión de red (por ejemplo, systemd-networkd-wait-online.service) para solucionar esto.
*   Hilo antiguo del foro: [sshfs: Connection reset by peer](https://bbs.archlinux.org/viewtopic.php?id=27613)
*   Asegúrese de que su usuario pueda iniciar sesión en el servidor (especialmente al utilizar AllowUsers)
*   Asegúrese de que `Subsystem sftp /usr/lib/ssh/sftp-server` está activado en `/etc/ssh/sshd_config`.

**Nota:** Cuando se proporciona más de una opción para sshfs, deben estar separadas por comas. Al igual que: '`sshfs -o sshfs_debug,IdentityFile=</ruta/a/la/clave> usuario@servidor ...`')

### El host remoto se ha desconectado

Si recibe este mensaje directamente después de intentar utilizar *sshfs*:

*   Primero asegúrese de que la máquina **remota** tiene instalado *sftp*. No funcionará si no lo tiene.
*   Después, comprueba que la ruta de `Subsystem sftp` en `/etc/ssh/sshd_config` en la máquina remota es válida.

### Problemas de montaje fstab

Para obtener una salida de depuración detallada, añada lo siguiente a las opciones de montaje:

```
ssh_command=ssh\040-vv,sshfs_debug,debug

```

**Nota:** Aquí, `\040` representa un espacio que fstab utiliza para separar campos.

Para poder ejecutar `mount -av` y ver la salida de depuración, elimine lo siguiente:

```
 noauto,x-systemd.automount

```

## Véase también

*   [Cómo montar el sistema de archivos SSH en chroot](http://wiki.gilug.org/index.php/How_to_mount_SFTP_accesses), Con especial cuidado con las preguntas de propietarios y permisos.