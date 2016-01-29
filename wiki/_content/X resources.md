# X resources

**Xresources** is a user-level configuration _dotfile_, typically located at `~/.Xresources`. It can be used to set [X resources](https://en.wikipedia.org/wiki/X_resources "wikipedia:X resources"), which are configuration parameters for X client applications.

They can do many operations, including:

*   defining terminal colours
*   configuring terminal preferences
*   setting DPI, antialiasing, hinting and other X font settings
*   changing the Xcursor theme
*   theming xscreensaver
*   altering preferences on low-level X applications (xclock ([xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock)), [xpdf](https://aur.archlinux.org/packages/xpdf/)<sup><small>AUR</small></sup>, [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode), etc.)

**Note:** Using `~/.Xdefaults` is deprecated, so this article will only refer to resources loaded with xrdb

## Contents

*   [1 Getting started](#Getting_started)
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
    *   [2.2 Xcursor resources](#Xcursor_resources)
    *   [2.3 Xft resources](#Xft_resources)
    *   [2.4 Xterm resources](#Xterm_resources)
    *   [2.5 rxvt-unicode (urxvt) resources](#rxvt-unicode_.28urxvt.29_resources)
    *   [2.6 Aterm preferences](#Aterm_preferences)
    *   [2.7 Xpdf resources](#Xpdf_resources)
    *   [2.8 Lal clock resources](#Lal_clock_resources)
    *   [2.9 Xclock preferences](#Xclock_preferences)
    *   [2.10 X11-ssh-askpass resources](#X11-ssh-askpass_resources)
    *   [2.11 XScreenSaver resources](#XScreenSaver_resources)
    *   [2.12 Xcalc resources](#Xcalc_resources)
*   [3 Color scheme commands](#Color_scheme_commands)
    *   [3.1 Display all 256 colors](#Display_all_256_colors)
    *   [3.2 Display tput escape codes](#Display_tput_escape_codes)
    *   [3.3 Enumerating colors supported by terminals](#Enumerating_colors_supported_by_terminals)
    *   [3.4 Enumerating terminal capabilities](#Enumerating_terminal_capabilities)
*   [4 Color scheme scripts](#Color_scheme_scripts)
    *   [4.1 Script #1](#Script_.231)
    *   [4.2 Script #2](#Script_.232)
    *   [4.3 Script #3](#Script_.233)
    *   [4.4 Script #4](#Script_.234)
    *   [4.5 Script #5](#Script_.235)
    *   [4.6 Script #6](#Script_.236)
    *   [4.7 Script #7](#Script_.237)
*   [5 Contributed examples](#Contributed_examples)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Parsing errors](#Parsing_errors)
*   [7 See also](#See_also)

## Getting started

Make sure that [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb) is installed in your system.

### Parsing .Xresources

The file `~/.Xresources` does not exist by default. Being a plain-text file, you can create and edit it with the text editor of your choice. Once present, it will be parsed by the `xrdb` (Xorg resource database) program automatically, provided that you either:

*   are using a [Display manager](/index.php/Display_manager "Display manager") to log into X. Most DM will automatically load the `~/.Xresources` file on login.
*   if you are using `startx`, you have to edit your `~/.[xinitrc](/index.php/Xinitrc "Xinitrc")`. See below for details.

The resources will be stored in the X server so the file does not need to be read every time an app is started.

To reread your .Xresources file, and throw away your old resources:

```
xrdb ~/.Xresources

```

To reread your .Xresources file, and keep your old resources:

```
xrdb -merge ~/.Xresources

```

**Tip:** `~/.Xresources` is just a naming convention; xrdb can load any file. If you use xrdb manually, you can put such a file anywhere you want (for example, `~/.config/Xresources`).

**Note:** Resources loaded with xrdb are also accessible to _remote_ X11 clients (such as those forwarded over SSH).

**Warning:**

*   If you background the execution of xrdb in a chain of commands in `~/.xinitrc`, the programs launched in the same chain might not be able to make use of it, so it is recommended to _never_ background the xrdb command within `~/.xinitrc`.
*   The older and deprecated `~/.Xdefaults` file is read every time you start an X11 program such as `xterm`, but **only** if `xrdb` has not **ever** been used in the current X session. [[1]](https://groups.google.com/forum/#!msg/comp.windows.x/hQBEdql8l-Q/hF3DETcIHGwJ)

### Adding to xinitrc

If you do not use a [desktop environment](/index.php/Desktop_environment "Desktop environment"), add the following line to [xinitrc](/index.php/Xinitrc "Xinitrc"):

```
[[ -f ~/.Xresources ]] && xrdb -merge -I$HOME ~/.Xresources

```

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

NaN

NaN

NaN

NaN

NaN

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

If files fail to load, specify the directory to _xrdb_ with the `-I` parameter. For example:

 `~/.xinitrc` 

```
xrdb -I_$HOME_ ~/.Xresources

```

## Sample usage

The following samples should provide a good understanding of how application settings can be modified using an Xresources file. For full details, refer to the man page of the application in question.

### Terminal colors

Most terminals, including [xterm](/index.php/Xterm "Xterm") and [urxvt](/index.php/Urxvt "Urxvt"), support at least 16 basic colors. The following is an example of a 16-color scheme. The colors 0-7 are the 'normal' colors, while colors 8-15 are their 'bright' counterparts, used for highlighting and such. A good place to start when making your Xresources, is to define the default terminal colors:

```
! terminal colors ------------------------------------------------------------

! tangoesque scheme
*background: #111111
*foreground: #babdb6
! Black (not tango) + DarkGrey
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

For more examples of color schemes, see the [#Contributed examples](#Contributed_examples) section at the bottom of this article.

### Xcursor resources

Set the theme and size of your mouse cursor:

```
! Xcursor --------------------------------------------------------------------

Xcursor.theme: Vanilla-DMZ-AA
Xcursor.size:  22

```

Available themes reside in `/usr/share/icons` and local themes can be installed to `~/.icons`.

### Xft resources

You can define basic font resources without the need of a `fonts.conf` file or a desktop environment. Note however, the use of a desktop environment and/or `fonts.conf` can override these settings. Your best option is to use one or the other, but not both.

```
! Xft settings ---------------------------------------------------------------

Xft.dpi:        96
Xft.antialias:  true
Xft.rgba:       rgb
Xft.hinting:    true
Xft.hintstyle:  hintslight

```

### Xterm resources

The following resources will open [xterm](/index.php/Xterm "Xterm") in an 80x25 character window with a scroll-bar and scroll capability for the last 512 lines. The specified [Terminus](/index.php/Fonts#Bitmap "Fonts") facename is a popular and clean terminal font.

```
! xterm ----------------------------------------------------------------------

xterm*VT100.geometry:     80x25
xterm*faceName:           Terminus:style=Regular:size=10
!xterm*font:              -*-dina-medium-r-*-*-16-*-*-*-*-*-*-*
xterm*dynamicColors:      true
xterm*utf8:               2
xterm*eightBitInput:      true
xterm*saveLines:          512
xterm*scrollKey:          true
xterm*scrollTtyOutput:    false
xterm*scrollBar:          true
xterm*rightScrollBar:     true
xterm*jumpScroll:         true
xterm*multiScroll:        true
xterm*toolBar:            false

```

### rxvt-unicode (urxvt) resources

[rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) features an extensive list of options which can be configured via `~/.Xresources`. Refer to the _urxvt_ man page or [rxvt-unicode#Creating ~/.Xresources](/index.php/Rxvt-unicode#Creating_.7E.2F.Xresources "Rxvt-unicode") article for details.

### Aterm preferences

Sample settings for aterm (very similar to urxvt):

```
!aterm settings-------------------------------------------------------------     

aterm*background:               black
aterm*foreground:               white
aterm*transparent:              true
aterm*shading:                  30
aterm*cursorColor:              gray
aterm*saveLines:                2000
!aterm*tinting:                 gray
aterm*scrollBar:                false
!aterm*scrollBar_right:          true
aterm*transpscrollbar:          true
aterm*borderwidth:              0
aterm*font:                     -*-terminus-*-*-*-*-*-*-*-*-*-*-*-*
aterm*geometry:                 80x25
!aterm*fading:                  70  

```

### Xpdf resources

Following are some basic resources for [xpdf](https://aur.archlinux.org/packages/xpdf/)<sup><small>AUR</small></sup>, a lightweight PDF viewer:

```
! xpdf -----------------------------------------------------------------------

xpdf*enableFreetype:    yes
xpdf*antialias:         yes
xpdf*foreground:        black
xpdf*background:        white
xpdf*urlCommand:        /usr/bin/firefox %s

```

Anything more detailed than the above you should be putting in `~/.xpdfrc` instead. See the xpdf man page for more information. Note that `viKeys` is deprecated.

### Lal clock resources

```
! lal clock ------------------------------------------------------------------

lal*font:       Arial
lal*fontsize:   12
lal*bold:       true
lal*color:      #ffffff
lal*width:      150
lal*format:     %a %b %d %l:%M%P

```

### Xclock preferences

Some basic xclock settings. See the xclock man page for all X resources.

```
! xclock ---------------------------------------------------------------------

xclock*update:            1
xclock*analog:            false
xclock*Foreground:        white
xclock*background:        black

```

### X11-ssh-askpass resources

```
! x11-ssh-askpass ------------------------------------------------------------

x11-ssh-askpass*font:                   -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
x11-ssh-askpass*background:             #000000
x11-ssh-askpass*foreground:             #ffffff
x11-ssh-askpass.Button*background:      #000000
x11-ssh-askpass.Indicator*foreground:   #ff9900
x11-ssh-askpass.Indicator*background:   #090909
x11-ssh-askpass*topShadowColor:         #000000
x11-ssh-askpass*bottomShadowColor:      #000000
x11-ssh-askpass.*borderWidth:           1

```

### XScreenSaver resources

The following is a sample [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") theme. For more information, refer to the XScreenSaver man page.

**Note:** In older versions of XScreenSaver, if the `~/.xscreensaver` file exists, it overrides any settings in the X resource database. However, in the latest versions, you can use both simultaneously.

```
! xscreensaver ---------------------------------------------------------------

!font settings
xscreensaver.Dialog.headingFont:        -*-dina-bold-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.bodyFont:           -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.labelFont:          -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.unameFont:          -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.buttonFont:         -*-dina-bold-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.dateFont:           -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.passwd.passwdFont:         -*-dina-bold-r-*-*-12-*-*-*-*-*-*-*
!general dialog box (affects main hostname, username, password text)
xscreensaver.Dialog.foreground:         #ffffff
xscreensaver.Dialog.background:         #111111
xscreensaver.Dialog.topShadowColor:     #111111
xscreensaver.Dialog.bottomShadowColor:  #111111
xscreensaver.Dialog.Button.foreground:  #666666
xscreensaver.Dialog.Button.background:  #ffffff
!username/password input box and date text colour
xscreensaver.Dialog.text.foreground:    #666666
xscreensaver.Dialog.text.background:    #ffffff
xscreensaver.Dialog.internalBorderWidth:24
xscreensaver.Dialog.borderWidth:        20
xscreensaver.Dialog.shadowThickness:    2
!timeout bar (background is actually determined by Dialog.text.background)
xscreensaver.passwd.thermometer.foreground:  #ff0000
xscreensaver.passwd.thermometer.background:  #000000
xscreensaver.passwd.thermometer.width:       8
!datestamp format--see the strftime(3) manual page for details
xscreensaver.dateFormat:    %I:%M%P %a %b %d, %Y

```

### Xcalc resources

Following are some xcalc resources to colorize and customize buttons.

```
!xcalc-----------------------------------------------------------------------

xcalc*geometry:                        200x275
xcalc.ti.bevel.background:             #111111
xcalc.ti.bevel.screen.background:      #000000
xcalc.ti.bevel.screen.DEG.background:  #000000
xcalc.ti.bevel.screen.DEG.foreground:  LightSeaGreen
xcalc.ti.bevel.screen.GRAD.background: #000000
xcalc.ti.bevel.screen.GRAD.foreground: LightSeaGreen
xcalc.ti.bevel.screen.RAD.background:  #000000
xcalc.ti.bevel.screen.RAD.foreground:  LightSeaGreen
xcalc.ti.bevel.screen.INV.background:  #000000
xcalc.ti.bevel.screen.INV.foreground:  Red
xcalc.ti.bevel.screen.LCD.background:  #000000
xcalc.ti.bevel.screen.LCD.foreground:  LightSeaGreen
xcalc.ti.bevel.screen.LCD.shadowWidth: 0
xcalc.ti.bevel.screen.M.background:    #000000
xcalc.ti.bevel.screen.M.foreground:    LightSeaGreen
xcalc.ti.bevel.screen.P.background:    #000000
xcalc.ti.bevel.screen.P.foreground:    Yellow
xcalc.ti.Command.foreground:  White
xcalc.ti.Command.background:  #777777
xcalc.ti.button5.background:  Orange3
xcalc.ti.button19.background: #611161
xcalc.ti.button18.background: #611161
xcalc.ti.button20.background: #611111
!uncomment to change label on division button
!xcalc.ti.button20.label:      /
xcalc.ti.button25.background: #722222
xcalc.ti.button30.background: #833333
xcalc.ti.button35.background: #944444
xcalc.ti.button40.background: #a55555
xcalc.ti.button22.background: #222262
xcalc.ti.button23.background: #222262
xcalc.ti.button24.background: #222272
xcalc.ti.button27.background: #333373
xcalc.ti.button28.background: #333373
xcalc.ti.button29.background: #333373
xcalc.ti.button32.background: #444484
xcalc.ti.button33.background: #444484
xcalc.ti.button34.background: #444484
xcalc.ti.button37.background: #555595
xcalc.ti.button38.background: #555595
xcalc.ti.button39.background: #555595
XCalc*Cursor:                 hand2
XCalc*ShapeStyle:             rectangle

```

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

### Script #1

```
#!/usr/bin/bash
#
#   This file echoes a bunch of color codes to the 
#   terminal to demonstrate what's available.  Each 
#   line is the color code of one foreground color,
#   out of 17 (default + 16 escapes), followed by a 
#   test use of that color on all nine background 
#   colors (default + 8 escapes).
#

T='gYw'   # The test text

echo -e "\n                 40m     41m     42m     43m\
     44m     45m     46m     47m";

for FGs in '    m' '   1m' '  30m' '1;30m' '  31m' '1;31m' '  32m' \
           '1;32m' '  33m' '1;33m' '  34m' '1;34m' '  35m' '1;35m' \
           '  36m' '1;36m' '  37m' '1;37m';
  do FG=${FGs// /}
  echo -en " $FGs \033[$FG  $T  "
  for BG in 40m 41m 42m 43m 44m 45m 46m 47m;
    do echo -en "$EINS \033[$FG\033[$BG  $T  \033[0m";
  done
  echo;
done
echo
```

### Script #2

```
#!/usr/bin/bash
# Original: [http://frexx.de/xterm-256-notes/](http://frexx.de/xterm-256-notes/) <sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2013-11-21]</sup>
#           [http://frexx.de/xterm-256-notes/data/colortable16.sh](http://frexx.de/xterm-256-notes/data/colortable16.sh) <sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2013-11-21]</sup>
# Modified by Aaron Griffin
# and further by Kazuo Teramoto
FGNAMES=(' black ' '  red  ' ' green ' ' yellow' '  blue ' 'magenta' '  cyan ' ' white ')
BGNAMES=('DFT' 'BLK' 'RED' 'GRN' 'YEL' 'BLU' 'MAG' 'CYN' 'WHT')

echo "     ┌──────────────────────────────────────────────────────────────────────────┐"
for b in {0..8}; do
  ((b>0)) && bg=$((b+39))

  echo -en "\033[0m ${BGNAMES[b]} │ "

  for f in {0..7}; do
    echo -en "\033[${bg}m\033[$((f+30))m ${FGNAMES[f]} "
  done

  echo -en "\033[0m │"
  echo -en "\033[0m\n\033[0m     │ "

  for f in {0..7}; do
    echo -en "\033[${bg}m\033[1;$((f+30))m ${FGNAMES[f]} "
  done

  echo -en "\033[0m │"
  echo -e "\033[0m"

  ((b<8)) &&
  echo "     ├──────────────────────────────────────────────────────────────────────────┤"
done
echo "     └──────────────────────────────────────────────────────────────────────────┘"
```

### Script #3

```
#!/usr/bin/bash
# Original: [http://frexx.de/xterm-256-notes/](http://frexx.de/xterm-256-notes/) <sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2013-11-21]</sup>
#           [http://frexx.de/xterm-256-notes/data/colortable16.sh](http://frexx.de/xterm-256-notes/data/colortable16.sh) <sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2013-11-21]</sup>
# Modified by Aaron Griffin
# and further by Kazuo Teramoto

FGNAMES=(' black ' '  red  ' ' green ' ' yellow' '  blue ' 'magenta' '  cyan ' ' white ')
BGNAMES=('DFT' 'BLK' 'RED' 'GRN' 'YEL' 'BLU' 'MAG' 'CYN' 'WHT')
echo "     ----------------------------------------------------------------------------"
for b in $(seq 0 8); do
    if [ "$b" -gt 0 ]; then
      bg=$(($b+39))
    fi

    echo -en "\033[0m ${BGNAMES[$b]} : "
    for f in $(seq 0 7); do
      echo -en "\033[${bg}m\033[$(($f+30))m ${FGNAMES[$f]} "
    done
    echo -en "\033[0m :"

    echo -en "\033[0m\n\033[0m     : "
    for f in $(seq 0 7); do
      echo -en "\033[${bg}m\033[1;$(($f+30))m ${FGNAMES[$f]} "
    done
    echo -en "\033[0m :"
        echo -e "\033[0m"

  if [ "$b" -lt 8 ]; then
    echo "     ----------------------------------------------------------------------------"
  fi
done
echo "     ----------------------------------------------------------------------------"
```

### Script #4

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
	io.write('\n    ')
	print_fg(bg, '1;')
	io.write('\n\n')
end

-- Andres P
```

### Script #5

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

### Script #6

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

### Script #7

```
#!/bin/sh
# Original Posted at [http://crunchbang.org/forums/viewtopic.php?pid=126921%23p126921#p126921](http://crunchbang.org/forums/viewtopic.php?pid=126921%23p126921#p126921)
# [ESC] character in original post removed here.

# ANSI Color -- use these variables to easily have different color
#    and format output. Make sure to output the reset sequence after
#    colors (f = foreground, b = background), and use the 'off'
#    feature for anything you turn on.

initializeANSI()
{
 esc="$(echo -en '\e')"

  blackf="${esc}[30m";   redf="${esc}[31m";    greenf="${esc}[32m"
  yellowf="${esc}[33m"   bluef="${esc}[34m";   purplef="${esc}[35m"
  cyanf="${esc}[36m";    whitef="${esc}[37m"

  blackb="${esc}[40m";   redb="${esc}[41m";    greenb="${esc}[42m"
  yellowb="${esc}[43m"   blueb="${esc}[44m";   purpleb="${esc}[45m"
  cyanb="${esc}[46m";    whiteb="${esc}[47m"

  boldon="${esc}[1m";    boldoff="${esc}[22m"
  italicson="${esc}[3m"; italicsoff="${esc}[23m"
  ulon="${esc}[4m";      uloff="${esc}[24m"
  invon="${esc}[7m";     invoff="${esc}[27m"

  reset="${esc}[0m"
}

# note in this first use that switching colors doesn't require a reset
# first - the new color overrides the old one.

#clear

initializeANSI

cat << EOF

 ${yellowf}  ▄███████▄${reset}   ${redf}  ▄██████▄${reset}    ${greenf}  ▄██████▄${reset}    ${bluef}  ▄██████▄${reset}    ${purplef}  ▄██████▄${reset}    ${cyanf}  ▄██████▄${reset}
 ${yellowf}▄█████████▀▀${reset}  ${redf}▄${whitef}█▀█${redf}██${whitef}█▀█${redf}██▄${reset}  ${greenf}▄${whitef}█▀█${greenf}██${whitef}█▀█${greenf}██▄${reset}  ${bluef}▄${whitef}█▀█${bluef}██${whitef}█▀█${bluef}██▄${reset}  ${purplef}▄${whitef}█▀█${purplef}██${whitef}█▀█${purplef}██▄${reset}  ${cyanf}▄${whitef}█▀█${cyanf}██${whitef}█▀█${cyanf}██▄${reset}
 ${yellowf}███████▀${reset}      ${redf}█${whitef}▄▄█${redf}██${whitef}▄▄█${redf}███${reset}  ${greenf}█${whitef}▄▄█${greenf}██${whitef}▄▄█${greenf}███${reset}  ${bluef}█${whitef}▄▄█${bluef}██${whitef}▄▄█${bluef}███${reset}  ${purplef}█${whitef}▄▄█${purplef}██${whitef}▄▄█${purplef}███${reset}  ${cyanf}█${whitef}▄▄█${cyanf}██${whitef}▄▄█${cyanf}███${reset}
 ${yellowf}███████▄${reset}      ${redf}████████████${reset}  ${greenf}████████████${reset}  ${bluef}████████████${reset}  ${purplef}████████████${reset}  ${cyanf}████████████${reset}
 ${yellowf}▀█████████▄▄${reset}  ${redf}██▀██▀▀██▀██${reset}  ${greenf}██▀██▀▀██▀██${reset}  ${bluef}██▀██▀▀██▀██${reset}  ${purplef}██▀██▀▀██▀██${reset}  ${cyanf}██▀██▀▀██▀██${reset}
 ${yellowf}  ▀███████▀${reset}   ${redf}▀   ▀  ▀   ▀${reset}  ${greenf}▀   ▀  ▀   ▀${reset}  ${bluef}▀   ▀  ▀   ▀${reset}  ${purplef}▀   ▀  ▀   ▀${reset}  ${cyanf}▀   ▀  ▀   ▀${reset}

 ${boldon}${yellowf}  ▄███████▄   ${redf}  ▄██████▄    ${greenf}  ▄██████▄    ${bluef}  ▄██████▄    ${purplef}  ▄██████▄    ${cyanf}  ▄██████▄${reset}
 ${boldon}${yellowf}▄█████████▀▀  ${redf}▄${whitef}█▀█${redf}██${whitef}█▀█${redf}██▄  ${greenf}▄${whitef}█▀█${greenf}██${whitef}█▀█${greenf}██▄  ${bluef}▄${whitef}█▀█${bluef}██${whitef}█▀█${bluef}██▄  ${purplef}▄${whitef}█▀█${purplef}██${whitef}█▀█${purplef}██▄  ${cyanf}▄${whitef}█▀█${cyanf}██${whitef}█▀█${cyanf}██▄${reset}
 ${boldon}${yellowf}███████▀      ${redf}█${whitef}▄▄█${redf}██${whitef}▄▄█${redf}███  ${greenf}█${whitef}▄▄█${greenf}██${whitef}▄▄█${greenf}███  ${bluef}█${whitef}▄▄█${bluef}██${whitef}▄▄█${bluef}███  ${purplef}█${whitef}▄▄█${purplef}██${whitef}▄▄█${purplef}███  ${cyanf}█${whitef}▄▄█${cyanf}██${whitef}▄▄█${cyanf}███${reset}
 ${boldon}${yellowf}███████▄      ${redf}████████████  ${greenf}████████████  ${bluef}████████████  ${purplef}████████████  ${cyanf}████████████${reset}
 ${boldon}${yellowf}▀█████████▄▄  ${redf}██▀██▀▀██▀██  ${greenf}██▀██▀▀██▀██  ${bluef}██▀██▀▀██▀██  ${purplef}██▀██▀▀██▀██  ${cyanf}██▀██▀▀██▀██${reset}
 ${boldon}${yellowf}  ▀███████▀   ${redf}▀   ▀  ▀   ▀  ${greenf}▀   ▀  ▀   ▀  ${bluef}▀   ▀  ▀   ▀  ${purplef}▀   ▀  ▀   ▀  ${cyanf}▀   ▀  ▀   ▀${reset}

EOF
```

## Contributed examples

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Dotfiles](/index.php/Dotfiles "Dotfiles").**

**Notes:** Undocumented and setup-specific files are of little relevance in a general article (Discuss in [Talk:X resources#](https://wiki.archlinux.org/index.php/Talk:X_resources))

Check out these links for some real world examples of X resource files, contributed by fellow community members.

**Note:** `~/.Xdefaults` has the same syntax as `~/.Xresources`, and it is recommended that you use `~/.Xresources` because `~/.Xdefaults` is deprecated upstream.

*   [http://dotfiles.org/~buttons/.Xdefaults](http://dotfiles.org/~buttons/.Xdefaults)
*   [https://github.com/jelly/Dotfiles/blob/master/.Xdefaults](https://github.com/jelly/Dotfiles/blob/master/.Xdefaults)
*   [https://paste.debian.net/14515/](https://paste.debian.net/14515/) .Xresources

## Troubleshooting

### Parsing errors

[Display managers](/index.php/Display_manager "Display manager") such as [GDM](/index.php/GDM "GDM") and [LightDM](/index.php/LightDM "LightDM") may use the `--nocpp` argument for _xrdb_. See [LightDM#Xresources not being parsed correctly](/index.php/LightDM#Xresources_not_being_parsed_correctly "LightDM").

## See also

*   [Using the Xdefaults File](https://engineering.purdue.edu/ECN/Support/KB/Docs/UsingTheXdefaultsFil) - An in-depth article on how X interprets the Xdefaults file
*   [Rxvt-unicode Configuration Tutorial](http://wiki.afterstep.org/index.php?title=Rxvt-Unicode_Configuration_Tutorial) - lots of information for urxvt users
*   [Example Colors and their names](http://mkaz.com/solog/system/xterm-colors.html) - listing of example colors and their color names for xterm and other X-applications.
*   [Color Themes](https://web.archive.org/web/20090130061234/http://phraktured.net/terminal-colors/) - Extensive list of terminal color themes by Phraktured.
*   [Xcolors.net](http://xcolors.net/) List of user-contributed terminal color themes.
*   [Xcolors by dkeg](http://beta.andrewrcraig.us/index.php?page=xcolors)

Retrieved from "[https://wiki.archlinux.org/index.php?title=X_resources&oldid=403404](https://wiki.archlinux.org/index.php?title=X_resources&oldid=403404)"