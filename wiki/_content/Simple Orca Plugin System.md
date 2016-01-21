# Simple Orca Plugin System

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** This wiki page is a work in progress by chrys. (Discuss in [Talk:Simple Orca Plugin System#](https://wiki.archlinux.org/index.php/Talk:Simple_Orca_Plugin_System))

With the Simple Orca Plugin System (SOPS) you can extend the functionality of the orca screenreader. It offers the posibility to do this nearby any programming language in a easy way. The settings for the plugins are controlled via the filename.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
*   [3 Plugins](#Plugins)
    *   [3.1 Structure of the filename](#Structure_of_the_filename)
        *   [3.1.1 Modifiers](#Modifiers)
            *   [3.1.1.1 Valid modifier combinations](#Valid_modifier_combinations)
        *   [3.1.2 Key](#Key)
        *   [3.1.3 Commands](#Commands)
        *   [3.1.4 Examples](#Examples)
    *   [3.2 Types of plugins](#Types_of_plugins)
        *   [3.2.1 Subprocess plugins](#Subprocess_plugins)
            *   [3.2.1.1 Requrements](#Requrements)
            *   [3.2.1.2 Example](#Example)
        *   [3.2.2 Advanced plugins](#Advanced_plugins)
            *   [3.2.2.1 Requrements](#Requrements_2)
            *   [3.2.2.2 Example](#Example_2)
*   [4 Administration](#Administration)
    *   [4.1 Basics](#Basics)
    *   [4.2 Administration tools](#Administration_tools)
*   [5 Plugin hosting](#Plugin_hosting)

## Installation

Just [Install](/index.php/Install "Install") the package [simpleorcapluginsystem-git](https://aur.archlinux.org/packages/simpleorcapluginsystem-git/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## Setup

To setup the pluginsystem for the current user, just run

 `$ _/usr/share/SOPS/install-for-current-user.sh_` 

## Plugins

### Structure of the filename

The behaviour and and preferences of an plugin are controlled by its filename. The description part have to be seperated to the preferences part wtih `__-__`. The commands, modifier and the key has to be seperated by `__+__`. `<description>__-__[<command>__+__command...][__+__<modifier>__+__<modiier>__+__]<key>[.ext]`

#### Modifiers

With modifiers you could set different shortcut combinations to the `key`. You always have to press the orca key. The order of those three modifier keys doesn't matter and they are optional

*   `control` is the modifier for the `ctrl` key
*   `shift` is the modifier for the `shift` key
*   `alt` is the modifier for the `alt` key

##### Valid modifier combinations

If they are exist only a few combinations of modifiers are valid. Those are predefined by orca. Valid combinations are:

*   `alt` i.e. `description__-__alt__+__w.sh`
*   `control` i.e. `description__-__control__+__w.sh`
*   `shift` i.e. `description__-__shift__+__w.sh`
*   `control__+__alt` i.e. `description__-__control__+__alt+w.py`

#### Key

The `key` in the filename defines the basic shortcut that is used for that plugin (maybe together with the defined modifiers). You have to define a `key` or use the `exec` command for running once at start. Otherwhise the plugin is not loaded. The key, if one exists, has to be the last part in the filename before the extension starts. example_plugin__-__d.sh uses `orca+d` as shortcut.

#### Commands

With commands you could control the behavior of the plugins. You could add more than one command. The order of the commands doesnt matter. You can use them for all kinds of plugins.

*   `startnotify` announce "start <description>" before the plugin is executed. this useful as feedback for

plugins with longer progress times.

*   `stopnotify` announce "finish <description>". This is useful as feedback for plugins with no output.
*   `blockcall` don't start plugin in a thread, be careful, this locks orca until the plugin is finish. By default, plugins run in there own thread.
*   `showstderr` not only show stdout but also stderr
*   `parameters <parameter1> [parameter2] [parameter3]...` passes the parameters to the plugin
*   `exec` run the plugin once while loading it.
*   `loadmodule` does not load as a subprocess plugin but load it as advanced plugin.

#### Examples

*   `Plugin name__-__startnotify__+__control__+__alt__+__n.sh` Run with `orca+ctrl+alt+n` and announce the start of the process.
*   `PluginName__-__showstderr__+__stopnotify__+__shift__+__y.py` Run with `orca+shift+m` and announce the finishing. Does also read occouring errors .
*   `Plugin_Name__-__m.py` Run with `orca+m`
*   `Plugin_Name__-__exec.py` Run once at starting orca.

### Types of plugins

Basicaly there are two different types of plugins

#### Subprocess plugins

Those are realy simple plugins. They could be represented by any type of application or script that writes to STDOUT or STDERR. Orca executes the plugin, reads from STDOUT/ STDERR and announce the result to the user, when the defined shortcut is pressed or the plugin is executed via `exec` while starting screenreader.

##### Requrements

*   Execution permission
*   `key` or `exec` have to been defined in filename.

##### Example

Say "Hello World when pressing `orca+y`: Filename:`Hello_world__-__y.sh`

```
_#!/bin/sh_
echo "Hello World"
```

#### Advanced plugins

Those type of plugins are loaded with spec.loader.exec_module. They are fully included into orca as soon as orca starts. Advanced plugins are more powerful because you are able to work in orca context. They are mostly similar to the `orca-customizations.py`. See here for "real" orca scripting: [https://wiki.gnome.org/Projects/Orca/FrequentlyAskedQuestions/CustomizingOrca](https://wiki.gnome.org/Projects/Orca/FrequentlyAskedQuestions/CustomizingOrca)

##### Requrements

*   Correct code written in python3
*   Fileextension `.py`
*   Use `loadmodule` in the filename
*   `key` or `exec` have to been defined in filename

##### Example

Configure orca to speak/braille the word "bang" insteed of the "!" while loading the plugin. Filename:`replace_chnames__-__loadmodule__+__exec.py`

```
_#!/bin/python_
import orca.orca
orca.chnames.chnames["!"] = "bang"
```

## Administration

### Basics

*   This contains the default plugins and the administration tools:

`/usr/share/SOPS/`

*   Here you could put your own plugins:

`~/.config/SOPS/plugins-available`

*   Here are the the enabled (active) plugins located. All plugins in that folder will be loaded if they are valid.

`~/.config/SOPS/plugins-enabled`

### Administration tools

The tools are located in the "tools" folder at the installation directory. Enables an plugin so its active. But you have to rename the filename for having a shortcut and commands.

 `$ _./ensop <pluginname>_` 

Disable the plugin, its not loaded anymore.

 `$ _./dissop <pluginname>_` 

They basicaly just create links in ~./.config/SOPSP/plugins-enabled and make the plugins executable. You have to configure the plugins manualy. To reload the plugins in orca, you have to restart orca. SOPS also provides an plugin manager. its available after the installation. To open the plugin manager use `orca+ctrl+p` while orca is running. It can be used to activate, deactivate, install or configure plugins. Orca gets automatically new started after closing the plugin manager.

## Plugin hosting

You can also host plugins. So they are available for installation via the plugin manager. I you want to Host plugins read: `/usr/share/SOPS/tools/hosting.txt`

Default online resource: [https://stormdragon.tk/orca-plugins/index.php](https://stormdragon.tk/orca-plugins/index.php)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Simple_Orca_Plugin_System&oldid=416414](https://wiki.archlinux.org/index.php?title=Simple_Orca_Plugin_System&oldid=416414)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Accessibility](/index.php/Category:Accessibility "Category:Accessibility")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")