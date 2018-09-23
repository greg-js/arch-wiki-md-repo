**Estado de la traducción:** este artículo es una versión traducida de [Users and groups](/index.php/Users_and_groups "Users and groups"). Fecha de la última traducción/revisión: **2018-09-05**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Users_and_groups&diff=0&oldid=533656).

Artículos relacionados

*   [DeveloperWiki:UID / GID Database](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database")
*   [Sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)")
*   [polkit](/index.php/Polkit "Polkit")
*   [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")

Los usuarios y grupos se utilizan en GNU/Linux para el [control de acceso](https://en.wikipedia.org/wiki/access_control#Computer_security y [PAM#Configuration How-Tos](/index.php/PAM#Configuration_How-Tos "PAM").

## Contents

*   [1 Descripción](#Descripci.C3.B3n)
*   [2 Permisos y propiedad](#Permisos_y_propiedad)
*   [3 Lista de archivos](#Lista_de_archivos)
*   [4 Administración de usuarios](#Administraci.C3.B3n_de_usuarios)
    *   [4.1 Ejemplo para añadir un usuario](#Ejemplo_para_a.C3.B1adir_un_usuario)
    *   [4.2 Ejemplo para añadir un usuario del sistema](#Ejemplo_para_a.C3.B1adir_un_usuario_del_sistema)
    *   [4.3 Cambio del nombre de inicio de sesión de un usuario o el directorio personal](#Cambio_del_nombre_de_inicio_de_sesi.C3.B3n_de_un_usuario_o_el_directorio_personal)
    *   [4.4 Otros ejemplos de administración de usuarios](#Otros_ejemplos_de_administraci.C3.B3n_de_usuarios)
*   [5 Base de datos del usuario](#Base_de_datos_del_usuario)
*   [6 Administración de grupos](#Administraci.C3.B3n_de_grupos)
*   [7 Listado de grupos](#Listado_de_grupos)
    *   [7.1 Grupos de usuarios](#Grupos_de_usuarios)
    *   [7.2 Grupos del sistema](#Grupos_del_sistema)
    *   [7.3 Grupos pre-systemd](#Grupos_pre-systemd)
    *   [7.4 Grupos no utilizados](#Grupos_no_utilizados)

## Descripción

	*El superusuario (root) redirige aquí. Para el directorio raíz, consulte [Partición raíz](/index.php/Partitioning_(Espa%C3%B1ol)#Partici.C3.B3n_ra.C3.ADz "Partitioning (Español)").*

Un *usuario* es cualquiera que use una computadora. En este caso, estamos describiendo los nombres que representan a esos usuarios. Puede ser Mary o Bill, y pueden usar los nombres Dragonlady o Pirate en lugar de su nombre real. Lo único que importa es que la computadora tenga un nombre para cada cuenta que cree, y es este nombre por el que una persona obtiene acceso para usar la computadora. Algunos servicios del sistema también se ejecutan utilizando cuentas de usuario restringidas o privilegiadas.

La administración de los usuarios se realiza con fines de seguridad al limitar el acceso de ciertas maneras específicas. El [superusuario](https://en.wikipedia.org/wiki/es:Root y [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") para la escalada de privilegios controlada.

Cualquier persona puede tener más de una cuenta, siempre que utilicen un nombre diferente para cada una de ellas. Además, hay algunos nombres reservados que no se pueden usar, como «root».

Los usuarios pueden agruparse en un «grupo» y, del mismo modo, pueden añadirse a un grupo existente para utilizar el acceso privilegiado que dicho grupo concede.

**Nota:** El usuario inexperto debe utilizar estas herramientas con cuidado y evitar modificar cualquier otra cuenta de *usuario* existente, que no sea la suya propia.

## Permisos y propiedad

De [En Unix todo es un archivo](http://ph7spot.com/musings/in-unix-everything-is-a-file):

	El sistema operativo UNIX cristaliza un par de ideas y conceptos unificadores que dieron forma a su diseño, interfaz de usuario, cultura y evolución. Uno de los más importantes probablemente sea el mantra: "todo es un archivo", considerado ampliamente como uno de los puntos definitorios de UNIX.

	Este principio de diseño fundamental consiste en proporcionar un paradigma unificado para acceder a una amplia gama de recursos de entrada/salida: documentos, directorios, discos duros, CD-ROM, módems, teclados, impresoras, monitores, terminales e incluso algunas comunicaciones entre procesos y redes. El truco es proporcionar una abstracción común para todos estos recursos, cada uno de los cuales los padres de UNIX llamaron «archivo». Como cada «archivo» está expuesto a través de la misma API, se puede utilizar el mismo conjunto de comandos básicos para leer/escribir en un disco, teclado, documento o dispositivo de red.

De [Extendiendo la abstracción de archivo de UNIX para fines generales de administración de redes](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.597.4699&rep=rep1&type=pdf):

	Una abstracción fundamental, muy potente y consistente, proporcionada en UNIX y los sistemas operativos compatibles es la abstracción de archivos. Muchos servicios del sistema operativo e interfaces de dispositivos se implementan para proporcionar una metáfora de archivo o sistema de archivos a las aplicaciones. Esto permite nuevos usos y aumenta en gran medida el poder de las aplicaciones existentes — herramientas simples diseñadas para usos específicos pueden, con las abstracciones de archivos de UNIX, utilizarse de maneras novedosas. Una herramienta simple, como cat, diseñada para leer uno o más archivos y enviar los contenidos a la salida estándar, se puede utilizar para leer desde dispositivos E/S *(entrada/salida)* a través de archivos de dispositivos especiales, que generalmente se encuentran en el directorio `/dev`. En muchos sistemas, la grabación y reproducción de audio se puede hacer simplemente con los comandos, «{`cat /dev/audio > miarchivo`» y «{`cat miarchivo > /dev/audio`», respectivamente.

Cada archivo en un sistema GNU/Linux es propiedad de un usuario y un grupo. Además, hay tres tipos de permisos de acceso: lectura, escritura y ejecución. Los permisos de acceso pueden aplicarse de forma diferente al usuario propietario del archivo, al grupo propietario y a otros (aquellos que no tienen la propiedad). Uno puede determinar los propietarios y permisos de un archivo al ver el formato de listado extenso del comando [ls](/index.php/Core_utilities_(Espa%C3%B1ol)#ls "Core utilities (Español)"):

 `$ ls -l /boot/` 
```
total 13740
drwxr-xr-x 2 root root    4096 Jan 12 00:33 grub
-rw-r--r-- 1 root root 8570335 Jan 12 00:33 initramfs-linux-fallback.img
-rw-r--r-- 1 root root 1821573 Jan 12 00:31 initramfs-linux.img
-rw-r--r-- 1 root root 1457315 Jan  8 08:19 System.map26
-rw-r--r-- 1 root root 2209920 Jan  8 08:19 vmlinuz-linux

```

La primera columna muestra los permisos del archivo (por ejemplo, el archivo `initramfs-linux.img` tiene los permisos `-rw-r--r--`). La tercera y cuarta columnas muestran los propietarios de usuario y grupo del archivo, respectivamente. En el presente ejemplo, todos los archivos son propiedad del usuario *root* y del grupo *root*.

 `$ ls -l /media/` 
```
total 16
drwxrwx--- 1 root vboxsf 16384 Jan 29 11:02 sf_Shared
```

En este ejemplo, la carpeta `sf_Shared` es propiedad del usuario *root* y del grupo *vboxsf*. También es posible determinar los propietarios y los permisos de un archivo con el comando stat:

El usuario propietario:

 `$ stat -c %U /media/sf_Shared/` 
```
root

```

El grupo propietario:

 `$ stat -c %G /media/sf_Shared/` 
```
vboxsf

```

Los permisos de acceso:

 `$ stat -c %A /media/sf_Shared/` 
```
drwxrwx---

```

Los permisos de acceso se muestran en tres grupos de caracteres, representando los permisos del usuario propietario, del grupo propietario, y de los otros, respectivamente. Por ejemplo, los caracteres `-rw-r--r--` indican que el usuario propietario del archivo tiene permisos de lectura y escritura, pero no de ejecución (`rw-`), mientras que los usuarios que pertenecen al grupo propietario y los demás usuarios solo tienen permiso de lectura (`r--` y `r--`). Mientras tanto, los caracteres `drwxrwx---` indican que el usuario propietario del archivo y todos los usuarios que pertenecen al grupo propietario tienen permisos de lectura, escritura y ejecución (`rwx` y `rwx`), mientras que los demás usuarios no pueden acceder (`---`). El primer carácter representa el tipo de archivo.

Puede listar los archivos que pertenecen a un usuario o a un grupo con la orden `find`:

```
# find / -group *grupo*

```

```
# find / -user *usuario*

```

El usuario y el grupo propietarios de un archivo pueden ser cambiados con el comando [chown](/index.php/Chown "Chown") (***ch**ange **own**er*). Los permisos de acceso a un archivo se pueden cambiar con el comando [chmod](/index.php/Chmod "Chmod") (***ch**ange **mod**e*).

Consulte [chown(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chown.1), [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1), y [Linux file permissions](http://www.linux.com/learn/tutorials/309527-understanding-linux-file-permissions) para obtener información adicional.

## Lista de archivos

**Advertencia:** No modifique estos archivos manualmente. Existen utilidades que bloquean el manejo de las propiedades y evitan invalidar el formato de la base de datos. Consulte [administración de usuarios](#Administraci.C3.B3n_de_usuarios) y [administración de grupos](#Administraci.C3.B3n_de_grupos) para más detalles.

| Archivo | Propósito |
| `/etc/shadow` | Información reservada de las cuentas de usuario |
| `/etc/passwd` | Información de las cuentas de usuario |
| `/etc/gshadow` | Contiene información reservada de los grupos de usuarios |
| `/etc/group` | Define los grupos a los que pertenecen los usuarios |
| `/etc/sudoers` | Lista de quién puede ejecutar qué por sudo |
| `/home/*` | Carpetas personales de los usuarios |

## Administración de usuarios

Para listar los usuarios que actualmente están conectados en el sistema, se puede usar el comando *who*. Para listar todas las cuentas de usuario existentes, incluidas sus propiedades almacenadas en la [base de datos del usuario](#Base_de_datos_del_usuario), ejecute `passwd -Sa` como superusuario. Consulte [passwd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/passwd.1) para la descripción del formato de salida.

Para añadir un nuevo usuario, utilice el ocmando *useradd*:

```
# useradd -m -g *grupo_inicial* -G *grupos_adicionales* -s *intérprete_de_comandos* *nombre_de_usuario*

```

	`-m`/`--create-home`

	crea el directorio del usuario como `/home/*usuario*`. Dentro de este directorio, un usuario que no es superusuario puede escribir archivos, eliminarlos, instalar programas, etc.

	`-g`/`--gid`

	define el nombre o número del grupo inicial del usuario. Si se especifica, el nombre del grupo debe existir; si se proporciona un número de grupo, debe referirse a un grupo ya existente. Si no se especifica, el comportamiento de *useradd* dependerá de la variable `USERGROUPS_ENAB` contenida en `/etc/login.defs`. El comportamiento predeterminado (`USERGROUPS_ENAB yes`) es crear un grupo con el mismo nombre que el usuario, con `GID` igual a `UID`.

	`-G`/`--groups`

	introduce una lista de grupos suplementarios de los que el usuario también es miembro. Cada grupo está separado del siguiente mediante una coma, sin espacios intermedios. Por defecto el usuario pertenece solo al grupo inicial.

	`-s`/`--shell`

	define la ruta y el nombre de archivo del intérprete de comandos de inicio de sesión predeterminado del usuario. Una vez que se completa el arranque, el intérprete de comandos de inicio de sesión predeterminado es el que se especifica aquí. Asegúrese de que el intérprete de comandos elegido esté instalado si es distinto a [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)").

**Advertencia:** Para poder iniciar sesión, el intérprete de comandos de inicio de sesión debe ser uno de los listados en `/etc/shells`; de lo contrario, el módulo [PAM](/index.php/PAM "PAM") `pam_shell` negará la solicitud de inicio de sesión. En particular, no use la ruta `/usr/bin/bash` en lugar de `/bin/bash`, a menos que esté configurada correctamente en `/etc/shells`.

**Nota:** La contraseña del usuario recién creado debe definirse después, utilizando *passwd* como se muestra en [#Ejemplo para añadir un usuario](#Ejemplo_para_a.C3.B1adir_un_usuario).

Cuando el intérprete de comandos de inicio de sesión no es funcional, por ejemplo, cuando la cuenta de usuario se crea para un servicio específico, se puede especificar `/usr/bin/nologin` en lugar de un intérprete de comandos normal para rechazar amablemente el inicio de sesión (Consulte [nologin(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nologin.8)).

### Ejemplo para añadir un usuario

Para añadir un nuevo usuario llamado `archie`, creando su directorio de inicio y usando todos los valores predeterminados en términos de grupos, nombres de carpetas, intérpretes de comandos utilizados y otros parámetros:

```
# useradd --create-home archie

```

**Sugerencia:** El valor predeterminado utilizado para el intérprete de comandos de inicio de sesión de la nueva cuenta se puede mostrar usando `useradd --default`. El valor predeterminado es Bash, se puede especificar un intérprete de comandos diferente con la opción `-s`/`--shell`.

Aunque no es necesario proteger al usuario `archie` recién creado con una contraseña, se recomienda encarecidamente hacerlo:

```
# passwd archie

```

El comando *useradd* anterior también creará automáticamente un grupo llamado `archie` con el mismo GID que el UID del usuario `archie` y lo convierte en el grupo predeterminado para `archie` al iniciar sesión. Hacer que cada usuario tenga su propio grupo (con nombre de grupo igual al nombre de usuario y GID igual al UID) es la forma de añadir usuarios preferida.

También puede hacer que el grupo predeterminado sea distinto usando la opción `-g`, pero tenga en cuenta que en sistemas multiusuario, no se recomienda utilizar un único grupo predeterminado (por ejemplo, `users`) para cada usuario. La razón es que, por lo general, el método para facilitar el acceso de escritura compartido para grupos específicos de usuarios establece el valor de usuario [umask](/index.php/Umask "Umask") en `002`, lo que significa que el grupo predeterminado siempre tendrá acceso de escritura a cualquier archivo que cree. Consulte también [User Private Groups](https://security.ias.edu/how-and-why-user-private-groups-unix). Si un usuario debe ser miembro de un grupo específico, especifique ese grupo como un grupo suplementario al crear el usuario.

En el escenario recomendado, donde el grupo predeterminado tiene el mismo nombre que el usuario, todos los archivos se pueden escribir de forma predeterminada solo por el usuario que los creó. Para permitir el acceso de escritura a un grupo específico, los archivos/carpetas compartidos se pueden escribir de forma predeterminada por todos en este grupo y, el grupo propietario, se puede fijar automáticamente al grupo dueño del directorio personal estableciendo el bit setgid en este directorio:

```
# chmod g+s *nuestro_directorio_compartido*

```

De lo contrario, se utiliza el grupo predeterminado del creador del archivo (generalmente el mismo que el nombre de usuario).

Si se requiere un cambio de GID temporalmente, también puede usar el comando *newgrp* para cambiar el GID predeterminado del usuario a otro GID en tiempo de ejecución. Por ejemplo, después de ejecutar `newgrp *nombre_de_grupo*` los archivos creados por el usuario se asociarán con el GID de `*nombre_de_grupo*`, sin necesidad de volver a iniciar sesión. Para volver al GID predeterminado, ejecute *newgrp* sin un nombre de grupo.

### Ejemplo para añadir un usuario del sistema

Los usuarios del sistema se pueden usar para ejecutar procesos/demonios bajo un usuario diferente, protegiendo (por ejemplo, con [chown](/index.php/Chown "Chown")) en archivos y/o directorios y más ejemplos de fortalecimiento informático.

Con el comando siguiente se crea un usuario del sistema sin acceso al intérprete de comandos y sin un directorio personal `home` (opcionalmente se añade el parámetro `-U` para crear un grupo con el mismo nombre que el usuario, y se añade el usuario a este grupo):

```
# useradd -r -s /usr/bin/nologin *usuario*

```

### Cambio del nombre de inicio de sesión de un usuario o el directorio personal

Para cambiar el directorio de inicio de un usuario:

```
# usermod -d /mi/nuevo/directorio/personal -m *usuario*

```

La opción `-m` también crea automáticamente el nuevo directorio y mueve el contenido allí.

**Sugerencia:** Puede crear un enlace desde el directorio personal anterior del usuario al nuevo. Al hacer esto, los programas podrán encontrar archivos que tengan rutas codificadas.
```
# ln -s /mi/nuevo/directorio/personal/ /mi/antiguo/directorio/personal

```

Asegúrese de que **no** haya `/` al final de `/mi/antiguo/directorio/personal`.

Para cambiar el nombre de inicio de sesión de un usuario:

```
# usermod -l *nombrenuevo* *nombreantiguo*

```

**Advertencia:** Asegúrese de no haber iniciado sesión como el usuario cuyo nombre va a cambiar. Abra un nuevo tty (`Ctrl+Alt+F1`) e inicie sesión como superusuario o como otro usuario y haga *su* como superusuario. El usermod debería evitar que hagas esto por error.

Cambiar un nombre de usuario es seguro y fácil cuando se hace correctamente, simplemente use el comando [usermod](#Otros_ejemplos_de_administraci.C3.B3n_de_usuarios). Si el usuario está asociado a un grupo con el mismo nombre, puede cambiarle el nombre con el comando [groupmod](#Administraci.C3.B3n_de_grupos).

Alternativamente, el archivo `/etc/passwd` puede modificarse directamente, consulte [#Base de datos del usuario](#Base_de_datos_del_usuario) para una introducción a su formato.

Tenga también en cuenta las siguientes notas:

*   Si está utilizando [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)"), asegúrese de actualizar `/etc/sudoers` para reflejar el nuevo nombre de usuario (a través del comando visudo como superusuario).
*   Los [crontabs](/index.php/Cron#Crontab_format "Cron") personales debe ajustarse al cambiar el nombre del archivo del usuario en `/var/spool/cron` del antiguo al nuevo nombre, y luego abrir `crontab -e` para cambiar las rutas relevantes y ajustar los permisos del archivo en consecuencia.
*   Los archivos/carpetas personales de [Wine](/index.php/Wine_(Espa%C3%B1ol) "Wine (Español)") contenidos en `~/.wine/drive_c/users`, `~/local/share/applications/wine/Programs` y posiblemente otros necesiten ser renombrados/modificados manualmente.
*   Es posible que sea necesario volver a instalar ciertos complementos de Thunderbird, como [Enigmail](https://www.enigmail.net/index.php/en/).
*   Cualquier cosa en su sistema (atajos de escritorio, scripts del intérprete de comandos, etc.) que use una ruta de acceso absoluta a su directorio personal (es decir, `/home/nombreantiguo`) deberá modificarse para reflejar su nuevo nombre. Para evitar estos problemas en los scripts del intérprete de comandos, use las variables `~` o `$HOME` para definir el directorios personal.
*   Además, no olvide modificar en consecuencia los archivos de configuración en `/etc` que dependan de su ruta absoluta (es decir, Samba, CUPS, etc.). Una buena forma de aprender qué archivos necesita actualizar implica usar el comando grep de esta manera: `grep -r {usuario_antiguo} *`

### Otros ejemplos de administración de usuarios

Para añadir un usuario a otros grupos utilice (`*grupos_adicionales*` es una lista separada por comas):

```
# usermod -aG *grupos_adicionales* *usuario*

```

**Advertencia:** Si la opción `-a` se omite en el comando *usermod* anterior, el usuario se elimina de todos los grupos que no figuran en `*grupos_adicionales*` (es decir, el usuario solo será miembro de los grupos que figuran en `*grupos_adicionales*`).

Alternativamente, puede usarse *gpasswd*. Aunque el nombre de usuario solo se puede añadir (o eliminar) de un grupo a la vez:

```
# gpasswd --add *usuario* *grupo*

```

Para introducir información del usuario como comentarios en [GECOS](#Base_de_datos_del_usuario) (por ejemplo, el nombre de usuario completo), escriba:

```
# chfn *usuario*

```

(De esta forma *chfn* se ejecuta en modo interactivo).

Alternativamente, el comentario de GECOS se puede establecer de forma más liberal con:

```
# usermod -c "Comentario" *usuario*

```

Para marcar la contraseña de un usuario como caducada y solicitarles que creen una nueva la primera vez que inician sesión, escriba:

```
# chage -d 0 *usuario*

```

Las cuentas de usuario se pueden eliminar con el comando *userdel*:

```
# userdel -r *usuario*

```

La opción `-r` especifica que el directorio de inicio y la cola de mensajes del usuario también deben eliminarse.

Para cambiar el intérprete de comandos de inicio de sesión del usuario:

```
# usermod -s */bin/bash* *usuario*

```

**Sugerencia:** El script [adduser](https://aur.archlinux.org/packages/adduser/) permite realizar los trabajos de *useradd*, *chfn* y *passwd* de forma interactiva. Consulte también [FS#32893](https://bugs.archlinux.org/task/32893).

## Base de datos del usuario

La información del usuario local se almacena en el archivo de texto sin formato `/etc/passwd`: cada una de sus líneas representa una cuenta de usuario y tiene siete campos delimitados por dos puntos.

```
*cuenta:contraseña:UID:GID:GECOS:directorio:intérprete_de_comandos*

```

Donde:

*   `*cuenta*` es el nombre de usuario. Este campo no puede estar vacío. Se aplican las reglas de nomenclatura estándar de *NIX.
*   `*contraseña*` es la contraseña del usuario
    **Advertencia:** El archivo `passwd` es legible para todo el mundo, por lo que almacenar las contraseñas (con hash o sin él) en este archivo es inseguro. En cambio, Arch Linux utiliza [contraseñas ocultas (shadowed)](/index.php/Security#Password_hashes "Security"): el campo `contraseña` contendrá un carácter de marcador de posición (`x`) que indica que la contraseña hash se guarda en el archivo de acceso restringido `/etc/shadow`. Por esta razón, se recomienda cambiar siempre las contraseñas usando el comando **passwd**.

*   `*UID*` es la identificación numérica del usuario. En Arch, el primer nombre de inicio de sesión (después del superusuario) es UID 1000 de forma predeterminada; las entradas subsecuentes de UID para los usuarios deberían ser mayores a 1000.
*   `*GID*` es la identificación numérica del grupo principal para el usuario. Los valores numéricos para los GID se enumeran en [/etc/group](#Administraci.C3.B3n_de_grupos).
*   `*GECOS*` es un campo opcional utilizado con fines informativos; generalmente contiene el nombre de usuario completo, pero también puede ser utilizado por servicios como *finger* y se puede administrar con el comando [chfn](#Otros_ejemplos_de_administraci.C3.B3n_de_usuarios). Este campo es opcional y puede dejarse en blanco.
*   `*directorio*` es utilizado por el comando de inicio de sesión para establecer la variable de entorno `$HOME`. Varios servicios con sus propios usuarios usan `/`, pero los usuarios normales generalmente establecen una carpeta bajo `/home`.
*   `*intérprete_de_comandos*` es la ruta al [intérprete de comandos](/index.php/Command_shell "Command shell") predeterminado del usuario. Este campo es opcional y su valor predeterminado es `/bin/bash`.

Ejemplo:

```
jack:x:1001:100:Jack Smith,algún comentario va aquí,,:/home/jack:/bin/bash

```

Desglosado, esto significa: usuario `jack`, cuya contraseña está en `/etc/shadow`, cuyo UID es 1001 y cuyo grupo principal es 100\. Jack Smith es su nombre completo y existe un comentario asociado a su cuenta; su directorio personal es `/home/jack` y está usando [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)").

El comando *pwck* se puede usar para verificar la integridad de la base de datos del usuario. Puede ordenar la lista de usuarios por GID al mismo tiempo, lo que puede ser útil para comparar:

```
# pwck -s

```

**Nota:** En Arch Linux los valores predeterminados de los archivos se crean como archivos *.pacnew* mediante nuevas versiones del paquete [filesystem](https://www.archlinux.org/packages/?name=filesystem). A menos que Pacman genere mensajes relacionados para la acción, estos archivos *.pacnew* pueden, y deberían, ser descartados/eliminados. Los nuevos usuarios y grupos predeterminados necesarios se añaden o se vuelven a añadir según sea necesario por [systemd-sysusers(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sysusers.8).

## Administración de grupos

`/etc/group` es el archivo que define los grupos en el sistema (consulte [group(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/group.5) para más detalles).

El comando `groups` muestra la pertenencia al grupo:

```
$ groups *usuario*

```

Si se omite `usuario`, se muestran los grupos a los que pertenece el usuario actual.

El ocmando `id` proporciona detalles adicionales, tales como el UID del usuario y los GID asociados:

```
$ id *usuario*

```

Para listar todos los grupos en el sistema:

```
$ cat /etc/group

```

Cree un nuevo grupo con el comando `groupadd`:

```
# groupadd *grupo*

```

Añada un usuario a un grupo con el ocmando `gpasswd`:

```
# gpasswd -a *usuario* *grupo*

```

Modifique un grupo existente con `groupmod`; por ejemplo, para renombrar el grupo `grupo_antiguo` a `grupo_nuevo` mientras se conserva el gid (todos los archivos que anteriormente eran de `grupo_antiguo` serán propiedad de `grupo_nuevo`):

```
# groupmod -n *grupo_nuevo* *grupo_antiguo*

```

**Nota:** Esto cambiará el nombre del grupo pero no el GID numérico del mismo.

Puede eliminar un grupo existente:

```
# groupdel *grupo*

```

Puede eliminar un usuario de un grupo:

```
# gpasswd -d *usuario* *grupo*

```

Si el usuario está actualmente conectado, debe cerrar la sesión y volver a entrar para que el cambio surta efecto.

El comando *grpck* se puede utilizar para comprobar la integridad de los archivos de grupo del sistema.

Las actualizaciones del paquete [filesystem](https://www.archlinux.org/packages/?name=filesystem) crean archivos *.pacnew*. Al igual que los archivos *.pacnew* para la [#Base de datos del usuario](#Base_de_datos_del_usuario), estos pueden descartarse/eliminarse, porque la secuencia de comandos de instalación añade cualquier grupo nuevo requerido.

## Listado de grupos

Esta sección explica el propósito de los grupos esenciales del paquete [core/filesystem](https://git.archlinux.org/svntogit/packages.git/tree/trunk/group?h=packages/filesystem). Hay muchos otros grupos, que se crearán con el [GID correcto](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database") cuando se instale el paquete correspondiente. Consulte la página principal del software para más detalles.

**Nota:** La eliminación posterior de un paquete no elimina el usuario/grupo creado automáticamente (UID/GID) de nuevo. Esto es intencionado porque cualquier archivo creado durante su uso se dejaría huérfano con el posible riesgo de seguridad.

### Grupos de usuarios

A menudo, los usuarios que no son superusuarios de la computadora deben añadirse a algunos de los siguientes grupos para permitir el acceso a los periféricos y facilitar la administración del sistema:

| Grupo | Archivos afectados | Propósito |
| adm | Grupo de administración, similar a `wheel`. |
| ftp | `/srv/ftp/` | Acceso a archivos servidos por servidores [FTP](https://en.wikipedia.org/wiki/es:Protocolo_de_transferencia_de_archivos "wikipedia:es:Protocolo de transferencia de archivos"). |
| games | `/var/games` | Acceso a algunas aplicaciones de juegos. |
| http | `/srv/http/` | Acceso a archivos servidos por servidores [HTTP](https://en.wikipedia.org/wiki/es:Protocolo_de_transferencia_de_hipertexto "wikipedia:es:Protocolo de transferencia de hipertexto"). |
| log | Acceso a archivos de registro en `/var/log/` creados por [syslog-ng](/index.php/Syslog-ng "Syslog-ng"). |
| rfkill | `/dev/rfkill` | Derecho a controlar el estado de energía de los dispositivos inalámbricos (utilizado por *rfkill*). |
| sys | Derecho a administrar impresoras en [CUPS](/index.php/CUPS_(Espa%C3%B1ol) "CUPS (Español)"). |
| systemd-journal | `/var/log/journal/*` | Se utiliza para proporcionar acceso de solo lectura a los registros systemd, como una alternativa a `adm` y `wheel` [[1]](https://cgit.freedesktop.org/systemd/systemd/tree/README?id=fdbbf0eeda929451e2aaf34937a72f03a225e315#n190). De lo contrario, solo se muestran los mensajes generados por el usuario. |
| users | Grupo de usuarios estándar. |
| uucp | `/dev/ttyS[0-9]+`, `/dev/tts/[0-9]+`, `/dev/ttyUSB[0-9]+`, `/dev/ttyACM[0-9]+`, `/dev/rfcomm[0-9]+` | Acceso a los puertos serie RS-232 y dispositivos conectados a ellos. |
| wheel | Grupo de administración, comúnmente utilizado para dar acceso a las utilidades [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") y [su](/index.php/Su_(Espa%C3%B1ol) "Su (Español)") (ninguno lo usa por defecto, configurable en `/etc/pam.d/su` y `/etc/pam.d/su-l`). También se puede utilizar para obtener acceso completo de lectura a los archivos de [registro](/index.php/Systemd_(Espa%C3%B1ol)#Journal "Systemd (Español)"). |

### Grupos del sistema

Los siguientes grupos se utilizan para fines del sistema, solo es necesario su asignación a los usuarios para fines específicos:

| Grupo | Archivos afectados | Propósito |
| dbus | Utilizado internamente por [dbus](https://www.archlinux.org/packages/?name=dbus) |
| kmem | `/dev/port`, `/dev/mem`, `/dev/kmem` |
| locate | `/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate` | Consulte [Core utilities (Español)#locate](/index.php/Core_utilities_(Espa%C3%B1ol)#locate "Core utilities (Español)"). |
| lp | `/dev/lp[0-9]*`, `/dev/parport[0-9]*` | Acceso a dispositivos de puerto paralelo (impresoras y otros). |
| mail | `/usr/bin/mail` |
| nobody | Grupo sin privilegios. |
| proc | `/proc/*pid*/` | Un grupo autorizado para aprender información de procesos que de lo contrario está prohibida por la opción de montaje `hidepid=` del [sistema de archivos de proc](https://www.kernel.org/doc/Documentation/filesystems/proc.txt). El grupo debe establecerse explícitamente con la opción de montaje `gid=`. |
| root | `/*` | Administración y control completo del sistema (root, admin). |
| smmsp | Grupo [sendmail](/index.php/Sendmail "Sendmail"). |
| tty | `/dev/tty`, `/dev/vcc`, `/dev/vc`, `/dev/ptmx` |
| utmp | `/run/utmp`, `/var/log/btmp`, `/var/log/wtmp` |

### Grupos pre-systemd

Antes de que Arch migrase a [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), los usuarios tenían que añadirse manualmente a estos grupos para poder acceder a los dispositivos correspondientes. Esta metodología está obsoleta en favor de [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") marcando los dispositivos con `uaccess` [tag](https://github.com/systemd/systemd/blob/master/src/login/70-uaccess.rules) y *logind* asignando los permisos a los usuarios dinámicamente a través de [ACLs](/index.php/Access_Control_Lists_(Espa%C3%B1ol) "Access Control Lists (Español)") según la sesión que esté actualmente activa. Tenga en cuenta que la sesión no debe interrumpirse para que esto funcione (consulte [Permisos de sesión](/index.php/General_troubleshooting_(Espa%C3%B1ol)#Permisos_de_sesi.C3.B3n "General troubleshooting (Español)") para comprobarlo).

Hay algunas excepciones notables que requieren añadir un usuario a algunos de estos grupos: por ejemplo, si desea permitir que los usuarios accedan al dispositivo incluso cuando no están conectados. Sin embargo, tenga en cuenta que añadir usuarios a los grupos puede incluso causar la rotura de alguna funcionalidad (por ejemplo, el grupo `audio` romperá el cambio rápido de usuario y permite que las aplicaciones bloqueen el mezclador por software).

| Grupo | Archivos afectados | Propósito |
| audio | `/dev/audio`, `/dev/snd/*`, `/dev/rtc0` | Acceso directo a hardware de sonido para todas las sesiones. Todavía es necesario hacer que [ALSA](/index.php/Advanced_Linux_Sound_Architecture_(Espa%C3%B1ol) "Advanced Linux Sound Architecture (Español)") y [OSS](/index.php/Open_Sound_System_(Espa%C3%B1ol) "Open Sound System (Español)") funcionen en sesiones remotas, consulte [ALSA#User privileges](/index.php/ALSA#User_privileges "ALSA"). También utilizado por [JACK](/index.php/JACK "JACK") para dar a los usuarios permisos de procesamiento en tiempo real. |
| disk | `/dev/sd[a-z][1-9]` | Acceso a dispositivos de bloques no afectados por otros grupos como `optical`, `floppy`, y `storage`. |
| floppy | `/dev/fd[0-9]` | Acceso a unidades de disquete. |
| input | `/dev/input/event[0-9]*`, `/dev/input/mouse[0-9]*` | Acceso a dispositivos de entrada. Introducido en systemd 215 [[2]](http://lists.freedesktop.org/archives/systemd-commits/2014-June/006343.html). |
| kvm | `/dev/kvm` | Acceso a máquinas virtuales usando [KVM](/index.php/KVM "KVM"). |
| optical | `/dev/sr[0-9]`, `/dev/sg[0-9]` | Acceso a dispositivos ópticos como unidades de CD y DVD. |
| scanner | `/var/lock/sane` | Acceso al hardware del escáner. |
| storage | Acceso a unidades extraíbles como discos duros USB, unidades flash, reproductores de MP3; permite al usuario montar dispositivos de almacenamiento. |
| video | `/dev/fb/0`, `/dev/misc/agpgart` | Acceso a dispositivos de captura de vídeo, aceleración por hardware 2D/3D, framebuffer (se puede utilizar [X](/index.php/X "X") *sin* pertenecer a este grupo). |

### Grupos no utilizados

Los siguientes grupos no tienen actualmente ninguna propósito:

| Grupo | Archivos afectados | Propósito |
| bin | ninguno | Histórico |
| daemon |
| lock | Usado para el acceso de bloqueo de archivos. Requerido por ejemplo en [gnokii](https://www.archlinux.org/packages/?name=gnokii). |
| mem |
| network | No utilizado por defecto. Puede ser utilizado, por ejemplo para otorgar acceso a NetworkManager (consulte [Configurar permisos PolicyKit](/index.php/NetworkManager_(Espa%C3%B1ol)#Configurar_permisos_PolicyKit "NetworkManager (Español)")). |
| power |
| uuidd |