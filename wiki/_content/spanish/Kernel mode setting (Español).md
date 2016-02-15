Kernel [Mode Setting](https://en.wikipedia.org/wiki/Mode-setting "wikipedia:Mode-setting") (KMS) es un método de fijación de la resolución y la profundidad de la pantalla en el espacio del kernel, en vez de en el espacio de usuario (userspace).

KMS permite la resolución nativa en el framebuffer y permite al instante una consola (TTY) de conmutación. KMS también puede permitir a las nuevas tecnologías (como DRI2) reducir los defectos y aumentar el rendimiento 3D, incluso el ahorro de energía en el espacio del kernel.

**Nota:** Los controladores propietarios [nvidia](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)") y [Catalyst](/index.php/ATI_Catalyst_(Espa%C3%B1ol) "ATI Catalyst (Español)") también implementan el kernel mode-setting, pero como no implementan la integración en el kernel, carecen de un controlador fbdev para la consola de alta resolución.

## Contents

*   [1 Antecedentes](#Antecedentes)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Iniciar KMS con retardo](#Iniciar_KMS_con_retardo)
    *   [2.2 Iniciar KMS tempranamente](#Iniciar_KMS_tempranamente)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [3.1 Tipos de letras demasiado pequeñas](#Tipos_de_letras_demasiado_peque.C3.B1as)
    *   [3.2 Cuestión sobre bootloading y dmesg](#Cuesti.C3.B3n_sobre_bootloading_y_dmesg)
*   [4 Forzar modos y EDID](#Forzar_modos_y_EDID)
*   [5 Desactivar modesetting](#Desactivar_modesetting)

## Antecedentes

Anteriormente, la inicialización de la tarjeta de video era trabajo del servidor X. Debido a ésto, no era fácil obtener gráficos lujosos en las consolas virtuales. Además, cada vez que se interrumpía X (`Ctrl+Alt+F1`) para acceder a una consola virtual, el servidor tenía que dar el control de la tarjeta de vídeo al kernel, que era lento y causaba parpadeo. El mismo «doloroso» proceso sucedía cuando el control se le devolvía al servidor X (`Ctrl+Alt+F7`).

Con Kernel Mode Setting (KMS), el kernel es ahora capaz de establecer el modo de la tarjeta de vídeo. Esto hace posible los gráficos aceptables durante el arranque, y el cambio rápido entre la consola virtual y X, entre otras cosas.

## Instalación

En primer lugar, tenga en cuenta que para cualquier método que utilice, debe siempre desactivar:

*   Cualquier opción «vga=» en el gestor de arranque, ya que éstos entren en conflicto con la resolución nativa habilitada por KMS.
*   Cualquier línea «video=» que provoque a framebuffer entrar en conflicto con el controlador.
*   Todos los demás controladores framebuffer (por ejemplo, [uvesafb](/index.php/Uvesafb "Uvesafb")).

### Iniciar KMS con retardo

Los controladores [Intel](/index.php/Intel_(Espa%C3%B1ol) "Intel (Español)"), [Nouveau](/index.php/Nouveau_(Espa%C3%B1ol) "Nouveau (Español)") y [ATI](/index.php/ATI_(Espa%C3%B1ol) "ATI (Español)") ya permiten activar KMS de forma automática para todos los chipsets. Así que no es necesario instalarlo de forma manual.

Los controladores propietarios [NVIDIA](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)") y [ATI Catalyst](/index.php/ATI_Catalyst_(Espa%C3%B1ol) "ATI Catalyst (Español)") no se utilizan con los controladores abiertos. A fin de poder utilizar KMS debe reemplazarlos por los controladores de código abierto.

### Iniciar KMS tempranamente

Para cargar KMS tan pronto como sea posible en el proceso de arranque, añada el módulo [radeon](/index.php/Radeon "Radeon") (para tarjetas ATI/AMD), [i915](/index.php/Intel "Intel") (para tarjetas intel integradas) o [noveau](/index.php/Nouveau_(Espa%C3%B1ol) "Nouveau (Español)") (para tarjetas Nvidia) a la línea de `MODULES` en el archivo`/etc/mkinitcpio.conf`:

 `/etc/mkinitcpio.conf` 

```
MODULES="i915"
**o**
MODULES="radeon"
**o**
MODULES="nouveau"
```

Si utiliza un archivo EDID personalizado, debe incorporarlo en initramfs así:

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

Reconstruya la imagen del kernel (remítase al artículo [mkinitcpio](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") para más información):

 `# mkinitcpio -p <nombre del kernel presente; por ejemplo, _linux_>` 

## Solución de problemas

### Tipos de letras demasiado pequeñas

Vea [cambiar el tipo de letra por defecto](/index.php/Fonts#Changing_the_default_font "Fonts") para saber cómo cambiar las fuentes de la consola a una fuente grande. Los tipos de letras del terminal están disponibles en [community] para muchos tamaños, incluyendo los tamaños más grandes.

### Cuestión sobre bootloading y dmesg

Sondear los dispositivos de pantalla conectados a sistemas antiguos puede ser bastante gravoso. El sondeo sucederá periódicamente y puede, en el peor de los casos, tomar varios cientos de milisegundos, dependiendo del hardware. Esto provocará paradas visibles, por ejemplo, en la reproducción de vídeo. Estos paradas pueden ocurrir incluso cuando el vídeo está en la salida de HDP, pero, en cualquier caso, tiene otras salidas que no son HDP en la configuración de su hardware. Si experimenta paradas en la salida de la pantalla que ocurran cada 10 segundos, la desactivación de polling podría ayudar.

Si ve un código de error 0x00000010 (2) durante el arranque, (recibirá alrededor de 10 líneas de texto, la última parte indicando el código de error), proceda a añadir la siguiente línea en el archivo `/etc/modprobe.d/modprobe.conf`:

```
options drm_kms_helper poll=0

```

## Forzar modos y EDID

**Nota:** Esta sección es un trabajo en curso. Las mejoras y correcciones son bienvenidos.

En caso de que su monitor/TV no está enviando el dato [EDID](https://en.wikipedia.org/wiki/EDID "wikipedia:EDID") adecuado o problemas similares, se dará cuenta de que la resolución nativa no se configura automáticamente o no se muestre en absoluto. El kernel tiende a cargar los datos EDID binarios, y proporciona así los datos, para establecer cuatro de las resoluciones más típicas.

Si tiene el archivo EDID de su monitor el proceso es fácil. En otro caso, puede utilizar uno de los binarios EDID para obtener una de las resoluciones incorporadas (o generar uno durante la compilación del kernel, [más información aquí](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/EDID/HOWTO.txt)) o compilar su propio EDID.

En caso de que tenga un archivo EDID (por ejemplo extraído de los controladores de Windows para el monitor), cree un directorio `edid` en `/lib/firmware`:

```
# mkdir /lib/firmware/edid

```

y luego copiar el binario en el directorio `/lib/firmware/edid`.

Para cargarlo en el arranque, especifique lo siguiente en la línea de órdenes del kernel:

 `drm_kms_helper.edid_firmware=edid/your_edid.bin` 

También puede especificarlo solo para una conexión determinada:

 `drm_kms_helper.edid_firmware=VGA-1:edid/your_edid.bin` 

Respecto a las cuatro resoluciones incorporados, consulte la tabla siguiente para especifiar el nombre:

| **Resolución** | **Nombre a especificar** |
| 1024x768 | edid/1024x768.bin |
| 1280x1024 | edid/1280x1024.bin |
| 1600x1200 (kernel 3.10 o superior) | edid/1600x1200.bin |
| 1680x1050 | edid/1680x1050.bin |
| 1920x1080 | edid/1920x1080.bin |

Si estamos utilizando KMS tempranamente, debemos incluir el archivo EDID personalizado en initramfs si queremos evitar problemas.

La información completa se puede leer [aquí](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/EDID/HOWTO.txt) y [aquí](https://www.osadl.org/Single-View.111+M591850c02b5.0.html).

**Advertencia:** El método descrito a continuación está, de algún modo incompleto, porque por ejemplo, Xorg no tiene en cuenta la resolución especificada, por lo que se aconseja a los usuarios utilizar el método descrito anteriormente; no obstante, especificar la resolución con `video=` en la línea de órdenes puede ser útil en algunos escenarios.

De la [wiki nouveau](http://nouveau.freedesktop.org/wiki/KernelModeSetting):

Un modo puede ser forzado en la línea de comandos del kernel. Por desgracia, la opción de vídeo en la línea de comandos no está bien documentado en el caso de DRM. Opiniones sobre la manera de proceder se pueden encontrar en:

*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt)
*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c)

El formato es:

```
 video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]

```

*   <conn>: conector, por ejemplo, DVI-I-1, consulte su registro del kernel.
*   <xres> x <yres>: resolución
*   M: ¿conmutar a modo CVT?
*   R: ¿reducción de borrado?
*   -<bpp>: profundidad de color
*   @ <refresh>: refrescar tasa
*   i: entrelazado (modo non-CVT)
*   m: ¿los márgenes?
*   e: salida forzada en on
*   d: salida forzada en off
*   D: salida digital forzada a (por ejemplo, conector DVI-I)

Puede anular los modos de varias salidas usando de varias maneras «vídeo», por ejemplo, forzando a DVI a 1024x768 a 85 Hz y TV-out off:

```
video=DVI-I-1:1024x768@85 video=TV-1:d

```

Para obtener el nombre y el estado actual de los conectores, puede utilizar la siguiente línea de órdenes:

 `for p in /sys/class/drm/*/status; do con=${p%/status}; echo -n "${con#*/card?-}: "; cat $p; done` 

```

DVI-I-1: connected
HDMI-A-1: disconnected
VGA-1: disconnected

```

## Desactivar modesetting

Es posible que desee desactivar KMS por diversas razones, tales como evitar una pantalla en blanco o un error de «no signal» del monitor, cuando se utiliza el controlador Catalyst, etc. Para desactivar KMS, agregue `nomodeset` a los [parámetros del kernel](/index.php/Kernel_parameters "Kernel parameters"). Vea [parámetros del Kernel](/index.php/Kernel_parameters "Kernel parameters") para más información.

Junto con el parámetro del kernel `nomodeset`, la tarjeta gráfica de Intel necesita añadir `i915.modeset=0` y la tarjeta gráfica de Nvidia `nouveau.modeset=0`. Para el sistema Nvidia Optimus con dos tarjetas gráficas, es necesario agregar los tres parámetros del kerne (es decir, `"nomodeset i915.modeset=0 nouveau.modeset=0"`).

**Nota:** Algunos controladores de [Xorg](/index.php/Xorg "Xorg") no funcionan con KMS desactivado. Consulte la página de la wiki sobre su controlador específico para más detalles.