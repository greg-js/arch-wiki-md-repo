[Notion](http://notion.sf.net) is a tiling, tabbed [window manager](/index.php/Window_manager "Window manager") for X.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting Notion](#Starting_Notion)
    *   [2.1 With a login manager](#With_a_login_manager)
    *   [2.2 With xinitrc](#With_xinitrc)
*   [3 Using Notion](#Using_Notion)
*   [4 Lua 5.2](#Lua_5.2)
    *   [4.1 gfind](#gfind)
    *   [4.2 goto](#goto)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [notion](https://www.archlinux.org/packages/?name=notion).

## Starting Notion

### With a login manager

To start/select Notion from most login managers, a standard .desktop file can be created in the /usr/share/xsessions/ directory. An example notion.desktop file can be found below:

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

### With xinitrc

You can start Notion from the command line by adding `exec notion` to [~/.xinitrc](/index.php/~/.xinitrc "~/.xinitrc") or any other startup script you may want to use. An example .xinitrc file can be found below.

```
DEFAULT_SESSION=notion
case $1 in
awesome) 
                   exec awesome
                   ;;
notion) 
                   exec notion
                   ;;
openbox) 
                   exec openbox-session
                   ;;
*) 
                   exec $DEFAULT_SESSION
                   ;;
esac

```

## Using Notion

You can view Notion's man page at any time during use by pressing the F1 key and pressing the return key This will tell you the default key bindings for Notion. You can also access the man page for other programs this way by pressing F1, typing in the program's name and pressing return.

## Lua 5.2

### gfind

You should replace 'gfind' to 'gmatch' because of 'gfind' was removed

### goto

'goto' is a keyword now. You can use following workaround:

replace

```
 win:goto()

```

to

```
 function win_goto(w) return w['goto'](w) end
 ...
 win_goto(win)

```

## See also

*   [http://sourceforge.net/apps/mediawiki/notion/index.php?title=Tour](http://sourceforge.net/apps/mediawiki/notion/index.php?title=Tour) - Tour of Notion
*   [http://notion.sourceforge.net/notionconf/](http://notion.sourceforge.net/notionconf/) - Configuring and Extending Notion using LUA
*   [http://sourceforge.net/apps/mediawiki/notion](http://sourceforge.net/apps/mediawiki/notion) - Notion Wiki