World of Warcraft (WoW) is a Massively Multiplayer Online Role-Playing Game (MMORPG) by Blizzard Entertainment taking place in the fictional world of Azeroth, the world that previous Blizzard titles in the Realtime Stategy (RTS) Warcraft series. For more information about the game itself, visit [the Official World of Warcraft website](http://www.worldofwarcraft.com/).

This article will describe how install and run in on Arch Linux using [Wine](http://winehq.org/).

Some of this information was provided by [http://wowpedia.org/World_of_Warcraft_functionality_on_Wine](http://wowpedia.org/World_of_Warcraft_functionality_on_Wine) which is the best general source of information on WoW on Wine.

## Contents

*   [1 Installing Wine](#Installing_Wine)
*   [2 Installing the game](#Installing_the_game)
    *   [2.1 Using an existing installation](#Using_an_existing_installation)
    *   [2.2 New installation from DVD](#New_installation_from_DVD)
*   [3 Configuration](#Configuration)
    *   [3.1 Resolution and colour depth](#Resolution_and_colour_depth)
    *   [3.2 Windowing](#Windowing)
    *   [3.3 Configuring the sound buffer](#Configuring_the_sound_buffer)
*   [4 Performance tweaks](#Performance_tweaks)
    *   [4.1 For Nvidia users](#For_Nvidia_users)
        *   [4.1.1 glBufferSubDataARB](#glBufferSubDataARB)
        *   [4.1.2 GLXUnsupportedPrivateRequest problem](#GLXUnsupportedPrivateRequest_problem)
    *   [4.2 AMD CPU users](#AMD_CPU_users)
    *   [4.3 CPU/I-O schedulers](#CPU.2FI-O_schedulers)
    *   [4.4 Enable CSMT](#Enable_CSMT)
*   [5 Links](#Links)

## Installing Wine

See [Wine](/index.php/Wine "Wine").

## Installing the game

Install the Blizzard App, as described in [Blizzard App](/index.php/Blizzard_App "Blizzard App"). You can then install World of Warcraft from within the client.

### Using an existing installation

After installing the Blizzard App, you can choose "Locate the game" in the bottom of the screen, and point to the existing install location. You can also point to an installation on a mounted Windows drive.

### New installation from DVD

**Note:** Note that on some WoW DVD's the installer executable is hidden and you need to mount the disc with the 'unhide' option. To do this type in a terminal: `mount -t iso9660 -o ro,unhide /dev/cdrom /media/cdrom/`

Insert first the DVD. If it will be mounted automatically - just unmount.

```
 # umount /media/dvd

```

Now mount manually

```
 # mount -t iso9660 /dev/dvd0 /mnt/dvd

```

Now you will find the Install.exe on the DVD

```
 ~ wine /mnt/dvd/Installer.exe

```

## Configuration

**Note:** The OpenGL renderer is no longer maintained and produces flickery/buggy rendering. Switch back to the Direct3D renderer by setting `SET gxApi d3d9` in `Config.wtf`.

The World of Warcraft configuration file is located at `World of Warcraft\WTF\Config.wtf`.

### Resolution and colour depth

You can change the following two lines to set the default resolution.

 `Config.wtf` 
```
SET gxColorBits "24"
SET gxResolution "1440x900"

```

### Windowing

You can run in a Window by setting this.

 `Config.wtf` 
```
SET gxWindow "1"

```

### Configuring the sound buffer

If the sound makes a horrendous racket with squeaks and white noise the following settings.

 `Config.wtf` 
```
SET SoundOutputSystem "1" 
SET SoundBufferSize "100"

```

## Performance tweaks

### For Nvidia users

The [NVIDIA](/index.php/NVIDIA "NVIDIA") driver has an option for threaded OpenGL performance optimization. WoW benefits greatly from utilizing this.

Exporting `__GL_THREADED_OPTIMIZATIONS=1` enables the optimizations. Example of launching WoW with these optimizations:

```
__GL_THREADED_OPTIMIZATIONS=1 wine Wow-64.exe

```

Once you've confirmed the game works well for you (applies to any game, not just WoW) you can turn off debugging output to potentially improve performance further:

```
WINEDEBUG=-all __GL_THREADED_OPTIMIZATIONS=1 wine Wow-64.exe

```

#### glBufferSubDataARB

Compiling Wine with the [*"Use glBufferSubDataARB for dynamic buffer uploads"*](http://bugs.winehq.org/show_bug.cgi?id=11674#c263) patch should yield a further performance increase.

**Note:** You MUST turn off Wine's debugging to benefit from this

#### GLXUnsupportedPrivateRequest problem

On 64 bit systems, if you're using bumblebee and using optirun to run game with Nvidia graphic card on your system, you will encounter this error:

```
X Error of failed request:  GLXUnsupportedPrivateRequest

```

In most cases installing [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) will solve this problem. [bbs](https://bbs.archlinux.org/viewtopic.php?pid=1381891#p1381891)

### AMD CPU users

As WoW significant benefits from L3-Cache you should check if your Processor/Bios has a L3-allocation Option available, BSP-Only allocation is what worked for me pretty well. By switching from all-cores allocation to BSP-only the FPS on my system did jump from ~70 outdoors to over 120+. This was done on a II X4 640 with Nvidia Graphics Card(proprietary driver) using -opengl and the thread optimization.

### CPU/I-O schedulers

You can greatly increase World of Warcraft performance by choosing the right schedulers for your machine. Currently, the most-recent version of wine in the official repositories is not configured to fully take advantage of the linux-ck kernel. Instead, it is recommended that wine gamers use the CFS scheduler. Also, World of Warcraft runs better with the deadline I/O scheduler (as opposed to noop, cfq, bfq, etc). You can check if you will benefit from switching I/O schedulers first by determining which I/O scheduler you are using on your drive:

```
# fdisk -l *to determine the hard drive arch is installed on*
# cat /sys/block/sdX/queue/scheduler *Where X is the letter of the drive fdisk reports*
# echo deadline > /sys/block/sdX/queue/scheduler

```

This is a temporary fix (it does not set deadline permanently), but you may gain an additional 5-30fps, by enabling deadline as the I/O scheduler. Moreover, feel free to play around with other schedulers to pick the one which runs best on your machine, especially if you have an SSD.

### Enable CSMT

You can use [CSMT](https://github.com/wine-compholio/wine-staging/wiki/CSMT) (making wine use multithreading) for a significant performance boost. You will need to install [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) (testing branch of wine) and open *winecfg* and enable CSMT in the "Staging" tab.

## Links

*   [World of Warcraft in the Wine AppDB](https://appdb.winehq.org/objectManager.php?sClass=application&iId=1922)
*   [Wowpedia](https://wow.gamepedia.com/Portal:Main)