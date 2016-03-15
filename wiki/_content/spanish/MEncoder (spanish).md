Ésta tarea es relativamente sencillla. Lo primero es instalar mplayer (con mencoder):

```
 pacman -S mplayer

```

Ahora, en el directorio dónde está guardado el archivo RMVB ejecutamos la siguiente orden:

```
 mencoder entrada.rmvb -oac mp3lame -lameopts preset=128 -ovc xvid -xvidencopts bitrate= 1200 -ofps 25 -of avi -o salida.avi

```

Dónde "entrada.rmvb" es el nombre del archivo a convertir y "salida.avi" es el nombre que le vamos a asignar al archivo convertido.

El tiempo de conversión depende del hardware dónde se encuentre corriendo. Para un para un procesador de 1.7 mhz tarda aproximadamente un poco menos que lo que dura el video que queremos convertir.

Utilizando los parámetros especificados, crea un archivo AVI para reproducir en aparatos de DVD caseros que soportan ésa característica.