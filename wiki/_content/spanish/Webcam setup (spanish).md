**Estado de la traducción**
Este artículo es una traducción de [Webcam setup](/index.php/Webcam_setup "Webcam setup"), revisada por última vez el **2018-12-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Webcam_setup&diff=0&oldid=560708) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Esta es una guía para configurar su webcam en Arch Linux.

Lo más probable es que su webcam funcione sin necesidad de configuración. Los permisos para acceder a los dispositivos de vídeo (por ejemplo, `/dev/video0`) son manejados por [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)"), no es necesaria ninguna configuración.

## Contents

*   [1 Cargar](#Cargar)
*   [2 Configuración](#Configuración)
*   [3 Aplicaciones](#Aplicaciones)
    *   [3.1 xawtv](#xawtv)
    *   [3.2 VLC](#VLC)
    *   [3.3 MPlayer](#MPlayer)
    *   [3.4 mpv](#mpv)
    *   [3.5 FFmpeg](#FFmpeg)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 Soporte V4L1](#Soporte_V4L1)
    *   [4.2 Microsoft Lifecam Studio/Cinema](#Microsoft_Lifecam_Studio/Cinema)
    *   [4.3 Skype](#Skype)
    *   [4.4 Comprobar el ancho de banda utilizado por las webcams USB](#Comprobar_el_ancho_de_banda_utilizado_por_las_webcams_USB)
    *   [4.5 Grupos](#Grupos)

## Cargar

Identifique el nombre de su webcam (utilizando, por ejemplo, `lsusb`) y encuentre el controlador adecuado. Véase [dispositivos webcam](https://www.linuxtv.org/wiki/index.php/Webcam_devices) para obtener detalles sobre los controladores.

Agregue el [módulo del kernel](/index.php/Kernel_module_(Espa%C3%B1ol) "Kernel module (Español)") de su webcam a `/etc/modules-load.d/webcam.conf` para que se cargue en el kernel durante la etapa inicial del arranque.

Si su webcam funciona por USB, el kernel *debería* cargar automáticamente el controlador adecuado. Si este es el caso, compruebe dmesg después de conectar su webcam. Debería ver algo así:

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

## Configuración

Si desea configurar el brillo, el color y otros parámetros de la webcam (por ejemplo, en el caso de que los colores sin necesidad de configuración sean demasiado azulados/rojizos/verdosos) puede usar **Qt V4L2 Test Bench** (*qv4l2*), disponible en el paquete [v4l-utils](https://www.archlinux.org/packages/?name=v4l-utils). Simplemente instálelo y ejecútelo, y le presentará una lista de ajustes configurables. Cambiar estos ajustes afectará a todas las aplicaciones.

## Aplicaciones

Véase también [Lista de aplicaciones/Multimedia#Webcam](/index.php/List_of_applications/Multimedia#Webcam "List of applications/Multimedia").

### xawtv

Este es un visor de dispositivo v4l básico, y aunque está diseñado para usarse con tarjetas sintonizadoras de TV, funciona bien con webcams. Mostrará lo que ve su webcam en una ventana. Instálelo ([xawtv](https://www.archlinux.org/packages/?name=xawtv)) y ejecútelo con:

```
$ xawtv -c /dev/video0

```

Si está utilizando una tarjeta gráfica nVidia, y obtiene un error como

```
X Error of failed request:  XF86DGANoDirectVideoMode
 Major opcode of failed request:  139 (XFree86-DGA)
 Minor opcode of failed request:  1 (XF86DGAGetVideoLL)
 Serial number of failed request:  69
 Current serial number in output stream:  69

```

en su lugar debería ejecutarlo como:

```
$ xawtv -nodga

```

### VLC

[VLC](/index.php/VLC_(Espa%C3%B1ol) "VLC (Español)") también se puede usar para ver y grabar su webcam. En el menú "Medio" de VLC, abra el cuadro de diálogo 'Dispositivo de captura ...' e ingrese los archivos del dispositivo de vídeo y audio. O desde la línea de comando, haga:

```
$ vlc v4l:// :v4l-vdev="/dev/video0" :v4l-adev="/dev/audio2"

```

Esto hará que VLC refleje su webcam. Para tomar instantáneas, simplemente elija 'Instantánea' en el menú 'Vídeo'. Para grabar una transmisión, agregue un argumento `--sout`. Por ejemplo:

```
$ vlc v4l:// :v4l-vdev="/dev/video0" :v4l-adev="/dev/audio2" \ 
  --sout "#transcode{vcodec=mp1v,vb=1024,scale=1,acodec=mpga,ab=192,channels=2}:duplicate{dst=std{access=file,mux=mpeg1,dst=/tmp/test.mpg}}"

```

(Obviamente, es un poco exagerado con respecto a las tasas de bits, pero está bien para propósitos de testeo). Tenga en cuenta que esto no producirá un espejo en la pantalla - para ver lo que está grabando, deberá agregar el monitor como un argumento de destino:

```
... :duplicate{dst=display,dst=std{access= ....

```

(Aunque esto puede cargar un poco el hardware antiguo...)

### MPlayer

Para usar [MPlayer](/index.php/MPlayer_(Espa%C3%B1ol) "MPlayer (Español)") para tomar instantáneas de su webcam, ejecute este comando desde la terminal:

```
$ mplayer tv:// -tv driver=v4l2:width=640:height=480:device=/dev/video0 -fps 15 -vf screenshot

```

Desde aquí, debe pulsar `s` para tomar la instantánea. La instantánea se guardará en su carpeta actual como **shotXXXX.png**. Si desea grabar un vídeo continuo:

```
$ mencoder tv:// -tv driver=v4l2:width=640:height=480:device=/dev/video0:forceaudio:adevice=/dev/dsp -ovc lavc -oac mp3lame -lameopts cbr:br=64:mode=3 -o *filename*.avi

```

Presione `Ctrl+c` para finalizar la grabación.

### mpv

Para usar [mpv](/index.php/Mpv_(Espa%C3%B1ol) "Mpv (Español)") para tomar instantáneas desde su webcam, ejecute este comando desde la terminal:

```
$ mpv av://v4l2:/dev/video0

```

Para utilizar MJPEG como formato de pixel en lugar del predeterminado (en muchos casos, YUYV), puede hacer lo siguiente:

```
$ mpv --demuxer-lavf-format video4linux2 --demuxer-lavf-o-set input_format=mjpeg /dev/video0

```

En algunos casos, esto puede llevar a mejoras drásticas en la calidad y el rendimiento (5FPS -> 30FPS por ejemplo).

Desde aquí, debe pulsar `s` para tomar la instantánea. La instantánea se guardará en su carpeta actual como `mpv-shot*NNNN*.jpg`.

### FFmpeg

Véase [FFmpeg#Grabación de la webcam](/index.php/FFmpeg#Recording_webcam "FFmpeg").

## Solución de problemas

### Soporte V4L1

La versión 2.6.27 del kernel de Linux eliminó la compatibilidad con la API de Video4Linux (1) heredada. La decodificación en formato de píxeles se ha insertado en el espacio del usuario, ya que la versión 2 de Video4Linux no admite la decodificación del espacio del kernel. La librería libv4l proporciona aplicaciones de usuario con servicios de decodificación de píxeles y será utilizada por la mayoría de los programas. Otras capas de compatibilidad también están disponibles.

**Si su dispositivo está creado pero la imagen se ve extraña (por ejemplo, casi completamente verde), probablemente necesite esto.**

Si la aplicación es compatible con V4L2 pero no es compatible con pixelformat, use el siguiente comando:

```
LD_PRELOAD=/usr/lib/libv4l/v4l2convert.so application

```

Si la aplicación solo admite la versión antigua de V4L, use este comando:

```
LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so application

```

**Sugerencia:** También le convendría agregar la siguiente línea a `/etc/profile` o [xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)") para que no tenga que escribir ese largo comando todo el rato: `export LD_PRELOAD=/usr/lib/libv4l/v4l2convert.so` 

o

 `export LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so` 

Para aplicaciones [multilib](/index.php/Official_repositories_(Espa%C3%B1ol)#multilib "Official repositories (Español)") de 32 bits, instale el paquete [lib32-v4l-utils](https://www.archlinux.org/packages/?name=lib32-v4l-utils) y reemplace `/usr/lib/libv4l/` por `/usr/lib32/libv4l/` en los comandos anteriores.

### Microsoft Lifecam Studio/Cinema

Bajo ciertas configuraciones, Microsoft lifecam studio/cinema puede solicitar demasiado ancho de banda de usb y fallar. [Véase las preguntas frecuentes sobre Uvcvideo](http://www.ideasonboard.org/uvc/#footnote-13). En este caso, cambie el búfer cargando el controlador `uvcvideo` con `quirks=0x80`. Agréguelo a `/etc/modprobe.d/uvcvideo.conf`:

 `/etc/modprobe.d/uvcvideo.conf` 
```
## fix bandwidth issue for lifecam studio/cinema
options uvcvideo quirks=0x80
```

**Nota:** Si los retrasos son visibles en los registros, o la cámara funciona periódicamente, esta solución debería aplicarse en general. Valores más grandes como `quirks=0x100` son posibles.

### Skype

Al probar la webcam, tenga en cuenta lo siguiente:

*   Echobot no soporta vídeochat. No lo use para probar su webcam.
*   Skype puede reconocer diferentes dispositivos de vídeo/cámara (/dev/video*). Se enumerarán y nombrarán algo así como "cámara integrada ..." en un menú desplegable en la configuración de la cámara. Pruebe cada cámara y espere unos segundos, porque lleva tiempo cambiar a una cámara distinta.

### Comprobar el ancho de banda utilizado por las webcams USB

Cuando se ejecutan varias webcams en un único bus USB, pueden llegar a saturar el ancho de banda del bus USB y dejar de funcionar correctamente. Esto puede ser diagnosticado con la herramienta *usbtop* del paquete [usbtop](https://aur.archlinux.org/packages/usbtop/).

### Grupos

Si el sistema le dice que no puede encontrar el dispositivo, posiblemente sea debido a que no forma parte del grupo `video`. Asegúrese de que forma parte del grupo `video` usando `groups`. Si no lo es, agréguese usando `gpasswd`.