**Estado de la traducción**
Este artículo es una traducción de [Font configuration](/index.php/Font_configuration "Font configuration"), revisada por última vez el **2019-03-04**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Font_configuration&diff=0&oldid=566533) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

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
    *   [2.3 Optimización](#Optimización)
        *   [2.3.1 Intérprete Byte-Code (BCI)](#Intérprete_Byte-Code_(BCI))
        *   [2.3.2 Auto-optimizado](#Auto-optimizado)
        *   [2.3.3 Estilo de optimización](#Estilo_de_optimización)
    *   [2.4 Alineamiento de píxeles](#Alineamiento_de_píxeles)
    *   [2.5 Representación subpixel](#Representación_subpixel)
        *   [2.5.1 Filtro LCD](#Filtro_LCD)
        *   [2.5.2 Especificaciones avanzadas del filtro LCD](#Especificaciones_avanzadas_del_filtro_LCD)
    *   [2.6 Desactivar auto-hinter para fuentes en negrita](#Desactivar_auto-hinter_para_fuentes_en_negrita)
    *   [2.7 Reemplazar o establecer las fuentes por defecto](#Reemplazar_o_establecer_las_fuentes_por_defecto)
    *   [2.8 Lista blanca y lista negra de fuentes](#Lista_blanca_y_lista_negra_de_fuentes)
    *   [2.9 Desactivar fuentes bitmap](#Desactivar_fuentes_bitmap)
    *   [2.10 Desactivar escalado de fuentes bitmap](#Desactivar_escalado_de_fuentes_bitmap)
    *   [2.11 Crear estilos negrita e itálica para fuentes incompletas](#Crear_estilos_negrita_e_itálica_para_fuentes_incompletas)
    *   [2.12 Cambiar prioridad de las reglas](#Cambiar_prioridad_de_las_reglas)
    *   [2.13 Consultar la configuración actual](#Consultar_la_configuración_actual)
*   [3 Aplicaciones sin soporte fontconfig](#Aplicaciones_sin_soporte_fontconfig)
*   [4 Solución de problemas](#Solución_de_problemas)
    *   [4.1 Fuentes distorsionadas](#Fuentes_distorsionadas)
    *   [4.2 Calibri, Cambria, Monaco, etc. no se representan apropiadamente](#Calibri,_Cambria,_Monaco,_etc._no_se_representan_apropiadamente)
    *   [4.3 Applicaciones que ignoran hinting](#Applicaciones_que_ignoran_hinting)
    *   [4.4 Aplicaciones no recogen hinting de la configuración del entorno de escritorio](#Aplicaciones_no_recogen_hinting_de_la_configuración_del_entorno_de_escritorio)
    *   [4.5 Hinting incorrecto en aplicaciones GTK sobre sistemas no Gnome](#Hinting_incorrecto_en_aplicaciones_GTK_sobre_sistemas_no_Gnome)
    *   [4.6 Problema con la fuente Helvetica en PDFs generados](#Problema_con_la_fuente_Helvetica_en_PDFs_generados)
    *   [4.7 FreeType rompe fuentes Bitmap](#FreeType_rompe_fuentes_Bitmap)
*   [5 Véase también](#Véase_también)

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

### Optimización

[Hinting (en inglés)](https://en.wikipedia.org/wiki/Font_hinting "wikipedia:Font hinting") (optimización de la renderización) es el uso de instrucciones matemáticas para ajustar el contorno de la fuente de forma que se alinee a una cuadricula rasterizada ( es decir la cuadrícula de píxeles de la pantalla). Este efecto hace que la fuente sea más nítida y por lo tanto más legible. Las fuentes se alinean sin optimizarse cuando las pantallas tienen alrededor de 300 [ppp](https://en.wikipedia.org/wiki/es:Puntos_por_pulgada "wikipedia:es:Puntos por pulgada").

#### Intérprete Byte-Code (BCI)

Utilizando las optimizaciones del BCI las instrucciones en las fuentes TrueType se representan acorde con el intérprete FreeTypes. La optimización está *activada* por defecto. Para desactivarla:

```
  <match target="font">
    <edit name="hinting" mode="assign">
      <bool>false</bool>
    </edit>
  </match>

```

**Nota:** Puede cambiar las implementaciones BCI editando `/etc/profile.d/freetype2.sh` que incluye una breve documentación. Los valores posibles son `truetype:interpreter-version=35` (modo clásico, emula Windows 98; 2.6 por defecto), `truetype:interpreter-version=38` (modo subpixel "ifinito"), `truetype:interpreter-version=40` (modo subpixel minimo; 2.7 por defecto). La renderización subpixel debe utilizar al BCI subpixel. Para más detalles, vea [[1]](https://www.freetype.org/freetype2/docs/subpixel-hinting.html).

#### Auto-optimizado

El auto-optimizado intenta optimizar automáticamente y obvia toda la información de optimización. Originalmente era la que estaba por defecto porque las fuentes TrueType2 estaban patentadas pero ahora esas patentes expiraron y esa es la pequeña razón para utilizarla. Funciona mejor con fuentes que no tienen información de optimización o que dicha información este defectuosa, pero sobre-optimiza fuentes con una información de optimización válida. Generalmente las fuentes son del último tipo y auto-optimizado no es útil. El auto-optimizado está *desactivado* por defecto. Para activarlo:

```
  <match target="font">
    <edit name="autohint" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

#### Estilo de optimización

El estilo de optimizado (hintstyle) es la cantidad de remodelado de fuentes que se utiliza para alinearla a la cuadricula. Los valores de optimización son: `hintnone`, `hintslight`, `hintmedium`, y `hintfull`. `hintslight` hará la fuente más borrosa para alinearla a la cuadrícula pero con una mejor conservación de la forma de la fuente (vea [[2]](https://www.freetype.org/freetype2/docs/text-rendering-general.html)), mientras `hintfull` la hará más nítida para que se alinee bien a la cuadrícula pero se pierde bastante la forma de la fuente. `hintslight` usa solo el auto-optimizado en un modo vertical a favor de la información nativa de las fuentes no-CFF (*.otf*).

`hintslight` es la configuración por defecto. Para cambiarla:

```
  <match target="font">
    <edit name="hintstyle" mode="assign">
      <const>hintnone</const>
    </edit>
  </match>

```

**Nota:** Algunas aplicaciones, como [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") puede [sobrescribir los ajustes de optimización por defecto.](#Solución_de_problemas)

### Alineamiento de píxeles

Muchos monitores fabricados hoy en día utilizan las especificaciones rojo, verde, azul (RGB, red, green, blue). Fontconfig necesita conocer su tipo de monitor para poder mostrar las fuentes correctamente. Los monitores son: **RGB** (más común), **BGR**, **V-RGB** (vertical), or **V-BGR**. Un test del monitor se puede encontrar [aquí](http://www.lagom.nl/lcd-test/subpixel.php).

```
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>rgb</const>
    </edit>
  </match>

```

**Nota:** Sin la representación subpixel (vea abajo), freetype solo se ocupará sobre la alineación (vertical o horizontal) de los subpíxeles. Por ejemplo, no diferencia entre **RGB** y **BGR**.

### Representación subpixel

[La representación subpixel](https://en.wikipedia.org/wiki/es:Renderizaci%C3%B3n_de_subpixel "wikipedia:es:Renderización de subpixel") es una técnica para mejorar la nitidez de las fuentes triplicando la resilución horizontal (o vertical) a través del uso de los subpixel. En los sistemas Windows, esta técnica se llama "ClearType".

FreeType implementa su propio renderizador optimizado LCD llamado [Harmony](http://lists.gnu.org/archive/html/freetype-commit/2017-03/msg00012.html). Con esta tecnología de renderizado LCD, el resultado no requiere ningún filtro LCD adicional, no como renderizador subpixel patentado de Microsoft ClearType donde se recomienda un filtro LCD. Vea abajo la sección cómo activar el filtro LCD y sus beneficios.

El renderizador subpixel ClearType está protegido por las patentes de Microsoft y **desactivado** por defecto en Arch Linux. Para habilitarlo, tiene que recompilar [freetype2](https://www.archlinux.org/packages/?name=freetype2) y definir la macro `FT_CONFIG_OPTION_SUBPIXEL_RENDERING`, o utilizar p.ej. el paquete del AUR [freetype2-cleartype](https://aur.archlinux.org/packages/freetype2-cleartype/).

#### Filtro LCD

Cuando utilize el renderizador subpixel ClearType, debe de activar el filtro LCD, que está diseñado para reducir la franja de color. Está descrito en [Filtrar LCD (en inglés)](https://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html) en la referencia de la API FreeType 2\. Las diferentes opciones están descritas en [FT_LcdFilter](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html#FT_LcdFilter), y están ilustradas en la página [test de filtros LCD](http://www.spasche.net/files/lcdfiltering/).

El filtro `lcddefault` será suficiente para la mayoría de los usuarios. Otros filtros están disponibles y se pueden utilizar en situaciones especiales: `lcdlight`; un filtro ligero ideales para fuentes que se ven demasiado borrosas o negrita, `lcdlegacy`, el filtro original Cairo; y `lcdnone` para desactivarlo completamente.

```
  <match target="font">
    <edit name="lcdfilter" mode="assign">
      <const>lcddefault</const>
    </edit>
  </match>

```

#### Especificaciones avanzadas del filtro LCD

Si los filtros LCD incluidos no le resultan satisfactorios, es posible retocar el renderizador de fuentes de forma muy específica construyendo un paquete freetype2 personalizado y modificar los filtros codificados. El [sistema de construcción de Arch](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") se puede utilizar para construir e instalar paquetes desde código fuente. Esto requiere la instalación del paquete [asp](https://www.archlinux.org/packages/?name=asp).

Revise el PKGBUILD de [freetype2](https://www.archlinux.org/packages/?name=freetype2) y descargue/extraiga los archivos:

```
$ asp checkout freetype2
$ cd freetype2/trunk
$ makepkg -o

```

Para activar el renderizado subpixel edite el archivo `src/freetype-VERSION/include/freetype/config/ftoption.h` y descomente la macro `FT_CONFIG_OPTION_SUBPIXEL_RENDERING`.

Después, edite el archivo `src/freetype-VERSION/src/base/ftlcdfil.c` y busque la definición de la constante `default_filter[5]`:

```
static const FT_Byte  default_filter[5] =
    { 0x10, 0x40, 0x70, 0x40, 0x10 };

```

Esta constante define un filtro que suaviza el glifo renderizado. Modifiquelo tanto como sea necesario. (referencia: [lista de discusión freetype (en inglés)](https://lists.nongnu.org/archive/html/freetype/2006-09/msg00069.html)) Guarde el archivo, construyalo e instale el paquete personalizado:

```
$ makepkg -e
# pacman -Rd freetype2
# pacman -U freetype2-VERSION-ARCH.pkg.tar.xz

```

Reinicie o reinicie X. El filtro lcddefault debe renderizar las fuentes de forma diferente.

### Desactivar auto-hinter para fuentes en negrita

Auto-hinter utiliza métodos sofisticados para renderizar fuentes, pero a veces hace que las fuentes sean demasiado grandes. Afortunadamente, una solución es desactivar autohinter para fuentes en negritas mientras que para el resto sige activado:

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

### Reemplazar o establecer las fuentes por defecto

La forma más fiable de hacer esto es añadir un fragmento XML similar al que hay abajo. *Utilizar el atributo "Unión (binding)" le dará mejores resultados*, por ejemplo, en Firefox cuando no quiera cambiar las propiedades de la fuente que se está reemplazando. Esto hará que Ubuntu se use en vez de Georgia:

```
...
 <match target="pattern">
   <test qual="any" name="family"><string>georgia</string></test>
   <edit name="family" mode="assign" binding="same"><string>Ubuntu</string></edit>
 </match>
...

```

El enfoque alternativo es establecer la fuente "preferida", pero *esto solo funciona si la fuente original no está en el sistema*, en este caso se sustituirá el valor especificado:

```
...
<!-- Reemplazando Helvetica con Bitstream Vera Sans Mono -->
<!-- Nota, debe existir un alias para Helvetica en los archivos de configuración por defecto -->
<alias>
    <family>Helvetica</family>
    <prefer><family>Bitstream Vera Sans Mono</family></prefer>
    <default><family>fixed</family></default>
</alias>
...

```

### Lista blanca y lista negra de fuentes

El elemento `<selectfont>` se usa en conjunto con los elementos `<acceptfont>` y `<rejectfont>` para seleccionar las fuentes en las listas blanca y negra y resolver las coincidencias y solicitudes. El más simple y el más típico caso es rechazar una fuente que necesita instalarse, sin embargo coincide con una fuente genérica que puede causar problemas en las interfaces de las aplicaciones.

Primero obtenga el nombre de la familia de la fuente:

 `$ fc-scan .fonts/lklug.ttf --format='%{family}
'`  `LKLUG` 

Después utilice ese nombre de la familia en la estrofa `<rejectfont>`:

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

Normalmente cuando ambos elementos se combinan, `<rejectfont>` se usa primero de una forma general para rechazar un gran grupo (como todo un directorio), después `<acceptfont>` se utiliza para poner en la lista blanca fuentes especificas que están en el gran grupo de la lista negra.

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

### Desactivar fuentes bitmap

Las fuentes mapa de bits (bitmap) se utilizan a veces como alternativa de una fuente que falta, puede hacer que el texto se represente pixelado o muy grande. Utilice el [ajuste predeterminado](#Ajustes_predeterminados) `70-no-bitmaps.conf` para desactivar este comportamiento.

Para desactivar bitmap incrustado para todas las fuentes:

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

Para desactivar bitmap incrustado para una fuente específica:

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

### Desactivar escalado de fuentes bitmap

Para desactivar el escalado de las fuentes bitmap (lo que a veces los emborrona), elimine `/etc/fonts/conf.d/10-scale-bitmap-fonts.conf`.

### Crear estilos negrita e itálica para fuentes incompletas

FreeType tiene la habilidad de crear automáticamente los estilos **itálica** y **negrita** para fuentes que no los tienen, pero solo si la aplicación lo requiere. Los programas raramente envían estas peticiones, esta sección cubre la generación forzada de los estilos faltantes.

Empiece editando `/usr/share/fonts/fonts.cache-1` como se explica abajo. Guarde una copia de la modificación en otro archivo porque la actualización de fuentes con `fc-cache` sobrescribirá `/usr/share/fonts/fonts.cache-1`.

Asumiendo que la fuente Dupree está instalada:

```
"dupree.ttf" 0 "Dupree:style=Regular:slant=0:weight=80:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Duplique la linea, cambie `style=Regular` a `style=Bold` o cualquier otro estilo. Cambie también `slant=0` a `slant=100` para itálica, `weight=80` a `weight=200` para negrita, o combinelas para ***negrita e itálica***:

```
"dupree.ttf" 0 "Dupree:style=Bold Italic:slant=100:weight=200:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Ahora añada las modificaciones necesarias a `$XDG_CONFIG_HOME/fontconfig/fonts.conf`:

```
...
<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
         <!-- otras fuentes aqui .... -->
     </test>
     <test name="weight" compare="more_eq"><int>140</int></test>
     <edit name="embolden" mode="assign"><bool>true</bool></edit>
</match>

<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
        <!-- otras fuentes aqui .... -->
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

**Sugerencia:** Utilice el valor `embolden` para las fuentes negritas existentes para hacerlas aún mas negritas.

### Cambiar prioridad de las reglas

Fontconfig procesa archivos de `/etc/fonts/conf.d` en un orden numérico. Esto activa reglas o archivos que se anulan unos a otros, pero a menudo confunde a los usuarios cobre cual es el último archivo que se analiza.

Para garantizar que los ajustes personales tienen preferencia sobre cualquier regla, cambie el orden:

```
# cd /etc/fonts/conf.d
# mv 50-user.conf 99-user.conf

```

Este cambio parece innecesario para la mayoría de los casos, porque el usuario tiene suficiente control por defecto para establecer sus propias preferencias, hinting y propiedades antialiasing, alias de nuevas fuentes para generar familias de fuentes, etc.

### Consultar la configuración actual

Para ver qué ajustes están aplicandose, utilize `fc-match --verbose`. p.ej.

 `$ fc-match --verbose Sans` 
```
family: "DejaVu Sans"(s)
hintstyle: 3(i)(s)
hinting: True(s)
...

```

Busque el significado de los números en [fonts-conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fonts-conf.5) P.ej. 'hintstyle: 3' significa 'hintfull'.

## Aplicaciones sin soporte fontconfig

Algunas aplicaciones como [URxvt](/index.php/URxvt "URxvt") ignoran los ajustes fontconfig. Puede abordarlo utilizando `~/.Xresources`, pero es tan flexible como fontconfig. Por Ejemplo (vea [Configuración de FontConfig](#Configuración_de_FontConfig) para las explicaciones de las opciones):

 `~/.Xresources` 
```
Xft.autohint: 0
Xft.lcdfilter: lcddefault
Xft.hintstyle: hintslight
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

```

Asegúrese que los ajustes se cargan apropiadamente cuando X se inicia con `xrdb -q` (vea [Xresources (en inglés)](/index.php/Xresources "Xresources") para más información).

## Solución de problemas

### Fuentes distorsionadas

**Nota:** 96 ppp no es estándar. Debe de utilizar sus ppp actuales de su monitor para que las fuentes se rendericen adecuadamente, especialmente cuando se utiliza el renderizado subpixel.

Si las fuentes de forma inesperada se ven grandes o pequeñas, mal proporcionadas o simplemente mal renderizadas, fontconfig puede estar utilizando unos ppp incorrectos.

Fontconfig debe ser capaz de detectar los parámetros ppp que Xorg server descubre. Puede comprobar automáticamente los ppp descubiertos con `xdpyinfo` (proporcionado por el paquete [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo)):

 `$ xdpyinfo | grep dots` 
```
  resolution:    102x102 dots per inch

```

Si los ppp que se detectan son incorrectos (usualmente debido a un [EDID](https://en.wikipedia.org/wiki/es:EDID "wikipedia:es:EDID") del monitor incorrecto) puede especificar manualmente la configuración de Xorg, vea [Tamaño de la pantalla y DPI](/index.php/Xorg_(Espa%C3%B1ol)#Tamaño_de_la_pantalla_y_DPI "Xorg (Español)"). Esta es la solución recomendada, pero puede que no funcione con controladores buggy.

Fontconfig por defecto irá a la variable Xft.dpi si está establecida. Xft.dpi lo establecen normalmente los entornos de escritorio (generalmente los ajustes ppp de Xorg) o manualmente en `~/.Xdefaults` o `~/.Xresources`. Utilice xrdb para consultar el valor:

 `$ xrdb -query | grep dpi` 
```
Xft.dpi:	102

```

Aquellos que todavía tienen problemas pueden volver manualmente a la configuración ppp utilizada por fontconfig:

```
...
<match target="pattern">
   <edit name="dpi" mode="assign"><double>102</double></edit>
</match>
...

```

### Calibri, Cambria, Monaco, etc. no se representan apropiadamente

Algunas fuentes escalables tienen versiones bitmap incrustados que se representan en su lugar, principalmente en los tamaños pequeños. Utilizar [Fuentes compatibles con la métrica (en inglés)](/index.php/Metric-compatible_fonts "Metric-compatible fonts") como sustituto puede mejorar la representación en estos casos.

También puede forzar que se utilice fuentes escalables para todos los tamaños con [deshabilitar bitmap incrustado](#Desactivar_fuentes_bitmap), sacrificando alguna calidad de renderizado.

### Applicaciones que ignoran hinting

Algunas aplicaciones o entornos de escritorio pueden anular la configuración hinting de fontconfig y anti-aliasing por defecto. Esto puede ocurrir con [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") 3, por ejemplo mientras utiliza aplicaciones Qt como [vlc](https://www.archlinux.org/packages/?name=vlc) o [smplayer](https://www.archlinux.org/packages/?name=smplayer). Utilice la configuración del programa específico de la aplicación para estos casos. Para GNOME, pruebe [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

### Aplicaciones no recogen hinting de la configuración del entorno de escritorio

Por ejemplo, en GNOME a veces ocurre que Firefox aplica hinting completo en vez del valor "ninguno" en los ajustes de GNOME, que termina con unas fuentes afiladas y ampliadas. En este caso tendría que añadir ajustes hinting al archivo `fonts.conf`:

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

En este ejemplo, hinting se establece a "escala de grises".

### Hinting incorrecto en aplicaciones GTK sobre sistemas no Gnome

[GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") utiliza el sistema XSETTINGS para configurar la renderización de fuentes. Fuera de GNOME, aplicaciones GTK confían en fontconfig, pero algunas fuentes obtienen un hinting incorrecto causando que se vean demasiado negritas o demasiado finas.

Una solución simple es utilizar [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/) para proporcionar la configuración, por ejemplo:

 `~/.xsettingsd` 
```
Xft/Hinting 1
Xft/RGBA "rgb"
Xft/HintStyle "hintslight"
Xft/Antialias 1

```

También puede simplemente escribir en la configuración de la fuente como directivas `Xft.*` en `~/.Xresources` sin utilizar un demonio configurador.

### Problema con la fuente Helvetica en PDFs generados

En el siguiente comando

```
fc-match helvetica

```

produce

```
helvR12-ISO8859-1.pcf.gz: "Helvetica" "Regular"

```

entonces la fuente bitamp proporcionada por [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) es probable que se incruste dentro del PDF generado por "Imprimir a un archivo" o "Exportar" en varias aplicaciones. La fuente bitmap probablemente estaba instalada como consecuencia de instalar el grupo de la familia [xorg](https://www.archlinux.org/groups/x86_64/xorg/) (que normalmente NO se recomienda). Para solucionar el problema de la fuente pixelada, puede desinstalar el paquete. Instalar [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) (Type 1) o [tex-gyre-fonts](https://www.archlinux.org/packages/?name=tex-gyre-fonts) (OpenType) para una adecuada sustitución libre de Helvetica (y otras fuentes basadas en PostScript/PDF).

Puede experimentar problemas similares cuando abra un PDF que requiera Helvetica pero no la tiene incrustada para ver.

### FreeType rompe fuentes Bitmap

Algunos usuarios están reportando problemas ([FS#52502](https://bugs.archlinux.org/task/52502)) con las fuentes bitmap tienen nombres cambiados después de actualizar [freetype2](https://www.archlinux.org/packages/?name=freetype2) a la versión 2.7.1, creando havok en emuladores de terminal y otros muchos programas como [dwm](https://aur.archlinux.org/packages/dwm/) o [dmenu](https://www.archlinux.org/packages/?name=dmenu) utilizando como fuentes alternativas otras fuentes diferentes. Esto se causó por los cambios del formato de la familia de fuentes PCF, que como se describe en *notas de la versión* [[3]](https://sourceforge.net/projects/freetype/files/freetype2/2.7.1/). Usuarios que han realizado la transición del antiguo formato podrían crear un *alias de fuente* para resolver los problemas, como la solución que se describe en [[4]](https://forum.manjaro.org/t/terminus-font-name-fix-after-freetype2-update-to-2-7-1-1/15530), dada aquí también:

Asuma que queremos crear un alias para [terminus-font](https://www.archlinux.org/packages/?name=terminus-font), que se renombró de `Terminus` a `xos4 Terminus` en la anterior actualización de [freetype2](https://www.archlinux.org/packages/?name=freetype2) descrita previamente:

*   Crea un archivo de configuración en `/etc/fonts/conf.avail/` para el *alias de fuente*:

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

*   Crea un enlace simbólico hacia el directorio `/etc/fonts/conf.d`. En nuestro ejemplo deberíamos enlazarlo así: `ln -s /etc/fonts/conf.avail/33-TerminusPCFFont.conf /etc/fonts/conf.d` para hacer que los cambios sean permanentes.

Todo debería funcionar como lo hacía antes de la actualización, el *alias de fuente* no debería surtir efecto, pero asegúrese de que recarga `.Xresources` o reinicia el servidor de la pantalla antes de que los programas afectados puedan utilizar el alias.

## Véase también

*   [Fontconfig Wikipedia](https://en.wikipedia.org/wiki/Fontconfig "wikipedia:Fontconfig")
*   [Fuentes en X11R6.8.2](http://www.x.org/X11R6.8.2/doc/fonts.html) - Información oficial de la fuente Xorg
*   [FreeType 2 visión general](http://freetype.sourceforge.net/freetype2/)
*   [Hilo de la representación de fuentes Gentoo](https://forums.gentoo.org/viewtopic-t-723341.html)
*   [hinting leve](http://www.freetype.org/freetype2/docs/text-rendering-general.html)