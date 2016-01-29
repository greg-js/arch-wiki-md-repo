# Simple Orca Plugin System

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** This wiki page is a work in progress by chrys. (Discuss in [Talk:Simple Orca Plugin System#](https://wiki.archlinux.org/index.php/Talk:Simple_Orca_Plugin_System))

With the Simple Orca Plugin System (SOPS) you can extend the functionality of the Orca screen reader. It offers the possibility to add plug-ins in nearly any programming language in an easy way. The settings for the plug-ins are controlled via the filename.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
*   [3 Administration](#Administration)
    *   [3.1 Basics](#Basics)
    *   [3.2 Administration tools](#Administration_tools)
*   [4 Plug-ins](#Plug-ins)
    *   [4.1 Structure of the filename](#Structure_of_the_filename)
    *   [4.2 Run a plug-in](#Run_a_plug-in)
        *   [4.2.1 Modifiers/ Shortcuts](#Modifiers.2F_Shortcuts)
            *   [4.2.1.1 Valid shortcuts](#Valid_shortcuts)
        *   [4.2.2 Commands/ Preferences](#Commands.2F_Preferences)
        *   [4.2.3 Examples](#Examples)
    *   [4.3 Types of plug-ins](#Types_of_plug-ins)
        *   [4.3.1 Sub process plug-ins](#Sub_process_plug-ins)
            *   [4.3.1.1 Requirements](#Requirements)
            *   [4.3.1.2 Example](#Example)
        *   [4.3.2 Advanced plug-ins](#Advanced_plug-ins)
            *   [4.3.2.1 Requirements](#Requirements_2)
            *   [4.3.2.2 Example](#Example_2)
*   [5 Plug-in hosting](#Plug-in_hosting)

## Installation

Just [Install](/index.php/Install "Install") the package [simpleorcapluginsystem-git](https://aur.archlinux.org/packages/simpleorcapluginsystem-git/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## Setup

To setup the plug-in system for the current user, run:

 `$ _/usr/share/SOPS/install-for-current-user.sh_` 

## Administration

### Basics

*   The Installation path. This contains the default plug-ins, the documentation,the plugin loader and the administration tools:

NaN

*   The path for user plug-ins is:

NaN

*   The following path is used for all enabled (active) plug-ins. All plug-ins in that folder will be loaded, if they are valid:

NaN

### Administration tools

The tools are located in the "tools" folder beneath the installation directory. The following command enables/activates a plug-in, but you have to rename the filename to create a shortcut and pass a command to the plug-in:

```
$ _./ensop <pluginname>_ 

```

The command to disable and unload a plug-in is:

```
$ _./dissop <pluginname>_

```

Both commands basically just create or delete links in `~./.config/SOPSP/plugins-enabled` and make the plug-ins executable. You have to configure the plug-ins manually. Restart Orca to reload the plug-ins after changes. SOPS also provides a plug-in manager, it is available after the installation. To open the plug-in manager use `orca+ctrl+p` while Orca is running. It can be used to activate, deactivate, install or configure plug-ins. Orca gets re-started automatically after closing the plug-in manager.

## Plug-ins

**Tip:** You can find some fully predefined example plugins in `/usr/share/SOPS/examples`.

### Structure of the filename

The shortcut, plug-in type and preference of a plug-in are controlled by its filename. The descriptive part of the filename has to be separated from the preferences part with `__-__`. The commands, modifier and the key has to be separated by `__+__`.

```
<description>__-__[<command>__+__command...][__+__<modifier>__+__<modifier>__+__key_<key>].ext

```

### Run a plug-in

There are two different ways to run a plug-in:

*   shortcut (See [#Modifiers/ Shortcuts](#Modifiers.2F_Shortcuts))
*   exec run once when the plug-in loads. (See [#Commands/ Preferences](#Commands.2F_Preferences))

If none of those are present. the plug-in does not load. There are some more [#Commands](#Commands) to control the behaviour of a plug-in.

#### Modifiers/ Shortcuts

With modifiers you can set different shortcut combinations for a `key`. You always have to press the Orca-modifier. The order of the three modifier keys does not matter:

*   `control` is the modifier for the `ctrl` key on the keyboard
*   `shift` is the modifier for the `shift` key on the keyboard
*   `alt` is the modifier for the `alt` key on the keyboard
*   `key_<key>` defines the basic shortcut that is used for the plug-in, maybe together with the defined modifiers (example_plugin__-__key_d.sh uses `orca+d`).

##### Valid shortcuts

Only a few combinations of modifiers are valid. Those are predefined by Orca. Valid combinations are:

*   `alt` i.e. `description__-__alt__+__key_y.sh`
*   `control` i.e. `description__-__control__+__key_b.sh`
*   `shift` i.e. `description__-__shift__+__key_c.sh`
*   `control + alt` i.e. `description__-__control__+__alt+key_w.py`
*   `shift + alt` i.e. `description__-__shift__+__alt__+__key_y.sh`

As `key_<key>` you can use every alphanumerical key.

#### Commands/ Preferences

Preferences for plug-ins are called commands. A command defines the action to pass to the plug-in. With commands you control the behaviour of the plug-ins. You may add more than one command. The order of the commands does not matter. You can use them mostly for all kinds of plug-ins.

*   `startnotify` announces "start <description>" before the plug-in is executed. It is useful as feedback for plug-ins with longer progress times. (all plug-ins)
*   `stopnotify` announces "finish <description>". This is useful as feedback for plug-ins with no output. (all plugins)
*   `blockcall` do not start the plug-in in a thread. Be careful, as this locks Orca until the plug-in is finished. By default, plug-ins each run in a dedicated thread. (all plug-ins)
*   `error` announces returned errors. (all plug-ins)
*   `supressoutput` ignores the output of STDOUT. This is useful for plugins that may have a UI and do not pass output to STDOUT. (sub process plug-in only)
*   `parameters_<parameter1> [parameter2] [parameter3]...` passes the parameters to the plug-in. (sub process plug-in only)
*   `exec` run the plug-in once while loading it. Mostly useful as advanced-plug-in. (all plug-ins)
*   `loadmodule` does not load as a sub process plug-in but loads it as advanced plug-in. (advanced plug-in only)

#### Examples

*   `Plugin name__-__startnotify__+__control__+__alt__+__key_n.sh` Run with `orca+ctrl+alt+n` and announce the start of the process.
*   `PluginName__-__error__+__stopnotify__+__shift__+__key_y.py` Run with `orca+shift+m` and announce the finishing. Does also read occurring errors .
*   `Plugin_Name__-__key_m.py` Run with `orca+m`
*   `Plugin_Name__-__exec.py` Run once at starting Orca.

### Types of plug-ins

Basically there are two different types of plugins.

#### Sub process plug-ins

Sub process plug-ins are simple plug-ins and the default type. They may be any type of application or script that writes to STDOUT or STDERR. Orca executes the plug-in, reads from STDOUT/ STDERR and announces the result to the user, when the defined shortcut is pressed or the plug-in is executed via `exec` while starting screen reader.

##### Requirements

*   Execution permission
*   `key_<key>` or `exec` have to be defined in the filename.

##### Example

Say "Hello World when pressing `orca+y`: Filename:`Hello_world__-__key_y.sh`

```
_#!/bin/sh_
echo "Hello World"
```

#### Advanced plug-ins

Those type of plug-ins are loaded with the spec.loader.exec_module. you can load them by using `loadmodule` in the filename. They are fully included into Orca as soon as it starts. Advanced plug-ins are more powerful, because you are able to work in the Orca context. They are mostly similar to the `orca-customizations.py`. See also for "real" Orca scripting: [https://wiki.gnome.org/Projects/Orca/FrequentlyAskedQuestions/CustomizingOrca](https://wiki.gnome.org/Projects/Orca/FrequentlyAskedQuestions/CustomizingOrca)

##### Requirements

*   Correct code written in python3
*   Fileextension `.py`
*   Use `loadmodule` in the filename
*   `key_<key>` or `exec` have to been defined in filename

##### Example

Configure Orca to speak/braille the word "bang" instead of the "!" while loading the plug-in. Filename:`replace_chnames__-__loadmodule__+__exec.py`

```
_#!/bin/python_
import orca.orca
orca.chnames.chnames["!"] = "bang"
```

## Plug-in hosting

You can also host plug-ins, making them available for installation via the plug-in manager. If you want to Host plug-ins, read: `/usr/share/SOPS/tools/hosting.txt`

The default online resource is: [https://stormdragon.tk/orca-plugins/index.php](https://stormdragon.tk/orca-plugins/index.php)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Simple_Orca_Plugin_System&oldid=418039](https://wiki.archlinux.org/index.php?title=Simple_Orca_Plugin_System&oldid=418039)"