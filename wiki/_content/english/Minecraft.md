Minecraft is a game about breaking and placing blocks. At first, people built structures to protect against nocturnal monsters, but as the game grew players worked together to create wonderful, imaginative things.

## Contents

*   [1 Client](#Client)
    *   [1.1 Installation](#Installation)
    *   [1.2 Running](#Running)
    *   [1.3 Firewall configuration for LAN worlds](#Firewall_configuration_for_LAN_worlds)
    *   [1.4 Extras](#Extras)
*   [2 Server](#Server)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Setup](#Setup)
        *   [2.2.1 Introduction](#Introduction)
        *   [2.2.2 Starting the server](#Starting_the_server)
        *   [2.2.3 Server management script](#Server_management_script)
        *   [2.2.4 Tweaking](#Tweaking)
    *   [2.3 Spigot (respectively Craftbukkit)](#Spigot_.28respectively_Craftbukkit.29)
    *   [2.4 Cuberite](#Cuberite)
    *   [2.5 Additional notes](#Additional_notes)
*   [3 Minecraft Mod Launchers](#Minecraft_Mod_Launchers)
    *   [3.1 Feed The Beast](#Feed_The_Beast)
    *   [3.2 Technic Launcher](#Technic_Launcher)
*   [4 See also](#See_also)

## Client

### Installation

Simply install the [minecraft](https://aur.archlinux.org/packages/minecraft/) package to get the official game launcher, a script to launch it and a proper `.desktop` file.

Though using a proper package should always be preferred, there is still the options to use the plain minecraft launcher which can be found at the [official download page](https://minecraft.net/download).

### Running

If you installed Minecraft from the AUR, you can use the included script:

```
$ minecraft

```

Otherwise, you will need to manually launch Minecraft:

```
$ java -jar Minecraft.jar

```

### Firewall configuration for LAN worlds

To host a Minecraft world on the LAN you will need two ports to be open on your [firewall](/index.php/Firewall "Firewall"):

*   UDP port `4445`. If this port is closed, the game will hang when you save and exit from the world;
*   the TCP port minecraft randomly picks after you open your world to LAN. If this port is closed, your friends won't be able to join your world.

### Extras

There are several [programs and editors](http://www.minecraftwiki.net/wiki/Programs_and_editors) which can make your Minecraft experience a little easier to navigate. The most common of these programs are map generators. Using one of these programs will allow you to load up a Minecraft world file and render it as a 2D image, providing you with a top-down map of the world.

*   AMIDST (Advanced Minecraft Interface and Data/Structure Tracking) is a program that aids in the process of finding structures, biomes, and players in Minecraft worlds. It can draw the biomes of a world out and show where points of interest are likely to be by either giving it a seed, telling it to make a random seed, or having it read the seed from an existing world (in which case it can also show where players in that world are). [amidst](https://aur.archlinux.org/packages/amidst/) is available in the [AUR](/index.php/AUR "AUR"). Bear in mind that AMIDST is currently unmaintained due to its main author being busy with work and other real life obligations. The primary fork is "Amidst Exporter" and has an AUR package at [amidstexporter](https://aur.archlinux.org/packages/amidstexporter/). This is notably updated to include a patch for calculating Ocean Monument locations in 1.8+ worlds.

*   Mapcrafter is a high performance Minecraft map renderer which renders worlds to maps with an 3D-isometric perspective. You can view these maps in any webbrowser and you can host them with a webserver for example for the players of your server. Mapcrafter has a simple configuration file format to specify worlds to render, different rendermodes such as day/night/cave and can also render worlds from different rotations. [mapcrafter-git](https://aur.archlinux.org/packages/mapcrafter-git/) is available in the [AUR](/index.php/AUR "AUR").

*   Minutor is described as a minimalistic map generator for Minecraft. Do not let this mislead you, it generates maps of existing worlds, not the other way around. You are provided with a simple GTK+ based interface for viewing your world. Several rendering modes are available, as well as custom coloring modes and the ability to slice through z-levels. [minutor](https://aur.archlinux.org/packages/minutor/) is available in the [AUR](/index.php/AUR "AUR").

## Server

### Installation

The simplest way to install the Minecraft server on an Arch Linux system is by using the [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) package. It provides additional [SystemD](/index.php/SystemD "SystemD") unit files and includes a small control script.

**Note:** Almost all Minecraft servers will require [Java](/index.php/Java "Java") in order to run, except for [Cuberite](#Cuberite) which is written in C++ and Lua. Some people (apparently especially on ARMv7 machines) have reported that the server doesn't run well, if at all, using the OpenJDK packages and have reported success using the Oracle Java packages ([jdk-arm](https://aur.archlinux.org/packages/jdk-arm/)) instead. Your mileage may vary.

### Setup

#### Introduction

In the installation process the `minecraft` user and group is introduced. Establishing a Minecraft-specific user is recommended for security reasons. By running Minecraft under an unprivileged user account, anyone who successfully exploits your Minecraft server will only get access to that user account, and not yours. However you may safely add your user to the `minecraft` group and add group write permission to the directory `/srv/minecraft` (default) to modify Minecraft server settings. Make sure that all files in the `/srv/minecraft` directory are either owned by the `minecraft` user, or that the user has by other means r/w permissions. The server will error out if it is unable to access certain files and might even have insufficient rights to write an according error message to the log.

The package provides a systemd service and timer to take automatic backups. The backups are located in the `backup` folder under the server root directory by default. The related systemd files reside under `/usr/lib/systemd/system/minecraftd-backup.timer` and `/usr/lib/systemd/system/minecraftd-backup.service`. They may easily be adapted to your liking, e.g. a custom backup interval.

#### Starting the server

To start the server you may either use systemd or run it directly from the command line. Either way the server is encapsulated in a [screen](/index.php/Screen "Screen") session which is owned by the `minecraft` user. Using systemd you may [start](/index.php/Start "Start") and enable the included `minecraftd.service`. Alternatively run

```
# minecraftd start

```

**Note:** If you run the server for the first time an [EULA](https://en.wikipedia.org/wiki/EULA "wikipedia:EULA") file residing under `/srv/minecraft/eula.txt` gets created. You will need to edit this file to state that you have agreed to the contract in order to run the server.

#### Server management script

To easily control the server you may use the provided `minecraftd` script. It is capable of doing the basic commands like `start`, `stop`, `restart` or attaching to the session with `console`. Moreover it may be used to display status information with `status`, backup the server world directory with `backup`, restore world data from backups with `restore` or run single commands in the server console with `command <server command>`.

**Note:** Regarding the server `console`, remember that you can exit any screen session with `ctrl+a` `d`.

#### Tweaking

To tweak the default settings (e.g. the maximum RAM, number of threads etc.) edit the file `/etc/conf.d/minecraft`.

More advanced users may wish enable `IDLE_SERVER` by setting it to true in `/etc/conf.d/minecraft`. This will enable the management script to suspend the server if no player was online for at least `IDLE_IF_TIME` (defaults to 20 minutes). When the server is suspended an `idle_server` will listen on the Minecraft port using `netcat` and will immediately start the server at the first incoming connection. Though this obviously delays joining for the first time, it significantly decreases the CPU and memory usage, leading to more reasonably resource/power consumption.

### Spigot (respectively Craftbukkit)

Spigot is the most widely-used **modded** Minecraft server in the world, hence there is a [spigot](https://aur.archlinux.org/packages/spigot/) package in the [AUR](/index.php/AUR "AUR"). The spigot PKGBUILD builds on top of the files from the [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) package. This means that the spigot server as well provides its own systemd unit files, spigot script and the corresponding script configuration file. The binary is called `spigot` and is capable of fulfilling the same commands as `minecraftd` and the configuration file resides under `/etc/conf.d/spigot`.

Be sure read [#Setup](#Setup) and replace `minecraftd` with `spigot` wherever you encounter it.

It is somewhat affiliated with [Bukkit](http://bukkit.org/) and has grown in popularity since Bukkit's demise.

### Cuberite

[Cuberite](http://cuberite.org/) is a highly efficient Minecraft compatible server written in C++ and Lua. It achieves better performances than the vanilla Minecraft server plus it is extensively moddable. The [cuberite](https://aur.archlinux.org/packages/cuberite/) package is available in the [AUR](/index.php/AUR "AUR"). The program provides a simple web interface by default at port `8080` with which most server operations can easily be done through the browser. The cuberite PKGBUILD as well builds on top of the files from the [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) package. This means that the cuberite server provides its own systemd unit files, cuberite script and the corresponding script configuration file. The binary is called `cuberite` and is capable of fulfilling the same commands as `minecraftd` and the configuration file resides under `/etc/conf.d/cuberite`.

Be sure read [#Setup](#Setup) and replace `minecraftd` with `cuberite` wherever you encounter it.

### Additional notes

*   There are several server wrappers available providing everything from automatic backup to managing dozens of servers in parallel, refer to [Server Wrappers](http://www.minecraftwiki.net/wiki/Programs_and_editors#Server_Wrappers) for more information. However the management script provided by the AUR packages should suffice most needs.
*   You might want to set up a [systemd timer](/index.php/Systemd/Timers "Systemd/Timers") with e.g. [mapper](http://www.minecraftwiki.net/wiki/Programs_and_editors#Mappers) to generate periodic maps of your world.
*   Remember to take periodic backups, e.g. using [rsync](/index.php/Rsync "Rsync") or the provided management script.

## Minecraft Mod Launchers

You can launch Minecraft from different "Launchers" that often include an array of Mod Packs to enchance one's gameplay and add [mods](http://minecraft.gamepedia.com/Mods).

### Feed The Beast

[feedthebeast](https://aur.archlinux.org/packages/feedthebeast/) includes the Feed The Beast launcher. The official page for Feed The Beast is: [feed-the-beast.com](https://www.feed-the-beast.com/)

### Technic Launcher

[minecraft-technic-launcher](https://aur.archlinux.org/packages/minecraft-technic-launcher/) includes the Technic Launcher. The official page for Technic Launcher is: [technicpack.net](http://www.technicpack.net/)

## See also

*   [Official Minecraft site](https://www.minecraft.net/)
*   [Minecraft community links](https://www.minecraft.net/community)
*   [Minecraft Client and Server download link](https://minecraft.net/download)
*   [Crafting Recipes](http://www.minecraftwiki.net/wiki/Crafting)
*   [Block and item data values](http://www.minecraftwiki.net/wiki/Data_values)
*   [Reddit Minecraft community](http://www.reddit.com/r/minecraft)
*   [Minecraft Skins](http://www.minecraftskins.net)