Artículos relacionados

*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Linux console#Fonts](/index.php/Linux_console#Fonts "Linux console")
*   [Java Runtime Environment fonts](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts")
*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")
*   [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts")

De [Fuentes del ordenador (En ingles)](https://en.wikipedia.org/wiki/Computer_font "wikipedia:Computer font"): "Una tipografía del ordenador (o fuente) es un archivo de datos electrónicos que contiene un conjunto de glifos, caracteres, o símbolos como dingbats."

Note que ciertas licencias de fuentes pueden imponer ciertas limitaciones legales.

## Contents

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
        *   [3.3.4 Chino, Japonés, Coreano, Vietnamita](#Chino,_Japonés,_Coreano,_Vietnamita)
            *   [3.3.4.1 Pan-CJK](#Pan-CJK)
            *   [3.3.4.2 Chino](#Chino)
            *   [3.3.4.3 Japonés](#Japonés)
            *   [3.3.4.4 Coreano](#Coreano)
            *   [3.3.4.5 Vietnamita](#Vietnamita)
        *   [3.3.5 Cirílico](#Cirílico)

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
$ for dir in * ; do if [  -d  "$dir"  ]; then cd "$dir";xset +fp "$PWD" ;mkfontscale; mkfontdir;cd .. ;fi; done && xset fp rehash

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
*   [Lime](http://artwizaleczapka.sourceforge.net/) ([artwiz-fonts](https://www.archlinux.org/packages/?name=artwiz-fonts)).
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
*   Fantasque Sans Mono ([ttf-fantasque-sans-git](https://aur.archlinux.org/packages/ttf-fantasque-sans-git/)).
*   [Fira Mono](https://en.wikipedia.org/wiki/Fira_Sans "wikipedia:Fira Sans") ([ttf-fira-mono](https://www.archlinux.org/packages/?name=ttf-fira-mono), [otf-fira-mono](https://www.archlinux.org/packages/?name=otf-fira-mono)) – diseñado para Firefox OS.
*   [FreeMono](https://en.wikipedia.org/wiki/es:GNU_FreeFont "wikipedia:es:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Hack](https://sourcefoundry.org/hack/) ([ttf-hack](https://www.archlinux.org/packages/?name=ttf-hack)) - fuente mono espaciada de código abierto, utilizada por defecto en KDE Plasma.
*   [Inconsolata](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata](https://www.archlinux.org/packages/?name=ttf-inconsolata), incluida en [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - inspirado por Consolas.
*   [Inconsolata-g](https://leonardo-m.livejournal.com/77079.html) ([ttf-inconsolata-g](https://aur.archlinux.org/packages/ttf-inconsolata-g/)) - añade algunas modificaciones familiares para el programador.
*   [Iosevka](https://be5invis.github.io/Iosevka/) ([ttf-iosevka](https://aur.archlinux.org/packages/ttf-iosevka/)) – Iosevka es un esbelto tipo de letra monospace sans-serif y slab-serif inspirado por Pragmata Pro, M+ y PF DIN Mono, diseñado para ser la fuente ideal para programar.
*   [Lucida Typewriter](https://en.wikipedia.org/wiki/Lucida_Typewriter "wikipedia:Lucida Typewriter") (incluida en el paquete [jre](https://aur.archlinux.org/packages/jre/)).
*   [Menlo](https://en.wikipedia.org/wiki/Menlo_(typeface) (derivado: [ttf-meslo](https://aur.archlinux.org/packages/ttf-meslo/)) - fuente mono espaciada por defecto de OS X.
*   [Monaco](https://en.wikipedia.org/wiki/es:Monaco_(tipograf%C3%ADa) ([ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco/)) - fuente propietaria diseñada por Apple para OS X.
*   Monofur ([ttf-monofur](https://aur.archlinux.org/packages/ttf-monofur/))
*   [Mononoki](https://madmalik.github.io/mononoki) ([ttf-mononoki](https://aur.archlinux.org/packages/ttf-mononoki/))
*   [Source Code Pro](https://en.wikipedia.org/wiki/Source_Code_Pro "wikipedia:Source Code Pro") ([adobe-source-code-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-code-pro-fonts))

Webs relevantes:

*   [Dan Benjamin's Top 10 fuentes de programación](http://hivelogic.com/articles/top-10-programming-fonts).
*   [Lista de fuentes de Trevor Lowing](http://www.lowing.org/fonts/) .
*   [Slant: ¿Cuales son las mejores fuentes de programación?](https://www.slant.co/topics/67/~what-are-the-best-programming-fonts).
*   [Stack Overflow: Fuentes recomendadas para programar](https://stackoverflow.com/questions/4689/recommended-fonts-for-programming).

#### Sans-serif

*   [Andika](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=andika) ([ttf-andika](https://aur.archlinux.org/packages/ttf-andika/)).
*   [FreeSans](https://en.wikipedia.org/wiki/es:GNU_FreeFont "wikipedia:es:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode.
*   [Inter UI](https://github.com/rsms/inter) ([ttf-inter-ui](https://aur.archlinux.org/packages/ttf-inter-ui/)) – diseñada para las interfaces de usuario.
*   [Linux Biolinum](https://en.wikipedia.org/wiki/es:Linux_Libertine "wikipedia:es:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) – sustituto libre para Times New Roman.
*   [PT Sans](https://en.wikipedia.org/wiki/PT_Sans "wikipedia:PT Sans") ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - tres pricipales variantes: normal, estrecho, y subtítulo - Unicode: Latín, Cyrillic
*   [Source Sans Pro](https://en.wikipedia.org/wiki/Source_Sans_Pro "wikipedia:Source Sans Pro") ([adobe-source-sans-pro-fonts](https://www.archlinux.org/packages/?name=adobe-source-sans-pro-fonts))
*   [Tahoma](https://en.wikipedia.org/wiki/es:Tahoma "wikipedia:es:Tahoma") ([ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/))

#### Serif

*   [EB Garamond](http://www.georgduffner.at/ebgaramond/) ([otf-eb-garamond](https://aur.archlinux.org/packages/otf-eb-garamond/)).
*   [FreeSerif](https://en.wikipedia.org/wiki/es:GNU_FreeFont "wikipedia:es:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode.
*   [Gentium](https://en.wikipedia.org/wiki/es:Gentium "wikipedia:es:Gentium") ([ttf-gentium](https://www.archlinux.org/packages/?name=ttf-gentium)) - Unicode: Latin, Greek, Cyrillic, Phonetic Alphabet.
*   [Linux Libertine](https://en.wikipedia.org/wiki/es:Linux_Libertine "wikipedia:es:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) - Unicode: Latin, Greek, Cyrillic, Hebrew.

#### Sin clasificación

*   [ttf-cheapskate](https://www.archlinux.org/packages/?name=ttf-cheapskate) - Coleccion de fuentes de *dustismo.com*.
*   [ttf-junicode](https://www.archlinux.org/packages/?name=ttf-junicode) - Fuente Junius que contiene casi todos los script y glifos medivales.
*   [ttf-mph-2b-damase](https://www.archlinux.org/packages/?name=ttf-mph-2b-damase) - Cubre el primer plano completo y muchos scripts.
*   [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) - Conjuntos IBM Courier y Adobe Utopia del [tipo de letra PostScript](https://en.wikipedia.org/wiki/es:Tipo_de_letra_PostScript "wikipedia:es:Tipo de letra PostScript").
*   [all-repository-fonts](https://aur.archlinux.org/packages/all-repository-fonts/) - Meta paquete para todas las fuentes de los repositorios oficiales.
*   [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/) - una enorme colección de fuentes libres (incluye Ubuntu, Inconsolata, Roboto, etc.) - Nota: Su diálogo de fuentes puede ser muy grande ya que se añadirán más de cien fuentes.

### Escritura no latina

#### Escritura antigua

*   [ttf-ancient-fonts](https://aur.archlinux.org/packages/ttf-ancient-fonts/) - Fuentes que contienen simbolos Unicode para las escrituras Egeo, Egipcio, Cuneiforme, Anatolian, Maya y Analecta.

#### Árabe

*   [ttf-amiri](https://aur.archlinux.org/packages/ttf-amiri/) - Un tipo de letra clásico en Naskh, estilo pionero de Amiria Press.
*   [ttf-arabeyes-fonts](https://aur.archlinux.org/packages/ttf-arabeyes-fonts/) - Colección de fuentes árabes libres.
*   [ttf-qurancomplex-fonts](https://aur.archlinux.org/packages/ttf-qurancomplex-fonts/) - Fuentes de El complejo de impresión del gran Corán Rey Fahd en al-Madinah al-Munawwarah.
*   [ttf-sil-lateef](https://aur.archlinux.org/packages/ttf-sil-lateef/) - Fuente árabe Unicode desde SIL.
*   [ttf-sil-scheherazade](https://aur.archlinux.org/packages/ttf-sil-scheherazade/) - Fuente árabe Unicode desde SIL. (Alternativa de la fuente árabe tradicional).

#### Braille

*   [ttf-ubraille](https://www.archlinux.org/packages/?name=ttf-ubraille) - Fuente que contiene símbolos Unicode para el *braille*.

#### Chino, Japonés, Coreano, Vietnamita

##### Pan-CJK

*   Fuentes adobe source han - Una gran colección de fuentes con un soporte comprensible de Chino simplificado, Chino tradicional, Japones, y Coreano, con un diseño y aspecto consistente.
    *   [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts) - Sans fonts.
    *   [adobe-source-han-serif-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-otc-fonts) - Serif fonts.

*   [noto-fonts-cjk](https://www.archlinux.org/packages/?name=noto-fonts-cjk) - Otra gran colección de fuentes con un soporte comprensible de Chino simplificado, Chino tradicional, Japones, y Coreano, con un diseño y aspecto consistente. Actualmente es una versión renombrada de [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts).

##### Chino

*   Fuentes adobe source han.
    *   [adobe-source-han-sans-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-cn-fonts) - Fuentes de Chino simplificado OpenType/CFF Sans.
    *   [adobe-source-han-sans-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-tw-fonts) - Fuentes de Chino tradicional OpenType/CFF Sans.
    *   [adobe-source-han-serif-cn-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-cn-fonts) - Fuentes de Chino simplificado OpenType/CFF Serif.
    *   [adobe-source-han-serif-tw-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-serif-tw-fonts) - Fuentes de Chino tradicional OpenType/CFF Serif.

*   Fuentes noto, Chino.
    *   [noto-fonts-sc](https://aur.archlinux.org/packages/noto-fonts-sc/) - Fuentes Noto CJK-SC para Chino simplificado.
    *   [noto-fonts-tc](https://aur.archlinux.org/packages/noto-fonts-tc/) - Fuentes Noto CJK-TC para Chino tradicional.

*   Fuentes wqy
    *   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) - La Familia tipográfica WenQuanYi Micro Hei (también conocida como Hei, Gothic o Dotum) es un estilo sans-serif derivado de Droid Sans Fallback, ofrece una gran calidad CJK y un gran contorno, además es extremadamente compacto (~5M).
    *   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) - Estilo Hei Ti (sans-serif) Contorno Chino con incrustaciones con Bitmapped Song Ti (también soporta Japonés (parcialmente) y caracteres Coreanos).
    *   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont) - Fuente china Bitmapped Song Ti (serif).

*   Fuentes arficas.
    *   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai) - Fuente Unicode *Kaiti* (trazos de pincel) (se sugiere habilitar anti-aliasing).
    *   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) - Fuente Unicode *Mingti* (impresa).

*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts) - Fuente *New Sung*, anteriormente era el paquete ttf-fireflysung.

*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - Fuentes ttf Chinas and Vietnamitas.

*   Fuentes estándar del ministerio de educación de la república china en Taiwan.
    *   [ttf-tw](https://aur.archlinux.org/packages/ttf-tw/) - Fuentes Chinas tradicionales Kai y Song del ministerio de educación de Taiwan.
    *   [ttf-twcns-fonts](https://aur.archlinux.org/packages/ttf-twcns-fonts/) Fuentes Chinas TrueType por el ministerio de educación del gobierno de Taiwan, soporta el estándar CNS11643, incluido el tipo de letra Kai y Sung.

*   Fuentes Chinas de Windows
    *   [ttf-ms-win8-zh_cn](https://aur.archlinux.org/packages/ttf-ms-win8-zh_cn/) - Fuentes de Chino simplificado de windows 8.
    *   [ttf-ms-win8-zh_tw](https://aur.archlinux.org/packages/ttf-ms-win8-zh_tw/) - Fuentes de Chino tradicional de windows 8.
    *   [ttf-ms-win10-zh_cn](https://aur.archlinux.org/packages/ttf-ms-win10-zh_cn/) - Fuentes de Chino simplificado de windows 10.
    *   [ttf-ms-win10-zh_tw](https://aur.archlinux.org/packages/ttf-ms-win10-zh_tw/) - Fuentes de Chino tradicional de windows 10.

*   [ttf-i.bming](https://aur.archlinux.org/packages/ttf-i.bming/) - Fuente CJK serif que enfatiza en un estilo de letra antiguo.

##### Japonés

*   [adobe-source-han-sans-jp-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-jp-fonts) - Fuentes Japonesas OpenType/CFF.
*   [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont) - Conjunto de fuentes formales góticas Japonesas (sans-serif) y Mincho (serif); una fuente de código abierto de gran calidad. Fuente por defecto de openSUSE-ja.
*   [ttf-hanazono](https://www.archlinux.org/packages/?name=ttf-hanazono) - Una fuente libre Japonesa kanji, estilo Mincho (serif).
*   [ttf-sazanami](https://www.archlinux.org/packages/?name=ttf-sazanami) - Una fuente libre Japonesa TrueType. Esta era desactualizada y no se mantendrá más, pero varios entornos puede que tengan establecido esta fuente como fuente alternativa.
*   [ttf-koruri](https://aur.archlinux.org/packages/ttf-koruri/) - Fuente Japonesa TrueType obtenida mezclando [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) y Open Sans.
*   [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/) - Fuente Japonesa para ver [2channel Shift JIS art](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art") apropiadamente.
*   [ttf-mplus](https://aur.archlinux.org/packages/ttf-mplus/) - Fuente Japonesa con un estilo gótico moderno en su contorno. Incluye todo de Japonés Hiragana/Katakana, Latino básico, Latino-1 suplemento, Latino extandido-A, Extensiones IPA y la mayoría de Kanji Japonés, Griego, Cirílico, Vietnamita con siete pesos (proporcional) o 5 pesos (mono espaciado).
*   [ttf-vlgothic](https://aur.archlinux.org/packages/ttf-vlgothic/) - Fuente gótica Japonesa. Por defecto en los Linux Debian/Fedora/Vine.

##### Coreano

*   [adobe-source-han-sans-kr-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-kr-fonts) - Fuente Coreana OpenType/CFF.
*   [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk) - Colección de fuentes Coreanas TrueType.
*   [spoqa-han-sans](https://aur.archlinux.org/packages/spoqa-han-sans/) - Fuentes Han Sans personalizadas por Spoqa
*   [ttf-d2coding](https://aur.archlinux.org/packages/ttf-d2coding/) - Fuente D2Coding de ancho fijo TrueType hecho por Naver.
*   [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/) - Serie de fuentes Nanum TrueType.
*   [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) - Serie de fuentes Nanum TrueType de ancho fijo.
*   [ttf-kopub](https://aur.archlinux.org/packages/ttf-kopub/)/[otf-kopub](https://aur.archlinux.org/packages/otf-kopub/) - Fuente Coreanas TrueType/OpenType por la sociedad de editores de Corea.
*   [ttf-kopubworld](https://aur.archlinux.org/packages/ttf-kopubworld/)/[otf-kopubworld](https://aur.archlinux.org/packages/otf-kopubworld/) - Fuentes plurilingües (Coreano, Yethangul, Chino extendido, Japonés, Latino extendido, Cirílico, Árabe, Hebreo, Devanagari) TrueType/OpenType por la sociedad de editores de Corea.
*   [ttf-unfonts-core-ibx](https://aur.archlinux.org/packages/ttf-unfonts-core-ibx/) - Una colección de fuentes Coreanas TrueType por KLDP.

##### Vietnamita

*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - Fuente Vietnamita TrueType font para los caracteres chữ Nôm.

#### Cirílico

Vea también [#Escritura latina](#Escritura_latina)

*   [ttf-paratype](https://aur.archlinux.org/packages/ttf-paratype/) - Familia de fuente por ParaType: sans, serif, mono, cirílico extendido y latino, licencia OFL.
*   [otf-russkopis](https://aur.archlinux.org/packages/otf-russkopis/) - Una fuente libre cursiva OpenType para la escritura Cirílica.