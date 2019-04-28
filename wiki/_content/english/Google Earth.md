From the [project web page](http://support.google.com/earth/bin/answer.py?hl=en&answer=176145):

	Google Earth allows you to travel the world through a virtual globe and view satellite imagery, maps, terrain, 3D buildings, and much more. With Google Earth's rich, geographical content, you are able to experience a more realistic view of the world. You can fly to your favorite place, search for businesses and even navigate through directions.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Crash on startup](#Crash_on_startup)
        *   [2.1.1 Startup tips are enabled](#Startup_tips_are_enabled)
        *   [2.1.2 No new line at the end of ~/.drirc](#No_new_line_at_the_end_of_~/.drirc)
        *   [2.1.3 Corrupt settings](#Corrupt_settings)
        *   [2.1.4 Another crash happened while handling crash!](#Another_crash_happened_while_handling_crash!)
    *   [2.2 Panoramio photos not working](#Panoramio_photos_not_working)
    *   [2.3 Graphical corruption](#Graphical_corruption)
    *   [2.4 Earth shows nothing but yellow borders](#Earth_shows_nothing_but_yellow_borders)
    *   [2.5 Excessive memory use](#Excessive_memory_use)

## Installation

As all versions depend on a 32-bit library, enable the [multilib](/index.php/Multilib "Multilib") repository first.

There are multiple Google Earth versions available in the [AUR](/index.php/AUR "AUR"):

*   [google-earth-pro](https://aur.archlinux.org/packages/google-earth-pro/) - Latest version (still freeware)
*   [google-earth](https://aur.archlinux.org/packages/google-earth/) - Semi-legacy version

## Troubleshooting

**Tip:** See the [official support forum](https://productforums.google.com/forum/#!categories/earth/linux) for topics not covered here.

### Crash on startup

Google Earth can crash on startup for numerous reasons. Here are some of the most common ones.

#### Startup tips are enabled

While startup tips can be useful, they are also known to cause crashes. To disable them, change or add the line below to the appropriate configuration file for your version.

Google Earth `~/.config/Google/GoogleEarthPlus.conf`

Google Earth Pro `~/.config/Google/GoogleEarthPro.conf`

```
[General]
enableTips=false

```

#### No new line at the end of `~/.drirc`

This can cause a crash with *-dri* drivers:

```
$ echo >> ~/.drirc

```

#### Corrupt settings

In case the cache is corrupt and needs recreation, remove it:

```
$ rm -r ~/.googleearth/Cache/

```

If that didn't work, try removing the whole settings folder:

```
$ rm -r ~/.googleearth/

```

#### Another crash happened while handling crash!

You may try removing the following:

```
$ rm -f ~/.googleearth/Cache/cookies ~/.googleearth/instance-running-lock

```

### Panoramio photos not working

There have been numerous reports [[1]](http://productforums.google.com/d/msg/earth/548PQIT8bKI/rbpVsbMawwIJ) [[2]](http://productforums.google.com/forum/#!msg/earth/_h4t6SpY_II/6O_DTry49pgJ) [[3]](http://productforums.google.com/d/msg/earth/tZfKSs2AaZc/r_rBDl5djIMJ) on this in the [Google Earth forums](https://productforums.google.com/forum/#!categories/earth/linux) with varying solutions.

### Graphical corruption

Either refer to the [#Corrupt settings](#Corrupt_settings) section above or disable texture compression in *Tools > Options... > 3D View > Compress*.

### Earth shows nothing but yellow borders

Taken from the changelog of [7.0.3](https://support.google.com/earth/bin/answer.py?hl=en&answer=40901) this issue has improved to some extent but overall it's still there:

```
Imagery now displays for Linux users running specific families of Intel GPUs.

```

### Excessive memory use

Memory use can be controlled by limiting the maximum cache size in *Tools > Options... > Cache*, or by lowering the graphics settings in the *3D View* tab.