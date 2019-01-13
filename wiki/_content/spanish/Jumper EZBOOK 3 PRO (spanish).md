**Estado de la traducción**
Este artículo es una traducción de [Jumper EZBOOK 3 PRO](/index.php/Jumper_EZBOOK_3_PRO "Jumper EZBOOK 3 PRO"), revisada por última vez el **2019-01-11**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Jumper_EZBOOK_3_PRO&diff=0&oldid=562736) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

El Jumper EZBOOK 3 PRO es un notebook fabricado en China equipado con una pantalla FHD IPS de 13.3 pulgadas, un procesador Intel Apollo Lake N3450, 6GB de RAM DDR3, 64GB de almacenamiento eMMC, 802.11b/g/n/ac dual band wireless Internet (Intel Corporation Wireless 3165).

## Compatibilidad de hardware

El notebook puede ejecutar la versión x86_64 de Archlinux; casi todo funciona sin necesidad de configuración con el kernel común de Archlinux.

Instale [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) para una mejor compatibilidad del panel táctil.

El wifi, los altavoces, la webcam, la batería/gestión de energía funcionan sin necesidad de configuración.

La instalación se puede hacer como de costumbre en un sistema uefi x86_64.

## Problemas

*   El puerto HDMI funciona pero no es compatible con la salida de audio, parece ser un problema común de los dispositivos Intel con Linux en este momento.
*   No cambie la configuración del sistema operativo en la BIOS de Windows a Linux. Esto hace que el teclado integrado deje de funcionar durante el arranque (aunque los teclados USB todavía funcionan) e invierte los controles de retroiluminación.