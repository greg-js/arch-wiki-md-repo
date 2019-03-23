**Estado de la traducción**
Este artículo es una traducción de [EPSXe](/index.php/EPSXe "EPSXe"), revisada por última vez el **2019-03-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=EPSXe&diff=0&oldid=569418) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[ePSXe](https://en.wikipedia.org/wiki/ePSXe "wikipedia:ePSXe") (enhanced PSX emulator) es un emulador de PlayStation para hardware de PC basado en x86 con Microsoft Windows o Linux, así como dispositivos que ejecuten Android. Fue escrito por tres autores usando los alias *Calb*, *_Demo_* y *Galtor*. ePSXe es de código cerrado con la excepción de la interfaz de programación de aplicaciones (API) para sus complementos.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
*   [3 Jugando](#Jugando)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 Complemento xgl2 no funciona](#Complemento_xgl2_no_funciona)
    *   [4.2 Dispositivo de sonido no encontrado](#Dispositivo_de_sonido_no_encontrado)
*   [5 Véase también](#Véase_también)

## Instalación

**Advertencia:** La instalación y uso de éste emulador requiere un archivo BIOS de Sony PlayStation. No podría usar dicho archivo para jugar en un emulador de PSX si no es propietario de una consola Sony PlayStation, Sony PSOne o Sony PlayStation 2\. Tener la imágen de BIOS sin tener la consola real es una violación de la ley de derechos de autor. Usted ha sido advertido.

Instale [epsxe](https://aur.archlinux.org/packages/epsxe/) de [AUR](/index.php/AUR "AUR"), junto con cualquier [complemento](https://aur.archlinux.org/packages.php?K=epsxe-plugin). Además, debería tener a mano un archivo BIOS obtenido legalmente.

Agréguese al grupo `games`:

```
# usermod -G games -a USERNAME

```

Si el grupo no existe, creelo primero:

```
# groupadd games

```

Ejecute epsxe desde el acceso directo o escribiendo 'epsxe' en una terminal.

## Configuración

Configure el vídeo y sonido al ir a *Config > Video* y *Config > Sound* respectivamente, y configure los complementos que desee. Verifique que estén funcionando haciendo clic en los botones de Prueba en cada una de las ventanas.

La ruta del CD-ROM debería estar establecida por defecto. Puede comprobarlo al ir a *Config > Cdrom*.

Configure los controles para el jugador uno al ir a *Config > Game Pad > Port 1 > Pad 1*.

## Jugando

Ejecute un juego desde su CD-ROM haciendo clic en *File > Run CDROM*.

Cargue un juego desde un ISO haciendo clic en *File > Run ISO*.

Puede manipular estados del juego al ir a *Run > Save State (F1)* y *Run > Load State (F3)*, o usando las teclas de acceso rápido F1 y F3.

## Solución de problemas

### Complemento xgl2 no funciona

Tendrá que instalar nvidia-utils, si se ejecuta en un chroot de 32-bit .

### Dispositivo de sonido no encontrado

Si el complemento de sonido no funciona y está usando alsa, ejecute:

```
# modprobe snd-pcm-oss

```

## Véase también

*   ePSXe - [http://www.epsxe.com/](http://www.epsxe.com/)
*   Pete's PSX plugins - [http://www.pbernert.com/index.htm](http://www.pbernert.com/index.htm)