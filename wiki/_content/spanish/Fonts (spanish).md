Artículos relacionados

*   [MS Fonts](/index.php/MS_Fonts "MS Fonts")
*   [Configuración de fuentes Xorg.](/index.php?title=Configuraci%C3%B3n_de_fuentes_Xorg.&action=edit&redlink=1 "Configuración de fuentes Xorg. (page does not exist)")

## Contents

*   [1 Introducción](#Introducci.C3.B3n)
    *   [1.1 Diferentes clases de fuentes](#Diferentes_clases_de_fuentes)
    *   [1.2 Instalando fuentes](#Instalando_fuentes)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 FreeType autohinter (opcional)](#FreeType_autohinter_.28opcional.29)
    *   [2.2 Deshabilitar las Fuentes de mapa de Bits que son feas (opcional)](#Deshabilitar_las_Fuentes_de_mapa_de_Bits_que_son_feas_.28opcional.29)
*   [3 Preguntas Más Frecuentes](#Preguntas_M.C3.A1s_Frecuentes)

## Introducción

La instalación estándar de un escritorio en Arch Linux nos proporcionará un gran soporte de fuentes, con las últimas versiones estables de X org, X server, freetype2 (con el intérprete bytecode habilitado) y fontconfig. Para más información sobre la configuración de fuentes, podéis visitar [Configuración de fuentes](/index.php?title=Configuraci%C3%B3n_de_fuentes&action=edit&redlink=1 "Configuración de fuentes (page does not exist)").

### Diferentes clases de fuentes

En Linux existen varias clases de fuentes.

*   fuentes bitmap (.pcf .bdf .pcf.gz .bdf.gz)
*   fuentes PostScript (.pfa .pfb)

(pfa:formato ascii; pfb:formato binario)

*   fuentes TrueType/OpenType (.ttf)

### Instalando fuentes

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