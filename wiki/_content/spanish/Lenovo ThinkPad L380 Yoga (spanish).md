**Estado de la traducción**
Este artículo es una traducción de [Lenovo ThinkPad L380 Yoga](/index.php/Lenovo_ThinkPad_L380_Yoga "Lenovo ThinkPad L380 Yoga"), revisada por última vez el **2019-01-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_L380_Yoga&diff=0&oldid=562919) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Para asegurarse de que tiene esta versión, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) y ejecute:

```
# dmidecode -t system | grep Version

Version: ThinkPad L380 Yoga

```

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuración](#Configuración)
    *   [1.1 Tarjeta SD](#Tarjeta_SD)
    *   [1.2 Wacom](#Wacom)
*   [2 Características adicionales](#Características_adicionales)

## Configuración

### Tarjeta SD

Funciona sin necesidad de configuración, pero no olvide instalar [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils).

### Wacom

Funciona sin necesidad de configuración.

Véase [Tablet PC](/index.php/Tablet_PC "Tablet PC") para saber más sobre la configuración.

## Características adicionales

El paquete [thinkpad-yoga-scripts-git](https://aur.archlinux.org/packages/thinkpad-yoga-scripts-git/) no funciona bien, porque el fabricante del panel táctil y del trackpoint fue sustituido.

En cambio, [https://github.com/ffejery/thinkpad-l380-yoga-scripts](https://github.com/ffejery/thinkpad-l380-yoga-scripts) funciona en su lugar. Véase [makepkg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)") sobre cómo compilarlo. También existe un paquete AUR: [thinkpad-l380-yoga-scripts-git](https://aur.archlinux.org/packages/thinkpad-l380-yoga-scripts-git/).

Recuerde editar `/opt/thinkpad-l380-yoga-scripts/rotate/thinkpad-rotate.py` tal y como se indica en el archivo Léame, ya que probablemente querrá que la pantalla táctil y el lápiz giren junto con la pantalla.