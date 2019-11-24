**Estado de la traducción**
Este artículo es una traducción de [Linux console](/index.php/Linux_console "Linux console"), revisada por última vez el **2019-11-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Linux_console&diff=0&oldid=589649) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Linux console/Keyboard configuration](/index.php/Linux_console/Keyboard_configuration "Linux console/Keyboard configuration")
*   [Screen capture#Virtual console](/index.php/Screen_capture#Virtual_console "Screen capture")
*   [Color output in console](/index.php/Color_output_in_console "Color output in console")
*   [getty](/index.php/Getty "Getty")

Según [Wikipedia](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"):

	La **consola de Linux** es una consola del sistema interno del [kernel de Linux](/index.php/Linux_kernel "Linux kernel"). La consola de Linux proporciona una manera para que el kernel y otros procesos envíen resultados de texto al usuario y reciban entradas de texto del usuario. El usuario generalmente ingresa texto con un teclado de ordenador y lee el texto de salida en un monitor de ordenador. El kernel de Linux admite consolas virtuales, esto es consolas que están lógicamente separadas, pero que acceden al mismo teclado y pantalla físicos.

Este artículo describe los conceptos básicos de la consola de Linux y cómo configurar la visualización del tipo de letra. La configuración del teclado se describe en la subpágina [Linux console/Keyboard configuration](/index.php/Linux_console/Keyboard_configuration "Linux console/Keyboard configuration").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Implementación](#Implementación)
    *   [1.1 Consolas virtuales](#Consolas_virtuales)
    *   [1.2 Modo texto](#Modo_texto)
    *   [1.3 Consola framebuffer](#Consola_framebuffer)
*   [2 Atajos del teclado](#Atajos_del_teclado)
*   [3 Tipografías](#Tipografías)
    *   [3.1 Vista previa y cambios temporales](#Vista_previa_y_cambios_temporales)
    *   [3.2 Configuración permanente](#Configuración_permanente)
    *   [3.3 HiDPI](#HiDPI)
*   [4 Véase también](#Véase_también)

## Implementación

La consola, a diferencia de la mayoría de los servicios que interactúan directamente con los usuarios, se implementa en el kernel. Esto contrasta con el software de emulación de terminal, como [Xterm](/index.php/Xterm "Xterm"), que se implementa en el espacio del usuario como una aplicación normal. La consola siempre ha sido parte de los kernel de Linux liberados, pero ha sufrido cambios en su historia, especialmente la transición al uso de [framebuffer](https://en.wikipedia.org/wiki/Linux_framebuffer "wikipedia:Linux framebuffer") y soporte para [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode").

A pesar de las muchas mejoras en la consola, su compatibilidad con versiones anteriores de hardware heredado significa que es limitada en comparación con un emulador de terminal gráfico.

### Consolas virtuales

La consola se presenta al usuario como una serie de [consolas virtuales](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"). Estas dan la impresión de que varios terminales independientes se ejecutan simultáneamente. Cada consola virtual puede iniciar sesión con diferentes usuarios, ejecutar su propio intérprete de órdenes y tener su propia configuración de tipografía. Cada una de las consolas virtuales utiliza un dispositivo `/dev/ttyX`, y se puede alternar entre ellas presionando `Alt+F*x*` (donde `*x*` es igual al número de la consola virtual, comenzando con 1). El dispositivo `/dev/console` se asigna automáticamente a la consola virtual activa.

Véase también [chvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chvt.1), [openvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/openvt.1) y [deallocvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/deallocvt.1).

### Modo texto

Dado que Linux originalmente comenzó como un kernel para hardware de PC, la consola se desarrolló utilizando gráficos estándar [CGA/EGA/VGA](https://en.wikipedia.org/wiki/VGA "wikipedia:VGA") de IBM, que todos los PC admitían en ese momento. Los gráficos funcionan en modo de texto VGA, que proporciona una pantalla simple de 80x25 caracteres con 16 colores. Este modo heredado es similar a las capacidades de los terminales de texto dedicados, como la serie [DEC VT100](https://en.wikipedia.org/wiki/VT100 "wikipedia:VT100"). Todavía es posible arrancar en modo texto si el hardware del sistema lo admite, pero casi todas las distribuciones modernas (incluida Arch Linux) utilizan la consola framebuffer.

### Consola framebuffer

Como Linux fue portado a otras arquitecturas que no eran de PC, se requirió una mejor solución, ya que otras arquitecturas no usaban adaptadores gráficos compatibles con VGA y era posible que no admitieran modos de texto. La consola framebuffer se implementó para proporcionar una consola estándar en todas las plataformas y, por lo tanto, presenta la misma interfaz de estilo VGA independientemente del hardware gráfico subyacente. Como tal, la consola de Linux no es un emulador de terminal, sino un terminal en sí mismo. Utiliza el tipo de terminal `linux`, y es ampliamente compatible con VT100.

## Atajos del teclado

| Atajos del teclado | Descripción |
| `Ctrl+Alt+Del` | Reinicia el equipo (especificado por el enlace simbólico `/usr/lib/systemd/system/ctrl-alt-del.target`) |
| `Alt+F1`, `F2`, `F3`, ... | Alterna a la consola virtual *«n»* (número) |
| `Alt+ ←` | Cambia a la consola virtual anterior |
| `Alt+ →` | Cambia a la consola virtual siguiente |
| `Scroll Lock` | Cuando el bloqueo de desplazamiento está activado, la entrada/salida está bloqueada |
| `Shift+PgUp`/`PgDown` | Desplaza el búfer de la consola hacia arriba/abajo |
| `Ctrl+c` | Mata la tarea actual |
| `Ctrl+d` | Inserta un EOF (fin de archivo) |
| `Ctrl+z` | Pausa la tarea actual |

Véase también [console_codes(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/console_codes.4).

## Tipografías

**Nota:** esta sección trata sobre [consola de Linux](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"). Para obtener soluciones de consola alternativas que ofrecen más funciones (fuentes tipográficas Unicode completas, adaptadores gráficos modernos, etc.), consulte [fbterm](/index.php/Fbterm "Fbterm"), [KMSCON](/index.php/KMSCON "KMSCON") o proyectos similares.

De forma predeterminada, la [consola virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") utiliza la fuente incorporada del kernel con un conjunto de caracteres [CP437](https://en.wikipedia.org/wiki/CP437 "wikipedia:CP437"), pero esto se puede cambiar fácilmente.

La [consola de Linux](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console") usa la codificación UTF-8 de forma predeterminada, pero debido a que se usa el framebuffer compatible con VGA estándar, la fuente tipográfica de la consola está limitada a un [glifo](https://en.wikipedia.org/wiki/es:Glifo "wikipedia:es:Glifo") estándar de 256 o 512\. Si la fuente tipográfica tiene más de 256 glifos, la cantidad de colores se reduce de 16 a 8\. Para asignar el símbolo correcto para que se muestre al valor Unicode dado, se necesita un mapa de traducción especial, a menudo llamado *unimap*. Hoy en día, la mayoría de las fuentes tipográficas de la consola tienen incorporado *unimap*; históricamente, tuvo que cargarse por separado.

El paquete [kbd](https://www.archlinux.org/packages/?name=kbd) proporciona herramientas para cambiar el tipo de letra de la consola virtual y la asignación de fuentes tipográficas. Las fuentes tipográficas disponibles se guardan en el directorio `/usr/share/kbd/consolefonts/`, las que terminan en *.psfu* or *.psfu.gz* tienen un mapa de traducción Unicode incorporado.

Los mapas de teclas («keymaps»), esto es la conexión entre la tecla presionada y el carácter utilizado por el ordenador, se encuentran en los subdirectorios de `/usr/share/kbd/keymaps/`, consulte [Linux console/Keyboard configuration](/index.php/Linux_console/Keyboard_configuration "Linux console/Keyboard configuration") para obtener más detalles.

**Nota:** reemplazar el tipo de letra puede causar problemas con los programas que esperan una tipografía de estilo VGA estándar, como los que usan gráficos de dibujo lineal.

**Sugerencia:** para los idiomas europeos escritos en letras latinas/griegas, pueden usar la tipografía `eurlatgr`, que incluye una amplia gama de variaciones de letras latinas/griegas, así como caracteres especiales [[2]](https://lists.altlinux.org/pipermail/kbd/2014-February/000439.html).

### Vista previa y cambios temporales

**Sugerencia:** una biblioteca organizada de imágenes para su visualización está disponible en: [Linux console fonts screenshots](http://alexandre.deverteuil.net/pages/consolefonts/).

```
$ showconsolefont

```

muestra una tabla de glifos o letras de una tipografía.

`setfont` cambia temporalmente la fuente tipográfica si se pasa un nombre de tipo de letra (en `/usr/share/kbd/consolefonts/`) como

```
$ setfont lat2-16 -m 8859-2

```

Los nombres de las fuentes tipográficas distinguen entre mayúsculas y minúsculas. Sin ningún parámetro, `setfont` devuelve la consola al tipo de letra predeterminado.

Entonces, para tener una fuente tipográfica **8x8 pequeña**, con ese tipo de letra instalado, como se ve a continuación, utilice, por ejemplo:

```
$ setfont -h8 /usr/share/kbd/consolefonts/drdos8x8.psfu.gz

```

Para tener una fuente tipográfica **más grande**, el tipo de letra Terminus ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font)) está disponible en muchos tamaños, como `ter-132n` que es grande.

**Sugerencia:** todas las órdenes de cambio de fuente se pueden escribir en «blind».

**Nota:** *setfont* solo funciona en la consola que se está utilizando actualmente. Cualquier otra consola, activa o inactiva, no se ve afectada.

### Configuración permanente

La variable `FONT` en `/etc/vconsole.conf` se usa para configurar la fuente tipográfica en el arranque, de forma permanente para todas las consolas. Vea [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) para más detalles.

Para mostrar caracteres como *Č, ž, đ, š* or *Ł, ę, ą, ś* utilizando la fuente `lat2-16.psfu.gz`:

 `/etc/vconsole.conf` 
```
...
FONT=lat2-16
FONT_MAP=8859-2
```

Significa que la segunda parte de los caracteres ISO/IEC 8859 se utiliza con el tamaño 16\. Puede cambiar el tamaño de fuente tipográfica utilizando otros valores (por ejemplo, `lat2-08`). Para las regiones determinadas por la especificación 8859, mire la [Wikipedia:ISO/IEC 8859#The parts of ISO/IEC 8859](https://en.wikipedia.org/wiki/ISO/IEC_8859#The_parts_of_ISO.2FIEC_8859 "wikipedia:ISO/IEC 8859").

Para usar la fuente tipográfica especificada en el espacio de usuario inicial, use el hook`consolefont` en `/etc/mkinitcpio.conf`. Vea [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") para más información.

Si parece que las fuentes tipográficas no cambian en el arranque, o cambian solo temporalmente, lo más probable es que se restablecieron cuando se inicializó el controlador gráfico y la consola se cambió a framebuffer. Para evitar esto, cargue su controlador gráfico antes. Consulte, por ejemplo, [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"), [[3]](https://bbs.archlinux.org/viewtopic.php?id=145765) u otras formas de configurar su framebuffer antes de aplicar `/etc/vconsole.conf`.

### HiDPI

Consulte [HiDPI#Linux console](/index.php/HiDPI#Linux_console "HiDPI").

## Véase también

*   [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting")
*   [The TTY demystified – Linus Åkesson](https://www.linusakesson.net/programming/tty/)