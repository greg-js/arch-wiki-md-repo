**Estado de la traducción**
Este artículo es una traducción de [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts"), revisada por última vez el **2019-04-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Microsoft_fonts&diff=0&oldid=570808) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Related articles

*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")
*   [Fonts (Español)](/index.php/Fonts_(Espa%C3%B1ol) "Fonts (Español)")
*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Java Runtime Environment Fonts](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")

Éste artículo explica cómo instalar las fuentes TrueType de Microsoft y emular la renderización de fuentes de Windows.

**Sugerencia:** Véase [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts") para alternativas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Utilizando fuentes de una partición de Windows](#Utilizando_fuentes_de_una_partición_de_Windows)
    *   [1.2 Extrayendo fuentes de un ISO de Windows](#Extrayendo_fuentes_de_un_ISO_de_Windows)
    *   [1.3 Paquetes actuales](#Paquetes_actuales)
    *   [1.4 Legado de paquetes](#Legado_de_paquetes)
*   [2 Reglas de Fontconfig útiles para MS Fonts](#Reglas_de_Fontconfig_útiles_para_MS_Fonts)
*   [3 Windows 8](#Windows_8)

## Instalación

### Utilizando fuentes de una partición de Windows

Si hay una partición de Windows montada, sus fuentes pueden ser usadas enlanzádolas.

**Nota:** Los usuarios de [google-chrome](https://aur.archlinux.org/packages/google-chrome/) deberían optar por copiar ya que las fuentes enlazadas causan que Chrome se bloquee.

Por ejemplo, si la partición C:\ Windows está montada en `/windows`:

```
# ln -s /windows/Windows/Fonts /usr/share/fonts/WindowsFonts

```

Después regenere la caché de fontconfig:

```
# fc-cache -f

```

Alternativamente, copie las fuentes de Windows a `/usr/share/fonts`:

```
# mkdir /usr/share/fonts/WindowsFonts
# cp -r /windows/Windows/Fonts/ /usr/share/fonts/WindowsFonts
# chmod 755 /usr/share/fonts/WindowsFonts/*

```

Después regenere la caché de fontconfig:

```
# fc-cache -f

```

### Extrayendo fuentes de un ISO de Windows

Las fuentes también pueden ser encontradas en un archivo ISO de Windows. El formato del archivo de imagen que contiene las fuentes en el ISO es ya sea WIM (*Windows Imaging Format*) si el ISO es descargado en línea o ESD (*Windows Electronic Software Download*) si está creado con *Media Creation Tool* de Windows. Extraiga el `sources/install.esd` o el archivo `sources/install.wim` del *.iso* y busque un directorio `Windows/Fonts` dentro del archivo. Puede ser extraído usando *7z* (en [p7zip](/index.php/P7zip_(Espa%C3%B1ol) "P7zip (Español)")) o *wimextract* (en [wimlib](https://www.archlinux.org/packages/?name=wimlib)). Vea un ejemplo a continuación usando *7z*:

```
$ 7z e *Win10_1709_English_x64.iso* sources/install.wim
$ 7z e install.wim 1/Windows/{Fonts/"*".{ttf,ttc},System32/Licenses/neutral/"*"/"*"/license.rtf} -ofonts/

```

Las fuentes y la licencia se ubicarán en el directorio `fonts`.

### Paquetes actuales

**Nota:** Éstos paquetes **requieren acceso** a una instalación o medio de instalación de **Windows 7/8/10 y/o uno de Office 2007**, consulte el correspondiente [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") para detalles.

*   [ttf-office-2007-fonts](https://aur.archlinux.org/packages/ttf-office-2007-fonts/) — Office 2007 fonts
*   [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/) — Windows 7 fonts
*   [ttf-ms-win8](https://aur.archlinux.org/packages/ttf-ms-win8/) — Windows 8.1 fonts
*   [ttf-ms-win10](https://aur.archlinux.org/packages/ttf-ms-win10/) — Windows 10 fonts

### Legado de paquetes

**Nota:** Las fuentes proporcionadas por estos paquetes están desactualizadas y les faltan instrucciones de sugerencias modernas y juegos de caracteres completos. Se recomienda utilizar los paquetes anteriores.

[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) incluye:

*   [Andalé Mono](https://en.wikipedia.org/wiki/Andal%C3%A9_Mono "wikipedia:Andalé Mono")
*   [Arial](https://en.wikipedia.org/wiki/Arial "wikipedia:Arial")
*   [Arial Black](https://en.wikipedia.org/wiki/Arial_Black "wikipedia:Arial Black")
*   [Comic Sans](https://en.wikipedia.org/wiki/Comic_Sans "wikipedia:Comic Sans")
*   [Courier New](https://en.wikipedia.org/wiki/Courier_New "wikipedia:Courier New")
*   [Georgia](https://en.wikipedia.org/wiki/Georgia_(typeface) "wikipedia:Georgia (typeface)")
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) "wikipedia:Impact (typeface)")
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans")
*   [Lucida Console](https://en.wikipedia.org/wiki/Lucida_Console "wikipedia:Lucida Console")
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif")
*   ~~[Symbol](https://en.wikipedia.org/wiki/Symbol_(typeface) "wikipedia:Symbol (typeface)")~~
*   [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman "wikipedia:Times New Roman")
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS")
*   [Verdana](https://en.wikipedia.org/wiki/Verdana "wikipedia:Verdana")
*   [Webdings](https://en.wikipedia.org/wiki/Webdings "wikipedia:Webdings")
*   ~~[Wingdings](https://en.wikipedia.org/wiki/Wingdings "wikipedia:Wingdings")~~

**Advertencia:** De acuerdo al [original Contrato de Licencia para el Usuario Final de Microsoft](http://web.archive.org/web/20020227054122/www.microsoft.com/typography/fontpack/eula.htm), hay *algunas* limitaciones legales cuando se utilizan las fuentes anteriores.

También puede obtener [ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/) que, como es de esperar, contiene [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) "wikipedia:Tahoma (typeface)").

[ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/) incluye:

*   [Calibri](https://en.wikipedia.org/wiki/Calibri "wikipedia:Calibri")
*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) "wikipedia:Cambria (typeface)")
*   [Candara](https://en.wikipedia.org/wiki/Candara "wikipedia:Candara")
*   [Consolas](https://en.wikipedia.org/wiki/Consolas "wikipedia:Consolas")
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) "wikipedia:Constantia (typeface)")
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) "wikipedia:Corbel (typeface)")

## Reglas de Fontconfig útiles para MS Fonts

Frecuentemente los sitios web especifican las fuentes utilizando nombres genéricos (helvetica, courier, times o times new roman) una regla en fontconfig reemplaza éstas fuentes con fuentes libres (feas):

```
/etc/fonts/conf.d/30-metric-aliases-free.conf

```

para hacer uso completo de las fuentes MS es necesario crear una regla que mapee esos nombres genéricos a las fuentes específicas de MS contenidas en los distintos paquetes anteriores:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
       <alias binding="same">
         <family>Helvetica</family>
         <accept>
         <family>Arial</family>
         </accept>
       </alias>
       <alias binding="same">
         <family>Times</family>
         <accept>
         <family>Times New Roman</family>
         </accept>
       </alias>
       <alias binding="same">
         <family>Courier</family>
         <accept>
         <family>Courier New</family>
         </accept>
       </alias>
</fontconfig>

```

También es útil asociar las fuentes serif,sans-serif,monospace en su navegador favorito a las fuentes MS.

## Windows 8

El paquete dividido [ttf-ms-win8](https://aur.archlinux.org/packages/ttf-ms-win8/) pretende ser un reemplazo más actualizado para [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/), [ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/) y [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/).

Aunque proporciona versiones recientes de las fuentes, **no puede descargar las fuentes automáticamente** debido a problemas de licencias.

**Nota:** el uso de las fuentes de Microsoft fuera de un sistema Windows está prohibido por EULA (aunque en ciertos países EULA es inválido). Por favor consulte la licencia de Microsoft antes de usar las fuentes.

Puede obtener fuentes desde un sistema Windows 8.1 instalado y totalmente actualizado. Cualquier edición de *Windows 8.1 build **Windows 8.1 6.3.9600.17238*** funcionará.

En el sistema Windows 8.1 instalado las fuentes son usualmente localizadas en `[%WINDIR%](http://technet.microsoft.com/en-us/library/hh825266.aspx)\Fonts` y el archivo de licencia es `[%SYSTEM32%](http://technet.microsoft.com/en-us/library/hh825266.aspx)\license.rtf`.

Necesita los archivos listados en el arreglo `source=()`. Colóquelos en el mismo directorio que éste archivo [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)"), luego ejecute [makepkg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)").

`makepkg --pkg ttf-ms-win8` creará solo el paquete de fuentes principales de Windows 8.1 que debería cubrir incluso más que [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).