**Estado de la traducción**
Este artículo es una traducción de [Readline](/index.php/Readline "Readline"), revisada por última vez el **2018-10-26**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Readline&diff=0&oldid=551245) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Readline](https://www.gnu.org/software/readline/) es una biblioteca del [Proyecto GNU](/index.php/GNU_Project_(Espa%C3%B1ol) "GNU Project (Español)"), utilizada por [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)") y otros programas con interfaz CLI para editar e interactuar con la línea de órdenes. Véase [readline(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/readline.3) para más información.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Modo de edición](#Modo_de_edición)
    *   [2.1 Indicador de modo en el prompt](#Indicador_de_modo_en_el_prompt)
    *   [2.2 Diferentes formas de cursor para cada modo](#Diferentes_formas_de_cursor_para_cada_modo)
*   [3 Movimiento rápido entre palabras](#Movimiento_rápido_entre_palabras)
*   [4 Historial](#Historial)
*   [5 Completado más rápido](#Completado_más_rápido)
*   [6 Colores en el completado](#Colores_en_el_completado)
*   [7 Macros](#Macros)
*   [8 Desactivando el control de eco](#Desactivando_el_control_de_eco)
*   [9 Véase también](#Véase_también)

## Instalación

Es probable que el paquete [readline](https://www.archlinux.org/packages/?name=readline) ya esté instalado como una dependencia de [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)").

## Modo de edición

De manera predeterminada, Readline utiliza los atajos de estilo Emacs para interactuar con la línea de órdenes. Sin embargo, la interfaz de edición de estilo [vi](/index.php/Vi_(Espa%C3%B1ol) "Vi (Español)") también están soportados añadiendo lo siguiente a `~/.inputrc`:

 `~/.inputrc`  ` set editing-mode vi` 

Alternativamente, para configurarlo solo para [Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)"), añada la siguiente línea a `~/.bashrc`:

 `~/.bashrc`  ` set -o vi` 

### Indicador de modo en el prompt

La edición de estilo vi tiene dos modos: comando e insertar. Puede visualizar cuál está activo actualmente añadiendo la siguiente opción:

 `~/.inputrc` 
```
set show-mode-in-prompt on

```

Esto imprimirá una cadena en su prompt (`(cmd)`/`(ins)` por defecto) que se puede personalizar con las variables `vi-ins-mode-string` y `vi-cmd-mode-string`.

### Diferentes formas de cursor para cada modo

Puede configurar una forma de cursor diferente para cada modo utilizando ["\1 .. \2" escapes](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html#index-vi_002dcmd_002dmode_002dstring):

 `~/.inputrc` 
```
set vi-ins-mode-string \1\e[6 q\2
set vi-cmd-mode-string \1\e[2 q\2

```

Esto establecerá un cursor en forma de bloque cuando esté en el modo de comando y un cursor de tubería cuando esté en el modo de inserción.

La consola virtual utiliza diferentes códigos de escape, por lo que antes debe verificar qué terminal se está utilizando:

 `~/.inputrc` 
```
$if term=linux
	set vi-ins-mode-string \1\e[?0c\2
	set vi-cmd-mode-string \1\e[?8c\2
$else
	set vi-ins-mode-string \1\e[6 q\2
	set vi-cmd-mode-string \1\e[2 q\2
$endif
```

Véase [Cursor software para VGA](https://www.kernel.org/doc/Documentation/admin-guide/vga-softcursor.rst) para mas detalles.

## Movimiento rápido entre palabras

[Xterm](/index.php/Xterm "Xterm") permite moverse entre palabras con `Control+Izquierda` y `Control+Derecha` [de forma predeterminada](http://stackoverflow.com/a/7783928). Para lograr este efecto con otros emuladores de terminal, encuentre los códigos de terminal correctos [[1]](http://wiki.bash-hackers.org/scripting/terminalcodes), y conéctelos a `backward-word` y `forward-word` en `~/.inputrc`.

Por ejemplo, para [urxvt](/index.php/Urxvt_(Espa%C3%B1ol) "Urxvt (Español)"):

 `~/.inputrc` 
```
"\e[1;5D": backward-word
"\e[1;5C": forward-word
```

## Historial

Por lo general, presionar la tecla de flecha hacia arriba hará que se muestre la última orden, independientemente de la orden que se haya escrito hasta el momento. Sin embargo, a los usuarios les puede resultar más práctico listar solo las órdenes anteriores ​​que coincidan con la entrada actual.

Por ejemplo, si el usuario ha escrito las siguientes órdenes:

*   `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`
*   `who`
*   `mount`
*   `man mount`

En esta situación, al escribir `ls` y presionar la tecla de flecha hacia arriba, la entrada actual se reemplazará con `man mount`, la última orden ejecutada. Si se ha habilitado la búsqueda de historial, solo se mostrarán las órdenes anteriores que comiencen con `ls` (la entrada actual), en este caso `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`.

Puede habilitar el modo de búsqueda de historial añadiendo las siguientes líneas a `/etc/inputrc` o `~/.inputrc`:

```
"\e[A": history-search-backward
"\e[B": history-search-forward

```

Si está utilizando el modo vi, puede añadir las siguientes líneas a `~/.inputrc` (de [esta publicación](https://bbs.archlinux.org/viewtopic.php?pid=428760#p428760)):

```
set editing-mode vi
$if mode=vi
set keymap vi-command
# these are for vi-command mode
"\e[A": history-search-backward
"\e[B": history-search-forward
j: history-search-forward
k: history-search-backward
set keymap vi-insert
# these are for vi-insert mode
"\e[A": history-search-backward
"\e[B": history-search-forward
$endif

```

Si eligió añadir estas líneas a `~/.inputrc`, se recomienda que también añada la siguiente línea al principio de este archivo para evitar cosas extrañas como [esta](https://bbs.archlinux.org/viewtopic.php?id=112537):

```
$include /etc/inputrc

```

Alternativamente, se puede utilizar el historial de búsqueda inversa (búsqueda incremental) presionando `Control+R`, que no busca en base a la entrada anterior, sino que salta hacia atrás en el búfer del historial a medida que se escriben las órdenes en la búsqueda de términos. Al presionar nuevamente `Control+R` durante este modo, se mostrará la línea anterior en el búfer que coincide con el término de búsqueda actual, mientras que al presionar `Control+G` (abortar) se cancelará la búsqueda y se restaurará la línea de entrada actual. Entonces, para buscar en todos las órdenes `mount` anteriores, presione `Control+R`, escriba 'mount' y siga presionando `Control+R` hasta que se encuentre la línea deseada.

El equivalente directo de este modo se denomina historial de búsqueda avanzada y está vinculado a `Control+S` de forma predeterminada. Tenga en cuenta que la mayoría de los terminales anulan `Control+S` para suspender la ejecución hasta que se presione `Control+Q`. (A esto se le llama control de flujo XON/XOFF). Para activar el historial de búsqueda avanzada, deshabilite el control de flujo de esta forma:

```
$ stty -ixon

```

o utilice una tecla diferente en `inputrc`. Por ejemplo, para utilizar `Alt+S` que no está enlazado por defecto:

```
"\es": forward-search-history

```

## Completado más rápido

Al realizar el completado mediante tabulador, una sola pulsación intenta completar parcialmente la palabra actual. Si no son posibles los completados parciales, una doble pulsación muestra todas los completados posibles.

La doble pulsación de tabulador se puede cambiar a una sola pulsación con la configuración siguiente:

 `~/.inputrc` 
```
set show-all-if-unmodified on

```

O puede configurarlo de modo que una sola pulsación de tabulador realice ambos pasos: que complete parcialmente la palabra *y* que muestre todas los completados posibles si aún es ambigua:

 `~/.inputrc` 
```
set show-all-if-ambiguous on

```

## Colores en el completado

Puede habilitar el coloreado del completado de los nombres de archivo con la opción `colored-stats`. También puede colorear el prefijo idéntico de las listas de completado con `colored-completed-prefix`. Por ejemplo:

 `~/.inputrc` 
```
# Archivos de color por tipos
set colored-stats On
# Añadir un carácter para indicar el tipo
set visible-stats On
# Marcar directorios enlazados
set mark-symlinked-directories On
# Colorea el prefijo común
set colored-completion-prefix On
# Colorea el prefijo común en completado por menú
set menu-complete-display-prefix On

```

## Macros

Readline también admite teclas enlazadas para macros de teclado. Para un ejemplo simple, ejecute esta orden en Bash:

```
bind '"\ew": "\C-e # macro"'

```

o añada la parte entre comillas simples a inputrc:

```
"\ew": "\C-e # macro"

```

Ahora escriba una línea y presione `Alt+W`. Readline actuará como si se hubiera presionado `Control+E` (final de línea), añadido con ' `# macro`'.

Utilice cualquiera de las combinaciones de teclas existentes dentro de una macro de readline, lo que puede ser bastante útil para automatizar los términos de uso frecuente. Por ejemplo, este hace que `Control+Alt+L` añada "| less" a la línea y la ejecute (`Control+M` es equivalente a `Intro`):

```
"\e\C-l": "\C-e | less\C-m"

```

El siguiente prefija la línea con 'yes |' al presionar `Control+Alt+Y`, confirmando cualquier pregunta de sí/no que la orden pudiera preguntar:

```
"\e\C-y": "\C-ayes | \C-m"

```

Este ejemplo ajusta la línea en `su -c ''`, si se presiona `Alt+S`:

```
"\es": "\C-a su -c '\C-e'\C-m"

```

Este ejemplo prefija la línea con `sudo` , si se presiona `Alt+S`. Es más seguro porque no introduce la tecla `Intro`.

```
"\es": "\C-asudo \C-e"

```

Como último ejemplo, envíe rápidamente una orden en segundo plano con `Control+Alt+B`, descartando toda su salida:

```
"\e\C-b": "\C-e > /dev/null 2>&1 &\C-m"

```

## Desactivando el control de eco

Readline hace que el terminal se haga eco de `^C` después de presionar `Control+C`. Para los usuarios que deseen deshabilitar esto, simplemente añada lo siguiente a `~/.inputrc`:

```
set echo-control-characters off

```

## Véase también

*   [vi readline editing cheat sheat](http://www.catonmat.net/download/bash-vi-editing-mode-cheat-sheet.pdf)
*   [emacs readline editing cheat sheet](http://www.catonmat.net/download/readline-emacs-editing-mode-cheat-sheet.pdf)