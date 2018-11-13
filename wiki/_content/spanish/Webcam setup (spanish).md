Esto es una guía para configurar su webcam en Arch Linux.

## Contents

*   [1 Soporte para webcams en Linux](#Soporte_para_webcams_en_Linux)
*   [2 Identificar su webcam](#Identificar_su_webcam)
    *   [2.1 pwc](#pwc)
    *   [2.2 qc-usb](#qc-usb)
    *   [2.3 qc-usb-messenger](#qc-usb-messenger)
    *   [2.4 zr364xx](#zr364xx)
    *   [2.5 sn9c102](#sn9c102)
    *   [2.6 gspca](#gspca)
    *   [2.7 stv680](#stv680)
    *   [2.8 linux-uvc](#linux-uvc)
    *   [2.9 ov51x-jpeg](#ov51x-jpeg)
    *   [2.10 r5u870 (Ricoh)](#r5u870_(Ricoh))
    *   [2.11 stk11xx (Syntek)](#stk11xx_(Syntek))
*   [3 Asegúrese de que el modulo para su webcam está cargado](#Asegúrese_de_que_el_modulo_para_su_webcam_está_cargado)
*   [4 Permisos](#Permisos)
*   [5 Configuración de la webcam](#Configuración_de_la_webcam)
*   [6 Consiga que el software use su webcam](#Consiga_que_el_software_use_su_webcam)
    *   [6.1 Cheese](#Cheese)
    *   [6.2 fswebcam](#fswebcam)
    *   [6.3 GTK+ UVC Viewer (guvcview)](#GTK+_UVC_Viewer_(guvcview))
    *   [6.4 Kopete](#Kopete)
    *   [6.5 Kamoso](#Kamoso)
    *   [6.6 xawtv](#xawtv)
    *   [6.7 VLC](#VLC)
    *   [6.8 MPlayer](#MPlayer)
    *   [6.9 FFmpeg](#FFmpeg)
    *   [6.10 ekiga](#ekiga)
    *   [6.11 Sonic-snap](#Sonic-snap)
    *   [6.12 Skype](#Skype)
    *   [6.13 Motion](#Motion)
*   [7 Solución de problemas](#Solución_de_problemas)
    *   [7.1 Microsoft Lifecam Studio/Cinema](#Microsoft_Lifecam_Studio/Cinema)

## Soporte para webcams en Linux

Muy probablemente, su webcam funcione sin necesidad de configuraciones previas. Si este es su caso, puede ir directamente a la sección [#Configuración de la webcam](#Configuración_de_la_webcam) si desea ajustar el color, el brillo y otros parámetros. En caso contrario, siga los siguientes pasos.

## Identificar su webcam

Identifique el nombre de su webcam (usando, por ejemplo, `lsusb`) y busque un controlador apropiado. A continuación se listan algunas webcams, junto con el controlador apropiado. Si consigue poner a funcionar su webcam, ¡Añada el nombre de la webcam junto con el controlador a la lista!

### pwc

*   Creative Labs Webcam Pro Ex
*   Logitech QuickCam Notebook Pro (Solo los modelos "Pro")
*   Logitech Quickcam Pro 4000
*   Philips ToUCams (Sin confirmar por lo pronto, pero usa el controlador pwc si no recuerdo mal)
*   Philips SPC900NC

### qc-usb

*   Dexxa Webcam
*   Labtec Webcam (modelo antiguo)
*   LegoCam
*   Logitech Quickcam Express (modelo antiguo)
*   Logitech QuickCam Notebook (no los modelos "Pro")
*   Logitech Quickcam Web

### qc-usb-messenger

*   Logitech Quickcam Messenger
*   Logitech Quickcam Communicate (para el Communicate MP/S5500 o para el "for business" vea la sección linux-uvc más abajo)

Ahora esta en el repositorio community.

**Nota:**

*   Si qc-usb-messenger no funciona, use el módulo gspca instalando para ello el paquete gspcav1.
*   Ahora el controlador es un módulo incluido en el kernel 2.6.27.

### zr364xx

Este driver puede usarse con muchas webcams como:

*   Aiptek PocketDV 3300
*   Creative PC-CAM 880
*   Konica Revio 2
*   Genius Digital Camera
*   Maxell Maxcam PRO DV3

Puede encontrar una lista completa de los dispositivos soportados [aquí](http://royale.zerezo.com/zr364xx/). También puede encontrar un PKGBUILD para este controlador en [AUR](/index.php/Arch_User_Repository "Arch User Repository").

### sn9c102

*   Trust Spacecam series
*   Maxell Smartcam (para notebooks): 352x288 máx. resolución a 3fps

### gspca

Una extensa lista de webcams soportadas está disponible en [[1]](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/video4linux/gspca.txt;hb=HEAD).

**Nota:** Este controlador no tiene soporte para V4L1.

### stv680

Muchas cámaras baratas sin nombre que vinieron de Asia en el último par de años usan el chipset stv680\. La mayoría de estas cámaras fueron artículos novedosos (p. ej. Pencam, SpyC@m y LegoCam).

*   Aiptek PenCam series
*   Digitaldream series
*   Dolphin Peripherals series
*   Lego LegoCam
*   Trust SpyC@m series
*   Welback Coolcam

Una lista más completa de webcams que usen el chipset stv680 está disponible [aquí](http://webcam-osx.sourceforge.net/cameras/index.php?orderBy=controller).

### linux-uvc

*   Genius iLook 1321
*   Logitech Webcam C210
*   Logitech Webcam C250
*   Logitech Webcam C270
*   Logitech Webcam C600
*   Logitech HD Webcam C525
*   Logitech HD Pro Webcam C920
*   Logitech Quickcam Pro 5000
*   Logitech Quickcam Pro 9000
*   Logitech Quickcam Orbit AF
*   Logitech Quickcam Orbit MP
*   Logitech Quickcam S5500
*   Microdia Pavilion Webcam (on MSI PR200)
*   Logitech Quickcam Communicate MP/S5500 o "for business"
*   Chicony Electronics CNF7051

Puede encontrar una lista completa de los dispositivos UVC soportados [aquí](http://www.ideasonboard.org/uvc/).

A partir del kernel 2.6.26 linux-uvc forma parte del mismo kernel. Tan solo cargue el módulo uvcvideo.

**Nota:**

*   Este controlador no tiene soporte para V4L1.
*   Con la WebCam SCB-0385N (usb ID 2232:1005), la WebCam SC-0311139N (usb ID 2232:1020) y la WebCam SC-03FFL11939N (usb ID 2232:1028), puede que necesite añadir alguna configuración extra al módulo si al usar la cámara el sistema se congela:

 `/etc/modprobe.d/uvcvideo.conf`  `options uvcvideo nodrop=1` 

### ov51x-jpeg

*   Sony EyeToy
*   Chicony DC-2120
*   Chicony DC-2120 pro
*   Trust Spacecam 320
*   Hercules Webcam Deluxe
*   Hercules Webcam Classic
*   Creative Live! Cam Notebook Pro VF0400
*   Creative Live! Cam Vista IM
*   Creative Live! Cam Vista IM VF0420
*   Creative Vista Webcam VF0330
*   ASUS webcam Model?
*   Philips PCVC820K/00
*   NGS showtime plus
*   HP VGA Webcam con micrófono integrado

Este es un módulo del kernel encontrado en el AUR con algunos añadidos con respecto al controlador original que provee de capacidades para la descompresión de jpeg.

En mi caso, para hacer que mi "Creative Live! Cam Vista IM" funcionase con Skype, tuve que añadir esta línea a `/etc/modprobe.d/modprobe.conf`:

```
options ov51x-jpeg forceblock=1

```

### r5u870 (Ricoh)

*   HP Pavilion Webcam
*   HP Webcam 1000
*   Sony VAIO VGP-VCCx

La webcam Ricoh está integrada en la mayoría de los nuevos portátiles Sony.

Instale [r5u87x-hg](https://aur.archlinux.org/packages/r5u87x-hg/) (contiene también el firmware) y ejecute el comando `loader`.

### stk11xx (Syntek)

*   Cámara integrada En la mayoría de los portátiles Asus.
*   Asus A8J, F3S, F5R, F5GL, F9E, VX2S, V1S, A6T.

Tan solo instale el paquete de AUR [stk11xx](https://aur.archlinux.org/packages/stk11xx/). Contiene el módulo del kernel adecuado.

## Asegúrese de que el modulo para su webcam está cargado

Añada el [módulo](/index.php/Kernel_modules_(Espa%C3%B1ol)#Cargar_módulos "Kernel modules (Español)") de su webcam a `/etc/modules-load.d/webcam.conf` para que sea cargado por el kernel durante la fase de arranque.

Si su webcam es USB, el kernel *debería* cargar de forma automática el controlador adecuado. Si este es el caso, compruebe el dmesg tras conectar la webcam. Debería ver algo como esto:

 `$ dmesg|tail` 
```
sn9c102: V4L2 driver for SN9C10x PC Camera Controllers v1:1.24a
usb 1-1: SN9C10[12] PC Camera Controller detected (vid/pid 0x0C45/0x600D)
usb 1-1: PAS106B image sensor detected
usb 1-1: Initialization succeeded
usb 1-1: V4L2 device registered as /dev/video0
usb 1-1: Optional device control through 'sysfs' interface ready
usbcore: registered new driver sn9c102

```

## Permisos

Los permisos para acceder a dispositivos de video (p. ej. `/dev/video0`) los maneja [udev (Español)](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)"), no se necesita ninguna configuración.

## Configuración de la webcam

Si desea configurar el brillo, el color y otros parámetros de la webcam (p. ej. cuando los colores de la webcam al usarla por primera vez son muy azules/rojizos/verduscos) puede usar [GTK+ UVC Viewer](http://guvcview.berlios.de/) (guvcview), disponible en los [Repositorio oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") como el paquete [guvcview](https://www.archlinux.org/packages/?name=guvcview). Tan solo instálelo y láncelo, y le mostrará una serie de ajustes configurables. Cambiar estos ajustes afectarán a todas las aplicaciones que hagan uso de la webcam (p. ej. Skype).

## Consiga que el software use su webcam

La versión 2.6.27 del kernel de linux soporta [muchos controladores nuevos de webcams](http://mxhaard.free.fr/spca5xx.html). Se ha eliminado el soporte para versiones antiguas de la API de Video4Linux API, y estos controladores solo soportan ahora la versión 2 de Video4Linux. La decodificación de formato de píxel se ha pasado a espacio de usuario, ya que Video4Linux en su versión 2 no soporta decodificación en espacio de kernel. La librería libv4l proporciona aplicaciones de espacio de usuario con servicios de decodificación de píxeles y será usado por la mayoría de los programas. Otras capas de compatibilidad también están disponibles.

**Si su dispositivo es creado pero la imagen se ve rara (la mía se veía completamente verde), probablemente necesite esto.**

Si la aplicación tiene soporte para V4L2 pero no tiene soporte para formato de píxel (ej: cheese), use entonces el siguiente comando:

```
LD_PRELOAD=/usr/lib/libv4l/v4l2convert.so cheese

```

Si la aplicación solo soporta versiones antiguas de V4L (Skype es el más popular de este tipo de software) use entonces este comando:

```
LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so skype

```

**Sugerencia:** Puede que quiera añadir línea como la siguiente en `/etc/profile` o en [xprofile (Español)](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)") para no tener que escribir un comando tan largo cada vez: `export LD_PRELOAD=/usr/'$LIB'/libv4l/v4l2convert.so` 

o

 `export LD_PRELOAD=/usr/'$LIB'/libv4l/v4l1compat.so` 

Para aplicaciones de 32 bits (p. ej. Skype) en Arch64, instale el paquete [lib32-v4l-utils](https://www.archlinux.org/packages/?name=lib32-v4l-utils).

Si la webcam funciona bien en guvcview, pero no funciona en Skype, puede que también tenga que establecer

```
export XLIB_SKIP_ARGB_VISUALS=1

```

antes de iniciarlo.

### Cheese

Cheese es el cliente para captura de fotos/vídeos de GNOME. Es similar a Photo Booth de Mac OS X. Esta en los repositorios oficiales.

En caso de tener el siguiente error:

```
Error during camera setup: One or more needed GStreamer elements are missing: cluttervideosink.

```

Primero cierre cheese, y luego ejecute los siguientes comandos:

```
# pacman -R clutter-gst
$ rm -r ~/.cache/gstreamer-1.0/

```

Inicie nuevamente cheese.

### fswebcam

fswebcam es una aplicación de webcam pequeña y flexible que puede lanzarse desde la línea de comandos. Instálela desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") con el paquete [fswebcam](https://aur.archlinux.org/packages/fswebcam/).

### GTK+ UVC Viewer (guvcview)

Además de ser una manera muy práctica de configurar su webcam, [guvcview](http://guvcview.sourceforge.net/) permite capturar (¡con sonido!) y visualizar video desde dispositivos soportados por el controlador de linux UVC. Disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") con el paquete [guvcview](https://www.archlinux.org/packages/?name=guvcview). Tan solo instálelo y láncelo, y le mostrará una serie de ajustes configurables. Cambiar estos ajustes afectarán a todas las aplicaciones que hagan uso de la webcam (p. ej. Skype).

### Kopete

Kopete es el cliente de mensajería instantánea (MI) de [KDE (Español)](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)"). A partir de KDE 3.5, tiene soporte para webcams de MSN y Yahoo!, pero no todas las cámaras funcionan aún. Está incluido en el paquete kdenetwork.

### Kamoso

Aplicación para tomar fotos y grabar vídeos usando la webcam para KDE. Disponible en AUR:

*   KDE4: [kamoso](https://www.archlinux.org/packages/?name=kamoso)
*   KDE Plasma 5: [kamoso-git](https://aur.archlinux.org/packages/kamoso-git/)

### xawtv

Esto es un visor de dispositivos v4l básico, y aunque su propósito es trabajar con tarjetas sintonizadoras de televisión, funciona muy bien con webcams. Mostrará lo que ve su webcam en pantalla. Instale ([xawtv](https://www.archlinux.org/packages/?name=xawtv)) y ejecútelo con:

```
$ xawtv -c /dev/video0

```

Si está usando una gráfica nVidia, y le sale un error como este

```
X Error of failed request:  XF86DGANoDirectVideoMode
 Major opcode of failed request:  139 (XFree86-DGA)
 Minor opcode of failed request:  1 (XF86DGAGetVideoLL)
 Serial number of failed request:  69
 Current serial number in output stream:  69

```

debería ejecutarlo en su lugar con:

```
$ xawtv -nodga

```

### VLC

[VLC](/index.php/VLC_(Espa%C3%B1ol) "VLC (Español)") puede usarse también para grabar y ver con su webcam. en el menú archivo de VLC, abra el diálogo 'Dispositivo de captura...' e introduzca los dispositivos de audio y video. O,desde la línea de comandos, ejecute:

```
$ vlc v4l:// :v4l-vdev="/dev/video0" :v4l-adev="/dev/audio2"

```

Esto hará que VLC muestre lo que ve su webcam. Para sacar capturas, simplemente dele a 'Capturar pantalla' en el menú 'Video'. Para grabar, añada un argumento `--sout`, p. ej:

```
$ vlc v4l:// :v4l-vdev="/dev/video0" :v4l-adev="/dev/audio2" \ 
  --sout "#transcode{vcodec=mp1v,vb=1024,scale=1,acodec=mpga,ab=192,channels=2}:duplicate{dst=std{access=file,mux=mpeg1,dst=/tmp/test.mpg}}"

```

(Obviamente un poco exagerados los bitrates pero esta bien para pruebas.) Dese cuenta de que esto no mostrará lo que está grabando en pantalla - para ello, debería añadir la pantalla como argumento de destino:

```
... :duplicate{dst=display,dst=std{access= ....

```

(Aunque esto puede resultar un poco duro para máquinas con hardware antiguo...)

### MPlayer

Para usar [MPlayer](/index.php/MPlayer "MPlayer") para tomar instantáneas desde su webcam ejecute este comando desde la terminal:

```
$ mplayer tv:// -tv driver=v4l2:width=640:height=480:device=/dev/video0 -fps 15 -vf screenshot

```

Desde aquí usted deber presionar `s` para tomar una instantánea. La instantánea se guardará en el directorio donde abrió el programa como **shotXXXX.png**. Si desea grabar un video:

```
$ mencoder tv:// -tv driver=v4l2:width=640:height=480:device=/dev/video0:forceaudio:adevice=/dev/dsp -ovc lavc -oac mp3lame -lameopts cbr:br=64:mode=3 -o *filename*.avi

```

Presione `Ctrl+c` para finalizar la grabación.

### FFmpeg

Vea [FFmpeg(Español)#Grabando webcam](/index.php?title=FFmpeg(Espa%C3%B1ol)&action=edit&redlink=1 "FFmpeg(Español) (page does not exist)").

### ekiga

Esta aplicación es muy parecida a Microsoft NetMeeting. Instale el paquete [ekiga](https://www.archlinux.org/packages/?name=ekiga) desde los repositorios oficiales. El druida de configuración ajustará todo lo demás por usted.

### Sonic-snap

Sonic-snap [[2]](http://www.stolk.org/sonic-snap/) es un visor/capturador para webcams basada **únicamente** en sn9c102. [sonic-snap](https://aur.archlinux.org/packages/sonic-snap/) está disponible en AUR.

### Skype

La nueva versión de [Skype (Español)](/index.php?title=Skype_(Espa%C3%B1ol)&action=edit&redlink=1 "Skype (Español) (page does not exist)") tiene soporte para video. Compruebe dispositivos de video en las opciones para una imagen de prueba a la cual puede hacer doble clic para ponerla a pantalla completa. Instale el paquete [skype](https://aur.archlinux.org/packages/skype/). Si ve una imagen verde o distorsionada con skype, lea la sección [#Consiga que el software use su webcam](#Consiga_que_el_software_use_su_webcam) más arriba.

Si su sistema es x86-64, debería instalar [lib32-v4l-utils](https://www.archlinux.org/packages/?name=lib32-v4l-utils) y ejecutar skype con

```
LD_PRELOAD=/usr/lib32/libv4l/v4l1compat.so skype

```

Puede tanto establecer un alias para skype, o renombrar el binario de skype original en `/usr/bin` y crear un script que contenga el comando de arriba, o puede simplemente configurar la opción de línea de comandos en el icono de skype de su entorno de escritorio favorito.

### Motion

	*Motion es un programa que monitoriza la señal de video de cámaras. Es capaz de detectar si una parte significativa de la imagen a cambiado; es decir, puede detectar el movimiento.*

[motion](https://aur.archlinux.org/packages/motion/) solo maneja dispositivos v4l2, por lo que si su cámara solo está soportada por controladores para v4l1 necesita precargar v4l1compat.so como se mencionó anteriormente. De otra manera le aparecerán muchos errores de motion acerca de no poder encontrar una paleta adecuada.

**Sugerencia:** Si necesita cargar webcams en un orden determinado (p. ej. cargar los dispositivos /dev/video0..n en orden) o establecer el propietario o los permisos, eche un vistazo a como [escribir reglas para udev](/index.php/Udev_(Espa%C3%B1ol)#Escribir_reglas_udev "Udev (Español)").

## Solución de problemas

### Microsoft Lifecam Studio/Cinema

Bajo determinadas condiciones, el Microsoft lifecam studio/cinema puede pedir ancho de banda usb en exceso y fallar [vea el FAQ de Uvcvideo](http://www.ideasonboard.org/uvc/#footnote-13). En este caso intente cargar el controlador `uvcvideo` con `quirks=0x80`. Añádalo a `/etc/modprobe.d/uvcvideo.conf` :

 `/etc/modprobe.d/uvcvideo.conf` 
```
## Apaño para el problema de ancho de banda para lifecam studio/cinema
options uvcvideo quirks=0x80

```