# Simple Orca Plugin System

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** This wiki page is a work in progress by chrys. (Discuss in [Talk:Simple Orca Plugin System#](https://wiki.archlinux.org/index.php/Talk:Simple_Orca_Plugin_System))

With the Simple Orca Plugin System (SOPS) you can extend the functionality of the Orca screen reader. It offers the possibility to do this nearby any programming language in a easy way. The settings for the plug ins are controlled via the filename.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
*   [3 Administration](#Administration)
    *   [3.1 Basics](#Basics)
    *   [3.2 Administration tools](#Administration_tools)
*   [4 Plug-ins](#Plug-ins)
    *   [4.1 Structure of the filename](#Structure_of_the_filename)
        *   [4.1.1 Modifiers](#Modifiers)
            *   [4.1.1.1 Valid modifier combinations](#Valid_modifier_combinations)
        *   [4.1.2 Key](#Key)
        *   [4.1.3 Commands](#Commands)
        *   [4.1.4 Examples](#Examples)
    *   [4.2 Types of plug-ins](#Types_of_plug-ins)
        *   [4.2.1 Subprocess plug-ins](#Subprocess_plug-ins)
            *   [4.2.1.1 Requirements](#Requirements)
            *   [4.2.1.2 Example](#Example)
        *   [4.2.2 Advanced plug-ins](#Advanced_plug-ins)
            *   [4.2.2.1 Requirements](#Requirements_2)
            *   [4.2.2.2 Example](#Example_2)
*   [5 Plug-in hosting](#Plug-in_hosting)

## Installation

Just [Install](/index.php/Install "Install") the package [simpleorcapluginsystem-git](https://aur.archlinux.org/packages/simpleorcapluginsystem-git/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## Setup

To setup the plug-in system for the current user, just run

 `$ _/usr/share/SOPS/install-for-current-user.sh_` 

## Administration

### Basics

*   The Installation path. This contains the default plug-ins and the administration tools:

`/usr/share/SOPS/`

*   Here you could put your own plug-ins:

`~/.config/SOPS/plugins-available/`

*   Here are the the enabled (active) plug-ins located. All plug-ins in that folder will be loaded if they are valid.

`~/.config/SOPS/plugins-enabled/`

### Administration tools

The tools are located in the "tools" folder at the installation directory. Enables an plug-in so its active. But you have to rename the filename for having a shortcut and commands.

 `$ _./ensop <pluginname>_` 

Disable the plug-in, its not loaded anymore.

 `$ _./dissop <pluginname>_` 

They basically just create links in ~./.config/SOPSP/plugins-enabled and make the plug-ins executable. You have to configure the plug-ins manually. To reload the plug-ins in Orca, you have to restart Orca. SOPS also provides an plug-in manager. its available after the installation. To open the plug-in manager use `orca+ctrl+p` while Orca is running. It can be used to activate, deactivate, install or configure plug-ins. Orca gets automatically new started after closing the plug-in manager.

## Plug-ins

**Tip:** You can find some fully predefined example plugins in `/usr/share/SOPS/examples`.

### Structure of the filename

The behavior and and preferences of an plug-in are controlled by its filename. The description part have to be separated to the preferences part with `__-__`. The commands, modifier and the key has to be separated by `__+__`. `<description>__-__[<command>__+__command...][__+__<modifier>__+__<modifier>__+__]<key>[.ext]`

#### Modifiers

With modifiers you could set different shortcut combinations to the `key`. You always have to press the Orca-modifier. The order of those three modifier keys doesn't matter and they are optional

*   `control` is the modifier for the `ctrl` key on the keyboard
*   `shift` is the modifier for the `shift` key on the keyboard
*   `alt` is the modifier for the `alt` key on the keyboard

##### Valid modifier combinations

If they are exist only a few combinations of modifiers are valid. Those are predefined by Orca. Valid combinations are:

*   `alt` i.e. `description__-__alt__+__w.sh`
*   `control` i.e. `description__-__control__+__w.sh`
*   `shift` i.e. `description__-__shift__+__w.sh`
*   `control__+__alt` i.e. `description__-__control__+__alt+w.py`

#### Key

The `key` in the filename defines the basic shortcut that is used for that plug-in (maybe together with the defined modifiers). You have to define a `key` or use the `exec` command for running once at start. Otherwise the plug-in is not loaded. The key, if one exists, has to be the last part in the filename before the extension starts. example_plugin__-__d.sh uses `orca+d` as shortcut.

#### Commands

With commands you could control the behavior of the plug-ins. You could add more than one command. The order of the commands doesn't matter. You can use them for all kinds of plug-ins.

*   `startnotify` announce "start <description>" before the plug-in is executed. this useful as feedback for

plugins with longer progress times.

*   `stopnotify` announce "finish <description>". This is useful as feedback for plug-ins with no output.
*   `blockcall` don't start plug-in in a thread, be careful, this locks Orca until the plug-in is finish. By default, plug-ins run in there own thread.
*   `error` announce thrown errors
*   `parameters <parameter1> [parameter2] [parameter3]...` passes the parameters to the plug-in
*   `exec` run the plug-in once while loading it.
*   `loadmodule` does not load as a subprocess plug-in but load it as advanced plug-in.

#### Examples

*   `Plugin name__-__startnotify__+__control__+__alt__+__n.sh` Run with `orca+ctrl+alt+n` and announce the start of the process.
*   `PluginName__-__error__+__stopnotify__+__shift__+__y.py` Run with `orca+shift+m` and announce the finishing. Does also read occurring errors .
*   `Plugin_Name__-__m.py` Run with `orca+m`
*   `Plugin_Name__-__exec.py` Run once at starting Orca.

### Types of plug-ins

Basically there are two different types of plugins

#### Subprocess plug-ins

Those are really simple plug-ins. They could be represented by any type of application or script that writes to STDOUT or STDERR. Orca executes the plug-in, reads from STDOUT/ STDERR and announce the result to the user, when the defined shortcut is pressed or the plug-in is executed via `exec` while starting screen reader.

##### Requirements

*   Execution permission
*   `key` or `exec` have to been defined in filename.

##### Example

Say "Hello World when pressing `orca+y`: Filename:`Hello_world__-__y.sh`

```
_#!/bin/sh_
echo "Hello World"
```

#### Advanced plug-ins

Those type of plug-ins are loaded with spec.loader.exec_module. They are fully included into Orca as soon as it starts. Advanced plug-ins are more powerful because you are able to work in orca context. They are mostly similar to the `orca-customizations.py`. See here for "real" Orca scripting: [https://wiki.gnome.org/Projects/Orca/FrequentlyAskedQuestions/CustomizingOrca](https://wiki.gnome.org/Projects/Orca/FrequentlyAskedQuestions/CustomizingOrca)

##### Requirements

*   Correct code written in python3
*   Fileextension `.py`
*   Use `loadmodule` in the filename
*   `key` or `exec` have to been defined in filename

##### Example

Configure Orca to speak/braille the word "bang" instead of the "!" while loading the plug-in. Filename:`replace_chnames__-__loadmodule__+__exec.py`

```
_#!/bin/python_
import orca.orca
orca.chnames.chnames["!"] = "bang"
```

## Plug-in hosting

You can also host plug-ins. So they are available for installation via the plug-in manager. I you want to Host plug-ins read: `/usr/share/SOPS/tools/hosting.txt`

Default online resource: [https://stormdragon.tk/orca-plugins/index.php](https://stormdragon.tk/orca-plugins/index.php)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Simple_Orca_Plugin_System&oldid=416932](https://wiki.archlinux.org/index.php?title=Simple_Orca_Plugin_System&oldid=416932)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Accessibility](/index.php/Category:Accessibility "Category:Accessibility")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")