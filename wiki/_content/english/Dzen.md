[Dzen](http://robm.github.com/dzen/) is "a general purpose messaging, notification and menuing program for X11\. It was designed to be scriptable in any language and integrate well with window managers like [dwm](/index.php/Dwm "Dwm"), [wmii](/index.php/Wmii "Wmii") and [xmonad](/index.php/Xmonad "Xmonad") though it will work with any window manager."

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Using custom fonts with dzen](#Using_custom_fonts_with_dzen)
    *   [3.2 Dzen and Conky](#Dzen_and_Conky)
    *   [3.3 Clickable areas and popups](#Clickable_areas_and_popups)
    *   [3.4 Enabling Xft support for dzen](#Enabling_Xft_support_for_dzen)
    *   [3.5 Gadgets](#Gadgets)
        *   [3.5.1 dbar](#dbar)
        *   [3.5.2 gdbar](#gdbar)
        *   [3.5.3 Others](#Others)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dzen2](https://www.archlinux.org/packages/?name=dzen2) package which is available in the [official repositories](/index.php/Official_repositories "Official repositories") which includes Xft, XPM, and Xinerama support.

## Configuration

Dzen is able to read font and color settings from [X resources](/index.php/X_resources "X resources"). As an example, you can add following lines to `~/.Xresources`:

```
dzen2.font:       -*-fixed-*-*-*-*-*-*-*-*-*-*-*-*
dzen2.foreground: #22EE11
dzen2.background: black

```

## Tips and tricks

### Using custom fonts with dzen

Dzen follows the [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description") so it will only find fonts in the X font path. See [Fonts#Older applications](/index.php/Fonts#Older_applications "Fonts") for details.

### Dzen and Conky

[Conky](/index.php/Conky "Conky") can be used to pipe information directly to dzen for output in a status bar. This can be done with Conky in the official repositories and also with [conky-cli](https://aur.archlinux.org/packages/conky-cli/), a stripped-down version of the Conky status utility from the [AUR](/index.php/AUR "AUR").

The following example displays the average load values in red and the current time in the default dzen foreground colour:

 `~/.conkyrc` 
```
conky.config = {
      background = false
    , out_to_console = true
    , out_to_x = false
    , update_interval = 1.0
    , total_run_times = 0
    , use_spacer = none
}

conky.text = [[^fg(\#ff0000)${loadavg 1 2 3} ^fg()${time %a %b %d %I:%M%P}]]

```
 `~/bin/dzconky` 
```
 #!/bin/sh

 FG='#aaaaaa'
 BG='#1a1a1a'
 FONT='-*-terminus-*-r-normal-*-*-120-*-*-*-*-iso8859-*'
 conky | dzen2 -e - -h '16' -w '600' -ta r -fg $FG -bg $BG -fn $FONT &

```

Simply execute `dzconky` in your startup scripts.

### Clickable areas and popups

dzen2 allows you to define clickable areas using `^ca(*button*, *command*)Text^ca()`. You can use this property to create popups giving arbitrary information, as seen in various screenshot gifs like [this](http://i.imgur.com/bZegioR.gif).

A simple example can be:

 `sysinfo_popup.sh` 
```
 #/bin/bash

 #A simple popup showing system information

 HOST=$(uname -n)
 KERNEL=$(uname -r)
 UPTIME=$( uptime | sed 's/.* up //' | sed 's/[0-9]* us.*//' | sed 's/ day, /d /'\
          | sed 's/ days, /d /' | sed 's/:/h /' | sed 's/ min//'\
            |  sed 's/,/m/' | sed 's/  / /')
 PACKAGES=$(pacman -Q | wc -l)
 UPDATED=$(awk '/upgraded/ {line=$0;} END { $0=line; gsub(/[\[\]]/,"",$0); \
          printf "%s %s",$1,$2;}' /var/log/pacman.log)

 (
 echo "System Information" # Fist line goes to title
 # The following lines go to slave window
 echo "Host: $HOST "
 echo "Kernel: $KERNEL"
 echo "Uptime: $UPTIME "
 echo "Pacman: $PACKAGES packages"
 echo "Last updated on: $UPDATED"
 ) | dzen2 -p -x "500" -y "30" -w "220" -l "5" -sa 'l' -ta 'c'\
    -title-name 'popup_sysinfo' -e 'onstart=uncollapse;button1=exit;button3=exit'

 # "onstart=uncollapse" ensures that slave window is visible from start.

```

Save this script and make it executable and then use the `^ca()` attribute in your conkyrc (or the script that you pipe to dzen2) to trigger it.

```
`^ca(1,*<path to your script>*)Sysinfo^ca()`

```

This will bind the script to mouse button 1 and execute it when it is clicked over the text.

### Enabling Xft support for dzen

**Note:** You need to install the [libxft](https://www.archlinux.org/packages/?name=libxft) package.

As of SVN revision 241 (development), dzen2 has optional support for Xft. To enable Xft support, build dzen2 with these options by editing `config.mk`:

 `config.mk` 
```
 ## Option: With Xinerama and XPM and XFT
 LIBS = -L/usr/lib -lc -L${X11LIB} -lX11 -lXinerama -lXpm $(pkg-config --libs xft)
 CFLAGS = -Wall -Os ${INCS} -DVERSION=\"${VERSION}\" -DDZEN_XINERAMA -DDZEN_XPM -DDZEN_XFT $(pkg-config --cflags xft)

```

To check libxft support, you can use this command:

```
echo "hello world" | dzen2 -fn 'Times New Roman' -p

```

### Gadgets

There are some gadgets on dzen that may be used to make a good customize. Follow below some of they with a brief explanation and examples.

#### dbar

Dbar receive a pipe from another command with any number and outputs a semi-graphical progress bar with it, by default the max number of *100%* is "100". The maximum and minimum values can be changed with `-max`/`-min` respectively.

Output example:

```
50% [=============            ]

```

Code example:

 `~/test` 
```
#!/bin/sh

(
amixer get Master | \
awk '/Left:/{gsub(/[[:punct:]]/,"",$5);left=$5}
     /Right:/{gsub(/[[:punct:]]/,"",$5);right=$5}
     END {print left ORS right}'
) | dbar -max 100 -min 0 -s '|' -l 'Vol'

```

See [README.dbar](https://github.com/robm/dzen/blob/master/gadgets/README.dbar) for details.

#### gdbar

Gdbar as well as [dbar](#dbar) outputs a progress bar based on a value of *100%*, but here it is full-graphical. Gdbar have the same options of dbar with some additional options. Some of the options are:

*   *-fg* set the foreground.
*   *-bg* set the background.
*   *-w*/*-h* set the width and height respectively.

Code example:

 `~/test` 
```
#!/bin/sh

(
amixer get Master | \
awk '/Left:/{gsub(/[[:punct:]]/,"",$5);left=$5}
     /Right:/{gsub(/[[:punct:]]/,"",$5);right=$5}
     END{print left ORS right}'
) | gdbar -max 100 -min 0 -l 'Vol ' -bg '#777777' -fg '#00ff00' -ss '2' | dzen2 -p -l '1' -w '150' -y '100' -x '100' -ta c -sa c -e 'onstartup=uncollapse;button3=exit'

```

See [README.gdbar](https://github.com/robm/dzen/blob/master/gadgets/README.gdbar) for details.

**Note:** Gdbar will only be useful in combination with dzen >= 0.7.0.

#### Others

Information about others gadgets can be found [here](https://github.com/robm/dzen/tree/master/gadgets).

## See also

*   [Official website](http://robm.github.com/dzen/), [wiki](https://github.com/robm/dzen/wiki/_pages), and [source](https://github.com/robm/dzen)

**Forum threads**

*   2007-12-04 - Arch Linux - [dzen & xmobar Hacking Thread](https://bbs.archlinux.org/viewtopic.php?id=40637)