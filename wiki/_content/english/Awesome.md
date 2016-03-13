From the [awesome website](https://awesome.naquadah.org/):

	*[awesome](https://en.wikipedia.org/wiki/awesome_(window_manager) is a highly configurable, next generation framework window manager for X. It is very fast, extensible and licensed under the GNU GPLv2 license. It is primarily targeted at power users, developers and any people dealing with every day computing tasks and who want to have fine-grained control on its graphical environment.*

## Contents

*   [1 Installation](#Installation)
    *   [1.1 KDM](#KDM)
    *   [1.2 With GNOME](#With_GNOME)
*   [2 Configuration](#Configuration)
    *   [2.1 Creating the configuration file](#Creating_the_configuration_file)
        *   [2.1.1 Examples](#Examples)
    *   [2.2 Extensions](#Extensions)
    *   [2.3 Autorun programs](#Autorun_programs)
    *   [2.4 Changing keyboard layout](#Changing_keyboard_layout)
    *   [2.5 Theming](#Theming)
        *   [2.5.1 Wallpaper](#Wallpaper)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Hide / show wibox](#Hide_.2F_show_wibox)
    *   [3.2 Screenshot](#Screenshot)
    *   [3.3 Removing window gaps](#Removing_window_gaps)
    *   [3.4 Transparency](#Transparency)
        *   [3.4.1 Conky](#Conky)
        *   [3.4.2 wiboxes](#wiboxes)
        *   [3.4.3 ImageMagick](#ImageMagick)
    *   [3.5 Passing content to widgets with awesome-client](#Passing_content_to_widgets_with_awesome-client)
    *   [3.6 Using a different panel with awesome](#Using_a_different_panel_with_awesome)
    *   [3.7 Application directories in menubar](#Application_directories_in_menubar)
    *   [3.8 Pop-up menus](#Pop-up_menus)
    *   [3.9 Applications menu](#Applications_menu)
    *   [3.10 Titlebars](#Titlebars)
    *   [3.11 Battery notification](#Battery_notification)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Debugging rc.lua](#Debugging_rc.lua)
        *   [4.1.1 awmtt](#awmtt)
    *   [4.2 Log Files](#Log_Files)
    *   [4.3 Mod4 key](#Mod4_key)
        *   [4.3.1 Mod4 key vs. IBM ThinkPad users](#Mod4_key_vs._IBM_ThinkPad_users)
    *   [4.4 Fix Java (GUI appears gray only)](#Fix_Java_.28GUI_appears_gray_only.29)
    *   [4.5 Eclipse: cannot resize/move main window](#Eclipse:_cannot_resize.2Fmove_main_window)
    *   [4.6 YouTube: fullscreen appears in background](#YouTube:_fullscreen_appears_in_background)
    *   [4.7 Prevent the mouse scroll wheel from changing tags](#Prevent_the_mouse_scroll_wheel_from_changing_tags)
    *   [4.8 Starting console clients on specific tags](#Starting_console_clients_on_specific_tags)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [awesome](https://www.archlinux.org/packages/?name=awesome). The development version is [awesome-git](https://aur.archlinux.org/packages/awesome-git/), which is considered unstable and may have a different configuration API.

To run awesome from [Xinitrc](/index.php/Xinitrc "Xinitrc"), add `exec awesome` to `~/.xinitrc`. To use the included [xsession](/index.php/Xsession "Xsession") file, see [Display manager](/index.php/Display_manager "Display manager").

### KDM

Create as root:

 `/usr/share/apps/kdm/sessions/awesome.desktop` 
```
[Desktop Entry]
Name=Awesome
Comment=Tiling Window Manager
Type=Application
Exec=/usr/bin/awesome
TryExec=/usr/bin/awesome
```

### With GNOME

You can set up [GNOME](/index.php/GNOME "GNOME") to use awesome as the visual interface, but have GNOME work in the background. See [awesome wiki](http://awesome.naquadah.org/wiki/Quickly_Setting_up_Awesome_with_Gnome) for details.

## Configuration

The lua based configuration file is at `~/.config/awesome/rc.lua`.

### Creating the configuration file

First, run the following to create the directory needed in the next step:

```
$ mkdir -p ~/.config/awesome/

```

Whenever compiled, awesome will attempt to use whatever custom settings are contained in ~/.config/awesome/rc.lua. This file is not created by default, so we must copy the template file first:

```
$ cp /etc/xdg/awesome/rc.lua ~/.config/awesome/

```

The API for the configuration often changes when awesome updates. So, remember to repeat the command above when you get something strange with awesome, or you want to modify the configuration.

For more information about configuring awesome, check out the [configuration page at awesome wiki](http://awesome.naquadah.org/wiki/Awesome_3_configuration)

#### Examples

**Note:** The API for awesome configuration changes regularly, so you will likely have to modify any file you download.

Some good examples of rc.lua would be as follows:

*   [https://github.com/setkeh/Awesome-3.5](https://github.com/setkeh/Awesome-3.5) - [Setkeh](/index.php/User:Setkeh "User:Setkeh")'s 3.5 Configuration.
*   [http://awesome.naquadah.org/wiki/User_Configuration_Files](http://awesome.naquadah.org/wiki/User_Configuration_Files) - Collection of user configurations on the awesome homepage.

### Extensions

Several extensions are available for awesome (3.5+):

| Extension | Functionality |
| 

*   [Revelation](http://awesome.naquadah.org/wiki/Revelation)

 | Bring up a view of all opened clients |
| 

*   [Shifty](http://awesome.naquadah.org/wiki/Shifty)

 | Dynamic tagging |
| 

*   [Naughty](http://awesome.naquadah.org/wiki/Naughty)

 | Pop-up notifications |
| 

*   [Vicious](http://awesome.naquadah.org/wiki/Vicious) ([README](http://git.sysphere.org/vicious/tree/README))
*   [Obvious](http://awesome.naquadah.org/wiki/Obvious)
*   [Bashets](http://awesome.naquadah.org/wiki/Bashets)

 | Additional [widgets](http://awesome.naquadah.org/wiki/Widgets_in_awesome) |
| 

*   [Run or raise](http://awesome.naquadah.org/wiki/Run_or_raise)

 | Start a program if no instance exists, else jump to it |

### Autorun programs

See [awesome wiki](http://awesome.naquadah.org/wiki/Autostart) and [Autostart](/index.php/Autostart "Autostart").

### Changing keyboard layout

See [awesome wiki](http://awesome.naquadah.org/wiki/Change_keyboard_maps#Display.2Fchange_keyboard_map) and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

### Theming

[Beautiful](http://awesome.naquadah.org/wiki/Beautiful) is a lua library that allows you to theme awesome using an external file, it becomes very easy to dynamically change your whole awesome colours and wallpaper without changing your `rc.lua`.

The default theme is at `/usr/share/awesome/themes/default`. Copy it to `~/.config/awesome/themes/default` and change `theme_path` in `rc.lua`.

```
beautiful.init(awful.util.getdir("config") .. "/themes/default/theme.lua")

```

See also [[1]](http://awesome.naquadah.org/wiki/Beautiful) and [[2]](http://awesome.naquadah.org/wiki/Beautiful_themes).

#### Wallpaper

Beautiful can handle your wallpaper, thus you do not need to set it up in your `.xinitrc` or `.xsession` files. This allows you to have a specific wallpaper for each theme.

With version 3.5 Awesome no longer provides a awsetbg command, instead it has a gears module. You can set your wallpaper inside `theme.lua` with

```
theme.wallpaper = "~/.config/awesome/themes/awesome-wallpaper.png" 

```

To load the wallpaper, make sure your `rc.lua` contains

```
beautiful.init("~/.config/awesome/themes/default/theme.lua")
for s = 1, screen.count() do
	gears.wallpaper.maximized(beautiful.wallpaper, s, true)
end

```

For a random background image, add [[3]](https://gist.github.com/anonymous/37f3b1c58d6616cab756) to `rc.lua` (v3.5+). To automatically fetch images from a given directory use [[4]](https://gist.github.com/anonymous/9072154f03247ab6e28c) instead.

## Tips and tricks

### Hide / show wibox

To map Modkey-b to hide/show default statusbar on active screen (as default in awesome 2.3), add to your *globalkeys* in rc.lua:

```
awful.key({ modkey }, "b", function ()
    mywibox[mouse.screen].visible = not mywibox[mouse.screen].visible
end),

```

### Screenshot

See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") to ensure the `PrtSc` button is assigned correctly. Then install a [screen capturing program](/index.php/Taking_a_screenshot "Taking a screenshot") such as [scrot](/index.php/Taking_a_screenshot#scrot "Taking a screenshot")

Add to the `globalkeys` array:

```
 awful.key({ }, "Print", function () awful.util.spawn("scrot -e 'mv $f ~/screenshots/ 2>/dev/null'") end),

```

This function saves screenshots inside `~/screenshots/`, edit as needed.

### Removing window gaps

As of awesome 3.4, it is possible to remove the small gaps between windows; in the *awful.rules.rules* table there is a *properties* section, add to it

```
 size_hints_honor = false

```

### Transparency

See [composite manager](/index.php/Composite_manager "Composite manager").

In awesome 3.5, window transparency can be set dynamically using signals. For example, `rc.lua` could contain the following:

```
client.connect_signal("focus", function(c)
                              c.border_color = beautiful.border_focus
                              c.opacity = 1
                           end)
client.connect_signal("unfocus", function(c)
                                c.border_color = beautiful.border_normal
                                c.opacity = 0.7
                             end)

```

#### Conky

If using conky, you must set it to create its own window instead of using the desktop. To do so, edit `~/.conkyrc` to contain

```
own_window yes
own_window_transparent yes
own_window_type desktop

```

Otherwise strange behavior may be observed, such as all windows becoming fully transparent. Note also that since conky will be creating a transparent window on your desktop, any actions defined in awesome's `rc.lua` for the desktop will not work where conky is.

#### wiboxes

As of Awesome 3.1, there is built-in pseudo-transparency for wiboxes. To enable it, append 2 hexadecimal digits to the colors in your theme file (`~/.config/awesome/themes/default`, which is usually a copy of `/usr/share/awesome/themes/default`), like shown here:

```
bg_normal = #000000AA

```

where "AA" is the transparency value.

To change transparency for the actual selected window by pressing `Modkey + PgUp/PgDown` you can also use [transset-df](https://www.archlinux.org/packages/?name=transset-df) and the following modification to your `rc.lua`:

```
globalkeys = awful.util.table.join(
    -- your keybindings
    [...]
    awful.key({ modkey }, "Next", function (c)
        awful.util.spawn("transset-df --actual --inc 0.1")
    end),
    awful.key({ modkey }, "Prior", function (c)
        awful.util.spawn("transset-df --actual --dec 0.1")
    end),
    -- Your other key bindings
    [...]
)

```

#### ImageMagick

You may have problems if you set your wallpaper with imagemagick's *display* command. It does not work well with xcompmgr. Please note that awsetbg may be using *display* if it does not have any other options. Installing habak, feh, hsetroot or whatever should fix the problem (*grep -A 1 wpsetters /usr/bin/awsetbg* to see your options).

### Passing content to widgets with awesome-client

You can easily send text to an awesome widget. Just create a new widget:

```
mywidget = widget({ type = "textbox", name = "mywidget" })
mywidget.text = "initial text"

```

To update the text from an external source, use awesome-client:

```
echo -e 'mywidget.text = "new text"' | awesome-client

```

Do not forget to add the widget to your wibox.

### Using a different panel with awesome

If you like awesome's lightweightness and functionality but do not like the way its default panel looks, you can install a different panel, for example [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel).

Then add it to the [autorun section](#Autorun_programs) of your `rc.lua`. You may also comment out the section which creates wiboxes for each screen (starting from `mywibox[s] = awful.wibox({ position = "top", screen = s })`) but it is not necessary. Do not forget to check your `rc.lua` for errors by typing:

```
$ awesome -k rc.lua

```

You should also change your `*modkey*+R` keybinding, in order to start some other application launcher instead of built in awesome. See [List of applications#Application launchers](/index.php/List_of_applications#Application_launchers "List of applications") for examples. Do not forget to add:

```
      properties = { floating = true } },
    { rule = { instance = "$yourapplicationlauncher" },

```

to your `rc.lua`.

### Application directories in menubar

[awesome](https://www.archlinux.org/packages/?name=awesome) includes [menubar](http://awesome.naquadah.org/wiki/Menubar/3.5). By default, pressing `*Mod*+p` will open a dmenu-like applications menu at the top of the screen. However, this menu only searches for `.desktop` files in `/usr/share/applications` and `/usr/local/share/applications`.

To change this, add the following line to `rc.lua`, ideally, under *Menubar configuration*:

```
app_folders = { "/usr/share/applications/", "~/.local/share/applications/" }

```

Note that the `.desktop` files are re-read each time awesome starts, thereby slowing down the startup. If you prefer other means of launching programs, the menubar can be disabled in `rc.lua` by removing `local menubar = require("menubar")` and other references to the `menubar` variable.

### Pop-up menus

There is a simple menu by default in awesome 3, simplifying custom menus. [[5]](http://awesome.naquadah.org/wiki/Awful.menu) If you want a freedesktop.org menu, you could take a look at *[awesome-freedesktop](https://github.com/terceiro/awesome-freedesktop)*. See [[6]](https://gist.github.com/anonymous/5a5ea49638662cefdb3b) for an example for awesome3.

### Applications menu

If you prefer to see a more traditional applications menu when you click on the Awesome icon, or right-click on an empty area of the desktop, you can follow the instructions in [Xdg-menu#Awesome](/index.php/Xdg-menu#Awesome "Xdg-menu"). However this menu is not updated when you add or remove programs. So, be sure to run the command to update your menu. It may look something like:

```
 xdg_menu --format awesome --root-menu /etc/xdg/menus/arch-applications.menu >~/.config/awesome/archmenu.lua

```

### Titlebars

It is easy to enable titlebars in awesome by simply setting the variable titlebars_enabled to true in the config file. However, you may want to be able to toggle the titlebar on or off. You can do this by simply adding something like this to your key bindings:

```
awful.key({ modkey, "Control" }, "t",
   function (c)
       -- toggle titlebar
       awful.titlebar.toggle(c)
   end)

```

Then you may want to initially hide the titlebars. To do that just add this immediately after the title bar is created:

```
awful.titlebar.hide(c)

```

### Battery notification

See [[7]](http://bpdp.blogspot.be/2013/06/battery-warning-notification-for.html) for a simple battery notification to add to `rc.lua`. Note that its needs *naughty* for the notifications (installed by default in version 3.5). Other examples are available at [awesome wiki](https://awesome.naquadah.org/wiki/Gigamo_Battery_Widget#Simple_modular_version_for_3.4)

## Troubleshooting

### Debugging rc.lua

[Xephyr](https://www.archlinux.org/packages/?q=xephyr) allows you to run X nested in another X's client window. This allows you to debug rc.lua without breaking your current desktop. Start by copying rc.lua into a new file (e.g. rc.lua.new), and modify it as needed. Then run new instance of awesome in Xephyr, supplying rc.lua.new as a config file like this:

```
$ Xephyr :1 -ac -br -noreset -screen 1152x720 &
$ DISPLAY=:1.0 awesome -c ~/.config/awesome/rc.lua.new

```

The advantage of this approach is that if you introduce bugs you do not break your current awesome desktop, potentially crashing X apps and losing work. Once you are happy with the new configuration, copy rc.lua.new to rc.lua and restart awesome.

#### awmtt

[awmtt](https://aur.archlinux.org/packages/awmtt/) (Awesome WM Testing Tool) is an easy to use wrapper script around Xephyr. By default, it will use ~/.config/awesome/rc.lua.test. If it cannot find that test file, it will use your actual rc.lua. You can also specify the location of the configuration file you want to test:

```
$ awmtt start -C ~/.config/awesome/rc.lua.new

```

When you are done testing, close the window with:

```
$ awmtt stop

```

Or immediately see the changes you are doing to the configuration file by issuing:

```
$ awmtt restart

```

### Log Files

If you are using [LightDM](/index.php/LightDM "LightDM"), awesome will log errors to `$HOME/.xsession-errors`. If you use `.xinitrc` to start awesome, this [FAQ entry](http://awesome.naquadah.org/wiki/FAQ#Where_are_logs.2C_error_messages_or_something.3F) may be a helpful resource.

### Mod4 key

Awesome recommends to remap `mod4`, which by default should be **Win key**. If for some reason it isn't mapped to `mod4`, use [xmodmap](/index.php/Xmodmap "Xmodmap") to find out what is. To change the mapping, use `xev` to find the keycode and name of the key to be mapped. Then add something like the following to `~/.xinitrc`

```
xmodmap -e "keycode 115 = Super_L" -e "add mod4 = Super_L"
exec awesome

```

The problem in this case is that some xorg installations recognize keycode 115, but incorrectly as the 'Select' key. The above command explictly remaps keycode 115 to the correct 'Super_L' key.

To remap `mod4` with `setxkbmap` (conflict with `xmodmap`) see:

```
tail -50 /usr/share/X11/xkb/rules/evdev

```

To set the caps lock key as `mod4` add the following to [Template:~/.xinitrc](/index.php?title=Template:~/.xinitrc&action=edit&redlink=1 "Template:~/.xinitrc (page does not exist)"):

```
setxkbmap -option caps:hyper

```

#### Mod4 key vs. IBM ThinkPad users

IBM ThinkPads, IBM Model M's and Chromebooks do not come equipped with a Window key (although Lenovo have changed this tradition on their ThinkPads). As of writing, the Alt key is not used in command combinations by the default rc.lua (refer to the Awesome wiki for a table of commands), which allows it be used as a replacement for the Super/Mod4/Win key. To do this, edit your rc.lua and replace:

```
modkey = "Mod4"

```

by:

```
modkey = "Mod1"

```

Note: Awesome does a have a few commands that make use of Mod4 plus a single letter. Changing Mod4 to Mod1/Alt could cause overlaps for some key combinations. The small amount of instances where this happens can be changed in the rc.lua file.

If you have a Chromebook or do not like to change the Awesome standards, you might like to remap a key. For instance the caps lock key is rather useless (for me) adding the following contents to ~/.Xmodmap

```
clear lock
add mod4 = Caps_Lock

```

and run `xmodmap ~/.Xmodmap` to (re)load the file. This will change the caps lock key into the mod4 key and works nicely with the standard awesome settings. In addition, if needed, it provides the mod4 key to other X-programs as well.

Recent updates of xorg related packages break mentioned remapping the second line can be replaced by (tested on a DasKeyboard and IBM Model M and xorg-server 1.14.5-2):

```
keysym Caps_Lock = Super_L Caps_Lock

```

### Fix Java (GUI appears gray only)

See [awesome wiki](http://awesome.naquadah.org/wiki/Problems_with_Java) and [[8]](https://bbs.archlinux.org/viewtopic.php?pid=450870).

### Eclipse: cannot resize/move main window

If you get stuck and cannot move or resize the main window (using mod4 + left/right mouse button) edit the `workbench.xml` and set fullscreen/maximized to false (if set) and reduce the width and height to numbers smaller than your single screen desktop area.

`workbench.xml` can be found in `*eclipse_workspace*/.metadata/.plugins/org.eclipse.ui.workbench/`. Edit the line:

```
<window height="xx" maximized="true" width="xx" x="xx" y="xx"

```

### YouTube: fullscreen appears in background

If YouTube videos appear underneath your web browser when in fullscreen mode, or underneath the panel with controls hidden, add this to `rc.lua`

```
{ rule = { instance = "plugin-container" },
  properties = { floating = true } },

```

With Chromium add

```
{ rule = { instance = "exe" },
  properties = { floating = true } },

```

or:

```
{ rule = { role = "_NET_WM_STATE_FULLSCREEN" },
  properties = { floating = true } },

```

See [[9]](https://bbs.archlinux.org/viewtopic.php?pid=1085494#p1085494).

### Prevent the mouse scroll wheel from changing tags

In your rc.lua, change the Mouse Bindings section to the following;

```
-- {{{ Mouse bindings
root.buttons(awful.util.table.join(
    awful.button({ }, 3, function () mymainmenu:toggle() end)))
-- }}}

```

### Starting console clients on specific tags

It does not work when the console application is invoked from a GTK terminal (e.g. LXTerminal). [URxvt](/index.php/URxvt "URxvt") is known to work.

## See also

*   [http://awesome.naquadah.org/wiki/FAQ](http://awesome.naquadah.org/wiki/FAQ) - FAQ
*   [http://www.lua.org/pil/](http://www.lua.org/pil/) - Programming in Lua (first edition)
*   [http://awesome.naquadah.org/](http://awesome.naquadah.org/) - The official awesome website
*   [http://awesome.naquadah.org/wiki/Main_Page](http://awesome.naquadah.org/wiki/Main_Page) - the awesome wiki
*   [https://bbs.archlinux.org/viewtopic.php?id=88926](https://bbs.archlinux.org/viewtopic.php?id=88926) - share your awesome!