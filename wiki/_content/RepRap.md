# RepRap

RepRap is an open-source 3D printer project. A RepRap prints objects of plastic and is intended for rapid-prototyping, the printer itself is built with small plastic parts which can be printed out and replaced. This page explains how to install RepRap host software on Arch Linux and how to print 3D models. More information is available on the [RepRap homepage](http://www.reprap.org).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Host software alternatives](#Host_software_alternatives)
    *   [3.1 Cura](#Cura)
    *   [3.2 MatterControl](#MatterControl)
    *   [3.3 Printrun / Pronterface](#Printrun_.2F_Pronterface)
    *   [3.4 ReplicatorG](#ReplicatorG)
    *   [3.5 Repetier](#Repetier)
*   [4 See Also](#See_Also)
    *   [4.1 Calibration](#Calibration)
    *   [4.2 3D models & STL files](#3D_models_.26_STL_files)
    *   [4.3 Manual](#Manual)

## Installation

**Note:** Custom firmware may be available to you from your electronics supplier, it may even be pre-installed.

Many of the controller chips for RepRap are arduino based, or arduino derived (such as Melzi). Figure out what electronics you have from the RepRap [Official Electronics](http://reprap.org/wiki/%22Official%22_Electronics) page. You will also find what firmware you have on that page.

Follow the [arduino](/index.php/Arduino "Arduino") wiki page if you have an arduino based controller. Do the Installation and Configuration steps.

Install the host software by following this guide [Installing RepRap on your computer](http://reprap.org/wiki/Installing_RepRap_on_your_computer). There are alternative host software solutions which are easier to install and are described in the following sections.

## Configuration

**Note:** If you do not have firmware installed on your electronics, you may not be able to connect via USB or control the motors.

Connect your 3D printer to your computer and run the host software. Use the host software's user interface to send commands to the printer.

**Warning:** If you have not tested your printer previously, make sure you have your hand on the emergency stop button (your power plug). Don't let the hotend go through the hotbed, if the stepper motors don't stop when they reach the end stoppers or move the wrong way, stop the printer and check your wiring.

## Host software alternatives

#### Cura

*   Install [cura](https://aur.archlinux.org/packages/cura/) from [AUR](/index.php/AUR "AUR").

Run cura

```
$ cura

```

Configure it to use RepRap in the startup configuration wizard. Select the RepRap model you are using, or select Custom RepRap.

#### MatterControl

MatterControl is a combined slicer/host similar to Cura. Install [mattercontrol](https://aur.archlinux.org/packages/mattercontrol/) from [AUR](/index.php/AUR "AUR"), then run it.

```
$ mattercontrol

```

The AUR package is built from source and does not include the closed source plugins. You can add these by extracting the appropriate DLLs from the Debian package at [mattercontrol.com](http://www.mattercontrol.com/) and copying them into `/usr/lib/mattercontrol`. These files include...

```
 CloudServices.dll
 CloudServices.dll.config
 CloudServices.dll.mdb
 MatterControlAuth.dll
 MatterControlAuth.dll.config
 MatterControlAuth.dll.mdb
 Mono.Nat.dll
 Mono.Nat.dll.mdb
 PictureCreator.dll
 PictureCreator.dll.config
 PictureCreator.dll.mdb
 PrintNotifications.dll
 PrintNotifications.dll.config
 PrintNotifications.dll.mdb

```

MatterControl's built in slice engine is MatterSlice, which is a port of CuraEngine to C#. You can also choose other slicing engines. To use Slic3r in MatterControl, make a symlink in `/usr/lib/mattercontrol/Slic3r/bin` to the Slic3r executable.

```
 $ mkdir /usr/lib/mattercontrol/Slic3r/bin
 $ ln -s /usr/bin/slic3r /usr/lib/mattercontrol/Slic3r/bin/slic3r

```

To use CuraEngine, do

```
 $ ln -s /usr/share/cura/CuraEngine /usr/lib/mattercontrol/CuraEngine.exe

```

#### Printrun / Pronterface

Printrun consists of printcore, pronsole and pronterface, and a small collection of helpful scripts.

*   printcore.py is a library that makes writing reprap hosts easy
*   pronsole.py is an interactive command-line host software with tabcompletion goodness
*   pronterface.py is a graphical host software with the same functionality as pronsole

It is pronterface and pronsole which will be most usefull to us.

*   Install [printrun](https://aur.archlinux.org/packages/printrun/) from [AUR](/index.php/AUR "AUR").

Now you can run the pronterface and pronsole commands directly. Let's start pronterface, as it has a GUI.

```
$ pronterface.py

```

Use it to send commands to your 3D printer.

If you have to run it by calling a helper script like mendel.sh, it might be a good idea modify the script to use python2 instead of default python (python3).

```
# sed -r 's,bin/python(2)*,bin/python2,' _/path/to/mendel.sh_

```

#### ReplicatorG

*   Install [replicatorg](https://aur.archlinux.org/packages/replicatorg/) from [AUR](/index.php/AUR "AUR").
*   Make sure you are in group users

Set write permissions in /opt/replicatorg

```
# chmod g+w /opt/replicatorg

```

On a 64-bit system, copy to following libraries into /opt/replicatorg

```
# cp /usr/lib/librxtxSerial-2.2pre1.so /opt/replicatorg/lib-x86_64
# cp /usr/share/java/rxtx/RXTXcomm.jar /opt/replicatorg/lib

```

Then simply run replicatorg

```
$ replicatorg

```

Alternatively download ReplicatorG from somewhere else. You will need [java](/index.php/Java "Java") installed.

```
$ ./replicatorg

```

#### Repetier

Repetier is a little like pronterface.

*   Install [repetier-host](https://aur.archlinux.org/packages/repetier-host/) from [AUR](/index.php/AUR "AUR").

Read more at [http://www.repetier.com/](http://www.repetier.com/)

## See Also

#### Calibration

[http://youtu.be/wAL9d7FgInk](http://youtu.be/wAL9d7FgInk) [http://calculator.josefprusa.cz/](http://calculator.josefprusa.cz/) [http://reprap.org/wiki/Calibration](http://reprap.org/wiki/Calibration) [http://reprap.org/wiki/Triffid_Hunter%27s_Calibration_Guide](http://reprap.org/wiki/Triffid_Hunter%27s_Calibration_Guide) [http://www.thingiverse.com/thing:5573](http://www.thingiverse.com/thing:5573) [https://sites.google.com/site/repraplogphase/calibration-of-your-reprap](https://sites.google.com/site/repraplogphase/calibration-of-your-reprap)

#### 3D models & STL files

[http://www.thingiverse.com/](http://www.thingiverse.com/)

#### Manual

[http://reprapbook.appspot.com/](http://reprapbook.appspot.com/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=RepRap&oldid=398116](https://wiki.archlinux.org/index.php?title=RepRap&oldid=398116)"