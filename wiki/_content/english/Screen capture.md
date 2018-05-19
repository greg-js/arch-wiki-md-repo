Related articles

*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

This article explains different methods to capture your screen.

For a list of [screenshot](https://en.wikipedia.org/wiki/Screenshot "wikipedia:Screenshot") software, see [List of applications/Multimedia#Screenshot](/index.php/List_of_applications/Multimedia#Screenshot "List of applications/Multimedia").

For a list of [screencast](https://en.wikipedia.org/wiki/Screencast "wikipedia:Screencast") software, see [List of applications/Multimedia#Screencast](/index.php/List_of_applications/Multimedia#Screencast "List of applications/Multimedia").

## Contents

*   [1 Screenshot software](#Screenshot_software)
    *   [1.1 ImageMagick/GraphicsMagick](#ImageMagick.2FGraphicsMagick)
        *   [1.1.1 Screenshot of multiple X screens](#Screenshot_of_multiple_X_screens)
        *   [1.1.2 Screenshot of individual Xinerama heads](#Screenshot_of_individual_Xinerama_heads)
        *   [1.1.3 Screenshot of the active/focused window](#Screenshot_of_the_active.2Ffocused_window)
    *   [1.2 GIMP](#GIMP)
    *   [1.3 xwd](#xwd)
    *   [1.4 scrot](#scrot)
    *   [1.5 escrotum](#escrotum)
    *   [1.6 imlib2](#imlib2)
    *   [1.7 maim](#maim)
    *   [1.8 FFmpeg](#FFmpeg)
    *   [1.9 Weston](#Weston)
*   [2 Details: desktop environment specific](#Details:_desktop_environment_specific)
    *   [2.1 Spectacle](#Spectacle)
    *   [2.2 Xfce Screenshooter](#Xfce_Screenshooter)
    *   [2.3 GNOME](#GNOME)
    *   [2.4 Cinnamon](#Cinnamon)
    *   [2.5 Other desktop environments or window managers](#Other_desktop_environments_or_window_managers)
*   [3 Terminal](#Terminal)
    *   [3.1 Capture with ANSI codes](#Capture_with_ANSI_codes)
    *   [3.2 Framebuffer](#Framebuffer)
    *   [3.3 Virtual console](#Virtual_console)

## Screenshot software

### ImageMagick/GraphicsMagick

An easy way to take a screenshot of your current system is using the [import(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/import.1) command:

```
$ import -window root screenshot.jpg

```

`import` is part of the [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) package.

Running `import` without the `-window` option allows selecting a window or an arbitrary region interactively.

**Note:** If you prefer **graphicsmagick** alternative, just prepend "gm", e.g. `$ gm import -window root screenshot.jpg`.

#### Screenshot of multiple X screens

If you run twinview or dualhead, simply take the screenshot twice and use `imagemagick` to paste them together:

```
import -window root -display :0.0 -screen /tmp/0.png
import -window root -display :0.1 -screen /tmp/1.png
convert +append /tmp/0.png /tmp/1.png screenshot.png
rm /tmp/{0,1}.png

```

#### Screenshot of individual Xinerama heads

Xinerama-based multi-head setups have only one virtual screen. If the physical screens are different in height, you will find dead space in the screenshot. In this case, you may want to take screenshot of each physical screen individually. As long as Xinerama information is available from the X server, the following will work:

```
#!/bin/sh
xdpyinfo -ext XINERAMA | sed '/^  head #/!d;s///' |
while IFS=' :x@,' read i w h x y; do
        import -window root -crop ${w}x$h+$x+$y head_$i.png
done

```

#### Screenshot of the active/focused window

The following script takes a screenshot of the currently focused window. It works with EWMH/NetWM compatible X Window Managers. To avoid overwriting previous screenshots, the current date is used as the filename.

```
#!/bin/sh
activeWinLine=$(xprop -root | grep "_NET_ACTIVE_WINDOW(WINDOW)")
activeWinId=${activeWinLine:40}
import -window "$activeWinId" /tmp/$(date +%F_%H%M%S_%N).png

```

Alternatively, the following should work regardless of EWMH support:

```
$ import -window "$(xdotool getwindowfocus -f)" /tmp/$(date +%F_%H%M%S_%N).png

```

**Note:** If screenshots of some programs (dwb and zathura) appear blank, try appending `-frame` or removing `-f` from the `xdotool` command.

### GIMP

You also can take screenshots with [GIMP](/index.php/GIMP "GIMP") (*File > Create > Screenshot*...).

### xwd

[xwd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xwd.1) provided by [xorg-xwd](https://www.archlinux.org/packages/?name=xorg-xwd)

Take a screenshot of the root window:

```
$ xwd -root -out screenshot.xwd

```

**Note:** The methods for taking shots of active windows with `import` can also be used with `xwd`.

### scrot

[scrot](https://www.archlinux.org/packages/?name=scrot) enables taking screenshots from the CLI and offers features such as a user-definable time delay. Unless instructed otherwise, it saves the file in the current working directory.

```
$ scrot -t 20 -d 5

```

The above command saves a dated `.png` file, along with a thumbnail (20% of original), for Web posting. It provides a 5 second delay before capturing in this instance.

You can also use standard date and time formatting when saving to a file. e.g.,

```
$ scrot ~/screenshots/%Y-%m-%d-%T-screenshot.png

```

saves the screenshot in a filename with the current year, month, date, hours, minutes, and seconds to a folder in your home directory called "screenshots"

See [scrot(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/scrot.1) for more information. You can simply automate the file to uploaded like so [[1]](https://github.com/kaihendry/Kai-s--HOME/tree/master/bin).

**Note:** In some window managers ([dwm](https://aur.archlinux.org/packages/dwm/), [xmonad](https://www.archlinux.org/packages/?name=xmonad) and possibly others) `scrot -s` does not work properly when running via window manager's keyboard shortcut, this can be worked around by prepending scrot invocation with a short pause `sleep 0.2; scrot -s`.

### escrotum

[escrotum-git](https://aur.archlinux.org/packages/escrotum-git/) screen capture using pygtk, inspired by scrot

Created because scrot has glitches when selection mode is used with refreshing windows.

Because the command line interface its almost the same as scrot, can be used as a replacement of it.

### imlib2

[imlib2](https://www.archlinux.org/packages/?name=imlib2) provides a binary `imlib2_grab` to take screenshots. To take a screenshot of the full screen, type:

```
$ imlib2_grab screenshot.png

```

Note that [scrot](https://www.archlinux.org/packages/?name=scrot) actually uses `imlib2`.

### maim

[maim](https://www.archlinux.org/packages/?name=maim) is aimed to be an improved scrot.

Takes screenshots of your desktop using [slop](https://github.com/naelstrof/slop) for regions. It's meant to overcome shortcomings of scrot.

### FFmpeg

See [FFmpeg#Screen capture](/index.php/FFmpeg#Screen_capture "FFmpeg").

### Weston

In the [Weston](/index.php/Wayland#Weston "Wayland") Wayland compositor, screenshots can be taking by pressing `Super+s`, which are stored in Weston's current working directory. Screencasts are also supported; recording is started and stopped by pressing `Super+r`, which will create a file called `capture.wcap` in Weston's current working directory. The capture can be decoded to YUV format by running `wcap-decode --yuv4mpeg2 capture.wcap`; the output of this command can be written to a file or piped into FFmpeg for further processing.

## Details: desktop environment specific

### Spectacle

If you use [KDE](/index.php/KDE "KDE"), you might want to use `Spectacle`.

Spectacle is provided by the [spectacle](https://www.archlinux.org/packages/?name=spectacle).

### Xfce Screenshooter

If you use [Xfce](/index.php/Xfce "Xfce") you can install [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter) and then add a keyboard binding:

*Xfce Menu > Settings > Keyboard > Application Shortcuts*

If you want to skip the Screenshot prompt, type `$ xfce4-screenshooter -h` in terminal for the options.

### GNOME

[GNOME](/index.php/GNOME "GNOME") users can press `Prnt Scr` or *Apps > Accessories > Take Screenshot*. You may need to install [gnome-screenshot](https://www.archlinux.org/packages/?name=gnome-screenshot).

### Cinnamon

The default installation of [Cinnamon](/index.php/Cinnamon "Cinnamon") does not provide a screenshot utility. Installing [gnome-screenshot](https://www.archlinux.org/packages/?name=gnome-screenshot) will enable screenshots through the *Menu > Accessories > Screenshot* or by pressing `Prnt Scr`.

### Other desktop environments or window managers

For other desktop environments such as [LXDE](/index.php/LXDE "LXDE") or window managers such as [Openbox](/index.php/Openbox "Openbox") and [Compiz](/index.php/Compiz "Compiz"), one can add the above commands to the hotkey to take the screenshot. For example,

```
$ import -window root ~/Pictures/$(date '+%Y%m%d-%H%M%S').png

```

Adding the above command to the `Prnt Scr` key to Compiz allows to take the screenshot to the Pictures folder according to date and time. Notice that the `rc.xml` file in Openbox does not understand commas; so, in order to bind that command to the `Prnt Scr` key in Openbox, you need to add the following to the keyboard section of your `rc.xml` file:

 `rc.xml` 
```
<!-- Screenshot -->
    <keybind key="Print">
      <action name="Execute">
        <command>sh -c "import -window root ~/Pictures/$(date '+%Y%m%d-%H%M%S').png"</command>
      </action>
    </keybind>

```

If the `Print` above does not work, see [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") and use different *keysym* or *keycode*.

## Terminal

### Capture with ANSI codes

You can use the [script(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/script.1) command, part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package. Just run `script` and from that moment, all the output is going to be saved to the `typescript` file, including the ANSI codes.

Once you are done, just run `exit` and the `typescript` would ready. The resulting file can be converted to HTML using the [ansi2html](https://aur.archlinux.org/packages/ansi2html/) package, from the [AUR](/index.php/AUR "AUR").

To convert the `typescript` file to `typescript.html`, do the following:

```
$ ansi2html --bg=dark < typescript > typescript.html

```

Actually, **some** commands can be piped directly to ansi2html:

```
$ ls --color|ansi2html --bg=dark >output.html

```

That does not work on every single case, so in those cases, using `script` is mandatory.

### Framebuffer

Install a [framebuffer](/index.php/Framebuffer "Framebuffer") and use [fbgrab](https://aur.archlinux.org/packages/fbgrab/) or [fbdump](https://aur.archlinux.org/packages/fbdump/) to take a screenshot.

### Virtual console

If you merely want to capture the text in the console and not an actual image, you can use `setterm`, which is part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package. The following command will dump the textual contents of virtual console 1 to a file screen.dump in the current directory:

```
# setterm -dump 1 -file screen.dump

```

Root permission is needed because the contents of `/dev/vcs1` need to be read.