# Xcompmgr

[Xcompmgr](http://cgit.freedesktop.org/xorg/app/xcompmgr/) is a simple [composite manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager") capable of rendering drop shadows and, with the use of the **transset** utility, primitive window transparency. Designed solely as a proof-of-concept, Xcompmgr is a lightweight alternative to Compiz and similar composite managers.

Because it does not replace any existing window manager, it is an ideal solution for users of lightweight [window managers](/index.php/Window_managers "Window managers"), seeking a more elegant desktop.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Forks and updated versions](#Forks_and_updated_versions)
*   [2 Configuration](#Configuration)
    *   [2.1 Window transparency](#Window_transparency)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Start/Stop Xcompmgr on demand](#Start.2FStop_Xcompmgr_on_demand)
    *   [3.2 Toggle Xcompmgr](#Toggle_Xcompmgr)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Mozilla Firefox crashes when entering a Flash site](#Mozilla_Firefox_crashes_when_entering_a_Flash_site)
    *   [4.2 Background turns light gray briefly after logging in (e.g. in Openbox)](#Background_turns_light_gray_briefly_after_logging_in_.28e.g._in_Openbox.29)
    *   [4.3 BadPicture request in awesome](#BadPicture_request_in_awesome)
    *   [4.4 Screen not updating in awesome after resolution change](#Screen_not_updating_in_awesome_after_resolution_change)

## Installation

Before installing Xcompmgr, make sure you have installed and correctly configured [Xorg](/index.php/Xorg "Xorg"). To make sure the [Composite](/index.php/Composite "Composite") extension is enabled for the X Server, run:

 `$ xdpyinfo | grep Composite`  `Composite` 

If there is no output, add the `Composite` option to the `Extensions` section of xorg.conf:

 `/etc/X11/xorg.conf` 

```
Section "Extensions"
        Option  "Composite" "true"
EndSection
```

Xcompmgr can be [installed](/index.php/Pacman "Pacman") with the package [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr), available in the [official repositories](/index.php/Official_repositories "Official repositories"). For transparency also install [transset-df](https://www.archlinux.org/packages/?name=transset-df) from the [official repositories](/index.php/Official_repositories "Official repositories"). See [Xterm#Automatic transparency](/index.php/Xterm#Automatic_transparency "Xterm") for an example.

### Forks and updated versions

There are some forks available, with various bugfixes:

*   **xcompmgr-dana** — One of the first forks of Xcompmgr.

	[http://oliwer.net/xcompmgr-dana/](http://oliwer.net/xcompmgr-dana/) || [xcompmgr-dana](https://aur.archlinux.org/packages/xcompmgr-dana/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xcompmgr-dana)]</sup>

*   **[Compton](/index.php/Compton "Compton")** — A fork of Xcompmgr that contains most of the previous fixes as well as many others.

	[https://github.com/chjj/compton](https://github.com/chjj/compton) || [compton-git](https://aur.archlinux.org/packages/compton-git/)<sup><small>AUR</small></sup>

## Configuration

To load `xcompmgr`, simply run:

```
$ xcompmgr -c

```

To have it load at session start, add the following to [xprofile](/index.php/Xprofile "Xprofile"):

```
xcompmgr -c &

```

Instead of `-c` you can experiment with the other switches to modify the drop-shadows or even enable fading. Below is a common example:

```
xcompmgr -c -C -t-5 -l-5 -r4.2 -o.55 &

```

For a full list of options, run:

```
$ xcompmgr --help

```

### Window transparency

Although its practical use is limited, due to its slow performance, the `transset-df` utility can be used to set the transparency of individual windows.

To set the transparency of a program window, make sure the desired program is already running, then execute:

```
$ transset-df _opacity_

```

where _opacity_ is a number between **0** and **1**, 0 being transparent and 1 being opaque.

Once execution, the mouse cursor will transform to a cross-hair. Click a window and its transparency will change to the value specified. For example, `transset-df 0.25` will set the target window to 25% opacity (75% transparency).

## Tips and tricks

### Start/Stop Xcompmgr on demand

This script allows easy (re)starting and stopping of the compositing manager.

 `~/.bin/comp` 

```
#!/bin/bash
#
# Start a composition manager.
# (xcompmgr in this case)

comphelp() {
    echo "Composition Manager:"
    echo "   (re)start: COMP"
    echo "   stop:      COMP -s"
    echo "   query:     COMP -q"
    echo "              returns 0 if composition manager is running, else 1"
    exit
}

checkcomp() {
    pgrep xcompmgr &>/dev/null
}

stopcomp() {
    checkcomp && killall xcompmgr
}

startcomp() {
    stopcomp
    # Example settings only. Replace with your own.
    xcompmgr -CcfF -I-.015 -O-.03 -D6 -t-1 -l-3 -r4.2 -o.5 &
    exit
}

case "$1" in
    "")   startcomp ;;
    "-q") checkcomp ;;
    "-s") stopcomp; exit ;;
    *)    comphelp ;;
esac

```

For ease of use, you can bind this script to a hot-key using, for example, [Xbindkeys](/index.php/Xbindkeys "Xbindkeys"). This allows for fast restart or temporary composition removal if needed without interrupting other work.

### Toggle Xcompmgr

Assign the following script to any hot-key:

```
#!/bin/bash

if pgrep xcompmgr &>/dev/null; then
    echo "Turning xcompmgr ON"
    xcompmgr -c -C -t-5 -l-5 -r4.2 -o.55 &
else
    echo "Turning xcompmgr OFF"
    pkill xcompmgr &
fi

exit 0

```

## Troubleshooting

### Mozilla Firefox crashes when entering a Flash site

You can fix it by creating an executable file named `/etc/profile.d/flash.sh` containing this line:

```
export XLIB_SKIP_ARGB_VISUALS=1

```

**Warning:** This will disable compositing effects.

### Background turns light gray briefly after logging in (e.g. in Openbox)

This is fixed by installing [hsetroot](https://aur.archlinux.org/packages/hsetroot/)<sup><small>AUR</small></sup> and setting the background color by executing `hsetroot -solid "#000000"` (just type the code of the color you want instead of _#000000_) before `xcompmgr`.

### BadPicture request in awesome

If you get the following error in [awesome](/index.php/Awesome "Awesome"):

```
 error 163: BadPicture request 149 minor 8 serial 34943
 error 163: BadPicture request 149 minor 8 serial 34988
 error 163: BadPicture request 149 minor 8 serial 35033

```

just install [feh](/index.php/Feh "Feh") and restart [awesome](/index.php/Awesome "Awesome").

### Screen not updating in awesome after resolution change

When using an external monitor, you may encounter problems when automatically changing display resolutions: a part of the screen becomes "stuck" and no longer updates itself. This problem occurs because of the initial resolution change (happening before Xcompmgr starts) as well as [awesome](/index.php/Awesome "Awesome") setting the background via [feh](/index.php/Feh "Feh").

To fix it, you need to install [hsetroot](https://aur.archlinux.org/packages/hsetroot/)<sup><small>AUR</small></sup>, from the [official repositories](/index.php/Official_repositories "Official repositories"), and put the following line in `.xinitrc`, just before `xcompmgr`:

```
hsetroot -solid "#000066"

```

(you can replace _#000066_ with your color of choice).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xcompmgr&oldid=410109](https://wiki.archlinux.org/index.php?title=Xcompmgr&oldid=410109)"