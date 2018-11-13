Audacious es un reproductor de audio libre y avanzada, basada en GTK +2\. Se centra en la calidad de audio y soporta una amplia variedad de codecs de audio, y es fácilmente extensible a través de plugins de terceros.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Interfaces](#Interfaces)
        *   [2.1.1 agregar skins de winamp](#agregar_skins_de_winamp)
    *   [2.2 reproducir audio de CD](#reproducir_audio_de_CD)
    *   [2.3 soporte para OSS](#soporte_para_OSS)
    *   [2.4 soporte para OSS4](#soporte_para_OSS4)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Audtool](#Audtool)
*   [4 Más recursos](#Más_recursos)

## Installation

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [audacious](https://www.archlinux.org/packages/?name=audacious) disponible desde los repositorios oficiales.

## Configuration

### Interfaces

**Note:** GTK + es ahora la interfaz por defecto en audacious 2.4 y versiones superiores.

Audacious 2 que actualmente dispone de dos interfaces:

*   Winamp interfaz clásica.
*   interfaz GTK.

Se puede cambiar entre las dos interfaces en Audacious.

#### agregar skins de winamp

agregar de pieles de Winamp para audacious es muy simple. Sólo tienes que copiar el archivo de la piel (zip, wsz, tgz, tar.gz o tar.bz2.....) A `/usr/share/audacious/Skins`, y entonces usted puede buscar y seleccionar desde la pestaña **Skinned Interface** en **Preferencias**.

### reproducir audio de CD

Primero, instala libcdio:

```
# pacman -S libcdio

```

Entonces, audacious prodra reproducir CDs de audio.

### soporte para OSS

cuando se utilice Open Sound System en lugar de ALSA, asegúrese que Audacious es el adecuado. En preferencias, pestaña de audio, seleccioné **OSS Output Plugin** ya que es el plugin para OSS.

### soporte para OSS4

Necesitas construir audacious-plugins desde [ABS](/index.php/ABS "ABS") y editar el PKGBUILD para añadir la opción '--enable-oss4' opción en el build() sección.

Después, en Audacious debes configurar Audacious Preferences -> Audio -> plugin de salida de corriente de 'OSS4 Output Plugin'.

## Tips and tricks

### Audtool

Audacious trae una potente herramienta de gestión llamada Audtool. Audtool se prodra usar para obtener informacion o controlar el reproductor.

Por ejemplo, para recuperar título de la canción o el artista actual, ejecute el siguiente comando:

```
$ audtool2 current-song
$ audtool2 current-song-tuple-data artist

```

También hay funciones para controlar la reproducción, manipular la lista de reproducción, ecualizador y la ventana principal. Para toda la lista de opciones, consulte:

```
$ audtool2 --help

```

## Más recursos

*   [Sitio Oficial de Audacious](http://audacious-media-player.org/)