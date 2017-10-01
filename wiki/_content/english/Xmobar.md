[xmobar](https://github.com/jaor/xmobar) is a lightweight, text-based, status bar written in [Haskell](https://en.wikipedia.org/wiki/Haskell_(programming_language) "wikipedia:Haskell (programming language)"). It was originally designed to be used together with [Xmonad](/index.php/Xmonad "Xmonad"), but it is also usable with any other [window manager](/index.php/Window_manager "Window manager"). While *xmobar* is written in Haskell, no knowledge of the language is required to install and use it.

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 GMail integration](#GMail_integration)
    *   [4.2 MPD integration](#MPD_integration)
    *   [4.3 Conky-Cli integration](#Conky-Cli_integration)
    *   [4.4 Simple conky-cli integration](#Simple_conky-cli_integration)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [xmobar](https://www.archlinux.org/packages/?name=xmobar) from the [official repositories](/index.php/Official_repositories "Official repositories"). Available variants are:

*   [xmobar-git](https://aur.archlinux.org/packages/xmobar-git/) — development version.
*   *xmobar* from the unofficial [haskell-core](/index.php/ArchHaskell#haskell-core "ArchHaskell") repository — supports wireless and volume plugin with no additional configuration required; the repository also contains all the required dependencies.

## Running

If the configuration file is saved as `~/.xmobarrc`:

```
$ xmobar &

```

Alternatively, the path to a configuration file can be specified:

```
$ xmobar /path/to/config &

```

The following is an example of how to configure xmobar using command line options:

```
$ xmobar -B white -a right -F blue -t '%LIPB%' -c '[Run Weather "LIPB" [] 36000]' &

```

This will run *xmobar* right-aligned, with white background and blue text, using the `Weather` plugin. Note that the output template must contain at least one command. Read the following section for further explanation of options.

## Configuration

The configuration for *xmobar* is normally defined in `~/.xmobarrc` or by specifying a set of command line options when launching *xmobar*. Any given command line option will override the corresponding option in the configuration file. This can be useful to test new configurations without having to edit a configuration file.

Following is an example `~/.xmobarrc` file, followed by a description of each option. Note that each option has a corresponding command line option.

**Note**: The configuration file is (a subset of) Haskell source code, so '`--`' starts a single-line comment.

```
Config { 

   -- appearance
     font =         "xft:Bitstream Vera Sans Mono:size=9:bold:antialias=true"
   , bgColor =      "black"
   , fgColor =      "#646464"
   , position =     Top
   , border =       BottomB
   , borderColor =  "#646464"

   -- layout
   , sepChar =  "%"   -- delineator between plugin names and straight text
   , alignSep = "}{"  -- separator between left-right alignment
   , template = "%battery% | %multicpu% | %coretemp% | %memory% | %dynnetwork% }{ %RJTT% | %date% || %kbd% "

   -- general behavior
   , lowerOnStart =     True    -- send to bottom of window stack on start
   , hideOnStart =      False   -- start with window unmapped (hidden)
   , allDesktops =      True    -- show on all desktops
   , overrideRedirect = True    -- set the Override Redirect flag (Xlib)
   , pickBroadest =     False   -- choose widest display (multi-monitor)
   , persistent =       True    -- enable/disable hiding (True = disabled)

   -- plugins
   --   Numbers can be automatically colored according to their value. xmobar
   --   decides color based on a three-tier/two-cutoff system, controlled by
   --   command options:
   --     --Low sets the low cutoff
   --     --High sets the high cutoff
   --
   --     --low sets the color below --Low cutoff
   --     --normal sets the color between --Low and --High cutoffs
   --     --High sets the color above --High cutoff
   --
   --   The --template option controls how the plugin is displayed. Text
   --   color can be set by enclosing in <fc></fc> tags. For more details
   --   see http://projects.haskell.org/xmobar/#system-monitor-plugins.
   , commands = 

        -- weather monitor
        [ Run Weather "RJTT" [ "--template", "<skyCondition> | <fc=#4682B4><tempC></fc>°C | <fc=#4682B4><rh></fc>% | <fc=#4682B4><pressure></fc>hPa"
                             ] 36000

        -- network activity monitor (dynamic interface resolution)
        , Run DynNetwork     [ "--template" , "<dev>: <tx>kB/s|<rx>kB/s"
                             , "--Low"      , "1000"       -- units: B/s
                             , "--High"     , "5000"       -- units: B/s
                             , "--low"      , "darkgreen"
                             , "--normal"   , "darkorange"
                             , "--high"     , "darkred"
                             ] 10

        -- cpu activity monitor
        , Run MultiCpu       [ "--template" , "Cpu: <total0>%|<total1>%"
                             , "--Low"      , "50"         -- units: %
                             , "--High"     , "85"         -- units: %
                             , "--low"      , "darkgreen"
                             , "--normal"   , "darkorange"
                             , "--high"     , "darkred"
                             ] 10

        -- cpu core temperature monitor
        , Run CoreTemp       [ "--template" , "Temp: <core0>°C|<core1>°C"
                             , "--Low"      , "70"        -- units: °C
                             , "--High"     , "80"        -- units: °C
                             , "--low"      , "darkgreen"
                             , "--normal"   , "darkorange"
                             , "--high"     , "darkred"
                             ] 50

        -- memory usage monitor
        , Run Memory         [ "--template" ,"Mem: <usedratio>%"
                             , "--Low"      , "20"        -- units: %
                             , "--High"     , "90"        -- units: %
                             , "--low"      , "darkgreen"
                             , "--normal"   , "darkorange"
                             , "--high"     , "darkred"
                             ] 10

        -- battery monitor
        , Run Battery        [ "--template" , "Batt: <acstatus>"
                             , "--Low"      , "10"        -- units: %
                             , "--High"     , "80"        -- units: %
                             , "--low"      , "darkred"
                             , "--normal"   , "darkorange"
                             , "--high"     , "darkgreen"

                             , "--" -- battery specific options
                                       -- discharging status
                                       , "-o"	, "<left>% (<timeleft>)"
                                       -- AC "on" status
                                       , "-O"	, "<fc=#dAA520>Charging</fc>"
                                       -- charged status
                                       , "-i"	, "<fc=#006000>Charged</fc>"
                             ] 50

        -- time and date indicator 
        --   (%F = y-m-d date, %a = day of week, %T = h:m:s time)
        , Run Date           "<fc=#ABABAB>%F (%a) %T</fc>" "date" 10

        -- keyboard layout indicator
        , Run Kbd            [ ("us(dvorak)" , "<fc=#00008B>DV</fc>")
                             , ("us"         , "<fc=#8B0000>US</fc>")
                             ]
        ]
   }

```

*   **font** - The name of the font to use. If XFT fonts are enabled, prefix XFT font names with "`xft:`".

Example:

```
font = "xft:Bitstream Vera Sans Mono:size=8:antialias=true"

```

*   **fgColor** - The colour of the font, takes both colour names like `black` and hex colours like `#000000`.
*   **bgColor** - The colour of the bar, takes both colour names like `red` and hex colours like `#ff0000`.
*   **position** - The position of the bar. Keywords are: `Top`/`Bottom`, `TopW`/`BottomW` and `Static`.
    *   `Top`/`Bottom` - The top/bottom of the screen.
    *   `TopW`/`BottomW` - The top/bottom of the screen with a fixed width. TopW/BottomW takes 2 arguments:
        *   Alignment: `L`eft, `C`enter or `R`ight aligned.
        *   Width: An integer for the width of the bar in percentage.
    *   `Static` - A fixed position on the screen, with a fixed width. Static takes 4 arguments:
        *   xpos: Horisontal position in pixels, starting at the upper left corner.
        *   ypos: Vertical position in pixels, starting at the upper left corner.
        *   width: The width of the bar in pixels.
        *   height: The height of the bar in pixels.

Example - centered at the bottom of the screen, with a width of 75% of the screen:

```
position = BottomW C 75

```

Example - top left of the screen, with a width of 1024 pixels and height of 15 pixels:

```
position = Static { xpos = 0 , ypos = 0, width = 1024, height = 15 }

```

*   **border** - The position and appearance of a border. Keywords are: `TopB, TopBM, BottomB, BottomBM, FullB, FullBM` and `NoBorder (default)`
    *   `TopB`/`BottomB` - The top/bottom of the bar
    *   `FullB` - The entire perimeter of the bar
    *   `TopBM`/`BottomBM`/`FullBM` - Same as other options, except you can specify how many pixels off the bar's edge the border should be drawn. Each option takes a single integer argument.

Example - border placed 3 pixels off bottom edge of the bar:

```
border: BottomBM 3

```

*   **sepChar** - The character to be used for indicating commands in the output template. Default character is `"%"`.
*   **alignSep** - A string of characters for aligning text in the output template. The text before the first character will be left aligned, the text between them will be centered, and the text to the right of the last character will be right aligned. Default string is `"}{"`.
*   **template** - The output template is a string containing the text and commands that will be displayed. It contains the alias for a `%command%`, written text and color tags that sets the colour of text.

Example:

```
template = "%StdinReader%}{%cpu% %memory% <fc=#ffaaff>battery:</fc> %battery% %date%"

```

*   **commands** For setting the options of the programs to run. Commands is a comma seperated list of commands, optionally specified with options.

Example - runs the `Memory` plugin, with the specified template and the `Swap` plugin, with default args. Both updates every second:

```
commands = [Run Memory ["-t","Mem: <usedratio>%"] 10, Run Swap [] 10]

```

And finally some options which control the bar's general behavior---each is set to a single `True` or `False` value:

*   **lowerOnStart** - Controls whether to keep the bar behind all other windows.
*   **hideOnStart** - Controls whether to hide the bar on start.
*   **allDesktops** - Controls whether to show the bar on all desktops.
*   **overrideRedirect** - An option necessary for some window managers to prevent the bar from being treated like a normal window.
*   **pickBroadest** - On multi-monitor setups place the bar on the widest monitor instead of the first.
*   **persistent** - Controls whether to always be visible or not, regardless of the bar's 'hidden' state.

## Tips and tricks

There are various plugins that can be used with *xmobar* - to name a few, there are plugins for disk usage, ram, cpu, battery status, weather report and network activity. A detailed description of each plugin, its dependencies and how to configure it is on the project [website](http://projects.haskell.org/xmobar/#system-monitor-plugins).

### GMail integration

Assuming you have either *xmobar-gmail-darcs* or *xmobar-gmail* installed, you can configure `.xmobarrc` as follows. Add the GMail plugin to the commands list:

```
, Run GMail "gmail.username" "GmailPassword" ["-t", "Mail: <count>"] 3000

```

Then add the command to the template

```
, template = "... **%gmail.username%** ..."

```

### [MPD](/index.php/MPD "MPD") integration

Assuming you have [xmobar-git](https://aur.archlinux.org/packages/xmobar-git/) installed (with [haskell-libmpd](https://www.archlinux.org/packages/?name=haskell-libmpd)), there is a plugin to pull information to display on the status bar about the currently playing song. To add a simple plugin displaying the artist and song of the current track, add this line to your commands list in your `~/.xmobarrc`:

```
, Run MPD ["-t", "<state>: <artist> - <track>"] 10

```

Finally, you will need to place the plugin some place in your template, as follows:

```
, template = "%StdinReader% }{ ... **%mpd%** ..."

```

### Conky-Cli integration

It is possible to utilize the features of [conky-cli](https://aur.archlinux.org/packages/conky-cli/) such as disk space, top and system messages, by piping the information from conky into a text file and read the contents from it. Following is a bash script to use with xmobar for this purpose.

 `~/.xmonad/conkyscript` 
```
#!/bin/bash
conky -c ~/.conkyclirc -i1 -q > conkystat &
sleep 4
killall -q conky
cat conkystat
rm conkystat

```

Add the following line to the commands section in `~/.xmobarrc`.

```
, Run Com ".xmonad/conkyscript" ["&"] "conky" 300

```

This makes the script run every 30 seconds.

Then add the following to your `.xinitrc` before the `exec xmonad` entry.

```
.xmonad/conkyscript &
sleep 6 && xmobar &

```

Then add `%conky%` to your template section.

### Simple conky-cli integration

Just place this code:

```
Run Com "conky" ["-q", "-i", "1"] "conky" 600

```

in your `.xmobarrc`.

## See also

*   [xmobar hackage](http://hackage.haskell.org/package/xmobar)
*   [xmobar project](http://projects.haskell.org/xmobar/)
*   [dzen and xmobar hacking thread](https://bbs.archlinux.org/viewtopic.php?pid=304851)