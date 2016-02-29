## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Instalación mediante el paquete git](#Instalaci.C3.B3n_mediante_el_paquete_git)
*   [3 Uso General](#Uso_General)
*   [4 Configuración](#Configuraci.C3.B3n)
*   [5 Barra de estado](#Barra_de_estado)
*   [6 Recursos](#Recursos)

## Introducción

[WMFS2](http://wmfs.info/) (Window Manager From Scratch)es la segunda version de este gestor dinámico de ventanas en mosaico totalmente re escrito

## Instalación

Encontramos en [AUR](/index.php/AUR "AUR") el paquete [wmfs2-git](https://aur.archlinux.org/packages/wmfs2-git/) facilmente instalable mediante el [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") o mediante un [AUR-Helper](/index.php/AUR_helpers "AUR helpers").

Instalando WMFS2 con ayuda de yaourt:

```
$ yaourt -S wmfs2-git

```

Una vez instalado creamos una carpeta en nuestro $HOME donde guardaremos el archivo de configuración de WMFS2 para facilitar su configuración de una forma segura.

```
$ mkdir -p ~/.config/wmfs

```

copiamos el archivo de configuración `wmfsrc` a la carpeta que hemos creado en nuestro $HOME

```
$ cp /etc/xdg/wmfs/wmfsrc ~/.config/wmfs/

```

### Instalación mediante el paquete git

```
$ git clone [git://github.com/xorg62/wmfs.git](git://github.com/xorg62/wmfs.git)
$ cd wmfs
$ ./configure -h
$ ./configure
$ make
$ sudo make install
$ mkdir -p ~/.config/wmfs
$ cp wmfsrc ~/.config/wmfs/

```

Para usar WMFS2 como su gestor de ventanas por defecto, añadalo a su `.xinitrc`:

```
$ echo "exec wmfs" >> ~/.xinitrc

```

## Uso General

Iniciar el launcher: `Super`+`p`

El launcher es un promt que se inicia en la barra y que nos permitira lanzar nuestras aplicaciones. El launcher tiene la capacidad de autocompletar el comando de la aplicacion a lanzar mediante el tabulador.

Salir del entorno: `Ctrl`+`Alt`+`q`

Recargar el entorno: `Ctrl`+`Alt`+`r`

Manejar una ventana en modo FREE: `Super`+`f`

Esta modalidad nos permite usar de la forma tradicional de los window manager una ventana.

## Configuración

La configuración de WMFS2 se realiza desde el archivo `wmfsrc` que hemos ubicado en nuestro `$HOME`, el cual es un archivo de texto fácilmente comprensible.

Cuando se realicen cambios en el `wmfsrc` es conveniente hacerlos de forma gradual. Haga pequeños cambios en el `wmfsrc` y recargue el entorno mediante la combinación de teclas por defecto `Ctrl`+`Alt`+`r` para poder observar el cambio hecho al entorno y en caso de no ser un cambio grato poder regresar al estado anterior sin mayor complicación.

Para crear un combinación de teclas personalizado para lanzar una aplicación determinada podemos añadirla en la sección `[keys]` de nuestro `wmfsrc` ejemplo:

```
[key] mod = {"Super"} key = "b" func = "spawn" cmd = "firefox [/key]

```

En esta combinación de teclas definimos que nuestra tecla modificadora **(mod)** sea *“super”*, nuestra tecla para completar la combinación **(key)** seria *“b”*, nuestra función **(spawn)** seria lanzar una aplicación y el elemento a lanzar **(cmd)** seria *firefox* en este caso.

Si deseamos lanzar aplicaciones al inicio del entorno podemos añadir la aplicaciones a iniciar a nuestro `.xinitrc` o crear un script de bash como un autostart.sh y encanalarlo para ser lanzado por el `.xinitrc`

## Barra de estado

La barra de estado puede mostrarnos información especifica como es el uso del procesador, de la memoria, uso del disco, canción en reproducción entre otras. La información a mostrar puede ser proporcionada mediante un script de bash o mediante el uso de [conky](/index.php/Conky "Conky").

```
#!/bin/sh
#WMFS status.sh example file
TIMING=10
statustext()
{
     wmfs -c status "default `date`"
}
while true;
do
statustext
    sleep $TIMING
done

```

Este es un script de bash muy básico que solamente nos mostrara información como la fecha y la hora en nuestra barra de estado.

Para que este bash script se ejecute lo encanalamos en nuestro archivo `.xinitrc` o en nuestro script de bash

Para usar [conky](/index.php/Conky "Conky") se agrega la linea correspondiente al `.xinitrc` o a nuestro script de bash

```
conky -c ~/.conkyrc | while true; read line; do wmfs -c status "default $line"; done &

```

## Recursos

*   [Configuración de la Barra de Estado](https://github.com/xorg62/wmfs/wiki/statusbar)(Ingles)
*   [Configuraciones de Usuarios](https://github.com/xorg62/wmfs/wiki/Users-config) (Ingles)
*   [Tips y Trucos para WMFS2](https://github.com/xorg62/wmfs/wiki/bonus) (Ingles)
*   [WMFS](http://wmfs.info/) Página web
*   #wmfs en Freenode