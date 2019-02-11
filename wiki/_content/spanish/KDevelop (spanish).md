**Estado de la traducción**
Este artículo es una traducción de [KDevelop](/index.php/KDevelop "KDevelop"), revisada por última vez el **2019-01-11**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=KDevelop&diff=0&oldid=562728) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

*"[KDevelop](http://kdevelop.org/) es un IDE (Entorno de Desarrollo Integrado) de código abierto y gratuito para MS Windows, Mac OS X, Linux, Solaris y FreeBSD. Es un IDE ampliable con plugins, repleto de características para desarrollar en C/C++ y otros lenguajes de programación. Se basa en KDevPlatform y las librerías [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)") y [Qt](/index.php/Qt "Qt"), y está en desarrollo desde 1998."*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Plugins](#Plugins)
*   [2 Compilar plugins adicionales](#Compilar_plugins_adicionales)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 KDevCMakeManager](#KDevCMakeManager)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [kdevelop](https://www.archlinux.org/packages/?name=kdevelop).

### Plugins

Instale plugins para proporcionar el autocompletado y otras características específicas del lenguaje:

*   Para PHP, instale el paquete [kdevelop-php](https://www.archlinux.org/packages/?name=kdevelop-php)
*   Para Python, instale el paquete [kdevelop-python](https://www.archlinux.org/packages/?name=kdevelop-python)

## Compilar plugins adicionales

Se requiere el paquete KDevelop Parser Generator ([kdevelop-pg-qt](https://www.archlinux.org/packages/?name=kdevelop-pg-qt)) para compilar plugins adicionales. Los plugins no se compilarán si el paquete no se instala de antemano.

## Solución de problemas

### KDevCMakeManager

Asegúrese de que [cmake](https://www.archlinux.org/packages/?name=cmake) esté instalado si se muestra el siguiente error: "*Could not load project management plugin KDevCMakeManager*".