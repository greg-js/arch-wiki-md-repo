Related articles

*   [Desktop Notifications](/index.php/Desktop_Notifications "Desktop Notifications")
*   [Dunstify](/index.php/Dunstify "Dunstify")

[Dunst](https://dunst-project.org/) is a lightweight replacement for the notification-daemons provided by most desktop environments.

## Contents

*   [1 Installation](#Installation)
*   [2 Appearance](#Appearance)
    *   [2.1 Icon Sets](#Icon_Sets)
*   [3 Shortcuts](#Shortcuts)
*   [4 Rules](#Rules)
    *   [4.1 Filtering](#Filtering)
    *   [4.2 Modifying](#Modifying)
    *   [4.3 Scripting](#Scripting)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Dunst fails to start via systemd](#Dunst_fails_to_start_via_systemd)

## Installation

[Install](/index.php/Install "Install") the [dunst](https://www.archlinux.org/packages/?name=dunst) package. There is no need to start or enable dunst; it is called by systemd when programs send notifications through dbus.

An example configuration file is included at `/usr/share/dunst/dunstrc`. Copy this file to `~/.config/dunst/dunstrc` and edit it accordingly.

## Appearance

Dunst allows for the use of html markup in notifications. Some examples are bold, italics, strikethrough and underline. For a complete reference see [[1]](https://developer.gnome.org/pango/stable/PangoMarkupFormat.html). HTML can be stripped from notifications if `markup` is set to `none`.

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

Icons are set in the option `icon_path`. Status and devices icons are needed. By default, Dunst looks for the [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) icons. For example, to use [adwaita-icon-theme](https://www.archlinux.org/packages/?name=adwaita-icon-theme) (gnome-icon-theme's successor), instead:

```
icon_path = /usr/share/icons/Adwaita/16x16/status/:/usr/share/icons/Adwaita/16x16/devices/

```

## Shortcuts

Idle thresholds can be set letting the notification stay onscreen if the user is idle longer than the threshold.

To close a notification before it times out use `Control + space`. If multiple notifications are onscreen `Control + Shift + Space` closes all of them.

**Tip:** The commands for closing and reopening notifications can be changed. If using a symbol rather than an alphabetical letter it must be spelled out, e.g. period.

A history list can be accessed by using `Control + grave`. A context menu can be opened using `Control + Shift + period`. The context menu uses dmenu to filter out URLs and open them in your browser. The default browser can be set in the config like so:

```
browser = /usr/bin/chromium 

```

## Rules

You can create rules in your dunstrc file which match certain notifications and then perform an action on it such as executing a script.

### Filtering

To create a new rule create a new section with a custom name in your config file. In that section you can now use the attributes appname, summary, body, icon, category, match_transient and msg_urgency to match the notification. Globbing is supported. See [Scripting](#Scripting) for an example. Start dunst with the `-print` option to find out useful information about a notification to write proper rules.

### Modifying

When a notification is matched you can perform certain actions on it like modifying the format string, which is especially useful if you want tocompletely ignore certain notifications. In that case simply add the line `format=""` to your rule.

Another useful feature is if you want to keep certain notifications out of your history for example if you use dunst as a [Volume indicator](/index.php/Dunstify#Using_dunstify_as_volume/brightness_level_indicator "Dunstify"). To achieve this simply add `history_ignore=yes` to your rule.

### Scripting

Dunst can be configured to run scripts based on certain notification content. Here is an example using Dunst to run a script when someone from [pidgin](https://www.archlinux.org/packages/?name=pidgin) signs on:

```
[signed_on]
   appname = Pidgin
   summary = "*signed on*"
   urgency = low
   script = do_something.sh

```

The specified script will be passed the following parameters in that order: appname, summary, body, icon, urgency.

## Troubleshooting

### Dunst fails to start via systemd

When using dunst without a Display Manager, the `DISPLAY` environment variable might not be correctly set.[[2]](https://github.com/dunst-project/dunst/issues/347)

To fix this, add the following to your `.xinitrc`:

```
systemctl --user import-environment DISPLAY

```