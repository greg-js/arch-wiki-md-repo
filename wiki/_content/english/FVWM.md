Related articles

*   [Window manager](/index.php/Window_manager "Window manager")

[FVWM](http://fvwm.org/) is an ICCCM-compliant multiple virtual desktop window manager for the X Window system. It is configured by editing text-based configuration files. Although using FVWM does not require any knowledge of programming languages, it is possible to extend FVWM with [M4](http://www.fvwm.org/documentation/manpages/stable/FvwmM4.php), [C](http://www.fvwm.org/documentation/manpages/stable/FvwmCpp.php), and [Perl](http://www.fvwm.org/documentation/manpages/stable/FvwmPerl.php) preprocessing. FVWM also has a [Perl library](http://www.fvwm.org/documentation/perllib/) which allows one to create [modules](#Modules). FVWM stands for F Virtual Window Manager. The official stance is that the F does not stand for anything in particular [[1]](http://fvwm.org/documentation/faq/#what-does-fvwm-stand-for).

## Contents

*   [1 Installing](#Installing)
*   [2 Starting](#Starting)
    *   [2.1 Startup functions](#Startup_functions)
*   [3 Configuration](#Configuration)
    *   [3.1 The virtual desktop](#The_virtual_desktop)
    *   [3.2 Keyboard and mouse bindings](#Keyboard_and_mouse_bindings)
    *   [3.3 Window decoration](#Window_decoration)
        *   [3.3.1 Titlebar buttons](#Titlebar_buttons)
        *   [3.3.2 Button styles](#Button_styles)
        *   [3.3.3 Title and border styles](#Title_and_border_styles)
    *   [3.4 Menus](#Menus)
    *   [3.5 Style command](#Style_command)
    *   [3.6 Functions](#Functions)
    *   [3.7 Modules](#Modules)
        *   [3.7.1 FvwmPager](#FvwmPager)
        *   [3.7.2 FvwmButtons](#FvwmButtons)
        *   [3.7.3 FvwmEvent](#FvwmEvent)
    *   [3.8 Colors](#Colors)
        *   [3.8.1 Colorsets](#Colorsets)
    *   [3.9 Fonts](#Fonts)
    *   [3.10 Icons](#Icons)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 MWM compatibility options](#MWM_compatibility_options)
    *   [4.2 Force icon size and background](#Force_icon_size_and_background)
    *   [4.3 Ignore resize hints](#Ignore_resize_hints)
    *   [4.4 Do not use a wireframe when moving or resizing windows](#Do_not_use_a_wireframe_when_moving_or_resizing_windows)
    *   [4.5 Disable edge scrolling](#Disable_edge_scrolling)
    *   [4.6 Stop modifiers from interfering with mouse and key bindings](#Stop_modifiers_from_interfering_with_mouse_and_key_bindings)
    *   [4.7 Use ClickToFocus](#Use_ClickToFocus)
    *   [4.8 Window tiling](#Window_tiling)
    *   [4.9 Transfer focus on page or desk switch](#Transfer_focus_on_page_or_desk_switch)
*   [5 See also](#See_also)

## Installing

[Install](/index.php/Install "Install") [fvwm](https://www.archlinux.org/packages/?name=fvwm) or [fvwm-cvs](https://aur.archlinux.org/packages/fvwm-cvs/) (for the development version). Alternatively, you can install [fvwm+](https://aur.archlinux.org/packages/fvwm%2B/) which provides a patched version of FVWM.

The following packages provide themes and icons for FVWM: [fvwm-crystal](https://www.archlinux.org/packages/?name=fvwm-crystal), [fvwm-icons](https://aur.archlinux.org/packages/fvwm-icons/), [fvwm-themes](https://aur.archlinux.org/packages/fvwm-themes/), [fvwm-themes-extra](https://aur.archlinux.org/packages/fvwm-themes-extra/). FVWM Crystal provides a separate session for a desktop environment like experience.

## Starting

Select *FVWM* from the session menu in a [display manager](/index.php/Display_manager "Display manager") of choice. Otherwise, add `exec fvwm` to your user's `.xinitrc`.

For FVWM Crystal, select *FVWM-Crystal* from the session menu or add `exec fvwm-crystal` to your user's `.xinitrc`.

See [xinitrc](/index.php/Xinitrc "Xinitrc") for details, such as preserving the logind session.

### Startup functions

**Note:** It is [recommended](http://www.fvwmforums.org/phpBB3/viewtopic.php?f=40&t=1505) that you only use the StartFunction and make use of the `Test` command - explained below.

FVWM provides a number of functions to start modules or applications when initialising, restarting or exiting the window manager.

*   StartFunction - executed when FVWM is first initialised and on restarts.
*   InitFunction - executed only when FVWM is first initialised.
*   RestartFunction - executed only when FVWM is restarted.
*   ExitFunction - executed when exiting FVWM.

You can add your own actions to any of these functions using the `AddToFunc` command. For example, if one wanted to start *network-manager-applet* on startup (but not for any subsequent restarts of the window manager) one could add the *nm-applet* command to the InitFunction:

```
AddToFunc InitFunction
+ I Exec nm-applet &

```

You can also use just StartFunction and prepend your commands with Test commands which check whether the window manager has started or restarted and run the action only if the test is true. Using this method, *nm-applet* could be started in the following manner:

```
AddToFunc StartFunction
+ I Test (Init) Exec nm-applet &

```

## Configuration

The following configuration file locations are supported:

*   `$HOME/.fvwm/config`
*   `/usr/local/share/fvwm/config`

The following configuration locations are supported as of version 2.6.7, but may not be supported in the future:

*   `$HOME/.fvwm/.fvwm2rc`
*   `$HOME/.fvwm2rc`
*   `/usr/local/share/fvwm/.fvwm2rc`
*   `/usr/local/share/fvwm/system.fvwm2rc`
*   `/etc/system.fvwm2rc`

As of version 2.6.7, FVWM ships with a new default configuration, located in `/usr/share/fvwm/default-config`. As such, the older sample configuration files are no longer provided. However, they can still be viewed on [GitHub](https://github.com/fvwmorg/fvwm/tree/4fc2bf68493c098da54af63cff3ebf3c58882a8d/sample.fvwmrc). The [fvwm-themes](http://fvwm-themes.sourceforge.net/) project also provides ready-made configurations though it should be noted that these have not been updated since 2003 and may require modifications to work correctly with more recent FVWM versions.

**Tip:** You can split up your configuration into multiple files and then source those files from the main configuration file using the `read` command. The syntax is `read /path/to/file`.

### The virtual desktop

For its virtual desktop, FVWM implements both workspaces (used by window managers such as Metacity and [Openbox](/index.php/Openbox "Openbox")) and viewports (used by window managers such as Compiz). See [[2]](http://www.circuitousroot.com/artifice/programming/useful/fvwm/viewports/index.html) for a description of the differences between workspaces and viewports. FVWM refers to workspaces as desks and viewports as pages.

Pages in FVWM are arranged in a grid. The number of pages used can be defined with the `DesktopSize` command. For instance, adding `DesktopSize 3x3` to your configuration file will give you 9 pages, arranged in a 3x3 grid. Pages can be navigated using the [pager module](#FvwmPager) or with the `GoToPage` command which could be mapped to a keyboard shortcut or menu entry. For instance, the command `GoToPage -1p +0p` will move the viewport 1 page to the left of the current page.

The number of desks available in FVWM is very large, the minimum desk number is -2147483648 and the maximum is 2147483647\. By default, FVWM starts on desk 0\. Desks can be navigated using the pager module (if it is configured to show a number of desks) or with the `GoToDesk` command - `GoToDesk +1` will move to the next desk, relative to the currently used desk.

### Keyboard and mouse bindings

Keyboard or bindings can be defined in the configuration file with the `Key` or `Mouse` command. The syntax of the command takes the following form: `Key/Mouse *(window)* *button/key name* *context* *modifiers* *action*`. For instance, the following example will launch an XTerm on an `Alt+F2` keypress: `Key F2 A 1 Exec xterm`. Note that the `*(window)*` argument is optional.

The context value defines where the binding will be applied. The following contexts are valid: **R** (root window), **W** (application window), **D** (desktop manager window - PCManFM desktop manager for instance), **T** (title bar), **S** (window side, top, bottom), **[ ] - _** (left side, right side, top, bottom respectively), **F** (window frame corners), **< > ^ v** (left, right, top, bottom corners respectively), **I** (icon window), **0-9** (titlebar buttons) and **A** (all contexts). Any combination of these letters is also acceptable.

The modifier value can be one of the following: **A** (any), **C** (control), **S** (shift), **M** (meta), **N** (none), or **1-5**, representing the X Modifiers - run `xmodmap` to see which X modifier is which. Multiple modifiers should not be spaced. For instance, to use the modifier `Control+Alt`, you would supply as the modifier argument `C1`.

The action must be an FVWM [function](#Functions) to run, such as the *Quit* function or *Menu* function. Execution of external commands, such as *xterm*, can be achieved with the *Exec* function, as shown above.

### Window decoration

#### Titlebar buttons

FVWM can provide up to 10 window buttons. These are numbered 0-9\. Even numbers indicate buttons located on the right hand side of the titlebar whilst odd numbers indicate buttons located on the left. The layout is as follows:

```
1 3 5 7 9    0 8 6 4 2 

```

Window buttons will remain hidden unless a `Mouse` command is used which specifies one of the titlebar buttons as the context. For instance, to activate the rightmost titlebar button and make it close the window on a left click, one would use the following command:

```
Mouse 1 2 A Close

```

*Mouse* is the name of the command, *1* is the mouse button, *2* is the number of the rightmost titlebar button, *A* is the modifier (any) and *Close* is the action to be taken. See [#Keyboard and mouse bindings](#Keyboard_and_mouse_bindings) for more information.

#### Button styles

The style of your titlebar buttons can be configured with the `ButtonStyle` command. This takes the following syntax:

```
ButtonStyle *button-number* *state* *style* -- *flag*

```

The state can be one of *ActiveUp*, *ActiveDown*, *InactiveUp*, *InactiveDown*. *ActiveUp* and *ActiveDown* refer to the un-pressed and pressed button states of the active window. Likewise for the Inactive states. One can also use just *Active* or *Inactive* which are shortcuts for both the pressed and un-pressed button states.

The style argument can be one of the following:

*   Simple - does nothing.
*   Default - takes argument of button number for default style to load.
*   Solid - fill button a solid color.
*   ColorSet - fill button with the ColorSet specified - takes an alpha argument between 0 and 100.
*   Vector - draws a line pattern - using the keyword Vector is optional as this is a standard style.
*   ?Gradient - fills the button with a gradient - see the FVWM man page Color Gradients section for the syntax.
*   Pixmap - fills the button with a given pixmap - see also the following variants: AdjustedPixmap, ShrunkPixmap, StretchedPixmap, TiledPixmap.
*   MiniIcon - fills the button with the window's mini icon.

A number of vector styles are documented [here](http://fvwmforums.org/wiki/Config/VectorButtons/). You can also create your own vector buttons using this [vector buttons viewer](http://gromnitsky.users.sourceforge.net/js/fvwm-vector/). Finally, see [this page](http://fvwmforums.org/wiki/Decor/) for some example decoration configurations that use pixmaps, including imitations of Crux (a Sawfish theme), Mac OS and Windows 98.

The flag affects the state for a button. Some examples of flags include *Raised*, *Sunk* and *Flat*. For more information, see [fvwm(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fvwm.1) and look for the ButtonStyle section.

**Note:** To give the buttons the same background as the title, use the `UseTitleStyle` flag. Alternatively, specify your button backgrounds using the `ButtonStyle` command and then follow this with an `AddButtonStyle` command to specify the vector or pixmap image. `AddButtonStyle` takes the same syntax as `ButtonStyle`.

#### Title and border styles

The window titles and borders can be configured with the `TitleStyle` and `BorderStyle` commands respectively.

TitleStyle can take the following arguments:

```
TitleStyle *justify* Height *height-in-pixels*

```

The justify argument can be *LeftJustified*, *RightJustified* or *Centered*. TitleStyle and BorderStyle can take the following arguments:

```
TitleStyle/BorderStyle *state* *style* -- *flag*

```

See [#Button styles](#Button_styles) for the *state*, *style* and *flag* arguments.

### Menus

**Note:** The `AddToMenu` command is cumulative, meaning that if it is used twice on the same menu, the items specified in the second command will be appended to the menu in its current state instead of overwriting the previous menu configuration. For this reason, it is good practice to call `DestroyMenu *menu-name*` before calling `AddToMenu` unless the cumulative behavior is desired.

Menus can be created with the `AddToMenu` command. This takes the following syntax:

```
AddToMenu *menu-name* *menu-title* Title

```

Remove the *menu-title* and Title arguments to create a menu with no title. Subsequent entries in the menu take the following syntax:

```
+ *entry-name* *action*

```

See the following example:

```
AddToMenu "Web" "Web Browsers" Title
+ "Firefox" Exec firefox
+ "Chromium Exec chromium
+ "Opera"   Exec opera

```

Use the `Popup` command to show other menus. For instance, to include the menu defined above in another menu one could use the following syntax:

```
+ "Web Browsers" Popup "Web"

```

FVWM menus also support icons. To give a menu entry an icon, provide the path to the icon enclosed in `%` signs after the entry name - see below:

```
+ "Chromium %/usr/share/icons/hicolor/16x16/apps/chromium.png%" Exec chromium

```

Use the *xdg_menu* tool, provided by [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu), to automatically generate menus - see [Xdg-menu#Fvwm2](/index.php/Xdg-menu#Fvwm2 "Xdg-menu").

### Style command

**Note:** Most styles can be negated with a `!`. For instance the style `Title` forces the window manager to give the window a title whilst `!Title` has the opposite effect.

The `Style` command allows one to configure various aspects of the window manager itself and also to set behaviors for certain windows. The syntax is `Style *window-name* *stylename*`. The *window-name* argument can be a window name, class, title name or resource string. Use `*` to match all windows. See [fvwm(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fvwm.1) for all available styles - some examples are provided below:

*   `Style "*" CascadePlacement` - make the window manager use the cascade placement algorithm for all new windows.
*   `Style "Chromium" PositionPlacement center` - ensure that all new Chromium windows are placed in the center of the screen.
*   `Style "xterm" StartIconic` - ensure that all new XTerm windows start iconified.
*   `Style "*" HilightBack indianred` - set the frame background of any focused window to the color indianred.

### Functions

**Note:** The `AddToFunc` command is cumulative, meaning that if it is used twice on the same fuction, the items specified in the second command will be appended to the function in its current state instead of overwriting the previous function configuration. For this reason, it is good practice to call `DestroyFunc *func-name*` before calling `AddToFunc` unless the cumulative behavior is desired.

FVWM provides many built in functions, examples being `Close` to close a window or `Exec` which allows the execution of an external command. Users can also define their own functions or add to existing functions using the `AddToFunc` command. This uses the following syntax: `AddToFunc *func-name* I|M|C|H|D *action*`. The letter codes stand for the following: **I** - execute immediately, **M** - execute when the user moves the mouse, **C** - execute on mouse click, **H** - execute when the user holds the mouse button, **D** - execute when the user double clicks the mouse button. Below is a trivial example of a function:

```
AddToFunc VolumeFunc
+ I Exec xterm -e alsamixer

```

One can also use conditional commands (see [fvwm(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fvwm.1) and look for the Conditional Commands section). For instance, suppose one wanted a function that would close all windows in the current page other than the one which has focus. That function can be defined as below:

```
AddToFunc CloseAllButThis
+ I All (CurrentPage, !Focused) Close

```

The `All` conditional matches all windows that meet the conditions defined in parenthesis. Functions can execute more than one action, just add one line for each action beginning with a plus sign:

```
AddToFunc MyFunc
+ I *action1*
+ D *action2*
+ I *action3*

```

### Modules

**Note:** A number of older FVWM modules have been removed as of version 2.6.7\. [[3]](https://github.com/fvwmorg/fvwm/releases/tag/2.6.7)

Modules are separate programs, spawned by FVWM that can add extra functionality. Modules can be spawned using the following syntax: `Module *ModuleName* (*identifier*) *ModuleArgs*`.

Sometimes, one might want to spawn multiple instances of the same type of module, each with their own separate configuration. In this case, one should spawn the module with an identifier, for instance:

```
AddToFunc StartFunction
+ I Module FvwmButtons Panel1
+ I Module FvwmButtons Panel2

```

where *Panel1* and *Panel2* are the identifiers.

Most modules will have a number of module commands which can be used to configure the module's appearance or behavior. Use the following syntax:

```
*ModuleName/Identifier: *module-command* *command-args*

```

For instance, if one spawned an FvwmPager with the identifier MyPager then one could configure it in the following fashion:

```
*MyPager: Geometry 135x90+0+0
*MyPager: Back midnightblue

```

#### FvwmPager

The FvwmPager is a module which provides a visual representation of the desks and pages provided by the window manager. Like all modules, it must be spawned by FVWM. To start an FvwmPager, add something similar to the following to your StartFunction:

```
+ I Module FvwmPager

```

With no arguments, the FvwmPager will only display the viewports for desk 0\. With the arguments 0 9, FvwmPager will show the 10 desks from 0-9.

```
+ I Module FvwmPager 0 9

```

With the argument * the FvwmPager will show only one desk but it will always be the desk that is currently being used.

```
+ I Module FvwmPager *

```

See [FvwmPager(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/FvwmPager.1) for a list of module commands.

#### FvwmButtons

FvwmButtons is a module which can create a box of buttons which can perform actions when pressed. FvwmButtons can also "swallow" application windows. This might be useful for swallowing a system tray window or a clock window. The size of the panel is automatically determined (the panel will resize to accommodate all elements) however it is also possible to manually set a size using the `Geometry` command. This takes a standard X geometry. The basic commands needed to create an FvwmButtons panel are outlined below.

Set the number of rows and columns:

```
*FvwmButtons: Rows *x*
*FvwmButtons: Columns *x*

```

Create a button (this example creates a button with a title and an icon which launches an XTerm when left clicked):

```
*FvwmButtons: (Title "Xterm", Icon /usr/share/pixmaps/mini.xterm_48x48.xpm, Action (Mouse1) Exec xterm)

```

You can omit any of these arguments if you so choose.

Swallow a window (this example swallows a stalonetray):

```
*FvwmButtons: (Swallow(UseOld, NoClose) "stalonetray" "Nop")

```

The Swallow command takes a number of "hangon" arguments. Here, the *UseOld* and *NoClose* arguments have been used. UseOld means that an existing window will be swallowed if it exists. NoClose means that the window will not be closed if the FvwmButtons process is terminated. The *stalonetray* argument is the class of the window that we want to swallow. Replace as appropriate. The last argument is a command to start the application that is to be swallowed. In this example, it is assumed that the application has already been started so the argument provided is *Nop* which is a function that does nothing. One could replace this with `"Exec stalonetray"` to start the application from the FvwmButtons module instead of assuming that the application has been started elsewhere.

Containers are spaces defined which can span multiple rows and columns or subdivide a row or column into more rows or columns. This can be useful for instance if one wants to allocate a certain percentage of space to an element. Say one wants to swallow an XClock and allocate 100% of the width and 80% of the height to the XClock. This can be defined as such:

```
*FvwmButtons: Rows 5
*FvwmButtons: Columns 1
*FvwmButtons: (1x4, Container)
*FvwmButtons: (Swallow(UseOld, NoClose) "xclock" "Nop")
*FvwmButtons: (End)

```

Note that a container is created by defining a certain number of columns and rows and then using the keyword container. Elements inside the container are defined underneath this line and the container is then closed with the *End* command.

For a full list of options, see [FvwmButtons(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/FvwmButtons.1).

#### FvwmEvent

FvwmEvent is a module which can be used to bind a [function](#Functions) or an audio file to a window manager event (such as the closing of a window). In the case of an audio file, the audio will be played when the event that it is bound to occurs. FvwmEvent can be spawned from within Fvwm by adding the following to your `StartFunction`:

```
+ I Module FvwmEvent

```

FvwmEvent can also be spawned with an identifier - see [#Modules](#Modules). Once spawned, FvwmEvent will run in the background, waiting for events that it has been configured to recognize. Events can be configured in the following form:

```
* FvwmEvent: windowshade Lower

```

where `windowshade` is the event and `Lower` is the command to be executed when that event occurs. In the case where you wish to execute a function with arguments, that function and its arguments need to be quoted - see below:

```
* FvwmEvent: new_page "Exec xterm"

```

For a full list of events, see [FvwmEvent(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/FvwmEvent.1).

### Colors

FVWM color styles can take a number of color code types such as hexcolors (`#ffffff` for instance), rbg colors (`rgb:ff/ff/ff` for instance) as well as the pre-defined [X11 colors](https://en.wikipedia.org/wiki/X11_color_names "wikipedia:X11 color names").

The following [styles](#Style_command) might be useful:

*   `Color` - this takes two arguments, the color of the unfocused window title text and the color of the unfocused window frame separated by a forward slash, *black/lightgrey* for example.
*   `HilightBack` - takes a single argument, the color of the focused window frame.
*   `HilightFore` - takes a single argument, the color of the focused window title text.

#### Colorsets

Colorsets in FVWM are a set of four colors (a foreground color, a background color, a shadow color and a highlight color) as well as an optional background pixmap. Any part of FVWM that uses a particular colorset will be affected if that colorset is changed.

All colorsets are identified by a number. Any numbering convention can be used; the fvwm-themes project documents one such convention that uses the first 40 colorsets (0-39). See [[4]](http://fvwm-themes.sourceforge.net/doc/colorsets).

Colorsets can be created with the `ColorSet` command - syntax: `ColorSet *number* *options*`. See [fvwm(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fvwm.1) - the Colorsets section - for more information.

**Tip:** Using `Style "*" Colorset *num*` overrides the `Color` style and using `Style "*" HilightColorset *num*` overrides the `HilightFore` and `HilightBack` styles.

### Fonts

For styles such as `Font`, use [xorg-xfontsel](https://www.archlinux.org/packages/?name=xorg-xfontsel) to determine the correct font names for X11 fonts - see [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description") and [Font configuration](/index.php/Font_configuration "Font configuration") for more information. You can also specify xft fonts, for example: `"xft:DejaVu Sans:size=10"`.

### Icons

Windows in FVWM can be iconified (minimized). This means that the window will disappear from view and be replaced by an icon on the desktop, similar to the behavior in Microsoft Windows 3.1\.

The program itself will supply the icon. One can also set a default icon to be used, in case a program does not have an icon to supply: `Style "*" Icon /path/to/default/icon.png`.

To disable icons altogether, use the following style: `Style "*" NoIcon`. This means that the window will simply disappear when iconified.

The positioning of icons can be controlled using the `IconBox` style - note that this is not the same thing as the FvwmIconBox module - along with the `IconFill` style. Use `Style "*" IconBox none` to disable the IconBox. This means that icons will be placed at the position of the top left corner of the window. Else, use `Style "*" IconBox l t r b` where *l t r b* stand for *left*, *top*, *right* and *bottom* respectively. These arguments should be the number of pixels away from the screen edge that the IconBox edge should be. Hence, arguments of `+0 +0 -0 -0` means that the IconBox will fill the entire screen.

Multiple IconBox styles can be defined but they must be defined on the same line, for instance:

```
Style "*" IconBox +0 +800 -100 -0, IconBox -200 +0 -0 -120

```

When the first IconBox overflows, icons will then be placed in the second IconBox. Note that if the last IconBox overflows then the default IconBox will be used which covers the entire screen and fills from top to bottom - left to right.

Use the `IconFill` style to control how icons will be filled. A style of `Style "*" IconFill left bottom` means that icons will be filled from left to right - bottom to top (Motif Window Manager behavior). A style of `Style "*" IconFill top left` means that icons will be filled from top to bottom - left to right. Note that the IconFill style should be defined on the same line as the IconBox style, for instance:

```
Style "*" IconBox +0 +0 -0 -0, IconFill left bottom

```

## Tips and tricks

### MWM compatibility options

FVWM provides a number of options that allow it to mimic the appearance and behaviour of MWM (Motif Window Manager).

*   `Emulate Mwm` - this commands places the geometry feedback window in the center of the screen.
*   `MenuStyle Mwm` - this command gives menus the appearance of Motif menus.
*   `MwmButtons` - this style makes the maximize button look pressed in when a window is maximized.
*   `MwmBorder` - this style makes the window border bevel more closely match the style of Mwm window borders
*   `MwmDecor` - this style makes FVWM attempt to honor MWM hints that some applications might set.
*   `MwmFunctions` - this style make FVWM attempt to recognize and respect functions that MWM would prohibit.
*   `HintOverride` - this style is similar to MwmFunctions but instead it shades out the prohibited functions but allows the user to perform them anyway.

### Force icon size and background

The sizing of icons is not regular as different programs provide icons of differing sizes. Use the `IconSize` style to force a regular size: `Style "*" IconSize 48 48` for instance. Note that icons larger than the given size will be clipped.

By default, icons also have no background. You can use the `IconBackgroundColorset` style to force icons to have a background. See [#Colorsets](#Colorsets).

### Ignore resize hints

Some applications, such as XTerm, supply a maximum size to the window manager that might be smaller than the screen size. This means that if such an application is maximized, it will not cover the whole screen. To force FVWM to ignore these hints, use the following: `Style "*" ResizeHintOverride`.

### Do not use a wireframe when moving or resizing windows

Use the `OpaqueMoveSize unlimited` command to view the window itself when moving.

Use `Style "*" ResizeOpaque` to view the window itself when resizing.

### Disable edge scrolling

To disable scrolling to the next viewport when moving the mouse pointer to the screen edge, use the following command: `EdgeScroll 0 0`.

### Stop modifiers from interfering with mouse and key bindings

NumLock, CapsLock and ScrollLock can intefere with ClickToFocus as well as mouse and key bindings. To disable this behavior, use the following command: `IgnoreModifiers L25`.

### Use ClickToFocus

Ensure that [perl-tk](https://www.archlinux.org/packages/?name=perl-tk) and [perl-x11-protocol](https://www.archlinux.org/packages/?name=perl-x11-protocol) are installed. The use the following style command: `Style "*" ClickToFocus`. See [fvwm(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fvwm.1) for other focus behaviors.

### Window tiling

The following functions can tile a window to the left half, right half, top half or bottom half of the screen, or to each corner of the screen, when called and return the window to its original position and size when called again.

```
DestroyFunc TileLeft
AddToFunc TileLeft
+ I ThisWindow (!Shaded, !Iconic) Maximize 50 100
+ I ThisWindow (Maximized, !Shaded, !Iconic) Move +0 +0

DestroyFunc TileRight
AddToFunc TileRight
+ I ThisWindow (!Shaded, !Iconic) Maximize 50 100
+ I ThisWindow (Maximized, !Shaded, !Iconic) Move -0 +0

DestroyFunc TileTop
AddToFunc TileTop
+ I ThisWindow (!Shaded, !Iconic) Maximize 100 50
+ I ThisWindow (Maximized, !Shaded, !Iconic) Move +0 +0

DestroyFunc TileBottom
AddToFunc TileBottom
+ I ThisWindow (!Shaded, !Iconic) Maximize 100 50
+ I ThisWindow (Maximized, !Shaded, !Iconic) Move +0 -0

DestroyFunc TileTopLeft
AddToFunc TileTopLeft
+ I ThisWindow (!Shaded, !Iconic) Maximize 50 50
+ I ThisWindow (Maximized, !Shaded, !Iconic) Move +0 +0

DestroyFunc TileTopRight
AddToFunc TileTopRight
+ I ThisWindow (!Shaded, !Iconic) Maximize 50 50
+ I ThisWindow (Maximized, !Shaded, !Iconic) Move -0 +0

DestroyFunc TileBottomLeft
AddToFunc TileBottomLeft
+ I ThisWindow (!Shaded, !Iconic) Maximize 50 50
+ I ThisWindow (Maximized, !Shaded, !Iconic) Move +0 -0

DestroyFunc TileBottomRight
AddToFunc TileBottomRight
+ I ThisWindow (!Shaded, !Iconic) Maximize 50 50
+ I ThisWindow (Maximized, !Shaded, !Iconic) Move -0 -0
```

### Transfer focus on page or desk switch

**Note:** The approach of using FvwmEvent allows for a window in a page to be automatically focused when clicking on that page in the FvwmPager. However, it breaks the right-click and drag panning functionality of the pager. For this reason, you might prefer to call `GoToPage` and `Focus-Previous` from within another function which can be bound to a hotkey instead of using the `new_page` event.

If you are using ClickToFocus, you might wish to automatically transfer keyboard focus when switching pages or desks to the previously focused window in that page or desk. Otherwise, you will have to click on the window you wish to interact with on every page or desk switch. This can be accomplished by using the [FvwmEvent](#FvwmEvent) module to bind a function which focuses the currently or previous focused window to the `new_page` and `new_desk` events.

Below is an example of such a function:

```
DestroyFunc Focus-Previous
AddToFunc Focus-Previous
+ I All ($0, Focused) FlipFocus $1
+ I TestRc (NoMatch) Prev ($0, AcceptsFocus) FlipFocus $1
```

The `$0` argument should be either `CurrentPage` or `CurrentDesk`. The `$1` argument is for supplying the `NoWarp` argument to `FlipFocus` - by default, FlipFocus will initiate a page switch to the page containing the focused window. This behaviour is useful when switching desks but must be disabled when switching pages because windows can span more than one page.

With the function appropriately configured, ensure that FvwmEvent is started and then bind it to the required events as show below:

```
* FvwmEvent: new_page "Focus-Previous CurrentPage NoWarp"
* FvwmEvent: new_desk "Focus-Previous CurrentDesk"

```

## See also

*   [FVWM beginners guide](http://zensites.net/fvwm/guide/) - Zensites.
*   [FVWM Homepage](http://fvwm.org/) - includes documentation and a FAQ.
*   [FVWM Wiki](http://fvwmforums.org/wiki/).
*   [FVWM Forums](http://www.fvwmforums.org).
*   [FVWM - Man Page](http://fvwm.org/documentation/manpages/fvwm.html).
*   [FVWM Themes](https://www.box-look.org/browse/cat/143/ord/latest/) - Box-Look.org.
*   [FVWM Configurations](http://www.fvwmforums.org/phpBB3/viewforum.php?f=39&sid=468469f95f9a2a90cd9d5a0819d26eec) - threads in the FVWM forums.
*   [FVWM Tips](http://www.fvwmforums.org/phpBB3/viewtopic.php?f=40&t=1505) - forum post by Thomas Adam - an FVWM developer.