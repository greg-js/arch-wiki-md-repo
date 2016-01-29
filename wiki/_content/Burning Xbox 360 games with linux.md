# Burning Xbox 360 games with linux

**Warning:** The legality of this process may be questionable. Refer to the copyright laws in your country for clarification. Playing backup games online may result in your Xbox 360 console being banned from Xbox Live. Follow this guide at your own risk!

**Tip:** Backups may only be played on an Xbox 360 with a flashed firmware.

## Contents

*   [1 Overview](#Overview)
*   [2 Stealth Patching](#Stealth_Patching)
*   [3 Burning ISO Files](#Burning_ISO_Files)
*   [4 Burning .000 Files](#Burning_.000_Files)
*   [5 xbox 360_burn](#xbox_360_burn)
*   [6 Notes](#Notes)

## Overview

Xbox 360 games come in two image formats: .iso and .000\. They are burned on dual layer DVD+R discs. This requires a dual-layer DVD burner. No specific brand or burner is needed. In order to maximize the success of your burn, you should burn at the slowest speed your burner and media allow.

Please note that games must be burned onto DVD+R DL (Dual Layered), as DVD-R DL would not work.

## Stealth Patching

Stealth patching patches a game image to make it ignore the security check done by the Xbox 360 console upon boot. If you use a stealth firmware, you will need to patch your backup. You can do this with a tool called [abgx360](https://aur.archlinux.org/packages/abgx360/)<sup><small>AUR</small></sup>, which can be found in the [AUR](/index.php/AUR "AUR").

abgx360 works on .iso _and_ .000 images. In order to patch these images, use the `--af3` flag, as such:

```
   abgx360 --af3 /path/to/game.iso

```

Using this tool should patch the file with no issues. It will also output metadata about the game.

## Burning ISO Files

**Note:** You can use [Imgburn + Wine](https://wiki.archlinux.org/index.php/Wine#Burning_optical_media) to burn ISO (yes, XGD3 burns work with burnermax drives and since Imgburn 2.5.8 the builtin "BurnerMax Payload" feature works as well).

Burning an iso is best done through the command line with growisofs. This is found in the [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) package found in the [Official repositories](/index.php/Official_repositories "Official repositories").

There are other applications you can use to burn the image ([k3b](https://www.archlinux.org/packages/?name=k3b), [gnomebaker](https://aur.archlinux.org/packages/gnomebaker/)<sup><small>AUR</small></sup>, etc) but you may miss some configuration options and end up with a dud burn. Use the following command to burn the image to disc.

XGD1/XGD2:

```
   growisofs -use-the-force-luke=dao -use-the-force-luke=break:1913760 -dvd-compat -speed=2 -Z /dev/sr0=/path/to/game.iso

```

XGD3(iXtreme Burner Max Firmware):

```
   growisofs -use-the-force-luke=dao -use-the-force-luke=break:2133520 -dvd-compat -speed=2 -Z /dev/sr0=/path/to/game.iso

```

Replace `/dev/sr0` with the path to your dual layer drive. For most systems it will be `/dev/sr0`. Since May 2011, the `/dev/dvd` symlink has been removed in [udev](/index.php/Udev "Udev"). See [[1]](https://bbs.archlinux.org/viewtopic.php?id=120010) for more details.

If everything has been set up correctly you should see a messages like this:

```
   Executing 'builtin_dd if=TalesOfVesperia.iso of=/dev/sr0 obs=32k seek=0'
   /dev/sr0: splitting layers at 1913760 blocks
   /dev/sr0: "Current Write Speed" is 2.5x1352KBps.
   3538944/7835492352 ( 0.0%) @0.8x, remaining 45:39 RBU  89.7% UBU   7.1%

```

The burn should take around approximately 40 minutes at 2.4x write speed, depending on the size of the iso.

## Burning .000 Files

To burn a .000 image you must first patch it with a Java application called imagebpatch.jar. You can get it [here](http://www.megaupload.com/?d=2JOIHFU3). You will need to have java installed to use this.

```
   pacman -S jre

```

Logout and login again (or `source /etc/profile`) in order to update your $PATH.

After you've installed Java and downloaded the application, just run it in the console:

```
   java -jar imgbpatch.jar /path/to/image.000

```

Now it can be burned like an iso, using the following.

XGD1/XGD2:

```
   growisofs -use-the-force-luke=dao -use-the-force-luke=break:1913760  -dvd-compat -speed=2 -Z /dev/sr0=/path/to/game.000

```

XGD3(iXtreme Burner Max Firmware):

```
   growisofs -use-the-force-luke=dao -use-the-force-luke=break:2133520  -dvd-compat -speed=2 -Z /dev/sr0=/path/to/game.000

```

Replace `/dev/sr0` with the path to your dual layer drive. For most systems it will be `/dev/sr0`. Since May 2011, the /dev/dvd symlink has been removed in udev. See [[2]](https://bbs.archlinux.org/viewtopic.php?id=120010) for more details.

## xbox 360_burn

It's obviously possible to create an executable file containing the command to burn DVD, as such, someone has created a bash script to allow for a more user-friendly interface. [It has since been rewritten into python](https://github.com/jawilson/dotfiles/blob/master/bin/xbox360_burn).

To burn, you then only have to use this command:

```
   xbox360_burn -ib /dev/sr0 rom.iso

```

Replace `/dev/sr0` with the path to your dual layer drive. For most systems it will be `/dev/sr0`. Since May 2011, the /dev/dvd symlink has been removed in udev. See [[3]](https://bbs.archlinux.org/viewtopic.php?id=120010) for more details.

## Notes

**Warning:** It seems that removing these parameters from the command line for XGD1/2 burning will set a wrong layer break and make your backup broken.

To fix error **"...INVALID FIELD IN PARAMETER LIST..."** you need to omit these options from the command line:

```
   -use-the-force-luke=dao -dvd-compat

```

So for example command becomes:

```
   growisofs -use-the-force-luke=break:layer_break_size -speed=2 -Z /dev/sr0=/path/to/game.iso

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Burning_Xbox_360_games_with_linux&oldid=376514](https://wiki.archlinux.org/index.php?title=Burning_Xbox_360_games_with_linux&oldid=376514)"