**Estado de la traducción**
Este artículo es una traducción de [rsync](/index.php/Rsync "Rsync"), revisada por última vez el **2019-11-15**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Rsync&diff=0&oldid=586256) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Related articles

*   [System backup](/index.php/System_backup "System backup")
*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")

[rsync](https://rsync.samba.org/) es una utilidad de código abierto que proporciona una transferencia de archivos incremental rápida.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Interfaces gráficas](#Interfaces_gráficas)
*   [2 Como alternativa de cp/mv](#Como_alternativa_de_cp/mv)
    *   [2.1 Lidiar con la barra diagonal](#Lidiar_con_la_barra_diagonal)
*   [3 Como herramienta para realizar copias de seguridad](#Como_herramienta_para_realizar_copias_de_seguridad)
    *   [3.1 Realizar copia de seguridad automatizada](#Realizar_copia_de_seguridad_automatizada)
    *   [3.2 Realizar copia de seguridad automatizada con SSH](#Realizar_copia_de_seguridad_automatizada_con_SSH)
    *   [3.3 Realizar copia de seguridad automatizada con NetworkManager](#Realizar_copia_de_seguridad_automatizada_con_NetworkManager)
    *   [3.4 Realizar copia de seguridad automatizada con systemd e inotify](#Realizar_copia_de_seguridad_automatizada_con_systemd_e_inotify)
    *   [3.5 Realizar copia de seguridad diferencial por semana](#Realizar_copia_de_seguridad_diferencial_por_semana)
    *   [3.6 Realizar copia de seguridad basada en instantáneas](#Realizar_copia_de_seguridad_basada_en_instantáneas)
    *   [3.7 Realizar copia de seguridad completa del sistema](#Realizar_copia_de_seguridad_completa_del_sistema)
    *   [3.8 Restaurar una copia de seguridad](#Restaurar_una_copia_de_seguridad)
*   [4 Clonar el sistema de archivos](#Clonar_el_sistema_de_archivos)
*   [5 Demonio rsync](#Demonio_rsync)
*   [6 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [rsync](https://www.archlinux.org/packages/?name=rsync).

*rsync* debe instalarse en la máquina tanto de origen como de destino.

### Interfaces gráficas

*   **Grsync** — Front-end GTK.

	[http://www.opbyte.it/grsync/](http://www.opbyte.it/grsync/) || [grsync](https://www.archlinux.org/packages/?name=grsync)

*   **gutback** — Wrapper de rsync escrito en Shell.

	[https://github.com/gutenye/gutbackup](https://github.com/gutenye/gutbackup) || [gutbackup](https://aur.archlinux.org/packages/gutbackup/)

*   **JotaSync** — Interfaz Java Swing para rsync con planificador integrado.

	[https://trixon.se/projects/jotasync/](https://trixon.se/projects/jotasync/) || [jotasync](https://aur.archlinux.org/packages/jotasync/)

*   **luckyBackup** — Front-end Qt escrito en C++.

	[http://luckybackup.sourceforge.net/index.html](http://luckybackup.sourceforge.net/index.html) || [luckybackup](https://aur.archlinux.org/packages/luckybackup/)

Otras herramientas que usan rsync son [rdiff-backup](https://www.archlinux.org/packages/?name=rdiff-backup) y [osync](https://aur.archlinux.org/packages/osync/).

## Como alternativa de cp/mv

rsync se puede usar como una alternativa avanzada para la orden `cp` o `mv`, especialmente para copiar archivos más grandes:

```
$ rsync -P source destination

```

La opción `-P` es la misma que `--partial --progress`, que mantiene los archivos parcialmente transferidos y muestra una barra de progreso de la transferencia.

Es posible que desee utilizar la opción `-r`/`--recursive` para recoger recursivamente el contenido de los directorios.

Los archivos se pueden copiar localmente como con cp, pero el propósito motivador de rsync es copiar archivos de forma remota, es decir, entre dos servidores diferentes. Las ubicaciones remotas se pueden especificar con una sintaxis de dos puntos entre servidores:

```
$ rsync source host:destination

```

o

```
$ rsync host:source destination

```

Las transferencias de archivos en red utilizan el protocolo [SSH](/index.php/SSH "SSH") de forma predeterminada y `host` puede ser un nombre de equipo real o un perfil/alias predefinido desde `.ssh/config`.

Ya sea que transfiera archivos de forma local o remota, rsync primero crea una lista de archivos que contiene información (de manera predeterminada, el tamaño del archivo y la última marca de tiempo de modificación) que luego se utilizará para determinar si el archivo necesita ser construido. Para cada archivo que se construirá, se encuentra una suma de comprobación débil y fuerte para todos los bloques, de modo que cada bloque tenga una longitud de **S** bytes, que no se superponga y que tenga un desplazamiento que sea divisible por **S**. Con esta información, se puede construir un archivo grande usando rsync sin tener que transferir todo el archivo. Para obtener una explicación práctica y matemática detallada, remítase a [how rsync works](https://rsync.samba.org/how-rsync-works.html) y [the rsync algorithm](https://rsync.samba.org/tech_report/tech_report.html), respectivamente.

Para pasar a rsync valores predeterminados rápidamente, puede usar algunos alias:

```
function cpr() {
  rsync --archive -hh --partial --info=stats1 --info=progress2 --modify-window=1 "$@"
} 
function mvr() {
  rsync --archive -hh --partial --info=stats1 --info=progress2 --modify-window=1 --remove-source-files "$@"
}
```

**Nota:** el uso del término *checksum* («suma de verificación») **no** es asimilable al comportamiento de la opción `--checksum`. La opción `--checksum` afecta a la heurística del archivo utilizada antes de transferir cualquier archivo. Independientemente de la opción `--checksum`, siempre se usa una «suma de verificación» (*checksum*) para la construcción de archivos basada en bloques, que es como rynsc transfiere un archivo.

### Lidiar con la barra diagonal

Arch por defecto usa «cp» de GNU (parte de [coreutils](https://www.archlinux.org/packages/?name=coreutils) de GNU). Sin embargo, rsync sigue la convención de BSD para «cp», que da un tratamiento especial a los directorios de origen con una bara diagonal «/». A pesar de que:

```
$ rsync -r source destination

```

crea un directorio «destination/source» con el contenido de «source»;

y la orden:

```
$ rsync -r source/ destination

```

copia todos los archivos presentes en «source/» directamente a «destination», sin subdirectorio intermedio, como si lo hubiera invocado así:

```
$ rsync -r source/. destination

```

Este comportamiento es diferente al de GNU para cp, que trata «source» y «source/» de forma idéntica (pero no «source/.»). Además, algunos intérpretes de órdenes añaden automáticamente la barra inclinada final cuando se completan los nombres de directorios con el tabulador. Debido a estos factores, puede haber cierta tendencia entre los usuarios de rsync nuevos u ocasionales a olvidarse del comportamiento diferente de rsync, y sin darse cuenta provoquen un desastre o incluso sobrescribir archivos importantes al dejar la barra diagonal en la línea de órdenes.

Por lo tanto, puede ser prudente usar un script para eliminar automáticamente las barras diagonales finales antes de invocar rsync:

```
#!/bin/zsh
new_args=();
for i in "$@"; do
    case $i in /) i=/;; */) i=${i%/};; esac
    new_args+=$i;
done
exec rsync "${(@)new_args}"

```

Este script se puede colocar en algún lugar de la ruta y crear un alias a rsync en el archivo de inicio de shell.

## Como herramienta para realizar copias de seguridad

El protocolo rsync puede usarse fácilmente para realizar copias de seguridad, transfiriendo solo los archivos que han cambiado desde la última copia de seguridad. Esta sección describe un script para realizar copias de seguridad programada muy simple que utiliza rsync, el cual generalmente se utiliza para realizar copias a medios extraíbles.

### Realizar copia de seguridad automatizada

A modo de ejemplo, el script se creará en el directorio `/etc/cron.daily`, y se ejecutará diariamente si un [demonio](/index.php/Daemon "Daemon") cron está instalado y configurado correctamente. Configurar y usar [cron](/index.php/Cron "Cron") no entra en el ámbito de este artículo.

Primero, cree un script que contenga las opciones de órdenes apropiadas:

 `/etc/cron.daily/backup` 
```
#!/bin/bash
rsync -a --delete --quiet /folder/to/backup /location/of/backup
```

	`-a` 

	indica que los archivos deben archivarse, lo que significa que la mayoría de sus características se conservan (**no** así las ACL, enlaces duros o atributos extendidos como capacidades)

	`--delete` 

	significa que los archivos eliminados en origen también serán eliminados en la copia de seguridad

Aquí, `/folder/to/backup` debe cambiarse por aquello que quiere respaldar (`/home`, por ejemplo) y `/location/of/backup` es donde se quiere guardar la copia de seguridad (`/media/disk`, pongamos por caso).

Por último, el script debe hacerse ejecutable:

```
# chmod +x /etc/cron.daily/backup

```

### Realizar copia de seguridad automatizada con SSH

Si realiza una copia de seguridad en un servidor remoto utilizando [SSH](/index.php/SSH "SSH"), utilice este script en su lugar:

 `/etc/cron.daily/backup` 
```
#!/bin/bash
rsync -a --delete --quiet -e ssh /folder/to/backup remoteuser@remotehost:/location/of/backup

```

	`-e ssh` 

	le dice a rsync que use SSH

	`remoteuser` 

	es el usuario en el servidor `remotehost`

	`-a` 

	agrupa todas estas opciones de `-rlptgoD` (recursivo, enlaces, permisos, tiempos, grupo, propietario, dispositivos)

**Nota:** Rsync intentará modificar cualquier archivo respaldado previamente en la máquina de destino para que coincida con su estado actual en la máquina de origen, con cada copia de seguridad incremental. Esto significa que al hacer una copia de seguridad de los archivos que son propiedad de root mediante SSH (y al preservar los permisos y las propiedades como con la opción `-a`), se necesita acceso de root a la máquina de destino. La forma preferida de lograr esto para la automatización es configurar el demonio SSH para permitir que root inicie sesión utilizando una [clave pública sin contraseña](https://unix.stackexchange.com/a/92397) y ejecutar la orden rsync como root.

### Realizar copia de seguridad automatizada con NetworkManager

Este script inicia una copia de seguridad cuando se establece la conexión de red.

Primero, cree un script que contenga las opciones de órdenes apropiadas:

 `/etc/NetworkManager/dispatcher.d/backup` 
```
#!/bin/bash

if [ x"$2" = "xup" ] ; then
        rsync --force --ignore-errors -a --delete --bwlimit=2000 --files-from=files.rsync /folder/to/backup /location/to/backup
fi
```

	`-a` 

	agrupa todas estas opciones de `-rlptgoD` (recursivo, enlaces, permisos, tiempos, grupo, propietario, dispositivos=

	`--files-from` 

	lee la ruta relativa de */folder/to/backup* desde este archivo

	`--bwlimit` 

	limita el ancho de banda de E/S; KBytes por segundo

Además, el script debe tener permiso de escritura solo para el propietario (root, por supuesto) (vea [NetworkManager#Network services with NetworkManager dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") para más detalles).

### Realizar copia de seguridad automatizada con systemd e inotify

**Nota:**

*   Debido a las limitaciones de inotify y systemd (vea [esta pregunta y respuesta](http://www.quora.com/Linux-Kernel/Inotify-monitoring-of-directories-is-not-recursive-Is-there-any-specific-reason-for-this-design-in-Linux-kernel)), el monitoreo recursivo del sistema de archivos no es posible. Aunque puede observar un directorio y su contenido, no monitoreará recursivamente los subdirectorios ni observará su contenido; debe especificar explícitamente cada directorio a seguir, incluso si ese directorio es hijo de un directorio que está siendo monitoreado.
*   Esta configuración se basa en una instancia de [systemd/User](/index.php/Systemd/User "Systemd/User").

En lugar de ejecutar copias de seguridad a intervalos de tiempo según se haya programado, como las implementadas en [cron](/index.php/Cron "Cron"), es posible ejecutar una copia de seguridad cada vez que uno de los archivos de los que está realizando una copia de seguridad cambia. Las unidades `systemd.path` usan `inotify` para monitorear el sistema de archivos, y se pueden usar junto con los archivos `systemd.service` para iniciar cualquier proceso (en este caso su copia de seguridad con [rsync](/index.php/Rsync "Rsync")) basado en un evento del sistema de archivos.

Primero, cree el archivo `systemd.path` que monitoreará los archivos que está respaldando:

 `~/.config/systemd/user/backup.path` 
```
[Unit]
Description=Comprueba si las rutas que se están copiando actualmente han cambiado

[Path]
PathChanged=%h/documents
PathChanged=%h/music

[Install]
WantedBy=default.target

```

Luego cree un archivo `systemd.service` que se activará cuando detecte un cambio. De manera predeterminada, se activará un archivo de servicio con el mismo nombre que la unidad de ruta (en este caso, `backup.path`), salvo por la extensión `.service` en lugar de `.path` (en este caso `backup.service`).

**Nota:** si necesita ejecutar múltiples órdenes rsync, utilice `Type=oneshot`. Esto le permite especificar múltiples parámetros `ExecStart=`, uno para cada órden [rsync](/index.php/Rsync "Rsync"), que se ejecutará. Alternativamente, puede simplemente escribir un script para realizar todas sus copias de seguridad, al igual que con los scripts de [cron](/index.php/Cron "Cron").
 `~/.config/systemd/user/backup.service` 
```
[Unit]
Description=Backs up files

[Service]
ExecStart=/usr/bin/rsync %h/./documents %h/./music -CERrltm --delete ubuntu:

```

Ahora todo lo que tiene que hacer es [iniciar](/index.php/Start_(Espa%C3%B1ol) "Start (Español)")/activar `backup.path` como un servicio de systemd normal y comenzará a monitorear los cambios de los archivos e iniciará en consecuencia `backup.service`.

### Realizar copia de seguridad diferencial por semana

Esta es una opción útil de rsync, que consiste en realizar una copia de seguridad completa (en cada ejecución) y mantener una copia de seguridad diferencial solo de los archivos modificados en un directorio separado para cada día de la semana.

Primero, cree un script que contenga las opciones de órdenes apropiadas:

 `/etc/cron.daily/backup` 
```
#!/bin/bash

DAY=$(date +%A)

if [ -e /location/to/backup/incr/$DAY ] ; then
  rm -fr /location/to/backup/incr/$DAY
fi

rsync -a --delete --quiet --inplace --backup --backup-dir=/location/to/backup/incr/$DAY /folder/to/backup/ /location/to/backup/full/
```

	`--inplace` 

	implica la actualización `--partial` de los archivos de destino en el lugar

### Realizar copia de seguridad basada en instantáneas

La misma idea se puede utilizar para mantener un árbol de instantáneas de sus archivos. En otras palabras, un directorio con copias de los archivos ordenadas por fecha. Las copias se realizan mediante enlaces, lo que significa que solo los archivos que cambiaron ocuparán espacio. En términos generales, esta es la idea detrás de TimeMachine de Apple.

Este script básico es fácil de implementar y crea instantáneas incrementales rápidas utilizando la opción `--link-dest` para enlazar archivos sin cambios:

 `/usr/local/bin/snapbackup.sh` 
```
#!/bin/bash

# Script básico de copia de seguridad con rsync de estilo de instantáneas
# Config
OPT="-aPh"
LINK="--link-dest=/snapshots/username/last/" 
SRC="/home/username/files/"
SNAP="/snapshots/username/"
LAST="/snapshots/username/last"
date=`date "+%Y-%b-%d:_%T"`

# Ejecutar rsync para crear una instantánea
rsync $OPT $LINK $SRC ${SNAP}$date

# Eliminar la instantánea anterior del enlace simbólico
rm -f $LAST

# Crear un nuevo enlace simbólico a la última instantánea
ln -s ${SNAP}$date $LAST

```

Debe existir un enlace simbólico a una copia de seguridad completa como destino para `--link-dest`. Si se elimina la instantánea más reciente, será necesario volver a crear el enlace simbólico para que apunte a la instantánea más reciente. Si `--link-dest` no encuentra un enlace simbólico que funcione, rsync procederá a copiar todos los archivos de origen en lugar de solo los cambios.

Una versión más sofisticada mantiene una copia de seguridad completa actualizada `$SNAP/latest` y, en caso de que un cierto número de archivos haya cambiado desde la última copia de seguridad completa, crea una instantánea `$SNAP/$DATETAG` de la copia de seguridad completa actual utilizando `cp -al` para vincular archivos sin cambios:

 `/usr/local/bin/rsnapshot.sh` 
```
#!/bin/bash

## mi propio procedimiento de copia de seguridad
## estilo instantánea basado en rsync
## (cc) marcio rps AT gmail.com

# config vars

SRC="/home/username/files/" #no olvidar la barra diagonal final
SNAP="/snapshots/username"
OPTS="-rltgoi --delay-updates --delete --chmod=a-w"
MINCHANGES=20

# ejecutar este proceso con prioridad baja

ionice -c 3 -p $$
renice +12  -p $$

# sincronizar

rsync $OPTS $SRC $SNAP/latest >> $SNAP/rsync.log

# compruebar si ha cambiado lo suficiente y si es así
# hacer una copia enlazada denominada por fecha

COUNT=$( wc -l $SNAP/rsync.log|cut -d" " -f1 )
if [ $COUNT -gt $MINCHANGES ] ; then
        DATETAG=$(date +%Y-%m-%d)
        if [ ! -e $SNAP/$DATETAG ] ; then
                cp -al $SNAP/latest $SNAP/$DATETAG
                chmod u+w $SNAP/$DATETAG
                mv $SNAP/rsync.log $SNAP/$DATETAG
                chmod u-w $SNAP/$DATETAG
        fi
fi

```

Para hacer las cosas realmente simples, este script puede ejecutarse desde una unidad [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

### Realizar copia de seguridad completa del sistema

Esta sección trata sobre el uso de *rsync* para transferir una copia de todo el árbol `/`, excluyendo algunas carpetas seleccionadas. Se considera que este enfoque es mejor que [clonar un disco](/index.php/Disk_cloning_(Espa%C3%B1ol) "Disk cloning (Español)") con `dd` dado que ello utilizar un tamaño diferente, una tabla de partición y un sistema de archivos, y mejor que copiar con `cp -a` también, porque permite un mayor control sobre los permisos de archivos, atributos, [Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") y [extended attributes](/index.php/Extended_attributes "Extended attributes").

*rsync* funcionará incluso mientras el sistema se está ejecutando, pero los archivos modificados durante la transferencia pueden o no transferirse, lo que puede causar un comportamiento inesperado de algunos programas que usan los archivos transferidos.

Este enfoque funciona bien para migrar una instalación existente a un nuevo disco duro o [SSD](/index.php/SSD "SSD").

Ejecute la siguiente orden como root para asegurarse de que rsync pueda acceder a todos los archivos del sistema y preservar su propiedad:

```
# rsync -aAXv --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"} / */path/to/backup/folder*

```

Al utilizar el conjunto de opciones `-aAX`, los archivos se transfieren en modo de comprimido, lo que garantiza que los enlaces simbólicos, los dispositivos, los permisos, las propiedades, los tiempos de modificación, los [ACL](/index.php/ACL "ACL") y los atributos extendidos se conserven, suponiendo que el [sistema de archivos](/index.php/File_system "File system") de destino dé soporte a esta función.

La opción `--exclude` hace que se excluyan los archivos que coinciden con los patrones dados. Se excluye el contenido de `/dev`, `/proc`, `/sys`, `/tmp` y `/run` en la orden anterior, porque se rellenan en el arranque, aunque las carpetas *no* se crean por sí mismas. `/lost+found` es específico del sistema de archivos. La orden anterior depende de la expansión de llaves disponible tanto en las shells [bash](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html) como [zsh](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Brace-Expansion).Cuando se utiliza un [shell](/index.php/Shell "Shell") diferente, los patrones `--exclude` deben repetirse manualmente. Citar los patrones de exclusión evitará la expansión por la [shell](/index.php/Shell "Shell"), lo cual es necesario, por ejemplo, cuando se realiza una copia de seguridad mediante [SSH](/index.php/SSH "SSH"). Al terminar las rutas excluidas con `*` se garantiza que dichos directorios se creen si aún no existen.

**Note:**

*   Si planea hacer una copia de seguridad de su sistema en otro lugar que no sea `/mnt` o `/media`, no olvide agregarlo a la lista de patrones de exclusión para evitar un bucle infinito.
*   Si hay montajes de enlace en el sistema, también deben excluirse para que el contenido asociado al enlace se copie solo una vez.
*   Si utiliza un [swap file](/index.php/Swap_file "Swap file"), asegúrese de excluirlo también.
*   Considere si desea hacer una copia de seguridad de la carpeta `/home/`. Si contiene sus datos, podría ser considerablemente más grande que el sistema. De lo contrario, considere excluir subdirectorios sin importancia como `/home/*/.thumbnails/*`, `/home/*/.cache/mozilla/*`, `/home/*/.cache/chromium/*` y `/home/*/.local/share/Trash/*`, dependiendo del software instalado en el sistema. Si [GVFS](/index.php/GVFS "GVFS") está instalado, `/home/*/.gvfs` debe excluirse para evitar errores de rsync.

Es posible que desee incluir opciones [rsync](/index.php/Rsync "Rsync") adicionales, como las siguientes. Consulte [rsync(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rsync.1) para ver la lista completa.

*   Si usa muchos enlaces duros (por ejemplo, si está usando [Flatpak](/index.php/Flatpak "Flatpak")), considere agregar la opción `-H`, que está desactivada por defecto debido a su gasto de memoria. Sin embargo, no debería ser un problema en la mayoría de los ordenadores modernos. Muchos enlaces duros residen en el directorio `/usr/`.
*   Es posible que desee agregar la opción `--delete` de rsync si está ejecutando esto varias veces en la misma carpeta de respaldo. En este caso, asegúrese de que la ruta de origen no termine con `/*`, o esta opción solo tendrá efecto en los archivos dentro de los subdirectorios del directorio de origen, pero no tendrá ningún efecto en los archivos que residen directamente dentro del directorio de origen.
*   Si utiliza archivos dispersos, como discos virtuales, imágenes [Docker](/index.php/Docker "Docker") y similares, debe agregar la opción `-S`.
*   La opción `--numeric-ids` desactivará la asignación de nombres de usuarios y grupos; en su lugar, se transferirán las identificaciones numéricas de grupo y de usuario. Esto es útil cuando se realiza una copia de seguridad mediante [SSH](/index.php/SSH "SSH") o cuando se utiliza un sistema live para hacer una copia de seguridad de un disco con sistema diferente.
*   Al elegir la opción `--info=progress2` en lugar de `-v`se mostrará la información general del progreso y la velocidad de transferencia, en lugar de la lista de archivos que se están transfiriendo.
*   To avoid crossing a filesystem boundary when recursing, add the option `-x`/`--one-file-system`. This will prevent backing up any mount point in the hierarchy.

### Restaurar una copia de seguridad

Si desea restaurar una copia de seguridad, use la misma orden de rsync que se ejecutó, pero con el origen y el destino invertidos.

## Clonar el sistema de archivos

rsync proporciona una forma de hacer una copia de todos los datos en un sistema de archivos al tiempo que conserva la mayor cantidad de información posible, incluidos los metadatos del sistema de archivos. Es un procedimiento de clonación de datos en un nivel de sistema de archivos donde los sistemas de archivos de origen y de destino no necesitan ser del mismo tipo. Se puede utilizar para realizar copias de seguridad, migrar sistemas de archivos o recuperar datos.

El modo *archive* de rsync está cerca de ser apto para el trabajo, pero no realiza una copia de seguridad de los metadatos especiales del sistema de archivos, como listas de control de acceso, atributos extendidos o propiedades de archivos dispersos. Para una clonación exitosa a nivel del sistema de archivos, se deben proporcionar algunas opciones adicionales:

```
rsync -qaHAXS DIRECTORIO_ORIGEN DIRECTORIO_DESTINO

```

Y su significado es (de la página de manual):

```
-H, --hard-links      preserva los enlaces duros
-A, --acls            preserva las ACL (implica -p)
-X, --xattrs          preserva los atributos extendidos
-S, --sparse          manejar archivos dispersos de manera eficiente

```

Además, use `-x` si tiene otros sistemas de archivos montados bajo el árbol que desea excluir de la copia. La copia producida se puede volver a leer y verificar (por ejemplo, después de un intento de recuperación de datos) a nivel del sistema de archivos con la opción recursiva de `diff`:

```
diff -r DIRECTORIO_ORIGEN DIRECTORIO_DESTINO

```

Es posible realizar una migración exitosa del sistema de archivos usando rsync como se describe en este artículo y actualizando [fstab](/index.php/Fstab "Fstab") y [bootloader](/index.php/Bootloader "Bootloader") como se describe en [Migrate installation to new hardware](/index.php/Migrate_installation_to_new_hardware "Migrate installation to new hardware").Básicamente, esto proporciona una forma de convertir cualquier sistema de archivos raíz a otro.

## Demonio rsync

*rsync* se puede ejecutar como demonio en un servidor que escucha el puerto `873`.

Edite la plantilla `/etc/rsyncd.conf`, configure un recurso compartido e [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") el servicio `rsyncd.service`.

**Nota:** a partir de [rsync](https://www.archlinux.org/packages/?name=rsync)-3.1.2-5 la unidad de systemd `rsyncd.service`, incluida en el paquete, agrega la función de seguridad `ProtectSystem=full` (la opción `ProtectHome=on` se ha deshecho en [rsync](https://www.archlinux.org/packages/?name=rsync)-3.1.2-8) en la sección `[Service]`. Esto hace que los directorios `/boot/`, `/etc/` y `/usr/` sean de solo lectura. Si necesita directorios del sistema de escritura de rsyncd, puede [editar](/index.php/Edit "Edit") la unidad y establecer `ProtectSystem=off` en la sección `[Service]` del fragmento sobrescrito.

Utilización del cliente, por ejemplo listar el contenido del servidor:

```
$ rsync rsync://*server/share*

```

Transferir archivo del cliente al servidor:

```
$ rsync *local-file* rsync://*server/share/*

```

Tenga en cuenta iptables para abrir el puerto `873` y la autenticación de usuario.

**Nota:** todos los datos transferidos, incluida la autenticación del usuario, no están cifrados.

## Véase también

*   Se pueden buscar más ejemplos de uso en los foros [Community Contributions](https://bbs.archlinux.org/viewforum.php?id=27) y [General Programming](https://bbs.archlinux.org/viewforum.php?id=33)
*   [Howto – local and remote snapshot backup using rsync with hard links](http://www.pointsoftware.ch/en/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) Includes file deduplication with hard-links, MD5 integrity signature, 'chattr' protection, filter rules, disk quota, retention policy with exponential distribution (backups rotation while saving more recent backups than older)
*   [Using SSH keys/identity files with rsync](https://stackoverflow.com/questions/5527068/how-do-you-use-an-identity-file-with-rsync)