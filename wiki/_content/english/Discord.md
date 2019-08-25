Discord is a proprietary all-in-one voice and text chat application, cross-platform chat application, especially tailored for Gamers, however many open source communities have [official servers through Discord](https://discordapp.com/open-source) as well. Discord can be used through the browser, however there is also a desktop application as well. The desktop application uses [Electron](https://github.com/electron/electron).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Graphical clients](#Graphical_clients)
    *   [1.2 Command-line clients](#Command-line_clients)
    *   [1.3 Chat client plugins](#Chat_client_plugins)
*   [2 Troubleshooting](#Troubleshooting)

## Installation

You can use one of following packages in order to install the desktop application for Discord:

### Graphical clients

The [official app](https://discordapp.com/):

*   Stable: [discord](https://www.archlinux.org/packages/?name=discord)
*   Nightly: [discord-canary](https://aur.archlinux.org/packages/discord-canary/)

Third-party clients:

*   [ripcord](https://aur.archlinux.org/packages/ripcord/), see the [Ripcord](/index.php/Ripcord "Ripcord") article for more information

### Command-line clients

*   [cordless-git](https://aur.archlinux.org/packages/cordless-git/)

There are more CLI-based third-party clients out there hosted on places like GitHub (such as [Discline](https://github.com/MitchWeaver/Discline) or [terminal-discord](https://github.com/xynxynxyn/terminal-discord)), although only Cordless is currently packaged on the AUR.

### Chat client plugins

*   By using [purple-discord-git](https://aur.archlinux.org/packages/purple-discord-git/), you can use Discord on graphical or terminal messenger softwares based on [libpurple](https://www.archlinux.org/packages/?name=libpurple) such as [Pidgin](/index.php/Pidgin "Pidgin").
*   By using [bitlbee-discord-git](https://aur.archlinux.org/packages/bitlbee-discord-git/), you can use Discord via [Bitlbee](/index.php/Bitlbee "Bitlbee").

## Troubleshooting

If you experience crackling sounds when in voice chat, you should try the steps outlined here: [PulseAudio/Troubleshooting](/index.php/PulseAudio/Troubleshooting#Glitches,_skips_or_crackling "PulseAudio/Troubleshooting")

If you can't share individual monitors on a multi-monitor setup, you should try [mon2cam-git](https://aur.archlinux.org/packages/mon2cam-git/) as a workaround to this bug: [Discord Trello](https://trello.com/c/SJEH2Fsi/41-multiple-monitors-are-shown-as-one-in-screenshare)