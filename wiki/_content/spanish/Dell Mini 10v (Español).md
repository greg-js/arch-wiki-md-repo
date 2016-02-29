## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Hardware](#Hardware)
    *   [2.1 Video](#Video)
    *   [2.2 Audio](#Audio)
    *   [2.3 Tarjeta Inalámbrica](#Tarjeta_Inal.C3.A1mbrica)
    *   [2.4 Webcam](#Webcam)
*   [3 Extras](#Extras)
    *   [3.1 Synaptics](#Synaptics)

## Introducción

Este artículo pretende ofrecer al usuario una guía básica de configuración para una netbook Dell Inspiron mini 10v. El hardware de estos equipos varía, así que nos enfocaremos en un modelo: el PRN 6326, también conocida como [Mini 10v](http://www.dell.com/us/dfh/p/inspiron-mini10/pd?cs=22) y pertenece a la serie 1010.

Como era de esperarse, asumimos que existe una instalación fresca de Arch Linux, la cual puede encontrarse en esta Wiki como [Beginners' guide (Español)](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)"). Ya que este equipo no dispone de una unidad óptica para gestionar la instalacion, puede adaptar otros medios externos como una [Unidad Flash USB](/index.php/Install_from_a_USB_flash_drive_(Espa%C3%B1ol) "Install from a USB flash drive (Español)") o un CD-ROM externo USB.

## Hardware

Comenzamos detectando el hardware del equipo mediante:

```
$ lspci && lsusb

```

Nos centraremos en los dispositivos siguientes:

*   **Video**

	Intel Corporation Mobile 945GME

*   **Audio**

	Intel Corporation 82801 Mobile

*   **Tarjeta Inalámbrica**

	Broadcom BCM4312 802.11b/g LP-PHY

*   **Webcam**

	Suyin Corp.

### Video

La configuración de este chip no suele dar problemas en Arch Linux, después de pasar por el apartado de la instalación de las *X* en la [La Guía de Principiantes](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Instalar_X "Beginners' guide (Español)"), instale el driver correspondiente:

```
# pacman -S xf86-video-intel

```

### Audio

La tarjeta de sonido puede ser configurada fácilmente, siguendo los pasos que se enlistan en la [Sección de Instalación de ALSA](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Sonido "Beginners' guide (Español)"). Una vez hecho esto, y en cuanto el entorno gráfico arranque, asegúrese de ejecutar:

```
$ alsamixer

```

Utilizando las teclas de cursor, seleccione **PCM** y aumente el valor a 100, seguido de la tecla *Esc*. Para finalizar guarde la configuración anterior con el siguiente comando:

```
# alsactl store

```

### Tarjeta Inalámbrica

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless")

### Webcam

Este dispositivo queda configurado al [Instalar las X](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Instalar_X "Beginners' guide (Español)"), sólo necesitamos **Cheese**, el cual gestionará nuestra Webcam. Si eligió [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") como entorno de escritorio puede encontrarlo en el menú Aplicaciones > Sonido y Vídeo > Cheese. En cualquier caso puede instalarlo con:

```
# pacman -S cheese

```

## Extras

### Synaptics

Para el funcionamiento básico del touchpad requerimos instalar el [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"), el paquete correcto para nuestro caso es el siguiente:

```
# pacman -S pacman -S xf86-input-synaptics

```

Notaremos que el *Scroll* y el *Tapping* no funciona, esto requiere la edición del archivo */etc/X11/xorg.conf.d/10-synaptics.conf*. A partir de la línea 8 justo debajo del Tapbutton3, agregue las siguientes líneas respetando la indentación:

```
Option "JumpyCursorThreshold" "90"
Option "AreaBottomEdge" "4100"

```