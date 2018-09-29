**Estado de la traducción:** este artículo es una versión traducida de [Mlocate](/index.php/Mlocate "Mlocate"). Fecha de la última traducción/revisión: **2018-09-26**. Puede ayudar a actualizar la traducción, si advierte que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Mlocate&diff=0&oldid=544335).

Artículos relacionados

*   [find](/index.php/Find_(Espa%C3%B1ol) "Find (Español)")
*   [Core utilities (Español)](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)")
*   [List of applications/Utilities#File searching](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities")

[mlocate](https://pagure.io/mlocate) (Merging Locate) es una versión más segura de la utilidad [locate](https://en.wikipedia.org/wiki/es:locate "wikipedia:es:locate"), que solo muestra los archivos accesibles para el usuario.

`locate` es una herramienta común de Unix para buscar rápidamente archivos por nombre. Ofrece mejoras de velocidad sobre la herramienta [find](/index.php/Find_(Espa%C3%B1ol) "Find (Español)") al buscar en un archivo de base de datos preconstruido, en lugar del [sistema de archivos](/index.php/File_systems_(Espa%C3%B1ol) "File systems (Español)") directamente. La desventaja de este enfoque es que los cambios realizados desde la construcción del archivo de la base de datos no pueden ser detectados por `locate`. Este problema se puede minimizar mediante actualizaciones programadas de la base de datos.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [mlocate](https://www.archlinux.org/packages/?name=mlocate).

Mientras que [GNU findutils](https://www.gnu.org/software/findutils/) incluye también una implementación de *locate*, el paquete de Arch [findutils](https://www.archlinux.org/packages/?name=findutils) no lo hace.

## Utilización

Antes de que se pueda utilizar [locate(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locate.1), deberá crearse la base de datos, esto se hace con el comando [updatedb(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.8), que (como su nombre indica) actualiza la base de datos.

El paquete contiene una unidad `updatedb.timer`, que invoca una actualización de la base de datos cada día. El temporizador se habilita justo después de la instalación, [inícielo](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") manualmente si desea utilizarlo antes de reiniciar. También puede ejecutar manualmente *updatedb* como superusuario (root) en cualquier momento.

Para ahorrar tiempo, *updatedb* puede (y está así por defecto) configurarse para ignorar ciertos sistemas de archivos y rutas editando `/etc/updatedb.conf`. [updatedb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.conf.5) describe la semántica de este archivo. Vale la pena señalar que entre las rutas ignoradas en la configuración predeterminada (`PRUNEPATHS`) están `/media` y `/mnt`, por lo que *locate* puede no descubrir archivos en dispositivos externos.

## Véase tambien

*   [Cómo funciona *locate* y reescribirlo en un minuto](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/)