Artículos relacionados

*   [Mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)")
*   [Creating packages (Español)](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)")

**Estado de la traducción**
Este artículo es una traducción de [Pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks"), revisada por última vez el **2020-01-02**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Pacman/Tips_and_tricks&diff=0&oldid=593602) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Para conocer métodos generales que permitan mejorar la flexibilidad de las presentes sugerencias o del propio *pacman*, consulte [Core utilities (Español)](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)") y [Bash (Español)](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Mantenimiento](#Mantenimiento)
    *   [1.1 Listar paquetes](#Listar_paquetes)
        *   [1.1.1 Por tamaño](#Por_tamaño)
            *   [1.1.1.1 Paquetes individuales](#Paquetes_individuales)
            *   [1.1.1.2 Paquetes y dependencias](#Paquetes_y_dependencias)
        *   [1.1.2 Por fecha](#Por_fecha)
        *   [1.1.3 No especificados en un grupo o repositorio](#No_especificados_en_un_grupo_o_repositorio)
        *   [1.1.4 Paquetes en desarrollo](#Paquetes_en_desarrollo)
    *   [1.2 Explorar paquetes](#Explorar_paquetes)
    *   [1.3 Listar archivos que pertenecen a un paquete con su correspondiente tamaño](#Listar_archivos_que_pertenecen_a_un_paquete_con_su_correspondiente_tamaño)
    *   [1.4 Identificar archivos que no pertenecen a ningún paquete](#Identificar_archivos_que_no_pertenecen_a_ningún_paquete)
    *   [1.5 Rastrear archivos sin dueño creados por paquetes](#Rastrear_archivos_sin_dueño_creados_por_paquetes)
    *   [1.6 Eliminar paquetes no utilizados (huérfanos)](#Eliminar_paquetes_no_utilizados_(huérfanos))
    *   [1.7 Eliminar todo menos los paquetes esenciales](#Eliminar_todo_menos_los_paquetes_esenciales)
    *   [1.8 Obtener la lista de dependencias de varios paquetes](#Obtener_la_lista_de_dependencias_de_varios_paquetes)
    *   [1.9 Listar los archivos de copia de seguridad modificados](#Listar_los_archivos_de_copia_de_seguridad_modificados)
    *   [1.10 Realizar copia de seguridad de la base de datos de pacman](#Realizar_copia_de_seguridad_de_la_base_de_datos_de_pacman)
    *   [1.11 Verificar registros de cambios fácilmente](#Verificar_registros_de_cambios_fácilmente)
*   [2 Instalación y recuperación](#Instalación_y_recuperación)
    *   [2.1 Instalar paquetes desde un CD/DVD o dispositivo USB](#Instalar_paquetes_desde_un_CD/DVD_o_dispositivo_USB)
    *   [2.2 Repositorio local personalizado](#Repositorio_local_personalizado)
    *   [2.3 Caché de pacman compartida en red](#Caché_de_pacman_compartida_en_red)
        *   [2.3.1 Caché de solo lectura](#Caché_de_solo_lectura)
        *   [2.3.2 Caché de solo lectura distribuido](#Caché_de_solo_lectura_distribuido)
        *   [2.3.3 Caché de lectura y escritura](#Caché_de_lectura_y_escritura)
        *   [2.3.4 De doble sentido con rsync](#De_doble_sentido_con_rsync)
        *   [2.3.5 Caché dinámico de proxy inverso usando nginx](#Caché_dinámico_de_proxy_inverso_usando_nginx)
        *   [2.3.6 Actualizar la memoria caché de *pacman* utilizando programas de sincronización](#Actualizar_la_memoria_caché_de_pacman_utilizando_programas_de_sincronización)
        *   [2.3.7 Prevenir la limpieza no deseada de la memoria caché](#Prevenir_la_limpieza_no_deseada_de_la_memoria_caché)
    *   [2.4 Reconstituir un paquete del sistema de archivos](#Reconstituir_un_paquete_del_sistema_de_archivos)
    *   [2.5 Listar paquetes instalados](#Listar_paquetes_instalados)
    *   [2.6 Instalar paquetes de una lista](#Instalar_paquetes_de_una_lista)
    *   [2.7 Listar todos los archivos modificados de los paquetes](#Listar_todos_los_archivos_modificados_de_los_paquetes)
    *   [2.8 Reinstalar todos los paquetes](#Reinstalar_todos_los_paquetes)
    *   [2.9 Restaurar la base de datos local de pacman](#Restaurar_la_base_de_datos_local_de_pacman)
    *   [2.10 Recuperar una memoria USB desde la instalación existente](#Recuperar_una_memoria_USB_desde_la_instalación_existente)
    *   [2.11 Visualizar un único archivo dentro de un archivo .pkg](#Visualizar_un_único_archivo_dentro_de_un_archivo_.pkg)
    *   [2.12 Localizar aplicaciones que usan bibliotecas de paquetes más antiguos](#Localizar_aplicaciones_que_usan_bibliotecas_de_paquetes_más_antiguos)
    *   [2.13 Instalar solo contenido en los idiomas requeridos](#Instalar_solo_contenido_en_los_idiomas_requeridos)
*   [3 Optimización](#Optimización)
    *   [3.1 Acelerar las descargas](#Acelerar_las_descargas)
        *   [3.1.1 Powerpill](#Powerpill)
        *   [3.1.2 wget](#wget)
        *   [3.1.3 aria2](#aria2)
        *   [3.1.4 Otras aplicaciones](#Otras_aplicaciones)
*   [4 Utilidades](#Utilidades)
    *   [4.1 Front-ends gráficos](#Front-ends_gráficos)

## Mantenimiento

**Nota:** en lugar de utilizar *comm* (que requiere una entrada ordenada con *sort*) en las secciones siguientes, también puede utilizar `grep -Fxf` o `grep -Fxvf`.

Véase también [System maintenance (Español)](/index.php/System_maintenance_(Espa%C3%B1ol) "System maintenance (Español)").

### Listar paquetes

Es posible que desee obtener la lista de paquetes instalados con su versión, lo cual es útil cuando se reportan errores o se discuten los paquetes instalados.

*   Lista de todos los paquetes explícitamente instalados: `pacman -Qe`.
*   Lista de todos los [package group](/index.php/Package_group "Package group") llamado `*group*`: `pacman -Sg *group*`
*   Lista de los paquetes originales instalados explícitamente (es decir, presentes en la base de datos de sincronización) que no sean dependencias directas o opcionales: `pacman -Qent` .
*   Lista de todos los paquetes externos (normalmente descargados e instalados manualmente o paquete quitados de los repositorios): `pacman -Qm`.
*   Lista de todos los paquetes originales (instalados desde la(s) base de datos de sincronización): `pacman -Qn` .
*   Lista de paquetes por su [expresión regular](https://en.wikipedia.org/wiki/es:Expresi%C3%B3n_regular "wikipedia:es:Expresión regular") también conocida como «*regex*»: `pacman -Qs *regex*` .
*   Lista de paquetes por regex con formato de salida personalizado: `expac -s "%-30n %v" *regex*` (necesita [expac](https://www.archlinux.org/packages/?name=expac)).

#### Por tamaño

Descubrir qué paquetes son más grandes puede ser útil cuando se trata de liberar espacio en el disco duro. Aquí se presentan dos opciones: o bien obtener el tamaño de los paquetes individuales, o bien obtener el tamaño de los paquetes y sus dependencias.

##### Paquetes individuales

La siguiente orden listará todos los paquetes instalados y sus tamaños particulares:

```
$ LC_ALL=C pacman -Qi | awk '/^Name/{name=$3} /^Installed Size/{print $4$5, name}' | sort -h

```

##### Paquetes y dependencias

Para listar los tamaños de los paquetes con sus dependencias,

*   Instale [expac](https://www.archlinux.org/packages/?name=expac) y ejecute `expac -H M '%m\t%n' | sort -h`.
*   Ejecute [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) con la opción `-c`.

Para listar el tamaño de descarga de varios paquetes (deje `*packages*` en blanco para listar todos los paquetes):

```
$ expac -S -H M '%k\t%n' *packages*

```

Para listar paquetes instalados explícitamente que no estén en [base](https://www.archlinux.org/packages/?name=base) ni en [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) con su tamaño y descripción:

```
$ expac -H M "%011m\t%-20n\t%10d" $(comm -23 <(pacman -Qqen | sort) <(pacman -Qqg base base-devel | sort)) | sort -n

```

Para listar los paquetes marcados para actualizar con su tamaño de descarga:

```
$ pacman -Quq|xargs expac -S -H M '%k\t%n' | sort -sh

```

#### Por fecha

Para enumerar los 20 últimos paquetes instalados con [expac](https://www.archlinux.org/packages/?name=expac), ejecute:

```
$ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20

```

O, con segundos desde la fecha (1970-01-01 UTC):

```
$ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20

```

#### No especificados en un grupo o repositorio

**Nota:** para obtener una lista de paquetes instalados como dependencias pero que ya no son necesarios para ningún paquete instalado, consulte [#Eliminar paquetes no utilizados (huérfanos)](#Eliminar_paquetes_no_utilizados_(huérfanos)).

Listado de los paquetes explícitamente instalados que no están en los grupos [base](https://www.archlinux.org/packages/?name=base) o [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/):

```
$ comm -23 <(pacman -Qeq | sort) <(pacman -Qgq base base-devel | sort)

```

Listado de todos los paquetes instalados no requeridos por otros paquetes y que no estén en los grupos [base](https://www.archlinux.org/packages/?name=base) o [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) :

```
$ comm -23 <(pacman -Qqt | sort) <(pacman -Sqg base base-devel | sort)

```

Como arriba, pero con descripciones:

```
$ expac -HM '%-20n\t%10d' $(comm -23 <(pacman -Qqt | sort) <(pacman -Qqg base base-devel | sort))

```

Listado de todos los paquetes instalados que *no* están en el repositorio especificado como *repo_name*

```
$ comm -23 <(pacman -Qq | sort) <(pacman -Slq *repo_name* | sort)

```

Listado de todos los paquetes instalados que están en el repositorio repo_name :

```
$ comm -12 <(pacman -Qq | sort) <(pacman -Slq *repo_name* | sort)

```

Listado de todos los paquetes presentes en la ISO de Arch Linux que no están en el grupo base:

```
$ comm -23 <(curl https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) <(pacman -Qqg base | sort)

```

#### Paquetes en desarrollo

Para listar todos lo paquetes *development/unstable*, ejecute:

```
$ pacman -Qq | grep -Ee '-(bzr|cvs|darcs|git|hg|svn)$'

```

### Explorar paquetes

Para explorar todos los paquetes instalados con una visualización instantánea de cada paquete:

```
 $ pacman -Qq | fzf --preview 'pacman -Qil {}' --layout=reverse --bind 'enter:execute(pacman -Qil {} | less)'

```

Esto utiliza [fzf](/index.php/Fzf_(Espa%C3%B1ol) "Fzf (Español)") para presentar una vista de dos paneles donde se muestran todos los paquetes con la información de cada cual a la derecha.

Introduzca letras para filtrar la lista de paquetes; use las teclas de flecha (o `Ctrl-j`/`Ctrl-k`) para desplazarse; presione `Intro` para ver la información del paquete *señalado*.

### Listar archivos que pertenecen a un paquete con su correspondiente tamaño

Esto podría ser útil si descubrió que un paquete específico utiliza una gran cantidad de espacio y desea saber qué archivos lo componen.

```
$ pacman -Qlq *package* | grep -v '/$' | xargs du -h | sort -h

```

### Identificar archivos que no pertenecen a ningún paquete

Si su sistema tiene archivos huérfanos que no pertenecen a ningún paquete (un caso común si no [usa el gestor de paquetes para instalar software](/index.php/Enhance_system_stability#Use_the_package_manager_to_install_software "Enhance system stability")), es posible que desee encontrar dichos archivos para limpiarlos.

Un método consiste en utilizar `# pacreport --unowned-files` del paquete [pacutils](https://www.archlinux.org/packages/?name=pacutils) que incluirá una lista de los archivos sin dueño entre otros detalles.

Otro método es enumerar todos los archivos de interés y compararlos con pacman:

```
# find /etc /usr /opt /var | LC_ALL=C pacman -Qqo - 2>&1 > /dev/null | cut -d ' ' -f 5-

```

**Sugerencia:** el script [lostfiles](https://www.archlinux.org/packages/?name=lostfiles) realiza pasos similares, pero también incluye una extensa lista negra para eliminar falsos positivos comunes de la salida.

### Rastrear archivos sin dueño creados por paquetes

La mayoría de los sistemas recolectarán lentamente diversos archivos [fantasmas](http://ftp.rpm.org/max-rpm/s1-rpm-inside-files-list-directives.html#S3-RPM-INSIDE-FLIST-GHOST-DIRECTIVE) tales como archivos de estado, registros, índices, etc. durante el curso de la operación habitual.

`pacreport` de [pacutils](https://www.archlinux.org/packages/?name=pacutils) se puede usar para rastrear estos archivos y sus asociaciones a través de `/etc/pacreport.conf` (vea [pacreport(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacreport.1#FILES)).

Un ejemplo podría ser algo parecido a esto (abreviado):

 `/etc/pacreport.conf` 
```
[Options]
IgnoreUnowned = usr/share/applications/mimeinfo.cache

[PkgIgnoreUnowned]
alsa-utils = var/lib/alsa/asound.state
bluez = var/lib/bluetooth
ca-certificates = etc/ca-certificates/trust-source/*
dbus = var/lib/dbus/machine-id
glibc = etc/ld.so.cache
grub = boot/grub/*
linux = boot/initramfs-linux.img
pacman = var/lib/pacman/local
update-mime-database = usr/share/mime/magic

```

Luego, cuando utilice `# pacreport --unowned-files`, todos los archivos sin propietario se mostrarán si el paquete asociado ya no está instalado (o si se han creado nuevos archivos).

Además, [aconfmgr](https://github.com/CyberShadow/aconfmgr) ([aconfmgr-git](https://aur.archlinux.org/packages/aconfmgr-git/)) permite rastrear archivos modificados y huérfanos usando un script de configuración.

### Eliminar paquetes no utilizados (huérfanos)

Para eliminar de forma *recursiva* los paquetes huérfanos y sus archivos de configuración:

```
# pacman -Rns $(pacman -Qtdq)

```

Si no se encontraron paquetes huérfanos, aparecerán errores de pacman con `error: no targets specified`. Esto se espera ya que no se pasaron argumentos a `pacman -Rns`.

**Nota:** los argumentos `-Qt` enumeran solo huérfanos verdaderos. Para incluir paquetes que son *opcionalmente* requeridos por otro paquete, pase el indicador `-t` dos veces (*esto es*, `-Qtt`).

### Eliminar todo menos los paquetes esenciales

Si alguna vez es necesario eliminar todos los paquetes, excepto los paquetes esenciales, un método es establecer el motivo de instalación de los no esenciales como dependencia y luego eliminar todas las dependencias innecesarias.

Primero, para todos los paquetes instalados «como explícitamente», cambie su razón de instalación a «como dependencia»:

```
# pacman -D --asdeps $(pacman -Qqe)

```

Luego, cambie el motivo de instalación a instalados «como explícitamente» para los paquetes esenciales solamente, esto es, aquellos que **no** desea eliminar, para apuntarlos:

```
# pacman -D --asexplicit base linux linux-firmware

```

**Nota:**

*   Se pueden añadir paquetes adicionales a la orden anterior para evitar que se eliminen. Consulte [Installation guide (Español)#Instalar paquetes esenciales](/index.php/Installation_guide_(Espa%C3%B1ol)#Instalar_paquetes_esenciales "Installation guide (Español)") para obtener más información sobre otros paquetes que pueden ser necesarios para un sistema base completamente funcional.
*   Esta orden también seleccionará el paquete del gestor de arranque para su eliminación. El sistema aún debería ser arrancable, pero los parámetros de arranque podrían no ser modificables sin él.

Finalmente, siga las instrucciones de [#Eliminar paquetes no utilizados (huérfanos)](#Eliminar_paquetes_no_utilizados_(huérfanos)) para eliminar todos los paquetes que tengan una razón de instalación «como dependencia».

### Obtener la lista de dependencias de varios paquetes

Las dependencias se ordenan alfabéticamente y las repetidas se eliminan.

**Nota:** para mostrar solo el árbol de paquetes locales instalados, utilice `pacman -Qi`.

```
$ LC_ALL=C pacman -Si *packages* | awk -F'[:<=>]' '/^Depends/ {print $2}' | xargs -n1 | sort -u

```

Como alternativa puede utilizar [expac](https://www.archlinux.org/packages/?name=expac):

```
$ expac -l '
' %E -S *packages* | sort -u

```

### Listar los archivos de copia de seguridad modificados

Si desea realizar una copia de seguridad de los archivos de configuración del sistema, puede copiar todos los archivos en `/etc/`, pero normalmente solo le interesan los ficheros que ha modificado. Los archivos de [copias de seguridad](/index.php/Pacman_(Espa%C3%B1ol)/Pacnew_and_Pacsave_(Espa%C3%B1ol)#Copias_de_seguridad_de_archivos_de_paquetes "Pacman (Español)/Pacnew and Pacsave (Español)") se puede ver con la siguiente orden:

```
# pacman -Qii | awk '/^MODIFIED/ {print $2}'

```

Ejecutar esta orden con permisos de root asegurará que los archivos solo pueden ser leídos por root (por ejemplo `/etc/sudoers`) están incluidos en la salida.

**Sugerencia:** vea [#Listar todos los archivos modificados de los paquetes](#Listar_todos_los_archivos_modificados_de_los_paquetes) para enumerar todos los archivos modificados que conoce *pacman*, no solo los archivos de respaldo.

### Realizar copia de seguridad de la base de datos de pacman

La siguiente orden se puede usar para realizar una copia de seguridad de la base de datos local de *pacman* :

```
$ tar -cjf pacman_database.tar.bz2 /var/lib/pacman/local

```

Almacene la copia de seguridad de la base de datos de *pacman* en uno o más medios sin conexión, como una memoria USB, disco duro externo o CD-R.

La base de datos se puede restaurar moviendo el archivo `pacman_database.tar.bz2` en el `/` directorio y ejecutando la siguiente orden :

```
# tar -xjvf pacman_database.tar.bz2

```

**Nota:** si los archivos de la base de datos *pacman* están dañados y no hay un archivo de respaldo disponible, existe la esperanza de reconstruir la base de datos de *pacman*. Consulte [Pacman (Español)/Restore local database (Español)](/index.php/Pacman_(Espa%C3%B1ol)/Restore_local_database_(Espa%C3%B1ol) "Pacman (Español)/Restore local database (Español)").

**Sugerencia:** el paquete [pakbak-git](https://aur.archlinux.org/packages/pakbak-git/) proporciona un script y un servicio de [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") para automatizar la tarea. La configuración es posible en `/etc/pakbak.conf`.

### Verificar registros de cambios fácilmente

Cuando los mantenedores actualizan los paquetes, las confirmaciones a menudo se comentan de manera útil. Los usuarios pueden comprobarlo rápidamente desde la línea de órdenes instalando [pacolog](https://aur.archlinux.org/packages/pacolog/). Esta utilidad enumera mensajes de confirmación recientes para paquetes de los repositorios oficiales o en AUR, mediante el uso de `pacolog <package>`.

## Instalación y recuperación

Formas alternativas de obtener y restaurar paquetes.

### Instalar paquetes desde un CD/DVD o dispositivo USB

Para descargar paquetes o grupos de paquetes:

```
# cd ~/Packages
# pacman -Syw base base-devel grub-bios xorg gimp --cachedir .
# repo-add ./custom.db.tar.gz ./*

```

A continuación puede grabar la carpeta «Packages» en un CD/DVD o transferir a un dispositivo USB, disco duro externo, etc.

Para instalar:

**1.** Monte los medios:

```
# mkdir /mnt/repo
# mount /dev/sr0 /mnt/repo    #Para un disco CD/DVD.
# mount /dev/sdxY /mnt/repo   #Para una memoria USB.

```

**2.** Edite `pacman.conf` y agrege este repositorio *por encima* de los demás (es decir, extra, core, etc.). Esto es importante. No se limite a descomentar el que está en la parte inferior. De esta manera se asegura que los archivos del CD/DVD/USB tengan prioridad sobre los de los repositorios estándar.:

 `/etc/pacman.conf` 
```
[custom]
SigLevel = PackageRequired
Server = file:///mnt/repo/Packages
```

**3.** Finalmente, sincronice la base de datos de *pacman* para poder usar el nuevo repositorio:

```
# pacman -Syu

```

### Repositorio local personalizado

Utilice el script *repo-add* incluido con *pacman* para generar una base de datos para un repositorio personal. Utilize `repo-add --help` para conocer más detalles sobre su uso.

A package database is a tar file, optionally compressed. Valid extensions are *.db* or *.files* followed by an archive extension of *.tar*, *.tar.gz*, *.tar.bz2*, *.tar.xz*, *.tar.zst*, or *.tar.Z*. The file does not need to exist, but all parent directories must exist.

Para agregar un nuevo paquete a la base de datos o para reemplazar la versión anterior de un paquete existente en la base de datos, ejecute:

```
$ repo-add */path/to/repo.db.tar.gz /path/to/package-1.0-1-x86_64.pkg.tar.xz*

```

La base de datos y los paquetes no necesitan estar en el mismo directorio cuando se utiliza *repo-add*, pero tenga en cuenta que cuando se usa *pacman* con esa base de datos, deben estar juntos. Almacenar todos los paquetes construidos para ser incluidos en el repositorio en un directorio también permite usar la expansión shell glob para añadir o actualizar múltiples paquetes a la vez:

```
$ repo-add */path/to/repo.db.tar.gz /path/to/*.pkg.tar.xz*

```

**Advertencia:** *repo-add* agrega las entradas a la base de datos en el mismo orden que se pasó en la línea de órdenes. Si se trata de varias versiones del mismo paquete, se debe tener cuidado para asegurarse de que se agregue la versión correcta al final. En particular, tenga en cuenta que el orden léxico utilizado por el intérprete de órdenes depende de la configuración regional y difiere de la [vercmp](https://www.archlinux.org/pacman/vercmp.8.html) ordenación utilizada por *pacman*.

If you are looking to support multiple architectures then precautions should be taken to prevent errors from occurring. Each architecture should have its own directory tree:

 `$ tree ~/customrepo/ | sed "s/$(uname -m)/<arch>/g"` 
```
/home/archie/customrepo/
└── <arch>
    ├── customrepo.db -> customrepo.db.tar.xz
    ├── customrepo.db.tar.xz
    ├── customrepo.files -> customrepo.files.tar.xz
    ├── customrepo.files.tar.xz
    └── personal-website-git-b99cce0-1-<arch>.pkg.tar.xz

1 directory, 5 files

```

El ejecutable *repo-add* verifica si el paquete es apropiado. Si este no es el caso, se encontrará con mensajes de error similares a este:

```
==> ERROR: '/home/archie/customrepo/<arch>/foo-<arch>.pkg.tar.xz' does not have a valid database archive extension.

```

*repo-remove* se usa para eliminar paquetes de la base de datos, excepto si el nombre del paquete se especifica con la siguiente orden.

```
$ repo-remove */path/to/repo.db.tar.gz pkgname*

```

Una vez que se haya creado la base de datos del repositorio local, agregue el repositorio a `pacman.conf` para cada sistema que usará el repositorio. Un ejemplo de repositorio personalizado está en `pacman.conf`. El nombre del repositorio es el nombre de archivo de la base de datos con la extensión de archivo omitida. En el caso del ejemplo anterior, el nombre del repositorio sería simplemente *repo*. Haga referencia a la ubicación del repositorio utilizando un `file://` url, o por FTP usando [ftp://localhost/path/to/directory](ftp://localhost/path/to/directory).

Si lo desea, añada el repositorio personalizado al directorio de la [lista de repositorios no oficiales de usuario](/index.php/Unofficial_user_repositories "Unofficial user repositories"), para que la comunidad pueda beneficiarse de ello.

### Caché de pacman compartida en red

Si ejecuta varios sistemas de Arch en su LAN, puede compartir paquetes para que pueda disminuir considerablemente los tiempos de descarga. Tenga en cuenta que no debe compartir entre diferentes arquitecturas (es decir, i686 y x86_64) o se encontrará con problemas.

#### Caché de solo lectura

Si está buscando una solución rápida, puede simplemente ejecutar un servidor web independiente que otros ordenadores pueden utilizar como primer servidor de réplica:

```
# ln -s /var/lib/pacman/sync/*.db /var/cache/pacman/pkg
$ sudo -u http darkhttpd /var/cache/pacman/pkg --no-server-id

```

También podría ejecutar darkhttpd como un servicio systemd para su comodidad. Basta agregar este servidor en la parte superior del archivo `/etc/pacman.d/mirrorlist` en equipos clientes con `Server = http://mymirror:8080`. Asegúrese de mantener su servidor de réplica actualizado.

Si ya está ejecutando un servidor web para algún otro propósito, es posible que desee reutilizarlo como su servidor de repositorio local en lugar de darkhttpd. Por ejemplo, digamos que ya tiene un servidor en un sitio con [nginx](/index.php/Nginx "Nginx"), puede agregar una sección para que otro servidor de nginx escuche en el puerto 8080:

 `/etc/nginx/nginx.conf` 
```
server {
    listen 8080;
    root /var/cache/pacman/pkg;
    server_name myarchrepo.localdomain;
    try_files $uri $uri/;
}

```

Recuerde reiniciar nginx después de hacer este cambio.

Sea cual sea el servidor web que utilice, recuerde abrir el puerto 8080 para el tráfico local (y probablemente desee negar todo lo que no sea local), así que agregue una regla como la siguiente a [iptables (Español)](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)"):

 `/etc/iptables/iptables.rules` 
```
-A TCP -s 192.168.0.0/16 -p tcp -m tcp --dport 8080 -j ACCEPT

```

Recuerde reiniciar iptables después de hacer este cambio.

#### Caché de solo lectura distribuido

Existen herramientas específicas de Arch para descubrir automáticamente otros equipos de la red que ofrecen una caché de paquetes. Intente [pacserve](/index.php/Pacserve "Pacserve"), [pkgdistcache](https://aur.archlinux.org/packages/pkgdistcache/), o [paclan](https://aur.archlinux.org/packages/paclan/). pkgdistcache utilize Avahi en lugar de UDP el cual puede funcionar mejor en ciertas redes domésticas que enrutan en lugar de tender un puente entre WiFi y Ethernet .

Históricamente, teníamos [PkgD](https://bbs.archlinux.org/viewtopic.php?id=64391) y [multipkg](https://github.com/toofishes/multipkg), pero ya no se mantienen.

#### Caché de lectura y escritura

Para compartir paquetes entre varios equipos, simplemente comparta `/var/cache/pacman/` utilizando cualquier protocolo de montaje basado en red. Esta sección muestra cómo usar [shfs](/index.php/Shfs "Shfs") o [SSHFS (Español)](/index.php/SSHFS_(Espa%C3%B1ol) "SSHFS (Español)") para compartir una caché de paquetes más los directorios de biblioteca relacionados entre múltiples ordenadores de la misma red local. Tenga en cuenta que una caché compartida en red puede ser lenta dependiendo de la elección del sistema de archivos, entre otros factores.

Primero, instale cualquier paquete de sistema de ficheros que soporte la red: [shfs-utils](https://www.archlinux.org/packages/?name=shfs-utils), [sshfs](https://www.archlinux.org/packages/?name=sshfs), [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs), [samba](https://www.archlinux.org/packages/?name=samba) o [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils).

**Sugerencia:**

*   Para usar *sshfs* o *shfs*, considere leer [Using SSH Keys (Español)](/index.php/Using_SSH_Keys_(Espa%C3%B1ol) "Using SSH Keys (Español)").
*   Por defecto, *smbfs* no sirve nombres de archivo que contengan dos puntos, lo que hace que el cliente descargue de nuevo el paquete otra vez. Para evitarlo, utilice la opción de montaje `mapchars` en el cliente.

Luego, para compartir los paquetes actuales, monte `/var/cache/pacman/pkg` del servidor a `/var/cache/pacman/pkg` en cada máquina cliente.

**Advertencia:** no cree un enlace simbólico de `/var/cache/pacman/pkg` ni de ninguno de sus directorios precedentes (por ejemplo, de `/var`). *Pacman* espera que estos sean directorios. Cuando *pacman* se reinstale o actualice, eliminará los enlaces simbólicos y creará directorios vacíos. Sin embargo, durante la operación *pacman* se basará en algunos archivos que residen allí, rompiendo así el proceso de actualización. Consulte [FS#50298](https://bugs.archlinux.org/task/50298) para más detalles.

#### De doble sentido con rsync

Otro enfoque en un entorno local es [rsync (Español)](/index.php/Rsync_(Espa%C3%B1ol) "Rsync (Español)"). Elija un servidor para el almacenamiento caché y active el demonio [Rsync (Español)#Demonio rsync](/index.php/Rsync_(Espa%C3%B1ol)#Demonio_rsync "Rsync (Español)"). En los clientes, sincronice bidireccionalmente con este recurso compartido mediante el protocolo rsync. Los nombres de archivo que contienen dos puntos no son un problema para el protocolo rsync.

Ejemplo para un cliente, utilizando `uname -m` dentro del nombre compartido asegura una arquitectura dependiente sync:

```
 # rsync rsync://server/share_$(uname -m)/ /var/cache/pacman/pkg/ ...
 # pacman ...
 # paccache ...
 # rsync /var/cache/pacman/pkg/ rsync://server/share_$(uname -m)/  ...

```

#### Caché dinámico de proxy inverso usando nginx

[nginx](/index.php/Nginx "Nginx") se puede usar para enviar solicitudes de paquetes proxy a servidores de réplicas ascendentes oficiales y almacenar los resultados en el disco local. Todas las solicitudes posteriores para ese paquete serán atendidas directamente desde la memoria caché local, minimizando la cantidad de tráfico de Internet necesaria para actualizar una gran cantidad de ordenadores.

En este ejemplo, el servidor de caché se ejecutará en `http://cache.domain.example:8080/` y almacenará los paquetes enn `/srv/http/pacman-cache/`.

Instale [nginx](/index.php/Nginx "Nginx") en el ordenador que vaya a alojar la caché. Cree el directorio para el caché y ajuste los permisos para que nginx pueda escribir archivos en él:

```
# mkdir /srv/http/pacman-cache
# chown http:http /srv/http/pacman-cache

```

Utilice la [nginx pacman cache config](https://github.com/nastasie-octavian/nginx_pacman_cache_config/blob/87d4897b8fa37e70da4238d7074c639c041daf39/nginx.conf) como punto de partida para `/etc/nginx/nginx.conf`. Compruebe que la directiva `resolver` funciona para sus necesidades. En los bloques del servidor ascendente, configure las directivas `proxy_pass` con las direcciones de los espejos oficiales, vea ejemplos en el archivo de configuración sobre el formato esperado. Una vez que esté satisfecho con el archivo de configuración [inicie y active nginx](/index.php/Nginx#Running "Nginx").

Para usar la caché, cada ordenador Arch Linux (incluida la que aloja el caché) debe tener la siguiente línea en la parte superior del archivo `mirrorlist` file:

 `/etc/pacman.d/mirrorlist` 
```
Server = http://cache.domain.local:8080/$repo/os/$arch
...

```

**Nota:** habrá que crear un método para borrar paquetes viejos, ya que este directorio caché continuará creciendo con el tiempo. `paccache` (que se incluye con *pacman*) se puede utilizar para automatizarlo , utilizando criterios de retención de su elección. Por ejemplo, `find /srv/http/pacman-cache/ -type d -exec paccache -v -r -k 2 -c {} \;` mantendrá las dos últimas versiones de los paquetes en su directorio caché.

#### Actualizar la memoria caché de *pacman* utilizando programas de sincronización

Utilice [Syncthing](/index.php/Syncthing "Syncthing") o [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync") para sincronizar las carpetas de la caché de «pacman» (esto es, `/var/cache/pacman/pkg`).

#### Prevenir la limpieza no deseada de la memoria caché

Por defecto, `pacman -Sc` elimina los paquetes tarballs de la memoria caché que corresponden a paquetes que no están instalados en el equipo en el que se emitió la orden. Dado que *pacman* no puede predecir qué paquetes están instalados en todos los equipos que comparten la memoria caché, acabará eliminando archivos que no debería.

Para limpiar la memoria de caché de forma que solo se eliminen los tarballs *obsoletos*, añada esta entrada en el archivo `[options]` en la sección de `/etc/pacman.conf`:

```
CleanMethod = KeepCurrent

```

### Reconstituir un paquete del sistema de archivos

Para reconstituir un paquete desde el sistema de archivos, utilice [fakepkg](https://aur.archlinux.org/packages/fakepkg/). Los archivos del sistema se toman tal como están, por lo tanto, cualquier modificación estará presente en el paquete ensamblado. Por lo tanto, se desaconseja la distribución del paquete reconstituido; vea [ABS (Español)](/index.php/ABS_(Espa%C3%B1ol) "ABS (Español)") y [Arch Linux Archive (Español)](/index.php/Arch_Linux_Archive_(Espa%C3%B1ol) "Arch Linux Archive (Español)") para las alternativas.

### Listar paquetes instalados

Mantener una lista de paquetes instalados explícitamente puede ser útil para acelerar la instalación en un nuevo sistema:

```
$ pacman -Qqe > pkglist.txt

```

**Nota:**

*   Con la opción `-t`, no se mencionan los paquetes ya requeridos por otros paquetes instalados explícitamente. Si se vuelve a instalar desde esta lista, se instalarán pero solo como dependencias.
*   Con la opción `-n`, los paquetes foráneos (por ejemplo, los de [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)")) se omitirán de la lista.
*   Utilice `comm -13 <(pacman -Qqdt | sort) < (pacman -Qqdtt | sort) > optdeplist.txt` también para crear una lista de las dependencias opcionales instaladas que se pueden reinstalar con `--asdeps`.
*   Utilice `pacman -Qqem > foreignpkglist.txt` para crear la lista de paquetes de AUR y otros paquetes foráneos que se hayan instalado explícitamente.

Para mantener una lista actualizada de paquetes instalados explícitamente (por ejemplo, en combinación con una versión de `/etc/`), puede configurar un [hook](/index.php/Pacman_(Espa%C3%B1ol)#Hooks "Pacman (Español)"). Ejemplo:

```
[Trigger]
Operation = Install
Operation = Remove
Type = Package
Target = *

[Action]
When = PostTransaction
Exec = /bin/sh -c '/usr/bin/pacman -Qqe > /etc/pkglist.txt'

```

### Instalar paquetes de una lista

Para instalar paquetes desde una lista de paquetes previamente guardada, al tiempo que no se reinstalan los paquetes que ya estén actualizados, ejecute:

```
# pacman -S --needed - < pkglist.txt

```

Sin embargo, es probable que en la lista se encuentren paquetes foráneos como los procedentes de AUR o los instalados localmente. Para filtrar de la lista los paquetes externos, la línea de órdenes anterior se puede enriquecer de la siguiente manera:

```
# pacman -S --needed $(comm -12 <(pacman -Slq | sort) <(sort pkglist.txt))

```

Finalmente, para asegurarse de que los paquetes instalados del sistema coincidan con la lista y se eliminen todos los paquetes que no se mencionan en ella:

```
# pacman -Rsu $(comm -23 <(pacman -Qq | sort) <(sort pkglist.txt))

```

**Sugerencia:** estas tareas pueden ser automatizadas. Consulte [bacpac](https://aur.archlinux.org/packages/bacpac/), [packup](https://aur.archlinux.org/packages/packup/), [pacmanity](https://aur.archlinux.org/packages/pacmanity/), y [pug](https://aur.archlinux.org/packages/pug/) para obtener ejemplos.

### Listar todos los archivos modificados de los paquetes

Si sospecha que hay corrupción de archivos (por ejemplo, por fallos de software o hardware), pero no está seguro de si los archivos se corrompieron, es posible que desee compararlos con las sumas de hash de los paquetes. Esto se puede hacer con [pacutils](https://www.archlinux.org/packages/?name=pacutils):

```
# paccheck --md5sum --quiet

```

Para la recuperación de la base de datos, véase [#Restaurar la base de datos local de pacman](#Restaurar_la_base_de_datos_local_de_pacman). Los archivos `mtree` también pueden ser [extraído como `.MTREE` de los respectivos archivos del paquete](#Visualizar_un_único_archivo_dentro_de_un_archivo_.pkg).

**Nota:** esto **no** debe usarse cuando se sospeche de cambios maliciosos. En este caso, se recomiendan precauciones de seguridad, como usar un medio live o una fuente independiente para comprobar las sumas de hash.

### Reinstalar todos los paquetes

Para reinstalar todos los paquetes originales, utilice:

```
# pacman -Qqn | pacman -S -

```

Los paquetes externos (AUR) deben reinstalarse por separado; puede listarlos con `pacman -Qmq`.

*Pacman* conserva el [motivo de la instalación](/index.php/Pacman_(Espa%C3%B1ol)#Motivo_de_la_instalación "Pacman (Español)") por defecto.

### Restaurar la base de datos local de pacman

Véase [Pacman (Español)/Restore local database (Español)](/index.php/Pacman_(Espa%C3%B1ol)/Restore_local_database_(Espa%C3%B1ol) "Pacman (Español)/Restore local database (Español)").

### Recuperar una memoria USB desde la instalación existente

Si tiene Arch instalado en una memoria USB y se las arregla para estropearla ( por ejemplo, quitándola mientras todavía está siendo escrita), entonces es posible reinstalar todos los paquetes y esperar que vuelva a funcionar (suponiendo que la memoria USB está montada en `/newarch`)

```
# pacman -S $(pacman -Qq --dbpath /newarch/var/lib/pacman) --root /newarch --dbpath /newarch/var/lib/pacman

```

### Visualizar un único archivo dentro de un archivo .pkg

Por ejemplo, si desea ver el contenido de `/etc/systemd/logind.conf` suministrado dentro del paquete [systemd](https://www.archlinux.org/packages/?name=systemd):

```
$ tar -xOf /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz etc/systemd/logind.conf

```

O puede usar [vim](https://www.archlinux.org/packages/?name=vim) para explorar el archivo:

```
$ vim /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz

```

### Localizar aplicaciones que usan bibliotecas de paquetes más antiguos

Incluso después de haber instalado un paquete, los programas existentes que se ejecutan desde hace mucho tiempo (como los demonios y los servidores) siguen utilizando código de antiguas bibliotecas.Y es una mala idea dejar que estos programas se ejecuten si la biblioteca anterior contiene un error de seguridad.

Esta es una manera de encontrar todos los programas que usan código de paquetes antiguos:

```
# lsof +c 0 | grep -w DEL | awk '1 { print $1 ": " $NF }' | sort -u

```

Imprimirá el nombre del programa en ejecución y la biblioteca antigua que se eliminó o reemplazó con contenido más reciente.

### Instalar solo contenido en los idiomas requeridos

Muchos paquetes intentan instalar documentación y traducciones en varios idiomas. Algunos programas están diseñados para eliminar dichos archivos innecesarios, como [localepurge](https://aur.archlinux.org/packages/localepurge/), que se ejecuta después de instalar un paquete para eliminar los archivos locales innecesarios. Un enfoque más directo se proporcina a través de la directiva `NoExtract` en `pacman.conf`, que evita que estos archivos se instalen. El siguiente ejemplo instala archivos en inglés (US) o ninguno:

**Warning:** Algunos usuarios notaron que eliminar configuraciones regionales ha dado [consecuencias no deseadas](https://wiki.archlinux.org/index.php?title=Talk:Pacman&oldid=460285#Dangerous_NoExtract_example), incluso bajo [Xorg](https://bbs.archlinux.org/viewtopic.php?id=250846).

El siguiente ejemplo instala archivos en inglés (US) o ninguno:

 `/etc/pacman.conf` 
```
NoExtract = usr/share/help/* !usr/share/help/en*
NoExtract = usr/share/gtk-doc/html/*
NoExtract = usr/share/locale/* usr/share/X11/locale/* usr/share/i18n/* opt/google/chrome/locales/* !usr/share/X11/locale/C/*
NoExtract = !*locale*/en*/* !usr/share/i18n/charmaps/UTF-8.gz !usr/share/*locale*/locale.*
NoExtract = !usr/share/*locales/en_?? !usr/share/*locales/i18n !usr/share/*locales/iso*
NoExtract = !usr/share/*locales/trans*
NoExtract = usr/share/qt4/translations/*
NoExtract = usr/share/man/* !usr/share/man/man*
NoExtract = usr/share/vim/vim*/lang/*
NoExtract = usr/lib/libreoffice/help/en-US/*
```

## Optimización

### Acelerar las descargas

**Nota:** si las velocidades de descarga se han reducido asegúrese de que está utilizando uno de los muchos [servidores de réplicas](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)") y no ftp.archlinux.org, que está [saturado desde marzo de 2007](https://www.archlinux.org/news/302/).

Al descargar paquetes *pacman* usa los servidores de réplicas en el orden en que están en `/etc/pacman.d/mirrorlist`. Sin embargo, los servidores de réplicas que está en la parte superior de la lista, pueden no ser los más rápido para usted. Para seleccionar los servidores de réplicas más rápidos, consulte [Mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)").

La velocidad de *pacman* en la descarga de paquetes también puede ser mejorada mediante el uso de una aplicación diferente para descargar paquetes, en lugar del descargador de archivos integrado de *pacman*.

En todos los casos, asegúrese de tener la última *pacman* antes de hacer cualquier modificación.

```
 # pacman -Syu

```

#### Powerpill

[Powerpill (Español)](/index.php/Powerpill_(Espa%C3%B1ol) "Powerpill (Español)") es un wrapper de *pacman* que utiliza la descarga paralela y segmentada para tratar de acelerar las descargas de *pacman*.

#### wget

Esto también es muy útil si necesita configuraciones proxy más potentes que las capacidades incorporadas de *pacman*.

Para usar `wget`, primero [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [wget](https://www.archlinux.org/packages/?name=wget) y luego modifique `/etc/pacman.conf` descomentando la siguiente línea en la sección `[options]` :

```
XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u

```

En lugar de descomentar los parámetros de `wget` en `/etc/pacman.conf`, también puede modificar el archivo de configuración de `wget` directamente, el archivo de todo el sistema es `/etc/wgetrc`, o `$HOME/.wgetrc` para el usuario.

#### aria2

[aria2](/index.php/Aria2 "Aria2") es una utilidad de descarga ligera con soporte para HTTP/HTTPS y transferencias directas continuas y segmentadas. aria2 permite múltiples y simultáneas conexiones HTTP/HTTPS y FTP a un servidor de réplica de Arch, lo que debería dar como resultado un aumento en las velocidades de descarga para la obtención de archivos y paquetes.

**Nota:** el uso de aria2c en XferCommand de *pacman* **no** dará lugar a descargas paralelas de varios paquetes. *Pacman* invoca el parámetro XferCommand con un solo paquete a la vez y espera a que se complete antes de invocar el siguiente. Para descargar varios paquetes en paralelo, vea [Powerpill (Español)](/index.php/Powerpill_(Espa%C3%B1ol) "Powerpill (Español)").

Instale [aria2](https://www.archlinux.org/packages/?name=aria2) y luego edite `/etc/pacman.conf` agregando la siguiente línea a la sección `[options]`:

```
XferCommand = /usr/bin/aria2c --allow-overwrite=true --continue=true --file-allocation=none --log-level=error --max-tries=2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 --timeout=5 --dir=/ --out %o %u

```

**Sugerencia:** [esta configuración alternativa para usar *pacman* con aria2](https://bbs.archlinux.org/viewtopic.php?pid=1491879#p1491879) intenta simplificar sus ajustes y añade más opciones de configuración.

Vea [OPTIONS](http://aria2.sourceforge.net/manual/en/html/aria2c.html#options) en [aria2c(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aria2c.1) para usar las configuraciones de aria2\.

*   `-d, --dir`: el directorio para almacenar los archivo(s) descargado según lo especificado por *pacman* .
*   `-o, --out`: el nombre(s) del archivo(s) de salida descargado(s).
*   `%o`: la variable que representa el nombre(s) del archivo(s) local especificado por *pacman*.
*   `%u`: la variable que representa la URL de descarga especificada por *pacman*.

#### Otras aplicaciones

Hay otras aplicaciones de descarga que puede usar con *pacman* . Aquí están, y su configuración asociada de XferCommand:

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`
*   `hget`: `XferCommand = /usr/bin/hget %u -n 2 -skip-tls false`

(lea la [documentación en la página del proyecto de Github](https://github.com/huydx/hget) para mas información)

## Utilidades

*   **Lostfiles** — Script que identifica archivos que no son propiedad de ningún paquete.

	[https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [lostfiles](https://www.archlinux.org/packages/?name=lostfiles)

*   **Pacmatic** — [Wrapper](https://en.wikipedia.org/wiki/es:Wrapper "wikipedia:es:Wrapper") de *pacman* para comprobar noticias de Arch antes de la actualización, evitar actualizaciones parciales y advertir sobre cambios en el archivo de configuración.

	[http://kmkeen.com/pacmatic](http://kmkeen.com/pacmatic) || [pacmatic](https://www.archlinux.org/packages/?name=pacmatic)

*   **pacutils** — Biblioteca de ayuda para programas basados en libalpm.

	[https://github.com/andrewgregory/pacutils](https://github.com/andrewgregory/pacutils) || [pacutils](https://www.archlinux.org/packages/?name=pacutils)

*   **[pkgfile](/index.php/Pkgfile "Pkgfile")** — Herramienta para buscar archivos en paquetes.

	[http://github.com/falconindy/pkgfile](http://github.com/falconindy/pkgfile) || [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)

*   **pkgtools** — Colección de scripts para los paquetes de Arch Linux.

	[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)

*   **pkgtop** — Gestor de paquetes interactivo y monitor de recursos diseñado para GNU/Linux.

	[https://github.com/orhun/pkgtop](https://github.com/orhun/pkgtop) || [pkgtop-git](https://aur.archlinux.org/packages/pkgtop-git/)

*   **[Powerpill](/index.php/Powerpill "Powerpill")** — Utiliza descargas paralelas y segmentadas a través de [aria2](/index.php/Aria2 "Aria2") y [Reflector](/index.php/Reflector "Reflector") para intentar acelerar las descargas de *pacman*.

	[https://xyne.archlinux.ca/projects/powerpill/](https://xyne.archlinux.ca/projects/powerpill/) || [powerpill](https://aur.archlinux.org/packages/powerpill/)

*   **repoctl** — Herramienta para ayudar a gestionar repositorios locales.

	[https://github.com/cassava/repoctl](https://github.com/cassava/repoctl) || [repoctl](https://aur.archlinux.org/packages/repoctl/)

*   **repose** — Una herramienta de construcción de repositorios Arch Linux.

	[https://github.com/vodik/repose](https://github.com/vodik/repose) || [repose](https://www.archlinux.org/packages/?name=repose)

*   **[snap-pac](/index.php/Snapper#Wrapping_pacman_transactions_in_snapshots "Snapper")** — Hace que *pacman* utilice automáticamente *snapper* para crear instantáneas previas y posteriores como YaST de openSUSE.

	[https://github.com/wesbarnett/snap-pac](https://github.com/wesbarnett/snap-pac) || [snap-pac](https://www.archlinux.org/packages/?name=snap-pac)

*   **vrms-arch** — Un [Richard M. Stallman virtual](https://en.wikipedia.org/wiki/es:Richard_Stallman "wikipedia:es:Richard Stallman") para decirle qué paquetes no libres tiene instalados.

	[https://github.com/orospakr/vrms-arch](https://github.com/orospakr/vrms-arch) || [vrms-arch](https://aur.archlinux.org/packages/vrms-arch/)

### Front-ends gráficos

**Advertencia:** PackageKit abre los permisos del sistema de forma predeterminada y, por lo tanto, no se recomienda para su uso general. Vea [FS#50459](https://bugs.archlinux.org/task/50459) y [FS#57943](https://bugs.archlinux.org/task/57943).

*   **Apper** — Gestor de paquetes y aplicación Qt 5 que utiliza PackageKit escrito en C++. Admite [AppStream metadata](https://www.freedesktop.org/wiki/Distributions/AppStream/).

	[https://userbase.kde.org/Apper](https://userbase.kde.org/Apper) || [apper](https://www.archlinux.org/packages/?name=apper)

*   **Discover** — Gestor de aplicaciones Qt 5 que utiliza PackageKit escrito en C++/QML. Admite [AppStream metadata](https://www.freedesktop.org/wiki/Distributions/AppStream/), [Flatpak](/index.php/Flatpak "Flatpak") y [firmware updates](/index.php/Fwupd "Fwupd").

	[https://userbase.kde.org/Discover](https://userbase.kde.org/Discover) || [discover](https://www.archlinux.org/packages/?name=discover)

*   **GNOME PackageKit** — Gestor de paquetes GTK+ 3 que utiliza PackageKit escrito en C.

	[https://freedesktop.org/software/PackageKit/](https://freedesktop.org/software/PackageKit/) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **GNOME Software** — Gestor de aplicaciones GTK+ 3 que utiliza PackageKit escrito en C. Admite [AppStream metadata](https://www.freedesktop.org/wiki/Distributions/AppStream/), [Flatpak](/index.php/Flatpak "Flatpak") y [firmware updates](/index.php/Fwupd "Fwupd").

	[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **pcurses** — Empaquetador TUI de curses para pacman escrito en C++.

	[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **tkPacman** — Wrapper Tk para pacman escrito en Tcl.

	[https://sourceforge.net/projects/tkpacman](https://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)