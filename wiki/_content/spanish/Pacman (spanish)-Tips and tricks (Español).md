Artículos relacionados

*   [pacman](/index.php/Pacman "Pacman")
*   [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance")
*   [Mirrors](/index.php/Mirrors "Mirrors")
*   [Creating packages](/index.php/Creating_packages "Creating packages")

Para métodos generales para mejorar la flexibilidad de las sugerencias proporcionadas o del propio pacman, consulte [Core utilities](/index.php/Core_utilities "Core utilities") y [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Mantenimiento](#Mantenimiento)
    *   [1.1 Listando paquetes](#Listando_paquetes)
        *   [1.1.1 Por tamaño](#Por_tamaño)
        *   [1.1.2 Por fecha](#Por_fecha)
        *   [1.1.3 No especificado en un grupo o repositorio](#No_especificado_en_un_grupo_o_repositorio)
        *   [1.1.4 Paquetes en desarrollo](#Paquetes_en_desarrollo)
    *   [1.2 Listado de archivos propiedad de un paquete , ordenado por tamaño](#Listado_de_archivos_propiedad_de_un_paquete_,_ordenado_por_tamaño)
    *   [1.3 Identificar archivos que no pertenecen a ningún paquete](#Identificar_archivos_que_no_pertenecen_a_ningún_paquete)
    *   [1.4 Eliminación de paquetes no utilizados (huérfanos)](#Eliminación_de_paquetes_no_utilizados_(huérfanos))
    *   [1.5 Eliminar todo menos el grupo base](#Eliminar_todo_menos_el_grupo_base)
    *   [1.6 Obtener la lista de dependencias de varios paquetes](#Obtener_la_lista_de_dependencias_de_varios_paquetes)
    *   [1.7 Listado de archivos de copia de seguridad modificados](#Listado_de_archivos_de_copia_de_seguridad_modificados)
    *   [1.8 Copia de seguridad de la base de datos de pacman](#Copia_de_seguridad_de_la_base_de_datos_de_pacman)
    *   [1.9 Verifique registros de cambios fácilmente](#Verifique_registros_de_cambios_fácilmente)
*   [2 Instalación y recuperación](#Instalación_y_recuperación)
    *   [2.1 Instalación de paquetes desde un CD / DVD o dispositivo USB](#Instalación_de_paquetes_desde_un_CD_/_DVD_o_dispositivo_USB)
    *   [2.2 Repositorio local personalizado](#Repositorio_local_personalizado)
    *   [2.3 Caché de pacman compartida en red](#Caché_de_pacman_compartida_en_red)
        *   [2.3.1 Caché de solo lectura](#Caché_de_solo_lectura)
        *   [2.3.2 Distribución de caché de solo lectura](#Distribución_de_caché_de_solo_lectura)
        *   [2.3.3 Caché de lectura y escritura](#Caché_de_lectura_y_escritura)
        *   [2.3.4 de doble sentido con rsync](#de_doble_sentido_con_rsync)
        *   [2.3.5 Caché de proxy inverso dinámico usando nginx](#Caché_de_proxy_inverso_dinámico_usando_nginx)
        *   [2.3.6 Sincronice la memoria caché de *pacman* utilizando programas de sincronización](#Sincronice_la_memoria_caché_de_pacman_utilizando_programas_de_sincronización)
        *   [2.3.7 Prevención de limpiezas de caché no deseadas](#Prevención_de_limpiezas_de_caché_no_deseadas)
    *   [2.4 Reconstituir un paquete del sistema de archivos](#Reconstituir_un_paquete_del_sistema_de_archivos)
    *   [2.5 Lista de paquetes instalados](#Lista_de_paquetes_instalados)
    *   [2.6 Listado de todos los archivos modificados de los paquetes](#Listado_de_todos_los_archivos_modificados_de_los_paquetes)
    *   [2.7 Reinstalar todos los paquetes](#Reinstalar_todos_los_paquetes)
    *   [2.8 Restaurar la base de datos local de pacman](#Restaurar_la_base_de_datos_local_de_pacman)
    *   [2.9 Recuperar una memoria USB desde la instalación existente](#Recuperar_una_memoria_USB_desde_la_instalación_existente)
    *   [2.10 Visualización de un único archivo dentro de un .pkg](#Visualización_de_un_único_archivo_dentro_de_un_.pkg)
    *   [2.11 Buscar aplicaciones que usan bibliotecas de paquetes antiguos](#Buscar_aplicaciones_que_usan_bibliotecas_de_paquetes_antiguos)
*   [3 Optimización](#Optimización)
    *   [3.1 Velocidades de acceso a la base de datos](#Velocidades_de_acceso_a_la_base_de_datos)
    *   [3.2 Velocidades de descarga](#Velocidades_de_descarga)
        *   [3.2.1 Powerpill](#Powerpill)
        *   [3.2.2 Wget](#Wget)
        *   [3.2.3 Aria2](#Aria2)
        *   [3.2.4 Otras aplcaciones](#Otras_aplcaciones)
*   [4 Utilidades](#Utilidades)
    *   [4.1 Front-ends gráficos](#Front-ends_gráficos)

## Mantenimiento

**Nota:** En lugar de utilizar *comm* (que requiere una entrada ordenada con *sort*) en las secciones siguientes, también puede utilizar `grep -Fxf` o `grep -Fxvf`.

Véase también [System maintenance](/index.php/System_maintenance "System maintenance").

### Listando paquetes

Es posible que desee obtener la lista de paquetes instalados con su versión, lo cual es útil cuando se reportan errores o se discuten los paquetes instalados.

*   Lista todos los paquetes explícitamente instalados: `pacman -Qe`.
*   Lista los paquetes originales instalados explícitamente (es decir, presentes en la base de datos de sincronización) que no sean dependencias directas o opcionales: `pacman -Qent` .
*   Lista de todos los paquetes externos (normalmente descargados e instalados manualmente): `pacman -Qm`.
*   Lista de todos los paquetes originales (instalados desde la (s) base de datos de sincronización): `pacman -Qn` .
*   Lista de paquetes por regex: `pacman -Qs *regex*` .
*   Lista de paquetes por regex con formato de salida personalizado: `expac -s "%-30n %v" *regex*` (necesita [expac](https://www.archlinux.org/packages/?name=expac)).

#### Por tamaño

Para obtener una lista de paquetes instalados ordenados por tamaño, lo que puede ser útil para liberar espacio en su disco duro:

*   Instalar [expac](https://www.archlinux.org/packages/?name=expac) y ejecutar `expac -H M '%m\t%n' | sort -h`.
*   Ejecute [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) con la opción `-c` .

Para crear un listado de paquetes y su tamaño (deje *packages* en blanco para listar todos los paquetes):

```
 $ expac -S -H M '%k \ t%n' *packages*

```

Para listar los paquetes explícitamente instalados que no están en [base](https://www.archlinux.org/packages/?name=base) ni en [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) con tamaño y descripción:

```
 $ expac -H M "%011m\t%-20n\t%10d" $(comm -23 <(pacman -Qqen | sort) <(pacman -Qqg base base-devel | sort)) | sort -n

```

#### Por fecha

Para enumerar los 20 últimos paquetes instalados con expac , ejecute:

```
 $ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20

```

O, con segundos desde la fecha (1970-01-01 UTC):

```
 $ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20

```

#### No especificado en un grupo o repositorio

**Nota:** Para obtener una lista de paquetes instalados como dependencias pero que ya no son necesarios para ningún paquete instalado, consulte [#Eliminación de paquetes no utilizados (huérfanos)](#Eliminación_de_paquetes_no_utilizados_(huérfanos)).

Lista los paquetes explícitamente instalados que no están en los grupos de [base](https://www.archlinux.org/packages/?name=base) o [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) :

```
 $ comm -23 <(pacman -Qeq | sort) <(pacman -Qgq base base-devel | sort)

```

Lista de todos los paquetes instalados no requeridos por otros paquetes y que no estén en los grupos de [base](https://www.archlinux.org/packages/?name=base) o de [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) :

```
 $ comm -23 <(pacman -Qqt | sort) <(pacman -Sqg base base-devel | sort)

```

Como arriba, pero con descripciones:

```
 $ expac -HM '%-20n\t%10d' $(comm -23 <(pacman -Qqt | sort) <(pacman -Qqg base base-devel | sort))

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

**Sugerencia:** El [lostfiles](https://www.archlinux.org/packages/?name=lostfiles) script realiza pasos similares, pero también incluye una extensa lista negra para eliminar falsos positivos comunes de la salida. [aconfmgr](https://github.com/CyberShadow/aconfmgr) ([aconfmgr-git](https://aur.archlinux.org/packages/aconfmgr-git/)) también permite rastrear archivos huérfanos usando una secuencia de comandos de configuración.

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
' %E -S *packages* | sort -u

```

### Listado de archivos de copia de seguridad modificados

Si desea realizar una copia de seguridad de los archivos de configuración del sistema, puede copiar todos los archivos en `/etc/`, pero normalmente sólo le interesan los ficheros que ha modificado. Los archivos de [copias de seguridad](/index.php/Pacnew_and_Pacsave_files#Package_backup_files "Pacnew and Pacsave files") se puede ver con el siguiente comando:

```
# pacman -Qii | awk '/^MODIFIED/ {print $2}'

```

Ejecutar este comando con permisos de root asegurará que los archivos sólo pueden ser leídos por root (por ejemplo `/etc/sudoers`) están incluidos en la salida.

**Sugerencia:** Mire [#Listado de todos los archivos modificados de los paquetes](#Listado_de_todos_los_archivos_modificados_de_los_paquetes) para listar todos los archivos modificados que conoce *pacman* , no sólo los archivos de copia de seguridad.

### Copia de seguridad de la base de datos de pacman

El siguiente comando se puede usar para realizar una copia de seguridad de la base de datos local de *pacman* :

```
$ tar -cjf pacman_database.tar.bz2 /var/lib/pacman/local

```

Almacene el archivo de base de datos de respaldo *pacman* en uno o más medios sin conexión, como una memoria USB, disco duro externo o CD-R.

La base de datos se puede restaurar moviendo el archivo `pacman_database.tar.bz2` en el `/` directorio y ejecutando el siguiente comando :

```
# tar -xjvf pacman_database.tar.bz2

```

{{Nota|Si los archivos de la base de datos *pacman* están dañados y no hay un archivo de respaldo disponible, existe la esperanza de reconstruir la base de datos *pacman* . Consultar [Pacman/Restore local database](/index.php/Pacman/Restore_local_database "Pacman/Restore local database").

**Sugerencia:** El paquete [pakbak-git](https://aur.archlinux.org/packages/pakbak-git/) proporciona una secuencia de comandos y un servicio en [systemd](/index.php/Systemd "Systemd") para automatizar la tarea. La configuración es posible en `/etc/pakbak.conf`.

### Verifique registros de cambios fácilmente

Cuando los mantenedores actualizan los paquetes, las confirmaciones a menudo se comentan de manera útil. Los usuarios pueden comprobarlo rápidamente desde la línea de comando instalando [pacolog](https://aur.archlinux.org/packages/pacolog/). Esta utilidad enumera mensajes de confirmación recientes para paquetes de los repositorios oficiales o en AUR, mediante el uso de `pacolog <package>`.

## Instalación y recuperación

Formas alternativas de obtener y restaurar paquetes.

### Instalación de paquetes desde un CD / DVD o dispositivo USB

Para descargar paquetes o grupos de paquetes:

```
# cd ~/Packages
# pacman -Syw base base-devel grub-bios xorg gimp --cachedir .
# repo-add ./custom.db.tar.gz ./*

```

A continuación puede grabar la carpeta "Packages" en un CD/DVD o transferir a una dispositivo USB , disco duro externo HDD, etc.

Para instalar:

**1.** Montar los medios:

```
# mkdir /mnt/repo
# mount /dev/sr0 /mnt/repo    #For a CD/DVD.
# mount /dev/sdxY /mnt/repo   #For a USB stick.

```

**2.** Edite `pacman.conf` y agrege este repositorio *antes* de los otros (e.g. extra, core, etc.). Esto es importante. No se limite a descomentar el que está en la parte inferior. De esta manera se asegura de que los archivos del CD/DVD/USB tengan prioridad sobre los de los repositorios estándar.:

 `/etc/pacman.conf` 
```
[custom]
SigLevel = PackageRequired
Server = file:///mnt/repo/Packages
```

**3.** Finalmente, sincronice la base de datos *pacman* para poder usar el nuevo repositorio:

```
# pacman -Syu

```

### Repositorio local personalizado

Utilice el script *repo-add* incluido con *pacman* para generar una base de datos para un repositorio personal. Utilize `repo-add --help` para más detalles sobre su uso. Para agregar un nuevo paquete a la base de datos o para reemplazar la versión anterior de un paquete existente en la base de datos, ejecute:

```
$ repo-add */path/to/repo.db.tar.gz /path/to/package-1.0-1-x86_64.pkg.tar.xz*

```

**Nota:** Una base de datos de paquetes es un archivo tar, opcionalmente comprimido. Las extensiones válidas son *.db* o *.files* seguidas por una extensión de archivo de *.tar* , *.tar.gz* , *.tar.bz2* , *. tar.xz* o *.tar.z* . No es necesario que exista el fichero, pero deben existir todos los directorios principales.

La base de datos y los paquetes no necesitan estar en el mismo directorio cuando se utiliza *repo-add* , pero tenga en cuenta que cuando se usa *pacman* con esa base de datos, deben estar juntos. Almacenar todos los paquetes construidos para ser incluidos en el repositorio en un directorio también permite usar la expansión shell glob para añadir o actualizar múltiples paquetes a la vez:

```
$ repo-add */path/to/repo.db.tar.gz /path/to/*.pkg.tar.xz*

```

**Advertencia:** *repo-add* agrega las entradas a la base de datos en el mismo orden que se pasó en la línea de comando. Si se trata de varias versiones del mismo paquete, se debe tener cuidado para asegurarse de que se agregue la versión correcta al final. En particular, tenga en cuenta que el orden léxico utilizado por el shell depende de la configuración regional y difiere de la [vercmp](https://www.archlinux.org/pacman/vercmp.8.html) orden utilizado por *pacman*.

*repo-remove* se usa para eliminar paquetes de la base de datos, excepto si el nombre del paquete se especifica con el siguiente comando.

```
$ repo-remove */path/to/repo.db.tar.gz pkgname*

```

Una vez que se haya creado la base de datos del repositorio local, agregue el repositorio a `pacman.conf` para cada sistema que usará el repositorio. Un ejemplo de repositorio personalizado está en `pacman.conf`. El nombre del repositorio es el nombre de archivo de la base de datos con la extensión de archivo omitida. En el caso del ejemplo anterior, el nombre del repositorio sería simplemente *repo* . Haga referencia a la ubicación del repositorio utilizando un `file://` url, o por FTP usando [ftp://localhost/path/to/directory](ftp://localhost/path/to/directory).

Si lo desea, añada el repositorio personalizado al directorio [list of unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories"), para que la comunidad pueda beneficiarse de ello.

### Caché de pacman compartida en red

Si ejecuta varios Arch boxes en su LAN, puede compartir paquetes para que pueda disminuir considerablemente los tiempos de descarga. Tenga en cuenta que no debe compartir entre diferentes arquitecturas (es decir, i686 y x86_64) o se encontrará con problemas.

#### Caché de solo lectura

Si está buscando una solución rápida, puede simplemente ejecutar un servidor web independiente que otros ordenadores pueden utilizar como primera réplica.:

```
# ln -s /var/lib/pacman/sync/*.db /var/cache/pacman/pkg
$ sudo -u http darkhttpd /var/cache/pacman/pkg --no-server-id

```

También podría ejecutar darkhttpd como un servicio systemd para su comodidad.Solo agregue este servidor en la parte superior de su `/etc/pacman.d/mirrorlist` in client machines with `Server = http://mymirror:8080`.Asegúrese de mantener su réplica actualizada .

#### Distribución de caché de solo lectura

Existen herramientas específicas de Arch para descubrir automáticamente otros equipos de la red que ofrecen una caché de paquetes. Intente [pacserve](/index.php/Pacserve "Pacserve"), [pkgdistcache](https://aur.archlinux.org/packages/pkgdistcache/), o [paclan](https://aur.archlinux.org/packages/paclan/). pkgdistcache utilize Avahi en lugar de UDP el cual puede funcionar mejor en ciertas redes domésticas que enrutan en lugar de tender un puente entre WiFi y Ethernet .

Históricamente, hubo [PkgD](https://bbs.archlinux.org/viewtopic.php?id=64391) y [multipkg](https://github.com/toofishes/multipkg), pero ya no se mantienen.

#### Caché de lectura y escritura

Para compartir paquetes entre varios equipos, simplemente comparta `/var/cache/pacman/` utilizando cualquier protocolo de montaje basado en red. Esta sección muestra cómo usar [shfs](/index.php/Shfs "Shfs") o [SSHFS](/index.php/SSHFS_(Espa%C3%B1ol) "SSHFS (Español)") para compartir una caché de paquetes más los directorios de biblioteca relacionados entre múltiples ordenadores de la misma red local. Tenga en cuenta que una caché compartida en red puede ser lenta dependiendo de la elección del sistema de archivos, entre otros factores.

Primero, instale cualquier paquete de sistema de ficheros que soporte la red: [shfs-utils](https://www.archlinux.org/packages/?name=shfs-utils), [sshfs](https://www.archlinux.org/packages/?name=sshfs), [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs), [samba](https://www.archlinux.org/packages/?name=samba) or [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils).

**Sugerencia:**

*   Para usar *sshfs* o *shfs*, considere leer [Using SSH Keys (Español)](/index.php/Using_SSH_Keys_(Espa%C3%B1ol) "Using SSH Keys (Español)").
*   Por defecto, *smbfs* no sirve nombres de archivo que contengan dos puntos, lo que hace que el cliente descargue de nuevo el paquete otra vez. Para evitarlo, utilice la función `mapchars` opción de montaje en el cliente.

Luego, para compartir los paquetes actuales, monte `/var/cache/pacman/pkg` del servidor a `/var/cache/pacman/pkg` en cada máquina cliente

**Nota:** No haga `/var/cache/pacman/pkg` ni a ninguno de sus antecesores (e.g., `/var`) un enlace simbólico *Pacman* espera que estos sean directorios. Cuando *pacman* se reinstale o actualice, eliminará los enlaces simbólicos y creará directorios vacíos. Sin embargo, durante la operación *pacman* se basará en algunos archivos que residen allí, rompiendo así el proceso de actualización. Consulte [FS#50298](https://bugs.archlinux.org/task/50298) para más detalles.

#### de doble sentido con rsync

Otro enfoque en un entorno local es [rsync](/index.php/Rsync "Rsync"). Elija un servidor para el almacenamiento en caché y active el [Rsync#rsync daemon](/index.php/Rsync#rsync_daemon "Rsync"). En los clientes, sincronice bidireccionalmente con este recurso compartido mediante el protocolo rsync. Los nombres de archivo que contienen dos puntos no son un problema para el protocolo rsync.

Ejemplo para un cliente, utilizando `uname -m` dentro del nombre compartido asegura una arquitectura dependiente sync:

```
 # rsync rsync://server/share_$(uname -m)/ /var/cache/pacman/pkg/ ...
 # pacman ...
 # paccache ...
 # rsync /var/cache/pacman/pkg/ rsync://server/share_$(uname -m)/  ...

```

#### Caché de proxy inverso dinámico usando nginx

[nginx](/index.php/Nginx "Nginx") puede utilizarse para realizar peticiones proxy a las réplicas ascendentes oficiales y almacenar los resultados en caché en el disco local. Todas las solicitudes posteriores de ese archivo se servirán directamente desde la caché local, lo que minimiza la cantidad de tráfico de Internet necesario para actualizar un gran número de servidores con el mínimo esfuerzo.

**Advertencia:** Este método tiene una limitación. Debe usar réplicas que usan la misma ruta relativa a los archivos del paquete y debe configurar su caché para usar esa misma ruta. En este ejemplo, estamos usando réplicas que usan la ruta relativa `/archlinux/$repo/os/$arch` y la configuración de nuestro `Server` en `mirrorlist` está configuradara de forma similar.

En este ejemplo, ejecutaremos el servidor de caché en `http://cache.domain.local:8080/` y almacenaremos los paquetes en `/srv/http/pacman-cache/`.

Cree el directorio para la memoria caché y ajuste los permisos para que nginx pueda escribir archivos en ella:

```
 # mkdir /srv/http/pacman-cache
 # chown http:http /srv/http/pacman-cache

```

A continuación, configure nginx como la opción [dynamic cache](https://gist.github.com/anonymous/97ec4148f643de925e433bed3dc7ee7d) (lea los comentarios para una explicación de los comandos).

Finalmente, actualice sus otros servidores Arch Linux para usar esta nueva caché agregando la siguiente línea al archivo `mirrorlist`:

 `/etc/pacman.d/mirrorlist` 
```
Server = http://cache.domain.local:8080/archlinux/$repo/os/$arch
...

```

**Nota:** Habrá que crear un método para borrar paquetes viejos, ya que este directorio continuará creciendo con el tiempo. `paccache` (que se incluye con *pacman*) se puede utilizar para automatizarlo , utilizando criterios de retención de su elección. Por ejemplo, `find /srv/http/pacman-cache/ -type d -exec paccache -v -r -k 2 -c {} \;` mantendrá las dos últimas versiones de los paquetes en su directorio de caché.

#### Sincronice la memoria caché de *pacman* utilizando programas de sincronización

Use [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync") o [Syncthing](/index.php/Syncthing "Syncthing") para sincronizar las carpetas de la caché de "pacman" (i.e. `/var/cache/pacman/pkg`).

#### Prevención de limpiezas de caché no deseadas

Por defecto, `pacman -Sc` elimina los paquetes tarballs de la caché que corresponden a paquetes que no están instalados en la máquina en la que se emitió el comando. Dado que "pacman" no puede predecir qué paquetes están instalados en todos los equipos que comparten la caché, acabará eliminando archivos que no deberían estarlo.

Para limpiar la caché de forma que sólo se eliminen los tarballs *obsoletos*, añada esta entrada en el archivo `[options]` en la sección de `/etc/pacman.conf`:

```
CleanMethod = KeepCurrent

```

### Reconstituir un paquete del sistema de archivos

Para reconstituir un paquete desde el sistema de archivos, use *bacman* (incluido con *pacman* ). Los archivos del sistema se toman tal como están, por lo tanto, cualquier modificación estará presente en el paquete ensamblado. Por lo tanto, se desaconseja la distribución del paquete reconstituido; ver [ABS](/index.php/ABS "ABS") y [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") para las alternativas.

**Sugerencia:** *bacman* respeta las opciones de `PACKAGER`, `PKGDEST` y `PKGEXT` de `makepkg.conf`. Las opciones personalizadas para las herramientas de compresión se pueden configurar exportando la variable de entorno relevante, por ejemplo `XZ_OPT = "- T 0"` habilitará la compresión paralela para *xz* .

Una herramienta alternativa sería [fakepkg](https://aur.archlinux.org/packages/fakepkg/). Es compatible con la paralelización y puede manejar múltiples paquetes de entrada en un comando, lo que *bacman* no soporta.

### Lista de paquetes instalados

Mantener una lista de paquetes instalados explícitamente puede ser útil para acelerar la instalación en un nuevo sistema:

```
$ pacman -Qqe > pkglist.txt

```

**Nota:** Si se usó la opción `-t` al reinstalar la lista, todos los paquetes que no sean de nivel superior se establecerán como dependencias. Con la opción `-n`, los paquetes externos (por ejemplo, de AUR) se omitirán de la lista.

Para instalar paquetes de la copia de seguridad de la lista, ejecute:

```
# pacman -S - < pkglist.txt

```

**Sugerencia:**

*   Para omitir los paquetes ya instalados, use `--needed`.
*   Use `comm -13 <(pacman -Qqdt | sort) <(pacman -Qqdtt | sort) > optdeplist.txt` para crear también una lista de las dependencias opcionales instaladas que se pueden reinstalar con `--asdeps`.

En caso de que la lista incluya paquetes externos, como paquetes [AUR](/index.php/AUR "AUR"), quítelos primero:

```
# pacman -S $(comm -12 <(pacman -Slq | sort) <(sort pkglist.txt))

```

Para eliminar todos los paquetes en su sistema que no se mencionan en la lista:

```
# pacman -Rsu $(comm -23 <(pacman -Qq | sort) <(sort pkglist.txt))

```

**Sugerencia:** Estas tareas pueden ser automatizadas. Consulte [bacpac](https://aur.archlinux.org/packages/bacpac/), [packup](https://aur.archlinux.org/packages/packup/), [pacmanity](https://aur.archlinux.org/packages/pacmanity/) y [pug](https://aur.archlinux.org/packages/pug/) por ejemplo.

Si desea mantener una lista actualizada de los paquetes explícitamente instalados (e.g. en combinación con una versión `/etc/`), puede configurar un [hook](/index.php/Pacman#Hooks "Pacman"). Ejemplo:

```
[Trigger]
Operation = Install
Operation = Remove
Type = Package
Target = *

[Action]
When = PostTransaction
Exec = /bin/sh -c '/usr/bin/pacman -Qqe > /etc/packages.txt'

```

### Listado de todos los archivos modificados de los paquetes

Si sospecha que hay corrupción de archivos (por ejemplo, por fallos de software o hardware), pero no está seguro de si los archivos se corrompieron, es posible que desee compararlos con las sumas de hash de los paquetes. Esto se puede hacer con [pacutils](https://www.archlinux.org/packages/?name=pacutils):

```
# paccheck --md5sum --quiet

```

Para la recuperación de la base de datos, véase [#Restaurar la base de datos local de pacman](#Restaurar_la_base_de_datos_local_de_pacman). Los archivos `mtree` también pueden ser [extraído como `.MTREE` de los respectivos archivos del paquete](#Visualización_de_un_único_archivo_dentro_de_un_.pkg).

**Nota:** ¡Esto *no* debe usarse cuando se sospeche de cambios maliciosos! En este caso, se recomiendan precauciones de seguridad, como usar un medio en vivo o una fuente independiente para las sumas de hash.

### Reinstalar todos los paquetes

Para reinstalar todos los paquetes originales, use:

```
# pacman -Qnq | pacman -S -

```

Los paquetes externos (AUR) deben reinstalarse por separado; puede listarlos con `pacman -Qmq`.

*Pacman* conserva el [Motivo de la instalación](/index.php/Installation_reason "Installation reason") por defecto.

### Restaurar la base de datos local de pacman

Véase [Pacman/Restore local database](/index.php/Pacman/Restore_local_database "Pacman/Restore local database").

### Recuperar una memoria USB desde la instalación existente

Si tiene Arch instalado en una memoria USB y se las arregla para estropearlo ( por ejemplo, quitándola mientras todavía está siendo escrita), entonces es posible reinstalar todos los paquetes y esperar que vuelva a funcionar (suponiendo que la memoria USB está montada en `/newarch`)

```
# pacman -S $(pacman -Qq --dbpath /newarch/var/lib/pacman) --root /newarch --dbpath /newarch/var/lib/pacman

```

### Visualización de un único archivo dentro de un .pkg

Por ejemplo, si desea ver el contenido de `/etc/systemd/logind.conf` suministrado dentro del paquete [systemd](https://www.archlinux.org/packages/?name=systemd):

```
$ tar -xOf /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz etc/systemd/logind.conf

```

O puede usar [vim](https://www.archlinux.org/packages/?name=vim) para explorar el archivo:

```
$ vim /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz

```

### Buscar aplicaciones que usan bibliotecas de paquetes antiguos

Incluso después de haber instalado un paquete, los programas existentes que se ejecutan desde hace mucho tiempo (como los demonios y los servidores) siguen utilizando código de antiguas bibliotecas.Y es una mala idea dejar que estos programas se ejecuten si la biblioteca anterior contiene un error de seguridad.

Esta es una manera de encontrar todos los programas que usan código de paquetes antiguos:

```
# lsof +c 0 | grep -w DEL | awk '1 { print $1 ": " $NF }' | sort -u

```

Imprimirá el nombre del programa en ejecución y la biblioteca antigua que se eliminó o reemplazó con contenido más reciente.

## Optimización

### Velocidades de acceso a la base de datos

*Pacman* almacena toda la información del los paquetes en una colección de archivos pequeños, uno por cada paquete. La mejora de las velocidades de acceso a la base de datos reduce el tiempo necesario en las tareas relacionadas con esta, por ejemplo, buscar paquetes y resolver las dependencias. El método más seguro y fácil es ejecutarlo como root:

```
 # pacman-optimize

```

Esto intentará poner todos los archivos pequeños juntos en una ubicación (física) en el disco duro para que la cabeza del disco no tenga que moverse tanto al acceder a todos los datos. Este método es seguro, pero no es infalible, depende del sistema de archivos, el uso del disco y la fragmentación del espacio vacío. Otra opción más agresiva sería eliminar primero los paquetes desinstalados de la caché y eliminar los repositorios no utilizados antes de la optimización de la base de datos:

```
 # pacman -Sc && pacman-optimize

```

### Velocidades de descarga

**Nota:** Si las velocidades de descarga se han reducido , asegúrese de que está utilizando uno de los muchos [mirrors](/index.php/Mirrors "Mirrors") y no ftp.archlinux.org, que está saturado desde marzo de 2007.

Al descargar paquetes *pacman* usa los *mirrors* en el orden en que están en `/etc/pacman.d/mirrorlist` .Sin embargo los *mirrors* que está en la parte superior de la lista , pueden no ser los más rápido para usted. Para seleccionar los *mirrors* más rápidos, consulte [Mirrors](/index.php/Mirrors "Mirrors").

La velocidad de *pacman* en la descarga de paquetes también puede ser mejorada mediante el uso de una aplicación diferente para descargar paquetes, en lugar del descargador de archivos integrado de *pacman*.

En todos los casos, asegúrese de tener la última *pacman* antes de hacer cualquier modificación.

```
 # pacman -Syu

```

#### Powerpill

[Powerpill](/index.php/Powerpill "Powerpill") es un envoltorio de Pacman que utiliza la descarga paralela y segmentada para tratar de acelerar las descargas de Pacman.

#### Wget

Esto también es muy útil si necesita configuraciones proxy más potentes que las capacidades incorporadas de *pacman*.

Para usar `wget` , primero instale el paquete [wget](https://www.archlinux.org/packages/?name=wget) y luego modifique `/etc/pacman.conf` descomentando la siguiente línea en la sección `[options]` :

```
 XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u

```

En lugar de descomentar los parámetros de `wget` en `/etc/pacman.conf` , también puede modificar el archivo de configuración de `wget` directamente , el archivo de todo el sistema es `/etc/wgetrc` o por usuario , el archivo es `$HOME/.wgetrc` .

#### Aria2

[aria2](/index.php/Aria2 "Aria2") es una utilidad de descarga de peso ligero con soporte para HTTP / HTTPS y transferencias directas continuas y segmentadas. Aria2 permite múltiples y simultáneas conexiones HTTP / HTTPS y FTP a un *mirror* de Arch, lo que debería dar como resultado un aumento en las velocidades de descarga para la recuperación de archivos y paquetes.

**Nota:** El uso de aria2c en XferCommand de *pacman* *no* dará lugar a descargas paralelas de varios paquetes. Pacman invoca el XferCommand con un solo paquete a la vez y espera a que se complete antes de invocar el siguiente. Para descargar varios paquetes en paralelo, consulte [Powerpill](/index.php/Powerpill "Powerpill").

Instale [aria2](https://www.archlinux.org/packages/?name=aria2) y luego edite `/etc/pacman.conf` agregando la siguiente línea a la sección `[options]` :

```
XferCommand = /usr/bin/aria2c --allow-overwrite=true --continue=true --file-allocation=none --log-level=error --max-tries=2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 --timeout=5 --dir=/ --out %o %u

```

**Sugerencia:** [Esta configuración alternativa para usar *pacman* con aria2](https://bbs.archlinux.org/viewtopic.php?pid=1491879#p1491879) intenta simplificar la configuración y añade más opciones de configuración.

Vea [OPTIONS](http://aria2.sourceforge.net/manual/en/html/aria2c.html#options) en [aria2c(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aria2c.1) para usar las configuraciones de aria2\.

*   `-d, --dir`: El directorio para almacenar los archivo(s) descargado según lo especificado por *pacman* .
*   `-o, --out`: El nombre(s) de archivo(s) de salida descargado(s).
*   `%o`: Variable que representa el nombre(s) de archivo(s) local especificado por *pacman*.
*   `%u`: Variable que representa la URL de descarga especificada por *pacman*.

#### Otras aplcaciones

Hay otras aplicaciones de descarga que puede usar con *pacman* . Aquí están, y su configuración asociada de XferCommand

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`
*   `hget`: `XferCommand = /usr/bin/hget %u -n 2 -skip-tls false` (por favor lea [documentation on the Github project page](https://github.com/huydx/hget) for para mas información)

## Utilidades

*   **Lostfiles** — Script que identifica archivos que no son propiedad de ningún paquete.

	[https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [lostfiles](https://www.archlinux.org/packages/?name=lostfiles)

*   **Pacmatic** — Envoltura de *Pacman* para comprobar notícias de Arch antes de la actualización, evitar actualizaciones parciales y advertir sobre cambios en el archivo de configuración.

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

*   **GNOME Software** — Gnome Software App. (Selección conservada por GNOME)

	[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **kalu** — Una pequeña aplicación que agregará un ícono a su bandeja de sistema, verificando regularmente si hay nuevas actualizaciones.

	[https://jjacky.com/kalu/](https://jjacky.com/kalu/) || [kalu](https://aur.archlinux.org/packages/kalu/)

*   **pcurses** — Gestión de paquetes en una interfaz de curses

	[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **PkgBrowser** — Aplicación para buscar y explorar paquetes de Arch, muestra detalles sobre paquetes seleccionados.

	[https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home](https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

*   **tkPacman** — Depende solo de Tcl/Tk y X11, e interactúa con la base de datos del paquete a través de la CLI de *pacman*.

	[http://sourceforge.net/projects/tkpacman](http://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)