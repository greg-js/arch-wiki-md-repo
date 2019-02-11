To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# dmidecode -t system | grep Version

Version: ThinkPad L380 Yoga

```

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 SD Card](#SD_Card)
    *   [1.2 Wacom](#Wacom)
*   [2 Additional Functionality](#Additional_Functionality)

## Configuration

### SD Card

Works out of box, just don't forget exfat-utils.

### Wacom

Works out of the box.

See [Tablet PC](/index.php/Tablet_PC "Tablet PC") for more configuration

## Additional Functionality

The [thinkpad-yoga-scripts-git](https://aur.archlinux.org/packages/thinkpad-yoga-scripts-git/) package doesn't work well, because the TouchPad and TrackPoint manufacturer was changed.

Using [https://github.com/ffejery/thinkpad-l380-yoga-scripts](https://github.com/ffejery/thinkpad-l380-yoga-scripts) instead works. See [makepkg](/index.php/Makepkg "Makepkg") on how to build it. There's also an AUR: [thinkpad-l380-yoga-scripts-git](https://aur.archlinux.org/packages/thinkpad-l380-yoga-scripts-git/).

Remember to edit the `/opt/thinkpad-l380-yoga-scripts/rotate/thinkpad-rotate.py` as hinted in the readme, because you will probably want the Touchscreen and Pen to rotate together with the screen.