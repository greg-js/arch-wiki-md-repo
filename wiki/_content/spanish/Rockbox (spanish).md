**Estado de la traducción**
Este artículo es una traducción de [Rockbox](/index.php/Rockbox "Rockbox"), revisada por última vez el **2018-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Rockbox&diff=0&oldid=545160) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Codecs (Español)](/index.php/Codecs_(Espa%C3%B1ol) "Codecs (Español)")
*   [FAT](/index.php/FAT "FAT")

[Rockbox](https://www.rockbox.org) es un firmware de reemplazo gratuito para reproductores de audio digital (reproductores de MP3). Sus mejoras incluyen soporte para casi todos los [codecs (Español)](/index.php/Codecs_(Espa%C3%B1ol) "Codecs (Español)"), configuraciones avanzadas de sonido, aplicaciones, utilidades y juegos.

**Sugerencia:** Rockbox a menudo puede instalarse junto con el firmware original.

## Contents

*   [1 Dispositivos compatibles](#Dispositivos_compatibles)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Utilidad Rockbox](#Utilidad_Rockbox)
    *   [2.2 Intalar Rockbox en el dispositivo](#Intalar_Rockbox_en_el_dispositivo)
        *   [2.2.1 Cargador de arranque](#Cargador_de_arranque)
*   [3 Copia de seguridad](#Copia_de_seguridad)

## Dispositivos compatibles

Compruebe si su dispositivo tiene un puerto Rockbox utilizable: [https://www.rockbox.org/](https://www.rockbox.org/).

## Instalación

### Utilidad Rockbox

La herramienta oficial para administrar Rockbox se puede [instalar](/index.php/Install "Install") con el paquete [rbutil](https://www.archlinux.org/packages/?name=rbutil). La [utilidad Rockbox](https://www.rockbox.org/wiki/RockboxUtility) puede instalar el cargador de arranque de reemplazo, el firmware principal y cualquier característica adicional, como tipos de letras, temas y aplicaciones.

### Intalar Rockbox en el dispositivo

El proyecto Rockbox tiene fantásticas instrucciones de instalación. Puede encontrarlos en [https://www.rockbox.org/manual.shtml](https://www.rockbox.org/manual.shtml).

#### Cargador de arranque

Se recomienda instalar el cargador de arranque utilizando la [#Utilidad Rockbox](#Utilidad_Rockbox). Para que la utilidad Rockbox detecte su reproductor, debe tener acceso de escritura al disco interno del reproductor.

**Sugerencia:** Como necesita acceso de escritura al disco del reproductor, puede dársela cuando lo [monte](/index.php/Mount "Mount"). Por ejemplo: `# mount -o uid=1000,gid=1000 /dev/sdb /mnt`.

## Copia de seguridad

La [#Utilidad Rockbox](#Utilidad_Rockbox) puede hacer copias de seguridad del dispositivo.