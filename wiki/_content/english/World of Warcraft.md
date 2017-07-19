World of Warcraft (WoW) is a Massively Multiplayer Online Role-Playing Game (MMORPG) by Blizzard Entertainment taking place in the fictional world of Azeroth, the world that previous Blizzard titles in the Realtime Stategy (RTS) Warcraft series. For more information about the game itself, visit [the Official World of Warcraft website](http://www.worldofwarcraft.com/).

This article will describe how install and run in on Arch Linux using [Wine](http://winehq.org/).

Some of this information was provided by [http://wowpedia.org/World_of_Warcraft_functionality_on_Wine](http://wowpedia.org/World_of_Warcraft_functionality_on_Wine) which is the best general source of information on WoW on Wine.

## Contents

*   [1 Installing Wine](#Installing_Wine)
*   [2 Installing the game](#Installing_the_game)
    *   [2.1 Using an existing installation](#Using_an_existing_installation)
    *   [2.2 New installation from DVD](#New_installation_from_DVD)
*   [3 Configuration](#Configuration)
    *   [3.1 Using OpenGL](#Using_OpenGL)
    *   [3.2 Resolution and colour depth](#Resolution_and_colour_depth)
    *   [3.3 Windowing](#Windowing)
    *   [3.4 Black textures issue](#Black_textures_issue)
    *   [3.5 Sound Issues](#Sound_Issues)
        *   [3.5.1 Configuring the buffer](#Configuring_the_buffer)
*   [4 Performance tweaks](#Performance_tweaks)
    *   [4.1 Disable OpenGL Vertex Buffer Object](#Disable_OpenGL_Vertex_Buffer_Object)
    *   [4.2 For Nvidia users](#For_Nvidia_users)
        *   [4.2.1 Direct3D mode](#Direct3D_mode)
        *   [4.2.2 GLXUnsupportedPrivateRequest problem](#GLXUnsupportedPrivateRequest_problem)
    *   [4.3 AMD CPU users](#AMD_CPU_users)
    *   [4.4 CPU/I-O schedulers](#CPU.2FI-O_schedulers)
    *   [4.5 Enable CSMT](#Enable_CSMT)
*   [5 Links](#Links)

## Installing Wine

See [Wine](/index.php/Wine "Wine").

## Installing the game

Install the Battle.net client, as described in [Battle.net](/index.php/Battle.net "Battle.net"). You can then install World of Warcraft from within the client.

### Using an existing installation

After installing the Battle.net client, you can choose "Locate the game" in the bottom of the screen, and point to the existing install location. You can also point to an installation on a mounted Windows drive.

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

The World of Warcraft configuration file is located at `World of Warcraft\WTF\Config.wtf`.

### Using OpenGL

Add the following line which makes WoW run in OpenGL instead of DirectX Mode. Doing so though will result in lower quality graphics as it appears the OpenGL renderer isn't updated as frequently. D3D9 has more graphical features (like stencil shadows, liquid water, sunshafts) and higher shader model.

 `Config.wtf` 
```
SET gxApi "opengl"

```

If you run Intel/AMD on the open source Mesa drivers and the game crashes on launch due to an access violation, you may need to force WoW to use OpenGL 3.3\. Add this to your startup script:

```
export MESA_GL_VERSION_OVERRIDE=3.3COMPAT

```

### Resolution and colour depth

You can change the following two lines to set the default WoW resolution. I have a 19" Monitor so I can use the following.

 `Config.wtf` 
```
SET gxColorBits "24"
SET gxResolution "1440x900"

```

### Windowing

You can run in a Window by setting this, which is confirmed to work in Wine.

 `Config.wtf` 
```
SET gxWindow "1"

```

### Black textures issue

If you're using an Intel graphics card and you can see black textures in the game (or the game crashes in OpenGL mode), you should enable S3TC texture compression support. It can be enabled through [driconf](https://www.archlinux.org/packages/?name=driconf) or by installing [libtxc_dxtn](https://www.archlinux.org/packages/?name=libtxc_dxtn).

### Sound Issues

#### Configuring the buffer

If the sound makes a horrendous racket with squeaks and white noise try :

 `Config.wtf` 
```
SET SoundOutputSystem "1" 
SET SoundBufferSize "100"

```

## Performance tweaks

### Disable OpenGL Vertex Buffer Object

1\. Here is a performance tweak that can boost your FPS significantly (everything without quotes):

```
 - Open Wine's version of the registry editor by running "regedit"
 - Navigate to HKEY_CURRENT_USER\Software\Wine\ 
 - Select the "Wine" folder, right-click onto the folder symbol and select  New-> Key and rename it to "OpenGL"
 - Select the OpenGL-Key, then right-click into the right-hand pane, chose New-> String Value and hit enter
 - Rename "New Value #1" to "DisabledExtensions"
 - Double-Click on the renamed Key and enter "GL_ARB_vertex_buffer_object" into the "value" field

```

That was it, close the registry editor again, your changes will be saved automatically.

2\. If you are finding it annoying that turning your character by let us say 90 degree takes n seconds normally, but n+m seconds in pupolated areas (in other words: that the polygon count of your surroundings affects the camera turning speed), apply something to "GL_ARB_vertex_buffer_object", like let us say a "2", so it looks like this: "GL_ARB_vertex_buffer_object2". You will still have the performance boost of the above tweak, but with a smoother feeling.

### For Nvidia users

As of version 310.14 of the [NVIDIA](/index.php/NVIDIA "NVIDIA") driver, an option exists for threaded OpenGL performance optimization. WoW benefits greatly from utilizing this.

(Sidenote: this makes the 'RGL' patch/library/hack redundant for Nvidia users)

Exporting __GL_THREADED_OPTIMIZATIONS=1 enables the optimizations. Example of launching WoW with these optimizations:

```
__GL_THREADED_OPTIMIZATIONS=1 wine Wow.exe -opengl

```

Once you've confirmed the game works well for you (applies to any game, not just WoW) you can turn off debugging output to potentially improve performance further:

```
WINEDEBUG=-all __GL_THREADED_OPTIMIZATIONS=1 wine Wow.exe -opengl $> /dev/null

```

#### Direct3D mode

If running the game in Direct3D mode, in conjunction with the above optimization, compiling Wine with the [*"Use glBufferSubDataARB for dynamic buffer uploads"*](http://bugs.winehq.org/show_bug.cgi?id=11674#c263) patch should yield a further performance increase. This patch does not appear to increase performance in OpenGL mode, though OpenGL mode generally results in higher framerates anyway... albeit at the cost of the game's more advanced Direct3D eye candy.

**Note:** You MUST turn off Wine's debugging to benefit from this

```
WINEDEBUG=-all __GL_THREADED_OPTIMIZATIONS=1 wine Wow.exe

```

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

If you're using Direct3D 9 (no effect on OpenGL) you can use [CSMT](https://github.com/wine-compholio/wine-staging/wiki/CSMT) (making wine use multithreading) for a significant performance boost. You will need to install [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) (testing branch of wine) and open *winecfg* and enable CSMT in the "Staging" tab.

## Links

*   [World of Warcraft in the Wine AppDB](https://appdb.winehq.org/objectManager.php?sClass=application&iId=1922)
*   [Wowpedia](http://www.wowpedia.org/Main_Page)
*   [Patch Mirrors](http://www.wowpedia.org/Patch_mirrors)