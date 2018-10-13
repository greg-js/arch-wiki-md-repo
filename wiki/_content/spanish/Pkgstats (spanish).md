**Estado de la traducción**
Este artículo es una traducción de [Pkgstats](/index.php/Pkgstats "Pkgstats"), revisada por última vez el **2015-04-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Pkgstats&diff=0&oldid=511582) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

pkgstatus envía un listado de todos los paquetes instalados, [kernel modules](https://www.archlinux.org/news/pkgstats-now-collects-modules-usage/), la arquitectura y el mirror que está utilizando para el proyecto Arch Linux. Esta información es anónima y no puede ser utilizada para identificar al usuario, sinó que ayudará a los desarrolladores de Arch priorizar sus esfuerzos.

## Instalación

[Instalar](/index.php/Install "Install") el paquete [pkgstats](https://www.archlinux.org/packages/?name=pkgstats).

## Utilización

*pkgstats* está configurado para ejecutarse automáticamente cada semana usando [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). Una vez instalado, se activa después del siguiente reinicio.

Si no desea esperar al ciclo de reinicio, puede hacerlo manualmente [start](/index.php/Start "Start") `pkgstats.timer`.

*pkgstats* También se pueden ejecutar de forma manual: ver `pkgstats -h` para información sobre su uso.

## Resultados y referencia

Las estadísticas se encuentran disponibles [aquí](https://www.archlinux.de/?page=Statistics).

El siguiente proyecto de código abierto le permite obtener los datos estadísticos como JSON: [ArchLinuxPkgStatsScraper](https://github.com/chrissound/ArchLinuxPkgStatsScraper), así como una interfaz web para comparar los datos disponible: [https://trycatchchris.co.uk/archpackagecompare/](https://trycatchchris.co.uk/archpackagecompare/comparePackage/gnome-terminal/lxterminal/rxvt/rxvt-unicode/st/terminator/termite/xterm). Puede leer el [hilo del foro](https://bbs.archlinux.org/viewtopic.php?id=105431) oficial para obtener más información.