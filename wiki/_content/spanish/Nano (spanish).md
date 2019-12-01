**Estado de la traducción**
Este artículo es una traducción de [nano](/index.php/Nano "Nano"), revisada por última vez el **2019-11-27**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Nano&diff=0&oldid=590241) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[GNU nano](https://www.nano-editor.org/) (o nano) es un editor de texto cuya finalidad es presentar una interface simple con opciones de órdenes intuitivas para la edición de texto basada en consola. *nano* admite funciones que incluyen resaltado coloreado de la sintaxis, conversión de tipos de archivos DOS/Mac, corrección ortográfica y codificación [UTF-8](https://en.wikipedia.org/wiki/UTF-8 "wikipedia:UTF-8"). *nano* se inicia con un búfer vacío que generalmente ocupa menos de 4 MB alojado en la memoria.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Resaltado de sintaxis](#Resaltado_de_sintaxis)
        *   [2.1.1 Forth](#Forth)
        *   [2.1.2 PKGBUILD](#PKGBUILD)
    *   [2.2 Suspensión](#Suspensión)
    *   [2.3 Ajuste de texto](#Ajuste_de_texto)
*   [3 Utilización](#Utilización)
    *   [3.1 Funciones especiales](#Funciones_especiales)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Reemplazar vi con nano](#Reemplazar_vi_con_nano)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 Conflictos con combinaciones de teclas](#Conflictos_con_combinaciones_de_teclas)
*   [6 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [nano](https://www.archlinux.org/packages/?name=nano).

## Configuración

La apariencia, experiencia y funcionamiento de nano, generalmente, se controlan mediante argumentos dados en la línea de órdenes u mediante órdenes de configuración presentes en el archivo `~/.config/nano/nanorc`.

Se instala un archivo de configuración de muestra al instalar el programa, que se encuentra en `/etc/nanorc`. Para personalizar la configuración de nano, primero cree una copia local en `~/.config/nano/nanorc`:

```
$ cp /etc/nanorc ~/.config/nano/nanorc

```

Proceda a establecer el entorno de la consola de nano marcando y/o desmarcando órdenes en el archivo `~/.config/nano/nanorc`.

**Sugerencia:** [nanorc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nanorc.5) detalla el listado completo de las órdenes de configuración disponibles para nano.

**Nota:** los argumentos dados en la línea de órdenes anulan y tienen prioridad sobre las órdenes de configuración establecidas en `~/.config/nano/nanorc`

### Resaltado de sintaxis

Nano se entrega con reglas predefinidas de [resaltado de sintaxis](https://en.wikipedia.org/wiki/Syntax_highlighting "wikipedia:Syntax highlighting"), establecidas en `/usr/share/nano/*.nanorc`. Para activarlas, añada la siguiente línea a `~/.config/nano/nanorc` o a `/etc/nanorc`:

```
include "/usr/share/nano/*.nanorc"

```

Para mejorar el resaltado de la sintaxis que reemplacen y expandan los valores predeterminados, [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [nano-syntax-highlighting](https://www.archlinux.org/packages/?name=nano-syntax-highlighting) o [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/) y, además de la configuración anterior, añada también:

```
include "/usr/share/nano-syntax-highlighting/*.nanorc"

```

#### Forth

Consulte [https://paste.xinu.at/wc17YG/](https://paste.xinu.at/wc17YG/) para resaltar [Forth](https://en.wikipedia.org/wiki/Forth_(programming_language) "wikipedia:Forth (programming language)").

#### PKGBUILD

Guarde [https://paste.xinu.at/4ss/](https://paste.xinu.at/4ss/) (similar a [svntogit-server](https://projects.archlinux.org/svntogit/packages.git/tree)) en `/etc/nano/pkgbuild.nanorc` e inclúyalo:

```
include "/etc/nano/pkgbuild.nanorc"

```

**Sugerencia:** [nano-syntax-highlighting](https://www.archlinux.org/packages/?name=nano-syntax-highlighting) tiene una versión alternativa.

### Suspensión

A diferencia de la mayoría de los programas interactivos, la suspensión no está activada de manera predeterminada. Para cambiar esto, descomente la línea `set suspend` en `/etc/nanorc`. Esto le permitirá utilizar las teclas `Ctrl+z` para hacer que nano funcione en segundo plano.

### Ajuste de texto

*nano*, antes de la versión 4.0, a diferencia de muchos editores de texto, ajusta el texto. Para desactivar esto, ponga lo siguiente en `~/.config/nano/nanorc`

```
set nowrap

```

## Utilización

Los accesos directos se pueden ver desde el interior de *nano*. Consulte los archivos de ayuda de nano en línea con `Ctrl+g` una vez dentro de nano y el [Manual de órdenes de nano](https://www.nano-editor.org/dist/latest/nano.html) para obtener descripciones completas y asistencia adicional.

Vea también la [cheatsheet para nano](https://www.nano-editor.org/dist/latest/cheatsheet.html).

### Funciones especiales

Los atajos del teclado que representan las funciones comunmente utilizadas, se enumeran a lo largo de las dos líneas inferiores en la pantalla de nano.

Se pueden alternar mediante:

*   `Ctrl` para atajos basados ​​en `^`.
*   *`Meta`* (normalmente `Alt`) o `Esc` para atajos basados ​​en `M-`.

**Sugerencia:** [Feature Toggles](https://www.nano-editor.org/dist/latest/nano.html#Feature-Toggles) enumera los características globales para alternar funciones disponibles para nano.

## Consejos y trucos

### Reemplazar vi con nano

Para reemplazar vi con nano como editor de texto predeterminado para órdenes como [visudo](/index.php/Sudo#Using_visudo "Sudo"), ajuste las [variables de entorno](/index.php/Environment_variable#Defining_variables "Environment variable") `VISUAL` y `EDITOR`, por ejemplo:

```
export VISUAL=nano
export EDITOR=nano

```

## Solución de problemas

### Conflictos con combinaciones de teclas

Algunos gestores de ventanas tienen combinaciones de teclas que entran en conflicto con nano, por ejemplo `Alt+Intro`. Elimínelas o reasígnelas, por ejemplo, a `Super` (con [dconf](https://www.archlinux.org/packages/?name=dconf) para [mutter](https://www.archlinux.org/packages/?name=mutter), [muffin](https://www.archlinux.org/packages/?name=muffin) y [marco](https://www.archlinux.org/packages/?name=marco)) y reinicie el gestor de ventanas.

## Véase también

*   [nano (editor de texto)](https://en.wikipedia.org/wiki/Nano_(text_editor) — Entrada de Wikipedia.
*   [GNU nano Homepage](https://www.nano-editor.org/) — Sitio oficial.
*   [GNU nano Bugs](https://savannah.gnu.org/bugs/?group=nano) — Informe de errores.
*   [Improved Nano Syntax Highlighting Files](https://github.com/scopatz/nanorc).