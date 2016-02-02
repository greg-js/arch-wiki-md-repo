# Taking a screenshot

Related articles

*   [Extra_keyboard_keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

This article explain different methods to take [screenshots](https://en.wikipedia.org/wiki/Screenshot "wikipedia:Screenshot") on your system.

## Contents

*   [1 Dedicated software](#Dedicated_software)
*   [2 Packages including a screenshot utility](#Packages_including_a_screenshot_utility)
*   [3 Details: general methods](#Details:_general_methods)
    *   [3.1 ImageMagick/GraphicsMagick](#ImageMagick.2FGraphicsMagick)
        *   [3.1.1 Screenshot of multiple X screens](#Screenshot_of_multiple_X_screens)
        *   [3.1.2 Screenshot of individual Xinerama heads](#Screenshot_of_individual_Xinerama_heads)
        *   [3.1.3 Screenshot of the active/focused window](#Screenshot_of_the_active.2Ffocused_window)
    *   [3.2 GIMP](#GIMP)
    *   [3.3 xwd](#xwd)
    *   [3.4 scrot](#scrot)
    *   [3.5 escrotum](#escrotum)
    *   [3.6 imlib2](#imlib2)
    *   [3.7 maim](#maim)
    *   [3.8 FFmpeg](#FFmpeg)
    *   [3.9 Weston](#Weston)
*   [4 Details: desktop environment specific](#Details:_desktop_environment_specific)
    *   [4.1 Spectacle](#Spectacle)
    *   [4.2 Xfce Screenshooter](#Xfce_Screenshooter)
    *   [4.3 GNOME](#GNOME)
    *   [4.4 Cinnamon](#Cinnamon)
    *   [4.5 Other desktop environments or window managers](#Other_desktop_environments_or_window_managers)
*   [5 Terminal](#Terminal)
    *   [5.1 Output with ansi codes](#Output_with_ansi_codes)
    *   [5.2 Virtual console](#Virtual_console)

## Dedicated software

*   **Deepin Screenshot** — Provide a quite easy-to-use screenshot tool. Features: global hotkey to trigger screenshot tool, take screenshot of a selected area, easy to add text and line drawings onto the screenshot. Python/Qt5 based.

	[http://www.linuxdeepin.com/](http://www.linuxdeepin.com/) || [deepin-screenshot](https://www.archlinux.org/packages/?name=deepin-screenshot)

*   **Escrotum** — Screen capture using pygtk, inspired by scrot.

	[https://github.com/Roger/escrotum](https://github.com/Roger/escrotum) || [escrotum-git](https://aur.archlinux.org/packages/escrotum-git/)<sup><small>AUR</small></sup>

*   **gnome-screenshot** — Take pictures of your screen. Even if its used Gnome in their name, its dependencies only dconf, gtk3, and libcanberra.

	[http://gnome.org](http://gnome.org) || [gnome-screenshot](https://www.archlinux.org/packages/?name=gnome-screenshot)

*   **imgur-screenshot** — Take screenshot selection, upload to [imgur](http://imgur.com). + more cool things

	[https://github.com/jomo/imgur-screenshot](https://github.com/jomo/imgur-screenshot) || [imgur-screenshot-git](https://aur.archlinux.org/packages/imgur-screenshot-git/)<sup><small>AUR</small></sup>

*   **Lightscreen** — Lightscreen is a simple tool to automate the tedious process of saving and cataloging screenshots, it operates as a hidden background process that is invoked with one (or multiple) hotkeys and then saves a screenshot file to disk according to the user's preferences.

	[http://lightscreen.com.ar](http://lightscreen.com.ar) || [lightscreen](https://aur.archlinux.org/packages/lightscreen/)<sup><small>AUR</small></sup>

*   **maim** — A simple command line utility that takes screenshots using imlib2\. It's meant to replace scrot and performs better than scrot in many ways.

	[https://github.com/naelstrof/maim](https://github.com/naelstrof/maim) || [maim](https://www.archlinux.org/packages/?name=maim)

*   **maimclip** — Simple bash wrapper for maim screenshot taking tool with OSD notification support

	[https://github.com/orschiro/scriptlets/tree/master/Maimclip](https://github.com/orschiro/scriptlets/tree/master/Maimclip) || [maimclip-git](https://aur.archlinux.org/packages/maimclip-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/maimclip-git)]</sup>

*   **qscreenshot** — Simple creation and editing of screenshots (Qt).

	[https://code.google.com/p/qscreenshot/](https://code.google.com/p/qscreenshot/) || [qscreenshot-git](https://aur.archlinux.org/packages/qscreenshot-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qscreenshot-git)]</sup>

*   **screencloud** — allows you to take a screenshot of the entire screen or to select an area and then uploading the screenshot to [imgur](http://imgur.com)+auth. has plugins and system tray.

	[http://screencloud.net/](http://screencloud.net/) || [screencloud](https://aur.archlinux.org/packages/screencloud/)<sup><small>AUR</small></sup>

*   **screengrab** — Cross-platform application designed to quickly get screenshots (Qt).

	[http://screengrab.doomer.org/](http://screengrab.doomer.org/) || [screengrab](https://aur.archlinux.org/packages/screengrab/)<sup><small>AUR</small></sup>

*   **[Scrot](https://en.wikipedia.org/wiki/Scrot "wikipedia:Scrot")** — Simple command-line screenshot utility for X.

	[http://freecode.com/projects/scrot](http://freecode.com/projects/scrot) || [scrot](https://www.archlinux.org/packages/?name=scrot)

*   **Shutter** — Rich screenshot and editing program.

	[http://shutter-project.org/](http://shutter-project.org/) || [shutter](https://www.archlinux.org/packages/?name=shutter)

*   **Spectacle** — [KDE](/index.php/KDE "KDE") application for taking screenshots. It is capable of capturing images of the whole desktop, a single window, a section of a window, a selected rectangular region or a freehand region. Part of [kdegraphics](https://www.archlinux.org/groups/x86_64/kdegraphics/).

	[https://github.com/KDE/spectacle/](https://github.com/KDE/spectacle/) || [spectacle](https://www.archlinux.org/packages/?name=spectacle)

*   **Xfce4 Screenshooter** — This application allows you to capture the entire screen, the active window or a selected region. You can set the delay that elapses before the screenshot is taken and the action that will be done with the screenshot: save it to a PNG file, copy it to the clipboard, open it using another application, or host it on ZimageZ, a free online image hosting service. Part of [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

	[http://goodies.xfce.org/projects/applications/xfce4-screenshooter](http://goodies.xfce.org/projects/applications/xfce4-screenshooter) || [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter)

*   **xwd** — X Window System image dumping utility

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xorg-xwd](https://www.archlinux.org/packages/?name=xorg-xwd)

*   **zscreen** — Lightweight GUI which allows you to take a screenshot of the entire screen or to select an area and then uploading the screenshot automatically to [imgur](http://imgur.com). For taking the screenshot it uses scrot and zenity for the GUI.

	[https://github.com/ChrisZeta/Scrot-and-imgur-zenity-GUI](https://github.com/ChrisZeta/Scrot-and-imgur-zenity-GUI) || [zscreen](https://aur.archlinux.org/packages/zscreen/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/zscreen)]</sup>

## Packages including a screenshot utility

*   **[GIMP](https://en.wikipedia.org/wiki/GIMP "wikipedia:GIMP")** — Image editing suite in the vein of proprietary editors such as [Adobe Photoshop](https://en.wikipedia.org/wiki/Adobe_Photoshop "wikipedia:Adobe Photoshop"). GIMP ([GNU](/index.php/GNU "GNU") Image Manipulation Program) has been started in the mid 1990s and has acquired a large number of [plugins](/index.php/CMYK_support_in_The_GIMP "CMYK support in The GIMP") and additional tools.

	[http://www.gimp.org/](http://www.gimp.org/) || [gimp](https://www.archlinux.org/packages/?name=gimp)

*   **[GraphicsMagick](https://en.wikipedia.org/wiki/GraphicsMagick "wikipedia:GraphicsMagick")** — Fork of ImageMagick designed to have API and command-line stability. It also supports multi-CPU for enhanced performance and thus is used by some large commercial sites (Flickr, etsy) for its performance.

	[http://www.graphicsmagick.org/](http://www.graphicsmagick.org/) || [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick)

*   **[ImageMagick](https://en.wikipedia.org/wiki/ImageMagick "wikipedia:ImageMagick")** — Command-line image manipulation program. It is known for its accurate format conversions with support for over 100 formats. Its API enables it to be scripted and it is usually used as a backend processor.

	[http://www.imagemagick.org/script/index.php](http://www.imagemagick.org/script/index.php) || [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)

*   **Imlib2** — Library that does image file loading and saving as well as rendering, manipulation, arbitrary polygon support.

	[http://sourceforge.net/projects/enlightenment/](http://sourceforge.net/projects/enlightenment/) || [imlib2](https://www.archlinux.org/packages/?name=imlib2)

## Details: general methods

### ImageMagick/GraphicsMagick

An easy way to take a screenshot of your current system is using the `import` command:

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

You also can take screenshots with GIMP (_File > Create > Screenshot_...).

### xwd

Take a screenshot of the root window:

```
$ xwd -root -out screenshot.xwd

```

**Note:** The methods for taking shots of active windows with `import` can also be used with `xwd`.

### scrot

**Note:** According to [this thread](http://comments.gmane.org/gmane.comp.misc.suckless/6901), `[scrot](https://www.archlinux.org/packages/?name=scrot) -s` does not work with [dwm](https://www.archlinux.org/packages/?name=dwm).

[scrot](https://www.archlinux.org/packages/?name=scrot), enables taking screenshots from the CLI and offers features such as a user-definable time delay. Unless instructed otherwise, it saves the file in the current working directory.

```
$ scrot -t 20 -d 5

```

The above command saves a dated `.png` file, along with a thumbnail (20% of original), for Web posting. It provides a 5 second delay before capturing in this instance.

You can also use standard date and time formatting when saving to a file. e.g.,

```
$ scrot ~/screenshots/%Y-%m-%d-%T-screenshot.png

```

saves the screenshot in a filename with the current year, month, date, hours, minutes, and seconds to a folder in your home directory called "screenshots"

See `man scrot` for more information. You can simply automate the file to uploaded like so [[1]](https://github.com/kaihendry/Kai-s--HOME/tree/master/bin).

### escrotum

[escrotum-git](https://aur.archlinux.org/packages/escrotum-git/)<sup><small>AUR</small></sup> screen capture using pygtk, inspired by scrot

Created because scrot has glitches when selection mode is used with refreshing windows.

Because the command line interface its almost the same as scrot, can be used as a replacement of it.

### imlib2

[imlib2](https://www.archlinux.org/packages/?name=imlib2) provides a binary `imlib2_grab` to take screenshots. To take a screenshot of the full screen, type:

```
$ imlib2_grab screenshot.png

```

Note that [scrot](https://www.archlinux.org/packages/?name=scrot) actually uses `imlib2`.

### maim

[maim-git](https://aur.archlinux.org/packages/maim-git/)<sup><small>AUR</small></sup> is aimed to be an improved scrot.

Takes screenshots of your desktop using imlib2 and [slop](https://github.com/naelstrof/slop) for regions. It's meant to overcome shortcomings of scrot and performs better in [several ways](https://github.com/naelstrof/maim#why-use-maim-over-import-or-scrot).

### FFmpeg

[FFmpeg](/index.php/FFmpeg "FFmpeg") provides an x11grab device that allows the screen to be captured in X11.

Take a screenshot on a _width_ x _height_ display:

```
$ ffmpeg -f x11grab -video_size _width_x_height_ -i $DISPLAY -vframes 1 screen.png

```

Here, the PNG codec is used as it's lossless and suitable for screenshots, but any image codec can be used.

The same device allows for screencasting (on a display with a refresh rate of _rate_ HZ):

```
$ ffmpeg -f x11grab -video_size _width_x_height_ -framerate _rate_ -i $DISPLAY -c:v libx264 -preset ultrafast cast.mkv

```

Here, the x264 codec with the fastest possible encoding speed is used. Other codecs can be used; if writing each frame is too slow (either due to inadequate disk performance or slow encoding), then frames will be dropped and video output will be choppy.

### Weston

In the [Weston](/index.php/Wayland#Weston "Wayland") Wayland compositor, screenshots can be taking by pressing `Super+s`, which are stored in Weston's current working directory. Screencasts are also supported; recording is started and stopped by pressing `Super+r`, which will create a file called `capture.wcap` in Weston's current working directory. The capture can be decoded to YUV format by running `wcap-decode --yuv4mpeg2 capture.wcap`; the output of this command can be written to a file or piped into FFmpeg for further processing.

## Details: desktop environment specific

### Spectacle

If you use [KDE](/index.php/KDE "KDE"), you might want to use `Spectacle`.

Spectacle is provided by the [spectacle](https://www.archlinux.org/packages/?name=spectacle).

### Xfce Screenshooter

If you use [Xfce](/index.php/Xfce "Xfce") you can install [xfce4-screenshooter](https://www.archlinux.org/packages/?name=xfce4-screenshooter) and then add a keyboard binding:

_Xfce Menu > Settings > Keyboard > Application Shortcuts_

If you want to skip the Screenshot prompt, type `$ xfce4-screenshooter -h` in terminal for the options.

### GNOME

[GNOME](/index.php/GNOME "GNOME") users can press `Prnt Scr` or _Apps > Accessories > Take Screenshot_. You may need to install [gnome-screenshot](https://www.archlinux.org/packages/?name=gnome-screenshot).

### Cinnamon

The default installation of [Cinnamon](/index.php/Cinnamon "Cinnamon") does not provide a screenshot utility. Installing [gnome-screenshot](https://www.archlinux.org/packages/?name=gnome-screenshot) will enable screenshots through the _Menu > Accessories > Screenshot_ or by pressing `Prnt Scr`.

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

If the `Print` above does not work, see [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") and use different _keysym_ or _keycode_.

## Terminal

### Output with ansi codes

You can use the `script` command, part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package. Just enter `$ script` and from that moment, all the output is going to be saved to the `typescript` file, including the ansi codes.

Once you are done, just type `exit` and the `typescript` would ready. The resulting file can be converted to html using the package [ansi2html](https://aur.archlinux.org/packages/ansi2html/)<sup><small>AUR</small></sup>, from the [AUR](/index.php/AUR "AUR").

To convert the `typescript` file to `typescript.html`, do the following:

```
$ ansi2html --bg=dark < typescript > typescript.html

```

Actually, **some** commands can be piped directly to ansi2html:

```
$ ls --color|ansi2html --bg=dark >output.html

```

That does not work on every single case, so in those cases, using `script` is mandatory.

### Virtual console

Install a [framebuffer](/index.php/Framebuffer "Framebuffer") and use [fbgrab](https://www.archlinux.org/packages/?name=fbgrab) or [fbdump](https://www.archlinux.org/packages/?name=fbdump) to take a screenshot.

If you merely want to capture the text in the console and not an actual image, you can use `setterm`, which is part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package. The following command will dump the textual contents of virtual console 1 to a file screen.dump in the current directory:

```
# setterm -dump 1 -file screen.dump

```

Root permission is needed because the contents of `/dev/vcs1` need to be read.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Taking_a_screenshot&oldid=417224](https://wiki.archlinux.org/index.php?title=Taking_a_screenshot&oldid=417224)"