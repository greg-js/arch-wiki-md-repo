[Minecraft](https://minecraft.net/en-us/) is a game about breaking and placing blocks. At first, people built structures to protect against nocturnal monsters, but as the game grew players worked together to create wonderful, imaginative things.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Client](#Client)
    *   [1.1 Installation](#Installation)
    *   [1.2 Firewall configuration for LAN worlds](#Firewall_configuration_for_LAN_worlds)
*   [2 Server](#Server)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Setup](#Setup)
        *   [2.2.1 Introduction](#Introduction)
        *   [2.2.2 Starting the server](#Starting_the_server)
        *   [2.2.3 Server management script](#Server_management_script)
        *   [2.2.4 Tweaking](#Tweaking)
    *   [2.3 Alternative servers](#Alternative_servers)
        *   [2.3.1 Spigot (respectively Craftbukkit)](#Spigot_(respectively_Craftbukkit))
        *   [2.3.2 Cuberite](#Cuberite)
        *   [2.3.3 PaperMC](#PaperMC)
        *   [2.3.4 Forge](#Forge)
    *   [2.4 Additional notes](#Additional_notes)
*   [3 Minecraft mod launchers](#Minecraft_mod_launchers)
*   [4 Other programs and editors](#Other_programs_and_editors)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Server on ARM devices](#Server_on_ARM_devices)
    *   [5.2 Client Wayland support](#Client_Wayland_support)
    *   [5.3 Client or server does not start](#Client_or_server_does_not_start)
    *   [5.4 Broken fonts with MinecraftForge](#Broken_fonts_with_MinecraftForge)
    *   [5.5 MultiMC unable to build](#MultiMC_unable_to_build)
*   [6 See also](#See_also)

## Client

### Installation

The minecraft client can be installed via the [minecraft-launcher](https://aur.archlinux.org/packages/minecraft-launcher/) package. It provides the official game launcher, a script to launch it and a `.desktop` file. The package is officially recommended by Mojang on their website.

Alternatively, it can also be installed via the [minecraft](https://aur.archlinux.org/packages/minecraft/) package.

### Firewall configuration for LAN worlds

To host a Minecraft world on the LAN you will need two ports to be open on your [firewall](/index.php/Firewall "Firewall"):

*   UDP port `4445`. If this port is closed, the game will hang when you save and exit from the world;
*   the TCP port minecraft randomly picks after you open your world to LAN. If this port is closed, other players won't be able to join your world.

## Server

### Installation

Minecraft server can be installed via the [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) package. It provides additional [systemd](/index.php/Systemd "Systemd") unit files and includes a small control script.

Also see [#Alternative servers](#Alternative_servers) for an overview of alternative programs allowing to host Minecraft.

### Setup

#### Introduction

In the installation process the `minecraft` user and group is introduced. Establishing a Minecraft-specific user is recommended for security reasons. By running Minecraft under an unprivileged user account, anyone who successfully exploits your Minecraft server will only get access to that user account, and not yours. However you may safely add your user to the `minecraft` group and add group write permission to the directory `/srv/minecraft` (default) to modify Minecraft server settings. Make sure that all files in the `/srv/minecraft` directory are either owned by the `minecraft` user, or that the user has by other means read and write permissions. The server will error out if it is unable to access certain files and might even have insufficient rights to write an according error message to the log.

The package provides a systemd service and timer to take automatic backups. By default the backups are located in the `backup` folder under the server root directory. Though to keep the disk footprint small only the 10 most recent backups are preserved (configurable via `KEEP_BACKUPS`). The related systemd files are `minecraftd-backup.timer` and `minecraftd-backup.service`. They may easily be [adapted](/index.php/Edit "Edit") to your liking, e.g. to follow a custom backup interval.

#### Starting the server

To start the server you may either use systemd or run it directly from the command line. Either way the server is encapsulated in a [GNU Screen](/index.php/GNU_Screen "GNU Screen") session which is owned by the `minecraft` user. Using systemd you may [start](/index.php/Start "Start") and enable the included `minecraftd.service`. Alternatively run

```
# minecraftd start

```

**Note:** If you run the server for the first time an [EULA](https://en.wikipedia.org/wiki/EULA "wikipedia:EULA") file residing under `/srv/minecraft/eula.txt` gets created. You will need to edit this file to state that you have agreed to the contract in order to run the server.

#### Server management script

To easily control the server you may use the provided `minecraftd` script. It is capable of doing basic commands like `start`, `stop`, `restart` or attaching to the session with `console`. Moreover it may be used to display status information with `status`, backup the server world directory with `backup`, restore world data from backups with `restore` or run single commands in the server console with `command *do-something*`.

**Note:** Regarding the server console (reachable via `minecraftd console`), remember that you can exit any GNU screen session with `ctrl+a` `d`.

#### Tweaking

To tweak the default settings (e.g. the maximum RAM, number of threads etc.) edit the file `/etc/conf.d/minecraft`.

For example, more advanced users may wish to enable `IDLE_SERVER` by setting it to `true`. This will enable the management script to suspend the server if no player was online for at least `IDLE_IF_TIME` (defaults to 20 minutes). When the server is suspended an `idle_server` will listen on the Minecraft port using [ncat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ncat.1) (also called netcat or simply nc for short) and will immediately start the server at the first incoming connection. Though this obviously delays joining for the first time after suspension, it significantly decreases the CPU and memory usage leading to more reasonable resource and power consumption levels.

**Note:** If running for the first time with this option enabled, the `/srv/minecraft/eula.txt` file will not get created. You need to disable it to initially start.

### Alternative servers

#### Spigot (respectively Craftbukkit)

[Spigot](https://www.spigotmc.org/) is the most widely-used **modded** Minecraft server in the world. It can be installed as [spigot](https://aur.archlinux.org/packages/spigot/) via the [AUR](/index.php/AUR "AUR"). The spigot PKGBUILD builds on top of the files from the [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) package. This means that the spigot server provides its own systemd unit files, spigot script and corresponding script configuration file. The binary is called `spigot` and is capable of fulfilling the same commands as `minecraftd`. The configuration file resides under `/etc/conf.d/spigot`.

Be sure to read [#Setup](#Setup) and replace `minecraftd` with `spigot` wherever you encounter it.

It is somewhat affiliated with [Bukkit](http://bukkit.org/) and has grown in popularity since Bukkit's demise.

#### Cuberite

[Cuberite](https://cuberite.org/) is a highly efficient and extensively moddable Minecraft server, written in C++ and Lua. It achieves much better performances than the vanilla Minecraft server, but is not fully compatible with the latest Minecraft client (some game aspects might be missing or not working).

Cuberite minecraft server can be installed as a [cuberite](https://aur.archlinux.org/packages/cuberite/) package, which provides a simple web interface by default at port `8080` with which most server operations can easily be done through the browser. The cuberite PKGBUILD builds on top of the files from the [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) package. This means that the cuberite server provides its own systemd unit files, cuberite script and corresponding script configuration file. The binary is called `cuberite` and is capable of fulfilling the same commands as `minecraftd`. The configuration file resides under `/etc/conf.d/cuberite`.

Be sure to read [#Setup](#Setup) and replace `minecraftd` with `cuberite` wherever you encounter it.

#### PaperMC

[PaperMC](https://papermc.io) is a Minecraft server, compatible with Spigot plugins which aims to offer better performance. It can be installed via [papermc](https://aur.archlinux.org/packages/papermc/).

Be sure to read [#Setup](#Setup) and replace `minecraftd` with `papermc` wherever you encounter it.

#### Forge

[Forge](https://minecraftforge.net) is a widely used Minecraft modding API. The following server packages are available:

*   [forge-server](https://aur.archlinux.org/packages/forge-server/) for the latest Minecraft version
*   [forge-server-1.12.2](https://aur.archlinux.org/packages/forge-server-1.12.2/) for Minecraft 1.12.2
*   [forge-server-1.11.2](https://aur.archlinux.org/packages/forge-server-1.11.2/) for Minecraft 1.11.2
*   [forge-server-1.10.2](https://aur.archlinux.org/packages/forge-server-1.10.2/) for Minecraft 1.10.2
*   [forge-server-1.9.4](https://aur.archlinux.org/packages/forge-server-1.9.4/) for Minecraft 1.9.4
*   [forge-server-1.8.9](https://aur.archlinux.org/packages/forge-server-1.8.9/) for Minecraft 1.8.9
*   [forge-server-1.7.10](https://aur.archlinux.org/packages/forge-server-1.7.10/) for Minecraft 1.7.10
*   [forge-server-1.6.4](https://aur.archlinux.org/packages/forge-server-1.6.4/) for Minecraft 1.6.4
*   [forge-server-1.5.2](https://aur.archlinux.org/packages/forge-server-1.5.2/) for Minecraft 1.5.2

Be sure to read [#Setup](#Setup) and replace `minecraftd` with `forged` wherever you encounter it.

### Additional notes

*   There are several server wrappers available providing everything from automatic backup to managing dozens of servers in parallel, refer to [Server Wrappers](http://www.minecraftwiki.net/wiki/Programs_and_editors#Server_Wrappers) for more information. However the management script provided by the AUR packages should suffice most needs.
*   You might want to set up a [systemd timer](/index.php/Systemd/Timers "Systemd/Timers") with e.g. [mapper](http://www.minecraftwiki.net/wiki/Programs_and_editors#Mappers) to generate periodic maps of your world.
*   Be sure to take periodic backups e.g. using the provided management script (see [#Introduction](#Introduction)) or plain [rsync](/index.php/Rsync "Rsync").

## Minecraft mod launchers

You can launch Minecraft from different so called *launchers* that often include an array of mod packs to enhance one's gameplay and add [mods](http://minecraft.gamepedia.com/Mods).

*   **Feed The Beast** — Originated as a custom challenge map in Minecraft that made heavy use of multiple tech mods and evolved into a mod package launcher.

	[https://www.feed-the-beast.com/](https://www.feed-the-beast.com/) || [feedthebeast](https://aur.archlinux.org/packages/feedthebeast/)

*   **MultiMC** — Sandbox environment manager for separable pack association.

	[https://multimc.org/](https://multimc.org/) || [multimc5](https://aur.archlinux.org/packages/multimc5/) and [multimc-git](https://aur.archlinux.org/packages/multimc-git/)

*   **Technic Launcher** — Modpack installer with a focus on mod discovery via popularity rankings.

	[http://www.technicpack.net/](http://www.technicpack.net/) || [minecraft-technic-launcher](https://aur.archlinux.org/packages/minecraft-technic-launcher/)

## Other programs and editors

There are several [programs and editors](http://www.minecraftwiki.net/wiki/Programs_and_editors) which can make your Minecraft experience a little easier to navigate. The most common of these programs are map generators. Using one of these programs will allow you to load up a Minecraft world file and render it as a 2D image, providing you with a top-down map of the world.

*   AMIDST (Advanced Minecraft Interface and Data/Structure Tracking) ([amidst](https://aur.archlinux.org/packages/amidst/)) is a program that aids in the process of finding structures, biomes, and players in Minecraft worlds. It can draw the biomes of a world out and show where points of interest are likely to be by either giving it a seed, telling it to make a random seed, or having it read the seed from an existing world (in which case it can also show where players in that world are). The project has been forked in the past, of which the most notable one is "Amidst Exporter" ([amidstexporter](https://aur.archlinux.org/packages/amidstexporter/)) which includes a patch for calculating Ocean Monument locations in 1.8+ worlds.

*   Mapcrafter ([mapcrafter-git](https://aur.archlinux.org/packages/mapcrafter-git/)) is a high performance Minecraft map renderer written in C++ which renders worlds to maps with an 3D-isometric perspective. You can view these maps in any webbrowser hence they are easily deployed on one's server. Mapcrafter has a simple configuration file format to specify worlds to render, different rendermodes such as day/night/cave and can also render worlds from different rotations.

*   Minutor ([minutor-git](https://aur.archlinux.org/packages/minutor-git/)) is a minimalistic map generator for Minecraft. You are provided with a simple GTK based interface for viewing your world. Several rendering modes are available, as well as custom coloring modes and the ability to slice through z-levels.

## Troubleshooting

### Server on ARM devices

Minecraft server should run without any issues on [ARM](https://archlinuxarm.org/) devices with latest [Java](/index.php/Java "Java"), such as [jre10-openjdk-headless](https://www.archlinux.org/packages/?name=jre10-openjdk-headless). However, if you encounter any issues, try using [jdk-arm](https://aur.archlinux.org/packages/jdk-arm/) instead. Also consider [#Cuberite](#Cuberite) server as an alternative.

### Client Wayland support

Wayland and other window managers are currently not supported with Minecraft, as Minecraft has the prerequisite of [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) and should be opened with xorg.

### Client or server does not start

It might be the problem with [Java](/index.php/Java "Java") version. Java version 8 is guaranteed to work well in all cases.

Both Minecraft server and the actual game work perfectly fine with the latest version of [Java](/index.php/Java "Java"), such as [jre10-openjdk](https://www.archlinux.org/packages/?name=jre10-openjdk), but the Minecraft game launcher (and possibly all other mods) might only work with the [Java](/index.php/Java "Java") version 8.

### Broken fonts with MinecraftForge

Force Unicode fonts from the language menu.

Since you can't read any of the menu options: in the main menu, choose the bottom-left most button is Options, second-from-the-bottom on the left side is the Language Button. From there, the Force Unicode Font button is on the bottom, on the left side.

### MultiMC unable to build

If you are trying to install [multimc5](https://aur.archlinux.org/packages/multimc5/) and get an error similar to:

```
No CMAKE_Java_COMPILER could be found.
Tell CMake where to find the compiler by setting either the environment
variable "JAVA_COMPILER" or the CMake cache entry CMAKE_Java_COMPILER to
the full path to the compiler, or to the compiler name if it is in the
PATH.

```

The error could be caused by Java missing, which can be fixed by installing [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk). If the error is not fixed by that or Java was properly installed in the first place, the wrong version could still be the default environment:

 `$ archlinux-java status` 
```
Available Java environments:
  java-13-openjdk (default)
  java-8-openjdk

```

You can set the default java version using `archlinux-java set <version>`.

## See also

*   [Official Minecraft site](https://www.minecraft.net/)
*   [Minecraft community links](https://www.minecraft.net/community)
*   [Minecraft Client and Server download link](https://minecraft.net/download)
*   [Crafting Recipes](http://www.minecraftwiki.net/wiki/Crafting)
*   [Block and item data values](http://www.minecraftwiki.net/wiki/Data_values)
*   [Reddit Minecraft community](http://www.reddit.com/r/minecraft)
*   [Minecraft Skins](http://www.minecraftskins.net)