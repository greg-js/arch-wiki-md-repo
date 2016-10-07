Window Maker is a [window manager](/index.php/Window_manager "Window manager") (WM) for the X Window System. It is designed to emulate the NeXT user interface as an OpenStep-compatible environment, and is characterized by low memory demands and high flexibility. As one of the lighter WMs, it is well suited for machines with modest performance specifications.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting Window Maker](#Starting_Window_Maker)
    *   [2.1 Graphically](#Graphically)
    *   [2.2 Manually](#Manually)
*   [3 Configuration](#Configuration)
    *   [3.1 Files](#Files)
    *   [3.2 Styles](#Styles)
    *   [3.3 Keyboard shortcuts](#Keyboard_shortcuts)
    *   [3.4 Background](#Background)
*   [4 Dock](#Dock)
*   [5 Clip](#Clip)
*   [6 Dockapps](#Dockapps)
*   [7 System tray](#System_tray)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Removing unwanted application icons](#Removing_unwanted_application_icons)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Can't disable smooth fonts](#Can.27t_disable_smooth_fonts)
    *   [9.2 The dock is not covered by fullscreen windows](#The_dock_is_not_covered_by_fullscreen_windows)
    *   [9.3 No application icons for some applications](#No_application_icons_for_some_applications)
*   [10 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") the [windowmaker](https://www.archlinux.org/packages/?name=windowmaker) package. You may also wish to install the [windowmaker-extra](https://www.archlinux.org/packages/?name=windowmaker-extra) package which contains a number of extra icons and themes.

## Starting Window Maker

### Graphically

Select the *windowmaker* session from the display manager's session menu.

### Manually

Once installed create or edit the file [~/.xinitrc](/index.php/~/.xinitrc "~/.xinitrc") as follows:

```
exec wmaker

```

To start Window Maker:

 `$ startx` 

## Configuration

### Files

All of the settings for Window Maker can be found in the `GNUSTEP_USER_ROOT` directory, under `Default` and `Library`. They are saved as simple text files. You can use the `Preferences Utility` (`WPrefs`) GUI application to change the settings, or edit them by hand.

*   `Defaults/WindowMaker` - The current Window Maker settings.
*   `Defaults/WMGLOBAL`
*   `Defaults/WMRootMenu` - The desktop main menu. It uses a simple text format that can be edited by hand. For more details, see the menu editing section in the Preferences Utility application.
*   `Defaults/WMState` - Used to restore a Window Maker session.
*   `Defaults/WMWindowAttributes` - Individual application and window settings, such as application icon settings and title bar settings. You can also edit this by right clicking on any application or window icon and selecting "Attributes".
*   `Defaults/WPrefs` - Settings for the Preferences Utility.
*   `Library/Colors/`
*   `Library/Icons/` - One of the default locations Window Maker looks for application icons. You can personally save your favorite icons here and use them by changing application or window attributes.
*   `Library/WindowMaker/autostart` - Add applications that you want to automatically start when Window Maker starts. Be sure to run them in the background by using "&".
*   `Library/exitscript` - Same as autostart, but used when exiting.
*   `Library/Backgrounds` - One of the default locations where Window Maker looks for desktop wallpapers.
*   `Library/Styles` - One of the default locations where Window Maker looks for styles.

### Styles

Styles are simple text files that change the appearance of Window Maker. They are very similar in appearance to the `Defaults/WindowMaker` file. Whatever settings are in the style file will be applied to the `Defaults/WindowMaker` file. Here is an example style that gives Window Maker a blue and gray Arch Linux like look:

`Arch.style`

```
{
  FTitleBack = (solid, "#0088CC");
  FTitleColor = white;
  UTitleBack = (solid, "#333333");
  UTitleColor = "#999999";
  PTitleBack = (solid, "#333333");
  PTitleColor = "#999999";
  MenuTextBack = (solid, "#ECF2F5");
  MenuTextColor = black;
  IconTitleBack = "#333333";
  IconTitleColor = white;
  MenuTitleBack = (solid, "#0088CC");
  MenuTitleColor = white;
  HighlightTextColor = white;
  HighlightColor = "#333333";
  MenuDisabledColor = "#999999";
  ClipTitleColor = black;
  IconBack = (solid, "#ECF2F5");
  ResizebarBack = (solid, "#333333");
  MenuStyle = flat;
  WorkspaceBack = (solid, black);
  ClipTitleFont = "Arial:slant=0:weight=200:width=100:pixelsize=10";
  IconTitleFont = "Arial:slant=0:weight=80:width=100:pixelsize=9";
  LargeDisplayFont = "Arial:slant=0:weight=80:width=100:pixelsize=24";
  MenuTextFont = "Arial:slant=0:weight=80:width=100:pixelsize=12";
  MenuTitleFont = "Arial:slant=0:weight=200:width=100:pixelsize=12";
  WindowTitleFont = "Arial:slant=0:weight=200:width=100:pixelsize=12";
}
```

Styles can also be edited by using the Preferences Utility application.

### Keyboard shortcuts

Window maker allows keyboard shortcuts to be assigned both to window manager actions and to menu entries.

To assign a keyboard shortcut to a window manager action, start the WPrefs application and navigate to the *Keyboard Shortcut Preferences* tab. Choose an action, click the *Capture* button and hit the desired keyboard combination. Then hit *Save*.

You can also assign keyboard shortcuts to menu entries. For instance, if one were using GNOME Screensaver to lock the screen, one could create a Lock Screen menu entry with the command `gnome-screensaver-command --lock`. To then assign a keyboard shortcut to this menu entry, start the WPrefs application and navigate to the *Application Menu Definition* tab. In the root menu that appears on screen, click on the Lock Screen entry. In the Wprefs window, click the *Capture* button, hit the desired keyboard combination and then click *Save*.

### Background

To use an image as a background in Window Maker, copy the image to the `~/GNUstep/Library/WindowMaker/Backgrounds` directory. Then, from the root menu, select *Appearance* -> *Background* -> *Images* -> *image-name*.

Alternatively, you could use a standalone background setter such as [Nitrogen](/index.php/Nitrogen "Nitrogen").

## Dock

The user interface of macOS evolved from the style of user interface that Window Maker uses. There is a "dock" that contains applications icons that are "pinned" to the dock by the user. Also, the dock can hold special small applications called "dockapps", which run only inside the dock. By default, all applications run in Window Maker will have an application icon, which you can use to run a new instance of the application, hide and unhide all windows of the application, or kill the application. The application icon does not represent a window. Instead, if you minimize a window, a small icon representing the window will appear on the desktop.

After starting any application, (for example, from the command line) the application icon will appear on the desktop. You can pin it to the dock by clicking and dragging the icon into the dock area. To remove the application icon from the dock, click and drag the icon away from the dock area. You change settings, such as making an application automatically start when Window Maker starts, by right clicking on the application icon in the dock.

The default action to activate application icons and window icons is to double click them. You can change a setting to allow you to activate them with a single click.

## Clip

The "clip" is a button that has the image of a paperclip on it. You can change the name of the current workspace by right clicking on the clip. You can change workspaces by clicking the arrows that are on the clip.

The clip also has similar functionality to the dock. Application icons that are added to the dock are visible on all workspaces, while application icons that are attached to the clip are only seen on the workspace where they are attached. This allows you to conveniently associate specific application icons with specific workspaces.

Double click the clip to hide and unhide the application icons that are attached to it.

## Dockapps

Dockapps are small applications that run in the dock. They can be useful for showing system information. Some useful dockapps that are in the [AUR](/index.php/AUR "AUR") include:

*   [wmclockmon](https://aur.archlinux.org/packages/wmclockmon/) - Show time and date.
*   [wmcpuload](https://aur.archlinux.org/packages/wmcpuload/) - Show CPU status and usage.
*   [wmnetload](https://aur.archlinux.org/packages/wmnetload/) - Show network status. Usage: `wmnetload -i eth0`
*   [wmdiskmon](https://aur.archlinux.org/packages/wmdiskmon/) - Show disk usage. Usage: `wmdiskmon -p /dev/sda1 -p /dev/sda2`

See the Window Maker website for more information about dockapps.

## System tray

Window Maker does not ship with a system tray however there are a number of standalone trays that can be used with Window Maker.

	stalonetray

Prior to version 0.8, [stalonetray](https://www.archlinux.org/packages/?name=stalonetray) did not work as a dockapp in Window Maker, use Docker instead. However, starting from version 0.8, there is very basic dockapp support for Window Maker which can be enabled using the `--dockapp-mode wmaker` command line option. The following options should also be used: `--slot-size 32 --geometry 2x2 --parent-bg --scrollbars none`.

	System tray dockapps for Window Maker

[wmsystray](https://aur.archlinux.org/packages/wmsystray/) and [wmsystemtray](https://aur.archlinux.org/packages/wmsystemtray/) are both system tray dockapps designed for Window Maker; the latter is also reported to work well in other desktops.

	Peksystray

[Peksystray](https://aur.archlinux.org/packages/Peksystray/) is a system tray designed for all the light window managers that support docking. Peksystray provides a window where icons will automatically add up depending on the requests from the applications. Both the size of the window and the size of the icons can be selected by the user. If the window is full, it can automatically display another window in order to display more icons.

## Tips and tricks

### Removing unwanted application icons

For some applications, you may not want Window Maker to display an application icon or appicon. To disable the appicon for an application, right click on the application's titlebar and choose *Attributes...* and from the drop down menu choose *Application Specific*. Tick the *No application icon* option and then hit *Apply* and *Save*.

## Troubleshooting

### Can't disable smooth fonts

Delete (but keep a backup) the `~/.fontconfig/` directory and `~/.fonts.conf` file, then restart Window Maker.

### The dock is not covered by fullscreen windows

To correct this issue, right click on any pinned application and, from the *Dock position* submenu, choose *Normal*. Then start the WPrefs tool. Under the *Window Handling Preferences* tab, tick the *...do not cover dock* option. This will ensure that maximised applications do not cover the dock but that fullscreen applications do.

### No application icons for some applications

Some applications such as [Chromium](/index.php/Chromium "Chromium") will not display an application icon. For a workaround involving Chromium, see the following [bug report](https://code.google.com/p/chromium/issues/detail?id=375758#c3).

## See Also

*   [Official website](http://www.windowmaker.org/)
*   [Window Maker (Wikipedia)](https://en.wikipedia.org/wiki/Window_Maker "wikipedia:Window Maker")