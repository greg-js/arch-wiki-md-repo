# nano

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[GNU nano](http://www.nano-editor.org/) (or nano) is a text editor which aims to introduce a simple interface and intuitive command options to console based text editing. _nano_ supports features including colorized syntax highlighting, DOS/Mac file type conversions, spellchecking and [UTF-8](https://en.wikipedia.org/wiki/UTF-8 "wikipedia:UTF-8") encoding. _nano_ opened with an empty buffer typically occupies under 1.5 MB of resident memory.

## Contents

*   [1 Package installation](#Package_installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Creating ~/.nanorc](#Creating_.7E.2F.nanorc)
    *   [2.2 Syntax highlighting](#Syntax_highlighting)
        *   [2.2.1 Enable highlighting](#Enable_highlighting)
        *   [2.2.2 PKGBUILD](#PKGBUILD)
        *   [2.2.3 Forth](#Forth)
        *   [2.2.4 Other definitions](#Other_definitions)
    *   [2.3 Suggested configuration](#Suggested_configuration)
        *   [2.3.1 Suspension](#Suspension)
        *   [2.3.2 Text wrapping](#Text_wrapping)
*   [3 Usage](#Usage)
    *   [3.1 Special functions](#Special_functions)
        *   [3.1.1 Shortcut lists overview](#Shortcut_lists_overview)
        *   [3.1.2 Selected toggle functions](#Selected_toggle_functions)
*   [4 Tips & tricks](#Tips_.26_tricks)
    *   [4.1 Replacing vi with nano](#Replacing_vi_with_nano)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Hijacked keybindings](#Hijacked_keybindings)
*   [6 See also](#See_also)

## Package installation

You can install the [nano](https://www.archlinux.org/packages/?name=nano) package from the [official repositories](/index.php/Official_repositories "Official repositories"). It is likely that is already on your system, as it is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group.

## Configuration

### Creating ~/.nanorc

The look, feel, and function of nano is typically controlled by way of either command-line arguments, or configuration commands within the file `~/.nanorc`.

A sample configuration file is installed upon program installation and is located at `/etc/nanorc`. To customize your nano configuration, first create a local copy at `~/.nanorc`:

```
$ cp /etc/nanorc ~/.nanorc

```

Proceed to establish the nano console environment by setting and/or unsetting commands within `~/.nanorc` file.

**Tip:** [NANORC](http://www.nano-editor.org/dist/v2.2/nanorc.5.html) details the complete list configuration commands available for nano.

**Note:** Command-line arguments override and take precedence over the configuration commands established in `~/.nanorc`

### Syntax highlighting

#### Enable highlighting

Install [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/)<sup><small>AUR</small></sup> package and run:

```
cat /usr/share/nano-syntax-highlighting/nanorc.sample | xargs -0 echo >> ~/.nanorc

```

#### PKGBUILD

This new version highlights like the Arch Linux ["svntogit-server"](https://projects.archlinux.org/svntogit/packages.git/tree).

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

This is another version from this [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=565476).

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

Save this file as (for example) `/etc/nano/pkgbuild.nanorc`.

Then include the file in your `~/.nanorc` or to `/etc/nanorc` by adding the following line:

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

#### Other definitions

Syntax highlighting enhancements which replace and expand the defaults can be found in the AUR, [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/)<sup><small>AUR</small></sup>.

### Suggested configuration

#### Suspension

Unlike most interactive programs, suspension is not enabled by default. To change this, uncomment the 'set suspend' line in `/etc/nanorc`. This will allow you to use the keys `Ctrl+z` to send nano to the background.

#### Text wrapping

Unlike many text editors, _nano_ wraps text. To disable this put this in your `~/.nanorc`

```
set nowrap

```

## Usage

### Special functions

*   `Ctrl` key modified shortcuts (`^`) representing commonly used functions are listed along the bottom two lines of the nano screen.
*   Additional functions can be interactively toggled by way of `Meta` (typically `Alt`) and/or `Esc` key modified sequences.

#### Shortcut lists overview

<table class="wikitable">

<tbody>

<tr>

<th>Key1</th>

<th>Key2</th>

<th>Command</th>

<th>Description</th>

</tr>

<tr>

<td>^G</td>

<td>F1</td>

<td>Get Help</td>

<td>Displays the online help files within the session window. A suggested read for nano users of all levels</td>

</tr>

<tr>

<td>^X</td>

<td>F2</td>

<td>Exit</td>

<td>Close and exit nano</td>

</tr>

<tr>

<td>^O</td>

<td>F3</td>

<td>WriteOut</td>

<td>Save the contents of the current file buffer to a file on the disk</td>

</tr>

<tr>

<td>^J</td>

<td>F4</td>

<td>Justify</td>

<td>Aligns text according to the geometry of the console window</td>

</tr>

<tr>

<td>^R</td>

<td>F5</td>

<td>Read File</td>

<td>Inserts another file into the current one at the cursor location</td>

</tr>

<tr>

<td>^W</td>

<td>F6</td>

<td>Where</td>

<td>Perform a case-insensitive string, or regular expression search</td>

</tr>

<tr>

<td>^Y</td>

<td>F7</td>

<td>Prev Page</td>

<td>Display the previous buffered screen</td>

</tr>

<tr>

<td>^V</td>

<td>F8</td>

<td>Next Page</td>

<td>Display the next buffered screen</td>

</tr>

<tr>

<td>^K</td>

<td>F9</td>

<td>Cut Text</td>

<td>Cut and store the current line from the beginning of the line to the end of the line</td>

</tr>

<tr>

<td>^U</td>

<td>F10</td>

<td>UnCut Text</td>

<td>Paste the contents of the cut buffer to the current cursor location</td>

</tr>

<tr>

<td>^C</td>

<td>F11</td>

<td>Cur Pos</td>

<td>Display line, column and character position information at the current location of the cursor</td>

</tr>

<tr>

<td>^T</td>

<td>F12</td>

<td>To Spell</td>

<td>Spellcheck the contents of the buffer with the built-in `spell`, if available</td>

</tr>

</tbody>

</table>

**Tip:** See the nano online help files via `Ctrl+g` within nano and the [nano Command Manual](http://www.nano-editor.org/dist/v2.1/nano.html) for complete descriptions and additional support.

#### Selected toggle functions

<table class="wikitable">

<tbody>

<tr>

<th>Key1</th>

<th>Key2</th>

<th>Description</th>

</tr>

<tr>

<td>Meta+c</td>

<td>Esc+c</td>

<td>Toggles support for line, column and character position information</td>

</tr>

<tr>

<td>Meta+i</td>

<td>Esc+i</td>

<td>Toggles support for the auto indentation of lines</td>

</tr>

<tr>

<td>Meta+k</td>

<td>Esc+k</td>

<td>Toggles support for cutting text from the current cursor position to the end of the line</td>

</tr>

<tr>

<td>Meta+m</td>

<td>Esc+m</td>

<td>Toggles mouse support for cursor placement, marking and shortcut execution</td>

</tr>

<tr>

<td>Meta+x</td>

<td>Esc+x</td>

<td>Toggles the display of the shortcut list at the bottom of the nano screen for additional screen space</td>

</tr>

</tbody>

</table>

**Tip:** [Feature Toggles](http://www.nano-editor.org/dist/v2.1/nano.html#Feature-Toggles) lists the global toggles available for nano.

## Tips & tricks

### Replacing vi with nano

Casual users may prefer to use `nano` over `vi` for its simplicity and ease of use, and may opt to replace vi with nano as the default text editor for commands such as [visudo](/index.php/Sudo#Using_visudo "Sudo").

Setting the `EDITOR` [environment variable](/index.php/Environment_variable#Defining_variables "Environment variable") will work for many applications, for example:

```
export EDITOR=nano

```

## Troubleshooting

### Hijacked keybindings

Some window managers have keybindings that conflict with nano, for example `Alt+Enter`. Remove or remap them to e.g `Super` (with [dconf](https://www.archlinux.org/packages/?name=dconf) for [mutter](https://www.archlinux.org/packages/?name=mutter), [muffin](https://www.archlinux.org/packages/?name=muffin) and [marco](https://www.archlinux.org/packages/?name=marco)) and restart the window manager.

## See also

*   [nano (text editor)](https://en.wikipedia.org/wiki/Nano_(text_editor) "wikipedia:Nano (text editor)") - Wikipedia Entry
*   [GNU nano Homepage](http://www.nano-editor.org/) - Official Site
*   [GNU nano Bugs](https://savannah.gnu.org/bugs/?group=nano) Bug Reporting
*   [Better syntax highlighting definitions](https://github.com/craigbarnes/nanorc)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Nano&oldid=404015](https://wiki.archlinux.org/index.php?title=Nano&oldid=404015)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Text editors](/index.php/Category:Text_editors "Category:Text editors")