[Notion](https://notionwm.net/) is a tiling, tabbed [window manager](/index.php/Window_manager "Window manager") for X.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
    *   [2.1 With a display manager](#With_a_display_manager)
*   [3 Usage](#Usage)
*   [4 Configuration](#Configuration)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [notion](https://www.archlinux.org/packages/?name=notion).

## Starting

Run `notion` with [xinit](/index.php/Xinit "Xinit").

### With a display manager

To start/select Notion with a [display manager](/index.php/Display_manager "Display manager"), a standard .desktop file can be created in the `/usr/share/xsessions/` directory. An example `notion.desktop` file can be found below:

```
[Desktop Entry]
Name=Notion
Comment=This session logs you into Notion
Exec=/usr/bin/notion
TryExec=/usr/bin/notion
Icon=
Type=XSession

```

See the [display manager](/index.php/Display_manager "Display manager") article for more details.

## Usage

You can view Notion's man page during use with the F1 key and pressing the return key, this will tell you the default key bindings for Notion. You can also access the man page for other programs this way by pressing F1, typing in the program's name and pressing return. Besides the manual there is also a [getting started tour](http://raboof.github.io/notion/tour/) available for a quick overview of Notion.

## Configuration

Notion can be configured using Lua. To get started, copy `/etc/notion/cfg_notion.lua` to `~/.notion`. For more information, read [Configuring and Extending Notion using Lua](http://notion.sourceforge.net/notionconf/).

## See also

*   [http://notionwm.net/](http://notionwm.net/) - Notion website
*   [http://notion.sourceforge.net/notionconf/](http://notion.sourceforge.net/notionconf/) - Configuring and Extending Notion using Lua
*   [https://github.com/raboof/notion/](https://github.com/raboof/notion/) - Notion GitHub