Related articles

*   [pacman](/index.php/Pacman "Pacman")
*   [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance")
*   [Mirrors](/index.php/Mirrors "Mirrors")
*   [Creating packages](/index.php/Creating_packages "Creating packages")

Para métodos generales para mejorar la flexibilidad de las sugerencias proporcionadas o del propio pacman, consulte [Core utilities](/index.php/Core_utilities "Core utilities") y [Bash](/index.php/Bash "Bash").

## Contents

*   [1 Mantenimiento](#Mantenimiento)
    *   [1.1 Listando paquetes](#Listando_paquetes)
        *   [1.1.1 Por tamaño](#Por_tama.C3.B1o)
        *   [1.1.2 Por fecha](#Por_fecha)
        *   [1.1.3 No especificado en un grupo o repositorio](#No_especificado_en_un_grupo_o_repositorio)
        *   [1.1.4 Paquetes en desarrollo](#Paquetes_en_desarrollo)
    *   [1.2 Listado de archivos propiedad de un paquete , ordenado por tamaño](#Listado_de_archivos_propiedad_de_un_paquete_.2C_ordenado_por_tama.C3.B1o)
    *   [1.3 Identificar archivos que no pertenecen a ningún paquete](#Identificar_archivos_que_no_pertenecen_a_ning.C3.BAn_paquete)
    *   [1.4 Eliminación de paquetes no utilizados (huérfanos)](#Eliminaci.C3.B3n_de_paquetes_no_utilizados_.28hu.C3.A9rfanos.29)
    *   [1.5 Eliminar todo menos el grupo base](#Eliminar_todo_menos_el_grupo_base)
    *   [1.6 Obtener la lista de dependencias de varios paquetes](#Obtener_la_lista_de_dependencias_de_varios_paquetes)
    *   [1.7 Listado de archivos de copia de seguridad modificados](#Listado_de_archivos_de_copia_de_seguridad_modificados)
*   [2 Optimización](#Optimizaci.C3.B3n)
    *   [2.1 Velocidades de acceso a la base de datos](#Velocidades_de_acceso_a_la_base_de_datos)
    *   [2.2 Velocidades de descarga](#Velocidades_de_descarga)
    *   [2.3 Powerpill](#Powerpill)
    *   [2.4 Wget](#Wget)
    *   [2.5 Aria2](#Aria2)
*   [3 Utilidades](#Utilidades)
    *   [3.1 Front-ends gráficos](#Front-ends_gr.C3.A1ficos)

## Mantenimiento

### Listando paquetes

Es posible que desee obtener la lista de paquetes instalados con su versión, lo cual es útil cuando se reportan errores o se discuten los paquetes instalados.

*   Enumere todos los paquetes explícitamente instalados: `pacman -Qe`.
*   todos los paquetes nativos instalados explícitamente (es decir, presentes en la base de datos de sincronización) que no sean dependencias directas o opcionales: `pacman -Qent` .
*   Lista de todos los paquetes extranjeros (normalmente descargados e instalados manualmente): `pacman -Qm`.
*   Haga una lista de todos los paquetes nativos (instalados desde la (s) base de datos de sincronización): `pacman -Qn` .
*   Listar paquetes por regex: `pacman -Qs *regex*` .
*   Lista de paquetes por regex con formato de salida personalizado: `expac -s "%-30n %v" *regex*` (necesita [expac](https://www.archlinux.org/packages/?name=expac)).

#### Por tamaño

Para obtener una lista de paquetes instalados ordenados por tamaño, lo que puede ser útil al liberar espacio en el disco duro:

*   Instalar [expac](https://www.archlinux.org/packages/?name=expac) y ejecutar `expac -H M '%m\t%n' | sort -h`.
*   Ejecute [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) con la opción `-c` .

Para enumerar el tamaño de descarga de varios paquetes (deje packages en blanco para listar todos los paquetes):

```
 $ expac -S -H M '%k \ t%n' *packages*

```

Para listar los paquetes explícitamente instalados que no están en [base](https://www.archlinux.org/groups/x86_64/base/) ni en [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) con tamaño y descripción:

```
 $ expac -H M "%011m\t%-20n\t%10d" $(comm -23 <(pacman -Qqen | sort) <(pacman -Qqg base base-devel | sort)) | sort -n

```

Enumere todos los paquetes en Arch Linux ISO que no están en el grupo base:

```
$ comm -23 <(wget -q -O - https://git.archlinux.org/archiso.git/plain/configs/releng/packages.both) <(pacman -Qqg base | sort)

```

#### Por fecha

Para enumerar los 20 últimos paquetes instalados con expac , ejecute:

```
 $ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20

```

O, con segundos desde la época (1970-01-01 UTC):

```
 $ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20

```

#### No especificado en un grupo o repositorio

**Nota:** Para obtener una lista de paquetes instalados como dependencias pero que ya no son necesarios para ningún paquete instalado, consulte [#Eliminación de paquetes no utilizados (huérfanos)](#Eliminaci.C3.B3n_de_paquetes_no_utilizados_.28hu.C3.A9rfanos.29).

Lista los paquetes explícitamente instalados que no están en los grupos de [base](https://www.archlinux.org/groups/x86_64/base/) o [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) :

```
 $ comm -23 <(pacman -Qeq | sort) <(pacman -Qgq base base-devel | sort)

```

Enumere todos los paquetes instalados no requeridos por otros paquetes y que no estén en los grupos de [base](https://www.archlinux.org/groups/x86_64/base/) o de [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) :

```
 $ comm -23 <(pacman -Qqt | sort) <(pacman -Sqg base base-devel | sort)

```

Como arriba, pero con descripciones:

```
 $ expac -HM '% -20n \ t% 10d' $ (comm -23 <(pacman -Qqt | sort) <(pacman -Qqg base -devel | sort)

```

Lista todos los paquetes instalados que *no* están en el repositorio especificado *repo_name*

```
 $ comm -23 <(pacman -Qtq | sort) <(pacman -Slq repo_name | sort)

```

Liste todos los paquetes instalados que están en el repositorio repo_name :

```
 $ comm -12 <(pacman -Qtq | sort) <(pacman -Slq repo_name | sort)

```

Lista todos los paquetes en Arch Linux ISO que no están en el grupo base:

```
$ comm -23 <(wget -q -O - https://git.archlinux.org/archiso.git/plain/configs/releng/packages.both) <(pacman -Qqg base | sort)

```

#### Paquetes en desarrollo

Para listar todos lo paquetes *development/unstable* , ejecute:

```
$ pacman -Qq | awk '/^.+(-cvs|-svn|-git|-hg|-bzr|-darcs)$/'

```

### Listado de archivos propiedad de un paquete , ordenado por tamaño

Esto podría ser útil si descubrió que un paquete específico utiliza una gran cantidad de espacio y desea saber qué archivos lo componen.

```
$ pacman -Qlq *package* | grep -v '/$' | xargs du -h | sort -h

```

### Identificar archivos que no pertenecen a ningún paquete

Si su sistema tiene archivos huérfanos que no pertenecen a ningún paquete (un caso común si no [usa el administrador de paquetes para instalar software](/index.php/Enhance_system_stability#Use_the_package_manager_to_install_software "Enhance system stability")), es posible que desee encontrar dichos archivos para limpiarlos. El proceso general para hacerlo es:

1.  Crear una lista ordenada de los archivos que desea verificar los propietarios: `$ find /etc /opt /usr | sort > all_files.txt` 

1.  Crear una lista ordenada de los archivos rastreados por *pacman* (y elimina las barras diagonales de los directorios): `$ pacman -Qlq | sed 's|/$||' | sort > owned_files.txt` 

1.  Encuentra líneas en la primera lista que no están en el segundo: `$ comm -23 all_files.txt owned_files.txt` 

En la práctica, este proceso es complicado porque muchos archivos importantes no forman parte de ningún paquete (por ejemplo, archivos generados en tiempo de ejecución, configuraciones personalizadas), por lo que se incluirán en el resultado final, lo que dificulta seleccionar los archivos que pueden eliminarse de manera segura.

**Tip:** El [lostfiles](https://aur.archlinux.org/packages/lostfiles/) script realiza pasos similares, pero también incluye una extensa lista negra para eliminar falsos positivos comunes de la salida. [aconfmgr](https://github.com/CyberShadow/aconfmgr) ([aconfmgr-git](https://aur.archlinux.org/packages/aconfmgr-git/)) también permite rastrear archivos huérfanos usando una secuencia de comandos de configuración.

### Eliminación de paquetes no utilizados (huérfanos)

Para eliminar de forma *recursiva* los huérfanos y sus archivos de configuración:

```
# pacman -Rns $(pacman -Qtdq)

```

Si no se encontraron paquetes huérfanos, aparecerán errores de pacman con `error: no targets specified`. Esto se espera ya que no se pasaron argumentos a `pacman -Rns`.

**Note:** Los argumentos `-Qt` enumeran sólo huérfanos verdaderos. Para incluir paquetes que son *opcionalmente* requeridos por otro paquete, pase el indicador `-t` dos veces (*i.e.*, `-Qtt`).

### Eliminar todo menos el grupo base

Si alguna vez es necesario eliminar todos los paquetes, excepto el grupo base, pruebe esta sola linea:

```
# pacman -R $(comm -23 <(pacman -Qq | sort) <((for i in $(pacman -Qqg base); do pactree -ul "$i"; done) | sort -u))

```

Esta única linea fue originalmente concebida en [esta conversación](https://bbs.archlinux.org/viewtopic.php?id=130176), y posteriormente mejorada en este artículo.

### Obtener la lista de dependencias de varios paquetes

Las dependencias se ordenan alfabéticamente y las repetidas se eliminan.

**Nota:** Para mostrar solo el árbol de paquetes locales instalados, use `pacman -Qi`.

```
$ pacman -Si *packages* | awk -F'[:<=>]' '/^Depends/ {print $2}' | xargs -n1 | sort -u

```

Como alternativa puede utilizar [expac](https://www.archlinux.org/packages/?name=expac):

```
$ expac -l '
' %E -S *packages* | sort -u

```

### Listado de archivos de copia de seguridad modificados

Si desea realizar una copia de seguridad de los archivos de configuración del sistema, puede copiar todos los archivos en `/etc/`, pero normalmente sólo le interesan los ficheros que ha modificado. Los archivos de [copias de seguridad](/index.php/Pacnew_and_Pacsave_files#Package_backup_files "Pacnew and Pacsave files") se puede ver con el siguiente comando:

```
# pacman -Qii | awk '/^MODIFIED/ {print $2}'

```

Ejecutar este comando con permisos de root asegurará que los archivos sólo pueden ser leídos por root (por ejemplo `/etc/sudoers`) están incluidos en la salida.

**Tip:** Mire [#Listado de todos los archivos modificados de los paquetes](#Listado_de_todos_los_archivos_modificados_de_los_paquetes) para listar todos los archivos modificados que conoce *pacman* , no sólo los archivos de copia de seguridad.

## Optimización

### Velocidades de acceso a la base de datos

Pacman almacena toda la información del paquete en una colección de archivos pequeños, uno para cada paquete. La mejora de las velocidades de acceso a la base de datos reduce el tiempo empleado en las tareas relacionadas con la base de datos, por ejemplo, buscar paquetes y resolver las dependencias del paquete. El método más seguro y fácil es ejecutarlo como root:

```
 # pacman-optimize

```

Esto intentará poner todos los archivos pequeños juntos en una ubicación (física) en el disco duro para que la cabeza del disco duro no tenga que moverse tanto al acceder a todos los datos. Este método es seguro, pero no es infalible: depende del sistema de archivos, el uso del disco y la fragmentación del espacio vacío. Otra opción más agresiva sería eliminar primero los paquetes desinstalados del caché y eliminar los repositorios no utilizados antes de la optimización de la base de datos:

```
 # pacman -Sc && pacman-optimize

```

### Velocidades de descarga

Nota: Si las velocidades de descarga se han reducido a un rastreo, asegúrese de que está utilizando uno de los muchos espejos y no ftp.archlinux.org, que se estrangula desde marzo de 2007 . Al descargar paquetes pacman usa los espejos en el orden en que están en /etc/pacman.d/mirrorlist . El espejo que está en la parte superior de la lista por defecto, sin embargo, puede no ser el más rápido para usted. Para seleccionar un espejo más rápido, consulte Espejos . La velocidad de Pacman en la descarga de paquetes también puede ser mejorada mediante el uso de una aplicación diferente para descargar paquetes, en lugar del descargador de archivos integrado de Pacman. En todos los casos, asegúrese de tener la última Pacman antes de hacer cualquier modificación.

```
 # pacman -Syu

```

### Powerpill

Powerpill es un envoltorio de Pacman que utiliza la descarga paralela y segmentada para tratar de acelerar las descargas de Pacman.

### Wget

Esto también es muy útil si necesita configuraciones proxy más potentes que las capacidades incorporadas de pacman.

Para usar wget , primero instale el paquete wget y luego modifique /etc/pacman.conf descomentando la siguiente línea en la sección [options] :

```
 XferCommand = / usr / bin / wget -c -q --show-progress --passive-ftp -O% o% u

```

En lugar de descomentar los parámetros de wget en /etc/pacman.conf , también puede modificar el archivo de configuración de wget directamente (el archivo de todo el sistema es /etc/wgetrc , por usuario los archivos son $HOME/.wgetrc .

### Aria2

Aria2 es una utilidad de descarga de peso ligero con soporte para HTTP / HTTPS y transferencias directas continuas y segmentadas. Aria2 permite múltiples y simultáneas conexiones HTTP / HTTPS y FTP a un espejo de Arch, lo que debería resultar en un aumento en las velocidades de descarga para la recuperación de archivos y paquetes.

Nota: El uso de aria2c en XferCommand de Pacman no dará lugar a descargas paralelas de varios paquetes. Pacman invoca el XferCommand con un solo paquete a la vez y espera a que se complete antes de invocar el siguiente. Para descargar varios paquetes en paralelo, consulte Powerpill.

Instale aria2 y luego edite /etc/pacman.conf agregando la siguiente línea a la sección [options] :

```
 XferCommand = / usr / bin / aria2c --allow-overwrite = true --continue = true --file-allocation = ninguno --log-level = error --max-tries = 2 --max-connection-per-server = 2 --max-file-not-found = 5 --min-split-size = 5M --no-conf --remote-time = true --summary-interval = 60 --timeout = 5 --dir = / --out% o% u

```

Sugerencia: Esta configuración alternativa para usar pacman con aria2 intenta simplificar la configuración y añade más opciones de configuración.

Vea OPCIONES en man aria2c para las opciones de aria2c usadas.

*   -d, --dir : El directorio para almacenar los archivos descargados según lo especificado por pacman .
*   -o, --out : El nombre de archivo de salida del archivo (s) descargado (s).
*   %o : Variable que representa el nombre de archivo local especificado por pacman.
*   %u : Variable que representa la URL de descarga especificada por pacman.

## Utilidades

*   **Lostfiles** — Script que identifica archivos que no son propiedad de ningún paquete.

	[https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [lostfiles](https://aur.archlinux.org/packages/lostfiles/)

*   **Pacmatic** — Wrapper de *Pacman* para comprobar notícias de Arch antes de la actualización, evitar actualizaciones parciales y advertir sobre cambios en el archivo de configuración.

	[http://kmkeen.com/pacmatic](http://kmkeen.com/pacmatic) || [pacmatic](https://www.archlinux.org/packages/?name=pacmatic)

*   **pacutils** — Biblioteca de ayuda para programas basados en libalpm.

	[https://github.com/andrewgregory/pacutils](https://github.com/andrewgregory/pacutils) || [pacutils](https://www.archlinux.org/packages/?name=pacutils)

*   **[pkgfile](/index.php/Pkgfile "Pkgfile")** — Es una herramienta para buscar ficheros en paquetes.

	[http://github.com/falconindy/pkgfile](http://github.com/falconindy/pkgfile) || [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)

*   **pkgtools** — Colección de scripts para los paquetes de Arch Linux.

	[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)

*   **repoctl** — Herramienta para ayudar a gestionar repositorios locales.

	[https://github.com/cassava/repoctl](https://github.com/cassava/repoctl) || [repoctl](https://aur.archlinux.org/packages/repoctl/)

*   **repose** — Una herramienta de construcción de repositorios Arch Linux.

	[https://github.com/vodik/repose](https://github.com/vodik/repose) || [repose](https://www.archlinux.org/packages/?name=repose)

*   **[snap-pac](/index.php/Snapper#Wrapping_pacman_transactions_in_snapshots "Snapper")** — Haga que *pacman* utilice automáticamente *snapper* para crear instantáneas previas y posteriores como YaST de openSUSE.

	[https://github.com/wesbarnett/snap-pac](https://github.com/wesbarnett/snap-pac) || [snap-pac](https://www.archlinux.org/packages/?name=snap-pac)

### Front-ends gráficos

**Advertencia:** Algunos front-ends como [octopi](https://aur.archlinux.org/packages/octopi/) [[1]](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) or [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/) [[2]](https://github.com/manjaro/pamac/blob/master/data/systemd/pamac-mirrorlist.service#L9) realizan [partial upgrades](/index.php/Partial_upgrade "Partial upgrade") periódicamente.

*   **Aarchup** — Fork de archup. Tiene las mismas opciones que *archup* más algunas otras características. Para las diferencias entre ambos, compruebe [changelog](https://bbs.archlinux.org/viewtopic.php?id=119129).

	[https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/) || [aarchup](https://aur.archlinux.org/packages/aarchup/)

*   **Arch-Update** — Indicador de actualización para Gnome-Shell.

	[https://github.com/RaphaelRochet/arch-update](https://github.com/RaphaelRochet/arch-update) || [gnome-shell-extension-arch-update](https://aur.archlinux.org/packages/gnome-shell-extension-arch-update/)

*   **Arch-Update-Notifier** — Indicador de actualización para KDE.

	[https://github.com/I-Dream-in-Code/kde-arch-update-plasmoid](https://github.com/I-Dream-in-Code/kde-arch-update-plasmoid) || [plasma5-applets-kde-arch-update-notifier-git](https://aur.archlinux.org/packages/plasma5-applets-kde-arch-update-notifier-git/)

*   **Discover** — Una colección de herramientas de administración de paquetes para KDE, utilizando PackageKit.

	[https://projects.kde.org/projects/kde/workspace/discover](https://projects.kde.org/projects/kde/workspace/discover) || [discover](https://www.archlinux.org/packages/?name=discover)

*   **GNOME packagekit** — Herramienta de gestión de paquetes basada en GTK.

	[http://www.freedesktop.org/software/PackageKit/](http://www.freedesktop.org/software/PackageKit/) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **GNOME Software** — Gnome Software App. (Curated selection for GNOME)

	[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **kalu** — Una pequeña aplicación que agregará un ícono a su bandeja de sistema, verificando regularmente si hay nuevas actualizaciones.

	[https://jjacky.com/kalu/](https://jjacky.com/kalu/) || [kalu](https://aur.archlinux.org/packages/kalu/)

*   **pcurses** — Gestión de paquetes en una interfaz de curses

	[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **PkgBrowser** — Aplicación para buscar y explorar paquetes de Arch, muestra detalles sobre paquetes seleccionados.

	[https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home](https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

*   **tkPacman** — Depende solo de Tcl/Tk y X11, e interactúa con la base de datos del paquete a través de la CLI de *pacman*.

	[http://sourceforge.net/projects/tkpacman](http://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)