Artículos relacionados

*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages")
*   [pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing")
*   [pacman/Pacnew and Pacsave](/index.php/Pacman/Pacnew_and_Pacsave "Pacman/Pacnew and Pacsave")
*   [pacman/Restore local database](/index.php/Pacman/Restore_local_database "Pacman/Restore local database")
*   [pacman/Rosetta](/index.php/Pacman/Rosetta "Pacman/Rosetta")
*   [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks")
*   [FAQ#Package management](/index.php/FAQ#Package_management "FAQ")
*   [System maintenance](/index.php/System_maintenance "System maintenance")
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [Official repositories](/index.php/Official_repositories "Official repositories")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")

**Estado de la traducción:** este artículo es una versión traducida de [pacman](/index.php/Pacman "Pacman"). Fecha de la última traducción/revisión: **2017-10-08**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Pacman&diff=0&oldid=490231).

El [gestor de paquetes](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system") [pacman](https://www.archlinux.org/pacman/) es una de las principales características distintivas de Arch Linux. Combina un simple formato de paquetes binarios con un fácil [sistema de compilación de paquetes](/index.php/Arch_Build_System "Arch Build System"). El objetivo de *pacman* es hacer posible gestionar fácilmente los paquetes, tanto si son los de los [repositorios oficiales de Arch](/index.php/Official_repositories "Official repositories") como las compilaciones realizadas por los propios usuarios.

*pacman* mantiene el sistema actualizado mediante la sincronización con las listas de paquetes del servidor principal. Este modelo servidor/cliente le permite descargar y/o instalar paquetes con una simple orden y cubrir sus dependencias necesarias.

*pacman* está escrito en lenguaje de programación C y utiliza el formato [tar](https://en.wikipedia.org/wiki/tar_(computing) "w:tar (computing)") para empaquetar.

**Sugerencia:** el paquete oficial [pacman](https://www.archlinux.org/packages/?name=pacman) también contiene otras herramientas útiles, tales como [makepkg](/index.php/Makepkg "Makepkg"), **pactree**, **vercmp** y [checkupdates](/index.php/Checkupdates "Checkupdates"). Se puede obtener la lista completa de dichas herramientas con `pacman -Qlq pacman | grep bin`

## Contents

*   [1 Utilización](#Utilizaci.C3.B3n)
    *   [1.1 Instalar paquetes](#Instalar_paquetes)
        *   [1.1.1 Instalar paquetes específicos](#Instalar_paquetes_espec.C3.ADficos)
        *   [1.1.2 Instalar grupos de paquetes](#Instalar_grupos_de_paquetes)
    *   [1.2 Desinstalar paquetes](#Desinstalar_paquetes)
    *   [1.3 Actualizar paquetes](#Actualizar_paquetes)
    *   [1.4 Consultar la base de datos de los paquetes](#Consultar_la_base_de_datos_de_los_paquetes)
        *   [1.4.1 Estructura de la base de datos](#Estructura_de_la_base_de_datos)
    *   [1.5 Limpiar la memoria caché de los paquetes](#Limpiar_la_memoria_cach.C3.A9_de_los_paquetes)
    *   [1.6 Órdenes adicionales](#.C3.93rdenes_adicionales)
    *   [1.7 Motivo de la instalación](#Motivo_de_la_instalaci.C3.B3n)
    *   [1.8 Buscar un paquete que contenga un archivo específico](#Buscar_un_paquete_que_contenga_un_archivo_espec.C3.ADfico)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Opciones Generales](#Opciones_Generales)
        *   [2.1.1 Comparar versiones antes de actualizar](#Comparar_versiones_antes_de_actualizar)
        *   [2.1.2 Evitar la actualización de un paquete](#Evitar_la_actualizaci.C3.B3n_de_un_paquete)
        *   [2.1.3 Evitar la actualización de un grupo de paquetes](#Evitar_la_actualizaci.C3.B3n_de_un_grupo_de_paquetes)
        *   [2.1.4 Evitar la instalación de archivos en el sistema](#Evitar_la_instalaci.C3.B3n_de_archivos_en_el_sistema)
        *   [2.1.5 Mantener varios archivos de configuración](#Mantener_varios_archivos_de_configuraci.C3.B3n)
        *   [2.1.6 Hooks](#Hooks)
    *   [2.2 Repositorios y servidores de réplicas](#Repositorios_y_servidores_de_r.C3.A9plicas)
        *   [2.2.1 Seguridad de los paquetes](#Seguridad_de_los_paquetes)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [3.1 Error «Failed to commit transaction (conflicting files)»](#Error_.C2.ABFailed_to_commit_transaction_.28conflicting_files.29.C2.BB)
    *   [3.2 Error «Failed to commit transaction (invalid or corrupted package)»](#Error_.C2.ABFailed_to_commit_transaction_.28invalid_or_corrupted_package.29.C2.BB)
    *   [3.3 Error «Failed to init transaction (unable to lock database)»](#Error_.C2.ABFailed_to_init_transaction_.28unable_to_lock_database.29.C2.BB)
    *   [3.4 Los paquetes no se pueden recibir en la instalación](#Los_paquetes_no_se_pueden_recibir_en_la_instalaci.C3.B3n)
    *   [3.5 Reinstalar manualmente pacman](#Reinstalar_manualmente_pacman)
    *   [3.6 pacman se bloquea durante una actualización](#pacman_se_bloquea_durante_una_actualizaci.C3.B3n)
    *   [3.7 Error «unable to find root device» después de reiniciar](#Error_.C2.ABunable_to_find_root_device.C2.BB_despu.C3.A9s_de_reiniciar)
    *   [3.8 Signature from "User <email@gmail.com>" is unknown trust, installation failed](#Signature_from_.22User_.3Cemail.40gmail.com.3E.22_is_unknown_trust.2C_installation_failed)
    *   [3.9 Solicitud para importar las claves PGP](#Solicitud_para_importar_las_claves_PGP)
    *   [3.10 Error: key "0123456789ABCDEF" could not be looked up remotely](#Error:_key_.220123456789ABCDEF.22_could_not_be_looked_up_remotely)
    *   [3.11 Signature from "User <email@archlinux.org>" is invalid, installation failed](#Signature_from_.22User_.3Cemail.40archlinux.org.3E.22_is_invalid.2C_installation_failed)
    *   [3.12 Error «Warning: current locale is invalid; using default "C" locale»](#Error_.C2.ABWarning:_current_locale_is_invalid.3B_using_default_.22C.22_locale.C2.BB)
    *   [3.13 pacman no respeta los ajustes del proxy](#pacman_no_respeta_los_ajustes_del_proxy)
    *   [3.14 ¿Cómo reinstalar todos los paquetes, conservando la información sobre si algo se instaló explícitamente o como una dependencia?](#.C2.BFC.C3.B3mo_reinstalar_todos_los_paquetes.2C_conservando_la_informaci.C3.B3n_sobre_si_algo_se_instal.C3.B3_expl.C3.ADcitamente_o_como_una_dependencia.3F)
    *   [3.15 Error «Cannot open shared object file»](#Error_.C2.ABCannot_open_shared_object_file.C2.BB)
    *   [3.16 Descarga de paquetes congelada](#Descarga_de_paquetes_congelada)
    *   [3.17 Error al recuperar el archivo 'core.db' del servidor de réplica](#Error_al_recuperar_el_archivo_.27core.db.27_del_servidor_de_r.C3.A9plica)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Utilización

Lo que sigue es una pequeña muestra de las operaciones que se pueden realizar con *pacman*. Para leer más ejemplos, remítase a [pacman(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8).

**Sugerencia:** para aquellos usuarios que han utilizado antes otras distribuciones de Linux, el artículo [Pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta") les puede resultar útil.

### Instalar paquetes

**Nota:** los paquetes suelen tener [dependencias opcionales](/index.php/PKGBUILD#optdepends "PKGBUILD"), dependencias que proporcionan características adicionales a la aplicación, sin ser necesarias para su funcionamiento. Al instalar un paquete, *pacman* mostrará sus dependencias opcionales sin registrarlas en `pacman.log`: utilice la orden [pacman -Si](#Consultar_la_base_de_datos_de_los_paquetes) para ver las dependencias opcionales de un paquete así como una breve descripción de sus funcionalidades.

**Advertencia:** al instalar paquetes en Arch, evite actualizar la lista de paquetes sin [actualizar el sistema](#Actualizar_paquetes) (imagine, por ejemplo, el caso de un [paquete que ya no se mantiene](#Los_paquetes_no_se_pueden_recibir_en_la_instalaci.C3.B3n) en los repositorios). En la práctica, **no** es aconsejable ejecutar `pacman -Sy *nombre_paquete*`, sino más bien `pacman -Sy**u** *nombre_paquete*`, ya que la primera orden podría ocasionar problemas de dependencia. Consulte [System maintenance#Partial upgrades are unsupported](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance") y [BBS#89328](https://bbs.archlinux.org/viewtopic.php?id=89328).

#### Instalar paquetes específicos

Para instalar o actualizar un solo paquete o lista de paquetes (incluyendo las dependencias), ejecute la orden siguiente:

```
# pacman -S *nombre_paquete1* *nombre_paquete2* ...

```

Para instalar una lista de paquetes con una [expresión regular (regex)](https://en.wikipedia.org/wiki/Expresi%C3%B3n_regular "wikipedia:Expresión regular") (vea [este hilo del foro](https://bbs.archlinux.org/viewtopic.php?id=7179)):

```
# pacman -S $(pacman -Ssq *expresion-regular_paquete*)

```

A veces hay varias versiones de un paquete en diferentes repositorios, por ejemplo, *extra* y *testing*. Para instalar la versión precedente necesita especificar el nombre del repositorio:

```
# pacman -S extra/*nombre_paquete*

```

Para instalar un número de paquetes que comparten patrones similares en sus nombres —no todo el grupo ni todos los paquetes coincidentes— p.ej. [plasma](https://www.archlinux.org/groups/x86_64/plasma/):

```
# pacman -S plasma-{desktop,mediacenter,nm}

```

Por supuesto, esto no está limitado y se puede ampliar a los niveles que sean necesarios:

```
# pacman -S plasma-{workspace{,-wallpapers},pa}

```

#### Instalar grupos de paquetes

Algunos paquetes pertenecen a un [grupo de paquetes](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages"), los cuales se pueden instalar simultáneamente. Por ejemplo, emitiendo la orden:

```
# pacman -S gnome

```

el prompt le pedirá que seleccione los paquetes del grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/) que desea instalar.

En algunas ocasiones, un grupo contiene una gran cantidad de paquetes, y puede que solo le interese, o no desee instalar, unos pocos de ellos. En lugar de tener que introducir todos los números excepto los que no desea, quizás sea más conveniente, para seleccionar o excluir paquetes o intervalos de paquetes, la siguiente sintaxis:

```
Enter a selection (default=all): 1-10 15

```

que seleccionará los paquetes del 1 al 10 y 15 para la instalación, o bien:

```
Enter a selection (default=all): ^5-8 ^2

```

que seleccionará todos los paquetes excepto 5 a 8 y 2 para la instalación.

Para ver qué paquetes pertenecen al grupo gnome, ejecute:

```
# pacman -Sg gnome

```

Visite también [https://www.archlinux.org/groups/](https://www.archlinux.org/groups/) para ver qué grupos de paquetes están disponibles.

**Nota:** si un paquete de la lista ya está instalado en el sistema, este se volverá a reinstalar, incluso si ya está actualizado, a menos que se utilice la opción `--needed`.

### Desinstalar paquetes

Para eliminar un solo paquete, dejando todas sus dependencias instaladas:

```
# pacman -R *nombre_paquete*

```

Para eliminar un paquete y sus dependencias (siempre que no sean usadas por ningún otro paquete instalado):

```
# pacman -Rs *nombre_paquete*

```

Para eliminar un paquete, sus dependencias y todos los paquetes que dependen de esas dependencias:

**Advertencia:** esta operación es recursiva, y debe utilizarse con precaución, ya que puede eliminar muchos paquetes potencialmente necesarios.

```
# pacman -Rsc *nombre_paquete*

```

Para eliminar un paquete, el cual es requerido por otro paquete, sin quitar el paquete dependiente:

```
# pacman -Rdd *nombre_paquete*

```

*pacman* guarda los archivos de configuración importantes al quitar ciertas aplicaciones y los renombra con la extensión: *.pacsave*. Para evitar la creación de estos archivos de respaldo utilice la opción `-n`:

```
# pacman -Rn *nombre_paquete*

```

**Nota:** *pacman* no eliminará las configuraciones creadas por la aplicación misma (por ejemplo los «dotfiles» —archivos que comienzan con un punto— presentes en la carpeta personal [*«home»*]).

### Actualizar paquetes

**Advertencia:**

*   se espera que los usuarios se ilustren con la sección [System maintenance#Upgrading the system](/index.php/System_maintenance#Upgrading_the_system "System maintenance") para actualizar sus sistemas regularmente y no ejecuten a ciegas la orden de abajo;
*   Arch solo admite actualizaciones completas del sistema. Vea [System maintenance#Partial upgrades are unsupported](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance") y [#Instalar paquetes](#Instalar_paquetes) para obtener más detalles.

*pacman* puede actualizar todos los paquetes del sistema con una sola orden. Esto proceso puede durar bastante dependiendo de cuánto tiempo haya estado el sistema sin actualizar. La siguiente orden sincroniza las bases de datos de los repositorios *y* actualiza los paquetes del sistema (excluyendo los paquetes «locales» que no estén en los repositorios configurados):

```
# pacman -Syu

```

### Consultar la base de datos de los paquetes

*pacman* puede consultar la base de datos de los paquetes presentes en el sistema con la opción `-Q`, las bases de datos de los servidores remotos con la opción `-S` y los archivos presentes en dichas bases con la opión `-F`. Vea `pacman -Q --help`, `pacman -S --help` y `pacman -F --help` para conocer las subopciones respectivas de cada opción.

*pacman* puede buscar paquetes en la base de datos, la búsqueda se realiza tanto por los nombres como por las descripciones de los paquetes:

```
$ pacman -Ss *cadena1* *cadena2* ...

```

Algunas veces `-s` construye una ERE (Expresión Regular Extendida) que puede causar resultados no deseados, por lo cual debe limitarse para que coincida con el nombre del paquete y no con la descripción u otro campo:

```
$ pacman -Ss '^vim-'

```

Para buscar paquetes ya instalados:

```
$ pacman -Qs *cadena1* *cadena2* ...

```

Para buscar nombres de archivos de paquetes en los paquetes de los servidores remotos:

```
$ pacman -Fs *cadena1* *cadena2* ...

```

Para mostrar información detallada acerca de un determinado paquete:

```
$ pacman -Si *nombre_paquete*

```

Para conocer los paquetes instalados en el sistema:

```
$ pacman -Qi *nombre_paquete*

```

Pasando la doble opción `-i` también se mostrará la lista de archivos de respaldo y sus estados de modificación:

```
$ pacman -Qii *nombre_paquete*

```

Para obtener una lista de los archivos instalados por un paquete:

```
$ pacman -Ql *nombre_paquete*

```

Para obtener un listado de los archivos instalados por un paquete recibido desde un servidor remoto:

```
$ pacman -Fl *nombre_paquete*

```

Para verificar la presencia de los archivos instalados por un paquete:

```
$ pacman -Qk *nombre_paquete*

```

Pasando la opción `k` dos veces, se realizará un chequeo más exhaustivo.

Para consultar la base de datos para saber a qué paquete pertenece un archivo del sistema de archivos:

```
$ pacman -Qo */ruta/al/nombre_del_archivo*

```

Para consultar la base de datos para saber a qué paquete del servidor remoto pertenece un archivo:

```
$ pacman -Fo */ruta/al/nombre_del_archivo*

```

Para enumerar todos los paquetes que no sean necesarios como dependencias (huérfanos):

```
$ pacman -Qdt

```

Para enumerar todos los paquetes explícitamente instalados y no requeridos como dependencias:

```
$ pacman -Qet

```

Para enumerar el árbol de dependencias de un paquete:

```
$ pactree *nombre_paquete*

```

Para enumerar todos los paquetes que dependen de un paquete específico, utilice *whoneeds* de [pkgtools](https://aur.archlinux.org/packages/pkgtools/):

```
$ whoneeds *nombre_paquete*

```

o la opción inversa *pactree*:

```
$ pactree -r *nombre_paquete*

```

Véase [Pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") para conocer más ejemplos.

#### Estructura de la base de datos

Las bases de datos de pacman se encuentran, normalmente, en `/var/lib/pacman/sync`. Para cada repositorio especificado en `/etc/pacman.conf` habrá su correspondiente archivo de base de datos ubicado allí. Los archivos de base de datos son archivos en formato tar-gzip que contienen un directorio para cada paquete, por ejemplo para el paquete [which](https://www.archlinux.org/packages/?name=which):

```
% tree which-2.20-6 
which-2.20-6
|-- depends
`-- desc

```

El archivo `depends` enumera los paquetes de los que depende este paquete, mientras que el archivo `desc` contiene una descripción del paquete, como el tamaño del archivo y el hash MD5.

### Limpiar la memoria caché de los paquetes

*pacman* almacena los paquetes descargados en `/var/cache/pacman/pkg/` y no elimina las versiones antiguas o desinstaladas automáticamente, por lo tanto, es necesario limpiar a drede esa carpeta periódicamente para evitar que la misma crezca indefinidamente.

La opción integrada para eliminar todos los paquetes de la memoria caché que no están instalados es:

```
# pacman -Sc

```

**Advertencia:**

*   haga esto únicamente cuando esté seguro de que no se requieren versiones anteriores de paquetes, por ejemplo para un [downgrade](/index.php/Downgrade "Downgrade") posterior. `pacman -Sc` solo deja disponibles las versiones de los paquetes que están *actualmente instalados*, las versiones anteriores tendrían que ser recuperadas por otros medios, como [Archive](/index.php/Archive "Archive");
*   es posible vaciar completamente la carpeta de la caché con `pacman -Scc`. Además de lo anterior, esto también impide la reinstalación de un paquete directamente *desde* la carpeta de la caché, requiriendo, en caso de necesidad, de una nueva descarga. Debe evitarse, a menos que se necesite recuperar inmediatemente espacio en el disco.

Debido a las limitaciones anteriores, considere el uso de una alternativa que le permita más control sobre qué paquetes y cuántos desea eliminar de la memoria caché:

el script *paccache*, proporcionado por el propio paquete [pacman](https://www.archlinux.org/packages/?name=pacman), elimina todas las versiones de cada paquete presentes en la memoria caché, independientemente de si están instaladas o no, excepto las 3 más recientes, de forma predeterminada:

```
# paccache -r

```

**Sugerencia:** puede crear [hooks de pacman](/index.php/Pacman_hooks "Pacman hooks") para ejecutarlos automáticamente después de cada operación de pacman. Consulte [este hilo](https://bbs.archlinux.org/viewtopic.php?pid=1694743#p1694743) para conocer ejemplos.

También puede definir cuántas versiones recientes desea conservar:

```
# paccache -rk 1

```

Para eliminar de la memoria caché todas las versiones de los paquetes desinstalados, vuelva a ejecutar *paccache* con:

```
# paccache -ruk0

```

Vea `paccache -h` para conocer más opciones.

[pkgcacheclean](https://aur.archlinux.org/packages/pkgcacheclean/) y [pacleaner](https://aur.archlinux.org/packages/pacleaner/) son dos alternativas más.

### Órdenes adicionales

Descargar un paquete sin instalarlo:

```
# pacman -Sw *nombre_paquete*

```

Instalar un paquete 'local' que no proviene de un repositorio remoto (por ejemplo, el paquete viene de [AUR](/index.php/Arch_User_Repository "Arch User Repository")):

```
# pacman -U /ruta/al/paquete/nombre_paquete-versión.pkg.tar.xz

```

Para mantener una copia del paquete local en la caché de *pacman*, utilice:

```
# pacman -U file://ruta/al/paquete/nombre_paquete-versión.pkg.tar.xz

```

Instalar un paquete 'remoto' (no de un repositorio indicado en los archivos de configuración de pacman):

```
# pacman -U http://www.ejemplo.com/repo/ejemplo.pkg.tar.xz

```

Para inhibir las acciones derivadas de `-S`, `-U` y `-R`, puede utilizarse `-p`.

*pacman* siempre enumerará los paquetes que se van a instalar o eliminar y pedirá permiso antes de realizar la acción.

### Motivo de la instalación

La base de datos de *pacman* diferencia los paquetes instalados en dos grupos, de acuerdo a la razón por la que fueron instalados:

*   **explicitly-installed**: (instalado explícitamente), son aquellos paquetes que se instalaron con una orden genérica de *pacman* como `-S` o `-U`;
*   **dependencies**: (dependencias), son aquellos paquetes que, pese a que nunca se pasaron (en general) por una orden de instalación de *pacman*, fueron implícitamente instalados porque eran [requeridos](/index.php/Dependency "Dependency") por otro paquete que fue explícitamente instalado.

Al instalar un paquete, es posible forzar su motivo de instalación a *dependency* con:

```
# pacman -S --asdeps *nombre_paquete*

```

Cuando se **re**instala un paquete, no obstante, el motivo de instalación establecido se conserva de forma predeterminada.

La lista de paquetes explícitamente instalados se puede mostrar con `pacman -Qe`, mientras que la lista complementaria de dependencias se puede mostrar con `pacman -Qd`.

Para cambiar el motivo de la instalación de un paquete ya instalado, ejecute:

```
# pacman -D --asdeps *nombre_paquete*

```

Utilice `--asexplicit` para realizar la operación opuesta.

**Sugerencia:** instalar dependencias opcionales con `--asdeps` hará que, si se [eliminan paquetes huérfanos](/index.php/Pacman/Tips_and_tricks#Removing_unused_packages_.28orphans.29 "Pacman/Tips and tricks"), *pacman* también elimine estos restos de dependencias opcionales.

### Buscar un paquete que contenga un archivo específico

Sincronice la base de datos de archivos:

```
# pacman -Fy

```

Busque un paquete que contenga un archivo, por ejemplo:

```
# pacman -Fs pacman
core/pacman 5.0.1-4
    usr/bin/pacman
    usr/share/bash-completion/completions/pacman
extra/xscreensaver 5.36-1
    usr/lib/xscreensaver/pacman

```

**Sugerencia:** puede configurar un trabajo cron o un temporizador de systemd para sincronizar la base de datos de archivos regularmente.

Para obtener funcionalidades avanzadas instale [pkgfile](/index.php/Pkgfile "Pkgfile"), que utiliza una base de datos separada con todos los archivos y sus paquetes asociados.

## Configuración

La configuración de *pacman* se encuentra en el archivo `/etc/pacman.conf`. Este es el archivo donde el usuario configura el programa para que funcione de la manera deseada. Se puede encontrar información en profundidad sobre el archivo de configuración en [pacman.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5).

### Opciones Generales

Las opciones generales están en la sección `[options]`. Lea la página del manual de [pacman(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) o eche un vistazo al archivo predefinido `pacman.conf` para obtener información adicional.

#### Comparar versiones antes de actualizar

Para ver versiones antiguas y nuevas de paquetes disponibles, descomente la línea «VerbosePkgLists» en`/etc/pacman.conf`.La salida de `pacman -Syu` se verá así:

```
Package (6)             Old Version  New Version  Net Change  Download Size

extra/libmariadbclient  10.1.9-4     10.1.10-1      0.03 MiB       4.35 MiB
extra/libpng            1.6.19-1     1.6.20-1       0.00 MiB       0.23 MiB
extra/mariadb           10.1.9-4     10.1.10-1      0.26 MiB      13.80 MiB

```

#### Evitar la actualización de un paquete

**Advertencia:** tenga cuidado al omitir paquetes, ya que, como sabe, no son posibles las [actualizaciones parciales](/index.php/Partial_upgrades "Partial upgrades").

Para omitir la actualización de un paquete en particular cuando vaya a [actualizar](#Upgrading_packages) el sistema, debe especificarlo así:

```
IgnorePkg=linux

```

Para ignorar la actualización de varios paquetes, utilice una lista separada por espacios, o utilice líneas adicionales de `IgnorePkg`. También se pueden utilizar la sintaxis *«glob patterns»*. Si desea omitir paquetes pero solo una vez, puede utilizar la opción `--ignore` en la línea de órdenes, esta vez con una lista separada por comas.

Aún será posible actualizar los paquetes ignorados usando `pacman -S`: en este caso *pacman* le recordará que los paquetes han sido incluidos en una declaración de `IgnorePkg`.

#### Evitar la actualización de un grupo de paquetes

**Advertencia:** tenga cuidado al omitir grupo de paquetes, ya que, como sabe, no son posibles las [actualizaciones parciales](/index.php/Partial_upgrades "Partial upgrades").

Al igual que con los paquetes, saltarse un grupo de paquetes completo también es posible:

```
IgnoreGroup=gnome

```

#### Evitar la instalación de archivos en el sistema

Para ignorar siempre la instalación de archivos o directorios específicos, enumérelos en `NoExtract`. Por ejemplo, para evitar la instalación de unidades de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), proceda así:

```
NoExtract=usr/lib/systemd/system/*

```

Las reglas posteriores anulan las anteriores, pero se puede negar una regla añadiéndole el signo `!`.

**Sugerencia:** *pacman* emite mensajes de advertencia sobre locales que faltan al actualizar un paquete para el cual los locales han sido eliminados por *localepurge* o *bleachbit*. Comentando la opción `CheckSpace` en `pacman.conf` hace que se supriman tales advertencias, pero tenga en cuenta que la función de comprobación del espacio disponible en disco estará desactivada para todos los paquetes.

#### Mantener varios archivos de configuración

Si tiene varios archivos de configuración (por ejemplo, configuración principal y configuración para el repositorio [testing](/index.php/Testing "Testing") activado) y quiere compartir las opciones entre dichas configuraciones, puede utilizar la declaración `Include` de los archivos de configuración, por ejemplo:

```
Include = */ruta/a/configuraciones/comunes*

```

Donde el archivo `*/ruta/a/configuraciones/comunes*` contiene las mismas opciones para ambas configuraciones.

#### Hooks

*pacman* puede ejecutar hooks antes y después de la transacción, desde el directorio `/usr/share/libalpm/hooks/`; se pueden especificar más directorios con la opción `HookDir` en `pacman.conf`, cuya ruta por defecto es `/etc/pacman.d/hooks`. Los nombres de los archivos hooks deben tener el sufijo *.hook*.

Para obtener más información sobre los hooks de alpm, consulte [alpm-hooks(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/alpm-hooks.5).

### Repositorios y servidores de réplicas

Además de la sección especial [[options](#General_options)], cada valor `[section]` en `pacman.conf` define un repositorio de paquetes para ser utilizado. Un «repositorio» es una colección «lógica» de paquetes, los cuales están «físicamente» almacenados en uno o más servidores: por esta razón cada servidor se llama «espejo» (mirror) del repositorio.

Los repositorios se dividen en [oficiales](/index.php/Official_repositories "Official repositories") y [no oficiales](/index.php/Unofficial_user_repositories "Unofficial user repositories"). El orden de los repositorios en el archivo de configuración es importante; los repositorios listados primero en dicho archivo de configuración tendrán prioridad sobre los listados más adelante respecto de los paquetes presentes en dos repositorios cuando estos tengan nombres idénticos, independientemente del número de versión. Para usar un repositorio después de agregarlo, necesitará primero [actualizar](#Upgrading_packages) todo el sistema.

Cada sección del repositorio permite definir la lista de sus servidores de réplicas, bien directamente, bien en un archivo externo dedicado a través de la directiva `Include`: por ejemplo, los servidores de réplicas de los repositorios oficiales están incluidos en `/etc/pacman.d/mirrorlist`. Vea el artículo [Mirrors](/index.php/Mirrors "Mirrors") para la configuración de los servidores de réplicas.

#### Seguridad de los paquetes

*pacman* soporta firmas de los paquetes, que añaden una capa adicional de seguridad a los mismos. La configuración por defecto, `SigLevel = Required DatabaseOptional`, permite la verificación de las firmas para todos los paquetes a nivel global: esto puede ser anulado en la línea `SigLevel` de cada repositorio en cuestión. Para conocer más detalles sobre la firma de paquetes y la verificación de firma, eche un vistazo a [pacman-key](/index.php/Pacman-key "Pacman-key").

## Solución de problemas

### Error «Failed to commit transaction (conflicting files)»

Si ve el error siguiente: [[1]](https://bbs.archlinux.org/viewtopic.php?id=56373)

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
*package*: */path/to/file* exists in filesystem
Errors occurred, no packages were upgraded.

```

Esto sucede porque *pacman* ha detectado un conflicto de archivos, y por diseño, no sobrescribirá los archivos por usted. Esta es una característica de diseño, no un defecto.

El problema es generalmente trivial de resolver. Una forma segura es comprobar primero si el archivo pertenece a otro paquete (`pacman -Qo */path/to/file*`). Si el archivo es propiedad de otro paquete, [informe de un error de archivo](/index.php/Reporting_bug_guidelines "Reporting bug guidelines"). Si el archivo no es propiedad de otro paquete, cambie el nombre del archivo que existe en el sistema de archivos y vuelva a emitir la orden de actualización. Si todo va bien, el archivo puede ser eliminado.

Si ha instalado un programa manualmente sin usar *pacman* o utilizando un frontend, por ejemplo a través de `make install`, tiene que quitarlo con todos sus archivos, y volver a instalarlo correctamente usando *pacman*. Véase también [Pacman tips#Identify files not owned by any package](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips").

Cada paquete instalado proporciona un archivo `/var/lib/pacman/local/*$paquete-$versión*/files` que contiene metadatos sobre este paquete. Si este archivo se daña, está vacío o se pierde, produce errores del tipo `file exists in filesystem` al intentar actualizar el paquete. Este tipo de error suele referirse solo a un paquete. En lugar de renombrar manualmente y eliminar posteriormente todos los archivos que pertenecen al paquete en cuestión, puede ejecutar excepcionalmente `pacman -S --force $paquete` para forzar a *pacman* a sobrescribir estos archivos.

**Advertencia:** tenga cuidado cuando utilice el parámetro `--force` (por ejemplo `pacman -Syu --force`) ya que puede causar problemas importantes si se utiliza incorrectamente. Se recomienda encarecidamente que solo utilice esta opción cuando *«Arch news»* indique al usuario que lo haga.

### Error «Failed to commit transaction (invalid or corrupted package)»

Busque los archivos *.part* (paquetes parcialmente descargados) en `/var/cache/pacman/pkg` y elimínelos (a menudo causados por el uso de un parámetro `XferCommand` personalizado en `pacman.conf`).

```
# find /var/cache/pacman/pkg/ -iname "*.part" -exec rm {} \;

```

### Error «Failed to init transaction (unable to lock database)»

Cuando *pacman* está a punto de alterar las bases de datos de los paquetes, por ejemplo al instalar un paquete, crea un archivo de bloqueo en `/var/lib/pacman/db.lck`. Esto evita que otra instancia de *pacman* intente alterar la base de datos al mismo tiempo.

Si se interrumpe *pacman* mientras este altera la base de datos, este archivo de bloqueo obsoleto puede permanecer. Si está seguro de que no hay instancias de *pacman* ejecutándose, elimine el archivo de bloqueo:

```
# rm /var/lib/pacman/db.lck

```

### Los paquetes no se pueden recibir en la instalación

Este error se manifiesta como `Not found in sync db`, `Target not found` o `Failed retrieving file`.

En primer lugar, asegúrese de que el paquete existe realmente (¡y cuidado con los errores tipográficos!). Si ciertamente el paquete existe, es posible que la lista de paquetes esté desactualizada o que los repositorios estén configurados incorrectamente. Pruebe ejecutando `pacman -Syyu` para forzar una actualización de todas las listas de paquetes y, seguidamente, actualizar el sistema.

También podría ser que el repositorio que contiene el paquete no esté activado en su sistema, por ejemplo, el paquete podría estar en el repositorio *multilib*, pero el mismo no está activado en el archivo *pacman.conf*.

Véase también [FAQ#Why is there only a single version of each shared library in the official repositories?](/index.php/FAQ#Why_is_there_only_a_single_version_of_each_shared_library_in_the_official_repositories.3F "FAQ").

### Reinstalar manualmente pacman

**Advertencia:** es extremadamente fácil romper el sistema aún más utilizando este enfoque. Utilice esto como último recurso si el método descrito en la sección [#pacman se bloquea durante una actualización](#pacman_se_bloquea_durante_una_actualizaci.C3.B3n) no es una opción.

Incluso si *pacman* está seriamente dañado, puede arreglarse manualmente descargando los paquetes más recientes y extrayéndolos a las ubicaciones correctas. Los pasos ásperos a realizar son:

1.  determinar dependencias a instalar;
2.  descargar cada paquete de un repositorio de réplica de su elección;
3.  extraer cada paquete a la raíz del sistema;
4.  reinstalar estos paquetes con `pacman -Sf` para actualizar la base de datos del paquete;
5.  hacer una actualización completa del sistema.

Si dispone de un sistema Arch operativo, puede ver la lista completa de dependencias con:

```
$ pacman -Q $(pactree -u pacman)

```

pero es posible que solo tenga que actualizar algunas de ellas dependiendo de su problema. Un ejemplo de extracción de un paquete es:

```
# tar -xvpwf *package.tar.xz* -C / --exclude .PKGINFO --exclude .INSTALL

```

Observe el uso del parámetro `w` para ejecutar la orden en modo interactivo. Ejecutar la orden de forma no interactiva es muy arriesgado, ya que podría terminar sobrescribiendo un archivo importante. También debe tener cuidado de extraer los paquetes en el orden correcto (es decir, dependencias primero). [Esta publicación del foro](https://bbs.archlinux.org/viewtopic.php?id=95007) contiene un ejemplo de este proceso en el que solo se rompen un par de dependencias de *pacman*.

### pacman se bloquea durante una actualización

En el caso de que *pacman* se bloquee con un error de «database write» al eliminar paquetes, y, al intentar reinstalar o actualizar después otros paquetes, falla, haga lo siguiente:

1.  arranque Arch utilizando el soporte de instalación. Utilice preferentemente una imagen reciente que contenga una versión de pacman lo más coincidente con la de su sistema;
2.  monte el sistema de archivos raíz del sistema, por ejemplo, `mount /dev/sdaX /mnt` con privilegios de root, y compruebe que el montaje tenga suficiente espacio con `df -h`;
3.  monte también los sistemas de archivos proc y sysfs: `mount -t {proc,sysfs} /dev/sdaX {/mnt/proc, /mnt/sys}` ;
4.  si el sistema utiliza las ubicaciones por defecto de las bases de datos y directorios, ahora puede actualizar la base de datos de pacman y actualizar el sistema con `pacman --root=/mnt --cachedir=/mnt/var/cache/pacman/pkg -Syyu` como root;
5.  después de la actualización, una forma de comprobar si hay paquetes no actualizados pero que aún están rotos, es con: `find /mnt/usr/lib -size 0`;
6.  por último, reinstale cualquier paquete roto con `pacman --root /mnt --cachedir=/mnt/var/cache/pacman/pkg -S *paquete*`.

### Error «unable to find root device» después de reiniciar

Lo más probable es que su imagen initramfs se haya roto durante una actualización del kernel (el uso inadecuado de la opción `--force` de pacman puede ser una causa). Tiene dos opciones. En primer lugar, pruebe la entrada *Fallback*.

**Sugerencia:** en caso de que haya eliminado la entrada *Fallback*, siempre puede pulsar la tecla `Tab` cuando aparezca el menú del gestor de arranque (para Syslinux) o `e` (para GRUB o systemd-boot), renombrar la imagen a `initramfs-linux-fallback.img` y presionar `Enter` o `b` (dependiendo de su gestor de arranque) para arrancar con los nuevos parámetros.

Una vez que el sistema se haya iniciado, ejecute la siguiente orden (para el kernel de [linux](https://www.archlinux.org/packages/?name=linux) por defecto) desde la consola o desde un terminal para reconstruir la imagen initramfs:

```
# mkinitcpio -p linux

```

Si eso no funciona, desde una versión actual de Arch (CD/DVD o memoria USB), [monte](/index.php/Mount "Mount") las particiones root y boot. Luego [enjaule](/index.php/Chroot "Chroot") el sistema utilizando *arch-chroot*:

```
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd linux

```

**Nota:**

*   si no tiene una versión actual de Arch o si solo dispone de otra distribución Linux «live», puede [enjaular](/index.php/Chroot "Chroot") el sistema siguiendo la forma antigua. Obviamente, tendrá que escribir más que con la simple ejecución del script `arch-chroot`;
*   si *pacman* falla con el mensaje `Could not resolve host`, [compruebe su conexión a Internet](/index.php/Network_configuration#Check_the_connection "Network configuration");
*   si no puede entrar en el entorno arch-chroot o chroot, pero necesita reinstalar los paquetes, puede utilizar la orden `pacman -r /mnt -Syu foo bar` para ejecutar *pacman* sobre la partición raíz del sistema.

Al reinstalar el kernel (el paquete [linux](https://www.archlinux.org/packages/?name=linux)) se generará automáticamente la imagen initramfs con `mkinitcpio -p linux`. No hay necesidad de hacerlo por separado.

Después, se recomienda ejecutar `exit`, `umount /mnt/{boot,}` y `reboot`.

### Signature from "User <email@gmail.com>" is unknown trust, installation failed

Puede intentar:

*   actualizar las claves conocidas, es decir, `pacman-key --refresh-keys`;
*   actualizar manualmente el paquete [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) primero, es decir, ejecutando: `pacman -S archlinux-keyring`;
*   y, seguidamente, [restablecer todas las claves](/index.php/Pacman-key#Resetting_all_the_keys "Pacman-key").

### Solicitud para importar las claves PGP

Si [instala](/index.php/Installation_guide "Installation guide") Arch con una ISO obsoleta, es probable que se le pida que importe las claves PGP. Acepte, para descargar las claves y poder continuar. Si no puede agregar la clave PGP correctamente, actualice el depósito de llaves o actualice [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) (vea [lo anterior](#Signature_from_.22User_.3Cemail.40gmail.com.3E.22_is_unknown_trust.2C_installation_failed)).

### Error: key "0123456789ABCDEF" could not be looked up remotely

Si los paquetes se firman con claves nuevas, las cuales se agregaron a última hora a [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring), estas claves no estarán disponibles localmente durante la actualización (el dilema del huevo o la gallina). El llavero [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) no contendrá las claves (nuevas) hasta que se actualice. Pacman trata de evitar esto mediante una búsqueda a través de un servidor de claves, lo que no siempre es posible, por ejemplo, si nos encontramos detrás de un proxy o un cortafuegos, lo que dará como resultado el error indicado. Actualice [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) primero como se indica [arriba](#Signature_from_.22User_.3Cemail.40example.org.3E.22_is_unknown_trust.2C_installation_failed).

### Signature from "User <email@archlinux.org>" is invalid, installation failed

Cuando la hora del sistema es errónea, las claves de firma se consideran caducadas (o no válidas) y las comprobaciones de firma en los paquetes fallarán con el siguiente error:

```
error: *package*: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded.

```

Asegúrese de corregir la [hora](/index.php/Time "Time"), por ejemplo con `ntpd -qg` ejecutado como root, y luego `hwclock -w`, antes de realizar instalaciones o actualizaciones posteriores.

### Error «Warning: current locale is invalid; using default "C" locale»

Como indica el mensaje de error, la configuración del idioma no está establecida correctamente. Vea [Locale](/index.php/Locale "Locale").

### pacman no respeta los ajustes del proxy

Asegúrese de que las variables de entorno relevantes (`$http_proxy`, `$ftp_proxy`, etc.) están configuradas. Si utiliza *pacman* con [sudo](/index.php/Sudo "Sudo"), debe configurar sudo para que [pase estas variables de entorno a pacman](/index.php/Sudo#Environment_variables "Sudo").

### ¿Cómo reinstalar todos los paquetes, conservando la información sobre si algo se instaló explícitamente o como una dependencia?

Para reinstalar todos los paquetes nativos: `pacman -Qnq | pacman -S -` (la opción `-S` conserva el motivo de la instalación de forma predeterminada).

A continuación, tendrá que reinstalar todos los paquetes foráneos, que se pueden enumerar con `pacman -Qmq`.

### Error «Cannot open shared object file»

Este error se da cuando al ejecutar *pacman*, este hubiera eliminado o dañado las bibliotecas compartidas del mismo pacman.

Para recuperarse de esta situación es necesario descomprimir manualmente en su sistema de archivos las bibliotecas necesarias. En primer lugar, busque qué paquete contiene la biblioteca perdida y, luego, localícela en la caché de *pacman* (`/var/cache/pacman/pkg/`). Desempaquete la biblioteca compartida requerida por el sistema de archivos. Esto permitirá ejecutar *pacman*.

Ahora necesita [reinstalar](#Installing_specific_packages) el paquete roto. Tenga en cuenta que necesita utilizar el parámetro `--force` como si acabara de desempaquetar los archivos del sistema y *pacman* no lo supiera. *pacman* reemplazará correctamente nuestro archivo de biblioteca compartida con uno del paquete (reinstalado).

Hecho esto, actualice el resto del sistema.

### Descarga de paquetes congelada

Se han reportado algunos problemas relacionados con problemas de red que impiden que *pacman* actualice o sincronice los repositorios. [[2]](https://bbs.archlinux.org/viewtopic.php?id=68944) [[3]](https://bbs.archlinux.org/viewtopic.php?id=65728). Al instalar Arch Linux de forma nativa, estos problemas han sido resueltos remplazando el gestor de descargas de archivos *pacman* por defecto con otro alternativo (vea [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance") para obtener más detalles). Al instalar Arch Linux como SO invitado en [VirtualBox](/index.php/VirtualBox "VirtualBox"), este problema también se ha solucionado utilizando *Host interface* en lugar de *NAT* en las propiedades de la máquina.

### Error al recuperar el archivo 'core.db' del servidor de réplica

Si recibe este mensaje de error con los [mirrors](/index.php/Mirrors "Mirrors") correctos, intente establecer un [servidor de nombres](/index.php/Resolv.conf "Resolv.conf") diferente.

## Véase también

*   [Pacman Home Page](https://www.archlinux.org/pacman/)
*   [libalpm(3)](http://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3)
*   [pacman(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)
*   [pacman.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5)
*   [repo-add(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/repo-add.8)