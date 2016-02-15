Cambiar el nombre de usuario en Arch (o en cualquier distribución de Linux) es seguro y fácil cuando se hace correctamente. También puede cambiar el nombre del grupo asociado para el usuario si lo desea. Siguiendo el procedimiento siguiente hará precisamente esto conservando su UID/GID para el usuario afectado sin alterar los permisos de los archivos que haya configurado.

## Contents

*   [1 Procedimiento](#Procedimiento)
    *   [1.1 Cambiar el nombre del inicio de sesión del usuario](#Cambiar_el_nombre_del_inicio_de_sesi.C3.B3n_del_usuario)
    *   [1.2 Cambiar el nombre del usuario](#Cambiar_el_nombre_del_usuario)
    *   [1.3 Cambiar $HOME del usuario](#Cambiar_.24HOME_del_usuario)
    *   [1.4 Cambiar $HOME del usuario y mover su contenido](#Cambiar_.24HOME_del_usuario_y_mover_su_contenido)
    *   [1.5 Cambiar el nombre del grupo](#Cambiar_el_nombre_del_grupo)
    *   [1.6 Manualmente con /etc/passwd](#Manualmente_con_.2Fetc.2Fpasswd)
        *   [1.6.1 Formato del archivo /etc/passwd](#Formato_del_archivo_.2Fetc.2Fpasswd)
*   [2 Puntualizaciones](#Puntualizaciones)

## Procedimiento

**Advertencia:** Asegúrese de que no está en el sistema como el usuario cuyo nombre está a punto de cambiar. Abra una nueva terminal tty (`Ctrl`+`Alt`+`F1`) e inicie sesión como root, o como otro usuario y haga «su» para actuar como root.

### Cambiar el nombre del inicio de sesión del usuario

Esto cambiará solo el nombre del inicio de sesión del usuario:

```
# usermod -l nombrenuevo nombreantiguo

```

### Cambiar el nombre del usuario

Esto cambiará el nombre del propio usuario:

```
# usermod -c "Nuevo-Nombre-Usuario" nombredeusuario

```

### Cambiar $HOME del usuario

Esto cambiará solo el directorio home del **usuario**:

```
# usermod -d /mi/nuevo/home nombredeusuario

```

### Cambiar $HOME del usuario y mover su contenido

Esto moverá el contenido del directorio home del **usuario** a `/mi/nuevo/home` y establecerá el directorio personal del usuario en otra carpeta distinta:

```
# usermod -md /mi/nuevo/home nombredeusuario;

```

### Cambiar el nombre del grupo

Si desea cambiar el grupo del usuario también:

```
# groupmod -n nuevonombre nombreantiguo

```

**Nota:** Esto va a cambiar el nombre del grupo, pero no el GID numérico del grupo.

Para más información, consulte las páginas man para usermod y groupmod.

### Manualmente con /etc/passwd

En la medida de lo posible, debe usar las órdenes anteriores para modificar los nombres de usuario y los directorios home, sin embargo, para aquellos que quieren conocer las «entresijos» de las operaciones, se puede hacer de forma manual.

#### Formato del archivo /etc/passwd

Cada línea del archivo sigue un formato específico. Hay siete campos, cada uno delimitado por dos puntos («:»).

```
<login name>:<password>:<numerical UID>:<numerical GID>:<Real name/comments>:<home directory>:<user command interpreter>

```

**Advertencia:** Este procedimiento no es seguro para establecer el campo <password> en `/etc/passwd`. Las contraseñas deben cambiarse (por root) con la orden **passwd**.

*   <login name> Este campo no puede estar en blanco. Se aplican las reglas de nomenclatura estándar *NIX.
*   <password> Debería haber una contraseña encriptada, sin embargo, se debe marcar con una «x» minúscula (sin comillas) para indicar que la contraseña se encuentra en `/etc/shadow`.
*   Los nombres de usuario y grupo tiene un UID y un GID numérico correspondiente al ID de usuario y al ID de grupo. En Arch, el primer nombre de inicio de sesión (después de root) es el UID 1000 de forma predeterminada. Las entradas UID/GID posteriores de los usuarios deben ser mayores que 1000\. El GID debe coincidir con el grupo primario para el usuario particular. Los valores numéricos para los GID se enumeran en `/etc/group`.
*   <Real name/comments> es utilizado por servicios tales como **finger**. Este campo es opcional y puede dejarse en blanco.
*   <home directory> es utilizado por la orden login para establecer la variable de entorno `$HOME`. Varios servicios con sus propios usuarios usan «/», que es seguro para los servicios , pero no se recomienda para los usuarios normales.
*   <user command interpreter> es la ruta a la shell por defecto del usuario. Esta es normalmente [Bash](/index.php/Bash "Bash"), pero hay otros intérpretes de línea de órdenes disponibles. La configuración por defecto es «/bin/bash» (sin comillas) para los usuarios. Si utiliza otro CLI, establezca la ruta de aquí. Este campo es opcional.

Ejemplo (usuario):

```
jack:x:1001:100:Jack Smith,some comment here,,:/home/jack:/bin/bash

```

Desglosándolo, esto quiere decir: Jack es el usuario (cuya contraseña está en `/etc/shadow`) con la UID 1001 y su grupo principal es 100 (users). Jack Smith es su nombre completo y hay un comentario asociado a su cuenta. Su directorio principal es `/home/jack` y está usando Bash.

## Puntualizaciones

*   Si está usando [sudo](/index.php/Sudo "Sudo") asegúrese de actualizar el archivo `/etc/sudoers` para reflejar el nuevo nombre de usuario (a través de la orden visudo como root).
*   Si ha modificado el parámetro PATH en `~/.bashrc`, asegúrese de cambiarlo para reflejar el nuevo nombre de usuario.
*   Del mismo modo, asegúrese de cambiar cualquier archivo de configuración como `/etc/rc.local` o lo que sea, si está apuntando a un script o un punto de montaje, etc. dentro del directorio home del usuario anterior.
*   Los [crontabs](/index.php/Cron#Crontab_format "Cron") personales necesitan ser ajustados para adaptar los archivos del usuario del antiguo al nuevo nombre en `/var/spool/cron`, y luego tendrá que abrir `crontab -e` para cambiar las rutas relevantes y ajustar los permisos de los archivos en consecuencia.
*   Las carpetas/archivos personales de [Wine](/index.php/Wine "Wine") contenidas en `~/.wine/drive_c/users`, `~/.local/share/applications/wine/Programs` y posiblemente algún directorio más, necesitan ser renombrados/editados manualmente.
*   El procedimiento para [activar la corrección ortográfica](/index.php/Firefox#Enable_spell_checking "Firefox") de Firefox puede necesitar ser hecho de nuevo, o de lo contrario la comprobación ortográfica podría no funcionar después de cambiar el nombre del usuario.
*   Ciertos complementos de Thunderbird, como [Enigmail](http://enigmail.mozdev.org/home/index.php), podrían necesitar ser reinstalados.
*   Cualquier cosa en su sistema (accesos directos del escritorio, scripts de shell, etc.) que utilice una ruta absoluta a su anterior directorio home (es decir, `/home/nombreusuarioantiguo`) tendrá que ser cambiada para reflejar el nuevo nombre. Para evitar estos problemas en los scripts de shell, basta con utilizar las variables `~` o `$HOME` para los directorios home.
*   Tampoco se olvide de editar consecuentemente los archivos de configuración en `/etc` que se basen en una ruta absoluta (es decir, Samba, CUPS, etc.). Una buena manera de aprender qué archivos son necesario actualizar es usar la orden grep de esta manera: `# grep -r {usuario_antiguor} *`