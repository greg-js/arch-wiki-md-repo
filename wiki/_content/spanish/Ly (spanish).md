**Estado de la traducción**
Este artículo es una traducción de [Ly](/index.php/Ly "Ly"), revisada por última vez el **2019-02-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Ly&diff=0&oldid=566610) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Ly](https://github.com/cylgom/ly) es un [gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") experimental que utiliza ncurses.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [ly-git](https://aur.archlinux.org/packages/ly-git/).

## Configuración

Toda la configuración se da en `/etc/ly/config.ini`. El archivo contiene comentarios, e incluye valores predeterminados de utilidad.

## Utilización

1.  [Desactive](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") otros gestores de pantalla.
2.  [Active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `ly.service`.
3.  [Desactive](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `getty@tty2.service`: getty en el tty utilizado por *Ly* (tty2 por defecto), para evitar que el *inicio de sesión* se genere encima de él.