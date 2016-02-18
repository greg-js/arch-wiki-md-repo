[GNU nano](http://www.nano-editor.org/) (или просто nano) это текстовый редактор, с простым и интуитивно понятным интерфейсом, включающим в себя основные команды по редактированию текста. *Nano* поддерживает раскраску синтаксиса, конвертацию файлов DOS/Mac, проверку орфографии и кодировку [UTF-8](https://en.wikipedia.org/wiki/ru:UTF-8 "wikipedia:ru:UTF-8"). Программа *Nano* (с пустым буфером) занимает в оперативной памяти всего 1.5 Мб.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Насторйка](#.D0.9D.D0.B0.D1.81.D1.82.D0.BE.D1.80.D0.B9.D0.BA.D0.B0)
    *   [2.1 Создание ~/.nanorc](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.7E.2F.nanorc)
    *   [2.2 Подсветка синтаксиса](#.D0.9F.D0.BE.D0.B4.D1.81.D0.B2.D0.B5.D1.82.D0.BA.D0.B0_.D1.81.D0.B8.D0.BD.D1.82.D0.B0.D0.BA.D1.81.D0.B8.D1.81.D0.B0)
        *   [2.2.1 Включение подсветки](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D1.81.D0.B2.D0.B5.D1.82.D0.BA.D0.B8)
        *   [2.2.2 PKGBUILD](#PKGBUILD)
        *   [2.2.3 Forth](#Forth)
        *   [2.2.4 Другие определения](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.3 Другие настройки](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
        *   [2.3.1 Фоновый режим](#.D0.A4.D0.BE.D0.BD.D0.BE.D0.B2.D1.8B.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC)
        *   [2.3.2 Перенос текста](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BD.D0.BE.D1.81_.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.B0)
*   [3 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [3.1 Специальные функции](#.D0.A1.D0.BF.D0.B5.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.84.D1.83.D0.BD.D0.BA.D1.86.D0.B8.D0.B8)
        *   [3.1.1 Горячие клавиши](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
        *   [3.1.2 Selected toggle functions](#Selected_toggle_functions)
*   [4 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [4.1 Замена vi на nano](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_vi_.D0.BD.D0.B0_nano)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Оконный менеджер перехватывает горячие клавиши](#.D0.9E.D0.BA.D0.BE.D0.BD.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80_.D0.BF.D0.B5.D1.80.D0.B5.D1.85.D0.B2.D0.B0.D1.82.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D0.B3.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Вы можете установить пакет [nano](https://www.archlinux.org/packages/?name=nano) из [Официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Скорее всего он уже установлен на вашей системе, т.к. входит в группу [base](https://www.archlinux.org/groups/x86_64/base/).

## Насторйка

### Создание ~/.nanorc

Вид, поведение и функции nano управляются посредством аргументов командной строки или настроек в файле `~/.nanorc`.

После установки программы, пример файла настроек находится в `/etc/nanorc`. Чтобы настроить nano, сначала сделайте копию `~/.nanorc` в домашнюю папку:

```
$ cp /etc/nanorc ~/.nanorc

```

Продолжите настройку nano путём установки и/или отключения команд в файле `~/.nanorc`.

**Совет:** [NANORC](http://www.nano-editor.org/dist/v2.2/nanorc.5.html) Список полных и подробных команд настроек для nano.

**Обратите внимание:** Аргументы командной строки переопределяют и имеют приоритет над командами настроек, установленных в `~/.nanorc`

### Подсветка синтаксиса

#### Включение подсветки

Установите пакет [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/) и выполните:

```
cat /usr/share/nano-syntax-highlighting/nanorc.sample | xargs -0 echo >> ~/.nanorc

```

#### PKGBUILD

Arch Linux понравится эта новая версия из ["svntogit-server"](https://projects.archlinux.org/svntogit/packages.git/tree).

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

Еще один вариант из [темы форума](https://bbs.archlinux.org/viewtopic.php?pid=565476).

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

Сохраните этот файл как (например) `/etc/nano/pkgbuild.nanorc`.

Затем "включите" файл в `~/.nanorc` или в `/etc/nanorc` добавив следующую строку:

```
include "/etc/nano/pkgbuild.nanorc"

```

#### Forth

```
 ## Here is an example for Forth.
 ##
 syntax "forth" "\.(fs|4th|4mu)$" 

 ## Preprocessor statements
 color brightred "\[.+\]"

 ## Numbers
 color magenta "-?[0-9]+"

 ## Floats
 color cyan "-?[0-9\.]+e[0-9]+"

 ## Other Words

 color green "\<(2constant|2drop|2dup|2literal|2nip|2over|2rdrop|2rot|2swap|2tuck|2variable|abort|abs|accept|again|ahead|alias|align|aligned|allocate|allot|also|and|arg|argc|argv|asptr|asptr|assembler|base|begin|bin|bind|bind|bl|blank|blk|block|bootmessage|bound|bounds|buffer|bye|case|catch|cell|cells|cfalign|cfaligned|char|chars|class|class|class|clearstack|clearstacks|cmove|code|compare|constant|construct|context|convert|count|cputime|cr|create|current|dabs|dbg|decimal|defer|defer|defers|defines|definitions|definitions|depth|dfalign|dfaligned|dfloats|discode|dispose|dmax|dmin|dnegate|do|done|dpl|drop|dump|dup|early|ekey|else|emit|endcase|endif|endof|endscope|endtry|endwith|erase|evaluate|exception|execute|exit|exitm|expect|fabs|facos|facosh|falign|faligned|falog|false|fasin|fasinh|fatan|fatan2|fatanh|fconstant|fcos|fcosh|fdepth|fdrop|fdup|fexp|fexpm1|field|fill|find|fliteral|fln|flnp1|float|floats|flog|floor|floored|flush|fmax|fmin|fnegate|fnip|for|form|forth|fover|fp0|fpath|fpick|free|frot|fround|fsin|fsincos|fsinh|fsqrt|fswap|ftan|ftanh|ftuck|fvariable|getenv|gforth|here|hex|hold|i|if|iferror|immediate|implementation|include|included|init|interface|invert|is|is|j|k|key|latest|latestxt|leave|link|list|literal|load|loop|lp0|lshift|marker|max|maxalign|maxaligned|method|method|method|methods|min|mod|move|ms|naligned|name|needs|negate|new|new|next|nextname|nip|noname|nothrow|object|object|of|off|on|only|or|order|over|overrides|pad|page|parse|perform|pi|pick|postpone|postpone|precision|previous|print|printdebugdata|protected|ptr|ptr|public|query|quit|rdrop|recurse|recursive|refill|repeat|represent|require|required|resize|restore|restrict|roll|root|rot|rp0|rshift|savesystem|scope|scr|seal|search|see|selector|self|sfalign|sfaligned|sfloats|sh|sign|sliteral|source|sourcefilename|sp0|space|spaces|span|static|stderr|stdin|stdout|struct|super|swap|system|table|then|this|throw|thru|tib|to|toupper|true|try|tuck|type|typewhite|unloop|unreachable|until|unused|update|use|user|utime|value|var|var|variable|vlist|vocabulary|vocs|while|with|within|word|wordlist|words|xemit|xkey|xor)\>"

 ## I can't get words with symbols in their names to work :/
 #color brightgreen "(\<!\|\#\|\#\!\|\#\>\|\#\>\>\|\#s\|\#tib\|\$\?\|%align\|\%alignment\|\%alloc\|\%allocate\|\%allot\|\%size\|\'\|\'\|\'cold\|\(\|\(local\)\|\)\|\*\|\*\/\|\*\/mod\|\+\|\+\!\|\+DO\|\+field\|\+load\|\+LOOP\|\+thru\|\+x\/string\|\,\|\-\|\-\-\>\|\-DO\|\-LOOP\|\-rot\|\-trailing\|\-trailing\-garbage\|\.\|\.\"\|\.\(\|\.\\\"\|\.debugline\|\.id\|\.name\|\.path\|\.r\|\.s\|\/\|\/does\-handler\|\/l\|\/mod\|\/string\|\/w\|0\<\|0\<\=\|0\<\>\|0\=\|0\>\|0\>\=\|1\+\|1\-\|1\/f\|2\!\|2\*\|2\,\|2\/\|2\>r\|2\@\|2field\:\|2r\>\|2r\@\|\:\|\:\|\:\:\|\:\:\|\:m\|\:noname\|\;\|\;code\|\;m\|\;s\|\<\|\<\#\|\<\<\#\|\<\=\|\<\>\|\<bind\>\|\<compilation\|\<interpretation\|\<to\-inst\>\|\=\|\>\|\>\=\|\>body\|\>code\-address\|\>definer\|\>does\-code\|\>float\|\>in\|\>l\|\>name\|\>number\|\>order\|\>r\|\?\|\?DO\|\?dup\|\?DUP\-0\=\-IF\|\?DUP\-IF\|\?LEAVE\|\@\|\@local\#\|\[\|\[\'\]\|\[\+LOOP\]\|\[\?DO\]\|\[\]\|\[AGAIN\]\|\[BEGIN\]\|\[bind\]\|\[Char\]\|\[COMP\'\]\|\[compile\]\|\[current\]\|\[DO\]\|\[ELSE\]\|\[ENDIF\]\|\[FOR\]\|\[IF\]\|\[IFDEF\]\|\[IFUNDEF\]\|\[LOOP\]\|\[NEXT\]\|\[parent\]\|\[REPEAT\]\|\[THEN\]\|\[to\-inst\]\|\[UNTIL\]\|\[WHILE\]\|\\\|\\c\|\\G\|\]\|\]L\|ABORT\"\|action\-of\|add\-lib\|ADDRESS\-UNIT\-BITS\|also\-path\|assert\(\|assert\-level\|assert0\(\|assert1\(\|assert2\(\|assert3\(\|ASSUME\-LIVE\|at\-xy\|base\-execute\|begin\-structure\|bind\'\|block\-included\|block\-offset\|block\-position\|break\"\|break\:\|broken\-pipe\-error\|c\!\|C\"\|c\,\|c\-function\|c\-library\|c\-library\-name\|c\@\|call\-c\|cell\%\|cell\+\|cfield\:\|char\%\|char\+\|class\-\>map\|class\-inst\-size\|class\-override\!\|class\-previous\|class\;\|class\>order\|class\?\|clear\-libs\|clear\-path\|close\-file\|close\-pipe\|cmove\>\|code\-address\!\|common\-list\|COMP\'\|compilation\>\|compile\,\|compile\-lp\+\!\|compile\-only\|const\-does\>\|create\-file\|create\-interpret\/compile\|CS\-PICK\|CS\-ROLL\|current\'\|current\-interface\|d\+\|d\-\|d\.\|d\.r\|d0\<\|d0\<\=\|d0\<\>\|d0\=\|d0\>\|d0\>\=\|d2\*\|d2\/\|d\<\|d\<\=\|d\<\>\|d\=\|d\>\|d\>\=\|d\>f\|d\>s\|dec\.\|defer\!\|defer\@\|definer\!\|delete\-file\|df\!\|df\@\|dffield\:\|dfloat\%\|dfloat\+\|dict\-new\|docol\:\|docon\:\|dodefer\:\|does\-code\!\|does\-handler\!\|DOES\>\|dofield\:\|double\%\|douser\:\|dovar\:\|du\<\|du\<\=\|du\>\|du\>\=\|edit\-line\|ekey\>char\|ekey\>fkey\|ekey\?\|emit\-file\|empty\-buffer\|empty\-buffers\|end\-c\-library\|end\-class\|end\-class\|end\-class\-noname\|end\-code\|end\-interface\|end\-interface\-noname\|end\-methods\|end\-struct\|end\-structure\|endtry\-iferror\|environment\-wordlist\|environment\?\|execute\-parsing\|execute\-parsing\-file\|f\!\|f\*\|f\*\*\|f\+\|f\,\|f\-\|f\.\|f\.rdp\|f\.s\|f\/\|f0\<\|f0\<\=\|f0\<\>\|f0\=\|f0\>\|f0\>\=\|f2\*\|f2\/\|f\<\|f\<\=\|f\<\>\|f\=\|f\>\|f\>\=\|f\>buf\-rdp\|f\>d\|f\>l\|f\>str\-rdp\|f\@\|f\@local\#\|fe\.\|ffield\:\|field\:\|file\-position\|file\-size\|file\-status\|find\-name\|float\%\|float\+\|floating\-stack\|flush\-file\|flush\-icache\|fm\/mod\|forth\-wordlist\|fp\!\|fp\@\|fs\.\|f\~\|f\~abs\|f\~rel\|get\-block\-fid\|get\-current\|get\-order\|heap\-new\|hex\.\|how\:\|id\.\|include\-file\|included\?\|infile\-execute\|init\-asm\|init\-object\|inst\-value\|inst\-var\|interpret\/compile\:\|interpretation\>\|k\-alt\-mask\|k\-ctrl\-mask\|k\-delete\|k\-down\|k\-end\|k\-f1\|k\-f10\|k\-f11\|k\-f12\|k\-f2\|k\-f3\|k\-f4\|k\-f5\|k\-f6\|k\-f7\|k\-f8\|k\-f9\|k\-home\|k\-insert\|k\-left\|k\-next\|k\-prior\|k\-right\|k\-shift\-mask\|k\-up\|key\-file\|key\?\|key\?\-file\|l\!\|laddr\#\|lib\-error\|lib\-sym\|list\-size\|lp\!\|lp\!\|lp\+\!\#\|lp\@\|m\*\|m\*\/\|m\+\|m\:\|maxdepth\-\.s\|name\>comp\|name\>int\|name\>string\|name\?int\|new\[\]\|next\-arg\|open\-blocks\|open\-file\|open\-lib\|open\-path\-file\|open\-pipe\|os\-class\|outfile\-execute\|parse\-name\|parse\-word\|path\+\|path\-allot\|path\=\|postpone\,\|r\/o\|r\/w\|r\>\|r\@\|read\-file\|read\-line\|rename\-file\|reposition\-file\|resize\-file\|restore\-input\|rp\!\|rp\@\|S\"\|s\>d\|s\>number\?\|s\>unumber\?\|s\\\"\|save\-buffer\|save\-buffers\|save\-input\|search\-wordlist\|see\-code\|see\-code\-range\|set\-current\|set\-order\|set\-precision\|sf\!\|sf\@\|sffield\:\|sfloat\%\|sfloat\+\|shift\-args\|simple\-see\|simple\-see\-range\|sl\@\|slurp\-fid\|slurp\-file\|sm\/rem\|source\-id\|sourceline\#\|sp\!\|sp\@\|str\<\|str\=\|string\-prefix\?\|sub\-list\?\|sw\@\|threading\-method\|time\&date\|to\-this\|U\+DO\|U\-DO\|u\.\|u\.r\|u\<\|u\<\=\|u\>\|u\>\=\|ud\.\|ud\.r\|ul\@\|um\*\|um\/mod\|under\+\|updated\?\|uw\@\|w\!\|w\/o\|write\-file\|write\-line\|x\-size\|x\-width\|x\\string\-\|xc\!\+\?\|xc\-size\|xc\@\+\|xchar\+\|xchar\-\|xchar\-encoding\|xt\-new\|xt\-see\|\~\~)\>"

 ## Comment highlighting
 color brightblue start="(^| )\( " end="\)"
 color brightblue "\\ .*$"

```

#### Другие определения

Усовершенствованная подсветка синтаксиса, которая заменит и расширит подсветку по умолчанию находится в AUR, [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/).

### Другие настройки

#### Фоновый режим

В отличие от большинства интерактивных программ, фоновый режим не включен по умолчанию. Чтобы изменить это, раскомментируйте строку 'set suspend' в `/etc/nanorc`. Это позволит вам использовать клавиши `Ctrl+z` чтобы отправить nano в фоновый режим.

#### Перенос текста

В отличие от многих других текстовых редакторов, *nano* переносит длинные строки. Чтобы отключить это, добавьте следующую строку в `~/.nanorc`

```
set nowrap

```

## Использование

### Специальные функции

*   `Ctrl` Клавиша модификации сочетаний (`^`) представляющих часто используемые функции перечисленные в двух строках внизу экрана nano.
*   Дополнительные интерактивные функции доступны путём нажатия `Meta` (обычно это `Alt`) и/или `Esc`.

#### Горячие клавиши

| Сочетание клавиш (Ctrl+..) | Клавиша | Команда | Описание |
| ^G | F1 | Get Help | Показать справку |
| ^X | F2 | Exit | Выйти из nano |
| ^O | F3 | WriteOut | Сохранить внесенные изменения |
| ^J | F4 | Justify | Выровнять текущий абзац (абзацы отделены пустой строкой) |
| ^R | F5 | Read File | Добавить содержимое другого файла в текущий |
| ^W | F6 | Where | Поиск по файлу |
| ^Y | F7 | Prev Page | Страница назад |
| ^V | F8 | Next Page | Страница вперед |
| ^K | F9 | Cut Text | Вырезать текущую строку и запомнить |
| ^U | F10 | UnCut Text | Вставить |
| ^C | F11 | Cur Pos | Положение курсора |
| ^T | F12 | To Spell | Проверить орфографию `spell`, если достумно |

**Совет:** Смотрите онлайн справку в nano используя `Ctrl+g` и [nano Command Manual](http://www.nano-editor.org/dist/v2.1/nano.html) для полного описания и поддержки.

#### Selected toggle functions

| Key1 | Key2 | Description |
| Meta+c | Esc+c | Toggles support for line, column and character position information |
| Meta+i | Esc+i | Toggles support for the auto indentation of lines |
| Meta+k | Esc+k | Toggles support for cutting text from the current cursor position to the end of the line |
| Meta+m | Esc+m | Toggles mouse support for cursor placement, marking and shortcut execution |
| Meta+x | Esc+x | Toggles the display of the shortcut list at the bottom of the nano screen for additional screen space |

**Tip:** [Feature Toggles](http://www.nano-editor.org/dist/v2.1/nano.html#Feature-Toggles) lists the global toggles available for nano.

## Советы и хитрости

### Замена vi на nano

Обычные пользователи предпочитают использовать вместо `vi` `nano`. При своей лёгкости и простоте в использовании, можете заменить VI на nano, как текстовый редактор по умолчанию для таких команд, как [visudo](/index.php/Sudo#Using_visudo "Sudo"). [Установка переменных](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D1.85 "Environment variables (Русский)") EDITOR будет работать для многих приложений, например:

```
export EDITOR=nano

```

## Решение проблем

### Оконный менеджер перехватывает горячие клавиши

Некоторые оконные менеджеры используют сочетания клавиш конфликтующие с nano, например `Alt+Enter`. Удалите и переназначьте их на `Super` ([dconf](https://www.archlinux.org/packages/?name=dconf) для [mutter](https://www.archlinux.org/packages/?name=mutter), [muffin](https://www.archlinux.org/packages/?name=muffin) и [marco](https://www.archlinux.org/packages/?name=marco)) перезапустите оконный менеджер.

## Смотрите также

*   [nano (text editor)](https://en.wikipedia.org/wiki/ru:Nano_(text_editor) - Статья в Википедии
*   [GNU nano Homepage](http://www.nano-editor.org/) - Официальный сайт (Eng)
*   [GNU nano Bugs](https://savannah.gnu.org/bugs/?group=nano) Отчёт ошибок (Eng)
*   [Улучшенное определение подсветки синтаксиса (Eng)](https://github.com/craigbarnes/nanorc)