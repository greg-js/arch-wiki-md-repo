**Estado de la traducción**
Este artículo es una traducción de [DOSBox](/index.php/DOSBox "DOSBox"), revisada por última vez el **2018-11-11**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=DOSBox&diff=0&oldid=504003) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[DOSBox](http://www.dosbox.com/) es un emulador de DOS para ordenadores x86 que permite ejecutar juegos o programas antiguos DOS.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
*   [3 Utilización](#Utilización)
*   [4 Consejos](#Consejos)
*   [5 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [dosbox](https://www.archlinux.org/packages/?name=dosbox).

## Configuración

No es necesaria una configuración inicial. Sin embargo, el manual oficial de DOSBox menciona un archivo de configuración llamado `dosbox.conf`. Por defecto, ese archivo se encuentra en su carpeta `~/.dosbox`.

También puede crear un nuevo archivo de configuración por cada aplicación copiando `dosbox.conf` de `~/.dosbox` al directorio donde reside la aplicación de DOS y modificando la configuración en consecuencia. También puede crear un archivo de configuración automáticamente: simplemente ejecute `dosbox` sin ningún parámetro dentro de la carpeta de su aplicación deseada:

```
$ dosbox

```

Luego, en la pantalla DOS, escriba:

```
Z:\> config -wc dosbox.conf

```

El archivo de configuración `dosbox.conf` se guardará en el directorio actual. Realize los cambios que desee dependiendo de la configuración que necesite.

Las opciones de configuración se detallan en la wiki oficial de DosBox: [http://www.dosbox.com/wiki/Dosbox.conf](http://www.dosbox.com/wiki/Dosbox.conf).

## Utilización

Una sencilla forma de ejecutar DOSBox es colocar su juego de DOS (o sus archivos de configuración) en un directorio y luego ejecutar dosbox con la ruta del directorio adjunta. Por ejemplo:

```
$ dosbox ./nombre_carpeta/

```

Ahora debería tener una pantalla DOS cuyo directorio de trabajo es el especificado anteriormente. Desde allí, puede ejecutar los programas que desee:

```
C:\> SETUP.EXE

```

## Consejos

Si DOSBox captura el puntero de su ratón, use `Ctrl+F10` para liberarlo.

Para reproducir música, algunos juegos de DOS requieren un sintetizador [MIDI](/index.php/MIDI "MIDI") el cual DOSBox no emula. Sin embargo, DOSBox puede usar uno si hay alguno disponible. Se puede usar un sintetizador de software como [FluidSynth](/index.php/FluidSynth "FluidSynth") o [Timidity](/index.php/Timidity "Timidity") si su ordenador no tiene un sintetizador de hardware.

## Véase también

*   [http://www.dosbox.com/](http://www.dosbox.com/) - Página web oficial de DOSBox.
*   [http://www.abandonia.com/](http://www.abandonia.com/) - Abandonia: gran repositorio de juegos antiguos y abandonados de DOS.
*   [http://www.dosgames.com/](http://www.dosgames.com/) - DosGames.com: gran repositorio de juegos DOS.