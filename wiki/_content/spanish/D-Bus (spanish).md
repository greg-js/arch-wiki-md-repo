**Estado de la traducción**
Este artículo es una traducción de [D-Bus](/index.php/D-Bus "D-Bus"), revisada por última vez el **2019-02-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=D-Bus&diff=0&oldid=565460) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[D-Bus](https://en.wikipedia.org/wiki/es:D-Bus "wikipedia:es:D-Bus") es un sistema de mensajes de bus que proporciona un método sencillo para la comunicación entre procesos. Consta de un daemon, que puede ejecutarse tanto para todo el sistema como para cada sesión de usuario, y un conjunto de librerías para permitir que las aplicaciones usen D-Bus.

El paquete [dbus](https://www.archlinux.org/packages/?name=dbus) se extrae e instala como una dependencia de [systemd](https://www.archlinux.org/packages/?name=systemd) y el bus de sesión del usuario se [inicia automáticamente](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) para cada usuario.

## Depuración

*   **D-Feet** — Herramienta de depuración D-Bus con interfaz gráfica fácil de utilizar. D-Feet se puede usar para inspeccionar las interfaces D-Bus de los programas en ejecución e invocar métodos en esas interfaces.

	[https://wiki.gnome.org/Apps/DFeet](https://wiki.gnome.org/Apps/DFeet) || [d-feet](https://www.archlinux.org/packages/?name=d-feet)

*   **QDbusViewer** — Depurador D-Bus con interfaz gráfica. Puede utilizarse para inspeccionar servicios de D-Bus e invocar métodos en ellos.

	[https://doc.qt.io/qt-5/qdbusviewer.html](https://doc.qt.io/qt-5/qdbusviewer.html) || [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools)

## Véase también

*   [Página web de D-Bus](https://www.freedesktop.org/wiki/Software/dbus/) - freedesktop.org
*   [Introducción a D-Bus](https://www.freedesktop.org/wiki/IntroductionToDBus/) - freedesktop.org