**Estado de la traducción**
Este artículo es una traducción de [Gnumeric](/index.php/Gnumeric "Gnumeric"), revisada por última vez el **2018-11-28**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Gnumeric&diff=0&oldid=557667) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Gnumeric](https://en.wikipedia.org/wiki/es:Gnumeric "wikipedia:es:Gnumeric") es una potente aplicación de hojas de cálculo que puede importar y exportar a varios formatos, incluyendo .csv, HTML, LaTeX, Lotus 1-2-3, OpenDocument Spreadsheet y Microsoft Excel.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [gnumeric](https://www.archlinux.org/packages/?name=gnumeric).

Las dependencias opcionales son [psiconv](https://www.archlinux.org/packages/?name=psiconv) (para el soporte de archivos Psion 5), [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) (para el soporte del complemento python) y [yelp](https://www.archlinux.org/packages/?name=yelp) (para ver el manual de ayuda).

## Consejos y trucos

Gnumeric respeta su [locale](/index.php/Locale_(Espa%C3%B1ol) "Locale (Español)") para el separador decimal numérico y lo usa para exportar, (por ejemplo, a archivos .csv) también. Por ejemplo

*   con una locale alemana `de`, un número se muestra como `0,5` *(coma)*,
*   con una locale inglesa `en`, un número se muestra como `0.5` *(punto)*.

Para iniciar Gnumeric con un locale diferente, ejecute

```
 LC_NUMERIC="en" gnumeric

```

## Véase también

*   [Página web oficial de Gnumeric](http://projects.gnome.org/gnumeric/)