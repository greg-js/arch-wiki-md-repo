**Estado de la traducción**
Este artículo es una traducción de [Package group](/index.php/Package_group "Package group"), revisada por última vez el **2019-01-15**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Package_group&diff=0&oldid=563418) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Un **grupo de paquetes** es un conjunto de paquetes relacionados, definidos por el [empaquetador](/index.php/Packager_(Espa%C3%B1ol) "Packager (Español)"), que se pueden instalar o desinstalar simultáneamente usando el nombre del grupo como sustituto del nombre de cada paquete individual. Si bien un grupo no es un paquete, se puede instalar de manera similar a un paquete, véase [Pacman (Español)#Instalar grupos de paquetes](/index.php/Pacman_(Espa%C3%B1ol)#Instalar_grupos_de_paquetes "Pacman (Español)") y [PKGBUILD#groups](/index.php/PKGBUILD#groups "PKGBUILD").

## Contents

*   [1 Grupos](#Grupos)
    *   [1.1 base](#base)
    *   [1.2 base-devel](#base-devel)
*   [2 Diferencia con un meta paquete](#Diferencia_con_un_meta_paquete)
*   [3 Véase también](#Véase_también)

## Grupos

Los grupos de paquetes más importantes son:

### base

El grupo [base](https://www.archlinux.org/groups/x86_64/base/) contiene:

*   software esencial como el [kernel](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)"), [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)"), las [utilidades principales](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)") y [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   software no esencial como [dhcpcd](/index.php/Dhcpcd_(Espa%C3%B1ol) "Dhcpcd (Español)"), [netctl](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)"), [nano](/index.php/Nano_(Espa%C3%B1ol) "Nano (Español)") y [vi](/index.php/Vi "Vi").

### base-devel

El grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) contiene herramientas necesarias para construir paquetes como [GCC](/index.php/GCC_(Espa%C3%B1ol) "GCC (Español)") y [make](/index.php/GNU_make "GNU make"). Véase también [makepkg (Español)#Utilización](/index.php/Makepkg_(Espa%C3%B1ol)#Utilización "Makepkg (Español)").

## Diferencia con un meta paquete

Un *meta paquete*, a menudo (aunque no siempre) titulado con el sufijo "-meta", proporciona una funcionalidad similar a un grupo de paquetes en el sentido de que permite que varios paquetes relacionados se instalen o desinstalen simultáneamente. Los paquetes meta pueden instalarse como cualquier otro paquete (véase [Pacman (Español)#Instalar paquetes específicos](/index.php/Pacman_(Espa%C3%B1ol)#Instalar_paquetes_específicos "Pacman (Español)")). La única diferencia entre un meta paquete y un paquete regular es que un meta paquete está vacío y existe únicamente para vincular paquetes relacionados a través de dependencias.

La ventaja de un meta paquete, en comparación con un grupo, es que cualquier nuevo paquete miembro se instalará cuando el meta paquete se actualice con un nuevo conjunto de dependencias. Esto contrasta con un grupo donde los nuevos miembros del grupo no se instalarán automáticamente. La desventaja de un meta paquete es que no es tan flexible como un grupo; puede elegir qué miembros del grupo desea instalar pero no puede elegir qué dependencias de meta paquetes desea instalar. Del mismo modo, puede desinstalar miembros del grupo sin tener que eliminar todo el grupo. Sin embargo, no puede eliminar las dependencias de meta paquetes sin tener que desinstalar el meta paquete en sí.

## Véase también

*   [Listado de todos los grupos de paquetes](https://www.archlinux.org/groups/)
*   Ejemplos:
    *   [GNOME (Español)#Instalación](/index.php/GNOME_(Espa%C3%B1ol)#Instalación "GNOME (Español)")
    *   [KDE (Español)#Instalación](/index.php/KDE_(Espa%C3%B1ol)#Instalación "KDE (Español)")
    *   [i3#Installation](/index.php/I3#Installation "I3")