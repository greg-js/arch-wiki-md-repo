**Estado de la traducción**
Este artículo es una traducción de [Acer Aspire 2930](/index.php/Acer_Aspire_2930 "Acer Aspire 2930"), revisada por última vez el **2018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Acer_Aspire_2930&diff=0&oldid=553269) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Contents

*   [1 Hardware](#Hardware)
*   [2 Ethernet](#Ethernet)
*   [3 Conexión inalámbrica](#Conexión_inalámbrica)
*   [4 Xorg](#Xorg)
*   [5 Sonido](#Sonido)
*   [6 Lector de tarjetas](#Lector_de_tarjetas)
*   [7 Webcam](#Webcam)
*   [8 ACPI](#ACPI)
*   [9 Panel táctil](#Panel_táctil)

## Hardware

**Procesador:** Intel Core 2 Duo T5800 *Esto puede variar según el modelo exacto*

**Vídeo:** Intel Corporation GM45 Chipset

**Audio:** Intel Coporation 82801I HD Audio Controller

**TIR cableada:** Realtek RTL8111/8168B

**TIR inalámbrica:** Intel Corporation Wireless Wifi Link 5100

## Ethernet

Debería funcionar sin necesidad de configuración.

## Conexión inalámbrica

Véase [Configuración de red inalámbrica#iwlwifi](/index.php/Wireless_network_configuration_(Espa%C3%B1ol)#iwlwifi "Wireless network configuration (Español)").

## Xorg

Véase [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") e [Intel graphics](/index.php/Intel_graphics_(Espa%C3%B1ol) "Intel graphics (Español)").

## Sonido

[PulseAudio](/index.php/PulseAudio_(Espa%C3%B1ol) "PulseAudio (Español)") me hizo un trabajo admirable al conseguir que el sonido funcionase.

Los altavoces externos funcionarán después de la configuración. Sin embargo, las tomas de auriculares y micrófono necesitan un arreglo adicional

 `/etc/modprobe.d/modprobe.conf`  `options snd-hda-intel model=acer position_fix=1 enable=yes` 

## Lector de tarjetas

Parecía funcionar sin necesidad de configuración adicional.

## Webcam

Funcionó sin ninguna configuración adicional.

## ACPI

Funcionó sin ninguna configuración adicional.

## Panel táctil

Funciona después de que se instala [synaptics](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol) "Touchpad Synaptics (Español)"). Para los toques táctiles, siga las instrucciones de configuración copiando /usr/share/X11/xorg.conf.d/50-synaptics.conf a /etc/X11/xorg.conf.d/