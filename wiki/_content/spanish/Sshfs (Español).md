Puedes usar **sshfs** para montar un sistema remoto (accesible mediante [SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)")) en un directorio local, de forma que podrás hacer cualquier operación sobre los archivos montados, con cualquier herramienta (copiar, renombrar, editar, etc.). En general, se recomienda el uso de sshfs en lugar de shfs, ya que no se ha publicado una nueva versión de shfs desde 2004.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Montar](#Montar)
    *   [1.2 Desmontar](#Desmontar)
*   [2 Chroot](#Chroot)
*   [3 Asistentes](#Asistentes)
*   [4 Automontaje](#Automontaje)
    *   [4.1 Bajo demanda](#Bajo_demanda)
    *   [4.2 Al arrancar](#Al_arrancar)
    *   [4.3 Acceso seguro de usuario](#Acceso_seguro_de_usuario)
*   [5 Opciones](#Opciones)
*   [6 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [6.1 Lista de comprobación](#Lista_de_comprobaci.C3.B3n)
    *   [6.2 Conexión reiniciada por par (_connection reset by peer_)](#Conexi.C3.B3n_reiniciada_por_par_.28connection_reset_by_peer.29)
    *   [6.3 Servidor remoto se ha desconectado](#Servidor_remoto_se_ha_desconectado)
    *   [6.4 Thunar tiene problemas con FAM y el acceso a archivos remotos](#Thunar_tiene_problemas_con_FAM_y_el_acceso_a_archivos_remotos)
    *   [6.5 El apagado se interrumpe cuando sshfs está montado](#El_apagado_se_interrumpe_cuando_sshfs_est.C3.A1_montado)
*   [7 Ver también](#Ver_tambi.C3.A9n)

## Instalación

[Instala](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [sshfs](https://www.archlinux.org/packages/?name=sshfs) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

### Montar

Antes de intentar montar un directorio, asegúrate de que los permisos del directorio donde lo deseas montar permiten del acceso correcto del usuario. Para montar un directorio remoto ejecuta `sshfs`:

```
$ sshfs _USUARIO@HOSTNAME_O_IP:/RUTA_REMOTA PUNTO_DE_MONTAJE_LOCAL OPCIONES_DE_SSH_

```

Por ejemplo:

```
$ sshfs sessy@mycomputer:/foo/bar /mnt/bar -C -p 9876

```

Donde `9876` es el número de puerto del servicio ssh en el servidor `mycomputer`.

**Nota:** Los usuarios pueden definir un puerto no estándar para un servidor en `~/.ssh/config`, para evitar añadir la opción `-p` cada vez. Para más información ver [este apartado](/index.php/Secure_Shell_(Espa%C3%B1ol)#Guardar_los_datos_de_conexi.C3.B3n_en_la_configuraci.C3.B3n_de_SSH "Secure Shell (Español)").

SSH te pedirá la contraseña, si es necesario. Si no quieres tener que introducir la contraseña cada vez, es recomendable usar [claves SSH](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)").

**Sugerencia:** Para montar rápidamente un directorio remoto, hacer alguna operación sobre archivos y desmontarlo, utiliza un _script_ como este:

```
sshfs _USUARIO@HOSTNAME_O_IP:/RUTA_REMOTA PUNTO_DE_MONTAJE_LOCAL OPCIONES_DE_SSH_
mc ~ PUNTO_DE_MONTAJE_LOCAL
fusermount -u PUNTO_DE_MONTAJE_LOCAL

```

Esto montará el directorio remoto, ejecutará MC, y lo desmontará cuando cierres MC.

### Desmontar

Para desmontar el sistema remoto:

```
$ fusermount -u _PUNTO_DE_MONTAJE_LOCAL_

```

Ejemplo:

```
$ fusermount -u /mnt/sessy

```

## Chroot

Quizá quieras restringir a un usuario a un directorio en concreto (y sus subdirectorios). Para hacer esto, edita `/etc/ssh/sshd_config`:

 `/etc/ssh/sshd_config` 

```
.....
Match User usuario 
       ChrootDirectory /chroot/%u
       ForceCommand internal-sftp #para obligar al usuario a usar solo sftp
       AllowTcpForwarding no
       X11Forwarding no
.....
```

**Nota:** El directorio de `chroot` **debe** ser propiedad del usuario `root`. Si no, no serás capaz de conectar. Para más información, busca `Match, ChrootDirectory` y `ForceCommand` en las páginas del manual.

## Asistentes

Si necesitas montar sistemas de archivos con sshfs frecuentemente, puede interesarte usar un asistente de sshfs, como [sftpman](/index.php/Sftpman "Sftpman"). Este proporciona una línea de órdenes y una interfaz GTK para hacer que el montaje y desmontaje se puede hacer con un solo click.

## Automontaje

El automontaje se puede hacer al arrancar, o bajo demanda (cuando se acceda al directorio). En ambos casos, hay que modificar la configuración en `/etc/[fstab](/index.php/Fstab "Fstab")`.

**Nota:** Ten presente que el automontaje se hace a través del usuario root, por lo que no puedes usar la información configurada en el `.ssh/config` de un usuario normal.

Para permitir que root use la clave SSH de un usuario normal, especifica su ruta completa con la opción `IdentityFile`.

**Y lo más importante**, monta manualmente, como root, al menos una vez cada sistema de archivos sshfs, para que la firma del servidor se añada al archivo `.ssh/known_hosts`.

### Bajo demanda

Con `systemd` es posible configurar el montaje bajo demanda en `/etc/fstab`.

Ejemplo:

```
usuario@servidor:/directorio/remoto /punto/de/montaje  fuse.sshfs noauto,x-systemd.automount,_netdev,users,idmap=user,IdentityFile=/home/usuario/.ssh/id_rsa,allow_other,reconnect 0 0

```

Las opciones de montaje importantes son _noauto,x-systemd.automount,_netdev_.

*   _noauto_ indica que no se monte al arrancar
*   _x-systemd.automount_ indica que se monte bajo demanda
*   __netdev_ indica que es un dispositivo de red, no un dispositivo de bloques (sin esta opción podrían aparecer errores de tipo "Dispositivo no encontrado")

### Al arrancar

Un ejemplo de como usar sshfs para montar un sistema de archivos remoto mediante `/etc/[fstab](/index.php/Fstab "Fstab")`:

```
USUARIO@HOSTNAME_O_IP:/DIRECTORIO/REMOTO  /PUNTO/DE/MONTAJE/LOCAL  fuse.sshfs  defaults,_netdev  0  0

```

Por ejemplo, esta línea en _fstab_:

```
llib@192.168.1.200:/home/llib/FAH  /media/FAH2  fuse.sshfs  defaults,_netdev  0  0

```

Esto funcionará automáticamente si estás usando un clave SSH para el usuario. Ver [claves SSH](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)").

Si quieres usar sshfs con varios usuarios:

```
usuario@dominio.org:/home/usuario  /media/usuario   fuse.sshfs    defaults,allow_other,_netdev    0  0

```

De nuevo, es importante establecer la opción de montaje __netdev_ para asegurarse de que la red está disponible antes de intentar el montaje.

### Acceso seguro de usuario

Cuando se hace el automontaje desde `/etc/[fstab](/index.php/Fstab "Fstab")`, normalmente el sistema de archivos se montará como root. Por defecto, esto tiene resultados indeseables si deseas acceder como usuario normal y limitar el acceso a otros usuarios.

Un ejemplo de configuración:

```
USUARIO@HOSTNAME_O_IP:/DIRECTORIO/REMOTO  /PUNTO/DE/MONTAJE/LOCAL  fuse.sshfs noauto,x-systemd.automount,_netdev,user,idmap=usuario,transform_symlinks,identityfile=/home/USUARIO/.ssh/id_rsa,allow_other,default_permissions,uid=USER_ID_N,gid=USER_GID_N 0 0

```

Resumen de opciones relevantes:

*   _allow_other_ - Permite que usuarios distintos a root accedan al directorio.
*   _default_permissions_ - Permite que el kernel establezca los permisos (es decir, que se usen los permisos del sistema remoto). Esto permite prohibir el acceso a todos excepto si se añade _allow_other_.
*   _uid_, _gid_ - establece la propiedad de los archivos a estos valores; _uid_ es la identificación numérica de tu usuario, _gid_ es la identificación numérica del grupo.

## Opciones

sshfs puede convertir automáticamente las IDs de tus usuarios local y remoto.

Añade la opción_idmap_ con el valor _user_ para convertir el UID del usuario que se conecta:

```
# sshfs -o idmap=user sessy@mycomputer:/home/sessy /mnt/sessy -C -p 9876

```

Esto asignará el UID del usuario remoto "sessy" al usuario local, que ejecuta este proces ("root" en el ejemplo anterior) y el GID permanece sin cambios. Si necesitas un control más preciso en la conversión de UID y GID, mira las opciones _idmap=file_, _uidfile_ y _gidfile_.

## Solución de problemas

### Lista de comprobación

Lee [este párrafo](/index.php/Secure_Shell_(Espa%C3%B1ol)#Lista_de_comprobaci.C3.B3n "Secure Shell (Español)") primero. Otras cosas a comprobar son:

1\. ¿Estás recibiendo información adicional del archivo `/etc/issue` del servidor? Esto podría confundir a SSHFS. Deberías desactivar temporalmente el archivo `/etc/issue`:

```
$ mv /etc/issue /etc/issue.orig

```

2\. Ten en cuenta que la mayoría de artículos sobre resolución de problemas relacionados con SSH que encontrarás en la red no están relacionados con Systemd. Es frecuente que las configuraciones de `/etc/fstab` comiencen erróneamente con `_sshfs#_usuario@host:/mnt/servidor/directorio ... fuse ...` en lugar de usar la sintaxis `usaurio@host:/mnt/servidor/directorio ... fuse._sshfs_ ... _x-systemd_, ...`.

3\. Comprueba que el propietario del directorio de origen en el servidor y sus contenidos es el usuario del servidor.

```
$ chown -R USER_S: /mnt/servers/folder

```

4\. El ID del usuario del servidor puede ser diferente del ID del usuario del cliente. Obviamente, ambos nombres de usuario deben ser iguales. Solo tienes que preocuparte por el ID del usuario del cliente. SSHFS convertirá este UID con las siguientes opciones de montaje:

```
uid=_USER_C_ID_,gid=_GROUP_C_ID_

```

5\. Comprueba que el punto de montaje del cliente (directorio) es propiedad del usuario del cliente. Este directorio debería tener la misma ID de usuario que se define en las opciones de montaje de SSHFS.

```
$ chown -R USER_C: /mnt/client/folder

```

6\. Comprueba que el punto de montaje del cliente (directorio) está vacío. Por defecto, no puedes montar sistemas de archivos SSHFS en directorios no vacíos.

7\. Si quieres automontar sistemas de archivos SSHFS usando identificación mediante clave pública (sin contraseña) mediante `/etc/fstab`, puedes usar esta línea como ejemplo:

```
_USER_S_@_SERVER_:/mnt/on/server      /nmt/on/client        fuse.sshfs      x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/_USER_C_/.ssh/id_rsa,allow_other,default_permissions,uid=_USER_C_ID_,gid=_GROUP_C_ID_,umask=0   0 0

```

Considera como ejemplo la siguiente configuración:

SERVER = Server host name (serv) USER_S = Server user name (pete) USER_C = Client user name (pete) USER_S_ID = Server user ID (1004) USER_C_ID = Client user ID (1000) GROUP_C_ID = Client user's group ID (100)

puedes obtener el UID y GID del usuario del cliente con

```
$ id USERNAME

```

esta es la línea que habría que incluir en `/etc/fstab`:

```
pete@serv:/mnt/on/server      /nmt/on/client        fuse.sshfs      x-systemd.automount,_netdev,user,idmap=user,transform_symlinks,identityfile=/home/pete/.ssh/id_rsa,allow_other,default_permissions,uid=1004,gid=1000,umask=0   0 0

```

8\. Si conoces otro problema a tener en cuenta en esta lista, por favor, añádelo.

### Conexión reiniciada por par (_connection reset by peer_)

*   Si estás intentando acceder al sistema remoto con un nombre de host, intenta utilizar la dirección IP en su lugar, ya que puede ser un problema de resolución de nombres de dominio. Asegúrate de editar `/etc/hosts` con los detalles del servidor.
*   Si estás usando nombres de clave no estándar y las estás indicando como `-i .ssh/mi_clave`, esto no funcionará. Tienes que usar `-o IdentityFile=/home/user/.ssh/mi_clave`, con la ruta completa de la clave.
*   Añadir la opción '`sshfs_debug`' (p.ej. '`sshfs -o sshfs_debug user@server ...`') puede ayudarte a resolver el problema.
*   Si estás intentando usar sshfs a través de un router que usa DD-WRT o similar, hay una solución [aquí](http://www.dd-wrt.com/wiki/index.php/SFTP_with_DD-WRT). Observa que la opción -osftp_server=/opt/libexec/sftp-server se puede usar con el comando sshfs command en lugar de parchear dropbear)
*   Viejo hilo del foro: [sshfs: Connection reset by peer](https://bbs.archlinux.org/viewtopic.php?id=27613)
*   Asegúrate de que el usuario puede iniciar sesión en el servidor (especialmente cuando se use AllowUsers).

**Nota:** Cuando uses más de una opción para sshfs, debes separarlas por comas. P.ej: '`sshfs -o sshfs_debug,IdentityFile=</path/to/key> user@server ...`')

### Servidor remoto se ha desconectado

Si recibes este mensaje justo después de intentar usar _sshfs_:

*   Primero asegúrate de que la máquina **remota** tiene _sftp_ instalado. Si no, no funcionará.

**Sugerencia:** Si tu servidor remoto está usando OpenWRT: `opkg install openssh-sftp-server` será suficiente

*   Después, intenta comprobar la ruta del `Subsystem` listado en `/etc/ssh/sshd_config` en la máquina remota para ver si es válida. PUedes comprobar la ruta con `find / -name sftp-server`.

Para Arch Linux el valor por defecto en `/etc/ssh/sshd_config` es `Subsystem sftp /usr/lib/ssh/sftp-server`.

### Thunar tiene problemas con FAM y el acceso a archivos remotos

Si las carpetas remotas no se muestran, y en su lugar se muestra tu directorio home, o si tienes otros problemas para acceder a archivos remotos mediante Thunar, reemplaza _fam_ por [gamin](https://www.archlinux.org/packages/?name=gamin). _Gamin_ procede de _fam_.

### El apagado se interrumpe cuando sshfs está montado

Systemd puede interrumpirse durante el apagado si se montó manualmente un sistema de archivos sshfs y no se desmontó antes de apagar. Para solucionar este problema, crea este archivo (como root):

 `/etc/systemd/system/killsshfs.service` 

```
[Unit]
After=network.target

[Service]
RemainAfterExit=yes
ExecStart=-/bin/true
ExecStop=-/usr/bin/pkill sshfs

[Install]
WantedBy=multi-user.target

```

Para activar el servicio: `systemctl enable killsshfs.service`

## Ver también

*   [sftpman](/index.php/Sftpman "Sftpman") - herramienta asistente de sshfs
*   [SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)")
*   [Como montar sistemas de archivos SSH en una jaula](http://wiki.gilug.org/index.php/How_to_mount_SFTP_accesses), con especial atención en los usuarios y permisos.