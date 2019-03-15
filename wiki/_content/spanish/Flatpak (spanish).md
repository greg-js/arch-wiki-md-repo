**Estado de la traducción**
Este artículo es una traducción de [Flatpak](/index.php/Flatpak "Flatpak"), revisada por última vez el **2019-03-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Flatpak&diff=0&oldid=568742) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Snap (Español)](/index.php/Snap_(Espa%C3%B1ol) "Snap (Español)")
*   [bubblewrap](/index.php/Bubblewrap "Bubblewrap")

Del proyecto [README](https://github.com/flatpak/flatpak/blob/master/README.md): "*[Flatpak](http://flatpak.org) es un sistema de compilación, distribución y ejecución de aplicaciones de escritorio aisladas en Linux.*"

De [flatpak(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/flatpak.1):

	*Flatpak es una herramienta para la gestión de aplicaciones y los tiempos de ejecución ('runtimes') que utilizan. En el modelo Flatpak, las aplicaciones pueden ser compiladas y distribuidas de manera independiente del sistema host en que se utilizan, y están aisladas del sistema host ('aislamiento de proceso') en cierto punto, en tiempo de ejecución.*

	*Flatpak utiliza [OSTree](https://ostree.readthedocs.io/en/latest/) para distribuir y implementar datos. Los repositorios que utiliza son los repositorios OSTree y pueden ser manipulados con la utilidad de ostree. Los tiempos de ejecución y aplicaciones instaladas son comprobaciones de OSTree.*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Administrando repositorios](#Administrando_repositorios)
    *   [2.1 Añadir un repositorio](#Añadir_un_repositorio)
    *   [2.2 Eliminar un repositorio](#Eliminar_un_repositorio)
*   [3 Administrando tiempos de ejecución y aplicaciones](#Administrando_tiempos_de_ejecución_y_aplicaciones)
    *   [3.1 Búsqueda de un tiempo de ejecución o aplicación remota](#Búsqueda_de_un_tiempo_de_ejecución_o_aplicación_remota)
    *   [3.2 Listar todos los tiempos de ejecución y aplicaciones disponibles](#Listar_todos_los_tiempos_de_ejecución_y_aplicaciones_disponibles)
    *   [3.3 Instalar un tiempo de ejecución o aplicación](#Instalar_un_tiempo_de_ejecución_o_aplicación)
    *   [3.4 Listar los tiempos de ejecución y aplicaciones instaladas](#Listar_los_tiempos_de_ejecución_y_aplicaciones_instaladas)
    *   [3.5 Ejecutar aplicaciones](#Ejecutar_aplicaciones)
    *   [3.6 Actualizar un tiempo de ejecución o aplicación](#Actualizar_un_tiempo_de_ejecución_o_aplicación)
    *   [3.7 Desinstalar un tiempo de ejecución o aplicación](#Desinstalar_un_tiempo_de_ejecución_o_aplicación)
    *   [3.8 Añadiendo archivos .desktop de Flatpak a su menú](#Añadiendo_archivos_.desktop_de_Flatpak_a_su_menú)
*   [4 Creación de un tiempo de ejecución base personalizado](#Creación_de_un_tiempo_de_ejecución_base_personalizado)
    *   [4.1 Creación de aplicaciones con pacman](#Creación_de_aplicaciones_con_pacman)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [flatpak](https://www.archlinux.org/packages/?name=flatpak).

**Note:** Si desea compilar flatpaks con `flatpak-builder` necesitará instalar las dependencias opcionales de [elfutils](https://www.archlinux.org/packages/?name=elfutils) y [patch](https://www.archlinux.org/packages/?name=patch).

## Administrando repositorios

### Añadir un repositorio

Para añadir un repositorio remoto de flatpak haga:

```
$ flatpak remote-add *nombre* *ubicación*

```

Donde *nombre* es el nombre para el nuevo remoto y *ubicación* es la ruta o URL del repositorio.

Por ejemplo para añadir el [repositorio Flathub](https://flathub.org/) oficial:

```
$ flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

```

### Eliminar un repositorio

Para eliminar un repositorio remoto de flatpak haga:

```
$ flatpak remote-delete *nombre*

```

Donde *nombre* es el nombre del ropositorio remoto a eliminar.

## Administrando tiempos de ejecución y aplicaciones

### Búsqueda de un tiempo de ejecución o aplicación remota

Antes de poder buscar un tiempo de ejecución o aplicación en un repositorio recién agregado, necesitamos recuparar los datos del flujo de aplicaciones para ello:

 `$ flatpak update` 
```
Looking for updates...
Updating appstream data for remote *name*

```

Ahora podemos proceder a buscar un paquete con `flatpak search *nombre-del-paquete*`, *e.j.* para buscar el paquete `libreoffice` con el `flathub` remoto configurado:

 `$ flatpak search libreoffice` 
```
Application ID              Version Branch Remotes Description                       
org.libreoffice.LibreOffice         stable flathub The LibreOffice productivity suite

```

### Listar todos los tiempos de ejecución y aplicaciones disponibles

Para listar todas los tiempos de ejecución y aplicaciones en un repositorio remoto llamado *remoto* haga:

```
$ flatpak remote-ls *remoto*

```

### Instalar un tiempo de ejecución o aplicación

Para instalar un tiempo de ejecución o aplicación haga:

```
$ flatpak install *remoto* *nombre*

```

Donde *remoto* es el nombre del repositorio remoto, y *nombre* es el nombre de la aplicación o tiempo de ejecución a instalar.

**Sugerencia:** Puede usar indicadores parciales `flatpak install *nombre-parcial*` (por ejemplo `flatpak install libreoffice`).

### Listar los tiempos de ejecución y aplicaciones instaladas

Para listar tiempos de ejecución y aplicaciones instaladas haga:

```
$ flatpak list

```

### Ejecutar aplicaciones

Las aplicaciones flatpak también pueden ser ejecutadas desde la línea de comandos:

```
$ flatpak run *nombre*

```

### Actualizar un tiempo de ejecución o aplicación

Para actualizar un tiempo de ejecución o aplicación llamada *nombre* haga:

```
$ flatpak update *nombre*

```

### Desinstalar un tiempo de ejecución o aplicación

Para desinstalar un tiempo de ejecución o aplicación llamada *nombre* haga:

```
$ flatpak uninstall *nombre*

```

**Sugerencia:** Puede desinstalar "referencias" flatpak no utilizadas (también conocidos como huérfanos sin aplicación/tiempo de ejecución) con `flatpak uninstall --unused`.

### Añadiendo archivos .desktop de Flatpak a su menú

Flatpak espera que los manejadores de ventana respeten la variable de entorno XDG_DATA_DIRS para descubrir aplicaciones. Esto puede requerir reiniciar la sesión o el lanzador podría no admitirlo. En caso de que puede editar la lista de directorios escaneados, agréguelos a esta:

```
~/.local/share/flatpak/exports/share/applications
/var/lib/flatpak/exports/share/applications

```

Es sabido que ésto es necesario en Awesome.

## Creación de un tiempo de ejecución base personalizado

**Advertencia:** Si quiere liberar su software al público como un Flatpak, un tiempo de ejecución basado en Arch no es adecuado. En éste caso, deseará seguir la [documentación oficial](http://docs.flatpak.org) para integrar su software en el ecosistema apropiado Flatpak usando las [tiempos de ejecución comunes](http://flatpak.org/runtimes.html).

**Nota:** Posiblemente desee utilizar una cuenta de usuario no confiable y sin privilegios para empaquetar software que no sea de confianza porque no es aislado durante la creación de la app y el tiempo de ejecución.

**Nota:** Al distribuir paquetes a otros, puede ser obligado legalmente a proporcionar el código fuente de parte del software empaquetado que sea solicitado. Posiblemente desee utilizar [ABS](/index.php/ABS "ABS") para compilar paquetes desde la fuente.

Puede crear un tiempo de ejecución personalizado basada en Arch y SDK base para Flatpak usando pacman. Así puede utilizarlo para compilar y empaquetar aplicaciones. Esto es una alternativa para uso personal para los tiempos de ejecución por defecto `org.freedesktop.BasePlatform` y `org.freedesktop.BaseSdk`.

Además de [flatpak](https://www.archlinux.org/packages/?name=flatpak), necesita tener instalado [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) y para el soporte de los enganches de pacman también [fakechroot](https://www.archlinux.org/packages/?name=fakechroot).

Primero, empiece creando un directorio para compilar el tiempo de ejecución y las posibles aplicaciones.

```
$ mkdir *myflatpakbuilddir*
$ cd *myflatpakbuilddir*

```

Enseguida puede preparar un directorio para compilar la plataforma base del tiempo de ejecución. Los subdirectorios del archivo contendrán lo que después será el directorio `/usr` en el aislamiento de proceso. Por lo tanto tendrá que crear enlaces simbólicos para que las rutas predeterminadas `/usr/share` etc. puedans ser accesadas desde Arch en la ruta habitual.

```
$ mkdir -p *myruntime*/files/var/lib/pacman
$ touch *myruntime*/files/.ref
$ ln -s /usr/usr/share *myruntime*/files/share
$ ln -s /usr/usr/include *myruntime*/files/include
$ ln -s /usr/usr/local *myruntime*/files/local

```

Haga que las fuentes de su OS estén disponibles para el tiempo de ejecución de Arch:

```
$ mkdir -p *myruntime*/files/usr/share/fonts
$ ln -s /run/host/fonts *myruntime*/files/usr/share/fonts/flatpakhostfonts

```

Necesita y posiblemente desee adaptar su `pacman.conf` antes de instalar los paquetes en el tiempo de ejecución. Copie `/etc/pacman.conf` en su directorio de compilación y después haga los cambios siguientes:

*   Elimine la opción `CheckSpace` de tal modo que pacman no se quejará de los errores al encontrar sistema de archivo raíz para verificar espacio de disco.
*   Elimine cualquier repositorio personalizado no deseado y las configuraciones `IgnorePkg`, `IgnoreGroup`, `NoUpgrade` y `NoExtract` que son necesarias solo en el sistema host.

Ahora instale los paquetes para el tiempo de ejecución:

```
$ fakechroot fakeroot pacman -Syu --root *myruntime*/files --dbpath *myruntime*/files/var/lib/pacman --config pacman.conf base
$ mv pacman.conf *myruntime*/files/etc/pacman.conf

```

Configure los [locales](/index.php/Locale_(Espa%C3%B1ol) "Locale (Español)") para usarlas editando `*myruntime*/files/etc/locale.gen`. Luego regenere los locales de los tiempos de ejecución.

```
$ fakechroot chroot *myruntime*/files locale-gen

```

El SDK base se puede crear desde el tiempo de ejecución base con aplicaciones adicionales necesarias para crear paquetes y ejecución de pacman.

```
$ cp -r *myruntime* mysdk
$ fakechroot fakeroot pacman -S --root mysdk/files --dbpath mysdk/files/var/lib/pacman --config mysdk/files/etc/pacman.conf base-devel fakeroot fakechroot --needed

```

Inserte metadatos acerca del tiempo de ejecución y SDK.

 `*myruntime*/metadata` 
```
[Runtime]
name=org.mydomain.BasePlatform
runtime=org.mydomain.BasePlatform/x86_64/2016-06-26
sdk=org.mydomain.BaseSdk/x86_64/2016-06-26
```
 `mysdk/metadata` 
```
[Runtime]
name=org.mydomain.BaseSdk
runtime=org.mydomain.BasePlatform/x86_64/2016-06-26
sdk=org.mydomain.BaseSdk/x86_64/2016-06-26
```

Agregue el tiempo de ejecución base y el SDK al repositorio local en el directorio actual. Probablemete desee darles los mensajes de confirmación adecuados como “Mi tiempo de ejecución base de Arch” and “Mi SDK base de Arch”.

```
$ ostree init --mode archive-z2 --repo=.
$ EDITOR="nano -w" ostree commit -b runtime/org.mydomain.BasePlatform/x86_64/2016-06-26 --tree=dir=*myruntime*
$ EDITOR="nano -w" ostree commit -b runtime/org.mydomain.BaseSdk/x86_64/2016-06-26 --tree=dir=mysdk
$ ostree summary -u

```

Instale el tiempo de ejecución y SDK.

```
$ flatpak remote-add --user --no-gpg-verify myarchos file://$(pwd)
$ flatpak install --user myarchos org.mydomain.BasePlatform 2016-06-26
$ flatpak install --user myarchos org.mydomain.BaseSdk 2016-06-26

```

### Creación de aplicaciones con pacman

Como alternativa para crear aplicaciones [de la manera usual](http://flatpak.org/developer.html), podemo usar pacman para crear una versión en contenedor de los paquetes regulares de Arch. Tenga en cuenta que `/usr` es de solo lectura al crear apps, por lo que no podemos usar los paquetes de Arch mientras se compila una apliación. Para crear una aplicación real con pacman, podemos

*   usar pacman para crear tiempo de ejecución que contenga todas las dependencias
*   y compilar la aplicación nosotros mismos [de la manera usual](http://flatpak.org/developer.html) o quizás usando pacman con un [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") personalizado adaptado a Flatpak quien utiliza `--prefix=/app` para el script `configure`,

o podemos

*   usar pacman para crear un tiempo de ejecución que contenga la aplicación instalada con pacman
*   y crear una aplicación ficticia para lanzarla.

Para hacer lo último, primero cree un tiempo de ejecución usando pacman como ésta para [gedit](https://www.archlinux.org/packages/?name=gedit). El tiempo de ejecución primero es inicializado y preparado para usarse con pacman.

```
$ flatpak build-init -w geditruntime org.mydomain.geditruntime org.mydomain.BaseSdk org.mydomain.BasePlatform 2016-06-26
$ flatpak build geditruntime sed -i "s/^#Server/Server/g" /etc/pacman.d/mirrorlist
$ flatpak build geditruntime ln -s /usr/var/lib /var/lib
$ flatpak build geditruntime fakeroot pacman-key --init
$ flatpak build geditruntime fakeroot pacman-key --populate archlinux

```

Después de que el paquete es instalado. La conexión de red del host debe estar disponible para pacman.

```
$ flatpak build --share=network geditruntime fakechroot fakeroot pacman --root /usr -S gedit

```

Puede probar la instalación antes de finalizar el tiempo de ejecución (sin un aislamiento apropiado).

```
$ flatpak build --socket=x11 geditruntime gedit

```

Ahora finalize la creación del tiempo de ejecución y expórtelo al nuevo repositorio local. Las claves GnuPG de pacman tienen permisos que pueden interferir y necesitan ser eliminadas primero.

```
$ flatpak build geditruntime rm -r /etc/pacman.d/gnupg
$ flatpak build-finish geditruntime
$ sed -i "s/\[Application\]/\[Runtime\]/;s/runtime=org.mydomain.BasePlatform/runtime=org.mydomain.geditruntime/" geditruntime/metadata
$ flatpak build-export -r geditrepo geditruntime

```

Luego cree una aplicación ficticia.

```
$ flatpak build-init geditapp org.gnome.gedit org.mydomain.BaseSdk org.mydomain.geditruntime

```

Ahora termine la aplicación ficticia. Puede afinar los permisos de acceso de la aplicación cuando se aisle dando opciones adicionales al finalizar la compilación. Para posibles opciones véase [documentation de Flatpak](#Véase_también) y los [Archivos de manifiesto de GNOME](https://gitlab.gnome.org/GNOME/gnome-apps-nightly/tree/master).

```
$ flatpak build-finish geditapp --socket=x11 *[possibly other options]* --command=gedit
$ flatpak build-export geditrepo geditapp

```

Instálela junto con el tiempo de ejecución.

```
$ flatpak --user remote-add --no-gpg-verify geditrepo geditrepo
$ flatpak install --user geditrepo org.mydomain.geditruntime
$ flatpak install --user geditrepo org.gnome.gedit
$ flatpak run org.gnome.gedit

```

## Véase también

*   [Sitio oficial](http://flatpak.org)
*   [Wiki oficial de Github](https://github.com/flatpak/flatpak/wiki)
*   [Página de Wikipedia](https://en.wikipedia.org/wiki/Flatpak "wikipedia:Flatpak")
*   [Aplicaciones Aisladas de Gnome](https://wiki.gnome.org/Projects/SandboxedApps)
*   [Tiempos de ejecución y Aplicaciones de Prueba de KDE](https://community.kde.org/Guidelines_and_HOWTOs/Flatpak)