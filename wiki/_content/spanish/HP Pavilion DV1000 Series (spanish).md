**Estado de la traducción**
Este artículo es una traducción de [HP Pavilion DV1000 Series](/index.php/HP_Pavilion_DV1000_Series "HP Pavilion DV1000 Series"), revisada por última vez el **2019-01-16**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=HP_Pavilion_DV1000_Series&diff=0&oldid=328639) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

En esta página, trataré de hacer que la instalación de Arch en su HP Pavillion serie dv1000 sea lo más sencilla que pueda. Si tiene algo que añadir, contribuya con esta página por favor.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 ¿Qué funciona?](#¿Qué_funciona?)
*   [2 ¿Qué es lo que no funciona?](#¿Qué_es_lo_que_no_funciona?)
*   [3 Instalación](#Instalación)
*   [4 Configuración](#Configuración)
    *   [4.1 Xorg y la tarjeta gráfica](#Xorg_y_la_tarjeta_gráfica)
*   [5 Módulos](#Módulos)
    *   [5.1 Conexión inalámbrica](#Conexión_inalámbrica)
    *   [5.2 Sonido](#Sonido)
*   [6 Enlaces externos](#Enlaces_externos)

## ¿Qué funciona?

La conexión Wifi utilizando los controladores ipw2200

El control táctil utilizando los controladores synaptics

El control remoto, cuando tenga sus teclas multimedia funcionando, funciona desde el primer momento.

Suspensión a ram/swap

## ¿Qué es lo que no funciona?

# Instalación

Arranque con el CD de Arch sin ninguna opción, no necesita acpi=off para este portátil. Particione a su gusto pero reserve algo más de 204MB de espacio libre en el disco **que no pertenezca a ninguna partición** para instalar más tarde Quickplay. Puede que tenga que seguir alguna guía de instalación de la wiki.

# Configuración

## Xorg y la tarjeta gráfica

Véase [Gráficas Intel](/index.php/Intel_graphics_(Espa%C3%B1ol) "Intel graphics (Español)").

# Módulos

## Conexión inalámbrica

Tiene que itilizar el controlador `ipw2200`; el kernel por defecto de Arch lo tiene activado, pero aún necesita el paquete de firmware [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw).

## Sonido

El sonido debería funcionar desde el primer momento.

# Enlaces externos

*   [Una guía de compatibilidad en Linux del HP Pavillion serie DV1000](http://www.linlap.com/wiki/HP+Pavilion+dv1000)
*   Este informe aparece listado en la [Linux Laptop and Notebook Installation Guides Survey: Hewlett-Packard - HP](http://tuxmobil.org/hp.html).