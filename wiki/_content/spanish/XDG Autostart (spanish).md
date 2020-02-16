**Estado de la traducción**
Este artículo es una traducción de [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart"), revisada por última vez el **2020-02-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=XDG_Autostart&diff=0&oldid=545496) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

La [especificación XDG Autostart](https://specifications.freedesktop.org/autostart-spec/autostart-spec-latest.html) define un método para [iniciar automáticamente](/index.php/Autostarting_(Espa%C3%B1ol) "Autostarting (Español)") [entradas de escritorio](/index.php/Desktop_entries "Desktop entries") ordinarias durante el inicio y montaje de medios extraíbles en un [entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)"), colocándolos en [directorios](#Directorios) específicos.

## Requisitos previos

Debe utilizar un [entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") que lo admita o una implementación dedicada, como [dex](https://www.archlinux.org/packages/?name=dex), [dapper](https://aur.archlinux.org/packages/dapper/) o [fbautostart](https://aur.archlinux.org/packages/fbautostart/).

## Directorios

Los directorios de inicio automático en orden de preferencia son:

*   Específicos del usuario: `$XDG_CONFIG_HOME/autostart` (`~/.config/autostart` de manera predeterminada)
*   Para todo el sistema: `$XDG_CONFIG_DIRS/autostart` (`/etc/xdg/autostart` de manera predeterminada)[[1]](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html#referencing)

Las [entradas de escritorio](/index.php/Desktop_entries "Desktop entries") para todo el sistema pueden ser anuladas por las entradas específicas del usuario con el mismo nombre de archivo.

Para deshabilitar una entrada para todo el sistema, cree una entrada de reemplazo que contenga `Hidden=true`.

Para más detalles, consulte [la especificación](https://specifications.freedesktop.org/autostart-spec/autostart-spec-latest.html).