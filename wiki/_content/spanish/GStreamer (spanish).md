GStreamer es una plataforma multimedia basado en tubería (*«pipeline»*), escrito en lenguaje de programación C, con el sistema de tipos basado en GObject.

GStreamer permite a un programador crear una variedad de componentes multimedia manipulables, incluyendo reproducción de audio sencilla, reproducción de audio y vídeo, grabación, transmisión y edición. El diseño de la tubería sirve como base para crear muchos tipos de aplicaciones multimedia como editores de vídeo, emisoras de radiodifusión y reproductores multimedia.

Diseñado para ser multiplataforma, se sabe que funciona en Linux (x86, PowerPC y ARM), Solaris (Intel y SPARC), Mac OS X, Microsoft Windows y OS/400\. GStreamer tiene enlaces para lenguajes de programación como [Python](/index.php/Python "Python"), C++, Perl, GNU Guile ([guile](https://www.archlinux.org/packages/?name=guile)), y [Ruby](/index.php/Ruby "Ruby"). GStreamer es software libre, licenciado bajo GNU Lesser General Public License.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Complementos de la versión actual](#Complementos_de_la_versi.C3.B3n_actual)
    *   [1.2 Complementos de la versión antigua](#Complementos_de_la_versi.C3.B3n_antigua)
*   [2 Integración](#Integraci.C3.B3n)
    *   [2.1 PulseAudio](#PulseAudio)
    *   [2.2 Escritorios ligeros](#Escritorios_ligeros)
    *   [2.3 Integración en KDE / Phonon](#Integraci.C3.B3n_en_KDE_.2F_Phonon)
*   [3 Errores](#Errores)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Instale una versión de GStreamer desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"):

*   [gstreamer0.10](https://www.archlinux.org/packages/?name=gstreamer0.10) - Versión antigua y extensamente utilizada.
*   [gstreamer](https://www.archlinux.org/packages/?name=gstreamer) - Versión actual.

Para hacer a GStreamer más versátil, instale los paquetes de complementos que necesite.

### Complementos de la versión actual

*   [gst-libav](https://www.archlinux.org/packages/?name=gst-libav) - Complemento basado en libav que contiene muchos codificadores y decodificadores.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) - Complementos que necesitan más calidad, pruebas o documentación.
*   [gst-plugins-base](https://www.archlinux.org/packages/?name=gst-plugins-base) - Conjunto ejemplar de elementos esenciales.
*   [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) - Complementos de buena calidad bajo licencia LGPL.
*   [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) - Complementos de buena calidad que podrían plantear problemas de distribución.

### Complementos de la versión antigua

*   [gstreamer0.10-bad-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-bad-plugins) - Complementos que necesitan más calidad, pruebas o documentación.
*   [gstreamer0.10-base-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-base-plugins) - Conjunto ejemplar de elementos esenciales.
*   [gstreamer0.10-ffmpeg](https://www.archlinux.org/packages/?name=gstreamer0.10-ffmpeg) - Complemento basado en libav que contiene muchos codificadores y decodificadores.
*   [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) - Complementos de buena calidad bajo licencia LGPL.
*   [gstreamer0.10-good-plugins-slim](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins-slim/) - Complementos de buena calidad bajo licencia LGPL. Eliminada la dependencia de GNOME y ASCII-art.
*   [gstreamer0.10-ugly-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-ugly-plugins) - Complementos de buena calidad que podrían plantear problemas de distribución.
*   [gstreamer0.10-vaapi](https://aur.archlinux.org/packages/gstreamer0.10-vaapi/) - Soporte (Intel) para VAAPI. Véase más en [http://docs.gstreamer.com/display/GstSDK/Playback+tutorial+8%3A+Hardware-accelerated+video+decoding](http://docs.gstreamer.com/display/GstSDK/Playback+tutorial+8%3A+Hardware-accelerated+video+decoding).

## Integración

### PulseAudio

El soporte a [PulseAudio](/index.php/PulseAudio "PulseAudio") es proporcionado por los paquetes de complementos *good*.

### Escritorios ligeros

Para configurar GStreamer, por ejemplo, para cambiar el dispositivo de salida de audio, use *gstreamer-properties* del paquete [gnome-media](https://www.archlinux.org/packages/?name=gnome-media). Esto se puede ejecutar por cada usuario normal o, como administrador, para todos los usuarios. Los archivos de configuración de cada usuario están en `$HOME/.gconf/system/gstreamer`, y los archivos globales están en `/etc/gconf/gconf.xml.defaults`.

### Integración en KDE / Phonon

Véase [Phonon](/index.php/Phonon "Phonon").

## Errores

En caso del mensaje de error: `GStreamer-CRITICAL **: gst_mini_object_unref: assertion `mini_object->refcount > 0' failed`, que generalmente se produce durante la grabación de vídeo a través de software de grabación, instale [gstreamer0.10-ffmpeg](https://www.archlinux.org/packages/?name=gstreamer0.10-ffmpeg) para arreglarlo.

## Véase también

*   [Sound](/index.php/Sound_system_(Espa%C3%B1ol) "Sound system (Español)")
*   [http://gstreamer.freedesktop.org/](http://gstreamer.freedesktop.org/)