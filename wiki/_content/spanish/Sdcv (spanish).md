**Estado de la traducción**
Este artículo es una traducción de [Sdcv](/index.php/Sdcv "Sdcv"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Sdcv&diff=0&oldid=551752) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Sdcv](https://dushistov.github.io/sdcv/) es un diccionario de línea de comandos. Proporciona acceso a los diccionarios en formato [StarDict](https://en.wikipedia.org/wiki/es:StarDict "wikipedia:es:StarDict").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Añadir diccionarios](#Añadir_diccionarios)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Alias ​​sdcv](#Alias_​​sdcv)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [sdcv](https://www.archlinux.org/packages/?name=sdcv).

## Utilización

Ejecute la orden

```
sdcv

```

Esto le otorgará una línea de comandos 'tipo shell' desde la que puede consultar la base de datos.

## Añadir diccionarios

Hay varios lugares en la web donde puede descargar diccionarios de StarDict, como, por ejemplo, [http://download.huzheng.org/](http://download.huzheng.org/)

Posteriormente, extraiga los archivos en `/usr/share/stardict/dic`.

Si no tiene permisos de root, puede establecer la variable de entorno `STARDICT_DATA_DIR`. Una buena opción podría ser:

```
export STARDICT_DATA_DIR=$XDG_DATA_HOME

```

[sdcv](https://www.archlinux.org/packages/?name=sdcv) buscará en el subdirectorio `dic`, así que asegúrese de que esté creado y coloque sus diccionarios dentro del mismo.

## Consejos y trucos

### Alias ​​sdcv

sdcv no es un nombre muy recomendable para un comando de terminal que probablemente usará mucho. Un buen nombre sería:

```
alias def="/usr/bin/sdcv"

```

## Véase también

*   [Página web oficial](http://sdcv.sourceforge.net/)
*   [Publicar en askubuntu.com](https://askubuntu.com/a/191268)