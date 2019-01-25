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
*   [2 Instalando fuentes](#Instalando_fuentes)
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

## Instalando fuentes

En un sistema Linux moderno, añadir e instalar fuentes resulta mucho más fácil que antes. Veremos a continuación algunos consejos que harán el proceso más claro y asequible para el usuario medio. En primer lugar hemos de plantearnos el lugar donde se guardarán las nuevas fuentes. En general, los directorios más usados son:

*   /usr/share/fonts
*   /usr/X11R6/lib/X11/fonts

De esta manera todos los usuarios del sistema tendrán acceso a ellas (siempre bajo privilegios de root). Copiarlas a ~/.fonts puede ser también una buena idea.

En Arch Linux disponemos de algunas colecciones de fuentes ya preempaquetadas. Para buscarlas podemos ejecutar

```
pacman -Ss fonts

```

Entre los paquetes disponibles podemos encontrar

```
extra/artwiz-fonts 1.3-3
 This is set of (improved) artwiz fonts.
extra/ttf-ms-fonts 2.0-1
 Un-extracted TTF Fonts from Microsoft

```

Para la instalación de los paquetes hacemos:

```
pacman -S artwiz-fonts ttf-ms-fonts

```

De esta manera, las fuentes quedarán bajo el directorio /usr/X11R6/lib/X11/fonts. Se recomienda a los usuarios CJK (chinos, japoneses y coreanos) la instalación de ttf-arphic-uming, ttf-arphic-ukai y ttf-fireflysung para una visualización apropiada

Otra opción podría ser el uso de KDE *Font Installer*, en KDE *Control Center*. Funciona perfectamente para aquellos que usen KDE. Además, las fuentes pueden ser instaladas manualmente bajo los tres directorios arriba especificados. En ese caso, como root hemos de hacer

```
fc-cache -vf

```

{translate_me}

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