# Guitar Pro

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Guitar Pro is great to transcribe and compose for stringed instruments, organized in terms of tablature notation correctness and ease of use. One use of using Guitar Pro is to create backing tracks and export them to MIDI, then use those as a backing tracks to practice with on an instrument.

This article covers how to start using the outdated Guitar Pro 5.2 with Linux. Native binaries do not exist for Guitar Pro 5, opposed to the case of Guitar Pro 6, so this requires [Wine](/index.php/Wine "Wine") running the windows version and [Timidity](/index.php/Timidity "Timidity") as a MIDI backend.

**Tip:** If you want to use Guitar Pro 6, as it runs natively in Linux, you can use the [guitar-pro](https://aur.archlinux.org/packages/guitar-pro/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR") instead. Guitar Pro 6 can also use timidity instead of RSE, so this guide maybe still be useful to Guitar Pro 6 users as well.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 MIDI doesn't play](#MIDI_doesn.27t_play)
    *   [3.2 Missing note heads and other symbols](#Missing_note_heads_and_other_symbols)
*   [4 See also](#See_also)

## Installation

As a prerequisite, you need [Wine](/index.php/Wine "Wine") and [Timidity](/index.php/Timidity "Timidity") installed. Consult respective wikis on how to install them.

The directory _~/wine_ is suggested for Wine installations. After downloading Guitar Pro installer (either [demo versions](http://www.guitar-pro.com/en/index.php?pg=download) or [full versions](http://www.guitar-pro.com/en/index.php?pg=support-customers-area)), cd to the download folder and run these commands:

```
$ WINEPREFIX="$HOME/wine/guitar_pro_5"
$ mkdir $WINEPREFIX
$ wine GP5FULL.exe

```

What happens is a similar to standard Windows install procedure that leaves you with $WINEPREFIX dirctory occupied with installed Guitar Pro ready to be configured/used.

## Configuration

Configuration of Timidity is covered in it's wiki. Once it's running, run Guitar Pro. You can use a little convenience script to launch Guitar Pro from command line/prompt box if you do not want to use Timidity as a daemon:

 `~/bin/GP5.EXE` 

```
#!/bin/bash
# script GP5.EXE
# author: dante4d <dante4d@gmail.com>

timidity -iA &
PID=$!
sleep 1
WINEPREFIX="$HOME/wine/guitar_pro_5" wine "C:\\Program Files\\Guitar Pro 5\\GP5.EXE"
sleep 1
kill $PID

```

First, you need to setup Guitar Pro to use right MIDI output device. In menu, go to **Options->Audio Settings (MIDI/RSE)...** . On top of the dialog, select Timidity as an output device for port 1 as it should suffice.

You may also want to turn off the splash screen and the intro jingle under menu **Options->Preferences** (F12).

## Troubleshooting

### MIDI doesn't play

Check Timidity settings in _/etc/timidity++/timidity.cfg_. You may have this issue if you forget to include soundpatches there :).

### Missing note heads and other symbols

Sometimes you will see just whitespaces instead of note heads and some other symbols. One of the solutions is to link font files from Guitar Pro directory in Wine folders to _/usr/shared/fonts/TTF_ or _~/.fonts_. For more info, check [Guitar Pro 5.x at WineHQ](http://appdb.winehq.org/objectManager.php?sClass=version&iId=3782) or use [Google](http://www.google.com/).

## See also

*   Guitar Pro Home - [http://www.guitar-pro.com/](http://www.guitar-pro.com/)
*   Guitar Pro 5.x at WineHQ - [http://appdb.winehq.org/objectManager.php?sClass=version&iId=3782](http://appdb.winehq.org/objectManager.php?sClass=version&iId=3782)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Guitar_Pro&oldid=389800](https://wiki.archlinux.org/index.php?title=Guitar_Pro&oldid=389800)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia](/index.php/Category:Multimedia "Category:Multimedia")
*   [Wine](/index.php/Category:Wine "Category:Wine")