# ThinkPad OSD

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

New desktop environments ([GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), and maybe even [Xfce](/index.php/Xfce "Xfce")) support their own osd notifications for important events (volume up/down/mute and brightness up/down), which might be enough for most users. In order to use those notifications instead of the ones provided by TPB, map the keyboard-events of those keys to the proper keycodes.

## Contents

*   [1 Loading nvram at boot and give permission to access /dev/nvram](#Loading_nvram_at_boot_and_give_permission_to_access_.2Fdev.2Fnvram)
*   [2 Setting a more readable color and better placement](#Setting_a_more_readable_color_and_better_placement)
*   [3 Starting with KDE](#Starting_with_KDE)
*   [4 Starting with Fluxbox](#Starting_with_Fluxbox)
*   [5 Play a sound on volume change](#Play_a_sound_on_volume_change)
*   [6 See also](#See_also)

## Loading nvram at boot and give permission to access /dev/nvram

*   Check with lsmod if the nvram module is loaded on boot
*   If not, add `nvram` to `MODULES=(... nvram)` in `/etc/rc.conf`
*   Check /dev/nvram permissions, your user must have read access to it.
*   Edit /etc/udev/rules.d/51-arch.rules (WARNING: It will be overwritten with new udev update!)

```
KERNEL=="nvram",   NAME="misc/%k", SYMLINK+="%k", GROUP="kmem", MODE="0660"

```

*   Note: this line seems to work better for some users:

```
KERNEL=="nvram", GROUP="kmem", MODE="0660"

```

**Note:** Check if there is already a line matching `nvram` in the `/etc/udev/rules.d/` directory. In this case, you have to modify the existing entry, and do not create a tpb.rules.

**Note:** Write access to nvram is only needed to set volume with MIXER ON. see /etc/tpbrc.

## Setting a more readable color and better placement

 `/etc/tpbrc` 

```
OSDCOLOR    Green
OSDVERTICAL 0
OSDHORIZONTAL 0
OSDPOS      MIDDLE
OSDALIGN    CENTER

```

## Starting with KDE

 `~/.kde/Autostart/tpb-startup.sh` 

```
# Start Thinkpad OSD daemon
if [ -x /usr/bin/tpb ] &&  [ -w /dev/nvram ] && [ -r /dev/nvram ]; then
    /usr/bin/tpb -d
fi

```

## Starting with Fluxbox

 `~/.fluxbox/startup` 

```
# Start Thinkpad OSD daemon
if [ -x /usr/bin/tpb ] &&  [ -w /dev/nvram ] && [ -r /dev/nvram ]; then
    /usr/bin/tpb -d
fi

```

## Play a sound on volume change

You can play a sound when using the volume buttons (mac like).

 `/etc/tpbrc` 

```
CALLBACK /usr/local/bin/callback_volume.sh

```

 `/usr/local/bin/callback_volume.sh` 

```
#!/bin/sh
[ "$1" = "volume" ] && exec canberra-gtk-play --file=/usr/share/sounds/freedesktop/stereo/audio-volume-change.oga
```

Then:

```
# chmod +x /usr/local/bin/callback_volume.sh

```

Finally, restart tpb.

## See also

*   [http://www.thinkwiki.org/wiki/Tpb](http://www.thinkwiki.org/wiki/Tpb)

Retrieved from "[https://wiki.archlinux.org/index.php?title=ThinkPad_OSD&oldid=411379](https://wiki.archlinux.org/index.php?title=ThinkPad_OSD&oldid=411379)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")