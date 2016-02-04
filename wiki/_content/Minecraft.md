# Minecraft

Minecraft is a game about breaking and placing blocks. At first, people built structures to protect against nocturnal monsters, but as the game grew players worked together to create wonderful, imaginative things.

## Contents

*   [1 Client](#Client)
    *   [1.1 Installation](#Installation)
    *   [1.2 Running](#Running)
    *   [1.3 Extras](#Extras)
*   [2 Server](#Server)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Setup](#Setup)
    *   [2.3 Spigot (respectively Craftbukkit)](#Spigot_.28respectively_Craftbukkit.29)
    *   [2.4 Additional notes](#Additional_notes)
*   [3 See also](#See_also)

## Client

### Installation

[minecraft](https://aur.archlinux.org/packages/minecraft/) includes the official game launcher and a script to launch it. Otherwise, just get the launcher on the [official download site](https://minecraft.net/download).

### Running

If you installed Minecraft from the AUR, you can use the included script:

```
$ minecraft

```

Otherwise, you will need to manually launch Minecraft:

```
$ java -jar Minecraft.jar

```

### Extras

There are several [programs and editors](http://www.minecraftwiki.net/wiki/Programs_and_editors) which can make your Minecraft experience a little easier to navigate. The most common of these programs are map generators. Using one of these programs will allow you to load up a Minecraft world file and render it as a 2D image, providing you with a top-down map of the world.

*   AMIDST (Advanced Minecraft Interface and Data/Structure Tracking) is a program that aids in the process of finding structures, biomes, and players in Minecraft worlds. It can draw the biomes of a world out and show where points of interest are likely to be by either giving it a seed, telling it to make a random seed, or having it read the seed from an existing world (in which case it can also show where players in that world are). [amidst](https://aur.archlinux.org/packages/amidst/) is available in the [AUR](/index.php/AUR "AUR"). Bear in mind that AMIDST is currently unmaintained due to its main author being busy with work and other real life obligations. The primary fork is "Amidst Exporter" and has an AUR package at [amidstexporter](https://aur.archlinux.org/packages/amidstexporter/). This is notably updated to include a patch for calculating Ocean Monument locations in 1.8+ worlds.

*   Mapcrafter is a high performance Minecraft map renderer which renders worlds to maps with an 3D-isometric perspective. You can view these maps in any webbrowser and you can host them with a webserver for example for the players of your server. Mapcrafter has a simple configuration file format to specify worlds to render, different rendermodes such as day/night/cave and can also render worlds from different rotations. [mapcrafter-git](https://aur.archlinux.org/packages/mapcrafter-git/) is available in the [AUR](/index.php/AUR "AUR").

*   Minutor is described as a minimalistic map generator for Minecraft. Do not let this mislead you, it generates maps of existing worlds, not the other way around. You are provided with a simple GTK+ based interface for viewing your world. Several rendering modes are available, as well as custom coloring modes and the ability to slice through z-levels. [minutor](https://aur.archlinux.org/packages/minutor/) is available in the [AUR](/index.php/AUR "AUR").

## Server

### Installation

**Note:** Regardless of how you install the Minecraft server, it will need [Java](/index.php/Java "Java") to run. Some people (apparently especially on ARMv7 machines) have reported that the server doesn't run well, if at all, using the OpenJDK packages and have reported success using the Oracle Java packages ([jdk-arm](https://aur.archlinux.org/packages/jdk-arm/)) instead. Your mileage may vary.

The simplest way to install the Minecraft server on an Arch Linux system is by using the [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) package. It provides additional systemd unit files and includes a small control script.

### Setup

In the installation process the `minecraft` user and group is introduced. Establishing a Minecraft-specific user is recommended for security. By running Minecraft under an unprivileged user account, anyone who successfully exploits your Minecraft server will only get access to that user account, and not yours. However you may safely add your user to the `minecraft` group and add group write permission to the directory `/srv/minecraft` to modify Minecraft server settings. Make sure that all files in the `/srv/minecraft` directory are either owned by the `minecraft` user, or have r/w permissions for all three groups (user,group,other), otherwise the server will error out.

To start the server you may either use systemd or run it directly from the command line. Either way it the server is encapsulated in a [screen](/index.php/Screen "Screen") session which is owned by the `minecraft` user. Using systemd you may [start](/index.php/Start "Start") and enable the included `minecraftd.service`. Alternatively run

```
# minecraftd start

```

**Note:** The first time you run the server, `/srv/minecraft/eula.txt` will be created. You will need to edit this file to state that you have agreed to the EULA to run the server.

To easily control the server you may use the provided `minecraftd` script. It is capable of doing the basic commands like `start`, `stop`, `restart` or attaching to the session with `console`. Moreover it may be used to display status information with `status`, backup the server world directory with `backup` or run single commands in the server console with `command <server command>`.

**Note:** Regarding the server `console`, remember that you can exit any screen session with `^A,D`.

To tweak the default settings (e.g. the maximum RAM, number of threads etc.) edit the file `/etc/conf.d/minecraft`.

### Spigot (respectively Craftbukkit)

Spigot is the most widely-used **modded** Minecraft server software in the world, hence there is a [spigot](https://aur.archlinux.org/packages/spigot/) package in the [AUR](/index.php/AUR "AUR"). The spigot PKGBUILD builds on top of the files from the [minecraft-server](https://aur.archlinux.org/packages/minecraft-server/) package. This means that the spigot server as well provides its own systemd unit files, spigot script and the corresponding script configuration file. The binary is called `spigot` and is capable of fulfilling the same commands as `minecrafd` and the configuration file resides under `/etc/conf.d/spigot`.

It is somewhat affiliated with [Bukkit](http://bukkit.org/) and has grown in popularity since Bukkit's demise.

### Additional notes

*   You may wish to modify your server, to provide additional features, e.g. [Server Wrappers](http://www.minecraftwiki.net/wiki/Programs_and_editors#Server_Wrappers)
*   You might even set up a cron job with a [mapper](http://www.minecraftwiki.net/wiki/Programs_and_editors#Mappers) to generate periodic maps of your world.
*   ...or you could use [rsync](/index.php/Rsync "Rsync") to perform routine backups.

## See also

*   [Official Minecraft site](https://www.minecraft.net/)
*   [Minecraft community links](https://www.minecraft.net/community)
*   [Minecraft Client and Server download link](https://minecraft.net/download)
*   [Crafting Recipes](http://www.minecraftwiki.net/wiki/Crafting)
*   [Block and item data values](http://www.minecraftwiki.net/wiki/Data_values)
*   [Reddit Minecraft community](http://www.reddit.com/r/minecraft)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Minecraft&oldid=417208](https://wiki.archlinux.org/index.php?title=Minecraft&oldid=417208)"