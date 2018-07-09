[Compton](https://github.com/chjj/compton) is a standalone [compositor](/index.php/Compositor "Compositor") for [Xorg](/index.php/Xorg "Xorg"), suitable for use with [window managers](/index.php/Window_managers "Window managers") that do not provide compositing. Compton is a fork of [xcompmgr-dana](http://oliwer.net/xcompmgr-dana/), which in turn is a fork of [xcompmgr](/index.php/Xcompmgr "Xcompmgr").

**Note:** Compton is currently dormant (last code change 2016) and may cause issues depending on your configuration, see [#Troubleshooting](#Troubleshooting).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Autostarting](#Autostarting)
    *   [2.2 Command only](#Command_only)
    *   [2.3 Using a configuration file](#Using_a_configuration_file)
        *   [2.3.1 Disable shadows for some windows](#Disable_shadows_for_some_windows)
*   [3 Multihead](#Multihead)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Freezing video playback](#Freezing_video_playback)
    *   [4.2 Conky](#Conky)
    *   [4.3 dwm | dmenu](#dwm_.7C_dmenu)
    *   [4.4 Firefox](#Firefox)
    *   [4.5 slock](#slock)
    *   [4.6 Corrupted screen contents with Intel graphics](#Corrupted_screen_contents_with_Intel_graphics)
    *   [4.7 Flicker](#Flicker)
    *   [4.8 Fullscreen tearing](#Fullscreen_tearing)
    *   [4.9 Lag when using xft fonts](#Lag_when_using_xft_fonts)
    *   [4.10 Screen artifacts/screenshot issues when using AMD's Catalyst driver](#Screen_artifacts.2Fscreenshot_issues_when_using_AMD.27s_Catalyst_driver)
    *   [4.11 Tabbed windows](#Tabbed_windows)
    *   [4.12 Unable to change the background color with xsetroot](#Unable_to_change_the_background_color_with_xsetroot)
    *   [4.13 Lag with Nvidia proprietary drivers and FullCompositionPipeline](#Lag_with_Nvidia_proprietary_drivers_and_FullCompositionPipeline)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [compton](https://www.archlinux.org/packages/?name=compton) or its [git](/index.php/Git "Git") version, [compton-git](https://aur.archlinux.org/packages/compton-git/).

[compton-conf](https://aur.archlinux.org/packages/compton-conf/) or [compton-conf-git](https://aur.archlinux.org/packages/compton-conf-git/) package provide [Qt](/index.php/Qt "Qt")-based GUI for Compton configuration.

## Usage

See [compton(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/compton.1). Compton may be manually enabled or disabled at any time during a session, or autostarted as a background ([Daemon](/index.php/Daemon "Daemon")) process for sessions. There are also several optional arguments that may be used to tweak the compositing effects provided. These include:

*   `-b`: Run as a background ([Daemon](/index.php/Daemon "Daemon")) process for a session (e.g. when autostarting for a [window manager](/index.php/Window_manager "Window manager") such as [Openbox](/index.php/Openbox "Openbox"))
*   `-c`: Enable shadow effects
*   `-C`: Disable shadow effects on panels and docks
*   `-G`: Disable shadow effects for application windows and drag-and-drop objects
*   `--config`: Use a specified configuration file

Many more options are available, including to set timing, displays to be managed, and the opacity of menus, window borders, and inactive application menus. See the [Compton Man Page](https://github.com/chjj/compton/blob/master/man/compton.1.asciidoc) for further information.

**Note:** If a different [composite manager](/index.php/Composite_manager "Composite manager") is running, it should be disabled before starting *compton*.

### Autostarting

How compton would be autostarted as a [Daemon](/index.php/Daemon "Daemon") process will depend on the [desktop environment](/index.php/Desktop_environment "Desktop environment") or [window manager](/index.php/Window_manager "Window manager") used. For example, for [Openbox](/index.php/Openbox "Openbox") the `~/.config/openbox/autostart` file must be edited, while for [i3](/index.php/I3 "I3") it would be the `~/.i3/config` file. Where necessary, compton may also be autostarted from [xprofile](/index.php/Xprofile "Xprofile") or [Xinitrc](/index.php/Xinitrc "Xinitrc"). Read the [startup files](/index.php/Startup_files "Startup files") article for further information.

### Command only

To manually enable default compositing effects during a session, use the following command:

```
$ compton

```

Alternatively, to disable all shadowing effects during a session, the `-C` and `-G` arguments must be added:

```
$ compton -CG

```

To autostart compton as a background ([Daemon](/index.php/Daemon "Daemon")) process for a session, the `-b` argument must be used:

```
$ compton -b

```

To disable all shadowing effects from the [Daemon](/index.php/Daemon "Daemon") process, the `-C` and `-G` arguments must again be added:

```
$ compton -CGb

```

Finally, this is an example where additional arguments that require values to be set have been used:

```
$ compton -cCGfF -o 0.38 -O 200 -I 200 -t 0 -l 0 -r 3 -D2 -m 0.88

```

### Using a configuration file

The default configuration is available in `/etc/xdg/compton.conf`. For modifications, it can be copied to `~/.config/compton.conf`, or to `~/.compton.conf`.

To use a custom configuration file with compton during a session, use the following command:

```
$ compton --config *path/to/compton.conf*

```

To auto-start compton as a background ([Daemon](/index.php/Daemon "Daemon")) process for a session, specify the `-b` argument:

```
$ compton --config *path/to/compton.conf* -b

```

#### Disable shadows for some windows

The `shadow-exclude` option can disable shadows for windows if required. For currently disabled windows, see [here](https://projects.archlinux.org/svntogit/community.git/tree/trunk/compton.conf?h=packages/compton#n80).

To disable shadows for menus add the following to wintypes in `compton.conf`:

```
# menu        = { shadow = false; };
dropdown_menu = { shadow = false; };
popup_menu    = { shadow = false; };
# utility     = { shadow = false; };

```

## Multihead

If a [multihead](/index.php/Multihead "Multihead") configuration is used without xinerama - meaning that X server is started with more than one screen - then compton will start on only one screen by default. It can be started on all screens by using the `-d` argument. For example, to run on X screen 0 in the background:

```
 compton -b -d :0

```

The above should work on all monitors, but if it doesn't try an older method that manually specifies each one:

```
seq 0 3 | xargs -l1 -I@ compton -b -d :0.@

```

## Troubleshooting

The use of compositing effects may on occasion cause issues such as visual glitches when not configured correctly for use with other applications and programs.

### Freezing video playback

Some media players may experience an issue where the video will momentarily freeze while the audio continues to play. There is currently no known fix aside from stopping Compton while playing videos.

See the [bug report](https://github.com/chjj/compton/issues/494).

### Conky

To disable shadows around [Conky](/index.php/Conky "Conky") windows, have the following in `~/.conkyrc`:

```
own_window_class conky

```

### dwm | dmenu

dwm's statusbar is not detected by any of compton's functions to automatically exclude window manager elements. Neither dwm statusbar nor dmenu have a static window id. If you want to exclude it from inactive window transparency (or other), you'll have to either patch a window class into the source code of each, or exclude by less precise attributes. The following example is with dwm's status on top, which allows a resolution independent of location exclusion:

```
$ compton <any other arguments> --focus-exclude "x = 0 && y = 0 && override_redirect = true"

```

Otherwise, where using a configuration file:

```
focus-exclude = "x = 0 && y = 0 && override_redirect = true";

```

The override redirect property seems to be false for most windows- having this in the exclusion rule prevents other windows drawn in the upper left corner from being excluded (for example, when dwm statusbar is hidden, x0 y0 will match whatever is in dwm's master stack).

### Firefox

To disable shadows for Firefox elements add the following to shadow-exclude in `compton.conf`:

```
"class_g = 'Firefox' && argb",

```

See [[1]](https://github.com/chjj/compton/issues/201#issuecomment-45288510) for more information.

### slock

Where inactive window transparency has been enabled (the `-i` argument when running as a command), this may provide troublesome results when also using [slock](/index.php/Slock "Slock"). One solution is to amend the transparency to `0.2`. For example, where running compton arguments as a command:

```
$ compton <any other arguments> -i 0.2

```

Otherwise, where using a configuration file:

```
inactive-dim = 0.2;

```

Alternatively, you may try to exclude slock by its window id, or by excluding all windows with no name.

**Note:** Some programs change their id for every new instance, but slock's appears to be static. Someone more knowledgeable will have to confirm that slock's id is in fact static- until then, use at your own risk.

Exclude all windows with no name from compton using the following options:

```
$ compton <other arguments> --focus-exclude "! name~=''"

```

Find your slock's window id by running the command:

```
$ xwininfo & slock

```

Quickly click anywhere on the screen (before slock exits), then type your password to unlock. You should see the window id in the output:

```
xwininfo: Window id: 0x1800001 (has no name)

```

Take the window id and exclude it from compton with:

```
$ compton <any other arguments> --focus-exclude 'id = 0x1800001'

```

Otherwise, where using a configuration file:

```
focus-exclude = "id = 0x1800001";

```

### Corrupted screen contents with Intel graphics

On at least some Intel chipsets, DRI3 is known to cause [trouble](https://bugs.freedesktop.org/show_bug.cgi?id=97916) for compton when the display resolution is changed or a new monitor is connected. This can happen with either the `intel` or `modesetting` driver. A workaround is to run compton with the `--paint-on-overlay` option.

### Flicker

Applies to fully maximized windows (in sessions without any panels) with the default `compton.conf` caused and resolved by the following option:

```
unredir-if-possible = false;

```

See [[2]](https://github.com/chjj/compton/issues/402) for more information.

### Fullscreen tearing

If you observe screen tearing of video playback only in fullscreen mode see [#Flicker](#Flicker).

### Lag when using xft fonts

If you experience heavy lag when using Xft fonts in applications such as [xterm](/index.php/Xterm "Xterm") or [urxvt](/index.php/Urxvt "Urxvt") try:

```
--xrender-sync --xrender-sync-fence

```

Or the xrender backend.

See [[3]](https://github.com/chjj/compton/issues/152) for more information.

### Screen artifacts/screenshot issues when using AMD's Catalyst driver

Try running Compton with:

```
--backend xrender

```

Or add

```
backend = "xrender";

```

to your `compton.conf` file.

See [[4]](https://github.com/chjj/compton/issues/208) for more information.

### Tabbed windows

When windows with transparency are tabbed, the underlying tabbed windows are still visible because of transparency. Each tabbed window also draws its own shadow resulting in multiple shadows.

Removing the multiple shadows issue can be done by adding the following to the already existing [shadow-exclude list](https://projects.archlinux.org/svntogit/community.git/tree/trunk/compton.conf?h=packages/compton#n80):

```
"_NET_WM_STATE@:32a *= '_NET_WM_STATE_HIDDEN'"

```

Not drawing underlying tabbed windows can be enabled by adding the following to your `compton.conf`:

```
opacity-rule = [
  "95:class_g = 'URxvt' && !_NET_WM_STATE@:32a",
  "0:_NET_WM_STATE@:32a *= '_NET_WM_STATE_HIDDEN'"
];

```

Note that `URxvt` is the Xorg class name of your terminal. Change this if you use a different terminal. You can query a window's class by running the command `xprop WM_CLASS` and clicking the window.

See [[5]](https://www.reddit.com/r/unixporn/comments/330zxl/webmi3_no_more_overlaying_shadows_and_windows_in/) for more information.

### Unable to change the background color with xsetroot

Currently, compton is incompatible with `xsetroot`'s `-solid` option, a workaround is to use [hsetroot](https://aur.archlinux.org/packages/hsetroot/) to set the background color:

```
$ hsetroot -solid '#000000'

```

See [[6]](https://github.com/chjj/compton/issues/162) for more information.

### Lag with Nvidia proprietary drivers and FullCompositionPipeline

See [Screen artifacts/screenshot issues when using AMD's Catalyst driver](https://wiki.archlinux.org/index.php/Compton#Screen_artifacts.2Fscreenshot_issues_when_using_AMD.27s_Catalyst_driver).

## See also

*   [Howto: Using Compton for tear-free compositing on XFCE or LXDE](http://ubuntuforums.org/showthread.php?t=2144468&p=12644745#post12644745)