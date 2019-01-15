**Estado de la traducción**
Este artículo es una traducción de [Sony Vaio SVF15216](/index.php/Sony_Vaio_SVF15216 "Sony Vaio SVF15216"), revisada por última vez el **2019-01-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Sony_Vaio_SVF15216&diff=0&oldid=563120) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este artículo describe algunos consejos de instalación de ArchLinux en el portátil Sony VAIO SVF15216.

## Wifi

El portátil cuenta con la tarjeta de red BCM43142 y es un poco problemática en algunas distros, pero no en el caso de Arch x86_64 (si se instala el paquete correcto). Puede utilizar el BCM43142 instalando el paquete [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms). También hay un PKGBUILD disponible en el [AUR](https://aur.archlinux.org/packages/broadcom-wl-dkms/) 

## Velocidad del ventilador

Puede controlar la velocidad del ventilador utilizando el daemon **vaiofand**, que se puede encontrar en el siguiente [enlace](https://vaio-utils.org/fan/). También hay un PKGBUILD disponible en el [AUR](https://aur.archlinux.org/packages.php?ID=38826).

## Ahorro de energía

Puede desactivar automáticamente algunos dispositivos como el bluetooth, el puerto firewire, la unidad de CD/DVD o la tarjeta de sonido utilizando el daemon [vaiopower](https://aur.archlinux.org/packages/vaiopower/) que se puede encontrar en el siguiente [enlace](https://vaio-utils.org/power/).