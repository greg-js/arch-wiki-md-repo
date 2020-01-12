**Estado de la traducción**
Este artículo es una traducción de [pacman](/index.php/Pacman "Pacman"), revisada por última vez el **2019-09-15**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Pacman&diff=0&oldid=576411) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Creating packages (Español)](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)")
*   [Downgrading packages (Español)](/index.php/Downgrading_packages_(Espa%C3%B1ol) "Downgrading packages (Español)")
*   [pacman/Package signing (Español)](/index.php/Pacman/Package_signing_(Espa%C3%B1ol) "Pacman/Package signing (Español)")
*   [pacman/Pacnew and Pacsave (Español)](/index.php/Pacman/Pacnew_and_Pacsave_(Espa%C3%B1ol) "Pacman/Pacnew and Pacsave (Español)")
*   [pacman/Restore local database (Español)](/index.php/Pacman/Restore_local_database_(Espa%C3%B1ol) "Pacman/Restore local database (Español)")
*   [pacman/Rosetta (Español)](/index.php/Pacman/Rosetta_(Espa%C3%B1ol) "Pacman/Rosetta (Español)")
*   [pacman/Tips and tricks (Español)](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol) "Pacman/Tips and tricks (Español)")
*   [FAQ (Español)#Administración de paquetes](/index.php/FAQ_(Espa%C3%B1ol)#Administración_de_paquetes "FAQ (Español)")
*   [System maintenance (Español)](/index.php/System_maintenance_(Espa%C3%B1ol) "System maintenance (Español)")
*   [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")
*   [Official repositories (Español)](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")
*   [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")

El [gestor de paquetes](https://en.wikipedia.org/wiki/es:Sistema_de_gesti%C3%B3n_de_paquetes como las compilaciones realizadas por los propios usuarios.

*Pacman* mantiene el sistema actualizado mediante la sincronización con las listas de paquetes del servidor principal. Este modelo servidor/cliente le permite descargar y/o instalar paquetes con una simple orden y cubrir sus dependencias necesarias.

*Pacman* está escrito en lenguaje de programación [C (Español)](/index.php/C_(Espa%C3%B1ol) "C (Español)") y utiliza el formato [tar](https://en.wikipedia.org/wiki/es:tar "wikipedia:es:tar") de [bsdtar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bsdtar.1) para empaquetar.

**Sugerencia:** el paquete oficial [pacman](https://www.archlinux.org/packages/?name=pacman) también contiene otras herramientas útiles, tales como [makepkg (Español)](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)"), y *vercmp*. Otras herramientas útiles como [pactree](#Pactree) y [checkupdates](/index.php/Checkupdates "Checkupdates") se encuentran en [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) ([anteriormente](https://git.archlinux.org/pacman.git/commit/?id=0c99eabd50752310f42ec808c8734a338122ec86) parte de pacman). Ejecute `pacman -Ql pacman pacman-contrib | grep -E 'bin/.+'` para ver la lista completa.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Utilización](#Utilización)
    *   [1.1 Instalar paquetes](#Instalar_paquetes)
        *   [1.1.1 Instalar paquetes específicos](#Instalar_paquetes_específicos)
        *   [1.1.2 Instalar grupos de paquetes](#Instalar_grupos_de_paquetes)
    *   [1.2 Desinstalar paquetes](#Desinstalar_paquetes)
    *   [1.3 Actualizar paquetes](#Actualizar_paquetes)
    *   [1.4 Consultar la base de datos de los paquetes](#Consultar_la_base_de_datos_de_los_paquetes)
        *   [1.4.1 Pactree](#Pactree)
        *   [1.4.2 Estructura de la base de datos](#Estructura_de_la_base_de_datos)
    *   [1.5 Limpiar la memoria caché de los paquetes](#Limpiar_la_memoria_caché_de_los_paquetes)
    *   [1.6 Órdenes adicionales](#Órdenes_adicionales)
    *   [1.7 Motivo de la instalación](#Motivo_de_la_instalación)
    *   [1.8 Buscar un paquete que contenga un archivo específico](#Buscar_un_paquete_que_contenga_un_archivo_específico)
*   [2 Configuración](#Configuración)
    *   [2.1 Opciones generales](#Opciones_generales)
        *   [2.1.1 Comparar versiones antes de actualizar](#Comparar_versiones_antes_de_actualizar)
        *   [2.1.2 Evitar la actualización de un paquete](#Evitar_la_actualización_de_un_paquete)
        *   [2.1.3 Evitar la actualización de un grupo de paquetes](#Evitar_la_actualización_de_un_grupo_de_paquetes)
        *   [2.1.4 Evitar que un archivo sea actualizado](#Evitar_que_un_archivo_sea_actualizado)
        *   [2.1.5 Evitar la instalación de archivos en el sistema](#Evitar_la_instalación_de_archivos_en_el_sistema)
        *   [2.1.6 Mantener varios archivos de configuración](#Mantener_varios_archivos_de_configuración)
        *   [2.1.7 Hooks](#Hooks)
    *   [2.2 Repositorios y servidores de réplicas](#Repositorios_y_servidores_de_réplicas)
        *   [2.2.1 Seguridad de los paquetes](#Seguridad_de_los_paquetes)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 Error «Failed to commit transaction (conflicting files)»](#Error_«Failed_to_commit_transaction_(conflicting_files)»)
    *   [3.2 Error «Failed to commit transaction (invalid or corrupted package)»](#Error_«Failed_to_commit_transaction_(invalid_or_corrupted_package)»)
    *   [3.3 Error «Failed to init transaction (unable to lock database)»](#Error_«Failed_to_init_transaction_(unable_to_lock_database)»)
    *   [3.4 Los paquetes no se pueden recibir en la instalación](#Los_paquetes_no_se_pueden_recibir_en_la_instalación)
    *   [3.5 Reinstalar manualmente pacman](#Reinstalar_manualmente_pacman)
    *   [3.6 Pacman se bloquea durante una actualización](#Pacman_se_bloquea_durante_una_actualización)
    *   [3.7 Error «unable to find root device» después de reiniciar](#Error_«unable_to_find_root_device»_después_de_reiniciar)
    *   [3.8 Signature from "User <email@gmail.com>" is unknown trust, installation failed](#Signature_from_"User_<email@gmail.com>"_is_unknown_trust,_installation_failed)
    *   [3.9 Solicitud para importar las claves PGP](#Solicitud_para_importar_las_claves_PGP)
    *   [3.10 Error: key "0123456789ABCDEF" could not be looked up remotely](#Error:_key_"0123456789ABCDEF"_could_not_be_looked_up_remotely)
    *   [3.11 Signature from "User <email@archlinux.org>" is invalid, installation failed](#Signature_from_"User_<email@archlinux.org>"_is_invalid,_installation_failed)
    *   [3.12 Error «Warning: current locale is invalid; using default "C" locale»](#Error_«Warning:_current_locale_is_invalid;_using_default_"C"_locale»)
    *   [3.13 Pacman no respeta los ajustes del proxy](#Pacman_no_respeta_los_ajustes_del_proxy)
    *   [3.14 ¿Cómo reinstalar todos los paquetes, conservando la información sobre si algo se instaló explícitamente o como una dependencia?](#¿Cómo_reinstalar_todos_los_paquetes,_conservando_la_información_sobre_si_algo_se_instaló_explícitamente_o_como_una_dependencia?)
    *   [3.15 Error «Cannot open shared object file»](#Error_«Cannot_open_shared_object_file»)
    *   [3.16 Descarga de paquetes congelada](#Descarga_de_paquetes_congelada)
    *   [3.17 Error al recuperar el archivo 'core.db' del servidor de réplica](#Error_al_recuperar_el_archivo_'core.db'_del_servidor_de_réplica)
*   [4 Explicación comprensiva](#Explicación_comprensiva)
    *   [4.1 Qué sucede durante la instalación/actualización/eliminación de un paquete](#Qué_sucede_durante_la_instalación/actualización/eliminación_de_un_paquete)
*   [5 Véase también](#Véase_también)

## Utilización

Lo que sigue es una pequeña muestra de las operaciones que se pueden realizar con *pacman*. Para leer más ejemplos, remítase a [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8).

**Sugerencia:** para aquellos usuarios que han utilizado antes otras distribuciones de Linux, el artículo [Pacman Rosetta (Español)](/index.php/Pacman_Rosetta_(Espa%C3%B1ol) "Pacman Rosetta (Español)") les puede resultar útil.

### Instalar paquetes

**Nota:**

*   Los paquetes a menudo tienen [dependencias opcionales](/index.php/PKGBUILD#optdepends "PKGBUILD") que son paquetes que proporcionan funcionalidad adicional a la aplicación pero que no son estrictamente necesarios para ejecutarla. Al instalar un paquete, *pacman* enumerará las dependencias opcionales de un paquete, pero no se encontrarán en `pacman.log`. Utilice la orden [#Consultar la base de datos de los paquetes](#Consultar_la_base_de_datos_de_los_paquetes) para ver las dependencias opcionales de un paquete.
*   Al instalar un paquete que se requiera solo como dependencia (opcional) de algún otro paquete (es decir, no lo requiere explícitamente de otro modo), se recomienda utilizar la opción `--asdeps`. Para obtener más información, consulte la sección [#Motivo de la instalación](#Motivo_de_la_instalación).

**Advertencia:** al instalar paquetes en Arch, evite actualizar la lista de paquetes sin [actualizar el sistema](#Actualizar_paquetes) (imagine, por ejemplo, el caso de un [paquete que ya no se mantiene](#Los_paquetes_no_se_pueden_recibir_en_la_instalación) en los repositorios). En la práctica, **no** es aconsejable ejecutar `pacman -Sy *nombre_del_paquete*`, sino más bien `pacman -Sy**u** *nombre_del_paquete*`, ya que la primera orden podría ocasionar problemas de dependencia. Consulte [System maintenance (Español)#Las actualizaciones parciales no son compatibles](/index.php/System_maintenance_(Espa%C3%B1ol)#Las_actualizaciones_parciales_no_son_compatibles "System maintenance (Español)") y [BBS#89328](https://bbs.archlinux.org/viewtopic.php?id=89328).

#### Instalar paquetes específicos

Para instalar o actualizar un solo paquete o lista de paquetes (incluyendo las dependencias), ejecute la orden siguiente:

```
# pacman -S *nombre_del_paquete1* *nombre_del_paquete2* ...

```

Para instalar una lista de paquetes con una [expresión regular (regex)](https://en.wikipedia.org/wiki/Expresi%C3%B3n_regular "wikipedia:Expresión regular") (vea [este hilo del foro](https://bbs.archlinux.org/viewtopic.php?id=7179)):

```
# pacman -S $(pacman -Ssq *expresion-regular_paquete*)

```

A veces hay varias versiones de un paquete en diferentes repositorios (por ejemplo, *extra* y *testing*=. Para instalar la versión desde el repositorio *extra* en este ejemplo, el repositorio debe definirse delante del nombre del paquete:

```
# pacman -S extra/*nombre_del_paquete*

```

Para instalar un número de paquetes que comparten patrones similares en sus nombres uno puede usar la expansión de llaves. Por ejemplo:

```
# pacman -S plasma-{desktop,mediacenter,nm}

```

Esto se puede ampliar a los niveles que sean necesarios:

```
# pacman -S plasma-{workspace{,-wallpapers},pa}

```

#### Instalar grupos de paquetes

Algunos paquetes pertenecen a un [grupo de paquetes](/index.php/Package_group_(Espa%C3%B1ol) "Package group (Español)"), los cuales se pueden instalar simultáneamente. Por ejemplo, emitiendo la orden:

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
# pacman -R *nombre_del_paquete*

```

Para eliminar un paquete y sus dependencias (siempre que no sean usadas por ningún otro paquete instalado):

```
# pacman -Rs *nombre_del_paquete*

```

Para eliminar un paquete, sus dependencias y todos los paquetes que dependen de esas dependencias:

**Advertencia:** esta operación es recursiva, y debe utilizarse con precaución, ya que puede eliminar muchos paquetes potencialmente necesarios.

```
# pacman -Rsc *nombre_del_paquete*

```

Para eliminar un paquete, el cual es requerido por otro paquete, sin quitar el paquete dependiente:

**Advertencia:** la siguiente operación puede romper un sistema y debe evitarse. Ver [System maintenance (Español)#Evite ciertos comandos de pacman](/index.php/System_maintenance_(Espa%C3%B1ol)#Evite_ciertos_comandos_de_pacman "System maintenance (Español)").

```
# pacman -Rdd *nombre_del_paquete*

```

*Pacman* guarda los archivos de configuración importantes al quitar ciertas aplicaciones y los renombra con la extensión: *.pacsave*. Para evitar la creación de estos archivos de respaldo utilice la opción `-n`:

```
# pacman -Rn *nombre_del_paquete*

```

**Nota:** *pacman* no eliminará las configuraciones creadas por la aplicación misma (por ejemplo los «dotfiles» —archivos que comienzan con un punto— presentes en la carpeta personal [*«home»*]).

### Actualizar paquetes

**Advertencia:**

*   se espera que los usuarios se ilustren con la sección [System maintenance (Español)#Actualización del sistema](/index.php/System_maintenance_(Espa%C3%B1ol)#Actualización_del_sistema "System maintenance (Español)") para actualizar sus sistemas regularmente y no ejecuten a ciegas la orden de abajo;
*   Arch solo admite actualizaciones completas del sistema. Vea [System maintenance (Español)#Las actualizaciones parciales no son compatibles](/index.php/System_maintenance_(Espa%C3%B1ol)#Las_actualizaciones_parciales_no_son_compatibles "System maintenance (Español)") y [#Instalar paquetes](#Instalar_paquetes) para obtener más detalles.

*Pacman* puede actualizar todos los paquetes del sistema con una sola orden. Esto proceso puede durar bastante dependiendo de cuánto tiempo haya estado el sistema sin actualizar. La siguiente orden sincroniza las bases de datos de los repositorios *y* actualiza los paquetes del sistema (excluyendo los paquetes «locales» que no estén en los repositorios configurados):

```
# pacman -Syu

```

### Consultar la base de datos de los paquetes

*Pacman* puede consultar la base de datos de los paquetes presentes en el sistema con la opción `-Q`, las bases de datos de los servidores remotos con la opción `-S` y los archivos presentes en dichas bases con la opión `-F`. Vea `pacman -Q --help`, `pacman -S --help` y `pacman -F --help` para conocer las subopciones respectivas de cada opción.

*Pacman* puede buscar paquetes en la base de datos, la búsqueda se realiza tanto por los nombres como por las descripciones de los paquetes:

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
$ pacman -Si *nombre_del_paquete*

```

Para conocer los paquetes instalados en el sistema:

```
$ pacman -Qi *nombre_del_paquete*

```

Pasando la doble opción `-i` también se mostrará la lista de archivos de respaldo y sus estados de modificación:

```
$ pacman -Qii *nombre_del_paquete*

```

Para obtener una lista de los archivos instalados por un paquete:

```
$ pacman -Ql *nombre_del_paquete*

```

Para obtener un listado de los archivos instalados por un paquete recibido desde un servidor remoto:

```
$ pacman -Fl *nombre_del_paquete*

```

Para verificar la presencia de los archivos instalados por un paquete:

```
$ pacman -Qk *nombre_del_paquete*

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

Para listar todos los paquetes que no sean necesarios como dependencias (huérfanos):

```
$ pacman -Qdt

```

**Sugerencia:** añada la orden anterior a un [hook](#Hooks) postransaccional de pacman para recibir una notificación cuando una instalación deje huérfano un paquete. Esto puede ser útil para ser notificado cuando un paquete se ha descartado de un repositorio, ya que cualquier paquete eliminado también quedará huérfano en una instalación local (a menos que se haya instalado explícitamente). Para evitar cualquier error de «failed to execute command» cuando no se encuentran paquetes huérfanos, utilice la siguiente orden para `Exec` en su hook: `/usr/bin/bash -c "/usr/bin/pacman -Qtd || /usr/bin/echo '=> None found.'"`

Para listar todos los paquetes explícitamente instalados y no requeridos como dependencias:

```
$ pacman -Qet

```

Véase [Pacman/Tips and tricks (Español)](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol) "Pacman/Tips and tricks (Español)") para más ejemplos.

#### Pactree

**Nota:** [pactree(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pactree.8) ya no es parte del paquete [pacman](https://www.archlinux.org/packages/?name=pacman). En cambio, se puede encontrar en [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib).

Para ver el árbol de dependencias de un paquete:

```
$ pactree *nombre_del_paquete*

```

Para ver el árbol dependiente de un paquete, pase la opción inversa `-r` a *pactree*, o utilice *whoneeds* desde [pkgtools](https://aur.archlinux.org/packages/pkgtools/).

#### Estructura de la base de datos

Las bases de datos de *pacman* se encuentran, normalmente, en `/var/lib/pacman/sync`. Para cada repositorio especificado en `/etc/pacman.conf` habrá su correspondiente archivo de base de datos ubicado allí. Los archivos de base de datos son archivos en formato tar-gzip que contienen un directorio para cada paquete, por ejemplo para el paquete [which](https://www.archlinux.org/packages/?name=which):

```
% tree which-2.20-6 
which-2.20-6
|-- depends
`-- desc

```

El archivo `depends` enumera los paquetes de los que depende este paquete, mientras que el archivo `desc` contiene una descripción del paquete, como el tamaño del archivo y el hash MD5.

### Limpiar la memoria caché de los paquetes

*Pacman* almacena los paquetes descargados en `/var/cache/pacman/pkg/` y no elimina las versiones antiguas o desinstaladas automáticamente. Esto tiene algunas ventajas:

1.  Permite realizar [downgrade](/index.php/Downgrade "Downgrade") de un paquete sin necesidad de recuperar la versión anterior por otros medios, como de [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive").
2.  Un paquete que se ha desinstalado se puede reinstalar fácilmente directamente desde la carpeta caché, sin necesidad de una nueva descarga desde el repositorio.

Sin embargo, es necesario limpiar deliberadamente la caché periódicamente para evitar que la carpeta crezca indefinidamente en tamaño.

El script *paccache*, proporcionado dentro del paquete [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib), elimina todas las versiones en caché de los paquetes instalados y desinstalados, excepto los 3 más recientes, por defecto:

```
 # paccache -r

```

[Active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") e [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `paccache.timer` para descartar paquetes no utilizados semanalmente.

**Sugerencia:** Puede crear [#Hooks](#Hooks) para ejecutar esto automáticamente después de cada transacción de pacman, [vea ejemplos](https://bbs.archlinux.org/viewtopic.php?pid=1694743#p1694743).

También puede definir cuántas versiones recientes desea conservar. Para conservar solo una versión anterior, utilice:

```
# paccache -rk1

```

Añada la opción `u` para limitar la acción de *paccache* a los paquetes desinstalados. Por ejemplo, para eliminar todas las versiones en caché de paquetes desinstalados, utilice lo siguiente:

```
# paccache -ruk0

```

Véase `paccache -h` para más opcioines.

*Pacman* también tiene algunas opciones integradas para limpiar el caché y los archivos de base de datos sobrantes de los repositorios que ya no figuran en el archivo de configuración de `/etc/pacman.conf`. Sin embargo, *pacman* no ofrece la posibilidad de mantener una serie de versiones anteriores y, por lo tanto, es más agresivo que las opciones predeterminadas de *paccache*.

Para eliminar todos los paquetes en caché que no están instalados actualmente, y la base de datos de sincronización no utilizada, ejecute:

```
 # pacman -Sc

```

**Advertencia:** se deben evitar eliminar de la caché todas las versiones anteriores de los paquetes instalados y todos los paquetes desinstalados, a menos que se necesite desesperadamente liberar espacio en el disco. Esto permitirá degradar o reinstalar paquetes sin descargarlos nuevamente.

[pkgcacheclean](https://aur.archlinux.org/packages/pkgcacheclean/) y [pacleaner](https://aur.archlinux.org/packages/pacleaner/) son dos alternativas más para limpiar la caché.

### Órdenes adicionales

Descargar un paquete sin instalarlo:

```
# pacman -Sw *nombre_del_paquete*

```

Instalar un paquete «local» que no proviene de un repositorio remoto (por ejemplo, el paquete proviene de [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)")):

```
# pacman -U /ruta/al/paquete/nombre_del_paquete-versión.pkg.tar.xz

```

Para mantener una copia del paquete local en la caché de *pacman*, utilice:

```
# pacman -U file://ruta/al/paquete/nombre_del_paquete-versión.pkg.tar.xz

```

Instalar un paquete 'remoto' (no de un repositorio indicado en los archivos de configuración de pacman):

```
# pacman -U http://www.ejemplo.com/repo/ejemplo.pkg.tar.xz

```

Para inhibir las acciones derivadas de `-S`, `-U` y `-R`, puede utilizarse `-p`.

*Pacman* siempre enumerará los paquetes que se van a instalar o eliminar y pedirá permiso antes de realizar la acción.

### Motivo de la instalación

La base de datos de *pacman* diferencia los paquetes instalados en dos grupos, de acuerdo a la razón por la que fueron instalados:

*   **explicitly-installed**: (instalado explícitamente), son aquellos paquetes que se instalaron con una orden genérica de *pacman* como `-S` o `-U`;
*   **dependencies**: (dependencias), son aquellos paquetes que, pese a que nunca se pasaron (en general) por una orden de instalación de *pacman*, fueron implícitamente instalados porque eran [requeridos](/index.php/Dependency "Dependency") por otro paquete que fue explícitamente instalado.

Al instalar un paquete, es posible forzar su motivo de instalación a *dependency* con:

```
# pacman -S --asdeps *nombre_del_paquete*

```

**Sugerencia:** la instalación de dependencias opcionales con `--asdeps` lo hará de tal manera que si [eliminan paquetes huérfanos](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol)#Eliminar_paquetes_no_utilizados_(huérfanos) "Pacman/Tips and tricks (Español)"), *pacman* también eliminará las dependencias opcionales de ellos.

Cuando se **re**instala un paquete, no obstante, el motivo de instalación establecido se conserva de forma predeterminada.

La lista de paquetes explícitamente instalados se puede mostrar con `pacman -Qe`, mientras que la lista complementaria de dependencias se puede mostrar con `pacman -Qd`.

Para cambiar el motivo de la instalación de un paquete ya instalado, ejecute:

```
# pacman -D --asdeps *nombre_del_paquete*

```

Utilice `--asexplicit` para realizar la operación opuesta.

**Nota:** se desaconseja utilizar las opciones `--asdeps` y `--asexplicit` al actualizar, de este modo `pacman -Syu *nombre_del_paquete* --asdeps`. Esto cambiaría la razón de instalación no solo del paquete que se está instalando, sino también de los paquetes que se están actualizando.

### Buscar un paquete que contenga un archivo específico

Sincronice la base de datos de archivos:

```
# pacman -Fy

```

Busque un paquete que contenga un archivo, por ejemplo:

```
$ pacman -Fs pacman
core/pacman 5.0.1-4
    usr/bin/pacman
    usr/share/bash-completion/completions/pacman
extra/xscreensaver 5.36-1
    usr/lib/xscreensaver/pacman

```

**Sugerencia:** puede configurar un trabajo cron o un temporizador de systemd para sincronizar la base de datos de archivos regularmente.

Para obtener funcionalidades avanzadas instale [pkgfile (Español)](/index.php/Pkgfile_(Espa%C3%B1ol) "Pkgfile (Español)"), que utiliza una base de datos separada con todos los archivos y sus paquetes asociados.

## Configuración

La configuración de *pacman* se encuentra en el archivo `/etc/pacman.conf`. Este es el archivo donde el usuario configura el programa para que funcione de la manera deseada. Se puede encontrar información en profundidad sobre el archivo de configuración en [pacman.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5).

### Opciones generales

Las opciones generales están en la sección `[options]`. Lea la página del manual de [pacman.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5) o eche un vistazo al archivo predefinido `pacman.conf` para obtener información adicional.

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

Para omitir la actualización de un paquete en particular cuando vaya a [actualizar](#Actualizar_paquetes) el sistema, debe especificarlo así:

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

#### Evitar que un archivo sea actualizado

Todos los archivos enumerados con una directiva`NoUpgrade` nunca se tocarán durante la instalación/actualización de un paquete, y los nuevos archivos se instalarán con una extensión *.pacnew*.

```
NoUpgrade=*ruta/al/archivo*

```

**Nota:** la ruta se refiere a los archivos del paquete. Por lo tanto, no incluya la barra inclinada.

#### Evitar la instalación de archivos en el sistema

Para ignorar siempre la instalación de archivos o directorios específicos, enumérelos en `NoExtract`. Por ejemplo, para evitar la instalación de unidades de [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), proceda así:

```
NoExtract=usr/lib/systemd/system/*

```

Las reglas posteriores anulan las anteriores, pero se puede negar una regla añadiéndole el signo `!`.

**Sugerencia:** *pacman* emite mensajes de advertencia sobre locales que faltan al actualizar un paquete para el cual los locales han sido eliminados por *localepurge* o *bleachbit*. Comentando la opción `CheckSpace` en `pacman.conf` hace que se supriman tales advertencias, pero tenga en cuenta que la función de comprobación del espacio disponible en disco estará desactivada para todos los paquetes.

#### Mantener varios archivos de configuración

Si tiene varios archivos de configuración (por ejemplo, configuración principal y configuración para el repositorio [testing (Español)](/index.php/Testing_(Espa%C3%B1ol) "Testing (Español)") activado) y quiere compartir las opciones entre dichas configuraciones, puede utilizar la declaración `Include` de los archivos de configuración, por ejemplo:

```
Include = */ruta/a/configuraciones/comunes*

```

Donde el archivo `*/ruta/a/configuraciones/comunes*` contiene las mismas opciones para ambas configuraciones.

#### Hooks

*Pacman* puede ejecutar hooks antes y después de la instalación, desde el directorio `/usr/share/libalpm/hooks/`; se pueden especificar más directorios con la opción `HookDir` en `pacman.conf`, cuya ruta por defecto es `/etc/pacman.d/hooks`. Los nombres de los archivos hooks deben tener el sufijo *.hook*.

Los hooks de *pacman* se usan, por ejemplo, en combinación con `systemd-sysusers` y `systemd-tmpfiles` para crear automáticamente usuarios y archivos del sistema durante la instalación de paquetes. Por ejemplo, el paquete `tomcat8` especifica que quiere un usuario del sistema llamado `tomcat8`y ciertos directorios propiedad de este usuario. Los hooks de *pacman* `systemd-sysusers.hook` y `systemd-tmpfiles.hook` invocan a `systemd-sysusers` y `systemd-tmpfiles` cuando *pacman* determina que el paquete `tomcat8` contiene archivos que especifican usuarios y archivos en tmp.

Para obtener más información sobre los hooks de alpm, consulte [alpm-hooks(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/alpm-hooks.5).

### Repositorios y servidores de réplicas

Además de la sección especial [[options]](#Opciones_generales), cada valor `[section]` en `pacman.conf` define un repositorio de paquetes para ser utilizado. Un «repositorio» es una colección «lógica» de paquetes, los cuales están «físicamente» almacenados en uno o más servidores: por esta razón cada servidor se llama «espejo» (mirror) del repositorio.

Los repositorios se dividen en [oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") y [no oficiales](/index.php/Unofficial_user_repositories "Unofficial user repositories"). El orden de los repositorios en el archivo de configuración es importante; los repositorios listados primero en dicho archivo de configuración tendrán prioridad sobre los listados más adelante respecto de los paquetes presentes en dos repositorios cuando estos tengan nombres idénticos, independientemente del número de versión. Para usar un repositorio después de agregarlo, necesitará primero [actualizar](#Actualizar_paquetes) todo el sistema.

Cada sección del repositorio permite definir la lista de sus servidores de réplicas, bien directamente, bien en un archivo externo dedicado a través de la directiva `Include`: por ejemplo, los servidores de réplicas de los repositorios oficiales están incluidos en `/etc/pacman.d/mirrorlist`. Vea el artículo [Mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)") para la configuración de los servidores de réplicas.

#### Seguridad de los paquetes

*Pacman* soporta firmas de los paquetes, que añaden una capa adicional de seguridad a los mismos. La configuración por defecto, `SigLevel = Required DatabaseOptional`, permite la verificación de las firmas para todos los paquetes a nivel global: esto puede ser anulado en la línea `SigLevel` de cada repositorio en cuestión. Para conocer más detalles sobre la firma de paquetes y la verificación de firma, eche un vistazo a [pacman-key (Español)](/index.php/Pacman-key_(Espa%C3%B1ol) "Pacman-key (Español)").

## Solución de problemas

### Error «Failed to commit transaction (conflicting files)»

Si ve el error siguiente: [[1]](https://bbs.archlinux.org/viewtopic.php?id=56373)

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
*package*: */path/to/file* exists in filesystem
Errors occurred, no packages were upgraded.

```

Esto sucede porque *pacman* ha detectado un conflicto de archivos, y por diseño, no sobrescribirá los archivos por usted. Esta es por diseño, no un defecto.

El problema es generalmente trivial de resolver. Una forma segura es comprobar primero si el archivo pertenece a otro paquete (`pacman -Qo */ruta/al/archivo*`). Si el archivo es propiedad de otro paquete, [informe de un error de archivo](/index.php/Reporting_bug_guidelines "Reporting bug guidelines"). Si el archivo no es propiedad de otro paquete, cambie el nombre del archivo que existe en el sistema de archivos y vuelva a emitir la orden de actualización. Si todo va bien, el archivo puede ser eliminado.

Si ha instalado un programa manualmente sin usar *pacman* o utilizando un frontend, por ejemplo a través de `make install`, tiene que quitar/desinstalar estos programas con todos sus archivos. Véase también [pacman/Tips and tricks (Español)#Identificar archivos que no pertenecen a ningún paquete](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol)#Identificar_archivos_que_no_pertenecen_a_ningún_paquete "Pacman/Tips and tricks (Español)").

Cada paquete instalado proporciona un archivo `/var/lib/pacman/local/*$paquete-$versión*/files` que contiene metadatos sobre este paquete. Si este archivo se daña, está vacío o se pierde, produce errores del tipo `file exists in filesystem` al intentar actualizar el paquete. Este tipo de error suele referirse solo a un paquete. En lugar de renombrar manualmente y eliminar posteriormente todos los archivos que pertenecen al paquete en cuestión, puede ejecutar explícitamente`pacman -S --overwrite *glob* *paquete*` para forzar a *pacman* a sobrescribir estos archivos que empareja `*glob*`.

**Advertencia:** en general, evite utilizar la opción `--overwrite`. Consulte [System maintenance (Español)#Evite ciertos comandos de pacman](/index.php/System_maintenance_(Espa%C3%B1ol)#Evite_ciertos_comandos_de_pacman "System maintenance (Español)").

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

En primer lugar, asegúrese de que el paquete existe realmente. Si ciertamente el paquete existe, es posible que la lista de paquetes esté desactualizada. Pruebe ejecutando `pacman -Syu` para forzar una actualización de todas las listas de paquetes y, seguidamente, actualizar el sistema. Asegúrese también de que los [mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)") estén actualizados y de que los [repositorios](#Repositorios_y_servidores_de_réplicas) estén configurados correctamente.

También podría ser que el repositorio que contiene el paquete no esté activado en su sistema, por ejemplo, el paquete podría estar en el repositorio [multilib (Español)](/index.php/Multilib_(Espa%C3%B1ol) "Multilib (Español)") , pero el mismo no está activado en el archivo `pacman.conf`.

Consulte también: [¿Por qué hay solo una única versión de cada biblioteca compartida en los repositorios oficiales?](/index.php/Frequently_asked_questions_(Espa%C3%B1ol)#¿Por_qué_hay_solo_una_única_versión_de_cada_biblioteca_compartida_en_los_repositorios_oficiales? "Frequently asked questions (Español)")

### Reinstalar manualmente pacman

**Advertencia:** es extremadamente fácil romper el sistema aún más utilizando este enfoque. Utilice esto como último recurso si el método descrito en la sección [#Pacman se bloquea durante una actualización](#Pacman_se_bloquea_durante_una_actualización) no es una opción.

Incluso si *pacman* está seriamente dañado, puede arreglarse manualmente descargando los paquetes más recientes y extrayéndolos a las ubicaciones correctas. Los pasos ásperos a realizar son:

1.  determinar dependencias de [pacman](https://www.archlinux.org/packages/?name=pacman) a instalar;
2.  descargar cada paquete de un [repositorio de réplica](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)") de su elección;
3.  extraer cada paquete a la raíz del sistema;
4.  reinstalar estos paquetes con `pacman -S --overwrite` para actualizar la base de datos del paquete;
5.  hacer una actualización completa del sistema.

Si dispone de un sistema Arch operativo, puede ver la lista completa de dependencias con:

```
$ pacman -Q $(pactree -u pacman)

```

Pero es posible que solo tenga que actualizar algunas de ellas dependiendo de su problema. Un ejemplo de extracción de un paquete es:

```
# tar -xvpwf *package.tar.xz* -C / --exclude .PKGINFO --exclude .INSTALL --exclude .MTREE --exclude .BUILDINFO

```

Observe el uso del parámetro `w` para ejecutar la orden en modo interactivo. Ejecutar la orden de forma no interactiva es muy arriesgado, ya que podría terminar sobrescribiendo un archivo importante. También debe tener cuidado de extraer los paquetes en el orden correcto (es decir, dependencias primero). [Esta publicación del foro](https://bbs.archlinux.org/viewtopic.php?id=95007) contiene un ejemplo de este proceso en el que solo se rompen un par de dependencias de *pacman*.

### Pacman se bloquea durante una actualización

En el caso de que *pacman* se bloquee con un error de «database write» al eliminar paquetes, y, al intentar reinstalar o actualizar después otros paquetes, falla, haga lo siguiente:

1.  arranque Arch utilizando el soporte de instalación. Utilice preferentemente una imagen reciente que contenga una versión de pacman lo más coincidente con la de su sistema;
2.  monte el sistema de archivos raíz del sistema, por ejemplo, `mount /dev/sdaX /mnt` con privilegios de root, y compruebe que el montaje tenga suficiente espacio con `df -h`;
3.  monte también los sistemas de archivos proc, sysfs y dev, así: `mount -t proc proc /mnt/proc; mount --rbind /sys /mnt/sys; mount --rbind /dev /mnt/dev` ;
4.  si el sistema utiliza las ubicaciones por defecto de las bases de datos y directorios, ahora puede actualizar la base de datos de pacman y actualizar el sistema con `pacman --sysroot /mnt -Syu` como root;
5.  después de la actualización, una forma de comprobar si hay paquetes no actualizados pero que aún están rotos, es con: `find /mnt/usr/lib -size 0`;
6.  por último, reinstale cualquier paquete roto con `pacman --sysroot /mnt -S *paquete*`.

### Error «unable to find root device» después de reiniciar

Lo más probable es que su imagen [initramfs (Español)](/index.php/Initramfs_(Espa%C3%B1ol) "Initramfs (Español)") se haya roto durante una actualización del [kernel (Español)](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)") (el uso inadecuado de la opción `--force` de *pacman* puede ser una causa). Tiene dos opciones. En primer lugar, pruebe la entrada *Fallback*.

**Sugerencia:** en caso de que haya eliminado la entrada *Fallback*, siempre puede pulsar la tecla `Tab` cuando aparezca el menú del gestor de arranque (para Syslinux) o `e` (para GRUB o systemd-boot), renombrar la imagen a `initramfs-linux-fallback.img` y presionar `Intro` o `b` (dependiendo de su [gestor de arranque](/index.php/Boot_loader_(Espa%C3%B1ol) "Boot loader (Español)")) para arrancar con los nuevos parámetros.

Una vez que el sistema se haya iniciado, ejecute la siguiente orden (para el kernel de [linux](https://www.archlinux.org/packages/?name=linux) por defecto) desde la consola o desde un terminal para reconstruir la imagen initramfs:

```
# mkinitcpio -p linux

```

Si eso no funciona, desde una versión actual de Arch (CD/DVD o memoria USB), [monte](/index.php/Mount_(Espa%C3%B1ol) "Mount (Español)") las particiones root y boot. Luego [enjaule](/index.php/Chroot_(Espa%C3%B1ol) "Chroot (Español)") el sistema utilizando *arch-chroot*:

```
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd linux

```

**Nota:**

*   si no tiene una versión actual de Arch o si solo dispone de otra distribución Linux «live», puede [enjaular](/index.php/Chroot_(Espa%C3%B1ol) "Chroot (Español)") el sistema siguiendo la forma antigua. Obviamente, tendrá que escribir más que con la simple ejecución del script `arch-chroot`;
*   si *pacman* falla con el mensaje `Could not resolve host`, [compruebe su conexión a Internet](/index.php/Network_configuration_(Espa%C3%B1ol)#Comprobar_la_conexión "Network configuration (Español)");
*   si no puede entrar en el entorno arch-chroot o chroot, pero necesita reinstalar los paquetes, puede utilizar la orden `pacman --sysroot /mnt -Syu foo bar` para ejecutar *pacman* sobre la partición raíz del sistema.

Al reinstalar el kernel (el paquete [linux](https://www.archlinux.org/packages/?name=linux)) se generará automáticamente la imagen initramfs con `mkinitcpio -p linux`. No hay necesidad de hacerlo por separado.

Después, se recomienda ejecutar `exit`, `umount /mnt/{boot,}` y `reboot`.

### Signature from "User <email@gmail.com>" is unknown trust, installation failed

Soluciones potenciales:

*   actualizar las claves conocidas, es decir, `pacman-key --refresh-keys`;
*   actualizar manualmente el paquete [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) primero, es decir, ejecutando: `pacman -S archlinux-keyring`;
*   y, seguidamente, [restablecer todas las claves](/index.php/Pacman-key_(Espa%C3%B1ol)#Restablecer_todas_las_claves "Pacman-key (Español)").

### Solicitud para importar las claves PGP

Si [instala](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") Arch con una ISO obsoleta, es probable que se le pida que importe las claves PGP. Acepte, para descargar las claves y poder continuar. Si no puede agregar la clave PGP correctamente, actualice el depósito de llaves o actualice [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) (vea [lo anterior](#Signature_from_"User_<email@gmail.com>"_is_unknown_trust,_installation_failed)).

### Error: key "0123456789ABCDEF" could not be looked up remotely

Si los paquetes se firman con claves nuevas, las cuales se agregaron a última hora a [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring), estas claves no estarán disponibles localmente durante la actualización (el dilema del huevo o la gallina). El llavero [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) no contendrá las claves (nuevas) hasta que se actualice. Pacman trata de evitar esto mediante una búsqueda a través de un servidor de claves, lo que no siempre es posible, por ejemplo, si nos encontramos detrás de un proxy o un cortafuegos, lo que dará como resultado el error indicado. Actualice [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) primero como se indica [arriba](#Signature_from_"User_<email@example.org>"_is_unknown_trust,_installation_failed).

### Signature from "User <email@archlinux.org>" is invalid, installation failed

Cuando la hora del sistema es errónea, las claves de firma se consideran caducadas (o no válidas) y las comprobaciones de firma en los paquetes fallarán con el siguiente error:

```
error: *package*: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded.

```

Asegúrese de corregir la [hora](/index.php/System_time_(Espa%C3%B1ol) "System time (Español)"), por ejemplo con `ntpd -qg` ejecutado como root, y luego `hwclock -w`, antes de realizar instalaciones o actualizaciones posteriores.

### Error «Warning: current locale is invalid; using default "C" locale»

Como indica el mensaje de error, la configuración del idioma no está establecida correctamente. Vea [Locale (Español)](/index.php/Locale_(Espa%C3%B1ol) "Locale (Español)").

### Pacman no respeta los ajustes del proxy

Asegúrese de que las variables de entorno relevantes (`$http_proxy`, `$ftp_proxy`, etc.) están configuradas. Si utiliza *pacman* con [sudo (Español)](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)"), debe configurar sudo para que [pase estas variables de entorno a pacman](/index.php/Sudo_(Espa%C3%B1ol)#Variables_de_entorno "Sudo (Español)").

### ¿Cómo reinstalar todos los paquetes, conservando la información sobre si algo se instaló explícitamente o como una dependencia?

Para reinstalar todos los paquetes nativos: `pacman -Qnq | pacman -S -` (la opción `-S` conserva el motivo de la instalación de forma predeterminada).

A continuación, tendrá que reinstalar todos los paquetes foráneos, que se pueden enumerar con `pacman -Qmq`.

### Error «Cannot open shared object file»

Este error se da cuando al ejecutar *pacman*, este hubiera eliminado o dañado las bibliotecas compartidas del mismo *pacman*.

Para recuperarse de esta situación es necesario descomprimir manualmente en su sistema de archivos las bibliotecas necesarias. En primer lugar, busque qué paquete contiene la biblioteca perdida y, luego, localícela en la caché de *pacman* (`/var/cache/pacman/pkg/`). Desempaquete la biblioteca compartida requerida por el sistema de archivos. Esto permitirá ejecutar *pacman*.

Ahora necesita [reinstalar](#Instalar_paquetes_específicos) el paquete roto. Tenga en cuenta que necesita utilizar el parámetro `--overwrite` como si acabara de desempaquetar los archivos del sistema y *pacman* no lo supiera. *Pacman* reemplazará correctamente nuestro archivo de biblioteca compartida con uno del paquete (reinstalado).

Hecho esto, actualice el resto del sistema.

### Descarga de paquetes congelada

Se han reportado algunos problemas relacionados con problemas de red que impiden que *pacman* actualice o sincronice los repositorios. [[2]](https://bbs.archlinux.org/viewtopic.php?id=68944) [[3]](https://bbs.archlinux.org/viewtopic.php?id=65728). Al instalar Arch Linux de forma nativa, estos problemas han sido resueltos remplazando el gestor de descargas de archivos *pacman* por defecto con otro alternativo (vea [Improve pacman performance (Español)](/index.php/Improve_pacman_performance_(Espa%C3%B1ol) "Improve pacman performance (Español)") para obtener más detalles). Al instalar Arch Linux como sistema operativo invitado en [VirtualBox (Español)](/index.php/VirtualBox_(Espa%C3%B1ol) "VirtualBox (Español)"), este problema también se ha solucionado utilizando *Host interface* en lugar de *NAT* en las propiedades de la máquina.

### Error al recuperar el archivo 'core.db' del servidor de réplica

Si recibe este mensaje de error con los [mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)") correctos, intente establecer un [servidor de nombres](/index.php/Domain_name_resolution_(Espa%C3%B1ol) "Domain name resolution (Español)") diferente.

## Explicación comprensiva

### Qué sucede durante la instalación/actualización/eliminación de un paquete

Al completar con éxito la operación de un paquete, *pacman* realiza los siguientes pasos de alto nivel:

1.  *pacman* obtiene los archivos del paquete que se instalará para todos los paquetes en cola en una sola operación.
2.  *pacman* realizará varias comprobaciones de que los paquetes tienen posibilidad de instalarse.
3.  Si existen hooks de `PreTransaction` de *pacman* aplicables, estos se ejecutarán.
4.  Cada paquete se instala/actualiza/elimina a la vez.
    1.  Si el paquete tiene un script de instalación, se ejecuta su función `pre_install` (o `pre_upgrade` o `pre_remove` en el caso de un paquete actualizado o eliminado, respectivamente).
    2.  *pacman* elimina todos los archivos de una versión preexistente del paquete (en el caso de un paquete actualizado o eliminado). Sin embargo, los archivos que se marcaron como archivos de configuración en el paquete se mantendrán (consulte [Pacman/Pacnew and Pacsave (Español)](/index.php/Pacman/Pacnew_and_Pacsave_(Espa%C3%B1ol) "Pacman/Pacnew and Pacsave (Español)")).
    3.  *pacman* libera el paquete y vuelca sus archivos en el sistema de archivos (en el caso de un paquete instalado o actualizado). Los archivos que sobrescriban los archivos de configuración guardados y los modificados manualmente (consulte el paso anterior) se almacenan con un nuevo nombre (.pacnew).
    4.  Si el paquete tiene un script de instalación, se ejecuta su función (or `post_upgrade` o `post_remove` en el caso de un paquete actualizado o eliminado, respectivamente).
5.  Si existen hooks de `PostTransaction` de *pacman* aplicables al final de la instalación, estos se ejecutarán.

## Véase también

*   [Pacman Home Page](https://www.archlinux.org/pacman/)
*   [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3)
*   [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)
*   [pacman.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5)
*   [repo-add(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/repo-add.8)