Artículos relacionados

*   [Font configuration/Examples](/index.php/Font_configuration/Examples "Font configuration/Examples")
*   [Fuentes](/index.php/Fonts_(Espa%C3%B1ol) "Fonts (Español)")
*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")
*   [Microsoft fonts](/index.php/Microsoft_fonts "Microsoft fonts")
*   [Java Runtime Environment fonts](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts")
*   [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description")

[Fontconfig](http://www.freedesktop.org/wiki/Software/fontconfig/) es una biblioteca diseñada para proporcionar una lista de [fuentes](/index.php/Fonts_(Espa%C3%B1ol) "Fonts (Español)") disponibles para las aplicaciones, y también para configurar cómo representa las fuentes. La biblioteca FreeType representa las fuentes, basada en esta configuración. La representación de fuentes *freetype2* en Arch Linux incluye el intérprete bytecode (BCI) activado para una representación mejor de las fuentes, especialmente en los monitores LCD. Vea [#Configuración de FontConfig](#Configuración_de_FontConfig) y [Configuración de FontConfig/Ejemplos (en inglés)](/index.php/Font_configuration/Examples "Font configuration/Examples").

Aunque Fontconfig se utiliza a menudo en los Unix modernos y en los sistemas operativos Unix-like, algunas aplicaciones confían en el método original para seleccionar fuentes y mostrarlas, la [descripción de la fuente lógica X (en inglés)](/index.php/X_Logical_Font_Description "X Logical Font Description").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Path de fuentes](#Path_de_fuentes)
*   [2 Configuración de FontConfig](#Configuración_de_FontConfig)
    *   [2.1 Ajustes predeterminados](#Ajustes_predeterminados)
    *   [2.2 Anti-aliasing](#Anti-aliasing)
    *   [2.3 Hinting](#Hinting)
        *   [2.3.1 Byte-Code Interpreter (BCI)](#Byte-Code_Interpreter_(BCI))
        *   [2.3.2 Autohinter](#Autohinter)
        *   [2.3.3 Hintstyle](#Hintstyle)
    *   [2.4 Pixel alignment](#Pixel_alignment)
    *   [2.5 Subpixel rendering](#Subpixel_rendering)
        *   [2.5.1 LCD filter](#LCD_filter)
        *   [2.5.2 Advanced LCD filter specification](#Advanced_LCD_filter_specification)
    *   [2.6 Disable auto-hinter for bold fonts](#Disable_auto-hinter_for_bold_fonts)
    *   [2.7 Replace or set default fonts](#Replace_or_set_default_fonts)
    *   [2.8 Whitelisting and blacklisting fonts](#Whitelisting_and_blacklisting_fonts)
    *   [2.9 Disable bitmap fonts](#Disable_bitmap_fonts)
    *   [2.10 Disable scaling of bitmap fonts](#Disable_scaling_of_bitmap_fonts)
    *   [2.11 Create bold and italic styles for incomplete fonts](#Create_bold_and_italic_styles_for_incomplete_fonts)
    *   [2.12 Change rule overriding](#Change_rule_overriding)
    *   [2.13 Query the current settings](#Query_the_current_settings)
*   [3 Applications without fontconfig support](#Applications_without_fontconfig_support)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 Distorted fonts](#Distorted_fonts)
    *   [4.2 Calibri, Cambria, Monaco, etc. not rendering properly](#Calibri,_Cambria,_Monaco,_etc._not_rendering_properly)
    *   [4.3 Applications overriding hinting](#Applications_overriding_hinting)
    *   [4.4 Applications not picking up hinting from DE's settings](#Applications_not_picking_up_hinting_from_DE's_settings)
    *   [4.5 Incorrect hinting in GTK applications on non-Gnome systems](#Incorrect_hinting_in_GTK_applications_on_non-Gnome_systems)
    *   [4.6 Helvetica font problem in generated PDFs](#Helvetica_font_problem_in_generated_PDFs)
    *   [4.7 FreeType Breaking Bitmap Fonts](#FreeType_Breaking_Bitmap_Fonts)
*   [5 See also](#See_also)

## Path de fuentes

Para que las aplicaciones reconozcan las fuentes tienen que estar catalogadas para un acceso fácil y rápido.

El path de fuente reconocido inicialmente por Fontconfig son: `/usr/share/fonts/`, `~/.local/share/fonts` (y `~/.fonts/`, en desuso). Fontconfig escaneará estos directorios recursivamente. Para una organización e instalación fácil está recomendado utilizar estas rutas cuando se [añaden fuentes](/index.php/Fonts_(Espa%C3%B1ol)#Instalación "Fonts (Español)").

Para ver una lista de fuentes reconocidas por Fontconfig:

```
$ fc-list : file

```

Vea [fc-list(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fc-list.1) para más formatos de salida.

Comprobar path de fuentes reconocidas por Xorg revisando su log:

```
$ grep /fonts ~/.local/share/xorg/Xorg.0.log

```

**Sugerencia:**

*   También puedes comprobar la lista de path de fuentes reconocida por [Xorg](/index.php/Xorg "Xorg") utilizando el comando `xset q`.
*   Utilice `/var/log/Xorg.0.log` si Xorg se está ejecutando con privilegios de root

Tenga en cuenta que Xorg no busca recursivamente a través del directorio `/usr/share/fonts/` como lo hace Fontconfig. Para añadir una ruta, todo el path tiene que utilizarse:

```
Section "Files"
    FontPath     "/usr/share/fonts/local/"
EndSection

```

Si quiere que el path de fuentes se establezca en base de cada usuario, puede añadir y quitar rutas por defecto añadiendo las siguientes lineas a `~/.xinitrc`:

```
xset +fp /usr/share/fonts/local/           # Antepone un path personalizado a la lista de Xorg.
xset -fp /usr/share/fonts/sucky_fonts/     # Elimina una fuente específica del path de Xorg.

```

Para ver una lista de fuentes Xorg reconocidas utilice `xlsfonts`, del paquete [xorg-xlsfonts](https://www.archlinux.org/packages/?name=xorg-xlsfonts).

## Configuración de FontConfig

La documentación de fontconfig se encuentra en la página del manual [fonts-conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fonts-conf.5).

La configuración se puede hacer por usuario via `$XDG_CONFIG_HOME/fontconfig/fonts.conf`, y globalmente con `/etc/fonts/local.conf`. Las configuraciones por usuario tienen prioridad sobre la configuración global. Ambos archivos utilizan la misma sintaxis.

**Nota:** Los archivos de configuración y los directorios: `~/.fonts.conf/`, `~/.fonts.conf.d/` y `~/.fontconfig/*.cache-*` están obsoletos desde [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) 2.10.1 ([upstream commit](http://cgit.freedesktop.org/fontconfig/commit/?id=8c255fb185d5651b57380b0a9443001e8051b29d)) y no se leerá por defecto en las futuras versiones del paquete. Los nuevos paths son `$XDG_CONFIG_HOME/fontconfig/fonts.conf`, `$XDG_CONFIG_HOME/fontconfig/conf.d/NN-name.conf` y `$XDG_CACHE_HOME/fontconfig/*.cache-*` respectivamente. Si utiliza la segunda localización, asegúrese de que el nombre es válido (donde `NN` es un número de dos dígitos como `00`, `10`, o `99`).

Fontconfig reúne toda su configuración en un archivo principal (`/etc/fonts/fonts.conf`). Este archivo se reemplaza durante las actualizaciones y no se debe editar. Las aplicaciones compatibles con fontconfig obtienen este archivo para conocer las fuentes disponibles y saber cómo se procesan. Este archivo es un conjunto de reglas de la configuración global (`/etc/fonts/local.conf`), la configuración presente en `/etc/fonts/conf.d/`, y el archivo de configuración del usuario (`$XDG_CONFIG_HOME/fontconfig/fonts.conf`). `fc-cache` se puede utilizar para reconstruir la configuración de fontconfig, aunque los cambios solo serán visibles para las aplicaciones lanzadas a partir de ese momento.

**Nota:** En algunos entornos de escritorio (como [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") y [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)") crea o sobrescribe el archivo de configuración de fuentes del usuario al utilizar el *panel de control de fuentes*. Para estos entornos de escritorio es mejor coincidir con las configuraciones definidas a fin de obtener el comportamiento deseado. También asegurese de que la *configuración regional* o los [locales](/index.php/Locale_(Espa%C3%B1ol) "Locale (Español)") del escritorio están soportados por la fuente configurada, si no la configuración de las fuentes puede sobrescribirse.

Los archivos de configuración utiliza el formato [XML](https://en.wikipedia.org/wiki/es:Extensible_Markup_Language "wikipedia:es:Extensible Markup Language") y necesita estas cabeceras:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- Los ajustes van aquí -->

</fontconfig>

```

Los ejemplos de configuración en este artículo omite estas etiquetas.

### Ajustes predeterminados

Los ajustes predeterminados están instalados en el directorio `/etc/fonts/conf.avail`. Se pueden activar creando [enlaces simbólicos](https://en.wikipedia.org/wiki/es:Enlace_simb%C3%B3lico "wikipedia:es:Enlace simbólico") a los archivos de configuración del usuario o globalmente o a ambos, como se describe en `/etc/fonts/conf.d/README`. Estos ajustes sobrescribirán los ajustes correspondientes en sus respectivos archivos de configuración.

Por ejemplo, para activar el renderizado sub-pixel RGB globalmente:

```
# cd /etc/fonts/conf.d
# ln -s ../conf.avail/10-sub-pixel-rgb.conf

```

Para hacer lo mismo pero con la configuración del usuario:

```
$ mkdir $XDG_CONFIG_HOME/fontconfig/conf.d
$ ln -s /etc/fonts/conf.avail/10-sub-pixel-rgb.conf $XDG_CONFIG_HOME/fontconfig/conf.d

```

### Anti-aliasing

La [renderización de fuentes (en inglés)](https://en.wikipedia.org/wiki/Font_rasterization "wikipedia:Font rasterization") convierte los datos vectoriales de la fuente a un mapa de bits para poder mostrarla. El resultado puede parecer dentado debido al [aliasing](https://en.wikipedia.org/wiki/es:Aliasing "wikipedia:es:Aliasing"). La técnica conocida como [anti-aliasing (en inglés)](https://en.wikipedia.org/wiki/Anti-aliasing "wikipedia:Anti-aliasing") puede utilizarse para aumentar aparentemente la resolución de los bordes de las fuentes. Anti-aliasing está *activado* por defecto. Para desactivarlo:

```
  <match target="font">
    <edit name="antialias" mode="assign">
      <bool>false</bool>
    </edit>
  </match>

```

**Nota:** Algunas aplicaciones, como [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") puede [sobrescribir los ajustes anti-aliasing por defecto](#Solución_de_problemas).

### Hinting

[Font hinting](https://en.wikipedia.org/wiki/Font_hinting "wikipedia:Font hinting") (also known as instructing) is the use of mathematical instructions to adjust the display of an outline font so that it lines up with a rasterized grid (i.e. the pixel grid of the display). Its intended effect is to make fonts appear more crisp so that they are more readable. Fonts will line up correctly without hinting when displays have around 300 [DPI](https://en.wikipedia.org/wiki/Dots_per_inch "wikipedia:Dots per inch").

#### Byte-Code Interpreter (BCI)

Using BCI hinting, instructions in TrueType fonts are rendered according to FreeTypes's interpreter. BCI hinting works well with fonts with good hinting instructions. Hinting is **enabled** by default. To disable it:

```
  <match target="font">
    <edit name="hinting" mode="assign">
      <bool>false</bool>
    </edit>
  </match>

```

**Note:** You can switch BCI implementations by editing `/etc/profile.d/freetype2.sh` which includes a brief documentation. Possible values are `truetype:interpreter-version=35` (classic mode, emulates Windows 98; 2.6 default), `truetype:interpreter-version=38` ("Infinality" subpixel mode), `truetype:interpreter-version=40` (minimal subpixel mode; 2.7 default). Subpixel rendering should use a subpixel BCI. For details, see [[1]](https://www.freetype.org/freetype2/docs/subpixel-hinting.html).

#### Autohinter

The autohinter attempts to do automatic hinting and disregards any existing hinting information. Originally it was the default because TrueType2 fonts were patent-protected but now that these patents have expired there is very little reason to use it. It does work better with fonts that have broken or no hinting information but it will be strongly sub-optimal for fonts with good hinting information. Generally common fonts are of the later kind so autohinter will not be useful. Autohinter is **disabled** by default. To enable it:

```
  <match target="font">
    <edit name="autohint" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

#### Hintstyle

Hintstyle is the amount of font reshaping done to line up to the grid. Hinting values are: `hintnone`, `hintslight`, `hintmedium`, and `hintfull`. `hintslight` will make the font more fuzzy to line up to the grid but will be better in retaining font shape (see [[2]](https://www.freetype.org/freetype2/docs/text-rendering-general.html)), while `hintfull` will be a crisp font that aligns well to the pixel grid but will lose a greater amount of font shape. `hintslight` implicitly uses the autohinter in a vertical-only mode in favor of font-native information for non-CFF (*.otf*) fonts.

`hintslight` is the default setting. To change it:

```
  <match target="font">
    <edit name="hintstyle" mode="assign">
      <const>hintnone</const>
    </edit>
  </match>

```

**Note:** Some applications, like [GNOME](/index.php/GNOME "GNOME") may [override default hinting settings.](#Troubleshooting)

### Pixel alignment

Most monitors manufactured today use the Red, Green, Blue (RGB) specification. Fontconfig will need to know your monitor type to be able to display your fonts correctly. Monitors are either: **RGB** (most common), **BGR**, **V-RGB** (vertical), or **V-BGR**. A monitor test can be found [here](http://www.lagom.nl/lcd-test/subpixel.php).

```
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>rgb</const>
    </edit>
  </match>

```

**Note:** Without subpixel rendering (see below), freetype will only care about the alignment (vertical or horizontal) of the subpixels. There is no difference between **RGB** and **BGR**, for example.

### Subpixel rendering

[Subpixel rendering](https://en.wikipedia.org/wiki/Subpixel_rendering "wikipedia:Subpixel rendering") is a technique to improve sharpness of font rendering by effectively tripling the horizontal (or vertical) resolution through the use of subpixels. On Windows machines, this technique is called "ClearType".

FreeType implements its own LCD-optimized rendering called [Harmony](http://lists.gnu.org/archive/html/freetype-commit/2017-03/msg00012.html). With this FreeType LCD rendering technology, the resulting output does not require additional LCD filtering, unlike Microsoft's patented Cleartype subpixel rendering where an LCD filter is recommended. See section below on how to enable LCD filter and its benefits.

Cleartype subpixel rendering is covered by Microsoft patents and **disabled** by default on Arch Linux. To enable it, you have to re-compile [freetype2](https://www.archlinux.org/packages/?name=freetype2) and define the `FT_CONFIG_OPTION_SUBPIXEL_RENDERING` macro, or use e.g. the AUR package [freetype2-cleartype](https://aur.archlinux.org/packages/freetype2-cleartype/).

#### LCD filter

When using Cleartype subpixel rendering, you should enable the LCD filter, which is designed to reduce colour fringing. This is described under [LCD filtering](https://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html) in the FreeType 2 API reference. Different options are described under [FT_LcdFilter](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html#FT_LcdFilter), and are illustrated by this [LCD filter test](http://www.spasche.net/files/lcdfiltering/) page.

The `lcddefault` filter will work for most users. Other filters are available that can be used in special situations: `lcdlight`; a lighter filter ideal for fonts that look too bold or fuzzy, `lcdlegacy`, the original Cairo filter; and `lcdnone` to disable it entirely.

```
  <match target="font">
    <edit name="lcdfilter" mode="assign">
      <const>lcddefault</const>
    </edit>
  </match>

```

#### Advanced LCD filter specification

If the available built-in LCD filters are not satisfactory, it is possible to tweak the font rendering very specifically by building a custom freetype2 package and modifying the hardcoded filters. The [Arch Build System](/index.php/Arch_Build_System "Arch Build System") can be used to build and install packages from source. This requires installation of the [asp](https://www.archlinux.org/packages/?name=asp) package.

Checkout the [freetype2](https://www.archlinux.org/packages/?name=freetype2) PKGBUILD and download/extract the build files:

```
$ asp checkout freetype2
$ cd freetype2/trunk
$ makepkg -o

```

Enable subpixel rendering by editing the file `src/freetype-VERSION/include/freetype/config/ftoption.h` and uncommenting the `FT_CONFIG_OPTION_SUBPIXEL_RENDERING` macro.

Then, edit the file `src/freetype-VERSION/src/base/ftlcdfil.c` and look up the definition of the constant `default_filter[5]`:

```
static const FT_Byte  default_filter[5] =
    { 0x10, 0x40, 0x70, 0x40, 0x10 };

```

This constant defines a low-pass filter applied to the rendered glyph. Modify it as needed. (reference: [freetype list discussion](https://lists.nongnu.org/archive/html/freetype/2006-09/msg00069.html)) Save the file, build and install the custom package:

```
$ makepkg -e
# pacman -Rd freetype2
# pacman -U freetype2-VERSION-ARCH.pkg.tar.xz

```

Reboot or restart X. The lcddefault filter should now render fonts differently.

### Disable auto-hinter for bold fonts

The auto-hinter uses sophisticated methods for font rendering, but often makes bold fonts too wide. Fortunately, a solution can be turning off the autohinter for bold fonts while leaving it on for the rest:

```
...
<match target="font">
    <test name="weight" compare="more">
        <const>medium</const>
    </test>
    <edit name="autohint" mode="assign">
        <bool>false</bool>
    </edit>
</match>
...

```

### Replace or set default fonts

The most reliable way to do this is to add an XML fragment similar to the one below. *Using the "binding" attribute will give you better results*, for example, in Firefox where you may not want to change properties of font being replaced. This will cause Ubuntu to be used in place of Georgia:

```
...
 <match target="pattern">
   <test qual="any" name="family"><string>georgia</string></test>
   <edit name="family" mode="assign" binding="same"><string>Ubuntu</string></edit>
 </match>
...

```

An alternate approach is to set the "preferred" font, but *this only works if the original font is not on the system*, in which case the one specified will be substituted:

```
...
<!-- Replace Helvetica with Bitstream Vera Sans Mono -->
<!-- Note, an alias for Helvetica should already exist in default conf files -->
<alias>
    <family>Helvetica</family>
    <prefer><family>Bitstream Vera Sans Mono</family></prefer>
    <default><family>fixed</family></default>
</alias>
...

```

### Whitelisting and blacklisting fonts

The element `<selectfont>` is used in conjunction with the `<acceptfont>` and `<rejectfont>` elements to selectively whitelist or blacklist fonts from the resolve list and match requests. The simplest and most typical use case it to reject one font that is needed to be installed, however is getting matched for a generic font query that is causing problems within application user interfaces.

First obtain the Family name as listed in the font itself:

 `$ fc-scan .fonts/lklug.ttf --format='%{family}
'`  `LKLUG` 

Then use that Family name in a `<rejectfont>` stanza:

```
<selectfont>
    <rejectfont>
        <pattern>
            <patelt name="family" >
                <string>LKLUG</string>
            </patelt>
        </pattern>
    </rejectfont>
</selectfont>

```

Typically when both elements are combined, `<rejectfont>` is first used on a more general matching glob to reject a large group (such as a whole directory), then `<acceptfont>` is used after it to whitelist individual fonts out of the larger blacklisted group.

```
<selectfont>
    <rejectfont>
        <glob>/usr/share/fonts/OTF/*</glob>
    </rejectfont>
    <acceptfont>
        <pattern>
            <patelt name="family" >
                <string>Monaco</string>
            </patelt>
        </pattern>
    </acceptfont>
</selectfont>

```

### Disable bitmap fonts

Bitmap fonts are sometimes used as fallbacks for missing fonts, which may cause text to be rendered pixelated or too large. Use the `70-no-bitmaps.conf` [preset](#Presets) to disable this behavior.

To disable embedded bitmap for all fonts:

 `~/.config/fontconfig/conf.d/20-no-embedded.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="font">
    <edit name="embeddedbitmap" mode="assign">
      <bool>false</bool>
    </edit>
  </match>
</fontconfig>

```

To disable embedded bitmap fonts for a specific font:

```
<match target="font">
  <test qual="any" name="family">
    <string>Monaco</string>
  </test>
  <edit name="embeddedbitmap">
    <bool>false</bool>
  </edit>
</match>

```

### Disable scaling of bitmap fonts

To disable scaling of bitmap fonts (which often makes them blurry), remove `/etc/fonts/conf.d/10-scale-bitmap-fonts.conf`.

### Create bold and italic styles for incomplete fonts

FreeType has the ability to automatically create *italic* and **bold** styles for fonts that do not have them, but only if explicitly required by the application. Given programs rarely send these requests, this section covers manually forcing generation of missing styles.

Start by editing `/usr/share/fonts/fonts.cache-1` as explained below. Store a copy of the modifications on another file, because a font update with `fc-cache` will overwrite `/usr/share/fonts/fonts.cache-1`.

Assuming the Dupree font is installed:

```
"dupree.ttf" 0 "Dupree:style=Regular:slant=0:weight=80:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Duplicate the line, change `style=Regular` to `style=Bold` or any other style. Also change `slant=0` to `slant=100` for italic, `weight=80` to `weight=200` for bold, or combine them for ***bold italic***:

```
"dupree.ttf" 0 "Dupree:style=Bold Italic:slant=100:weight=200:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Now add necessary modifications to `$XDG_CONFIG_HOME/fontconfig/fonts.conf`:

```
...
<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
         <!-- other fonts here .... -->
     </test>
     <test name="weight" compare="more_eq"><int>140</int></test>
     <edit name="embolden" mode="assign"><bool>true</bool></edit>
</match>

<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
        <!-- other fonts here .... -->
    </test>
    <test name="slant" compare="more_eq"><int>80</int></test>
    <edit name="matrix" mode="assign">
        <times>
            <name>matrix</name>
                <matrix>
                    <double>1</double><double>0.2</double>
                    <double>0</double><double>1</double>
                </matrix>
        </times>
    </edit>
</match>
...

```

**Tip:** Use the value `embolden` for existing bold fonts in order to make them even bolder.

### Change rule overriding

Fontconfig processes files in `/etc/fonts/conf.d` in numerical order. This enables rules or files to override one another, but often confuses users about what file gets parsed last.

To guarantee that personal settings take precedence over any other rules, change their ordering:

```
# cd /etc/fonts/conf.d
# mv 50-user.conf 99-user.conf

```

This change seems however to be unnecessary for the most of the cases, because a user is given enough control by default to set up own font preferences, hinting and antialiasing properties, alias new fonts to generic font families, etc.

### Query the current settings

To find out what settings are in effect, use `fc-match --verbose`. eg.

 `$ fc-match --verbose Sans` 
```
family: "DejaVu Sans"(s)
hintstyle: 3(i)(s)
hinting: True(s)
...

```

Look up the meaning of the numbers at [fonts-conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fonts-conf.5) Eg. 'hintstyle: 3' means 'hintfull'

## Applications without fontconfig support

Some applications like [URxvt](/index.php/URxvt "URxvt") will ignore fontconfig settings. You can work around this by using `~/.Xresources`, but it is as flexible as fontconfig. Example (see [#Fontconfig configuration](#Fontconfig_configuration) for explanations of the options):

 `~/.Xresources` 
```
Xft.autohint: 0
Xft.lcdfilter: lcddefault
Xft.hintstyle: hintslight
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

```

Make sure the settings are loaded properly when X starts with `xrdb -q` (see [Xresources](/index.php/Xresources "Xresources") for more information).

## Solución de problemas

### Distorted fonts

**Note:** 96 DPI is not a standard. You should use your monitor's actual DPI to get proper font rendering, especially when using subpixel rendering.

If fonts are still unexpectedly large or small, poorly proportioned or simply rendering poorly, fontconfig may be using the incorrect DPI.

Fontconfig should be able to detect DPI parameters as discovered by the Xorg server. You can check the automatically discovered DPI with `xdpyinfo` (provided by the [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo) package):

 `$ xdpyinfo | grep dots` 
```
  resolution:    102x102 dots per inch

```

If the DPI is detected incorrectly (usually due to an incorrect monitor [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data "wikipedia:Extended Display Identification Data")), you can specify it manually in the Xorg configuration, see [Xorg#Display size and DPI](/index.php/Xorg#Display_size_and_DPI "Xorg"). This is the recommended solution, but it may not work with buggy drivers.

Fontconfig will default to the Xft.dpi variable if it is set. Xft.dpi is usually set by desktop environments (usually to Xorg's DPI setting) or manually in `~/.Xdefaults` or `~/.Xresources`. Use xrdb to query for the value:

 `$ xrdb -query | grep dpi` 
```
Xft.dpi:	102

```

Those still having problems can fall back to manually setting the DPI used by fontconfig:

```
...
<match target="pattern">
   <edit name="dpi" mode="assign"><double>102</double></edit>
</match>
...

```

### Calibri, Cambria, Monaco, etc. not rendering properly

Some scalable fonts have embedded bitmap versions which are rendered instead, mainly at smaller sizes. Using [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts") as replacements can improve the rendering in these cases.

You can also force using scalable fonts at all sizes by [disabling embedded bitmap](#Disable_bitmap_fonts), sacrificing some rendering quality.

### Applications overriding hinting

Some applications or desktop environments may override default fontconfig hinting and anti-aliasing settings. This may happen with [GNOME](/index.php/GNOME "GNOME") 3, for example while you are using Qt applications like [vlc](https://www.archlinux.org/packages/?name=vlc) or [smplayer](https://www.archlinux.org/packages/?name=smplayer). Use the specific configuration program for the application in such cases. For GNOME, try [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

### Applications not picking up hinting from DE's settings

For instance, under GNOME it sometimes happens that Firefox applies full hinting even when it's set to "none" in GNOME's settings, which results in sharp and widened fonts. In this case you would have to add hinting settings to your `fonts.conf` file:

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>	
<fontconfig>
 <match target="font">
  <edit mode="assign" name="hinting">
   <bool>false</bool>
  </edit>
 </match>
</fontconfig>

```

In this example, hinting is set to "grayscale".

### Incorrect hinting in GTK applications on non-Gnome systems

[GNOME](/index.php/GNOME "GNOME") uses the XSETTINGS system to configure font rendering. Outside of GNOME, GTK applications rely on fontconfig, but some fonts get the hinting wrong causing them to look too bold or too light.

A simple solution is using [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/) to provide the configuration, for example:

 `~/.xsettingsd` 
```
Xft/Hinting 1
Xft/RGBA "rgb"
Xft/HintStyle "hintslight"
Xft/Antialias 1

```

Alternatively you could just write the font configuration as `Xft.*` directives in `~/.Xresources` without using a settings daemon.

### Helvetica font problem in generated PDFs

If the following command

```
fc-match helvetica

```

produces

```
helvR12-ISO8859-1.pcf.gz: "Helvetica" "Regular"

```

then the bitmap font provided by [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) is likely to be embedded into PDFs generated by "Print to File" or "Export" in various applications. The bitmap font was probably installed as a consequence of installing the whole [xorg](https://www.archlinux.org/groups/x86_64/xorg/) group (which is usually NOT recommended). To solve the pixelized font problem, you can uninstall the package. Install [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) (Type 1) or [tex-gyre-fonts](https://www.archlinux.org/packages/?name=tex-gyre-fonts) (OpenType) for corresponding free subsitute of Helvetica (and other PostScript/PDF base fonts).

You may also experience similar problem when you open a PDF which requires Helvetica but does not have it embedded for viewing.

### FreeType Breaking Bitmap Fonts

Some users are reporting problems ([FS#52502](https://bugs.archlinux.org/task/52502)) with bitmap fonts having changed names after upgrading [freetype2](https://www.archlinux.org/packages/?name=freetype2) to version 2.7.1, creating havok in terminal emulators and several other programs such as [dwm](https://aur.archlinux.org/packages/dwm/) or [dmenu](https://www.archlinux.org/packages/?name=dmenu) by falling back to another (different) font. This was caused by the changes to the PCF font family format, which is described in their *release notes* [[4]](https://sourceforge.net/projects/freetype/files/freetype2/2.7.1/). Users transitioning from the old format might want to create a *font alias* to remedy the problems, like the solution which is described in [[5]](https://forum.manjaro.org/t/terminus-font-name-fix-after-freetype2-update-to-2-7-1-1/15530), given here too:

Assume we want to create an alias for [terminus-font](https://www.archlinux.org/packages/?name=terminus-font), which was renamed from `Terminus` to `xos4 Terminus` in the previously described [freetype2](https://www.archlinux.org/packages/?name=freetype2) update:

*   Create a configuration file in `/etc/fonts/conf.avail/` for the *font alias*:

 `/etc/fonts/conf.avail/33-TerminusPCFFont.conf` 
```
<?xml version="1.0"?>
 <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
 <fontconfig>
     <alias>
         <family>Terminus</family>
         <prefer><family>xos4 Terminus</family></prefer>
         <default><family>fixed</family></default>
     </alias>
 </fontconfig>

```

*   Create a symbolic link towards it in the `/etc/fonts/conf.d` directory. In our example we would link as follows: `ln -s /etc/fonts/conf.avail/33-TerminusPCFFont.conf /etc/fonts/conf.d` to make the change permanent.

Everything should now work as it did before the update, the *font alias* should not be in effect, but make sure to either reload `.Xresources` or restart the display server first so the affected programs can use the alias.

## See also

*   [Wikipedia:Fontconfig](https://en.wikipedia.org/wiki/Fontconfig "wikipedia:Fontconfig")
*   [Fonts in X11R6.8.2](http://www.x.org/X11R6.8.2/doc/fonts.html) - Official Xorg font information
*   [FreeType 2 overview](http://freetype.sourceforge.net/freetype2/)
*   [Gentoo font-rendering thread](https://forums.gentoo.org/viewtopic-t-723341.html)
*   [On slight hinting](http://www.freetype.org/freetype2/docs/text-rendering-general.html)