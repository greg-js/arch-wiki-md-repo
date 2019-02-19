**Estado de la traducción**
Este artículo es una traducción de [Lout](/index.php/Lout "Lout"), revisada por última vez el **2019-02-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Lout&diff=0&oldid=566855) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Lout](http://savannah.nongnu.org/projects/lout) es un sistema de formato de documentos ligero inventado por Jeffrey H. Kingston. Lee una descripción de alto nivel de un documento similar en estilo a LaTeX y produce un PostScript.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [lout](https://www.archlinux.org/packages/?name=lout).

Para habilitar la impresión cirílica, las fuentes deben instalarse por separado (por ejemplo, [lout-dejavu](https://aur.archlinux.org/packages/lout-dejavu/)).

## Utilización

Lout solo admite codificación de un byte, por lo que se debe usar un mapa de caracteres específico en caso de que no se utilize entrada inglesa.

 `example.lout` 
```
@SysInclude {doc}
@SysInclude {dejavu}
@Document
  @InitialFont { DejaVuSerif Base 12p}
  @InitialLanguage { Russian }
@Text @Begin

@Display @Heading {Russian language example}

@LP
Параграф на русском языке.

@End @Text

```

Se puede utilizar [iconv](/index.php/Core_utilities_(Espa%C3%B1ol)#No_esenciales "Core utilities (Español)") para obtener la codificación requerida, antes de proporcionar código a Lout:

```
$ iconv -f utf-8 -t koi8-r example.lout example.koi8-r.lout
$ lout  example.koi8-r.lout example.ps

```

Se puede utilizar [Ps2pdf](/index.php/Ps2pdf "Ps2pdf") para convertir un archivo PostScript a PDF:

```
$ ps2pdf example.ps example.pdf

```

## Véase también

*   [Guía de usuario para el sistema de formato de documentos Lout](https://src.fedoraproject.org/repo/pkgs/lout/user-guide.pdf/10b5825ad7e3e9d801aab159bce41545/user-guide.pdf)
*   [Guía de experto para el sistema de formato de documentos Lout](https://src.fedoraproject.org/repo/pkgs/lout/expert-guide.pdf/6952736ef663234ad0585ac7de29ccd6/expert-guide.pdf)
*   [Wikipedia:Lout](https://en.wikipedia.org/wiki/Lout_(software) "wikipedia:Lout (software)")