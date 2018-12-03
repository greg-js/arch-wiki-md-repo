**Estado de la traducción**
Este artículo es una traducción de [Xephyr](/index.php/Xephyr "Xephyr"), revisada por última vez el **2018-12-01**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Xephyr&diff=0&oldid=491123) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

**Xephyr** es un servidor X anidado que se ejecuta como una aplicación X.

## Instalación

[xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr) está disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Instálelo con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

## Ejecución

Si desea ejecutar una ventana X anidada, necesita especificar una pantalla.

```
$ Xephyr -br -ac -noreset -screen 800x600 :1

```

Esto abrirá una nueva ventana Xephyr con una PANTALLA de ":1". Para iniciar una aplicación en esa ventana, necesita especificar esa pantalla.

```
$ DISPLAY=:1 xterm

```

Si quisiera iniciar otro WM, por ejemplo [spectrwm](/index.php/Spectrwm "Spectrwm"), escribiría:

```
$ DISPLAY=:1 spectrwm

```

También puede iniciar Xephyr con su [xinitrc](/index.php/Xinit_(Espa%C3%B1ol)#xinitrc "Xinit (Español)") usando startx:

```
 $ startx -- /usr/bin/Xephyr :1

```