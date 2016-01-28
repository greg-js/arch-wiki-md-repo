# WeTab

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:WeTab#](https://wiki.archlinux.org/index.php/Talk:WeTab))

[The WeTab is a tablet-PC by 4tiitoo and Neofonie.](http://en.wikipedia.org/wiki/WeTab)

## BIOS Update

**Warning:** This part is incomplete and you might have to do your own research about it. Nobody can guarantee that you can't make your WeTab unusuable (brick)

Download the Bios-Update-Stick-V2.zip from [pherzog's website](http://www.pherzog.net/WeTab.das-neue-BIOS-fur-das-WeTab.ashx) and apply the `.img` file inside the zip with dd to a USB Stick like that:

```
dd if=./Bios-Update-Stick-V2.img of=/dev/sdx

```

The text file in the zip describes how to boot the USB Stick, this one is a non-literal translation:

*   Have the WeTab turned on. _Also, have the WeTab connected with the charger, the USB Stick and a Keyboard._
*   Turn it off while holding down the "Hotkey" (Upper-left, that touch-sensitive circle)
*   It should reboot after approximately five seconds.
*   Hold down the "Hotkey" and smash on F11 like it's the last thing you could do before death.
*   Select the USB Stick as boot device, follow your common sense from now on.

## Drivers

### HDMI

There's a very hacky solution for getting the HDMI-slot to work in Archlinux.

You first have to install [chrontel-wetab-rpm](https://aur.archlinux.org/packages/chrontel-wetab-rpm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/chrontel-wetab-rpm)]</sup> from [AUR](/index.php/AUR "AUR").

Then execute the following commands as root:

```
modprobe i2c-dev
mv /dev/i2c-0 /dev/i2c-2
tiitoo-hdmi-daemon

```

**Note:** if mv tells you that i2c-0 doesn't exist, try i2c-14 instead. It depends on the kernel.

*   When you see something on the screen you've plugged on the HDMI-port, you can kill the `tiitoo-hdmi-daemon`. But you don't have to.

*   These commands have to be executed on every booting process.

*   The graphics card in the WeTab is only capable of cloning the output of the internal screen to the HDMI-port, with the same resolution. Because of that, the driver doesn't need a running Xorg to function properly.

Retrieved from "[https://wiki.archlinux.org/index.php?title=WeTab&oldid=392806](https://wiki.archlinux.org/index.php?title=WeTab&oldid=392806)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Other hardware](/index.php/Category:Other_hardware "Category:Other hardware")

Hidden categories:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")