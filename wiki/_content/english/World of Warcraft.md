World of Warcraft (WoW) is a Massively Multiplayer Online Role-Playing Game (MMORPG) by Blizzard Entertainment taking place in the fictional world of Azeroth, the world that previous Blizzard titles in the Realtime Stategy (RTS) Warcraft series. For more information about the game itself, visit [the Official World of Warcraft website](http://www.worldofwarcraft.com/).

This article will describe how install and run in on Arch Linux using [Wine](http://winehq.org/).

Some of this information was provided by [http://wowpedia.org/World_of_Warcraft_functionality_on_Wine](http://wowpedia.org/World_of_Warcraft_functionality_on_Wine) which is the best general source of information on WoW on Wine.

## Contents

*   [1 Installing Wine](#Installing_Wine)
*   [2 Installing the Game](#Installing_the_Game)
    *   [2.1 Downloading and installing via Blizzard's client](#Downloading_and_installing_via_Blizzard.27s_client)
        *   [2.1.1 Downloading the Client](#Downloading_the_Client)
        *   [2.1.2 Installing the Game](#Installing_the_Game_2)
        *   [2.1.3 Troubleshooting](#Troubleshooting)
            *   [2.1.3.1 Not able to agree to terms](#Not_able_to_agree_to_terms)
            *   [2.1.3.2 Wine crashes while reading terms](#Wine_crashes_while_reading_terms)
            *   [2.1.3.3 Battle.net cannot connect](#Battle.net_cannot_connect)
            *   [2.1.3.4 Error Message: This application failed to start because it could not find or load the qt platform plugin windows](#Error_Message:_This_application_failed_to_start_because_it_could_not_find_or_load_the_qt_platform_plugin_windows)
    *   [2.2 Copying the CDs to a folder](#Copying_the_CDs_to_a_folder)
    *   [2.3 Copying an Existing Installation](#Copying_an_Existing_Installation)
    *   [2.4 New Installation from CD](#New_Installation_from_CD)
    *   [2.5 New Installation from DVD](#New_Installation_from_DVD)
*   [3 Installing Patches](#Installing_Patches)
*   [4 Configuration](#Configuration)
    *   [4.1 Using OpenGL](#Using_OpenGL)
    *   [4.2 Resolution and Colour depth](#Resolution_and_Colour_depth)
    *   [4.3 Windowing](#Windowing)
    *   [4.4 Black textures issue](#Black_textures_issue)
    *   [4.5 Sound Issues](#Sound_Issues)
        *   [4.5.1 Configuring the Buffer](#Configuring_the_Buffer)
        *   [4.5.2 Stuttering or Static Sound](#Stuttering_or_Static_Sound)
*   [5 Performance Tweaks](#Performance_Tweaks)
    *   [5.1 For NVIDIA users](#For_NVIDIA_users)
        *   [5.1.1 NVIDIA users and Direct3D mode](#NVIDIA_users_and_Direct3D_mode)
        *   [5.1.2 GLXUnsupportedPrivateRequest Problem](#GLXUnsupportedPrivateRequest_Problem)
    *   [5.2 AMD CPU users=](#AMD_CPU_users.3D)
    *   [5.3 CPU/I-O Schedulers=](#CPU.2FI-O_Schedulers.3D)
*   [6 Links](#Links)

## Installing Wine

See [Wine](/index.php/Wine "Wine").

## Installing the Game

There are five options for installing World of Warcraft.

### Downloading and installing via Blizzard's client

The most straightforward way of installing World of Warcraft on Linux is usually this method, while it may not be the fastest. On slower connections, however, you may not wish to use this method due to the fact that you will have to download the entire game, including patches.

It is known to work with Wine 1.1.39 which can be downloaded off [Wine's website](http://www.winehq.org/) and compiled. However, you may wish to try with the newest version from the extra section, installed via Pacman like so:

```
# pacman -S wine

```

#### Downloading the Client

First step is to download the client. European users can download it off the european World of Warcraft website [here,](http://www.wow-europe.com/en/downloads/client/index.html) while people from the United States would probably want to download the [US client.](http://www.worldofwarcraft.com/downloads/wowclient-download.html)

#### Installing the Game

Once the client is downloaded run the file with Wine:

```
wine World-of-Warcraft-Setup-enGB.exe

```

#### Troubleshooting

##### Not able to agree to terms

In case you can not see the license text, you probably have to install gecko, since the license is rendered as HTML.

To install it (on 64 bit enable [multilib])

```
pacman -S wine_gecko

```

In some versions of Wine, you can not agree to the terms even though you scrolled down. Try to compile the latest Wine from source. Or use a version of Wine it is known to work with, i.e. 1.1.39, **1.7.10** (please add more here).

##### Wine crashes while reading terms

Wine crashes as soon as the terms which must be agreed to install the game opens. This is because the installer fetches the terms from a website somewhere, and therefore uses a browser implementation to show them. Wine's implementation of this is named [Gecko [http://wiki.winehq.org/Gecko](http://wiki.winehq.org/Gecko)], and this must be installed in order for the installation to work!

##### Battle.net cannot connect

The new (V5) battle.net installer will not be able to connect without libldap. To install:

```
 pacman -S lib32-libldap

```

##### Error Message: This application failed to start because it could not find or load the qt platform plugin windows

Use winecfg to change Battle.net.exe to use Windows XP mode.

### Copying the CDs to a folder

This method's goal is to copy the 5 install CDs to a folder. This seems to solve problems with deciding whether a CD is mounted and needs changing or not ; I think this is a fundamental problem because Windows does not have the basic concept of mounting and unmounting drives.

```
mkdir /mnt/temp
cd /mnt/temp

```

```
mount /mnt/cdrom
cp -R /mnt/cdrom/* /mnt/temp
umount /mnt/cdrom
(repeat above for each of the 5 CDs)

```

Then run the World of Warcraft Installer with :

```
 wine Installer.exe

```

### Copying an Existing Installation

The third is to simply copy an exisiting WoW installation from a Windows drive to Linux.

**NOTE:** If you do not alreay have Wine installed, or have not run World of Warcraft with Wine before, you should skip down to [#Installing Wine](#Installing_Wine), then come back to this section. *Please DO NOT SKIP this section unless you are absolutely sure you know what you are doing.*

Copy the C:\Program Files\World of Warcraft directory from Windows to ~/.wine/drive_c/Program Files/World of Warcraft.

Example (assuming your windows partition is mounted at `/mnt/windows` and you are in your home directory) (Quotes are needed because of the spaces in the file names):

```
 cp -R "/mnt/windows/Program Files/World of Warcraft" ".wine/drive_c/Program Files/World of Warcraft"

```

This will ensure that Wine knows about your WoW and will be able to configure it properly, and also ensures that WoW will not notice it has even been moved at all.

Now that you have WoW installed, skip down to [#Post-Installation](#Post-Installation).

### New Installation from CD

**NOTE:** We will assume that your Wine CD-ROM drive is "D:\" for this guide. Please use the correct letter as set up in the [#Installing Wine](#Installing_Wine) section.

Insert the first CD, mount it, and start the installation with:

```
 wine "D:\Installer.exe"

```

When it asks for the next cd, simply unmount your CD drive and mount the next CD. Make absolutely sure that you mount the CD before telling the installer to load the CD, or it may make the installation fail. If you have any issues installing using the CDs, please read the next section.

The WoW installation uses all 5 CDs, so it will take a while. Go outside and get some fresh air while the CD loads, because soon you will not have any "free time". :P

### New Installation from DVD

**NOTE:** Note that on some WoW DVD's the installer executable is hidden and you need to mount the disc with the 'unhide' option. To do this type in a terminal:

```
mount -t iso9660 -o ro,unhide /dev/cdrom /media/cdrom/

```

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

## Installing Patches

Now we will need to update WoW. As of Noevember 30th 2010, the latest version of World of Warcraft is 4.0.3.13329\. This will change over time, of course. The best place I have found to access the latest patches is [http://www.wowpedia.org/Patch_mirrors](http://www.wowpedia.org/Patch_mirrors)

I think the simplest way of updating World of Warcraft is to download the patches (links are at the Patch Wiki) and copy them into the working directory for World of Warcraft. I have had problems with the Blizzard Downloaders either not working at all, or working very slowly. If you download them, you can reuse them if you reinstall or have an accident.

When you have downloaded the files into their own folder for neatness, copy these patches into the World of Warcraft working directory.

```
cp * ~/.wine/drive_c/Program\ Files/World\ of\ Warcraft/

```

The 1.12.x patch needs to be unzipped into the working directory

```
 cd ~/.wine/drive_c/Program\ Files/World\ of\ Warcraft/
 unzip wow-1.12.x-to-2.0.1-engb-patch-3.zip

```

The simplest way to install the patches seems to be to run World of Warcraft. It detects that you have downloaded the patches and does not do it again.

```
 cd ~/.wine/drive_c/Program\ Files/World\ of\ Warcraft/
 wine WoW.exe

```

You have to keep going round 5 times, it does get a bit dull, but it is fairly reliable. Accept the offer to Install the Gecko renderer when it comes up on your first patch install.

The original Wiki says you can install patches with Wine as follows:

```
wine wow-VERSION-LANG-patch.exe

```

This method is currently still working.

If the Launcher (it displays a little box with News and Play) seems to stop when downloading, close its window and re-run WoW.exe

**UPDATED for 4.3**

If the Launcher crashes when downloading patches start backgrounddownloader and deactivate peer to peer and restart the launcher. Now everything will download and install.

## Configuration

The World of Warcraft configuration file is kept in the WTF directory (do Blizzard have a sense of humour ?)

Edit it with

```
gedit WTF/Config.wtf

```

### Using OpenGL

Add the following line which makes WoW run in OpenGL instead of DirectX Mode. Doing so though will result in lower quality graphics as it appears the OpenGL renderer isn't updated as frequently. D3D9 has more graphical features (like stencil shadows, liquid water, sunshafts) and higher shader model.

```
SET gxApi "opengl"

```

If you run Intel/AMD on the open source Mesa drivers and the game crashes on launch due to an access violation, you may need to force WoW to use OpenGL 3.3\. Add this to your startup script:

```
export MESA_GL_VERSION_OVERRIDE=3.3COMPAT

```

### Resolution and Colour depth

You can change the following two lines to set the default WoW resolution. I have a 19" Monitor so I can use the following.

```
SET gxColorBits "24"
SET gxResolution "1440x900"

```

### Windowing

You can run in a Window by setting this, which is confirmed to work in Wine.

```
SET gxWindow "1" 

```

### Black textures issue

If you're using an Intel graphics card and you can see black textures in the game (or the game crashes in OpenGL mode), you should enable S3TC texture compression support. It can be enabled through [driconf](https://www.archlinux.org/packages/?name=driconf) or by installing [libtxc_dxtn](https://www.archlinux.org/packages/?name=libtxc_dxtn).

### Sound Issues

#### Configuring the Buffer

If the sound makes a horrendous racket with squeaks and white noise try :

```
SET SoundOutputSystem "1" 
SET SoundBufferSize "100"

```

#### Stuttering or Static Sound

Run `winecfg`, and in the "Audio" tab, selected "OSS" as the sound driver, using "Standard" hardware acceleration and driver emulation enabled.

You can also set WoW to run at a higher "nice level", which will usually improve sound performance (`renice` must be run as root):

```
sudo renice -15 `pidof WoW.exe`

```

## Performance Tweaks

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

You can also find [this](http://appdb.winehq.org/objectManager.php?bIsQueue=false&bIsRejected=false&sClass=comment&sAction=add&sReturnTo=http%3A%2F%2Fappdb.winehq.org%2FobjectManager.php%3FsClass%3Dversion%26amp%3BiId%3D25610&sTitle=Post+new+comment&iVersionId=25610&iThread=80686) comment on WineHQ very useful. It can double your FPS.

### For NVIDIA users

As of version 310.14 of the nvidia driver, an option exists for threaded OpenGL performance optimization. WoW benefits greatly from utilizing this.

(Sidenote: this makes the 'RGL' patch/library/hack redundant for nVidia users)

Exporting __GL_THREADED_OPTIMIZATIONS=1 enables the optimizations. Example of launching WoW with these optimizations:

```
__GL_THREADED_OPTIMIZATIONS=1 wine Wow.exe -opengl

```

Once you've confirmed the game works well for you (applies to any game, not just WoW) you can turn off debugging output to potentially improve performance further:

```
WINEDEBUG=-all __GL_THREADED_OPTIMIZATIONS=1 wine Wow.exe -opengl $> /dev/null

```

#### NVIDIA users and Direct3D mode

If running the game in Direct3D mode, in conjunction with the above optimization, compiling Wine with the [*"Use glBufferSubDataARB for dynamic buffer uploads"*](http://bugs.winehq.org/show_bug.cgi?id=11674#c263) patch should yield a further performance increase. This patch does not appear to increase performance in OpenGL mode, though OpenGL mode generally results in higher framerates anyway... albeit at the cost of the game's more advanced Direct3D eye candy.

**NOTE: You MUST turn off Wine's debugging to benefit from this**

```
WINEDEBUG=-all __GL_THREADED_OPTIMIZATIONS=1 wine Wow.exe

```

#### GLXUnsupportedPrivateRequest Problem

On 64 bit systesm, if you're using bumblebee and using optirun to run game with Nvidia Graphic card on your system, you will encounter this error:

```
X Error of failed request:  GLXUnsupportedPrivateRequest

```

In most cases installing [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) will solve this problem. [bbs](https://bbs.archlinux.org/viewtopic.php?pid=1381891#p1381891)

### AMD CPU users=

As WoW significant benefits from L3-Cache you should check if your Processor/Bios has a L3-allocation Option available, BSP-Only allocation is what worked for me pretty well. By switching from all-cores allocation to BSP-only the FPS on my system did jump from ~70 outdoors to over 120+. This was done on a II X4 640 with Nvidia Graphics Card(proprietary driver) using -opengl and the thread optimization.

### CPU/I-O Schedulers=

You can greatly increase World of Warcraft performance by choosing the right schedulers for your machine. Currently, the most-recent version of wine in the official repositories is not configured to fully take advantage of the linux-ck kernel. Instead, it is recommended that wine gamers use the CFS scheduler. Also, World of Warcraft runs better with the deadline I/O scheduler (as opposed to noop, cfq, bfq, etc). You can check if you will benefit from switching I/O schedulers first by determining which I/O scheduler you are using on your drive:

```
# fdisk -l *to determine the hard drive arch is installed on*
# cat /sys/block/sdX/queue/scheduler *Where X is the letter of the drive fdisk reports*
# echo deadline > /sys/block/sdX/queue/scheduler

```

This is a temporary fix (it does not set deadline permanently), but you may gain an additional 5-30fps, by enabling deadline as the I/O scheduler. Moreover, feel free to play around with other schedulers to pick the one which runs best on your machine, especially if you have an SSD

## Links

*   [World of Warcraft in the Wine AppDB](https://appdb.winehq.org/objectManager.php?sClass=application&iId=1922)
*   [Wowpedia](http://www.wowpedia.org/Main_Page)
*   [Patch Mirrors](http://www.wowpedia.org/Patch_mirrors)