**Estado de la traducción**
Este artículo es una traducción de [Mbrola](/index.php/Mbrola "Mbrola"), revisada por última vez el **2018-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Mbrola&diff=0&oldid=546275) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[mbrola](http://tcts.fpms.ac.be/synthesis/mbrola.html) es un programa no libre de [phonemas a audio](https://es.scribd.com/document/234749453/White-Paper-Demystifying-Speech-Recognition-by-Charles-Corfield-July2012) para usar con aplicaciones de texto a voz. Es de uso gratuito para aplicaciones no comerciales y no militares.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Añadir voces](#A.C3.B1adir_voces)
*   [2 Prueba](#Prueba)
*   [3 Instalar un programa de texto a fonemas](#Instalar_un_programa_de_texto_a_fonemas)
    *   [3.1 LLiaphon](#LLiaphon)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [mbrola](https://aur.archlinux.org/packages/mbrola/).

### Añadir voces

Los paquetes denominados *mbrola-voices-xxx* están disponibles en [AUR](https://aur.archlinux.org/packages.php?K=mbrola-voices)

**Nota:** Estos paquetes han sido creados por un script, por lo que si algo falla, deje un comentario para el encargado del paquete.

## Prueba

Una vez que haya instalado la(s) voz/voces deseada(s), vaya al directorio del idioma instalado:

```
$ cd /usr/share/mbrola/us1/

```

luego liste los archivos de prueba:

```
$ ls TEST/

```

Si no hay archivos de prueba para este idioma, intente con otro idioma o salte a [#Instalar un programa de texto a fonemas](#Instalar_un_programa_de_texto_a_fonemas).

De lo contrario elija un archivo de prueba (archivos con extensión .pho) e intente:

```
$ mbrola ./us1 ./TEST/mbrola.pho ~/test.wav; aplay ~/test.wav; rm ~/test.wav

```

Si la instalación funcionó bien, debería escuchar la voz ahora.

Tenga en cuenta que en esta prueba no le dimos un archivo de texto a *mbrola* sino un archivo de fonemas. Para convertirlo en un sistema de texto a voz, vea más abajo.

## Instalar un programa de texto a fonemas

Para obtener un sistema TTS completo necesitamos un programa de texto a fonemas compatible con mbrola: [Lista de programas TTS compatibles con mbrola](http://tcts.fpms.ac.be/synthesis/mbrola.html).

### LLiaphon

[LLiaPhon](http://gna.org/projects/lliaphon) es un programa de TTS que utiliza mbrola.

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [lliaphon](https://aur.archlinux.org/packages/lliaphon/).

Una vez que haya instalado ambos, pruebe esto:

```
$ export MBROLA_VOICE=/usr/share/mbrola/us1/us1;echo "Esto es una prueba."|lliaphon|play_ola

```