## Contents

*   [1 Descripción](#Descripción)
*   [2 Instalacion](#Instalacion)
*   [3 Activando Imágenes de álbum, Letras de canciones y tablaturas de guitarra](#Activando_Imágenes_de_álbum,_Letras_de_canciones_y_tablaturas_de_guitarra)
*   [4 Tocando CD de Audio](#Tocando_CD_de_Audio)
*   [5 Problemas Conocidos](#Problemas_Conocidos)
    *   [5.1 Barra de progreso se detiene en 0:00](#Barra_de_progreso_se_detiene_en_0:00)
    *   [5.2 "Playback error encountered! Configured audiosink bin0 is not working"](#"Playback_error_encountered!_Configured_audiosink_bin0_is_not_working")
    *   [5.3 Tocando Archivos desde carpetas compartidas por SMB](#Tocando_Archivos_desde_carpetas_compartidas_por_SMB)

# Descripción

[Exaile](http://www.exaile.org/) es un reproductor de musica escrito en python que usa el conjuto de herramientas GTK+. Exaile es liberado bajo la licencia[GPL](http://www.gnu.org/copyleft/gpl.html). Las Caracteristicas que incluye son:

*   Obtencion de Letras de canciones, Caratulas de álbum , información del álbum, artista y/o grupo desde wikipedia y partituras de las canciones

*   Pestañas de listas de Reproducción de música

*   Soporte para Ipod

*   Soporte para Last.fm

*   Directorio de búsqueda para SHOUTcast

*   Track blacklisting

# Instalacion

Exaile esta disponible en el repositorio oficial . Para que este disponible se debe activar el repositorio community, esto se logra en /etc/pacman.conf:

De esto:

```
#[community]
# Add your preferred servers here, they will be used first
#Include = /etc/pacman.d/community

```

A esto:

```
[community]
# Add your preferred servers here, they will be used first
 Include = /etc/pacman.d/community

```

Exaile puede ser instalado usando [Pacman](/index.php/Pacman "Pacman"):

```
pacman -S exaile

```

Si tu usas [ALSA](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)") y quieres usar alsasink en vez del que viene por default , se debe instalar el plugin gstreamer0.10-base-plugins:

```
pacman -S gstreamer0.10-base-plugins

```

Esto tambien resuelve un problema si no se escucha sonido alguno luego de la instalacion y ademas cuando se intenta reproducir varios sonidos de diversas fuentes.

# Activando Imágenes de álbum, Letras de canciones y tablaturas de guitarra

Mientras se instala Exaile via pacman va a instalar cualquier dependencia necesaria, 2 paquetes necesarios ([gnome-python-extras](https://www.archlinux.org/packages/search/?q=gnome-python-extras) & [libgtkhtml](https://www.archlinux.org/packages/search/?q=libgtkhtml)) van a ser necesario para activar las imagenes de albums , letras de canciones , tablaturas de guitarra y funciones de wiki en Exaile.

```
sudo pacman -S gnome-python-extras libgtkhtml

```

# Tocando CD de Audio

Exaile requiere el paquete 'python-cddb' para poder tocar cd's de audio. El paquete correcto para esto es el siguiente [cddb-py](https://aur.archlinux.org/packages.php?do_Details=1&ID=3717&O=0&L=0&C=0&K=cddb&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=ndcddb-py/).

# Problemas Conocidos

### Barra de progreso se detiene en 0:00

First, make sure there are no problems with your sound architecture ([ALSA](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)"), [OSS](/index.php/OSS "OSS"), etc.). And your *playback sink* in Exaile is set correctly. Try setting it to automatic first.

If you're trying to listen to an MP3 file, try playing an audio file encoded in a different format, such as .ogg or .flac. If these play correctly then try installing gstreamer-ugly.

```
pacman -S gstreamer0.10-ugly gstreamer0.10-ugly-plugins

```

### "Playback error encountered! Configured audiosink bin0 is not working"

If you're getting a message like this, or "Configured audiosink bin1 is not working" (or with another number after 'bin'), it may be because Flash is blocking the use of ALSA by Exaile. You can fix this by running

```
killall npviewer.bin

```

In certain cases (such as if a YouTube video has finished playing), Flash may be blocking the use of ALSA even if an 'npviewer.bin' process is not running. In that case, refreshing the offending page while using a Flash blocking browser extension should fix the problem.

### Tocando Archivos desde carpetas compartidas por SMB

Por desgracia, Exaile no soporta el protocolo para compartir de Samba Unfortunately, Exaile does NOT support smb protocol.