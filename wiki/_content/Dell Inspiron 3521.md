# Dell Inspiron 3521

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The Dell Inspiron 3521 is a Dell laptop made in 2012 and comes with UEFI and Windows 8 by default. This guide will tell you how to configure the Dell Inspiron 3521 to run Arch Linux quite well. We will cover: Turning on Legacy BIOS mode, controlling the Fans, and controlling CPU temperatures.

## Turn on Legacy BIOS

You can turn on the Legacy BIOS boot mode in the BIOS menu. Press f2 on startup to access the setup. Set secure boot to off and set boot list order to legacy. This will allow you to load other Operating Systems from the BIOS. (You can also use [UEFI](/index.php/UEFI "UEFI") mode, but secure boot needs to be off, and the Operating System you want (Arch in this case) needs to support UEFI).

## Controlling Fans

This laptop does not have any options for fan settings in the BIOS. But the good news is, geocool on github wrote a ruby script for controlling fans on this laptop, which you can find [here](https://github.com/geocool/CPU-Fan-Control-Dell-3521). You will need i8kutils and i8kmonitor installed. Get i8kutils from the [official repositories](/index.php/Official_repositories "Official repositories") and i8kmonitor from the [AUR](/index.php/AUR "AUR") You will also need [ruby](/index.php/Ruby "Ruby") installed.

Download the script with git, then run the install.rb. Then you need to copy fanControl.rb to /usr/bin Also it is a good idea to comment out the espeak notifications in fanControl.rb. Do that on the Fan=off, fan=low and fan=high settings. This will prevent espeak from speaking those settings.

In order to use fanControl.rb i8kutils needs to be loaded. To load it at boot add:

 `/etc/modprobe.d/i8k.conf`  `i8k` 

to your kernel modules, or you can do:

```
# modprobe i8k

```

Then run fanControl.rb and your fans are controlled.

If you want to set the fan to a specific setting, you can do that with:

```
$ fanControl.rb -no -cl (for constant low) -ch (constant high) -co (constant off)

```

I personally keep my fan on a Constant Low. I do not have to really worry about summer temps affecting my cpu. Depending on where you live however, you might consider using -ch as otherwise your cpu will melt.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Inspiron_3521&oldid=380451](https://wiki.archlinux.org/index.php?title=Dell_Inspiron_3521&oldid=380451)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dell](/index.php/Category:Dell "Category:Dell")