[Rockbox](https://www.rockbox.org) is a free replacement firmware for digital audio players (MP3 players). Its enhancements include support for pretty much all [codecs](/index.php/Codecs "Codecs"), advanced sound settings, applications, utilities and games.

**Tip:** Rockbox can often be installed alongside the original firmware.

## Contents

*   [1 Supported devices](#Supported_devices)
*   [2 Installation](#Installation)
    *   [2.1 Rockbox Utility](#Rockbox_Utility)
    *   [2.2 Installing Rockbox on your device](#Installing_Rockbox_on_your_device)
        *   [2.2.1 Boot loader](#Boot_loader)
*   [3 Backup](#Backup)

## Supported devices

Check if your device has a usable Rockbox port: [https://www.rockbox.org/](https://www.rockbox.org/).

## Installation

### Rockbox Utility

The official tool to manage Rockbox can be [installed](/index.php/Installed "Installed") with the [rbutil](https://www.archlinux.org/packages/?name=rbutil) package. [Rockbox Utility](https://www.rockbox.org/wiki/RockboxUtility) can install the replacement boot loader, the main firmware, and any extra features like fonts, themes and applications.

### Installing Rockbox on your device

The Rockbox project has fantastic install instructions. You can find them at [https://www.rockbox.org/manual.shtml](https://www.rockbox.org/manual.shtml).

#### Boot loader

It is recommended to install the boot loader using [#Rockbox Utility](#Rockbox_Utility). For Rockbox Utility to detect your player, it must have write access to the internal disk of the player.

**Tip:** As you need write access to the player disk, you could give that when [mounting](/index.php/Mount "Mount"). For example: `# mount -o uid=1000,gid=1000 /dev/sdb /mnt`.

## Backup

[#Rockbox Utility](#Rockbox_Utility) can make backups of your device.