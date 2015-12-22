# Dzen

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** The current official package works with Xft but not X Logical Font Description (Discuss in [Talk:Dzen#](https://wiki.archlinux.org/index.php/Talk:Dzen))

[Dzen](http://robm.github.com/dzen/) is "a general purpose messaging, notification and menuing program for X11\. It was designed to be scriptable in any language and integrate well with window managers like [dwm](/index.php/Dwm "Dwm"), [wmii](/index.php/Wmii "Wmii") and [xmonad](/index.php/Xmonad "Xmonad") though it will work with any window manager."

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Using custom fonts with dzen](#Using_custom_fonts_with_dzen)
    *   [3.2 Dzen and Conky](#Dzen_and_Conky)
    *   [3.3 Clickable areas and popups](#Clickable_areas_and_popups)
    *   [3.4 Enabling Xft support for dzen](#Enabling_Xft_support_for_dzen)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dzen2](https://www.archlinux.org/packages/?name=dzen2) package which is available in the [official repositories](/index.php/Official_repositories "Official repositories") which includes Xft, XPM, and Xinerama support.

**Note:** Xft doesn't seem to work with the official package. Alternatively, you can install the [dzen2-xft-xpm-xinerama-git](https://aur.archlinux.org/packages/dzen2-xft-xpm-xinerama-git/)<sup><small>AUR</small></sup> package located in the [AUR](/index.php/AUR "AUR") with Xft, XPM and Xinerama support.

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

[Conky](/index.php/Conky "Conky") can be used to pipe information directly to dzen for output in a status bar. This can be done with Conky in the official repositories and also with [conky-cli](https://aur.archlinux.org/packages/conky-cli/)<sup><small>AUR</small></sup>, a stripped-down version of the Conky status utility from the [AUR](/index.php/AUR "AUR").

The following example displays the average load values in red and the current time in the default dzen foreground colour:

 `~/.conkyrc` 

```
 background no
 out_to_console yes
 out_to_x no
 update_interval 1.0
 total_run_times 0
 use_spacer none

 TEXT
 ^fg(\#ff0000)${loadavg 1 2 3} ^fg()${time %a %b %d %I:%M%P}

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

dzen2 allows you to define clickable areas using `^ca(_button_, _command_)Text^ca()`. You can use this property to create popups giving arbitrary information, as seen in various screenshot gifs like [this](http://i.minus.com/ibzmjKMXKk7IbH.gif).

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
`^ca(1,_<path to your script>_)Sysinfo^ca()`

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

## See also

*   [Official website](http://robm.github.com/dzen/), [wiki](https://github.com/robm/dzen/wiki/_pages), and [source](https://github.com/robm/dzen)

**Forum threads**

*   2007-12-04 - Arch Linux - [dzen & xmobar Hacking Thread](https://bbs.archlinux.org/viewtopic.php?id=40637)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dzen&oldid=413083](https://wiki.archlinux.org/index.php?title=Dzen&oldid=413083)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Application launchers](/index.php/Category:Application_launchers "Category:Application launchers")
*   [Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")
*   [Status monitoring and notification](/index.php/Category:Status_monitoring_and_notification "Category:Status monitoring and notification")