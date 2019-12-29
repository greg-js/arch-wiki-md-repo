<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introducción](#Introducción)
*   [2 En general](#En_general)
*   [3 Localmente](#Localmente)
    *   [3.1 En X](#En_X)
    *   [3.2 Desde consola](#Desde_consola)
    *   [3.3 Usando ALSA](#Usando_ALSA)
    *   [3.4 En GNOME/Metacity](#En_GNOME/Metacity)
    *   [3.5 GTK+](#GTK+)
*   [4 Véase también](#Véase_también)

## Introducción

El ordenador hace ruidos a modo de pitidos u otros sonidos en diversas ocasiones, ajenos a nuestra voluntad. Provienen de diversas fuentes, y, como tal, se pueden configurar para que se produzcan o no y cuándo.

Por otro lado, los sonidos del ordenador se pueden escuchar bien a través del altavoz integrado, en su caso, bien a través de los altavoces que están conectados a la tarjeta de sonido. En este artículo se trata principalmente del primer caso.

Los sonidos pueden ser causados ​​por la BIOS (Basic Input/Output System), el OS (sistema operativo), el DE (entorno de escritorio), o otros programas instalados. El causado por la BIOS es un problema particularmente molesto porque se mantiene dentro de un chip EPROM de la placa base, y el único control directo del usuario sobre el mismo es desconectando la alimentación de encendida o apagada. A menos que la configuración de la BIOS permita ajustarla o, en su defecto, desee intentar reprogramar el chip con el código correcto, no es probable que se sea capaz de cambiarlo en absoluto. Los pitidos generados por la BIOS no se abordan aquí, lo único que se le puede decir al respecto es que desconectando el altavoz integrado del ordenador impedirá que se escuchen tales sonidos. (Lo cual debe hacer bajo su propia responsabilidad.)

Sin embargo, obviando lo anterior, lo demás sonidos que pueden salir del altavoz de su ordenador pueden ser controlados con las sugerencias que se enumeran a continuación.

Hay que señalar también que la opción de apagar un determinado sonido, mientras se dejan otros funcionales, es posible si se puede identificar qué parte del entorno es la fuente de la generación del sonido en particular. Con esta información, hacer una selección personalizada de sonidos sobre eventos del sistema, parece posible. Por favor, siéntase libre de añadir sus conclusiones a esta página Wiki cuando encuentre ejemplos particulares de combinaciones de parámetros que puedan ser útiles para otros usuarios.

## En general

El altavoz del PC se desactiva [deshabilitando](/index.php/Kernel_modules_(Espa%C3%B1ol)#Manejar_módulos_manualmente "Kernel modules (Español)") el [módulo del núcleo](/index.php/Kernel_module_(Espa%C3%B1ol) "Kernel module (Español)") `pcspkr`:

```
# rmmod pcspkr

```

Coloque en la [lista negra](/index.php/Kernel_modules_(Espa%C3%B1ol)#Lista_negra "Kernel modules (Español)") el módulo `pcspkr` para evitar que [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") lo cargue en el arranque.

```
# echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf

```

## Localmente

### En X

```
$ xset -b

```

Se puede añadir este comando a un archivo de inicio, como [xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)") para hacerlo permanente.

### Desde consola

Se puede añadir el comando de abajo en el archivo `/etc/profile` o crear un archivo específico como `/etc/profile.d/disable-beep.sh` (debe ser ejecutable):

```
setterm-blength 0

```

Otra forma de hacerlo es añadir o descomentar la línea siguiente en el archivo general del sistema `/etc/inputrc` o en el específico del usuario `~/.inputrc`:

```
set bell-style none

```

### Usando ALSA

**Sugerencia:** Para la mayoría de las tarjetas de Intel, si no ve el altavoz del PC en el dispositivo por defecto de alsamixer, entonces pruebe a seleccionar el dispositivo «HDA Intel PCH» pulsando F6\. Está listado allí como «Beep». Esto es porque los controles del proxy de PulseAudio no pueden enumerar todos los altavoces del PC.

Intente silenciar el altavoz del PC con el siguiente comando:

```
$ amixer set 'PC Speaker' 0% mute

```

Para ciertas tarjetas de sonido, la variable es PC Beep:

```
$ amixer set 'PC Beep' 0% mute

```

O simplemente Beep:

```
$ amixer set 'Beep' 0% mute

```

También puede utilizar alsamixer como interfaz gráfica de usuario desde consola:

```
$ alsamixer

```

Desplácese hasta beep PC y pulse 'M' para silenciar. Para guardar la configuración establecida en alsa, escriba:

```
# alsactl store

```

**Nota:** No todas las tarjetas de sonido muestran el altavoz del PC o un control deslizante del Beep del PC en alsamixer

.

### En GNOME/Metacity

En Gconf establezca la siguiente cadena **`/apps/metacity/general/audible_bell`** con el valor **`false`**, mediante el siguiente comando:

```
$ gconftool-2 -s -t string /apps/metacity/general/audible_bell false

```

### GTK+

Añada esta línea a su .gtkrc-2.0 y en la sección [Settings] de $XDG_CONFIG_HOME/gtk-3.0/settings.ini:

```
gtk-error-bell = 0

```

## Véase también

*   Consulte estas página `man` para obtener más información: `xset(1)`, `setterm(1)`, `readline(3)`.
*   [Módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)")