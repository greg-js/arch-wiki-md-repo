Artículos relacionados

*   [Firefox Tips and Tweaks](/index.php/Firefox_Tips_and_Tweaks "Firefox Tips and Tweaks")

[Firefox](http://www.firefox.com) es un popular proyecto open-source, es el navegador web de [Mozilla](http://www.mozilla.com).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Add-ons](#Add-ons)
*   [3 Plugins](#Plugins)
    *   [3.1 Integración con Gnome](#Integración_con_Gnome)
    *   [3.2 Diccionarios para corrección ortográfica](#Diccionarios_para_corrección_ortográfica)
    *   [3.3 Añadiendo motores de búsqueda a Firefox](#Añadiendo_motores_de_búsqueda_a_Firefox)
        *   [3.3.1 arch-firefox-search](#arch-firefox-search)
    *   [3.4 Firefox en español](#Firefox_en_español)
*   [4 Proyectos relacionados con Firefox](#Proyectos_relacionados_con_Firefox)
    *   [4.1 Derivados de Firefox](#Derivados_de_Firefox)
    *   [4.2 Mejorar la integración de Firefox con KDE](#Mejorar_la_integración_de_Firefox_con_KDE)
*   [5 Resolución de problemas](#Resolución_de_problemas)
    *   [5.1 Nueva barra de menús de Firefox 4/ botón de Firefox](#Nueva_barra_de_menús_de_Firefox_4/_botón_de_Firefox)
    *   [5.2 Problema abriendo carpetas contenedoras (KDE)](#Problema_abriendo_carpetas_contenedoras_(KDE))
    *   [5.3 Firefox continua creando ~/Desktop incluso cuando no quiero!](#Firefox_continua_creando_~/Desktop_incluso_cuando_no_quiero!)
    *   [5.4 Cómo prevenir que los plugins abran popups ?](#Cómo_prevenir_que_los_plugins_abran_popups_?)
    *   [5.5 Errores haciendo click con el botón central](#Errores_haciendo_click_con_el_botón_central)
    *   [5.6 La tecla de borrar no funciona como botón "Atrás"](#La_tecla_de_borrar_no_funciona_como_botón_"Atrás")
    *   [5.7 Firefox no recuerda la información de login](#Firefox_no_recuerda_la_información_de_login)
    *   [5.8 Sitios web rotos / campos de entrada con temas Gtk oscuros](#Sitios_web_rotos_/_campos_de_entrada_con_temas_Gtk_oscuros)
    *   [5.9 Problemas de asociación de ficheros](#Problemas_de_asociación_de_ficheros)
    *   [5.10 Modo "Voy a tener suerte"](#Modo_"Voy_a_tener_suerte")
    *   [5.11 Modo "Voy a tener suerte" (para DuckDuckGo)](#Modo_"Voy_a_tener_suerte"_(para_DuckDuckGo))
    *   [5.12 El diálogo "Desea que Firefox guarde sus pestañas para la próxima vez?" no aparece](#El_diálogo_"Desea_que_Firefox_guarde_sus_pestañas_para_la_próxima_vez?"_no_aparece)
*   [6 Recursos](#Recursos)

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [firefox](https://www.archlinux.org/packages/?name=firefox) de los repositorios oficiales.

Instale el idioma español con alguno de los siguientes paquetes:

*   [firefox-i18n-es-ar](https://www.archlinux.org/packages/?name=firefox-i18n-es-ar) – Español Argentina
*   [firefox-i18n-es-cl](https://www.archlinux.org/packages/?name=firefox-i18n-es-cl) – Español Chile
*   [firefox-i18n-es-es](https://www.archlinux.org/packages/?name=firefox-i18n-es-es) – Español España
*   [firefox-i18n-es-mx](https://www.archlinux.org/packages/?name=firefox-i18n-es-mx) – Español Mexico

Otras alternativas incluyen:

*   **Firefox Extended Support Release** — versión de soporte extendido

	[https://www.mozilla.org/firefox/organizations/](https://www.mozilla.org/firefox/organizations/) || [firefox-esr-bin](https://aur.archlinux.org/packages/firefox-esr-bin/)

*   **Firefox Beta** — versión en desarrollo

	[https://www.mozilla.org/firefox/channel/#beta](https://www.mozilla.org/firefox/channel/#beta) || [firefox-beta-bin](https://aur.archlinux.org/packages/firefox-beta-bin/)

*   **Firefox Developer Edition/Aurora** — para desarrolladores

	[https://www.mozilla.org/firefox/channel/#developer](https://www.mozilla.org/firefox/channel/#developer) || [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition)

*   **Firefox Nightly** — creadas diariamente para pruebas

	[https://nightly.mozilla.org/](https://nightly.mozilla.org/) || [firefox-nightly](https://aur.archlinux.org/packages/firefox-nightly/)

*   **Firefox KDE** — Version de Firefox que incorpora un parche de OpenSUSE para una mejor intregración con KDE de la que es posible con plugis de Firefox

	[https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox](https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox) || [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

Aquí pueden dar un vistazo a las diferentes [versiones](https://wiki.mozilla.org/Releases) de Firefox.

## Add-ons

Firefox es bien conocido por su gran cantidad de add-ons que pueden ser empleados para añadir nuevas características o modificar el comportamiento de las características existentes de Firefox. Puede encontrar nuevos add-ons o administrar los instalados mediante el "Administrador de Add-ons" del propio Firefox.

Para obtener una lista de add-ons populares, visite: [extensiones por descargas semanales](https://addons.mozilla.org/es-ES/firefox/extensions/?sort=popular) en Mozilla.

## Plugins

*See: [Browser plugins](/index.php/Browser_plugins "Browser plugins")*

Para comprobar qué plugins están instalados/habilitados, introduzca:

```
about:plugins

```

en la barra de direcciones de firefox. O vaya a *Addons* desde la barra principal y seleccione la pestaña *Plugins*. <-- tengo pendiente ponerme el vimperator -->

### Integración con Gnome

Instalar [firefox-extension-gnome-keyring-git](https://aur.archlinux.org/packages/firefox-extension-gnome-keyring-git/) de [AUR](/index.php/AUR "AUR") para integrar Firefox 3.6.x con el Gnome-keyring ("llavero" de gnome).

También puede instalar [firefox-extension-firefoxnotify-git](https://aur.archlinux.org/packages/firefox-extension-firefoxnotify-git/) para obtener la integración con libnotify/notifyOSD.

### Diccionarios para corrección ortográfica

Haga click derecho con el ratón en cualquier campo de texto y añada el diccionario para el idioma solicitado. Reinicie Firefox, y haga click en el campo de texto de nuevo para habilitar la corrección ortográfica.

U obténgalo mediante pacman:

```
pacman -Ss hunspell

```

### Añadiendo motores de búsqueda a Firefox

Visite [https://addons.mozilla.org/en-US/firefox/browse/type:4/](https://addons.mozilla.org/en-US/firefox/browse/type:4/) e instálelos.

Si desea uno personalizado, eche un vistazo a: `~/.mozilla/firefox/xxx.default/searchplugins/` donde xxx es su identificador de perfil.

#### arch-firefox-search

Añade soporte para las búsquedas relacionadas con Arch (AUR, wiki, forum, etc, según el usuario especifique) a la barra de utilidades de Firefox.

```
# pacman -S arch-firefox-search

```

### Firefox en español

Para que Firefox se muestre en español, además de instalar el paquete de idioma, es necesario establecer la variable de entorno `LC_ALL`. Por ejemplo, para español de España, se puede establecer en el fichero `~/.bashrc` añadiendo esta línea:

```
export LC_ALL=es_ES.UTF-8

```

## Proyectos relacionados con Firefox

### Derivados de Firefox

*   [Iceweasel](https://en.wikipedia.org/wiki/Iceweasel "wikipedia:Iceweasel") - El nombre de **dos** forks (variantes) de Firefox. Uno era un proyecto GNU; el nombre de este proyecto ha cambiado desde entonces a [Icecat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat"). [second](http://wiki.debian.org/Iceweasel) está siendo desarrollado por Debian y está basado en 2.0\. En el momento en el que se escribe en [AUR](/index.php/AUR "AUR") sólo está disponible Icecat.

*   [GNU/IceCat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat") - antiguamente conocido como GNU IceWeasel, es un navegador web distribuido por el proyecto GNU. IceCat es un fork de Mozilla Firefox realizado totalmente de software libre. Es compatible con el sistema operativo GNU/Linux y la gran mayoría de plugins de addons de Firefox. GNU/IceCat puede reemplazar totalmente a Firefox.

### Mejorar la integración de Firefox con KDE

*   [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

	con los parches de OpenSUSE, mejora la integración con KDE. Los parches de integración de OpenSUSE's con KDE son considerados los mejores por parte de muchos usuarios.

*   [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin)

	este plugin utiliza las KDE's KParts para empotrar visores de ficheros en navegadores no-KDE.

*   [Oxygen KDE](http://kde-look.org/content/show.php/?content=117962)

	Este addon provee de una integración mejor con el tema Oxygen de KDE, detección de esquemas de colores, iconos Faenza y varias personalizaciones más.

## Resolución de problemas

### Nueva barra de menús de Firefox 4/ botón de Firefox

Por defecto, Arch Linux muestra la disposición clásica de la barra de menú. Para activar la disposición nueva de Firefox 4 con el botón "Firefox" reemplazando la barra de menús, desmarque Vista -> Barra de tareas -> Barra de menú.

En GNU/Linux sólo obtendrá un botón de color gris en lugar del nuevo botón naranja de Windows. De todas maneras, puede cambiar esto por un agradable icono de Firefox añadiendo a su `~/.mozilla/firefox/userprofile/chrome/userChrome.css` esto:

```
#appmenu-toolbar-button {
  list-style-image: url("chrome://branding/content/icon16.png");
}
#appmenu-toolbar-button > .toolbarbutton-text,
#appmenu-toolbar-button > .toolbarbutton-menu-dropmarker {
  display: none !important;
}
```

NOTA: puede ser que, si no existen previamente, necesite crear los directorios `chrome` y `userChrome.css`.

### Problema abriendo carpetas contenedoras (KDE)

Si Firefox en lugar de lanzar su gestor de ficheros preferidos cuando se utiliza la opción "Abrir carpeta contenedora" en el administrador de descargas lanza otro, asegúrese que ha seleccionado su gestor de ficheros elegido (por ejemplo, Dolphin) en los ajustes de sistema de KDE.

	**System Settings -> Default Applications -> File Manager**

Si ya ha seleccionado su administrador de ficheros y Cervisia (u otro administrador de ficheros que no sea el favorito) es el que se está abriendo modifique el `$HOME/.local/share/applications/defaults.list` de su usuario, añadiendo estas dos líneas:

```
x-directory/normal=kde4-dolphin.desktop;kde4-kfmclient_dir.desktop;
inode/directory=kde4-dolphin.desktop;kde4-kfmclient_dir.desktop;kde4-gwenview.desktop;kde4-filelight.desktop;kde4-cervisia.desktop;

```

### Firefox continua creando `~/Desktop` incluso cuando no quiero!

Vea este [post](https://bbs.archlinux.org/viewtopic.php?id=66940).

### Cómo prevenir que los plugins abran popups ?

Se pregunta por qué aparecen popups incluso cuando los ha bloqueado? Al parecer el plugin de Flash puede esquivar los ajustes por defecto y molestarnos a base de popups. Nada que temer, podemos prevenir que esto suceda.

Para evitarlo:

1.  Escriba about:config en la barra de direcciones.
2.  Haga click en la página y seleccione Nuevo y después Entero.
3.  Llámelo privacy.popups.disable_from_plugins
4.  Ponga el valor a 2.

Los valores posibles son:

*   0: Permite que los plugins emitan popups
*   1: Permite popups, pero los limita a dom.popup_maximum.
*   2: Bloquea los popups de los plugins.
*   3: Bloquea los popups de los plugins, incluso en los sitios que están permitidos.

### Errores haciendo click con el botón central

```
! La URL no es válida y no puede ser cargada.

```

Otro síntoma es que hacer click con el botón central tiene un comportamiento inesperado, como por ejemplo acceder a una página aleatoria.

El motivo viene dado por el uso del botón central en los sistemas operativos derivados de UNIX. El botón central se emplea para pegar el texto que ha sido marcado/añadido al portapapeles. Luego esto posiblemente es lo que entra en conflicto con la característia de Firefox, el cual por defecto carga la URL del texto correspondiente cuando el botón es pulsado. Esto puede ser deshabilitado como sigue:

Abra el navegador, y escriba lo siguiente en la barra de direcciones:

```
about:config

```

Busque **middlemouse.contentLoadURL** y póngalo a false.

En caso alternativo, disponer del scroll tradicional al pulsar el botón central (comportamiento por defecto en los navegadores de Windows) puede obtenerse buscando **general.autoScroll** y poniéndo la variable a true.

### La tecla de borrar no funciona como botón "Atrás"

Como se indica en [este artículo](http://ubuntu.wordpress.com/2006/12/21/fix-firefox-backspace-to-take-you-to-the-previous-page/), la característica ha sido eliminada para solucionar un bug. Siga las siguientes instrucciones para volver al comportamiento original.

Abra el navegador y escriba la siguiente dirección:

```
about:config

```

Busque la propiedad **browser.backspace_action** y póngala a 0 (cero).

### Firefox no recuerda la información de login

Puede ser debido a que el fichero `cookies.sqlite` del directorio [de su perfil](http://support.mozilla.com/en-US/kb/Profiles#How_to_find_your_profile) está corrupto. Para solucionarlo, renombre o elimine el fichero cookie.sqlite mientras Firefox no se está ejecutando.

Abra un terminal (de su elección) y escriba lo siguiente:

```
$ cd ~/.mozilla/firefox/xxxxxxxx.default/
$ rm -f cookies.sqlite

```

**Nota:** xxxxxxxx es una cadena de caracteres aletoria de 8 caracteres.

Reinicie Firefox y comprube si ha resuelto el problema.

### Sitios web rotos / campos de entrada con temas Gtk oscuros

Cuando se usa un tema [GTK](/index.php/GTK_(Espa%C3%B1ol) "GTK (Español)") oscuro, es posible que algunas páginas de Internet tengan campos de entrada y de texto ilegibles (p.e. Amazon - texto blanco sobre fondo blanco). Esto puede suceder porque el sitio web sólo defina el color de fondo o el de texto, y Firefox utilice el del tema [GTK](/index.php/GTK_(Espa%C3%B1ol) "GTK (Español)").

Una solución es definir explícitamente colores estándar para todas las páginas web en `~/.mozilla/firefox/.../chrome/userContent.css`.

Lo siguiente define los campos de entrada de texto al estándar letra negra sobre fondo blanco; Ambos pueden ser redefinidos por el sitio web, así que se fuerza que los colores sean los siguientes:

```
input {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

textarea {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

```

Esto forzará los colores (Opción "Permitir a las páginas elegir sus propios colores [..]" , en el diálogo **Preferencias > Contenido > Color**):

```
input {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

textarea {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

```

Cambie los colores por valores adecuados, o utilice un add-on como por ejemplo [Stylish](https://addons.mozilla.org/en-US/firefox/addon/2108).

### Problemas de asociación de ficheros

Para no usuarios de [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), es posible que Firefox no asocie los tipos de archivo (en el diálogo "Abrir Con"). Instalar [libgnome](https://aur.archlinux.org/packages/libgnome/) soluciona el problema:

```
pacman -S libgnome

```

Si está utilizando KDE también puede hacer lo siguiente:

```
ln -s ~/.local/share/applications/mimeapps.list ~/.local/share/applications/mimeinfo.cache

```

De ahora en adelante Firefox debería utilizar las aplicaciones que están indicadas explícitamente en KDE.

### Modo "Voy a tener suerte"

El modo "Voy a tener suerte" permite al usuario aprovechar la potencia de la característica "Voy a tener suerte" de Google mediante la barra de direcciones de Firefox.

To activate this mode, do the following Para activar este modo, haga lo siguiente (solución extraída de [este post](http://superuser.com/questions/76530/default-to-im-feeling-lucky-for-non-url-search-terms-in-firefox-address-bar)):

1.  Teclee "**about:config**" en la barra de direcciones.
2.  Busque la cadena de caracteres **keyword.url**
3.  Modifique su valor (si lo tiene) a

```
http://www.google.com/search?btnI=I%27m+Feeling+Lucky&q=

```

### Modo "Voy a tener suerte" (para DuckDuckGo)

"Voy a tener suerte" es similar al modo "Voy a tener suerte" de Google pero utilizando el motor de búsqueda DuckDuckGo.

Para activar este modo, haga lo siguiente (solución utilizando la anterior):

1.  Teclee "**about:config**" en la barra de direcciones.
2.  Busque la cadena de caracteres **keyword.url**
3.  Modifique su valor (si lo tiene) a

```
https://duckduckgo.com/?q=! 

```

El último caracter es un espacio ' '. Es necesario porque si no lo pone, se convertirá en un !Bang.

### El diálogo "Desea que Firefox guarde sus pestañas para la próxima vez?" no aparece

Desde el [sitio de soporte de Mozilla](http://support.mozilla.com/en-US/questions/767751):

1.  Teclee "**about:config**" en la barra de direcciones.
2.  Ponga la variable **browser.warnOnQuit** a **true**.
3.  Ponga la variable **browser.showQuitWarning** a **true**.

## Recursos

*   [Detalles sobre Debian y Mozilla® Firefox](http://web.glandium.org/blog/?p=97)

	Una recolección de los problemas de los que mantienen el paquete de Firefox para Debian.

*   [Gnuzilla and IceWeasel](http://www.gnu.org/software/gnuzilla/)

	Website oficial para los forks de GNU Mozilla.