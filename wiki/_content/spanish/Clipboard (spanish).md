**Estado de la traducción**
Este artículo es una traducción de [Clipboard](/index.php/Clipboard "Clipboard"), revisada por última vez el **2019-02-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Clipboard&diff=0&oldid=562231) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Copiando texto desde un terminal](/index.php/Copying_text_from_a_terminal "Copying text from a terminal")
*   [Errores pulsando con el botón central en Firefox](/index.php/Firefox_(Espa%C3%B1ol)#Errores_haciendo_click_con_el_botón_central "Firefox (Español)")
*   [Desactivar pegar desde el ratón en GTK+](/index.php/GTK%2B_(Espa%C3%B1ol)#Desactivar_pegar_desde_el_ratón "GTK+ (Español)")
*   [Vim#Clipboard](/index.php/Vim#Clipboard "Vim")

De acuerdo con [Wikipedia:es:Portapapeles](https://en.wikipedia.org/wiki/es:Portapapeles "wikipedia:es:Portapapeles"):

	El portapapeles es una habilidad utilizada para el almacenamiento de datos a corto plazo y/o la transferencia de datos entre documentos o aplicaciones, a través de las operaciones [copiar y pegar](https://en.wikipedia.org/wiki/es:copiar_y_pegar "wikipedia:es:copiar y pegar").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Historia](#Historia)
*   [2 Selecciones](#Selecciones)
*   [3 Herramientas](#Herramientas)
*   [4 Gestores](#Gestores)
*   [5 Véase también](#Véase_también)

## Historia

En X10, se introdujeron *búffers de corte*. Estos eran buffers limitados que almacenaban texto arbitrario y eran utilizados por la mayoría de las aplicaciones. Sin embargo, fueron ineficientes y su implementación varió, por lo que se introdujeron las selecciones. Los búferes de corte han quedado en desuso hace mucho tiempo, y aunque algunas aplicaciones (como [xterm](/index.php/Xterm "Xterm")) pueden tener soporte heredado para ellos, no se recomienda su uso.

## Selecciones

[Freedesktop.org](/index.php/Freedesktop.org_(Espa%C3%B1ol) "Freedesktop.org (Español)") describe las dos *selecciones* principales de la siguiente manera: [[1]](https://specifications.freedesktop.org/clipboards-spec/clipboards-latest.txt)

	PRIMARIA

	se utiliza para el texto seleccionado actualmente, incluso si no se ha copiado explícitamente, y para pegar con el botón central del ratón. En algunos casos, también es posible pegar con un atajo de teclado.

	PORTAPAPELES

	se utiliza para las órdenes explícitas de copiar/pegar que involucran atajos de teclado o elementos de menú. Por lo tanto, se comporta como el sistema de un solo portapapeles en Windows. A diferencia de PRIMARIA, también puede manejar [mútiples formatos de datos](https://stackoverflow.com/questions/3571179/how-does-x11-clipboard-handle-multiple-data-formats).

La mayoría de los programas para [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"), incluidas las aplicaciones [Qt](/index.php/Qt "Qt") y [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)"), siguen este comportamiento. Si bien [ICCCM](https://tronche.com/gui/x/icccm/) también define una selección SECUNDARIA, no tiene un acuerdo consensuado sobre el propósito. A pesar de la denominación, las tres selecciones son básicamente "portapapeles". En lugar del antiguo sistema de "buffers de corte" donde las aplicaciones arbitrarias podrían modificar los datos almacenados en los buffers de corte, solo una aplicación puede controlar o "poseer" una selección a la vez. Esto evita inconsistencias en el funcionamiento de las selecciones.

Véase la página de [atajos de teclado](/index.php/Keyboard_shortcuts "Keyboard shortcuts") que enumera los accesos directos predeterminados en muchos programas.

También es importante darse cuenta de que, según los protocolos de selección, no se copia nada [hasta que se pegue](https://unix.stackexchange.com/questions/213840/how-to-toggle-or-turn-off-text-selection-being-sent-to-the-clipboard/213843#213843). Por ejemplo, si selecciona una palabra en una ventana de terminal, cierra el terminal y luego quiere pegarlo en otro lugar, no funcionará porque el terminal se ha ido y el texto no se ha copiado en ninguna parte. Si desea que la palabra se mantenga después de cerrar la ventana del terminal, considere instalar un [gestor de portapapeles](#Gestores).

**Nota:** Los [gestores de portapapeles](#Gestores) pueden cambiar significativamente la experiencia del usuario, por ejemplo, podrían sincronizar las selecciones PRIMARIA y PORTAPAPELES para emular un sistema de un solo portapapeles.

## Herramientas

Esta sección lista las herramientas para manipular los portapapeles en la línea de órdenes.

*   **sselp** — Impresora de selección X simple. Imprime la selección X a la salida estándar.

	[http://tools.suckless.org/x/sselp](http://tools.suckless.org/x/sselp) || [sselp](https://aur.archlinux.org/packages/sselp/)

*   **xclip** — Una interfaz ligera y basada en la línea de órdenes para el portapapeles.

	[https://github.com/astrand/xclip](https://github.com/astrand/xclip) || [xclip](https://www.archlinux.org/packages/?name=xclip)

*   **xsel** — Programa de línea de órdenes para obtener y configurar los contenidos de la selección en X.

	[http://www.vergenet.net/~conrad/software/xsel/](http://www.vergenet.net/~conrad/software/xsel/) || [xsel](https://www.archlinux.org/packages/?name=xsel)

## Gestores

Esta sección lista los demonios que rastrean su portapapeles, para proporcionar un historial y/o sincronización del portapapeles.

*   **Anamnesis** — Gestor de portapapeles que almacena todo el historial del portapapeles y ofrece una interfaz para realizar una búsqueda de texto completo. Tiene disponibles una línea de órdenes y un modo gráfico.

	[http://anamnesis.sourceforge.net/](http://anamnesis.sourceforge.net/) || [anamnesis](https://aur.archlinux.org/packages/anamnesis/)

*   **Autocutsel** — Interfaces de línea de órdenes y demonio para sincronizar PRIMARIA, `PORTAPAPELES` y cortar selecciones del búfer.

	[http://www.nongnu.org/autocutsel/](http://www.nongnu.org/autocutsel/) || [autocutsel](https://www.archlinux.org/packages/?name=autocutsel)

*   **Clipboard Indicator** — Extensión del gestor del portapapeles para GNOME Shell. Añade un indicador del portapapeles al panel superior y almacena en caché el historial del portapapeles.

	[https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator](https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator) || [gnome-shell-extension-clipboard-indicator-git](https://aur.archlinux.org/packages/gnome-shell-extension-clipboard-indicator-git/)

*   **ClipIt** — Bifurcación de Parcellite. Tiene disponible una línea de órdenes y un modo gráfico.

	[https://github.com/CristianHenzel/ClipIt](https://github.com/CristianHenzel/ClipIt) || [clipit](https://aur.archlinux.org/packages/clipit/)

*   **Clipman** — Complemento de gestor de portapapeles para el panel de Xfce4\. Mantiene el contenido del portapapeles mientras que se suele perder cuando se cierra una aplicación. Es capaz de manejar texto e imágenes, y tiene una función para ejecutar acciones específicas en el texto seleccionado al compararlas con expresiones regulares.

	[https://goodies.xfce.org/projects/panel-plugins/xfce4-clipman-plugin](https://goodies.xfce.org/projects/panel-plugins/xfce4-clipman-plugin) || [xfce4-clipman-plugin](https://www.archlinux.org/packages/?name=xfce4-clipman-plugin)

*   **ClipManager** — Gestor de portapapeles multiplataforma escrito en Python y Qt.

	[https://github.com/scottwernervt/clipmanager](https://github.com/scottwernervt/clipmanager) || [clipmanager](https://aur.archlinux.org/packages/clipmanager/)

*   **Clipmenu** — Gestor de portapapeles basado en Dmenu.

	[https://github.com/cdown/clipmenu/](https://github.com/cdown/clipmenu/) || [clipmenu](https://www.archlinux.org/packages/?name=clipmenu)

*   **Clipster** — Un gestor de portapapeles ligero, controlado por línea de órdenes, escrito en Python.

	[https://github.com/mrichar1/clipster](https://github.com/mrichar1/clipster) || [clipster](https://aur.archlinux.org/packages/clipster/)

*   **CopyQ** — Gestor de portapapeles Qt inteligente con historial de búsqueda y modificable, con acciones personalizadas en elementos y soporte de línea de órdenes.

	[https://github.com/hluk/CopyQ](https://github.com/hluk/CopyQ) || [copyq](https://www.archlinux.org/packages/?name=copyq)

*   **[Glipper](https://en.wikipedia.org/wiki/Glipper "wikipedia:Glipper")** — Gestor de portapapeles para el escritorio de GNOME con muchas características y soporte para complementos.

	[https://launchpad.net/glipper](https://launchpad.net/glipper) || [glipper](https://aur.archlinux.org/packages/glipper/)

*   **GPaste** — Sistema de gestión de portapapeles que pretende ser un Parcellite de nueva generación, con una estructura modular dividida en un par de bibliotecas y un demonio para la adaptabilidad. Ofrece una extensión de GNOME Shell y una interfaz CLI..

	[https://github.com/Keruspe/GPaste](https://github.com/Keruspe/GPaste) || [gpaste](https://www.archlinux.org/packages/?name=gpaste)

*   **[Greenclip](/index.php/Greenclip "Greenclip")** — Gestor de portapapeles simple para ser integrado con rofi.

	[https://github.com/erebe/greenclip](https://github.com/erebe/greenclip) || [rofi-greenclip](https://aur.archlinux.org/packages/rofi-greenclip/)

*   **[Klipper](https://en.wikipedia.org/wiki/Klipper "wikipedia:Klipper")** — Gestor de portapapeles con todas las funciones para el escritorio KDE.

	[https://userbase.kde.org/Klipper](https://userbase.kde.org/Klipper) || [plasma-workspace](https://www.archlinux.org/packages/?name=plasma-workspace)

*   **Parcellite** — Gestor de portapapeles ligero pero lleno de funciones. Tiene disponible una línea de órdenes y un modo gráfico.

	[http://parcellite.sourceforge.net/](http://parcellite.sourceforge.net/) || [parcellite](https://www.archlinux.org/packages/?name=parcellite)

*   **Pasteall** — Monitor de portapapeles simple y funcional (con notificaciones en portugués).

	[https://github.com/ShyPixie/Pasteall](https://github.com/ShyPixie/Pasteall) || [pasteall](https://aur.archlinux.org/packages/pasteall/)

*   **Qlipper** — Applet de historial de portapapeles ligero y multiplataforma basado en Qt.

	[https://github.com/pvanek/qlipper/](https://github.com/pvanek/qlipper/) || [qlipper](https://aur.archlinux.org/packages/qlipper/)

*   **xclipboard** — Cliente de línea de órdenes del portapapeles oficial de X.

	[https://www.x.org/releases/X11R7.5/doc/man/man1/xclipboard.1.html](https://www.x.org/releases/X11R7.5/doc/man/man1/xclipboard.1.html) || [xorg-xclipboard](https://www.archlinux.org/packages/?name=xorg-xclipboard)

*   **xcmenu** — Sincronizador del portapapeles desarrollado para usuarios de gestores de ventanas.

	[https://github.com/dindon-sournois/xcmenu](https://github.com/dindon-sournois/xcmenu) || [xcmenu-git](https://aur.archlinux.org/packages/xcmenu-git/)

## Véase también

*   [Cortar y pegar en X](https://specifications.freedesktop.org/clipboards-spec/clipboards-latest.txt)
*   [Selecciones en X, Cortar Búffers, y Matar Anillos.](https://www.jwz.org/doc/x-cut-and-paste.html)