**Estado de la traducción**
Este artículo es una traducción de [Cube KNote i1101](/index.php/Cube_KNote_i1101 "Cube KNote i1101"), revisada por última vez el **2019-01-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Cube_KNote_i1101&diff=0&oldid=563276) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

| **Dispositivo** | **Estado** | **Módulos** |
| Monitor | Funciona | xf86-video-intel |
| Pantalla táctil | Funciona,con el firmware [mssl1680-firmware](https://aur.archlinux.org/packages/mssl1680-firmware/) | silead_ts |
| Wifi | Funciona | iwlwifi |
| Audio | Funciona | alc269 |
| Panel táctil | Funciona |
| Estado de la batería | Funciona |
| Cámara | No funciona |
| Bluetooth | Funciona | btintel |
| Lector tarjetas microSD | Funciona |
| Gestión de energía | Parece que funciona correctamente |
| Acelerómetro | Funciona, con un kernel compilado personalizado | bma150_accel_i2c |
| Botones de hardware | Funciona |
| Tapa/Teclado | Funciona |

Cube KNote i1101 es una tablet de 11 pulgadas con el procesador Apollo Lake (Celeron N3450) y 6GB de memoria RAM. También cuenta con una pantalla de resolución Full HD (1920x1080).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación y configuración](#Instalación_y_configuración)
    *   [1.1 Sonido](#Sonido)
        *   [1.1.1 No hay sonido](#No_hay_sonido)
        *   [1.1.2 No se reconoce el jack de 3.5mm](#No_se_reconoce_el_jack_de_3.5mm)
    *   [1.2 Acelerómetro](#Acelerómetro)

## Instalación y configuración

La mayoría de los dispositivos deberían funcionar sin necesidad de configuración después de una instalación estándar, aunque algunos dispositivos necesitan ajustes adicionales.

### Sonido

#### No hay sonido

Necesita agregarse al grupo de audio.

#### No se reconoce el jack de 3.5mm

Añada las siguientes líneas al archivo `/etc/modprobe.d/50-sound.conf`

```
alias snd-card-0 snd-hda-intel
alias sound-slot-0 snd-hda-intel

```

### Acelerómetro

Debe compilar el kernel manualmente para habilitar el controlador IIO `bmc150_accel_i2c` e instalar [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) si utiliza un entorno de escritorio. La información DSDT proporcionan datos `ACCEL_MOUNT_MATRIX` defectuosos, así que cree el siguiente archivo en `/etc/udev/hwdb.d/61-sensor-local.hwdb` con el siguiente contenido:

```
sensor:modalias:acpi:BOSC0200*:dmi:*:svnALLDOCUBE:pni1101:*
 ACCEL_MOUNT_MATRIX=1, 0, 0; 0, -1, 0; 0, 0, -1

```

Reinicie y el acelerómetro funcionará. Sin embargo, fallará después de suspender y reanudar la sesión de la tablet, lo que se considera un error del controlador.