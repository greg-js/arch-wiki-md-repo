[Dunst](http://knopwob.org/dunst/index.html) is a lightweight replacement for the notification-daemons provided by most desktop environments.

## Contents

*   [1 Installation](#Installation)
*   [2 Appearance](#Appearance)
    *   [2.1 Icon Sets](#Icon_Sets)
*   [3 Shortcuts](#Shortcuts)
*   [4 Scripting](#Scripting)

## Installation

[Install](/index.php/Install "Install") the [dunst](https://www.archlinux.org/packages/?name=dunst) package.

An example configuration file is included at `/usr/share/dunst/dunstrc`.

Copy this file to ~/.config/dunst/dunstrc and edit it accordingly.

```
$ cp /usr/share/dunst/dunstrc ~/.config/dunst/dunstrc

```

## Appearance

Dunst allows for the use of html markup in notifications. Some examples are bold, italics, strikethrough and underline. For a complete reference see [https://developer.gnome.org/pango/stable/PangoMarkupFormat.html](https://developer.gnome.org/pango/stable/PangoMarkupFormat.html). HTML can be stripped from notifications if `allow_markup` is set to `no`.

The formatting of the notification can be specified. Options are as follows:

```
%a  appname
%s  summary
%b  body
%i  iconname (including its path)
%I  iconname (without its path)
%p  progress value if set ([  0%] to [100%]) or nothing

```

These can be used in conjunction with HTML markup. For example the `format` can be set to `<b>%s</b>
%b` for a bolded notification summary, a newline and the body unformatted.

### Icon Sets

Icons are set in the option `icon_folders`. Status and devices icons are needed.

```
# Paths to default icons.
icon_folders = /usr/share/icons/Arc/status/16/:/usr/share/icons/Arc/devices/16/

```

## Shortcuts

Idle thresholds can be set letting the notification stay onscreen if the user is idle longer than the threhold.

To close a notification before it times out use `Control + space`. If multiple notifications are onscreen `Control + Shift + Space` closes all of them.

**Tip:** The commands for closing and reopening notifications can be changed. If using a symbol rather than an alphabetical letter it must be spelled out, e.g. period.

A history list can be accessed by using `Control + grave`. A context menu can be opened using `Control + Shift + period`. The context menu uses dmenu to filter out URLs and open them in your browser. The default browser can be set in the config like so:

```
browser = /usr/bin/chromium 

```

## Scripting

Dunst can be configured to run scripts based on certain notification content. Here is an example using Dunst to run a script when someone from [pidgin](https://www.archlinux.org/packages/?name=pidgin) signs on:

```
[signed_on]
   appname = Pidgin
   summary = "*signed on*"
   urgency = low
   script = do_something.sh

```