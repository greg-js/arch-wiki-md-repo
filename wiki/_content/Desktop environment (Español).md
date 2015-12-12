# Desktop environment (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Artículos relacionados

*   [Display Manager (Español)](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)")
*   [Window Manager (Español)](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)")
*   [Default applications](/index.php/Default_applications "Default applications")

Un [entorno de escritorio](https://en.wikipedia.org/wiki/es:Desktop_environment "wikipedia:es:Desktop environment") proporciona una _completa_ interfaz gráfica de usuario (GUI) para un sistema donde se agrupan una diversidad de clientes de X escritos con un conjunto de herramientas Widget y un conjunto de bibliotecas comunes.

## Contents

*   [1 X Window System](#X_Window_System)
*   [2 Entornos de Escritorio](#Entornos_de_Escritorio)
    *   [2.1 Lista de entornos de escritorio](#Lista_de_entornos_de_escritorio)
        *   [2.1.1 Soportados oficialmente](#Soportados_oficialmente)
        *   [2.1.2 Sin soporte oficial](#Sin_soporte_oficial)
    *   [2.2 Comparación de entornos de escritorio](#Comparaci.C3.B3n_de_entornos_de_escritorio)
        *   [2.2.1 Uso de los recursos](#Uso_de_los_recursos)
        *   [2.2.2 Entornos familiares](#Entornos_familiares)
*   [3 Entornos personalizados](#Entornos_personalizados)

## X Window System

El [sistema de ventanas X](https://en.wikipedia.org/wiki/es:X_Window_System "wikipedia:es:X Window System") proporciona la base para una interfaz gráfica de usuario. Antes de instalar un gestor de ventanas, es necesaria la instalación previa de un servidor X funcional. Consulte [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") para obtener información detallada.

_X proporciona el marco básico, o primigenio, para la construcción de estos entornos GUI: permite dibujar y mover ventanas en la pantalla e interactuar con el ratón y el teclado. X no proporciona la interfaz de usuario — otros programas clientes individuales conocidos como gestores de ventanas proporcionan dicha interfaz. En consecuencia, el estilo visual de los entornos que corren en X ​​varía mucho; diferentes tipos de programas pueden presentar interfaces radicalmente diferentes. X está construido como una capa de abstracción adicional (a modo de aplicación) que emerge después del kernel del sistema operativo._

El usuario tiene libertad para configurar su entorno GUI de muchas maneras.Los entornos de escritorio, simplemente, proporcionan un medio completo y conveniente de realizar esta tarea.

## Entornos de Escritorio

El entorno de escritorio, como diversidad de paquetes de clientes de X, viene a proporcionar los elementos comunes de la interfaz gráfica de usuario, tales como iconos, ventanas, barras de herramientas, fondos de pantalla y widgets de escritorio. Además, la mayoría de los entornos de escritorio incluyen un conjunto de aplicaciones integradas y de utilidades.

Tenga en cuenta que los usuarios son libres de mezclar aplicaciones y combinar múltiples entornos de escritorio. Por ejemplo, un usuario de KDE podrá instalar y ejecutar las aplicaciones de GNOME como el navegador web Epiphany, si lo prefiere antes que el navegador web Konqueror de KDE. Un inconveniente de este proceder es que muchas aplicaciones proporcionados por proyectos de un entorno de escritorio se basan, en gran medida, en las respectivas bibliotecas subyacentes al DE en cuestión. Como resultado, la instalación de aplicaciones de distintos entornos de escritorio implicará mayor instalación de número de dependencias. Los usuarios que buscan ahorrar espacio en disco y evitar [hinchar el software](https://en.wikipedia.org/wiki/es:Software_inflado "wikipedia:es:Software inflado") suelen eludir estos entornos mixtos, o mirar otras alternativas más ligeras.

Además, las aplicaciones proporcionadas por los DE tienden a integrarse mejor con sus ambientes nativos. Superficialmente, la utilización de entornos mixtos, que usan librerías de desarrollo diferentes, se traduce en discrepancias visuales (es decir, las interfaces utilizarán diferentes iconos y estilos de widget). En cuanto a la experiencia del usuario, entornos mixtos no pueden comportarse de manera similar a los entornos nativos (por ejemplo, los iconos de un solo clic versus doble clic, la función arrastrar y soltar) que puede causar confusión o comportamientos inesperados.

### Lista de entornos de escritorio

#### Soportados oficialmente

*   **[Cinnamon](/index.php/Cinnamon "Cinnamon")** — Cinnamon es un fork de GNOME 3\. Cinnamon se esfuerza por ofrecer una experiencia conocida por el usuario, similar a GNOME 2.

[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — El escritorio Enlightenment proporciona un gestor de ventanas eficiente, a la vez que impresionante, sobre la base de las bibliotecas Enlightenment Foundation Libraries (EFL), junto con otros componentes de escritorio esenciales como un gestor de archivos, iconos del escritorio y widgets. Cuenta con un nivel sin precedentes de capacidad para ejecutar temas gráficos, sin dejar por ello de ser capaz de ejecutarse en hardware antiguo o dispositivos integrados.

[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment17](https://www.archlinux.org/packages/?name=enlightenment17)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)]</sup>

*   **[GNOME](/index.php/GNOME "GNOME")** — El proyecto GNOME proporciona dos cosas: El entorno de escritorio GNOME, un escritorio intuitivo y atractivo para los usuarios, y la plataforma de desarrollo GNOME, un amplio marco para la creación de aplicaciones que se integran en el resto del escritorio. GNOME es libre, usable, accesible, internacional, amistoso para el desarrollador, organizado, sostenido por la comunidad.

[http://www.gnome.org/about/](http://www.gnome.org/about/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **[KDE Plasma](/index.php/KDE "KDE")** — El entorno de escritorio KDE Plasma es un entorno de trabajo familiar. El escritorio Plasma ofrece todas las herramientas necesarias para una experiencia de escritorio moderna con enfasis en la productividad

[http://www.kde.org/workspaces/plasmadesktop/](http://www.kde.org/workspaces/plasmadesktop/) || KDE 4:[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace), Plasma 5:[plasma](https://www.archlinux.org/groups/x86_64/plasma/)

*   **[LXDE](/index.php/LXDE "LXDE")** — The "Lightweight X11 Desktop Environment" es un entorno de escritorio rápido y de bajo consumo. Mantenido por una comunidad internacional de desarrolladores, viene con una interfaz atractiva, soporte multi-idioma, teclas de acceso rápido estándar y funciones adicionales como la navegación por pestañas de los archivos. Fundamentalmente diseñado para ser ligero, LXDE utiliza menos CPU y memoria RAM que otros entornos. Es especialmente beneficioso para los ordenadores con especificaciones de hardware de bajo rendimiento, tales como netbooks, dispositivos móviles (por ejemplo, MIDs) u otros ordenadores.

[http://lxde.org/](http://lxde.org/) || [lxde](https://www.archlinux.org/groups/x86_64/lxde/)

*   **[LXQt](/index.php/LXQt "LXQt")** — LXQt es un un puerto que utliza Qt con la última versión de LXDE ("Lightweight X11 Desktop Environment"). Es el producto de la fusión entre los proyectos LXDE-Qt y Razor-Qt: Un entorno liviano, modular, rápido y amigable.

[http://lxqt.org/](http://lxqt.org/) || [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/)

*   **[MATE](/index.php/MATE "MATE")** — MATE es un fork de GNOME 2\. Mate ofrece un escritorio intuitivo y atractivo para los usuarios de Linux que utilizan metáforas tradicionales.

[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || GTK+ 2:[mate](https://www.archlinux.org/groups/x86_64/mate/), GTK+ 3 (experimental): [mate-gtk3](https://www.archlinux.org/groups/x86_64/mate-gtk3/)

*   **[Xfce](/index.php/Xfce "Xfce")** — Xfce encarna la filosofía tradicional UNIX de modularidad y la reutilización. Se compone de un número de elementos que proporcionan la funcionalidad completa que se puede esperar de un moderno entorno de escritorio, mientras permanece relativamente ligero. Los componentes se empaquetan por separado y se puede escoger entre los paquetes disponibles para crear el ambiente óptimo de trabajo personal.

[http://www.xfce.org/](http://www.xfce.org/) || [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/)

#### Sin soporte oficial

*   **Budgie Desktop** — Budgie Desktop es un entorno de escritorio liviano diseñado con el usuario moderno en mente, centrado en la simplicidad y elegancia. Se asemeja a la configuracion del entorno de Chrome/Chromium.

[https://solus-project.com/budgie/](https://solus-project.com/budgie/) || [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)<sup><small>AUR</small></sup>

*   **[CDE](/index.php/CDE "CDE")** — El "Common Desktop Environment" (CDE)es un entorno de escritorio para Unix y OpenVMS, basado en el set de herramientas widget de Motif. Era parte del UNIX98 "Workstation Product Standard", y fue por bastante tiempo el entorno unix "clásico" asociado a las estaciones de trabajo comercial de Unix.

[http://sourceforge.net/projects/cdesktopenv/](http://sourceforge.net/projects/cdesktopenv/) || [cdesktopenv](https://aur.archlinux.org/packages/cdesktopenv/)<sup><small>AUR</small></sup>

*   **[Deepin Desktop Environment](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment")** — El entorno de escritorio y aplicaciones "deepin", poseen un diseño elegante e intuitivo. Moverse, compartir buscar, etc. se convierte simplenente en una experiencia feliz.

[http://www.linuxdeepin.com/](http://www.linuxdeepin.com/) || [deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/deepin-desktop-environment)]</sup>

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — El «Entorno de Escritorio Equinox» es un escritorio diseñado para ser simple, extremadamente ligero y rápido.

[http://equinox-project.org/](http://equinox-project.org/) || [ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup>

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — GNOME Flashback es un shell para GNOME 3 que se llamó inicialmente la modalidad de GNOME fallback. El diseño del escritorio y la tecnología subyacente es similar a GNOME 2.

[https://wiki.gnome.org/GnomeFlashback](https://wiki.gnome.org/GnomeFlashback) || [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)

*   **GNUstep** — GNUstep es una entorno de desarrollo multiplataforma, orientado a objetos, que busca la sencillez y la elegancia .

[http://gnustep.org/](http://gnustep.org/) || [windowmaker](https://www.archlinux.org/packages/?name=windowmaker)

*   **Hawaii** — Hawaii es un entorno de escritorio ligero, completo y rápido que se basa en Qt 5, QtQuick y Wayland, y que está diseñado para ofrecer la mejor experiencia de usuario para el dispositivo en el que se está ejecutando.

[http://www.maui-project.org/](http://www.maui-project.org/) || [hawaii-meta-git](https://aur.archlinux.org/packages/hawaii-meta-git/)<sup><small>AUR</small></sup>

*   **[Lumina](/index.php/Lumina "Lumina")** — Lumina es un entorno de escritorio liviano, escrito en Qt 5 para FreeBSD, que utiliza Fluxbox como organizador de ventanas.

[http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/](http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/) || [lumina-desktop-git](https://aur.archlinux.org/packages/lumina-desktop-git/)<sup><small>AUR</small></sup>

*   **Maynard** — Maynard es un entorno de escritorio diseñado (pero no limitado) para la [Raspberry Pi (Español)](/index.php?title=Raspberry_Pi_(Espa%C3%B1ol)&action=edit&redlink=1 "Raspberry Pi (Español) (page does not exist)") que corre con [Wayland (Español)](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)").

[https://github.com/raspberrypi/maynard](https://github.com/raspberrypi/maynard) || [maynard-git](https://aur.archlinux.org/packages/maynard-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/maynard-git)]</sup>

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — Pantheon es el entorno de escritorio por defecto originalmente creado por la distribución elementary OS. Está escrito desde cero utilizando Vala y las herramientas GTK3\. En cuanto a la usabilidad y la apariencia, el escritorio tiene algunas similitudes con GNOME Shell y Mac OS X.

[http://elementaryos.org/](http://elementaryos.org/) || [pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/)<sup><small>AUR</small></sup>

*   **[ROX](/index.php/ROX "ROX")** — ROX es un escritorio rápido, fácil de usar, que hace un uso amplio de drag-and-drop. La interfaz gira en torno a la gestión de ficheros, siguiendo la tradicional vista UNIX de que "todo es un archivo" en lugar de tratar de ocultar el sistema de ficheros por debajo de menús de inicio, asistentes o druidas. El objetivo es hacer un sistema que está bien diseñado y presentado claramente. El estilo ROX favorece el uso conjunto de varios programas pequeños, en lugar de crear todo en una gran aplicación.

[http://roscidus.com/desktop/](http://roscidus.com/desktop/) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **[Sugar](/index.php/Sugar "Sugar")** — La Plataforma de Aprendizaje Sugar es un entorno informático integrado de actividades diseñadas para ayudar a los niños de 5 a 12 años de edad donde aprenden a interrelacionarse con la expresión de medios dinámicos. Sugar es el componente central de un esfuerzo mundial para proporcionar a cada niño la oportunidad de una educación de calidad -es utilizado actualmente por cerca de un millón de niños en todo el mundo que hablan 25 idiomas en más de 40 países-. Sugar proporciona los medios para ayudar a las personas a llevar una vida satisfactoria a través del acceso a una educación de calidad que está ausente para tantos.

[http://wiki.sugarlabs.org/](http://wiki.sugarlabs.org/) || [sugar](https://aur.archlinux.org/packages/sugar/)<sup><small>AUR</small></sup>

*   **[Trinity](/index.php/Trinity "Trinity")** — El proyecto Trinity Desktop Environment (TDE) es un entorno de escritorio de ordenador para sistemas operativos tipo Unix con el objetivo principal de mantener el estilo de KDE 3.5.

[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || See [Trinity](/index.php/Trinity "Trinity")

*   **[Unity](/index.php/Unity "Unity")** — Unity es una shell para GNOME diseñada por Canonical para Ubuntu.

[http://unity.ubuntu.com/](http://unity.ubuntu.com/) || [unity](https://aur.archlinux.org/packages/unity/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/unity)]</sup>

### Comparación de entornos de escritorio

_Esta sección trata de establecer una comparación entre los entornos de escritorio más populares. Tenga en cuenta que de primera mano la experiencia es la única manera efectiva de evaluar realmente si un entorno de escritorio se adapta mejor o no a sus necesidades._

Ver también [Wikipedia:es:Comparación de entornos de escritorios de X Window System](https://en.wikipedia.org/wiki/es:Comparaci%C3%B3n_de_entornos_de_escritorios_de_X_Window_System "wikipedia:es:Comparación de entornos de escritorios de X Window System")

<table class="wikitable"><caption>Visión general de entornos de escritorio</caption>

<tbody>

<tr>

<th>Entorno de escritorio</th>

<th>librerías de desarrollo</th>

<th>Gestor de ventanas</th>

<th>Barra de tareas</th>

<th>Emulador de Terminal</th>

<th>Gestor de Ficheros</th>

<th>Calculadora</th>

<th>Editor de texto</th>

<th>Visor de Imagen</th>

<th>Reproductor multimedia</th>

<th>Navegador web</th>

<th>Gestor de inicio</th>

</tr>

<tr>

<td>[Budgie Desktop](/index.php/Budgie_Desktop "Budgie Desktop")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>budgie-wm  
[budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)<sup><small>AUR</small></sup></td>

<td>budgie-panel  
[budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)<sup><small>AUR</small></sup></td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[Budgie Media Player](https://github.com/evolve-os/budgie-media-player)  
[budgie-git](https://aur.archlinux.org/packages/budgie-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/budgie-git)]</sup></td>

<td>[Chromium](/index.php/Chromium "Chromium")  
[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>[Cinnamon](/index.php/Cinnamon "Cinnamon")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>Muffin  
[muffin](https://www.archlinux.org/packages/?name=muffin)</td>

<td>Cinnamon  
[cinnamon](https://www.archlinux.org/packages/?name=cinnamon)</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[Nemo](/index.php/Nemo "Nemo")  
[nemo](https://www.archlinux.org/packages/?name=nemo)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>[Deepin Desktop Environment](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Compiz](/index.php/Compiz "Compiz")  
[compiz](https://aur.archlinux.org/packages/compiz/)<sup><small>AUR</small></sup></td>

<td>Dock  
[deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/deepin-desktop-environment)]</sup></td>

<td>Deepin Terminal  
[deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>DPlayer  
[deepin-media-player](https://aur.archlinux.org/packages/deepin-media-player/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/deepin-media-player)]</sup></td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LightDM](/index.php/LightDM "LightDM") Deepin Greeter  
[deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/deepin-desktop-environment)]</sup></td>

</tr>

<tr>

<td>[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")</td>

<td>[FLTK](http://www.fltk.org/)  
[fltk](https://www.archlinux.org/packages/?name=fltk)</td>

<td>[PekWM](/index.php/PekWM "PekWM")  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>EDE Panel  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>[XTerm](/index.php/Xterm "Xterm")  
[xterm](https://www.archlinux.org/packages/?name=xterm)</td>

<td>Fluff  
[fluff](https://aur.archlinux.org/packages/fluff/)<sup><small>AUR</small></sup></td>

<td>Calculator  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>Editor  
[fltk-editor](https://aur.archlinux.org/packages/fltk-editor/)<sup><small>AUR</small></sup></td>

<td>Image Viewer  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>flmusic  
[flmusic](https://aur.archlinux.org/packages/flmusic/)<sup><small>AUR</small></sup></td>

<td>[Dillo](/index.php/Dillo "Dillo")  
[dillo](https://www.archlinux.org/packages/?name=dillo)</td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[Enlightenment](/index.php/Enlightenment "Enlightenment")</td>

<td>[Elementary](https://www.enlightenment.org/about-efl)  
[elementary](https://www.archlinux.org/packages/?name=elementary)</td>

<td>Enlightenment  
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment)</td>

<td>Enlightenment  
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment)</td>

<td>[Terminology](https://www.enlightenment.org/about-terminology)  
[terminology](https://www.archlinux.org/packages/?name=terminology)</td>

<td>Enligthenment  
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment)</td>

<td>Equate  
[equate-git](https://aur.archlinux.org/packages/equate-git/)<sup><small>AUR</small></sup></td>

<td>Ecrire  
[ecrire-git](https://aur.archlinux.org/packages/ecrire-git/)<sup><small>AUR</small></sup></td>

<td>Ephoto  
[ephoto-git](https://aur.archlinux.org/packages/ephoto-git/)<sup><small>AUR</small></sup></td>

<td>[Rage](https://www.enlightenment.org/about-rage)  
[rage](https://aur.archlinux.org/packages/rage/)<sup><small>AUR</small></sup></td>

<td>Elbow  
[elbow-git](https://aur.archlinux.org/packages/elbow-git/)<sup><small>AUR</small></sup></td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[GNOME](/index.php/GNOME "GNOME")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")  
[mutter](https://www.archlinux.org/packages/?name=mutter)</td>

<td>[GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell "wikipedia:GNOME Shell")  
[gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell)</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Epiphany](/index.php/Epiphany "Epiphany")  
[epiphany](https://www.archlinux.org/packages/?name=epiphany)</td>

<td>[GDM](/index.php/GDM "GDM")  
[gdm](https://www.archlinux.org/packages/?name=gdm)</td>

</tr>

<tr>

<td>[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")  
[metacity](https://www.archlinux.org/packages/?name=metacity)</td>

<td>[GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")  
[gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Epiphany](/index.php/Epiphany "Epiphany")  
[epiphany](https://www.archlinux.org/packages/?name=epiphany)</td>

<td>[GDM](/index.php/GDM "GDM")  
[gdm](https://www.archlinux.org/packages/?name=gdm)</td>

</tr>

<tr>

<td>GNUstep</td>

<td>[GNUstep](http://gnustep.org/)  
[gnustep-core](https://www.archlinux.org/groups/x86_64/gnustep-core/)</td>

<td>[Window Maker](/index.php/Window_Maker "Window Maker")  
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker)</td>

<td>[Window Maker](/index.php/Window_Maker "Window Maker")  
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker)</td>

<td>[Terminal](http://gap.nongnu.org/terminal/index.html)  
[gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-terminal)]</sup></td>

<td>[GWorkspace](http://www.gnustep.org/experience/GWorkspace.html)  
[gworkspace](https://aur.archlinux.org/packages/gworkspace/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gworkspace)]</sup></td>

<td>[Calculator](http://www.gnustep.org/experience/examples.html)  
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-examples)]</sup></td>

<td>[Ink](http://www.gnustep.org/experience/examples.html)  
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-examples)]</sup></td>

<td>[LaternaMagica](http://gap.nongnu.org/laternamagica/index.html)  
[laternamagica](https://aur.archlinux.org/packages/laternamagica/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/laternamagica)]</sup></td>

<td>[Cynthiune](http://gap.nongnu.org/cynthiune/index.html)  
[cynthiune](https://aur.archlinux.org/packages/cynthiune/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cynthiune)]</sup></td>

<td>[SWK Browser](http://wiki.gnustep.org/index.php/SimpleWebKit)  
[swkbrowser-svn](https://aur.archlinux.org/packages/swkbrowser-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/swkbrowser-svn)]</sup></td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[Hawaii](/index.php/Hawaii "Hawaii")</td>

<td>[Qt](/index.php/Qt "Qt") 5  
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>Green Island  
[greenisland-git](https://aur.archlinux.org/packages/greenisland-git/)<sup><small>AUR</small></sup></td>

<td>Hawaii Shell  
[hawaii-shell-git](https://aur.archlinux.org/packages/hawaii-shell-git/)<sup><small>AUR</small></sup></td>

<td>Terminal  
[hawaii-terminal-git](https://aur.archlinux.org/packages/hawaii-terminal-git/)<sup><small>AUR</small></sup></td>

<td>Swordfish  
[swordfish-git](https://aur.archlinux.org/packages/swordfish-git/)<sup><small>AUR</small></sup></td>

<td>[SpeedCrunch](http://speedcrunch.org/)  
[speedcrunch-git](https://aur.archlinux.org/packages/speedcrunch-git/)<sup><small>AUR</small></sup></td>

<td>JuffEd  
[juffed-qt5-git](https://aur.archlinux.org/packages/juffed-qt5-git/)<sup><small>AUR</small></sup></td>

<td>EyeSight  
[eyesight-git](https://aur.archlinux.org/packages/eyesight-git/)<sup><small>AUR</small></sup></td>

<td>SMPlayer  
[smplayer](https://www.archlinux.org/packages/?name=smplayer)</td>

<td>QupZilla  
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla)</td>

<td>SDDM  
[sddm](https://www.archlinux.org/packages/?name=sddm)</td>

</tr>

<tr>

<td>[KDE](/index.php/KDE "KDE") 4</td>

<td>[Qt](/index.php/Qt "Qt") 4/5  
[qt4](https://www.archlinux.org/packages/?name=qt4) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")  
[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

<td>[Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_4#Desktop "wikipedia:KDE Plasma 4")  
[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

<td>[Konsole](http://konsole.kde.org/)  
[konsole](https://www.archlinux.org/packages/?name=konsole)</td>

<td>[Dolphin](http://dolphin.kde.org/)  
[kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [dolphin](https://www.archlinux.org/packages/?name=dolphin)]</sup></td>

<td>[KCalc](http://www.kde.org/applications/utilities/kcalc/)  
[kcalc](https://www.archlinux.org/packages/?name=kcalc)</td>

<td>[KWrite/Kate](http://kate-editor.org/)  
[kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate)</td>

<td>[Gwenview](http://gwenview.sourceforge.net/)  
[gwenview](https://www.archlinux.org/packages/?name=gwenview)</td>

<td>[Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)  
[kdemultimedia-dragonplayer](https://www.archlinux.org/packages/?name=kdemultimedia-dragonplayer)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [dragon](https://www.archlinux.org/packages/?name=dragon)]</sup></td>

<td>[Konqueror](http://www.konqueror.org/)  
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)</td>

<td>[KDM](/index.php/KDM "KDM")  
[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

</tr>

<tr>

<td>[KDE Plasma](/index.php/KDE "KDE") 5</td>

<td>[Qt](/index.php/Qt "Qt") 4/5  
[qt4](https://www.archlinux.org/packages/?name=qt4) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")  
[kwin](https://www.archlinux.org/packages/?name=kwin)</td>

<td>[Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_5#Desktop "wikipedia:KDE Plasma 5")  
[plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop)</td>

<td>[Konsole](http://konsole.kde.org/)  
[konsole](https://www.archlinux.org/packages/?name=konsole)</td>

<td>[Dolphin](http://dolphin.kde.org/)  
[kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [dolphin](https://www.archlinux.org/packages/?name=dolphin)]</sup></td>

<td>[KCalc](http://www.kde.org/applications/utilities/kcalc/)  
[kcalc](https://www.archlinux.org/packages/?name=kcalc)</td>

<td>[KWrite/Kate](http://kate-editor.org/)  
[kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate)</td>

<td>[Gwenview](http://gwenview.sourceforge.net/)  
[gwenview](https://www.archlinux.org/packages/?name=gwenview)</td>

<td>[Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)  
[kdemultimedia-dragonplayer](https://www.archlinux.org/packages/?name=kdemultimedia-dragonplayer)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [dragon](https://www.archlinux.org/packages/?name=dragon)]</sup></td>

<td>[Konqueror](http://www.konqueror.org/)  
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)</td>

<td>[SDDM](/index.php/SDDM "SDDM")  
[sddm](https://www.archlinux.org/packages/?name=sddm)</td>

</tr>

<tr>

<td>[LXDE](/index.php/LXDE "LXDE")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2  
[gtk2](https://www.archlinux.org/packages/?name=gtk2)</td>

<td>[Openbox](/index.php/Openbox "Openbox")  
[openbox](https://www.archlinux.org/packages/?name=openbox)</td>

<td>[LXPanel](http://wiki.lxde.org/en/LXPanel)  
[lxpanel](https://www.archlinux.org/packages/?name=lxpanel)</td>

<td>[LXTerminal](http://wiki.lxde.org/en/LXTerminal)  
[lxterminal](https://www.archlinux.org/packages/?name=lxterminal)</td>

<td>[PCManFM](/index.php/PCManFM "PCManFM")  
[pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>[Leafpad](http://tarot.freeshell.org/leafpad/)  
[leafpad](https://www.archlinux.org/packages/?name=leafpad)</td>

<td>[GPicView](http://wiki.lxde.org/en/GPicView)  
[gpicview](https://www.archlinux.org/packages/?name=gpicview)</td>

<td>[LXMusic](http://wiki.lxde.org/en/LXMusic)  
[lxmusic](https://www.archlinux.org/packages/?name=lxmusic)</td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LXDM](/index.php/LXDM "LXDM")  
[lxdm](https://www.archlinux.org/packages/?name=lxdm)</td>

</tr>

<tr>

<td>[LXQt](/index.php/LXQt "LXQt")</td>

<td>[Qt](/index.php/Qt "Qt") 5  
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>[Openbox](/index.php/Openbox "Openbox")  
[openbox](https://www.archlinux.org/packages/?name=openbox)</td>

<td>LXQt Panel  
[lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel)</td>

<td>QTerminal  
[qterminal](https://aur.archlinux.org/packages/qterminal/)<sup><small>AUR</small></sup></td>

<td>PCManFM-Qt  
[pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt)</td>

<td>[SpeedCrunch](http://speedcrunch.org/)  
[speedcrunch-git](https://aur.archlinux.org/packages/speedcrunch-git/)<sup><small>AUR</small></sup></td>

<td>JuffEd  
[juffed-qt5-git](https://aur.archlinux.org/packages/juffed-qt5-git/)<sup><small>AUR</small></sup></td>

<td>LxImage-Qt  
[lximage-qt](https://aur.archlinux.org/packages/lximage-qt/)<sup><small>AUR</small></sup></td>

<td>SMPlayer  
[smplayer](https://www.archlinux.org/packages/?name=smplayer)</td>

<td>QupZilla  
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla)</td>

<td>SDDM  
[sddm](https://www.archlinux.org/packages/?name=sddm)</td>

</tr>

<tr>

<td>[MATE](/index.php/MATE "MATE") (GTK+ 2)</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2/3  
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>Marco  
[marco](https://www.archlinux.org/packages/?name=marco)</td>

<td>MATE Panel  
[mate-panel](https://www.archlinux.org/packages/?name=mate-panel)</td>

<td>MATE Terminal  
[mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal)</td>

<td>Caja  
[caja](https://www.archlinux.org/packages/?name=caja)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>pluma  
[pluma](https://www.archlinux.org/packages/?name=pluma)</td>

<td>Eye of MATE  
[eom](https://www.archlinux.org/packages/?name=eom)</td>

<td>[Parole](http://docs.xfce.org/apps/parole/start)  
[parole](https://www.archlinux.org/packages/?name=parole)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori](https://www.archlinux.org/packages/?name=midori)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>[MATE](/index.php/MATE "MATE") (GTK+ 3)</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>Marco  
[marco-gtk3](https://www.archlinux.org/packages/?name=marco-gtk3)</td>

<td>MATE Panel  
[mate-panel-gtk3](https://www.archlinux.org/packages/?name=mate-panel-gtk3)</td>

<td>MATE Terminal  
[mate-terminal-gtk3](https://www.archlinux.org/packages/?name=mate-terminal-gtk3)</td>

<td>Caja  
[caja-gtk3](https://www.archlinux.org/packages/?name=caja-gtk3)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator](https://www.archlinux.org/packages/?name=galculator)</td>

<td>pluma  
[pluma-gtk3](https://www.archlinux.org/packages/?name=pluma-gtk3)</td>

<td>Eye of MATE  
[eom-gtk3](https://www.archlinux.org/packages/?name=eom-gtk3)</td>

<td>[Parole](http://docs.xfce.org/apps/parole/start)  
[parole](https://www.archlinux.org/packages/?name=parole)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori-gtk3](https://www.archlinux.org/packages/?name=midori-gtk3)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [midori](https://www.archlinux.org/packages/?name=midori)]</sup></td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>Maynard</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>Weston  
[weston](https://www.archlinux.org/packages/?name=weston)</td>

<td>Maynard  
[maynard-git](https://aur.archlinux.org/packages/maynard-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/maynard-git)]</sup></td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Epiphany](/index.php/Epiphany "Epiphany")  
[epiphany](https://www.archlinux.org/packages/?name=epiphany)</td>

<td>-</td>

</tr>

<tr>

<td>[Pantheon](/index.php/Pantheon "Pantheon")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Gala](https://launchpad.net/gala)  
[gala-bzr](https://aur.archlinux.org/packages/gala-bzr/)<sup><small>AUR</small></sup></td>

<td>[Plank](https://launchpad.net/plank)/[Wingpanel](https://launchpad.net/wingpanel)  
[plank](https://www.archlinux.org/packages/?name=plank) [wingpanel](https://aur.archlinux.org/packages/wingpanel/)<sup><small>AUR</small></sup></td>

<td>[Pantheon Terminal](https://launchpad.net/pantheon-terminal)  
[pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal)</td>

<td>[Pantheon Files](https://launchpad.net/pantheon-files)  
[pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[Scratch](https://launchpad.net/scratch)  
[scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor)</td>

<td>[Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")  
[shotwell](https://www.archlinux.org/packages/?name=shotwell)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori-gtk3](https://www.archlinux.org/packages/?name=midori-gtk3)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [midori](https://www.archlinux.org/packages/?name=midori)]</sup></td>

<td>[LightDM](/index.php/LightDM "LightDM") Pantheon Greeter  
[lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>[ROX](/index.php/ROX "ROX")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2  
[gtk2](https://www.archlinux.org/packages/?name=gtk2)</td>

<td>[OroboROX](http://rox.sourceforge.net/desktop/OroboROX.html)  
[oroborox](https://aur.archlinux.org/packages/oroborox/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/oroborox)]</sup></td>

<td>[ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)  
[rox](https://www.archlinux.org/packages/?name=rox)</td>

<td>[ROXTerm](http://roxterm.sourceforge.net/)  
[roxterm-gtk2](https://aur.archlinux.org/packages/roxterm-gtk2/)<sup><small>AUR</small></sup></td>

<td>[ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)  
[rox](https://www.archlinux.org/packages/?name=rox)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>[Edit](http://rox.sourceforge.net/desktop/Edit.html)  
[rox-edit](https://aur.archlinux.org/packages/rox-edit/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/rox-edit)]</sup></td>

<td>[Picky](http://rox.sourceforge.net/desktop/picky.html)  
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=picky)</small></td>

<td>[MusicBox](http://rox.sourceforge.net/desktop/Software/Audio_Video/MusicBox.html)  
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=musicbox)</small></td>

<td>[Midori](/index.php/Midori "Midori")  
[midori](https://www.archlinux.org/packages/?name=midori)</td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[Sugar](/index.php/Sugar "Sugar")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")  
[metacity](https://www.archlinux.org/packages/?name=metacity)</td>

<td>Sugar  
[sugar](https://aur.archlinux.org/packages/sugar/)<sup><small>AUR</small></sup></td>

<td>Terminal  
[sugar-activity-terminal](https://aur.archlinux.org/packages/sugar-activity-terminal/)<sup><small>AUR</small></sup></td>

<td>Sugar Journal  
[sugar](https://aur.archlinux.org/packages/sugar/)<sup><small>AUR</small></sup></td>

<td>Calculate  
[sugar-activity-calculate](https://aur.archlinux.org/packages/sugar-activity-calculate/)<sup><small>AUR</small></sup></td>

<td>Write  
[sugar-activity-write](https://aur.archlinux.org/packages/sugar-activity-write/)<sup><small>AUR</small></sup></td>

<td>ImageViewer  
[sugar-activity-imageviewer](https://aur.archlinux.org/packages/sugar-activity-imageviewer/)<sup><small>AUR</small></sup></td>

<td>Jukebox  
[sugar-activity-jukebox](https://aur.archlinux.org/packages/sugar-activity-jukebox/)<sup><small>AUR</small></sup></td>

<td>Browse  
[sugar-activity-browse](https://aur.archlinux.org/packages/sugar-activity-browse/)<sup><small>AUR</small></sup></td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>[Trinity](/index.php/Trinity "Trinity")</td>

<td>TQt</td>

<td>TWin</td>

<td>Kicker</td>

<td>Konsole</td>

<td>Konqueror</td>

<td>KCalc</td>

<td>Kwrite / Kate</td>

<td>Kuickshow</td>

<td>Kaffeine</td>

<td>Konqueror</td>

<td>TDM</td>

</tr>

<tr>

<td>[Unity](/index.php/Unity "Unity")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Compiz](/index.php/Compiz "Compiz")  
[compiz-ubuntu](https://aur.archlinux.org/packages/compiz-ubuntu/)<sup><small>AUR</small></sup></td>

<td>Unity  
[unity](https://aur.archlinux.org/packages/unity/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/unity)]</sup></td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus-ubuntu](https://aur.archlinux.org/packages/nautilus-ubuntu/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/nautilus-ubuntu)]</sup></td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LightDM](/index.php/LightDM "LightDM") Unity Greeter  
[lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>[Xfce](/index.php/Xfce "Xfce")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2/3  
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Xfwm4](http://docs.xfce.org/xfce/xfwm4/start)  
[xfwm4](https://www.archlinux.org/packages/?name=xfwm4)</td>

<td>[Xfce Panel](http://docs.xfce.org/xfce/xfce4-panel/start)  
[xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel)</td>

<td>[Terminal](http://www.xfce.org/projects/terminal)  
[xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)</td>

<td>[Thunar](/index.php/Thunar "Thunar")  
[thunar](https://www.archlinux.org/packages/?name=thunar)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator](https://www.archlinux.org/packages/?name=galculator)</td>

<td>Mousepad  
[mousepad](https://www.archlinux.org/packages/?name=mousepad)</td>

<td>[Ristretto](http://goodies.xfce.org/projects/applications/ristretto)  
[ristretto](https://www.archlinux.org/packages/?name=ristretto)</td>

<td>[Parole](http://docs.xfce.org/apps/parole/start)  
[parole](https://www.archlinux.org/packages/?name=parole)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori](https://www.archlinux.org/packages/?name=midori)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

</tbody>

</table>

#### Uso de los recursos

Con respecto a los recursos del sistema, GNOME y KDE son entornos de escritorio _pesados_ . No sólo las instalaciones completas consumen más espacio de disco que las alternativas más ligeras (E17, LXDE, Razor-qt y Xfce), sino también más recursos de CPU y de memoria mientras están en uso. Esto se debe a que GNOME y KDE son considerados _full-optional_ (es decir, con todas las funciones relativamente disponibles), esto es: proporcionan los ambientes más completos y bien integrados.

Enlightment, LXDE, LX-Qt y Xfce, por otro lado, son entornos de escritorios _ligeros_. Están diseñados para correr bien sobre hardware antiguo o consumir menos energía y generalmente consumen menos recursos del sistema mientras están en uso. Ésto se logra mediante la reducción de las funciones _extras_ (que podrían considerarse _superfluas_).

#### Entornos familiares

Muchos usuarios de KDE describen a éste como _más similar a Windows_ y a GNOME _como más similar a Mac_. Esta es una comparación muy subjetiva, ya que cualquiera de los entornos de escritorio puede ser personalizado para emular Windows o Mac. Consulte [¿Es KDE más parecido a Windows respecto a Gnome?](http://www.psychocats.net/ubuntucat/is-kde-more-windows-like-than-gnome/) y [KDE vs Gnome](http://www.jeffwu.net/?p=71) para más información. ([Linux no es Windows](http://linux.oneandoneis2.org/LNW.htm) es otra excelente consulta.)

## Entornos personalizados

Los entornos de escritorio representan el medio más sencillo de instalar una _completa_ interfaz gráfica. Sin embargo, cada cual es libre de crear y personalizar su propio entorno gráfico de muchas maneras, si ninguno de los entornos de escritorio más populares satisface sus necesidades. En general, la construcción de un entorno personalizado implica, al menos, la selección de un adecuado [gestor de ventanas](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)"), una [barra de tareas](https://en.wikipedia.org/wiki/es:Barra_de_tareas "wikipedia:es:Barra de tareas") y un número variable de [aplicaciones](/index.php/List_of_Applications_(Espa%C3%B1ol) "List of Applications (Español)") (una selección minimalista, por lo general incluye un [emulador de terminal](/index.php/List_of_applications#Terminal_emulators "List of applications"), [administrador de archivos](/index.php/List_of_applications#File_managers "List of applications"), y [editor de texto](/index.php/List_of_applications#Text_editors "List of applications")).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Desktop_environment_(Español)&oldid=411566](https://wiki.archlinux.org/index.php?title=Desktop_environment_(Español)&oldid=411566)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments (Español)](/index.php/Category:Desktop_environments_(Espa%C3%B1ol) "Category:Desktop environments (Español)")