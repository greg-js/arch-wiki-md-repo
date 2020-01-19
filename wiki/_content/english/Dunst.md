Related articles

*   [Desktop Notifications](/index.php/Desktop_Notifications "Desktop Notifications")

[Dunst](https://dunst-project.org/) is a lightweight replacement for the notification-daemons provided by most desktop environments.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Appearance](#Appearance)
    *   [2.1 Icon sets](#Icon_sets)
*   [3 Shortcuts](#Shortcuts)
*   [4 Rules](#Rules)
    *   [4.1 Filtering](#Filtering)
    *   [4.2 Modifying](#Modifying)
    *   [4.3 Scripting](#Scripting)
*   [5 Disable dunst temporarily](#Disable_dunst_temporarily)
*   [6 Dunstify](#Dunstify)
    *   [6.1 Notification ID](#Notification_ID)
    *   [6.2 Actions](#Actions)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Using dunstify as volume/brightness level indicator](#Using_dunstify_as_volume/brightness_level_indicator)
    *   [7.2 Overwrite previous notification](#Overwrite_previous_notification)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Dunst fails to start via systemd](#Dunst_fails_to_start_via_systemd)
    *   [8.2 Non-matching font sizes (Emojis much larger than text)](#Non-matching_font_sizes_(Emojis_much_larger_than_text))

## Installation

[Install](/index.php/Install "Install") the [dunst](https://www.archlinux.org/packages/?name=dunst) package. Launch `/usr/bin/dunst` and make sure your window manager or desktop environment starts it on startup/login.

**Note:** It may seem like there's no need to manually start dunst, as it may get autostarted by dbus-daemon when programs send notifications through D-Bus. However, the notification service frequently has multiple daemons installed, and there is no way to know which daemon will be autostarted. The dbus-daemon maintainers explicitly warn against relying on autostart for multiple-provider services.

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

### Icon sets

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

When a notification is matched you can perform certain actions on it like modifying the format string, which is especially useful if you want to completely ignore certain notifications. In that case simply add the line `format=""` to your rule.

Another useful feature is if you want to keep certain notifications out of your history for example if you use dunst as a [Volume indicator](#Using_dunstify_as_volume/brightness_level_indicator). To achieve this simply add `history_ignore=yes` to your rule.

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

## Disable dunst temporarily

To disable dunst temporarily there are two options.

	Send a special notification

	Use `notify-send "DUNST_COMMAND_PAUSE"` to disable and `notify-send "DUNST_COMMAND_RESUME"` to reenable.

	Use `killall`

	Use `killall -SIGUSR1 dunst` to disable and `killall -SIGUSR2 dunst` to reenable

Once paused dunst will hold back all notifications. After enabling dunst again all held back notifications will be displayed.

## Dunstify

Dunstify is an alternative to the [notify-send](/index.php/Desktop_notifications#Usage_in_programming "Desktop notifications") command which is completely compatible to notify-send and can be used alongside it, but offers some more features. Dunstify works only with the <a class="mw-selflink selflink">Dunst</a> notification daemon.

Additionally to the options available in notify-send, dunstify offers some more features like IDs and actions.

### Notification ID

You can assign an ID to a notification by calling dunstify with the `-r ID` option, where `ID` needs to be an integer. If a notification with that ID already exists it will be replaced with the new one(therefore the long option name `--replace=ID`).

Furthermore you can close a notification by using `dunstify --close=ID`.

### Actions

You can define actions which can be invoked directly from the notification by specifying one or more `--action=action,label` parameters. For instance:

```
dunstify --action="replyAction,reply" "Message received"

```

The user can then access the specified actions via Dunst's context menu. The call to dunstify will block until either the notification disappears or an action is selected. In the former case dunstify will return 1 if the notification timed out and 2 if it was dismissed manually [[2]](https://developer.gnome.org/notification-spec/#signals). In the latter case it returns the action which was selected by the Dunst context menu.

In addition to invoking actions with the context menu, you may also define how mouse events invoke actions [[3]](https://github.com/dunst-project/dunst/blob/3f3082efb3724dcd369de78dc94d41190d089acf/dunstrc#L237). This allows Dunst to be used interactively, as was suggested in [[4]](https://github.com/dunst-project/dunst/issues/163#issuecomment-573191650). When a notification has only one action, or when an action is named "default", that action may be invoked by middle-clicking the notification (by default or when `dunstrc` defines `mouse_middle_click = do_action`).

```
reply_action () {}
forward_action () {}
handle_dismiss () {}

ACTION=$(dunstify --action="default,Reply" --action="forwardAction,Forward" "Message Received")

case "$ACTION" in
"default")
    reply_action
    ;;
"forwardAction")
    forward_action
    ;;
"2")
    handle_dismiss
    ;;
esac

```

## Tips and tricks

### Using dunstify as volume/brightness level indicator

You can use the replace id feature to implement a simple volume or brightness indicator notification like in this picture [[5]](https://i.postimg.cc/j2CDkS1H/screen1712.png).

To realize that volume indicator place the following script somewhere on your `PATH`.

```
#!/bin/bash
# changeVolume

# Arbitrary but unique message id
msgId="991049"

# Change the volume using alsa(might differ if you use pulseaudio)
amixer -c 0 set Master "$@" > /dev/null

# Query amixer for the current volume and whether or not the speaker is muted
volume="$(amixer -c 0 get Master | tail -1 | awk '{print $4}' | sed 's/[^0-9]*//g')"
mute="$(amixer -c 0 get Master | tail -1 | awk '{print $6}' | sed 's/[^a-z]*//g')"
if [[ $volume == 0 || "$mute" == "off" ]]; then
    # Show the sound muted notification
    dunstify -a "changeVolume" -u low -i audio-volume-muted -r "$msgId" "Volume muted" 
else
    # Show the volume notification
    dunstify -a "changeVolume" -u low -i audio-volume-high -r "$msgId" \
    "Volume: ${volume}%" "$(getProgressString 10 "<b> </b>" " " $volume)"
fi

# Play the volume changed sound
canberra-gtk-play -i audio-volume-change -d "changeVolume"

```

`getProgressString` needs to be some function assembling the progressbar like string. This script uses [[6]](https://github.com/Fabian-G/dotfiles/blob/master/scripts/bin/getProgressString).

Now simply bind `changeVolume 2dB+ unmute` etc. to some hotkey and you are done. You might also want to make dunst ignore these type of notifications in its history. See [#Modifying](#Modifying).

### Overwrite previous notification

For some notifications (for example sound or brightness), you might want to overwrite the previous notification. You can either use the [#Notification ID](#Notification_ID), or `-h string:x-canonical-private-synchronous:<notification-name>`.

## Troubleshooting

### Dunst fails to start via systemd

When using dunst without a Display Manager, the `DISPLAY` environment variable might not be correctly set.[[7]](https://github.com/dunst-project/dunst/issues/347)

To fix this, add the following to your `.xinitrc`:

```
systemctl --user import-environment DISPLAY

```

### Non-matching font sizes (Emojis much larger than text)

This is caused by [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) not rescaling bitmap fonts. This is usually only noticed with certain emoji fonts (e.g. [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji))

To solve, simply run:

```
# ln -s /etc/fonts/conf.avail/10-scale-bitmap-fonts.conf /etc/fonts/conf.d/

```

and restart Dunst.