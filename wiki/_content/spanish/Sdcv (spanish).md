[Sdcv](https://dushistov.github.io/sdcv/) es un diccionario de línea de comandos. Proporciona acceso a los diccionarios en formato [StarDict](https://en.wikipedia.org/wiki/es:StarDict "wikipedia:es:StarDict").

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Utilización](#Utilizaci.C3.B3n)
*   [3 Añadir diccionarios](#A.C3.B1adir_diccionarios)
*   [4 Consejos](#Consejos)
    *   [4.1 Alias ​​sdcv](#Alias_.E2.80.8B.E2.80.8Bsdcv)
*   [5 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

[sdcv](https://www.archlinux.org/packages/?name=sdcv) está disponible en los repositorios oficiales.

## Utilización

[sdcv](https://www.archlinux.org/packages/?name=sdcv) se puede iniciar desde la línea de comando:

```
sdcv

```

Esto le da una línea de comando 'tipo shell' desde la que puede consultar la base de datos.

## Añadir diccionarios

Hay varios lugares en la web donde puede descargar diccionarios de StarDict, como por ejemplo [http://download.huzheng.org/](http://download.huzheng.org/)

Luego puede extraer los archivos en `/usr/share/stardict/dic`.

Si no tiene permisos de root, puede establecer la variable de entorno `STARDICT_DATA_DIR`. Una buena opción podría ser:

```
export STARDICT_DATA_DIR=$XDG_DATA_HOME

```

sdcv buscará en el subdirectorio `dic` así que asegúrese de que esté creado y coloque sus diccionarios dentro del mismo

Después de eso, debería estar listo

## Consejos

### Alias ​​sdcv

sdcv no es un nombre muy recomendable para un comando de terminal que probablemente usará mucho. Un buen nombre sería:

```
alias def="/usr/bin/sdcv"

```

## Véase también

*   [Página web oficial](http://sdcv.sourceforge.net/)
*   [Publicar en askubuntu.com](https://askubuntu.com/a/191268)