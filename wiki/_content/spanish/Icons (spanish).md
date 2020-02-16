**Estado de la traducción**
Este artículo es una traducción de [Icons](/index.php/Icons "Icons"), revisada por última vez el **2020-02-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Icons&diff=0&oldid=597379) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Related articles

*   [Cursor themes](/index.php/Cursor_themes_(Espa%C3%B1ol) "Cursor themes (Español)")
*   [Xfce](/index.php/Xfce_(Espa%C3%B1ol) "Xfce (Español)")

El proyecto freedesktop proporciona la [Especificación de Tema de Iconos](https://specifications.freedesktop.org/icon-theme-spec/latest/), que se aplica a la mayoría de los entornos de escritorio de linux e intenta unificar el aspecto de un montón de iconos en un *tema de iconos*. Freedesktop proporciona además la [Especificación de Nombre de Iconos](https://specifications.freedesktop.org/icon-naming-spec/latest/), la cual define un esquema de denominación estándar para los iconos que se cree serán instalados en cualquier sistema. El tema por defecto *hicolor* debe incluirlos todos.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Iconos y emblemas](#Iconos_y_emblemas)
    *   [1.2 Iconos tipo Mime](#Iconos_tipo_Mime)
    *   [1.3 Temas de icono](#Temas_de_icono)
        *   [1.3.1 Desde un paquete](#Desde_un_paquete)
        *   [1.3.2 Manualmente](#Manualmente)
*   [2 fstab / gvfs](#fstab_/_gvfs)

## Instalación

### Iconos y emblemas

Para agregar un icono personalizado a un tema existente puede utilizarse `xdg-icon-resource`. Éste redimensionará y copiará el icono en `$HOME/.local/share/icons/`. Con éste método, los emblemas personalizados pueden también pueden ser agregados. Ejemplos:

```
$ xdg-icon-resource install --size 128 --context emblems archuser-example.png # add as emblem
$ xdg-icon-resource install --size 128 archuser-example.png # add as normal icon

```

### Iconos tipo Mime

Actualmente los administradores de archivos no se basan en el tipo mime tradicional que genera `file --mime`. En su lugar se utilizan las definiciones de `/usr/share/mime/`. Al llamar a un icono según la definición encontrada allí y copiarlo en `~/.local/share/icons` causará que el administrador de archivos muestre un icono de tipo mime personalizado. Ésta órden ilustra el método:

 `Creates a custom icon for keepass database files (*.kdb)` 
```
# grep kdb /usr/share/mime/globs | egrep -o '.+\/[^:]+' | tr '/' '-'
application-x-keepass ;# rename your icon according to this output
xdg-icon-resource install --size 128 --context mimetypes application-x-keepass.png

```

### Temas de icono

**Sugerencia:** Se recomienda instalar el paquete [hicolor-icon-theme](https://www.archlinux.org/packages/?name=hicolor-icon-theme) ya que muchos programas almacenarán sus iconos en `/usr/share/icons/hicolor` y la mayoría de temas de iconos heredarán los iconos del tema Hicolor.

#### Desde un paquete

*   [Repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") — [búsqueda de "icon-theme"](https://www.archlinux.org/packages/?sort=&q=icon-theme&maintainer=&last_update=&flagged=&limit=50).
*   [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") — [búsqueda de "icon-theme"](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=icon-theme&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go).

#### Manualmente

Si no puede encontrar un paquete para el tema de icono que está buscando, necesitará instalarlo manualmente.

*   En primer lugar, encuentre y descargue el paquete de iconos que desee. Muchos diferentes temas de iconos pueden ser descargados desde los siguientes sitios [Customize.org](http://www.customize.org), [Opendesktop.org](http://opendesktop.org) y [Xfce-look.org](http://xfce-look.org/).

*   Después diríjase al directorio que contiene el paquete de iconos y extráigalo. Ejemplo `tar -xzf /home/user/downloads/icon-pack.tar.gz`.

*   Mueva la carpeta extraída que contiene los iconos ya sea a `~/.icons` o `~/.local/share/icons` (solo para usuarios) o a `/usr/share/icons` (sistema completo).

*   Opcional: ejecute `gtk-update-icon-cache -f -t ~/.icons/<theme_name>` para actualizar la caché de iconos.

*   Seleccione el tema de iconos usando la herramienta de configuración apropiada para su [entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") o [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)").

## fstab / gvfs

De acuerdo con éste [documento](https://github.com/GNOME/gvfs/blob/master/monitor/udisks2/what-is-shown.txt) los administradores de archivos que utilicen [GVFS](/index.php/GVFS "GVFS") (como Gnome Files o Thunar) pueden mostrar iconos para ubicaciones personalizadas, como recursos compartidos de NFS. Todo lo que necesita son algunas opciones de montaje extendidas dentro de `/etc/fstab` con nombre de iconos compatibles por su tema de iconos seleccionado:

 `/etc/fstab` 
```
hostname:/ /mnt/ nfs4 defaults,_netdev,user,rw,exec,comment=x-gvfs-show,x-gvfs-name=Network%20Attached%20Storage,x-gvfs-icon=network-server,x-gvfs-symbolic-icon=network-server,timeo=14,noatime 0 0

```