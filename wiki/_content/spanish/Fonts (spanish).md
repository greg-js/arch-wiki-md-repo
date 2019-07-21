**Estado de la traducción**
Este artículo es una traducción de [Fonts](/index.php/Fonts "Fonts"), revisada por última vez el **2019-07-19**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Fonts&diff=0&oldid=577427) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Configuración de fuentes](/index.php/Font_configuration_(Espa%C3%B1ol) "Font configuration (Español)")
*   [Linux console#Fonts](/index.php/Linux_console#Fonts "Linux console")
*   [Java Runtime Environment fonts](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts")
*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")
*   [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts")

De [Fuentes del ordenador (En ingles)](https://en.wikipedia.org/wiki/Computer_font "wikipedia:Computer font"): "Una tipografía del ordenador (o fuente) es un archivo de datos electrónicos que contiene un conjunto de glifos, caracteres, o símbolos como dingbats."

Note que ciertas licencias de fuentes pueden imponer ciertas limitaciones legales.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Formatos de fuente](#Formatos_de_fuente)
    *   [1.1 Formato bitmap](#Formato_bitmap)
    *   [1.2 Formato de contorno](#Formato_de_contorno)
    *   [1.3 Otros Formatos](#Otros_Formatos)
*   [2 Instalación](#Instalación)
    *   [2.1 Pacman](#Pacman)
    *   [2.2 Crear un paquete](#Crear_un_paquete)
    *   [2.3 Instalación manual](#Instalación_manual)
    *   [2.4 Aplicaciones antiguas](#Aplicaciones_antiguas)
    *   [2.5 Advertencias sobre Pango](#Advertencias_sobre_Pango)
*   [3 Paquetes de fuente](#Paquetes_de_fuente)
    *   [3.1 Bitmap](#Bitmap)
    *   [3.2 Escritura latina](#Escritura_latina)
        *   [3.2.1 Familias](#Familias)
        *   [3.2.2 Mono espacio](#Mono_espacio)
        *   [3.2.3 Sans-serif](#Sans-serif)
        *   [3.2.4 Serif](#Serif)
        *   [3.2.5 Sin clasificación](#Sin_clasificación)
    *   [3.3 Escritura no latina](#Escritura_no_latina)
        *   [3.3.1 Escritura antigua](#Escritura_antigua)
        *   [3.3.2 Árabe](#Árabe)
        *   [3.3.3 Braille](#Braille)
        *   [3.3.4 Chino, japonés, coreano, vietnamita](#Chino,_japonés,_coreano,_vietnamita)
            *   [3.3.4.1 Pan-CJK](#Pan-CJK)
            *   [3.3.4.2 Chino](#Chino)
            *   [3.3.4.3 Japonés](#Japonés)
            *   [3.3.4.4 Coreano](#Coreano)
            *   [3.3.4.5 Vietnamita](#Vietnamita)
        *   [3.3.5 Cirílico](#Cirílico)
        *   [3.3.6 Griego](#Griego)
        *   [3.3.7 Hebreo](#Hebreo)
        *   [3.3.8 Índico](#Índico)
        *   [3.3.9 Camboyano](#Camboyano)
        *   [3.3.10 Mongol y tunguses](#Mongol_y_tunguses)
        *   [3.3.11 Persa](#Persa)
        *   [3.3.12 Tai–Kadai](#Tai–Kadai)
        *   [3.3.13 Tibeto-Burman](#Tibeto-Burman)
    *   [3.4 Emoji y símbolos](#Emoji_y_símbolos)
    *   [3.5 Matemáticas](#Matemáticas)
    *   [3.6 Fuentes de otros sistemas operativos](#Fuentes_de_otros_sistemas_operativos)
*   [4 Orden de fuentes alternativas con X11](#Orden_de_fuentes_alternativas_con_X11)
*   [5 Alias de fuente](#Alias_de_fuente)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 Listar todas las fuentes instaladas](#Listar_todas_las_fuentes_instaladas)
    *   [6.2 Listar las fuentes instaladas de un lenguaje particular](#Listar_las_fuentes_instaladas_de_un_lenguaje_particular)
    *   [6.3 Listar las fuentes instaladas de un caracter Unicode particular](#Listar_las_fuentes_instaladas_de_un_caracter_Unicode_particular)
    *   [6.4 Establecer la fuente del terminal sobre la marcha](#Establecer_la_fuente_del_terminal_sobre_la_marcha)
    *   [6.5 Caché específico de fuente de una aplicación](#Caché_específico_de_fuente_de_una_aplicación)
*   [7 Vea también](#Vea_también)

## Formatos de fuente

Muchos ordenadores que usan fuentes hoy en día están en un formato *mapa de bits* (bitmap) o en formato *contorno* (outline).

	Fuentes mapa de bits

	Consisten en una matriz de puntos o píxeles que representa la imagen de cada glifo en cada cara y tamaño.

	Fuentes de contorno o *vectoriales*

	Usa curvas de Bézier, instrucciones de dibujo y formulas matemáticas para describir cada glifo, que marcan el contorno del carácter en cualquier tamaño.

### Formato bitmap

*   [Distribución del formato mapa de bits (inglés)](https://en.wikipedia.org/wiki/Glyph_Bitmap_Distribution_Format "wikipedia:Glyph Bitmap Distribution Format") (BDF) por Adobe.
*   [Formato compilado portable (inglés)](https://en.wikipedia.org/wiki/Portable_Compiled_Format "wikipedia:Portable Compiled Format") (PCF) por Xorg.
*   [Fuentes de pantalla PC](https://en.wikipedia.org/wiki/PC_Screen_Font "wikipedia:PC Screen Font") (PSF) usado por el Kernel para las fuentes de la consola, no soportada por Xorg (la extension de los archivos Unicode PSF es `psfu`)

Estos formatos también pueden estar comprimidos. Vea [#Bitmap](#Bitmap) para ver las fuentes bitmap disponibles.

### Formato de contorno

*   [Fuentes PostScript](https://en.wikipedia.org/wiki/es:Tipo_de_letra_PostScript "wikipedia:es:Tipo de letra PostScript") por Adobe – con varios formatos, por ejemplo: Fuente ASCII de impresora (PFA) y fuente binaria de impresora (PFB)
*   [TrueType](https://en.wikipedia.org/wiki/es:TrueType "wikipedia:es:TrueType") por Apple y Microsoft (extensión: `ttf`)
*   [OpenType](https://en.wikipedia.org/wiki/es:OpenType "wikipedia:es:OpenType") por Microsoft, construido sobre TrueType (extensiones: `otf`, `ttf`)

Para la mayoría de casos, la diferencia técnica entre TrueType y OpenType puede ignorarse.

### Otros Formatos

La aplicación de composición, *Tex*, Y su software complementario, *Metafuente*, renderiza caracteres utilizando sus propios métodos. Algunas de estas extensiones utilizadas por estos dos programas son `*pk`, `*gf`, `mf` y `vf`.

[FontForge](https://fontforge.github.io/en-US/) ([fontforge](https://www.archlinux.org/packages/?name=fontforge)), un editor de fuentes, puede guardar fuentes en su propio formato basado en texto, `sfd`, base de datos de fuentes spline (*s*pline *f*ont *d*atabase).

El formato [SGV](https://www.w3.org/TR/SVG/text.html#FontsGlyphs) tiene también su propio método para describir fuentes.

## Instalación

Hay varios métodos para instalar fuentes.

### Pacman

Fuentes y colecciones de fuentes se pueden instalar con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") en repositorios habilitados.

Las fuentes disponibles se pueden encontrar [buscando paquetes](/index.php/Pacman_(Espa%C3%B1ol)#Consultar_la_base_de_datos_de_los_paquetes "Pacman (Español)") (Por ej. `font` o `ttf`).

### Crear un paquete

Debería dejar a pacman la habilidad de manejar sus fuentes, que se hace creando un paquete de Arch. Este se puede compartir con la comunidad en el [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"). Los paquetes para instalar fuentes son particularmente similares; simplemente tome un [paquete](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/adobe-source-code-pro-fonts) como plantilla que debería funcionar bien. Para aprender como se modifica para su fuente vea [Creando paquetes](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)").

El nombre de familia de un archivo de fuente se puede adquirir utilizando `fc-query` por ejemplo: `fc-query -f '%{family[0]}
' /path/to/file`. El formato se describe en el manual FcPatternFormat(3).

### Instalación manual

La forma recomendada para añadir fuentes al sistema que no están en los repositorios está descrito en [#Crear un paquete](#Crear_un_paquete). Esto le da a pacman la habilidad de quitar o actualizar después de un tiempo. De todas formas las fuentes también se pueden instalar manualmente.

Para instalar fuentes en todo el sistema (disponible para todos los usuarios), mueve la carpeta al directorio `/usr/share/fonts/`. Todos los usuarios tienen que poder leer el archivo, utilice [chmod](/index.php/Chmod "Chmod") para establecer los permisos correctos (es decir al menos `0444` para archivos y `0555` para carpetas). Para instalar las fuentes solo para un único usuario, utilice `~/.local/share/fonts` (`~/.fonts/` está obsoleto).

Para cargar las fuentes directamente en Xserver (lo contrario a utilizar un *servidor de fuentes*) el directorio recientemente añadido tiene que incluirse en la entrada FontPath. Esta entrada se localiza en la sección *Archivos* [de su archivo de configuración Xorg](/index.php/Xorg_(Espa%C3%B1ol)#Configuración "Xorg (Español)") (por ej. `/etc/X11/xorg.conf` o `/etc/xorg.conf`). vea [#Aplicaciones antiguas](#Aplicaciones_antiguas) para más detalles.

Después actualice la cache de fuente de fontconfig: (normalmente no es necesario ya que la librería de fontconfig lo hace)

```
$ fc-cache

```

### Aplicaciones antiguas

Con aplicaciones antiguas que no soportan fontconfig (por ej. Aplicaciones GTK+ 1.x, y `xfontsel`) se necesita crear el índice en el directorio de la fuente:

```
$ mkfontscale
$ mkfontdir

```

O incluir más de una carpeta con un comando:

```
$ for dir in /font/dir1/ /font/dir2/; do xset +fp $dir; done && xset fp rehash

```

O si la fuente está instalado en una sub-carpeta diferente dentro de por ej. `/usr/share/fonts`:

```
$ for dir in * ; do if [  -d  "$dir"  ]; then cd "$dir";xset +fp "$PWD" ;mkfontscale; mkfontdir;cd .. ;fi; done && xset fp rehash

```

Puede que a veces el servidor X puede fallar al cargar el directorio de las fuentes y necesites volver a escanear todos los archivos de `fonts.dir`:

```
# xset +fp /usr/share/fonts/misc # Informa al servidor X de los nuevos directorios
# xset fp rehash                # Fuerza un escaneo nuevo

```

Para comprobar que la o las fuentes están incluidas:

```
$ xlsfonts | grep fontname

```

**Nota:** Muchos paquetes configurarán automáticamente Xorg para utilizar la fuente sobre la instalación. Si este es el caso de su fuente este paso no es necesario.

También puede establecerse globalmente en `/etc/X11/xorg.conf` o `/etc/X11/xorg.conf.d`.

Aquí hay un ejemplo de la sección que ha de ser añadida a `/etc/X11/xorg.conf`. Añada o quite paths basado en los particulares requisitos de su fuente.

```
# Deje que X.Org conozca los directorios personalizados de fuente
Section "Files"
    FontPath    "/usr/share/fonts/100dpi"
    FontPath    "/usr/share/fonts/75dpi"
    FontPath    "/usr/share/fonts/cantarell"
    FontPath    "/usr/share/fonts/cyrillic"
    FontPath    "/usr/share/fonts/encodings"
    FontPath    "/usr/share/fonts/misc"
    FontPath    "/usr/share/fonts/truetype"
    FontPath    "/usr/share/fonts/TTF"
    FontPath    "/usr/share/fonts/util"
EndSection

```

### Advertencias sobre Pango

Cuando [Pango](http://www.pango.org/) se está utilizando en su sistema él leerá desde [fontconfig](http://www.freedesktop.org/wiki/Software/fontconfig) para saber de donde obtener las fuentes.

```
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='common'
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='latin'

```

Si usted ha visto errores similares y/o vee bloques en vez de caracteres en su aplicación necesita añadir las fuentes y actualizar font cache. En este ejemplo se utiliza la fuente [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) para mostrar la solución (después de una instalación exitosa del paquete) y ejecute como root para habilitarlo para todos los usuarios.

```
# fc-cache
/usr/share/fonts: caching, new cache contents: 0 fonts, 3 dirs
/usr/share/fonts/TTF: caching, new cache contents: 16 fonts, 0 dirs
/usr/share/fonts/encodings: caching, new cache contents: 0 fonts, 1 dirs
/usr/share/fonts/encodings/large: caching, new cache contents: 0 fonts, 0 dirs
/usr/share/fonts/util: caching, new cache contents: 0 fonts, 0 dirs
/var/cache/fontconfig: cleaning cache directory
fc-cache: succeeded

```

Puedes comprobar si una fuente por defecto está configurada como tal:

```
# fc-match
LiberationMono-Regular.ttf: "Liberation Mono" "Regular"

```

## Paquetes de fuente

Esta es una lista selectiva que incluye muchos paquetes de fuentes del [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") junto con los repositorios oficiales. Las fuentes que tiene soporte Unicode están estiquetadas con "Unicode", vea el proyecto o la Wikipedia para más detalles.

El [script Archfonts Python](https://github.com/ternstor/distrofonts) se puede utilizar para generar una visión general de todas las fuentes TTF encontradas en los repositorios oficiales / AUR (la generación de la imagen está hecha utilizando [ttf2png](https://aur.archlinux.org/packages/ttf2png/)).

### Bitmap

*   Por defecto 8x16.
*   [Dina](http://www.dcmembers.com/jibsen/download/61/) ([dina-font](https://www.archlinux.org/packages/?name=dina-font)) – 6pt, 8pt, 9pt, 10pt, mono espaciado , basada en Proggy.
*   [Efont](http://openlab.jp/efont/unicode/) ([efont-unicode-bdf](https://aur.archlinux.org/packages/efont-unicode-bdf/)) – 10px, 12px, 14px, 16px, 24px, normal, negrita y itálica.
*   [Gohu](http://font.gohu.org/) ([gohufont](https://aur.archlinux.org/packages/gohufont/)) – 11px, 14px, normal y negrita.
*   [Lime](http://artwizaleczapka.sourceforge.net/) ([artwiz-fonts](https://aur.archlinux.org/packages/artwiz-fonts/)).
*   [ProFont](http://tobiasjung.name/profont/) ([ttf-profont-iix](https://aur.archlinux.org/packages/ttf-profont-iix/)) – 10px, 11px, 12px, 15px, 17px, 22px, 29px, normal.
*   [Proggy](https://en.wikipedia.org/wiki/Proggy_programming_fonts "wikipedia:Proggy programming fonts") ([proggyfonts](https://aur.archlinux.org/packages/proggyfonts/)) – tiene diferentes variantes.
*   [Tamsyn](http://www.fial.com/~scott/tamsyn-font/) ([tamsyn-font](https://www.archlinux.org/packages/?name=tamsyn-font)).
*   [Terminus](http://terminus-font.sourceforge.net/) ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font)).
*   [Tewi](https://github.com/lucy/tewi-font) ([bdf-tewi-git](https://aur.archlinux.org/packages/bdf-tewi-git/)).
*   [Unifont](http://unifoundry.com/unifont.html) (Covetura Unicode [más extensa](https://en.wikipedia.org/wiki/Unicode_font#Comparison_of_fonts "wikipedia:Unicode font") que cualquier fuente) ([bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont)).

### Escritura latina

#### Familias

*   [Luxi fonts](https://en.wikipedia.org/wiki/Luxi_fonts "wikipedia:Luxi fonts") ([font-bh-ttf](https://www.archlinux.org/packages/?name=font-bh-ttf)) – Fuentes Luxi X.Org.
*   [Bitstream Vera](https://en.wikipedia.org/wiki/es:Bitstream_Vera "wikipedia:es:Bitstream Vera") ([ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera)) – serif, sans-serif, y mono espaciada.
*   [Courier Prime](https://quoteunquoteapps.com/courierprime/) ([ttf-courier-prime](https://aur.archlinux.org/packages/ttf-courier-prime/)) – Fuente alternativa Courier optimizada para las pantallas.
*   [Croscore fonts](https://en.wikipedia.org/wiki/es:Croscore_fonts "wikipedia:es:Croscore fonts") ([ttf-croscore](https://www.archlinux.org/packages/?name=ttf-croscore)) – Sustituto de Google para Arial de Window, Times New Roman, y Courier New.
*   [DejaVu](https://en.wikipedia.org/wiki/es:DejaVu "wikipedia:es:DejaVu") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) – Bitstream Vera modificado para una mayor cobertura de Unicode.
*   [Droid](https://en.wikipedia.org/wiki/es:Droid "wikipedia:es:Droid") ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid)) – Fuente por defecto de las versiones antiguas de Android.
*   [Roboto](https://en.wikipedia.org/wiki/es:Roboto "wikipedia:es:Roboto") ([ttf-roboto](https://www.archlinux.org/packages/?name=ttf-roboto)) – Fuente por defecto de las versiones nuevas de Android.
*   [Google Noto](https://en.wikipedia.org/wiki/es:Google_Noto "wikipedia:es:Google Noto") ([noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts)) – Unicode
*   [Liberation fonts](https://en.wikipedia.org/wiki/es:Liberation_fonts "wikipedia:es:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) – Fuente libre compatible con la métrica que sustituye las fuentes Arial, Arial Narrow, Times New Roman y Courier New encontradas en Windows y productos de Microsoft Office.
*   [Ubuntu](https://en.wikipedia.org/wiki/es:Ubuntu_(tipo_de_letra) ([ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family))
*   [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts") ([ttf-ms-win10](https://aur.archlinux.org/packages/ttf-ms-win10/)) – Fuentes de Windows 10.

Paquetes de fuentes licenciadas por Microsoft:

*   [Microsoft fonts](http://corefonts.sourceforge.net/) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)) – Andalé Mono, Courier New, Arial, Arial Black, Comic Sans, Impact, Lucida Sans, Microsoft Sans Serif, Trebuchet, Verdana, Georgia, Times New Roman
*   Vista fonts ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/)) – Consolas, Calibri, Candara, Corbel, Cambria, Constantia

#### Mono espacio

Para más fuentes mono espaciada vea [#Bitmap](#Bitmap) y [#Familias](#Familias).

*   [Anonymous Pro](http://www.marksimonson.com/fonts/view/anonymous-pro) ([ttf-anonymous-pro](https://www.archlinux.org/packages/?name=ttf-anonymous-pro), incluido en [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)).
*   [Envy Code R](https://damieng.com/blog/2008/05/26/envy-code-r-preview-7-coding-font-released) ([ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/)).
*   Fantasque Sans Mono ([ttf-fantasque-sans-mono](https://www.archlinux.org/packages/?name=ttf-fantasque-sans-mono), [otf-fantasque-sans-mono](https://www.archlinux.org/packages/?name=otf-fantasque-sans-mono)).
*   [Fira Mono](https://en.wikipedia.org/wiki/Fira_Sans "wikipedia:Fira Sans") ([ttf-fira-mono](https://www.archlinux.org/packages/?name=ttf-fira-mono), [otf-fira-mono](https://www.archlinux.org/packages/?name=otf-fira-mono)) – diseñado para Firefox OS.
*   [Fira Code](https://github.com/tonsky/FiraCode) ([ttf-fira-code](https://www.archlinux.org/packages/?name=ttf-fira-code), [otf-fira-code](https://www.archlinux.org/packages/?name=otf-fira-code)) – con ligaduras de programación.
*   [FreeMono](https://en.wikipedia.org/wiki/es:GNU_FreeFont "wikipedia:es:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont), [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts)) - Unicode.
*   [Hack](https://sourcefoundry.org/hack/) ([ttf-hack](https://www.archlinux.org/packages/?name=ttf-hack)) - fuente mono espaciada de código abierto, utilizada por defecto en KDE Plasma.
*   [Inconsolata](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata](https://www.archlinux.org/packages/?name=ttf-inconsolata), incluida en [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - inspirado por Consolas.
*   [Inconsolata-g](https://leonardo-m.livejournal.com/77079.html) ([ttf-inconsolata-g](https://aur.archlinux.org/packages/ttf-inconsolata-g/)) - añade algunas modificaciones familiares para el programador.
*   [Iosevka](https://be5invis.github.io/Iosevka/) ([ttf-iosevka](https://aur.archlinux.org/packages/ttf-iosevka/)) – Un esbelto tipo de letra sans-serif y slab-serif inspirado por Pragmata Pro, M+ y PF DIN Mono, diseñado para ser la fuente ideal para programar. Soporta ligaduras de programación y alrededor de 2000 glifos latinos, griegos, cirílicos, fonéticos y PowerLine.
*   [Lucida Typewriter](https://en.wikipedia.org/wiki/Lucida_Typewriter "wikipedia:Lucida Typewriter") (incluida en el paquete [jre](https://aur.archlinux.org/packages/jre/)).
*   [Menlo](https://en.wikipedia.org/wiki/Menlo_(typeface) (derivado: [ttf-meslo](https://aur.archlinux.org/packages/ttf-meslo/)) - fuente mono espaciada por defecto de OS X.
*   [Monaco](https://en.wikipedia.org/wiki/es:Monaco_(tipograf%C3%ADa) ([ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco/)) - fuente propietaria diseñada por Apple para OS X.
*   Monofur ([ttf-monofur](https://aur.archlinux.org/packages/ttf-monofur/))
*   [Mononoki](https://madmalik.github.io/mononoki) ([ttf-mononoki](https://aur.archlinux.org/packages/ttf-mononoki/))
*   [Source Code Pro](https://en.wikipedia.org/wiki/Source_Code_Pro "wikipedia:Source Code Pro") ([adobe-source-code-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-code-pro-fonts) incluido en [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))

Webs relevantes:

*   [Dan Benjamin's Top 10 fuentes de programación](http://hivelogic.com/articles/top-10-programming-fonts).
*   [Lista de fuentes de Trevor Lowing](http://www.lowing.org/fonts/) .
*   [Slant: ¿Cuales son las mejores fuentes de programación?](https://www.slant.co/topics/67/~what-are-the-best-programming-fonts).
*   [Stack Overflow: Fuentes recomendadas para programar](https://stackoverflow.com/questions/4689/recommended-fonts-for-programming).

#### Sans-serif

*   [Andika](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=andika) ([ttf-andika](https://aur.archlinux.org/packages/ttf-andika/)).
*   [FreeSans](https://en.wikipedia.org/wiki/es:GNU_FreeFont "wikipedia:es:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont), [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts)) - Unicode.
*   [Inter UI](https://github.com/rsms/inter) ([ttf-inter-ui](https://aur.archlinux.org/packages/ttf-inter-ui/)) – diseñada para las interfaces de usuario.
*   [Linux Biolinum](https://en.wikipedia.org/wiki/es:Linux_Libertine "wikipedia:es:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) – sustituto libre para Times New Roman.
*   [PT Sans](https://en.wikipedia.org/wiki/PT_Sans "wikipedia:PT Sans") ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - tres pricipales variantes: normal, estrecho, y subtítulo - Unicode: latín, cirílico.
*   [Source Sans Pro](https://en.wikipedia.org/wiki/Source_Sans_Pro "wikipedia:Source Sans Pro") ([adobe-source-sans-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-sans-pro-fonts))
*   [Tahoma](https://en.wikipedia.org/wiki/es:Tahoma "wikipedia:es:Tahoma") ([ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/))

#### Serif

*   [EB Garamond](http://www.georgduffner.at/ebgaramond/) ([otf-eb-garamond](https://aur.archlinux.org/packages/otf-eb-garamond/)).
*   [FreeSerif](https://en.wikipedia.org/wiki/es:GNU_FreeFont "wikipedia:es:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont), [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts)) - Unicode.
*   [Gentium](https://en.wikipedia.org/wiki/es:Gentium "wikipedia:es:Gentium") ([ttf-gentium](https://www.archlinux.org/packages/?name=ttf-gentium)) - Unicode: latín, griego cirílico, hebreo.
*   [Linux Libertine](https://en.wikipedia.org/wiki/es:Linux_Libertine "wikipedia:es:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) - Unicode: latín, griego cirílico, hebreo.

#### Sin clasificación

*   [ttf-cheapskate](https://aur.archlinux.org/packages/ttf-cheapskate/) - Coleccion de fuentes de *dustismo.com*.
*   [ttf-junicode](https://www.archlinux.org/packages/?name=ttf-junicode) - Fuente Junius que contiene casi todos los script y glifos medivales.
*   [ttf-mph-2b-damase](https://aur.archlinux.org/packages/ttf-mph-2b-damase/) - Cubre el primer plano completo y muchos scripts.
*   [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) - Conjuntos IBM Courier y Adobe Utopia del [tipo de letra PostScript](https://en.wikipedia.org/wiki/es:Tipo_de_letra_PostScript "wikipedia:es:Tipo de letra PostScript").
*   [all-repository-fonts](https://aur.archlinux.org/packages/all-repository-fonts/) - Meta paquete para todas las fuentes de los repositorios oficiales.
*   [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/) - una enorme colección de fuentes libres (incluye Ubuntu, Inconsolata, Roboto, etc.) - Nota: Su diálogo de fuentes puede ser muy grande ya que se añadirán más de cien fuentes.

### Escritura no latina

#### Escritura antigua

*   [ttf-ancient-fonts](https://aur.archlinux.org/packages/ttf-ancient-fonts/) - Fuentes que contienen simbolos Unicode para las escrituras egeo, egipcio, cuneiforme, anatolian, maya y analecta.

#### Árabe

*   [ttf-amiri](https://aur.archlinux.org/packages/ttf-amiri/) - Un tipo de letra clásico en Naskh, estilo pionero de Amiria Press.
*   [ttf-arabeyes-fonts](https://aur.archlinux.org/packages/ttf-arabeyes-fonts/) - Colección de fuentes árabes libres.
*   [ttf-qurancomplex-fonts](https://aur.archlinux.org/packages/ttf-qurancomplex-fonts/) - Fuentes de El complejo de impresión del gran Corán Rey Fahd en al-Madinah al-Munawwarah.
*   [ttf-sil-lateef](https://aur.archlinux.org/packages/ttf-sil-lateef/) - Fuente árabe Unicode desde SIL [SIL](https://en.wikipedia.org/wiki/es:SIL_International "wikipedia:es:SIL International").
*   [ttf-sil-scheherazade](https://aur.archlinux.org/packages/ttf-sil-scheherazade/) - Fuente árabe Unicode desde SIL. (Alternativa de la fuente árabe tradicional).

#### Braille

*   [ttf-ubraille](https://aur.archlinux.org/packages/ttf-ubraille/) - Fuente que contiene símbolos Unicode para el *braille*.

#### Chino, japonés, coreano, vietnamita

##### Pan-CJK

*   Fuentes adobe source han - Una gran colección de fuentes con un soporte comprensible de chino simplificado, chino tradicional, japones, y coreano, con un diseño y aspecto consistente.
    *   [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts) - Sans fonts.
    *   [adobe-source-han-serif-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-otc-fonts) - Serif fonts.

*   [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk) - Otra gran colección de fuentes con un soporte comprensible de chino simplificado, chino tradicional, japones, y coreano, con un diseño y aspecto consistente. Actualmente es una versión renombrada de [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts).

##### Chino

*   Fuentes adobe source han.
    *   [adobe-source-han-sans-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-cn-fonts) - Fuentes de chino simplificado OpenType/CFF Sans.
    *   [adobe-source-han-sans-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-tw-fonts) - Fuentes de chino tradicional OpenType/CFF Sans.
    *   [adobe-source-han-serif-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-cn-fonts) - Fuentes de chino simplificado OpenType/CFF Serif.
    *   [adobe-source-han-serif-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-tw-fonts) - Fuentes de chino tradicional OpenType/CFF Serif.

*   Fuentes noto, chino.
    *   [noto-fonts-sc](https://aur.archlinux.org/packages/noto-fonts-sc/) - Fuentes Noto CJK-SC para chino simplificado.
    *   [noto-fonts-tc](https://aur.archlinux.org/packages/noto-fonts-tc/) - Fuentes Noto CJK-TC para chino tradicional.

*   Fuentes wqy
    *   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) - La Familia tipográfica WenQuanYi Micro Hei (también conocida como Hei, Gothic o Dotum) es un estilo sans-serif derivado de Droid Sans Fallback, ofrece una gran calidad CJK y un gran contorno, además es extremadamente compacto (~5M).
    *   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) - Estilo Hei Ti (sans-serif) Contorno chino con incrustaciones con Bitmapped Song Ti (también soporta japonés (parcialmente) y caracteres coreanos).
    *   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont) - Fuente china Bitmapped Song Ti (serif).

*   Fuentes arficas.
    *   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai) - Fuente Unicode *kaiti* (trazos de pincel) (se sugiere habilitar anti-aliasing).
    *   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) - Fuente Unicode *mingti* (impresa).

*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts) - Fuente *New Sung*, anteriormente era el paquete ttf-fireflysung.

*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - Fuentes ttf chinas and vietnamitas.

*   Fuentes estándar del ministerio de educación de la república china en Taiwan.
    *   [ttf-tw](https://aur.archlinux.org/packages/ttf-tw/) - Fuentes chinas tradicionales Kai y Song del ministerio de educación de Taiwan.
    *   [ttf-twcns-fonts](https://aur.archlinux.org/packages/ttf-twcns-fonts/) Fuentes chinas TrueType por el ministerio de educación del gobierno de Taiwan, soporta el estándar CNS11643, incluido el tipo de letra kai y sung.

*   Fuentes chinas de Windows
    *   [ttf-ms-win8-zh_cn](https://aur.archlinux.org/packages/ttf-ms-win8-zh_cn/) - Fuentes de chino simplificado de windows 8.
    *   [ttf-ms-win8-zh_tw](https://aur.archlinux.org/packages/ttf-ms-win8-zh_tw/) - Fuentes de chino tradicional de windows 8.
    *   [ttf-ms-win10-zh_cn](https://aur.archlinux.org/packages/ttf-ms-win10-zh_cn/) - Fuentes de chino simplificado de windows 10.
    *   [ttf-ms-win10-zh_tw](https://aur.archlinux.org/packages/ttf-ms-win10-zh_tw/) - Fuentes de chino tradicional de windows 10.

*   [ttf-i.bming](https://aur.archlinux.org/packages/ttf-i.bming/) - Fuente CJK serif que enfatiza en un estilo de letra antiguo.

##### Japonés

*   [adobe-source-han-sans-jp-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-jp-fonts) - Fuentes japonesas OpenType/CFF.
*   [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont) - Conjunto de fuentes formales góticas japonesas (sans-serif) y mincho (serif); una fuente de código abierto de gran calidad. Fuente por defecto de openSUSE-ja.
*   [ttf-hanazono](https://www.archlinux.org/packages/?name=ttf-hanazono) - Una fuente libre japonesa kanji, estilo Mincho (serif).
*   [ttf-sazanami](https://www.archlinux.org/packages/?name=ttf-sazanami) - Una fuente libre japonesa TrueType. Esta estaba desactualizada y no se mantendrá más, pero varios entornos puede que tengan establecido esta fuente como fuente alternativa.
*   [ttf-koruri](https://aur.archlinux.org/packages/ttf-koruri/) - Fuente japonesa TrueType obtenida mezclando [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) y Open Sans.
*   [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/) - Fuente japonesa para ver [2channel Shift JIS art](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art") apropiadamente.
*   [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) - Fuente japonesa con un estilo gótico moderno en su contorno. Incluye todo de japonés hiragana/katakana, latín básico, latín-1 suplemento, latín extandido-A, extensiones IPA y la mayoría de kanji japonés, griego, cirílico, vietnamita con siete pesos (proporcional) o 5 pesos (mono espaciado).
*   [ttf-vlgothic](https://aur.archlinux.org/packages/ttf-vlgothic/) - Fuente gótica japonesa. Por defecto en los Linux Debian/Fedora/Vine.

##### Coreano

*   [adobe-source-han-sans-kr-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-kr-fonts) - Fuente coreana OpenType/CFF.
*   [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk) - Colección de fuentes coreanas TrueType.
*   [spoqa-han-sans](https://aur.archlinux.org/packages/spoqa-han-sans/) - Fuentes Han Sans personalizadas por Spoqa
*   [ttf-d2coding](https://aur.archlinux.org/packages/ttf-d2coding/) - Fuente D2Coding de ancho fijo TrueType hecho por Naver.
*   [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/) - Serie de fuentes Nanum TrueType.
*   [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) - Serie de fuentes Nanum TrueType de ancho fijo.
*   [ttf-kopub](https://aur.archlinux.org/packages/ttf-kopub/)/[otf-kopub](https://aur.archlinux.org/packages/otf-kopub/) - Fuente coreanas TrueType/OpenType por la sociedad de editores de Corea.
*   [ttf-kopubworld](https://aur.archlinux.org/packages/ttf-kopubworld/)/[otf-kopubworld](https://aur.archlinux.org/packages/otf-kopubworld/) - Fuentes plurilingües (coreano, yethangul, chino extendido, japonés, latín extendido, cirílico, árabe, hebreo, devanagari) TrueType/OpenType por la sociedad de editores de Corea.
*   [ttf-unfonts-core-ibx](https://aur.archlinux.org/packages/ttf-unfonts-core-ibx/) - Una colección de fuentes coreanas TrueType por KLDP.

##### Vietnamita

*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - Fuente vietnamita TrueType font para los caracteres chữ Nôm.

#### Cirílico

Vea también [#Escritura latina](#Escritura_latina)

*   [ttf-paratype](https://aur.archlinux.org/packages/ttf-paratype/) - Familia de fuente por ParaType: sans, serif, mono, cirílico extendido y latín, licencia OFL.
*   [otf-russkopis](https://aur.archlinux.org/packages/otf-russkopis/) - Una fuente libre cursiva OpenType para la escritura cirílica.

#### Griego

Casi todas las fuentes Unicode contienen el conjunto de caracteres griegos (politónico incluido). Estas fuentes adicionales puede que no tengan el conjunto completo de caracteres Unicode pero utiliza una gran calidad en los caracteres griegos (y en el latín, por supuesto).

*   [otf-gfs](https://aur.archlinux.org/packages/otf-gfs/) - Selección de fuentes de OpenType de la sociedad griega de fuentes.
*   [ttf-mgopen](https://aur.archlinux.org/packages/ttf-mgopen/) - Fuentes profesionales TrueType por Magenta.

#### Hebreo

*   [opensiddur-hebrew-fonts](https://aur.archlinux.org/packages/opensiddur-hebrew-fonts/) - Gran colección de fuentes hebreas con licencia de código abierto.
*   [culmus](https://aur.archlinux.org/packages/culmus/) - Una buena colección de fuentes hebreas libres.

#### Índico

*   [ttf-freebanglafont](https://aur.archlinux.org/packages/ttf-freebanglafont/) - Fuente para bangla.
*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf) - Colección de fuentes índicas OpenType (contiene ttf-freebanglafont), proporciona el carácter [U+0CA0](http://www.fileformat.info/info/unicode/char/ca0/index.htm) "ಠ".
*   [lohit-fonts](https://aur.archlinux.org/packages/lohit-fonts/) - Fuentes índicas TrueType del proyecto Fedora (contiene Fuentes Oriya y más).
*   [ttf-devanagarifonts](https://aur.archlinux.org/packages/ttf-devanagarifonts/) - Fuentes TrueType devanagaries (contiene 283 tipos de letra).
*   [ttf-gurmukhi-fonts_sikhnet](https://aur.archlinux.org/packages/ttf-gurmukhi-fonts_sikhnet/) - Fuentes TrueType gurmujíes (gurbaniwebthick,prabhki).
*   [ttf-gurmukhi_punjabi](https://aur.archlinux.org/packages/ttf-gurmukhi_punjabi/) - TTF gurmujíes / panyabí (contiene 252 tipos de letra).
*   [ttf-gujrati-fonts](https://aur.archlinux.org/packages/ttf-gujrati-fonts/) -Fuentes TTF guyaratíes (Avantika,Gopika,Shree768).
*   [ttf-kannada-font](https://aur.archlinux.org/packages/ttf-kannada-font/) - canarés, lengua del estado Karnataka en India.
*   [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/) - Fuentes Unicode cingalés.
*   [ttf-tamil](https://aur.archlinux.org/packages/ttf-tamil/) - Fuentes Unicode tamil.
*   [ttf-urdufonts](https://aur.archlinux.org/packages/ttf-urdufonts/) - Fuentes urdu (Jameel Noori Nastaleeq (+kasheeda), Nafees Web Naskh, PDMS Saleem Quran) y configuración para establecer Jameel Noori Nastaleeq como fuente por defecto para urdu.
*   [fonts-smc-malayalam](https://aur.archlinux.org/packages/fonts-smc-malayalam/) - Fuentes Unicode malabar lanzadas por 'Swathanthra Malayalam Computing' (contiene 11 tipos de letra).

#### Camboyano

*   [ttf-khmer](https://www.archlinux.org/packages/?name=ttf-khmer) - Fuente que cubre los glifos del lenguaje camboyano.
*   [Hanuman](https://www.google.com/fonts/specimen/Hanuman) ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))

#### Mongol y tunguses

*   [ttf-abkai](https://aur.archlinux.org/packages/ttf-abkai/) - Fuentes para las escrituras sibe, smnchu y daur (incompleto, aún en desarrollo).

#### Persa

*   [persian-fonts](https://aur.archlinux.org/packages/persian-fonts/) - Meta-paquete para instalar todas las fuentes persas del AUR.
*   [borna-fonts](https://aur.archlinux.org/packages/borna-fonts/) - Serie de fuentes persa B Borna Rayaneh Co..
*   [iran-nastaliq-fonts](https://aur.archlinux.org/packages/iran-nastaliq-fonts/) - Fuente caligráfica libre Unicode persa.
*   [iranian-fonts](https://aur.archlinux.org/packages/iranian-fonts/) - Familia Iranian-Sans e Iranian-Serif de fuentes persa.
*   [ir-standard-fonts](https://aur.archlinux.org/packages/ir-standard-fonts/) - Fuentes persas estándar del Consejo Supremo de Tecnologías de la Información y la Comunicación de Irán (SCICT).
*   [persian-hm-ftx-fonts](https://aur.archlinux.org/packages/persian-hm-ftx-fonts/) - Series de fuentes persa derivado de X Series 2, Metafont y Fuentes FarsiTeX con la característica kashida.
*   [persian-hm-xs2-fonts](https://aur.archlinux.org/packages/persian-hm-xs2-fonts/) - Series de fuentes persa derivado de X Series 2 con la característica kashida.
*   [sina-fonts](https://aur.archlinux.org/packages/sina-fonts/) - Serie de fuente persa Sina Pardazesh Co..
*   [gandom-fonts](https://aur.archlinux.org/packages/gandom-fonts/), [parastoo-fonts](https://aur.archlinux.org/packages/parastoo-fonts/), [sahel-fonts](https://aur.archlinux.org/packages/sahel-fonts/), [samim-fonts](https://aur.archlinux.org/packages/samim-fonts/), [shabnam-fonts](https://aur.archlinux.org/packages/shabnam-fonts/), [tanha-fonts](https://aur.archlinux.org/packages/tanha-fonts/), [vazir-fonts](https://aur.archlinux.org/packages/vazir-fonts/), [vazir-code-fonts](https://aur.archlinux.org/packages/vazir-code-fonts/) - Bonitas fuentes persa hecho por Ali Rasti Kerdar.
*   [ttf-yas](https://aur.archlinux.org/packages/ttf-yas/) - Serie de fuente persa Yas (con **hueco cero**).
*   [ttf-x2](https://aur.archlinux.org/packages/ttf-x2/) - Fuentes libres con soporte para persa, árabe, urdu, pashto, dari, uzbeko, kurdo, uigur, turco antiguo (otomano) y turco moderno (romano).

#### Tai–Kadai

*   [fonts-tlwg](https://aur.archlinux.org/packages/fonts-tlwg/) - Colección de fuentes escalables tailandesas.
*   [ttf-lao](https://aur.archlinux.org/packages/ttf-lao/) - Fuente TTF Lao (Phetsarath_OT)
*   [ttf-lao-fonts](https://aur.archlinux.org/packages/ttf-lao-fonts/) - Fuente TTF Lao, ambas Unicode y no-Unicode para Windows.

#### Tibeto-Burman

*   [ttf-tibetan-machine](https://www.archlinux.org/packages/?name=ttf-tibetan-machine) - Fuente TTF Tibetan Machine.
*   [ttf-myanmar-fonts](https://aur.archlinux.org/packages/ttf-myanmar-fonts/) - 121 tipos de letra de myordbok.com

### Emoji y símbolos

Una sección del Unicode estándar está dedicado a caracteres pictográficos que son llamados "emoji".

*   [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji) - Fuente de emoji de Google, como en Android o Google Hangouts.
*   [ttf-symbola](https://aur.archlinux.org/packages/ttf-symbola/) - proporciona muchos símbolos Unicode, incluido emoji, en un estilo de contorno.
*   [ttf-joypixels](https://www.archlinux.org/packages/?name=ttf-joypixels) - Fuente completa Unicode 12 Emoji font (formalmente EmojiOne)
*   [ttf-twemoji-color](https://aur.archlinux.org/packages/ttf-twemoji-color/) - Glifos código abierto de Twitter.

[Kaomoji](https://en.wikipedia.org/wiki/es:Emoticono#Estilo_de_Asia_Oriental "wikipedia:es:Emoticono") a veces como "emoticonos japoneses" están compuestos por caracteres de varios conjuntos, incluido CJK y fuentes índicas. Por ejemplo, estos paquetes proporcionan muchos kaomoji existentes: [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont), [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming), y [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf).

### Matemáticas

*   [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica) - Fuentes matemáticas por Wolfram Research, Inc.
*   [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) y [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra) contiene muchas fuentes matemáticas como la matemática moderna latina y [STIX Fonts](https://en.wikipedia.org/wiki/STIX_Fonts_project "wikipedia:STIX Fonts project"). Vea [Hacer que las fuentes estén disponibles en Fontconfig (en inglés)](/index.php/TeX_Live#Making_fonts_available_to_Fontconfig "TeX Live") para la configuración.
*   [otf-stix](https://aur.archlinux.org/packages/otf-stix/) - Versión independiente, una de las más recientes de STIX.
*   [otf-latin-modern](https://www.archlinux.org/packages/?name=otf-latin-modern), [otf-latinmodern-math](https://www.archlinux.org/packages/?name=otf-latinmodern-math) - Versión mejorada de fuentes computacionales modernas usadas en LaTeX.
*   [ttf-computer-modern-fonts](https://aur.archlinux.org/packages/ttf-computer-modern-fonts/), [otf-cm-unicode](https://aur.archlinux.org/packages/otf-cm-unicode/) - [Computación moderna (inglés)](https://en.wikipedia.org/wiki/Computer_Modern "wikipedia:Computer Modern") (de la fama de TeX).
*   [ttf-mathtype](https://aur.archlinux.org/packages/ttf-mathtype/) - Fuentes MathType.

### Fuentes de otros sistemas operativos

*   [ttf-mac-fonts](https://aur.archlinux.org/packages/ttf-mac-fonts/) - Fuentes de TrueType Apple MacOS.

Vea [Fuentes métricamente compatibles (inglés)](/index.php/Metric-compatible_fonts "Metric-compatible fonts"), que muestra las alternativas para las [Fuentes de Microsoft (inglés)](/index.php/Microsoft_fonts "Microsoft fonts").

## Orden de fuentes alternativas con X11

Automáticamente fontconfig selecciona una fuente que cumpla con los requisitos de ese momento. Es decir, que si una ventana contiene inglés y chino, fontconfig cambiará de fuente para el chino si la que está por defecto no lo soporta.

Fontconfig permite que cada usuario configure el orden a través de `$XDG_CONFIG_HOME/fontconfig/fonts.conf`. Si prefiere que una fuente particular se seleccione antes que su fuente Serif favorita, el archivo queda así:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
<alias>
   <family>serif</family>
   <prefer>
     <family>El nombre de su fuente serif favorita</family>
     <family>El nombre de su fuente china</family>
   </prefer>
 </alias>
</fontconfig>

```

**Sugerencia:** Si usa localmente chino, establezca `LC_LANG` a `und` para que funcione. Si no los textos chinos e ingleses serán renderizados por la fuente china.

También se puede añadir una sección para sans-serif y monospace. Para más información. eche un vistazo al manual de fontconfig.

Vea también [Establecer o reemplazar las fuentes por defecto](/index.php/Font_configuration_(Espa%C3%B1ol)#Reemplazar_o_establecer_las_fuentes_por_defecto "Font configuration (Español)").

## Alias de fuente

Hay varios alias de fuentes que representa a otras fuentes con la intención de que las aplicaciones utilicen fuentes similares. Los alias más comunes son: `serif` para las fuentes de tipo serif (p.ej. DejaVu Serif); `sans-serif` para las fuentes del tipo sans-serif (p.ej. DejaVu Sans); y `monospace` para las fuentes mono-espaciadas (p.ej. DejaVu Sans Mono). Sin embargo, el aspecto de las fuentes que representan puede variar y la relación no se observa en las herramientas de gestión de fuentes, como las que se encuentran en [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)") y otros [entornos de escritorio](/index.php/Desktop_environments_(Espa%C3%B1ol) "Desktop environments (Español)").

Para invertir un alias y encontrar qué fuente es la que representa, ejecute:

 `$ fc-match monospace` 
```
DejaVuSansMono.ttf: "DejaVu Sans Mono" "Book"

```

En este caso, `DejaVuSansMono.ttf` es la fuente representada por el alias de monospace.

## Consejos y trucos

### Listar todas las fuentes instaladas

Puede utilizar el siguiente comando para listar todas las fuentes instaladas fontconfig que están disponibles en su sistema.

```
$ fc-list

```

### Listar las fuentes instaladas de un lenguaje particular

Las aplicaciones y navegadores selecciona y muestra fuentes dependiendo de la configuración de fontconfig y de los glifos disponibles para el texto Unicode. Para listar las fuentes instaladas de un lenguaje particular, ejecute `fc-list :lang="two letter language code"`. Por ejemplo, para listar las fuentes árabes o las que soportan glifos árabes instaladas:

 `$ fc-list -f '%{file}
' :lang=ar` 
```
/usr/share/fonts/TTF/FreeMono.ttf
/usr/share/fonts/TTF/DejaVuSansCondensed.ttf
/usr/share/fonts/truetype/custom/DroidKufi-Bold.ttf
/usr/share/fonts/TTF/DejaVuSansMono.ttf
/usr/share/fonts/TTF/FreeSerif.ttf

```

### Listar las fuentes instaladas de un caracter Unicode particular

Para buscar fuentes monoespaciadas que soporten un punto de código en particular:

```
$ fc-match -s monospace:charset=1F4A9

```

### Establecer la fuente del terminal sobre la marcha

Para los emuladores de terminal que usan [X resources](/index.php/X_resources "X resources"), p.ej. [xterm](/index.php/Xterm "Xterm") o [rxvt-unicode](/index.php/Rxvt-unicode_(Espa%C3%B1ol) "Rxvt-unicode (Español)"), las fuentes se pueden establecer utilizando secuencias de escape. Especificamente, `echo -e "\033]710;$font\007"` para cambier la fuente normal (`*font` en `~/.Xresources`), y reemplazarla `710` con `711`, `712`, y `713` para cambiar las fuentes `*boldFont`, `*italicFont`, y `*boldItalicFont`, respectivamente.

### Caché específico de fuente de una aplicación

Matplotlib ([python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib) o [python2-matplotlib](https://www.archlinux.org/packages/?name=python2-matplotlib)) usa su propia cache de fuente, así que después de actualizar las fuentes, asegúrese de eliminar `~/.matplotlib/fontList.cache`, `~/.cache/matplotlib/fontList.cache`, `~/.sage/matplotlib-1.2.1/fontList.cache`, etc. Así regenerará su caché de fuente y encontrará las nuevas fuentes [[1]](http://matplotlib.1069221.n5.nabble.com/getting-matplotlib-to-recognize-a-new-font-td40500.html).

## Vea también

*   [Estado de la representación de texto](http://behdad.org/text/)
*   [Biblioteca de fuentes](https://fontlibrary.org/es) - Fuentes con licencia libre.
*   [Fuentes en screenshots.debian.net](https://screenshots.debian.net/packages?search=fonts&show=with)