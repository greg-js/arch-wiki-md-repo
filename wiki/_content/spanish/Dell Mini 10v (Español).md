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

Como era de esperarse, asumimos que existe una instalación fresca de Arch Linux, la cual puede encontrarse en esta Wiki como [Beginners' Guide (Español)](/index.php/Beginners%27_Guide_(Espa%C3%B1ol) "Beginners' Guide (Español)"). Ya que este equipo no dispone de una unidad óptica para gestionar la instalacion, puede adaptar otros medios externos como una [Unidad Flash USB](https://wiki.archlinux.org/index.php/Install_from_a_USB_flash_drive_(Espa%C3%B1ol)) o un CD-ROM externo USB.

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

La configuración de este chip no suele dar problemas en Arch Linux, después de pasar por el apartado de la instalación de las _X_ en la [La Guía de Principiantes](https://wiki.archlinux.org/index.php/Beginners%27_Guide_(Espa%C3%B1ol)#Instalar_X), instale el driver correspondiente:

```
# pacman -S xf86-video-intel

```

### Audio

La tarjeta de sonido puede ser configurada fácilmente, siguendo los pasos que se enlistan en la [Sección de Instalación de ALSA](https://wiki.archlinux.org/index.php/Beginners%27_Guide_(Espa%C3%B1ol)#Sonido). Una vez hecho esto, y en cuanto el entorno gráfico arranque, asegúrese de ejecutar:

```
$ alsamixer

```

Utilizando las teclas de cursor, seleccione **PCM** y aumente el valor a 100, seguido de la tecla _Esc_. Para finalizar guarde la configuración anterior con el siguiente comando:

```
# alsactl store

```

### Tarjeta Inalámbrica

El dispositivo siguiente es el que demanda más tiempo, preparar la configuración correcta puede resultar confusa pues hay demasiada información referente al mismo procedimiento y no siémpre concuerda. Aquí presentamos un método bastante sencillo y claro. Como información general, este dispositivo es propiciado por Dell bajo el nombre _1397 WLAN 802.11g Half Mini-Card_. Es conveniente leer el artículo relacionado a la [Configuración Wifi](https://wiki.archlinux.org/index.php/Wireless_Setup_(Espa%C3%B1ol)), para después continuar con las siguientes líneas.

El driver necesario se encuentra en [AUR](https://aur.archlinux.org/packages.php?ID=21690) y requerimos tener instalado [Yaourt](https://wiki.archlinux.org/index.php/Yaourt_(Espa%C3%B1ol)). Asegúrese de contar con un kernel mayor a 2.6.33, ya que en versiones anteriores presenta conflictos con dicho driver. Puede comprobar esto con un simple:

```
$ uname -r

```

Proseguimos con la instalación del driver desde el repositorio de usuarios con el siguiente comando:

```
$ yaourt -S b43-firmware

```

Con esto descargamos e instalamos el driver desde la página de [Broadcom](http://www.broadcom.com/support/802.11/linux_sta.php).

**Tip:** Cuando use _yaourt_, evite hacerlo como **root** o superusuario. Siempre es una mala idea.

Ahora cargaremos los módulos correspondientes para el correcto funcionamiento de nuestra tarjeta, para esto abrimos el archivo _/etc/rc.local_ con el editor de su elección, por ejemplo [Nano](/index.php/Nano "Nano"):

```
# nano /etc/rc.local

```

Agregamos la siguiente línea al final del archivo:

```
sudo modprobe b43 pio=1 qos=0

```

Guardamos los cambios presionando las teclas **Ctrl + O** y para salir del editor con **Ctrl + X**. Ahora sólo resta reiniciar el equipo y al próximo inicio notaremos que nuestro gestor de redes detectará un nuevo dispositivo de red para administrar.

### Webcam

Este dispositivo queda configurado al [Instalar las X](https://wiki.archlinux.org/index.php/Beginners%27_Guide_(Espa%C3%B1ol)#Instalar_X), sólo necesitamos **Cheese**, el cual gestionará nuestra Webcam. Si eligió [GNOME](https://wiki.archlinux.org/index.php/GNOME_(Espa%C3%B1ol)) como entorno de escritorio puede encontrarlo en el menú Aplicaciones > Sonido y Vídeo > Cheese. En cualquier caso puede instalarlo con:

```
# pacman -S cheese

```

## Extras

### Synaptics

Para el funcionamiento básico del touchpad requerimos instalar el [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"), el paquete correcto para nuestro caso es el siguiente:

```
# pacman -S pacman -S xf86-input-synaptics

```

Notaremos que el _Scroll_ y el _Tapping_ no funciona, esto requiere la edición del archivo _/etc/X11/xorg.conf.d/10-synaptics.conf_. A partir de la línea 8 justo debajo del Tapbutton3, agregue las siguientes líneas respetando la indentación:

```
Option "JumpyCursorThreshold" "90"
Option "AreaBottomEdge" "4100"

```