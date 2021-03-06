[Terminator](http://gnometerminator.blogspot.com/p/introduction.html) is a [terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") which supports tabs and multiple resizable terminal panels in one window. It is based on [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 GTK customization](#GTK_customization)
*   [3 Key commands](#Key_commands)
*   [4 Managing profiles](#Managing_profiles)
    *   [4.1 Drag and Drop](#Drag_and_Drop)
    *   [4.2 More key commands](#More_key_commands)
*   [5 See also](#See_also)

## Installation

[terminator](https://www.archlinux.org/packages/?name=terminator) is available in the [official repositories](/index.php/Official_repositories "Official repositories"). Install [terminator-gtk3-bzr](https://aur.archlinux.org/packages/terminator-gtk3-bzr/) for the latest (trunk) version.

## Configuration

See the [man page](https://en.wikipedia.org/wiki/man_page "wikipedia:man page") or right click Terminator and then click *Preferences*.

```
man terminator_config

```

User-specific configuration can be found in `~/.config/terminator/config`.

### GTK customization

Terminator supports tabs. Tab header height is sometimes considered too big. This can be fixed with gtk styling. From version 1.9 Terminator uses GTK 3, so that configuration can be done in `~/.config/gtk-3.0/gtk.css`. The items to customize are 'notebook tab', 'notebook tab button'. (note that this affects other gtk3 applications, too).

Example config:

 `~/.config/gtk-3.0/gtk.css` 
```
notebook tab {
  min-height: 0;
  padding: 2px;
}

notebook tab button {
  min-height: 0;
  min-width: 0;
  padding: 1px;
  margin: 1px;
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

If you add more profiles in the future and would like to have them included in the startup pool, you will have to reissue the command above. You can create an [alias](/index.php/Alias "Alias").

You must now modify Terminator's desktop file so that it selects a random profile from this list at startup.

```
sudoedit /usr/share/applications/terminator.desktop

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

## See also

*   [Terminator](http://gnometerminator.blogspot.com/p/introduction.html) - Official site
*   [Terminator BZR](http://code.launchpad.net/terminator/) - Source code