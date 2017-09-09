Related articles

*   [xmobar](/index.php/Xmobar "Xmobar")

[xmonad](http://xmonad.org/) is a tiling [window manager](/index.php/Window_manager "Window manager") for [X](/index.php/X "X"). Windows are arranged automatically to tile the screen without gaps or overlap, maximizing screen use. Window manager features are accessible from the keyboard: a mouse is optional.

xmonad is written, configured and extensible in [Haskell](http://haskell.org/). Custom layout algorithms, key bindings and other extensions may be written by the user in configuration files.

Layouts are applied dynamically, and different layouts may be used on each workspace. [Xinerama](https://en.wikipedia.org/wiki/Xinerama "wikipedia:Xinerama") is fully supported, allowing windows to be tiled on several physical screens.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting xmonad](#Starting_xmonad)
*   [3 Configuration](#Configuration)
    *   [3.1 A base desktop configuration](#A_base_desktop_configuration)
*   [4 Exiting xmonad](#Exiting_xmonad)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 X-Selection-Paste](#X-Selection-Paste)
    *   [5.2 Keyboard shortcuts](#Keyboard_shortcuts)
    *   [5.3 Targeting unbound keys:](#Targeting_unbound_keys:)
    *   [5.4 Increase the number of workspaces](#Increase_the_number_of_workspaces)
    *   [5.5 Making room for docks/panels/trays (Xmobar, Tint2, Conky, etc)](#Making_room_for_docks.2Fpanels.2Ftrays_.28Xmobar.2C_Tint2.2C_Conky.2C_etc.29)
    *   [5.6 Using xmobar with xmonad](#Using_xmobar_with_xmonad)
        *   [5.6.1 Quick, less flexible](#Quick.2C_less_flexible)
        *   [5.6.2 More configurable](#More_configurable)
        *   [5.6.3 Verify XMobar config](#Verify_XMobar_config)
    *   [5.7 Controlling xmonad with external scripts](#Controlling_xmonad_with_external_scripts)
    *   [5.8 Launching another window manager within xmonad](#Launching_another_window_manager_within_xmonad)
    *   [5.9 KDE and xmonad](#KDE_and_xmonad)
    *   [5.10 IM Layout for Skype](#IM_Layout_for_Skype)
    *   [5.11 Example configurations](#Example_configurations)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 GNOME 3 and xmonad](#GNOME_3_and_xmonad)
        *   [6.1.1 Compositing in GNOME and Xmonad](#Compositing_in_GNOME_and_Xmonad)
    *   [6.2 Xfce 4 and xmonad](#Xfce_4_and_xmonad)
    *   [6.3 Missing xmonad-i386-linux or xmonad-x86_64-linux](#Missing_xmonad-i386-linux_or_xmonad-x86_64-linux)
    *   [6.4 Problems with Java applications](#Problems_with_Java_applications)
    *   [6.5 Empty space at the bottom of gvim or terminals](#Empty_space_at_the_bottom_of_gvim_or_terminals)
    *   [6.6 Chromium/Chrome will not go fullscreen](#Chromium.2FChrome_will_not_go_fullscreen)
    *   [6.7 Multitouch / touchegg](#Multitouch_.2F_touchegg)
    *   [6.8 Keybinding issues with an azerty keyboard layout](#Keybinding_issues_with_an_azerty_keyboard_layout)
    *   [6.9 GNOME 3 mod4+p changes display configuration instead of launching dmenu](#GNOME_3_mod4.2Bp_changes_display_configuration_instead_of_launching_dmenu)
    *   [6.10 Problems with focused border in VirtualBox](#Problems_with_focused_border_in_VirtualBox)
    *   [6.11 Steam games (Half-Life, Left 4 Dead, …) and xmonad](#Steam_games_.28Half-Life.2C_Left_4_Dead.2C_.E2.80.A6.29_and_xmonad)
    *   [6.12 LibreOffice - focus flicking between main window and dialog](#LibreOffice_-_focus_flicking_between_main_window_and_dialog)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xmonad](https://www.archlinux.org/packages/?name=xmonad) package which provides a very basic configuration, ideally also install [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) for most notably a more useful desktop configuration as well as additional tiling algorithms, configurations, scripts, etc.

Alternatively, install [xmonad-git](https://aur.archlinux.org/packages/xmonad-git/), the development version, with some additional dependencies; and likewise [xmonad-contrib-git](https://aur.archlinux.org/packages/xmonad-contrib-git/).

**Note:** If you choose to use the [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") repositories, you need to install the *haskell-xmonad* package instead of [xmonad](https://www.archlinux.org/packages/?name=xmonad), as they have different dependencies.

## Starting xmonad

Select *Xmonad* from the session menu in a [display manager](/index.php/Display_manager "Display manager") of choice.

Alternatively, append `exec xmonad` to the `~/.xinitrc` file and then start the session by executing *startx*.

Make sure you have the [Xterm](/index.php/Xterm "Xterm") package installed or have changed the terminal emulator in the configuration. Otherwise you will not be able to do anything in Xmonad.

**Note:** By default, xmonad does not set an X cursor, therefore the "cross" cursor is usually displayed. To set the expected left-pointer, see [Cursor themes#Change X shaped default cursor](/index.php/Cursor_themes#Change_X_shaped_default_cursor "Cursor themes").

## Configuration

Create the `~/.xmonad` directory and the `~/.xmonad/xmonad.hs` file and edit it as described below.

After changes to `~/.xmonad/xmonad.hs` are made, use the Mod+q shortcut to recompile and have them take effect.

**Tip:** The default configuration for xmonad is quite usable and it is achieved by simply running without an `xmonad.hs` entirely.

Because the xmonad configuration file is written in Haskell, non-programmers may have a difficult time adjusting settings. For detailed HOWTO's and example configurations, we refer you to the following resources:

*   [xmonad wiki](http://wiki.haskell.org/Xmonad)
*   [xmonad configuration archive](http://wiki.haskell.org/Xmonad/Config_archive)
*   [xmonad FAQ](http://wiki.haskell.org/Xmonad/Frequently_asked_questions)
*   Arch Linux [forum thread](https://bbs.archlinux.org/viewtopic.php?id=40636)

The best approach is to only place your changes and customizations in `~/.xmonad/xmonad.hs` and write it such that any unset parameters are picked up from the built-in defaultConfig.

This is achieved by writing an `xmonad.hs` like this:

```
import XMonad

main = xmonad def
    { terminal    = "urxvt"
    , modMask     = mod4Mask
    , borderWidth = 3
    }

```

This simply overrides the default terminal and borderWidth while leaving all other settings at their defaults (inherited from the XConfig value defaultConfig).

As things get more complicated, it can be handy to call configuration options by function name inside the main function, and define these separately in their own sections of your `~/.xmonad/xmonad.hs`. This makes large customizations like your layout and manage hooks easier to visualize and maintain.

The simple `xmonad.hs` from above could have been written like this:

```
import XMonad

main = do
  xmonad $ defaultConfig
    { terminal    = myTerminal
    , modMask     = myModMask
    , borderWidth = myBorderWidth
    }

myTerminal    = "urxvt"
myModMask     = mod4Mask -- Win key or Super_L
myBorderWidth = 3

```

Also, order at top level (main, myTerminal, myModMask etc.), or within the {} does not matter in Haskell, as long as imports come first.

The following is taken from the 0.9 configuration file template. It is an example of the most common functions one might want to define in their main do block.

```
{
  terminal           = myTerminal,
  focusFollowsMouse  = myFocusFollowsMouse,
  borderWidth        = myBorderWidth,
  modMask            = myModMask,
  -- numlockMask deprecated in 0.9.1
  -- numlockMask        = myNumlockMask,
  workspaces         = myWorkspaces,
  normalBorderColor  = myNormalBorderColor,
  focusedBorderColor = myFocusedBorderColor,

  -- key bindings
  keys               = myKeys,
  mouseBindings      = myMouseBindings,

  -- hooks, layouts
  layoutHook         = myLayout,
  manageHook         = myManageHook,
  handleEventHook    = myEventHook,
  logHook            = myLogHook,
  startupHook        = myStartupHook
}

```

The package itself also includes a `xmonad.hs`, which is the latest official example `xmonad.hs` that comes with the **xmonad** Haskell module as an example of how to override everything. This should not be used as a template configuration, but as examples of parts you can pick to use in your own configuration. It is located in an architecture and version dependant directory in `/usr/share/` (e.g. `find /usr/share -name xmonad.hs`).

### A base desktop configuration

In [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) is a better default configuration for average desktop uses. It is also helps with problems in some modern programs like Chromium.

It can be added like so:

```
import XMonad
import XMonad.Config.Desktop

main = xmonad desktopConfig
    { terminal    = "urxvt"
    , modMask     = mod4Mask
    }

```

## Exiting xmonad

To end the current xmonad session, press `Mod+Shift+Q`. By default, `Mod` is the `Alt` key.

## Tips and tricks

### X-Selection-Paste

The keyboard-centered operation in Xmonad can be further supported with a keyboard shortcut for [X-Selection-Paste](/index.php/Keyboard_shortcuts#Key_binding_for_X-selection-paste "Keyboard shortcuts").

Also, there exists a function "pasteSelection" in XMonad.Util.Paste that can be bound to a key using a line like:

 `xmonad.hs` 
```
  import XMonad.Util.Paste -- Remember to include this line

  -- X-selection-paste buffer
  , ((0, xK_Insert), pasteSelection)
```

Pressing the "Insert" key will now paste the mouse buffer in the active window.

### Keyboard shortcuts

Default keyboard shortcuts are listed in the man page of xmonad.

### Targeting unbound keys:

If you use Xmonad as a stand alone window manager, you can edit the xmonad.hs to add unbound keyboard keys. You just need to find the Xf86 name of the key (such as XF86PowerDown) and look it up in `/usr/include/X11/XF86keysym.h`. It will give you a keycode (like 0x1008FF2A) which you can use to add a line like the following in the keybindings section of your `xmonad.hs`:

```
((0,               0x1008FF2A), spawn "sudo pm-suspend")

```

### Increase the number of workspaces

By default, xmonad uses a set of 9 workspaces. You can change this by changing the **workspaces** parameter:

 `xmonad.hs` 
```
import XMonad
import XMonad.Util.EZConfig (additionalKeys)

main=do
  xmonad $ defaultConfig
    { ...
    , workspaces = myWorkspaces
    , ...
    } `additionalKeys` myAdditionalKeys

myWorkspaces = ["1","2","3","4","5","6","7","8","9"] ++ (map snd myExtraWorkspaces) -- you can customize the names of the default workspaces by changing the list

myExtraWorkspaces = [(xK_0, "0")] -- list of (key, name)

myAdditionalKeys =
    [ -- ... your other hotkeys ...
    ] ++ [
        ((myModMask, key), (windows $ W.greedyView ws))
        | (key, ws) <- myExtraWorkspaces
    ] ++ [
        ((myModMask .|. shiftMask, key), (windows $ W.shift ws))
        | (key, ws) <- myExtraWorkspaces
    ]

```

### Making room for docks/panels/trays (Xmobar, Tint2, Conky, etc)

Wrap your layouts with avoidStruts from XMonad.Hooks.ManageDocks for automatic dock/panel/trayer spacing:

```
import XMonad
import XMonad.Hooks.ManageDocks

main=do
  xmonad $ defaultConfig
    { ...
    , layoutHook=avoidStruts $ layoutHook defaultConfig
    , manageHook=manageHook defaultConfig <+> manageDocks
    , ...
    }

```

If you ever want to toggle the gaps, this action can be added to your key bindings:

```
,((modMask x, xK_b     ), sendMessage ToggleStruts)

```

### Using xmobar with xmonad

**[xmobar](/index.php/Xmobar "Xmobar")** is a light and minimalistic text-based bar, designed to work with xmonad. To use xmobar with xmonad, you will need two packages in addition to the [xmonad](https://www.archlinux.org/packages/?name=xmonad) package. These packages are [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) and [xmobar](https://www.archlinux.org/packages/?name=xmobar) from the [official repositories](/index.php/Official_repositories "Official repositories"), or you can use [xmobar-git](https://aur.archlinux.org/packages/xmobar-git/) from the [AUR](/index.php/AUR "AUR") instead of the official [xmobar](https://www.archlinux.org/packages/?name=xmobar) package.

Here we will start xmobar from within xmonad, which reloads xmobar whenever you reload xmonad.

Open `~/.xmonad/xmonad.hs` in your favorite editor, and choose one of the two following options:

#### Quick, less flexible

**Note:** There is also [dzen2](https://www.archlinux.org/packages/?name=dzen2) which you can substitute for [xmobar](https://www.archlinux.org/packages/?name=xmobar) in either case.

Common imports:

```
import XMonad
import XMonad.Hooks.DynamicLog

```

The xmobar action starts xmobar and returns a modified configuration that includes all of the options described in [#More configurable](#More_configurable).

```
main = xmonad =<< xmobar defaultConfig { modMask = mod4Mask {- or any other configurations here ... -}}

```

#### More configurable

As of xmonad(-contrib) 0.9, there is a new [statusBar](https://hackage.haskell.org/package/xmonad-contrib-0.13/docs/XMonad-Hooks-DynamicLog.html#v:statusBar) function in [XMonad.Hooks.DynamicLog](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-DynamicLog.html). It allows you to use your own configuration for:

*   The command used to execute the bar
*   The PP that determines what is being written to the bar
*   The key binding to toggle the gap for the bar

The following is an example of how to use it:

 `~/.xmonad/xmonad.hs` 
```
-- Imports.
import XMonad
import XMonad.Hooks.DynamicLog

-- The main function.
main = xmonad =<< statusBar myBar myPP toggleStrutsKey myConfig

-- Command to launch the bar.
myBar = "xmobar"

-- Custom PP, configure it as you like. It determines what is being written to the bar.
myPP = xmobarPP { ppCurrent = xmobarColor "#429942" "" . wrap "<" ">" }

-- Key binding to toggle the gap for the bar.
toggleStrutsKey XConfig {XMonad.modMask = modMask} = (modMask, xK_b)

-- Main configuration, override the defaults to your liking.
myConfig = defaultConfig { modMask = mod4Mask }

```

#### Verify XMobar config

The template and default xmobarrc contains this.

At last, open up `~/.xmobarrc` and make sure you have `StdinReader` in the template and run the plugin. E.g.

 `~/.xmobarrc` 
```
Config { ...
       , commands = [ Run StdinReader .... ]
         ...
       , template = " %StdinReader% ... "
       }

```

Now, all you should have to do is either to start, or restart, xmonad.

### Controlling xmonad with external scripts

Here are a few ways to do it,

*   use the following xmonad extension, [XMonad.Hooks.ServerMode](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-ServerMode.html).

*   simulate keypress events using [xdotool](https://www.archlinux.org/packages/?name=xdotool) or similar programs. See this [Ubuntu forums thread](http://ubuntuforums.org/archive/index.php/t-658040.html). The following command would simulate the keypress `Super+n`:

```
xdotool key Super+n

```

*   [wmctrl](https://www.archlinux.org/packages/?name=wmctrl) -If you have desktopConfig or EwmhDesktops configured, this is a very easy to use and standard utility.

### Launching another window manager within xmonad

If you are using [xmonad-git](https://aur.archlinux.org/packages/xmonad-git/), as of January of 2011, you can restart to another window manager from within xmonad. You just need to write a small script, and add stuff to your `~/.xmonad/xmonad.hs`. Here is the script.

 `~/bin/obtoxmd` 
```
#!/bin/sh
openbox
xmonad

```

And here are the modifications you need to add to your `~/.xmonad/xmonad.hs`:

 `~/.xmonad/xmonad.hs` 
```
import XMonad
--You need to add this import
import XMonad.Util.Replace

main do
    -- And this "replace"
    replace
    xmonad $ defaultConfig
    {
    --Add the usual here
    }

```

You also need to add the following key binding:

 `~/xmonad/xmonad.hs` 
```
--Add a keybinding as follows:
((modm .|. shiftMask, xK_o     ), restart "/home/abijr/bin/obtoxmd" True)

```

Just remember to add a comma before or after and change the path to your actual script path. Now just `Mod+q` (restart xmonad to refresh the configuration), and then hit `Mod+Shift+o` and you should have Openbox running with the same windows open as in xmonad. To return to xmonad you should just exit Openbox. Here is a link to adamvo's `~/.xmonad/xmonad.hs` which uses this setup [Adamvo's xmonad.hs](http://wiki.haskell.org/Xmonad/Config_archive/adamvo%27s_xmonad.hs)

### KDE and xmonad

The xmonad wiki has instructions on how to [run xmonad inside KDE](https://wiki.haskell.org/Xmonad/Using_xmonad_in_KDE)

It also might be a good idea to set a global keyboard shortcut in KDE to start xmonad in case it is accidentally killed or closed.

### IM Layout for Skype

In orded to create an IM layout for the newer versions of skype, the following code can be used:

 `xmonad.hs` 
```
myIMLayout = withIM (1%7) skype Grid
    where
      skype = And (ClassName "Skype") (Role "")

```

### Example configurations

Below are some example configurations from fellow xmonad users. Feel free to add links to your own.

*   brisbin33 :: simple, useful, readable :: [config](https://github.com/pbrisbin/xmonad-config) [screenshot](http://files.pbrisbin.com/screenshots/current_desktop.png)
*   jelly :: Configuration with prompt, different layouts, twinview with xmobar :: [xmonad.hs](http://github.com/jelly/dotfiles/tree/master/.xmonad/xmonad.hs)
*   MrElendig :: Simple configuration, with xmobar :: [xmonad.hs](http://github.com/MrElendig/dotfiles-alice/blob/master/.xmonad/xmonad.hs), [.xmobarrc](http://github.com/MrElendig/dotfiles-alice/blob/master/.xmobarrc), [screenshot](http://arch.har-ikkje.net/gfx/ss/2010-09-05-163305_2960x1050_scrot.png).
*   thayer :: A minimal mouse-friendly config ideal for netbooks :: [configs](http://wiki.haskell.org/Xmonad/Config_archive/Thayer_Williams%27_xmonad.hs) [screenshot](http://wiki.haskell.org/Image:Thayer-xmonad-20110511.png)
*   vicfryzel :: Beautiful and usable xmonad configuration, along with xmobar configuration, xinitrc, dmenu, and other scripts that make xmonad more usable. :: [git repository](https://github.com/vicfryzel/xmonad-config), [screenshot](https://github.com/vicfryzel/xmonad-config/raw/master/screenshot.png).
*   vogt :: Check out adamvo's config and many others in the official [Xmonad/Config archive](http://wiki.haskell.org/Xmonad/Config_archive)
*   wulax :: Example of using xmonad inside Xfce. Contains two layouts for GIMP. :: [xmonad.hs](https://gist.github.com/jsjolund/94f6821b248ff79586ba), [screenshot](https://i.imgur.com/at9AbOl.png).

## Troubleshooting

### GNOME 3 and xmonad

With the release of GNOME 3 [custom GNOME sessions](/index.php/GNOME#Custom_GNOME_sessions "GNOME") require additional steps to make GNOME play nicely with xmonad.

Either install [xmonad-gnome3](https://aur.archlinux.org/packages/xmonad-gnome3/) from the AUR, or, manually:

Add an xmonad session file for use by gnome-session (`/usr/share/gnome-session/sessions/xmonad.session`):

```
[GNOME Session]
Name=Xmonad session
RequiredComponents=gnome-panel;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=xmonad
DefaultProvider-notifications=notification-daemon
```

Create a desktop file for GDM (`/usr/share/xsessions/xmonad-gnome-session.desktop`):

```
[Desktop Entry]
Name=Xmonad GNOME
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=gnome-session --session=xmonad
Type=XSession
```

Create or edit this file (`/usr/share/applications/xmonad.desktop`):

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=Xmonad
Exec=xmonad
NoDisplay=true
X-GNOME-WMName=Xmonad
X-GNOME-Autostart-Phase=WindowManager
X-GNOME-Provides=windowmanager
X-GNOME-Autostart-Notify=false
```

Finally, install [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) and create or edit `~/.xmonad/xmonad.hs` to have the following

```
import XMonad
import XMonad.Config.Gnome

main = xmonad gnomeConfig
```

Xmonad should now appear in the list of GDM sessions and also play nicely with gnome-session itself.

#### Compositing in GNOME and Xmonad

Some applications look better (e.g. GNOME Do) when composition is enabled. This, however, is not the case in the default Xmonad window manager. To enable it add an additional .desktop file `/usr/share/xsessions/xmonad-gnome-session-composite.desktop`:

```
[Desktop Entry]
Name=Xmonad GNOME (Composite)
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=/usr/sbin/gnome-xmonad-composite
Type=XSession
```

And create `/usr/sbin/gnome-xmonad-composite` and `chmod +x /usr/sbin/gnome-xmonad-composite`:

```
xcompmgr &
gnome-session --session=xmonad
```

Now choose "Xmonad GNOME (Composite)" in the list of sessions during login. Reference `man xcompmgr` for additional "eye candy".

### Xfce 4 and xmonad

Use `xfceConfig` instead of `defaultConfig` after importing `XMonad.Config.Xfce` in `~/.xmonad/xmonad.hs`, e.g. adapting the minimal configuration above:

```
import XMonad
import XMonad.Config.Xfce

main = xmonad xfceConfig
    { terminal    = "urxvt"
    , modMask     = mod4Mask
    }

```

Also add an entry to *Settings > Session and Startup > Application Autostart* that runs `xmonad --replace`.

### Missing xmonad-i386-linux or xmonad-x86_64-linux

Xmonad should automatically create the `xmonad-i386-linux` file (in `~/.xmonad/`). If this it not the case, grab a configuration file from the [xmonad wiki](http://wiki.haskell.org/Xmonad/Config_archive) or create your [own](http://wiki.haskell.org/Xmonad/Config_archive/John_Goerzen's_Configuration). Put the `.hs` and all others files in `~/.xmonad/` and run this command from the folder:

```
xmonad --recompile

```

Now you should see the file.

**Note:** A reason you may get an error message saying that xmonad-x86_64-linux is missing is that [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) is not installed.

### Problems with Java applications

If you have problems, like Java application Windows not resizing, or menus immediately closing after you click, see [Java#Applications not resizing with WM, menus immediately closing](/index.php/Java#Applications_not_resizing_with_WM.2C_menus_immediately_closing "Java").

### Empty space at the bottom of gvim or terminals

See [Vim#Empty space at the bottom of gVim windows](/index.php/Vim#Empty_space_at_the_bottom_of_gVim_windows "Vim") for a solution which makes the area match the background color.

For [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode"), you can use [rxvt-unicode-patched](https://aur.archlinux.org/packages/rxvt-unicode-patched/).

You can also configure xmonad to respect size hints, but this will leave a gap instead. See [the documentation on Xmonad.Layout.LayoutHints](http://www.eng.uwaterloo.ca/~aavogt/xmonad/docs/xmonad-contrib/XMonad-Layout-LayoutHints.html).

### Chromium/Chrome will not go fullscreen

If Chrome fails to go fullscreen when `F11` is pressed, you can use the [XMonad.Hooks.EwmhDesktops](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-EwmhDesktops.html) extension found in the [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) package. Simply add the `import` statement to your `~/.xmonad/xmonad.hs`:

```
import XMonad.Hooks.EwmhDesktops

```

and then add `handleEventHook = fullscreenEventHook` to the appropriate place; for example:

```
...
        xmonad $ defaultConfig
            { modMask            = mod4Mask
            , handleEventHook    = fullscreenEventHook
            }
...

```

After a recompile/restart of xmonad, Chromium should now respond to `F11` (fullscreen) as expected.

### Multitouch / touchegg

Touchégg polls the window manager for the `_NET_CLIENT_LIST` (in order to fetch a list of windows it should listen for mouse events on.) By default, xmonad does not supply this property. To enable this, use the [XMonad.Hooks.EwmhDesktops](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-EwmhDesktops.html) extension found in the [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) package.

### Keybinding issues with an azerty keyboard layout

Users with a keyboard with azerty layout can run into issues with certain keybindings. Using the [XMonad.Config.Azerty](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Config-Azerty.html) module will solve this.

### GNOME 3 mod4+p changes display configuration instead of launching dmenu

If you do not need the capability to switch the display-setup in the gnome-control-center, just execute

 `dconf write /org/gnome/settings-daemon/plugins/xrandr/active false` 

as your user, to disable the xrandr plugin which grabs Super+p.

### Problems with focused border in VirtualBox

A known issue with Virtualbox ([Ticket #6479](https://www.virtualbox.org/ticket/6479)) can cause problems with the focused window border. A solution can be found by installing a compositing manager like [xcompmgr](/index.php/Xcompmgr "Xcompmgr") which overrides the incorrect behavior of vboxvideo.

### Steam games (Half-Life, Left 4 Dead, …) and xmonad

There seems to be some trouble with xmonad and Source engine based games like Half-Life. If they do not start or get stuck with a black screen, a workaround is to start them in windowed mode. To do so, right click on the game in your Steam library and choose properties, click on launch options and enter [[1]](http://steamcommunity.com/app/221410/discussions/0/864960353968561426/):

```
-windowed

```

Another solution is to float the window of the game using the manage hook. For example, the following line can be used for Half-Life:

```
 className =? "hl_linux" --> doFloat

```

This can also be worked around by making XMonad pay attention to EWMH hints and including its fullscreen hook [[2]](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-EwmhDesktops.html):

```
  main = xmonad $ ewmh defaultConfig{ handleEventHook =
           handleEventHook defaultConfig <+> fullscreenEventHook }

```

This has a few other effects and makes it behave more akin to fullscreen apps in other WMs.

### LibreOffice - focus flicking between main window and dialog

The LibreOffice UI defaults to the gtk engine outside a desktop environment. This may cause problems with some xmonad configurations resulting in focus rapidly flicking between the LibreOffice main window and any open LibreOffice dialog window. Effectively locking the application. In this case the environment variable SAL_USE_VCLPLUGIN can be set to explicitly force LibreOffice to use another UI theme as outlined in [LibreOffice#Theme](/index.php/LibreOffice#Theme "LibreOffice") For instance

```
  export SAL_USE_VCLPLUGIN=gen lowriter

```

to use the general (QT) UI.

## See also

*   [xmonad](http://xmonad.org/) - The official xmonad website
*   [xmonad.hs](https://wiki.haskell.org/Xmonad/Config_archive/Template_xmonad.hs) - Template xmonad.hs
*   [xmonad: a guided tour](http://xmonad.org/tour.html)
*   [dzen](/index.php/Dzen "Dzen") - General purpose messaging and notification program
*   [dmenu](/index.php/Dmenu "Dmenu") - Dynamic X menu for the quick launching of programs
*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers") - Arch wiki article providing an overview of mainstream tiling window managers
*   [Share your xmonad desktop!](https://bbs.archlinux.org/viewtopic.php?id=94969)
*   [xmonad hacking thread](https://bbs.archlinux.org/viewtopic.php?id=40636)
*   [xmonad-log-applet](https://github.com/alexkay/xmonad-log-applet) - An applet for the GNOME, MATE or xfce panel.