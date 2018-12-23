**Estado de la traducción**
Este artículo es una traducción de [ASUS Zenbook UX391](/index.php/ASUS_Zenbook_UX391 "ASUS Zenbook UX391"), revisada por última vez el **2018-12-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=ASUS_Zenbook_UX391&diff=0&oldid=559860) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Corregir los fallos de la pantalla

Por defecto, aparecerán fallos en la pantalla en algún momento, pero aun así el sistema es completamente utilizable. Para solucionarlo, agregue `intel_idle.max_cstate=4` a sus opciones de arranque.

Para el [GRUB](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)"), puede editar `/etc/default/grub`, agregue `intel_idle.max_cstate=4` a `GRUB_CMDLINE_LINUX_DEFAULT` y actualize el grub con la nueva configuración.