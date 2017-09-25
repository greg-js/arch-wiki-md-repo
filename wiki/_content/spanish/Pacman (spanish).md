Artículos relacionados

*   [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages")
*   [Improve Pacman Performance (Español)](/index.php/Improve_Pacman_Performance_(Espa%C3%B1ol) "Improve Pacman Performance (Español)")
*   [Pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends")
*   [Pacman Rosetta (Español)](/index.php/Pacman_Rosetta_(Espa%C3%B1ol) "Pacman Rosetta (Español)")
*   [Pacman tips](/index.php/Pacman_tips "Pacman tips")
*   [Pacman package signing](/index.php/Pacman_package_signing "Pacman package signing")
*   [FAQ (Español)#Gestión de paquetes](/index.php/FAQ_(Espa%C3%B1ol)#Gesti.C3.B3n_de_paquetes "FAQ (Español)")
*   [pacman-key](/index.php/Pacman-key "Pacman-key")
*   [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files")
*   [List of Applications/Utilities (Español)#Gestores de paquetes](/index.php/List_of_Applications/Utilities_(Espa%C3%B1ol)#Gestores_de_paquetes "List of Applications/Utilities (Español)")
*   [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")
*   [Official Repositories (Español)](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)")
*   [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")

El [gestor de paquetes de pacman](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system") es una de las principales características distintivas de Arch Linux. Combina un simple formato de paquetes binarios con un fácil [sistema de compilación de paquetes](/index.php/Arch_Build_System "Arch Build System"). El objetivo de pacman es hacer posible gestionar fácilmente los paquetes, si son de los [repositorios oficiales de Arch](/index.php/Official_repositories "Official repositories") o compilaciones propias del usuario.

Pacman mantiene el sistema actualizado y sincronizado con la listas de paquetes del servidor principal. Este modelo servidor/cliente le permite descargar e instalar paquetes con una simple orden y cubrir las dependencias necesarias.

Pacman está escrito en lenguaje de programación C y usa el formato *.pkg.tar.xz* para los paquetes.

**Sugerencia:** El paquete oficial [pacman](https://www.archlinux.org/packages/?name=pacman) también contiene otras herramientas útiles, tales como **makepkg**, **pactree**, **vercmp** y otros. Se puede obtener la lista completa con `pacman -Ql pacman | grep bin`

## Contents

*   [1 Uso](#Uso)
    *   [1.1 Instalación de paquetes](#Instalaci.C3.B3n_de_paquetes)
        *   [1.1.1 Instalación de paquetes específicos](#Instalaci.C3.B3n_de_paquetes_espec.C3.ADficos)
        *   [1.1.2 Instalación de grupos de paquetes](#Instalaci.C3.B3n_de_grupos_de_paquetes)
    *   [1.2 Desintalar paquetes](#Desintalar_paquetes)
    *   [1.3 Actualización de paquetes](#Actualizaci.C3.B3n_de_paquetes)
    *   [1.4 Consulta de bases de datos de paquetes](#Consulta_de_bases_de_datos_de_paquetes)
        *   [1.4.1 Estructura de base de datos](#Estructura_de_base_de_datos)
    *   [1.5 Limpieza de la caché del paquete](#Limpieza_de_la_cach.C3.A9_del_paquete)
    *   [1.6 Órdenes adicionales](#.C3.93rdenes_adicionales)
    *   [1.7 Las actualizaciones parciales no son soportadas](#Las_actualizaciones_parciales_no_son_soportadas)
    *   [1.8 Nota general](#Nota_general)
*   [2 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [2.1 ¡Una actualización de un paquete XYZ me rompió el sistema!](#.C2.A1Una_actualizaci.C3.B3n_de_un_paquete_XYZ_me_rompi.C3.B3_el_sistema.21)
    *   [2.2 ¡Conozco un paquete de actualización para ABC que fue liberado, pero pacman dice que mi sistema está al día!](#.C2.A1Conozco_un_paquete_de_actualizaci.C3.B3n_para_ABC_que_fue_liberado.2C_pero_pacman_dice_que_mi_sistema_est.C3.A1_al_d.C3.ADa.21)
    *   [2.3 Me sale el siguiente error en la actualización: "file exists in filesystem"!](#Me_sale_el_siguiente_error_en_la_actualizaci.C3.B3n:_.22file_exists_in_filesystem.22.21)
    *   [2.4 Obtengo un error cuando instalo un paquete: "not found in sync db"](#Obtengo_un_error_cuando_instalo_un_paquete:_.22not_found_in_sync_db.22)
    *   [2.5 Obtengo un error cuando se instala un paquete: "target not found"](#Obtengo_un_error_cuando_se_instala_un_paquete:_.22target_not_found.22)
    *   [2.6 ¡Pacman me pregunta repetidamente por la actualización del mismo paquete!](#.C2.A1Pacman_me_pregunta_repetidamente_por_la_actualizaci.C3.B3n_del_mismo_paquete.21)
    *   [2.7 ¡Pacman se rompe durante una actualización!](#.C2.A1Pacman_se_rompe_durante_una_actualizaci.C3.B3n.21)
    *   [2.8 He instalado software usando "make install"; ¡estos archivos no pertenece a ningún paquete!](#He_instalado_software_usando_.22make_install.22.3B_.C2.A1estos_archivos_no_pertenece_a_ning.C3.BAn_paquete.21)
    *   [2.9 Necesito un paquete con un archivo específico. ¿Cómo puedo saber lo que ofrece?](#Necesito_un_paquete_con_un_archivo_espec.C3.ADfico._.C2.BFC.C3.B3mo_puedo_saber_lo_que_ofrece.3F)
    *   [2.10 ¡Pacman está completmente roto!. ¿Cómo puedo volver a reinstalarlo?](#.C2.A1Pacman_est.C3.A1_completmente_roto.21._.C2.BFC.C3.B3mo_puedo_volver_a_reinstalarlo.3F)
    *   [2.11 Después de actualizar mi sistema, me sale el siguiente error al reiniciar: "unable to find root device", y mi sistema ya no puede arrancar.](#Despu.C3.A9s_de_actualizar_mi_sistema.2C_me_sale_el_siguiente_error_al_reiniciar:_.22unable_to_find_root_device.22.2C_y_mi_sistema_ya_no_puede_arrancar.)
    *   [2.12 Signature from "User <email@gmail.com>" is unknown trust, installation failed](#Signature_from_.22User_.3Cemail.40gmail.com.3E.22_is_unknown_trust.2C_installation_failed)
    *   [2.13 Sigue saliendo el mensaje "PackageName: signature from "User <email@archlinux.org>" is invalid"](#Sigue_saliendo_el_mensaje_.22PackageName:_signature_from_.22User_.3Cemail.40archlinux.org.3E.22_is_invalid.22)
    *   [2.14 Sigo recibiendo un error de "failed to commit transaction (invalid or corrupted package)"](#Sigo_recibiendo_un_error_de_.22failed_to_commit_transaction_.28invalid_or_corrupted_package.29.22)
    *   [2.15 Me da un error cada vez que utilizo pacman diciendo 'warning: current locale is invalid; using default "C" locale'. ¿Qué debo hacer?](#Me_da_un_error_cada_vez_que_utilizo_pacman_diciendo_.27warning:_current_locale_is_invalid.3B_using_default_.22C.22_locale.27._.C2.BFQu.C3.A9_debo_hacer.3F)
    *   [2.16 ¿Cómo hacer que Pacman respete mi configuración del proxy?](#.C2.BFC.C3.B3mo_hacer_que_Pacman_respete_mi_configuraci.C3.B3n_del_proxy.3F)
    *   [2.17 ¿Cómo puedo volver a instalar todos los paquetes, manteniendo la información acerca de qué paquetes se han instalado de forma explícita y cúales como una dependencia?](#.C2.BFC.C3.B3mo_puedo_volver_a_instalar_todos_los_paquetes.2C_manteniendo_la_informaci.C3.B3n_acerca_de_qu.C3.A9_paquetes_se_han_instalado_de_forma_expl.C3.ADcita_y_c.C3.BAales_como_una_dependencia.3F)
*   [3 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Uso

Lo que sigue es sólo una pequeña muestra de las operaciones que *pacman* puede realizar. Para leer más ejemplos, consulte [pacman(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8).

**Tip:** Para aquellos que han utilizado otras distribuciones de Linux antes, hay un útil artículo de [Pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta")

### Instalación de paquetes

**Nota:** paquetes suelen tener una serie de [optional dependencies](/index.php/PKGBUILD#optdepends "PKGBUILD") que son paquetes que proporcionan funcionalidad adicional a la aplicación, aunque no estrictamente necesaria para su ejecución. Al instalar un paquete, *pacman* mostrará sus dependencias opcionales entre los mensajes de salida, pero no se encontrarán en `pacman.log`: use el comando [pacman -Si](#Querying_package_databases) para ver las dependencias opcionales de un paquete, junto con breves descripciones de su funcionalidad.

**Advertencia:** Al instalar paquetes en Arch, evite actualizar la lista de paquetes sin [actualizar el sistema](#Upgrading_packages) (por ejemplo, cuando [no se encuantra](#Packages_cannot_be_retrieved_on_installation) un paquete en los repositorios oficiales). En la práctica, **no** ejecute `pacman -Sy *package_name*` en lugar de `pacman -Sy**u** *package_name*`, ya que esto podría dar lugar a problemas de dependencia. Consulte [System maintenance#Partial upgrades are unsupported](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance") y [BBS#89328](https://bbs.archlinux.org/viewtopic.php?id=89328).

#### Instalación de paquetes específicos

Para instalar un solo paquete o una lista de paquetes (incluidas las dependencias), emita el siguiente comando:

```
 # pacman -S *package_name1* *package_name2* ...

```

Para instalar una lista de paquetes con regex (vea [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=7179)):

```
 # pacman -S $(pacman -Ssq *package_regex*)

```

A veces hay varias versiones de un paquete en diferentes repositorios, por ejemplo *extra* y *testing*. Para instalar la versión anterior, el repositorio debe definirse delante:

```
 # pacman -S extra/*package_name*

```

Para instalar un número de paquetes que comparten patrones similares en sus nombres - no todo el grupo ni todos los paquetes coincidentes; p.ej. [plasma](https://www.archlinux.org/groups/x86_64/plasma/):

```
 # pacman -S plasma-{desktop,mediacenter,nm}

```

Por supuesto, eso no es limitado y se puede ampliar a muchos niveles necesarios:

```
 # pacman -S plasma-{workspace{,-wallpapers},pa}

```

#### Instalación de grupos de paquetes

Algunos paquetes pertenecen a un grupo de paquetes [group of packages](/index.php/Creating_packages#Meta_packages_and_groups "Creating packages") que pueden instalarse simultáneamente. Por ejemplo, emitiendo el comando:

```
 # pacman -S gnome

```

le pedirá que seleccione los paquetes del grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/) que desea instalar. A veces un grupo de paquetes contendrá una gran cantidad de paquetes, y puede haber sólo unos pocos que usted hace o no desea instalar. En lugar de tener que introducir todos los números excepto los que no desea, a veces es más conveniente seleccionar o excluir paquetes o rangos de paquetes con la siguiente sintaxis:

```
 Introduzca una selección (predeterminado = todo): 1-10 15

```

que seleccionará los paquetes 1 a 10 y 15 para la instalación, o:

```
 Introduzca una selección (predeterminado = todo): ^ 5-8 ^ 2

```

que seleccionará todos los paquetes excepto 5 a 8 y 2 para la instalación. Para ver qué paquetes pertenecen al grupo gnome, ejecute:

```
 # pacman -Sg gnome

```

También visite [https://www.archlinux.org/groups/](https://www.archlinux.org/groups/) para ver qué grupos de paquetes están disponibles.

**Nota:** Si un paquete de la lista ya está instalado en el sistema, se reinstalará incluso si ya está actualizado. Este comportamiento se puede sobreescribir con la opción `--needed`.

### Desintalar paquetes

Para eliminar un solo paquete, dejando todas sus dependencias instaladas:

```
 # pacman -R *nombre_paquete*

```

Para eliminar un paquete y sus dependencias que no requieren ningún otro paquete instalado:

```
 # pacman -Rs *nombre_paquete*

```

Para eliminar un paquete, sus dependencias y todos los paquetes que dependen del paquete de destino:

**Advertencia:** Esta operación es recursiva y debe utilizarse con cuidado, ya que puede eliminar muchos paquetes potencialmente necesarios.

```
 # pacman -Rsc *nombre_paquete*

```

Para quitar un paquete, que es requerido por otro paquete, sin quitar el paquete dependiente:

```
 # pacman -Rdd *nombre_paquete*

```

pacman guarda los archivos de configuración importantes al eliminar ciertas aplicaciones y las nombra con la extensión: .pacsave . Para evitar la creación de estos archivos de copia de seguridad, utilice la opción -n :

```
 # pacman -Rn *nombre_paquete*

```

**Nota:** *pacman* no eliminará configuraciones creadas por la propia aplicación (por ejemplo, "dotfiles" en la carpeta de inicio).

### Actualización de paquetes

**Advertencia:**

*   Se espera que los usuarios sigan las instrucciones de la sección delManual de mantenimiento [System maintenance#Upgrading the system](/index.php/System_maintenance#Upgrading_the_system "System maintenance") para actualizar sus sistemas regularmente y no ejecutar ciegamente el siguiente comando.
*   Arch sólo admite actualizaciones completas del sistema. Consulte [System maintenance#Partial upgrades are unsupported](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance") y [#Installing packages](#Installing_packages) para obtener más detalles.

*pacman* puede actualizar todos los paquetes del sistema con un solo comando. Esto podría tomar bastante tiempo dependiendo de lo actualizado que esté el sistema. El siguiente comando sincroniza las bases de datos del repositorio “y” actualiza los paquetes del sistema, excluyendo paquetes "locales" que no están en los repositorios configurados:

```
 # pacman -Syu

```

### Consulta de bases de datos de paquetes

*pacman* consulta la base de datos de paquetes local con el indicador `-Q` , la base de datos de sincronización con el indicador `-S` y la base de datos de archivos con el indicador `-F` . Vea pacman `pacman -Q --help`, `pacman -S –help` y pacman `pacman -F --help` para las respectivas subopciones de cada flag. *pacman* puede buscar paquetes en la base de datos, buscando tanto en los nombres de los paquetes como en las descripciones:

```
 $ pacman -Ss *string1* *string2* ...

```

A veces, `-s` ERE (Expresiones regulares extendidas) incorporadas, puede causar muchos resultados no deseados, por lo que debe limitarse a coincidir con el nombre del paquete; no la descripción ni cualquier otro campo:

```
 $ pacman -Ss '^ vim-'

```

Para buscar paquetes ya instalados:

```
 $ pacman -Qs *string1* *string2* ...

```

Para buscar nombres de archivos de paquetes en paquetes remotos:

```
 $ pacman -Fs *string1* *string2* ...

```

Para mostrar información extensa sobre un paquete dado:

```
 $ pacman -Si *nombre_paquete*

```

Para paquetes instalados localmente:

```
 $ pacman -Qi *nombre_paquete*

```

Pasando dos indicadores `-i` también mostrará la lista de archivos de copia de seguridad y sus estados de modificación:

```
 $ pacman -Qii *nombre_paquete*

```

Para recuperar una lista de los archivos instalados por un paquete:

```
 $ pacman -Ql *nombre_paquete*

```

Para recuperar una lista de los archivos instalados por un paquete remoto:

```
 $ pacman -Fl *nombre_paquete*

```

Para verificar la presencia de los archivos instalados por un paquete:

```
 $ pacman -Qk *nombre_paquete*

```

Pasando la bandera `-k` dos veces se realizará una verificación más completa. Para consultar la base de datos para saber a qué paquete pertenece un archivo del sistema de archivos:

```
 $ pacman -Qo */path/to/file_name*

```

Para consultar la base de datos para saber a qué paquete remoto pertenece un archivo:

```
 $ pacman -Fo */path/to/file_name*

```

Para enumerar todos los paquetes que ya no se requieren como dependencias (huérfanos):

```
 $ pacman -Qdt

```

Para enumerar todos los paquetes explícitamente instalados y no necesarios como dependencias:

```
 $ pacman -Qet

```

Para enumerar un árbol de dependencias de un paquete:

```
 $ pactree “nombre_paquete”

```

Para enumerar todos los paquetes recursivamente dependiendo de un paquete *instalado* , use “whoneeds” de [pkgtools](https://aur.archlinux.org/packages/pkgtools/):

```
 $ whoneeds “nombre_paquete”

```

o la bandera de revés a pactree :

```
 $ pactree -r “nombre_paquete”

```

Vea [Pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") para más ejemplos.

#### Estructura de base de datos

Las bases de datos de pacman normalmente se encuentran en `/var/lib/pacman/sync`. Para cada repositorio especificado en `/etc/pacman.conf` habrá un archivo de base de datos correspondiente ubicado allí. Los archivos de base de datos son archivos tar-gzip que contienen un directorio para cada paquete, por ejemplo para el paquete `/etc/pacman.conf`:

```
% tree which-2.20-6 
which-2.20-6
|-- depends
`-- desc

```

El archivo `depends` lista los paquetes de los que este paquete depende, mientras `desc` tiene una descripción del paquete, como el tamaño del archivo y el hash MD5.

### Limpieza de la caché del paquete

*pacman* almacena sus paquetes descargados en `/var/cache/pacman/pkg/` y no elimina las versiones antiguas o desinstaladas automáticamente, por lo tanto es necesario limpiar deliberadamente esa carpeta periódicamente para evitar que dicha carpeta crezca indefinidamente en tamaño. La opción integrada para eliminar todos los paquetes en caché que no están instalados actualmente es:

```
 # pacman -Sc

```

**Advertencia:**

*   Unicamente haga esto cuando esté seguro de que no se requieren versiones anteriores de paquetes, por ejemplo, para una versión [downgrade](/index.php/Downgrade "Downgrade") posterior. `pacman -Sc` sólo deja disponibles las versiones de los paquetes que están actualmente disponibles, las versiones anteriores tendrían que ser recuperadas por otros medios, como el [Archive](/index.php/Archive "Archive").

*   Es posible vaciar completamente la carpeta de caché con `pacman -Scc` . Además de lo anterior, esto también evita la reinstalación de un paquete directamente “desde” la carpeta de caché en caso de necesidad, lo que requiere una nueva descarga. Debe evitarse a menos que haya una necesidad inmediata de espacio en disco.

Debido a las limitaciones anteriores, considere una alternativa para más control sobre qué paquetes y cuántos son eliminados de la memoria caché: La secuencia de comandos *paccache* , proporcionada por el propio paquete [pacman](https://www.archlinux.org/packages/?name=pacman) , elimina todas las versiones en caché de cada paquete, independientemente de si están instaladas o no, excepto por el 3 más reciente:

```
 # paccache -r

```

**Sugerencia:** Puede crear [pacman hooks](/index.php/Pacman_hooks "Pacman hooks") para ejecutarlo automáticamente después de cada transacción pacman. Vea [this thread](https://bbs.archlinux.org/viewtopic.php?pid=1694743#p1694743) para ver ejemplos.

También puede definir cuántas versiones recientes desea conservar:

```
 # paccache -rk 1

```

Para eliminar todas las versiones en caché de paquetes desinstalados, vuelva a ejecutar *paccache* con:

```
 # paccache -ruk0

```

Consulte `paccache -h` para obtener más opciones. [pkgcacheclean](https://aur.archlinux.org/packages/pkgcacheclean/) y [pacleaner](https://aur.archlinux.org/packages/pacleaner/) son dos alternativas más.

### Órdenes adicionales

Actualizar el sistema e instalar una lista de paquetes (una sola línea):

```
# pacman -Syu *nombre_paquete1* *nombre_paquete2* ...

```

Descargar un paquete sin instalarlo:

```
# pacman -Sw *nombre_paquete*

```

Instale un paquete 'local' que no proviene de un repositorio remoto (por ejemplo, el paquete viene de [AUR](/index.php/Arch_User_Repository "Arch User Repository")):

```
# pacman -U /ruta/al/paquete/nombre_paquete-versión.pkg.tar.xz

```

**Sugerencia:** Para mantener una copia del paquete local en la caché de pacman, use:
```
# pacman -U file://path/to/package/package_name-version.pkg.tar.xz

```

Instale un paquete 'remoto' (no de un repositorio indicado en los archivos de configuración de pacman):

```
# pacman -U http://www.ejemplo.com/repo/ejemplo.pkg.tar.xz

```

Para limpiar la caché de los paquetes descargados que no han sido instalados (`/var/cache/pacman/pkg`):

**Advertencia:** Haga esto solo si está seguro de que los paquetes instalados son estables y que una eventual [downgrade](/index.php/Downgrading_packages "Downgrading packages") no será necesaria, ya que se eliminarán todas las versiones anteriores de la carpeta de la caché, dejando solo las versiones de los paquetes que están instalados actualmente. Tener la versión antigua en el sistema es muy útil para el caso de que una futura actualización cause roturas.

```
# pacman -Sc

```

Limpie completamente la caché de todos los paquetes:

**Advertencia:** Esta operación borra la memoria caché por completo de todos los paquetes. Esta método se considera una mala práctica, porque si alguna vez necesita ejecutar el downgrade, no será capaz de hacerlo desde la carpeta de la caché. Probablemente tendrá que usar el [Arch Rollback Machine](/index.php/Downgrading_packages#ARM "Downgrading packages").

```
# pacman -Scc

```

**Sugerencia:** Como una alternativa tanto a la modalidad `-Sc` como a `-Scc`, considere la posibilidad de usar `paccache` con [pacman](https://www.archlinux.org/packages/?name=pacman). Este script ofrece un mayor control sobre qué y cuántos paquetes serán eliminados. Ejecute `paccache -h` para obtener instrucciones.

### Las actualizaciones parciales no son soportadas

Arch Linux es rolling release, y las nuevas versiones de [bibliotecas](https://en.wikipedia.org/wiki/Library_(computing) serán añadidas a los repositorios. Los Desarrolladores y los Trusted Users recompilarán consecuentemente todos los paquetes de los repositorios. Si el sistema se ha instalado con paquetes locales (como paquetes de [AUR](/index.php/Arch_User_Repository "Arch User Repository")), los usuarios necesitarán recompilar sus dependencias cuando modifiquen a nivel [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname").

Esto significa que las actualizaciones parciales **no están soportadas**. No utilice `pacman -Sy paquete` o cualquier equivalente como `pacman -Sy` y luego `pacman -S paquete`. Actualice siempre el sistema antes de instalar un paquete, especialmente si previamente se ha ejecutado una sincronización con los repositorios. Tenga mucho cuidado al usar `IgnorePkg` y `IgnoreGroup` por la misma razón.

Si se ha ejecutado una actualización y los binarios están rotos porque no pueden encontrar las bibliotecas correctas, **no pruebe a "arreglar" el problema simplemente creando enlaces simbólicos**. Las bibliotecas recibidas modifican [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") cuando **no son compatibles con versiones anteriores**. Un simple `pacman -Syu` a un mirror correctamente sincronizado solucionará el problema, siempre y cuando pacman no esté roto.

### Nota general

**Advertencia:** Tenga cuidado al utilizar el parámetro `--force` ya que puede causar serios problemas si se usa incorrectamente. Es muy recomendable que *únicamente* se utilice esta opción cuando Arch news indica expresamente que lo haga.

## Solución de problemas

### ¡Una actualización de un paquete XYZ me rompió el sistema!

Arch Linux es una distribución rolling-release vanguardista. Las actualizaciones de los paquete están disponibles tan pronto como se les considera lo suficientemente estable para su uso general. Sin embargo, las actualizaciones a veces requieren la intervención del usuario: algunos archivos de configuración puede que requieran ser actualizados, las dependencias opcionales pueden cambiar, etc.

El consejo más importante a recordar es que no actualice "a ciegas" el sistema. Lea siempre la lista de paquetes que vayan a ser actualizados. Preste atención si hay paquetes "sensibles" que van a ser actualizados ([linux](https://www.archlinux.org/packages/?name=linux), [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), y así sucesivamente). Si es así, por lo general, es una buena idea comprobar si hay alguna novedad en [https://www.archlinux.org/](https://www.archlinux.org/) y buscar mensajes en el foro para ver si los usuarios están experimentando problemas como resultado de una actualización.

Si una actualización de paquetes se espera que (o se conoce por) causar problemas, los responsables del paquete se asegurarán de que pacman muestre un mensaje apropiado cuando el paquete se haya actualizado. Si experimenta problemas después de una actualización, compruebe la salida de pacman mirando el archivo del registro (`/var/log/pacman.log`).

En este punto, **una vez se ha asegurado de que no existe información disponible a través de pacman, que no hay ninguna noticia relativa al tema en [https://www.archlinux.org/](https://www.archlinux.org/), y que no hay publicaciones en el foro acerca de la actualización**, se puede considerar la posibilidad de o bien solicitar ayuda en el foro, a través del canal [IRC](/index.php/IRC_channel "IRC channel"), o bien optar por [degradar el paquete problemático](/index.php/Downgrading_packages "Downgrading packages").

### ¡Conozco un paquete de actualización para ABC que fue liberado, pero pacman dice que mi sistema está al día!

Los mirrors de pacman no se sincronizan inmediatamente. Pueden tardar más de 24 horas antes de que una actualización esté disponible. Las únicas opciones son esperar o usar otro mirror. [MirrorStatus](https://www.archlinux.org/mirrors/status/) puede ayudar a identificar un mirror actualizado.

### Me sale el siguiente error en la actualización: "file exists in filesystem"!

ASIDE: *Tomado de [https://bbs.archlinux.org/viewtopic.php?id=56373](https://bbs.archlinux.org/viewtopic.php?id=56373) por Misfit138.*

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
package: /path/to/file exists in filesystem
Errors occurred, no packages were upgraded.

```

Por qué está sucediendo esto: pacman ha detectado un conflicto de archivos, y por diseño, no sobrescribirá los archivos. Esta es una característica de diseño, no un defecto.

La cuestión es generalmente trivial de resolver. Una forma segura es comprobar primero si el archivo pertenece a otro paquete (`pacman -Qo /ruta/al/archivo`). Si el archivo es propiedad de otro paquete, [reporte un informe de error](/index.php/Reporting_bug_guidelines "Reporting bug guidelines"). Si el archivo no es propiedad de otro paquete, cambie el nombre del archivo al que se refiere 'exists in filesystem' y vuelva a emitir la orden de actualización. Si todo va bien, el archivo puede ser eliminado.

Si ha instalado un programa manualmente sin usar pacman o usando una interfaz gráfica, hay que quitarlo y todos sus archivos y volver a instalarlo correctamente usando pacman.

Cada paquete instalado proporciona un archivo `/var/lib/pacman/local/$package-$version/files` que contiene metadatos acerca de este paquete. Si este archivo se corrompe -está vacío o falta- el resultado es un error por "file exists in filesystem" (el archivo existe en el sistema de archivos) al intentar actualizar el paquete. Este error normalmente se refiere a un solo paquete y, en vez de cambiar el nombre manualmente y más tarde la eliminación de todos los archivos que pertenecen al paquete en cuestión, puede ejecutar `pacman -S --force $paquete` para forzar a pacman a sobrescribir estos archivos.

**No** ejecute `pacman -Syu --force`.

### Obtengo un error cuando instalo un paquete: "not found in sync db"

En primer lugar, asegúrese de que el paquete existe realmente (¡y cuidado con los errores ortográficos!). Si el paquete existe, puede ser que la lista de paquetes esté desactualizada o los repositorios pueden estar configurados incorrectamente. Pruebe ejecutando `pacman -Syy` para forzar la actualización de todas las listas de paquetes.

### Obtengo un error cuando se instala un paquete: "target not found"

En primer lugar, asegúrese de que el paquete existe realmente (¡y cuidado con los errores de ortografía!). Si el paquete realmente existe, la lista de paquetes puede estar desacctualizada o los repositorios estar configurados de forma incorrecta. Pruebe ejecutando `pacman -Syy` para forzar una actualización de todas las listas de paquetes.
ambién podría ser que el repositorio que contiene el paquete no está habilitada en el sistema, por ejemplo, el paquete podría estar en el repositorio *multilib*, pero *multilib* no esté activado en el archivo *pacman.conf*.

### ¡Pacman me pregunta repetidamente por la actualización del mismo paquete!

Esto se debe a las entradas duplicadas en `/var/lib/pacman/local/`, por ejemplo dos versiones de `linux`. `pacman -Qi` emite la versión correcta, pero `pacman -Qu` reconoce la versión anterior, por lo que intentará actualizar.

Solución: elimine la entrada en conflicto en `/var/lib/pacman/local/`.

**Note:** La versión 3.4 de pacman debería mostrar un error en caso de entradas duplicadas, lo que debería hacer esta nota obsoleta.

### ¡Pacman se rompe durante una actualización!

En el caso de que pacman falle al "escribir la base de datos" mientras eliminaba paquetes, y volviendo a instalar o actualizar los paquetes, falla:

1.  Arranque el sistema utilizando el soporte de instalación de Arch.
2.  Monte el sistema de ficheros raíz (root).
3.  Actualice la base de datos a través de pacman `pacman -Syy`.
4.  Vuelva a instalar el paquete roto a través de `pacman -r /ruta/a/root -S paquete`.

### He instalado software usando "make install"; ¡estos archivos no pertenece a ningún paquete!

Si recibe el mensaje de error "conflicting files" , tenga en cuenta que pacman sobreescribe el software que se instaló de forma manual si se ejecuta combinado con la opción `--force` (por ejemplo (`pacman -S --force`). Véase [Pacman tips#Identify files not owned by any package](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips") para un script que busca en el sistema de archivos archivos *huérfanos*.

**Advertencia:** Tenga cuidado al usar la opción `--force` ya que puede causar graves problemas si se usa incorrectamente.

### Necesito un paquete con un archivo específico. ¿Cómo puedo saber lo que ofrece?

Instale [pkgfile](/index.php/Pkgfile "Pkgfile") que utiliza una base de datos independiente con todos los archivos y sus paquetes asociados.

### ¡Pacman está completmente roto!. ¿Cómo puedo volver a reinstalarlo?

En el caso de que pacman se rompa sin remedio, descargue manualmente los paquetes necesarios ([openssl](https://www.archlinux.org/packages/?name=openssl), [libarchive](https://www.archlinux.org/packages/?name=libarchive) y [pacman](https://www.archlinux.org/packages/?name=pacman)) y extráigalos a la raiz (root). Los binarios de pacman se restaurarán junto con su archivo de configuración por defecto. A continuación, vuelva a instalar estos paquetes con pacman para mantener la integridad de la base de datos de los paquetes. Información adicional y un script de ejemplo (desactualizado) que automatiza el proceso están disponibles en [este](https://bbs.archlinux.org/viewtopic.php?id=95007) post del foro.

### Después de actualizar mi sistema, me sale el siguiente error al reiniciar: "unable to find root device", y mi sistema ya no puede arrancar.

Muy probablemente su initramfs se rompió durante una actualización del kernel (el uso indebido de la opción `--force` de pacman puede ser una causa). Usted tiene dos opciones:

**1.** Pruebe la entrada *Fallback*.

**Sugerencia:** En el caso de que haya eliminado esta entrada por el motivo que sea, siempre puede pulsar la tecla `Tab` cuando el menú del gestor de arranque aparece (para Syslinux) o `e` (para GRUB), cambiarle el nombre `initramfs-linux-fallback.img` y presionar `Intro` o `b` (en función de su gestor de arranque) para arrancar con los nuevos parámetros.

	Una vez que se inicia el sistema, ejecute esta orden (para el [kernel linux](https://www.archlinux.org/packages/?name=kernel+linux) de serie) ya sea desde la consola o desde un terminal para reconstruir la imagen initramfs:

	 `# mkinitcpio -p linux` 

**2.** Si eso no funciona, a partir de la versión 2012 de Arch (CD/DVD o memoria USB), ejecute:

**Nota:** Si no se tiene una versión 2012 o si solo tiene alguna otra distribución "live" de Linux disponible, puede efectuar [chroot](/index.php/Chroot "Chroot") haciéndolo a la antigua usanza. Obviamente, solo consistirá en escribir el script que ejecuta `arch-chroot`.

```
# mount /dev/sdxY /mnt         #La partición raíz.
# mount /dev/sdxZ /mnt/boot    #Si utiliza una partición /boot.
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd linux
```

	Reinstalando el kernel (el paquete [linux](https://www.archlinux.org/packages/?name=linux)) automáticamente se volverá a generar la imagen initramfs con `mkinitcpio -p linux`. No hay necesidad de hacer esto por separado.

	A continuación, se recomienda que ejecute `exit`, `umount /mnt/{boot,}` y `reboot`

**Nota:** Si no puede entrar en el entorno chroot o archi-chroot, pero necesita volver a instalar paquetes puede utilizar la orden pacman -r /mnt -Syu foo para usar pacman en la partición raíz.

### Signature from "User <email@gmail.com>" is unknown trust, installation failed

Siga [pacman-key#Resetting all the keys](/index.php/Pacman-key#Resetting_all_the_keys "Pacman-key"). O bien, puede primero intentar actualizar manualmente el paquete `archlinux-keyring`, es decir, haciendo `pacman-S archlinux-keyring`.

### Sigue saliendo el mensaje "PackageName: signature from "User <email@archlinux.org>" is invalid"

```
error: PackageName: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded. 

```
Esto ocurre cuando el reloj del sistema está mal. Ajuste el [horario](/index.php/Time_(Espa%C3%B1ol) "Time (Español)") y ejecute: `# hwclock -w` antes de tratar de instalar/actualizar un paquete nuevo.

### Sigo recibiendo un error de "failed to commit transaction (invalid or corrupted package)"

Busque los archivos `*.part` (paquetes descargados parcialmente) en `/var/cache/pacman/pkg` y elimínelos (a menudo causado por un uso personalizado de `XferCommand` en `pacman.conf`).

### Me da un error cada vez que utilizo pacman diciendo 'warning: current locale is invalid; using default "C" locale'. ¿Qué debo hacer?

Como dice el mensaje de error, el entorno local no está configurado correctamente. Véase [Locale (Español)](/index.php/Locale_(Espa%C3%B1ol) "Locale (Español)").

### ¿Cómo hacer que Pacman respete mi configuración del proxy?

Asegúrese de que las variables de entorno relevantes (`$http_proxy`, `$ftp_proxy` etc.) están establecidas. Si utiliza Pacman con [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)"), necesita configurar sudo para [pasar estas variables de entorno a Pacman](/index.php/Sudo_(Espa%C3%B1ol)#Variables_de_entornos_.28.C2.BFDesactualizado.3F.29.29 "Sudo (Español)").

### ¿Cómo puedo volver a instalar todos los paquetes, manteniendo la información acerca de qué paquetes se han instalado de forma explícita y cúales como una dependencia?

Para volver a instalar todos los paquetes nativos: `pacman -S $(pacman -Qnq)` (la opción `-S` mantiene el origen de la instalación por defecto).
A continuación, tendrá que volver a instalar todos los paquetes foráneos manualmente, que se pueden enumerar con `pacman -Qmq`

## Véase también

*   [libalpm(3) Manual Page](https://www.archlinux.org/pacman/libalpm.3.html)
*   [pacman(8) Manual Page](https://www.archlinux.org/pacman/pacman.8.html)
*   [pacman.conf(5) Manual Page](https://www.archlinux.org/pacman/pacman.conf.5.html)
*   [repo-add(8) Manual Page](https://www.archlinux.org/pacman/repo-add.8.html)