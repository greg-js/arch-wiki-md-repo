**Estado de la traducción**
Este artículo es una traducción de [Lenovo ThinkPad T450](/index.php/Lenovo_ThinkPad_T450 "Lenovo ThinkPad T450"), revisada por última vez el **2019-01-20**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T450&diff=0&oldid=564084) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este artículo cubre los detalles relacionados con la instalación y configuración de Arch en el portátil Lenovo Thinkpad T450.

## Instalación

Soporta ambos estilos de BIOS: UEFI y MBR. No hay problemas conocidos con el proceso de instalación de Arch Linux con la última versión disponible en [Archiso](https://www.archlinux.org/download/). El proceso de instalación es el mismo que el de la [guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)"), exceptuando el apartado de sonido.

Véase el artículo de [Lenovo ThinkPad T450s](/index.php/Lenovo_ThinkPad_T450s "Lenovo ThinkPad T450s"), ya que casi todo lo que ahí se explica funciona para este portátil.

### Sonido

Asegúrese de instalar [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) o de que esté instalado.

Véase [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA") para establecer la tarjeta de sonido predeterminada a Intel PCH (los altavoces y auriculares).

 `/etc/modprobe.d/thinkpad-t450s.conf`  `options snd_hda_intel index=1,0` 

asegúrese de reiniciar el equipo después de aplicar los cambios.

### Reasignar las teclas Enter y Retroceso

Véase [Lenovo ThinkPad T420#Rebind Forward and Back keys](/index.php/Lenovo_ThinkPad_T420#Rebind_Forward_and_Back_keys "Lenovo ThinkPad T420")