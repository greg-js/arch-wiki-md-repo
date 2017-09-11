**MPlayer** es un popular reproductor multimedia para GNU/Linux. Tiene soporte para la mayoría de formatos de audio y vídeo existentes, lo que lo hace altamente versátil, incluso si es utilizado generalmente para ver vídeos.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Interfaces/GUIs](#Interfaces.2FGUIs)
*   [3 Integración en Navegadores](#Integraci.C3.B3n_en_Navegadores)
    *   [3.1 Firefox](#Firefox)
    *   [3.2 Konqueror](#Konqueror)
    *   [3.3 Chromium](#Chromium)
*   [4 Configuración](#Configuraci.C3.B3n)
    *   [4.1 Atajos del teclado](#Atajos_del_teclado)
*   [5 Tips and Tricks](#Tips_and_Tricks)
*   [6 Continuación de reproducción automática](#Continuaci.C3.B3n_de_reproducci.C3.B3n_autom.C3.A1tica)

## Instalación

Varias versiones de MPlayer pueden ser [instaladas](/index.php/Pacman "Pacman") desde los [repositorios oficiales](/index.php/Official_repositories "Official repositories") o desde [AUR](/index.php/AUR "AUR"):

*   **[MPlayer](/index.php/MPlayer "MPlayer")** — Paquete oficial

	[https://mplayerhq.hu/](https://mplayerhq.hu/) || [mplayer](https://www.archlinux.org/packages/?name=mplayer)

Algunas versiones destacables:

*   **MPlayer-VAAPI** — Versión con VAAPI (API de aceleración de vídeo) habilitado

	[http://gitorious.org/vaapi/mplayer](http://gitorious.org/vaapi/mplayer) || [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/)

*   **MPlayer-svn** — Versión de desarrollo

	|| [mplayer-svn](https://aur.archlinux.org/packages/mplayer-svn/)

*   **MPlayer2** — Una bifurcación de MPlayer

	[http://www.mplayer2.org/](http://www.mplayer2.org/) || [mplayer2](https://aur.archlinux.org/packages/mplayer2/) [mplayer2-git](https://aur.archlinux.org/packages/mplayer2-git/)

**Nota:** El desarrollo de *mplayer2* parece haber cesado en favor de [mpv](/index.php/Mpv "Mpv") (un reproductor basado en *mplayer* y *mplayer2*), que esta enfocado en la velocidad y calidad de desarrollo, aunque esto supone incompatibilidades entre hardware antiguo y el software. Tenga en cuenta estas [diferencias](https://github.com/mpv-player/mpv/blob/master/DOCS/man/changes.rst) si desea utilizarlo.

## Interfaces/GUIs

*   **Deepin Media Player** — Una rica inferfaz GTK2/Python para el escritorio Deepin.

	[http://www.linuxdeepin.com/](http://www.linuxdeepin.com/) || [deepin-media-player](https://aur.archlinux.org/packages/deepin-media-player/)

*   **GNOME MPlayer** — Una simple GUI para MPlayer basada en GTK+.

	[http://kdekorte.googlepages.com/gnomemplayer](http://kdekorte.googlepages.com/gnomemplayer) || [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)

*   **KPlayer** — Reproductor multimedia para KDE4 que usa mplayer como backend.

	[http://kplayer.sourceforge.net/](http://kplayer.sourceforge.net/) || [kplayer](https://aur.archlinux.org/packages/kplayer/)

*   **KMPlayer** — Complemento de vídeo para el navegador Konqueror y una básica interfaz MPlayer/Xine/ffmpeg/ffserver/VDR para KDE.

	[http://kmplayer.kde.org/](http://kmplayer.kde.org/) || [kmplayer](https://www.archlinux.org/packages/?name=kmplayer)

*   **Rosa Media Player** — Reproductor multimedia basado en SMPlayer con una UI limpia y elegante.

	[http://www.rosalab.com/](http://www.rosalab.com/) || [rosa-media-player](https://aur.archlinux.org/packages/rosa-media-player/)

*   **[SMPlayer](https://en.wikipedia.org/wiki/SMPlayer "wikipedia:SMPlayer")** — Reproductor multimedia Qt con características extra (Temas CSS, integración YouTube, etc.).

	[http://smplayer.sourceforge.net/](http://smplayer.sourceforge.net/) || [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **Xt7-Player** — Interfaz gráfica de usuario para MPlayer escrita en Gambas, con una enorme lista de características.

	[http://xt7-player.sourceforge.net/xt7forum/](http://xt7-player.sourceforge.net/xt7forum/) || [xt7-player](https://aur.archlinux.org/packages/xt7-player/)

## Integración en Navegadores

Si desea que MPlayer controle la reproducción de vídeos en su navegador favorito, instale uno de los siguientes complementos para su navegador.

### Firefox

Hay disponible en los repositorios oficiales un complemento para Firefox con el paquete [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer).

**Nota:** Este depende de [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer), que proporciona un frontend completo para MPlayer.

### Konqueror

Un complemento para Konqueror puede ser obtenido en [AUR](/index.php/AUR "AUR") con el paquete [kmplayer](https://www.archlinux.org/packages/?name=kmplayer).

**Nota:** [kmplayer](https://www.archlinux.org/packages/?name=kmplayer) también proporciona un frontend completo para MPlayer.

### Chromium

El complemento [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer) para Firefox también funciona en [Chromium](/index.php/Chromium "Chromium").

## Configuración

Los archivos de configuración global del sistema están situados en `/etc/mplayer/`, mientras que los archivos de configuración local del usuario son almacenados en el directorio `~/.mplayer/`. Los archivos por defecto en `/etc/mplayer/` son:

*   `codecs.conf` - Contienen la configuración de códecs.
*   `example.conf` - Es un ejemplo de mplayer.conf, el cual no es creado automáticamente tras la instalación.
*   `input.conf` - Contienen la configuración de atajos del teclado.

En el directorio `~/.mplayer/` hay un archivo creado automáticamente con el nombre *config* destinado a contener las configuraciones por defecto para el usuario.

Véase también: [Example MPlayer configuration file](http://mplayerhq.hu/DOCS/man/en/mplayer.1.html#CONFIGURATION%20FILES), [mplayer(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mplayer.1).

### Atajos del teclado

Los atajos del teclado del sistema son configurados por medio de `/etc/mplayer/input.conf`. Los atajos del teclado personales son guardados en `~/.mplayer/input.conf`. Para una lista completa de atajos del teclado véase [mplayer(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mplayer.1).

Véase también: [XF86 keyboard symbols](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols)

## Tips and Tricks

## Continuación de reproducción automática

La [AUR](/index.php/AUR "AUR") contiene un elegante script en perl el cual autocontinuará desde el punto en el cual se detuvo la producción [mplayer-resumer](https://aur.archlinux.org/packages/mplayer-resumer/).

El uso es trivial: una simple llamada del script en el lugar de mplayer Ejemplo:

```
 $mplayer-resumer [opciones] [directorio/]archivo

```

Si el script es reiniciado con $tdiff (5 segundos por defecto) entonces borrará el archivo usado para mantener la posición del vídeo

**Justificación** Ver el 90% de un vídeo y se detienes hace que se vuelva al inicio otra vez a la siguiente vez que lo quiera ver. recuerda donde estabas en el vídeo y continuar en esa posición es de buen comportamiento del usuario. Por defecto, mplayer separa la información del código de tiempo que te dice donde estás en el vídeo en la duración de un segundo. Mpĺayer además implementa la función de buscar en la linea de comandos. Podemos usar esas funciones para escribir un control de mplayer que recordará la ultima posición del vídeo y continuar desde ahí para reproducirlo.

**Limitación de Diseño**

Si el archivo de vídeo es reproducido en un sistema de sólo lectura, o de otra forma, está en una locación en la que no se pueda escribir, la continuación fallará. Es porque la implementación actual usa un archivo paralelo al vídeo donde se almacena el código de tiempo.