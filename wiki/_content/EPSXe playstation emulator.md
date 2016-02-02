# EPSXe playstation emulator

ePSXe (enhanced PSX emulator) is a PlayStation emulator for x86-based PC hardware with Microsoft Windows or Linux, as well as devices running Android. It was written by three authors, using the aliases _Calb_, __Demo__ and _Galtor_. ePSXe is closed source with the exception of the application programming interface (API) for its plug-ins.

## Contents

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

Configure video and sound by going to _Config > Video_ and _Config > Sound_ respectively, and configuring the plugins you want. Verify that they are working by clicking the Test buttons in each of the windows.

The CD-ROM path should be set by default. You can check it by going to _Config > Cdrom_.

Set up the controls for player one by going to _Config > Game Pad > Port 1 > Pad 1_.

## Playing

Run a game from your CD-ROM by clicking _File > Run CDROM_.

Load up a game from an ISO by clicking _File > Run ISO_.

You can manipulate game states by going to _Run > Save State (F1)_ and _Run > Load State (F3)_, or using the hotkeys F1 and F3.

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=EPSXe_playstation_emulator&oldid=394347](https://wiki.archlinux.org/index.php?title=EPSXe_playstation_emulator&oldid=394347)"