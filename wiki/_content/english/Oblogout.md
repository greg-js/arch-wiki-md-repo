Related articles

*   [Openbox](/index.php/Openbox "Openbox")
*   [Window manager](/index.php/Window_manager "Window manager")

[oblogout](https://www.archlinux.org/packages/?name=oblogout) is an optional, configurable logout script that presents a graphical interface (i.e. buttons) to `cancel`, `logout`, `restart`, `shutdown`, `suspend`, `hibernate`, and `lock` the screen.

## Contents

*   [1 Overview](#Overview)
*   [2 Keybind](#Keybind)
*   [3 Screen locking](#Screen_locking)
*   [4 Button theme](#Button_theme)
*   [5 Button display](#Button_display)
*   [6 Dual Head](#Dual_Head)

## Overview

**Tip:** Where using oblogout, it is best to have a compositor enabled to avoid screen distortion when executed. This is due to the default use of transparancy effects. Alternatively, it is also possible to edit `/etc/oblogout.conf` and amend the `opacity =` command setting to remove transparancy altogether.

Although [oblogout](https://www.archlinux.org/packages/?name=oblogout) may be used with a range of [window managers](/index.php/Window_managers "Window managers"), this article will focus on its use with the [Openbox window manager](/index.php/Openbox "Openbox"). It may be executed as keybind and/or as a desktop menu entry.

## Keybind

To execute the script by pressing `Super`+`x` (i.e. create a **keybind** for it), edit `~/.config/openbox/rc.xml` to add the following to the appropriate part of the `<keyboard>` section:

```
<keybind key="W-x">
 <action name="Execute">
  <startupnotify>
   <enabled>true</enabled>
    <name>oblogut</name>
  </startupnotify>
  <command>oblogout</command>
 </action>
</keybind>

```

## Screen locking

It will be necessary to edit `/etc/oblogout.conf` to change the `lock =` command under the `[commands]` section, in order to execute the desired package installed for this purpose.

For example, where having installed [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") - which must itself also be autostarted as a [Daemon](/index.php/Daemon "Daemon") process in the `~/.config/openbox/autostart` file - then `/etc/oblogout.conf` would be edited accordingly:

```
lock = xscreensaver-command --lock

```

Otherwise, where a package such as [xlockmore](https://www.archlinux.org/packages/?name=xlockmore) has been installed - which does not need to be autostarted - then an example of the necessary command (to lock with a blank screen) would be:

```
lock = xlock -mode blank

```

## Button theme

The default button theme is `oxygen`. A few other themes are also available, including the pre-installed (and more elegant) `foom`. To change the button theme, edit `/etc/oblogout.conf` and change the `buttontheme =` command under the `[looks]` section. An example has been provided below for `foom`:

```
buttontheme = foom

```

## Button display

**Tip:** where changing the order of and/or removing buttons, it is best to use a copy of the default button list, and hash the original. There will then be no need to memorise them.

Default buttons are available to `cancel`, `logout`, `restart`, `shutdown`, `suspend`, `hibernate`, and `lock` the screen. Each button also has a configurable shortcut key assigned (e.g. once oblogout has been executed, the system may then be shutdown by pressing the `s` key, for example).

Both the buttons presented and their order may be configured to suit personal preference. To do so, edit`/etc/oblogout.conf` and change the `buttons =` command under the `[looks]` section. In the example below, the `suspend` and `hibernate` buttons have been removed:

```
buttons = cancel, logout, lock, restart, shutdown
#buttons = cancel, logout, restart, shutdown, suspend, hibernate, lock

```

Where removing or adding buttons, it will also be necessary to amend the appropriate shortcut key commands under the `[shortcuts]` section. Not doing so will mean, for example, that it will still be possible to execute certain functions via the keyboard even where the buttons for them have been removed. For the example provided above, it will be necessary to hash out the `suspend` and `hibernate` shortcuts:

```
[shortcuts]
cancel = Escape
shutdown = S
restart = R
#suspend = U
logout = L
lock = K
#hibernate = H

```

## Dual Head

When using multiple monitors, oblogout may cover all monitors. If you only want oblogout to appear on one monitor, you can create an application rule in the Openbox rc.xml file set oblogout's position and size.

For example, if you have two monitors, and you only want oblogout to appear on the first monitor, add this to the applications section of `rc.xml`:

 `~/.config/openbox/rc.xml` 
```
<applications>
  <application class="oblogout">
    <position force="yes">
      <monitor>1</monitor>
    </position>
    <fullscreen>yes</fullscreen>
  </application>
  ...
</applications>

```