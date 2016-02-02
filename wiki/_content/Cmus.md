# Cmus

[cmus](http://cmus.sourceforge.net/) _(C* MUsic Player)_ is a small, fast and powerful console audio player which supports most major audio formats. Various features include gapless playback, ReplayGain support, MP3 and Ogg streaming, live filtering, instant startup, customizable key-bindings, and vi-style default key-bindings.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Using cmus with alsa](#Using_cmus_with_alsa)
*   [2 Usage](#Usage)
    *   [2.1 Starting Cmus](#Starting_Cmus)
    *   [2.2 Adding Music](#Adding_Music)
    *   [2.3 Playing Tracks](#Playing_Tracks)
    *   [2.4 Keybindings](#Keybindings)
*   [3 Tabs](#Tabs)
    *   [3.1 Library tab (1)](#Library_tab_.281.29)
    *   [3.2 Sorted library tab (2)](#Sorted_library_tab_.282.29)
    *   [3.3 Playlist tab (3)](#Playlist_tab_.283.29)
    *   [3.4 Play Queue tab (4)](#Play_Queue_tab_.284.29)
    *   [3.5 Browser (5)](#Browser_.285.29)
    *   [3.6 Filters tab (6)](#Filters_tab_.286.29)
    *   [3.7 Settings tab (7)](#Settings_tab_.287.29)
*   [4 Configuration](#Configuration)
    *   [4.1 Remote Control](#Remote_Control)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [cmus](https://www.archlinux.org/packages/?name=cmus) package, or [cmus-git](https://aur.archlinux.org/packages/cmus-git/)<sup><small>AUR</small></sup> for the development version.

### Using cmus with alsa

When using cmus with [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") the default configuration does not allow playing music. What you might encounter when trying to start cmus is a blank terminal line with no output whatsoever. To fix it, create a new config file and set the following variables

 `~/.config/cmus/rc` 

```
set output_plugin=alsa
set dsp.alsa.device=default
set mixer.alsa.device=default
set mixer.alsa.channel=Master
```

## Usage

Cmus comes with a great reference manual.

```
$ man cmus 
$ man cmus-tutorial
$ man cmus-remote

```

### Starting Cmus

To start cmus, type:

```
$ cmus

```

When you first launch cmus it will open to the album/artist tab.

### Adding Music

Press `5` to switch to the file-browser tab so we can add some music. Now, use the arrow keys (`up`, `down`), `Enter` and `Backspace` to navigate to where you have audio files stored. Alternatively, you may use the vim bindings (`k`, `j`) to navigate up and down through your music.

To add music to your cmus library, use the arrow keys to highlight a file or folder, and press `a`. When you press `a` cmus will move you to the next line down (so that it is easy to add a bunch of files/folders in a row) and start adding the file/folder you pressed `a` in to your library. This may take a bit if you added a folder with a lot of music in it. As files are added, you will see the second time in the bottom right go up. This is the total duration of all the music in the cmus library.

**Note:** cmus does not move, duplicate or change your files. It just remembers where they are and caches the metadata (duration, artist, etc.)

**Note:** Cmus automatically saves your settings, library and everything when you quit.

### Playing Tracks

Press `1` to go to the simple library view. Use the `up` and `down` arrow keys (or `k`, `j`) to select an artist and album you would like to hear. Pressing `space` on the artist name will collapse or expand the albums it contains. Switch between list of tracks and artist/album view by pressing `Tab` and press `Enter` to play the selected track. Here is some keys to control the playback:

	Press `c` to pause/unpause

	Press `right`/`left` (or `h`, `l`) arrow keys to seek by 10 seconds

	Press `<`/`>` seek by one minute

### Keybindings

See the configuration section on how to change keybindings.

## Tabs

There are 7 tabs in cmus. Press keys `1`-`7` to change active tab.

### Library tab (1)

Display all tracks in so-called **library**. Tracks are sorted artist/album tree. Artist sorting is done alphabetically. Albums are sorted by year.

### Sorted library tab (2)

Displays same content as view, but as a simple list which is automatically sorted by user criteria.

### Playlist tab (3)

Displays editable playlist with optional sorting.

### Play Queue tab (4)

Displays queue of tracks which are played next. These tracks are played before anything else (i.e. the playlist or library).

### Browser (5)

Directory browser. In this tab, music can be added to either the library, playlist or queue from the filesystem.

### Filters tab (6)

Lists user defined filters.

### Settings tab (7)

Change settings. See configuration for further information.

## Configuration

To configure cmus start it and switch to the configuration tab by pressing `7`. Now you can see a list of default keybindings. Select a field in the list with the arrow keys and press`Enter` to edit the values. You can also remove bindings with `D` or `del`. To edit unbound commands and option variables scroll down in the list to the relevant section. Variables can also be toggled instead of edited with `space`. Cmus allows changing the color of nearly every interface element. You can prefix colors with "light" to make them appear brighter and set attributes for some text elements.

### Remote Control

Cmus can be controlled externally through a unix-socket with `cmus-remote`. This makes it easy to control playback through an external application or key-binding.

One such usage of this feature is to control playback in Cmus with the XF86 keyboard events. The following script when run will start Cmus in an xterm terminal if it is not running, otherwise it will will toggle play/pause:

```
#!/bin/sh
# This command will break if you rename it to
# something containing "cmus".

if ! pgrep cmus ; then
  xterm -e cmus
else
  cmus-remote -u
fi
```

To use the previous script in [Openbox](/index.php/Openbox "Openbox"), copy the code above into a file `~/bin/cplay`. Make the file executable using `chmod +x ~/bin/cplay`. Next edit `~/.config/openbox/rc.xml` and change the following key-bindings to look like this:

**Note:** Make sure there are no conflicting keybindings in rc.xml

 `~/.config/openbox/rc.xml` 

```
  <keyboard>
    <keybind key="XF86AudioPlay">
      <action name="Execute">
        <command>cmus-remote -u</command>
      </action>
    </keybind>
    <keybind key="XF86AudioNext">
      <action name="Execute">
        <command>cmus-remote -n</command>
      </action>
    </keybind>
    <keybind key="XF86AudioPrev">
      <action name="Execute">
        <command>cmus-remote -r</command>
      </action>
    </keybind>
  </keyboard>

```

Now when you use the `XF86AudioPlay` key on your keyboard, cmus will open up. If it is opened already it will then start playing. Using the XF86AudioNext and XF86AudioPrev keys will change tracks.

## See also

*   [Git Repository](https://github.com/cmus/cmus)
*   [Website](https://cmus.github.io/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Cmus&oldid=414735](https://wiki.archlinux.org/index.php?title=Cmus&oldid=414735)"