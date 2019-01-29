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
*   [3 Configuración](#Configuración)
    *   [3.1 FreeType autohinter (opcional)](#FreeType_autohinter_(opcional))
    *   [3.2 Deshabilitar las Fuentes de mapa de Bits que son feas (opcional)](#Deshabilitar_las_Fuentes_de_mapa_de_Bits_que_son_feas_(opcional))
*   [4 Preguntas Más Frecuentes](#Preguntas_Más_Frecuentes)

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

# Configuración

## FreeType autohinter (opcional)

Puedes establecer el autohinter de FreeType . Ejecuta como root :

```
ln -s /etc/fonts/conf.avail/10-autohint.conf /etc/fonts/conf.d/10-autohint.conf

```

## Deshabilitar las Fuentes de mapa de Bits que son feas (opcional)

Edita ~/.fonts.conf y pon el siguiente contenido:

```
   <selectfont>
       <rejectfont>
           <pattern>
               <patelt name="scalable">
                   <bool>false</bool>
               </patelt>
           </pattern>
       </rejectfont>
   </selectfont>

```

Reinicia las X (ctrl+alt+backspace)

Si al llegar a este punto piensas que las fuentes se ven muy gruesas, modifica el archivo de configuración de fuentes: edita (o créalo si no existe) el archivo ~/.fonts.conf con el siguiente contenido:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
    <match target="font" >
        <test compare="more" name="weight">
            <const>medium</const>
        </test>
        <edit mode="assign" name="autohint">
            <bool>false</bool>
        </edit>
    </match>
</fontconfig>

```

# Preguntas Más Frecuentes

**P. Mis fuentes son muy grandes o muy pequeñas. La resolución parece mala. Mis fuentes están deformes.**

R(1). Lea la sección*Display Size/DPI* de [Xorg](/index.php/Xorg "Xorg") donde encontrará un ejemplo de configuración.

R(2). Obtenga la resolución correcta desde una consola, ejecutando:

```
xdpyinfo | grep resolution

```

Cambie el valor a lo que entregue la salida de este comando en el configurador de fuentes de Gnome. Reinicie las X. Algunas veces la tarjeta de video entrega información equivocada a las X. Puede ser mejor establecer un valor entre 72-78 DPI para pantallas de 1024x768\. 96 DPI es un buen valor para 1280x1024, pero depende de la resolución exacta. Yo prefiero una resolución de 75 en el computador de micasa, y el tamaño de las fuentes parece ser un poco más fiel a su tamaño adecuado cuando ésto está establecido. En la mayoría de los casos, si los números no hacen juego, puede usar el siguiente método.

También puede optar a forzar a que las X partan con una resolución. Esto puede producir buenos resultados en algunos modos de pantalla. Por ejemplo puede usar:

```
startx -- -dpi 75

```

Esto forzará a las X a partir en el modo DPI de 75x75\. Puede cambiar sus ajustes de las fuentes de Gnome (En el menú Aplicaciones/Preferencias del Escritorio/Fuentes) a 75 DPI y debería obtener un buen ajuste.

Si esto funcionó bien para usted, puede editar su guión "startx" para forzar siempre esta opción a la partida. Edite el fichero "/usr/bin/startx" como root.

Cambie la siguiente línea:

```
defaultserverargs=""

```

para que diga...

```
defaultserverargs="-dpi 75"

```

**P. ¿Cómo instalo fuentes?**

R. Una manera fácil de instalar fuentes es guardarlas en el directorio "$HOME/.fonts" y correr "fc-cache". También puede realizar una instalación a través de todo el sistema copiando las fuentes al directorio "/usr/share/fonts" u otro directorio (siempre que esté listado en el archivo "/etc/fonts/fonts.conf"), y luego ejecutando el comando "fc-cache" como root. También puede necesitar ejecutar el comando "ttmkfdir" o "mkfontdir".

**P. Las fuentes en GNU Emacs son mostradas como cuadrados.**

R. Se debe instalar el paquete xorg-fonts-75dpi o xorg-fonts-100dpi.

**P. Las fuentes lucen muy mal en OpenOffice.org.**

R. Si se tiene un error/problema-de-fuentes en el paquete openoffice-base, usar el original rpm-packages desde el sitio web official siempre funciona. "Las fuentes malas son cosa del pasado con la nueva version (2.3.1)." ([http://www.stchman.com/tweaks.html](http://www.stchman.com/tweaks.html)).

Notar que OpenOffice.org para Linux con una (inferior) copia de freetype2 que son construidas directamente dentro del código. En el pasado se podia forzar a conectar al ordenar, compartido, freetype2 configurando lo siguiente antes de empezar la version.

```
export LD_PRELOAD=/usr/lib/xorg/modules/fonts/libfreetype.so

```

Lo anterior (Ene. 2008) esta reportado para no funcionar mas pero para qa.openoffice.org un patch para este transpaso se esta desarrollando

A. This can be changed in the OpenOffice.org configurator. From the drop-down menu, select "Tools/Options/OpenOffice.org/Fonts". Check the box that says "Apply Replacement Table". Type "Andale Sans UI" in the font box (this may have to be input manually, if it doesn't appear in the drop-down menu) **P. La fuente del menú de OpenOffice.org luce bastante mal. No usa antialiasing tampoco.**

R. Esto se puede cambiar en el configurador de OpenOffice.org. Desde el menu deslizante hacia abajo, seleccionar "Herramientas/Opciones/OpenOffice.org/Fuentes"("Tools/Options/OpenOffice.org/Fonts"). Verificar la casilla que dice "Aplicar tabla de reemplazo" ("Apply Replacement Table"). Escribir "Andale Sans UI" en la casilla de fuente (A lo mejor esto debera ser ingresado manualmente, si no aparece en el menu desplazado hacia abajo) y elegir la fuente que desees con la opcion "Reemplazar con" ("Replace With"). Usuarios de linea de codigos (Dropline users) pueden preferir el sistema predeterminado, "Trebuchet MS". Cuando está seleccionado, hacer clic en la caja de chequeo (checkmark box). Luego eligir las opciones "siempre" y "pantalla" ("always" y "screen") en la caja a continuación. Aplicar los cambios, ahora las fuentes de los menu deberia lucir bien.

**P. OpenOffice.org no detecta mis fuentes TrueType.**

R. Asegurarse que se han agregado las entradas apropiadas en el archivo /etc/X11/xorg.conf que apunta los programas al directorio /usr/share/fonts/

Por ejemplo, aquí hay un ejemplo de un archivo xorg.conf:

```
Section "Files"
    RgbPath         "/usr/share/X11/rgb"
    ModulePath      "/usr/lib/xorg/modules"
    FontPath        "/usr/share/fonts/misc"
    FontPath        "/usr/share/fonts/75dpi"
    FontPath        "/usr/share/fonts/100dpi"
    FontPath        "/usr/share/fonts/TTF"
    FontPath        "/usr/share/fonts/Type1"
EndSection

```

Otra solucion es ejecutar la herramienta de administración de openoffice

```
# /opt/openoffice/program/spadmin

```

Desde la cual se puede agregar fuentes.

**P. Mozilla y otros programas no pueden acceder a fuentes TrueType en el sistema, en vez de eso se revierten a fuentes feas**

R. Asegurarse que el modulo "freetype" esta cargado en el archivo /etc/X11/xorg.conf y en /usr/share/fonts/TTF/fonts.dir se listan todas las fuentes de TrueType que estan instaladas.

Intentar verificar las secciones de "Archivos" en el xorg.conf, y asegurarse que se tienen todos (o varios) estos directorios listados.

```
Section "Files"
    RgbPath         "/usr/share/X11/rgb"
    ModulePath      "/usr/lib/xorg/modules"
    FontPath        "/usr/share/fonts/misc"
    FontPath        "/usr/share/fonts/75dpi"
    FontPath        "/usr/share/fonts/100dpi"
    FontPath        "/usr/share/fonts/TTF"
    FontPath        "/usr/share/fonts/Type1"
EndSection

```

Finalmente, ir al siguiente directorio de fuentes:

```
/usr/share/fonts/TTF
/usr/share/fonts

```

Intentar borrando los archivos "fonts.dir" y "fonts.scale" en estos directorios. Se querrá hacer un respaldo de ellos primero. Ejecutar estos comandos para reeplazarlos:

```
mkfontscale
mkfontdir

```

Asegurarse de reiniciar X para que los efectos tomen efecto.

**P. Cuales son las fuentes sugeridas para Mozilla/Firefox?**

R. Estas fuentes son recomendadas para Firefox:

```
Proportional: Serif   Size (pixels): 16
Serif: Times New Roman
Sans-serif: Arial
Monospace: Courier New   Size (pixels): 13
Display resolution: System settings

```

*   Nota: Times New Roman puede aparecer como una fuente non-TTF. Si este es el caso, leer "como arreglar esto" mas abajo.

Las siguientes son Dropline's predeterminadas de Mozilla (también recomendadas):

```
Proportional: Serif   Size (pixels): 14
Serif: Times New Roman
Sans-serif: Verdana
Cursive: Andale Mono
Fantasy: Andale Mono
Monospace: Courier New   Size (pixels): 11
Allow Documents to use other fonts: Enabled
Display resolution: System settings

```

**P. Porqué mis aplicaciones se muestran como cuadrados cuando deberian ser flechas o similares?**

R. Esto puede ayudar a activar las fuentes bitmap. Están desactivadas por defecto.

```
cd /etc/fonts/conf.d
rm 10-bitmaps.conf
ln -s yes-bitmaps.conf 10-bitmaps.conf
cd -

```

Si tú crees que tus fuentes lucen feas ahora, considera remover los siguiente paquetes:

```
pacman -Rs xorg-fonts-100dpi xorg-fonts-75dpi

```

Leer [aquí](https://bbs.archlinux.org/viewtopic.php?t=21250) y [aquí](https://bbs.archlinux.org/viewtopic.php?t=18425) para mas información.

**P. Acabo de actualizar via pacman -Syu y todas mis fuentes son feas**

R. Aquí hay varios errores posibles en conflicto. Mirar estos enlaces:

1 - [https://bbs.archlinux.org/viewtopic.php?t=866](https://bbs.archlinux.org/viewtopic.php?t=866)

2 - [https://bbs.archlinux.org/viewtopic.php?t=4975](https://bbs.archlinux.org/viewtopic.php?t=4975)