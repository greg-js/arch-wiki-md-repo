## Flash y plugins de Java

Para instalar el reproductor de Flash y Java, escriba en una terminal

```
pacman -S flashplugin jre

```

_Tal vez necesite instalar ttf-ms-fonts_ (pacman -S ttf-ms-fonts) _para que el reproductor de flash enseñe el texto de forma apropiada._

## Adobe Reader

De acuerdo a los términos de la licencia, Adobe Reader no puede ser distribuido desde ningún repositorio normal de Arch. Hay una version disponible en AUR [aquí](https://aur.archlinux.org/packages.php?ID=16980). Si usted usa yaourt, escriba en una terminal:

```
yaourt -S --aur acroread

```

Hay varias localizaciones disponibles en varios idiomas, revise el AUR de su idioma.

```
yaourt -Ss --aur acroread-

```

Por favor note que no importa cuantos votos reciba este paquete, nunca será incluido en el repositorio community. Revisa el comentario hecho por Snowman [here](https://aur.archlinux.org/packages.php?ID=16980).

## Instalando Flash en Konqueror

```
pacman -S kmplayer

```

Ejecute kmplayer para asegurarse de que creó un archivo de configuración, ahora cierre kmplayer.Abra "~/.kde/share/config/kmplayerrc" con el editor de texto de su preferencia y añada esto hasta el final:

```
[application/x-shockwave-flash]
player=npp
plugin=/usr/lib/mozilla/plugins/libflashplayer.so

```

Revise si la linea del plugin esta correcta haciendo:

```
slocate libflashplayer.so

```

Si no esta correcta entonces cámbiele al lugar correcto del documento. Ejecute Konqueror y vaya a Opciones > Configurar Konqueror > Asociacion de archivos,navegue a "aplicacion/x-shockwave-flash" y haga click en la pestaña de "Embedding" y haga click en "add.." y seleccione "Embedded MPlayer for KDE" y haga click en "Ok". Asegúrese que "Embedded MPlayer for KDE" este hasta arriba. Click "Ok". Ahora deberia funcionar, si no lo hace, pruebe reiniciando konqueror y/o KDE.

Referencia: [http://mikearthur.co.uk/?p=171](http://mikearthur.co.uk/?p=171)

* * *