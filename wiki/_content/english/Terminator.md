[Terminator](http://gnometerminator.blogspot.com/p/introduction.html) is a [terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") which supports tabs and multiple resizable terminal panels in one window. It is based on [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 GTK+ customization](#GTK.2B_customization)
*   [3 Key commands](#Key_commands)
*   [4 Managing profiles](#Managing_profiles)
    *   [4.1 Drag and Drop](#Drag_and_Drop)
    *   [4.2 More key commands](#More_key_commands)
*   [5 Plugins](#Plugins)
*   [6 See also](#See_also)

## Installation

[terminator](https://www.archlinux.org/packages/?name=terminator) is available in the [official repositories](/index.php/Official_repositories "Official repositories"). Install [terminator-gtk3-bzr](https://aur.archlinux.org/packages/terminator-gtk3-bzr/) for the latest (trunk) version.

## Configuration

See the [man page](https://en.wikipedia.org/wiki/man_page "wikipedia:man page") or right click Terminator and then click *Preferences*.

```
man terminator_config

```

User-specific configuration can be found in `~/.config/terminator/config`.

### GTK+ customization

**Note:** This configuration [doesn't](https://bbs.archlinux.org/viewtopic.php?pid=1687446#p1687446) work for all users, see [User talk:Szb#Reducing the size of Terminator tabs](/index.php/User_talk:Szb#Reducing_the_size_of_Terminator_tabs "User talk:Szb").

Terminator supports tabs. Tab header height is sometimes considered too big. This can be fixed with gtk styling. From version 1.9 Terminator uses gtk+ 3, so that configuration can be done in `~/.config/gtk-3.0/gtkcss`. The items to customize are 'notebook tab', 'notebook tab button'. (note that this affects other gtk3 applications, too).

Example config:

 `~/.config/gtk-3.0/gtkcss` 
```
notebook tab {
  min-height: 0;
  padding-top: 2px;
  padding-bottom: 2px;
}

notebook tab button {
  min-height: 0;
  min-width: 0;
  padding: 1px;
  margin-top: 1px;
  margin-bottom: 1px;
}

```

## Key commands

`F11` Toggle fullscreen

`Ctrl + Shift+ O` Split terminals h**o**rizontally

`Ctrl + Shift+ E` Split terminals v**e**rtically

`Ctrl + Shift+ W` Close current Panel

`Ctrl + Shift+ T` Open new tab

`Alt + ↑` Move to the terminal above the current one

`Alt + ↓` Move to the terminal below the current one

`Alt + ←` Move to the terminal left of the current one

`Alt + →` Move to the terminal right of the current one

## Managing profiles

It is possible to start terminator with a random profile every time. To avoid unexpected behavior, you should start with a clean `[profiles]` section. You can copy the one from this file: [http://pastebin.com/gGvYH6zD](http://pastebin.com/gGvYH6zD). It contains many well-known color schemes. Copy its contents to your `config` file, which is located in `~/.config/terminator/`. Then, `cat` your list of profiles to a destination of your choice.

```
cat $HOME/.config/terminator/config | grep -B 1 'background_color' | grep '\]\]' | tr -d '[]' > $HOME/.config/terminator/profiles

```

If you add more profiles in the future and would like to have them included in the startup pool, you will have to reissue the command above. You can create an [alias](/index.php/Bash#Aliases "Bash").

You must now modify Terminator's desktop file so that it selects a random profile from this list at startup.

```
sudo nano /usr/share/applications/terminator.desktop

```

Find the `Exec` line and comment it out with a `#`. Add your own `Exec` line as follows.

```
# Exec=terminator
Exec=sh -c "terminator -p $( shuf -n 1 $HOME/.config/terminator/profiles )"

```

Save the file and restart your [desktop environment](/index.php/Desktop_environment "Desktop environment").

Bonus: Go to the terminator preferences and under the "keybindings" tab, take note of how to switch to the next profile. This way,if the profile Terminator has started with is not your liking, you can quickly change it.

### Drag and Drop

The layout can be modified by moving terminals with Drag and Drop.

### More key commands

```
man terminator

```

## Plugins

Terminator also supports plugins. See [writing Terminator plugins](http://www.tenshu.net/2010/04/writing-terminator-plugins.html) for more details.

## See also

*   [Terminator](http://gnometerminator.blogspot.com/p/introduction.html) - Official site
*   [Writing Terminator plugins](http://www.tenshu.net/2010/04/writing-terminator-plugins.html) - Terminator Plugin HOWTO
*   [Terminator BZR](http://code.launchpad.net/terminator/) - Source code