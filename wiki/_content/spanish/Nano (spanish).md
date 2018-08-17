[GNU nano](http://www.nano-editor.org/) (o nano) es un editor de texto cuya finalidad es presentar una interface simple y opciones de comandos intuitivos de editores de textos basados en consola. *nano* incorpora características incluyendo resaltado colorida de sintaxis, conversión de tipos de archivos DOS/Mac, revisor de ortografía y codificación [UTF-8](https://en.wikipedia.org/wiki/UTF-8 "wikipedia:UTF-8"). *nano* inicia con un buffer vacío, normalmente ocupa menos de 1.5 MB de memoria.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Crear ~/.nanorc](#Crear_.7E.2F.nanorc)
    *   [2.2 Resaltado de sintaxis](#Resaltado_de_sintaxis)
        *   [2.2.1 PKGBUILD](#PKGBUILD)
        *   [2.2.2 Forth](#Forth)
        *   [2.2.3 Otras definiciones](#Otras_definiciones)
    *   [2.3 Configuraciones sugeridas](#Configuraciones_sugeridas)
        *   [2.3.1 Suspensión](#Suspensi.C3.B3n)
        *   [2.3.2 Ajuste de texto](#Ajuste_de_texto)
*   [3 Uso](#Uso)
    *   [3.1 Funciones especiales](#Funciones_especiales)
        *   [3.1.1 Vista general de la lista de atajos](#Vista_general_de_la_lista_de_atajos)
        *   [3.1.2 Selecciona las funciones secundarias](#Selecciona_las_funciones_secundarias)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Reemplazar vi con nano](#Reemplazar_vi_con_nano)
*   [5 Solución De Problemas](#Soluci.C3.B3n_De_Problemas)
    *   [5.1 Conflictos combinaciones de teclas](#Conflictos_combinaciones_de_teclas)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Puedes [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [nano](https://www.archlinux.org/packages/?name=nano) desde los [repositorios oficiales](/index.php/Official_repositories "Official repositories"). Es probable que ya esté en tu sistema, está incluido en el grupo [base](https://www.archlinux.org/groups/x86_64/base/)

## Configuración

### Crear ~/.nanorc

La apariencia, sensación, y funcionamiento de nano esta normalmente controlado ya sea por argumentos de lineas de comando, o comandos de configuración dentro el archivo `~/.nanorc`.

Un simple archivo de configuración durante la instalación del programa y se localiza en `/etc/nanorc`. Para personalizar la configuración de nano, primero se debe crear una copia local en `~/.nanorc`:

```
$ cp /etc/nanorc ~/.nanorc

```

Procede a establecer el entono en consola ajustando y/o comentando los comandos dentro del archivo `~/.nanorc`

**Sugerencia:** [NANORC](http://www.nano-editor.org/dist/v2.2/nanorc.5.html) detalla la lista completa de comandos de configuración disponibles para nano.

**Note:** La linea de comandos ignoras la configuración por defecto y da prioridad a los comandos de configuración establecidos en `~/.nanorc`

### Resaltado de sintaxis

#### PKGBUILD

Esta nueva versión de remarcado como la de Arch Linux ["svntogit-server"](https://projects.archlinux.org/svntogit/packages.git/tree).

```
# Arch PKGBUILD files
#
syntax "pkgbuild" "^.*PKGBUILD*"
# commands
color red "\<(cd|echo|enable|exec|export|kill|popd|pushd|read|source|touch|type)\>"
color brightblack "\<(case|cat|chmod|chown|cp|diff|do|done|elif|else|esac|exit|fi|find|for|ftp|function|grep|gzip|if|in)\>"
color brightblack "\<(install|ln|local|make|mv|patch|return|rm|sed|select|shift|sleep|tar|then|time|until|while|yes)\>"
# ${*}
icolor blue "\$\{?[0-9A-Z_!@#$*?-]+\}?"
# numerics
color blue "\ [0-9]*"
color blue "\.[0-9]*"
color blue "\-[0-9]*"
color blue "=[0-9]"
# spaces
color ,green "[[:space:]]+$"
# strings; multilines are not supported
color brightred ""(\\.|[^"])*"" "'(\\.|[^'])*'"
# comments
color brightblack "#.*$"

```

Esta es otra versión de este [foro](https://bbs.archlinux.org/viewtopic.php?pid=565476).

```
## Arch PKGBUILD files
##
syntax "pkgbuild" "^.*PKGBUILD$"
color green start="^." end="$"
color cyan "^.*(pkgbase|pkgname|pkgver|pkgrel|pkgdesc|arch|url|license).*=.*$"
color brightcyan "\<(pkgbase|pkgname|pkgver|pkgrel|pkgdesc|arch|url|license)\>"
color brightcyan "(\$|\$\{|\$\()(pkgbase|pkgname|pkgver|pkgrel|pkgdesc|arch|url|license)(|\}|\))"
color cyan "^.*(depends|makedepends|optdepends|conflicts|provides|replaces).*=.*$"
color brightcyan "\<(depends|makedepends|optdepends|conflicts|provides|replaces)\>"
color brightcyan "(\$|\$\{|\$\()(depends|makedepends|optdepends|conflicts|provides|replaces)(|\}|\))"
color cyan "^.*(groups|backup|noextract|options).*=.*$"
color brightcyan "\<(groups|backup|noextract|options)\>"
color brightcyan "(\$|\$\{|\$\()(groups|backup|noextract|options)(|\}|\))"
color cyan "^.*(install|source|md5sums|sha1sums|sha256sums|sha384sums|sha512sums).*=.*$"
color brightcyan "\<(install|source|md5sums|sha1sums|sha256sums|sha384sums|sha512sums)\>"
color brightcyan "(\$|\$\{|\$\()(install|source|md5sums|sha1sums|sha256sums|sha384sums|sha512sums)(|\}|\))"
color brightcyan "\<(startdir|srcdir|pkgdir)\>"
color cyan "\.install"
color brightwhite "=" "'" "\(" "\)" "\"" "#.*$" "\," "\{" "\}"
color brightred "build\(\)"
color brightred "package_.*.*$"
color brightred "\<(configure|make|cmake|scons)\>"
color red "\<(DESTDIR|PREFIX|prefix|sysconfdir|datadir|libdir|includedir|mandir|infodir)\>"

```

Guarde este archivo como (por ejemplo) `/etc/nano/pkgbuild.nanorc`.

Después importa el archivo a `~/.nanorc` o a `/etc/nanorc` editando la siguiente linea:

```
include "/etc/nano/pkgbuild.nanorc"

```

#### Forth

```
 ## Un ejemplo de Forth.
 ##
 syntax "forth" "\.(fs|4th|4mu)$" 

 ## Declaraciones de proceso
 color brightred "\[.+\]"

 ## Números
 color magenta "-?[0-9]+"

 ## Decimales
 color cyan "-?[0-9\.]+e[0-9]+"

 ## Otras palabras

 color green "\<(2constant|2drop|2dup|2literal|2nip|2over|2rdrop|2rot|2swap|2tuck|2variable|abort|abs|accept|again|ahead|alias|align|aligned|allocate|allot|also|and|arg|argc|argv|asptr|asptr|assembler|base|begin|bin|bind|bind|bl|blank|blk|block|bootmessage|bound|bounds|buffer|bye|case|catch|cell|cells|cfalign|cfaligned|char|chars|class|class|class|clearstack|clearstacks|cmove|code|compare|constant|construct|context|convert|count|cputime|cr|create|current|dabs|dbg|decimal|defer|defer|defers|defines|definitions|definitions|depth|dfalign|dfaligned|dfloats|discode|dispose|dmax|dmin|dnegate|do|done|dpl|drop|dump|dup|early|ekey|else|emit|endcase|endif|endof|endscope|endtry|endwith|erase|evaluate|exception|execute|exit|exitm|expect|fabs|facos|facosh|falign|faligned|falog|false|fasin|fasinh|fatan|fatan2|fatanh|fconstant|fcos|fcosh|fdepth|fdrop|fdup|fexp|fexpm1|field|fill|find|fliteral|fln|flnp1|float|floats|flog|floor|floored|flush|fmax|fmin|fnegate|fnip|for|form|forth|fover|fp0|fpath|fpick|free|frot|fround|fsin|fsincos|fsinh|fsqrt|fswap|ftan|ftanh|ftuck|fvariable|getenv|gforth|here|hex|hold|i|if|iferror|immediate|implementation|include|included|init|interface|invert|is|is|j|k|key|latest|latestxt|leave|link|list|literal|load|loop|lp0|lshift|marker|max|maxalign|maxaligned|method|method|method|methods|min|mod|move|ms|naligned|name|needs|negate|new|new|next|nextname|nip|noname|nothrow|object|object|of|off|on|only|or|order|over|overrides|pad|page|parse|perform|pi|pick|postpone|postpone|precision|previous|print|printdebugdata|protected|ptr|ptr|public|query|quit|rdrop|recurse|recursive|refill|repeat|represent|require|required|resize|restore|restrict|roll|root|rot|rp0|rshift|savesystem|scope|scr|seal|search|see|selector|self|sfalign|sfaligned|sfloats|sh|sign|sliteral|source|sourcefilename|sp0|space|spaces|span|static|stderr|stdin|stdout|struct|super|swap|system|table|then|this|throw|thru|tib|to|toupper|true|try|tuck|type|typewhite|unloop|unreachable|until|unused|update|use|user|utime|value|var|var|variable|vlist|vocabulary|vocs|while|with|within|word|wordlist|words|xemit|xkey|xor)\>"

 ## No se puede con palabras con simbolos en sus nombres :/
 #color brightgreen "(\<!\|\#\|\#\!\|\#\>\|\#\>\>\|\#s\|\#tib\|\$\?\|%align\|\%alignment\|\%alloc\|\%allocate\|\%allot\|\%size\|\'\|\'\|\'cold\|\(\|\(local\)\|\)\|\*\|\*\/\|\*\/mod\|\+\|\+\!\|\+DO\|\+field\|\+load\|\+LOOP\|\+thru\|\+x\/string\|\,\|\-\|\-\-\>\|\-DO\|\-LOOP\|\-rot\|\-trailing\|\-trailing\-garbage\|\.\|\.\"\|\.\(\|\.\\\"\|\.debugline\|\.id\|\.name\|\.path\|\.r\|\.s\|\/\|\/does\-handler\|\/l\|\/mod\|\/string\|\/w\|0\<\|0\<\=\|0\<\>\|0\=\|0\>\|0\>\=\|1\+\|1\-\|1\/f\|2\!\|2\*\|2\,\|2\/\|2\>r\|2\@\|2field\:\|2r\>\|2r\@\|\:\|\:\|\:\:\|\:\:\|\:m\|\:noname\|\;\|\;code\|\;m\|\;s\|\<\|\<\#\|\<\<\#\|\<\=\|\<\>\|\<bind\>\|\<compilation\|\<interpretation\|\<to\-inst\>\|\=\|\>\|\>\=\|\>body\|\>code\-address\|\>definer\|\>does\-code\|\>float\|\>in\|\>l\|\>name\|\>number\|\>order\|\>r\|\?\|\?DO\|\?dup\|\?DUP\-0\=\-IF\|\?DUP\-IF\|\?LEAVE\|\@\|\@local\#\|\[\|\[\'\]\|\[\+LOOP\]\|\[\?DO\]\|\[\]\|\[AGAIN\]\|\[BEGIN\]\|\[bind\]\|\[Char\]\|\[COMP\'\]\|\[compile\]\|\[current\]\|\[DO\]\|\[ELSE\]\|\[ENDIF\]\|\[FOR\]\|\[IF\]\|\[IFDEF\]\|\[IFUNDEF\]\|\[LOOP\]\|\[NEXT\]\|\[parent\]\|\[REPEAT\]\|\[THEN\]\|\[to\-inst\]\|\[UNTIL\]\|\[WHILE\]\|\\\|\\c\|\\G\|\]\|\]L\|ABORT\"\|action\-of\|add\-lib\|ADDRESS\-UNIT\-BITS\|also\-path\|assert\(\|assert\-level\|assert0\(\|assert1\(\|assert2\(\|assert3\(\|ASSUME\-LIVE\|at\-xy\|base\-execute\|begin\-structure\|bind\'\|block\-included\|block\-offset\|block\-position\|break\"\|break\:\|broken\-pipe\-error\|c\!\|C\"\|c\,\|c\-function\|c\-library\|c\-library\-name\|c\@\|call\-c\|cell\%\|cell\+\|cfield\:\|char\%\|char\+\|class\-\>map\|class\-inst\-size\|class\-override\!\|class\-previous\|class\;\|class\>order\|class\?\|clear\-libs\|clear\-path\|close\-file\|close\-pipe\|cmove\>\|code\-address\!\|common\-list\|COMP\'\|compilation\>\|compile\,\|compile\-lp\+\!\|compile\-only\|const\-does\>\|create\-file\|create\-interpret\/compile\|CS\-PICK\|CS\-ROLL\|current\'\|current\-interface\|d\+\|d\-\|d\.\|d\.r\|d0\<\|d0\<\=\|d0\<\>\|d0\=\|d0\>\|d0\>\=\|d2\*\|d2\/\|d\<\|d\<\=\|d\<\>\|d\=\|d\>\|d\>\=\|d\>f\|d\>s\|dec\.\|defer\!\|defer\@\|definer\!\|delete\-file\|df\!\|df\@\|dffield\:\|dfloat\%\|dfloat\+\|dict\-new\|docol\:\|docon\:\|dodefer\:\|does\-code\!\|does\-handler\!\|DOES\>\|dofield\:\|double\%\|douser\:\|dovar\:\|du\<\|du\<\=\|du\>\|du\>\=\|edit\-line\|ekey\>char\|ekey\>fkey\|ekey\?\|emit\-file\|empty\-buffer\|empty\-buffers\|end\-c\-library\|end\-class\|end\-class\|end\-class\-noname\|end\-code\|end\-interface\|end\-interface\-noname\|end\-methods\|end\-struct\|end\-structure\|endtry\-iferror\|environment\-wordlist\|environment\?\|execute\-parsing\|execute\-parsing\-file\|f\!\|f\*\|f\*\*\|f\+\|f\,\|f\-\|f\.\|f\.rdp\|f\.s\|f\/\|f0\<\|f0\<\=\|f0\<\>\|f0\=\|f0\>\|f0\>\=\|f2\*\|f2\/\|f\<\|f\<\=\|f\<\>\|f\=\|f\>\|f\>\=\|f\>buf\-rdp\|f\>d\|f\>l\|f\>str\-rdp\|f\@\|f\@local\#\|fe\.\|ffield\:\|field\:\|file\-position\|file\-size\|file\-status\|find\-name\|float\%\|float\+\|floating\-stack\|flush\-file\|flush\-icache\|fm\/mod\|forth\-wordlist\|fp\!\|fp\@\|fs\.\|f\~\|f\~abs\|f\~rel\|get\-block\-fid\|get\-current\|get\-order\|heap\-new\|hex\.\|how\:\|id\.\|include\-file\|included\?\|infile\-execute\|init\-asm\|init\-object\|inst\-value\|inst\-var\|interpret\/compile\:\|interpretation\>\|k\-alt\-mask\|k\-ctrl\-mask\|k\-delete\|k\-down\|k\-end\|k\-f1\|k\-f10\|k\-f11\|k\-f12\|k\-f2\|k\-f3\|k\-f4\|k\-f5\|k\-f6\|k\-f7\|k\-f8\|k\-f9\|k\-home\|k\-insert\|k\-left\|k\-next\|k\-prior\|k\-right\|k\-shift\-mask\|k\-up\|key\-file\|key\?\|key\?\-file\|l\!\|laddr\#\|lib\-error\|lib\-sym\|list\-size\|lp\!\|lp\!\|lp\+\!\#\|lp\@\|m\*\|m\*\/\|m\+\|m\:\|maxdepth\-\.s\|name\>comp\|name\>int\|name\>string\|name\?int\|new\[\]\|next\-arg\|open\-blocks\|open\-file\|open\-lib\|open\-path\-file\|open\-pipe\|os\-class\|outfile\-execute\|parse\-name\|parse\-word\|path\+\|path\-allot\|path\=\|postpone\,\|r\/o\|r\/w\|r\>\|r\@\|read\-file\|read\-line\|rename\-file\|reposition\-file\|resize\-file\|restore\-input\|rp\!\|rp\@\|S\"\|s\>d\|s\>number\?\|s\>unumber\?\|s\\\"\|save\-buffer\|save\-buffers\|save\-input\|search\-wordlist\|see\-code\|see\-code\-range\|set\-current\|set\-order\|set\-precision\|sf\!\|sf\@\|sffield\:\|sfloat\%\|sfloat\+\|shift\-args\|simple\-see\|simple\-see\-range\|sl\@\|slurp\-fid\|slurp\-file\|sm\/rem\|source\-id\|sourceline\#\|sp\!\|sp\@\|str\<\|str\=\|string\-prefix\?\|sub\-list\?\|sw\@\|threading\-method\|time\&date\|to\-this\|U\+DO\|U\-DO\|u\.\|u\.r\|u\<\|u\<\=\|u\>\|u\>\=\|ud\.\|ud\.r\|ul\@\|um\*\|um\/mod\|under\+\|updated\?\|uw\@\|w\!\|w\/o\|write\-file\|write\-line\|x\-size\|x\-width\|x\\string\-\|xc\!\+\?\|xc\-size\|xc\@\+\|xchar\+\|xchar\-\|xchar\-encoding\|xt\-new\|xt\-see\|\~\~)\>"

 ## Marcar comentarios
 color brightblue start="(^| )\( " end="\)"
 color brightblue "\\ .*$"

```

#### Otras definiciones

Las mejoras del resaltado de sintaxis que sustituyen y amplían los valores predeterminados se pueden encontrar en la AUR. [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/).

### Configuraciones sugeridas

#### Suspensión

A diferencia de muchos programas interactivos, la suspensión no esta disponible por defecto. Para cambiarlo, descomenta la linea 'set suspenden' en `/etc/nanorc`. Esto permitirá que sus las teclas `Ctrl+z` para mandar a nano a segundo plano.

#### Ajuste de texto

Diferente a muchos editores de texto, *nano* ajusta el texto. Para desactivar esto, añade esto a `~/.nanorc`

```
set nowrap

```

## Uso

### Funciones especiales

*   La tecla`Ctrl` modifica atajos (`^`) comunmente representado usado para las funciones listadas en dos lineas en la parte inferior

de la pantalla de nano

*   Funciones adicionales pueden ser interactivamente cambiados usando `Meta` (normalmente con la secuencia de teclas`Alt`) y/o `Esc`.

#### Vista general de la lista de atajos

| Tecla 1 | Tecla 2 | Commando | Descripción |
| ^G | F1 | Ver Ayuda | Muestra los archivops de ayuda en linea desntro de las ventana de sesión. Una lectura recomendada para los usuarios de nano de cualquier nivel |
| ^X | F2 | Salir | Cerrar y salir de nano. |
| ^O | F3 | Guardar | Guarda el contenido del archivo actual a un archivo en el disco. |
| ^J | F4 | Justificado | Alinea el texto acorde de la geometria de la ventana de consola. |
| ^R | F5 | Leer Fichero | Inserta otro archivo dentro de la localización actual del cursor. |
| ^W | F6 | Buscar | Busca una frase (reconoce mayusculas) o expresión |
| ^Y | F7 | Página Anterior | Muestra la pantalla anterior. |
| ^V | F8 | Página Siguiente | Muestra la siguiente pantalla. |
| ^K | F9 | Cortar Texto | Corta y almacena toda la linea actual desde el inicio hasta el final. |
| ^U | F10 | Pegar Texto | Pega el contenido cortado a la posición actual del cursor. |
| ^C | F11 | Posición del cursor | Muestra la informacion de linea, columna y caracter de la posisión actual de cursor. |
| ^T | F12 | Ortografía | Revisa la ortografía del contenido con el complemento `spell`, si está disponible. |

**Sugerencia:** Consulte los archivos de ayuda en linea mediante `Ctrl+G` dentro de nano y el [Manual de comandos de nano](http://www.nano-editor.org/dist/v2.1/nano.html) para una descripción completa y soporte adicional.

#### Selecciona las funciones secundarias

| Tecla 1 | Tecla 2 | Descripción |
| Meta+c | Esc+c | Cambia de soporte a la información de linea, columna y posición del caracter. |
| Meta+i | Esc+i | Cabia de soporte para la auto sangría de las lineas. |
| Meta+k | Esc+k | Cambia de soporte para el cortado de la linea completa en la posición actual del cursor. |
| Meta+m | Esc+m | Cambia de soporte de mouse para posicionar el cursor, marcación y atajo. |
| Meta+x | Esc+x | Muestra u oculta la lista de atajos de la parte superior de la pantalla, añadiendo más espacio de pantalla. |

**Sugerencia:** [Caracteristicas Secundarias](http://www.nano-editor.org/dist/v2.1/nano.html#Feature-Toggles) enlista las funciones secundarias globales disponibles para nano.

## Consejos y trucos

### Reemplazar vi con nano

Aveces los usuarios prefieren usar `nano` que `vi` por su simplicidad y uso fácil, y pueden optar por reemplazar a vi por nano como editor de texto por comandos como [visudo](/index.php/Sudo_(Espa%C3%B1ol)#Utilizando_visudo "Sudo (Español)").

Ajustando la [Variable de entorno](/index.php/Environment_variable#Defining_variables "Environment variable") `EDITOR` funcionará para muchas aplicaciones, por ejemplo:

```
export EDITOR=nano

```

## Solución De Problemas

### Conflictos combinaciones de teclas

Algunos administradores de ventanas tienen algunas combinaciones de teclas que coinciden con nano, por ejemplo `Alt+Enter`. Borrarlas o reasignelas por ejemplo `Super` (con [dconf](https://www.archlinux.org/packages/?name=dconf) por [mutter](https://www.archlinux.org/packages/?name=mutter), [muffin](https://www.archlinux.org/packages/?name=muffin) y [marco](https://www.archlinux.org/packages/?name=marco)) y reinicie el administrador de ventanas.

## Véase también

*   [nano (text editor)](https://en.wikipedia.org/wiki/Nano_(text_editor) - Wikipedia
*   [GNU nano Homepage](http://www.nano-editor.org/) - Sitio Oficial (en Inglés)
*   [GNU nano Bugs](https://savannah.gnu.org/bugs/?group=nano) Reportar fallos
*   [Mejor remarcado de sintaxis](https://github.com/craigbarnes/nanorc)