**Estado de la traducción**
Este artículo es una traducción de [YEd](/index.php/YEd "YEd"), revisada por última vez el **2018-12-02**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=YEd&diff=0&oldid=558156) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[yEd](http://www.yworks.com/en/products_yed_about.html) es un potente editor de gráficos, escrito en Java, que se puede usar para generar diagramas. Los diagramas pueden crearse manualmente o importarse a partir de datos externos para su análisis. Un algoritmo de diseño automático organiza los conjuntos de datos en caso de ser necesario.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [yed](https://aur.archlinux.org/packages/yed/), el cual está disponible en el [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"). Requiere un Java runtime environment instalado, como [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) o [jre](https://aur.archlinux.org/packages/jre/).

Una vez instalado, yEd se puede ejecutar utilizando el comando `yed`.

## Consejos y trucos

### Problemas con las fuentes

Si tiene problemas con las fuentes, como por ejemplo [fuentes defectuosas](http://i.imgur.com/mcvU014.png), pruebe a utilizar el runtime propietario [jre](https://aur.archlinux.org/packages/jre/) en lugar de OpenJDK y agregue la siguiente línea al archivo rc de su shell :

```
export _JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=lcd_hrgb'

```