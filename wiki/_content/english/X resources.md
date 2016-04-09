**Xresources** is a user-level configuration *dotfile*, typically located at `~/.Xresources`. It can be used to set [X resources](https://en.wikipedia.org/wiki/X_resources "wikipedia:X resources"), which are configuration parameters for X client applications.

They can do many operations, including:

*   defining terminal colours
*   configuring terminal preferences
*   setting DPI, antialiasing, hinting and other X font settings
*   changing the Xcursor theme
*   theming xscreensaver
*   altering preferences on low-level X applications (xclock ([xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock)), [xpdf](https://aur.archlinux.org/packages/xpdf/), [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode), etc.)

**Note:** Using `~/.Xdefaults` is deprecated, so this article will only refer to resources loaded with xrdb

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Parsing .Xresources](#Parsing_.Xresources)
    *   [1.2 Adding to xinitrc](#Adding_to_xinitrc)
    *   [1.3 Default settings](#Default_settings)
    *   [1.4 Xresources syntax](#Xresources_syntax)
        *   [1.4.1 Basic syntax](#Basic_syntax)
        *   [1.4.2 Wildcard matching](#Wildcard_matching)
        *   [1.4.3 Commenting](#Commenting)
        *   [1.4.4 Include files](#Include_files)
*   [2 Sample usage](#Sample_usage)
    *   [2.1 Terminal colors](#Terminal_colors)
    *   [2.2 Xcursor](#Xcursor)
    *   [2.3 Xft](#Xft)
    *   [2.4 Xterm](#Xterm)
    *   [2.5 rxvt-unicode](#rxvt-unicode)
    *   [2.6 Xpdf](#Xpdf)
*   [3 Color scheme commands](#Color_scheme_commands)
    *   [3.1 Display all 256 colors](#Display_all_256_colors)
    *   [3.2 Display tput escape codes](#Display_tput_escape_codes)
    *   [3.3 Enumerating colors supported by terminals](#Enumerating_colors_supported_by_terminals)
    *   [3.4 Enumerating terminal capabilities](#Enumerating_terminal_capabilities)
*   [4 Color scheme scripts](#Color_scheme_scripts)
    *   [4.1 LUA](#LUA)
    *   [4.2 Bash](#Bash)
    *   [4.3 Ruby](#Ruby)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Parsing errors](#Parsing_errors)
*   [6 See also](#See_also)

## Usage

Make sure that [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb) is installed in your system.

### Parsing .Xresources

The file `~/.Xresources` does not exist by default. It is a plain-text file, so you can create it with any text editor. Once present it will be parsed automatically, by one of:

*   Most [Display managers](/index.php/Display_manager "Display manager") will load the `~/.Xresources` file on login.
*   If using `startx` you may need to edit `.xinitrc`, see below for details.

The resources will be stored in the X server, so the file does not need to be read every time an app is started. The file can be reread to make any changes take effect.

To reread the `.Xresources` file and throw away the old resources:

```
xrdb ~/.Xresources

```

To reread the `.Xresources` file and keep the old resources:

```
xrdb -merge ~/.Xresources

```

**Tip:** `~/.Xresources` is just a naming convention; `xrdb` can load any file. If you use `xrdb` manually, you can put such a file anywhere you want (for example, `~/.config/Xresources`).

**Note:** Resources loaded with `xrdb` are also accessible to *remote* X11 clients (such as those forwarded over SSH).

**Warning:** The older and deprecated `~/.Xdefaults` file is read every time you start an X11 program such as `xterm`, but **only** if `xrdb` has not **ever** been used in the current X session. [[1]](https://groups.google.com/forum/#!msg/comp.windows.x/hQBEdql8l-Q/hF3DETcIHGwJ)

### Adding to xinitrc

If you are using a copy of the default [xinitrc](/index.php/Xinitrc "Xinitrc") as your `.xinitrc` it already merges `~/.Xresources`.

If you are using a custom `.xinitrc` add the following line:

```
[[ -f ~/.Xresources ]] && xrdb -merge -I$HOME ~/.Xresources

```

**Warning:** Never background the xrdb command within `~/.xinitrc`. Otherwise, programs launched after xrdb may look for resources before it has finished loading them.

### Default settings

To see the default settings for your installed X11 apps, look in `/usr/share/X11/app-defaults/`.

Detailed information on program-specific resources is usually provided in the man page for the program. xterm's man page is a good example, as it contains a list of X resources and their default values.

To see the current loaded resources:

```
xrdb -query -all

```

### Xresources syntax

#### Basic syntax

The syntax of an Xresources file is as follows:

```
**name.Class.resource: value**

```

and here is a real world example:

```
xscreensaver.Dialog.headingFont: -*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

	name

	The name of the application, such as xterm, xpdf, etc

	class

	The classification used to group resources together. Class names are typically uppercase.

	resource

	The name of the resource whose value is to be changed. Resources are typically lowercase with uppercase concatenation.

	value

	The actual value of the resource. This can be 1 of 3 types:

*   Integer (whole numbers)
*   Boolean (true/false, yes/no, on/off)
*   String (a string of characters) (for example a word (`white`), a color (`#ffffff`), or a path (`/usr/bin/firefox`))

	delimiters

	A dot (`**.**`) is used to signify each step down into the hierarchy — in the above example we start at name, then descend into Class, and finally into the resource itself. A colon (`**:**`) is used to separate the resource declaration from the actual value.

#### Wildcard matching

The asterisk can be used as a wildcard, making it easy to write a single rule that can be applied to many different applications or elements.

Using the previous example, if you want to apply the same font to all programs (not just XScreenSaver) that contain the class name `Dialog` which contains the resource name `headingFont`, you would write:

```
*****Dialog.headingFont:     -*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

If you want to apply this same rule to all programs that contain the resource `headingFont`, regardless of its class, you would write:

```
*****headingFont:    -*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

#### Commenting

To add a comment to your Xresources file, simply prefix it with an exclamation mark (`!`), for example:

```
! The following rule will be ignored because it has been commented out
!Xft.antialias:        true

```

#### Include files

To use different files for each application, use `#include` in the main file. For example:

 `~/.Xresources` 
```
#include ".Xresources.d/xterm"
#include ".Xresources.d/rxvt-unicode"
#include ".Xresources.d/fonts"
#include ".Xresources.d/xscreensaver"

```

If files fail to load, specify the directory to *xrdb* with the `-I` parameter. For example:

 `~/.xinitrc` 
```
xrdb -I*$HOME* ~/.Xresources

```

## Sample usage

The following samples should provide a good understanding of how application settings can be modified using an Xresources file. See [[2]](https://gist.github.com/anonymous/fa98de9fd70b51611303) for more examples. Refer to the man page of the application in question otherwise.

### Terminal colors

Most terminals, including [xterm](/index.php/Xterm "Xterm") and [urxvt](/index.php/Urxvt "Urxvt"), support at least 16 basic colors. The colors 0-7 are the 'normal' colors. Colors 8-15 are their 'bright' counterparts, used for highlighting.

```
! Black + DarkGrey
*color0:  #000000
*color8:  #555753
! DarkRed + Red
*color1:  #ff6565
*color9:  #ff8d8d
! DarkGreen + Green
*color2:  #93d44f
*color10: #c8e7a8
! DarkYellow + Yellow
*color3:  #eab93d
*color11: #ffc123
! DarkBlue + Blue
*color4:  #204a87
*color12: #3465a4
! DarkMagenta + Magenta
*color5:  #ce5c00
*color13: #f57900
!DarkCyan + Cyan (both not tango)
*color6:  #89b6e2
*color14: #46a4ff
! LightGrey + White
*color7:  #cccccc
*color15: #ffffff

```

See [man page#Colored man pages on xterm or rxvt-unicode](/index.php/Man_page#Colored_man_pages_on_xterm_or_rxvt-unicode "Man page") for how to color bold and underlined text automatically xterm and rxvt.

**Warning:** Color resources such as `foreground` and `background` can be read by other applications (such as [emacs](https://www.gnu.org/software/emacs/manual/html_node/emacs/Table-of-Resources.html)). This can be avoided by specifiying the class name, for example `XTerm.foreground`.

### Xcursor

See [Cursor themes#X resources](/index.php/Cursor_themes#X_resources "Cursor themes").

### Xft

See [Font configuration#Applications without fontconfig support](/index.php/Font_configuration#Applications_without_fontconfig_support "Font configuration").

### Xterm

See [Xterm#Configuration](/index.php/Xterm#Configuration "Xterm").

### rxvt-unicode

See [Rxvt-unicode#Configuration](/index.php/Rxvt-unicode#Configuration "Rxvt-unicode").

### Xpdf

See `**Options**` in [man xpdf](http://linux.die.net/man/1/xpdf).

## Color scheme commands

Here are some fast bash commands you can run right in your shell.

### Display all 256 colors

Prints all 256 colors across the screen, very quick.

```
(x=`tput op` y=`printf %76s`;for i in {0..256};do o=00$i;echo -e ${o:${#o}-3:3} `tput setaf $i;tput setab $i`${y// /=}$x;done)

```

### Display tput escape codes

Replace `tput op` with whatever tput you want to trace. `op` is the default foreground and background color.

```
$ ( strace -s5000 -e write tput op 2>&2 2>&1 ) | tee -a /dev/stderr | grep -o '"[^"]*"'

```

```
033[\033[1;34m"\33[39;49m"\033[00m

```

### Enumerating colors supported by terminals

The following command will let you discover all the terminals you have terminfo support for, and the number of colors each terminal supports. The possible values are: 8, 15, 16, 52, 64, 88 and 256.

```
$ for T in `find /usr/share/terminfo -type f -printf '%f '`;do echo "$T `tput -T $T colors`";done|sort -nk2

```

```
Eterm-88color 88
rxvt-88color 88
xterm+88color 88
xterm-88color 88
Eterm-256color 256
gnome-256color 256
konsole-256color 256
putty-256color 256
rxvt-256color 256
screen-256color 256
screen-256color-bce 256
screen-256color-bce-s 256
screen-256color-s 256
xterm+256color 256
xterm-256color 256

```

### Enumerating terminal capabilities

This command is useful to see what features that are supported by your terminal.

```
$ infocmp -1 | sed -nu 's/^[ \000\t]*//;s/[ \000\t]*$//;/[^ \t\000]\{1,\}/!d;/acsc/d;s/=.*,//p'|column -c80

```

```
bel	cuu	ich	kb2	kf15	kf3	kf44	kf59	mc0	rmso	smul
blink	cuu1	il	kbs	kf16	kf30	kf45	kf6	mc4	rmul	tbc
bold	cvvis	il1	kcbt	kf17	kf31	kf46	kf60	mc5	rs1	u6
cbt	dch	ind	kcub1	kf18	kf32	kf47	kf61	meml	rs2	u7
civis	dch1	indn	kcud1	kf19	kf33	kf48	kf62	memu	sc	u8
clear	dl	initc	kcuf1	kf2	kf34	kf49	kf63	op	setab	u9
cnorm	dl1	invis	kcuu1	kf20	kf35	kf5	kf7	rc	setaf	vpa

```

## Color scheme scripts

Any of the following scripts will display a chart of your current terminal color scheme. Handy for testing and whatnot.

### LUA

```
#!/usr/bin/env lua

function cl(e)
	return string.format('\27[%sm', e)
end

function print_fg(bg, pre)
	for fg = 30,37 do
		fg = pre..fg
		io.write(cl(bg), cl(fg), string.format(' %6s ', fg), cl(0))
	end
end

for bg = 40,47 do
	io.write(cl(0), ' ', bg, ' ')
	print_fg(bg, ' ')
	io.write('
    ')
	print_fg(bg, '1;')
	io.write('

')
end

-- Andres P
```

### Bash

```
#!/usr/bin/bash
#
# ANSI color scheme script featuring Space Invaders
#
# Original: [http://crunchbang.org/forums/viewtopic.php?pid=126921%23p126921#p126921](http://crunchbang.org/forums/viewtopic.php?pid=126921%23p126921#p126921)
# Modified by lolilolicon
#

f=3 b=4
for j in f b; do
  for i in {0..7}; do
    printf -v $j$i %b "\e[${!j}${i}m"
  done
done
bld=$'\e[1m'
rst=$'\e[0m'

cat << EOF

 $f1  ▀▄   ▄▀     $f2 ▄▄▄████▄▄▄    $f3  ▄██▄     $f4  ▀▄   ▄▀     $f5 ▄▄▄████▄▄▄    $f6  ▄██▄  $rst
 $f1 ▄█▀███▀█▄    $f2███▀▀██▀▀███   $f3▄█▀██▀█▄   $f4 ▄█▀███▀█▄    $f5███▀▀██▀▀███   $f6▄█▀██▀█▄$rst
 $f1█▀███████▀█   $f2▀▀███▀▀███▀▀   $f3▀█▀██▀█▀   $f4█▀███████▀█   $f5▀▀███▀▀███▀▀   $f6▀█▀██▀█▀$rst
 $f1▀ ▀▄▄ ▄▄▀ ▀   $f2 ▀█▄ ▀▀ ▄█▀    $f3▀▄    ▄▀   $f4▀ ▀▄▄ ▄▄▀ ▀   $f5 ▀█▄ ▀▀ ▄█▀    $f6▀▄    ▄▀$rst

 $bld$f1▄ ▀▄   ▄▀ ▄   $f2 ▄▄▄████▄▄▄    $f3  ▄██▄     $f4▄ ▀▄   ▄▀ ▄   $f5 ▄▄▄████▄▄▄    $f6  ▄██▄  $rst
 $bld$f1█▄█▀███▀█▄█   $f2███▀▀██▀▀███   $f3▄█▀██▀█▄   $f4█▄█▀███▀█▄█   $f5███▀▀██▀▀███   $f6▄█▀██▀█▄$rst
 $bld$f1▀█████████▀   $f2▀▀▀██▀▀██▀▀▀   $f3▀▀█▀▀█▀▀   $f4▀█████████▀   $f5▀▀▀██▀▀██▀▀▀   $f6▀▀█▀▀█▀▀$rst
 $bld$f1 ▄▀     ▀▄    $f2▄▄▀▀ ▀▀ ▀▀▄▄   $f3▄▀▄▀▀▄▀▄   $f4 ▄▀     ▀▄    $f5▄▄▀▀ ▀▀ ▀▀▄▄   $f6▄▀▄▀▀▄▀▄$rst

                                     $f7▌$rst

                                   $f7▌$rst

                              $f7    ▄█▄    $rst
                              $f7▄█████████▄$rst
                              $f7▀▀▀▀▀▀▀▀▀▀▀$rst

EOF
```

### Ruby

```
#!/usr/bin/env ruby
# coding: utf-8

# ANSI color scheme script 
# Author: Ivaylo Kuzev < Ivo >
# Original: [http://crunchbang.org/forums/viewtopic.php?pid=134749%23p134749#p134749](http://crunchbang.org/forums/viewtopic.php?pid=134749%23p134749#p134749)
# Modified using Ruby.

CL = "\e[0m"
BO = "\e[1m"

R = "\e[31m" 
G = "\e[32m"
Y = "\e[33m"
B = "\e[34m"
P = "\e[35m"
C = "\e[36m"

print <<EOF 

#{BO}#{R}  ██████  #{CL} #{BO}#{G}██████  #{CL}#{BO}#{Y}   ██████#{CL} #{BO}#{B}██████ #{CL}  #{BO}#{P}  ██████#{CL} #{BO}#{C}  ███████#{CL}
#{BO}#{R}  ████████#{CL} #{BO}#{G}██    ██ #{CL}#{BO}#{Y}██ #{CL}      #{BO}#{B}██    ██#{CL} #{BO}#{P}██████ #{CL} #{BO}#{C} █████████#{CL}
#{R}  ██  ████#{CL} #{G}██  ████#{CL}#{Y} ████    #{CL} #{B}████  ██#{CL} #{P}████ #{CL}    #{C}█████ #{CL}
#{R}  ██    ██#{CL} #{G}██████ #{CL}#{Y}  ████████#{CL} #{B}██████ #{CL}  #{P}████████#{CL} #{C}██ #{CL}

EOF
```

## Troubleshooting

### Parsing errors

[Display managers](/index.php/Display_manager "Display manager") such as [GDM](/index.php/GDM "GDM") and [LightDM](/index.php/LightDM "LightDM") may use the `--nocpp` argument for *xrdb*. See [LightDM#Xresources not being parsed correctly](/index.php/LightDM#Xresources_not_being_parsed_correctly "LightDM").

## See also

*   [Using the Xdefaults File](https://engineering.purdue.edu/ECN/Support/KB/Docs/UsingTheXdefaultsFil) - An in-depth article on how X interprets the Xdefaults file
*   [Rxvt-unicode Configuration Tutorial](http://wiki.afterstep.org/index.php?title=Rxvt-Unicode_Configuration_Tutorial) - lots of information for urxvt users
*   [Example Colors and their names](http://mkaz.com/solog/system/xterm-colors.html) - listing of example colors and their color names for xterm and other X-applications.
*   [Color Themes](https://web.archive.org/web/20090130061234/http://phraktured.net/terminal-colors/) - Extensive list of terminal color themes by Phraktured.
*   [Xcolors.net](http://xcolors.net/) List of user-contributed terminal color themes.
*   [Xcolors by dkeg](http://beta.andrewrcraig.us/index.php?page=xcolors)