Existen muchos temas de cursores disponibles para el sistema de ventanas X11 además del cursor negro que su utiliza por defecto. Esta guía le enseñará donde conseguirlos, como instalarlos y como configurarlos.

## Contents

*   [1 Obtener temas de cursor para el ratón](#Obtener_temas_de_cursor_para_el_ratón)
*   [2 Instalar temas de cursor para el ratón](#Instalar_temas_de_cursor_para_el_ratón)
*   [3 Configurando temas de cursor](#Configurando_temas_de_cursor)
*   [4 Más información](#Más_información)

## Obtener temas de cursor para el ratón

A continuación se listan enlaces donde puede usted bajarse temas de cursor:

*   [KDE Look](http://kde-look.org/index.php?xcontentmode=36)
*   [Freshmeat](http://themes.freshmeat.net/browse/982/)
*   [Customize.org](http://www.customize.org/list/xcursors)

## Instalar temas de cursor para el ratón

*   Extraiga el paquete de temas de cursor:

```
tar -zxvf foobar-cursor-theme-package-foo.tar.gz
o bien
tar -jxvf foobar-cursor-theme-package-foo.tar.bz2

```

*   Cree un directorio para el tema de cursor:

Ejemplo: ~FooBar-~AweSoMe-Cursors-v2.98beta

Instalación personal de usuario:

```
mkdir -p ~/.icons/foobar/cursors

```

Instalación global de sistema:

```
mkdir -p /usr/share/icons/foobar/cursors

```

Asegúrese de simplificar el nombre del tema ('foobar' en vez de '~FooBar-~AweSoMe-Cursors-v2.98beta')

*   Copie los archivos de cursor en el directorio apropiado:

```
cp -R FooBar-AweSoMe-Cursors-v2.98beta/cursors/* /usr/share/icons/foobar/cursors/

```

Si el paquete incluye un archivo index.theme file compruebe si hay una línea "Inherits" dentro. Si es así, compruebe si el tema heredado existe también bajo ese nombre en su sistema (renómbrelo si es necesario). Tenga en cuenta que X ya viene con los temas 'redglass' y 'whiteglass' en /usr/X11R6/lib/icons o /usr/share/icons. Algunas aplicaciones siguen usando el cursor X11 por defecto cuando se debería mostrar una versión left_ptr_watch del tema o similar. Eche un vistazo a los enlaces simbólicos en el "changelog" que pertenece al [proyecto 3Dcursors de KDE-Look](http://www.kde-look.org/content/show.php?content=5265) para arreglar esto.

*   Copie el archivo index.theme en el directorio:

```
cp -R FooBar-AweSoMe-Cursors-v2.98beta/index.theme /usr/share/icons/foobar/index.theme

```

Si el paquete no tiene index.theme o si no incluye una línea "Inherits" no tiene que copiar este archivo.

## Configurando temas de cursor

Para cambiar localmente un tema de cursor, añada esta línea a su archivo ~/.Xdefaults:

```
Xcursor.theme: foobar

```

Asegúrese de que el archivo ~/.Xdefaults es llamado por su gestor de ventanas. Puede obligar a que sea cargado ejecutando xrdb ~/.Xdefaults antes de cargar su gestor de ventanas (por ejemplo en .xinitrc si utiliza startx). Consulte la documentación de su gestor de ventanas para los detalles. Si lo que quiere usted es más bien cambiar el cursor globalmente, o si encuentra problemas con el método anterior (por ejemplo en Firefox), cree el archivo /usr/share/icons/default/index.theme. Edítelo entonces, y añada lo siguiente:

```
[icon theme] 
Inherits=foobar

```

Puede opcionalmente añadir esta línea a ~/.Xdefaults si su tema de cursor permite multiples tamaños:

```
Xcursor.size:  32       #  32, 48 or 64 are probably good values

```

Si no sabe nada acerca de tamaños de cursor permitidos simplemente arranque X sin esta configuración y deje que éste alija el tamaño de cursor automáticamente.

## Más información

Para obtener más información acerca de los cursores en X (directorios admitidos, formatos, compatibilidad, etc.) consulte la página de manual:

```
man Xcursor

```

**Nota:** Si las animaciones parpadean en su tarjeta nvidia, añada la línea siguiente a su archivo xorg.conf, en la sección "nvidia device", para arreglarlo:

```
Option "HWCursor" "off"

```