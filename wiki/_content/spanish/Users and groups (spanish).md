Artículos relacionados

*   [DeveloperWiki:UID / GID Database](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database")
*   [polkit](/index.php/Polkit "Polkit")
*   [chmod](/index.php/Chmod "Chmod")
*   [Change username (Español)](/index.php/Change_username_(Espa%C3%B1ol) "Change username (Español)")

Los usuarios y los grupos son usados ​​en los sistemas GNU/Linux para el [control de los accesos](https://en.wikipedia.org/wiki/access_control#Computer_security "wikipedia:access control") —es decir, determina qué usuarios y servicios están autorizados para acceder a los archivos, directorios y dispositivos periféricos presentes en el sistema—. Linux ofrece de forma predefinida mecanismos de control de acceso relativamente simples/básicos. Para obtener opciones más avanzadas, consulte [ACL](/index.php/Lista_de_Control_de_Acceso "Lista de Control de Acceso") y [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication").

## Contents

*   [1 Descripción](#Descripci.C3.B3n)
*   [2 Permisos y propiedad](#Permisos_y_propiedad)
*   [3 Lista de archivos](#Lista_de_archivos)
*   [4 Gestión de usuarios](#Gesti.C3.B3n_de_usuarios)
    *   [4.1 Base de datos del usuario](#Base_de_datos_del_usuario)
*   [5 Gestión de grupos](#Gesti.C3.B3n_de_grupos)
*   [6 Lista de grupos](#Lista_de_grupos)
    *   [6.1 Grupos para los usuarios](#Grupos_para_los_usuarios)
    *   [6.2 Grupos del sistema](#Grupos_del_sistema)
    *   [6.3 Grupos para el software](#Grupos_para_el_software)
    *   [6.4 Grupos en desuso o desatendidos](#Grupos_en_desuso_o_desatendidos)

## Descripción

Un *usuario* es cualquier persona que usa un ordenador. En este caso, estamos describiendo los nombres que representan a dichos usuarios. Esos nombres pueden ser María o Bill, y pueden ser tambien Dragonlady o Pirata en lugar de sus nombres reales. Lo único que importa es que el equipo tenga un nombre para cada cuenta, y es con este nombre a través del cual una persona adquiere los permisos para usar el sistema. No obstante, algunos servicios del sistema se ejecutan utilizando cuentas de usuario restringidas o privilegiadas.

La gestión de usuarios se realiza con el propósito de dar seguridad al sistema, limitando el acceso de ciertas maneras específicas.

Cualquier persona puede tener más de una cuenta, siempre y cuando se utilice un nombre diferente para cada cuenta que cree. Además, hay algunos nombres reservados, que no pueden ser utilizados, como «root».

Los usuarios pueden ser congregados en un «grupo», y, del mismo modo, pueden optar por unirse a un grupo ya existente para utilizar los privilegios de acceso que dicho grupo concede.

**Nota:** El usuario inexperto debe utilizar estas herramientas con cuidado y evitar modificar cualquier otra cuenta de *usuario* existente, que no sea la suya propia.

## Permisos y propiedad

De la página [In UNIX Everything is a File (*«En Unix Todo es un Archivo»*)](http://ph7spot.com/musings/in-unix-everything-is-a-file):

	*El sistema operativo UNIX es el resultado de algunas ideas y conceptos unificadores que dieron forma a su diseño, la interfaz de usuario, la cultura y la evolución. Uno de los más importantes es probablemente el lema: «everything is a file» (*todo es un archivo)*, considerado como uno de los puntos definitorios de UNIX.*

	*Este principio fundamental de diseño consiste en proporcionar un paradigma unificado para acceder a una amplia gama de recursos de entrada/salida: documentos, directorios, discos duros, CD-ROM, módems, teclados, impresoras, monitores, terminales e, incluso, algunas comunicaciones de procesos internos y de red. El truco consiste en proporcionar una abstracción común para todos estos recursos, para cada uno de los cuales, los padres de UNIX, llamaron «archivo». Debido a que cada «archivo» se expone a través de la misma API, se puede utilizar el mismo conjunto de órdernes básicas para leer/escribir en un disco, un teclado, un documento o un dispositivo de red.*

Del archivo [Extending UNIX File Abstraction for General-Purpose Networking (*«Extender la abstracción de archivo de UNIX para fines generales de gestión de la red»*)](http://www.intel-research.net/Publications/Pittsburgh/101220041324_277.pdf):

	*Una abstracción fundamental, potente y consistente, proporcionada en UNIX y sistemas operativos compatibles, es la abstracción de archivo. Muchos servicios del sistema operativo e interfaces de dispositivos se implementan para proporcionar una metáfora del archivo o del sistema de archivos para las aplicaciones. Esto permite usos nuevos, y aumenta, en gran medida, el poder de las aplicaciones existentes —herramientas sencillas diseñadas para usos específicos pueden, con las abstracciones de archivos de UNIX, utilizarse de otras formas novedosas—. Una herramienta simple, como cat, diseñada para leer uno o más archivos y mostrar los contenidos en la salida estándar, se puede utilizar para leer la salida/entrada de dispositivos mediante los archivos de dispositivos especiales, que, por lo general, se encuentran en el directorio `/dev`. En muchos sistemas, la grabación de audio y la reproducción, se pueden hacer simplemente con las órdenes, «`cat /dev/audio > miarchivo`» y «`cat miarchivo > /dev/audio`», respectivamente.*

Cada archivo en un sistema GNU/Linux es propiedad de un usuario y de un grupo. Además, hay tres tipos de permisos de acceso: lectura, escritura y ejecución. Los permisos de acceso pueden aplicarse de forma diferente al usuario propietario de un archivo, al grupo propietario, y o otros (los que no tienen propiedad). Se pueden visualizar los propietarios y los permisos de un archivo utilizando el formato «long listing» (*listado largo*) de la orden `ls`:

 `$ ls -l /boot/` 
```
total 13740
drwxr-xr-x 2 root root    4096 Jan 12 00:33 grub
-rw-r--r-- 1 root root 8570335 Jan 12 00:33 initramfs-linux-fallback.img
-rw-r--r-- 1 root root 1821573 Jan 12 00:31 initramfs-linux.img
-rw-r--r-- 1 root root 1457315 Jan  8 08:19 System.map26
-rw-r--r-- 1 root root 2209920 Jan  8 08:19 vmlinuz-linux
```

La primera columna muestra los permisos del archivo (por ejemplo, el archivo `initramfs-linux.img` tiene los permisos `-rw-r--r--`). La tercera y cuarta columnas muestran al usuario y al grupo propietarios del archivo, respectivamente. En el presente ejemplo, todos los archivos son propiedad del usuario *root* y del grupo *root*.

 `$ ls -l /media/` 
```
total 16
drwxrwx--- 1 root vboxsf 16384 Jan 29 11:02 sf_Shared
```

En este ejemplo, la carpeta `sf_Shared` es propiedad del usuario *root* y del grupo *vboxsf* . También es posible determinar los propietarios y los permisos de un archivo con la orden `stat`:

El usuario propietario:

 `$ stat -c %U /media/sf_Shared/`  `root` 

El grupo propietario:

 `$ stat -c %G /media/sf_Shared/`  `vboxsf` 

Los permisos de acceso:

 `$ stat -c %A /media/sf_Shared/`  `drwxrwx---` 

Los permisos de acceso se muestran en tres grupos de caracteres, representando los permisos del usuario propietario, del grupo propietario, y de los otros, respectivamente. Por ejemplo, los caracteres `-rw-r--r--` indican que el usuario propietario del archivo tiene permisos de lectura y escritura, pero no de ejecución (`rw-`), mientras que los usuarios que pertenecen al grupo propietario y los demás usuarios solo tienen permiso de lectura (`r--` y `r--`). Mientras tanto, los caracteres `drwxrwx---` indican que el usuario propietario del archivo y todos los usuarios que pertenecen al grupo propietario tienen permisos de lectura, escritura y ejecución (`rwx` y `rwx`), mientras que los demás usuarios no pueden acceder (`---`). El primer carácter representa el tipo de archivo.

Puede listar los archivos que pertenecen a un usuario o a un grupo con la orden `find`:

```
# find / -group [grupo]

```

```
# find / -user [usuario]

```

El usuario y el grupo propietarios de un archivo pueden ser cambiados con la orden `chown` (*«change owner»*). Los permisos de acceso a un archivo se pueden cambiar con la orden `chmod` (*«change mode»*).

Véase [chown(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/chown.1), [chmod(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1), y [Linux file permissions](http://www.tuxfiles.org/linuxhelp/filepermissions.html) para obtener información adicional.

## Lista de archivos

**Advertencia:** No modifique estos archivos manualmente. Existen utilidades que bloquean el manejo de las propiedades y evitan invalidar el formato de la base de datos. Véase [#Gestión de usuarios](#Gesti.C3.B3n_de_usuarios) y [#Gestión de grupos](#Gesti.C3.B3n_de_grupos) para más detalles.

| Archivo | Contenido |
| `/etc/shadow` | Información reservada de las cuentas de usuario |
| `/etc/passwd` | Información de las cuentas de usuario |
| `/etc/gshadow` | Contiene información reservada de los grupos de usuarios |
| `/etc/group` | Define a que grupos pertenecen los usuarios |
| `/etc/sudoers` | Lista lo que se puede ejecutar con sudo |
| `/home/*` | Carpeta personal del usuario |

## Gestión de usuarios

Para visualizar una lista de los usuarios actualmente conectados al sistema, se puede usar la orden `who`.

Para agregar un nuevo usuario, utilice la orden `useradd`:

```
# useradd -m -g [grupo_principal] -G [grupos_adicionales] -s [shell_de_ingreso] [nombre_de_usuario]

```

*   **`-m`** crea el directorio home del usuario con la ruta `/home/[nombre de usuario]`, dentro de su directorio de usuario, de modo que un usuario normal puede escribir archivos, borrarlos, instalar programas, etc.
*   **`-g`** define el nombre o el número del grupo principal del inicio de sesión del usuario; el nombre del grupo debe existir; si un número de grupo se proporciona, se debe hacer referencia a un grupo ya existente; si no se especifica, el comportamiento de useradd dependerá de la variable del entorno USERGROUPS_ENAB definida en `/etc/login.defs`.
*   **`-G`** introduce una lista de grupos suplementarios de los que el usuario será miembro: cada grupo estará separado del siguiente por una coma, sin espacios en blanco; el valor predeterminado es que el usuario solo pertenece al grupo principal.
*   **`-s`** define la ruta y el nombre de la shell predeterminada de inicio de sesión del usuario; después de que el proceso de arranque se ha completado, la shell de inicio de sesión predeterminada será lanzada; compruebe que el paquete de la shell elegida, si es distinta de Bash, se ha instalado.

**Advertencia:** La shell de acceso debería ser una de las que figuran en `/etc/shells`. Para los programas que utilizan PAM, esto se comprueba por el módulo `pam_shells`.

He aquí un ejemplo típico de sistema de escritorio, añadiendo un usuario llamado *archie* y especificando *bash* como la shell de inicio de sesión:

```
# useradd -m -g users -G wheel -s /bin/bash archie

```

Para añadir más adelante al usuario a otros grupos utilice:

```
# usermod -aG [grupos_adicionales] [nombredeusuario]

```

Alternativamente, se puede utilizar gpasswd. Aunque el nombre de usuario solo se puede añadir a (o eliminar de) un grupo cada vez.

```
# gpasswd --add [nombredeusuario] [grupo]

```

**Advertencia:** Si se omite la opción `-a` el usuario será quitado de todos los grupos no mencionados en `[additional_groups]` (es decir, el usuario será miembro únicamente de los grupos listados en `[additional_groups]`).

Para introducir la información del usuario para el campo *GECOS* (por ejemplo, el nombre completo del usuario), escriba:

```
# chfn [nombredeusuario]

```

(De esta manera `chfn` se ejecuta en modo interactivo).

Para especificar la contraseña del usuario, escriba:

```
# passwd [nombredeusuario]

```

Para marcar una contraseña de usuaria como expirada, requiriéndole que cree una nueva contraseña la primera vez que inicie sesión, escriba

```
# chage -d 0 [nombredeusuario]

```

Las cuentas de usuario se pueden eliminar con la orden `userdel`.

```
# userdel -r [nombredeusuario]

```

La opción `-r` especifica que el directorio del usuario y su contenido también deben suprimirse.

### Base de datos del usuario

La información del usuario local se guarda en el archivo `/etc/passwd`. Para obtener una lista de todas las cuentas de usuarios existentes en el sistema, escriba:

```
$ cat /etc/passwd

```

Habrá una línea por cada cuenta, y cada una tendrá el siguiente formato:

```
account:password:UID:GID:GECOS:directory:shell

```

donde:

*   `account` es el nombre del usuario
*   `password` es la contraseña del usuario
*   `UID` es el ID numérico del usuario
*   `GID` es el ID numérico del grupo principal del usuario
*   `GECOS` es un campo opcional que contiene información adicional del usuario; por lo general, contiene el nombre completo del usuario
*   `directory` es la carpeta `$HOME` del usuario
*   `shell` es el intérprete de órdenes utilizado por el usuario (por defecto es `/bin/sh`)

**Nota:** Arch Linux utiliza contraseñas *shadowed*. El archivo `passwd` es legible por todos los usuarios, de modo que guardar las contraseñas (sean cifradas o no) en este archivo es inseguro. Por ello, el campo `password` contendrá un carácter de posición (`x`) que indica que la contraseña cifrada se guarde en el archivo de acceso restringido `/etc/shadow`.

## Gestión de grupos

En el archivo `/etc/group` se definen los grupos presentes en el sistema (ejecute la orden [group(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/group.5) para conocer más detalle).

La orden `groups` muestra la pertenencia al grupo:

```
$ groups [usuario]

```

Si la variable `usuario` se omite, se muestran los grupos a los cuales pertenece el usuario actual.

La orden `id` proporciona detalles adicionales, como la UID del usuario y los GID asociados:

```
$ id [usuario]

```

Puede listar todos los grupos presentes en el sistema, ejecutando:

```
$ cat /etc/group

```

Puede crear un nuevo grupo con la orden `groupadd`:

```
# groupadd [grupo]

```

Puede agregar un usuario a un grupo con la orden `gpasswd`:

```
# gpasswd -a [usuario] [grupo]

```

Puede eliminar un grupo existente, ejecutando:

```
# groupdel [grupo]

```

Puede eliminar un usuario de un grupo, ejecutando:

```
# gpasswd -d [usuario] [grupo]

```

Si el usuario estaba conectado a la sesión cuando ha ejecutado la orden, debe reiniciar la sesión para que los cambios surtan efecto.

## Lista de grupos

### Grupos para los usuarios

**Nota:** La pertenencia a estos grupos no es necesaria para obtener permisos en el escritorio estándar para acceder al sonido, gráficas 3D, impresión, montaje, etc., siempre y cuando el período de sesiones de logind no se rompa (véase [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") para comprobarlo).

Los usuarios de estaciones de trabajo/escritorios suelen añadir su propio usuario normal (no root) a algunos de los grupos siguientes para permitir el acceso a los periféricos y a otros equipos, y facilitar así la administración del sistema:

| Grupo | Archivos afectados | Propósito |
| camera | Permite el acceso a [Digital Cameras](/index.php/Digital_Cameras "Digital Cameras"). |
| floppy | `/dev/fd[0-9]` | Permite el acceso a unidades floppy. |
| games | `/var/games` | Permite el acceso a algún software de juego. |
| locate | `/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate` | Faculta para hacer uso de la orden [updatedb](https://en.wikipedia.org/wiki/updatedb "wikipedia:updatedb"). |
| networkmanager | Requisito necesario para que el usuario pueda conectarse de forma inalámbrica con [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)"). Este grupo no se incluye con Arch de forma predefinida, por lo que se debe agregar manualmente. |
| rfkill | `/dev/rfkill` | Permite controlar el estado de energía del dispositivo móvil (utilizado por [rfkill](https://www.archlinux.org/packages/?name=rfkill)). |
| users | Grupo de usuarios estándar. |
| uucp | `/dev/ttyS[0-9]`, `/dev/tts/[0-9]` | Permite el acceso a dispositivos de serie y USB tales como módems, handhelds, puertos de la serie RS-232. |
| wheel | Grupo de administración, utilizado normalmente para dar acceso a las órdenes `sudo` y `su` (no habilitado por defecto). |

### Grupos del sistema

Los grupos siguientes se utilizan para los fines del sistema y no son apropiados de ser utilizados por un usuario inexperto en Arch:

**Nota:** Algunos de estos grupos solían ser necesarios antes de que Arch migrara a systemd. Actualmente no es el caso. Véase [esta sección](/index.php/Systemd_(Espa%C3%B1ol)#Informaci.C3.B3n_complementariasection_for_systemd "Systemd (Español)") para más información.

| Grupo | Archivos afectados | Propósito |
| audio | `/dev/audio`, `/dev/snd/*`, `/dev/rtc0` | Permite el acceso directo al hardware de sonido, para todas las sesiones (requisito necesario, por tanto, para [ALSA](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)") y [OSS](/index.php/OSS_(Espa%C3%B1ol) "OSS (Español)")). Las sesiones locales tienen ya la capacidad de poner en marcha los controles del sonido y del acceso al mezclador. |
| avahi |
| bin | none | Histórico |
| clamav | `/var/lib/clamav/*`, `/var/log/clamav/*` | Utilizado por [Clam AntiVirus](/index.php/Clam_AntiVirus "Clam AntiVirus"). |
| daemon |
| dbus | `/var/run/dbus/*` |
| disk | `/dev/sda[1-9]`, `/dev/sdb[1-9]` | Permite el acceso a dispositivos de bloque que no se ven afectados por otros grupos como `optical`, `floppy`, y `storage`. |
| ftp | `/srv/ftp` | Usado por servidores [FTP](https://en.wikipedia.org/wiki/FTP "wikipedia:FTP") como [Proftpd](/index.php/Proftpd "Proftpd") |
| fuse | Usado por fuse para permitir apoyo al usuario. |
| gdm | Directorio de autorización del servidor (ServAuthDir) | Grupo [GDM](/index.php/GDM "GDM"). |
| http |
| kmem | `/dev/port`, `/dev/mem`, `/dev/kmem` |
| log | `/var/log/*` | Permite el acceso a los archivos de registro en `/var/log`. |
| lp | `/etc/cups`, `/var/log/cups`, `/var/cache/cups`, `/var/spool/cups`, `/dev/parport[0-9]` | Permite el acceso al hardware de la impresora; le permite al usuario gestionar los trabajos de impresión. |
| mail | `/usr/bin/mail` |
| mem |
| mpd | `/var/lib/mpd/*`, `/var/log/mpd/*`, `/var/run/mpd/*`, opcionalmente directorios de música | Grupo [MPD](/index.php/MPD "MPD"). |
| network | Permite cambiar la configuración de la red, como cuando se utiliza [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)"). |
| nobody | Grupo sin privilegios |
| ntp | `/var/lib/ntp/*` | Grupo [NTPd](/index.php/Network_Time_Protocol_daemon_(Espa%C3%B1ol) "Network Time Protocol daemon (Español)"). |
| optical | `/dev/sr[0-9]`, `/dev/sg[0-9]` | Permite el acceso a los dispositivos ópticos como unidades de CD y DVD. |
| policykit | Grupo [PolicyKit](/index.php/PolicyKit "PolicyKit"). |
| power | Faculta para hacer uso de [Pm-utils](/index.php/Pm-utils "Pm-utils") (suspensión, hibernación...) y de los controles de la admnistración de la energía. |
| root | `/*` | Control y administración completos del sistema (root, admin). |
| scanner | `/var/lock/sane` | Permite el acceso al hardware del escáner |
| smmsp | Grupo [sendmail](https://en.wikipedia.org/wiki/sendmail "wikipedia:sendmail"). |
| storage | Permite el acceso a unidades extraíbles, como discos duros USB, unidades flash/jump, reproductores de MP3; permite al usuario montar dispositivos de almacenamiento. |
| systemd-journal | `/var/log/journal/*` | Proporciona acceso a los registros completos de systemd. En su defecto, solo se muestran los mensajes generados por los usuarios. |
| vboxsf | Carpetas compartidad de máquinas virtuales | Usado por [VirtualBox](/index.php/VirtualBox "VirtualBox"). |
| video | `/dev/fb/0`, `/dev/misc/agpgart` | Permite el acceso a los dispositivos de captura de video, aceleración de hardware 2D/3D, framebuffer (el servidor [X](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") se puede utilizar *sin* pertenecer a este grupo). Las sesiones locales ya tienen la capacidad de utilizar la aceleración de hardware y de captura de vídeo. |

### Grupos para el software

Estos grupos permiten a sus miembros utilizar un software específico:

| Grupo | Archivos afectados | Propósito |
| adbusers | Archivos de los dispositivos en `/dev/` | Faculta el acceso al Debugging Bridge de [Android](/index.php/Android "Android"). |
| cdemu | `/dev/vhba_ctl` | Faculta el uso de la emulación de disco de [CDemu](/index.php/CDemu "CDemu"). |
| thinkpad | `/dev/misc/nvram` | Utilizado por los usuarios de ThinkPad para acceder a herramientas como [tpb](/index.php/Tpb "Tpb"). |
| vboxusers | `/dev/vboxdrv` | Faculta para utilizar el software VirtualBox. |
| vmware | Faculta para utilizar el software [VMware](/index.php/VMware "VMware"). |
| ssh | [Sshd](/index.php/Sshd "Sshd") se puede configurar para que solo permita a los miembros de este grupo iniciar sesión. |
| wireshark | Faculta para capturar paquetes con [Wireshark](/index.php/Wireshark "Wireshark"). |

### Grupos en desuso o desatendidos

Los siguientes grupos no tienen actualmente ninguna utilidad:

| Grupo | Propósito |
| stb-admin | **¡En desuso!** Faculta para controlar [system-tools-backends](http://system-tools-backends.freedesktop.org/) |
| kvm | Añadía un usuario al grupo `kvm`, lo que solía ser necesario para permitir a los usuarios normales (no root) acceder a máquinas virtuales usando [KVM](/index.php/KVM "KVM"). Este ha caído en desuso en favor de las reglas [udev](/index.php/Udev "Udev"), las cuales hacen lo anterior automáticamente. |