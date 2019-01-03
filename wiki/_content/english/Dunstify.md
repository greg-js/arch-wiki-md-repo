Related articles

*   [Dunst](/index.php/Dunst "Dunst")
*   [Desktop Notifications](/index.php/Desktop_Notifications "Desktop Notifications")

Dunstify is an alternative to the [notify-send](/index.php/Desktop_notifications#Usage_in_programming "Desktop notifications") command which is completely compatible to notify-send and can be used alongside it, but offers some more features. Dunstify works only with the [Dunst](/index.php/Dunst "Dunst") notification daemon.

Additionally to the options available in notify-send, dunstify offers some more features like IDs and actions.

## Contents

*   [1 Installation](#Installation)
*   [2 Notification ID](#Notification_ID)
*   [3 Actions](#Actions)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Using dunstify as volume/brightness level indicator](#Using_dunstify_as_volume/brightness_level_indicator)

## Installation

Dunstify is available through the [AUR](/index.php/AUR "AUR"). Simply install the [dunstify](https://aur.archlinux.org/packages/dunstify/) package.

## Notification ID

You can assign an ID to a notification by calling dunstify with the `-r ID` option, where `ID` needs to be an integer. If a notification with that ID already exists it will be replaced with the new one(therefore the long option name `--replace=ID`).

Furthermore you can close a notification by using `dunstify --close=ID`.

## Actions

You can define actions which can be invoked directly from the notification by specifying one or more `--action=action,label` parameters. For instance:

```
dunstify --action="replyAction,reply" "Message received"

```

The user can then access the specified actions via dunsts context menu. The call to dunstify will block until either the notification disappears or an action is selected. In the former case dunstify will return 1 if the notification timed out and 2 if it was closed manually. In the latter case it returns the action which was selected.

## Tips and tricks

### Using dunstify as volume/brightness level indicator

You can use the replace id feature to implement a simple volume or brightness indicator notification like in this picture [[1]](https://i.postimg.cc/j2CDkS1H/screen1712.png).

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

`getProgressString` needs to be some function assembling the progressbar like string. This script uses [[2]](https://github.com/Fabian-G/dotfiles/blob/master/bin/getProgressString).

Now simply bind `changeVolume 2dB+ unmute` etc. to some hotkey and you are done. You might also want to make dunst ignore these type of notifications in its history. See [Dunst#Modifying](/index.php/Dunst#Modifying "Dunst").