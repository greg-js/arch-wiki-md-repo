**Estado de la traducción**
Este artículo es una traducción de [GNOME/Gedit](/index.php/GNOME/Gedit "GNOME/Gedit"), revisada por última vez el **2018-12-25**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GNOME/Gedit&diff=0&oldid=560355) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[gedit](https://en.wikipedia.org/wiki/es:gedit "w:es:gedit") es un editor de texto de propósito general para GNOME.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 No terminar archivos con una nueva línea](#No_terminar_archivos_con_una_nueva_línea)
    *   [2.2 Guardar versiones de copia de seguridad de los archivos editados](#Guardar_versiones_de_copia_de_seguridad_de_los_archivos_editados)
*   [3 Corrección ortográfica](#Corrección_ortográfica)
*   [4 Complementos](#Complementos)
    *   [4.1 Añadiendo y haciendo complementos personalizados.](#Añadiendo_y_haciendo_complementos_personalizados.)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gedit](https://www.archlinux.org/packages/?name=gedit).

## Configuración

### No terminar archivos con una nueva línea

Si quiere asegurarse de que gedit no finalice los archivos con una nueva línea, ejecute lo siguiente:

```
$ gsettings set org.gnome.gedit.preferences.editor ensure-trailing-newline false

```

### Guardar versiones de copia de seguridad de los archivos editados

Si lo desea, gedit puede crear una copia de seguridad de un archivo editado; el contenido del archivo de copia de seguridad será el mismo que el contenido del archivo original antes de que se realizara la edición antes de guardarlo. El nombre del archivo de copia de seguridad será el mismo que el nombre del archivo original pero con el símbolo ~. Por lo tanto, para el archivo llamado `archivo1`, la copia de seguridad tendrá el nombre `archivo1~`. Los archivos de copia de seguridad están ocultos por defecto.

Para activar este comportamiento, acceda al panel de Preferencias de gedit (para usuarios de GNOME Shell, esto se puede encontrar en el menú global de gedit). En el panel de preferencias, pulse en la pestaña *Editor* y marque la opción *Crear una copia de seguridad de los archivos antes de guardarlos*.

## Corrección ortográfica

Gedit puede utilizar múltiples diccionarios de correctores ortográficos, véase [corrección de idiomas](/index.php/Language_checking_(Espa%C3%B1ol) "Language checking (Español)").

## Complementos

Algunos complementos están disponibles en el paquete [gedit-plugins](https://www.archlinux.org/packages/?name=gedit-plugins).

### Añadiendo y haciendo complementos personalizados.

Un complemento que muestre errores mientras escribe para lenguajes como C, C++, etc, está disponible como [gedit-code-assistance](https://www.archlinux.org/packages/?name=gedit-code-assistance).

## Véase también

*   [Apps/Gedit - GNOME Wiki!](https://wiki.gnome.org/Apps/Gedit)