**Estado de la traducción**
Este artículo es una traducción de [Autostarting](/index.php/Autostarting "Autostarting"), revisada por última vez el **2018-09-28**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Autostarting&diff=0&oldid=539671) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Demonios](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)")

Este artículo se enlaza con varios métodos para iniciar scripts o aplicaciones automáticamente cuando se está produciendo algún evento en particular.

## Contents

*   [1 En el arranque / apagado](#En_el_arranque_/_apagado)
*   [2 En el inicio / fin de sesión](#En_el_inicio_/_fin_de_sesión)
*   [3 Al enchufar / desenchufar un dispositivo](#Al_enchufar_/_desenchufar_un_dispositivo)
*   [4 En eventos temporales](#En_eventos_temporales)
*   [5 En eventos de sistemas de archivos](#En_eventos_de_sistemas_de_archivos)
*   [6 En el inicio / fin del intérprete de comandos](#En_el_inicio_/_fin_del_intérprete_de_comandos)
*   [7 En el inicio de Xorg](#En_el_inicio_de_Xorg)
*   [8 En el inicio del entorno de escritorio](#En_el_inicio_del_entorno_de_escritorio)
*   [9 En el inicio del gestor de ventanas](#En_el_inicio_del_gestor_de_ventanas)

## En el arranque / apagado

Utilice los servicios [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

## En el inicio / fin de sesión

Utilice los servicios [systemd/User](/index.php/Systemd/User_(Espa%C3%B1ol) "Systemd/User (Español)").

## Al enchufar / desenchufar un dispositivo

Utilice las reglas [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)").

## En eventos temporales

Periódicamente a determinadas horas, fechas o intervalos:

*   [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")
*   [Cron](/index.php/Cron "Cron")

Una vez en una fecha y hora:

*   [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")
*   [at](https://www.archlinux.org/packages/?name=at)

## En eventos de sistemas de archivos

Utilice un observador de eventor [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify"):

*   [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools), véase [inotifywait(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/inotifywait.1)
*   [Incron](/index.php/Incron "Incron")
*   [fswatch](https://aur.archlinux.org/packages/fswatch/)

## En el inicio / fin del intérprete de comandos

Véase [Command-line shell (Español)#Archivos de configuración](/index.php/Command-line_shell_(Espa%C3%B1ol)#Archivos_de_configuración "Command-line shell (Español)").

## En el inicio de Xorg

*   [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") si está iniciando [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") manualmente con [xinit](/index.php/Xinit_(Espa%C3%B1ol) "Xinit (Español)").
*   [xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)") si está usando un [gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)").

## En el inicio del entorno de escritorio

Muchos [entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") implementan [XDG Autostart](/index.php/XDG_Autostart_(Espa%C3%B1ol) "XDG Autostart (Español)").

Si los entornos de escritorio tienen un artículo, véase su sección *Inicio automático*.

*   [GNOME (Español)#Inicio automático](/index.php/GNOME_(Espa%C3%B1ol)#Inicio_automático "GNOME (Español)")
*   [KDE#Autostart](/index.php/KDE#Autostart "KDE")
*   [Xfce#Autostart](/index.php/Xfce#Autostart "Xfce")
*   [LXDE#Autostart](/index.php/LXDE#Autostart "LXDE")
*   [LXQt#Autostart](/index.php/LXQt#Autostart "LXQt")

## En el inicio del gestor de ventanas

Si el [gestor de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") tiene un artículo, véase su sección *Inicio automático*.

*   [Fluxbox#Autostart](/index.php/Fluxbox#Autostart "Fluxbox")
*   [Openbox#Autostart](/index.php/Openbox#Autostart "Openbox")
*   [Awesome#Autostart](/index.php/Awesome#Autostart "Awesome")