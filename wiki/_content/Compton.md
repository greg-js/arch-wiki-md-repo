# Compton

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Compton is a lightweight, standalone composite manager, suitable for use with [window managers](/index.php/Window_managers "Window managers") that do not natively provide compositing functionality. Compton itself is a fork of [xcompmgr-dana](https://aur.archlinux.org/packages/xcompmgr-dana/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xcompmgr-dana)]</sup>, which in turn is a fork of [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr). See the [compton github page](https://github.com/chjj/compton) for further information.

Compton in particular is notable for fixing numerous bugs found in its predecessors, and as such, is popular due to its reliability and stability. Numerous additional improvements and configuration options have also been implemented, including a faster GLX (OpenGL) backend (disabled by default), default inactive/active window opacity, window frame transparency, window background blur, window color inversion, painting rate throttling, VSync, condition-based fine-tune control, configuration file reading, and D-Bus control.

## Contents

*   [1 Installation](#Installation)
*   [2 Use](#Use)
    *   [2.1 Autostarting](#Autostarting)
    *   [2.2 Command only](#Command_only)
    *   [2.3 Using a configuration file](#Using_a_configuration_file)
        *   [2.3.1 Disable conky shadowing](#Disable_conky_shadowing)
*   [3 Multihead](#Multihead)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Slock](#Slock)
    *   [4.2 Dual shadow on some GTK3 applications](#Dual_shadow_on_some_GTK3_applications)
    *   [4.3 Unable to change the background color with xsetroot](#Unable_to_change_the_background_color_with_xsetroot)
    *   [4.4 Screen artifacts/screenshot issues when using AMD's Catalyst driver](#Screen_artifacts.2Fscreenshot_issues_when_using_AMD.27s_Catalyst_driver)
    *   [4.5 High CPU use with nvidia drivers](#High_CPU_use_with_nvidia_drivers)
*   [5 See also](#See_also)

## Installation

Install [compton](https://aur.archlinux.org/packages/compton/)<sup><small>AUR</small></sup> or its [git](/index.php/Git "Git") version, [compton-git](https://aur.archlinux.org/packages/compton-git/)<sup><small>AUR</small></sup>.

## Use

Compton may be manually enabled or disabled at any time during a session, or autostarted as a background ([Daemon](/index.php/Daemon "Daemon")) process for sessions. There are also several optional arguments that may be used to tweak the compositing effects provided. These include:

*   `-b`: Run as a background ([Daemon](/index.php/Daemon "Daemon")) process for a session (e.g. when autostarting for a [window manager](/index.php/Window_manager "Window manager") such as [Openbox](/index.php/Openbox "Openbox"))
*   `-c`: Enable shadow effects
*   `-C`: Disable shadow effects on panels and docks
*   `-G`: Disable shadow effects for application windows and drag-and-drop objects
*   `--config`: Use a specified configuration file

Many more options are availble, including to set timing, displays to be managed, and the opacity of menus, window borders, and inactive application menus. See the [Compton Man Page](https://github.com/chjj/compton/blob/master/man/compton.1.asciidoc) for further information.

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
compton -b

```

To disable all shadowing effects from the [Daemon](/index.php/Daemon "Daemon") process, the `-C` and `-G` arguments must again be added:

```
compton -CGb

```

Finally, this is an example where additional arguments that require values to be set have been used:

```
compton -cCGfF -o 0.38 -O 200 -I 200 -t 0 -l 0 -r 3 -D2 -m 0.88

```

### Using a configuration file

To use a custom configuration file with compton during a session, use the following command:

```
compton --config <path/to/compton.conf>

```

To auto-start compton as a background ([Daemon](/index.php/Daemon "Daemon")) process for a session, the `-b` argument must again be used:

```
compton --config <path/to/compton.conf> -b

```

It is recommended to either create the configuration file in the hidden `~/.config` directory (`~/.config/compton.conf`) or as a hidden file in the `Home` directory (`~/.compton.conf`). A sample config file can be found here: [Compton Sample Config](https://github.com/chjj/compton/blob/master/compton.sample.conf)

#### Disable conky shadowing

To disable shadows around [conky](/index.php/Conky "Conky") windows - where used - first amend the conky configuration file `~/.conkyrc` as follows:

```
own_window_class conky

```

Then amend the compton configuration file as follows:

```
shadow-exclude = "class_g = 'conky'";

```

## Multihead

If a [multihead](/index.php/Multihead "Multihead") configuration is used without xinerama - meaning that X server is started with more than one screen - then compton will start on only one screen by default. It can be started on all screens by using the `-d` argument. For example, compton can be executed for 4 monitors with the following command:

```
seq 0 3 | xargs -l1 -I@ compton -b -d :0.@

```

## Troubleshooting

The use of compositing effects may on occasion cause issues such as visual glitches when not configured correctly for use with other applications and programs.

### Slock

**Note:** Use of the `--focus-exclude` argument may be a cleaner solution.

Where inactive window transparency has been enabled (the `-i` argument when running as a command), this may provide troublesome results when also using [slock](/index.php/Slock "Slock"). The solution is to amend the transparency to `0.2`. For example, where running compton arguments as a command:

```
compton <any other arguments> -i 0.2

```

Otherwise, where using a configuration file:

```
inactive-dim = 0.2;

```

### Dual shadow on some GTK3 applications

Since [gtk3](https://www.archlinux.org/packages/?name=gtk3) version 3.12.1, some GTK+ 3 windows and dialogs render a double shadow when used with Compton. This is because both shadows from GTK+ 3 and Compton are [applied concurrently](https://github.com/chjj/compton/issues/189). See [GTK+#Client-side decorations](/index.php/GTK%2B#Client-side_decorations "GTK+").

To disable Compton shadows on all GTK +3 windows, add a new rule to `compton.conf`:

 `shadow-exclude = [ "_GTK_FRAME_EXTENTS@:c" ]` 

or run `compton` with the following arguments: `--shadow-exclude 'argb && _NET_WM_OPAQUE_REGION@:c'`

### Unable to change the background color with xsetroot

Currently, compton is incompatible with `xsetroot`'s `-solid` option, a workaround is to use [hsetroot](https://aur.archlinux.org/packages/hsetroot/)<sup><small>AUR</small></sup> to set the background color:

```
$ hsetroot -solid '#000000'

```

For a detailed explaination, please see [https://github.com/chjj/compton/issues/162](https://github.com/chjj/compton/issues/162).

### Screen artifacts/screenshot issues when using AMD's Catalyst driver

Try running compton with

```
--backend xrender

```

or adding

```
backend = "xrender";

```

to your compton.conf file.

For more info, please see [https://github.com/chjj/compton/issues/208](https://github.com/chjj/compton/issues/208)

### High CPU use with nvidia drivers

When facing high CPU use with `--backend glx` or tearing with `--vsync` enabled, [install](/index.php/Install "Install") [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl) as described in [NVIDIA](/index.php/NVIDIA "NVIDIA").

## See also

*   [Howto: Using Compton for tear-free compositing on XFCE or LXDE](http://ubuntuforums.org/showthread.php?t=2144468&p=12644745#post12644745)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Compton&oldid=400530](https://wiki.archlinux.org/index.php?title=Compton&oldid=400530)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [X server](/index.php/Category:X_server "Category:X server")
*   [Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")