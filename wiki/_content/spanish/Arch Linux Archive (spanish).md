**Estado de la traducción**
Este artículo es una traducción de [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive"), revisada por última vez el **2019-11-17**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Arch_Linux_Archive&diff=0&oldid=589222) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Downgrading packages (Español)](/index.php/Downgrading_packages_(Espa%C3%B1ol) "Downgrading packages (Español)")

**Arch Linux Archive** (también conocido como **ALA**), anteriormente conocido como **Arch Linux Rollback Machine** (también conocido como **ARM**), almacena *instantáneas de los repositorios oficiales*, *imágenes iso* y *tarballs de bootstrap* a lo largo del tiempo.

**Puede utilizarlo para:**

*   Degradar a una versión anterior de un paquete (la última versión está rota y desea la anterior)
*   Restaurar todos sus paquetes a un momento preciso (el sistema está roto, desea restaurarlo a hace 2 meses)
*   Encuentrar una versión anterior de una imagen ISO

Los paquetes solo se guardan durante unos años, posteriormente se trasladan a [Arch Linux Historical Archive](#Historical_Archive) en archive.org.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Ubicación](#Ubicación)
*   [2 Directorios](#Directorios)
    *   [2.1 /repos](#/repos)
    *   [2.2 /packages](#/packages)
    *   [2.3 /iso](#/iso)
*   [3 FAQ](#FAQ)
    *   [3.1 Cómo degradar un paquete](#Cómo_degradar_un_paquete)
    *   [3.2 Cómo restaurar todos los paquetes a una fecha específica](#Cómo_restaurar_todos_los_paquetes_a_una_fecha_específica)
*   [4 Histórico de Archive](#Histórico_de_Archive)
    *   [4.1 Encontrar paquetes en el Histórico de Archive](#Encontrar_paquetes_en_el_Histórico_de_Archive)
    *   [4.2 Descargar paquetes del Histórico de Archive](#Descargar_paquetes_del_Histórico_de_Archive)
*   [5 Historia](#Historia)

## Ubicación

Arch Linux Archive está disponible en [https://archive.archlinux.org/](https://archive.archlinux.org/).

El [código fuente](https://github.com/seblu/archivetools) también está disponible para configurar su propio servidor de réplica.

## Directorios

**Archive** se divide en 3 directorios principales detallados a continuación.

```
├── iso
├── packages
└── repos

```

### /repos

El directorio [repos](https://archive.archlinux.org/repos) contiene instantáneas diarias del servidor de réplica oficial, organizadas por fecha, como en el siguiente ejemplo.

```
repos
├── 2013
│   ├── 08
│   │   └── 31
│   │       ├── community
│   │       ├── community-staging
│   │       ├── community-testing
│   │       ├── core
│   │       ├── extra
│   │       ├── gnome-unstable
│   │       ├── kde-unstable
│   │       ├── lastsync
│   │       ├── multilib
│   │       ├── multilib-staging
│   │       ├── multilib-testing
│   │       ├── pool
│   │       ├── staging
│   │       └── testing
│   ├── 09
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │   ├── 21
│   │   └── 22
│   ├── 10
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 11
│   └── 12
├── 2014
│   ├── 01
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 02
│   ├── 03
│   ├── ...
│   └── 09
│       ├── 01
│       ├── ...
│       └── 28
├── last
├── month
└── week

```

Nota: los últimos 3 directorios especiales (**last**, **week** y **month**) enlazan respectivamente al último repositorio sincronizado, al del último del lunes y al del primero del mes actual.

### /packages

El directorio [packages](https://archive.archlinux.org/packages) contiene todas las versiones de cada paquete con sus firmas. Un directorio por paquete y los directorios de paquete se agrupan por su primera letra.

```
├── packages
│   ├── a
│   │   ├── awesome
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz.sig
│   │   │   ├── ...
│   │   │ 
│   │   ├── ...
│   │   ├── awstats
│   │   └── axel
│   │   
│   ├── b
│   ├── ...
│   └── z

```

Puede usar el subdirectorio mágico [.all](https://archive.archlinux.org/packages/.all) para acceder a todos los paquetes por su nombre. Actúa como un directorio plano que contiene todas las versiones de cada paquete.

```
├── packages
│   ├── .all
│   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   ├── ...
│   │   ├── zsh-5.0.2-3-i686.pkg.tar.xz
│   │   ├── zsh-5.0.2-4-i686.pkg.tar.xz
│   │   └── ...

```

Puede descargar la lista completa de paquetes (hay más de cien mil paquetes) como un índice comprimido: [index.0.xz](https://archive.archlinux.org/packages/.all/index.0.xz).

 `$ curl https://archive.archlinux.org/packages/.all/index.0.xz | unxz` 
```
0ad-a14-1-i686
0ad-a14-1-x86_64
0ad-a14-2-i686
...
zziplib-0.13.62-1-x86_64
zziplib-0.13.62-2-i686
zziplib-0.13.62-2-x86_64
```

### /iso

El directorio [iso](https://archive.archlinux.org/iso) contiene imágenes ISO oficiales y tarballs bootstrap ordenados por fecha de lanzamiento.

```
├── 2014.09.03
├── 2014.10.01
├── 2014.11.01
├── 2014.12.01
├── 2015.07.01
├── 2015.08.01
├── 2015.09.01
└── 2017.04.01
    ├── arch
    ├── archlinux-2017.04.01-x86_64.iso
    ├── archlinux-2017.04.01-x86_64.iso.sig
    ├── archlinux-2017.04.01-x86_64.iso.torrent
    ├── archlinux-bootstrap-2017.04.01-x86_64.tar.gz
    ├── archlinux-bootstrap-2017.04.01-x86_64.tar.gz.sig
    ├── md5sums.txt
    └── sha1sums.txt

```

## FAQ

### Cómo degradar un paquete

Localice el paquete que desea en [/packages](#/packages) y deje que pacman lo busque para la instalación. Por ejemplo:

```
# pacman -U https://archive.archlinux.org/packages/ ... *packagename*.pkg.tar.xz

```

Si deja que pacman lo busque, descargará automáticamente el archivo *.sig* separado del paquete y lo verificará de acuerdo con la configuración de `/etc/pacman.conf`.

Alternativamente, descargue e instale el paquete manualmente usando `pacman -U`.

Consulte también [Downgrading packages (Español)#Automatización](/index.php/Downgrading_packages_(Espa%C3%B1ol)#Automatización "Downgrading packages (Español)") para obtener herramientas que simplifican el proceso.

### Cómo restaurar todos los paquetes a una fecha específica

Para restaurar todos los paquetes a la versión correspondiente a una fecha específica, digamos el 30 de marzo de 2014, debe dirigir [pacman](/index.php/Pacman "Pacman") a esta fecha, editando `/etc/pacman.conf` y utilizar la siguiente directiva de servidor:

```
[core]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

[extra]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

[community]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

```

o reemplazar `/etc/pacman.d/mirrorlist` con el siguiente contenido:

```
##                                                                              
## Arch Linux repository mirrorlist                                             
## Generated on 2042-01-01                                                      
##
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

```

Luego actualice la base de datos y fuerce la degradación:

```
# pacman -Syyuu

```

**Nota:** [no es seguro](/index.php/System_maintenance_(Espa%C3%B1ol)#Las_actualizaciones_parciales_no_son_compatibles "System maintenance (Español)") mezclar los servidores de Archive y los de réplicas actualizados. En caso de un error de descarga, recurrirá a un paquete ascendente y tendrá paquetes que no serán de la misma época respecto del resto del sistema

## Histórico de Archive

Mantener Arch Linux Archive consume una cantidad significativa de recursos, por lo que los paquetes antiguos se limpian de vez en cuando.

Antes de eliminarlos, los paquetes antiguos se cargan en una [colección dedicada de «Arch Linux Historical Archive» en archive.org](https://archive.org/details/archlinuxarchive).

El Histórico de Archive no proporciona una forma de acceder a una «instantánea» de los paquetes de Arch en un momento dado. Sin embargo, hay una redirección en `archive.archlinux.org` para que las descargas de paquetes antiguos se redirijan al Histórico de Archive en `archive.org`.No debería haber ningún sobresalto visible desde el lado del usuario, excepto por el hecho de que `archive.org` generalmente es bastante lento para la descarga.

### Encontrar paquetes en el Histórico de Archive

La colección **Arch Linux Historical Archive** tiene un índice de todos los paquetes: [https://archive.org/details/archlinuxarchive](https://archive.org/details/archlinuxarchive)

También es posible acceder directamente a un paquete mediante su **identificador**. El patrón general para los identificadores es:

```
archlinux_pkg_<sanitized package name>

```

Para obtener el nombre del paquete **saneado**, simplemente reemplace cualquier carácter `@`, `+` o `.` en el nombre del paquete con un guión bajo `_`.

Por ejemplo, el identificador para [lucene++](https://www.archlinux.org/packages/?name=lucene%2B%2B) es `archlinux_pkg_lucene__`.

Puede acceder a la página de detalles de un paquete a través de su identificador, por ejemplo: [https://archive.org/details/archlinux_pkg_lucene__](https://archive.org/details/archlinux_pkg_lucene__)

También es posible ejecutar búsquedas con el [cliente Python de archive.org](https://github.com/jjjake/internetarchive):

```
$ ia search subject:"archlinux package" subject:'mysql'                                                                                       
{"identifier": "archlinux_pkg_ejabberd-mod_mysql"}                                                                                                           
{"identifier": "archlinux_pkg_ejabberd-mod_mysql-svn"}
{"identifier": "archlinux_pkg_gambas3-gb-db-mysql"}
{"identifier": "archlinux_pkg_gambas3-gb-mysql"}
{"identifier": "archlinux_pkg_libgda-mysql"}

```

### Descargar paquetes del Histórico de Archive

Se puede acceder a todas las versiones de paquete disponibles (y su firma) a través de la página de descarga de un paquete: [https://archive.org/download/archlinux_pkg_lucene__](https://archive.org/download/archlinux_pkg_lucene__)

Para descargar, verificar e instalar un paquete usando [pacman](/index.php/Pacman "Pacman"):

```
# pacman -U https://archive.org/download/archlinux_pkg_cjdns/cjdns-16.1-3-x86_64.pkg.tar.xz

```

La verificación del paquete está controlada por la opción `RemoteFileSigLevel` de pacman. Tenga en cuenta que si usa pacman, deberá averiguar las dependencias usted mismo.

También es posible utilizar el [cliente Python de archive.org](https://github.com/jjjake/internetarchive):

```
# Descargar una versión específica de un paquete
$ ia download archlinux_pkg_cjdns cjdns-16.1-3-x86_64.pkg.tar.xz{,.sig}

# Descargar todas las versiones x86_64 de un paquete, con firmas
$ ia download archlinux_pkg_cjdns --glob="*x86_64.pkg.tar.xz*"

```

## Historia

*   El ARM original (*Archlinux Rollback Machine*) se cerró en 2013-08-18.[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1313360#p1313360)
*   El nuevo está alojado en [seblu.net](http://seblu.net) desde 2013-08-31.
*   Nueva URL y cierre de la antigua jerarquía ARM en 2015-10-13\. Se introdujo un nuevo software, [agetpkg-git](https://aur.archlinux.org/packages/agetpkg-git/).
*   Se trasladó a [archive.archlinux.org](https://archive.archlinux.org) en 2015-12-19.[[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2015-December/027635.html)
*   Paquetes antiguos de 2013-2016 cargados en [archive.org](https://archive.org/details/archlinuxarchive) el 2018-06-05.