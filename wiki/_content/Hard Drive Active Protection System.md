# Hard Drive Active Protection System

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**H**ard **D**rive **A**ctive **P**rotection **S**ystem (**HDAPS**) protects your hard drive from sudden shocks (such as dropping or banging your laptop on a desk). It does this by parking the disk heads, so that shocks do not cause them to crash into the drive's platters. Hopefully, this will prevent catastrophic failure.

**Note:** [SSD](/index.php/SSD "SSD") drives do not need HDAPS as they lack any mechanical components.

## Contents

*   [1 Shock detection](#Shock_detection)
    *   [1.1 tp_smapi](#tp_smapi)
    *   [1.2 Invert module parameter](#Invert_module_parameter)
*   [2 Shock protection](#Shock_protection)
    *   [2.1 hdapsd](#hdapsd)
*   [3 GUI Utilities](#GUI_Utilities)
    *   [3.1 gnome-hdaps-applet](#gnome-hdaps-applet)
    *   [3.2 kdeplasma-applets-hdaps-monitor](#kdeplasma-applets-hdaps-monitor)
    *   [3.3 xfce4-hdaps](#xfce4-hdaps)
    *   [3.4 HDAPSicon](#HDAPSicon)
    *   [3.5 hdaps-gl](#hdaps-gl)
*   [4 See also](#See_also)

## Shock detection

Your hardware needs to support some kind of shock detection. This is usually in the form of an accelerometer built into your laptop's motherboard. If you have the hardware, you also need a way to communicate what the hardware is detecting to your operating system. This section describes drivers to communicate the accelerometer's state to the OS so it can detect and protect against shocks.

### tp_smapi

[tp_smapi](/index.php/Tp_smapi "Tp smapi") is a set of drivers for many ThinkPad laptops. It is highly recommended if you have a supported ThinkPad, even if you do not plan to use HDAPS. Among a plethora of other useful things, tp_smapi represents the accelerometer output as joystick devices `/dev/input/js#` (Note! This could interfere with other joystick devices on your system).

Install tp_smapi from the community repository. After a reboot, this will activate most of the drivers, represented through the `/sys/devices/platform/smapi` filesystem.

The kernel provides its own HDAPS drivers. Previously, it was necessary to manually `insmod` the module via `/etc/rc.local` to prevent the default drivers from being loaded. The [tp_smapi](/index.php/Tp_smapi "Tp smapi") package from community now installs `hdaps.ko` to [/lib/modules/$(uname -r)/updates](http://www.mail-archive.com/arch-dev-public@archlinux.org/msg01995.html), which will let it supercede the built-in module. Thus, you can simply add `hdaps` to your `MODULES` array.

**Note:** According to [this bug report](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=628829), certain ThinkPad laptops use different firmware which tp_smapi does not support and is unlikely to support in the near future. This includes the following series: Edge, SL, L, X1xxe. Only one of these is listed in the "unsupported hardware" page for the project, however, and that listing suggests that the x121e should mostly work. I get the same error with the x121e listed at the bottom of the bug report as a different and more fundamental problem, though, so it may be that some models of the x121e are mostly supported and others are entirely unsupported.

### Invert module parameter

For some ThinkPads, the invert module parameter is needed in order to handle the X and Y rotation axes correctly. In that case, you can add the option in `/etc/modprobe.d/modprobe.conf`:

```
options hdaps invert=1

```

`invert=1` is an example value used for a ThinkPad T410\. The invert option takes the following values:

*   invert=1 invert both X and Y axes;
*   invert=2 invert the X axes (uninvert if already both axes inverted)
*   invert=4 swap X and Y (takes place before inverting)

Note that options can be summed. For instance, invert=5 swaps the axes and inverts them. The maximum value of invert is obviously 7\. If you do not know which option is correct for you, just try them out with hdaps-gl or some other GUI (see below). Alternatively, you can determine the exact value for your thinkpad model from [this table](http://www.thinkwiki.org/wiki/Tp_smapi) under the column labelled "HDAPS axis orientation".

As an alternative to reloading the `hdaps` module, the `invert` value can also be written directly to `/sys/devices/platform/hdaps/invert`.

## Shock protection

Now that your hardware is reporting its shock detection to the OS, we need to do something with this data. This section describes software utilities to transform the sensor output into shock protection.

### hdapsd

hdapsd monitors the output of the HDAPS joystick devices to determine if a shock is about to occur, then tells the kernel to park the disk heads.

You should check your "Load cycle count" in [SMART](/index.php/SMART "SMART") when setting up hdaps, if it is too sensitive the head would park too often and load cycle count would rise too rapidly.

[Install](/index.php/Install "Install") [hdapsd](https://www.archlinux.org/packages/?name=hdapsd). You can [start](/index.php/Start "Start") the hdapsd daemon with `hdapsd.service`.

You can adjust the parameters, with which hdapsd is run by providing your own unit file as explained in the [systemd article](/index.php/Systemd#Editing_provided_units "Systemd"), for example the following file will adjust sensitivity and logging behaviour of the hdaps daemon:

 `/etc/systemd/system/hdapsd.service.d/sensitivity.conf` 

```
[Service]
ExecStart=
ExecStart=/usr/bin/hdapsd --sensitivity=40 -blp

```

And reload the configuration.

## GUI Utilities

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Use Template:App (Discuss in [Talk:Hard Drive Active Protection System#](https://wiki.archlinux.org/index.php/Talk:Hard_Drive_Active_Protection_System))

Utilities exist to monitor hdapsd's status so you know what is going on while you are using your laptop. These are entirely optional, but very handy.

### gnome-hdaps-applet

This is a GNOME panel applet (Note: XFCE can use GNOME panel applets) that represents the current status of your hard drive. The package is available in [AUR](/index.php/AUR "AUR"): [gnome-hdaps-applet](https://aur.archlinux.org/packages/gnome-hdaps-applet/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnome-hdaps-applet)]</sup>. If you do not want to monitor sda or hda by default, edit the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") before compiling.

### kdeplasma-applets-hdaps-monitor

For KDE4 there is a plasmoid for HDAPS monitoring [HDAPS monitor](http://kde-look.org/content/show.php/HDAPS+monitor?content=103481). The package [kdeplasma-applets-hdaps-monitor](https://aur.archlinux.org/packages/kdeplasma-applets-hdaps-monitor/)<sup><small>AUR</small></sup> is available in [AUR](/index.php/AUR "AUR").

### xfce4-hdaps

This is a Xfce4 panel applet that can represents the current status of your hard drive. Available in [AUR](/index.php/AUR "AUR"): [xfce4-hdaps](https://aur.archlinux.org/packages/xfce4-hdaps/)<sup><small>AUR</small></sup>. After install, add this applet to a panel.

### HDAPSicon

HDAPSicon, formerly thinkhdaps, is a standalone GTK applet for HDAPS disk protection status. While running will show applet icon in the notification area. Available in AUR: [hdapsicon-git](https://aur.archlinux.org/packages/hdapsicon-git/)<sup><small>AUR</small></sup>.

### hdaps-gl

Simple OpenGL application showing the 3D animation of your Thinkpad. Similar to the apllication Lenovo distributes with Windows. [hdaps-gl](https://aur.archlinux.org/packages/hdaps-gl/)<sup><small>AUR</small></sup> is available in AUR.

## See also

*   [How to protect the harddisk through APS at ThinkWiki](http://www.thinkwiki.org/wiki/How_to_protect_the_harddisk_through_APS)
*   [HDAPS at ThinkWiki](http://www.thinkwiki.org/wiki/HDAPS)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hard_Drive_Active_Protection_System&oldid=411992](https://wiki.archlinux.org/index.php?title=Hard_Drive_Active_Protection_System&oldid=411992)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Laptops](/index.php/Category:Laptops "Category:Laptops")

Hidden categories:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")