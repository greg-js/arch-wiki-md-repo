**Estado de la traducción**
Este artículo es una traducción de [Toshiba Chromebook 2](/index.php/Toshiba_Chromebook_2 "Toshiba Chromebook 2"), revisada por última vez el **2018-12-23**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Toshiba_Chromebook_2&diff=0&oldid=560114) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Chromebook](/index.php/Chromebook "Chromebook")

**Advertencia:** Este artículo se basa en scripts y modificaciones de terceros, y puede dañar irreparablemente su hardware o sus datos. Proceda bajo su propia responsabilidad.

Para instalar Arch Linux en este modelo de Chromebook, debe ejecutar estas órdenes para instalar un stub de arranque Seabios:

```
$ cd; rm -f flash_chromebook_rom.sh; curl -k -L -O [https://johnlewis.ie/flash_chromebook_rom.sh](https://johnlewis.ie/flash_chromebook_rom.sh); sudo -E bash flash_chromebook_rom.sh

```

Para un tiempo de arranque más rápido, puede utilizar un gestor de arranque UEFI ([coreboot](https://www.coreboot.org/)), e incluso eliminar todos los componentes de Google.

A partir de aquí, puede seguir la [Guía para principiantes](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") para instalar Arch Linux.

## Problemas conocidos

*   El soporte para la distribución del teclado se puede encontrar en el paquete [xkeyboard-config-chromebook](https://aur.archlinux.org/packages/xkeyboard-config-chromebook/)

## Véase también

*   [https://www.reddit.com/r/chrultrabook/](https://www.reddit.com/r/chrultrabook/)
*   [https://johnlewis.ie/custom-chromebook-firmware/rom-download/](https://johnlewis.ie/custom-chromebook-firmware/rom-download/)
*   [https://cateee.net/lkddb/web-lkddb/SND_SOC_INTEL_BYT_MAX98090_MACH.html](https://cateee.net/lkddb/web-lkddb/SND_SOC_INTEL_BYT_MAX98090_MACH.html)
*   [https://lkml.org/lkml/2016/8/12/180](https://lkml.org/lkml/2016/8/12/180)