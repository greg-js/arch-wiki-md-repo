# Subtle

From [Subtle project page](http://subforge.org/projects/subtle):

NaN

Subtle is configured with [Ruby](/index.php/Ruby "Ruby") for [Xorg](/index.php/Xorg "Xorg").

**Note:** This article only explain the basics of Subtle. In depth information and tutorials exist at the [Subtle project page](http://subforge.org/projects/subtle).

## Contents

*   [1 Installing](#Installing)
*   [2 Starting Subtle](#Starting_Subtle)
*   [3 Basic function](#Basic_function)
*   [4 Configuration](#Configuration)
*   [5 Sublets](#Sublets)
    *   [5.1 Installing sublets](#Installing_sublets)
    *   [5.2 Enabling sublets](#Enabling_sublets)
*   [6 See also](#See_also)

## Installing

[Install](/index.php/Install "Install") the [subtle-git](https://aur.archlinux.org/packages/subtle-git/)<sup><small>AUR</small></sup> package.

## Starting Subtle

To start Subtle add `exec subtle` to your `.xinitrc` file and launch Xorg. Remember that Subtle does not provide any icons or menus, and the only predefined key binding that opens a terminal is `Super+Enter`, which will open [URxvt](/index.php/URxvt "URxvt"). So if you do not have URxvt, either install it or change the configuration file before starting. If you need to exit Subtle press `Super+Ctrl+q`.

## Basic function

When windows are opened they are matched against a set of user-defined rules to get proper position and size. The process of applying these rules can be broken down in three main parts:

*   View
*   Gravity
*   Tag

_Views_ are the environment in which the windows will be placed. Much like ordinary desktop surfaces. Defining the actual rules for a window is accomplished with a _tag_. In tags you also determine the _gravity_ to be used. Gravities control the size and position of windows.

**Note:** When configuring Subtle you actually need to declare these elements in reverse order. Gravity, tag then view.

## Configuration

Subtle will search for `subtle.rb` in your $XDG_CONFIG_HOME path. If it is non-existant it will load a default file from your $XDG_CONFIG_DIRS path. It is preferable to copy this file to your `$XDG_CONFIG_HOME/subtle` directory instead of using the default.

The default file will contain numerous gravities, tags and views. This is an excellent place to start when designing your own environment. Applications without matching tags will be placed on the view containing the default tag, if no view posses it, they are automatically placed on the first view.

To check your configuration file for potential errors, simply run the following command:

```
$ subtle -k

```

## Sublets

Sublets are tiny apps that appear in the Subtle panels. They can be used to control various applications and show system stats.

### Installing sublets

To install a sublet, type the following command in a terminal:

```
$ sur install <name of sublet>

```

For a list of sublets, go to the [sur website](http://sur.subforge.org).

**Note:** If you install a sublet as root, you will not be able to invoke the sublet as a regular user. Sublets used by non-root accounts must be installed under the user.

### Enabling sublets

By default all sublets are displayed in the top right corner. You can change this behavior in `subtle.rb` by removing `:sublets` from the screen config and adding your sublets like this:

```
screen 1 do
 top [ :title, :spacer, :views ]
 bottom [ :mpd, :wifi, :battery ]
end

```

Then just add the sublets name in the same fashion as the other ones, like this:

```
 bottom [ :mpd,  :<name of sublet>, :wifi, :battery ]

```

It can of course be inserted at a place by your own choice.

## See also

*   [Subtle project page](http://subforge.org/projects/subtle)
*   [Sublets archive](http://sur.subforge.org)
*   [The subtle thread](https://bbs.archlinux.org/viewtopic.php?id=71783)
*   [Share your Subtle desktop!](https://bbs.archlinux.org/viewtopic.php?id=112486)
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login")
*   [Window manager](/index.php/Window_manager "Window manager")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Subtle&oldid=378531](https://wiki.archlinux.org/index.php?title=Subtle&oldid=378531)"