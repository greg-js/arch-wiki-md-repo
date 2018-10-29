Artículos relacionados

*   [Browser Plugins (Español)](/index.php/Browser_Plugins_(Espa%C3%B1ol) "Browser Plugins (Español)")
*   [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon")
*   [UZBL-Browser](/index.php/UZBL-Browser "UZBL-Browser")
*   [Dillo](/index.php/Dillo "Dillo")

[Midori](http://midori-browser.org) es un navegador web ligero basado en Webkit y desarrollado por Christian Dywan. Forma parte del proyecto [Xfce](/index.php/Xfce "Xfce") Goodies.

Algunas de sus características son:

*   Integración completa con [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)") 2 and GTK+ 3.
*   Renderizado rápido, gracias al motor [WebKitGTK+](https://en.wikipedia.org/wiki/es:WebKit "wikipedia:es:WebKit").
*   Pestañas, ventanas y **gestión de sesión**.
*   Búsqueda web flexible y configurable.
*   Soporte para **estilos y scripts definidos por el usuario**.
*   **Gestión directa** de marcadores.
*   Interfaz extensible y personalizable.
*   **Extensiones** comunes como AdBlock, formulario de historial, acceso rápido, etc.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Extensiones](#Extensiones)
    *   [2.1 AdBlock](#AdBlock)
    *   [2.2 Motores de búsqueda](#Motores_de_b.C3.BAsqueda)
    *   [2.3 Scripts de usuarios](#Scripts_de_usuarios)
    *   [2.4 Plugin flash](#Plugin_flash)
*   [3 Trucos y consejos](#Trucos_y_consejos)
    *   [3.1 Flash Block](#Flash_Block)
    *   [3.2 Filtros de AdBlock personalizados](#Filtros_de_AdBlock_personalizados)
    *   [3.3 Corregir fuentes pixeladas](#Corregir_fuentes_pixeladas)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Hay varios opciones disponibles:

1.  Midori estable puede ser [instalado](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") con el paquete [midori](https://www.archlinux.org/packages/?name=midori).
2.  Midori establo que carece del requisito de [Zeitgeist](/index.php/Zeitgeist "Zeitgeist") está disponible con el paquete [midori-no-zeitgeist](https://aur.archlinux.org/packages/midori-no-zeitgeist/).
3.  La versión de desarrollo también está disponible con el paquete [midori-bzr](https://aur.archlinux.org/packages/midori-bzr/).

## Extensiones

### AdBlock

Para habilitar la extensión AdBlock vaya a *Menú > Preferencias > Extensiones* y marque la casilla *Bloqueador de publicidad* .

La extensión AdBlock de Midori usa las mismas listas que la extensión AdBlock Plus de Firefox por lo que puede obtener más listas en [Sitio de AdBlock Plus (en Inglés)](http://easylist.adblockplus.org/en/). Puede también bloquear imágenes de forma específica en varios sitios haciendo clic derecho en ellas y seleccionando *Bloquear imagen*.

### Motores de búsqueda

Midori también soporta motores de búsqueda, prácticamente de la misma manera que otros navegadores. Varios motores de búsqueda tienen accesos directos de manera que se puedan usar fácilmente desde la barra de direcciones. Para gestionar sus motores de búsqueda haga clic en el icono en la caja del motor de búsqueda y seleccione *Gestionar motores de búsqueda*.

Por su puesto puede aprovechar de forma inteligente estas características, como proveer varios accesso directos para varios sitios web (no solo para búsquedas). Por ejemplo puede añadir una entrada en el diálogo de los *Motores de búsqueda* con la clave *arch* y la información necesaria para acceder a la página principal de Arch Linux. Ahora puede acceder al sitio web de Arch Linux únicamente escrbiendo *arch*.

Otro ejemplo puede ser el añadir un acceso directo a un acortador de URLs:

*   Simplemente añade un nuevo motor de búsqueda con la URL `[http://is.gd/create.php?longurl=](http://is.gd/create.php?longurl=)` (u otro acortador con funcionalidad parecida).
*   Asígnele una clave (*sh* en este caso).
*   Obtenga una URL corta para cualquier enlace escribiendo:

```
sh *enlace*

```

en la barra de direcciones.

### Scripts de usuarios

Para habilitar la extensión de scripts de usuarios vaya a *Menú > Preferencias > Extensiones* y marque la casilla *Complementos de usuario* . Los scripts de usuario de Midori son compatibles con los scripts de [Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/). Puede encontrar una extensa lista de script en [http://userscripts-mirror.org/](http://userscripts-mirror.org/).

Para una instalación manual, tiene que crear la carpeta `~/.local/share/midori/scripts` y copiar ahí los scripts. Midori cargará de forma automática todos los scripts compatibles dentro de esa carpeta.

### Plugin flash

Para que el complemento Flash funcione en Midori, instale el paquete [midori-flash](https://aur.archlinux.org/packages/midori-flash/).

Alternativamente, instale [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) desde el repositorio principal y añada `export MOZ_PLUGIN_PATH="/usr/lib/mozilla/plugins"` a su `.bashrc`, `.xprofile`, o el archivo de configuración del intérprete de comandos correspondiente.

## Trucos y consejos

### Flash Block

También puede obtener la conocida extensión FlashBlock en formato script de usuario en [userscripts-mirror.org](http://userscripts-mirror.org/scripts/show/46673) o usando el Flash script WannaBe de [[1]](http://rightfootin.blogspot.fr/2009/04/flashblock-wannabe.html), este script tiene que instalar en `~/.local/share/midori/scripts` y en `~/.local/share/midori/styles`, el fichero JavaScript y el fichero CSS, respectivamente.

### Filtros de AdBlock personalizados

El soporte de AdBlock de Midori es más bien básico, tan solo puede usar lista pre-hechas o bloquear algunas imágenes. Puede resolver este problema creando sus propias listas e indicando a Midori donde encontrarlas.

Para ello:

*   Cree una carpeta para sus filtros, como `~/.local/share/midori/filters`
*   En esa carpeta cree un fichero con el contenido que desee bloquear:

 `myadblockfilters.txt` 
```
[Adblock]
! Title: Personal AdBlocker v1
! Last modified: 31 Oct 2012 18:14 UTC
! Expires: 365 days

! Los comentarios se escriben anteponiendo un símbolo de exclamación de cierre

! Puede filtrar algunos elementos directamente
[http://forums.fedoraforum.org//forum/images/smilies/smile.gif](http://forums.fedoraforum.org//forum/images/smilies/smile.gif)

! o usar wildcards para filtrar un conjunto de cosas de golpe.
[http://ubuntuforums.org/images/rebrand/statusicon/subforum_*.gif](http://ubuntuforums.org/images/rebrand/statusicon/subforum_*.gif)

! o usar etiquetas DOM, ids o clases
www.phoronix.com#DIV.phxcms_header_legacy
www.phoronix.com#DIV.phxcms_bar_align

```

*   Vaya a *Menú > Preferencias > Extensiones* y haga clic en el icono de configuración de Adblock y añada:

```
file://.local/share/midori/filters/myadblockfilters.txt

```

### Corregir fuentes pixeladas

Algunas webs como github.com tienden a usar una fuente de mapas de bits de X11 llamada Clean.

Un arreglo sencillo es deshabilitar las fuentes de mapas de bits, para ello ejecute:

```
# ln -s /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d/

```

## Véase también

*   [Midori FAQ](http://wiki.xfce.org/midori/faq)