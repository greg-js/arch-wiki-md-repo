**Estado de la traducción**
Este artículo es una traducción de [Dell Inspiron Mini 1018](/index.php/Dell_Inspiron_Mini_1018 "Dell Inspiron Mini 1018"), revisada por última vez el **2019-01-19**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dell_Inspiron_Mini_1018&diff=0&oldid=563922) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Peculiaridades](#Peculiaridades)
    *   [2.1 Pantalla negra durante el arranque](#Pantalla_negra_durante_el_arranque)
    *   [2.2 Algunas teclas no funcionan](#Algunas_teclas_no_funcionan)
    *   [2.3 No hay sonido](#No_hay_sonido)

## Instalación

Véase la [guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)"). Véase también [Dell 10v](/index.php/Dell_Mini_10v_(Espa%C3%B1ol) "Dell Mini 10v (Español)"), [Dell 1010](/index.php/Dell_Inspiron_Mini_1010 "Dell Inspiron Mini 1010"), [Dell 3531](/index.php/Dell_Inspiron_3531 "Dell Inspiron 3531") o artículos similares.

## Peculiaridades

### Pantalla negra durante el arranque

Pruebe a poner lo siguiente en [lista negra](/index.php/Kernel_module_(Espa%C3%B1ol)#Lista_negra "Kernel module (Español)") en `/etc/modprobe.d/` durante la etapa [chroot](/index.php/Installation_guide_(Espa%C3%B1ol)#Chroot "Installation guide (Español)") de la instalación

```
blacklist dell-laptop

```

### Algunas teclas no funcionan

Establezca la distribución del teclado a *Dell Laptops Precision M*

### No hay sonido

Ejecute

```
amixer -D pulse set Mute Playback

```