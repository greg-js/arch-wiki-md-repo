[ePSXe](https://en.wikipedia.org/wiki/ePSXe "wikipedia:ePSXe") (enhanced PSX emulator) is a PlayStation emulator for x86-based PC hardware with Microsoft Windows or Linux, as well as devices running Android. It was written by three authors, using the aliases *Calb*, *_Demo_* and *Galtor*. ePSXe is closed source with the exception of the application programming interface (API) for its plug-ins.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Playing](#Playing)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 xgl2 plugin does not work](#xgl2_plugin_does_not_work)
    *   [4.2 Sound device not found](#Sound_device_not_found)
*   [5 See also](#See_also)

## Installation

**Warning:** The installation and use of this emulator requires a Sony PlayStation BIOS file. You may not use such a file to play games in a PSX emulator if you do not own a Sony PlayStation, Sony PSOne or Sony PlayStation 2 console. Owning the BIOS image without owning the actual console is a violation of copyright law. You have been warned.

Install [epsxe](https://aur.archlinux.org/packages/epsxe/) from [AUR](/index.php/AUR "AUR"), along with any [plugins](https://aur.archlinux.org/packages.php?K=epsxe-plugin). Also, you should have a legally obtained BIOS file handy.

Add yourself to the `games` group:

```
# usermod -G games -a USERNAME

```

If the group does not exist, create it first:

```
# groupadd games

```

Run epsxe from the menu shortcut or by typing 'epsxe' into a terminal.

## Configuration

Configure video and sound by going to *Config > Video* and *Config > Sound* respectively, and configuring the plugins you want. Verify that they are working by clicking the Test buttons in each of the windows.

The CD-ROM path should be set by default. You can check it by going to *Config > Cdrom*.

Set up the controls for player one by going to *Config > Game Pad > Port 1 > Pad 1*.

## Playing

Run a game from your CD-ROM by clicking *File > Run CDROM*.

Load up a game from an ISO by clicking *File > Run ISO*.

You can manipulate game states by going to *Run > Save State (F1)* and *Run > Load State (F3)*, or using the hotkeys F1 and F3.

## Troubleshooting

### xgl2 plugin does not work

You will have to install nvidia-utils, if running from a 32-bit chroot.

### Sound device not found

If the sound plugin does not work and you are using alsa, run:

```
# modprobe snd-pcm-oss

```

## See also

*   ePSXe - [http://www.epsxe.com/](http://www.epsxe.com/)
*   Pete's PSX plugins - [http://www.pbernert.com/index.htm](http://www.pbernert.com/index.htm)