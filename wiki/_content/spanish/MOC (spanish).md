Artículos relacionados

*   [mpd](/index.php/Mpd "Mpd")

**M**usic **O**n **C**onsole (moc) es un reproductor de música para ncurses liviano y poderoso. Similar a [mpd](/index.php/Mpd "Mpd"), presenta un servidor (moc) y a la vez un cliente (mocp). Tiene una estructura análoga la del administrador de archivos [Midnight Commander](http://www.midnight-commander.org), donde prodrá navegar su disco duro en un panel, y su lista de reproducción en el otro.

Soporta ALSA, OSS y JACK, es altamente configurable, permite reproducir formatos como mp3, Ogg, Vorbis, FLAC, Musepack, Speex, WAVE, AIFF, AU, y otros menos conocidos. También soporta listas de reproducción (como `m3u`). Otras características de moc es que nos brinda la posibilidad de elegir de esquemas de colores, personalizar todos los atajos del teclado, crear listas reproducción y más. Para mayor información puede ver la [página oficial](http://moc.daper.net/about).

## Contents

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
*   [3 Uso](#Uso)
*   [4 Atajos de teclado](#Atajos_de_teclado)
*   [5 Cerrando moc](#Cerrando_moc)
*   [6 Recursos adicionales](#Recursos_adicionales)

# Instalación

Instalamos utilizando pacman:

```
# pacman -S moc

```

# Configuración

Si desea configurar moc para utilizar OSS v4.1 rediríjase a éste [article](/index.php/OSS "OSS").

# Uso

Para iniciar moc escribimos:

```
$ mocp

```

Para comenzar la reproducción de archivos, simplemente busque en el panel de la izquierda el directorio que contenga la música que desee escuchar. Apretando Enter se reproducirá de a una canción por vez, puede agregar canciones a la lista de reproducción pulsando `a`, o agregar una lista de reproducción (como ser `.m3u`) o un directorio en forma recursiva pulsando `A`. Para detener la reproducción utilice la tecla `s`, para pausar la tecla `p` o `espacio`. Para borrar un ítem de la lista de reproducción presione `d`, para borrar toda la lista de reproducción pulse `C` (nótese la capitalización en la letra C).

# Atajos de teclado

Aqui algunos de los atajos de teclado. Tenga en cuenta que deben ser respetadas las mayúsculas y minúsculas, así como también la posibilidad de re definir todos los atajos:

| Comenzar la reproducción | enter |
| Detener la reproducción | s |
| Pausar la reproducción | p |
| Pausar la reproducción | espacio |
| Reproducir el próximo ítem de la lista | n |
| Reproducir el ítem anterior en la lista | b |
| Reproducir la lista en orden aleatorio | S |
| Repetir la lista de reproducción en un bucle | R (la reproducció secuencial debe estar deshabilitada) |
| Reproducir la lista en orden secuencial | X |
| Reproducir un archivo desde Internet | o |
| Desplaza el ítem seleccionado de la lista hacia arriba | u |
| Desplaza el ítem seleccionado de la lista hacia arriba | j |
| Agrega una dirección URL a la lista de reproducción | Ctrl+u |
| Permite realizar una búsqueda rápida en las canciones | g |
| Permite realizar una búsqueda rápida en las canciones | / |
| Refresca el directorio | r |
| Cambia al menú de selección de esquemas de colores | T |
| Cambia el modo de mostrar los títulos de las canciones | f |
| Permite cambiar de un panel al otro | TAB |
| Permite mostrar sólo el panel de archivos o la lista de reproducción | l |
| Muestra el path completo en la lista de reproducción | P |
| Permite mostrar los archivos oculos | H |
| Permite mostrar la duración de la canción | Ctrl-t |
 Ctrl-f |
| Agrega un archivo a la lista de reproducción | a |
| Agrega una lista de reproducción o un directorio en forma recursiva, a la lista de reproducción | A |
| Limpia la lista de reproducción | C |
| Guarda la lista de reproducción | V |
| Elimina de la lista de reproducción el archivo seleccionado | d |
| Disminuye el volumen en 1% | < |
| Disminuye el volumen en 5% | , |
| Aumenta el volumen en 1% | > |
| Aumenta el volumen en 5% | . |
| Lleva el volumen al 10~100% | Meta + 1~0 |
| Cierra la interfaz del cliente |
| Archivo de ayuda | ? |

# Cerrando moc

Es importante tener en cuenta que cuando cerramos moc con `q` sólo cerramos el cliente (mocp), el servidor (moc) queda corriendo y reproduciendo música (si es que lo estaba haciendo). Para cerrar completamente moc debemos escribir:

```
$ mocp -x

```

# Recursos adicionales

[Página oficial de moc](http://moc.daper.net/)