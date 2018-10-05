**Estado de la traducción**
Este artículo es una traducción de [Aspell](/index.php/Aspell "Aspell"), revisada por última vez el **2018-10-03**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Aspell&diff=0&oldid=545827) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Del [sitio web oficial](http://aspell.net/): "GNU Aspell es un corrector ortográfico libre y de código abierto diseñado para eventualmente reemplazar [Ispell](https://en.wikipedia.org/wiki/Ispell "wikipedia:Ispell"). Se puede usar como una biblioteca o como un corrector ortográfico independiente."

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Utilización](#Utilizaci.C3.B3n)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [3.1 Todo el texto está marcado como mal escrito](#Todo_el_texto_est.C3.A1_marcado_como_mal_escrito)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el [diccionario aspell](https://www.archlinux.org/packages/?sort=&q=aspell-) para el idioma que necesite. Al hacerlo, también se incluirá el paquete [aspell](https://www.archlinux.org/packages/?name=aspell) como una dependencia.

## Utilización

Muchos programas utilizan *aspell* automáticamente y no necesitan más configuración. Adicionalmente se puede utilizar *aspell* manualmente. Aquí hay algunos usos básicos. Véase [aspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aspell.1) para ampliar.

Para revisar la ortografía de un solo archivo:

```
$ aspell check *algúnarchivo*

```

A continuación aparecerá un indicador mostrando el texto del archivo. Desde allí puede seleccionar *aspell* para hacer correcciones a cada palabra mal escrita que detecte, o puede optar por ignorar sus sugerencias. Las correcciones que realice se guardarán en el archivo.

Para listar las palabras mal escritas desde la entrada estándar:

```
$ cat *algúnarchivo* | aspell list

```

## Solución de problemas

### Todo el texto está marcado como mal escrito

Asegúrese de que tiene instalado el diccionario correcto. Si la instalación de los archivos del diccionario no resuelve el problema, es muy probable que sea un problema con `enchant`. Compruebe si hay archivos de diccionario conocidos:

 `$ aspell dicts` 
```
es
es_ES
...etc
```

Si su respectivo diccionario de idioma está en la lista, añádalo a `/usr/share/enchant/enchant.enchering`. En el ejemplo anterior, sería:

```
es_ES:aspell

```

## Véase también

*   [Documento de información de Aspell](http://aspell.net/man-html/index.html)
*   [Wikipedia:GNU Aspell](https://en.wikipedia.org/wiki/GNU_Aspell "wikipedia:GNU Aspell")